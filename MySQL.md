## 一、分组查询

## 二、多表连接查询

### 1、笛卡尔乘积

### 2、多表连接查询的分类
**（1）按年代分**：
- sql92标准
    - 在mysql中仅仅支持内连接
- sql99标准（推荐）
    - 支持内连接、外连接（全外连接除外）、交叉连接

**（2）按功能分**：
- 内连接
    - 等值连接
    - 非等值连接
    - 自连接
- 外链接
    - 左外连接
    - 右外连接
    - 全外连接（==mysql不支持==）
- 交叉连接

### 3、内连接
**（1）等值连接**

① 语法格式：

sql92标准：  
```
select 查询列表
表1, 表2
where 连接条件（用=连接）
[and]
[group by 分组]
[having 筛选条件]
[order by 排序]
```
sql99标准：

```
select 查询列表
表1 [inner] join 表2
on 连接条件（用=连接）
[and]
[where 筛选条件]
[group by 分组]
[having 筛选条件]
[order by 排序]
```

② 查询实例



**（2）非等值连接**

① 语法格式：

sql92标准：

```
select 查询列表
表1, 表2
where 连接条件（不用=连接）
[and]
[group by 分组]
[having 筛选条件]
[order by 排序]
```


sql99标准：

```
select 查询列表
表1 [inner] join 表2
on 连接条件（不用=连接）
[and]
[where 筛选条件]
[group by 分组]
[having 筛选条件]
[order by 排序]
```

② 查询实例


**（3）自连接**

① 语法格式：

sql92标准：

```
select 查询列表
表1, 表1
where 连接条件
[and]
[group by 分组]
[having 筛选条件]
[order by 排序]
```


sql99标准：

```
select 查询列表
表1 [inner] join 表1
where 连接条件
[and]
[group by 分组]
[having 筛选条件]
[order by 排序]
```

② 查询实例


### 4、外连接
**（1）应用场景**

用于查询一个表中有，而另外一个表中没有的记录

**（2）特点**
- 左外连接：left 左边的表为主表，left右边的表为从表
- 右外连接：right 右边的表为主表，right左边的表为从表

**（3）外连接查询过程**
- 主表的每一行，匹配从表的每一行
- 主表的每一行都会显示在查询结果中，而从表则会根据连接条件显示来显示在查询结果中
- 从表中的满足连接条件，则显示在查询结果中，不满足查询条件，则显示为null
- 所以外连接查询结果为：==内联连接查询结果+主表中有，而从表中没有的记录==
- 左外连接和右外连接两个表的顺序交换，可以实现同样的效果

**（4）左外连接**

①  语法格式：

```
select 查询列表
from 表1 left [outer] join 表2
on 连接条件
[and]
[where 筛选条件]
[group by 分组]
[order by 排序]
```

③ 查询实例：

- 查询没有男朋友的女神名称
```
SELECT b.name 
FROM beauty b LEFT JOIN boys bo 
ON b.boyfriend_id = bo.id 
WHERE bo.id IS NULL;
```
- 查询没有员工的部门id
```
SELECT d.DEPARTMENT_ID
FROM departments d LEFT JOIN employees e 
ON d.DEPARTMENT_ID = e.DEPARTMENT_ID 
WHERE e.EMPLOYEE_ID IS NULL;
```


**（2）右外连接**

①  语法格式：

```
select 查询列表
from 表1 right [outer] join 表2
on 连接条件
[and]
[where 筛选条件]
[group by 分组]
[order by 排序]
```

③ 查询实例：
- 查询没有男朋友的女神名称
```
SELECT b.name 
FROM boys bo RIGHT JOIN beauty b 
ON bo.id = b.boyfriend_id 
WHERE bo.id IS NULL;
```
- 查询没有员工的部门id
```
SELECT d.DEPARTMENT_ID 
FROM employees e RIGHT JOIN departments d
ON d.DEPARTMENT_ID = e.DEPARTMENT_ID
WHERE e.EMPLOYEE_ID IS NULL;
```


### 5、交叉连接
①  语法格式：

```
select 查询列表
from 表1 cross join 表2
on 连接条件
[and]
[where 筛选条件]
[group by 分组]
[order by 排序]
```

③ 说明：
- 交叉连接的查询结果就是==笛卡尔乘积==
- 查询结果的行数=表1的行数 * 表2的行数
- 即用表1的每一行去匹配表2的每一行