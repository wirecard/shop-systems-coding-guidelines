# Welcome to Wirecard shop systems coding guidelines


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
