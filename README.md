#ag84ark changes

I was finally able to make it work with plugin version 1.0.11 and Xcode 12.5

Podfile

```
post_install do |installer|
  installer.pods_project.targets.each do |target|
    flutter_additional_ios_build_settings(target)
    target.build_configurations.each do |config|
      config.build_settings['IPHONEOS_DEPLOYMENT_TARGET'] = '10.0'
    end
  end
end

pod 'Stripe', :git => 'https://github.com/stripe/stripe-ios.git', :tag => 'v19.4.1'
```

In the plugin v1.0.11 -> ios/TPSStripeManager.h change:

```
- #import <Stripe/Stripe.h>
+ @import Stripe;
```

Hope that this helps someone, it took me 2 days to get here :) ( No experience in Swift or Object C )

[![pub package](https://img.shields.io/pub/v/stripe_payment.svg)](https://pub.dev/packages/stripe_payment)

# stripe_payment

#### Conveniently secure payments methods using Stripe.

## Quick Glance

- This Flutter plugin is a straight port from tipsi-stripe plugin for React Native - we tried to
  keep the API as close as possible so the documentation applies this this plugin as well.
- Collect chargable tokens from users' **Card Input** and **Apple & Google Pay**
- For **SCA** compliant apps, setup payment intents for later confirmation.

## Supported features:

### Native Pay -  & G

- canMakeNativePayPayments()
- deviceSupportsNativePay()
- potentiallyAvailableNativePayNetworks()
- completeNativePayRequest()
- cancelNativePayRequest()

### Card Form

- paymentRequestWithCardForm()

### Card Params Object

- createTokenWithCard()

### Bank Account Params Object

- createTokenWithBankAccount()

### Create Source Object With Params

- createSourceWithParams()

<img src="https://github.com/jonasbark/flutter_stripe_payment/raw/master/screenshot_android.png" width="400">

![Apple Pay](https://user-images.githubusercontent.com/7946558/65780165-02838700-e0fe-11e9-9db9-5fe4e44ed819.gif)

## Dependencies

### Android & iOS

- Create a Stripe account and project
- Retrieve a publishable key from the Stripe dashboard

![Stripe Dashboard](https://miro.medium.com/max/847/1*GPDsrgR6RXYuRCWiGxIF1g.png)

### Android

- Requires AndroidX

Include support in android/gradle.properties

```properties
android.useAndroidX=true
android.enableJetifier=true
```

For proper setup also have a look at: https://github.com/jonasbark/flutter_stripe_payment/issues/88#issuecomment-553798157

## Documentation

As this plugin is a port from tipsi-stripe for React Native you may consult their documentation:
https://github.com/tipsi/tipsi-stripe/tree/experimental-connect/website/docs-md
It includes:

- how to setup Google / Apple Pay
- method documentations

## Blog Posts

- [Build a marketplace in your Flutter app and accept payments using Stripe and Firebase](https://medium.com/flutter-community/build-a-marketplace-in-your-flutter-app-and-accept-payments-using-stripe-and-firebase-72f3f7228625)
