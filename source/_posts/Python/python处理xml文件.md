---
title: python处理xml文件
date: 2021-11-14 17:08:52
tags: Python
---

简单介绍一些用python处理XML文件的函数与操作

#### 下面是一个xml文档里面的数据，我们把它保存进test0.xml这个文件

![](/images/Python/xml文件样例.jpg)

<?xml version="1.0"?>
<data>
    <country name="Liechtenstein">
        <rank>1</rank>
        <year>2008</year>
        <gdppc>141100</gdppc>
        <neighbor name="Austria" direction="E"/>
        <neighbor name="Switzerland" direction="W"/>
    </country>
    <country name="Singapore">
        <rank>4</rank>
        <year>2011</year>
        <gdppc>59900</gdppc>
        <neighbor name="Malaysia" direction="N"/>
    </country>
    <country name="Panama">
        <rank>68</rank>
        <year>2011</year>
        <gdppc>13600</gdppc>
        <neighbor name="Costa Rica" direction="W"/>
        <neighbor name="Colombia" direction="E"/>
    </country>
</data>



import xml.etree.ElementTree as ET
下面解析xml文件到tree
tree = ET.parse('test0.xml')
root其实就是xml下面的分支
root = tree.getroot()

root有一个标签和一个属性字典
print(root.tag)  # 标签 data
print(root.attrib)   # 属性字典 {},可以直接后面加[key名称]——>输出key对应的Value

root下面还有一个个分支，我们叫他child，可以遍历输出他们的标签和属性字典
for child in root:
    print(child.tag,child.attrib)

我们也可以选出我们具体想要的节点，指定其在根节点中具体的索引就好
child = root[1]
t = child[2]
当然可以直接写 t = root[1][2]
print(t.tag,t.attrib,t.text)

print(root[1].attrib)
print(root[1].attrib['name'])  


![](/images/Python/xml讲解.jpg)











参考资料：
https://blog.csdn.net/weixin_39753747/article/details/111005874
https://blog.csdn.net/weixin_36279318/article/details/79176475

