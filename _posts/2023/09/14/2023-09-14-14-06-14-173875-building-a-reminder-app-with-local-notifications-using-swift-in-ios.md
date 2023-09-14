---
layout: post
title: "Building a reminder app with local notifications using Swift in iOS"
description: " "
date: 2023-09-14
tags: [iOSDevelopment, SwiftProgramming]
comments: true
share: true
---

In this blog post, we will walk through the process of building a reminder app using Swift in iOS. Our app will allow users to set reminders and receive local notifications at the specified time. Let's get started!

## Prerequisites

- Xcode installed on your Mac
- Basic understanding of Swift programming language and iOS development

## Step 1: Project Setup

1. Open Xcode and create a new iOS project.
2. Choose the "Single View App" template and provide a name for your project.
3. Select Swift as the language and make sure "Storyboard" is selected for user interface.

## Step 2: User Interface

1. Open the Main.storyboard file.
2. Drag and drop a `UIDatePicker` onto the view controller.
3. Add a `UIButton` to set the reminder and a `UILabel` to display the reminder message.
4. Connect the necessary outlets and actions between the UI components and the view controller.

## Step 3: Local Notifications

1. In the project navigator, right-click on the project name and select "New File".
2. Choose the "Swift File" template and provide a name for the file, e.g., `NotificationManager`.
3. Define a static method `requestAuthorization` in the `NotificationManager` class to request permission for local notifications. This method should be called in the `AppDelegate`'s `didFinishLaunchingWithOptions` method.
4. Implement a method in the `NotificationManager` class to schedule a local notification at a specified time, using the `UNUserNotificationCenter` class.

```swift
import UserNotifications

class NotificationManager {
    static func requestAuthorization() {
        UNUserNotificationCenter.current().requestAuthorization(options: [.alert, .sound, .badge]) { (granted, error) in
            // Handle the authorization response
        }
    }
    
    static func scheduleNotification(at date: Date, withTitle title: String, andMessage message: String) {
        let content = UNMutableNotificationContent()
        content.title = title
        content.body = message
        
        let calendar = Calendar.current
        let components = calendar.dateComponents([.year, .month, .day, .hour, .minute], from: date)
        let trigger = UNCalendarNotificationTrigger(dateMatching: components, repeats: false)
        
        let request = UNNotificationRequest(identifier: "Reminder", content: content, trigger: trigger)
        UNUserNotificationCenter.current().add(request) { (error) in
            // Handle the notification request response
        }
    }
}
```

## Step 4: Setting the Reminder

1. In the view controller, implement an action method for the `UIButton` that is triggered when the user taps on it.
2. Inside the action method, retrieve the selected date from the `UIDatePicker` and present an alert controller to enter the reminder message.
3. Call the `scheduleNotification` method from the `NotificationManager` class to schedule the local notification.

```swift
@IBAction func setReminderTapped(_ sender: UIButton) {
    let selectedDate = datePicker.date
    
    let alertController = UIAlertController(title: "Set Reminder", message: "Enter your reminder message", preferredStyle: .alert)
    alertController.addTextField { (textField) in
        textField.placeholder = "Reminder message"
    }
    
    let saveAction = UIAlertAction(title: "Save", style: .default) { (_) in
        if let message = alertController.textFields?.first?.text {
            NotificationManager.scheduleNotification(at: selectedDate, withTitle: "Reminder", andMessage: message)
        }
    }
    
    alertController.addAction(saveAction)
    present(alertController, animated: true, completion: nil)
}
```

## Step 5: Handling Notifications

To handle notifications when the app is in the foreground, implement the `UNUserNotificationCenterDelegate` methods in the `AppDelegate` class.

```swift
class AppDelegate: UIResponder, UIApplicationDelegate, UNUserNotificationCenterDelegate {
    
    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        NotificationManager.requestAuthorization()
        UNUserNotificationCenter.current().delegate = self
        return true
    }
    
    // Handle the notification when it is received while the app is in the foreground
    func userNotificationCenter(_ center: UNUserNotificationCenter, willPresent notification: UNNotification, withCompletionHandler completionHandler: @escaping (UNNotificationPresentationOptions) -> Void) {
        completionHandler([.alert, .sound, .badge])
    }
    
    // Handle the user's response to the notification, e.g., tapping on it
    func userNotificationCenter(_ center: UNUserNotificationCenter, didReceive response: UNNotificationResponse, withCompletionHandler completionHandler: @escaping () -> Void) {
        // Handle the notification response
        
        // Call the completion handler when finished
        completionHandler()
    }
}
```

## Conclusion

In this tutorial, we've learned how to build a reminder app with local notifications using Swift in iOS. We covered setting up the project, creating the user interface, handling local notifications, and scheduling reminders. Feel free to enhance the app by adding features like notification customization, recurring reminders, or organizing reminders into categories. Happy coding!

#iOSDevelopment #SwiftProgramming