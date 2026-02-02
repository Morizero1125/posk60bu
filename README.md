# PixelOS for Redmi K60 (mondrian) - GitHub Actions 自动编译

使用 GitHub Actions 云编译 PixelOS ROM for Redmi K60 (mondrian)

## 功能特性

- 完全自动化的云编译流程
- 支持 PixelOS / LineageOS / AOSP
- 自动同步源码和设备树
- ccache 加速编译
- 自动上传编译产物
- 定时自动编译（每周日）

## 使用方法

### 手动触发编译

1. 进入 GitHub 仓库的 Actions 标签页
2. 选择 Build PixelOS for Redmi K60 (mondrian) 工作流
3. 点击 Run workflow
4. 选择设备代号（默认：mondrian）
5. 选择 ROM 类型（默认：pixelos）
6. 点击 Run workflow 开始编译

### 自动编译

- 每周日 UTC 0:00 自动触发编译
- 推送到 main 或 master 分支时自动触发

## 编译产物

编译完成后，产物会自动上传到 Actions Artifacts：

- ROM 包: pixelos-mondrian-{run_number}.zip
- 镜像文件: boot.img, vendor_boot.img, dtbo.img 等
- 编译日志: build-logs-{run_number}.zip

产物保留 30 天，编译日志保留 7 天。

## 工作流配置

### 环境变量

```yaml
DEVICE: mondrian              # 设备代号
ROM_TYPE: pixelos             # ROM 类型
CCACHE_SIZE: 50G              # ccache 缓存大小
```

### 支持的 ROM 类型

- pixelos: PixelOS (默认)
- lineageos: LineageOS
- aosp: AOSP

## 设备源码仓库

编译会自动克隆以下设备源码：

- LineageOS/android_device_xiaomi_mondrian - 设备树
- LineageOS/android_device_xiaomi_sm8475-common - 通用设备代码
- LineageOS/android_vendor_xiaomi_mondrian - Vendor
- LineageOS/android_kernel_xiaomi_sm8450 - 内核
- LineageOS/android_kernel_xiaomi_sm8450-modules - 内核模块
- LineageOS/android_kernel_xiaomi_sm8450-devicetrees - 设备树
- LineageOS/android_device_xiaomi_sepolicy - Sepolicy

## 编译时间

- 首次编译: 约 3-5 小时（需要下载完整源码）
- 增量编译: 约 1-2 小时（使用 ccache）

## 注意事项

### GitHub Actions 限制

- 免费账户每月 2000 分钟编译时间
- 每次编译约 360 分钟（6 小时）
- 建议使用缓存和 ccache 减少编译时间

### 存储空间

- 工作流会自动清理不必要的文件
- 编译产物会自动上传到 Artifacts

### 编译失败

- 查看 Actions 日志中的错误信息
- 下载 build-logs-{run_number}.zip 查看详细日志
- 检查设备源码仓库是否更新
- 确认 PixelOS 源码是否正常

## 故障排除

### 编译失败

1. 检查 Actions 日志中的错误信息
2. 下载 build-logs-{run_number}.zip 查看详细日志
3. 确认设备源码仓库是否需要更新

### 源码同步失败

1. 检查网络连接
2. 确认 PixelOS 官方仓库是否可访问
3. 尝试重新运行工作流

### 设备源码克隆失败

1. 确认设备源码仓库 URL 正确
2. 检查仓库是否为公开仓库
3. 确认设备代号是否正确

## 许可证

本工作流配置文件遵循 MIT 许可证。

## 致谢

- PixelOS - PixelOS ROM
- LineageOS - 设备源码
- GitHub Actions - CI/CD 平台

## 联系方式

如有问题，请提交 Issue 或 Pull Request。