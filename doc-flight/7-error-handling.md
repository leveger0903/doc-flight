# 錯誤處理

- 自訂錯誤訊息

```
Flight::set('flight.log_errors', true);
Flight::map('error', function (Exception $ex) {
    echo '<h1>' . $ex->getMessage() . '</h1><br>';
    echo str_replace("\n", '<br>', $ex->getTraceAsString());
});
```

- 自訂 404 找不到

```
Flight::map('notFound', function () {
    echo "404";
});
```
