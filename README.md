# Beijing-PM2.5-Forecast
based on ARIMA、LSTM and Transformer

# 基于ARIMA, LSTM与Transformer的北京市PM2.5浓度预测分析

## 📝 项目简介

本项目旨在对2014年至2015年的北京市空气质量数据进行深入的探索性分析（EDA），并利用其时间序列特性，构建和比较三种不同的预测模型：传统的统计学模型 **ARIMA**，以及深度学习模型 **LSTM** 和 **Transformer**，以预测未来的PM2.5浓度。

## 📊 数据集

* [cite_start]**来源**: 本项目使用的数据集为 `Beijing.csv` [cite: 2][cite_start]，来自于我的时间序列课程大作业，包含了从2014年到2015年逐小时的空气质量和气象数据 。
* [cite_start]**特征**: 包括PM2.5, PM10, SO2, NO2等空气质量指标，以及温度(TEMP), 湿度(HUMI), 风速(WS)等气象数据 。

## ⚙️ 分析流程

1.  **数据预处理**:
    * [cite_start]将年、月、日、小时合并为时间索引 。
    * [cite_start]使用线性插值和众数填充处理缺失值 。
    * [cite_start]通过IQR（四分位距）方法识别并处理PM2.5中的异常值 。
    * [cite_start]对风向（WD）等分类特征进行独热编码 。
2.  **探索性数据分析 (EDA)**:
    * [cite_start]通过可视化手段分析PM2.5浓度的时间序列图、分布直方图以及按月、按小时的季节性规律 。
    * [cite_start]利用热力图分析各空气质量和气象参数之间的相关性 。
3.  **模型构建与评估**:
    * [cite_start]**ARIMA**: 通过ADF检验确定序列平稳性（d=0），并结合ACF/PACF图定阶，构建ARIMA(1,0,1)模型作为基准 。
    * [cite_start]**LSTM**: 构建基于长短期记忆网络的深度学习模型，利用过去24小时数据预测未来10小时浓度 。
    * [cite_start]**Transformer**: 构建基于自注意力机制的Transformer模型，执行与LSTM相同的预测任务 。

## 📈 主要发现与结论

模型在测试集上的平均预测性能如下表所示。结果表明，深度学习模型在捕捉复杂的非线性关系方面远优于传统统计模型，其中**LSTM**在本研究中表现最佳。

| 模型 (Model) | RMSE (未来10小时平均) | MAE (未来10小时平均) |
| :--- | :---: | :---: |
| ARIMA | 86.133 | 70.776 |
| **LSTM** | **46.813** | **32.402** |
| Transformer | 48.119 | 33.885 |
[cite_start]*[数据来源: 表格 4: 各模型PM2.5预测性能指标比较 ]*

### 关键图表

**各模型预测结果对比 (测试集前段)**
![模型对比图](images/model_comparison_plot.png)
*上图直观展示了LSTM和Transformer模型能更精确地拟合PM2.5浓度的剧烈波动，而ARIMA的预测则相对平滑滞后。*

**PM2.5浓度月度季节性**
![月度箱线图](images/pm25_monthly_boxplot.png)
*PM2.5浓度在冬季（11月-1月）显著高于夏季，呈现明显的年度季节性规律。*


## 🚀 如何运行

1.  **克隆仓库**
    ```bash
    git clone [https://github.com/hanxiaoyu-coder/Beijing_PM2.5_Forecast.git](https://github.com/hanxiaoyu-coder/Beijing_PM2.5_Forecast.git)
    cd Beijing_PM2.5_Forecast
    ```
2.  **创建并激活虚拟环境 (推荐)**
    ```bash
    python -m venv venv
    # Windows
    venv\Scripts\activate
    # macOS/Linux
    source venv/bin/activate
    ```
3.  **安装依赖**
    ```bash
    pip install -r requirements.txt
    ```
4.  **运行分析**
    打开 `notebooks/` 文件夹中的 `PM2.5_Analysis_and_Forecasting.ipynb` 文件，并按顺序运行所有Jupyter Notebook单元格。

## 🛠️ 技术栈

* Python
* Pandas & Numpy (数据处理)
* Matplotlib & Seaborn (数据可视化)
* Statsmodels (ARIMA模型与时间序列分析)
* Scikit-learn (数据预处理与评估)
* TensorFlow / Keras (LSTM与Transformer模型)
* Jupyter Notebook
