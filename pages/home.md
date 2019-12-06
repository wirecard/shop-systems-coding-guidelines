# Welcome to Wirecard shop systems coding guidelines

+ Inspired from [clean-code-javascript](https://github.com/ryanmcdermott/clean-code-javascript)
+ Inspired from [clean-code-php](https://github.com/jupeter/clean-code-php)

## Table of Content

1. [Introduction](#introduction)
   * Code formatting
   * Shop system specific formatting
2. [Variables](#variables)
   * [Variable names](#use-meaningful-variable-names)
   * [Method naming](#use-the-same-vocabulary-for-the-same-type-of-variable)
   * [Use constants](#use-constants)
   * [Use searchable names](#use-searchable-names)
3. Methods
4. [Comparison](#comparison)
    * [Avoid one line if's](#avoid-one-line-ifs)
    * [Avoid too deep nesting of if's](#avoid-else-statements-and-too-deep-nesting-of-if-else)
    * [Avoid too many returns or if statements](#avoid-too-many-returns-or-if-statements)
5. Translations
6. Classes
7. Objects
8. Architecture
   * File naming
   * Plugin structure
   * Design patterns
      * Service
      * Factory
      * Builder
      * Strategy
      * Helper
9. Database
10. Error handling
11. Logging

## Introduction

Although many developers still use PHP 5, most of the examples in this article only work with PHP 7+.

### Code formatting
___
Here are general rules about how to formant your code. Every of these rules can be overruled by the shop system coding standard. So for specific shop systems there are specific rules.
___

### Variables
___

#### Use meaningful variable names
A variable’s name should express the intention (cause of uses) of the variable.

Bad:
```php
$adr = $this->getBillingAddress();
```

Good:
```php
$billingAddress = $this->getBillingAddress();
```
___

#### Use the same vocabulary for the same type of variable
Be consistent with the naming over the whole plugin. Don't name the same object differently.

Bad:
```php
$this->getUserInfo();
$this->getClientData();
$this->getCustomerRecord();
```

Good:
```php
$this->getUser();
```
___

#### Use constants

Bad:
```php
$result = $this->serielize($data, 448);
```

Good:
```php
$result = $this->serielize($data, JSON_UNESCAPED_SLASHES | JSON_PRETTY_PRINT | JSON_UNESCAPED_UNICODE);
```
___

#### Use searchable names 

Bad:
```php
if ($order->getStatus() === 4) { //what the heck is 4?
    //do somthing
}
```

Good:
```php
if ($order->getStatus() === ORDER_STATUS_PROCESSING) {
    //do somthing
}
```
___

### Comparison

#### Avoid else statements and too deep nesting of if else

Bad:
```php
if (isset($password)) {
    if ($password > 5) {
        $sql->savePassword($password);
    } else {
        echo "Your password is to short";
    }
} else {
    echo "You did not set a password";
}
```

Good:
```php
try {
    $this->validatePassword($password);
    $this->savePasswordToDatabase($password);
} catch (\Exception $error) {
    echo $error->getMessage();
}
```
___

#### Avoid one-line if's
They are messy and unclear to understand without deep knowledge of the code.

Bad:
```php
$isThreeD = is_null($config->getMerchantAccountId()) || ($config->getThreeDMerchantAccountId() && ($transaction->isFallback() || $transaction->getThreeD())) ? true : false;
```

Good:
```php
function isThreeD() {
    if ($config->isValid() && $transaction->isThreeD()) {
        return true;
    }

    return false;
}
```
___

#### Avoid too many returns or if statements

Bad:
```php
function getResponse() {
    if ($this->validation()) {
        return;
    }
    
    if ($this->status == 'success') {
        return new Success();
    }

    if ($this->status == 'failure') {
        return new Failure();
    }

    if ($this->status == 'pending') {
        return new Pending();
    }

    return Failure();
}
```

Good:
```php
function getResponse() {
    $this->validation();
    switch($this->status) {
        case 'success':
            $response = new Pending();
        case 'failure':
            $response = new Failure();
            break;
        case 'pending':
        default:
            $response = new Pending();
            break;
    }

    return $response;
}
```
___
