# 請求

- 取得請求範例

```
Flight::request()->url;
```

- 請求包含的屬性

```
- url
- base
- method
- reffer
- ip
- ajax
- scheme
- user_agent
- type
- length
- query
- data
- cookies
- files
- secure
- accept
- proxy_ip
```

- 請求 query 屬性允許取得特定鍵值, 無返回 NULL

```
Flight::request()->query['id'];
```

- 透過 RAW 方式請求, 請用 getBody 方法取得

```
Flight::request()->getBody();
```

- 透過 JSON 方式請求, 假設 { "id": "TEST" }, 下列取得方式

```
Flight::request()->data->id;
```