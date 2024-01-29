## Looker Data Explorer - Qwik Start [GSP718]

### Copy and Paste on FAA Model Inside Flights Model

```
# Place in `faa` model
explore: +airports {
    query: quicklab_task_1 {
      measures: [average_elevation]
    }
  }



# Place in `faa` model
explore: +airports {
    query: quicklab_task_2 {
      dimensions: [facility_type]
      measures: [average_elevation, count]
    }
  }
```
