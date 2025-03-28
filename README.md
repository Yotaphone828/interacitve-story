# 互动小说游戏

一个基于 AI 的互动小说游戏系统，能将任意小说章节转换为多关卡的互动游戏。

## 后端工作流程

1. **游戏创建** (`/create_game`)
   - 接收用户提供的小说章节内容
   - 调用 AI 提取小说信息（背景和角色）
   - 基于提取的信息生成多个游戏关卡
   - 创建游戏会话（session），存储游戏状态
   - 返回可选角色列表给前端

2. **角色选择** (`/select_character`)
   - 接收用户选择的角色索引
   - 将选择的角色保存到会话中
   - 准备开始第一个关卡

3. **关卡加载** (`/get_level`)
   - 获取当前关卡信息（描述、通关条件等）
   - 异步生成关卡背景图片
   - 选择一个 AI 角色（非玩家角色）
   - 返回关卡信息给前端
   - 使用会话缓存避免重复生成

4. **AI 对话流** (`/stream_level_dialogue`)
   - 以选定的 AI 角色身份生成对话
   - 使用 SSE 流式返回对话内容
   - 缓存生成的对话，避免重复请求

5. **回应评估** (`/submit_response`)
   - 接收用户的回应文本
   - 根据关卡通关条件评估回应
   - 更新聊天历史
   - 通过则进入下一关，否则继续当前关卡

## 数据缓存

- 使用 `stories.json` 持久化存储已处理的故事
- 使用内存中的 `sessions` 字典存储游戏会话
- 会话中缓存图片 URL 和对话内容，避免重复生成

## API 依赖

- 文本生成：DeepSeek API
- 图片生成：Janus Pro API
- 语音相关：FishAudio API（预留）

## 调试功能

- 使用 SSE 实时推送调试日志到前端
- 记录 AI 生成过程的中间推理
- 支持查看完整的请求响应过程

# 操作和应用
  先确保您的虚拟环境满足运行条件,并配置好您的API KEY,然后运行app.py文件即可
  
