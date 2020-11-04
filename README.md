Cardboard Java
=====================
Copyright (c) 2014 Google Inc.  All rights reserved.

Decompiled CardboardSDK 0.5.1.

The *TreasureHunt* sample project, running fully from source. It compiles and runs on Android Studio 1.0.2. The Cardboard.jar package has been replaced by the decompiled sources. Decompiled using [Luyten](https://github.com/deathmarine/Luyten).

Inspiration from [raasun's cardboard](https://github.com/raasun/cardboard) (decompilation of an older version of CardboardSDK). According to *raasun*, Google should eventually release the official CardboardSDK source.

[https://developers.google.com/cardboard/android/get-started](https://developers.google.com/cardboard/android/get-started)

九轴融合算法是指通过融合IMU中的加速度计（三轴）、陀螺仪（三轴）、磁场计（三轴），来获取物体姿态的方法。它是开发VR头显中的一个至关重要的部分。VR头显必须要实时准确地获取用户头部的姿态，然后在屏幕上渲染出在对应的姿态所应该要看到的画面，才能让用户在VR世界里获得沉浸感。
因为人眼是非常精密的器官，如果渲染出来的画面稍微有一点点的延时或者偏差，人眼都能察觉出来，导致用户头晕想吐，再也不相信VR了。所以，VR头显对九轴融合算法的实时性和精度提出了非常高的要求。
而另一方面，公开的九轴融合方法又少之又少，常见的就是互补滤波算法和Madgwick算法，但是这两个方法的精度都不能达到VR头显的要求。而精度高的九轴融合算法都掌握在一些算法公司手里，需要向他们支付高昂的算法使用费，源码的价格更是天价。

Cardboard是谷歌在2014年发布的VR盒子，虽然它不是开源的，但是在GitHub上有很多Cardboard的反编译工程，比如https://github.com/rsanchezsaez/cardboard-java。Cardboard的VR体验，可以在一定程度上，证明它的九轴融合算法是满足VR要求的。所以，我对Cardboard反编译工程中的九轴融合部分的程序进行了研读，这部分的程序大概有5000行左右。我在通读完程序之后，结合文献[1],把程序背后的算法理论公式全部都反推出来，总结成了本文，与各位分享。
虽然早在2014年，Cardboard就已经在GitHub上被反编译了，但是这么多年过去了，有关它的代码原理分析的文章却是几乎没有。能结合源代码，把它背后的算法理论基础详细推导出来的，本文应该算是第一篇。如有推导错误的地方，还请各位不吝赐教。
本文目标读者：传感器融合算法工程师。
https://www.cnblogs.com/ilekoaiq/p/8710812.html
