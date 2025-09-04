# OpenWrt Forks Build Bot

这是一个用于自动构建各种OpenWrt分支版本的项目。

## 下载构建产物

可以从以下链接下载构建好的固件：https://sourceforge.net/projects/openwrt-forks-build/files/

## 使用方法

### 默认构建

项目会自动构建默认的配置（Lean的x86/64版本）。当代码推送到main分支时会自动触发构建。

### 自定义Matrix构建

你可以通过GitHub Actions的手动触发功能来使用自定义的matrix配置：

1. 进入GitHub仓库的Actions页面
2. 选择"Build"工作流
3. 点击"Run workflow"
4. 选择构建类型：
   - **default**: 使用默认配置
   - **custom**: 使用自定义matrix配置

#### 自定义Matrix格式

当选择"custom"构建类型时，需要在"Custom matrix configuration"字段中输入JSON格式的配置。

**配置格式示例：**

```json
{
  "config": [
    {
      "fork-name": "Lean",
      "branch": "master",
      "target": "x86",
      "subtarget": "64",
      "repo": "https://github.com/coolsnowwolf/lede"
    },
    {
      "fork-name": "Lean",
      "branch": "master",
      "target": "rockchip",
      "subtarget": "armv8",
      "repo": "https://github.com/coolsnowwolf/lede"
    }
  ]
}
```

**字段说明：**

- `fork-name`: 分支名称标识
- `branch`: Git分支名
- `target`: OpenWrt目标平台
- `subtarget`: OpenWrt子目标平台
- `repo`: GitHub仓库URL

#### 支持的OpenWrt分支

**Lean分支 (lede):**
- 仓库: `https://github.com/coolsnowwolf/lede`
- 分支: `master`

**hanwckf分支 (immortalwrt-mt798x):**
- 仓库: `https://github.com/hanwckf/immortalwrt-mt798x`
- 分支: `openwrt-21.02`

**Lienol分支:**
- 仓库: `https://github.com/Lienol/openwrt`
- 分支: `24.10`

#### 常用目标平台

- `x86/64` - x86 64位平台
- `x86/generic` - x86通用平台
- `rockchip/armv8` - 瑞芯微ARM64平台
- `ramips/mt7621` - 联发科MT7621平台
- `mediatek/filogic` - 联发科Filogic平台
- `mediatek/mt7981` - 联发科MT7981平台
- `mediatek/mt7986` - 联发科MT7986平台
- `bcm27xx/bcm2711` - 树莓派4B平台
- `qualcommax/ipq807x` - 高通IPQ807x平台

#### 完整配置示例

```json
{
  "config": [
    {
      "fork-name": "Lean",
      "branch": "master",
      "target": "x86",
      "subtarget": "64",
      "repo": "https://github.com/coolsnowwolf/lede"
    },
    {
      "fork-name": "Lean",
      "branch": "master",
      "target": "rockchip",
      "subtarget": "armv8",
      "repo": "https://github.com/coolsnowwolf/lede"
    },
    {
      "fork-name": "hanwckf",
      "branch": "openwrt-21.02",
      "target": "mediatek",
      "subtarget": "mt7981",
      "repo": "https://github.com/hanwckf/immortalwrt-mt798x"
    },
    {
      "fork-name": "Lienol",
      "branch": "24.10",
      "target": "x86",
      "subtarget": "64",
      "repo": "https://github.com/Lienol/openwrt"
    }
  ]
}
```

## 注意事项

1. JSON配置必须格式正确，否则构建会失败
2. 每个配置项必须包含所有必需字段
3. 仓库URL必须是有效的GitHub地址
4. 构建时间较长，请耐心等待
5. 构建产物会自动上传到SourceForge

## 功能特性

- 支持多个OpenWrt分支同时构建
- 自动应用补丁
- CCACHE加速编译
- GPG签名验证
- 自动上传到SourceForge
- 支持自定义matrix配置，避免构建不需要的版本