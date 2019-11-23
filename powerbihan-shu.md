---
title: datediff
date: 2019-11-23
category: [pbi]
---

## 语法

```
DATEDIFF (
    开始日期,
    结束日期,
    间隔粒度
)
```

## 参数
- 参数1
- 参数2
- 参数3
    - SECOND：返回两个日期间隔的秒数
    - MINUTE：返回两个日期间隔的分钟
    - HOUR：返回两个日期间隔的小时
    - DAY：返回两个日期间隔的天数
    - WEEK：返回两个日期间隔的周数
    - MONTH：返回两个日期间隔的月数
    - QUARTER：返回两个日期间隔的季度
    - YEAR：返回两个日期间隔的年数

## 示例

- 以下计算结果都为1

```
DATEDIFF(MIN(日期表[日期]), MAX(日期表[日期]),,SECOND )
DATEDIFF(MIN(日期表[日期]), MAX(日期表[日期]), MINUTE )
DATEDIFF(MIN(日期表[日期]), MAX(日期表[日期]), HOUR)
DATEDIFF(MIN(日期表[日期]), MAX(日期表[日期]), DAY )
DATEDIFF(MIN(日期表[日期]), MAX(日期表[日期]), WEEK )
DATEDIFF(MIN(日期表[日期]), MAX(日期表[日期]), MONTH )
DATEDIFF(MIN(日期表[日期]), MAX(日期表[日期]), QUARTER )
DATEDIFF(MIN(日期表[日期]), MAX(日期表[日期]), YEAR )
```
