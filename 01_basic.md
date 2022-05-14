# 物件導向基礎

[TOC]

## 物件導向

1. OOP
2. 整理程式碼
3. class 藍圖
4. object 實體 (instance)

## 屬性與方法

1. 變數稱為屬性(property)
2. 函式稱為方法(method)

## 可見性修飾符

簡單的說，這是物件的屬性或方法的能見度

1. public : Anywhere: Inside other classes and object instances
2. private : Inside the current class only
3. protected : Inside the current class and any subclasses

## 建構函式

1. 每次物件被建立時會執行
2. 通常用於初始化屬性

## this

指向自己

## Getter & Setter

應該使用的論點

1. 專案重構較容易
2. 可以在 setter , getter 放置 breakpoints
3. 避免使用 Magic functions
4. 符合物件導向封裝特性

不應該使用的論點

1. 效能較差
2. 可閱讀性較差

[PHP performance tips](https://web.archive.org/web/20140625191431/https://developers.google.com/speed/articles/optimizing-php)
[What are PHP Magic Methods?](https://www.culttt.com/2014/04/16/php-magic-methods/)

結論

除非很有必要, 否則不使用

## 靜態屬性與方法

1. 關鍵字 static
2. 使用範圍解析操作符(::)訪問
3. 特色是類別(Class)直接使用, 不能被物件(Object)所使用。
4. 找自己用 self::
5. 通常被作為工具函式使用。

🤔 為何使用?

1. 需要全域的類別變數或涵式。
2. utility (helper) 性質的類別

實例:每次調用產生物件，靜態計數屬性將遞增 1。

```php
class Item {
    public static $count = 0;

    public function __construct($name, $description) {
        self::$count++;
    }

    public static showCount()
    {
        echo self::$count;
    }
}

item  = new Item();

Item::showCount();


```

## 常數

1. 定義後不能改變
2. 命名方式為全大寫, 用底線分隔單字
3. 常數屬於全域
4. 通常用於定義可能需要的設置或值貫穿整個網站, 例如資料庫連線
5. 在類別裡面定義常數使用 const 關鍵字 (一般使用 define)
6. 常數通常在頂部定義
7. 使用範圍解析操作符(::)訪問
8. 常數是靜態值，但不需要使用 static 關鍵字 宣告

```php
class Item
{
    CONST NAX_LENGTH = 24;
}

echo Item::MAX_LENGTH;
```

## 繼承

1. 避免重復
2. 使用`extends`關鍵字

```php
// parent class
class Item
{
    public $name;

    public function getListingDescription()
    {
        return $this->name;
    }
}

// child class
class Book extends Item
{
    public $author;
}
```

## 重寫方法

overriding a method

```php
class Item
{
    public $name;

    public function getListingDescription()
    {
        return $this->name;
    }
}

// child class
class Book extends Item
{
    public $author;

    public function getListingDescription()
    {
        // 重寫方法
        return $this->name . " by " . $this->author;

        // 調用父類別方法
        return parent::getListingDescription() . " by " . $this->author;
    }
}
```

## 範例

```php

<?php

// class 藍圖
class Car {
    // 屬性(property)
    public $color = 'red';
    public $weight;
    public $availableColors = [
        'red', 'green', 'blue', 'white'
    ];

    // 建構函式
    public __constructor($color, $weight) {
        $this->color = $color;
        $this->weight = $weight;
    }

    // 方法(method)
    public function getColor() {
        return $this->color;
    }

    public function setColor() {
        // 過濾輸入的內容 (零信任)
        if(in_array($color, $this->availableColors)) {
            $this->color = $color;
        }
    }
}

// object 實體 (instance)
$myCar = new Car("red", "1800kg");

// 這邊輸入了一個不被接受的顏色,因此並沒有寫入
$myCar->setColor("black");
$myCar->getColor().PHP_EOL;

```

## 面試 : Call by Reference , Call by Value

1. 這不是 OOP 的內容，但面試會跟 OOP 一起考
2. 要特別注意的是跟 JavaScript 特性有所不同!
3. 物件基本是 Call by Reference

```php
class Car {
    public $color = 'red';
}

$carOne = new Car();
$carTwo = $carOne;
$carTwo->color = 'green';

// 相等! 與JS不同
echo $carOne === $carTwo;

echo $carOne->color; // green
```

## Magic Methods

1. 冷門知識
2. 有可能開發中都不會用到 (除了 construct)

## Traits 多重繼承

1. 用來解決 PHP Inheritance 只能單一繼承的問題
2. Traits 不支援常數

## Abstract Class 抽象類別

1. 宣告類別的某些方法必須由子類別實作
2. 而且父類別中不會定義這些方法的實作。
