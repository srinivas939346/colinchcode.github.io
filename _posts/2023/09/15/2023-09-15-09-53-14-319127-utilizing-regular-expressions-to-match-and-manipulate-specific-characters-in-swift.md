---
layout: post
title: "Utilizing regular expressions to match and manipulate specific characters in Swift"
description: " "
date: 2023-09-15
tags: [RegularExpressions, Swift]
comments: true
share: true
---

To utilize regular expressions in Swift, we can use the NSRegularExpression class provided by the Foundation framework. Let's look at some common use cases:

## Matching a pattern in a string

To check if a string matches a specific pattern, we can use the `matches` method of `NSRegularExpression`. Here's an example:

```swift
import Foundation

let input = "Hello, world!"
let pattern = "Hello"

do {
    let regex = try NSRegularExpression(pattern: pattern, options: [])
    let matches = regex.matches(in: input, options: [], range: NSRange(location: 0, length: input.utf16.count))
    
    if !matches.isEmpty {
        print("Pattern matched")
    } else {
        print("Pattern not found")
    }
} catch {
    print("Invalid pattern")
}
```

In this example, we create an `NSRegularExpression` object with the specified pattern. We then use `matches` to check if the input string contains a match for the pattern. If matches exist, it will print "Pattern matched"; otherwise, it will print "Pattern not found".

## Extracting specific parts of a string

To extract specific parts of a string based on a pattern, we can use the `firstMatch` method of `NSRegularExpression`. Here's an example:

```swift
import Foundation

let input = "My name is John Doe and I'm 30 years old."
let pattern = "(\\w+) (\\w+) and I'm (\\d+) years old."

do {
    let regex = try NSRegularExpression(pattern: pattern, options: [])
    if let match = regex.firstMatch(in: input, options: [], range: NSRange(location: 0, length: input.utf16.count)) {
        let name = String(input[Range(match.range(at: 1), in: input)!])
        let age = String(input[Range(match.range(at: 3), in: input)!])

        print("Name: \(name)")
        print("Age: \(age)")
    } else {
        print("Pattern not found")
    }
} catch {
    print("Invalid pattern")
}
```

In this example, the pattern `(\\w+) (\\w+) and I'm (\\d+) years old.` represents a string containing a name, followed by "and I'm", and then an age. We use `firstMatch` to find the first occurrence of this pattern in the input string. If a match is found, we extract the name and age using `Range` and `String` conversion.

## Replacing parts of a string

To replace parts of a string based on a pattern, we can use the `stringByReplacingMatches` method of `NSRegularExpression`. Here's an example:

```swift
import Foundation

let input = "Hello, Swift!"
let pattern = "Swift"
let replacement = "World"

do {
    let regex = try NSRegularExpression(pattern: pattern, options: [])
    let updatedString = regex.stringByReplacingMatches(in: input, options: [], range: NSRange(location: 0, length: input.utf16.count), withTemplate: replacement)
    
    print("Updated String: \(updatedString)")
} catch {
    print("Invalid pattern")
}
```

In this example, we replace the word "Swift" with "World" in the input string using `stringByReplacingMatches`. The resulting string, "Hello, World!", will be printed.

Regular expressions provide a flexible and efficient way to work with character patterns in Swift. By understanding and utilizing regular expressions effectively, developers can solve complex text matching and manipulation tasks with ease. #RegularExpressions #Swift