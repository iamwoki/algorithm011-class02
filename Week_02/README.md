学习笔记

hashMap 底层是一个 Node<K,V> 数组。在这个数组里存储了key和value的对应关系。同时也能看到里面有个子元素 next。当hash冲突时，这个next就会存储冲突的key。
hashMap 在存储数据的时候，会先取key本身的hash值，然后做一次位运算，然后去取到真事地址，所以hashmap能在o(1)的时间里找到数据，就是因为他能够直接找到下标。
Node 有个子类，当hash冲突达到8的时候 binCount >= TREEIFY_THRESHOLD - 1 就会变成红黑树。然后 当元素小于 6 时，才会变回链表 hc <= UNTREEIFY_THRESHOLD

HashMap的数组长度一定保持2的次幂，比如16的二进制表示为 10000，那么length-1就是15，二进制为01111，同理扩容后的数组长度为32，二进制表示为100000，length-1为31，二进制表示为011111。从下图可以我们也能看到这样会保证低位全为1，而扩容后只有一位差异，也就是多出了最左位的1，这样在通过 h&(length-1)的时候，只要h对应的最左边的那一个差异位为0，就能保证得到的新的数组索引和老数组索引一致(大大减少了之前已经散列良好的老数组的数据位置重新调换)，
个人理解。还有，数组长度保持2的次幂，length-1的低位都为1，会使得获得的数组索引index更加均匀  -- 摘抄自 https://blog.csdn.net/woshimaxiao1/article/details/83661464