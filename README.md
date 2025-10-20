# Tomatomall

南京大学《软件工程与计算II》期末项目

TomatoMall 是一个全栈电子商务平台，后端采用 Spring Boot (Java) 开发，前端采用 Vue 3 (TypeScript) 开发。系统提供完整在线购物体验，包括商品浏览、购物车管理、订单处理和支付集成。

## 项目架构

### 后端 (Spring Boot)
- **框架**: Spring Boot 3.x
- **语言**: Java 17+
- **数据库**: MySQL
- **端口**: 8080
- **主应用类**: `TomatoMallApplication.java`

后端遵循标准的 MVC 架构，包含：
- **控制器**: 处理 HTTP 请求 (如 `AccountController`、`ProductController`、`OrderController`)
- **服务层**: 业务逻辑实现
- **仓库层**: 使用 Spring Data JPA 的数据访问层
- **实体类/POJO**: 数据库模型 (如 `Account`、`Product`、`Order`、`Cart`)
- **DTO/VO**: 用于 API 通信的数据传输对象和视图对象

### 前端 (Vue 3)
- **框架**: Vue 3
- **构建工具**: Vite
- **UI 库**: Element Plus
- **语言**: TypeScript
- **包管理器**: npm/yarn

位于 `tomatomall-frontend` 目录中，前端使用现代 Vue 组合式 API，遵循组件化架构。

## 核心功能

1. **用户管理**
   - 用户注册和身份验证
   - 基于角色的访问控制 (RoleEnum)
   - 分级会员 VIP 系统 (VIPEnum)

2. **商品管理**
   - 带有分类和规格的商品目录
   - 商品状态跟踪 (ProductStatusEnum)
   - 通过阿里云 OSS 进行图片上传和管理

3. **购物车与订单**
   - 添加/删除购物车商品
   - 订单创建和状态跟踪 (OrderStatusEnum)
   - 库存管理和库存控制

4. **支付集成**
   - 支付宝支付网关集成
   - 使用 RSA2 签名的安全支付处理
   - 异步通知处理

5. **AI 功能**
   - 集成 OpenAI 实现 AI 驱动的功能
   - 配置使用 DeepSeek-V3 模型
   - JSON 响应格式用于结构化数据

6. **评价与评分**
   - 带点赞功能的商品评价系统
   - 嵌套评论 (ChildReview)
   - 评价审核

7. **优惠券系统**
   - 带状态跟踪的优惠券管理 (CouponStatusEnum)
   - 用户专属优惠券
   - 过期规则

8. **广告管理**
   - 广告创建和展示
   - 状态控制的可见性

## 项目结构

```
tomatomall/
├── src/main/java/com/example/tomatomall/
│   ├── controller/          # REST API 控制器
│   ├── service/             # 业务逻辑服务
│   ├── repository/          # 数据访问仓库
│   ├── po/                  # 持久化对象 (实体)
│   ├── dto/                 # 数据传输对象
│   ├── vo/                  # 值对象 (视图模型)
│   ├── enums/               # 枚举类
│   ├── util/                # 工具类
│   └── configure/           # 配置类
├── src/main/resources/
│   ├── application.yml      # 主要配置
│   └── service-account-key/ # Firebase 服务账户密钥
└── pom.xml                 # Maven 配置

tomatomall-frontend/
├── src/
│   ├── api/                 # API 服务调用
│   ├── components/          # Vue 组件
│   ├── router/              # 路由配置
│   ├── store/               # 状态管理 (如果使用 Pinia/Vuex)
│   ├── types/               # TypeScript 类型定义
│   ├── utils/               # 工具函数
│   └── views/               # 页面组件
├── public/                  # 静态资源
├── vite.config.ts           # Vite 配置
└── package.json             # 前端依赖
```

## 安装说明

### 先决条件
- Java 17+
- MySQL 8.0+
- Node.js 18+
- npm 或 yarn
- 阿里云 OSS 账户 (用于图片存储)
- 支付宝开发者账户 (用于支付处理)

### 后端安装
1. 安装 MySQL 并创建名为 `TomatoMall` 的数据库
2. 如有必要，在 `application.yml` 中更新数据库凭据
3. 使用 Maven 构建项目：`mvn clean install`
4. 运行应用程序：`mvn spring-boot:run` 或执行 `TomatoMallApplication.java`
5. 后端将在 `http://localhost:8080` 可用

### 前端安装
1. 进入 `tomatomall-frontend` 目录
2. 安装依赖：`npm install`
3. 启动开发服务器：`npm run dev`
4. 前端将在 `http://localhost:3050` 可用 (与支付宝返回 URL 一致)

## 运行应用

设置好后端和前端后：
1. 启动 Spring Boot 后端
2. 启动 Vue 前端开发服务器
3. 在 `http://localhost:3050` 访问应用

## 安全考虑

**重要提示**: 当前配置包含硬编码凭据：
- 数据库密码：`123456`
- 支付宝私钥和公钥
- 阿里云 OSS 访问密钥

在生产环境中，这些凭据应移至环境变量或安全的配置管理系统中。

应用使用基于 JWT 的身份验证，并配有令牌生成和验证工具 (`TokenUtil.java`)。用户密码在存储前应进行适当哈希处理。

## 支付集成

系统集成了支付宝沙箱用于测试支付。配置指向支付宝沙箱网关。生产环境需将 `server-url` 更新为生产端点并使用生产凭据。

## AI 集成

应用配置通过兼容 OpenAI 的 API 使用 AI 服务，当前指向 DeepSeek 的 V3 模型。AI 功能预计返回 JSON 格式的响应以进行结构化数据处理。

## 附加文档

项目包含以下附加文档：
- `项目启动文档.pdf` - 项目启动文档
- `用例文档.pdf` - 用例文档
- `体系结构设计文档.pdf` - 架构设计文档
- `人机交互设计文档.pdf` - 人机交互设计文档

这些文档提供了关于系统需求、设计和用户界面的详细信息。
