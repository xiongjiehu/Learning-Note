---
description: web
---

# Requests@Beautiful Soup

Requests 和 Beautiful Soup 是两个常用于网络数据获取和解析的 Python 库。

Requests：是一个简洁而优雅的HTTP库，用于发送各种HTTP请求。它允许你以简单的方式发送HTTP请求，并处理响应数据。Requests 支持HTTP协议的各种方法（GET、POST、PUT、DELETE等），并提供了简单易用的API，使得发送HTTP请求变得非常方便。你可以使用 Requests 来获取网页内容、提交表单数据、发送文件等等。

Beautiful Soup：是一个用于从HTML或XML文件中提取数据的Python库，它提供了一种简单的方式来遍历HTML或XML文档的结构，并从中提取出感兴趣的信息。Beautiful Soup可以解析HTML或XML文档，并为我们提供了一组方法来遍历文档树、搜索特定元素、提取数据等。它可以处理不规范的HTML，使得即使在标记存在缺陷的情况下也能够正常解析。

Requests

请求操作

```
r = requests.post('http://httpbin.org/post', data = {'key':'value'})
r = requests.put('http://httpbin.org/put', data = {'key':'value'})
r = requests.delete('http://httpbin.org/delete')
r = requests.head('http://httpbin.org/get')
r = requests.options('http://httpbin.org/get')

```

构造请求并传递参数

```
>>> payload = {'key1': 'value1', 'key2': 'value2'}
>>> r = requests.get("http://httpbin.org/get", params=payload)
>>> payload = {'key1': 'value1', 'key2': ['value2', 'value3']}
>>> r = requests.get('http://httpbin.org/get', params=payload)
>>> print(r.url)
http://httpbin.org/get?key1=value1&key2=value2&key2=value3
```

响应内容操作（读取、改变编码、二进制、JSON、raw）

```
>>> r.text
u'[{"repository":{"open_issues":0,"url":"https://github.com/...
#二进制
>>> r.content
>>> r.json()
>>> r = requests.get('https://api.github.com/events', stream=True)
>>> r.raw
#改变编码
>>> r.encoding
'utf-8'
>>> r.encoding = 'ISO-8859-1'

```

构造请求头（可以从浏览器F12 Network快速获得）

```
>>> url = 'https://api.github.com/some/endpoint'
#协议头部大小不敏感
>>> headers = {'user-agent': 'my-app/0.0.1'} 
>>> r = requests.get(url, headers=headers)
```

状态码操作

```
>>> r = requests.get('http://httpbin.org/get')
>>> r.status_code
200

#内置引用
>>> r.status_code == requests.codes.ok
True

#状态码错误时抛出异常
>>> bad_r = requests.get('http://httpbin.org/status/404')
>>> bad_r.status_code
404

>>> bad_r.raise_for_status()
Traceback (most recent call last):
  File "requests/models.py", line 832, in raise_for_status
    raise http_error
requests.exceptions.HTTPError: 404 Client Error
```

响应头操作

```
>>> r.headers
>>> r.headers['Content-Type']
```

Cookie操作

```
>>> r.cookies['example_cookie_name']

#发送cookie
>>> url = 'http://httpbin.org/cookies'
>>> cookies = dict(cookies_are='working')

>>> r = requests.get(url, cookies=cookies)
>>> r.text
'{"cookies": {"cookies_are": "working"}}'

```

### 重定向与请求历史、超时限制

错误与异常类型

```
网络问题（如：DNS 查询失败、拒绝连接等）
ConnectionError
不成功的状态码
Response.raise_for_status() 会抛出一个 HTTPError 异常
请求超时
Timeout 异常
请求超过了设定的最大重定向次数
TooManyRedirects 异常
requests.exceptions.RequestException 
```

会话对象

Python的requests库中的Session类是一个会话对象，它可以在多个请求之间保持一些参数和状态。通过创建一个Session对象，可以在该对象上执行多个请求，这样可以更有效地利用网络资源。

1. 自动管理cookies：Session对象会自动处理请求和响应中的cookies，可以自动保存和发送cookies，无需手动处理。
2. 保持参数和状态：Session对象可以在多个请求之间保持一些参数和状态，例如HTTP头、身份验证信息等。这样可以避免在每个请求中重复设置这些参数。
3. 使用连接池：Session对象使用底层的urllib3库，可以使用连接池来管理和重用HTTP连接，提高性能。

使用Session对象的一般流程如下：

1. 创建一个Session对象：session = requests.Session()
2. 使用Session对象发送请求：response = session.get(url)
3. 处理响应：可以像使用requests库一样处理响应，例如获取响应内容、状态码等。
4. 使用Session对象发送其他请求：可以继续使用session对象发送其他请求，它会自动处理cookies和其他参数。
5. 关闭会话：session.close()，如果不主动关闭，会话会一直保持。支持上下文管理器，不需要显示close

```
# 创建一个会话对象
with requests.Session() as session:
    # 发送多个请求，会话对象会自动管理 cookie、身份验证信息等
    response1 = session.get('https://api.example.com/login')
    response2 = session.post('https://api.example.com/login', data={'username': 'user', 'password': 'pass'})
    response3 = session.get('https://api.example.com/data')
```



Beautiful Soup







































