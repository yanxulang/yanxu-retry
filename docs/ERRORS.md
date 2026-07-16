# 错误目录

言韧自身错误格式为`YANREN_<代码>：消息`。`错误详情(所误)`返回稳定`代码`与无前缀`消息`，并保留`源代码`、`类别`、`位置`和`踪迹`。

## 策略与计划

| 代码 | 含义 |
| --- | --- |
| `YANREN_POLICY_ATTEMPTS` | 最大次数不是 1 至 4096 的安全整数 |
| `YANREN_POLICY_DELAY` | 初始或最大延迟越界，或最大值小于初始值 |
| `YANREN_POLICY_MULTIPLIER` | 倍率不在 1 至 1000 |
| `YANREN_POLICY_BUDGET` | 无抖动计划累计等待超过七天 |
| `YANREN_POLICY_JITTER` | 抖动比例不在 0 至 1 |
| `YANREN_POLICY_SEED` | 种子不是留有尝试编号余量的安全整数 |
| `YANREN_ATTEMPT` | 查询的失败次数不在有效等待位置 |
| `YANREN_PREDICATE_CODES` | 错误代码白名单为空或超过 64 项 |
| `YANREN_PREDICATE_CODE` | 白名单项不符合`YAN[A-Z0-9_]+`约定 |

## 执行

| 代码 | 含义 |
| --- | --- |
| `YANREN_STOPPED` | 停止判定在下一次尝试前返回真 |
| `YANREN_STOP_CALLBACK` | 停止判定抛错或返回类型不符 |
| `YANREN_OBSERVER` | 观察器执行失败 |
| `YANREN_PREDICATE` | 重试判定器执行失败 |
| `YANREN_WAITER` | 等待器执行失败 |
| `YANREN_WAIT_VALUE` | 传给等待器的延迟超出安全范围 |
| `YANREN_STATE` | 内部重试状态出现不可达异常 |

## 断路器与时间

| 代码 | 含义 |
| --- | --- |
| `YANREN_BREAKER_THRESHOLD` | 失败阈值不在 1 至 4096 |
| `YANREN_BREAKER_COOLDOWN` | 恢复毫秒不是 0 至七天的安全整数 |
| `YANREN_OPEN` | 断路器仍开启或半开探针已占用 |
| `YANREN_CLOCK` | 自定义时间源执行失败 |
| `YANREN_CLOCK_VALUE` | 时间源未返回非负安全整数毫秒 |
| `YANREN_CLOCK_REVERSED` | 时间源相对上次读取倒退 |
| `YANREN_CLOCK_STATE` | 在非关闭状态更换时间源 |
| `YANREN_COUNTER_LIMIT` | 断路器累计计数超过安全整数范围 |

## 业务错误

直接执行入口在放弃或耗尽时原样抛出业务错误，不包裹成`YANREN_`。结构化尝试入口用`错误详情`表示它：符合`YAN[A-Z0-9_]+：`约定的代码会被保留，其余归为`YANREN_RUNTIME`。

回调错误会被包裹成上表的库错误，原回调消息出现在新消息中。不要按完整消息编程；机器判断只使用稳定代码。
