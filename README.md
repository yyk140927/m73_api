# m73_api
Feekr后台管理系统API Document
---

Author: shining@feekr.com
Version: 1.0.0
Description:Feekr后台管理系统接口
API地址：https://github.com/shiningwhite/m73_api
项目地址: http://m73.feekr.com

---

#### V1.0.0
+ 目录
    + [文档描述](#description)
    + [接口详情](#detail)
        + 创建玩法相关        
            + [选择城市](#city)
            + [搜索景点](#searchScenic)
            + [新增景点](#addScenic)
            + [提交新增玩法](#addPlay)
            + [提交修改玩法](#editPlay)
            + [玩法详情](#playDetail)
            + [获取更多评论](#moreComment)
            + [发布评论](#reply)
            + [删除评论](#deleteComment)
            + [点赞](#like)            
            + [获取预设标签](#addTag)
            + [编辑玩法获取用户基本信息](#getUsrInfo)
        +  用户相关
            + [用户登录](#login)
            + [用户主页](#people)
            + [我的玩法](#myPlay)
            + [我的消息](#myMsg)
            + [我的评论](#myComment)
            + [我的赞](#myLike)
            + [获取个人设置](#mySetting)
            + [修改个人设置](#submitMySetting)
            + [验证登录](#loginValidation)
        + 又拍云上传图片
            + [上传玩法图片](#uploadPic)
            + [上传base64图片](#uploadImg)
        + 第三方分享API
            + [分享API](#share)
    
<a name="description"></a>
##文档描述
###请求URL
接口地址以URI代替完整的URL,例如

    http://mfly.feekr.com/login/{userId}

将会简写成
    
    /login/{userId}
其中{}表示变量,由请求发起方传入相应的值。

###不同请求方法的含义
使用到的方法

    GET, POST, PUT, DELETE

+ GET    获取信息
+ POST   用于创建新内容操作
+ PUT    用于更新操作
+ DELETE 用于删除操作 

###参数
        * 表示必填
        
###出参：通用JSON格式
    {
        /**
          *对应http response状态码.
          *2xx--正常
          *401--没有登陆（跳转到登陆页）
          *403--没有权限
          *5xx--服务器内部异常
        */
       "statusCode": "200", 
        
       "result":{//存储请求成功的自定义数据
          ...
       },
       "errorCode":{//具体的业务错误码
           code:"",
           message:""
       } 
    }
    
    
<a name="detail"></a>
##接口详情 

<a name="searchScenic"></a>
###2.搜索景点
#### GET /search?scenicName={scenicName}&cityId={cityId}

######入参：
            * scenicName              String    景点名称
            * cityId                  String    城市ID
            
######出参：
    "result":
        {
            "scenic": [                //返回前七条数据
                {
                    “scenic“ : "00000000001",             
                    "scenicName" : "xxx"
                },
                {
                    “scenic“ : "00000000001",             
                    "scenicName" : "xxx"
                }
            ]
        }
        
          