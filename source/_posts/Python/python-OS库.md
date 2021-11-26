---
title: python OS库
date: 2021-11-14 14:15:57
tags: Python
---

  在自动化测试中，经常需要查找操作文件，比如说查找配置文件（从而读取配置文件的信息），查找测试报告（从而发送测试报告邮件），经常要对大量文件和大量路径进行操作，这就依赖于os模块, 下面简单介绍下os模块的一些常用函数：

#### 1. os.name（）
描述：显示当前使用的平台，'nt'表示Windows，'posix' 表示Linux

语法：os.name

os.name
'nt'


#### 2. os.getcwd（）
描述：返回当前进程的工作目录。

语法：os.getcwd()

os.getcwd()
'C:\\Users\\wuzhengxiang'


#### 3. os.chdir（）
描述：改变当前工作目录到指定的路径。

语法：os.chdir(path)

#查看当前目录
os.getcwd()
'C:\\Users\\wuzhengxiang'


#重新设置当前工作空间
os.chdir('C:/Users/wuzhengxiang/Desktop/股票数据分析')


#再次查看当前目录，已经变成新的了
os.getcwd()
'C:\\Users\\wuzhengxiang\\Desktop\\股票数据分析

#### 4. os.makedirs（）
描述：方法用于递归创建目录。像 mkdir(), 但创建的所有intermediate-level文件夹需要包含子目录。

语法：os.makedirs(path, mode=0o777)

os.makedirs('C:/Users/wuzhengxiang/Desktop/股票数据分析/1122', mode=0o777)


#### 5. os.mkdir（）
描述：以数字权限模式创建目录。默认的模式为 0777 (八进制)。

语法：os.mkdir(path[, mode])

#创建新的目2233
os.mkdir('C:/Users/wuzhengxiang/Desktop/股票数据分析/2233', mode=0777  )

#### 6. os.listdir（）
描述：列出目录下的所有文件和文件夹

语法：os.listdir（path）

os.listdir('C:/Users/wuzhengxiang/Desktop/股票数据分析')
['ETF研究.py', 'foo.txt', 'pi.txt', 'render.html']


os.listdir('.') 
['ETF研究.py', 'foo.txt', 'pi.txt', 'render.html']

#### 7. os.remove（）
描述：用于删除指定路径的文件。如果指定的路径是一个目录，将抛出OSError。

语法：os.remove(path)

os.remove('C:/Users/zhengxiang.wzx/Desktop/timg.jpg')

#### 8. os.rename（）
描述：命名文件或目录,能对相应的文件进行重命名

语法：os.rename(src, dst)

参数

src -- 要修改的目录名
dst -- 修改后的目录名
#空间设置
data_path = 'C:/Users/zhengxiang.wzx/Desktop/微博情绪识别'
os.chdir(data_path)#设置工作空间
os.getcwd()
'C:\\Users\\zhengxiang.wzx\\Desktop\\微博情绪识别'
os.rename("图片下载.py","图片下载1.py")

#### 9. os.renames()
描述：用于递归重命名目录或文件。类似rename()。既可以重命名文件, 也可以重命名文件的上级目录名

语法：os.renames(old, new)

参数：

old -- 要重命名的目录
new --文件或目录的新名字。甚至可以是包含在目录中的文件，或者完整的目录树。
os.chdir('C:/Users/wuzhengxiang/Desktop/Python知识点总结')
os.getcwd()


#文件夹和文件同时命名
os.renames("test/Python 63个内置函数详解.py","test2/内置函数详解.py")


