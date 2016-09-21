##11.1.注册新的URI模式

###11.1.1.注册“ws“模式

一个|ws| URI标识一个WebSocket服务器和资源名称。

URI模式名称

&nbsp;&nbsp;&nbsp;&nbsp;ws

状态

&nbsp;&nbsp;&nbsp;&nbsp;永久的

URI模式语法

&nbsp;&nbsp;&nbsp;&nbsp;使用ABNF[[RFC5234](http://tools.ietf.org/html/rfc5234)]语法和URI规范[[RFC3986](http://tools.ietf.org/html/rfc3986)]的ABNF终结符：

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"ws:" "//" authority path-abempty [ "?" query ]

&nbsp;&nbsp;&nbsp;&nbsp;<path-abempty>和<query> [[RFC3986](http://tools.ietf.org/html/rfc3986)]组件形成的资源名发生给服务器来确定服务期望的类型。其他组件的含义描述在[[RFC3986](http://tools.ietf.org/html/rfc3986)]。

模式语义

&nbsp;&nbsp;&nbsp;&nbsp;这个模式的作用仅是使用WebSocket协议打开一个连接。

编码考虑

&nbsp;&nbsp;&nbsp;&nbsp;上边定义的语法不包括host组件中的字符，必须按照[[RFC3987](http://tools.ietf.org/html/rfc3987)]从Unicode转换为ASCII或其替换。为了模式标准化的目的，国际化域名（IDN）形式的host组件和它们转换的域名代码（Punycode）被认为是等价的（参考[[RFC3987](http://tools.ietf.org/html/rfc3987)] 5.3.3节）。  

&nbsp;&nbsp;&nbsp;&nbsp;上边定义的语法不包括其他组件中的字符，必须按照定义在URI[[RFC3986](http://tools.ietf.org/html/rfc3986)] 和国际化资源标识符（IRI）[[RFC3987](http://tools.ietf.org/html/rfc3987)]规范从Unicode编码转换为ASCII，通过首先编码字符为UTF-8，接着使用它们百分数编码的形式替换相应的字节。

应用/协议使用这个URI模式命名

&nbsp;&nbsp;&nbsp;&nbsp;WebSokcet协议

互操作性考虑 

&nbsp;&nbsp;&nbsp;&nbsp;使用WebSocket需要使用HTTP版本1.1或更高。

&nbsp;&nbsp;&nbsp;&nbsp;安全考虑

&nbsp;&nbsp;&nbsp;&nbsp;参考“安全考虑”章节。

&nbsp;&nbsp;&nbsp;&nbsp;联系方式

&nbsp;&nbsp;&nbsp;&nbsp;HYBI WG <hybi@ietf.org>

&nbsp;&nbsp;&nbsp;&nbsp;作者/变更管理员

&nbsp;&nbsp;&nbsp;&nbsp;IETF <iesg@ietf.org>

&nbsp;&nbsp;&nbsp;&nbsp;参考资源

&nbsp;&nbsp;&nbsp;&nbsp;[RFC 6455](http://tools.ietf.org/html/rfc6455)

###11.1.2.注册”wss“模式

一个|wss| URI标识一个WebSocket服务器和资源名称，并表明在受TLS保护的连接之上通信（包括标准的TLS的好处，比如数据保密性和完整性和端点认证）。

URI模式名称

&nbsp;&nbsp;&nbsp;&nbsp;wss

状态

&nbsp;&nbsp;&nbsp;&nbsp;永久的

URI模式语法

&nbsp;&nbsp;&nbsp;&nbsp;使用ABNF[[RFC5234](http://tools.ietf.org/html/rfc5234)]语法和URI规范[[RFC3986](http://tools.ietf.org/html/rfc3986)]的ABNF终结符：

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  "wss:" "//" authority path-abempty [ "?" query ]

&nbsp;&nbsp;&nbsp;&nbsp;<path-abempty>和<query> [[RFC3986](http://tools.ietf.org/html/rfc3986)]组件形成的资源名发生给服务器来确定服务期望的类型。其他组件的含义描述在[[RFC3986](http://tools.ietf.org/html/rfc3986)]。

URI模式语义

&nbsp;&nbsp;&nbsp;&nbsp;这个模式的作用仅是使用WebSocket协议打开一个使用TLS的连接。

编码考虑

&nbsp;&nbsp;&nbsp;&nbsp;上边定义的语法不包括host组件中的字符，必须按照[[RFC3987](http://tools.ietf.org/html/rfc3987)]从Unicode转换为ASCII或其替换。为了模式标准化的目的，国际化域名（IDN）形式的host组件和它们转换的域名代码（Punycode）被认为是等价的（参考[[RFC3987](http://tools.ietf.org/html/rfc3987)] 5.3.3节）。  

&nbsp;&nbsp;&nbsp;&nbsp;上边定义的语法不包括其他组件中的字符，必须按照定义在URI[[RFC3986](http://tools.ietf.org/html/rfc3986)] 和国际化资源标识符（IRI）[[RFC3987](http://tools.ietf.org/html/rfc3987)]规范从Unicode编码转换为ASCII，通过首先编码字符为UTF-8，接着使用它们百分数编码的形式替换相应的字节。

应用/协议使用这个URI模式命名

&nbsp;&nbsp;&nbsp;&nbsp;TLS之上的WebSokcet协议

互操作性考虑 

&nbsp;&nbsp;&nbsp;&nbsp;使用WebSocket需要使用HTTP版本1.1或更高。

安全考虑

&nbsp;&nbsp;&nbsp;&nbsp;参考“安全考虑”章节。

联系方式

&nbsp;&nbsp;&nbsp;&nbsp;HYBI WG <hybi@ietf.org>

作者/变更管理员

&nbsp;&nbsp;&nbsp;&nbsp;IETF <iesg@ietf.org>

参考资源

&nbsp;&nbsp;&nbsp;&nbsp;[RFC 6455](http://tools.ietf.org/html/rfc6455)

##11.2.注册”WebSocket“ HTTP Upgrade关键字

本节按照[RFC2817](http://tools.ietf.org/html/rfc2817)[[RFC2817](http://tools.ietf.org/html/rfc2817)]定义了在HTTP Upgrade符号注册中心中注册一个关键字。

符号名称

&nbsp;&nbsp;&nbsp;&nbsp;WebSocket

作者/变更管理员

&nbsp;&nbsp;&nbsp;&nbsp;IETF <iesg@ietf.org>

参考资源

&nbsp;&nbsp;&nbsp;&nbsp;[RFC 6455](http://tools.ietf.org/html/rfc6455)

##11.3.注册新的HTTP头字段

###11.3.1. Sec-WebSocket-Key

本节描述了在永久消息头字段命名注册中心[[RFC3864](http://tools.ietf.org/html/rfc3864)]中注册一个头字段。

头字段名

&nbsp;&nbsp;&nbsp;&nbsp;Sec-WebSocket-Key

适用协议

&nbsp;&nbsp;&nbsp;&nbsp;http

状态


&nbsp;&nbsp;&nbsp;&nbsp;标准的

作者/变更管理员

&nbsp;&nbsp;&nbsp;&nbsp;IETF 

参考资源

&nbsp;&nbsp;&nbsp;&nbsp;[RFC 6455](http://tools.ietf.org/html/rfc6455)

相关信息

&nbsp;&nbsp;&nbsp;&nbsp;该头字段仅用于WebSocket打开阶段握手。

|Sec-WebSocket-Key| 头字段用于WebSocket打开阶段握手。它从客户端发送到服务器，提供部分信息用于服务器检验它收到了一个有效的WebSocket握手。这有助于确保服务器不接收正被滥用来发送数据给毫不知情的WebSocket服务器的非WebSocket客户端的连接（例如HTTP客户端）。

|Sec-WebSocket-Key| 头字段在一个HTTP请求中不能出现多于一个。

###11.3.2. Sec-WebSocket-Extensions

本节描述了在永久消息头字段命名注册中心[[RFC3864](http://tools.ietf.org/html/rfc3864)]中注册一个头字段。

头字段名

&nbsp;&nbsp;&nbsp;&nbsp;Sec-WebSocket-Extensions

适用协议

&nbsp;&nbsp;&nbsp;&nbsp;http

状态

&nbsp;&nbsp;&nbsp;&nbsp;标准的

作者/变更管理员

&nbsp;&nbsp;&nbsp;&nbsp;IETF

参考资源

&nbsp;&nbsp;&nbsp;&nbsp;[RFC 6455](http://tools.ietf.org/html/rfc6455)

相关信息

&nbsp;&nbsp;&nbsp;&nbsp;该头字段仅用于WebSocket打开阶段握手。

|Sec-WebSocket-Extensions|头字段用于WebSocket打开阶段握手。它最初是从客户端发送到服务器，随后从服务器端发送到客户端，用来达成在整个连接阶段的一组协议级扩展。

|Sec-WebSocket-Extensions|头字段在HTTP请求中可以出现多次（逻辑上等价于单个|Sec-WebSocket-Extensions|头字段包含所有值）。

但是，|Sec-WebSocket-Extensions|头字段在一个HTTP响应中必须不出现多于一次。

###11.3.3. Sec-WebSocket-Accept

本节描述了在永久消息头字段命名注册中心[[RFC3864](http://tools.ietf.org/html/rfc3864)]中注册一个头字段。

头字段名

&nbsp;&nbsp;&nbsp;&nbsp;Sec-WebSocket-Accept

适用协议

&nbsp;&nbsp;&nbsp;&nbsp;http

状态

&nbsp;&nbsp;&nbsp;&nbsp;标准的

作者/变更管理员

&nbsp;&nbsp;&nbsp;&nbsp;IETF

参考资源

&nbsp;&nbsp;&nbsp;&nbsp;[RFC 6455](http://tools.ietf.org/html/rfc6455)

规范文档

&nbsp;&nbsp;&nbsp;&nbsp;[RFC 6455](http://tools.ietf.org/html/rfc6455)

相关信息

&nbsp;&nbsp;&nbsp;&nbsp;该头字段仅用于WebSocket打开阶段握手。

| Sec-WebSocket-Accept|头字段用于WebSocket打开阶段握手。它从服务器发送到客户端来确定服务器愿意启动WebSocket连接。

|Sec-WebSocket-Accept| 头在一个HTTP响应中必须不出现多于一次。

###11.3.4. Sec-WebSocket-Protocol

本节描述了在永久消息头字段命名注册中心[[RFC3864](http://tools.ietf.org/html/rfc3864)]中注册一个头字段。

头字段名

&nbsp;&nbsp;&nbsp;&nbsp;Sec-WebSocket-Protocol

适用协议

&nbsp;&nbsp;&nbsp;&nbsp;http

状态

&nbsp;&nbsp;&nbsp;&nbsp;标准的

作者/变更管理员

&nbsp;&nbsp;&nbsp;&nbsp;IETF

参考资源

&nbsp;&nbsp;&nbsp;&nbsp;[RFC 6455](http://tools.ietf.org/html/rfc6455)

规范文档

&nbsp;&nbsp;&nbsp;&nbsp;[RFC 6455](http://tools.ietf.org/html/rfc6455)

相关信息

&nbsp;&nbsp;&nbsp;&nbsp;该头字段仅用于WebSocket打开阶段握手。

|Sec-WebSocket-Protocol|头字段用于WebSocket打开阶段握手。它从客户端发送到服务器端，并从服务器端发回到客户端来确定连接的子协议。这使脚本可以选择一个子协议和确定服务器同意服务子协议。

|Sec-WebSocket-Protocol|头字段在一个HTTP请求中可以出现多次（逻辑上等价于单个|Sec-WebSocket-Protocol|头字段包含所有值）。 

但是，|Sec-WebSocket-Protocol|头字段在一个HTTP响应中必须不出现多于一次。

###11.3.5.Sec-WebSocket-Version

本节描述了在永久消息头字段命名注册中心[[RFC3864](http://tools.ietf.org/html/rfc3864)]中注册一个头字段。

头字段名

&nbsp;&nbsp;&nbsp;&nbsp;Sec-WebSocket-Version

适用协议

&nbsp;&nbsp;&nbsp;&nbsp;http

状态

&nbsp;&nbsp;&nbsp;&nbsp;标准的

作者/变更管理员

&nbsp;&nbsp;&nbsp;&nbsp;IETF

参考资源

&nbsp;&nbsp;&nbsp;&nbsp;[RFC 6455](http://tools.ietf.org/html/rfc6455)

规范文档

&nbsp;&nbsp;&nbsp;&nbsp;[RFC 6455](http://tools.ietf.org/html/rfc6455)

相关信息

&nbsp;&nbsp;&nbsp;&nbsp;该头字段仅用于WebSocket打开阶段握手。

|Sec-WebSocket- Version |头字段用于WebSocket打开阶段握手。它从客户端发送到服务器端来指定连接的协议版本。这能使服务器正确解释打开阶段握手和发送数据的随后数据，如果服务器不能以安全的方式解释数据则关闭连接。当从客户端接收到不匹配服务器端理解的版本时，WebSocket握手错误，|Sec-WebSocket-Version|头字段也从服务器端发送到客户端。在这种情况下，头字段包括服务器端支持的协议版本。

注意，如果没有期望更高版本号，必然是向下兼容低版本号。

|Sec-WebSocket-Version|头字段在一个HTTP响应中可以出现多次（逻辑上等价于单个|Sec-WebSocket-Version|透过自动包含所有值）。

但是，|Sec-WebSocket-Version|头字段在HTTP请求中必须不出现多于一次。

##11.4.WebSocket扩展名注册

本规范依据[RFC5226](http://tools.ietf.org/html/rfc5226)[[RFC5226](http://tools.ietf.org/html/rfc5226)]陈述的原则，创建了一个新的IANA注册用于与WebSocket协议一起使用的WebSocket扩展名。

作为本注册的一部分，IANA维护以下信息：

扩展标识符

&nbsp;&nbsp;&nbsp;&nbsp;扩展标识符， 将被用在注册到本规范[11.3.2节](http://tools.ietf.org/html/rfc6455#section-11.3.4)的| Sec-WebSocket-Extensions|头字段。其值必须符合定义在本规范[9.1节](http://tools.ietf.org/html/rfc6455#section-4.1)的扩展-符号要求。

扩展通用名称

&nbsp;&nbsp;&nbsp;&nbsp;扩展名称，通常称为扩展。

扩展定义

&nbsp;&nbsp;&nbsp;&nbsp;在扩展用于的WebSocket协议中定义了文档参考。

已知的不兼容扩展

&nbsp;&nbsp;&nbsp;&nbsp;与此扩展是不兼容的一个扩展标识符列表。

WebSocket扩展名受制于“先来先服务”的IANA注册策略 [[RFC5226](http://tools.ietf.org/html/rfc5226)]。

在此注册中心没有初始值。

##11.5.WebSocket子协议名注册

本规范依据RFC5226[RFC5226]陈述的原则，创建了一个新的IANA注册用于与WebSocket协议一起使用的WebSocket子协议名。

作为本注册的一部分，IANA维护以下信息：

子协议标识符
&nbsp;&nbsp;&nbsp;&nbsp;子协议标识符， 将被用在注册到本规范[11.3.4节](http://tools.ietf.org/html/rfc6455#section-11.3.4)的|Sec-WebSocket-Protocol|头字段。其值必须符合定义在本规范[4.1节](http://tools.ietf.org/html/rfc6455#section-4.1)给出的第10条的符号要求——也就是，其值必须是[RFC5226](http://tools.ietf.org/html/rfc5226) [[RFC5226](http://tools.ietf.org/html/rfc5226)].定义的一个符号。

子协议通用名称

&nbsp;&nbsp;&nbsp;&nbsp;子协议名称，通常成为子协议。

子协议定义

&nbsp;&nbsp;&nbsp;&nbsp;在子协议用于的WebSocket协议中定义了文档参考。

WebSocket子协议名受制于“先来先服务”的IANA注册策略 [[RFC5226](http://tools.ietf.org/html/rfc5226)]。

##11.6.WebSocket版本号注册

本规范依据[RFC5226](http://tools.ietf.org/html/rfc5226)[[RFC5226](http://tools.ietf.org/html/rfc5226)]陈述的原则，创建了一个新的IANA注册用于与WebSocket协议一起使用的WebSocket版本号。

作为本注册的一部分，IANA维护以下信息：

版本号

&nbsp;&nbsp;&nbsp;&nbsp;用于|Sec-WebSocket-Version|的版本号指定在本规范[4.1节](http://tools.ietf.org/html/rfc6455#section-4.1)。其值必须是一个在0到255（包括）之间的非负整数。

参考

&nbsp;&nbsp;&nbsp;&nbsp;RFC请求一个新的版本号或带版本号的草案名称（见下文）。

状态

&nbsp;&nbsp;&nbsp;&nbsp;“临时的”或“标准的”。参考下面的说明。

一个版本号被指定为“临时的”或“标准的”。

“标准的”版本号是记录在一个RFC中并用来识别一个主要的、稳定的WebSocket协议版本，例如本RFC定义的版本。“标准的”版本号受制于“IETF评审”IANA注册策略 [[RFC5226](http://tools.ietf.org/html/rfc5226)]。

“Interim”的版本号记录在一个Internet草案中用并用于帮助实现者识别和与部署的WebSocket版本互操作，例如在公布这个RFC之前指定的版本。“临时的”版本号受制于“专家评审”IANA注册策略 [[RFC5226](http://tools.ietf.org/html/rfc5226)]，HYBI工作组主席（或，如果工作组关闭了，IETF应用区域的区域董事）将是初始的指定专家。

IANA 已经添加如下初始值到注册中心：

    +--------+-----------------------------------------+----------+
    |Version |                Reference                |  Status  |
    | Number |                                         |          |
    +--------+-----------------------------------------+----------+
    | 0      + draft-ietf-hybi-thewebsocketprotocol-00 | Interim  |
    +--------+-----------------------------------------+----------+
    | 1      + draft-ietf-hybi-thewebsocketprotocol-01 | Interim  |
    +--------+-----------------------------------------+----------+
    | 2      + draft-ietf-hybi-thewebsocketprotocol-02 | Interim  |
    +--------+-----------------------------------------+----------+
    | 3      + draft-ietf-hybi-thewebsocketprotocol-03 | Interim  |
    +--------+-----------------------------------------+----------+
    | 4      + draft-ietf-hybi-thewebsocketprotocol-04 | Interim  |
    +--------+-----------------------------------------+----------+
    | 5      + draft-ietf-hybi-thewebsocketprotocol-05 | Interim  |
    +--------+-----------------------------------------+----------+
    | 6      + draft-ietf-hybi-thewebsocketprotocol-06 | Interim  |
    +--------+-----------------------------------------+----------+
    | 7      + draft-ietf-hybi-thewebsocketprotocol-07 | Interim  |
    +--------+-----------------------------------------+----------+
    | 8      + draft-ietf-hybi-thewebsocketprotocol-08 | Interim  |
    +--------+-----------------------------------------+----------+
    | 9      +                Reserved                 |          |
    +--------+-----------------------------------------+----------+
    | 10     +                Reserved                 |          |
    +--------+-----------------------------------------+----------+
    | 11     +                Reserved                 |          |
    +--------+-----------------------------------------+----------+
    | 12     +                Reserved                 |          |
    +--------+-----------------------------------------+----------+
    | 13     +                RFC 6455                 | Standard |
    +--------+-----------------------------------------+----------+
 
##11.7.WebSocket关闭代码注册

本规范依据[RFC5226](http://tools.ietf.org/html/rfc5226)[[RFC5226](http://tools.ietf.org/html/rfc5226)]陈述的原则，创建了一个新的IANA注册用于WebSocket关闭代码。

作为本注册的一部分，IANA维护以下信息：

状态码
&nbsp;&nbsp;&nbsp;&nbsp;状态码表示一个按照本文档[7.4节](http://tools.ietf.org/html/rfc6455#section-7.4)的WebSocket连接关闭的原因。状态是一个在1000到4999（包括）之间的一个整数数字。

含义

&nbsp;&nbsp;&nbsp;&nbsp;状态码的含义。每一个状态码都必须有唯一的含义。

联系方式

&nbsp;&nbsp;&nbsp;&nbsp;保留状态代码实体的联系方式。

参考

&nbsp;&nbsp;&nbsp;&nbsp;稳定的文档要求状态码并定义它们的含义。在1000-2999范围内的状态码是必须的且推荐的状态码在3000-3999范围内。

WebSocket关闭代码根据它们的范围受不同的注册要求。本协议请求使用的状态码和其后续版本或扩展受制于“标准功能”、“规定要求”（这意味着“指定专家”）或“IESG审查”IANA注册策略中的任何一个，且应该允许在1000-2999范围内。库、框架和应用请求使用的状态码受制于“先来先服务”IANA注册策略且应该允许在3000-3999范围内。4000-4999范围的状态码被指定用于私有使用。请求应该指出他们要求的状态码是用于WebSocket协议（或未来版本的协议）、扩展，或库/框架/应用。

IANA 已经添加如下初始值到注册中心：

     |Status Code | Meaning         | Contact       | Reference |
    -+------------+-----------------+---------------+-----------|
     | 1000       | Normal Closure  | hybi@ietf.org | RFC 6455  |
    -+------------+-----------------+---------------+-----------|
     | 1001       | Going Away      | hybi@ietf.org | RFC 6455  |
    -+------------+-----------------+---------------+-----------|
     | 1002       | Protocol error  | hybi@ietf.org | RFC 6455  |
    -+------------+-----------------+---------------+-----------|
     | 1003       | Unsupported Data| hybi@ietf.org | RFC 6455  |
    -+------------+-----------------+---------------+-----------|
     | 1004       | ---Reserved---- | hybi@ietf.org | RFC 6455  |
    -+------------+-----------------+---------------+-----------|
     | 1005       | No Status Rcvd  | hybi@ietf.org | RFC 6455  |
    -+------------+-----------------+---------------+-----------|
     | 1006       | Abnormal Closure| hybi@ietf.org | RFC 6455  |
    -+------------+-----------------+---------------+-----------|
     | 1007       | Invalid frame   | hybi@ietf.org | RFC 6455  |
     |            | payload data    |               |           |
    -+------------+-----------------+---------------+-----------|
     | 1008       | Policy Violation| hybi@ietf.org | RFC 6455  |
    -+------------+-----------------+---------------+-----------|
     | 1009       | Message Too Big | hybi@ietf.org | RFC 6455  |
    -+------------+-----------------+---------------+-----------|
     | 1010       | Mandatory Ext.  | hybi@ietf.org | RFC 6455  |
    -+------------+-----------------+---------------+-----------|
     | 1011       | Internal Server | hybi@ietf.org | RFC 6455  |
     |            | Error           |               |           |
    -+------------+-----------------+---------------+-----------|
     | 1015       | TLS handshake   | hybi@ietf.org | RFC 6455  |
    -+------------+-----------------+---------------+-----------|

##11.8.WebSocket操作码注册

本规范依据[RFC5226](http://tools.ietf.org/html/rfc5226)[[RFC5226](http://tools.ietf.org/html/rfc5226)]陈述的原则，创建一个新的IANA注册用于WebSocket操作码。

作为本注册的一部分，IANA维护以下信息：

操作码
&nbsp;&nbsp;&nbsp;&nbsp;操作码表示WebSocket帧的帧类型，定义在[5.2节](http://tools.ietf.org/html/rfc6455#section-5.2)。操作码是一个在0到15（包括）之间的整数数字。

含义

&nbsp;&nbsp;&nbsp;&nbsp;状态码值的含义。

参考

&nbsp;&nbsp;&nbsp;&nbsp;规范要求的操作码。

WebSocket状态码受制于“标准功能”IANA注册策略[[RFC5226](http://tools.ietf.org/html/rfc5226)]。

IANA 已经添加如下初始值到注册中心：

     |Opcode  | Meaning                             | Reference |
    -+--------+-------------------------------------+-----------|
     | 0      | Continuation Frame                  | RFC 6455  |
    -+--------+-------------------------------------+-----------|
     | 1      | Text Frame                          | RFC 6455  |
    -+--------+-------------------------------------+-----------|
     | 2      | Binary Frame                        | RFC 6455  |
    -+--------+-------------------------------------+-----------|
     | 8      | Connection Close Frame              | RFC 6455  |
    -+--------+-------------------------------------+-----------|
     | 9      | Ping Frame                          | RFC 6455  |
    -+--------+-------------------------------------+-----------|
     | 10     | Pong Frame                          | RFC 6455  |
    -+--------+-------------------------------------+-----------|

##11.9.WebSocket帧头位注册

本规范依据[RFC5226](http://tools.ietf.org/html/rfc5226)[[RFC5226](http://tools.ietf.org/html/rfc5226)]陈述的原则，创建了一个新的IANA注册用于WebSocket帧头位（Framing Header Bits）。此注册控制的位分配标记为[5.2节](http://tools.ietf.org/html/rfc6455#section-5.2)的RSV1、RSV2和RSV3。

这些位被保留用于未来版本或本规范的扩展。

WebSocket帧头位分配受制于“标准功能”IANA注册测策略[[RFC5226](http://tools.ietf.org/html/rfc5226)]。