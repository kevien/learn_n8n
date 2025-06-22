# n8n 工作流自动化培训计划

## 培训概述

### 培训目标
- 掌握n8n核心概念和工作流设计原理
- 熟练使用n8n进行业务自动化
- 能够独立设计和实现复杂的工作流
- 掌握n8n部署和运维最佳实践

### 培训对象
- 有一定编程基础的技术人员
- 需要实现业务流程自动化的业务人员
- 对工作流自动化感兴趣的开发者

### 培训时长
- 总时长：5天（40小时）
- 理论讲解：20小时
- 实操练习：20小时

---

## 第一天：n8n基础入门

### 上午：n8n概述与环境搭建

#### 1.1 n8n简介与核心概念（2小时）

**理论内容：**
- n8n是什么：开源工作流自动化平台
- 核心优势：可视化编程、丰富的集成、开源免费
- 应用场景：数据同步、API集成、业务流程自动化
- 与其他工具的对比：Zapier、Make、Power Automate

**实操练习：**
- 注册n8n Cloud账号
- 本地Docker环境搭建
- 界面熟悉和基本操作

**练习任务：**
```bash
# 本地Docker安装
docker run -it --rm \
  --name n8n \
  -p 5678:5678 \
  -v ~/.n8n:/home/node/.n8n \
  n8nio/n8n
```

#### 1.2 工作流基础概念（2小时）

**理论内容：**
- 节点（Node）：工作流的基本构建块
- 连接（Connection）：节点间的数据流转
- 触发器（Trigger）：工作流的启动方式
- 执行器（Executor）：工作流的运行引擎

**实操练习：**
- 创建第一个简单工作流
- 理解节点配置界面
- 测试工作流执行

**练习案例：**
创建一个"Hello World"工作流：
1. 使用Manual Trigger节点
2. 添加Set节点设置消息
3. 使用HTTP Request节点发送到webhook.site

### 下午：基础节点操作

#### 1.3 常用节点详解（3小时）

**理论内容：**
- HTTP Request节点：API调用基础
- Set节点：数据转换和设置
- IF节点：条件判断和分支
- Switch节点：多路分支处理
- Code节点：自定义JavaScript代码

**实操练习：**
- HTTP Request节点调用公开API
- 使用Set节点进行数据转换
- 实现条件判断逻辑

**练习案例：**
天气查询工作流：
```javascript
// Code节点示例
const city = $input.first().json.city;
const apiKey = 'your_api_key';
const url = `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${apiKey}`;

return [{json: {url, city}}];
```

#### 1.4 数据流转与处理（3小时）

**理论内容：**
- 数据格式：JSON结构理解
- 数据访问：$json、$node、$position语法
- 数据转换：映射和转换技巧
- 错误处理：异常捕获和处理

**实操练习：**
- 数据映射练习
- 错误处理机制实现
- 数据验证和清洗

**练习案例：**
用户数据处理工作流：
1. 接收用户数据
2. 数据验证和清洗
3. 格式转换
4. 错误处理和日志记录

---

## 第二天：集成与连接

### 上午：API集成基础

#### 2.1 REST API集成（3小时）

**理论内容：**
- REST API基础概念
- HTTP方法：GET、POST、PUT、DELETE
- 认证方式：API Key、OAuth、Basic Auth
- 请求头和参数设置

**实操练习：**
- 调用GitHub API获取仓库信息
- 使用Postman测试API
- 在n8n中实现API调用

**练习案例：**
GitHub仓库监控工作流：
```javascript
// 获取用户仓库列表
const username = $input.first().json.username;
const url = `https://api.github.com/users/${username}/repos`;

