AI助手请查阅 working-notes 文件夹中的文件，以获取背景信息。

# Julia Canvas

基于Julia+React Flow的画布式编程环境，支持变量、表达式、公式对象的可视化、交互式编辑与复合。

## 🚀 快速开始

### 方式一：使用启动脚本（推荐）

#### 完整版脚本（推荐）
```powershell
# 启动前后端服务
.\start-services.ps1

# 仅启动后端
.\start-services.ps1 -BackendOnly

# 仅启动前端  
.\start-services.ps1 -FrontendOnly

# 查看帮助
.\start-services.ps1 -Help
```

#### 简化版脚本
```powershell
# 快速启动（在新窗口中运行）
.\start.ps1
```

### 方式二：手动启动

#### 启动后端（Julia API服务器）
```powershell
cd julia-backend
julia --project=. start_server.jl
```

#### 启动前端（React开发服务器）
```powershell
cd example-react-flow
pnpm dev
```

## 📡 服务地址

- **后端API**: http://127.0.0.1:8081
- **前端界面**: http://127.0.0.1:5173

## 🛠️ 技术栈

### 后端
- **Julia**: 代码执行引擎
- **HTTP.jl**: REST API服务器
- **JSON3.jl**: JSON处理

### 前端
- **React + TypeScript**: 前端框架
- **React Flow**: 画布和节点系统
- **Vite**: 构建工具
- **TailwindCSS**: 样式框架
- **Zustand**: 状态管理

## 🎯 核心功能

### ✅ 已实现
- [x] Julia代码节点编辑和执行
- [x] 变量控件系统（@input/@output标记）
  - [x] 滑动条控件 (`@slider`)
  - [x] 文本输入控件 (`@string`)
  - [x] 布尔开关控件 (`@boolean`)
- [x] 实时代码执行和结果显示
- [x] 节点间连接和数据流
- [x] 多模式工具栏（选择/文本/连接模式）
- [x] 键盘快捷键支持（WASD移动，V/T/C模式切换）
- [x] 画布状态持久化（自动保存/恢复）
- [x] 导入/导出功能
- [x] 错误处理和用户反馈

### 🚧 开发中- [ ] Julia语法高亮- [ ] 节点间依赖关系可视化- [ ] Desmos预览和导出- [ ] 更多变量控件类型- [ ] 性能优化（大规模画布支持）- [ ] 用户引导和帮助功能

## 💡 使用示例

创建一个简单的计算节点：

```julia
@input x @slider(0, 100, 1, 50)
@input y @slider(0, 100, 1, 30)

const sum = x + y
const product = x * y
const average = sum / 2

@output sum
@output product
@output average
```

这将创建：
- 两个滑动条控件（x和y）
- 自动计算总和、乘积和平均值
- 显示三个输出结果
- 滑动条改变时实时更新计算结果

## 🔧 开发环境要求

### 必需
- **Julia** (≥1.8)
- **Node.js** (≥18)
- **pnpm** (≥8)

### 安装Julia依赖
```powershell
cd julia-backend
julia --project=. -e "using Pkg; Pkg.instantiate()"
```

### 安装前端依赖
```powershell
cd example-react-flow
pnpm install
```

## 📖 API文档

### 后端API

#### 健康检查
```
GET /api/health
```

#### 解析代码结构
```
POST /api/parse
Content-Type: application/json

{
  "code": "Julia代码字符串"
}
```

#### 执行代码
```
POST /api/evaluate
Content-Type: application/json

{
  "code": "Julia代码字符串",
  "input_values": {
    "变量名": "变量值"
  }
}
```

## 🐛 故障排除

### 后端启动失败
1. 确认Julia已安装：`julia --version`
2. 检查项目依赖：`julia --project=. -e "using Pkg; Pkg.status()"`
3. 重新安装依赖：`julia --project=. -e "using Pkg; Pkg.instantiate()"`

### 前端启动失败
1. 确认Node.js和pnpm已安装：`node --version`, `pnpm --version`
2. 清理并重新安装依赖：`pnpm clean-install`
3. 检查端口占用：`netstat -ano | findstr :5173`

### 连接问题
1. 确认后端服务正常：访问 http://127.0.0.1:8081/api/health
2. 检查防火墙设置
3. 确认CORS配置正确

## 📄 许可证

本项目采用 MIT 许可证。

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

## 📞 联系方式

有问题或建议请创建 Issue。