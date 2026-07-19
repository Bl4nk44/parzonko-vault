---
limit: 200
mapWithTag: false
icon: map-pin
tagNames: []
excludes: []
extends: null
savedViews: []
favoriteView: null
fieldsOrder: []
version: "2.0"
fields:
  - name: uid
    type: Input
    options: {}
    path: ""
    id: plc01
  - name: name
    type: Input
    options: {}
    path: ""
    id: plc02
  - name: place_type
    type: Input
    options: {}
    path: ""
    id: plc03
  - name: region
    type: Input
    options: {}
    path: ""
    id: plc04
  - name: coordinates
    type: Input
    options: {}
    path: ""
    id: plc05
  - name: key_sources
    type: Multi
    options:
      sourceType: ValuesList
      valuesList: {}
    path: ""
    id: plc06
  - name: certainty
    type: Select
    options:
      sourceType: ValuesList
      valuesList:
        "1": high
        "2": medium
        "3": low
    path: ""
    id: plc07
---

# fileClass: place

Notatki miejsc w `50-Places/`. Schemat: [[Schema-and-Conventions]]. Pole `coordinates: [lat, lon]` używane przez plugin Map View (`frontMatterKey` ustawiony na `coordinates`).
