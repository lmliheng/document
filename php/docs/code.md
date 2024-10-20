### 响应文件
```php
<?php

function checkSignature()
{
    $signature = $_GET["signature"];
    $timestamp = $_GET["timestamp"];
    $nonce = $_GET["nonce"];

    $token = TOKEN;
    $tmpArr = array(TOKEN, $timestamp, $nonce);
    sort($tmpArr, SORT_STRING);
    $tmpStr = implode($tmpArr);
    $tmpStr = sha1($tmpStr);

    if ($tmpStr == $signature) {
        return true;
    } else {
        return false;
    }
}

if (checkSignature()) {
    echo $_GET["echostr"];
} else {
    echo "error";
}
?>

```
使用web服务器部署php，验证URL有效性成功后即服务器配置生效，即接入生效




