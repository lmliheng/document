可以添加一个新的PHP文件（例如login_with_wechat.php），用于处理使用微信公众号登录网页的请求
```php
login_with_wechat.php

<?php
// 获取access_token的URL
$url = "https://api.weixin.qq.com/cgi-bin/token?grant_type=client_credential&appid=APPID&secret=APPSECRET";

// 发送GET请求获取access_token
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, $url);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
$response = curl_exec($ch);
curl_close($ch);

// 解析响应
$result = json_decode($response, true);

// 检查是否获取到access_token
if (isset($result['access_token'])) {
    // 将access_token和过期时间存储到文件中
    file_put_contents('access_token.json', json_encode($result));
    echo "Access token saved successfully.";
} else {
    echo "Failed to get access token.";
}
```
请将APPID和APPSECRET替换为您的实际值。

要使用此代码，请将其保存为`login_with_wechat.php`文件，并确保已安装PHP和cURL扩展。然后，您可以通过运行php login_with_wechat.php命令来获取access_token并将其保存到access_token.json文件中。

为了在您的index.php文件中使用`access_token`，您可以从`access_token.json`文件中读取它。在index.php文件中，您可以添加以下代码来获取access_token：
```php
$access_token_data = json_decode(file_get_contents('access_token.json'), true);
$access_token = $access_token_data['access_token'];
```
然后，您可以在调用微信公众号API时使用$access_token变量。请注意，您需要确保access_token.json文件存在并包含有效的access_token数据。您可以使用计划任务（如cron job）定期运行login_with_wechat.php脚本以更新access_token。

接下来，我们需要在index.php文件中添加一个新的方法来处理微信公众号登录。在wechatCallBackapiTest类中，添加一个名为loginWithWechat的方法：
```php
public function loginWithWechat($code)
{
    // 获取access_token和openid
    $url = "https://api.weixin.qq.com/sns/oauth2/access_token?appid=APPID&secret=APPSECRET&code=$code&grant_type=authorization_code";
    $ch = curl_init();
    curl_setopt($ch, CURLOPT_URL, $url);
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
    $response = curl_exec($ch);
    curl_close($ch);
    $result = json_decode($response, true);

    if (isset($result['access_token']) && isset($result['openid'])) {
        $access_token = $result['access_token'];
        $openid = $result['openid'];

        // 获取用户信息
        $url = "https://api.weixin.qq.com/sns/userinfo?access_token=$access_token&openid=$openid&lang=zh_CN";
        $ch = curl_init();
        curl_setopt($ch, CURLOPT_URL, $url);
        curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
        $response = curl_exec($ch);
        curl_close($ch);
        $user_info = json_decode($response, true);

        if (isset($user_info['nickname'])) {
            // 登录成功，处理用户信息
            // ...
        } else {
            // 登录失败，返回错误信息
            return "Failed to get user info.";
        }
    } else {
        return "Failed to get access token and openid.";
    }
}
```
请将APPID和APPSECRET替换为您的实际值。

最后，在index.php文件中，您需要处理用户从微信公众号登录后返回的code参数。在index.php文件中，添加以下代码：
```php
if (isset($_GET['code'])) {
    $code = $_GET['code'];
    $wechat = new wechatCallBackapiTest();
    $result = $wechat->loginWithWechat($code);
    echo $result;
}

```
这将处理从微信公众号登录后返回的code参数，并调用loginWithWechat方法。如果登录成功，您可以在loginWithWechat方法中处理用户信息，例如将其存储到数据库或会话中。