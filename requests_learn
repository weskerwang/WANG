# -*- coding: utf-8 -*-
import requests
"""官方中文文档：
https://docs.python-requests.org/zh_CN/latest/user/quickstart.html
"""

"""
|——————————————————————————————————————————————————————|
|                                                      |
|                        快速上手                       |
|                                                      |
|——————————————————————————————————————————————————————|
"""

#----------------------   发送请求   ------------------------#
# url = 'https://finance.sina.com.cn/'
# r = requests.get(url)
# print(type(r))
""" requests其他请求方式：
r = requests.post('http://httpbin.org/post', data = {'key':'value'})
r = requests.put('http://httpbin.org/put', data = {'key':'value'})
r = requests.delete('http://httpbin.org/delete')
r = requests.head('http://httpbin.org/get')
r = requests.options('http://httpbin.org/get')
"""


#----------------------   手工构建URL   ------------------------#
# payload1 = {'key1': 'value1', 'key2': 'value2'}
# r1 = requests.get('http://httpbin.org/get', params = payload1)
# print(r1.url)
# payload2 = {'key1': 'value1', 'key2': ['value2', 'value3']}
# r2 = requests.get('http://httpbin.org/get', params = payload2)
# print(r2.url)
""" 手工构建url输出结果：
输出1：http://httpbin.org/get?key1=value1&key2=value2
输出2：http://httpbin.org/get?key1=value1&key2=value2&key2=value3

"""


#----------------------   读取响应内容   ------------------------#
# url = 'https://finance.sina.com.cn/'
# r = requests.get(url)
# print(r.encoding) 
# r.encoding = 'utf-8' # 你可以找出 Requests 使用了什么编码，并且能够使用 r.encoding 属性来改变它
# print(r.text) # 打印响应内容
# with open('sina_fin.txt', 'w') as f:
#   f.write(r.text) # 将响应内容保存到txt


#----------------------   JSON 响应内容   ------------------------#
# r = requests.get('https://finance.sina.com.cn/')
# r.json()
"""注意：
如果 JSON 解码失败， r.json() 就会抛出一个异常。例如，响应内容是 401 (Unauthorized)，尝试访问 r.json() 将会抛出 ValueError: No JSON object could be decoded 异常。
需要注意的是，成功调用 r.json() 并不意味着响应的成功。有的服务器会在失败的响应中包含一个 JSON 对象（比如 HTTP 500 的错误细节）。这种 JSON 会被解码返回。要检查请求是否成功，请使用 r.raise_for_status() 或者检查 r.status_code 是否和你的期望相同。
"""


#----------------------   定制请求头   ------------------------#
# url = 'https://finance.sina.com.cn/'
# headers = {'user-agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.110 Safari/537.36'}
# r = requests.get(url, headers = headers)


#----------------------   更加复杂的 POST 请求   ------------------------#
# payload = {'key1': 'value1', 'key2': 'value2'} # 使用字典传递表单数据
# payload = (('key1', 'value1'), ('key1', 'value2')) # 你还可以为 data 参数传入一个元组列表。在表单中多个元素使用同一 key 的时候，这种方式尤其有效
# r = requests.post("http://httpbin.org/post", data=payload)
# print(r.text)

# url = 'https://api.github.com/some/endpoint'
# payload = {'some': 'data'} # 此处除了可以自行对 dict 进行编码，你还可以使用 json 参数直接传递，然后它就会被自动编码。
# r = requests.post(url, json=payload)


#----------------------   响应头   ------------------------#
# url = 'https://finance.sina.com.cn/'
# r = requests.get(url)
# print((r.headers)) # 查看响应头
# print(r.headers['content-type']) 
# print(r.headers.get('content-type'))# HTTP 头部是大小写不敏感的。因此，我们可以使用任意大写形式来访问这些响应头字段。


