 JSP中一共预先定义了9个这样的对象，分别为：request、response、session、application、out、pagecontext、config、page、exception
1、request对象
request 对象是 javax.servlet.httpServletRequest类型的对象。 该对象代表了客户端的请求信息，主要用于接受通过HTTP协议传送到服务器的数据。（包括头信息、系统信息、请求方式以及请求参数等）。request对象的作用域为一次请求。
2、response对象
response 代表的是对客户端的响应，主要是将JSP容器处理过的对象传回到客户端。response对象也具有作用域，它只在JSP页面内有效。
3、session对象
session 对象是由服务器自动创建的与用户请求相关的对象。服务器为每个用户都生成一个session对象，用于保存该用户的信息，跟踪用户的操作状态。session对象内部使用Map类来保存数据，因此保存数据的格式为 “Key/value”。 session对象的value可以使复杂的对象类型，而不仅仅局限于字符串类型。
4、application对象
 application 对象可将信息保存在服务器中，直到服务器关闭，否则application对象中保存的信息会在整个应用中都有效。与session对象相比，application对象生命周期更长，类似于系统的“全局变量”。
5、out 对象
out 对象用于在Web浏览器内输出信息，并且管理应用服务器上的输出缓冲区。在使用 out 对象输出数据时，可以对数据缓冲区进行操作，及时清除缓冲区中的残余数据，为其他的输出让出缓冲空间。待数据输出完毕后，要及时关闭输出流。
6、pageContext 对象
pageContext 对象的作用是取得任何范围的参数，通过它可以获取 JSP页面的out、request、reponse、session、application 等对象。pageContext对象的创建和初始化都是由容器来完成的，在JSP页面中可以直接使用 pageContext对象。
7、config 对象
config 对象的主要作用是取得服务器的配置信息。通过 pageConext对象的 getServletConfig() 方法可以获取一个config对象。当一个Servlet 初始化时，容器把某些信息通过 config对象传递给这个 Servlet。 开发者可以在web.xml 文件中为应用程序环境中的Servlet程序和JSP页面提供初始化参数。
8、page 对象
page 对象代表JSP本身，只有在JSP页面内才是合法的。 page隐含对象本质上包含当前 Servlet接口引用的变量，类似于Java编程中的 this 指针。
9、exception 对象
exception 对象的作用是显示异常信息，只有在包含 isErrorPage="true" 的页面中才可以被使用，在一般的JSP页面中使用该对象将无法编译JSP文件。excepation对象和Java的所有对象一样，都具有系统提供的继承结构。exception 对象几乎定义了所有异常情况。在Java程序中，可以使用try/catch关键字来处理异常情况； 如果在JSP页面中出现没有捕获到的异常，就会生成 exception 对象，并把 exception 对象传送到在page指令中设定的错误页面中，然后在错误页面中处理相应的 exception 对象。
一,什么是内置对象?
在jsp开发中会频繁使用到一些对象,如ServletContext HttpSession PageContext等.如果每次我们在jsp页面中需要使用这些对象都要自己亲自动手创建就会特别的繁琐.SUN公司因此在设计jsp时,在jsp页面加载完毕之后自动帮开发者创建好了这些对象,开发者只需要使用相应的对象调用相应的方法即可.这些系统创建好的对象就叫做内置对象.
在servlet程序中,如果开发者希望使用session对象,必须通过request.getSession()来得到session对象;而在jsp程序中,开发中可直接使用session(系统帮我们创建好的session对象的名字就叫session)调用相应的方法即可,如:session.getId().
二,九大内置对象到底是哪九大呢?
[plain] view plain copy
1.	内置对象名          类型
2.	request        HttpServletRequest
3.	response       HttpServletResponse
4.	config         ServletConfig
5.	application    ServletContext
6.	session        HttpSession
7.	exception      Throwable
8.	page           Object(this)
9.	out            JspWriter
10.	pageContext    PageContext
三,解析几个内置对象
1)out对象对象,对象类型是JspWriter类,相当于带缓存的PrintWriter(不带缓存)
PrintWriter:write("内容")           直接向浏览器输出内容
JspWriter:writer("内容")            向jsp缓冲区写出内容
JspWriter当满足以下条件时之一时,缓冲区的内容写出:
a,缓冲区满了
b,刷新缓冲区
c,关闭缓冲区
d,jsp页面执行完毕
2)pageContext对象
pageContext的对象类型是PageContext,叫jsp的上下文对象.
pageContext作用:可以获取其他八个内置对象
[plain] view plain copy
1.	//示例:
2.	pageContext.getOut();
3.	pageContext.getServletConfig()
使用场景:在自定义标签时会频繁使用到PageContext对象;或者是定义一个方法需要用到多个对象时,传一个pageContext对象就能解决问题.
四,JSP中四大域对象
分类:
[plain] view plain copy
1.	ServletContext     context域
2.	HttpServletRequet  request域
3.	HttpSession        session域     --前三种在学习Servlet时就能接触到
4.	PageContext        page域     --jsp学习的
域对象的作用:保存数据,获取数据,共享数据.
保存数据:
[plain] view plain copy
1.	pageContext.setAttribute("内容");//默认保存到page域
2.	pageContext.setAttribute("内容",域范围常量);//保存到指定域中
3.	//四个域常量
4.	PageContext.PAGE_SCOPE
5.	PageContext.REQUEST_SCOPE
6.	PageContext..SESSION_SCOPE
7.	PageContext.APPLICATION_SCOPE
获取数据:
1.	pageContext.getAttribute("内容");
pageContext.getAttribute("name",域范围常量);
//自动在四个域中搜索数据 pageContext.findAttribute("内容");//在四个域中自动搜索数据,顺序:page域->request域->session域->application域(context域)
域作用范围:
[plain] view plain copy
1.	page域:    只能在当前jsp页面使用                (当前页面)
2.	request域: 只能在同一个请求中使用               (转发)
3.	session域: 只能在同一个会话(session对象)中使用  (私有的)
4.	context域: 只能在同一个web应用中使用            (全局的)
