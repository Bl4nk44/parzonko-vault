---
limit: 200
mapWithTag: false
icon: user
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
    id: per01
  - name: full_name
    type: Input
    options: {}
    path: ""
    id: per02
  - name: surname
    type: Input
    options: {}
    path: ""
    id: per03
  - name: aliases
    type: Multi
    options:
      sourceType: ValuesList
      valuesList: {}
    path: ""
    id: per04
  - name: gender
    type: Select
    options:
      sourceType: ValuesList
      valuesList:
        "1": M
        "2": K
        "3": unknown
    path: ""
    id: per05
  - name: birth_date
    type: Input
    options: {}
    path: ""
    id: per06
  - name: birth_date_accuracy
    type: Select
    options:
      sourceType: ValuesList
      valuesList:
        "1": day
        "2": month
        "3": year
        "4": unknown
    path: ""
    id: per07
  - name: death_date
    type: Input
    options: {}
    path: ""
    id: per08
  - name: death_date_accuracy
    type: Select
    options:
      sourceType: ValuesList
      valuesList:
        "1": day
        "2": month
        "3": year
        "4": unknown
    path: ""
    id: per09
  - name: occupation
    type: Multi
    options:
      sourceType: ValuesList
      valuesList: {}
    path: ""
    id: per10
  - name: certainty
    type: Select
    options:
      sourceType: ValuesList
      valuesList:
        "1": high
        "2": medium
        "3": low
    path: ""
    id: per11
---

# fileClass: person

Notatki osobowe w `40-People/`. Schemat: [[Schema-and-Conventions]].