return [{
  json: {
    method: 'GET',
    url: url,
    headers: {
      'Accept': 'application/vnd.github.v3+json'
    }
  }
}];
```

#### 2.2 Webhook集成（3小时）

**理论内容：**
- Webhook工作原理
- 安全验证：签名验证、Token验证
- 实时数据处理
- Webhook测试工具

**实操练习：**
- 创建Webhook端点
- 实现签名验证
- 处理实时数据流

**练习案例：**
订单通知系统：
1. 接收订单Webhook
2. 验证签名
3. 发送通知到Slack
4. 记录到数据库

### 下午：数据库集成

#### 2.3 数据库操作（3小时）

**理论内容：**
- 数据库连接配置
- CRUD操作：增删改查
- 事务处理
- 连接池管理

**实操练习：**
- MySQL/PostgreSQL连接
- 数据插入和查询
- 批量数据处理

**练习案例：**
用户管理系统：
```sql
-- 用户表结构
CREATE TABLE users (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(100),
  email VARCHAR(100) UNIQUE,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

#### 2.4 文件操作与存储（3小时）

**理论内容：**
- 文件系统操作
- 云存储集成：AWS S3、Google Cloud Storage
- 文件格式处理：CSV、Excel、JSON
- 大文件处理策略

**实操练习：**
- 本地文件读写
- 云存储文件上传下载
- 文件格式转换

**练习案例：**
数据导出工作流：
1. 从数据库查询数据
2. 转换为CSV格式
3. 上传到云存储
4. 发送下载链接

---

## 第三天：高级功能与优化

### 上午：高级节点与功能

#### 3.1 高级节点详解（3小时）

**理论内容：**
- Merge节点：数据合并策略
- Split In Batches：批量处理
- Wait节点：延时和调度
- Execute Workflow：工作流调用
- Function节点：复杂逻辑处理

**实操练习：**
- 数据合并和拆分
- 批量处理大量数据
- 工作流嵌套调用

**练习案例：**
批量邮件发送系统：
```javascript
// Function节点：邮件模板处理
const users = $input.all();
const template = $input.first().json.template;

return users.map(user => ({
  json: {
    to: user.json.email,
    subject: template.subject.replace('{name}', user.json.name),
    body: template.body.replace('{name}', user.json.name)
  }
}));
```

#### 3.2 调度与定时任务（3小时）

**理论内容：**
- Cron表达式语法
- 定时任务配置
- 时区处理
- 任务监控和管理

**实操练习：**
- 配置定时任务
- 实现数据同步
- 监控任务执行状态

**练习案例：**
每日数据备份工作流：
```cron
# 每天凌晨2点执行
0 2 * * *
```

### 下午：性能优化与监控

#### 3.3 性能优化策略（3小时）

**理论内容：**
- 工作流优化技巧
- 内存使用优化
- 执行时间优化
- 并发处理策略

**实操练习：**
- 分析工作流性能
- 优化慢查询
- 实现并发处理

**练习案例：**
大数据处理优化：
1. 使用Split In Batches分批处理
2. 实现并行执行
3. 监控内存使用
4. 错误重试机制

#### 3.4 监控与日志（3小时）

**理论内容：**
- 执行日志分析
- 性能监控指标
- 错误追踪和调试
- 告警机制设置

**实操练习：**
- 配置日志记录
- 设置性能监控
- 实现错误告警

**练习案例：**
监控告警系统：
1. 监控工作流执行状态
2. 检测异常情况
3. 发送告警通知
4. 生成监控报告

---

## 第四天：实战项目开发

### 上午：电商自动化项目

#### 4.1 订单处理自动化（4小时）

**项目背景：**
电商平台需要自动化处理订单流程，包括订单确认、库存检查、发货通知等。

**功能需求：**
- 接收新订单通知
- 验证订单信息
- 检查库存状态
- 生成发货单
- 发送通知邮件
- 更新订单状态

**技术实现：**
```javascript
// 订单验证逻辑
const order = $input.first().json;
const validation = {
  isValid: true,
  errors: []
};

// 检查必填字段
if (!order.customer_email) {
  validation.isValid = false;
  validation.errors.push('Customer email is required');
}

// 检查商品库存
if (order.items.some(item => item.stock < item.quantity)) {
  validation.isValid = false;
  validation.errors.push('Insufficient stock');
}

return [{json: {order, validation}}];
```

**实操步骤：**
1. 设计工作流架构
2. 实现订单验证逻辑
3. 集成库存系统
4. 配置邮件通知
5. 测试完整流程

### 下午：客户关系管理项目

#### 4.2 CRM自动化系统（4小时）

**项目背景：**
需要自动化客户关系管理流程，包括客户数据同步、营销活动、客户跟进等。

**功能需求：**
- 客户数据同步
- 营销活动自动化
- 客户跟进提醒
- 数据分析和报告

**技术实现：**
```javascript
// 客户数据同步
const customers = $input.all();
const crmData = customers.map(customer => ({
  id: customer.json.id,
  name: customer.json.name,
  email: customer.json.email,
  phone: customer.json.phone,
  status: customer.json.status,
  last_contact: new Date().toISOString(),
  source: 'website_form'
}));

return [{json: {customers: crmData}}];
```

**实操步骤：**
1. 设计CRM数据模型
2. 实现数据同步逻辑
3. 配置营销自动化
4. 设置跟进提醒
5. 创建分析报告

---

## 第五天：部署与运维

### 上午：部署与配置

#### 5.1 生产环境部署（3小时）

**理论内容：**
- Docker部署最佳实践
- 环境变量配置
- 数据库配置
- 反向代理设置

**实操练习：**
- Docker Compose部署
- 环境变量管理
- Nginx反向代理配置

**部署配置示例：**
```yaml
# docker-compose.yml
version: '3.8'
services:
  n8n:
    image: n8nio/n8n
    ports:
      - "5678:5678"
    environment:
      - N8N_BASIC_AUTH_ACTIVE=true
      - N8N_BASIC_AUTH_USER=admin
      - N8N_BASIC_AUTH_PASSWORD=secure_password
      - DB_TYPE=postgresdb
      - DB_POSTGRESDB_HOST=postgres
      - DB_POSTGRESDB_DATABASE=n8n
      - DB_POSTGRESDB_USER=n8n
      - DB_POSTGRESDB_PASSWORD=n8n_password
    volumes:
      - n8n_data:/home/node/.n8n
    depends_on:
      - postgres

  postgres:
    image: postgres:13
    environment:
      - POSTGRES_DB=n8n
      - POSTGRES_USER=n8n
      - POSTGRES_PASSWORD=n8n_password
    volumes:
      - postgres_data:/var/lib/postgresql/data

volumes:
  n8n_data:
  postgres_data:
```

#### 5.2 安全配置（3小时）

**理论内容：**
- 身份认证配置
- 访问控制策略
- 数据加密
- 网络安全

**实操练习：**
- 配置OAuth认证
- 设置访问权限
- 实现数据加密

### 下午：运维与故障排除

#### 5.3 运维最佳实践（3小时）

**理论内容：**
- 备份策略
- 监控告警
- 日志管理
- 性能调优

**实操练习：**
- 配置自动备份
- 设置监控告警
- 日志分析

#### 5.4 故障排除与调试（3小时）

**理论内容：**
- 常见问题诊断
- 调试技巧
- 性能问题排查
- 错误恢复策略

**实操练习：**
- 模拟故障场景
- 使用调试工具
- 性能问题分析

---

## 培训评估与认证

### 评估方式
1. **理论考试**（30%）
   - n8n核心概念
   - 工作流设计原理
   - 最佳实践理解

2. **实操考核**（50%）
   - 独立完成项目
   - 工作流设计能力
   - 问题解决能力

3. **项目答辩**（20%）
   - 项目展示
   - 技术方案说明
   - 问题回答

### 认证标准
- **优秀**：90分以上，能够独立设计复杂工作流
- **良好**：80-89分，能够完成中等复杂度项目
- **合格**：70-79分，掌握基础功能和应用
- **不合格**：70分以下，需要重新学习

---

## 培训资源

### 推荐学习资料
1. **官方文档**：https://docs.n8n.io/
2. **社区论坛**：https://community.n8n.io/
3. **GitHub仓库**：https://github.com/n8n-io/n8n
4. **视频教程**：官方YouTube频道

### 练习环境
- n8n Cloud免费版
- 本地Docker环境
- 测试数据库
- 模拟API服务

### 工具推荐
- Postman：API测试
- ngrok：本地服务暴露
- Docker Desktop：容器管理
- VS Code：代码编辑

---

## 培训总结

通过本培训，学员将能够：
1. 深入理解n8n的核心概念和工作原理
2. 熟练使用n8n进行业务流程自动化
3. 掌握高级功能和优化技巧
4. 具备独立开发和部署能力
5. 了解生产环境运维最佳实践

培训结束后，建议学员：
- 持续关注n8n社区动态
- 参与开源项目贡献
- 在实际项目中应用所学知识
- 分享经验和最佳实践 