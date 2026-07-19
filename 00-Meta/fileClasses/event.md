---
limit: 200
mapWithTag: false
icon: calendar
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
    id: evt01
  - name: title
    type: Input
    options: {}
    path: ""
    id: evt02
  - name: event_type
    type: Input
    options: {}
    path: ""
    id: evt03
  - name: date
    type: Input
    options: {}
    path: ""
    id: evt04
  - name: date_accuracy
    type: Select
    options:
      sourceType: ValuesList
      valuesList:
        "1": day
        "2": month
        "3": year
        "4": unknown
    path: ""
    id: evt05
  - name: place
    type: Input
    options: {}
    path: ""
    id: evt06
  - name: people_involved
    type: Multi
    options:
      sourceType: ValuesList
      valuesList: {}
    path: ""
    id: evt07
  - name: main_person_role
    type: Input
    options: {}
    path: ""
    id: evt08
  - name: key_sources
    type: Multi
    options:
      sourceType: ValuesList
      valuesList: {}
    path: ""
    id: evt09
  - name: certainty
    type: Select
    options:
      sourceType: ValuesList
      valuesList:
        "1": high
        "2": medium
        "3": low
    path: ""
    id: evt10
---

# fileClass: event

Notatki wydarzeń w `30-Events/`. Schemat: [[Schema-and-Conventions]].
