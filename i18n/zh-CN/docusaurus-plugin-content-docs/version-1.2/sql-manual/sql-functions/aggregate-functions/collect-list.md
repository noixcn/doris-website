---
{
    "title": "COLLECT_LIST",
    "language": "zh-CN"
}
---

## COLLECT_LIST
## 描述
## 语法

`ARRAY<T> collect_list(expr[,max_size])`

返回一个包含 expr 中所有元素(不包括NULL)的数组，可选参数`max_size`，通过设置该参数能够将结果数组的大小限制为 `max_size` 个元素。
得到的结果数组中不包含NULL元素，数组中的元素顺序不固定。该函数具有别名`group_array`。


## 注意事项

```
仅支持向量化引擎中使用
```

## 举例

```
mysql> select k1,k2,k3 from collect_list_test order by k1;
+------+------------+-------+
| k1   | k2         | k3    |
+------+------------+-------+
|    1 | 2023-01-01 | hello |
|    2 | 2023-01-02 | NULL  |
|    2 | 2023-01-02 | hello |
|    3 | NULL       | world |
|    3 | 2023-01-02 | hello |
|    4 | 2023-01-02 | sql   |
|    4 | 2023-01-03 | sql   |
+------+------------+-------+

mysql> select collect_list(k1),collect_list(k1,2) from collect_list_test;
+-------------------------+--------------------------+
| collect_list(`k1`)      | collect_list(`k1`,3)     |
+-------------------------+--------------------------+
| [1,2,2,3,3,4,4]         | [1,2,2]                  |
+-------------------------+--------------------------+

mysql> select k1,collect_list(k2),collect_list(k3,1) from collect_list_test group by k1 order by k1;
+------+-------------------------+--------------------------+
| k1   | collect_list(`k2`)      | collect_list(`k3`,1)     |
+------+-------------------------+--------------------------+
|    1 | [2023-01-01]            | [hello]                  |
|    2 | [2023-01-02,2023-01-02] | [hello]                  |
|    3 | [2023-01-02]            | [world]                  |
|    4 | [2023-01-02,2023-01-03] | [sql]                    |
+------+-------------------------+--------------------------+

```

### keywords
COLLECT_LIST,GROUP_ARRAY,COLLECT_SET,ARRAY
