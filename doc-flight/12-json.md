# JSON

Flight 支援 JSON 與 JSONP 響應,<br>
用於支援 API 傳遞.

- application/json

```
Flight::json([
    'id'   => $id,
    'name' => $name,
]);
```

- application/javascript (JSONP)

```
Flight::jsonp([
    'id'   => $id,
    'name' => $name,
], 'q');
```

JSONP 範例,
假設你以 q=myFunc 即可收到該資料.

```
myFunc({"id": 123, "name": "Kate"});
```

