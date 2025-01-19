
Socket系统前端集成指南
====================

* * *

概述
----

本文档提供了Socket系统与前端应用集成的指导和结构。它详细说明了事件结构、类型和前端开发人员需要处理的操作，以确保后端和前端之间的无缝通信。

* * *

事件结构
--------

通过Socket系统发送或接收的每个事件都遵循标准化结构：

```javascript
{
"uid": "11", // 用户ID 
"type": "payment", // 事件类别
"action": "withdraw", // 类型内的具体操作
"description": "从支付宝提现2000元: channelCode - 101" // 事件描述
}
```

### 字段描述

*   **uid** (字符串): 执行动作的用户唯一标识符。
*   **type** (字符串): 事件类别。可接受的值如下所列。
*   **action** (字符串): 与事件类型相关的具体操作。
*   **description** (字符串): 事件的详细说明。

* * *

事件类型和操作
--------------

以下是支持的事件类型及其关联操作的列表：

### 1\. Payment（支付）

*   **操作：**
    *   提现（withdraw）
    *   充值（recharge）
    *   兑换（exchange）
    *   联系（contact）
    *   查账单（check_bill）

### 2\. Game（游戏）

*   **操作：**
    *   提现（withdraw）
    *   存款（deposit）
    *   兑换（exchange）
    *   玩游戏（play）
    *   查看余额（check_balance）
    *   查看记录（check_record）

### 3\. Live（直播）

*   **操作：**
    *   观看（watch）
    *   打赏（tip）
    *   评论（comment）
    *   搜索（search）
    *   查看排名（check_ranking）

### 4\. Video（视频）

*   **操作：**
    *   观看（watch）
    *   搜索（search）

### 5\. VIP

*   **操作：**
    *   升级（upgrade）
    *   阅读书籍（read_book）

### 6\. Setting（设置）

*   **操作：**
    *   修改密码（change_password）
    *   编辑信息（edit_info）
    *   查看余额（check_balance）
    *   更改语言（change_language）
    *   安全设置（security）
    *   切换账号（switch_account）

### 7\. Promotion（促销）

*   **操作：**
    *   查看（check）
    *   使用（use）

### 8\. General（通用）

*   **操作：**
    *   登录（login）
    *   搜索（search）
    *   联系客服（contact_service）
    *   贡献（contribution）

* * *

使用JavaScript的集成示例
------------------------

### 1\. 监听事件：

前端应用应建立Socket连接，并监听来自后端的事件。事件数据将符合上述结构。

**示例：** 
```javascript
socket.on('event', (data) => { 
   console.log('接收到的事件:', data); 
   handleEvent(data); 
});
```

### 2\. 处理事件：

创建一个处理程序函数，根据事件的类型和操作处理传入的事件。

**示例：** 
```javascript 
function handleEvent(event) {
   switch (event.type)
      {
         case 'payment': handlePaymentEvent(event);
         break;
         case 'game': handleGameEvent(event);
         break;
         // 根据需要添加其他类型的处理
         default: console.warn('未知的事件类型:', event.type);
       }
 }

function handlePaymentEvent(event) {
   if (event.action === 'withdraw') {
      console.log('处理提现操作:', event.description); // 执行提现的前端逻辑
       }
};
```

### 3\. 发送事件：

要从前端发起事件，请遵循相同的结构，并通过Socket连接发送事件。

**示例：** 
```javascript
const event = { uid: '11', type: 'payment', action: 'recharge', description: '通过channelCode - 102充值5000元到账户' };

socket.emit('event', event);
 ```

### 4\. 错误处理：

确保优雅地处理任何错误或意外数据。

**示例：** 
```javascript
socket.on('error', (error) => { 
   console.error('Socket错误:', error); 
});
```

* * *

结论
----

通过遵循本指南，前端开发人员可以有效地将Socket系统集成到应用中，从而确保与后端高效、可靠的通信。如有任何疑问或需额外支持，请联系后端团队。
