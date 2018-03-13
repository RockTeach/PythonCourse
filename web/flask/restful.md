# RESTful API

---

### 什么是REST

一种软件架构风格、设计风格、而不是标准，只是提供了一组设计原则和约束条件。它主要用户客户端和服务器交互类的软件。基于这个风格设计的软件可以更简洁，更有层次，更易于实现缓存机制等。

REST全程是Representational State Transfer，表征性状态转移。首次在2000年Roy Thomas Fielding的博士论文中出现，Fielding是一个非常重要的人，他是HTTP协议（1.0版和1.1版）的主要设计者，Apache服务器软件的作者之一，Apache基金会的第一任主席。所以，他的这篇论文一经发表，就引起了广泛的关注。

论文:

本文研究计算机科学两大前沿----软件和网络----的交叉点。长期以来，软件研究主要关注软件设计的分类、设计方法的演化，很少客观地评估不同的设计选择对系统行为的影响。而相反地，网络研究主要关注系统之间通信行为的细节、如何改进特定通信机制的表现，常常忽视了一个事实，那就是改变应用程序的互动风格比改变互动协议，对整体表现有更大的影响。**我这篇文章的写作目的，就是想在符合架构原理的前提下，理解和评估以网络为基础的应用软件的架构设计，得到一个功能强、性能好、适宜通信的架构。**

\(This dissertation explores a junction on the frontiers of two research disciplines in computer science: software and networking. Software research has long been concerned with the categorization of software designs and the development of design methodologies, but has rarely been able to objectively evaluate the impact of various design choices on system behavior. Networking research, in contrast, is focused on the details of generic communication behavior between systems and improving the performance of particular communication techniques, often ignoring the fact that changing the interaction style of an application can have more impact on performance than the communication protocols used for that interaction. My work is motivated by the desire to understand and evaluate the architectural design of network-based application software through principled use of architectural constraints, thereby obtaining the functional, performance, and social properties desired of an architecture. \)

### REST爆发

其实在REST架构推出的十几年间，它并没有一路高歌的发展，真正的大范围推广是在2013年之后，伴随着移动端的飞速发展，越来越多人的开始意识到，网站即软件，而且是一种新型的软件。

这种"互联网软件采用"客户端/服务器"模式，也就是我们常说的C/S模式，这一切建立在分布式体系上，通过互联网通信，具有高延时，高并发等特点。

网站开发，完全采用软件开发开发的模式。但传统上，软件和网络是两个不同的领域，很少有交集，软件开发主要针对单机环境，网络则主要研究系统之间的通信。我们需要考虑的是如何开发在互联网环境中使用软件。



### 理解RESTful

要理解RESTful架构，最好的就是去理解它的单词 Representational State Transfer 到底是什么意思，它的每一个词到底要表达什么。

REST的释义，"表现层状态转化"，其实这省略了主语。“表现层”其实指的是“资源\(Resource\)”的“表现层”。

##### 资源（Resource）

所谓“资源”，就是网络上的一个实体，或者说是网络上的一个具体信息。它可以是一段文本，一张图片，一首歌曲，一种服务，总之就是一个具体的实例。你可以使用一个URI（统一资源定位符）指向它，每种资源对应一个特定的URI。要获取这个资源，访问它的URI就可以了，因此URI就成了每一个资源的地址或独一无二的识别符。所谓“上网”就是与互联网上一系列的“资源”互动，调用它们的URI。

##### 表现层（Representation）

“资源”是一种信息实体，它可以有多种外在表现形式。我们把“资源”具体呈现出来的形式，叫做它的”表现层“（Representation）。

URI只代表资源的实体，不代表它的形式。严格地说，有些网站最后的”.html“后缀名是不必要的，因为这个后缀表示格式，属于”表现层“范畴，而URI应该只代表”资源“的位置。它的具体表现形式，应该在HTTP请求头的信息中使用Accept和Content-Type字段指定。

##### 状态转换（State Transfer）

访问一个网站，就代表客户端和服务端的一个互动过程。在这个过程中，势必涉及到数据和状态的变化。

互联网通信协议HTTP协议，是一个无状态协议。这意味着，所有的状态都保存在服务端。因此，如果客户端想要操作服务器，就必须通过某种手段，让服务器端发生”状态转换（State Transfer）“。而这种转换是建立在表现层之上的，所以就是”表现层状态转化“。

客户端用到的手段，只能是HTTP协议。具体来说，就是HTTP协议中，四个表示操作方式的动词：GET，POST，PUT，DELETE。它们分别对应四种基本操作：GET用来获取资源，POST用来新建资源（也可用于更新资源），PUT用来更新资源，DELETE用来删除资源



#### 到底什么是RESTful架构

