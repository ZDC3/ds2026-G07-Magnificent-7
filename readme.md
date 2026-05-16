# T-A2: Magnificent 7 Financials & Price Panorama (G07)

项目简介：
本项目对美股“七姐妹”（AAPL、MSFT、NVDA、GOOGL、AMZN、META、TSLA）进行股价与财务指标的全景对比，包含数据获取、清洗、指标计算、可视化与结论建议，并输出图表与可排版的 Word 报告。

## 课程与题目信息
- 课程：数据分析与经济决策（ds2026）
- 题目：T-A2 美股「七姐妹」财务与股价全景对比
- 小组：第七组
- GitHub：https://github.com/ZDC3/ds2026-G07-Magnificent-7
- Pages：https://zdc3.github.io/ds2026-G07-Magnificent-7
- 日期：2026-05-16

## 小组成员与分工（可据实际调整）
- 7125210211 莫才有（组长）：总体统筹、数据质量与最终报告
- 225210189 刘帆：股价数据获取与质量核验
- 325210247 王天正：财务指标整理与解释
- 425210271 许玲敏：清洗流程与指标计算
- 625210132 高世杰：相关性/风险收益分析
- 725210291 曾垂健：报告撰写与 Word 排版
- 825210181 廖晟可：README 与提交材料整理

## 项目结构
```
T-A2_Magnificent7/
├── readme.md
├── data_raw/
│   ├── prices_raw.csv
│   └── financials_raw.csv
│   └── sp500_raw.csv
├── data_clean/
│   ├── prices_clean.csv
│   ├── returns.csv
│   ├── metrics.csv
│   └── correlation_matrix.csv
│   └── m7.sqlite
├── output/
│   ├── fig_price_trend.png
│   ├── fig_return_heatmap.png
│   ├── fig_risk_return.png
│   ├── fig_valuation.png
│   ├── fig_correlation_heatmap.png
│   ├── fig_alpha.png
│   ├── interactive_charts.html 
│   └── analysis_report.md
├── 01_get_data.ipynb
├── 02_data_clean.ipynb
└── 03_analysis_visualization.ipynb
```

## 数据来源
- yfinance：历史股价与财务摘要指标
- 标普 500 指数：^GSPC（扩展基准）
- 数据频率：日度（近 5 年）

## 数据质量与完整性控制
- 时间覆盖检查：起止日期与交易日数量
- 缺失值检查：按股票列计算缺失率
- 复权收盘价：使用 `auto_adjust=True`
- 清洗策略：节假日缺失前向填充；异常缺失记录说明
- 指标计算：年化收益率、年化波动率、最大回撤、夏普比率
- 数据落库：SQLite 便于复查与扩展

## 环境与依赖
建议使用 Python 3.10+。

```
pip install yfinance pandas numpy matplotlib seaborn python-docx
```

## 运行顺序
1. 运行 01_get_data.ipynb 获取原始数据
2. 运行 02_data_clean.ipynb 清洗与指标计算
3. 运行 03_analysis_visualization.ipynb 生成图表与报告

## 数据字段说明
- prices_raw.csv：交易日复权收盘价（列为股票代码）
- financials_raw.csv：ticker、公司名称、市值、PE、PB、营收增速、毛利率、ROE、货币、数据日期
- sp500_raw.csv：标普 500 复权收盘价（基准）
- metrics.csv：年化收益率、年化波动率、最大回撤、夏普比率
- correlation_matrix.csv：七家公司收益率相关系数矩阵

## 核心分析结论概述（基于实际结果）
本项目以七家科技巨头近五年日度复权股价为基础，构建了收益、风险、估值与相关性的全景对比框架。累计涨幅方面，NVDA 明显领先，AMZN 相对最弱，说明在 AI 与算力景气上行周期中，产业链核心公司获得了更强的超额收益，而平台型公司在 2022 年高利率与成本压力下修复节奏较慢。年度收益率热力图显示 2023 年整体表现最好、2022 年整体最弱，各公司最差年份均集中在 2022 年；GOOGL 的最佳年份为 2025 年，其余公司最佳年份多集中在 2023 年，体现行业景气与宏观流动性变化对收益的阶段性影响。

风险收益维度上，NVDA 的夏普比率最高、AMZN 最低，TSLA 的年化波动率最高，呈现“高风险、收益补偿不完全”的特征。这意味着高波动并不等同于高性价比收益，投资决策应结合风险预算与回撤容忍度。估值方面，TSLA 的 PE 最高、META 最低；PB 最高为 AAPL、最低为 META，反映市场对成长预期与盈利质量的差异化定价。在 2022 年估值压缩后，2023-2024 的股价修复更依赖盈利改善，而非单纯估值扩张。

分散化角度看，七家公司日度收益率平均相关系数约为 0.52，相关性最高的组合为 AMZN 与 MSFT（约 0.62），最低为 META 与 TSLA（约 0.34）。这说明组合仍主要暴露在科技板块 β 上，但存在一定结构性分化，适合通过行业内配置改善风险收益。基准对比显示七家公司全部跑赢标普 500，超额收益 α 排序为 NVDA（约 55.9%）> TSLA（约 20.1%）> GOOGL（约 17.0%）> META（约 10.3%）> AAPL（约 8.7%）> AMZN（约 2.9%）> MSFT（约 2.2%），说明公司层面的创新与基本面改善贡献了明显 α。

综合收益、风险与估值三维指标，若仅选择单一标的，NVDA 在收益与风险调整后收益上优势显著，但需接受更高波动；若构建等权组合，测算的年化收益约 29.7%，年化波动约 29.8%，建议以“稳健平台型 + 高成长”搭配，并关注估值回落与政策变化带来的回撤风险。后续建议结合事件驱动（AI 算力、利率周期、监管变化）进一步解释波动与估值变化，以形成可复核、可复现的结论闭环。

## 提交说明
- 压缩包命名：ds2026_G07_T-A2_莫才有.zip
- 提交内容：整个 T-A2_Magnificent7 目录
