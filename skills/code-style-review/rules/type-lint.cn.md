---
paths:
  - "*.ts"
---

# Type Lint Rules

在审查代码或编写新功能时，严格执行 TypeScript 类型检查规范，确保代码的类型安全、健壮性与可维护性。

**类型安全第一**：确保所有的变量、函数参数、组件 Props 和返回值都有明确或可推导的类型。
**类型简洁**：类型声明不应该过度嵌套，对于过深嵌套可以适当使用 any 进行优化
**类型定义准确**：类型声明明确具体，属性定义完整。
**利用类型推导**：充分利用 TS 的自动类型推导能力，避免画蛇添足的显式声明（例如：`let count: number = 0` 应直接写为 `let count = 0`）。

## 约束

**1. `interface` 与 `type` 的选择：**
- 优先使用 `interface` 来声明对象、API 响应和类的结构，便于扩展和利用声明合并（Declaration Merging）特性。
- 使用 `type` 来声明基本类型别名、联合类型（Union）、交叉类型（Intersection）以及复杂的工具类型。

**2. 严格的空值处理：**
- 遵守 `strictNullChecks` 规范，妥善处理潜在的 `null` 或 `undefined`。
- 在访问可能为空的属性或调用可能不存在的方法时，必须使用可选链操作符（`?.`）和空值合并运算符（`??`），避免 `Cannot read properties of undefined` 报错。

**3. 类型复用与派生：**
- 避免在不同文件中重复复制粘贴相同的结构。提取公用的业务类型到专门的 `types` 或 `interfaces` 目录中。
- 善用 TypeScript 内置的工具类型（如 `Pick<T, K>`, `Omit<T, K>`, `Partial<T>`, `Record<K, T>`）基于已有核心业务实体派生出新的类型（如 DTO，更新参数等）。

**4. 外部数据边界的类型断言：**
- 对于来自接口请求（API Response）或本地存储（localStorage）的动态数据，需定义明确的接口类型，并尽量配合类型守卫（Type Guards）或 Zod 等校验库在运行时验证结构，慎用强制断言 `as Type`。
