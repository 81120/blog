## 最小编辑距离问题

## 描述
给定两个列表`x`，`y`，只允许对`x`的头部进行三种操作，分别为：
  * 添加一个元素
  * 删除一个元素
  * 替换一个元素
那么，最少经过多少次的操作，能让`x`变成`y`，这个最少的次数被称为最小编辑距离

## 分析
  * 如果`x`的长度为0，`y`的长度为`l`，那么经过'l'次的添加操作可以将`x`变成`y`
  * 如果`y`的长度为0，`x`的长度为`l`，那么经过`l`次的删除操作可以将`x`变成`y`
  * 如果`x`和`y`的长度都不为0，那么来看`x`，`y`的第一个元素
  * 如果它们的第一个元素相等，那么`x`，`y`之间的最小编辑距离为`x`的尾和`y`的尾之间的最小编辑距离
  * 如果它们的第一个元素不相等，那么接下来的操作分三种情况讨论：
      * 对`x`的第一个元素进行替换操作，替换为`y`的第一个元素，那么`x`，`y`之间的最小编辑距离就变成了`x`的尾和`y`的尾之间的最小编辑距离加一，记为`distanceOfReplace`
      * 对`x`的第一个元素进行添加操作，将`y`的第一个元素添加到`x`的开头，那么`x`，`y`之间的最小编辑距离就变成了`x`和`y`的尾之间的最小编辑距离加一，记为`distanceOfAdd`
      * 对`x`的第一个元素进行删除操作，那么`x`，`y`之间的最小编辑距离就变成了`x`的尾和`y`之间的最小编辑距离加一，记为`distanceOfRemove`
  * 而`x`的头和`y`的头不想等的情况下，`x`，`y`之间的最小编辑距离就是`distanceOfRepace`，`distanceOfAdd`，`distanceOfRemove`之间的最小值

## 示例代码
```scheme
(define min-edit-distance
 (lambda (lst-x lst-y)
  (cond
   ((null? lst-x) (length lst-y))
   ((null? lst-y) (length lst-x))
   ((eq? (car lst-x) (car lst-y))
    (min-edit-distance (cdr lst-x) (cdr lst-y)))
   (else
    (+ 1
     (min
      (min-edit-distance (cdr lst-x) (cdr lst-y))
      (min-edit-distance lst-x (cdr lst-y))
      (min-edit-distance (cdr lst-x) lst-y)))))))
```
