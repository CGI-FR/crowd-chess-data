# Crowdchess Dataviz

## Win/Draw/Loss evaluation

Show evolution of win/draw/loss evaluation over time (white point of view), can be filtered in between turns to show a single chessgame.

### DevFest 2024 - Day 1

![devfest-2024-10-17-partie](https://github.com/user-attachments/assets/2a681329-532e-423b-bc25-6fb81ffed3bb)

### DevFest 2024 - Day 2

![devfest-2024-10-18-partie](https://github.com/user-attachments/assets/2f05916d-095c-47a7-9e07-19d2e0168623)

### Source code

[Link](https://vega.github.io/editor/#/url/vega-lite/N4IgJAzgxgFgpgWwIYgFwhgF0wBwqgegIDc4BzJAOjIEtMYBXAI0poHsDp5kTykBaADZ04JAKyUAVhDYA7EABoQAEySYUqUAwBOgtBmx5CBbUgDu1OoyYMIcbVDmY4szJUcICAYQDiASX4AMQAlAihtNjNlflg4CAh+VXUTOAAzCAJ4JGUM5BpZAgAmAAZCgBZigE5CgHZ+TB1ZCHcIYhAAXyUzGmV6NAAOYuKleBoyLDQANiGlTFMm1LZtBDQAbVBUmkFnbTQNmjhBZX0exRBtqcKARmL2zv3t+z2QTcPj9FOlMkwpq7FCu4KDZsI5rEDdeRKZSmMxnQRseIgAC6SiQEDBwQAlxAGNs1GcAAoRJhIJhbOiY5H3EBQJCCKC4tRwE6yZRwAAebFSAApVgByCF8hQAAj50PMQtF8PifJRwqSDAQlCxOLxmAAlGc0folmzdu0USBkNoANb6JDaOAoJQuRzKfJkZ7s56vUHoFzKAD6XM9DW0kJAmAAnjhmehnAgcEs6WdMHRBGGQAAJOA6ZmdEBBl0HN0gIlsElk4SYSmzEOJgCODCQrjoahopDOEHUUDN6FkS2QwgAXszZvHE-nC+SS8KGQhcZi4MLuQBSTWo9k0dGaF6d-HoWcdDOOeG7Veu94gFW49Q-Muh-QdhD5GP9zAJ-QntVN2mP1fKNh5eSoVbg-JnOKsJKNK6KGvMZBhn+ADEqRiHByhQGc0GDKhxTIUMmHoUigIgLqTwHjmR74bsF6Jrqt56Hc7RAA)

```json
{
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "data": {
    "url": "https://raw.githubusercontent.com/CGI-FR/crowd-chess-data/refs/heads/main/20240927-turns.csv"
  },
  "width": 800,
  "height": 600,
  "transform": [
    {"filter": {"field": "id", "lt": 6210}},
    {"filter": {"field": "id", "gt": 6152}},
    {"fold": ["win", "draw", "loss"], "as": ["Résultat", "Probabilité"]},
    {"calculate": "indexof(['win', 'draw', 'loss'], datum.Résultat)", "as": "order"}
  ],
  "mark": "area",
  "encoding": {
    "x": {"field": "end_of_turn", "type": "temporal", "title": "Heure"},
    "y": {
      "field": "Probabilité",
      "type": "quantitative",
      "stack": "normalize",
      "title": "Probabilité cumulée (%)",
      "axis": {"format": "%"}
    },
    "color": {
      "field": "Résultat",
      "type": "nominal",
      "title": "Résultat",
      "scale": {
        "domain": ["win", "draw", "loss"],
        "range": ["#f5f5dc", "#808080", "#000000"]
      }
    },
    "order": {"field": "order", "type": "ordinal"}
  }
}
```

## Active players over time

### DevFest 2024 - Day 1

![devfest-2024-10-17-joueurs](https://github.com/user-attachments/assets/118b38e9-d3e1-4899-a9b6-2a002c0e87c9)

### DevFest 2024 - Day 2

![devfest-2024-10-18-joueurs](https://github.com/user-attachments/assets/8deec2b1-6c8c-4ede-8511-2093ef9a0d0e)

### Source code

[Full month](https://vega.github.io/editor/#/url/vega-lite/N4IgJAzgxgFgpgWwIYgFwhgF0wBwqgegIDc4BzJAOjIEtMYBXAI0poHsDp5kTykBaADZ04JAKyUAVhDYA7EABoQAEySYUqUAwBOgtBmx5CBbUgDu1OoyYMIcbVDmY4szJUcICAYQDiASX4AMQAlAihtNjNlflg4CAh+VXUTOAAzCAJ4JGUM5BpZAgAmAAZCgBZigE5+YjZnCHcIYhAAXyViR1koNTQAbVAzGmV6NAAOYuKleBoyLDQANgmlHCRTBAg+0FkkBDh9STYdRRA7QTgoTDRQTABPHD30HDZ8y6UXR2V8sg3UXpAADxAAF0Wi0gUpkNoANb6JirY7vNifWRkK4AtGYGi7ACqsjo+iSeyUqRocEEyn0+Qg6lcx1u930zgQT1MeiUmMwZ30AClDtpjnDZMoAApsCB0djyVDFNogG5opBkMjaPjOAk0an5C7HElkimPQRIG72AD6eDgDGUbDpdweIAAjgwkK46GoaKQ6XQuegAHJsBBMFUAAmUcCDBwYFu0G1ljkEbH5mhAiuVqrtn01XVeIF15P0OENxu0ZrslutSjOZBc+uuXrtfoDwdD4cOUZjoLaAyGI1Q40mGDgMzmqEW-cwplkEFSCYQmxzNEEzkToBWa32fNaYIhqxh6Dh-LeXSRXzRgKTmJxeMu6BgfI2xNJefQVJp2fpdqZLKQbJAHO9IAACSjIkQEFEUxQlOQ0H7JB-g1NFiG-SMfl6SYAEYFEKBQAGYFDKBQxAUeYFAAdgUUYFEqBQ0PQjC0KwtDcLQ-C0MItDiLQsi0IotCqJKTCMMKLDCmwkFZXlJMUxVCg1XQDNMSzHVH31EACyNU1zTLG0GXQR1nQ5N0PXZOt9AbQMw2bCM21aJQ4wTBUlWktR0w1BTtQfPV80LDTSytY5K2rDETN9f1zJDMMrJ0GMlGgb8HlALhEDtFUck3UEQSAA)

[Single day](https://vega.github.io/editor/#/url/vega-lite/N4IgJAzgxgFgpgWwIYgFwhgF0wBwqgegIDc4BzJAOjIEtMYBXAI0poHsDp5kTykBaADZ04JAKyUAVhDYA7EABoQAEySYUqUAwBOgtBmx5CBbUgDu1OoyYMIcbVDmY4szJUcICAYQDiASX4AMQAlAihtNjNlflg4CAh+VXUTOAAzCAJ4JGUM5BpZAgAmAAZCgBZigE5CgHZ+YjZnCHcIYhAAXyUzGmV6NAAOYuKleBoyLDQANiGlZG0Aa30mJG1FEBdHZXyyNFAAD12QTBoEOABVWTp9GDYdCDXUmjhBZX18iHVXNcwATxw4fTOBA4NimPRKY6YQQA9AACTgOgBSmWsmUAAU2BA6Ox5KhhiAkHsaPdNCBiEhBAw4mgANrDACMCkKCgAzAoygoxApJgoagp+gpKgp6QzGfTmfS2fSOfSufSefS+fSBfShSUmYzCszCiyALrtTogH6HJBkMjaPjOfRbD75KCYB5PF76HCCJA-ewAfTwCOUbG+fxhIAAjgwkK46GoaKRvnRofoAHJsBBMC0AAmUcDTkluCO090NjkEoJNZotFCt6Btx1k9sdz1e6Fd7q9PoYfrW0LILkboEh8fQSZT6cz2dzdw6SmgFJhoC4iCDFpyHQN7SAA)

```json
{
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "data": {
    "url": "https://raw.githubusercontent.com/CGI-FR/crowd-chess-data/refs/heads/main/202409-votes.csv"
  },
  "vconcat": [
  {
    "width": 800,
    "height": 600,
    "params": [{"name": "jour", "select": {"type": "point", "encodings": ["x"]}}],
    "mark": "bar",
    "encoding": {
      "x": {
        "timeUnit": "date",
        "field": "instant",
        "type": "temporal",
        "title": "Jour",
        "bandPosition": 0
      },
      "y": {
        "aggregate": "distinct",
        "field": "player_pseudo",
        "type": "quantitative",
        "title": "Nombre de joueurs"
      },
      "color": {
        "aggregate": "distinct",
        "field": "player_pseudo",
        "legend": {
          "title": "Nombre de joueurs"
        }
      }
    }
  },
  {
    "width": 800,
    "height": 600,
    "transform": [{"filter": {"param": "jour"}}],
    "mark": "bar",
    "encoding": {
      "x": {
        "timeUnit": "hours",
        "field": "instant",
        "type": "temporal",
        "title": "Heure",
        "bandPosition": 0,
        "axis": {
          "values": [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23]
        }
      },
      "y": {
        "aggregate": "distinct",
        "field": "player_pseudo",
        "type": "quantitative",
        "title": "Nombre de joueurs"
      },
      "color": {
        "aggregate": "distinct",
        "field": "player_pseudo",
        "legend": {
          "title": "Nombre de joueurs"
        },
        "scale": {
          "scheme": "reds"
        }
      }
    }
  }]
}
```

## Average accuracy by players

Compute average accuracy of players with at least 5 active votes (an active vote is the last vote submitted on each turn).

### DevFest 2024 - Day 2

![devfest-2024-10-18-accuracy](https://github.com/user-attachments/assets/049156ee-0817-4907-afa4-98f44264903f)

### Source code

```json
{
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "data": {
    "url": "https://raw.githubusercontent.com/CGI-FR/crowd-chess-data/refs/heads/main/20241018-votes-effective.csv"
  },
  "width": 800,
  "height": 600,
  "transform": [
    {
      "groupby": ["player_pseudo"],
      "aggregate": [
        {"op": "count", "as": "nb_moves"},
        {"op": "mean", "field": "accuracy", "as": "avg_accuracy"}
      ]
    },
    {
      "filter": "datum.nb_moves >= 5"
    }
  ],
  "mark": "bar",
  "encoding": {
    "x": {
      "field": "avg_accuracy",
      "type": "quantitative",
      "title": "Précision moyenne"
    },
    "y": {
      "field": "player_pseudo",
      "type": "nominal",
      "sort": "-x",
      "title": "Joueur"
    }
  },
  "config": {
    "axis": {
      "labelFontSize": 10,
      "titleFontSize": 14
    }
  }
}
```

## Average points by turns

### DevFest 2024 - Day 2

![devfest-2024-10-18-points-filtered](https://github.com/user-attachments/assets/cca20e31-21b9-4ca7-89dd-2c000c28adfb)

### Source code

```json
{
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "data": {
    "url": "https://raw.githubusercontent.com/CGI-FR/crowd-chess-data/refs/heads/main/20241018-votes-effective.csv"
  },
  "width": 800,
  "height": 600,
  "transform": [
    {
      "filter": "datum.turn_id < 10552"
    },
    {
      "groupby": ["player_pseudo"],
      "aggregate": [
        {"op": "count", "as": "nb_moves"},
        {"op": "mean", "field": "accuracy", "as": "avg_accuracy"},
        {"op": "mean", "field": "points", "as": "avg_points"}
      ]
    },
    {
      "filter": "datum.nb_moves >= 5"
    }
  ],
  "mark": {
    "type": "bar",
    "color": "#b41f1f"
  },
  "encoding": {
    "x": {
      "field": "avg_points",
      "type": "quantitative",
      "title": "Quantité moyenne de points engrangés par tours"
    },
    "y": {
      "field": "player_pseudo",
      "type": "nominal",
      "sort": "-x",
      "title": "Joueur"
    },
    "color": {
      "field": "nb_moves", 
      "type": "quantitative",
      "scale": {"scheme": "reds"},
      "title": "Nombre de tours joués"
    }
  },
  "config": {
    "axis": {
      "labelFontSize": 10,
      "titleFontSize": 14
    }
  }
}
```

