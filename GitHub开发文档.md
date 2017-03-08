### GitHub api文档 V3

***

原文地址：

> https://developer.github.com/v3/

***

#### 请求实例

基于https 协议，返回json格式，请求地址：

```
https://api.github.com
```

返回日期格式:

```
YYYY-MM-DDTHH:MMSSZ
```

获取整列数据，例：获取octokit的repositories数据列：

```shell
$ GET /orgs/octokit/repos
```

获取单独数据：

```shell
$ GET /repos/octokit/octokit.rb
```

请求参数可选

GET请求示例（vgm, redcarpet的值对应`:owner`、`:repo`参数）：

```shell
$ curl -i "https://api.github.com/repos/vmg/redcarpet/issues?state=closed"
```

对于 POST, PATCH, PUT, 和 DELETE 请求，请求参数不包含在url中，包含在 'application/json'的json字段内：

```shell
$ curl -i -u username -d '{"scopes":["public_repo"]}' https://api.github.com/authorizations
```

查看尾指针（endpoint）种类：

```shell
$ curl https://api.github.com
```

***

#### 客户端错误类型

若发送一个无效的json将返回`404`

```json
HTTP/1.1 400 Bad Request
Content-Length: 35

{"message":"Problems parsing JSON"}
```

若发送一个错误的json类型，将返回`400`

```json
HTTP/1.1 400 Bad Request
Content-Length: 40

{"message":"Body should be a JSON object"}
```

若发送一个无效的fields，将返回`422`

```json
HTTP/1.1 422 Unprocessable Entity
Content-Length: 149

{
  "message": "Validation Failed",
  "errors": [
    {
      "resource": "Issue",
      "field": "title",
      "code": "missing_field"
    }
  ]
}
```
常用错误码
| error name     | description |
| -------------- | ----------- |
| missing        | 资源不存在       |
| missing_field  | field不存在    |
| invalid        | 格式化的field无效 |
| already_exists | 资源值冲突       |
***

#### HTTP 重定向

| 状态码     | 描述    |
| :------ | ----- |
| 301     | 重定向参数 |
| 302，307 | 临时重定向 |

***

#### HTTP verb

| verb   | description    |
| ------ | -------------- |
| HEAD   | header info    |
| GET    | 取回资源           |
| POST   | 创建资源           |
| PATCH  | 升级资源（部分json数据） |
| PUT    | 替换资源或集合        |
| DELETE | 删除资源           |

#### 验证

基本验证：

```shell
$ curl -u "username" https://api.github.com
```

授权（发送一个header）：

```shell
$ curl -H "Authorization: token OAUTH-TOKEN" https://api.github.com
```

授权（作为参数发送）：

```shell
$ curl https://api.github.com/?access_token=OAUTH-TOKEN
```

授权（key/secret）:

```shell
$ curl 'https://api.github.com/users/whatever?client_id=xxxx&client_secret=yyyy'
```

登录验证：用一个无效的证书验证将返回`401`：

```shell
$ curl -i https://api.github.com -u foo:bar
HTTP/1.1 401 Unauthorized

{
  "message": "Bad credentials",
  "documentation_url": "https://developer.github.com/v3"
}
```

上述请求过后，api将暂时拒绝用户验证：

```shell
$ curl -i https://api.github.com -u valid_username:valid_password
HTTP/1.1 403 Forbidden

{
  "message": "Maximum number of login attempts exceeded. Please try again later.",
  "documentation_url": "https://developer.github.com/v3"
}

```

***

####  Hypermedia （超媒体）

所有的资源都有一个或多个`*_url`属性连接至其他资源，若能提供明确的URL，客户端将不用再自己去构造一个URL，推荐客户端使用这种方式

uri模板（可扩展）：

```shell
>> tmpl = URITemplate.new('/notifications{?since,all,participating}')
>> tmpl.expand
=> "/notifications"

>> tmpl.expand :all => 1
=> "/notifications?all=1"

>> tmpl.expand :all => 1, :participating => 1
=> "/notifications?all=1&participating=1"
```

***

#### 页码

请求时默认返回30条内容，也可以通过参数指定页码

`?page`指定特定页码，`?per_page`指定页数

```shell
$ curl 'https://api.github.com/user/repos?page=2&per_page=100'
```

不指定`page`时默认返回第一页。

页码信息包含在链接头内（断行也被包含在内，增加可读性）：

