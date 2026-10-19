# ToAPIs · 更低成本的 baibot 图片方案

同一个提示词，三个图片模型，保留原图、调用代码、参数和价格。

[English](README.md) · [对应模型与价格](https://go2v.toapis.com/1019_bai_g) · [原项目](https://github.com/etkecc/baibot)

ToAPIs 独立维护的社区教程。当前验证边界：Existing OpenAI-compatible image provider via loopback bridge; Matrix delivery/encryption pending。这不是上游官方发行版或完整UI验收。

## 演示

![三个模型的案例与价格](social/image-comparison-cn.png)

## 价表与案例费用

实测日期：2026-10-19，按本例展示金额从低到高排序。图片“报价”来自同一生成Key的精确档位查询；未收到单任务结算回执时不称为已确认实扣。视频金额来自API已结算回执。

| 模型／本次档位 | 类型 | 本例金额／报价 | 对应模型价格 | 费用依据 |
|---|---|---:|---|---|
| gpt-image-2(VIP)<br>low / 1K | 图片 | 报价 $0.0019 | $0.0019/image | 当期精确档位报价；单任务未返回结算，同模型批次日志另有记录 |
| gpt-image-2<br>1K | 图片 | 报价 $0.015 | $0.015/image | 当期精确档位报价；单任务未返回结算，同模型批次日志另有记录 |
| gpt-image-2.5-flare<br>high / 1K | 图片 | 报价 $0.0225 | $0.0225/image | 当期精确档位报价；单任务未返回结算，同模型批次日志另有记录 |

**gpt-image-2(VIP)，$0.0019/image 起；本例 low/1K 就是 $0.0019/image。** 代码保留真实ID `gpt-image-2-vip`。Seedance按总token计费，美元/秒是具体案例折算，非固定秒价。

## 复用

复制 `.env.example` 为私有 `.env`，设置生成Key和独立的本地桥接令牌。先查价，再明确添加 `--live` 提交。

```bash
python run_case.py --job jobs/gpt-image-2-vip.json
python run_case.py --job jobs/gpt-image-2-vip.json --live
python bridge.py
```

[各项目配置和验收边界](integration/README.md) · [参数输入](jobs/) · [脱敏案例证据](evidence/) · [验收清单](ACCEPTANCE.md)

提交前保存任务；查询失败仅继续GET同一任务，提交响应丢失不自动重提。不要仅因支持自定义Key/Base URL就判定图片或视频即插即用。

固定上游版本：[5a9037cbac5d](https://github.com/etkecc/baibot/commit/5a9037cbac5d03ae4f5b1b55601cd40a44f6c09c)。图片和视频原始素材生成成功，不代表已完成上游产品全流程。

## 原创提示词

```text
Square friendly flat illustration for a private community chat: a small orange robot tending three green plants on a balcony above a bright seaside town, clear simple shapes, warm coral and cream palette, approachable original editorial artwork, no brand, no letters, no text, no watermark.
```

