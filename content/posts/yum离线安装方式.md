+++
title = 'Yum离线安装方式'
date = 2024-05-21T17:28:02+08:00
draft = false
tags = ["Linux"]
+++


1. 找一台可以联网的yum源下载rpm安装包
```shell
yum install samba --downloaddir=/opt/samba/ --downloadonly
```

2. 本地安装命令
```shell
yum localinstall ./*.rpm
```



6I6r6I+B6YKj5Liq5aW95pCc77yM6ZmI5ZiJ6YKj5Liq5pCc5YWz6ZSu6K+NKOS7jumrmOS4reWIsOe7k+WpmueahOaHteaHguWls+WtqSnvvIzojqvoj4HpgqPkuKrmnInlsIbov5E4R+Wkp++8jOmZiOWYiemCo+S4quWPquacieS4gOS4quWkmkfvvIzmiJHkuZ/kuI3nn6XpgZPmiJHnmoTmmK/lkKflrozmlbTniYjvvIwK5piZ6Iqx57O75YiXCuWwj+S4g+Wwj+WkqSBxaXRpYW4Kbm8xc3lnaXJsCumZiOWAqeWAqe+8jOS+r+aZk+mbqgrkuI3opoHlho3niKzmpbzkuobvvIzmiJHmiorlhbPplK7or43nu5nlkITkvY3mgLvnu5Plpb3kuobvvIjosLfmrYzmkJzntKLmnIDkvbPvvIkKMS7mn7Plt57ojqvoj4HvvIjlvLrng4jmjqjojZDvvIkKMi7pvpnlj6PmiqTlo6sKMy7miJDpg73lt6XooYzlpbPpg5HnkocKNC7ovbvlkLvkuZ/po5jnhLbvvIjlvojkuYXku6XliY3nmoTmjqLoirHvvIzlvLrmjqjvvIkKNS7ljZflroHpmYjlmIkKNi7lrabpmaLmtL7lpbPnpZ4KNy7mnKrlrozlvoXnu60K5Lul5LiK6YO95piv5riF5pmw5bqm6L+Y5Y+v5Lul55qE6ICB54mH5a2Q77yM5LiN5piv546w5Zyo55qE572R57qi6IS45Y+v5q+U55qE



要将XML错误码转换为C++代码，可以使用Python中的`xml.etree.ElementTree`模块来解析XML文件，然后使用Python的字符串操作方法构建C++代码字符串，最后将C++代码字符串写入到C++源文件中。

以下是一个简单的示例代码，假设我们有一个包含XML错误码的文件`error_codes.xml`，其中每个错误码都包含`code`和`description`两个属性：

```xml
<error_codes>
  <error_code code="1000" description="Invalid input parameter"/>
  <error_code code="1001" description="Missing required parameter"/>
  <error_code code="1002" description="Invalid parameter value"/>
  <error_code code="2000" description="Database error"/>
  <error_code code="2001" description="Database connection error"/>
</error_codes>
```

我们可以使用以下Python代码解析并将其转换为C++代码：

```python
import xml.etree.ElementTree as ET

# 解析XML文件
tree = ET.parse('error_codes.xml')
root = tree.getroot()

# 构建C++代码字符串
cpp_code = ''
for child in root:
    code = child.attrib['code']
    description = child.attrib['description']
    cpp_code += f'static const int ERROR_{code} = {code}; // {description}\n'

# 将C++代码写入源文件
with open('error_codes.cpp', 'w') as f:
    f.write(cpp_code)
```

以上代码将错误码转换为一个包含静态常量的C++源文件，每个常量的名称为`ERROR_`加上错误码，值为错误码本身，注释为错误描述。

输出的C++源文件内容如下：

```c++
static const int ERROR_1000 = 1000; // Invalid input parameter
static const int ERROR_1001 = 1001; // Missing required parameter
static const int ERROR_1002 = 1002; // Invalid parameter value
static const int ERROR_2000 = 2000; // Database error
static const int ERROR_2001 = 2001; // Database connection error
```

在以上代码中，我们首先使用`ET.parse()`函数解析XML文件，然后使用`getroot()`方法获取XML根节点。接着使用`for`循环遍历XML节点，使用字典操作方法获取节点属性，并使用字符串操作方法构建C++代码字符串。最后将C++代码字符串写入到C++源文件中。