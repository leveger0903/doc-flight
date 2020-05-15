# 延伸

## 映像方法

```
Flight::map('isTemperatureHigh', function (int $now) : bool {
    return $now > 30 ? true : false;
});

echo Flight::isTemperatureHigh(35);
```

## 註冊類別

App\Core\Database.php
```
namespace App\Core;

Class Database
{
    private $conn;
    private $server;
    private $user;
    private $pass;
    private $db;

    public function __construct (array $conf)
    {
        $this->server = $conf['server'];
        $this->user   = $conf['user'];
        $this->pass   = $conf['pass'];
        $this->db     = $conf['db'];

        $this->conn   = new \mysqli(
            $this->server,
            $this->user,
            $this->pass,
            $this->db
        );

        $this->conn->query("SET NAMES 'utf8'");
    }

    public function read (string $syntax)
    {
        $query  = $this->conn->query($syntax);
        $result = [];

        while ($row = $query->fetch_assoc())
           $result[] = $row;

        return $result;
    }
}
```

index.php

```
Flight::route('/', function () {
    Flight::register('db', '\App\Core\Database', [[
        'server' => 'localhost',
        'user'   => 'username',
        'pass'   => 'password',
        'db'     => 'database',
    ]]);

    echo json_encode(
        Flight::db()->read('SELECT * FROM contact')
    );
});
```

## 起始一組實例

```
Flight::route('/', function () {
    Flight::register('db', '\App\Core\Database');
    Flight::db(false);
});
```