---
description: isset使用中遇到的一个问题
---

# isset\(\)检测变量值为NULL时返回false

以下代码，输出结果会是什么？

```text
$array = [
    'key' => null
];

if (isset($array['key'])) {
    echo 'is set';
} else {
    echo 'not set';
}
```

最近遇到一个自己误解了isset\(\)功能的问题。我原以为isset\(\)就是用来检测某变量是否有被定义，有则返回true。还可用于检查数组中是否设置了某个键名。但是在你给该变量或者该键赋值`null`以后，则就返回`false`。而我的误解就是认为只要被定义了，不管值是什么，都返回`true`。所以上面的代码输出的会是`not set`。以下是[官方手册](https://www.php.net/manual/zh/function.isset.php)中的说明，而自己则完全忽视掉了`null`的情况。

> > 检测变量是否设置，并且不是 NULL。 如果已经使用 unset\(\) 释放了一个变量之后，它将不再是 isset\(\)。若使用 isset\(\) 测试一个被设置成 NULL 的变量，将返回 FALSE。同时要注意的是 "null" 字符串并不等同于 PHP 的 `NULL` 常量。

