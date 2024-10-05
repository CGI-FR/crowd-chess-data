# Crowdchess Dataviz

## Win/Draw/Loss evaluation

[Link](https://vega.github.io/editor/#/url/vega-lite/N4IgJAzgxgFgpgWwIYgFwhgF0wBwqgegIDc4BzJAOjIEtMYBXAI0poHsDp5kTykBaADZ04JAKyUAVhDYA7EABoQAEySYUqUAwBOgtBmx5CBbUgDu1OoyYMIcbVDmY4szJUcICAYQDiASX4AMQAlAihtNjNlflg4CAh+VXUTOAAzCAJ4JGUM5BpZAgAmAAZCgBZigE5CgHZ+TB1ZCHcIYhAAXyUzGmV6NAAOYuKleBoyLDQANiGlTFMm1LZtBDQAbVBFwWU1kG75JWVTM0UQQTZ4kABdJSQIHeCAS4gGQXVME4AFCKYkJhphTAPK6dUBQJCCKAvNRwfT5ZRwAAebFSAApVgByPbohQAAnRh3M2LxZ3i6OuOKSDAQlEez1eagAlCdbvolvDtB1riBkNoANb6JDaOAoJQuRzKfJkNCgBHSkCpGhwLb6FzKAD6yLVDW0+xAmAAnjgYehnAgcEtwSdMHRBMaQAAJOA6GGdED6uUKpXbdBfNg-P4AoGzQ12gCODCQrjoahopBOEHUUH56FkS2QwgAXjDZja7b7-f86A8cZCEC8HnAcSiAKRMm4Imh3TTytNqfTVjquxxnDnNz3K9C0l5vK0h-SphD5S05zC2-RD+nvJTQcHG0DKNh5eSoVa7fInAnHJQku5c+ZkY27gDEqTEt+UUBOV8GL+KT6GH7fl3arrZ9g9ioDiAf4csGRqstoEqyJaP7tEAA)

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
