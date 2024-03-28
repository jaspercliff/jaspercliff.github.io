# redis

## 使用场景
### 热点数据的缓存

### 限时业务的运用
expire设置过期时间
- 验证码
``` java
              stringRedisTemplate.opsForValue().set(REGISTER_VERIFICATION_CODE_KEY,String.valueOf(verificationCode),1, TimeUnit.MINUTES);
```
- 限时优惠活动
### 计数器相关问题
incrby命令可以实现原子性的递增，所以可以运用于高并发的秒杀活动、分布式序列号的生成
- 一个手机号发多少条短信
- 一个接口一分钟限制多少请求
