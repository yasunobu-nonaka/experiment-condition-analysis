# experiment_condition_analysis

ある実験装置における２つの測定手法（MethodA, MethodB）から出力されるCSVデータから、**前処理条件や温度データを抽出し、測定者ごと・測定時期ごとの変化や違いを可視化・分析**するJupyterノートブック群です。

実際の実験データの代わりに、ダミーデータをコードから生成して使用します。生成する場合はdata_generator_MethodA.ipynb, data_generator_MethodB.ipynbの全セルを実行してください。  
なおデータを生成しなくてもextract_conditions.ipynbまたはpretreatment_temperature_analysis.ipynbで作成したグラフなどはノート上に残っているためそのまま確認可能です。

## 目的

ある実験装置について、(i) **測定者ごとの前処理条件の違いの調査**、および(ii) **前処理時の目標温度と実際の温度との差の調査**を実施したい。  
そこで機械から出力されたCSVデータをPandasで読み込み目的のデータを抽出し、構造化データ（表データ）としてまとめる。  
そのデータからmatplotlibやseabornを用いてグラフ化を行い。前処理条件や前処理温度にどのような変化・特徴が見られるのかを分析する。

## 装置・測定法について

- この実験装置では指定した条件で試料を前処理した後、複数回のパルスを注入して測定を行います。
- 装置はMachine AとMachine Bの2台が存在します。
- 分析方法にはMethod AとMethod Bの２種類が存在します。
- データファイルには実際の測定データが記録されたデータ（SampleX_MethodX_yyyymmdd.csv）と、前処理から測定含む全体プロセスの温度・信号トレンドのデータ（Trend_SampleX_MethodX_yyyymmdd.csv）の２種類があります。
- 測定を行うユーザーはUserA, UserB, UserC, ..., UserOの15名存在します。

## ノート一覧

### **data_generator_MethodA.ipynb**, **data_generator_MethodB.ipynb**

測定法A（MethodA）および測定法B（MethodB）のダミー測定データを生成するためのノートです。  
extract_conditions.ipynbまたはpretreatment_temperature_analysis.ipynbを再度実行したい場合は事前にこの２つのノート上のセルをすべて実行する必要があります。  
実行すると機械、ユーザー、測定法ごとにフォルダ分けされてCSVデータが生成されます。

### **extract_conditions.ipynb**

CSVデータから前処理条件（ガス、流量、処理時間、温度）を抽出し、測定者・時期ごとの測定条件の違い・変化を分析するノートです。  
ヒストグラム、ヒートマップなどを用いて測定者・時期ごとの測定条件の違いを可視化します。

### **pretreatment_temperature_analysis.ipynb**

サンプル測定結果データ（名称がsampleXから始まるCSVデータ）と温度トレンドデータ（時系列温度記録、名称がTrendから始まるデータ）を対応付けて、前処理の目標温度と実際の到達温度（温度一定部分）を比較・分析するノートです。  
ヒストグラム、散布図などを用いて機器、測定法、時期ごとの傾向を分析します。

## （ノートを実行したい場合）セットアップ

1. 仮想環境を作成します。

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

2. JupyterLabを起動します。

```bash
jupyter lab
```

3. data_generator_MethodA.ipynbおよびdata_generator_MethodB.ipynbを開き、上から順にすべて実行してください。

4. (i) 測定者ごとの前処理条件の違いの調査については、extract_conditions.ipynbを、(ii) 前処理時の目標温度と実際の温度との差の調査についてはpretreatment_temperature_analysis.ipynbを上から実行してください。
