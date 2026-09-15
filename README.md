# experiment_condition_analysis

実験機器から出力されるCSVデータをもとに、前処理条件や温度データを分析するJupyterノートブック群です。アプリケーションコードは持たず、すべての分析ロジックは `.ipynb` ノートブック内に記述されています。

## データについて

実際の実験データの代わりに、合成したダミーデータ（`Data/dummy_data/`）を使用します。これにより、機密性の高い実機データを外部に出すことなくリポジトリ上で分析コードの開発・検証ができます。

## セットアップ

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

JupyterLabを起動し、対象のノートブックを上から順に実行してください。

```bash
jupyter lab
```

**注意:** `extract_conditions.ipynb` や `pretreatment_temperature_all.ipynb` などの分析ノートを実行する前に、`data_generator_MethodA.ipynb` と `data_generator_MethodB.ipynb` を実行して `Data/dummy_data/` にダミーデータを生成しておく必要があります。

## 主なノートブック

### `extract_conditions.ipynb`
前処理条件（ガス種、流量、時間、目標温度、設定値、パルス回数など）を多数のサンプルCSVから抽出し、測定者ごと・時期ごとの測定条件の違いを分析するノートです。

### `pretreatment_temperature_all.ipynb`
Trendログ（時系列温度記録）とサンプル測定CSVを対応付け、前処理の目標温度と実際の到達温度（定常状態）を比較・分析するノートです。機器、測定法、時期ごとの傾向を分析します。

### `data_generator_MethodA.ipynb` / `data_generator_MethodB.ipynb`
上記の分析ノートで使用する合成ダミーデータ（`Data/dummy_data/`）を生成するためのノートです。
