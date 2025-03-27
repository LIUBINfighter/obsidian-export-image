# Obsidian ExportImagePlugin 分析报告

## 插件结构分析

### 核心类
```typescript
export default class ExportImagePlugin extends Plugin {
  settings: ISettings;
  
  async epxortFile(file: TFile) { /*...*/ }
  async onload() { /*...*/ }
  onunload() { /*...*/ }
  async loadSettings() { /*...*/ }
  async saveSettings() { /*...*/ }
}
```

### 主要功能模块
1. **上下文菜单集成**
   - 文件右键菜单：导出Markdown文件或文件夹
   - 编辑器右键菜单：导出选中文本或整个文件

2. **命令集成**
   - `export-image`: 导出当前活动文件
   - `export-image-selection`: 导出选中文本

3. **设置面板**
   - `ImageSettingTab`类管理配置界面

### 依赖组件
- `L`: 本地化模块
- `utils`: 工具函数
- `components/file/exportImage`: 文件导出逻辑
- `components/folder/exportFolder`: 文件夹导出逻辑
- `SettingRenderer`: 设置面板渲染器

## 侧边栏图片预览设计方案

### 实现步骤
1. 创建`ImagePreviewView`类继承`ItemView`
2. 注册到Obsidian侧边栏
3. 实现实时预览机制：
   - 监听编辑器变化
   - 解析图片内容
   - 渲染Markdown预览

### 示例代码结构
```typescript
class ImagePreviewView extends ItemView {
  async onOpen() {
    // 初始化预览容器
  }

  async onClose() {
    // 清理资源
  }

  async updatePreview(content: string) {
    // 渲染Markdown为预览
  }
}
```

### 性能优化建议
1. 使用防抖处理频繁更新
2. 缓存已解析的图片
3. 支持配置预览刷新频率

## 后续开发建议
1. 增强预览交互功能
2. 支持多图片预览切换
3. 添加预览样式自定义选项