```
Link: <https://api.github.com/user/repos?page=3&per_page=100>; rel="next",
  <https://api.github.com/user/repos?page=50&per_page=100>; rel="last"
```

rel 可能的值：

| name  | description |
| ----- | ----------- |
| next  | 链接到下一页      |
| last  | 链接到最后一页     |
| first | 链接到第一页      |
| prev  | 链接到上一页      |

***

#### 限制

使用基础的验证或授权，每小时可进行5000次请求；对于未验证的请求，每小时可进行60次请求，并且所有请求都将关联到你的ip地址，而非用户的请求

可以查看最近的限制信息：

```shell
$ curl -i https://api.github.com/users/whatever
HTTP/1.1 200 OK
Date: Mon, 01 Jul 2013 17:27:06 GMT
Status: 200 OK
X-RateLimit-Limit: 60
X-RateLimit-Remaining: 56
X-RateLimit-Reset: 1372700873
```

| name                  | description      |
| --------------------- | ---------------- |
| X-RateLimit-Limit     | 每小时最大的请求次数       |
| X-RateLimit-Remaining | 剩余请求次数           |
| X-RateLimit-Reset     | 最近一次请求的时间（UTC秒数） |

超过限制时会返回错误

```json
HTTP/1.1 403 Forbidden
Date: Tue, 20 Aug 2013 14:50:41 GMT
Status: 403 Forbidden
X-RateLimit-Limit: 60
X-RateLimit-Remaining: 0
X-RateLimit-Reset: 1377013266

{
   "message": "API rate limit exceeded for xxx.xxx.xxx.xxx. (But here's the good news: Authenticated requests get a higher rate limit. Check out the documentation for more details.)",
   "documentation_url": "https://developer.github.com/v3/#rate-limiting"
}
```

通过app的 ID 和 secret 为授权app增加未验证的访问限制

```shell
$ curl -i 'https://api.github.com/users/whatever?client_id=xxxx&client_secret=yyyy'
HTTP/1.1 200 OK
Date: Mon, 01 Jul 2013 17:27:06 GMT
Status: 200 OK
X-RateLimit-Limit: 5000
X-RateLimit-Remaining: 4966
X-RateLimit-Reset: 1372700873
```

这个方法只用于server-to-server的访问。可以申请增加访问次数

若程序触发了这个限制，将收到如下消息：

```json
HTTP/1.1 403 Forbidden
Content-Type: application/json; charset=utf-8
Connection: close

{
  "message": "You have triggered an abuse detection mechanism and have been temporarily blocked from content creation. Please retry your request again later.",
  "documentation_url": "https://developer.github.com/v3#abuse-rate-limits"
}
```

***

#### 用户代理请求 

所有的请求必须包含一个有效的`User-Agent`header，若没有，请求将会被拒绝。用用户名和应用程序名作为`User-Agent`header的值。如：

```
User-Agent: Awesome-Octocat-App
```

若提供一个无效的header，将收到如下错误：

```shell
$ curl -iH 'User-Agent: ' https://api.github.com/meta
HTTP/1.0 403 Forbidden
Connection: close
Content-Type: text/html

Request forbidden by administrative rules.
Please make sure your request has a User-Agent header.
Check https://developer.github.com for other possible causes.
```

***

#### 有条件的请求

大多数响应返回一个`ETag`header。也有许多响应也返回一个`Last-Modified`header。可以用这个header做后续对各自使用了`If-None-Match`和`If-Modified-Since`header的请求。若资源为改变，则服务器将返回`304 Not Modified`

* Note: 做一次条件请求并返回304时，不消耗访问次数，因此这个行为无论何时都被鼓励使用 

