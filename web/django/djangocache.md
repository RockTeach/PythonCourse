# Cache

[https://docs.djangoproject.com/zh-hans/2.0/topics/cache/](https://docs.djangoproject.com/zh-hans/2.0/topics/cache/)



### 缓存框架的核心目标

* 较少的代码
  * 缓存应该尽可能快
  * 因此围绕缓存后端的所有框架代码应该保持在绝对最小值，特别是对于获取操作
* 一致性
  * 缓存API应该是提供跨越不同缓存后端的一致接口
* 可扩展性
  * 基于开发人员的需求，缓存API应该可以在应用程序级别扩展



### 缓存

* django内置了缓存框架，并提供了几种常用的缓存
  * 基于Memcached缓存
  * 使用数据库进行缓存
  * 使用文件系统进行缓存
  * 使用本地内存进行缓存
  * 提供缓存扩展接口



#### 缓存配置

1. 创建缓存表
   ```py
   python manage.py createcachetable [table_name]
   ```
2. 缓存配置
   ```py
   CACHES = {
       'default': {
           'BACKEND': 'django.core.cache.backends.db.DatabaseCache',
           'LOCATION': 'my_cache_table',
           'TIMEOUT': '60',
           'OPTIONS': {
               'MAX_ENTRIES': '300',
           },
           'KEY_PREFIX': 'rock',
           'VERSION': '1',
       }
   }
   ```



#### 缓存使用

* 在视图中使用（使用最多的场景）
* @cache\_page\(\)
  * time 秒  60\*5 缓存五分钟
  * cache 缓存配置, 默认default，
  * key\_prefix 前置字符串



#### 缓存底层

* 获取cache 
  * ```py
    from django.core.cache import caches
    cache = caches['cache_name']
    ```
* 获取cache

  * ```py
    from django.core.cache import cache
    ```

* 缓存操作

  * cache.set

    * key

    * value

    * timeout

  * get

  * add

  * get\__or \_set_

  * get\_many

  * set\_many

  * delete

  * delete\_many

  * clear

  * incr 增加

    * incr\(key, value\) key对应的值上添加 value

  * decr 减少

    * decr\(key, value\) key对应的值上减少value

    * 如果value不写，默认变更为1



### 使用Redis做缓存

* 常见的有两个实现
  * django-redis
    * [http://django-redis-chs.readthedocs.io/zh\_CN/latest/\#django](http://django-redis-chs.readthedocs.io/zh_CN/latest/#django)
  * django-redis-cache
    * ·[https://pypi.python.org/pypi/django-redis-cache/](https://pypi.python.org/pypi/django-redis-cache/)
* 配置和内置的缓存配置基本一致
  * ```py
    CACHES = {
        "default": {
            "BACKEND": "django_redis.cache.RedisCache",
            "LOCATION": "redis://127.0.0.1:6379/1",
            "OPTIONS": {
                "CLIENT_CLASS": "django_redis.client.DefaultClient",
            }
        }
    }
    ```
* 用法和内置缓存使用一样





