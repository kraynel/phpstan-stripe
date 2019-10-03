# phpstan-stripe
Stripe SDK extension for PHPStan

PHP library for the Stripe API uses PHP objects where some of the properties are used only when the object is updated.

- `Customer::$source`, [used only for `save()`](https://stripe.com/docs/api/customers/update#update_customer-source)
- `Subscription::$coupon`, [used only for `save()`](https://stripe.com/docs/api/subscriptions/update#update_subscription-coupon)
- `Source::$card`, [additional hash for a payment method](https://stripe.com/docs/api/sources/object#source_object-type)
- [`Invoice::$charge`](https://stripe.com/docs/api/invoices/object#invoice_object-charge) and [`Invoice::$customer`](https://stripe.com/docs/api/invoices/object#invoice_object-customer) are [expandable](https://stripe.com/docs/api/expanding_objects) and can be objects when retrieved, not just strings

These are not documented using `@property` tags on the classes, and the dev team [feels](https://github.com/stripe/stripe-php/pull/543) it should stay this way. Honestly, I'm not sure adding `@property` tags would be the best way either.

PHPStan will obviously flag such property access and this extension will resolve those errors by telling PHPStan such properties exist.

## Installation

The package is [hosted on Packagist](https://packagist.org/packages/spaze/phpstan-stripe) so you can install it using [Composer](https://getcomposer.org/):

```
composer require --dev spaze/phpstan-stripe
```

If you use [phpstan/extension-installer](https://github.com/phpstan/extension-installer), you are all set!

For manual installation, add this to your `phpstan.neon`:

```
includes:
    - vendor/spaze/phpstan-stripe/extension.neon
```
