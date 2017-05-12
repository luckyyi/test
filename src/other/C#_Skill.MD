# C#错误
- 当请求SSL资源返回如下错误时：An existing connection was forcibly closed by the remote host
  - http://stackoverflow.com/questions/4137106/are-there-net-implementation-of-tls-1-2

- 解决方法
  - 在代码中加上下面的代码，指定使用3种SSL(1.0 | 1.1 | 1.2)
  
  `System.Net.ServicePointManager.SecurityProtocol = SecurityProtocolType.Tls12 | SecurityProtocolType.Tls11 | SecurityProtocolType.Tls; // comparable to modern browsers
  `

  - http://stackoverflow.com/questions/28286086/default-securityprotocol-in-net-4-5
  - To turn on TLS 1.1 and 1.2 without affecting other protocols:
  
  `System.Net.ServicePointManager.SecurityProtocol |= SecurityProtocolType.Tls11 | SecurityProtocolType.Tls12;`

- NServiceBus 在命令行运行时报错 Index was outside the bounds of the array.
  - https://github.com/Particular/NServiceBus/issues/1964
  - V4.4.0的Bug，在命令行运行要用双引号把执行路径包起来。
  
  
- NHibernate的子对象为空时报错： NHibernate.ObjectNotFoundException: No row with the given identifier exists
  - 在Mapping的代码加上 .NotFound.Ignore();
  
 
# C#技巧
- App.Config，各个环境不同配置的覆盖。
  - 首先安装Extensions and updates : SlowCheetah
  - 再在工具环境下拉中选择：Configuration Manager.. New几个不同的环境：QA、STG、PROD。
  - 然后，点击项目中的App.Config，右键选择：Add transform即可。
  - 在不同的环境中，只需在对应的节点或子节点中加上 xdt:Transform="Replace"即可。
  - ****** 还有可以SetAttribute，修改指定属性值

- 轻量级开源ORM: Dapper
  - http://www.tuicool.com/articles/BVj26v
  - https://github.com/StackExchange/dapper-dot-net

- 同步执行Async方法
  - 在异步方法中直接用 .Result 去获取数据，有时会无限等待，最好用下面的类。
  - http://stackoverflow.com/questions/5095183/how-would-i-run-an-async-taskt-method-synchronously
  - https://social.msdn.microsoft.com/Forums/en-US/163ef755-ff7b-4ea5-b226-bbe8ef5f4796/is-there-a-pattern-for-calling-an-async-method-synchronously?forum=async 
  
  - **如果在子线程中使用主线程的线程的时候，就会无限等待，这种Case在子线程中New一个Task.Run就OK了**


- MVC传递匿名参数

  ```//传递匿名对象
  @Html.Partial("~/Views/Shared/_CustomerSupport.cshtml", new { btnId = "msgus-mb" })
  //反射获取btnId值
  <a herf="#" id="@Model.GetType().GetProperty("btnId").GetValue(Model, null).ToString()" class="fauxA"> Message Us</a>
  ```
  
- Url中去除指定参数

  ```
  NameValueCollection filtered = HttpUtility.ParseQueryString(HttpContext.Current.Request.Url.Query);
  filtered.Remove("Language");

  var uri = Request.Url.AbsolutePath + "?" + filtered.ToString();
  ```
  
- 枚举及为什么要用1，2，4，8这些2的n次幂来表示枚举的值
  - 枚举使用组合形式，这个时候一般需要为枚举加上[Flags]特性标记为位域，例如： 
  
    ```
    [Flags]  
    enum Styles{  
    ShowBorder = 1,         //是否显示边框 
    ShowCaption = 2,        //是否显示标题 
    ShowToolbox = 4         //是否显示工具箱 
    } 
    ```
    
　　这样我们就可以用"或"运算符组合多个状态，例如 myControl.Style = Styles.ShowBorder | Styles.ShowCaption;  
　　这时myControl.Style枚举的值将变成 1+2=3，它的ToString()将变成"Styles.ShowBorder , Styles.ShowCaption" 
　　这里我们可以解释为什么第三个值ShowToolbox可以为4,5..而不能为3。也就是说它的值不应该是前几项值的复合值。有一个比较简单的方法就是用2的n次方来依次为每一项赋值，例如 1,2,4,8,16,32,64..... 
    现在举个常见的Flags应用例子。例如一个简单的权限系统，有"Admin"和"User"两种角色，我们可以在表中放一个varchar()字段，以文本形式存放权限字"Admin,User"。但是用Flags型枚举的话，我们就可以直接将 Roles.Admin | Roles.User 的值放在一个int字段里。
    
检查枚举是否包含某个元素：
```
    var style = (Styles)7;
    bool hasFlag = ((style & Styles.ShowBorder) != 0);
```
其实我们还会碰到一种情况，就是需要从组合状态中去掉一个元素。
```
    style = style & (~Styles.ShowBorder) //可以方便去掉一个元素。
```
最简单的加减方法
```
style |= Styles.ShowBorder; //加Flag
style &= ~Styles.ShowBorder;  //减去Flag
```

在SQL中也支持与或运算
```
Update [dbo].[Settings]
 SET [style] &= ([style] ^ 8)  //减去Flag值
 
Update [dbo].[Settings]
 SET [style] = ([style] ^ 8)
 WHERE [style] & 8 = 0  //没有就加上Flag值
```

- 枚举加自定义属性
  - `http://blog.csdn.net/fanbin168/article/details/51576581`

- icon svg字体生成
  - https://icomoon.io/app/#/select

- web fonts字体转换
  - https://www.web-font-generator.com

- 如何搭建一个 HTTPS 服务端
  - http://www.tuicool.com/articles/QFnU7za

- FluentNHibernate
  - http://blog.csdn.net/eqera/article/details/8412261
