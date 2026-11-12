# dsh-private-pluginsmarket-index

私有插件仓 [dsh-private-pluginsmarket](https://github.com/mistake52/dsh-private-pluginsmarket) 的**公开市场索引**。

DeepSeek Harness 的自定义插件市场只读公开仓库，而插件源码仓需要保持私有——所以索引拆到本仓（公开），
源码留在私有仓。本仓只有两样东西，都由私有仓的 `scripts/build-market.mjs` 生成，**不要手改**：

| 文件 | 内容 |
|---|---|
| `index.json` | DSH 插件市场 format 1 索引：插件元数据 + 钉住的源码提交（40 位 commit） |
| `icons/` | 市场卡片图标（相对 `index.json` 的地址解析，必须与本文件同仓同目录） |

## 把索引源加进 DeepSeek Harness

**插件 → 更多（实验性插件）→ 自定义插件市场 → 发现 → 添加索引源**，填 raw 直链（市场拒绝重定向）：

```
https://raw.githubusercontent.com/mistake52/dsh-private-pluginsmarket-index/main/index.json
```

大陆网络 raw 超时时可换 jsDelivr 镜像：
`https://cdn.jsdelivr.net/gh/mistake52/dsh-private-pluginsmarket-index@<commit>/index.json`。

## 说明

- 插件源码**不在本仓**：索引里每个版本的 `source.url` 指向私有仓，安装规格是
  `git+<私有仓>.git#<commit>&path:/packages/<目录>`——没有该私有仓访问权的机器克隆会失败，属预期行为。
- 本仓公开的只有插件名 / 描述 / 分类 / 版本号与私有仓的提交号，不包含任何源码或私有内容。
- 版本更新流程（改包 → 提交 → `--publish` 钉索引 → 本仓提交推送）见私有仓的 `docs/publishing.md`。
