# Newtonsoft.Json 序列化Key首字母小写
```
_settings = new JsonSerializerSettings
            {
                NullValueHandling = NullValueHandling.Include,
                ContractResolver = new CamelCasePropertyNamesContractResolver()
            };
```


# Newtonsoft.Json 序列化空值转成Empty值

```
_settings = new JsonSerializerSettings
            {
                ContractResolver = new NullToEmptyStringResolver(),
            };
```

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Reflection;
using Newtonsoft.Json;
using Newtonsoft.Json.Serialization;

namespace ProfileExport.Base
{
    public class NullToEmptyStringResolver : CamelCasePropertyNamesContractResolver
    {
        /// <summary>
        /// just override the function to convert string from null to empty string
        /// </summary>
        /// <param name="member"></param>
        /// <returns></returns>
        protected override IValueProvider CreateMemberValueProvider(MemberInfo member)
        {
            return new NullToEmptyStringValueProvider((PropertyInfo)member);
        }
    }

    public class NullToEmptyStringValueProvider : IValueProvider
    {
        PropertyInfo _MemberInfo;
        public NullToEmptyStringValueProvider(PropertyInfo memberInfo)
        {
            _MemberInfo = memberInfo;
        }

        public object GetValue(object target)
        {
            object result = _MemberInfo.GetValue(target);
            if (_MemberInfo.PropertyType == typeof(string) && result == null) result = "";
            if (!_MemberInfo.PropertyType.ToString().ToLower().Substring(0, 7).Equals("system.") && result == null) result = new { };

            return result;
        }

        public void SetValue(object target, object value)
        {
            _MemberInfo.SetValue(target, value);
        }
    }
}

```

# 设置日期格式为ISO
```
设置：JsonSerializerSettings
options.Settings.DateFormatString = "yyyy-MM-ddTHH:mm:ss.fffZ";


C# 设置DateTime.ToString("yyyy-MM-ddTHH:mm:ss.fffZ");
```
