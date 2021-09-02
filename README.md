# gw2-api-event-timers
Guild Wars 2 timed events API

Guild Wars 2 additional JSON API to have full timed events list with possible rewards.
The events.json file contains an array of JSON objects structured in a similar way to the one used by the wiki event timers (https://wiki.guildwars2.com/wiki/Event_timers), for example:

```
{
    "id": section order in the specified category (usable as numerical ID),
    "category": "Category name, can be repeated in multiple sections - e.g. Core Tyria",
    "name": "Section Name - e.g. World Bosses",
    "active": true usually (false for inactive special events),
    "link": "wiki search keywords",
    "segments": [
      {
        "id": event order in the specified section (usable as numerical ID),
        "name": "Event Name",
        "link": "wiki search keywords",
        "chatlink": "chatlink - e.g. [&BKoBAAA=]",
        "bg": [255,255,255],
        "icon": "related achievements icon URL",
        "v1_event_id": "event ID (if any) to resolve against https://api.guildwars2.com/v1/event_details.json?event_id=...",
        "lfg": minutes needed to find a decent group to complete the achievement,
        "rewards": {
          "items": array of guaranteed item IDs from this event,
          "random_items": array of possible valuable item IDs that can drop randomly,
          "coins": guaranteed bronze coins count - e.g. 2G => 20000,
          "achievements": array of related achievement IDs,
          "items_for_achievements": array of droppable related collection items - e.g. [{"a": 2524, "i": 75371}, ...]
        }
      },
      ...
    ],
    "sequences": { <= actual timer information from last GMT midnight
      "partial": [ <= events in section that started before GMT midnight and have yet to finish (or events with irregular intervals)
        {
          "r": section ID (ordering number),
          "d": minutes duration
        },
        ...
      ],
      "pattern": [ <= events to be repeated until next GMT midnight
        {
          "r": section ID (ordering number),
          "d": minutes duration
        },
        ...
      ]
    }
  }
```
