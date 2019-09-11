---
title: Regular expression简介
date: 2019-09-11 20:44:44
tags: [regular expression]
---

# Regular expression - 正则表达式 

## 简单匹配

使用正则表达式，首先需要调用python的内置模块`re`, `import re`. 这样就可以调用`re.search()`进行查找。

> `re.match(pattern, string, flags=0)`
>
> pattern: 匹配的正则表达式
>
> string: 待匹配字符串
>
> flags: 标志位，用于控制正则表达式的匹配方式，如：是否区分大小写，多行匹配等等。[详情](<http://www.runoob.com/python/python-reg-expressions.html#flags>)
>
> | re.I | 使匹配对大小写不敏感                                         |
> | ---- | ------------------------------------------------------------ |
> | re.L | 做本地化识别（locale-aware）匹配                             |
> | re.M | 多行匹配，影响 ^ 和 $                                        |
> | re.S | 使 . 匹配包括换行在内的所有字符                              |
> | re.U | 根据Unicode字符集解析字符。这个标志影响 \w, \W, \b, \B.      |
> | re.X | 该标志通过给予你更灵活的格式以便你将正则表达式写得更易于理解。 |

<!-- more -->

如

```python
import re

# regular expression
pattern1 = "cat"
pattern2 = "bird"
string = "dog runs to cat"
print(re.search(pattern1, string))  # <_sre.SRE_Match object; span=(12, 15), match='cat'>
print(re.search(pattern2, string))  # None
```

## 灵活匹配

灵活匹配才是正则表达式的核心，使用特使的pattern来灵活匹配需要找的文字。

如果需要找到潜在的多个可能性文字, 我们可以使用 `[]` 将可能的字符囊括进来. 比如 `[ab]` 就说明我想要找的字符可以是 `a` 也可以是 `b`. 这里我们还需要注意的是, 建立一个正则的规则, __我们在 pattern 的 “” 前面需要加上一个 `r` 用来表示这是正则表达式__, 而不是普通字符串. 通过下面这种形式, 如果字符串中出现 “run” 或者是 “ran”, 它都能找到.

```python
# multiple patterns ("run" or "ran")
ptn = r"r[au]n"       # start with "r" means raw string
print(re.search(ptn, "dog runs to cat"))    
# <_sre.SRE_Match object; span=(4, 7), match='run'>
```

## 按类型匹配

除了自己定义规则, 还有很多匹配的规则时提前就给你定义好了的. 下面有一些特殊的匹配类型给大家先总结一下, 然后再上一些例子.

- \d : 任何数字
- \D : 不是数字
- \s : 任何 white space, 如 [\t\n\r\f\v]
- \S : 不是 white space
- \w : 任何大小写字母, 数字和 “*” [a-zA-Z0-9*]
- \W : 不是 \w
- \b : 空白字符 (**只**在某个字的开头或结尾)
- \B : 空白字符 (**不**在某个字的开头或结尾)
- \\ : 匹配 \
- . : 匹配任何字符 (除了 \n)
- ^ : 匹配开头
- $ : 匹配结尾
- ? : 前面的字符可有可无

```python
# \d : decimal digit
print(re.search(r"r\dn", "run r4n"))           
# <_sre.SRE_Match object; span=(4, 7), match='r4n'>
#
# \D : any non-decimal digit
print(re.search(r"r\Dn", "run r4n"))           
# <_sre.SRE_Match object; span=(0, 3), match='run'>
#
# \s : any white space [\t\n\r\f\v]
print(re.search(r"r\sn", "r\nn r4n"))          
# <_sre.SRE_Match object; span=(0, 3), match='r\nn'>
#
# \S : opposite to \s, any non-white space
print(re.search(r"r\Sn", "r\nn r4n"))          
# <_sre.SRE_Match object; span=(4, 7), match='r4n'>
#
# \w : [a-zA-Z0-9_]
print(re.search(r"r\wn", "r\nn r4n"))          
# <_sre.SRE_Match object; span=(4, 7), match='r4n'>
#
# \W : opposite to \w
print(re.search(r"r\Wn", "r\nn r4n"))          
# <_sre.SRE_Match object; span=(0, 3), match='r\nn'>
#
# \b : empty string (only at the start or end of the word)
print(re.search(r"\bruns\b", "dog runs to cat"))    
# <_sre.SRE_Match object; span=(4, 8), match='runs'>
#
# \B : empty string (but not at the start or end of a word)
print(re.search(r"\B runs \B", "dog   runs  to cat"))  
# <_sre.SRE_Match object; span=(8, 14), match=' runs '>
#
# \\ : match \
print(re.search(r"runs\\", "runs\ to me"))     
# <_sre.SRE_Match object; span=(0, 5), match='runs\\'>
#
# . : match anything (except \n)
print(re.search(r"r.n", "r[ns to me"))         
# <_sre.SRE_Match object; span=(0, 3), match='r[n'>
#
# ^ : match line beginning
print(re.search(r"^dog", "dog runs to cat"))   
# <_sre.SRE_Match object; span=(0, 3), match='dog'>
#
# $ : match line ending
print(re.search(r"cat$", "dog runs to cat"))   
# <_sre.SRE_Match object; span=(12, 15), match='cat'>
#
# ? : may or may not occur
print(re.search(r"Mon(day)?", "Monday"))       
# <_sre.SRE_Match object; span=(0, 6), match='Monday'>
#
print(re.search(r"Mon(day)?", "Mon"))          
# <_sre.SRE_Match object; span=(0, 3), match='Mon'>
```

如果一个字符串有很多行, 我们想使用 `^` 形式来匹配行开头的字符, 如果用通常的形式是不成功的. 比如下面的 “I” 出现在第二行开头, 但是使用 `r"^I"` 却匹配不到第二行, 这时候, 我们要使用 另外一个参数, 让 `re.search()` 可以对每一行单独处理. 这个参数就是 `flags=re.M`, 或者这样写也行 `flags=re.MULTILINE`.

```python
string = """
dog runs to cat.
I run to dog.
"""
print(re.search(r"^I", string))                 
# None
print(re.search(r"^I", string, flags=re.M))     
# <_sre.SRE_Match object; span=(18, 19), match='I'>
```

[复制到重复匹配了](<https://morvanzhou.github.io/tutorials/python-basic/basic/13-10-regular-expression/>)

> r"(.+?)"
>
> . 表示任意字符 (有些情况下不包括换行), + 修饰前面一个字符, 限定数量是一个或者多个, 但默认会尽可能匹配更长的字符串 (贪婪匹配), + 后面再来个 ? 就表示用非贪婪匹配.
>
> 举个例子: 假设字符串 "*abc*abc*", 如果有 ?, 那么匹配到的就是 *abc*, 如果没有, 匹配到的就是整个字符串, 因为 . 也可以匹配到 *.
>
> *?	重复任意次，但尽可能少重复 
> +?	重复1次或更多次，但尽可能少重复 
> ??	重复0次或1次，但尽可能少重复 

