**domain(服务域名):**
- http://47.120.22.253:8080/

---

# 0.目录
[TOC]

---

/debug (展示后台数据,curd)

---
# 1.用户相关API

/user(用户信息)

---
## 1.授权API

/auth (授权)

---

### 1.登录

/auth/login [POST]

**参数**

| 参数名  | 类型     |
|------|--------|
| code | string |

**返回值:**

| 参数名         | 类型     |
|-------------|--------|
| token       | string |
| openid      | string |
| first_login | bool   |

[回到目录](#0目录)

---

### 2.检验登录态 

/auth/checkLogin [POST]

status为false则token已过期

**Header**

| 参数名   | 类型名    |
|-------|--------|
| token | string |

**返回值**

| 参数名    | 类型名  |
|--------|------|
| status | bool |

[回到目录](#0目录)

---

## 2.用户信息API

/user/info 

**Header**

| 参数名   | 类型名    |
|-------|--------|
| token | string |

---

### 1.用户简介API

/user/info/text

---

#### 1.修改个人简介

/user/info/text/editInfo [POST]

**参数**

| 参数名  | 类型名    |
|------|--------|
| text | string |

**返回值**

success_msg_response

[回到目录](#0目录)

---

#### 2.获取用户信息和简介

/user/info/text/getInfo [POST]

**参数**

| 参数名               | 类型名    |
|-------------------|--------|
| user_id(可选，缺省为自己) | string |

**返回值**

| 参数名                        | 类型名    |
|----------------------------|--------|
| id                         | string |
| nickname                   | string |
| info                       | string |
| star_rating                | number |
| time ("%Y/%m/%d %H:%M:%S") | string |

[回到目录](#0目录)

---

#### 3.设置用户昵称

/user/info/text/setNickname [POST]

**参数**

| 参数名      | 类型名    |
|----------|--------|
| nickname | string |


**返回值**

success_msg_response

[回到目录](#0目录)

---

### 2.用户头像API

/user/info/avatar

---

#### 1.添加用户头像

/user/info/avatar/add [POST]

使用wx.uploadFile方法

**参数**

| 参数名                 | 类型名    |
|---------------------|--------|
| name(常量,填写avatar即可) | string |

**返回值**
success_msg_response

[回到目录](#0目录)

---

#### 2.获取用户头像

/user/info/avatar/get [GET]

**该API只接受GET方法**

**参数写在url中**

格式为 /user/info/avatar/get?token=&user_id=

**参数**

| 参数名                  | 类型名    |
|----------------------|--------|
| token                | string |
| user_id(可选,不填返回自己头像) | string |

**返回值**
图片数据,可直接使用src引用

[回到目录](#0目录)

---

### 3.用户个性标签API

/user/info/tag

#### 1.增加用户个人标签

/user/info/tag/add [POST]

**参数**

| 参数名      | 类型名    |
|----------|--------|
| tag_text | string |

**返回值**

success_msg_response

[回到目录](#0目录)

---

#### 2.获取用户个人标签

/user/info/tag/get [POST]

**参数**

| 参数名                    | 类型名    |
|------------------------|--------|
| user_id(可选，缺省即获取自己的标签) | string |

**返回值**

| 参数名             | 类型名    |
|-----------------|--------|
| tags            | array  |
| tags[]          | object |
| tags[].id       | number |
| tags[].user_id  | string |
| tags[].tag_text | string |

[回到目录](#0目录)


---
#### 3.删除用户个人标签

**参数**

| 参数名    | 类型名    |
|--------|--------|
| tag_id | number |


**返回值**

success_msg_response

---

#### 4.修改用户个人标签
``
**参数**

| 参数名      | 类型名    |
|----------|--------|
| tag_id   | number |
| tag_text | string |

**返回值**

success_msg_response


---

# 2.群组相关API

/group (群组)

**Header**

| 参数名   | 类型名    |
|-------|--------|
| token | string |

---

## 1.外部API (用户相对于群组)

/group/external

---
### 1.群组外API

/group/external/group

---
#### 1.创建群组

/group/external/group/create [POST]

**参数**

| 参数名        | 类型名    |
|------------|--------|
| type       | string |
| name       | string |
| user_limit | number |

**返回值**

success_msg_response

[回到目录](#0目录)

---


#### 2.发起加入群组请求

/group/external/group/join [POST]

**参数**

| 参数名      | 类型名    |
|----------|--------|
| group_id | string |

**返回值**

success_msg_response

[回到目录](#0目录)

---

### 2.加入请求API

/group/external/joinRequest

---

#### 1.获取该用户管理的组的所有加入请求

/group/external/joinRequest/getAll [POST]

**参数**
无

**返回值**

| 参数名                      | 类型名    |
|--------------------------|--------|
| join_requests            | array  |
| join_requests[]          | object |
| join_requests[].id       | number |
| join_requests[].user_id  | string |
| join_requests[].group_id | number |

[回到目录](#0目录)

---

#### 2.处理加入请求

/group/external/joinRequest/process [POST]

**参数**

| 参数名        | 类型名    |
|------------|--------|
| request_id | number |
| action     | bool   |

**返回值**

success_msg_response

[回到目录](#0目录)

---

### 3.搜索API

/group/external/search

---

#### 1.群组名提示

/group/external/search/name_hint [POST]

**参数**

| 参数名     | 类型名    |
|---------|--------|
| type    | string |
| key(可选) | string |

**返回值**

| 参数名     | 类型名    |
|---------|--------|
| hints   | array  |
| hints[] | string |

[回到目录](#0目录)

---

#### 2.群组标签提示

/group/external/search/tag_hint [POST]

**参数**

| 参数名     | 类型名    |
|---------|--------|
| type    | string |
| key(可选) | string |

**返回值**

| 参数名     | 类型名    |
|---------|--------|
| hints   | array  |
| hints[] | string |

[回到目录](#0目录)

---

#### 3.搜索群组

/group/external/search/group [POST]

sort_method 只能为 ('COMPREHENSIVE'(综合),
'RELATIVE'(相关度优先),
'TIME'(创建时间优先),
'MEMBER'(人数优先))

sort_order 只能为 ('ASC'(升序),'DESC'(降序))

**参数**

| 参数名                    | 类型名    |
|------------------------|--------|
| type                   | string |
| key(可选)                | string |
| tags(可选)               | array  |
| tags[]                 | string |
| sort_method(可选,默认综合排序) | string |
| sort_order(可选,默认降序)    | string |

**返回值**

| 参数名                 | 类型名    |
|---------------------|--------|
| groups              | array  |
| groups[]            | object |
| groups[].id         | number |
| groups[].name       | string |
| groups[].type       | string |
| groups[].user_cnt   | number |
| groups[].user_limit | number |
| groups[].time       | string |

[回到目录](#0目录)

---

#### 4.搜索我的群组

/group/external/search/my_group [POST]

sort_method 只能为 ('COMPREHENSIVE'(综合),
'RELATIVE'(相关度优先),
'TIME'(创建时间优先),
'MEMBER'(人数优先))

sort_order 只能为 ('ASC'(升序),'DESC'(降序))

**参数**

| 参数名                      | 类型名    |
|--------------------------|--------|
| type(可为空字符串,即从我的所有群组中搜索) | string |
| key(可选)                  | string |
| tags(可选)                 | array  |
| tags[]                   | string |
| sort_method(可选,默认综合排序)   | string |
| sort_order(可选,默认降序)      | string |

**返回值**

| 参数名                            | 类型名    |
|--------------------------------|--------|
| groups                         | array  |
| groups[]                       | object |
| groups[].id                    | number |
| groups[].name                  | string |
| groups[].type                  | string |
| groups[].user_cnt              | number |
| groups[].user_limit            | number |
| groups[].time                  | string |
| dismissed_groups (字段与groups相同) | array  |

[回到目录](#0目录)

---


## 2.内部API (用户相对于群组)

/group/internal

---

### 1.群组信息API

/group/internal/info

---

#### 1.群组简介API

/group/internal/info/text

---

##### 1.编辑群组简介

/group/internal/info/text/edit [POST]

**参数**

| 参数名      | 类型名    |
|----------|--------|
| group_id | number |
| text     | string |

**返回值**
success_msg_response

[回到目录](#0目录)

---

##### 2.查看群组信息和简介

/group/internal/info/text/get [POST]

**参数**

| 参数名      | 类型名    |
|----------|--------|
| group_id | number |

**返回值**

| 参数名                       | 类型名    |
|---------------------------|--------|
| id                        | number |
| type                      | string |
| name                      | string |
| user_cnt                  | number |
| user_limit                | number |
| info                      | string |
| time("%Y/%m/%d %H:%M:%S") | string |


[回到目录](#0目录)

---

##### 3.设置群组名

只有群主有权限调用此API

/group/internal/info/text/set_name [POST]

**参数**

| 参数名      | 类型名    |
|----------|--------|
| group_id | number |
| name     | string |

**返回值**
success_msg_response

[回到目录](#0目录)

---

#### 2.群组头像API

/group/internal/info/avatar

---

##### 1.添加群组头像 (需要管理员权限)

/group/internal/info/avatar/add [POST]

使用wx.uploadFile方法
group_id填写在formData中

**参数**

| 参数名                 | 类型名    |
|---------------------|--------|
| name(常量,填写avatar即可) | string |
| group_id            | number |

**返回值**
success_msg_response

[回到目录](#0目录)

---

##### 2.获取群组头像

/group/internal/info/avatar/get [GET]

**该API只接受GET方法**

**参数写在url中**

格式为 /group/internal/info/avatar/get?token=&group_id=

**参数**

| 参数名      | 类型名    |
|----------|--------|
| token    | string |
| group_id | number |

**返回值**
图片数据,可直接使用src引用

[回到目录](#0目录)

---

#### 3.群组简介图片API

/group/internal/info/picture

---

##### 1.获取所有照片id

/group/internal/info/picture/getAll [POST]

**参数**

| 参数名      | 类型名    |
|----------|--------|
| group_id | number |

**返回值**


| 参数名           | 类型名    |
|---------------|--------|
| pictures      | array  |
| pictures[]    | object |
| pictures[].id | number |

[回到目录](#0目录)

---
##### 2.获取照片

/group/internal/info/picture/get [GET]

**参数**

| 参数名      | 类型名    |
|----------|--------|
| group_id | number |
| pic_id   | number |

**返回值**

图片二进制数据 可直接使用src引用

[回到目录](#0目录)

---

##### 3.添加图片

/group/internal/info/picture/add [POST]

使用wx.uploadFile方法
group_id填写在formData中

**参数**

| 参数名              | 类型名    |
|------------------|--------|
| name(常量,填写pic即可) | string |
| group_id         | number |

**返回值**

success_msg_response

[回到目录](#0目录)

---

##### 4.移除照片

/group/internal/info/picture/del [POST]

**参数**

| 参数名      | 类型名    |
|----------|--------|
| group_id | number |
| pic_id   | number |

**返回值**

success_msg_response

[回到目录](#0目录)

---

#### 4.群组标签API

/group/internal/info/tag

---

##### 1.获取群组标签

/group/internal/info/tag/get [POST]

**参数**

| 参数名      | 类型名    |
|----------|--------|
| group_id | number |

**返回值**

| 参数名             | 类型名    |
|-----------------|--------|
| tags            | array  |
| tags[]          | object |
| tags[].id       | number |
| tags[].tag_text | string |


---

##### 2.添加群组标签

/group/internal/info/tag/add [POST]

**参数**

| 参数名      | 类型名    |
|----------|--------|
| group_id | number |
| tag_text | string |

**返回值**

success_msg_response

[回到目录](#0目录)

---

##### 3.删除群组标签

/group/internal/info/tag/remove [POST]

**参数**

| 参数名      | 类型名    |
|----------|--------|
| group_id | number |
| tag_id   | number |

**返回值**

success_msg_response

[回到目录](#0目录)

---
##### 4.编辑群组标签

/group/internal/info/tag/add [POST]

**参数**

| 参数名      | 类型名    |
|----------|--------|
| group_id | number |
| tag_id   | number |
| tag_text | string |

**返回值**

success_msg_response

[回到目录](#0目录)

---

### 2.群员API

/group/internal/member

---

#### 1.获取小组成员

/group/internal/member/get [POST]

**参数**

| 参数名      | 类型名    |
|----------|--------|
| group_id | number |

**返回值**

| 参数名                                | 类型名    |
|------------------------------------|--------|
| users                              | array  |
| users[]                            | object |
| users[].user_id                    | number |
| users[].nickname                   | string |
| users[].is_admin                   | bool   |
| users[].is_creator                 | bool   |
| users[].time ("%Y/%m/%d %H:%M:%S") | string |

[回到目录](#0目录)

---

#### 2.移除组员

/group/internal/member/remove [POST]

**参数**

| 参数名      | 类型名    |
|----------|--------|
| group_id | number |
| user_id  | string |

**返回值**
success_msg_response

[回到目录](#0目录)

---

#### 3.设置组内昵称

/group/internal/member/setNickname [POST]

**参数**

| 参数名      | 类型名    |
|----------|--------|
| group_id | number |
| nickname | string |

**返回值**
success_msg_response 

[回到目录](#0目录)

---

#### 4.对小组其他成员评分(只能在解散后的组中调用)

/group/internal/member/rate [POST]

**在token验证通过后，此API有且仅有一次调用机会!**

**参数**
**rates中不能包含自己**

| 参数名                 | 类型名    |
|---------------------|--------|
| group_id            | number |
| rates               | array  |
| rates[]             | object |
| rates[].user_id     | string |
| rates[].star_rating | number |

**返回值**

success_msg_response

[回到目录](#0目录)

---

#### 5.设置小组成员管理员

/group/internal/member/switchAdmin [POST]

**参数**

| 参数名      | 类型名    |
|----------|--------|
| group_id | number |
| user_id  | number |

**返回值**

success_msg_response

[回到目录](#0目录)

---

### 3.群组设置API

/group/internal/setting

---

#### 1.解散组队

/group/internal/setting/dismiss [POST]

**参数**

| 参数名      | 类型名    |
|----------|--------|
| group_id | number |

**返回值**
success_msg_response

[回到目录](#0目录)

---

#### 2.退出组队

/group/internal/setting/exit [POST]

**参数**

| 参数名      | 类型名    |
|----------|--------|
| group_id | number |

**返回值**
success_msg_response

[回到目录](#0目录)

---

### 4.群组公告

/group/internal/announcement

---

#### 1.获取所有公告

/group/internal/announcement/getAll [POST]


**参数**

| 参数名      | 类型名    |
|----------|--------|
| group_id | number |

**返回值**

| 参数名                                        | 类型名    |
|--------------------------------------------|--------|
| announcements                              | array  |
| announcements[]                            | object |
| announcements[].id                         | number |
| announcements[].title                      | string |
| announcements[].time ("%Y/%m/%d %H:%M:%S") | string |

[回到目录](#0目录)

---

#### 2.获取公告信息

/group/internal/announcement/get [POST]

**参数**

| 参数名             | 类型名    |
|-----------------|--------|
| group_id        | number |
| announcement_id | number |

**返回值**

| 参数名                | 类型名    |
|--------------------|--------|
| announcement       | object |
| announcement.id    | number |
| announcement.title | string |
| announcement.text  | string |

[回到目录](#0目录)

---

#### 3.发布公告

/group/internal/announcement/add [POST]

**参数**

| 参数名      | 类型名    |
|----------|--------|
| group_id | number |
| title    | string |
| text     | string |


**返回值**
success_msg_response

[回到目录](#0目录)

---

#### 4.编辑公告

/group/internal/announcement/edit [POST]

**参数**

| 参数名             | 类型名    |
|-----------------|--------|
| announcement_id | number |
| group_id        | number |
| title           | string |
| text            | string |

**返回值**
success_msg_response

[回到目录](#0目录)

---
#### 5.删除公告

/group/internal/announcement/delete [POST]

**参数**

| 参数名             | 类型名    |
|-----------------|--------|
| announcement_id | number |
| group_id        | number |

**返回值**
success_msg_response

[回到目录](#0目录)

---

#### 6.设置公告图片

/group/internal/announcement/setPic [POST]

使用wx.uploadFile方法
group_id填写在formData中

**参数**

| 参数名              | 类型名    |
|------------------|--------|
| name(常量,填写pic即可) | string |
| group_id         | number |
| announcement_id  | number |

**返回值**
success_msg_response

[回到目录](#0目录)

---

#### 7.删除公告图片 [POST]

/group/internal/announcement/delPic [POST]

**参数**

| 参数名              | 类型名    |
|------------------|--------|
| group_id         | number |
| announcement_id  | number |

**返回值**

success_msg_response

[回到目录](#0目录)

---

#### 8.获取公告图片 

/group/internal/announcement/getPic [GET]

**参数**

| 参数名              | 类型名    |
|------------------|--------|
| group_id         | number |
| announcement_id  | number |

**返回值**

图片数据

[回到目录](#0目录)


---

### 5.群组文件API

/group/internal/files

群文件最大容量:
**5GB**

**文件/文件夹重名是不合法的**

**parent_id代表父文件夹id**

---

#### 1.获取目录

/group/internal/files/get_dir [POST]

注:

parent_id为选填 不填即为查看群文件根目录

type为dir时代表此文件为文件夹 为.*时代表文件后缀

size单位为字节

time格式为"%Y/%m/%d %H:%M:%S"

**参数**

| 参数名       | 类型名    |
|-----------|--------|
| group_id  | number |
| parent_id | number |


**返回值**

| 参数名               | 类型名    |
|-------------------|--------|
| files             | array  |
| files[]           | object |
| files[].id        | number |
| files[].parent_id | number |
| files[].name      | string |
| files[].type      | string |
| files[].size      | number |
| files[].time      | string |
| files[].duration  | number |
| files[].file_type | string |

[回到目录](#0目录)

---

#### 2.创建文件夹

/group/internal/files/mk_dir [POST]

**参数**

| 参数名       | 类型名    |
|-----------|--------|
| group_id  | number |
| parent_id | number |
| name      | string |


**返回值**

success_msg_response

[回到目录](#0目录)

---

#### 3.下载文件

/group/internal/files/download [GET]

**使用wx.downloadFile方法**

**下载的文件不能是一个文件夹**

**参数**

| 参数名                      | 类型名                 |
|--------------------------|---------------------|
| group_id                 | number              |
| file_id                  | number              |
| thumbnail(可选,下载视频/图片缩略图) | string(填入任何非空字符串即可) |


**返回值**

文件数据

[回到目录](#0目录)

---

#### 4.上传文件

**使用wx.uploadFile方法**

parent_id为选填 不填即为上传到群文件根目录

/group/internal/files/upload [POST]

**参数**

| 参数名               | 类型名    |
|-------------------|--------|
| group_id          | number |
| parent_id         | number |
| name(常量,填写file即可) | string |

**返回值**

**参数**

| 参数名     | 类型名    |
|---------|--------|
| file_id | number |


[回到目录](#0目录)

---

#### 5.删除文件/文件夹

/group/internal/files/delete [POST]

**参数**

| 参数名      | 类型名    |
|----------|--------|
| group_id | number |
| file_id  | number |

**返回值**

success_msg_response

[回到目录](#0目录)

---

#### 6.修改文件/文件夹名

/group/internal/files/edit_name [POST]

**参数**

| 参数名      | 类型名    |
|----------|--------|
| group_id | number |
| file_id  | number |
| name     | string |

**返回值**

success_msg_response

[回到目录](#0目录)

---

#### 7.移动文件/文件夹

/group/internal/files/move [POST]

**参数**

| 参数名       | 类型名    |
|-----------|--------|
| group_id  | number |
| file_id   | number |
| parent_id | number |

**返回值**

success_msg_response

[回到目录](#0目录)

---

#### 8.分享文件至群聊

/group/internal/files/share [POST]

**参数**

| 参数名      | 类型名    |
|----------|--------|
| group_id | number |
| file_id  | number |

**返回值**

success_msg_response

[回到目录](#0目录)

---

# 3.聊天API

使用Websocket协议

wss://[域名]

**Header**

| 参数名   | 类型名    |
|-------|--------|
| token | string |

注: 服务器每5秒发送一个ping 若没有接收到可以自行新建连接

**客户端/服务端消息是一个JSON字符串**

一个客户端消息包含以下字段 (字段有严格检查,不能有多余字段):

    msg_type:('text'/'history')
    
    content (msy_type!='history',获取聊天记录时除外):string
    
    msg_id (msy_type=='history',当需要获取消息记录时,指定记录开始的前一个消息的ID):int

    file_id (msy_type!='history' or 'text',当消息类型不是文本时):int
    
    at (只能在群组聊天中):['user_id1','user_id2',...](user_id:string)

示例1:

    {
        "msg_type":"text",
        "content":"孩子们,我回来了",
        "at":["user1_id","user2_id"]
    }

示例2:

    {
        "msg_type":"history",
        "msg_id":114514
    }

服务端消息字段

msg.msg_type:('text'/'image'/'voice'/'video'/'file')

msg.content 只在text消息类型出现 代表消息内容

msg.file_id 只在除text以外的消息类型中出现 代表该文件的id

msg.file_info type == ('image'/'voice'/'video'/'file') 包含以下字段

    'id' 文件id
    'name' 文件名(包含后缀)
    'type' 后缀名
    'size' 文件大小 单位B
    'time' 上传时间
    'duration' 时长 type == ('voice'/'video') 时出现
    'file_type' 文件类型 ('image'/'voice'/'video'/'file')

history 为真表示该消息是历史记录

---

## 1.群组聊天

/chat/group?group_id=

**参数**

| 参数名      | 类型名    |
|----------|--------|
| group_id | number |

**服务器在连接或刷新时依次发送20条消息记录**

**消息记录按时间升序发送**

| 参数名          | 类型名                        |
|--------------|----------------------------|
| id           | number                     |
| user_id      | string                     |
| nickname     | string                     |
| msg          | object                     |
| msg.msg_type | string                     |
| msg.content  | string                     |
| msg.file_id  | number                     |
| msg.at       | array                      |
| msg.at[]     | string (user_id)           |
| time         | string (%Y/%m/%d %H:%M:%S) |
| history      | bool                       |

[回到目录](#0目录)

---

## 2.私密聊天

/chat/private?user_id=

**参数**

| 参数名     | 类型名    |
|---------|--------|
| user_id | string |

**返回值**


| 参数名          | 类型名                        |
|--------------|----------------------------|
| id           | number                     |
| user_id      | string                     |
| nickname     | string                     |
| msg          | object                     |
| msg.msg_type | string                     |
| msg.content  | string                     |
| msg.file_id  | number                     |
| msg.at       | array                      |
| msg.at[]     | string (user_id)           |
| time         | string (%Y/%m/%d %H:%M:%S) |
| history      | bool                       |


[回到目录](#0目录)

---

## 3.上传临时语音/图片/视频/文件

/chat/files/upload [POST]

**注意:若要上传群文件请移步至群文件API**

**参数**

| 参数名             | 类型名    |
|-----------------|--------|
| type            | string |
| room_id         | number |
| name (常量,填file) | string |

**返回值**


| 参数名     | 类型名    |
|---------|--------|
| file_id | number |

[回到目录](#0目录)

---

## 4.下载临时语音/图片/视频/文件

/chat/files/download [GET]

**参数**

| 参数名                      | 类型名                 |
|--------------------------|---------------------|
| type                     | string              |
| room_id                  | number              |
| file_id                  | number              |
| thumbnail(可选,下载视频/图片缩略图) | string(填入任何非空字符串即可) |

**返回值**
文件数据

[回到目录](#0目录)

---

## 5.获取所有私聊用户

/chat/getChat [POST]

**返回值**

| 参数名                   | 类型名    |
|-----------------------|--------|
| private               | array  |
| private[]             | object |
| private[].id          | string |
| private[].nickname    | string |
| private[].info        | string |
| private[].star_rating | number |
| private[].time        | string |

---
# 4.错误码

**错误码储存在code字段**

**错误信息储存在errorMsg字段**

---

## 100

所有服务错误的基类

---

### 101

参数缺少/有误

查阅API文档检查你的参数名是否缺失/正确

如果检查后依旧报错 上报这个错误给后端人员

[回到目录](#0目录)

---

## 110

token错误基类

[回到目录](#0目录)

---

### 111

token过期

需要重新登录

---

### 112

token不合法

检查token是否为本服务器签发

[回到目录](#0目录)

---

### 113

token缺失

检查header中是否包含token字段

[回到目录](#0目录)

---

## 200

用户服务错误的基类

---

### 201

昵称为空

检查传入的昵称是否为空

[回到目录](#0目录)

---

### 202

用户不存在

检查传入的用户id是否存在

[回到目录](#0目录)

---

## 210

个性标签错误的基类

---

### 211

个性标签不存在

检查传入的标签id是否存在

[回到目录](#0目录)

---

### 212

个性标签为空

检查传入的个性标签是否为空

[回到目录](#0目录)

---

## 300

群组服务错误基类

---

### 301

群组不存在

检查群组id是否存在

[回到目录](#0目录)

---

### 302

用户不存在

检查用户id是否存在

[回到目录](#0目录)

---

### 303

用户无权限进行此操作

检查用户身份

[回到目录](#0目录)

---

### 304

群组已解散

解散的群组的信息无法再被修改

[回到目录](#0目录)

---

## 310

加入群组错误基类

[回到目录](#0目录)

---

### 311

已经进入群组

不能对已经加入过的群组发起加入请求

[回到目录](#0目录)

---

### 312

已经加入过群组

不能对已经发起过加入请求的群组再次发送请求

[回到目录](#0目录)

---

### 314

群组已满

无法对已满的群组发起加入请求

[回到目录](#0目录)

---

## 320

群组参数错误基类

---

### 321

rating越界

rating只能是0-10之间的一个浮点数

[回到目录](#0目录)

---

## 330

群组简介照片错误基类

---

### 331

简介照片已满

[回到目录](#0目录)

---

### 332

简介照片不存在

检查照片id是否存在

[回到目录](#0目录)

---

## 340

群文件错误基类


---

### 341

文件不存在

[回到目录](#0目录)

---

### 342

文件夹不存在

[回到目录](#0目录)

---

### 343

文件已存在

检查文件名是否重复

[回到目录](#0目录)

---

### 344

群文件已满

[回到目录](#0目录)

---

### 350

搜索错误基类

---

### 351

群组类型不存在

[回到目录](#0目录)

---

### 352

排序顺序不存在

[回到目录](#0目录)

---


### 353

排序方法不存在

[回到目录](#0目录)

---

### 360

群组标签异常基类

---

### 361

群组标签不存在

---

### 362

群组标签为空

---

## 400

聊天错误基类

---

### 401

私聊用户不存在

---

### 402

群聊不存在

---

### 403

不在群组内

---

### 404

群组已解散

---

### 405

消息类型不存在

---

### 406

临时文件不存在

---

### 407

上传临时文件时不在房间内

---

### 408

房间号不存在

---

### 409

消息格式错误

---


### 410

房间类型错误

---
