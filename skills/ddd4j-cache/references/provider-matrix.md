# Provider 矩阵

- CaffeineCache、GuavaCache、HutoolCache：本地。
- LettuceCache、JedisCache、RedissonCache：Redis。
- JetCacheAdapter/Manager：统一/多级。
- MemcachedCache：Memcached。
- CacheKit：静态访问/注册入口。

使用前检查当前构造器、配置和测试；类存在不等于生产连接已验证。
