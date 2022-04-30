# 物件導向基礎

在物件導向當中:

1. 變數稱為屬性(property)
2. 函式稱為方法(method)
3. 建構函式在物件被建立時會執行!

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

## 補充 : Call by Reference , Call by Value

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
