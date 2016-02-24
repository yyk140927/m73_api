# m73_api
Feekr后台管理系统API Document
---

Author: shining@feekr.com

Version: 1.0.0

Description:Feekr后台管理系统接口

API地址: https://github.com/shiningwhite/m73_api

项目地址: http://m73.feekr.com

---

#### V1.0.0
+ 目录
    + [文档描述](#description)
    + [接口详情](#detail)
        +  用户相关
            + [用户登录](#login)
            + [修改密码](#resetPwd)
        + 审核管理        
            + [飞小编报名审核](#applyList)   
            + [飞小编申请搜索条件](#applySearchItem)         
            + [删除飞小编申请](#delApply)
            + [搜索飞小编申请列表](#searchApply)            
            + [编辑飞小编申请](#setApply)
            + [发送邮件通知](#sendEmail)
            + [飞小编报名审核详情页](#applyDetail)
            + [邮件通知模版](#emailTpl)
            + [编辑邮件模版](#setEmail)
        + 广告管理
            + [广告分类管理](#adCategory)
            + [编辑广告分类](#setAdCategory)
            + [新增广告分类](#addAdCategory)
            + [广告列表](#adList)
            + [编辑广告](#setAd)
            + [新增广告](#addAd)
            + [搜索广告](searchAd)
            
        + 权限管理
            + [用户列表](#userList)
            + [新增用户](#addUser)
            + [编辑用户](#setUser)
            + [搜索用户](#searchUser)
            + [删除用户](#delUser)
            + [角色列表](#roleList)
            + [新增角色](#addRole)
            + [编辑角色](#setRole)
            + [删除角色](#delRole)
            + [权限列表](#permissionList)
    
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

<a name="login"></a>
###用户登录
#### POST  /login

######入参：
            * username                  String    用户名
            * password                  String    密码
            * vcode                     String    验证码
            
######出参：
    "result":
        {
            "operation": 1  //登录成功返回，否则errorCode提示错误消息
        }
        
<a name="resetPwd"></a>
###修改密码
#### POST  /resetPwd

######入参：
            * oldPwd                  String    原密码
            * newPwd                  String    新密码
            * repeatPwd               String    确认密码
            
######出参：
    "result":
        {
            "operation": 1  //修改成功，否则errorCode提示错误消息

        }

<a name="applyList"></a>           
###飞小编报名审核
#### GET  /applyList?page={page}

######入参：
              page                    Int       页数
              periods                 String    期数
              applyStatus             String    申请状态
              mailStatus              String    邮件状态
              name                    String    姓名
              qq                      String    qq号
              city                    String    熟悉的城市
            
######出参：
    "result":
        {
            "applicants": [    //默认显示20条数据
               {
                  "applyId": "申请ID",
                  "name": "小白",
                  "qq": "123456",
                  "job": "学生",
                  "city": "熟悉的城市",
                  "experience": "旅行经历",
                  "special": "小众特色",
                  "applyTime": "报名时间",
                  "from": "来源",
                  "applyStatus": "状态",
                  "mailStatus": "邮件状态",  //  发送成功，发送失败，未发送
                  "failReason": "失败原因，该字段仅存在于邮件发送失败",
                  "remark": "备注"
              },
              { ... }
            ],             
            "pageTotal": "数量"
        }
 
 <a name="applySearchItem"></a>
###飞小编申请搜索条件
#### POST  /applySearchItem

######入参：
            
######出参：
    "result":
        {
            "periods": [1,2,3],  // 期数
            "applyStatus": [{
              "id": 1,   // 状态Id
              "status": "全部"   //  全部，通过，拒绝
             },
             { ... }
            ],
            "mailStatus": [{
              "id": 1,   // 状态Id
              "status": "全部"   //  发送成功，发送失败，未发送
             },
             { ... }
            ]
        }
        
 <a name="delApply"></a>
###删除飞小编申请
#### POST  /delApply

######入参：
            * applyId                 String    申请ID
            
######出参：
    "result":
        {
            "operation": 1  //修改成功，否则errorCode提示错误消息
        }
              

<a name="setApply"></a>
###编辑飞小编申请
#### POST  /setApply

######入参：
            * applyId                 String    申请ID
              applyStatus             Int       1表示通过， 0表示失败
              remark                  String    备注
                   
######出参：
    "result":
        {
            "operation": 1  //修改成功，否则errorCode提示错误消息
        }
 
<a name="sendEmail"></a>
###发送邮件通知
#### POST  /sendEmail

######入参：
            * applyId                 Array    申请ID
                   
######出参：
    "result":
        {
            notice: [{
               "applyId": 1111,
               "operation":  1 // 1表示修改成功, 0表示修改失败
               "failReason": "发送失败原因,仅当发送失败时给出" 
             },
             { ... }
            ]
        }                         
        
<a name="applyDetail"></a>
###飞小编报名审核详情页
#### GET  /applyDetail?apply={applyId}

######入参：
            * applyId                 String    申请ID
                   
######出参：
    "result":
        {
             "applicants": {
                  "applyId": "申请ID",
                  "name": "小白",
                  "qq": "123456",
                  "job": "学生",
                  "city": "熟悉的城市",
                  "experience": "旅行经历",
                  "special": "小众特色",
                  "applyTime": "报名时间",
                  "from": "来源",
                  "applyStatus": "状态",
                  "mailStatus": "邮件状态",  //  发送成功，发送失败，未发送
                  "failReason": "失败原因，该字段仅存在于邮件发送失败",
                  "remark": "备注"
             }
        } 
        
<a name="emailTpl"></a>
###邮件通知模版
#### GET  /emailTpl

######入参：
                   
######出参：
    "result":
        {
             "email": {
                "success": "通过的模版内容",
                "fail": "失败的模版内容"
             }
        }
        
 <a name="setEmail"></a>       
###编辑邮件模版
#### POST  /setEmail

######入参：
            * success                 String    通过的模版内容
            * fail                    String    失败的模版内容
                   
######出参：

    "result":
        {
            "operation": 1  //修改成功，否则errorCode提示错误消息
        }

<a name="adCategory"></a>
###广告分类管理
#### GET  /adCategory

######入参：
             page                      Int    分页     
######出参：
    "result":
        {
             "adCategory": [{
                  "cateId": "1111",
                  "createTime": "2015-09-11",
                  "name": "轮播图",
                  "code": "数据库字段",
                  "width": "600",
                  "height": "300",
                  "status": "开启"  // 停用
                },
                { ... }
             ],
              "pageTotal": "数量"
        }
                            
<a name="setAdCategory"></a>
###编辑广告分类
#### POST  /setAdCategory

######入参：
           * cateId                    String  广告分类ID
           * name                      String  名称
           * code                      String  数据库字段
           * width                     String  宽度
           * height                    String  高度
######出参：
    "result":
        {
            "operation": 1  //修改成功，否则errorCode提示错误消息
        }     
        
<a name="addAdCategory"></a>
###新增广告分类
#### POST  /addAdCategory

######入参：
            * name                      String  名称
            * code                      String  数据库字段
            * width                     String  宽度
            * height                    String  高度
######出参：
    "result":
        {
            "operation": 1  //修改成功，否则errorCode提示错误消息
        }                               