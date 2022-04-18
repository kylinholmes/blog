---
title: yolov5的坑，猛汉落泪😥
tag: 杂技
thumbnail: https://pic.kylinn.cloud/uploads/big/c8d28c219d9cf1d6b00dcf875c9b0ba8.jpg
---

## 1. 图片尺寸不一样
   不知道是不是我理解错了，还是怎么的，这个东西在用的时候好像就要设置好你训练的图片的尺寸
   那我怎么搞嘛，如果大小不一样，参数都不对。
- 一种解决办法是，预处理一下图片，我们先统计一下，大部分图片的尺寸所在区间，然后选择一个合适的大小，对于所有大于这个尺寸的图片全部去除，小于这个尺寸的图片，用(0,0,0)的像素补全
类似这样的

![](https://pic.kylinn.cloud/uploads/big/aad9013b5de3fbf3c96fe6582b3e2841.png)


## 2. 需要打标签
别用yolomark，上次给我整伤心了，用的C艹写的程序，打标签要用opencv库，配置半天还不能用😫
我后来在yolo文档里看到它推荐的几个打标记的工具，比如 ~~[labelbox](https://labelbox.com/)好像要收费的嗷，虽然现在还没有用过。或者~~ [makesense](https://www.makesense.ai/)，这个免费又开源，方便好用。

❌但是但是，其实最好的办法是去网上找现成打好标记的数据集，就算有很好的工具帮你打标记，还是不如你去网上找已经打好的来的快，yolo文档里说，建议一个类别要有1k以上的样本，1k个自己手打标记，怕是要我死在椅子上，所以最好是去找现成的

## 3.什么`value unpack`的错误
我打开cache一看，里面是空的，啥都没读到，后来发现可能是因为Windows里路径用的是`\`，所以导致不能正常读取文件

那我直接上<font color="#A2DBFB">**Linux** ~~Blue of Arch~~</font>了，结果上Linux还有坑😭，大哭痛哭😖，
 - 因为内存不够

我以为16G内存很够用了，swap分区也没开，结果现在直接爆内存了
`pycharm`里跑的，把我整个桌面都重启了一次，当然pycharm也没有了，后来在其他tty里面跑才发现是被系统杀掉了
所以下次建议swap分区开到64g，也不知道够用不

后来更新的：
一共好像到32G就差不多了，但是用硬盘速度太慢，好像导致他他读写出问题了，~~误以为不能读文件？~~
所以现在只有先买内存条再说了
当时用的机械硬盘做`swap`，速度慢是肯定的，不过因为固态都拿去装系统了，后面要分区还不好分，弄了一晚上也没弄好，就装上机械了