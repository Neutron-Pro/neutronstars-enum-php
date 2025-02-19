# Enum library for PHP 7.1 or more.

## Installation:

---

### Only Enum PHP whiteout Doctrine and Symfony:

```
composer require neutronstars/enum
```

---

### For Doctrine

```
composer require neutronstars/doctrine-enum-php-type
```

> Docs: https://github.com/Neutron-Pro/doctrine-enum-php-type

---

### For Symfony

```
composer require neutronstars/symfony-normalizer-enum-php
```

> Docs: https://github.com/Neutron-Pro/symfony-normalizer-enum-php

### For Symfony and Doctrine

```
composer require neutronstars/doctrine-enum-php-type
composer require neutronstars/symfony-normalizer-enum-php
```

---

## How create an Enum class:

### Method 1

```php
/**
 * @method static self ONE()
 * @method static self TWO()
 * @method static self THREE()
 */
class MyEnum extends \NeutronStars\Enum\Enum
{
   public const ONE = null;
   public const TWO = null;
   public const THREE = null;
}
```

This enum does not require a constructor. We simply create a list of constants that have no value other than their name.

### Method 2

```php
/**
 * @method static self ONE()
 * @method static self TWO()
 * @method static self THREE()
 */
class MyStringEnum extends \NeutronStars\Enum\Enum
{
   public const ONE   = 'One';
   public const TWO   = 'Two';
   public const THREE = 'Three';
}
```

```php
/**
 * @method static self ONE()
 * @method static self TWO()
 * @method static self THREE()
 */
class MyIntEnum extends \NeutronStars\Enum\Enum
{
   public const ONE   = 1;
   public const TWO   = 2;
   public const THREE = 3;
}
```

---

## Use an Enum class:


### Get instance of an enum

```php
$two = MyStringEnum::TWO();

echo $two; // return TWO
echo $two->key; // return TWO
echo $two->value; // return Two
```

### Get instance of an enum from a string

```php
$three = MyStringEnum::from('THREE');

echo $three; // THREE
echo $three->key; // return THREE
echo $three->value; // return Three
```

### Compare the instances of an enum

```php
$value = MyStringEnum::tryFrom($_GET['number']);
if ($value === MyStringEnum::ONE()) {
  echo 'The number is ONE !';
}
```
Result:

```
if $_GET['number] is ONE or One or 1 then 'The number is ONE !'
else nothing.
```

---

### Difference between `from` and `tryFrom`.

If you use "tryFrom" and the parameter value is not found, the method returns null.

If you use "from" and the value of the parameter is not found, an error of type ValueError is raised.

---

### Retrieve all keys of the enum.

```php
$cases = MyIntEnum::cases();
```

Result:

```
[
  MyIntEnum::ONE(),
  MyIntEnum::TWO(),
  MyIntEnum::THREE() 
]
```

```php
foreach (MyIntEnum::cases() as $case) {
    echo '- ' . $case->value;
}
```

Result:

```
- 1
- 2
- 3
```

---

### Serialization and Deserialization

You can serialize an enum with the serialize function of PHP.

```php
$serialized = serialize(MyEnum::THREE());
```

But for deserialization, there will be a small difference, You must use the `from` or `tryFrom` method:

```php
$deserialized = MyEnum::from(unserialize($deserialized));
// $deserialized = MyEnum::THREE()
```

---
