### laravel for qcloudapi

qcloudapi-sdk-php是为了让PHP开发者能够在自己的代码里更快捷方便的使用腾讯云的API而开发的SDK工具包。
laravel for qcloudapi 是对腾讯云官方SDK的封装

#### 更新历史

* [3/1]增加对HmacSHA1签名和HmacSHA256签名兼容的支持
* [7/15]增加Tdsql模块
* [7/6] 增加Cmem模块
* [6/17] 增加account模块
* [5/25] 添加Cbs、Snapshot和Scaling模块

#### 资源

* [公共参数](http://wiki.qcloud.com/wiki/%E5%85%AC%E5%85%B1%E5%8F%82%E6%95%B0)
* [API列表](http://wiki.qcloud.com/wiki/API)
* [错误码](http://wiki.qcloud.com/wiki/%E9%94%99%E8%AF%AF%E7%A0%81)

#### 入门

1. 申请安全凭证。
在第一次使用云API之前，用户首先需要在腾讯云网站上申请安全凭证，安全凭证包括 SecretId 和 SecretKey, SecretId 是用于标识 API 调用者的身份，SecretKey是用于加密签名字符串和服务器端验证签名字符串的密钥。SecretKey 必须严格保管，避免泄露。

2. 下载SDK，放入到您的程序目录。
使用方法请参考下面的例子。

#### 例子
```php
<?php

require 'vendor/autoload.php';
use QCLOUDAPI\QcloudApi;


error_reporting(E_ALL ^ E_NOTICE);


$config = array('SecretId'       => '你的secretId',
                'SecretKey'      => '你的secretKey',
                'RequestMethod'  => 'GET',
                'DefaultRegion'  => 'gz');

$cvm = QcloudApi::load(QcloudApi::MODULE_CVM, $config);

$package = array('offset' => 0, 'limit' => 3, 'SignatureMethod' =>'HmacSHA256');

$a = $cvm->DescribeInstances($package);
// $a = $cvm->generateUrl('DescribeInstances', $package);

if ($a === false) {
    $error = $cvm->getError();
    echo "Error code:" . $error->getCode() . ".\n";
    echo "message:" . $error->getMessage() . ".\n";
    echo "ext:" . var_export($error->getExt(), true) . ".\n";
} else {
    var_dump($a);
}

echo "\nRequest :" . $cvm->getLastRequest();
echo "\nResponse :" . $cvm->getLastResponse();
echo "\n";
```
