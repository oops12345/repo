---
title: MD语法
date: 2021-07-02 20:05:26
index_img: /img/3.png
tags: Md
categories: 技术
---

> ## 快捷键基于软件Typora

> ## 为了跳出上一个格式 切换源代码格式 
>
> ## 快捷键： CTRL + /

# 基本符号

> ##### * - +. >

> 基本上所有的markdown标记都是基于这四个符号或组合，需要注意的是，如果以基本符号开头的标记，注意基本符号后有一个用于分割标记符和内容的空格。

# 标题 （六级）

> 快捷键 CTRL +1、2、3、4、5、6

> 格式：# [空格] [文字]，标题级别取决于#个数

```xml
# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题
```

>        # 一级标题
>
> ## 二级标题
>
> ### 三级标题
>
> #### 四级标题
>
> ##### 五级标题
>
> ###### 六级标题

# 列表

## 无序列表 

- > #### 快捷键：CTRL +shift + ]

```swift
//形式一
+ a
+ b
+ c
//形式二
- d
- e
- f
//形式三
* g
* h
* i
```

> 三种形式实例

+ a
+ b
+ c
  - 1
  - 2
  - 3
    * 1
    * 2
    * 3



## 有序列表

- > #### 快捷键：CTRL +shift + [

```cpp
//正常形式
1. abc
2. bcd
3. cde
//错序效果
2. fgh
3. ghi
5. hij
```

> 形式实例：

1. 1
2. 2
3.  3
   2. 2
      3. 3
         5. w

## 嵌套列表

> # 不再赘述

# 引用

> ### 快捷键 ：CTRL +SHIFT + Q

> #  > 引用

> 引用

> ```undefined
> > 引用内容、说明内容。在语句前面加一个 > ，注意是英文的那个右尖括号，注意空格，引用因为是一个区块，理论上是应该什么内容都可以放，比如说：标题，列表，引用等等。
> ```

```ruby
> 一级引用
>> 二级引用
>>> 三级引用
>>>> 四级引用
>>>>> 五级引用
>>>>>> 六级引用
```

# 代码块

## 一行代码

> 快捷键 ：CTRL +shift + `

> # ` code`

```go
` code`
```

## 多行代码

快捷键 ：CTRL +SHIFT + K

~~~go
    ```
        123
        123
        123
        123
        123
    ```
~~~

```
        123
        123
        123
        123
        123
```

# 链接

快捷键 ：

1. 行内式
   链接的文字放在[]中，链接地址放在随后的()中，链接也可以带title属性，链接地址后面空一格，然后用引号引起来

   ```csharp
   [文字](https://www.jianshu.com),
   ```

2. 参数式
   链接的文字放在[]中，链接地址放在随后的:后，链接地址后面空一格，然后用引号引起来

```csharp
[简书]: https://www.jianshu.com "创作你的创作"
[简书]是一个创作社区,任何人均可以在其上进行创作。用户在简书上面可以方便的创作自己的作品,互相交流。
//参数定义的其他写法
[简书]: https://www.jianshu.com '创作你的创作'
[简书]: https://www.jianshu.com (创作你的创作)
[简书]: <https://www.jianshu.com> "创作你的创作"
```

# 图片

1. 行内式
   和链接的形式差不多，图片的名字放在[]中，图片地址放在随后的()中，title属性（图片地址后面空一格，然后用引号引起来）,注意的是[]前要加上!

```ruby
![图片名称](图片链接)
```

1. 参数式
   图片的文字放在[]中，图片地址放在随后的:后，title属性（图片地址后面空一格，然后用引号引起来）,注意引用图片的时候在[]前要加上!

```csharp
[my-logo.png]: https://upload-images.jianshu.io/upload_images/13623636-6d878e3d3ef63825.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240 "my-logo"
![my-logo.png]
//参数定义的其他写法
[my-logo.png]: https://upload-images.jianshu.io/upload_images/13623636-6d878e3d3ef63825.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240 'my-logo'
[my-logo.png]: https://upload-images.jianshu.io/upload_images/13623636-6d878e3d3ef63825.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240 (my-logo)
[my-logo.png]: <https://upload-images.jianshu.io/upload_images/13623636-6d878e3d3ef63825.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240> "my-logo"
```

# 分割线

分割线可以由* - _（星号，减号，底线）这3个符号的至少3个符号表示，注意至少要3个，且不需要连续，有空格也可以

```undefined
---
- - -
------
***
* * *
******
___
_ _ _
______
```

# 强调字体

1. 强调字体
   一个星号或者是一个下划线包起来，会转换为<em>倾斜，如果是2个，会转换为<strong>加粗

   ```undefined
   *md*    
   **md**
   _md_   
    __md__
   ```

*md*    
**md**
_md_   
 __md__

# 删除线

> # 快捷键： alt +shift + 5

```undefined
~~删除~~
```

~~删除线删除线删除线删除线删除线删除线删除线删除线删除线删除线删除线删除线删除线删除线删除线删除线删除线删除线删除线删除线删除线删除线删除线删除线删除线删除线删除线删除线删除线删除线删除线删除线删除线删除线删除线删除线删除线删除线删除线删除线删除线删除线删除线删除线~~

# 表格

```cpp
//例子一
|123|234|345|
|:-|:-:|-:|
|abc|bcd|cde|
|abc|bcd|cde|
|abc|bcd|cde|
//例子二
|123|234|345|
|:---|:---:|---:|
|abc|bcd|cde|
|abc|bcd|cde|
|abc|bcd|cde|
//例子三
123|234|345
:-|:-:|-:
abc|bcd|cde
abc|bcd|cde
abc|bcd|cde
```

> # 展示

//例子一

| 123  | 234  |  345 |
| :--- | :--: | ---: |
| abc  | bcd  |  cde |
| abc  | bcd  |  cde |
| abc  | bcd  |  cde |
//例子二
| 123  | 234  |  345 |
| :--- | :--: | ---: |
| abc  | bcd  |  cde |
| abc  | bcd  |  cde |
| abc  | bcd  |  cde |
//例子三
| 123  | 234  |  345 |
| :--- | :--: | ---: |
| abc  | bcd  |  cde |
| abc  | bcd  |  cde |
| abc  | bcd  |  cde |
