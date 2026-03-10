# libmpv 编译优化说明

## 字幕性能优化

### 1. libass 优化
- **启用 ASM 优化**: 从 `--disable-asm` 改为 `--enable-asm`
- **编译优化级别**: 添加 `-O3` 优化标志
- **影响**: 显著提升字幕渲染性能，减少卡顿

### 2. HarfBuzz 优化
- **构建类型**: 设置为 `release`
- **优化级别**: 设置为 `3` (最高优化)
- **影响**: 提升文本整形和字体渲染性能

### 3. FreeType 优化
- **构建类型**: 设置为 `release`
- **优化级别**: 设置为 `3` (最高优化)
- **影响**: 提升字体光栅化性能

### 4. FFmpeg 字幕支持
- **添加字幕过滤器**: `subtitles`, `ass`
- **PGS 字幕支持**: 添加 `pgssub` 解码器（蓝光字幕）
- **ARM NEON 优化**: 添加 `-mfloat-abi=softfp` 提升浮点运算性能

### 5. MPV 配置
- **启用 Lua**: 从 `disabled` 改为 `enabled`
- **影响**: 支持高级字幕脚本和自定义渲染

## 支持的字幕格式

### 文本字幕
- SRT (SubRip)
- ASS/SSA (Advanced SubStation Alpha)
- WebVTT
- SubViewer
- VPlayer
- STL
- MovText

### 图像字幕
- DVD 字幕 (dvdsub)
- 蓝光 PGS 字幕 (pgssub)
- DVB 字幕 (dvbsub)

## 性能提升预期

- **字幕渲染**: 30-50% 性能提升
- **复杂 ASS 特效**: 显著减少卡顿
- **多字幕轨道**: 更流畅的切换体验
- **高分辨率字幕**: 更好的渲染性能

## 编译说明

项目通过 GitHub Actions 自动编译，推送到 main 分支后会自动触发编译流程。

编译产物会生成 JAR 文件，包含所有架构的 libmpv.so：
- arm64-v8a
- armeabi-v7a
- x86
- x86_64
