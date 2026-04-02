# 实验 2：一般网络与可修系统可靠性分析（lab2-general）

本仓库基于原有桥式起重机机械系统案例，扩展为 `lab2-general` 实验模板。实验不再只关注
不可修任务下的 RBD 串并联系统，而是进一步研究：

- 一般网络系统的可靠性模型
- 可修系统的可靠性与可用度模型

实验的完整要求见 `description.md`。

---

## 1. 实验内容
### A) 一般网络可靠性建模
- 仍以桥式起重机机械系统为工程背景
- 不再仅用串联/并联 RBD 表达系统，而是将系统抽象为更一般的功能网络
- 需要围绕“源点到汇点连通且满足任务成功条件”建立可靠性模型

### B) 可修系统建模
- 在元件失效率基础上，引入维修恢复参数
- 比较不可修系统可靠度与可修系统可用度/稳态性能指标
- 分析维修策略、冗余路径和关键设备对系统性能的影响

### C) 保留任务剖面背景
- 保留 Pick / Lift / TravelLoaded / Place / ReturnEmpty 五阶段机械系统背景
- 任务剖面继续用于描述元件工作占空比和任务载荷特征
- 当前计算脚本同时输出一般网络可靠度和可修系统可用度
---

## 2. 一键运行
当前仓库已支持 `lab2-general` 实验格式输出。

在仓库根目录执行（示例,姓名使用拼音或英文）：

```bash
python src/calc.py --student_id 2026XXXXXX --student_name zhangsan --N 60
```

- `--N`：循环次数（默认 60，需自行调整）
- 单循环时长 `t_cyc` 来自 `data/mission_profile.csv` 的五阶段时长之和
- 运行后生成：`output/lab2_general_report_<student_id>_<student_name>.md`
- 输出包括：一般网络可靠度、可修系统稳态可用度、单元件表和 sanity checks

---

## 3. 输入数据
- `data/components.csv`：元件参数，包含 `lambda_per_h` 和 `mu_per_h`
- `data/mission_profile.csv`：阶段时长 + 元件工作标记（0/1）
- `data/model.json`：系统结构模型，包含 `network_model` 和 `repairable_model`
- `network_model`：一般网络结构，采用 source 到 target 连通作为成功判据
- `repairable_model`：可修系统分析口径，当前采用稳态可用度

---

## 4. 预期输出
- 一般网络模型的结构摘要与系统可靠度
- 可修系统的关键参数、单元可用度与系统可用度
- 不可修与可修模型的结果对比
- 薄弱环节与工程改进建议

---

## 5. 提交物 (submissions)

1. `lab2_general_report_<student_id>_<name>.md`（必须，要求见 `description.md`）
2. `calc.py`（或同等 Python 脚本，必须可运行）
3. `data/components.csv`（如有修改，必须提交）
4. `data/mission_profile.csv`（必须提交）
5. `data/model.json`（系统网络结构文件，必须提交）
6. 一份转为 PDF 的报告（双面打印提交）
---

## 0. 重要说明与常见问题

### 参数与数据自定义
- 默认所有同学的数据文件（components.csv、mission_profile.csv、model.json）一致，结果也一致。
- 如需个性化实验结果，可自行调整 N、任务剖面、网络结构或元件参数。
- 在自定义区块说明你的个性化修改内容。

### 结果文件命名与归档
- 程序自动生成结果文件，命名为：`lab2_general_report_<student_id>_<student_name>.md`，请勿手动更改。
- 所有结果自动归档到 output/ 目录，便于批量收集和自动化检查。

### 手动补充区块说明
- 自动生成区块（参数、表格、网络结构摘要等）请勿手动修改，否则自动化检查时会被覆盖。
- 请在报告的学生自定义补充区内补充建模思路、公式推导、工程解释等内容。

### 批量自动运行与归档（教师/助教参考）
- 可用脚本批量运行所有学生的 calc.py，并自动归档结果。
- 示例：
  ```bash
  for d in submissions/*; do
    id=$(basename "$d" | cut -d_ -f1)
    name=$(basename "$d" | cut -d_ -f2)
    python src/calc.py --student_id "$id" --student_name "$name" --N 60
  done
  ```

### 结果一致性与个性化
- 不修改数据时，所有同学结果一致。
- 如需差异，请按要求个性化数据或参数，并在自定义区说明。

### 提交物清单
- `lab2_general_report_<student_id>_<student_name>.md`（自动生成，含自定义补充区）
- `calc.py`（如有修改需一并提交）
- 数据文件（如有个性化修改需一并提交）

### 常见错误与解决方法
- 参数未填写或格式错误：请检查命令行参数和数据文件格式。
- 结果文件被覆盖：请只在自定义补充区填写手动内容。
- 自动化检查未通过：请检查网络结构、维修参数和任务剖面。

---

## 附录：Git 基础使用方法资源

- [Git 官方文档（简体中文）](https://git-scm.com/book/zh/v2)
- [Git 官方英文文档](https://git-scm.com/doc)
- [Git Cheat Sheet（官方速查表）](https://education.github.com/git-cheat-sheet-education.pdf)
- [廖雪峰的 Git 教程](https://www.liaoxuefeng.com/wiki/896043488029600)
- [菜鸟教程 Git](https://www.runoob.com/git/git-tutorial.html)
- [VS Code 官方 Git 指南](https://code.visualstudio.com/docs/sourcecontrol/overview)

以上资源适合初学者快速学习 Git 的基本操作和常用命令。
