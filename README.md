# Firebase iOS app

## Objective 

* Create a Firebase project. 
* Create an iOS project that communicates with your Firebase project. 

## 1. Firebase Console 

Navigate to the [Firebase console](https://console.firebase.google.com/u/1/) to create a Firebase project. 

![create project](https://user-images.githubusercontent.com/1819208/110934167-ab766f80-82fb-11eb-9c17-780d667094ee.png)

Continue going through the various creation screens and selecting appropriate choices. 

## 2. Add an app to your Firebase project 

The type of apps supported by Firebase include iOS, Android and Web applications. 

Since we're building an iOS app select iOS from the list illustrated below. 

![select ios](https://user-images.githubusercontent.com/1819208/110934887-a960e080-82fc-11eb-81a3-76d98608472d.png)

At this point you will need a bundle id from your Xcode project. 

#### Create an Xcode project 

* Create an Xcode project. 
* Give it a name such as iOSQuestions. 
* Locate and copy the bundle id and head back to the Firebase console. 
* Paste the bundle id in the required field. 

![add bundle id](https://user-images.githubusercontent.com/1819208/110935263-3310ae00-82fd-11eb-961d-274ac076fc97.png)


## 3. `GoogleService-info.plist`

The `GoogleService-info.plist` will now be available for download. This `plist` has all the required information needed for your Xcode project to communicate with your Firebase project.

Download the `GoogleService-info.plist` and add it to your Xcode project. 

## 4. Adding the Firebase dependencies 

As of this writing Firebase supports Swift Package Manager and also Cocoapods. In this project we will be installing Firebase via SPM.

Here is the [Firebase](https://github.com/firebase/firebase-ios-sdk/blob/master/SwiftPackageManager.md) SPM package url `https://github.com/firebase/firebase-ios-sdk.git`

Head over to Xcode and install the Swift package. 

![install firebase swift package](https://user-images.githubusercontent.com/1819208/110936108-5f78fa00-82fe-11eb-8706-c927114379a6.png)

![install package](https://user-images.githubusercontent.com/1819208/110936412-d8785180-82fe-11eb-8c9a-0342fac45b8c.png)

#### Select the Firebase products you need in your app

![firebase product selection](https://user-images.githubusercontent.com/1819208/110936621-2db46300-82ff-11eb-8961-460883988bd6.png)

## 5. Initialize Firebase in your Xcode project 

After intalling Firebase to your project via Swift Package manager or Cocoapods you now need to initialize Firebase in your Xcode project. 

Add the following code to your `AppDelegate.swift`

```swift 
import UIKit
import Firebase // code added 

@main
class AppDelegate: UIResponder, UIApplicationDelegate {
  
  func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    // Override point for customization after application launch.

    // initialize Firebase
    FirebaseApp.configure() // code added

    return true
  }
}
```

You now have in place the basic requirements for communicating between your Xcode application and Firebase. 

## 6. Setup Cloud Firestore 

Head over to the Firebase console and enable Cloud Firestore located under the **Build** panel on the left of the console. 

* Click on Cloud Firestore. 
* Click on Create database.

For now select **test mode** to enable writing and reading to the database without security rules in place. We will reviist security rules a bit later. 

![create database](https://user-images.githubusercontent.com/1819208/110940177-7e7a8a80-8304-11eb-96df-0af2ea79dbd1.png)


## 7. Posting data to Firebase database

Firebase Cloud Firestore is made up of collections at its top level. Collection consists of documents. Each document itself can have a collection and so on. 

![empty database](https://user-images.githubusercontent.com/1819208/110940476-f8127880-8304-11eb-811b-3525fddcb203.png)

When posting data from your Xcode project to Firebase Cloud Firestore, this data can be posted in two ways: 

* The data can be sent via a key, value pair. 
* The data can be sent by making your object conform to `Codbale` and using the `FirebaseFirestoreSwift` package. 

In this project we will be doing the latter. 

#### Question.swift 

```swift 
struct Question: Codable {
  var question: String
  var answer: String
  var id = UUID().uuidString
}
```

#### QuestionViewModel.swift 

```swift 
import Foundation
import Firebase
import FirebaseFirestoreSwift

struct QuestionViewModel {
  
  func postQuestion(question: Question) {
    // handle to the database
    let db = Firestore.firestore()
    
    do {
      try db.collection("questions").document(question.id).setData(from: question)
    } catch {
      print("Error writing to the Firestore: \(error)")
    }
  }
  
}
```

![successful post](https://user-images.githubusercontent.com/1819208/110941050-bafab600-8305-11eb-8afd-7ddd839ea8e7.png)



