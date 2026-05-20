# MarketMind —— AI 竞品内容分析与合规多平台分发系统

MarketMind 是一款基于 FastAPI 与 Vue 3 架构的前后端分离数字化营销大模型 Agent 协同应用。系统通过云端多 Agent 管道编排，实时检索外部竞品舆情痛点，并对冲召回本地品牌资产库（RAG），一键生成小红书、抖音脚本、公众号等多矩阵渠道的爆款流量宣发语料。

针对大模型在创意生成期普遍存在的 **AI 幻觉（恶意抹黑、品牌侵权风险）**，系统在架构出口整合了工业级 **Guardrail（安全合规护栏）终节点**；同时，针对多模推理叠加引发的 **57秒延迟危机**，系统通过线性拓扑重构与可视化执行大屏完成了高解耦的交互代偿。

---

## 🛰️ 云端 Agent 工作流拓扑架构 (Coze Engine)

由于扣子（Coze）平台编排的分布式智能体属于云端图形化资产，为了保证项目的开源透明度与可复现性，本项目已将工作流共享。

* 🔗 **云端工作流一键克隆入口**：[点击此处一键克隆本项目的 Coze 工作流](这里放你发布的扣子工作流分享链接)
* 📊 **V2.0 旗舰版纯线性合规管道拓扑图**：
  *(建议在根目录下创建 assets/ 文件夹并上传拓扑图，在此处引用：`![Architecture](assets/coze_workflow_v2.png)`)*

---

## 🔥 核心技术亮点与工程实践

### 1. 工业级 Guardrail 拦截心智
为了防止创意撰写模型为了追求“拉踩爽感”而捏造竞品物理缺陷，我们在流水线出口强制引流进入“精确模式审计终节点”。独立审计模型将逐句比对网络检索出的事实画像，拦截一切不合规语料，彻底规避品牌公关及法律红线。
```json
// 终节点标准化结构输出规约
{
  "is_passed": true,
  "risk_level": "NONE",
  "audit_log": "合规审查100%通过，无品牌侵权风险。",
  "fix_suggestion": "",
  "final_content": "..."
}
```
### 2. 后端自适应解包算法 (Recursive Unpacker)
扣子同步运行接口返回的响应极易因为多层嵌套产生双重序列化、单双引号错配等诡异变态形态（如自动包裹 {'output': '...'} 壳）。后端微网关（main.py）手写了递归自适应解包机制，并融合 json.loads 与 ast.literal_eval 双重解析保底，剥离嵌套字典，100% 确保合规调试面板在前端无损高阶渲染。

### 3. 多代架构演进心路 (Architecture Evolution)
项目内嵌的文档中心完整留存并对比了 V1.0（同步多分支五节点拓扑）因应对延迟危机和质量危机，最终向 V2.0（线性 Guardrail 强合并打包）旗舰架构重构演进的完整技术路线。
🛠️ 项目依赖对齐与快速开始

# 1. 克隆项目
git clone [https://github.com/sensy734-eng/MarketMind.git](https://github.com/sensy734-eng/MarketMind.git)
cd MarketMind

# 2. 安装标准依赖
pip install -r requirements.txt

# 3. 声明环境变量
# 复制 .env.example 并重命名为 .env，填入你的个人 COZE_API_TOKEN 和 WORKFLOW_ID

# 4. 启动后端微网关
uvicorn main:app --reload
