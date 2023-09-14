---
layout: post
title: "Building a custom UI control in Swift for iOS"
description: " "
date: 2023-09-14
tags: [selector(buttonTapped), SwiftUI, CustomUIControl]
comments: true
share: true
---

In this tutorial, we will explore how to build a custom UI control in Swift for iOS. Custom UI controls can enhance the user experience and add a unique touch to your app. We will create a custom button control that has a circular shape and changes its color when tapped.

## Getting Started

To get started, create a new Swift project in Xcode. Open the ViewController.swift file and add the following code:

```swift
import UIKit

class CustomButton: UIButton {

    override init(frame: CGRect) {
        super.init(frame: frame)
        setupButton()
    }
    
    required init?(coder aDecoder: NSCoder) {
        super.init(coder: aDecoder)
        setupButton()
    }
    
    private func setupButton() {
        layer.cornerRadius = frame.height / 2
        backgroundColor = .blue
        setTitleColor(.white, for: .normal)
        addTarget(self, action: #selector(buttonTapped), for: .touchUpInside)
    }
    
    @objc private func buttonTapped() {
        backgroundColor = .red
    }
}
```

In the code above, we created a new **CustomButton** class that subclasses **UIButton**. We override the `init(frame:)` and `init?(coder:)` methods to ensure our custom button is initialized properly.

The `setupButton()` method is called in both initializers to configure the appearance and behavior of our custom button. We set the corner radius to make the button circular, set the background color to blue, and change the title color to white. We also add a target and action to handle the button tap event.

The `buttonTapped()` method is called when the button is tapped. In this example, we change the background color to red, but you can modify this method to perform any desired action.

## Using the Custom Button

To use our custom button in the app, open the Main.storyboard file and drag a **UIButton** from the Object Library onto the view controller. With the button selected, go to the Identity Inspector tab in the Utilities panel and set the custom class to **CustomButton**.

![Custom Button Class](https://example.com/custom-button-class.png)

Now, run the app on the iOS simulator or a physical device. When you tap the button, you should see it change color to red as defined in the `buttonTapped()` method.

## Conclusion

In this tutorial, we learned how to build a custom UI control in Swift for iOS. We created a custom button control that has a circular shape and changes its color when tapped. You can further customize the control by adding additional properties and methods to suit your app's needs.

Building custom UI controls can provide a unique touch to your app and enhance the user experience. Using Swift and Xcode, you have the flexibility to create custom controls that fit seamlessly into your app's design.

#iOS #SwiftUI #CustomUIControl