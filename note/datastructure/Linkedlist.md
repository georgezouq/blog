# 链表

链表结构声明

[(1.8w字)负重前行，前端工程师如何系统练习数据结构和算法？【上】](https://juejin.im/post/5e2f88156fb9a02fdd38a184)

```js
function LinkedNode(val) {
  this.val = val
  this.next = null
}
```

## 反转链表

### 原地单链表的反转

    输入: 1->2->3->4->5->NULL
    输出: 5->4->3->2->1->NULL

#### 循环解决方案

```js
var reverseList = function(head) {
    var current = head
    var prev = null
    while(current) {
        var tmp = current.next
        current.next = prev
        prev = current
        current = tmp
    }
    return prev
}
```

#### 递归解决方案

```js
var reverseList = function(head) {
    let loop = function(prev, current) {
        if (!current) return prev

        let tmp = current.next
        current.next = prev
        return loop(current, tmp)
    }

    return loop(null, head)
};
```

### No.2 区间反转

反转操作上一题已经拆解过，这里不再赘述。值得注意的是反转后的工作，那么对于整个区间反转后的工作，其实就是一个移花接木的过程，首先将前节点的 next 指向区间终点，然后将区间起点的 next 指向后节点。因此这一题中有四个需要重视的节点: 前节点、后节点、区间起点和区间终点。接下来我们开始实际的编码操作。

#### 循环解法

1. keep the head
2. find start
4. set tail = start.next
5. reverse by use cur,prev
6. start.next = prev 
7. tail.next = current
8. return keepHead

```js
var reverseBetween = function(head, m, n) {
    let p = res = new ListNode()
    let prev, cur, start, tail = null
    let count = n - m

    p.next = head

    for (let i = 0; i < m - 1; i++) {
        p = p.next
    }

    start = p
    prev = tail = p.next
    cur = prev.next

    for (let i = 0; i < count; i++) {
        let tmp = cur.next
        cur.next = prev
        prev = cur
        cur = tmp
    }

    start.next = prev
    tail.next = cur

    return res.next
};
```

#### 递归解法

```js
var reverseBetween = function(head, m, n) {
    let loop = function(pre, cur) {
        if (!cur) return pre
        let tmp = cur.next
        cur.next = pre
        return loop(cur, tmp)
    }

    let before, after = null
    let p = res = new ListNode()
    res.next = head
    let start, end = null

    for (let i = 0; i < m-1; i++) {
        p = p.next
    }

    before = p
    start = p.next

    for (let i = m - 1; i < n; i++) {
        p = p.next
    }

    end = p
    after = end.next
    end.next = null

    before.next = loop(null, start)
    start.next = after

    return res.next
};
```

### 两个一组反转链表

### K个一组反转链表
