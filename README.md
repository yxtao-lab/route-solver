# Route Solver

**Route Solver**（`yxtao-lab/route-solver`）是面向行程 / 路径优化场景的独立产品仓库，由 [yxtao-lab](https://github.com/yxtao-lab) 维护，服务于兜行（Douxing）及可复用的求解能力封装。

> 本仓库**不是** Google 官方产品。内核基于 [Google OR-Tools](https://github.com/google/or-tools) 的一次冻结快照二次开发，默认**不自动同步**上游，以免影响产品稳定性与自主演进。

## 与 OR-Tools 的关系

| 项 | 说明 |
|----|------|
| 许可 | [Apache License 2.0](./LICENSE) |
| 归属声明 | 见 [NOTICE](./NOTICE) |
| 变更记录 | 见 [CHANGELOG.md](./CHANGELOG.md) |
| 快照版本 | OR-Tools **9.15**（`Version.txt`） |
| 快照提交 | `98c165a`（fork 时的 `stable`） |

默认策略：

- 日常开发只推送到 **本仓库**（`origin` = `yxtao-lab/route-solver`）
- **不**将 `google/or-tools` 设为自动跟踪上游
- 若需吸收官方修复：手动 `fetch` + `cherry-pick`，并写入 `CHANGELOG.md`

## 目标能力（产品方向）

- 旅行商 / 开环路径 / 带时间窗等行程顺序优化
- 车辆路径（VRP）及约束扩展（按产品节奏迭代）
- 对外稳定 API / SDK（在本仓后续 `bindings/` 或独立服务中提供），供兜行及其它项目复用

当前仍保留 OR-Tools 原有工程结构（CMake / Bazel、`ortools/` 源码树等），便于在既有求解器上做定向修改。

## 构建与文档

构建方式与官方 OR-Tools 基本一致，请参考：

- [OR-Tools 官方文档](https://developers.google.com/optimization)
- 本仓原有 `CMakeLists.txt` / `Makefile` / Bazel 配置

Python / Java / .NET 等语言绑定的安装说明，在未提供「Route Solver」独立发行包前，可暂按官方 OR-Tools 文档操作；产品化发版后以本仓 README / Release 为准。

## 在兜行 monorepo 中的使用

兜行通过 git submodule 引用本仓：

```text
packages/or-tools/upstream  →  https://github.com/yxtao-lab/route-solver.git
```

初始化：

```bash
git submodule update --init --depth 1 packages/or-tools/upstream
```

## 贡献与分支

| 分支 | 用途 |
|------|------|
| `stable` | 产品通用基线（与 fork 时上游一致；发版可用 tag，如 `v0.1.0`） |
| **`douxing`** | **专供兜行（Douxing）系统的定制分支**；兜行 monorepo submodule 跟踪此分支 |

- 兜行相关改动请提交到 `douxing`（或从 `douxing` 拉 `feat/...` 再合回）
- 与兜行无关、可复用的通用能力可合入 `stable`，再按需 cherry-pick / merge 到 `douxing`
- Issue / PR：请开在本仓库，勿向 `google/or-tools` 提交兜行业务相关改动

## License

Apache License 2.0. 详见 [LICENSE](./LICENSE) 与 [NOTICE](./NOTICE)。
