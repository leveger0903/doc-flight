# 視圖

Flight 提供基本的視圖功能,<br>
但建議使用 twig 或是 blade 處理視圖.

- 入門教學

Views\view.hello.php

```
<!doctype html>
<html>
<head></head>
<body>
  <h1><?php echo $name ?></h1>
</html>
```

index.php

```
Flight::set('flight.views.path', '../Views');
Flight::route('/@name', function ($name) {
    echo Flight::render(
        'view.hello.php',
        [
            'name' => $name
        ]
    );
});
```

- 入門教學

Views\view.hello.php

```
<!doctype html>
<html>
<head></head>
<body>
  <h1><?php echo $name ?>: <?php echo $tel ?></h1>
</html>
```

index.php

```
Flight::set('flight.views.path', '../Views');
Flight::set('flight.views.extension', '.php');
Flight::route('/@name/@tel', function ($name, $tel) {
    Flight::view()->set('name', $name);
    Flight::view()->set('tel', $tel);
    echo Flight::render('view.hello');
});
```

- 組件式模板

Views\view.header.php

```
<head>
    <title><?php echo $title; ?></title>
</head>
```

Views\view.body.php

```
<body>
    <h1><?php echo $content; ?></h1>
</body>
```

Views\view.hello.php

```
<!doctype html>
<html>
    <?php echo $header_var ?>
    <?php echo $body_var ?>
    <script><?php echo $script; ?></script>
</html>
```

index.php

```
Flight::set('flight.views.path', '../Views');
Flight::set('flight.views.extension', '.php');
Flight::route('/@name/@tel', function ($name, $tel) {
    Flight::render(
        'view.header',
        [
            'title' => $name
        ],
        'header_var'
    );

    Flight::render(
        'view.body',
        [
            'content' => $name . ': ' . $tel
        ],
        'body_var'
    );

    echo Flight::render(
        'view.hello',
        [
            'script' => 'console.log(\'test\');', 
        ]
    );
});
```

- Flight PHP 允許將模板元件替換

本範例為將模板元件替換成 Twig

```
use \Twig\Loader\FilesystemLoader as FilesystemLoader;
use \Twig\Environment as Environment;

Flight::register('view', new Class{ }, [], function ($anonymousClass) {
    $loader = new FilesystemLoader('../Views/');
    $twig = new Environment($loader);
    $anonymousClass->template = $twig->load('view.test.php');
});

Flight::map('render', function ($anonymousClass, $data) {
    $template = $anonymousClass->template;
    return $template->render($data);
});

Flight::route('/@name/@tel', function ($name, $tel) {
    echo Flight::render(
        Flight::view(),
        [
            'name' => $name,
            'tel'  => $tel,
        ]
    );
});
```