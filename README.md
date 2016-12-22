# m73_api


Feekr后台管理系统API Document
---

Author: shining@feekr.com

Version: 2.0.2

Description:Feekr后台管理系统接口

API地址: https://github.com/shiningwhite/m73_api

项目地址: http://m73.feekr.com

---

#### V2.0.2
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
       + [消息通知](#sendEmail)
       + [飞小编报名审核详情页](#applyDetail)
       + [邮件通知模版](#emailTpl)
       + [编辑邮件模版](#setEmail)
    +  广告管理
       + [广告分类管理](#adCategory)
       + [编辑广告分类](#setAdCategory)
       + [新增广告分类](#addAdCategory)
       + [广告列表](#adList)
       + [编辑广告](#setAd)
       + [新增广告](#addAd)
    +  权限管理
       + [用户列表](#userList)
       + [新增用户](#addUser)
       + [编辑用户](#setUser)
       + [删除用户](#delUser)
       + [角色列表](#roleList)
       + [新增角色](#addRole)
       + [编辑角色](#setRole)
       + [删除角色](#delRole)
       + [权限列表](#authlist)
       + [新增&修改权限](#accessset)
       + [删除权限](#accessdel)
       + [验证权限](#verifyAuth)
    +  搜索相关
       + [飞小编搜索条件](#applySearchTerm)
       + [广告搜索条件](#adSearchTerm)
       + [用户搜索条件](#userSearchTerm)
       + [玩法兑换搜索条件](#exchangeTerm)
       + [玩法商品搜索条件](#awardTerm)
       + [每日文章推荐搜索条件](#dailyTerm)
       + [文章管理搜索条件](#articleTerm)
       + [注册用户搜索条件](#userTerm)
       + [玩法管理搜索条件](#playTerm)
       + [活动管理搜索条件](#activityTerm)
       + [攻略当季小众推荐条件](#guideSeasonTerm)
    +  二维码相关
       + [生成二维码](#generateCode)
    +  导航相关
       + [导航列表](#navList)
    +  系统面板
       + [快捷方式](#hotkey)
    +  玩法商城管理
       + [玩法奖励列表](#awardList)
       + [玩法奖励设置](#awardSet)
       + [玩法兑换列表](#exchangeList)  
       + [玩法兑换编辑](#exchangeSet)
    +  图片上传
       + [获取又拍云上传签名](#getSign)
       + [图片上传](#upload)
    +  文章管理
       + [官方栏目列表](#officialSectionList)
       + [修改官方栏目](#setOfficialSection)
       + [新增官方栏目](#addOfficialSection)
       + [删除官方栏目](#delOfficialSection)
       + [专栏作者列表](#specialAuthorList)
       + [修改专栏作者](#setSpecialAuthor)
       + [删除专栏作者](#delSpecialAuthor)
       + [文章列表](#articleList)
       + [文章详情](#articleDetail)
       + [新增文章](#addArticle)
       + [编辑文章](#setArticle)
       + [搜索专栏作者](#spColumn)
       + [微信文章列表](#wxArticleList)
       + [微信文章详情](#wxArticleDetail)
       + [更新微信文章](#updateWxArticle)
    +  推荐管理
       + [每日文章推荐列表](#dailyList)
       + [编辑每日文章推荐](#setDaily)
       + [新增每日文章推荐](#addDaily)
       + [新增每日文章推荐状态修改](#addDailyStatus)
    +  用户管理
       + [用户列表](#regUserList)
       + [添加用户](#regUserAdd)
       + [编辑用户](#regUserSet)
       + [反馈列表](#feedbackList)
       + [反馈备注](#feedbackSet)
    +  玩法管理
       + [玩法列表](#playList)
       + [玩法编辑](#playSet)
       + [玩法评论列表](#playCommentList)
       + [玩法评论编辑](#playCommentSet)
       + [活动列表](#activityList)
       + [活动详情](#activityInfo)
       + [新增活动](#activityAdd)
       + [编辑活动](#activitySet)

    +  攻略管理
       - [当季小众推荐列表](#guideSeasonList)
       - [当季小众推荐编辑/新增](#guideSeasonSet)
       - [当季小众推荐详情](#guideSeasonDetail)
       - [当季小众推荐删除](#delSeason)
       - [攻略首页分类列表](#guideCityList)
       - [攻略首页分类编辑/新增](#guideCitySet)
       - [攻略首页分类详情](#guideCityDetail)
       - [攻略首页分类删除](#delCity)
       - [攻略首页分类排序](#citySort)
       - [攻略目的地搜索](#guideCitySearch)
       - [攻略目的地热门搜索关键词](#guideCityHotSearch)
       - [攻略目的地热门搜索关键词编辑](#guideCityHotSearchEdit)
    +  微信管理
       - [微信回复列表](#wechatReplyList)
       - [微信回复设置](#wechatReplySet)
       - [微信回复历史](#wechatReplyHistory)

<a name="description"></a>

##文档描述
###请求URL
接口地址以URI代替完整的URL,例如

	http://mfly.feekr.com/login/{userId}

将会简写成
​	
	/login/{userId}
其中{}表示变量,由请求发起方传入相应的值。

###不同请求方法的含义
使用到的方法

	GET, POST, PUT, DELETE

+ GET	获取信息
+ POST   用于创建新内容操作
  + PUT用于更新操作
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
			* username				  String	用户名
			* password				  String	密码
			* vcode					  String	验证码

######出参：
	"result":
		{
			"operation": 1  //登录成功返回，否则errorCode提示错误消息
		}

<a name="resetPwd"></a>
###修改密码
#### POST  /auth/resetPwd

######入参：
			* oldPwd				  String	原密码
			* newPwd				  String	新密码
			* repeatPwd				  String	确认密码

######出参：
	"result":
		{
			"operation": 1  //修改成功，否则errorCode提示错误消息
	
		}

<a name="applyList"></a>		   
###飞小编报名审核
#### GET  /apply/lists?page={page}

######入参：
			  applyId				String	申请ID // 用于详情页
			  page					Int	   页数
			  periods				String	期数
			  applyStatus			Boolean   申请状态
			  mailStatus			String	邮件状态
			  name					String	姓名
			  qq					String	qq号
			  city					String	熟悉的城市
			  remark				String	备注

######出参：
	"result":
		{
			"applicants": [	//默认显示20条数据
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
				  "mailStatus": "邮件状态",  //  0:未发送 1:发送成功 2:发送失败
				  "smsStatus": "短信状态",  //  0:未发送 1:发送成功 2:发送失败
				  "emailFailReason": "失败原因，该字段仅存在于邮件发送失败",
				  "smsFailReason": "失败原因，该字段仅存在于短信发送失败",
				  "remark": "备注",
				  "phone": "联系电话",
				  "email": "邮箱"
			  },
			  { ... }
			],			 
			"pageTotal": "数量"
		}


 <a name="delApply"></a>
###删除飞小编申请
#### POST  /apply/del

######入参：
			* applyId				 String	申请ID

######出参：
	"result":
		{
			"operation": 1  //修改成功，否则errorCode提示错误消息
		}


<a name="setApply"></a>
###编辑飞小编申请
#### POST  /apply/set

######入参：
			* applyId				 String	申请ID
			  applyStatus			 Boolean   状态 true表示通过， false表示失败
			  remark				 String	备注

######出参：
	"result":
		{
			"operation": 1  //修改成功，否则errorCode提示错误消息
		}

<a name="sendEmail"></a>
###发送邮件通知
#### POST  /email/send

######入参：
			* applyId				Array	申请ID
			  type					String   消息类型 ‘sms,email’

######出参：
	"result":
		{
			"sms": [{
			   "applyId": 1111,
			   "status":   true // true表示发送成功, false表示发送失败
			   "failReason": "发送失败原因,仅当发送失败时给出" 
			 },
			 { ... }
			],
			
		   "email": [{
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
			* applyId				 String	申请ID

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
				  "mailStatus": "邮件状态",  //  0:未发送 1:发送成功 2:发送失败
				  "failReason": "失败原因，该字段仅存在于邮件发送失败",
				  "remark": "备注",
				  "phone": "联系电话",
				  "email": "邮箱"				  
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
			 	"successTitle": "通过标题",
				"success": "通过的模版内容",
				"failTitle": "失败标题",
				"fail": "失败的模版内容"
			 }
		}

 <a name="setEmail"></a>	   
###编辑邮件模版
#### POST  /email/set

######入参：
			* success			   String	通过的模版内容
			* fail				   String	失败的模版内容
			* successTitle		   String	通过的标题
			* failTitle			   String	失败的标题

######出参：

	"result":
		{
			"operation": 1  //修改成功，否则errorCode提示错误消息
		}

<a name="adCategory"></a>
###广告分类管理
#### GET  /adCategory/lists

######入参：
			 page					  Int	分页	 
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
		   * cateId					String  广告分类ID
		   * name					String  名称
		   * code					String  数据库字段
		   * width					String  宽度
		   * height					String  高度
		   * status					Boolean 状态 // true 启用 false 停用
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
			* name					  String  名称
			* code					  String  数据库字段
			* width					  String  宽度
			* height				  String  高度
			* status				  Boolean 状态 // true 启用 false 停用
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
#### POST  /ad/lists

######入参：
			 adCategory				String  广告分类
			 adTitle				String  广告标题
			 page					Int  分页   

######出参：
	"result":
		{
			"ad": [
			  {
				"id": "广告ID",
				"picDomain": "图片domain",
				"picUrl": "图片路径",
				"title": "标题",
				"desc": "描述",
				"url": "文章地址",
				"category": {
				   id: "当前广告分类ID",
				   name: "当前分类名称"
				}
				"rank": "顺序",
				"statistics": "点击数",
				"status": "状态",  // true表示开启，false表示关闭
				"startTime": "上线时间",
				"endTime": "下线时间"
			   
			  }, 
			  { ... }
			],
		   "pageTotal": "数量"
		}

<a name="setAd"></a>		
###编辑广告
#### POST  /ad/set

######入参：
			 * id					  String  广告ID
			 * categoryId			  String  广告分类
			   desc					  String  描述
			   rank					  String  排序
			   status				  Boolean  状态 true or false
			   url					  String  链接
			   startTime			  String  上线时间
			   endTime				  String  下线时间
			   pic					  String  图片
			   title				  String  广告标题


######出参：
	"result":
		{
		   "ad": {
				"id": "广告ID",
				"pic": "广告图片",
				"title": "标题",
				"desc": "描述",
				"url": "文章地址",
				"category": {
				   id: "当前广告分类ID",
				   name: "当前分类名称"
				}
				"rank": "顺序",
				"statistics": "点击数",
				"status": "状态",  // true表示开启，false表示关闭
				"startTime": "上线时间",
				"endTime": "下线时间"
			 }
		}		  

<a name="addAd"></a>		
###新增广告
#### POST  /ad/set

######入参：
			 * category				 String  广告分类
			   desc					 String  描述
			   rank					 String  排序
			   status				 Boolean  状态 true or false
			   url					 String  链接
			   startTime			 String  上线时间
			   endTime				 String  下线时间
			   pic					 String  图片
			   title				 String  广告标题


######出参：
	"result":
		{
		  "ad": {
				"id": "广告ID",
				"pic": "广告图片",
				"title": "标题",
				"desc": "描述",
				"url": "文章地址",
				"category": {
				   id: "当前广告分类ID",
				   name: "当前分类名称"
				}
				"rank": "顺序",
				"statistics": "点击数",
				"status": "状态",  // true表示开启，false表示关闭
				"startTime": "上线时间",
				"endTime": "下线时间"
			 }
		} 


<a name="userList"></a>		
###用户列表
#### POST  /user/lists

######入参：
			   role					String  角色
			   name					String  姓名
			   page					Int 分页 

######出参：
	"result":
		{
		  "user": [
			{
			  "id": "用户ID",
			  "email": "邮箱",
			  "nickname": "昵称",
			  "name": "真实姓名",
			  "role": {
			  	"id": 1,
			  	"option": "管理员"
			  },
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
			   * role					String 角色
			   * name					String 姓名
			   * email					String 邮件
			   * nickname				String 昵称
				 pwd					String 密码
				 repeatPwd				String 重复密码

######出参：
	"result":
		{
		  "user": {
			  "id": "用户ID",
			  "email": "邮箱",
			  "nickname": "昵称",
			  "name": "真实姓名",
			  "role": {
			  	"id": 1,
			  	"option": "管理员"
			  },
			  "status": "状态",  // true or false
			  "createTime": "创建时间"
		  }
		} 

<a name="setUser"></a>		
###编辑用户
#### POST  /user/set

######入参：
			   * id					   String 用户ID
			   * role				   String 角色
			   * name				   String 姓名
			   * email				   String 邮件
			   * nickname			   String 昵称
				 pwd				   String 密码
				 repeatPwd			   String 重复密码

######出参：
	"result":
		{
		  "user": {
			  "id": "用户ID",
			  "email": "邮箱",
			  "nickname": "昵称",
			  "name": "真实姓名",
			  "role": {
			  	"id": 1,
			  	"option": "管理员"
			  },
			  "status": "状态",  // true or false
			  "create"Time": "创建时间"
		  }
		}

<a name="delUser"></a>		
###删除用户
#### POST  /user/del

######入参：
			   * id					  String 用户ID

######出参：
	"result":
		{
		  "operation": 1  //修改成功，否则errorCode提示错误消息
		}

<a name="roleList"></a>		
###角色列表
#### GET  /role/lists

######入参：  
				page				   Int  分页
				id					   Int  角色ID
######出参：
	"result":
		{
		  "rolelist": [
		   {
			  "id": "角色ID",
			  "name": "，角色名称",
			  "desc": "描述",
			  "userlist": ["penny", "pp", " ... "],  //  用户列表
			  "authlist": [
			   {
				 "id": 1,
				 "name": "审核管理",
				 "field": "对应数据库字段",
				 "children": [
				 {
				   "id": "001",
				   "name": "飞小编审核",
				   "field": "对应数据库字段",
				   "children": [
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
				* id					   String 角色ID
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
			  "authlist": [
			   {
				 "id": 1,
				 "name": "审核管理",
				 "field": "对应数据库字段",
				 "children": [
				 {
				   "id": "001",
				   "name": "飞小编审核",
				   "field": "对应数据库字段",
				   "children": [
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
		   "operation": 1
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
			   "authlist": [
			   {
				 "id": 1,
				 "name": "审核管理",
				 "field": "对应数据库字段",
				 "children": [
				 {
				   "id": "001",
				   "name": "飞小编审核",
				   "field": "对应数据库字段",
				   "children": [
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
		  "operation": 1
		} 

<a name="authlist"></a>		
###权限列表
#### GET  /access/lists

######入参：


######出参：
	"result":
		{
		  "auth": [
		  {
			"id": 1,
			"name": "审核管理",
			"field": "对应数据库字段",
			"children": [
			 {
			   "id": "001",
			   "name": "飞小编审核",
			   "field": "对应数据库字段",
			   "children": [
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

<a name="accessset"></a>
#### 新增&修改权限
#### POST /access/set
######入参：
			*field						 String 对应数据库字段
			*level						 Int	级别 0|1|2
			*parentId					 Int	父ID
			 name						 String 备注
			 id							 Int	如果是修改，就必须有ID

######出参：
	"result":
		{
			"operation":1,					//操作成功返回1
			"id":22						   //返回插入的ID
		}


<a name="accessdel"></a>
#### 删除权限
#### POST /access/del
######入参：
			* id					 Int  权限ID
			* level					 Int  级别 0|1|2

######出参：
	"result":
		{
			"operation":1					//删除成功
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
		* type					  String   条件类型		  
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
			 { ... },
			 "smsStatus": [{
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
		* type					  String   条件类型		  
######出参：
	"result":
		{
			"adCategory": [
			  {
				"id": 1,
				"option": "第一期",
				"width":600,
				"height": 400 
			  },
			 { ... }
			],  // 广告类别
		}

<a name="userSearchTerm"></a>
###用户搜索条件
#### GET  /searchTerm?type=user

######入参：
		* type					  String   条件类型		  
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

<a name="exchangeTerm"></a>
###玩法兑换搜索条件
#### GET  /searchTerm?type=exchange

######入参：
		* type					  String   条件类型		  	
######出参：
	"result":
		{
			"sendStatus": [
			  {
				"id": 1,
				"option": "兑换状态" 
			  },
			  { ... }
			]
		}															   

<a name="awardTerm"></a>
###玩法商品搜索条件
#### GET  /searchTerm?type=award

######入参：
		* type					  String   条件类型		  
######出参：
	"result":
		{
			"awardStatus": [
			  {
				"id": 1,
				"option": "兑换状态" 
			  },
			  { ... }
			]
		}

<a name="dailyTerm"></a>
###每日文章推荐搜索条件
#### GET  /searchTerm?type=daily

######入参：
		* type					  String   条件类型		  	
######出参：
	"result":
		{
			"status": [
			  {
				"id": 1,
				"option": "全部" 
			  },
			  { ... }
			]
		}

<a name="articleTerm"></a>
###文章管理搜索条件
#### GET  /searchTerm?type=article

######入参：
		* type					  String   条件类型		  	
######出参：
	"result":
		{
			"status": [
			  {
				"id": 1,
				"option": "有效" 
			  },
			  { ... }
			],
			"producer": [
				{
				"id": 1,
				"option": "系统" 
			  },
			  { ... }
			],
			"tag": [
				{
				"id": 1,
				"option": "玩小众" 
			  },
			  { ... }
			],
			"column": [   //  官方栏目， 专栏
				{
				"id": 1,
				"option": "全部" 
			  },
			  { ... }
			]
		}

<a name="userTerm"></a>
###注册用户管理搜索条件
#### GET  /searchTerm?type=regUser

######入参：
		* type					  String   条件类型		  	
######出参：
	"result":
		{
			"status": [
			  {
				"id": 1,
				"option": "停用" 
			  },
			  { ... }
			],
			"role": [
				{
				"id": -1,
				"option": "全部" 
			  },{
				"id": 1,
				"option": "飞小编" 
			  }
			  { ... }
			]
		}

<a name="playTerm"></a>
###玩法管理搜索条件
#### GET  /searchTerm?type=play

######入参：
		* type					  String   条件类型		  	
######出参：
	"result":
		{
			"status": [
			  {
				"id": 1,
				"option": "停用" 
			  },
			  { ... }
			]
		}

<a name="activityTerm"></a>
###活动管理搜索条件
#### GET  /searchTerm?type=activity

######入参：
		* type					  String   条件类型		  	
######出参：
	"result":
		{
			"status": [
			  {
				"id": 1,
				"option": "停用" 
			  },
			  { ... }
			]
		}					  

<a name="guideSeasonTerm"></a>

### 攻略当季小众推荐条件

#### GET  /searchTerm?type=guide_recommend

###### 入参:
		* type                    String   条件类型

###### 出参:
```javascript
"result":
	{
		"season": [
		  {
			"id": 1,
			"option": "春季"  
		  },
		  { ... }
		],
         "month": [
		  {
			"id": 1,
			"option": "1月"  
		  },
		  { ... }
		]
	}
```

<a name="generateCode"></a>

###生成二维码
#### GET  /qrcode

######入参：
		* url					 String   条件类型  
		  size					 String   图片大小		

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

 <a name="hotkey"></a>
###快捷方式
#### GET  /auth/hotkey

######入参：		

######出参：
	"result":
		{
			"hotkey": [
			  {
				 "name": "审核管理",
				 "url": "http://",
				 "icon": "对应的icon"
			  },
			  { ... }		   
			]
		}

<a name="awardList"></a>
###玩法奖励列表
#### POST  /award/lists

######入参：

			 id						  String 用户ID
			 awardStatus			  String 上下架状态
			 name					  String 奖励名称
			 page					  Int  分页   

######出参：
	"result":
		{
			"award": [
			  {
				"id": "奖励ID",
				"picDomain": "图片domain",
				"picUrl": "图片路径",
				"name": "奖励名称",
				"playCount": "玩法数量",
				"highPlayCount": "精华玩法数量",
				"awardDesc": "商品描述",  
				"awardStatus": "状态"  // 1表示上架，0表示下架
			  }, 
			  { ... }
			],
		   "pageTotal": "数量"
		}

<a name="awardSet"></a>
###玩法奖励编辑
#### POST  /award/set

######入参：
		   * id						  Int	 编辑时传ID，新增则不传
			 picUrl					  String  商品封面地址
			 name					  String  奖励商品名称
			 highPlayCount			  Int	 精华玩法数量
			 playCount				  Int	 玩法数量
			 awardStatus			  String  商品上架、下架
			 awardDesc				  String  商品描述				   

######出参：
	"result":
		{
			id: 001  // 返回商品ID
		}  

<a name="exchangeList"></a>
###玩法兑换列表
#### POST  /exchange/lists

######入参：

			 sendStatus				  String 投递状态
			 username				  String 飞小编用户名
			 page					  Int  分页   

######出参：
	"result":
		{
			"exchange": [
			  {
				"id": "飞小编ID",
				"awardName": "奖励名称",
				"username": "用户名",
				"contact": "联系人",
				"phone": "联系电话",
				"address": "收货地址",
				"remark": "备注"
				"sendStatus": "状态"  // 1表示已寄出，0表示未寄出
			  }, 
			  { ... }
			],
		   "pageTotal": "数量"
		}  

<a name="exchangeSet"></a>
###玩法兑换编辑
#### POST  /exchange/set

######入参：
			*id						Int	兑换ID 
			 remark					String  备注
			 sendStatus				String 寄出／未寄出状态 

######出参：
	"result":
		{
			"exchange":
			  {
				"id": "飞小编ID",
				"awardName": "奖励名称",
				"username": "用户名",
				"contact": "联系人",
				"phone": "联系电话",
				"address": "收货地址",
				"remark": "备注"
				"sendStatus": "寄出状态"  // 1表示已寄出，0表示未寄出
			  }, 
		} 

<a name="getSign"></a>
###获取又拍云上传签名
#### POST  /getSign

######入参：
		* spaceName				 String 上传文件到又拍云空间名
######出参：
	"result":
		{
			"sign": {
			  "signature": "校验签名",
			  "policy": "存储/校验信息",
			  "domain": "返回图片的domain",
			  "url": "图片上传的空间域名"
			}
		}	

<a name="upload"></a>
###上传到又拍云
#### POST  http://{domain}/{spaceName}

######入参：
			 * signature		   String 校验签名
			 * policy			   String 存储/校验信息
			 * domain			   String 又拍云接口
			 * spaceName		   String 图片空间名

######出参：
	"result":
		{
			"code": 200
			"ext-param": ""
			"image-frames": 1
			"image-height": 2309
			"image-type": "JPEG"
			"image-width": 1732
			"message": "ok"
			"sign": "632afefdfbb2149fd600b348bc13d857"
			"time": 1449655376
			"url": "/2015/12/09/1002567449e6b3dcc09dc6766c3045f0406a21"
		  
		}	

<a name="officialSectionList"></a>
###官方栏目列表
#### POST  /officialColumn/lists

######入参：
			   sort				Int 0: 文章数, 1:订阅数, 2:浏览数, 3:创建时间, 4:文章更新时间, 降序
			   page				Int 分页

######出参：
	"result":
		{
		  "list": [
			{
			  "id": ID,
			  "coverDomain": "封面domain",
			  "coverUrl": "封面图片路径",
			  "avatarDomain": "头像domain",
			  "avatarUrl": "头像相对路径",
			  "name": "名称",
			  "desc": "介绍",
			  "articleCount": "文章数",
			  "feedCount": "订阅数",
			  "readCount": "浏览数",
			  "createTime": "创建时间",
			  "updateTime": "文章更新时间"
			},
			{ ... }			
		  ],
		  "pageTotal": "数量"
		}
<a name="setOfficialSection"></a>
###修改官方栏目
#### POST  /officialColumn/set

######入参：
			   *name		   String 名称 
			   *desc		   String 介绍
			   *coverUrl	   String 封面
			   *avatarUrl	   String 头像
			   *id			   String ID

######出参：
	"result":
		{
		  "item": {
			  "id": ID,
			  "coverDomain": "封面domain",
			  "coverUrl": "封面图片路径",
			  "avatarDomain": "头像domain",
			  "avatarUrl": "头像相对路径",
			  "name": "名称",
			  "desc": "介绍",
			  "articleCount": "文章数",
			  "feedCount": "订阅数",
			  "readCount": "浏览数",
			  "createTime": "创建时间",
			  "updateTime": "文章更新时间"
		   }
		}

<a name="addOfficialSection"></a>
###新增官方栏目
#### POST  /officialColumn/set

######入参：
			   *name		   String 名称 
			   *desc		   String 介绍
			   *coverUrl	   String 封面
			   *avatarUrl	   String 头像

######出参：
	"result":
		{
		  "item": {
			  "id": ID,
			  "coverDomain": "封面domain",
			  "coverUrl": "封面图片路径",
			  "avatarDomain": "头像domain",
			  "avatarUrl": "头像相对路径",
			  "name": "名称",
			  "desc": "介绍",
			  "articleCount": "文章数",
			  "feedCount": "订阅数",
			  "readCount": "浏览数",
			  "createTime": "创建时间",
			  "updateTime": "文章更新时间"
		   }
		}

<a name="delOfficialSection"></a>
###删除官方栏目
#### POST  /officialColumn/del

######入参：
			   *id			  String 栏目ID

######出参：
	"result":
		{
		   "operation": 1
		}

<a name="specialAuthorList"></a>		
###专栏作者列表
#### POST  /specialColumn/lists

######入参：
			   nickname			String 用户名
			   sort				Int 0:文章数, 1:订阅数, 2:浏览数, 3:创建时间, 4:文章更新时间, 降序
			   page				Int 分页

######出参：
	"result":
		{
		  "list": [
			{
			  "id": ID,
			  "coverDomain": "封面domain",
			  "coverUrl": "封面图片路径",
			  "nickname": "用户名"
			  "name": "姓名",
			  "desc": "介绍",
			  "articleCount": "文章数",
			  "feedCount": "订阅数",
			  "readCount": "浏览数",
			  "createTime": "创建时间",
			  "updateTime": "文章更新时间",
			  "cellphone": "手机号码",
			  "qq": "qq号码",
			  "weixin": "微信",
			  "remark": "备注"
			},
			{ ... }			
		  ],
		  "pageTotal": "数量"
		}

<a name="setSpecialAuthor"></a>
###修改专栏作者
#### POST  /specialColumn/set

######入参：

			   *id			  Strinf ID
			   *desc		  String 介绍
			   *coverUrl	  String 封面
				name		  String 名称 
				cellphone	  Int 手机号码
				qq			  Int qq号码
				weixin		  String 微信
				remark		  String 备注

######出参：
	"result":
		{
		  "item": {
			  "id": ID,
			  "userId": "用户ID",
			  "coverDomain": "封面domain",
			  "coverUrl": "封面图片路径",
			  "nickname": "用户名"
			  "name": "姓名",
			  "desc": "介绍",
			  "articleCount": "文章数",
			  "feedCount": "订阅数",
			  "readCount": "浏览数",
			  "createTime": "创建时间",
			  "updateTime": "文章更新时间",
			  "cellphone": "手机号码",
			  "qq": "qq号码",
			  "weixin": "微信",
			  "remark": "备注"
			}
		}
<a name="delSpecialAuthor"></a>
###删除专栏作者
#### POST  /specialColumn/del

######入参：

			   *id			 String ID

######出参：
	"result":
		{
		  "operation": 1
		}

<a name="articleList"></a>
###文章列表
#### GET  /article/lists

######入参：
			   status			  String 状态：有效，删除...
			   sort				  Int 2:浏览数, 5:喜欢书, 6: 评论数 降序
			   page				  Int 分页
			   producer			  String 产生
			   tag				  String 标签
			   title			  String 标题
			   officialColumn	  String 官方栏目
			   spColumn			  String 专栏作者

######出参：
	"result":
		{
		  "list": [
			{
			  "id": ID,
			  "time": "时间",
			  "title": "标题"
			  "officialColumn": "官方栏目",
			  "spColumn": "专栏作者",
			  "tag": ["爱文艺", "好酒店"],
			  "status": 0, //  0.待审核 1有效 2拒绝 3删除
			  "producer": 1 //  1:系统 2:用户
			  "readCount": "阅读数", 
			  "likeCount": "喜欢数",
			  "commentCount": "评论数"
			},
			{ ... }			
		  ],
		  "pageTotal": "数量"
		}

<a name="articleDetail"></a>
###文章详情
#### GET  /article/detail

######入参：
			*id		   String ID
######出参:
	"result":
		{
		  "item": {
			  "id": ID,
			  "wxId": "微信文章ID"
			  "time": "时间",
			  "title": "标题"
			  "from": "来源",
			  "url": "来源地址",
			  "editor": "田田",
			  "status": [{
				"id": 1,
				"option": "有效",
				"isChecked": 1  //  选中
			  },
			  {
				"id": 2,
				"option": "待审核"
			  },{
				"id": 3,
				"option": "拒绝"
			  }, {
				"id": 0,
				"option": "删除"
			  }],
			  "officialColumn": [
				{
				  "id": 1,
				  "option": "大咖玩小众",
				  "isChecked": 1  //  选中
				},{ ... }
			  ],
			  "specialColumn": {
				"id": 1,
				"option": "专栏作者"
			  },
			  "tag": [
				{
				  "id": 1,
				  "option": "玩小众",
				  "isChecked": 1  //  选中
				},{ ... }
			  ],
			  "coverDomain": "封面domain",
			  "coverUrl": "封面图片路径",
			  "desc": "简介",
			  "content": "文章内容"
			}
		}

<a name="addArticle"></a>
###新增文章
#### POST  /article/set

######入参：
			 *time				 String
			 *title				 String
			 *coverUrl			 String
			 *content			 String	
			  from				 String
			  url				 String
			  editor			 String
			  status			 Array
			  officialColumn	 Array
			  specialColumn		 Array
			  tag				 Array
			  desc				 String
			  wxId				 String
######出参:	
	 "result":
		{
		  "operation": 1
		}

<a name="setArticle"></a>
###编辑文章
#### POST  /article/set

######入参：
			 *id				   String
			 *time				   String
			 *title				   String
			 *coverUrl			   String
			 *content			   String		
			  from				   String
			  url				   String
			  editor			   String
			  status			   Array
			  officialColumn	   Object
			  specialColumn		   Array
			  tag				   Array
			  desc				   String
			  wxId				   String
######出参:
	 "result":
		{
		  "operation": 1
		}

<a name="spColumn"></a>
###
#### GET  /specialColumn/author?name={name}

######入参：
			 *name	   //  用户名

######出参:
	 "result":
		{
		  "list": [
			{
			  "id": 1,
			  "text": "夏小暖"
			},
			 {
			  "id": 2,
			  "text": "夏雨天"
			}
		  ]
		}

<a name="wxArticleList"></a>
###微信文章列表
#### GET  /wxarticle/lists

######入参：
		title			  String  标题
		sort			 Int //排序降序  7:引用次数 

######出参:
	 "result":
		{
		  "list": [
			{
			  "id": ID,
			  "createTime": "创建时间",
			  "title": "标题"
			  "useCount": "引用次数",
			  "updateTime": "更新时间",
			  "url": "微信文章地址"
			},
			{ ... }	
		  ],
		  "pageTotal": "数量"
		}

<a name="wxArticleDetail"></a>
###微信文章详情
#### GET  /wxarticle/detail

######入参：
			wxId		  String ID // 微信文章ID

######出参:
	"result":
		{
		  "item": {
			  "wxId": ID,
			  "title": "标题"
			  "url": "来源地址",
			  "coverDomain": "封面domain",
			  "coverUrl": "封面图片路径",
			  "desc": "简介",
			  "content": "文章内容"
			}
		}

<a name="updateWxArticle"></a>
###更新微信文章
#### GET  /wxarticle/update

######入参：
			*id		  String ID  

######出参:
	 "result":
		{
		  "operation": 1
		}

<a name="dailyList"></a>
###每日文章推荐列表
#### POST  /daily/lists

######入参：
			   status			String 状态
			   title			String 标题
			   sort				Int 0:文章数, 1:订阅数, 2:浏览数, 3:创建时间, 4:文章更新时间, 降序
			   page				Int 分页

######出参：
	"result":
		{
		  "list": [
			{
			  "id": ID,
			  "articleId": "文章ID",
			  "time": "推荐日期"
			  "rank": "排序",
			  "title": "文章标题"
			  "officleColumn": "官方栏目",
			  "specialColumn": "专栏作者",
			  "tag": ["爱文艺", "好酒店", "..."],
			  "readCount": "浏览数",
			  "status": 1,   //  1: 发布， 0: 下线
			  "updateTime": "更新时间"
			},
			{ ... }			
		  ],
		  "pageTotal": "数量"
		}

<a name="setDaily"></a>
###编辑每日文章推荐
#### POST  /daily/set

######入参：
			   *id					  String  ID
			   *time				  String  推荐日期
			   *articleId			  String  推荐文章ID
			   *rank				  Int  排序

######出参：
	"result":
		{
		  "item": {
			  "id": ID,
			  "articleId": "文章ID",
			  "time": "推荐日期"
			  "rank": "排序",
			  "title": "文章标题"
			  "officleColumn": "官方栏目",
			  "specialColumn": "专栏作者",
			  "tag": ["爱文艺", "好酒店", "..."],
			  "readCount": "浏览数",
			  "status": 1,   //  1: 发布， 0: 下线
			  "updateTime": "更新时间"
			}
		}

<a name="addDaily"></a>
###新增每日文章推荐
#### POST  /daily/set

######入参：
			   *time				   String  推荐日期
			   *articleId			   String  推荐文章ID
			   *rank				   Int  排序

######出参：
	"result":
		{
		  "item": {
			  "id": ID,
			  "articleId": "文章ID",
			  "time": "推荐日期"
			  "rank": "排序",
			  "title": "文章标题"
			  "officleColumn": "官方栏目",
			  "specialColumn": "专栏作者",
			  "tag": ["爱文艺", "好酒店", "..."],
			  "readCount": "浏览数",
			  "status": 1,   //  1: 发布， 0: 下线
			  "updateTime": "更新时间"
			}
		}

<a name="addDailyStatus"></a>
###新增每日文章推荐状态修改
#### POST  /daily/status

######入参：

			   *articleId			   String  推荐文章ID

​		 
######出参：
	"result":
		{
		   "operation": 1
		}

<a name="regUserList"></a>
###用户列表
#### GET  /regUser/lists

######入参：
			   sort				  Int 9:注册时间 10:上次登录 11:登录数 13:玩法 14:主题  15:文章 16:关注  17:粉丝 降序
			   page				  Int 分页
			   status			  Int 状态
			   role				  Int 身份
			   nickname			  String 昵称

######出参：
	"result":
		{
		  "list": [
			{
			  "id": ID,
			  "regTime": "注册时间",
			  "lastLogin": "上次登录",
			  "nickname": "昵称",
			  "avatarDomain": "头像domain",
			  "avatarUrl": "头像相对路径",
			  "status": 0, //  0:停用， 1:启用
			  "source": "来源", 
			  "account": "帐号",
			  "loginCount": "登录数",
			  "role": [
				{
				  "id": 1,
				  "option": "飞小编",
				  "isChecked": 1  //  选中
				},{ ... }
			  ],
			  "playCount": "玩法"
			  "themeCount": "主题",
			  "articleCount": "文章",
			  "subscribCount": "关注",
			  "fansCount": "粉丝"
			},
			{ ... }			
		  ],
		  "pageTotal": "数量"
		}

<a name="regUserAdd"></a>
###新增用户
#### GET  /regUser/set

######入参：
			  *account		Int	 手机账号
			  *password	  	String  密码
			  *confirmPwd	String  确认密码
			  *nickname		String  昵称	
			  role			Array	 角色ID
			  avatarUrl		String  头像相对路径


######出参：
	"result":
		{
		  "operation": 1
		}

<a name="regUserSet"></a>
###编辑用户
#### GET  /regUser/set

######入参：
			 *id		  	Int 用户ID
			 *nickname		String  昵称	
			  role			Array	 角色ID
			  avatarUrl		String  头像相对路径
			  status   		Int 0:停用 1：启用

######出参：
	"result":
		{
		  "operation": 1
		}


<a name="feedbackList"></a>
###反馈列表
#### GET  /feedback/lists

######入参：
			 page			Int 分页

######出参：
	"result":
		{
		  "list": [
			{
			  "id": "反馈ID",
			  "nickname": "用户昵称",
			  "content": "内容"
			  "contact": "联系方式",
			  "platform": "平台",
			  "os": "操作系统"
			  "time": "时间", 
			  "remark": "备注"
			},
			{ ... }			
		  ],
		  "pageTotal": "数量"
		}

<a name="feedbackSet"></a>
###反馈备注
#### GET  /feedback/set

######入参：
 			   *id				Int ID
			   	remark			String 备注

######出参：
	"result":
		{
		  "operation": 1
		}

<a name="playList"></a>
###玩法列表
#### GET  /play/lists

######入参：
			   sort				  Int 2:浏览数 3:赞数 4:评论数 降序
			   page				  Int 分页
			   status			  Int 状态 0:待审核，1:其他
			   title			  String 玩法标题
			   activityTitle	  String 活动标题

######出参：
	"result":
		{
		  "list": [
			{
			  "id": ID,
			  "time": "时间",
			  "city": "城市",
			  "scenic": "景点",
			  "user": "用户",
			  "userId": "用户ID",
			  "title": "玩法标题",
			  "content": "玩法内容",
			  "status": 0, //  0:待审核， 1:拒绝  2:通过
			  "isRecommend": 0, // 0:否  1:是 
			  "readCount": "浏览数",
			  "commentCount": "评论数",
			  "likeCount": "赞数"			
			 },
			{ ... }			
		  ],
		  "pageTotal": "数量"
		}

<a name="playSet"></a>
###玩法编辑
#### GET  /play/set

######入参：
			 *id			Int	 玩法ID
			  status		Int  通过／拒绝
			  isRecommend	Int  是否推荐
			  isReview		Int  是否重审

######出参：
	"result":
		{
		  "operation": 1
		}

<a name="playCommentList"></a>
###玩法评论列表
#### GET  /playComment/lists

######入参：
			   page				Int 分页
		   	   status			int 0:待审核，1:其他  

######出参：
	"result":
		{
		  "list": [
			{
			  "id": ID,
			  "time": "时间",
			  "user": "用户",
			  "userId": "用户ID",
			  "title": "玩法标题",
			  "content": "玩法内容",
			  "playId":"玩法ID",		 
			 },
			{ ... }			
		  ],
		  "pageTotal": "数量"
		}

<a name="playCommentSet"></a>
###玩法评论编辑
#### GET  /playComment/set

######入参：
			 *id			Int	 玩法ID
			  status		Int 通过／拒绝

######出参：
	"result":
		{
		  "operation": 1
		}		

<a name="activityList"></a>
###活动列表
#### GET  /activity/lists

######入参：
			   page				Int 分页
			   status			Int -1:全部 0:停用 1:启用
			   sort				Int 2:浏览数 18:参与数  19:开始时间 20:截止时间

######出参：
	"result":
		{
		  "list": [
			{
			  "id": ID,
			  "coverDomain": "封面domain",
			  "coverUrl": "封面地址"
			  "title": "标题",
			  "user": "发起人",
			  "playCount": "参与数",
			  "readCount": "浏览数",
			  "status": 0:停用 1:启用,
			  "startTime":"开始日期",		
			  "endTime":"截止日期",
			  "activityLink": "活动链接"	
			 },
			{ ... }			
		  ],
		  "pageTotal": "数量"
		}

<a name="activityInfo"></a>		
###活动详情
#### GET  /activity/detail?id={id}

######入参：
			   id				Int ID // id为空为新增

######出参：
	"result":
		{
		  "item": {
		  	  "id": ID,
			  "coverDomain": "封面domain",
			  "coverUrl": "封面地址"
			  "title": "标题",
			  "userId": "发起人ID",
			  "startTime":"开始日期",		
			  "endTime":"截止日期",	
			  "lotteryUrl": "中奖地址",
			  "descUrl": "活动详情地址",
			  "desc": "简介",
			  "rule": "规则",
			  "lotteryCount":"中奖人数",
			  "shareUrl": "活动分享地址",
			  "shareTitle": "活动分享标题",
			  spaceName: "又拍云上传空间"，
			  type: [
			  	{
			  		id: 1,
			  		option: '活动',
			  		isChecked: 1
			  	},
			  	{ ... }
			  ]
		  }
		}		

<a name="activityAdd"></a>
###新增活动
#### GET  /activity/set

######入参：
			 *coverUrl		String 封面地址
			 *title			String 标题
			 *desc			String 简介
			 *startTime		String 开始日期	
			 *endTime		String 截止日期
			 *rule			String 规则
			 *type			String 活动类型
			 *shareUrl		String 活动分享地址
			 *shareTitle	String 活动分享标题
			  userId		String 发起人ID
			  lotteryUrl	String 中奖地址
			  descUrl		String 活动详情地址
			  lotteryCount	String 中奖人数

######出参：


<a name="activitySet"></a>
###编辑活动
#### GET  /activity/set

######入参：
			 *id			Int	 玩法ID
			  status		Int  停用／启用
			 *coverUrl		String 封面地址
			 *title			String 标题
			 *desc			String 简介
			 *startTime		String 开始日期	
			 *endTime		String 截止日期
			 *rule			String 规则
			 *type			String 活动类型
			 *shareUrl		String 活动分享地址
			 *shareTitle	String 活动分享标题
			  userId		String 发起人ID
			  lotteryUrl	String 中奖地址
			  descUrl		String 活动详情地址
			  lotteryCount	String 中奖人数

######出参：
	"result":
		{
		  "operation": 1
		}				

<a name="guideSeasonList"></a>

### 当季小众推荐列表

#### GET  /guide_season/lists

######入参：
			   page				Int 分页
			   month			Int 月份
			   season			Int 季节
			   site             String 目的地

######出参：

```javascript
"result":
	{
	  "list": [
		{
		  "id": ID,
		  "coverDomain": "封面domain",
		  "coverUrl": "封面地址"
		  "desc": "描述",
		  "season": "季节",
		  "month": "月份",
		  "addTime": "添加时间",
          "site": "目的地"
		 },
		{ ... }			
	  ],
	  "pageTotal": "数量"
	}
```

<a name="guideSeasonSet"></a>

### 当季小众推荐编辑/新增

#### POST /guide_season/set

######入参：
			 *id			Int	 ID  // 新增不是必填
			 *site          String 目的地
			 *season		Array 季节
			 *month         Array 月份
			 *desc          String 描述
			 *url           String 推荐地址URL
			  cover	        String 目的地封面  // size>=600X400

######出参：

```javascript
"result":
	{
	 	"operation": 1
	}
```
<a name="guideSeasonDetail"></a>

### 当季小众推荐详情

#### GET /guide_season/detail

######入参：
			 *id			Int	 ID

######出参：

```javascript
"result":
	{
	 	"info": {
          	"site": "",
            "desc": "",
            "coverUrl":"",
            "coverDomain": "",
            "season": [{
              "id": 1,
              "text": "春季",
              "checked": true
            }, {
              "id": 2,
              "text": "夏季",
              "checked": false   // 默认false 表示未选中
            }, { ... }],
            "month": [{
              "id": 1,
              "text": "1月",
              "checked": true
            }, {
              "id": 2,
              "text": "2月",
              "checked": false   // 默认false 表示未选中
            }, { ... }]  
	 	}
	}
```
<a name="delSeason"></a>

### 当季小众推荐删除

#### POST /guide_season/del

######入参：
			 *id			Int	 ID

######出参：

```javascript
"result":
	{
	 	"operation": 1
	}
```
<a name="guideCityList"></a>

### 攻略首页分类列表
#### GET  /guide_city/lists

######入参：
			   page				Int 分页

######出参：

```javascript
"result":
	{
	  "list": [
		{
		  "id": "ID",
		  "area": "区域",
		  "site": "目的地名称"
		  "desc": "区域描述",
		  "addTime": "添加时间",
          "layout": 3  //  前台展示风格 三栏：3，六栏：6
		 },
		{ ... }			
	  ],
	  "pageTotal": "数量"
	}
```

<a name="guideCitySet"></a>

### 攻略首页分类编辑/新增
#### post  /guide_city/set

######入参：
			*id     Int   ID   // 新增不是必填
			*layout Int   前台展示风格 三栏：3，六栏：6
			 area   String  区域名称
			 desc   String  区域描述
			 site   Array   目的地

######出参：

```javascript
"result":
	{
	  "oeration": 1
	}
```

<a name="guideCityDetail"></a>

### 攻略首页分类详情
#### GET  /guide_city/detail

######入参：
			   *id			Int ID	

######出参：

```javascript
"result":
	{
	  "info": {
		  "id": "ID",
		  "area": "区域",
		  "site": [{
            "id": 1,
            "text": "杭州",
            "coverUrl": "图片封面地址",
            "coverDomain": "封面域名"
		  }, { ... }]，
		  "desc": "区域描述",
		  "addTime": "添加时间",
          "layout": 3  //  前台展示风格 三栏：3，六栏：6
		 }	
	}
```

<a name="delCity"></a>

### 攻略首页分类删除
#### POST  /guide_city/del

######入参：
			   *id			Int ID	
######出参：

```javascript
"result":
	{
	  "operation": 1
	}
```
<a name="citySort"></a>

### 攻略首页分类排序
#### POST  /guide_city/sort

######入参：
######出参：

```javascript
"result":
	{
	  "sort": [{
        "id": 1,
        "rank": 2   // 位置
	  }, { ... }]
	}
```
<a name="guideCitySearch"></a>

### 攻略目的地搜索
#### POST  /guide_city/search

######入参：
			  *text			String 关键字
######出参：

```javascript
"result":
	{
		"list": [{
            "id": 1,
            "text": "杭州",
            "coverUrl": "图片封面地址",
            "coverDomain": "封面域名"
		  }, { ... }]，
	}
```
<a name="guideCityHotSearch"></a>

### 攻略目的地热门搜索关键词
#### POST  /guide_search/lists

######入参：
######出参：

```javascript
"result":
	{
		"list": [{
            "id": 1,  //  分组ID
          	"keyword": [{
              "text": "杭州",
              "viewCount": "访问量"
              },
              { ... }
          	],
          	"time": "创建时间"
		  }, { ... }]
	}
```
<a name="guideCityHotSearchEdit"></a>

### 攻略目的地热门搜索关键词编辑
#### POST  /guide_search/set

######入参：
			  *groupId           Int   分组ID
	           keyword           Array 关键字
######出参：

```javascript
"result":
	{
		"operation": 1
	}
```
<a name="wechatReplyList"></a>

### 微信回复列表
#### POST  /wechat_reply/lists

######入参：
    content        String 搜索内容
######出参：

```javascript
"result":
	{
		"list": [{
            "id": 1,  //  分组ID
          	"nickname":"用户昵称" ,
          	"content":"消息内容",
          	"replyStat":"已回复",
          	"replyName":"回复人",
          	"time": "创建时间"
		  }, { ... }]
	}
```
<a name="wechatReplyHistory"></a>

### 微信回复用户历史信息列表
#### POST  /wechat_reply/history

######入参：
######出参：

```javascript
"result":
	{
		"list": [{
          	"nickname":"用户昵称" ,
          	"content":"消息内容",
          	"time": "创建时间"
		  }, { ... }]
	}
```
<a name="wechatReplySet"></a>

### 向微信用户回复
#### POST  /wechat_reply/set

######入参：
			  *id                Int    回复的id
	          content            String 回复内容
######出参：

```javascript
"result":
	{
		"operation": 1
	}
```