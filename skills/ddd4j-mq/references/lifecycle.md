# 生命周期

顺序：validate→producer init→consumer init→listener register→ready。

任一步失败：逆序关闭已初始化资源。正常停止：先停止接收、drain、关闭 consumer、producer、connection。close 必须幂等。

