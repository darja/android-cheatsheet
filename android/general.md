# Android. General

## Core Components of Android Application

* Activity
* Service
* BroadcastReceiver
* ContentProvider

## Context
** TODO**

## Activity

Activity is an essential part of Android application, that is responsible for the UI.

Activity may contain some UI controls inside. However, nowadays the common approach is to leave in an activity as few logic as possible and split UI to fragments.

Activity lifecycle:

* Create
* Start
* Resume
* Pause
* Stop
* Destroy

## Fragment

**TODO**

## Service

Services are designed to perform long-running operations without user interaction. Services has higher priority than activities. Service runs in the caller thread. If a caller is destroyed, service continues working.

Examples of using services: music playback, downloading files.

Service can be used in two ways:

### Started Services

In this case a service is launched with `Context.startService`. It is used for performing long operation, that continues even if caller is destroyed. Interaction with service can be done in `onStartCommand`. After operation is finished, service should be stopped (by itself via `stopSelf` or from outside). 

### Bound Services

Such services should be connected with `Context.bindService`. That allows to establish long-living connection and returns `IBinder` object for interaction with this service.

Also a service can be started as foreground. That means that Android will never kill it. Such service should show a notification.

### What if Android kills a service?
** TODO**

## IntentService

`IntentService` is a kind of service that runs in background thread. Required operations are added as `Intents` and handled in `onHandleIntent` method. `IntentService` has an intent queue and stops if it is empty.

## BroadcastReceiver
**TODO**

## ContentProvider
**TODO**
