本规范定义了两个URI方案，使用定义在[RFC5234](http://tools.ietf.org/html/rfc5234)[[RFC5234](http://tools.ietf.org/html/rfc5234)]中的ABNF句法、和术语和由URI规范[RFC 3986](http://tools.ietf.org/html/rfc3986) [[RFC3986](http://tools.ietf.org/html/rfc3986)]定义的ABNF制品。

          ws-URI = "ws:" "//" host [ ":" port ] path [ "?" query ]
          wss-URI = "wss:" "//" host [ ":" port ] path [ "?" query ]

          host = <host, defined in [RFC3986], Section 3.2.2>
          port = <port, defined in [RFC3986], Section 3.2.3>
          path = <path-abempty, defined in [RFC3986], Section 3.3>
          query = <query, defined in [RFC3986], Section 3.4>

端口组件是可选的；用于“WS”的默认端点是80，而用于“WSS”默认端口是443。

如果方案组件不区分大写匹配“wss”，URI被称为“安全的”（它是说，“设置了安全标记”）。

“resource-name”（在4.1节也称为/resource name/）可以通过连接以下来构造：

 o  "/"  如果路径组件是空

 o  路径组件

 o  "?" 如果查询组件是非空

 o  查询组件

片段（译者注：# Fragment）标识符在WebSocket URI中是无意义的且禁止在这些URI上。任何URI方案，字符“#”，当不表示片段开始时，必须被转义为%23。