1. 每一个URI代表一种资源
2. 客户端和服务器之间，传递这种资源的某种表现层
3. 客户端通过四个HTTP动词，对服务端资源进行操作，实现”表现层状态转换“



## RESTful API设计

###### 协议

API与用户的通信协议，通常使用HTTP\(S\)协议。

###### 域名

应该尽量将API部署在专用域名之下。

```
http://api.rock.com
```

如果确定API很简单，不会有大规模扩充，可以考虑放在主域名之下。

```
http://www.rock.com/api/
```

###### 版本

应该将API的版本号放入URL。

```
http://api.rock.com/v1/
```

也有做法是将版本号放在HTTP的头信息中，但不如放在URL中方便和直观。GITHUB是这么搞的。

###### 路径（Endpoint）

路径又称”终点“（endpoint），表示API的具体网址。

在RESTful架构中，每个网址代表一种资源（Resource），所以网址中不能有动词，只能有名词，而且所用的名词往往与数据库的表格名对应。一般来说，数据库中的表都是同种记录的”集合“（collection），所以API中的名词也应该使用复数。

###### HTTP动词

对于资源的具体操作类型，由HTTP动词表示。

HTTP常用动词

* GET（SELECT）：从服务器取出资源
* POST（CREATE or UPDATE）：在服务器创建资源或更新资源
* PUT（UPDATE）：在服务器更新资源（客户端提供改变后的完整资源）
* PATCH（UPDATE）：在服务器更新资源（客户端提供改变的属性）
* DELETE（DELETE）：从服务器删除资源
* HEAD：获取资源的元数据
* OPTIONS：获取信息，关于资源的哪些属性是客户端可以改变的、

示例

* GET  /students：获取所有学生
* POST /students：新建学生
* GET  /students/id：获取某一个学生
* PUT /students/id ：更新某个学生的信息（需要提供学生的全部信息）
* PATCH /students/id：更新某个学生的信息（需要提供学生变更部分信息）
* DELETE /students/id：删除某个学生

###### 过滤信息（Filtering）

如果记录数量过多，服务器不可能将它们返回给用户。API应该提供参数，过滤返回结果。

* ?limit=10
* ?offset=10
* ?page=2&per\_page=20
* ?sortby=name&order=desc
* ?student\_id=id

参数的设计允许存在冗余，即允许API路径和URL参数偶尔有重复，比如 GET /students/id 和 ？student\_id=id

###### 状态码

服务器向用户返回的状态码和提示信息，常见的有以下一些地方

* 200 OK - \[GET\]：服务器成功返回用户请求的数据
* 201 CREATED -\[POST/PUT/PATCH\]：用户新建或修改数据成功
* 202 Accepted - \[\*\] ：表示一个请求已经进入后台排队（异步任务）
* 204 NO CONTENT - \[DELETE\]：表示数据删除成功
* 400 INVALID REQUEST - \[POST/PUT/PATCH\]：用户发出的请求有错误
* 401 Unauthorized - \[\*\] ：表示用户没有权限（令牌，用户名，密码错误）
* 403 Forbidden - \[\*\]：表示用户得到授权，但是访问是被禁止的
* 404 NOT FOUND - \[\*\]：用户发出的请求针对的是不存在的记录
* 406 Not Acceptable - \[\*\]：用户请求格式不可得
* 410 Gone - \[GET\] ：用户请求的资源被永久移除，且不会再得到的
* 422 Unprocesable entity -\[POST/PUT/PATCH\]：当创建一个对象时，发生一个验证错误
* 500 INTERNAL SERVER EROR - \[\*\] ：服务器内部发生错误

###### 错误处理

如果状态码是4xx，就应该向用户返回出错信息。一般来说，返回的信息中将error做为键名

###### 返回结果

针对不同操作，服务器想用户返回的结果应该符合以下规范

* GET /collection：返回资源对象的列表（数组，集合）
* GET /collection/id：返回单个资源对象
* POST /collection：返回新生成的资源对象
* PUT /collection/id：返回完整的资源对象
* PATCH /collection/id：返回完整的资源对象
* DELETE /collection/id：返回一个空文档

###### 使用链接关联资源

RESTful API最好做到Hypermedia，即返回结果中提供链接，连向其他API方法，使得用户不查文档，也知道下一步应该做什么。

```
{
    "link": {
        "rel":   "collection https://www.rock.com/zoostudents",
        "href":  "https://api.rock.com/students",
        "title": "List of students",
        "type":  "application/vnd.yourformat+json"
      }
}
```

* rel：表示这个API与当前网址的关系
* href：表示API的路径
* title：表示API的标题
* type：表示返回的类型

###### 其它

* 服务器返回的数据格式，应该尽量使用JSON
* API的身份认证应该使用OAuth2.0框架





















