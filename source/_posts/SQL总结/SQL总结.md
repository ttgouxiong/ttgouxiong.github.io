---
title: SQL总结
date: 2020-12-31 21:15:15
tags: SQL总结
---

- ROUND 函数保留小数点几位 ROUND(string,3)   如果是负数就是取几个0→1000
- LEFT(name,1) 表示左面 第一个字母
- 字符长度：LEN()
判断有没有哪个个字母或者没有那个字母（或者空格）用LIKE或者NOT LIKE
- SELECT name, REPLACE(name, 'a','') FROM bbc
- CONCAT 拼接函数
- BETWEEN　AND　包括两边
- 用到GROUP BY 的话自然而然想到HAVING
- GROUP BY 后面的要包含SELECT的不然不行
- CASE input_expression
WHEN when_expression THEN
    result_expression [...n ] [
ELSE
    else_result_expression
END
- Exclusive OR (XOR). 例：Show the countries that are big by area (more than 3 million) or big by population (more than 250 million) but not both. 

- SELECT name FROM world WHERE population >= **ALL**(SELECT population FROM world WHERE population>0)
You need the condition population>0 in the sub-query as some countries have null for population.

- 