# 覆寫

下列 HTTP 代碼可覆寫:

- 302: redirect
- 404: notFound
- 500: error

```
Flight::map('notFound', function () {
  echo '404';
});
```

Flight PHP 允許將路由元件替換\[待研究\]

```
Flight::map('route', '\App\Core\Router');
$myRouter = Flight::router();
```