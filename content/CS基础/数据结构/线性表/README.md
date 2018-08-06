# 线性表

线性表（List）：由零个或多个具有相同特性的数据元素组成的有限序列。

* **序列**：元素之间是有顺序的，第一个元素无前驱，最后一个元素无后继，其它每个元素都有且只有一个前驱和后继；
* **有限**：在计算机中处理的对象都是有限的，无限的数列只存在于数学概念中。

在较复杂的线性表中，一个数据元素可以由若干个数据项组成。

```
ADT 线性表（List）

Data
    线性表的数据对象集合为{a1, a2, a3, ……, an}，
    每个元素的类型均为DataType。
    其中，除第一个元素a1外，每个元素有且只有一个直接前驱元素，
    除了最后一个元素an外，每个元素有且只有一个直接后继元素。
    数据元素之间的关系是一对一的关系。

Operation
    InitList(*L):           初始化操作，建立一个空的线性表L；
    ListEmpty(L):           若线性表为空，返回true，否则返回false；
    ClearList(*L):          将线性表清空；
    GetElem(L, i, *e):      将线性表L中的第i个位置元素值返回给e；
    LocateElem(L, e):       在线性表L中查找与给定值e相等的元素，
                            如果查找成功，返回该元素在表中的序号表示成功，
                            否则返回0表示失败；
    ListInsert(*L, i, e):   在线性表L中的第i个位置插入新元素e；
    ListDelete(*L, i, *e):  删除线性表L中第i个位置元素，并将其值返回给e；
    ListLength(L):          返回线性表L的元素个数。

endADT
```

```
ADT List:
    List(self)              # 表构造操作，创建一个新表
    is_empty(self)          # 判断self是否为一个空表
    len(self)               # 获得self的长度
    prepend(self, elem)     # 将元素elem加入表中作为第一个元素
    append(self, elem)      # 将元素elem加入表中作为最后一个元素
    insert(self, elem, i)   # 将elem加入表中作为第i个元素，其他元素的顺序不变
    del_first(self)         # 删除表中的首元素
    del_last(self)          # 删除表中的微元素
    del(self, i)            # 删除表中的第i个元素
    search(self, elem)      # 查找元素elem在表中出现的位置，不出现时返回-1
    forall(self, op)        # 对表中的每个元素执行操作op
```