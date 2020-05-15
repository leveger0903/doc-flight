# 路由

## 基本路由

```
class Basic
{
  public static function greeting()
  {
    echo 'Hello World';
  }
}

Flight::route('/', array('Basic', 'greeting'));
Flight::start();
```

```
class Basic
{
  public $name;
  public function __construct($name) {
    $this->name = $name;
  }

  public function greeting()
  {
    echo 'Hello, ' . $this->name . '.';
  }
}

$class = new Basic('Kiwi');
Flight::route('/', array($class, 'greeting'));
Flight::start();
```

## 路由方法

```
Flight::route('GET /hello', function () {
  echo 'This is GET method.';
});

Flight::route('POST /hello', function () {
  echo 'This is POST method.';
});

Flight::route('DELETE /hello', function () {
  echo 'This is DELETE method.';
});
```

## 正規表達式與帶有變數的路由

```
Flight::route('/@name/@id:[0-9]+', function ($name, $id) {
  echo 'Hello, ' . $name . ', Your user id:' . $id;
});
```

## 選用路由

```
Flight::route('/birthday(/@year:[0-9]{4}(/@mon:[0-9]{2}(/@day:[0-9]{2})))', function ($year, $mon, $day) {
  echo json_encode([
    'year' => $year,
    'mon'  => $mon,
    'day'  => $day,
  ]);
});
```

## 萬用字元

```
Flight::route('/user/*', function () {
  echo 'user';
});

Flight::route('*', function () {
  echo 'Any route except user.';
});
```

## 跳過特定路由

```
Flight::route('/user/@name', function ($name) {
  if (in_array($name, ['Xi', 'Trump'])) {
    return true;
  }

  echo 'Hello, ' . $name;
});

Flight::route('/user/*', function () {
  echo 'We dont welcome you.';
});
```

## 取得更多路由內容

```
Flight::route('GET /@name/@id', function ($name, $id, $route) {
  echo json_encode([
    'method' => $route->methods,
    'params' => $route->params,
    'regex'  => $route->regex,
    'splat'  => $route->splat,
  ]);
}, true);
```