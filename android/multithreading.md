# Android. Multithreading

## Android-Specific Ways to Do Background Work

* AsyncTask
* Loaders
* IntentService

## AsyncTask and What Is Wrong With It

`AsyncTask` is a helper class for performing background operations. It has a number of methods for organizing code in a clean way:

* `onPreExecute` — what will be done in main thread before background task starts
* `doInBackground` — what will be done in background thread
* `onPostExecute` — what will be done in main thread after background task finishes
* `publishProgress` — can be called in `doInBackground` to indicate operation progress
* `onProgress` — callback for operation progress

### Execution

AsyncTasks by default are all executed one by one in one thread. It is possible to execute them in separate threads by `executeOnExecutor`.

### Cancelling

We can send cancel message to AsyncTask with `cancel` method. But it won't be cancelled immediately, as it works similar to Thread's `interrupt` logic. So, if we want to make AsyncTask stoppable, we may check `isCancelled()` in logical points of `doInBackground` method.

### Disadvantages

`AsyncTask` has significant disadvantages:

* As it is usually called from Activity, it holds reference to Activity until the task is finished. So, it may cause memory leaks.
* After screen rotation result of running AsyncTask cannot be used by recreated Activity.
* AsyncTask is not reusable. So, if we need to perform several background tasks, we need to create separate `AsyncTask` object for each of them.

### Proper Usage

AsyncTask can be used for quite short operations, as file reading or accessing database. It shouldn't be used for HTTP requests.

## Loaders

Loader API helps to load data from ContentProvider and other sources. Loaders run in separate threads and have callback methods for loading events.

However, Loaders have been deprecated since Android P (API 28). It is recommended to use ViewModels and LiveData.