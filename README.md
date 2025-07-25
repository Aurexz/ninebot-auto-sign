# 九号签到脚本

在 [青龙面板](https://github.com/whyour/qinglong) 中配置环境变量，实现“九号出行 APP 自动签到获取 N 币”。

---

## 一、前期准备

1. **安装青龙面板**  
   按照官方文档完成青龙部署 [->青龙面板](https://github.com/whyour/qinglong)
2. **获取 DeviceId & Authorization**
   - 打开九号出行 APP，抓包请求：`/portal/api/user-sign/v2/sign`
   - 从请求参数中复制 `deviceId`
   - 从请求头（headers）中复制 `authorization`

---

## 二、青龙面板环境变量配置

1. 登录青龙 Web 面板，点击左侧「环境变量」→「新增」
2. 填写如下信息：

   | 变量名           | 变量值                   | 说明                    |
   | ---------------- | ------------------------ | ----------------------- |
   | `NINEBOT_CONFIG` | `deviceId@authorization` | 多个账号用换行或 & 分隔 |

---

## 三、定时任务设置

在青龙面板「定时任务」中新建或编辑已有任务，填写：

- **命令**：`node /ql/scripts/ninebot_sign.js`
- **定时表达式**：例如 `0 0 8 * * *`（每天 8:00 自动触发）

---

## 四、常见问题

1. **脚本报错 “authorization 失效”**
   - 需重新抓包获取最新 `authorization`
2. **多账号只执行第一个**
   - 确保各账号间用换行或 `&` 正确分隔
