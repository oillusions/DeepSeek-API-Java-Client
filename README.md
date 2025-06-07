## 核心功能

### API配置

```java
// 使用Builder模式配置API参数
DeepSeekConfig config = new DeepSeekConfig.Builder()
    .apiKey("your_api_key_here")
    .model(Model.REASONER)
    .format(ResultFormat.JSON_OBJECT)
    .stream(true)
    .systemPrompt("你是一个专业的AI助手")
    .build();
```

### 对话上下文管理

```java
// 创建对话上下文
DeepSeekContext context = new DeepSeekContext(config);

// 添加消息
context.addMessage(Role.USER, "用户消息");
context.addMessage(Role.ASSISTANT, "AI回复");

// 发送请求
context.request();

// 重置对话
context.resetConversation();
```

### 响应处理与事件监听

```java
// 添加响应监听器
context.addListener(response -> {
    if (response.isSuccess()) {
        if (response.isReasoning()) {
            System.out.print(response.getReasoningContent());
        } else {
            System.out.print(response.getContent());
        }
    } else {
        System.err.println("请求失败: " + response.getStatusCode());
    }
});

// 流式响应处理核心逻辑
while ((line = reader.readLine()) != null) {
    if (line.startsWith("data: ")) {
        // 处理增量更新
    }
}
```

### 接口定义

```java
public interface DeepSeekResponse {
    String getContent();
    String getReasoningContent();
    boolean isReasoning();
    boolean isSuccess();
}
```

### 枚举类型

```java
public enum Model { CHAT, REASONER }
public enum Role { SYSTEM, USER, ASSISTANT }
public enum ResultFormat { TEXT, JSON_OBJECT }
```

## 快速开始

1. 添加依赖到项目
2. 配置API密钥和参数
3. 创建对话上下文并添加消息
4. 添加响应监听器
5. 发送请求并处理响应

```java
public static void main(String[] args) {
    DeepSeekConfig config = new DeepSeekConfig.Builder()
        .apiKey("your_api_key")
        .build();
    
    DeepSeekContext context = new DeepSeekContext(config);
    
    context.addListener(response -> {
        if (response.isSuccess()) {
            System.out.println(response.getContent());
        }
    });
    
    context.addMessage(Role.USER, "你好，你能做什么？");
    context.request();
}
```

---

> [打包好的jar](https://github.com/oillusions/DeepSeek-API-Java-Client/releases/tag/AAA)

---

DeepSeek好耶[这篇README.md也是DeepSeek-R1生成的哦]
