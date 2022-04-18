---
title: Kylin有图床啦
tag: 杂技
thumbnail: https://pic.kylinn.cloud/uploads/big/8dca4bc3663a98c3071198e42f7ebc51.png
---


服务来自[Lychee](https://lycheeorg.github.io/) ![pic](https://lycheeorg.github.io/docs/img/logo.png) 

直接用的docker，这个有点坑的是，默认的几个 **“智能”** 文件夹不能设置为 **公开**，然后会报`Server Error or API Not Found`搞得我以为我弄坏了,前前后后弄了好久

甚至想写DockerFile从Lamp开始重新搞个镜像

最后发现能设置成公开的相册，只能是你自己建的，所以新建一个相册就好了

这里是图床的[地址](https://pic.kylinn.cloud)