os.listdir()
['kaggle',
 'test2',
 '股票分析',
 '课程资源'

#### 10. os.linesep()
描述：当前平台用于分隔（或终止）行的字符串。它可以是单个字符，如 POSIX 上是 '\n'，也可以是多个字符，如 Windows 上是 '\r\n'。在写入以文本模式（默认模式）打开的文件时，请不要使用 os.linesep 作为行终止符，请在所有平台上都使用一个 '\n' 代替。

语法：os.linesep

os.linesep
'\r\n'

#### 11. os.pathsep()
描述：操作系统通常用于分隔搜索路径（如 PATH）中不同部分的字符，如 POSIX 上是 ':'，Windows 上是 ';'。在 os.path 中也可用。

语法：os.pathsep

os.pathsep
';'
 

#### 12. os.close（）
描述：关闭指定的文件描述符 fd

语法：os.close(fd)

fd = os.open( "foo.txt", os.O_RDWR|os.O_CREAT )
os.write(fd, bytes("This is test", encoding = "utf8"))
os.close( fd )


#### 13. os.stat（）
描述：获取文件或者目录信息

语法：os.stat(path)

os.stat('C:/Users/wuzhengxiang/Desktop/股票数据分析\\pi.txt')
os.stat_result(st_mode=33206, st_ino=22236523160361562, st_dev=2419217970, st_nlink=1, st_uid=0, st_gid=0, st_size=53, st_atime=1589638199, st_mtime=1589638199, st_ctime=1581868007)

#### 14. os.sep()
描述：显示当前平台下路径分隔符,在 POSIX 上是 '/'，在 Windows 上是是 '\\'

语法：os.sep

os.sep
'\\'

#### 15. os.path.abspath()
描述：返回文件的绝对路径

语法：os.path.abspath(path)

#Excel文件
os.path.abspath('all_data.xlsx') 
'C:\\Users\\zhengxiang.wzx\\all_data.xlsx'


#图片文件
os.path.abspath('IMG_7358.JPG') 
'C:\\Users\\zhengxiang.wzx\\IMG_7358.JPG'

#### 16. os.path.basename()
描述：返回文件名，纯粹字符串处理逻辑，路径错误也可以

语法：os.path.basename(path)

os.path.basename('C:\\Users\\zhengxiang.wzx\\all_data.xlsx')
'all_data.xlsx'


#### 17. os.path.commonprefix()
描述：返回list(多个路径)中，所有path共有的最长的路径

语法：os.path.commonprefix(list)

os.path.commonprefix(['http://c.biancheng.net/python/aaa', 'http://c.biancheng.net/shell/'])
'http://c.biancheng.net/'


os.path.commonprefix(['http://bianc/python/aaa', 'http://c.biancheng.net/shell/'])
'http://'

#### 18. os.path.dirname()
描述：返回文件路径

语法：os.path.dirname(path)

os.path.dirname('C://my_file.txt')
 'C://'


os.path.dirname('C://python//my_file.txt')
'C://python'

#### 19. os.path.exists()
描述：如果路径 path 存在，返回 True；如果路径 path 不存在，返回 False。

语法：os.path.exists(path)

os.path.exists('C:/Users/wuzhengxiang/Desktop/股票数据分析/pi.txt')
True


os.path.exists('C:/Users/wuzhengxiang/Desktop/股票数据分析/')
True


os.path.exists('C:/Users/wuzhengxiang/Desktop/股票数据分析/pi_01.txt')
Fals

#### 20. os.path.lexists()
描述：路径存在则返回True，路径损坏也返回True， 不存在，返回 False。

语法：os.path.lexists

os.path.lexists('C:/Users/wuzhengxiang/Desktop/股票数据分析/pi.txt')
True


os.path.lexists('C:/Users/wuzhengxiang/Desktop/股票数据分析/pi_01.txt')
False

#### 21. os.path.expanduser()
描述：把path中包含的"~"和"~user"转换成用户目录

语法：os.path.expanduser(path)

os.path.expanduser('~/wuzhengxiang/Desktop/股票数据分析/')
'C:\\Users\\wuzhengxiang/wuzhengxiang/Desktop/股票数据分析/'

#### 22. os.path.expandvars()
描述：根据环境变量的值替换path中包含的"$name"和"${name}"

语法：os.path.expandvars(path)

os.environ['KITTIPATH'] = 'D:/thunder'
path = '$KITTIPATH/train/2011_09_26_drive_0001_sync/proj_depth/velodyne_raw/image_02/0000000013.png'
os.path.expandvars(path)
'D:/thunder/train/2011_09_26_drive_0001_sync/proj_depth/velodyne_raw/image_02/0000000013.png'

#### 23. os.path.getatime()
描述：返回最近访问时间（浮点型秒数），从新纪元到访问时的秒数。

语法：os.path.getatime(path)

os.path.getatime('C:/Users/wuzhengxiang/Desktop/股票数据分析/pi.txt')
1589638199.1343248


#### 24. os.path.getmtime()
描述：返回最近文件修改时间，从新纪元到访问时的秒数。

语法：os.path.getmtime(path)

os.path.getmtime('C:/Users/wuzhengxiang/Desktop/股票数据分析/pi.txt')
1583069050.8148942 

#### 25. os.path.getctime()
描述：返回文件 path 创建时间，从新纪元到访问时的秒数。

语法：os.path.getctime(path)

os.path.getctime('C:/Users/wuzhengxiang/Desktop/股票数据分析/pi.txt')
1581868007.6123319

#### 26. os.path.getsize()
描述：返回文件大小，如果文件不存在就返回错误

语法：os.path.getsize(path)

os.path.getsize('C:/Users/wuzhengxiang/Desktop/股票数据分析/test.gif')
1128677

#### 27. os.path.isabs()
描述：判断是否为绝对路径，也就是说在WIndow系统下，如果输入的字符串以" / "开头，os.path.isabs()就会返回True

语法：os.path.isabs(path)

os.path.isabs('D:/thunder')
True


os.path.isabs('D:\thunder')
False


os.path.isabs('D:\\thunder')
Tru

#### 28. os.path.isfile()
描述：判断路径是否为文件

语法：os.path.isfile(path)

#文件不存在 返回False
os.path.isfile("C:/Users/wuzhengxiang/Desktop/股票数据分析/pi_01.txt")
False


os.path.isfile("C:/Users/wuzhengxiang/Desktop/股票数据分析/pi.txt")
True


#不是文件 返回False
os.path.isfile("C:/Users/wuzhengxiang/Desktop/股票数据分析/")
Fals

#### 29. os.path.isdir()
描述：判断路径是否为目录

语法：os.path.isdir(path)

os.path.isdir('C:/Users/wuzhengxiang/Desktop/股票数据分析')   
True


os.path.isdir('C:/Users/wuzhengxiang/Desktop/股票数据分析1')   
False


os.path.isdir('C:/Users/wuzhengxiang/Desktop/股票数据分析/pi.txt')   
Fals

#### 30. os.path.join()
描述：把目录和文件名合成一个路径,1.如果各组件名首字母不包含’/’，则函数会自动加上,2.如果有一个组件是一个绝对路径，则在它之前的所有组件均会被舍弃,3.如果最后一个组件为空，则生成的路径以一个’/’分隔符结尾

语法：os.path.join(path1[, path2[, ...]])

os.path.join('C:/Users','wuzhengxiang/Desktop/','股票数据分析')
'C:/Users\\wuzhengxiang/Desktop/股票数据分析'


Path1 = 'home'
Path2 = 'develop'
Path3 = 'code'


Path10 = Path1 + Path2 + Path3
Path20 = os.path.join(Path1,Path2,Path3)
print ('Path10 = ',Path10)
print ('Path20 = ',Path20)


Path10 =  homedevelopcode
Path20 =  home\develop\co

#### 31. os.path.normcase()
描述：转换path的大小写和斜杠

语法：os.path.normcase(path)

os.path.normcase('D:\Python\test\data.txt')
'd:\\python\test\\data.txt'


os.path.normcase('c:/WINDOWS\\system64\\')
'c:\\windows\\system64\\'

#### 32. os.path.normpath()
描述：规范path字符串形式

语法：os.path.normpath(path)

os.path.normpath('c://windows\\System32\\../Temp/')
'c:\\windows\\Temp'

#### 33. os.path.realpath()
描述：返回path的真实路径

语法：os.path.realpath(path)

os.path.relpath('C:\\Users\\Administrat\\代码TRY\\test.ipynb', '代码TRY')
'..\\..\\..\\..\\Administrat\\代码TRY\\test.ipynb'
#### 34. os.path.relpath()
描述：返回从当前目录或 start 目录（可选）到达 path 之间要经过的相对路径。这仅仅是对路径的计算，不会访问文件系统来确认 path 或 start 的存在性或属性。

语法：os.path.relpath(path[, start])

os.path.relpath('C:/Users/wuzhengxiang/Desktop/股票数据分析\\test.gif')
'test.gif'

#### 35. os.path.samefile( )
描述：判断目录或文件是否相同

语法：os.path.samefile(path1, path2)

os.path.samefile('C:\\Users', 'C:\\Users')
True


os.path.samefile('C:\\Users', 'C:/Users')
True


os.path.samefile('C:\\Users', 'C:/Users/wuzhengxiang')
Fals

#### 36. os.path.split()
描述：把路径分割成 dirname 和 basename，返回一个元组

语法：os.path.split(path)

os.path.split('D:\Python\test\data.txt')
 ('D:\\Python\test', 'data.txt')

#### 37. os.path.splitdrive()
描述：一般用在 windows 下，返回驱动器名和路径组成的元组

语法：os.path.splitdrive(path)

os.path.splitdrive('C:/Users/zhengxiang.wzx/IMG_7358.JPG')
('C:', '/Users/zhengxiang.wzx/IMG_7358.JPG')

#### 38. os.path.splitext()
描述：分割路径，返回路径名和文件扩展名的元组

语法：os.path.splitext(path)

os.path.splitext('C:/Users/zhengxiang.wzx/IMG_7358.JPG')
('C:/Users/zhengxiang.wzx/IMG_7358', '.JPG')

#### 39. os.path.walk()
描述：遍历path，进入每个目录都调用visit函数，visit函数必须有3个参数(arg, dirname, names)，dirname表示当前目录的目录名，names代表当前目录下的所有文件名，args则为walk的第三个参数

语法：os.path.walk(path, visit, arg)

list(os.walk(abs_cur_dir))
[('C:/Users/wuzhengxiang/Desktop/股票数据分析',
  ['1122'],
  ['ETF研究.py', 'foo.txt', 'pi.txt', 'render.html', 'test.gif']),
 ('C:/Users/wuzhengxiang/Desktop/股票数据分析\\1122', [], [])]




#穷举遍历一个文件夹里面的所有文件，并获取文件的目录名
abs_cur_dir ='C:/Users/wuzhengxiang/Desktop/股票数据分析'
file_url=[]
for dirs,folders,files in os.walk(abs_cur_dir):
    for i in files:
            file_url.append(os.path.join(dirs,i))
            
file_url           
['C:/Users/wuzhengxiang/Desktop/股票数据分析\\ETF研究.py',
 'C:/Users/wuzhengxiang/Desktop/股票数据分析\\foo.txt',
 'C:/Users/wuzhengxiang/Desktop/股票数据分析\\pi.txt',
 'C:/Users/wuzhengxiang/Desktop/股票数据分析\\render.html',
 'C:/Users/wuzhengxiang/Desktop/股票数据分析\\test.gif']


#pathlib也能实现类似的