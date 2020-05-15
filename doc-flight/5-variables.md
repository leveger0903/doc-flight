# 變數

- 設置變數

```
Flight::set('name', 'TOTO');
```

- 取得變數

```
$name = Flight::get('name');
```

- 查看是否有此變數

```
$hasName = Flight::has('name');
```

- 清除變數

```
Flight::clear('name');
```

- 清除所有的變數

```
Flight::clear();
```

- 將變數紀錄於 log

```
Flight::set('flight.log_errors', true);
```
