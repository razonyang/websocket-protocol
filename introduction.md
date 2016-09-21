## 1.1.背景
本节是非规范的。

过去，创建需要在客户端和服务之间双向通信（例如，即时消息和游戏应用）的web应用， 需要一个滥用的HTTP来轮询服务器进行更新但以不同的HTTP调用发生上行通知[[RFC6202](http://tools.ietf.org/html/rfc6202)]。

这将导致各种各样的问题：

   o  服务器被迫为每个客户端使用一些不同的底层TCP连接： 一个用于发送信息到客户端和一个新的用于每个传入消息。

   o  线路层协议有较高的开销，因为每个客户端-服务器消息都有一个HTTP头信息。

   o  客户端脚本被迫维护一个传出的连接到传入的连接的映射来跟踪回复。

一个简单的办法是使用单个TCP连接双向传输。这是为什么提供WebSocket 协议。与WebSocket API结合[[WSAPI](http://tools.ietf.org/html/rfc6455#ref-WSAPI)]，它提供了一个HTTP轮询的替代来进行从web 页面到远程服务器的双向通信。
同样的技术可以用于各种各样的web应用：

游戏、股票行情、同时编辑的多用户应用、服务器端服务以实时暴露的用户接口、等等。

WebSocket协议被设计来取代现有的使用HTTP作为传输层的双向通信技术，并受益于现有的基础设施（代理、过滤、身份验证）。这样的技术被实现来在效率和可靠性之间权衡，因为HTTP最初目的不是用于双向通信（参见[[RFC6202](http://tools.ietf.org/html/rfc6202)]的进一步讨论）。WebSocket协议试图在现有的HTTP基础设施上下文中解决现有的双向HTTP技术目标；同样，它被设计工作在HTTP端口80和443，也支持HTTP代理和中间件，即使这具体到当前环境意味着一些复杂性。但是，这种设计不限制WebSocket到HTTP，且未来的实现可以在一个专用的端口上使用一个更简单的握手，且没有再创造整个协议。最后一点是很重要的，因为交互消息的传输模式不精确地匹配标准HTTP传输并可能在相同组件上包含不常见的负载。
## 1.2.协议概述
本节是非规范的。

本协议有两部分：握手和数据传输。

来自客户端的握手看起来像如下形式：

        GET /chat HTTP/1.1
        Host: server.example.com
        Upgrade: websocket
        Connection: Upgrade
        Sec-WebSocket-Key: dGhlIHNhbXBsZSBub25jZQ==
        Origin: http://example.com
        Sec-WebSocket-Protocol: chat, superchat
        Sec-WebSocket-Version: 13

来自服务器的握手看起来像如下形式：

        HTTP/1.1 101 Switching Protocols
        Upgrade: websocket
        Connection: Upgrade
        Sec-WebSocket-Accept: s3pPLMBiTxaQ9kYGzzhZRbK+xOo=
        Sec-WebSocket-Protocol: chat

来自客户端的首行遵照Request-Line格式。

来自服务器的首行遵照Status-Line格式。

Request-Line 和 Status-Line 制品定义在[[RFC2616](http://tools.ietf.org/html/rfc2616)]。

在这两种情况中一个无序的头字段集合出现在首行之后。这些头字段的意思指定在本文档的第4章。另外的头字段也可能出现，例如cookies[[RFC6265](http://tools.ietf.org/html/rfc6265)]。头的格式和解析定义在[[RFC2616](http://tools.ietf.org/html/rfc2616)]。

一旦客户端和服务器都发送了它们的握手，且如果握手成功，接着开始数据传输部分。这是一个每一端都可以的双向通信信道，彼此独立，随意发生数据。

一个成功握手之后，客户端和服务器来回地传输数据，在本规范中提到的概念单位为“消息”。在线路上，一个消息是由一个或多个帧的组成。WebSocket的消息并不一定对应于一个特定的网络层帧，可以作为一个可以被一个中间件合并或分解的片段消息。

一个帧有一个相应的类型。属于相同消息的每一帧包含相同类型的数据。从广义上讲，有文本数据类型（它被解释为UTF-8[[RFC3629](http://tools.ietf.org/html/rfc3629)]文本）、二进制数据类型（它的解释是留给应用）、和控制帧类型（它是不准备包含用于应用的数据，而是协议级的信号，例如应关闭连接的信号）。这个版本的协议定义了六个帧类型并保留10以备将来使用。
## 1.3.打开阶段握手
本节是非规范的。

打开阶段握手目的是兼容基于HTTP的服务器软件和中间件，以便单个端口可以用于与服务器交流的HTTP客户端和与服务器交流的WebSocket客户端。最后，WebSocket客户端的握手是一个HTTP Upgrade请求：

        GET /chat HTTP/1.1
        Host: server.example.com
        Upgrade: websocket
        Connection: Upgrade
        Sec-WebSocket-Key: dGhlIHNhbXBsZSBub25jZQ==
        Origin: http://example.com
        Sec-WebSocket-Protocol: chat, superchat
        Sec-WebSocket-Version: 13

依照[[RFC2616](http://tools.ietf.org/html/rfc2616)]，握手中的头字段可能由客户端按照任意顺序发送，因此在接收的不同头字段中的顺序是不重要的。

“Request-URI”的GET方法[[RFC2616](http://tools.ietf.org/html/rfc2616)]用于识别WebSocket连接的端点，即允许从一个IP地址服务的多个域名，也允许由单台服务器服务的多个WebSocket端点。
客户端按照[[RFC2616](http://tools.ietf.org/html/rfc2616)]在它的握手的|Host|头字段中包含主机名，以便客户端和服务器都都能验证他们同意哪一个正在使用的主机。

在WebSocket协议中另外的头字段可以用于选择选项。典型的选项在这个版本中可用的是子协议选择器（|Sec-WebSocket-Protocol|）、客户端支持的扩展列表（|Sec-WebSocket-Extensions|）、|Origin|头字段等。|Sec-WebSocket-Protocol|请求头字段可以用来表示客户端接受的子协议（WebSocket协议上的应用级协议层）。服务器选择一个可接受的协议或不，并在它的握手中回应该值表示它已经选择了那个协议。

        Sec-WebSocket-Protocol: chat

|Origin|头字段[RFC6454]是用于保护防止未授权的被浏览器中的使用WebSocket API的脚本跨域使用WebSocket服务器。服务器收到WebSocket连接请求生成的脚本来源。如果服务器不想接受来自此来源的连接，它可以选择通过发送一个适当的HTTP错误码拒绝该连接。这个头字段由浏览器客户端发送，对于非浏览器客户端，如果它在这些客户端上下文中有意义，这个头字段可以被发送。

最后，服务器要证明收到客户端WebSocket握手的客户端，以便服务器不接受不是WebSocket连接的连接。这可以防止一个通过使用XMLHttpRequest [[XMLHttpRequest](http://tools.ietf.org/html/rfc6455#ref-XMLHttpRequest)]或一个表单提交发送它精心制作的包欺骗WebSocket服务器的攻击者。

为了证明收到的握手，服务器必须携带两条信息并组合他们形成一个响应。

第一条信息源自客户端握手中的| Sec-WebSocket-Key |头信息：
        Sec-WebSocket-Key: dGhlIHNhbXBsZSBub25jZQ==

对于这个头字段，服务器必须携带其值（出现在头字段上，如，减去开头和结尾空格的base64-编码[[RFC4648](http://tools.ietf.org/html/rfc4648)]的版本）并将这个与字符串形式的全局唯一标识符（GUID，[[RFC4122](http://tools.ietf.org/html/rfc4122)]）“258EAFA5-E914-47DA-95CA-C5AB0DC85B11”连接起来，其不太可能被不理解WebSocket协议的网络端点使用。SHA-1散列（160位）[[FIPS.180-3](http://tools.ietf.org/html/rfc6455#ref-FIPS.180-3)]、base-64编码（参见[[RFC4648](http://tools.ietf.org/html/rfc4648#section-4)]第4章）、用于这个的一系列相关事物接着在服务器握手过程中返回。

具体而言，如果在上面例子中，|Sec-WebSocket-Key|头字段的值为“dGhlIHNhbXBsZSBub25jZQ==”，服务器将连接字符串“258EAFA5-E914-47DA-95CA-C5AB0DC85B11”形成字符串“dGhlIHNhbXBsZSBub25jZQ==258EAFA5-E914-47DA-95CA-C5AB0DC85B11”。服务器接着使用SHA-1散列这个，并产生值0xb3 0x7a 0x4f 0x2c 0xc0 0x62 0x4f 0x16 0x90 0xf6 0x46 0x06 0xcf 0x38 0x59 0x45 0xb2 0xbe 0xc4 0xea。这个值接着使用base64编码（参见[RFC4648]第4章），产生值“s3pPLMBiTxaQ9kYGzzhZRbK+xOo=”。这个值将接着在|Sec-WebSocket-Accept|头字段中回应。

来自服务器的握手比客户端握手更简单。首行是一个HTTP Status-Line，具有状态码101：

        HTTP/1.1 101 Switching Protocols

101以外的任何状态码表示WebSocket握手没有完成且HTTP语义仍适用。头信息遵照该状态码。

|Connection|和|Upgrade|头字段完成HTTP升级。|Sec-WebSocket-Accept|头字段表示服务器是否将接受该连接。如果存在，这个头字段必须包括客户端在|Sec-WebSocket-Key|中现时发送的与预定义的GUID的散列。任何其他值不能被解释为一个服务器可接受的连接。

        HTTP/1.1 101 Switching Protocols
        Upgrade: websocket
        Connection: Upgrade
        Sec-WebSocket-Accept: s3pPLMBiTxaQ9kYGzzhZRbK+xOo=

这些字段由WebSocket客户端为脚本页面做检查。如果|Sec-WebSocket-Accept|不能匹配盼望的值、如果头字段缺失、或HTTP状态码不是101，则连接将不能建立，且WebSocket帧将不发生。

可选的字段也可以被包含在内。在这合格版本的协议中，主要可选字段是|Sec-WebSocket-Protocol|，其表示服务器选择的子协议。WebSocket客户端验证服务器包含的在WebSocket客户端握手中指定的一个值。声明多个子协议的服务器必须确保它选择一个，基于客户端握手并指定它在其握手中。

        Sec-WebSocket-Protocol: chat

服务器也可以设置cookie相关的可选字段为_set_cookies，描述在[[RFC6265](http://tools.ietf.org/html/rfc6265)]。

## 1.4.关闭阶段握手
本节是非规范的。

关闭阶段握手比打开阶段握手简单得多。

两个节点中的任一个都能发送一个控制帧与包含一个指定控制序列的数据来开始关闭阶段握手（详见5.5.1节）。在收到这样一个帧时，另一个节点在响应中发送一个Close帧，如果还没有发送一个。在收到那个控制帧时，第一个节点接着关闭连接，安全地知道没有更多的数据到来。

发送一个控制帧之后，表示连接将被关闭，一个节点不会发送任何更多的数据；在接收到一个控制帧之后，表示连接将被关闭，一个节点会丢弃收到的任何更多的数据。

对于两个节点同时地初始化这个握手是安全的。

关闭阶段握手目的是完成TCP关闭握手（FIN/ACK），基于TCP关闭阶段握手不总是可靠的端到端，尤其在存在拦截代理和中间件。
通过发送一个Close帧并等待响应中的Close帧，某些情况下可避免数据不必要的丢失。例如，在某些平台上，如果一个socket关闭了，且接收队列中有数据，一个RST包被发送了，这样会导致接受RST的一方的recv()失败，即使有数据等待读取。
## 1.5.设计理念
本节是非规范的。

WebSocket协议应该以最小帧的原则设计（唯一存在的框架是使协议基于帧而不是基于流且支持区分Unicode文本和二进制帧）。期望通过应用层将元数据分层在WebSocket之上，同样地，通过应用层将元数据分层在TCP之上（例如，HTTP）。

从概念上讲，WebSocket只是TCP之上的一层，执行以下操作：

o  为浏览器添加一个web 基于来源的安全模型

o  添加一个寻址和协议命名机制来支持在一个IP地址的一个端口的多个主机名的多个服务

o  在TCP之上分一个帧机制层以回到TCP基于的IP包机制，但没有长度限制

o  包括一个额外的带内（in-band）关闭阶段握手，其被设计来工作在现存的代理和其他中间件。

除此之外，WebSocket没有添加任何东西。基本上，它的目的是尽可能接近仅暴露原始TCP到脚本，尽可能考虑到Web的约束。它也被设计为它的服务器能与HTTP服务器共享一个端口的这样一种方式，通过持有它的握手是一个有效的HTTP Upgrade请求。一个可以在概念上使用其他协议来建立客户端-服务器消息，但WebSocket的意图是提供一个相对简单的协议，可以与现有HTTP和部署的HTTP基础设施（例如代理）同时存在，并尽可能接近TCP，且对于使用考虑到安全考虑的这样的基础设施同样是安全的，有针对性的补充以简化使用并保持简单的事情简单（如增加的消息语义）。

协议的目的是为了可扩展；未来版本将可能引入额外的概念如复用（multiplexing）。
## 1.6.安全模型
本节是非规范的。

WebSocket协议使用浏览器使用的来源模型限制web页面可以与WebSocket服务器通信，当WebSocket协议是从一个web页面使用。当然，当WebSocket协议被一个独立的客户端直接使用时（也就是，不是从浏览器中的一个web页面），来源模型不再有用，因为客户端可以提供任意随意的来源字符串。

该协议的目的是无法与现有的协议如SMTP[[RFC5321](http://tools.ietf.org/html/rfc5321)]和HTTP建立一个连接，同时允许HTTP服务器来选择支持该协议如果想要。这是通过具有严格的和详尽的握手和通过限制在握手完成之前能被插入到连接的数据（因此限制多少服务器可以被应用）实现的。

当数据是来自其他协议时，同样的目的是无法建立连接的，尤其发送到一个WebSocket服务器的HTTP，例如，如果一个HTML“表单”提交到WebScoket服务器可能会发生。这主要通过要求服务器验证它读取的握手来实现，它只能做 如果握手包含适当的部分，只能通过一个WebScoket客户端发送。尤其是，在写本规范的时侯，|Sec-|开头的字段不能由web浏览器的攻击者设置，仅能使用HTML和JavaScript API，例如XMLHttpRequest [[XMLHttpRequest](http://tools.ietf.org/html/rfc6455#ref-XMLHttpRequest)]。
## 1.7.与TCP和HTTP的关系
本节是非规范的。

WebSocket协议是一个独立的基于TCP的协议。它与HTTP唯一的关系是它的握手是由HTTP服务器解释为一个Upgrade请求。

默认情况下，WebSocket协议使用端口80用于常规的WebSocket连接和端口443用于WebSocket连接的在传输层安全（TLS）[[RFC2818](http://tools.ietf.org/html/rfc2818)]之上的隧道化。
## 1.8.建立连接
本节是非规范的。

当一个连接到一个HTTP服务器共享的端口时（这种情况是很可能在传输信息到端口80和443出现），连接将出现在HTTP服务器，是一个正常的具有一个Upgrade提议的GET请求。在相对简单的安装，只用一个IP地址和单台服务器用于所有数据传输到单个主机名，这可能允许一个切实可行的办法对基于WebSocket协议的系统进行部署。在更复杂的安装（例如，负载均衡和多服务器），一组独立的用于WebSocket连接的主机从HTTP服务器分离出来可能更容易管理。在写该规范的时候，应该指出的是，在端口80和443上的连接有明显不同的成功率，对于在端口443上的连接是明显更有可能成功，尽管这可能会随着时间而改变。
## 1.9.使用WebSocket协议的子协议
本节是非规范的。

客户端可能通过包含|Sec-WebSocket-Protocol|字段在它的握手中使用一个特定的子协议请求服务器。如果它被指定，服务器需要在它的响应中包含同样的字段和一个选择的子协议值用于建立连接。

这些子协议名字应该按照11.5节被注册。为了避免潜在的碰撞，推荐使用包含ASCII版本的子协议发明人的域名的名字。 例如，如果Example公司要创建一个Chat子协议，由Web上的很多服务器实现，它们可能命名它为“chat.example.com”。如果Example组织命名它们的竞争子协议为“chat.example.org”，那么两个子协议可能由服务器同时实现，因为服务器根据客户端发送的值动态地选择使用哪一个子协议。

通过改变子协议的名字，子协议可以以向后不兼容方式版本化，例如，要从“bookings.example.net”到“v2.bookings.example.net”。就WebSocket客户端而言，这些子协议将被视为是完全不同的。向后兼容的版本可以通过重用相同的子协议字符串实现，但要仔细设置实际的子协议以支持这种可扩展性。
