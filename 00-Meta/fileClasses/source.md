---
limit: 200
mapWithTag: false
icon: file-text
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
    id: src01
  - name: source_id
    type: Input
    options: {}
    path: ""
    id: src02
  - name: source_type
    type: Input
    options: {}
    path: ""
    id: src03
  - name: archive
    type: Select
    options:
      sourceType: ValuesList
      valuesList:
        "1": IPN
        "2": rodzinne
        "3": inne
    path: ""
    id: src04
  - name: call_number
    type: Input
    options: {}
    path: ""
    id: src05
  - name: date_document
    type: Input
    options: {}
    path: ""
    id: src06
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
    id: src07
  - name: pages
    type: Number
    options: {}
    path: ""
    id: src08
  - name: reliability
    type: Select
    options:
      sourceType: ValuesList
      valuesList:
        "1": primary
        "2": secondary
    path: ""
    id: src09
  - name: ocr_quality
    type: Input
    options: {}
    path: ""
    id: src10
  - name: main_person
    type: Input
    options: {}
    path: ""
    id: src11
  - name: people_mentioned
    type: Multi
    options:
      sourceType: ValuesList
      valuesList: {}
    path: ""
    id: src12
  - name: places_mentioned
    type: Multi
    options:
      sourceType: ValuesList
      valuesList: {}
    path: ""
    id: src13
---

# fileClass: source

Notatki źródłowe w `20-Sources/`. Schemat: [[Schema-and-Conventions]].
