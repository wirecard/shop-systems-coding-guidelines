# Welcome to Wirecard shop systems coding guidelines

+ Inspired from [clean-code-javascript](https://github.com/ryanmcdermott/clean-code-javascript)
+ Inspired from [clean-code-php](https://github.com/jupeter/clean-code-php)

## Introduction

Although many developers still use PHP 5, most of the examples in this article only work with PHP 7+.

### Variables
___

#### Use meaningful variable names
A variable’s name should express the intention (cause of uses) of the variable.

Bed:
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

Bed:
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
