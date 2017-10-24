# CodableFirebase
Use Codable with Firebase

[![Carthage compatible](https://img.shields.io/badge/Carthage-compatible-4BC51D.svg?style=flat)](https://github.com/Carthage/Carthage) 
[![Build Status](https://travis-ci.org/alickbass/SweetRouter.svg?branch=master)](https://travis-ci.org/alickbass/SweetRouter)
[![codecov](https://codecov.io/gh/alickbass/SweetRouter/branch/master/graph/badge.svg)](https://codecov.io/gh/alickbass/SweetRouter)

## Overview

This library helps you to use your custom type that conform to `Codable` protocol with Firebase. Here's an example of model:

```swift
struct Model: Codable {
    let stringExample: String
    let booleanExample: Bool
    let numberExample: Double
    let dateExample: Date
    let arrayExample: [String]
    let nullExample: Int?
    let objectExample: [String: String]
}
```

And this is how you would encode it with [Firebase Firestore](https://firebase.google.com/products/firestore/):

```
import Firebase

let model: Model // here you will create an instance of Model
do {
    let docData = try FirestoreEncoder().encode(model)
    Firestore.firestore().collection("data").document("one").setData(docData) { err in
        if let err = err {
            print("Error writing document: \(err)")
        } else {
            print("Document successfully written!")
        }
    }
}
```