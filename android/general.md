# Android. General

## Core Components of Android Application

* Activity
* Service
* BroadcastReceiver
* ContentProvider

## Context

`Context` is used as an interface of environment (current activity or whole application). Context allows to access application resources, UI in some cases, data storage, Android built-in services, etc.

Context can be obtained from different parts of the system. As it represents environment, it may be different.

* `Application Context` — context of the whole application, attached to `Application` object lifecycle. If some singleton object requires context, this one should be used to avoid memory leaks. However, may cause errors when used for GUI.
* `Activity` — attached to Activity lifecycle. 

## Activity

Activity is an essential part of Android application, that is responsible for the UI.

Activity may contain some UI controls inside. However, nowadays the common approach is to leave in an activity as few logic as possible and split UI to fragments.

Activity lifecycle:

* `onCreate`
* `onStart`
* `onResume`
* `onPause`
* `onStop`
* `onDestroy`

## Fragment

`Fragment` is a piece of UI and logic. The main difference with a View is that Fragment also has its own lifecycle similar to Activity's.

Fragment lifecycle:

* `onCreate`
* `onAttach`
* `onCreateView`
* `onActivityCreated`
* `onStart`
* `onResume`
* `onPause`
* `onStop`
* `onDestroyView`
* `onDestroy`
* `onDetach`

## Service

Services are designed to perform long-running operations without user interaction. Services has higher priority than activities. Service runs in the caller thread. If a caller is destroyed, service continues working.

Examples of using services: music playback, downloading files.

Service can be used in two ways:

### Started Services

In this case a service is launched with `Context.startService`. It is used for performing long operation, that continues even if caller is destroyed. Interaction with service can be done in `onStartCommand`. After operation is finished, service should be stopped (by itself via `stopSelf` or from outside). 

### Bound Services

Such services should be connected with `Context.bindService`. That allows to establish long-living connection and returns `IBinder` object for interaction with this service.

Also a service can be started as foreground. That means that Android will never kill it. Such service should show a notification.

## IntentService

`IntentService` is a kind of service that runs in background thread. Required operations are added as `Intents` and handled in `onHandleIntent` method. `IntentService` has an intent queue and stops if it is empty.

## BroadcastReceiver

`BroadcastReceiver` receives and handles broadcast intents sent by `Context.sendBroadcast(Intent)`.

There are two ways to subscribe to intents:

* Dynamically, by `Context.registerReceiver()`
* Statically, by defining `<receiver>` in the application manifest. In this case broadcast will be handled even if application is not started.

## ContentProvider

Content provider mechanism is used for unified data exchange between the apps. So, it can help with following:

* Access current application data (e.g. Database)
* Access other application data (e.g. Contacts, Calendar)
* Provide access to other applications to use current application data

`ContentProvider` class itself is an abstract class where we can define our own data manipulation. It has CRUD methods, that we should override for that.

Provided data is identified by URI. All requests are unified, data is passed as `ContentValues`. So, in our CRUD methods we should first define the subject of the request and them implement required logic.

Any data from `ContentProvider` is returned in a DB-like format, in Cursor.

`ContentResolver` is a class to access data from `ContentProvider`. We shouldn't create any instances of `ContentProvider`, we just obtain `ContentResolver` from the context and call CRUD method with some URI and arguments. `ContentResolver` will find necessary `ContentProvider` in the system and return proper data.

## Handler, Looper, MessageQueue

Java threads die after executing its run method. Looper approach means that thread contains infinite loop inside and can process some messages in this loop. It can also receive a message to stop. Such approach is used for UI.

In Android this approach works like this:

* `Message` contains an object and some secondary integer fields, that may help us to detect message purpose when handling it.
* `MessageQueue` is a queue of messages sent to the thread
* `Looper` is a worker that keep thread alive, loops through MessageQueue and sends them to `Handler` to process
* `Handler`:
    * Adds messages to the `MessageQueue`
    * Handles messages when `Looper` asks
    * Works in the thread where it was created
    
Applications for Handlers:

* Scheduling operations nearby future (`postDelayed`)
* Requesting an operation to be performed in different thread (`runOnUiThread`, `post`)

## ViewModel

`ViewModel` is a part of Android Arch library. It is designed to store and manage UI-related data in a lifecycle conscious way. It can survive when activities and fragments are recreated (e.g on screen rotation or application minimization).