# NAME

RxT4A - RxJava Toolbox for Android

[ ![Download](https://api.bintray.com/packages/cookpad/maven/RxT4A/images/download.svg) ](https://bintray.com/cookpad/maven/RxT4A/_latestVersion)

# SYNOPSIS

```java
// AndroidSchedulers

Scheduler scheduler = AndroidSchedulers.mainThread();
Scheduler scheduler = AndroidSchedulers.from(new Handler());

// AndroidCompositeSubscription

final AndroidCompositeSubscription s = new AndroidCompositeSubscription();

s.add(subscription1);
s.add(subscription2);

s.unsubscribe(); // unsubscribe 1 and 2

// it is reusable!
s.add(subscription3);
s.add(subscription4);

s.unsubscribe(); // unsubscribe 3 and 4, too!

// OperatorAddToCompositeSubscription

Observable.just("foo")
        .lift(new OperatorAddToCompositeSubscription<String>(s))
        .delay(5, TimeUnit.MILLISECONDS)
        .subscribe(...);

s.unsubscribe(); // unsubscribe the above subscription
```


# DESCRIPTION

This is a fork of [RxAndroid](https://github.com/ReactiveX/RxAndroid).

## AndroidSchedulers

This is almost the same as RxAndroid's `AndroidSchedulers`.

## AndroidCompositeSubscription

This is a variation of `CompositeSubscription` but can be reused multiple times.

## OperatorAddToCompositeSubscription

Add a subscription to `AndroidCompositeSubscription` in operator chains.

## AndroidSubscriptions

This class provides a way to create subscriptions for Android applications.

```java
Subscription subscription = observable.subscribe(subscriber);

// Like Subscriptions.create(Action0), but the action is called on the main thread.
subscription.add(AndroidSubscriptions.unsubscribeOnMainThread(new Action0() {
    @Override
    public void call() {
        // You can touch touch views.
    }
}));
```

# INSTALL

```groovy
dependencies {
    compile 'com.cookpad.android.rxt4a:rxt4a:0.10.0'
}
```

# LICENSE

The MIT License

# AUTHOR

Cookpad Inc.

