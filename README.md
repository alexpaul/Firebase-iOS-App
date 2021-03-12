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

Heere is the [Firebase](https://github.com/firebase/firebase-ios-sdk/blob/master/SwiftPackageManager.md) SPM package url `https://github.com/firebase/firebase-ios-sdk.git`

Head over to Xcode and install the Swift package. 

![install firebase swift package](https://user-images.githubusercontent.com/1819208/110936108-5f78fa00-82fe-11eb-8706-c927114379a6.png)
