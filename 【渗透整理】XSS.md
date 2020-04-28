### 目录

- - - [XSS漏洞](https://blog.csdn.net/weixin_42742658/article/details/105820713#XSS_2)

    - - [XSS的分类：](https://blog.csdn.net/weixin_42742658/article/details/105820713#XSS_6)

      - - [一、存储型XSS：](https://blog.csdn.net/weixin_42742658/article/details/105820713#XSS_23)

        - - [存储式xss的概念：](https://blog.csdn.net/weixin_42742658/article/details/105820713#xss_26)
          - [存储型的xss的检测：](https://blog.csdn.net/weixin_42742658/article/details/105820713#xss_29)
          - [存储式xss的修复：](https://blog.csdn.net/weixin_42742658/article/details/105820713#xss_32)
          - [存储型判断：（与服务器有关）](https://blog.csdn.net/weixin_42742658/article/details/105820713#_38)

        - [二、反射型XSS：](https://blog.csdn.net/weixin_42742658/article/details/105820713#XSS_41)

        - - [反射式xss概念：](https://blog.csdn.net/weixin_42742658/article/details/105820713#xss_42)
          - [反射和存储型的区别：](https://blog.csdn.net/weixin_42742658/article/details/105820713#_45)
          - [反射型XSS的触发：（URL，在URL上插入一些语句）](https://blog.csdn.net/weixin_42742658/article/details/105820713#XSSURLURL_49)
          - [反射型xss的检测：](https://blog.csdn.net/weixin_42742658/article/details/105820713#xss_53)
          - [反射式xss的修复：](https://blog.csdn.net/weixin_42742658/article/details/105820713#xss_56)

        - [三、DOM型的XSS：](https://blog.csdn.net/weixin_42742658/article/details/105820713#DOMXSS_62)

        - - [Dom式xss的检测：](https://blog.csdn.net/weixin_42742658/article/details/105820713#Domxss_65)
          - [Dom式xss的修复：](https://blog.csdn.net/weixin_42742658/article/details/105820713#Domxss_68)



### XSS漏洞

把代码参数插入到html里，去完成其他的一些动作。获取用户的cookie，用途广泛。

#### XSS的分类：

**存储行/入库型/持久型**：   数据不深，可以直接存入数据库，个人资料编辑，从数据库读取数据
 **反射型/非入库型**： 需要发送链接过去
 **DOM式xss**：

也可以这样分类：
 1 反射型：经过后端，不经过数据库
 2 存储型：经过后端，经过数据库
 3 DOM型：不经过后端，dom型漏洞是基于文档对象模型的一种漏洞，是通过url传入数据去触发的

XSS原理：
 1 反射型：浏览器–后端–浏览器
 2 存储型：浏览器–后端–数据库–后端–浏览器
 3 DOM型xss：url–数据库
 注：反射型和dom型都需要在url加入js代码才能够触发

##### 一、存储型XSS：

通常是因为服务器端将用户输入的恶意脚本没有通过验证就只直接存储在数据库，并且每次通过调用数据库的方式，将数据呈现在浏览器上。则该xss跨站脚本攻击将一直存在。若其他用户访问该界面，则恶意脚本就会触发，用于盗取其他用户的私人信息。

###### 存储式xss的概念：

存储型xss，持久化，代码是存储在服务器中的，如在个人信息或者发表文章等地方，如果没有过滤或者过滤不严，那么恶意代码就会存储在服务器中，用户访问该页面时就会触发代码执行。

###### 存储型的xss的检测：

存储式的xss一般采用人工检测的方法，无法使用扫描器进行检测，因为扫描器无法准确的识别表单中的内容，也无法识别程序中的验证码，扫描也可能对程序本身造成不可逆的影响，所以在检测时一般会使用等代码进行测试，同时要注意输入点的长度限制，漏洞的利用，恶意代码的隐蔽性。

###### 存储式xss的修复：

1 对于用户提交的数据通过调用函数进行过滤，htmlspecialchars()函数将输出的内容进行html的编码。
 2 使用XSS Filter。
 3 黑名单和白名单结合使用
 4 设置httponly的属性

###### 存储型判断：（与服务器有关）

我们输入的数据被存到数据库中，用户看的时候是从数据库中拿出来的，所以我们可以写一些js代码插入到数据库，用户访问页面的时候，js执行一些操作，从而到达攻击的目的

##### 二、反射型XSS：

###### 反射式xss概念：

反射型xss也被称为非持久型xss。当用户访问一个带有xss代码的URL请求时，服务器端接受数据后处理，然后把带有xss代码的数据发送到浏览器，浏览器解析这段带有xss的代码的数据后，最终经造成xss漏洞。这个过程就像一次反射。故称反射型xss漏洞

###### 反射和存储型的区别：

存储型xss持久化，代码存在服务器中，用户访问时触发代码，这种xss比较危险，容易造成蠕虫，盗窃cookie等。
 反射型xss，非持久化，需要欺骗用户自己去点击链接才能触发xss代码（服务器中没有这样的页面或内容），一般出现在搜索页面。

###### 反射型XSS的触发：（URL，在URL上插入一些语句）

反射型xss漏洞属于交互触发漏洞，需要用户中主动点击才能触发，所以需要攻击者主动将包含payload的url发送给用户点击，只有在用户点开后，网页运行恶意代码，黑客才完成攻击。
 要让用户访问我们给的界面，然后反射到一些网站，拿到cookie。

###### 反射型xss的检测：

反射式xss用以通过人工检测和扫描工具两种方式，若URL中的参数内容在html页面中输出，则替换参数内容为等payload进行测试，如果弹窗，则存在反射性xss。而扫描器则是通过爬虫抓取网站中的链接，逐个替换参数，使用正则匹配特定字符串，若匹配成功，则存在xss漏洞。

###### 反射式xss的修复：

1 对于用户提交的数据通过调用函数进行过滤，htmlspcialchars()函数将输出的内容进行html编码。
 2 使用xss filter
 3 白名单和黑名单结合使用
 4 设置httponly

##### 三、DOM型的XSS：

**dom式的xss其实是一种特殊的反射式xss**，它是基于dom文档对象模型的一种漏洞。客户端的脚本程序可以通过dom来动态修改页面内容，从客户端获取dom中的数据并保存在本地执行。基于这个特性，就可以利用js脚本来实现xss漏洞的利用。（输入框里的代码被js（js运行在浏览器上）拿出来执行了，从而造成了危害）

###### Dom式xss的检测：

dom式sxx可以用人工和扫描器两种方式检测，在URL结尾处加入#,等payload进行测试，如果payload在dom中运行弹窗，则存在dom式sxx漏洞。而扫描器则是则是通过爬虫去抓去网站中的链接，逐个在连接结尾加入payload。

###### Dom式xss的修复：

1 限制能够跳转页面的协议
 2 严格限制跳转的范围
 3 写入页面前先转义
 4 参考/使用filter.js

by 久违 2018.8