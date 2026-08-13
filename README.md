<p align="center">
  <img src="docs/pics/modi.png" alt="MODI" width="300">
</p>

<h1 align="center">MODI DESCRIPTION</h1>

<p align="center">
  MODI 机器人机型描述包（URDF / meshes）
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Release-v0.0.1-2f80ed" alt="Release v0.0.1">
  <img src="https://img.shields.io/badge/ROS%202-Humble-22314e?logo=ros" alt="ROS 2 Humble">
  <img src="https://img.shields.io/badge/Format-URDF-6c63ff" alt="URDF">
  <img src="https://img.shields.io/badge/Meshes-STL-26a69a" alt="STL meshes">
</p>

<p align="center">
  <a href="https://github.com/modi-robot/modi_description/releases"><strong>下载模型包</strong></a>
  ·
  <a href="#模型与坐标系"><strong>模型与坐标系</strong></a>
  ·
  <a href="#快速开始"><strong>快速开始</strong></a>
</p>

---

`modi_description` 提供 MODI 各机型的机器人描述资源：URDF、网格、配置与可视化相关文件。
可用于仿真、可视化、运动学/控制栈接入，以及与 `modi_system` / SDK 配套的机型模型分发。

## 主要功能

| 功能 | 说明 |
|---|---|
| 多机型 URDF | 提供左臂、右臂、双臂等机型描述 |
| 网格资源 | 附带 STL mesh，可直接用于 RViz / Gazebo 等 |
| 坐标系约定 | 发布页展示各机型连杆与关节坐标系分布 |
| 独立分发包 | 按机型打包，解压即可作为独立包名使用 |

## 模型与坐标系

以下图片展示当前公开机型的模型外形与关节/连杆坐标系分布（RGB 轴为局部坐标系，
绿色圆弧箭头示意转动关节方向）。

### `modi_dm3_l`

<p align="center">
  <img src="docs/pics/left.png" alt="modi_dm3_l model and frames" width="420">
</p>

### `modi_dm3_r`

<p align="center">
  <img src="docs/pics/right.png" alt="modi_dm3_r model and frames" width="360">
</p>

### `modi_dm3_dual`

<p align="center">
  <img src="docs/pics/dual.png" alt="modi_dm3_dual model and frames" width="560">
</p>

## 支持的机型包

当前 GitHub Releases 上传以下机型包：

| 机型 | 说明 |
|---|---|
| `modi_dm3_l` | DM3 左臂 |
| `modi_dm3_r` | DM3 右臂 |
| `modi_dm3_dual` | DM3 双臂加底座 |

## 下载模型包

前往 **[GitHub Releases](https://github.com/modi-robot/modi_description/releases)** 下载所需机型压缩包。

文件名格式：

```text
<机型>_<版本>_<Git短提交>.zip
```

例如：

```text
modi_dm3_l_0.0.1_a1b2c3d.zip
modi_dm3_r_0.0.1_a1b2c3d.zip
modi_dm3_dual_0.0.1_a1b2c3d.zip
```

## 快速开始

### 1. 解压发布包

```bash
unzip modi_dm3_l_*.zip
ls modi_dm3_l/
```

解压后第一层目录为机型名（不是 `modi_description/`）：

```text
modi_dm3_l/
├── urdf/
├── meshes/
└── ...
```

发布包内 URDF 已使用：

```text
package://modi_dm3_l/meshes/...
```

### 2. 作为独立 ROS 2 描述使用

将解压出的机型目录放入某个 ament 包的 `share/<机型>/`（或自建同名包并安装该目录），
保证 `package://<机型>/...` 可被资源解析，然后加载 URDF：

```bash
# 示例：用 check_urdf 校验
check_urdf modi_dm3_l/urdf/modi_dm3_l.urdf
```

在 Launch 中可按机型包名查找资源，例如：

```python
FindPackageShare('modi_dm3_l')
```

## 发布包结构

```text
<机型>_<版本>_<Git短提交>.zip
└── <机型>/
    ├── urdf/                 # 机型 URDF
    ├── meshes/               # STL 等网格
    └── ...
```
发布包不含 `config/`（仍留在源码仓，供开发使用）。

同版本多机型可并存于同一 Release；附件按机型分别下载。

## 问题反馈

使用中发现问题请在 [Issues](https://github.com/modi-robot/modi_description/issues) 提交，并尽量提供：

- 压缩包完整文件名与版本
- 机型名称（如 `modi_dm3_l`）
- 使用场景（RViz / Gazebo / 自研加载器等）
- 可复现步骤与完整报错
