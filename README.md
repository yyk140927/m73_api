# m73_api
Feekr后台管理系统API Document
---

Author: shining@feekr.com

Version: 1.0.1

Description:Feekr后台管理系统接口

API地址: https://github.com/shiningwhite/m73_api

项目地址: http://m73.feekr.com

---

#### V1.0.1
+ 目录
    + [文档描述](#description)
    + [接口详情](#detail)
        +  用户相关
            + [用户登录](#login)
            + [修改密码](#resetPwd)
        + 审核管理        
            + [飞小编报名审核](#applyList)         
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
        + 权限管理
            + [用户列表](#userList)
            + [新增用户](#addUser)
            + [编辑用户](#setUser)
            + [删除用户](#delUser)
            + [角色列表](#roleList)
            + [新增角色](#addRole)
            + [编辑角色](#setRole)
            + [删除角色](#delRole)
            + [权限列表](#authList)
            + [验证权限](#verifyAuth)
        + 搜索相关
            + [飞小编搜索条件](#applySearchTerm)
            + [广告搜索条件](#adSearchTerm)
            + [用户搜索条件](#userSearchTerm)
        + 二维码相关
            + [生成二维码](#generateCode)
        + 导航相关
            + [导航列表](#navList)                     
    
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
#### POST  /auth/login

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
#### POST  /auth/resetPwd

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
#### GET  /apply/list?page={page}

######入参：
              page                    Int       页数
              periods                 String    期数
              applyStatus             Boolean   申请状态
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
                  "applyStatus": "状态",  // true:通过, false: 未通过
                  "mailStatus": "邮件状态",  //  1:发送成功，2:未发送，0:发送失败
                  "failReason": "失败原因，该字段仅存在于邮件发送失败",
                  "remark": "备注"
              },
              { ... }
            ],             
            "pageTotal": "数量"
        }
 
        
 <a name="delApply"></a>
###删除飞小编申请
#### POST  /apply/del

######入参：
            * applyId                 String    申请ID
            
######出参：
    "result":
        {
            "operation": 1  //修改成功，否则errorCode提示错误消息
        }
              

<a name="setApply"></a>
###编辑飞小编申请
#### POST  /apply/set

######入参：
            * applyId                 String    申请ID
              applyStatus             Boolean   状态 true表示通过， false表示失败
              remark                  String    备注
                   
######出参：
    "result":
        {
            "operation": 1  //修改成功，否则errorCode提示错误消息
        }
 
<a name="sendEmail"></a>
###发送邮件通知
#### POST  /email/send

######入参：
            * applyId                 Array    申请ID
                   
######出参：
    "result":
        {
            notice: [{
               "applyId": 1111,
               "status":   true // true表示发送成功, false表示发送失败
               "failReason": "发送失败原因,仅当发送失败时给出" 
             },
             { ... }
            ]
        }                         
        
<a name="applyDetail"></a>
###飞小编报名审核详情页
#### GET  /apply/detail?apply={applyId}

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
                  "applyStatus": "状态",  // true:通过, false: 未通过
                  "mailStatus": "邮件状态",  //  1:发送成功，2:未发送，0:发送失败
                  "failReason": "失败原因，该字段仅存在于邮件发送失败",
                  "remark": "备注"
             }
        } 
        
<a name="emailTpl"></a>
###邮件通知模版
#### GET  /email/tpl

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
#### POST  /email/set

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
#### GET  /adCategory/list

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
                  "status": true  // 停用 true: 开启，false: 停用
                },
                { ... }
             ],
              "pageTotal": "数量"
        }
                            
<a name="setAdCategory"></a>
###编辑广告分类
#### POST  /adCategory/set

######入参：
           * cateId                    String  广告分类ID
           * name                      String  名称
           * code                      String  数据库字段
           * width                     String  宽度
           * height                    String  高度
           * status                    Boolean 状态 // true 启用 false 停用
######出参：
    "result":
        {
            "adCategory": {
                "cateId": "1111",
                "createTime": "2015-09-11",
                "name": "轮播图",
                "code": "数据库字段",
                "width": "600",
                "height": "300",
                "status": true  // 停用 true: 开启，false: 停用
            }
        }     
        
<a name="addAdCategory"></a>
###新增广告分类
#### POST  /adCategory/set

######入参：
            * name                      String  名称
            * code                      String  数据库字段
            * width                     String  宽度
            * height                    String  高度
            * status                    Boolean 状态 // true 启用 false 停用
######出参：
    "result":
        {
            "adCategory": {
                "cateId": "1111",
                "createTime": "2015-09-11",
                "name": "轮播图",
                "code": "数据库字段",
                "width": "600",
                "height": "300",
                "status": true  // 停用 true: 开启，false: 停用
            }
        } 
        
<a name="adList"></a>
###广告列表
#### POST  /ad/list

######入参：
             adCategory                String  广告分类
             adTitle                   String  广告标题
             page                      Int  分页   

######出参：
    "result":
        {
            "ad": [
              {
                "id": "广告ID",
                "pic": "广告图片",
                "title": "标题",
                "desc": "描述",
                "url": "文章地址",
                "category": "分类",
                "rank": "顺序",
                "statistics": "点击数",
                "status": "状态",  // true表示开启，false表示关闭
                "startTime": "上线时间",
                "endTime": "下线时间",
                "size": "图片尺寸"
              }, 
              { ... }
            ],
           "pageTotal": "数量"
        }

<a name="setAd"></a>        
###编辑广告
#### POST  /ad/set

######入参：
             * id                      String  广告ID
             * category                String  广告分类
               desc                    String  描述
               rank                    String  排序
               status                  Boolean  状态 true or false
               url                     String  链接
               startTime               String  上线时间
               endTime                 String  下线时间
               pic                     String  图片
               title                   String  广告标题
                

######出参：
    "result":
        {
           "ad": {
                "id": "广告ID",
                "pic": "广告图片",
                "title": "标题",
                "desc": "描述",
                "url": "文章地址",
                "category": "分类",
                "rank": "顺序",
                "statistics": "点击数",
                "status": "状态",  // true表示开启，false表示关闭
                "startTime": "上线时间",
                "endTime": "下线时间",
                "size": "图片尺寸"
             }
        }          
        
<a name="addAd"></a>        
###新增广告
#### POST  /ad/set

######入参：
             * category                String  广告分类
               desc                    String  描述
               rank                    String  排序
               status                  Boolean  状态 true or false
               url                     String  链接
               startTime               String  上线时间
               endTime                 String  下线时间
               pic                     String  图片
               title                   String  广告标题
                

######出参：
    "result":
        {
          "ad": {
                "id": "广告ID",
                "pic": "广告图片",
                "title": "标题",
                "desc": "描述",
                "url": "文章地址",
                "category": "分类",
                "rank": "顺序",
                "statistics": "点击数",
                "status": "状态",  // true表示开启，false表示关闭
                "startTime": "上线时间",
                "endTime": "下线时间",
                "size": "图片尺寸"
             }
        } 
          
          
<a name="userList"></a>        
###用户列表
#### POST  /user/list

######入参：
               role                    String  角色
               name                    String  姓名
               page                    Int 分页 

######出参：
    "result":
        {
          "user": [
            {
              "id": "用户ID",
              "email": "邮箱",
              "nickname": "昵称",
              "name": "真实姓名",
              "role": "角色",
              "status": "状态",  // true or false
              "createTime": "创建时间"
            },
            { ... }            
          ],
          "pageTotal": "数量"
        }  
        
<a name="addUser"></a>        
###新增用户
#### POST  /user/set

######入参：
               * role                    String 角色
               * name                    String 姓名
               * email                   String 邮件
               * nickname                String 昵称
               * pwd                     String 密码
               * repeatPwd               String 重复密码

######出参：
    "result":
        {
          "user": {
              "id": "用户ID",
              "email": "邮箱",
              "nickname": "昵称",
              "name": "真实姓名",
              "role": "角色",
              "status": "状态",  // true or false
              "createTime": "创建时间"
          }
        } 
        
<a name="setUser"></a>        
###编辑用户
#### POST  /user/set

######入参：
               * id                      String 用户ID
               * role                    String 角色
               * name                    String 姓名
               * email                   String 邮件
               * nickname                String 昵称
               * pwd                     String 密码
               * repeatPwd               String 重复密码

######出参：
    "result":
        {
          "user": {
              "id": "用户ID",
              "email": "邮箱",
              "nickname": "昵称",
              "name": "真实姓名",
              "role": "角色",
              "status": "状态",  // true or false
              "create"Time": "创建时间"
          }
        }   
        
<a name="delUser"></a>        
###删除用户
#### POST  /user/del

######入参：
               * id                      String 用户ID

######出参：
    "result":
        {
          "operation": 1  //修改成功，否则errorCode提示错误消息
        }
        
<a name="roleList"></a>        
###角色列表
#### GET  /role/list

######入参：  
                page                     Int  分页
######出参：
    "result":
        {
          "rolelist": [
           {
              "id": "角色ID",
              "name": "，角色名称",
              "desc": "描述",
              "userlist": ["penny", "pp", " ... "],  //  用户列表
               "firstAuth": [
               {
                 "id": 1,
                 "name": "审核管理",
                 "field": "对应数据库字段",
                 "secondAuth": [
                 {
                   "id": "001",
                   "name": "飞小编审核",
                   "field": "对应数据库字段",
                   "thirdAuth": [
                    {
                      "id": "1",
                      "name": "景点审核",
                      "field": "对应数据库字段"
                    },
                    { ... }
                  ] 
                 },
                 { ... }
                ]
              },
              { ... }
             ]             
            },
            { ... }              
           ],
          "pageTotal": "数量"
        }
 
 <a name="delRole"></a>        
###删除角色
#### GET  /role/del

######入参：
                * id                       String 角色ID
######出参：
    "result":
        {
          "operation": 1  //修改成功，否则errorCode提示错误消息
        }                                               
             
<a name="addRole"></a>        
###新增角色
#### GET  /role/set

######入参：
            {
              "name": "，角色名称",
              "desc": "描述",
              "userlist": ["penny", "pp", " ... "],  //  用户列表
               "firstAuth": [
               {
                 "id": 1,
                 "name": "审核管理",
                 "field": "对应数据库字段",
                 "secondAuth": [
                 {
                   "id": "001",
                   "name": "飞小编审核",
                   "field": "对应数据库字段",
                   "thirdAuth": [
                    {
                      "id": "1",
                      "name": "景点审核",
                      "field": "对应数据库字段"
                    },
                    { ... }
                  ] 
                 },
                 { ... }
                ]
              },
              { ... }
             ]

           }                   
                  
######出参：
    "result":
        {
          "operation": 1  //修改成功，否则errorCode提示错误消息
        }              
         
<a name="setRole"></a>        
###编辑角色
#### GET  /role/set

######入参：
            {
              "id": "角色ID",
              "name": "，角色名称",
              "desc": "描述",
              "userlist": ["penny", "pp", " ... "],  //  用户列表
               "firstAuth": [
               {
                 "id": 1,
                 "name": "审核管理",
                 "field": "对应数据库字段",
                 "secondAuth": [
                 {
                   "id": "001",
                   "name": "飞小编审核",
                   "field": "对应数据库字段",
                   "thirdAuth": [
                    {
                      "id": "1",
                      "name": "景点审核",
                      "field": "对应数据库字段"
                    },
                    { ... }
                  ] 
                 },
                 { ... }
                ]
              },
              { ... }
             ]
            }                   
                  
######出参：
    "result":
        {
          "operation": 1  //修改成功，否则errorCode提示错误消息
        } 
        
<a name="authList"></a>        
###权限列表
#### GET  /auth/list

######入参：
                        
                  
######出参：
    "result":
        {
          "firstAuth": [
          {
            "id": 1,
            "name": "审核管理",
            "field": "对应数据库字段",
            "secondAuth": [
             {
               "id": "001",
               "name": "飞小编审核",
               "field": "对应数据库字段",
               "thirdAuth": [
              {
                 "id": "1",
                 "name": "景点审核",
                 "field": "对应数据库字段"
              },
              { ... }
             ] 
           },
          { ... }
         ]
       },
      { ... }
     ]
    }
 <a name="verifyAuth"></a>
###验证权限
#### GET  /auth/verifyAuth

######入参：       
            
######出参：
    "result":
        {
            "operation": 1  //验证成功，否则errorCode提示错误消息
        }                  
                
<a name="applySearchTerm"></a>
###飞小编搜索条件
#### GET  /searchTerm?type=fxbApply

######入参：
        * type                      String   条件类型          
            
######出参：
    "result":
        {
            "periods": [{
              "id": 1,
              "option": "第一期" 
             },
             { ... }
            ],  // 期数
            "applyStatus": [{
              "id": 1,   // 状态Id
              "option": "全部"   //  全部，通过，拒绝
             },
             { ... }
            ],
            "mailStatus": [{
              "id": 1,   // 状态Id
              "option": "全部"   //  发送成功，发送失败，未发送
             },
             { ... }
            ]
        }
        
<a name="adSearchTerm"></a>
###广告搜索条件
#### GET  /searchTerm?type=ad

######入参：
        * type                      String   条件类型          
            
######出参：
    "result":
        {
            "adCategory": [
              {
                "id": 1,
                "option": "第一期" 
              },
             { ... }
            ],  // 广告类别
        }
        
<a name="userSearchTerm"></a>
###用户搜索条件
#### GET  /searchTerm?type=user

######入参：
        * type                      String   条件类型          
            
######出参：
    "result":
        {
            "role": [
              {
                "id": 1,
                "option": "第一期" 
              },
              { ... }
            ],  // 角色
        }                                                               
        
<a name="generateCode"></a>
###生成二维码
#### GET  /qrcode

######入参：
        * url                      String   条件类型  
          size                     String   图片大小        
            
######出参：
    "result":
        {
            "qrcode": "code.jpg"
        }
        
 <a name="navList"></a>
###导航列表
#### GET  /auth/navList

######入参：        
            
######出参：
    "result":
        {
            "firstMenu": [
              {
                 "name": "审核管理",
                 "secondMenu": [
                  {
                     "name": "分类管理",
                     "url": "user"
                  },
                  { ... }
                ]
              },
              { ... }           
            ]
        }         
