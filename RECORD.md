## 版本
Laravel 8

PHP 7.3
## 目录权限 可写权限
chmod -R 775 storage 和 bootstrap/cache
## Git忽略文件完善
.DS_Store

.idea

.settings/

*.swp

*.iml

*.ipr

*.iws

storage目录下有单独的忽略文件

_ide_helper.php

_ide_helper_models.php

.phpstorm.meta.php
## 其他配置
### env
数据库、缓存等其他需要的配置
### config/app.php
timezone PRC

locale zh-CN
## composer
如果本地PHP版本大于线上版本，可config中配置固定某个PHP版本
```
    "platform": {
        "php": "7.2.7"
    }
```
按需配置阿里云镜像
```
    "repositories": {
        "packagist": {
            "type": "composer",
            "url": "https://mirrors.aliyun.com/composer/"
        }
    }
```

composer require --dev caouecs/laravel-lang

cp -a vendor/caouecs/laravel-lang/src/zh-CN resources/lang

composer require --dev barryvdh/laravel-ide-helper
## JWT
composer require tymon/jwt-auth:dev-develop --prefer-source

php artisan vendor:publish --provider="Tymon\JWTAuth\Providers\LaravelServiceProvider"

php artisan jwt:secret
## 基础类等
### 权限
Services/Auth jwt token的相关操作

Middleware/JwtAuth中间件 调用权限验证
Http/Kernel $routeMiddleware增加中间件
### 异常处理
Exceptions/Handler 之前的错误会直接返回错误页面，增加判断返回指定的json格式错误数据

Exceptions/Exceptions.php 自定义的异常类，晚点可以改成直接继承Handler 在app.php配置成重写的类，主要是规范异常返回的参数和格式
### 控制器基础类
Http/Controller 成功、失败、参数验证公共方法、错误码常量
### 模型基础类
Models/BaseModel
### 表单验证基础类
Requests/BaseRequest 重写表单验证错误返回的方法，规范返回的错误参数，之前错误码为500，官方文档是422，500明显不合适所以重写方法，正好规范错误参数

## 本地化
lang里增加zh_cn\error.php 统一常用报错信息
## 跨域
暂未处理
## 删除
删除了默认的模型User、数据库迁移文件、Controllers下的Auth文件夹、view下的welcome，
并把web路由改成提示无权限
##优化
配置composer 路由配置项缓存
上线关闭debug
php artisan optimize:clear
opcache
## 其他规范
表单验证写在Reauests中

只有查看详情做了错误判断其他自带异常
