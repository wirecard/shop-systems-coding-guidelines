## Welcome to Wirecard shop systems coding guidelines



### Introduction

Although many developers still use PHP 5, most of the examples in this article only work with PHP 7+.

1. #### Variables
___
1.1 Use meaningful variable names
Nice description of the rule.

Bed:
```php
$adr = $this->getBillingAddress();
```

Good:
```php
$billingAddress = $this->getBillingAddress();
```
___
