# 物件導向進階

[TOC]

## 存取修飾字

簡單的說，這是物件的屬性或方法的能見度

1. public : 誰 (都可以) 使用
2. private : 只有 (自己的類別) 可以使用
3. protected : (自己的類別) 或 (繼承類別) 可以使用

## Static Method

1. 稱為靜態方法。
2. 包含靜態屬性與靜態方法。
3. 特色是類別(Class)直接使用, 不能被物件(Object)所使用。
4. 使用 scope resolution operator(::)
5. 找自己用 self::
6. 通常被作為工具函式使用。

🤔 為何使用?

1. 需要全域的類別變數或涵式。
2. utility (helper) 性質的類別

```php
class Timer
{
    static $timer = 0;

    public function __construct()
    {
        self::$timer++;
    }
}

echo Timer::now_time;
```

## Contant 常數

1. 定義了就不會改變
2. 找自己 self::

```php
<?php

class Car
{
    public $color;
    public $manufacturer;

    const MANUFACTURER_BENZ = 'benz';
    const MANUFACTURER_TESLA = 'tesla';
    const MANUFACTURER_BMW = 'bmw';

    const COLOR_RED = 'red';
    const COLOR_GREEN = 'green';
    const COLOR_BLUE = 'blue';

    public function __construct($color, $manufacturer)
    {
        $this->color = $color;
        $this->manufacturer = $manufacturer;
    }
}

// PHP 8.0之後可以使用命名參數,如此一來傳遞順序就不重要了
$myCar = new Car(color: Car::COLOR_RED, manufacturer: CAR::MANUFACTURER_BENZ);
```

## Magic Methods

1. 冷門知識
2. 有可能開發中都不會用到 (除了 construct)

[PHP Magic Methods 分類](https://imyoungyang.gitbooks.io/php7-study-group-notes/content/Chapter2/php-magic-methods.html)

## Inheritance 繼承

## Traits 多重繼承

1. 用來解決 PHP Inheritance 只能單一繼承的問題
2. Traits 不支援常數

## Abstract Class 抽象類別

1. 宣告類別的某些方法必須由子類別實作
2. 而且父類別中不會定義這些方法的實作。
