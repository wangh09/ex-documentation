# API Signature

## API Key and Secret

A user can request API key and secret. Both are secure random string.
用户可以申请API Key和Secret。Key和Secret均为随机字符构成的字符串串。

## Sign Request

Please do following steps to sign a request:
要对一个HTTP请求进行签名，需要以下步骤：

1. prepare a byte buffer as payload that will be signed.
1. 准备一个byte缓冲区作为待签名的payload

2. put each lines into the buffer.
2. 将每一行添加至缓冲区

For a get request: `https://www.hostname.com/orders?id=12345&filter=byName`:
例如，对于GET请求：`https://www.hostname.com/orders?id=12345&filter=byName`:

```
GET\n
www.hostname.com\n
/orders\n
filter=byName&id=12345\n
API-KEY: AbC123XyZ\n
API-SIGNATURE-METHOD: HmacSHA256\n
API-SIGNATURE-VERSION: 1\n
API-TIMESTAMP: 1234500000\n
```

For a post request, add the request body to the end if any:
对于POST请求，如果有body，还需要把body附加到最后：

```
POST\n
www.hostname.com\n
/orders\n
\n
API-KEY: AbC123XyZ\n
API-SIGNATURE-METHOD: HmacSHA256\n
API-SIGNATURE-VERSION: 1\n
API-TIMESTAMP: 1234500000\n
posted binary data...
```

Then calculate the HmacSHA256 using apiSecret as secret key:
通过API Secret计算该payload的HmacSHA256：

```
signature = HmacSHA256(payload, apiSecret)
```

Add header `API-SIGNATURE: abc123ff0011...` as signature.
将计算结果以`API-SIGNATURE: abc123ff0011...`添加到Header。

## NOTES

Request method: support `GET` or `POST`, all UPPERCASE.
请求方法必须是`GET`或`POST`，需要全部大写。

域名：全部小写。
Host name: all lowercase.

路径：大小写敏感，注意结尾没有`?`
URI: case sensitive. NO `?` at end.

Parameters:
请求参数：


build a list like `['key1=value1', 'key2=value2', 'key3=xxx']`. sorted the list.
首先，构造一个List，类似：`['key1=value1', 'key2=value2', 'key3=xxx']`，并对List排序；

using `key1=value1&key2=value2`, both keys and values are case-sensitive. NOTE the value is original string NOT url-encoded.
将排序后的List构造为`key1=value1&key2=value2`，注意Key和Value均大小写敏感，并且，Value*不要*进行URL编码。

NOTE: for POST request there is no parameters, and an EMPTY line MUST be added.
注意：对于POST请求，通常没有参数，需要添加一个空行。

Headers:
请求头：

The headers starts with `API-` must be included.
所有以`API-`开头的Header都必须被包含至payload中。

API-Key: `<your api-key>`, MUST;
API-Signature-Method: HmacSHA256. MUST be exactly `HmacSHA256`;
API-Signature-Version: 1. MUST be exactly `1`;
API-Timestamp: 123000000. MUST. The current timestamp in milliseconds;
API-Unique-ID: `any-unique-string`, optional, must be 1~40 chars of random string if provided. Suggest random UUID or timestamp + random number.

Header names are UPPERCASE when calculate hash. Header values are case-sensitive.
请求头名称必须全部大写，请求头的值是大小写敏感的。

Each line ends with `\n`, NOT `\r\n`.
每行以`\n`结束，不是`\r\n`。

If a POST request has body, append the body at last, but NO `\n` after body.
如果是POST请求，且含有body，注意附加body后不要添加`\n`。
