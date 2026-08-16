---
tags:
  - watchlist
  - anime
  - sheet-plus
excel-pro-plugin: parsed
---

# Anime Watch List

```sheet
{
  "id": "anime-watch-list",
  "name": "Anime Watch List",
  "appVersion": "0.25.0",
  "locale": "enUS",
  "sheetOrder": [
    "anime"
  ],
  "styles": {
    "header": {
      "bl": 1,
      "bg": {
        "rgb": "#E8F0FE"
      },
      "cl": {
        "rgb": "#1F1F1F"
      }
    }
  },
  "sheets": {
    "anime": {
      "id": "anime",
      "name": "Anime",
      "tabColor": "",
      "hidden": 0,
      "rowCount": 100,
      "columnCount": 5,
      "zoomRatio": 1,
      "scrollTop": 0,
      "scrollLeft": 0,
      "defaultColumnWidth": 160,
      "defaultRowHeight": 28,
      "showGridlines": 1,
      "rightToLeft": 0,
      "freeze": {
        "xSplit": 0,
        "ySplit": 1,
        "startRow": 1,
        "startColumn": 0
      },
      "rowHeader": {
        "width": 46,
        "hidden": 0
      },
      "columnHeader": {
        "height": 20,
        "hidden": 0
      },
      "mergeData": [],
      "cellData": {
        "0": {
          "0": {
            "v": "Anime",
            "s": "header"
          },
          "1": {
            "v": "Status",
            "s": "header"
          },
          "2": {
            "v": "Rating",
            "s": "header"
          },
          "3": {
            "v": "Finished",
            "s": "header"
          },
          "4": {
            "v": "Notes",
            "s": "header"
          }
        },
        "1": {
          "0": {
            "v": "Attack on Titan"
          },
          "1": {
            "v": "Awaiting first episode"
          }
        },
        "2": {
          "0": {
            "v": "Chainsaw Man"
          },
          "1": {
            "v": "Awaiting first episode"
          }
        },
        "3": {
          "0": {
            "v": "My Hero Academia"
          },
          "1": {
            "v": "Awaiting first episode"
          }
        },
        "4": {
          "0": {
            "v": "Tokyo Revengers"
          },
          "1": {
            "v": "Awaiting first episode"
          }
        },
        "5": {
          "0": {
            "v": "Vinland Saga"
          },
          "1": {
            "v": "Awaiting first episode"
          }
        },
        "6": {
          "0": {
            "v": "Wind Breaker"
          },
          "1": {
            "v": "Awaiting first episode"
          }
        },
        "7": {
          "0": {
            "v": "Frieren season 2"
          },
          "1": {
            "v": "Credits rolled"
          }
        }
      },
      "rowData": {},
      "columnData": {
        "0": {
          "w": 220
        },
        "1": {
          "w": 190
        },
        "2": {
          "w": 90
        },
        "3": {
          "w": 120
        },
        "4": {
          "w": 260
        }
      }
    }
  },
  "resources": []
}
```

## Status Dropdown Setup

Select the Status cells, starting from `B2`, then use Sheet Plus data validation to make a dropdown with:

- `Awaiting first episode`
- `Somewhere in the arc`
- `Credits rolled`

Keep this order when sorting the sheet:

1. `Awaiting first episode`
2. `Somewhere in the arc`
3. `Credits rolled`