#----------------------   Cookie   ------------------------#
""" cookies参数
要想发送你的cookies到服务器，可以使用 cookies 参数
"""
# url = 'https://finance.sina.com.cn/'
# cookies = dict(mycookie = 'this_is_my_cookie') 
# r = requests.get(url, cookies = cookies) # 传入一个cookies字典
# print(r.cookies) # 如果某个响应中包含一些 cookie，你可以快速访问它们
""" RequestsCookieJar
Cookie 的返回对象为 RequestsCookieJar，它的行为和字典类似，但接口更为完整，适合跨域名跨路径使用。你还可以把 Cookie Jar 传到 Requests 中。
"""
# jar = requests.cookies.RequestsCookieJar()
# jar.set('tasty_cookie', 'yum', domain='httpbin.org', path='/cookies')
# url = 'http://httpbin.org/cookies'
# r = requests.get(url, cookies=jar)
# print(r.text)


#----------------------   重定向与请求历史   ------------------------#
""" 重定向与请求历史:
默认情况下，除了 HEAD, Requests 会自动处理所有重定向。
可以使用响应对象的 history 方法来追踪重定向。
Response.history 是一个 Response 对象的列表，为了完成请求而创建了这些对象。这个对象列表按照从最老到最近的请求进行排序。
例如，Github 将所有的 HTTP 请求重定向到 HTTPS：
"""
# r = requests.get('http://github.com')
# print(r.url, '\n', r.status_code, '\n', r.history)
""" 
allow_redirects 参数<启用>和<禁用>重定向处理:
"""
# r = requests.get('http://github.com', allow_redirects=False)
# print(r.status_code, r.history)
# r = requests.head('http://github.com', allow_redirects=True)
# print(r.status_code, r.history)


#----------------------   超时 timeout   ------------------------#
""" 超时:
你可以告诉 requests 在经过以 timeout 参数设定的秒数时间之后停止等待响应。基本上所有的生产代码都应该使用这一参数。如果不使用，你的程序可能会永远失去响应。

timeout 仅对连接过程有效，与响应体的下载无关。 timeout 并不是整个下载响应的时间限制，而是如果服务器在 timeout 秒内没有应答，将会引发一个异常（更精确地说，是在 timeout 秒内没有从基础套接字上接收到任何字节的数据时）If no timeout is specified explicitly, requests do not time out.
"""
# requests.get('https://finance.sina.com.cn/', timeout=0.0001)


#----------------------   错误与异常   ------------------------#
"""
遇到网络问题（如：DNS 查询失败、拒绝连接等）时，Requests 会抛出一个 ConnectionError 异常。

如果 HTTP 请求返回了不成功的状态码， Response.raise_for_status() 会抛出一个 HTTPError 异常。

若请求超时，则抛出一个 Timeout 异常。

若请求超过了设定的最大重定向次数，则会抛出一个 TooManyRedirects 异常。

所有Requests显式抛出的异常都继承自 requests.exceptions.RequestException 。
"""




"""
|——————————————————————————————————————————————————————|
|                                                      |
|                        高级用法                       |
|                                                      |
|——————————————————————————————————————————————————————|
"""

#----------------------   会话对象   ------------------------#
""" 说明：
会话对象让你能够跨请求保持某些参数。它也会在同一个 Session 实例发出的所有请求之间保持 cookie， 期间使用 urllib3 的 connection pooling 功能。所以如果你向同一主机发送多个请求，底层的 TCP 连接将会被重用，从而带来显著的性能提升。 (参见 HTTP persistent connection).
"""
# 跨请求保持cookie
# s = requests.Session()
# s.get('http://httpbin.org/cookies/set/sessioncookie/123456789')
# r = s.get("http://httpbin.org/cookies") 
# print(r.text)
# # 会话也可用来为请求方法提供缺省数据。这是通过为会话对象的属性提供数据来实现的：
# s = requests.Session()
# s.auth = ('user', 'pass')
# s.headers.update({'x-test': 'ture'})
# s.get('http://httpbin.org/headers', headers={'x-test2': 'true'})
""" 注意：
不过需要注意，就算使用了会话，方法级别的参数也不会被跨请求保持。下面的例子只会和第一个请求发送 cookie ，而非第二个：
s = requests.Session()
r = s.get('http://httpbin.org/cookies', cookies={'from-my': 'browser'})
print(r.text)
  # '{"cookies": {"from-my": "browser"}}'
r = s.get('http://httpbin.org/cookies')
print(r.text)
  # '{"cookies": {}}'
"""


