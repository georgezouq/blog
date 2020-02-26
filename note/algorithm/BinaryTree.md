# 二叉树

### 层级遍历

比较简单，talk is cheap, see my code:

```js
var levelOrder = function(root) {
    if (!root) return []
    let res = []
    let queue = [root]
    let level = 0

    while (queue.length) {
        let size = queue.length
        res.push([])

        while(size --) {
            let front = queue.shift()
            res[level].push(front.val)

            front.left && queue.push(front.left)
            front.right && queue.push(front.right)
        }

        level++
    }

    return res
};
```
