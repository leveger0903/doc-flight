# 過濾

此功能相當於 slim 的 middleware 概念,<br>
但 slim 可透過 class 實作(__invoke method),<br>
但 flight 僅可透過 method.

```
Flight::map('hello', function ($params) {
    return 'Hello, ' . $params['name'];
});

Flight::before('hello', function (&$params, &$output) {
    $params[0]['authorize'] = false;  
});

Flight::after('hello', function (&$params, &$output) {
    if (!$params[0]['authorize'])
        $output = '';
});

Flight::route('/@name', function ($name) {
    echo Flight::hello([
        'name' => $name,
    ]);
});
```

允許多組 before,<br>
使用 return false 可停止後面的 before 方法繼續執行,<br>
另外像是 map 或是 register 方法不允許動態使用 before 或是 after 方法.

```
Flight::before('route', function (&$params, &$output) {
    echo 'one';
});

Flight::before('route', function (&$params, &$output) {
    echo '.two';
    return false;
});

Flight::before('route', function (&$params, &$output) {
    echo '.three';
});

Flight::route('/@name', function ($name) {
    echo 'Hello, world';
});
```