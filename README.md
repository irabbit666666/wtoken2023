# wtoken2023
Nike Wtoken算法分析
2023 nike App/snkrs wtoken 抽签/加车算法分析
通过分析发现，具体加密在这里libtiger_tally.so里
经过搜索我们知道这是ali安全的风控sdk，为了便于测试，我们自行注册了一个waf 3.0后台
并开启了所有风控最高级别（检测模拟器，root，重复ip，重复设备，包名，包签名等等）

按照传统方法，对于这种级别的混淆so，我们一般会选择unidbg模拟执行或者大神直接硬刚纯算法还原
但是这样有个坏处：
一旦sdk更新，大概率会失效，更新麻烦。

这里我们用了一个取巧的办法，直接制作一个apk出来调用sdk来生成算法，并通过远程调用。
这样，每次更新后，只要更换里面的sdk即可完成升级。

为了过风控，我们使用反射和hook来完成包名、签名、设备、各种系统信息的随机，这样每次获取到的wtoken都是全新的。
经过测试，能过所有的风控。
然后我们改为nike和snkrs的appkey，并使用加车请求测试，完美通过。

这样我们不仅不用考虑和分析难度极大的vmp混淆，也不必补各种烦人的环境，完成wtoken的完美调用。
wx:irabbit666
