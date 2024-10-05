# Crowdchess Dataviz

## Win/Draw/Loss evaluation

Show evolution of win/draw/loss evaluation over time, can be filtered in between turns to show a single chessgame.

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
