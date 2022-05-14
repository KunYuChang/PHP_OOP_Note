# 自動載入與命名空間

## 關鍵字

1. autoload
2. namespace
3. psr-4

## 為了解決什麼?

為了避免引用不同路徑但相同類別名稱的內容(會打架)，PHP 提供 Namespaces 來解決。

常見例子 :

1. 自己定義了 class Email
2. 使用的 Third Party 也定義了 class Email
3. 如果使用 require ，class 名稱是撞名的!(會有問題)

## 如何解決

4. 使用 composer
5. 使用 composer.json 輸入內容

```php
{
    "autoload": {
        "psr-4" : {
            "app\\": "./app"
        }
    }
}
```

3. 打完之後，必須於終端機下更新指令`composer update`

4. 要被引用的檔案需要輸入 namespace

   a. namespace 簡單說就是給一個識別名稱
   b. 通常會用路徑來當名稱
   c. 注意路徑要用\

```php
namespace App\Controllers;
```

5. index.php 輸入內容

```php

require_once "./vendor/03_autoload.php";

use App\Controllers\Email;
use App\Controllers\Person;

$enail = new Email();
$pseson = new Person();
```

[The Codeholic - Namespaces & Autoloading | PHP for Beginners](https://www.youtube.com/watch?v=NLXtGZ6Ilsw)

[Program With Gio - PHP Coding Standards, Autoloading (PSR-4) & Composer - Full PHP 8 Tutorial](https://www.youtube.com/watch?v=rqzYdHdyMH0)
