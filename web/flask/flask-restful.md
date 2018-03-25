# Flask-RESTful

[https://flask-restful.readthedocs.io/en/latest/](https://flask-restful.readthedocs.io/en/latest/ "官网地址")

#### 基本使用

* 安装

```
# pip 安装
pip install flask-restful

# 源码安装
git clone https://github.com/flask-restful/flask-restful.git
python setup.py develop
```

* 创建Resource实现类

```
class HelloRESTful(Resource):
    def get(self):
        return {"data":"HelloREST"}
```

* 创建API对象，并注册路由

```
# ① 创建并初始化
api = API(app)
# ② 创建，之后初始化
api = API()
api.init_app(app)

# 注册路由 
api.add_resource(HelloRESTFul,"/")
```



