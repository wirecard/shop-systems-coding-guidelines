# Welcome to Wirecard shop systems coding guidelines

+ Inspired from [clean-code-javascript](https://github.com/ryanmcdermott/clean-code-javascript)
+ Inspired from [clean-code-php](https://github.com/jupeter/clean-code-php)

## Table of Content

1. [Introduction](#introduction)
2. [Variables](#variables)
   * [Variable names](#use-meaningful-variable-names)
   * [Method naming](#use-the-same-vocabulary-for-the-same-type-of-variable)
3. Functions
4. [Comparison](#comparison)
5. Translations
6. Classes
7. Objects

## Introduction

Although many developers still use PHP 5, most of the examples in this article only work with PHP 7+.

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
Be consistent with the naming over the whole plugin. Don't name the same object different.

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

### Comparison

#### Avoid else statements and to deep nesting of if else

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
