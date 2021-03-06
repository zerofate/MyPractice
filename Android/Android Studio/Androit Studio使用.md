## 配置
### 新建类抬头内容更改
Settings -> Editor -> Code Style -> File and Code Templates -> Includes -> File Header    
该文件定义了类抬头的内容，但真正将 File Header 文件引入 Class 文件的是    
Settings -> Editor -> Code Style -> File and Code Templates -> Files -> Class    

如：按照阿里 Java 编码规约自动添加作者和日期，可以将 File Header 内容修改为：  
```java
/**
 * @author ${USER}
 * @date ${DATE}
 */
```

## 使用技巧
### TODO与自定义
在 AS 编辑器中输入 todo，将可以选择快速生成一条 TODO，然后显示在 TODO 窗口中。todo 的实际也是一个模板，它定义在 Live Templates 的配置中，类似的还有 fixme，根据实际开发需求，我们也可以仿照它的语法来自定义我们的注释（如），并显示在 TODO 窗口。  

参考：    
[Android Studio 必备技巧：TODO 用法及自定义 TODO](http://blog.csdn.net/my_truelove/article/details/72857949#三-android-studio-fixme-用法)



### 模拟应用被系统杀死

Logcat 窗口 -> Terminate Application



### 删除未使用的 import

快捷键 Ctrl + Alt + O（Windows），Control + Alt + O（Mac）

自动删除：Settings->Editor->Auto Import->Optimize Imports on the fly

## 快捷键
### 自带常用
| 功能                    | Windows          | Mac           |
| --------------------- | ---------------- | ------------- |
| 大小写转换                 | Ctrl + Shift + U | ⌘ + Shift + U |
| 打开设置                  | Ctrl + Alt + S   | ⌘ + ,         |
| 类型层级（Type Hierarchy）  | Ctrl + H         |               |
| 调用层级（Call Hierarchy）  | Ctrl + Alt + H   |               |
| 搜索源代码、数据库、操作和用户界面的元素等 | Shift + Shift    | ⇧ + ⇧         |
| 最近文件                  | Ctrl + E         | ⌘ + E         |
| 格式化                   | Ctrl + Shift + L | ⌥ + ⌘ + L     |
| 前一 tab                |                  | ⇧ + ⌘ + [     |
| 后一 tab                |                  | ⇧ + ⌘ + ]     |
| 查看文件结构（如类）            | Ctrl + F12       |               |
|                       |                  |               |
### 修改
| 功能                          | Windows        | Mac                 |
| --------------------------- | -------------- | ------------------- |
| 新建 Java 类                   | Alt+ Shift+1   | command + Shift + 1 |
| 新建布局                        | Alt+ Shift+2   | command + Shift + 2 |
| 添加文档注释（Fix doc comment）     | Alt+ Shift + J | command + Shift + J |
| doc 弹窗（Quick Documentation） | Alt + Q        | ⌥ + Q               |
| 前进                          |                | ⌘ + ]               |
| 后退                          |                | ⌘ + [               |
| implement 方法                |                | ⌥ + I               |
| 打开设置                        | Alt + ,        |                     |
| 将布局属性导出(extract)为 Style     | Ctrl + Alt + S |                     |

