# C#错误
- 当请求SSL资源返回如下错误时：An existing connection was forcibly closed by the remote host
  - http://stackoverflow.com/questions/4137106/are-there-net-implementation-of-tls-1-2

- 解决方法
  - 在代码中加上下面的代码，指定SSL1.2
```
System.Net.ServicePointManager.SecurityProtocol = SecurityProtocolType.Tls12 | SecurityProtocolType.Tls11 | SecurityProtocolType.Tls; // comparable to modern browsers
```


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
  
- MVC传递匿名参数
  ```
    //传递匿名对象
    @Html.Partial("~/Views/Shared/_CustomerSupport.cshtml", new { btnId = "msgus-mb" })
    
    //反射获取btnId值
    <a herf="#" id="@Model.GetType().GetProperty("btnId").GetValue(Model, null).ToString()" class="fauxA"> Message Us</a> 
  ```

- icon svg字体生成
  - https://icomoon.io/app/#/select

- web fonts字体转换
  - https://www.web-font-generator.com
