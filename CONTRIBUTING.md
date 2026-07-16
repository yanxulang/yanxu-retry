# 贡献指南

## 环境

- 最低言序 1.1.6；
- 当前稳定言序 1.1.8；
- Git；
- 无第三方包依赖。

## 本地门禁

从仓库根目录执行：

```sh
yanxu 格 --写 src/言韧.yx
find tests examples benchmarks -type f -name '*.yx' -exec yanxu 格 --写 {} \;
yanxu 查 src/言韧.yx
yanxu 试 tests --json
yanxu 兼容 tests --json
yanxu 兼容 examples --json
yanxu 兼容 benchmarks --json
yanxu 包 锁 .
yanxu 包 锁 --离线 .
yanxu 编 . -o yanxu-retry.yxb --release
yanxu 包 锁 integration/消费者
yanxu 包 运行 integration/消费者
yanxu 编 integration/消费者 -o yanxu-retry-consumer.yxb --release
```

所有文卷还须分别通过`yanxu 查`；生成 API 必须与`docs/API.md`逐字一致。提交前运行`git diff --check`。

## 变更要求

- 修复须带能先复现问题的规格；
- 新公共 API 须更新指南、错误目录、迁移说明或可观察性契约中的相关部分；
- 新事件字段必须保持事件模式向后兼容，破坏性变化只能进入新的模式版本；
- 新资源配置必须有有限硬上限和上下界规格；
- 时间、随机和等待相关测试必须可确定，不依赖真实睡眠；
- 业务操作错误须原样传播，库回调错误须使用独立稳定代码；
- 性能改动须更新确定性负载文卷，不能用机器相关耗时作正确性断言。

## 发布检查

稳定发布需要最低与当前工具链、Linux/macOS/Windows、树解释器/VM、锁图、Release YXB、生成 API、版本一致性和干净工作树全部通过。标签使用`v<语义版本>`并指向普通合并提交。
