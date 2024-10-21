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

## Average player accuracy by turns

Compute average accuracy of players with at least 5 active votes (an active vote is the last vote submitted on each turn).

### DevFest 2024 - Day 1

![devfest-2024-10-17-accuracy-filtered](https://github.com/user-attachments/assets/8b17941e-f9d3-4996-af1b-4f274fc5a82e)

### DevFest 2024 - Day 2

![devfest-2024-10-18-accuracy-filtered](https://github.com/user-attachments/assets/940a82c6-52b0-482c-9653-9b728f542f41)

### Source code

[Link](https://vega.github.io/editor/#/url/vega-lite/N4IgJAzgxgFgpgWwIYgFwhgF0wBwqgegIDc4BzJAOjIEtMYBXAI0poHsDp5kTykBaADZ04JAKyUAVhDYA7EABoQAEySYUqUAwBOgtBmx5CBbUgDu1OoyYMIcbVDmY4szJUcICAYQDiASX4AMQAlAihtNjNlflg4CAh+VXUTOAAzCAJ4JGUM5BpZAgAmAAZCgBYARmKKgHZ+YjZnCHcIYhAAXyUzGmV6NAAOYuKleBoyLDQANiGlTFNZCFS2bQQ0AG1QbtllSPXQNhx9CLMAfVkGBCZ7RRAkCCPIs4ur7Q6AXSUyCIYcJgBPdYgTA6WQnHo3HCCJB-ewnPBwBg7EAfEAybSYPYgVI0OCCZT6fIQdSuG7LZTXdDk6AuZT5MjvTqgbGCZyvSlqC6UY5PS72AAEAF4BXyKh0FEyaCyKSoOQhKMDtKCenyADzCqoAZjKAE4xaAvmwfv9AZDobD4Yi2MilEgyF8+M5MQd9I4GCSbfd0LImCcEGxSPdGSBnegEHAkPIlNjcfj0EgoFAdPGAR79EhiGQTvHE6YoACgyGQGGIzdo3j9Dg2PlMPdU3GM3Cq65A28g8zWfokpzvb7-XE+QA+YVid5KZDaADWaFAmD+ODg+iYSFeSkcgmW+gAxExKqkKqkxSAXI5abJ6ZoQAAPadYnHl+uZ7NJvM3Wfz-QARwYEcwdDUNFIV86EEBd0AABW0ABLqAaAgdhZD5P0YVkWQ4D5HBlz5TBDW0QMlABC8y1jEBTRhbQ4TsS1XznUCQFkNgEHyJA9CUNEMXQfhr1mYDaIAKUNBFXk6EA1w3Qi72Ins-QDaj33QL8fz-X9ANYqBmNA0AuEQWimEEBg4kPX9MBA-QADkGKYbQ0PJLCcIgPlJENSDA2ExxZGxc9QCQS9YJvKErkEQInAAZRoAAvUCqm44y4CC1xQoitAKjKdpUqAA)

```json
{
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "data": {
    "url": "https://raw.githubusercontent.com/CGI-FR/crowd-chess-data/refs/heads/main/20241017-votes.csv"
  },
  "width": 800,
  "height": 600,
  "transform": [
    {
      "window": [{"op": "row_number", "as": "row_number"}],
      "groupby": ["turn_id", "player_pseudo"],
      "sort": [{"field": "instant", "order": "descending"}]
    },
    {"filter": "datum.row_number == 1"},
    {"filter": "datum.turn_id <= 10349"},
    {
      "groupby": ["player_pseudo"],
      "aggregate": [
        {"op": "count", "as": "nb_moves"},
        {"op": "mean", "field": "accuracy", "as": "avg_accuracy"},
        {"op": "mean", "field": "points", "as": "avg_points"}
      ]
    },
    {"filter": "datum.nb_moves >= 5"}
  ],
  "mark": {"type": "bar", "color": "#b41f1f"},
  "encoding": {
    "x": {
      "field": "avg_accuracy",
      "type": "quantitative",
      "title": "Précision moyenne par tours"
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
      "scale": {"scheme": "blues"},
      "title": "Nombre de tours joués"
    }
  },
  "config": {"axis": {"labelFontSize": 10, "titleFontSize": 14}}
}
```

## Average points by turns

### DevFest 2024 - Day 1

![devfest-2024-10-17-points-filtered](https://github.com/user-attachments/assets/9beb5f1c-9eec-4427-a1f6-971294e3b74d)

### DevFest 2024 - Day 2

![devfest-2024-10-18-points-filtered](https://github.com/user-attachments/assets/cca20e31-21b9-4ca7-89dd-2c000c28adfb)

### Source code

[Link](https://vega.github.io/editor/#/url/vega-lite/N4IgJAzgxgFgpgWwIYgFwhgF0wBwqgegIDc4BzJAOjIEtMYBXAI0poHsDp5kTykBaADZ04JAKyUAVhDYA7EABoQAEySYUqUAwBOgtBmx5CBbUgDu1OoyYMIcbVDmY4szJUcICAYQDiASX4AMQAlAihtNjNlflg4CAh+VXUTOAAzCAJ4JGUM5BpZAgAmAAZCgBYARmKKgA5+YjZnCHcIYhAAXyUzGmV6NBri4qV4GjIsNAA2QaVMU1kIVLZtBDQAbVBu2WVItdA2HH0IswB9WQYEJntFECQIQ8jT88vtDoBdJTIIhhwmAE81kCYHSyY49a44QRIX72Y54OAMbYgd4gGTaTC7ECpGhwQTKfT5CDqVzXJbKK7oMnQFzKfJkN6dUBYwTOF4UtTnShHR4XewAAgAvPzeRUOgpGTRmeSVOyEJQgdoQT1eQAeYXFMRiQqi0CfNjfP4AiFQmFwhFsJFKJBkT58ZwY-b6RwMYmWu7oWRMY4INikO4MkAO9AIOBIeRKLE4vHoJBQKA6GP-V36JDEMjHGNx0xQf7+wMgYOh64R3H6HBsfKYO5J6Op2Hl1x+17+pks-RJDker0+uK8gB8QrEbyUyG0AGs0KBML8cHB9EwkC8lI5BEt9ABiJiVVIVVKikAuRw02R0zQgAAeE8x2JLNbTZYrVcB09n6AAjgxQ5g6GoaKRrl-MEEF8QAARQ-Vw6AAS95b1oVkWQ4F5MleXvBteRcT5QzISCIBQhdeUwPVtD9JR-lPYsoxAI1oW0WE7DNf9n30WQ2AQfIkD0JRUXRdB+AvGY6CA-QACk9XhF5OhAZdV3I69KM7b1fUYmd9HfT9vy-P8uKgDiX1ALhEGA7Q4ByPcAKE9AADlWKYYykMQwidFwyQ9RwjpJMcWQsRPUAkDPGg3VASFLkEQInAAZRoAAvF8qgEwC4DC1xIpitAKjKdpMqAA)

```json
{
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "data": {
    "url": "https://raw.githubusercontent.com/CGI-FR/crowd-chess-data/refs/heads/main/20241018-votes.csv"
  },
  "width": 800,
  "height": 600,
  "transform": [
    {
      "window": [
        {
          "op": "row_number",
          "as": "row_number"
        }
      ],
      "groupby": ["turn_id", "player_pseudo"],
      "sort": [
        {"field": "instant", "order": "descending"}
      ]
    },
    {
      "filter": "datum.row_number == 1"
    },
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

## Average rank of effective vote

Show the average rank of the effective vote counted for each player (e.g. your rank if 5 if 4 players played the same move as you before you). Lower value for average rank is better since you get more points.

### DevFest 2024 - Day 1

![devfest-2024-10-17-rank-filtered](https://github.com/user-attachments/assets/a8471bf5-f75f-472e-9860-659f85369f45)

### DevFest 2024 - Day 2

![devfest-2024-10-18-rank-filtered](https://github.com/user-attachments/assets/1a9d2910-492a-4571-87c5-f528efbf09f8)

### Source code

```json
{
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "data": {
    "url": "https://raw.githubusercontent.com/CGI-FR/crowd-chess-data/refs/heads/main/20241018-votes.csv"
  },
  "width": 800,
  "height": 600,
  "transform": [
    {
      "window": [{"op": "row_number", "as": "row_number"}],
      "groupby": ["turn_id", "player_pseudo"],
      "sort": [{"field": "instant", "order": "descending"}]
    },
    {"filter": "datum.row_number == 1"},
    {"filter": "datum.turn_id <= 10551"},
    {
      "window": [{"op": "rank", "as": "rank"}],
      "groupby": ["turn_id", "move"],
      "sort": [{"field": "instant", "order": "ascending"}]
    },
    {
      "groupby": ["player_pseudo"],
      "aggregate": [
        {"op": "count", "as": "nb_moves"},
        {"op": "mean", "field": "accuracy", "as": "avg_accuracy"},
        {"op": "mean", "field": "points", "as": "avg_points"},
        {"op": "mean", "field": "rank", "as": "med_rank"}
      ]
    },
    {"filter": "datum.nb_moves >= 5"}
  ],
  "mark": "bar",
  "encoding": {
    "x": {
      "field": "med_rank",
      "type": "quantitative",
      "title": "Rang médian"
    },
    "y": {
      "field": "player_pseudo",
      "type": "nominal",
      "sort": "x",
      "title": "Joueur"
    },
    "color": {
      "field": "nb_moves",
      "type": "quantitative",
      "scale": {"scheme": "greens"},
      "title": "Nombre de tours joués"
    }
  },
  "config": {"axis": {"labelFontSize": 10, "titleFontSize": 14}}
}
```
