# 中止程式

- 中止呼叫特定方法

```
Flight::route('/@name', function ($name) {
    echo 'Hello, ' . $name . '.<br>';
    Flight::stop();
    echo 'Here we go.<br>';
});
```

結果

```

```

- 中止呼叫特定方法, 並帶有特定訊息或 HTTP 代碼

```
Flight::route('/@name', function ($name) {
    echo 'Hello, ' . $name . '.<br>';
    Flight::halt(200, 'Coming Soon.');
    echo 'Here we go.<br>';
});
```

結果

```
Coming Soon.
```

- 在特定位置中止後續的動作

```
Flight::route('/@name', function ($name) {
    echo 'Hello, ' . $name . '.<br>';
    Flight::stop();
    echo 'Here we go.<br>';
});
```

結果

```
Hello, Kate.
```