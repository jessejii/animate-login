# Animate Login

一个基于 `Vue 3 + Vite + TypeScript + Element Plus + Tailwind CSS` 的动画登录页示例。

## 项目亮点

- 动态角色联动：角色会跟随鼠标、输入状态与密码可见状态变化
- 细节动画：眨眼、入场、窥视等微交互
- 响应式布局：桌面双栏 + 移动端单栏
- 简洁工程结构：组件拆分清晰，便于二次开发

## 技术栈

- `Vue 3`
- `Vite`
- `TypeScript`
- `Vue Router`
- `Element Plus`
- `Tailwind CSS`

## 快速开始

```bash
npm install
npm run dev
```

访问：`http://localhost:5173`

## 可用脚本

```bash
npm run dev         # 启动开发环境
npm run build       # 类型检查并打包
npm run preview     # 预览打包结果
npm run type-check  # 仅类型检查
```

## 登录演示账号

- Email: `erik@gmail.com`
- Password: `1234`

## 目录结构

```text
src/
  components/
    AnimatedCharacters.vue
    AnimatedCharactersLoginPage.vue
    EyeBall.vue
    Pupil.vue
  router/
    index.ts
  views/
    HomeView.vue
  assets/
    main.css
  App.vue
  main.ts
```

## 最近优化内容

- 修复角色动画中的定时器清理逻辑，避免页面切换后潜在的计时器泄漏
- 改进登录提交流程（空值校验、按钮禁用、成功提示）
- 清理无用导入与项目元信息（页面标题、包名）
- 补充 `vite` 类型声明，解决样式导入类型报错

## 说明

当前为前端演示项目，登录逻辑使用本地模拟，不包含真实后端鉴权。