#----------------------   请求与响应对象   ------------------------#
""" 说明：
任何时候进行了类似 requests.get() 的调用，你都在做两件主要的事情。其一，你在构建一个 Request 对象， 该对象将被发送到某个服务器请求或查询一些资源。其二，一旦 requests 得到一个从服务器返回的响应就会产生一个 Response 对象。该响应对象包含服务器返回的所有信息，也包含你原来创建的 Request 对象。
"""
# r = requests.get('http://en.wikipedia.org/wiki/Monty_Python')
# print(r.content.decode())
# # 如果想得到发送到服务器的请求的头部，我们可以简单地访问该请求，然后是该请求的头部：
# print(r.request.headers)


#----------------------   准备的请求   ------------------------#
""" 说明：
当你从 API 或者会话调用中收到一个 Response 对象时，request 属性其实是使用了 PreparedRequest。有时在发送请求之前，你需要对 body 或者 header （或者别的什么东西）做一些额外处理，下面演示了一个简单的做法：
"""
# s = requests.Session()
# req = requests.Request('GET', url, data = data, headers = headers)
# prepped = req.prepare()
# resp = s.send(prepped, stream=stream, verify=verify, proxies=proxies, cert=cert, timeout=timeout)
# print(resp.status_code)
"""
由于你没有对 Request 对象做什么特殊事情，你立即准备和修改了 PreparedRequest 对象，然后把它和别的参数一起发送到 requests.* 或者 Session.*。
然而，上述代码会失去 Requests Session 对象的一些优势， 尤其 Session 级别的状态，例如 cookie 就不会被应用到你的请求上去。要获取一个带有状态的 PreparedRequest， 请用 Session.prepare_request() 取代 Request.prepare() 的调用，如下所示：
"""
# from requests import Request, Session
# s = Session()
# req = Request('GET', url,
#   data = data,
#   headers = headers
# )
# prepped = s.prepare_request(req)
# resp = s.send(prepped,
#   stream = stream,
#   verify = verify,
#   proxies = proxies,
#   cert = cert,
#   timeout = timeout
# )
# print(resp.status_code)


#----------------------   设置代理IP   ------------------------#
""" 说明：
如果需要使用代理，你可以通过为任意请求方法提供 proxies 参数来配置单个请求:
"""
# proxies = {
#   "http": "http://10.10.1.10:3128",
#   "https": "http://10.10.1.10:1080",
# }
# resp = requests.get("http://example.org", proxies = proxies)


#----------------------   HTTP 动词   ------------------------#
""" 说明：
Requests 提供了几乎所有HTTP动词的功能：GET、OPTIONS、HEAD、POST、PUT、PATCH、DELETE。以下内容为使用 Requests 中的这些动词以及 Github API 提供了详细示例。

我将从最常使用的动词 GET 开始。HTTP GET 是一个幂等方法，从给定的 URL 返回一个资源。因而，当你试图从一个 web 位置获取数据之时，你应该使用这个动词。
"""


#----------------------   响应头链接字段   ------------------------#
""" 说明：
许多 HTTP API 都有响应头链接字段的特性，它们使得 API 能够更好地自我描述和自我显露。"""
r = requests.head("https://api.github.com/users/kennethreitz/repos?page=1&per_page=10")
# Requests 会自动解析这些响应头链接字段，并使得它们非常易于使用。
print(r.links['next'])
print(r.links['last'])
