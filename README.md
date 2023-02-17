# Dependency

## The Problem

In `before.py`:

class `PaymentProcessor` is dependent on the `AuthorizerSMS` class. 

The `pay` method in `PaymentProcssor` is responsible for both: the creation and the usage of the `AuthorizerSMS` object. 

This coupling makes the `PaymentProcessor` hard to test (check `before-test.py` ) and very dependent on the `AuthorizerSMS`.


## Dependency Injection
Separating the object creation from the object usage:

In `dep_inj.py`, we updated `PaymentProcessor` to be initialized with an `AuthorizerSMS` as an argument.

In other words, we're now injecting the `AuthorizerSMS` object into the `PaymentProcessor` object instead of creating it within.

This also helps in testing (check `dep_inj_test.py`) as now we can expect certain outcomes from `PaymentProcessor.pay` method based on the outcome of the authorizer.


## Dependency Inversion
`PaymentProcessor` is still directly dependent on `AuthorizerSMS` (payment processing is coupled with sms authorization).

In `dep_inv.py` we added an Abstract Base Class `Authorizer`, updated `AuthorizerSMS` and added `AuthorizerRobot` as different type of authorization. 

We then updated `PaymentProcessor` so it's dependent on the newly added ABC `Authorizer` (decoupled from a sepcific authorization type).

Now both `PaymentProcessor` and `AuthorizerSMS` are dependent on an Abstract Base Class `Authorizer` in what's known as Dependency Inversion, instead of being dependent directly. This allows `PaymentProcessor` to be decoupled from any concrete implementation of an authorizer.