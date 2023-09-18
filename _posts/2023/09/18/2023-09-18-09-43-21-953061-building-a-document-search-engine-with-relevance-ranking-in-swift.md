---
layout: post
title: "Building a document search engine with relevance ranking in Swift"
description: " "
date: 2023-09-18
tags: [searchengine, Swift]
comments: true
share: true
---

In this tutorial, we will walk you through building a document search engine with relevance ranking using Swift. Search engines are essential applications that allow users to find specific information within a vast collection of documents. Relevance ranking helps determine the most relevant results based on the user's query.

## Prerequisites
Before we begin, make sure you have the following:

- Xcode installed on your machine
- Basic knowledge of Swift programming language

## Step 1: Create Document Data Structure
The first step in building our search engine is to create a data structure to represent the documents. Each document will contain information like a **title** and **content**. Let's create a `Document` struct in Swift:

```swift
struct Document {
    let title: String
    let content: String
}
```

## Step 2: Index the Documents
Next, we need to index the documents to make them searchable. Indexing involves creating an **inverted index** which maps each word in the documents to the documents that contain it.

```swift
class DocumentSearchEngine {
    private var invertedIndex: [String: [Document]] = [:]

    func indexDocument(_ document: Document) {
        let words = document.content.components(separatedBy: CharacterSet.whitespacesAndNewlines)
        
        for word in words {
            invertedIndex[word, default: []].append(document)
        }
    }
    
    func search(_ query: String) -> [Document] {
        let queryWords = query.components(separatedBy: CharacterSet.whitespacesAndNewlines)
        var searchResults: Set<Document> = []
        
        for word in queryWords {
            if let documents = invertedIndex[word] {
                searchResults.formUnion(documents)
            }
        }
        
        return Array(searchResults)
    }
}
```

In the above code, we create a `DocumentSearchEngine` class with an `invertedIndex` property. The `indexDocument` method takes a `Document` object, splits its content into words, and updates the inverted index accordingly. The `search` method takes a query, splits it into words, and retrieves the relevant documents from the inverted index.

## Step 3: Relevance Ranking
To implement relevance ranking, we will use a simple scoring algorithm based on word frequency. Each document's score will be calculated by counting the frequency of query words in the document's content. Let's enhance our `search` method to include relevance ranking:

```swift
// ...

struct SearchResult {
    let document: Document
    let relevanceScore: Int
}

// ...

func search(_ query: String) -> [SearchResult] {
    let queryWords = query.components(separatedBy: CharacterSet.whitespacesAndNewlines)
    var searchResults: [SearchResult] = []
    
    for word in queryWords {
        if let documents = invertedIndex[word] {
            for document in documents {
                let relevanceScore = document.content.components(separatedBy: word).count - 1
                
                if let existingResult = searchResults.first(where: { $0.document == document }) {
                    existingResult.relevanceScore += relevanceScore
                } else {
                    searchResults.append(SearchResult(document: document, relevanceScore: relevanceScore))
                }
            }
        }
    }
    
    return searchResults.sorted { $0.relevanceScore > $1.relevanceScore }
}
```

In the revised code, we introduce a new `SearchResult` struct to store both the document and its relevance score. We iterate through the query words, calculate the relevance score based on word frequency, and update the existing result if it exists, or add a new result otherwise. Finally, we sort the results based on relevance score in descending order.

## Conclusion
Congratulations! You have successfully built a document search engine with **relevance ranking** in Swift. This search engine can be further enhanced with more advanced techniques, such as stemming, stop-word removal, and TF-IDF scoring. Feel free to explore and improve upon the code to suit your specific needs.

#searchengine #Swift