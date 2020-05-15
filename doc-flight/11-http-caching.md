# HTTP 快取

Flight 提供 HTTP 快取,<br>
如果未進行修改時返回 HTTP 304 未修改響應,<br>
客戶端就會使用本地端快取版本.

- Last-Modified

```
Flight::lastModified(1589500800);
```

- ETag

```
Flight::etag('216ef68af065471052435a010638fee7');
```

如果快取值與請求相同時,<br>
Flight 會返回 HTTP 代碼 304 並停止處理.