```shell
$ curl -i https://api.github.com/user
HTTP/1.1 200 OK
Cache-Control: private, max-age=60
ETag: "644b5b0155e6404a9cc4bd9d8b1ae730"
Last-Modified: Thu, 05 Jul 2012 15:31:30 GMT
Status: 200 OK
Vary: Accept, Authorization, Cookie

X-RateLimit-Limit: 5000
X-RateLimit-Remaining: 4996
X-RateLimit-Reset: 1372700873


$ curl -i https://api.github.com/user -H 'If-None-Match: "644b5b0155e6404a9cc4bd9d8b1ae730"'
HTTP/1.1 304 Not Modified
Cache-Control: private, max-age=60
ETag: "644b5b0155e6404a9cc4bd9d8b1ae730"
Last-Modified: Thu, 05 Jul 2012 15:31:30 GMT
Status: 304 Not Modified
Vary: Accept, Authorization, Cookie

X-RateLimit-Limit: 5000
X-RateLimit-Remaining: 4996
X-RateLimit-Reset: 1372700873


$ curl -i https://api.github.com/user -H "If-Modified-Since: Thu, 05 Jul 2012 15:31:30 GMT"
HTTP/1.1 304 Not Modified
Cache-Control: private, max-age=60
Last-Modified: Thu, 05 Jul 2012 15:31:30 GMT
Status: 304 Not Modified
Vary: Accept, Authorization, Cookie

X-RateLimit-Limit: 5000
X-RateLimit-Remaining: 4996
X-RateLimit-Reset: 1372700873
```

***

#### 源资源（origin resource sharing）分享

例`http://example.com`：

```shell
$ curl -i https://api.github.com -H "Origin: http://example.com"
HTTP/1.1 302 Found
Access-Control-Allow-Origin: *
Access-Control-Expose-Headers: ETag, Link, X-GitHub-OTP, X-RateLimit-Limit, X-RateLimit-Remaining, X-RateLimit-Reset, X-OAuth-Scopes, X-Accepted-OAuth-Scopes, X-Poll-Interval
Access-Control-Allow-Credentials: true
```

CORS preflight 请求：

```shell
$ curl -i https://api.github.com -H "Origin: http://example.com" -X OPTIONS
HTTP/1.1 204 No Content
Access-Control-Allow-Origin: *
Access-Control-Allow-Headers: Authorization, Content-Type, If-Match, If-Modified-Since, If-None-Match, If-Unmodified-Since, X-GitHub-OTP, X-Requested-With
Access-Control-Allow-Methods: GET, POST, PATCH, PUT, DELETE
Access-Control-Expose-Headers: ETag, Link, X-GitHub-OTP, X-RateLimit-Limit, X-RateLimit-Remaining, X-RateLimit-Reset, X-OAuth-Scopes, X-Accepted-OAuth-Scopes, X-Poll-Interval
Access-Control-Max-Age: 86400
Access-Control-Allow-Credentials: true
```

***

#### JSON-P 回调

向任意GET请求发送`？callback`的结果包含在一个JSON函数中，这是浏览器需要将GitHub网页嵌入时典型的用法，响应值作为正则API包括相同的数据输出，包括相关的HTTP Header信息。

```shell
$ curl https://api.github.com?callback=foo

/**/foo({
  "meta": {
    "status": 200,

    "X-RateLimit-Limit": "5000",
    "X-RateLimit-Remaining": "4966",
    "X-RateLimit-Reset": "1372700873",

    "Link": [ // pagination headers and other links
      ["https://api.github.com?page=2", {"rel": "next"}]
    ]
  },
  "data": {
    // the data
  }
})
```

可以用JavaScript来处理这个回调：

```html
<html>
<head>
<script type="text/javascript">
function foo(response) {
  var meta = response.meta;
  var data = response.data;
  console.log(meta);
  console.log(data);
}

var script = document.createElement('script');
script.src = 'https://api.github.com?callback=foo';

document.getElementsByTagName('head')[0].appendChild(script);
</script>
</head>

<body>
  <p>Open up your browser's console.</p>
</body>
</html>
```

所有的headers都是相同的字符串值作为HTTP Header伴随着重要的表达式：Link：

```html
Link: <url1>; rel="next", <url2>; rel="foo"; bar="baz"
```

回调输出示例：

```json
{
  "Link": [
    [
      "url1",
      {
        "rel": "next"
      }
    ],
    [
      "url2",
      {
        "rel": "foo",
        "bar": "baz"
      }
    ]
  ]
}
```

***

#### Timezones时区

规则：

跟去ISO 8601规则，时间格式：`2014-02-27T15:05:06+01:00`

使用时区header`Time-Zone`

```shell
$ curl -H "Time-Zone: Europe/Amsterdam" -X POST https://api.github.com/repos/github/linguist/contents/new_file.md
```

若在一次授权请求中未包含`Time-Zone`header，则使用最后一次的授权用户时区。

UTC

如果这一步未得到任何结果，则使用UTC作为时区创建提交。








