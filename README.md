# Trey Cabbage 打撃・走力分析（2023・2024年）

2023年・2024年にMLBでプレーしたトレイ・キャベッジの打撃と走力を、データで読み解いた分析です。

📝 解説記事（note）: 【note記事のURL】

## 分析の問い

- キャベッジは、どのような打撃をしていたのか？
- 2023年から2024年にかけて、打球の質やスイングはどう変化したのか？
- 強い打球を生み出す力は、実際の打撃結果にどのようにつながっていたのか？
- 打撃以外に、どのような選手としての特徴があったのか？

## 使用データ

| データ | 出典 | 内容 |
|---|---|---|
| reference_2023 / 2024 | Baseball Reference | 年間の打撃成績（PA、BA、OBP、SLG、OPS、BB、SOなど） |
| savant_2023 / 2024 | Baseball Savant（Statcast） | 年間の打撃指標（平均打球速度、Hard-Hit%、Barrel%、Launch Angle、xBA、xSLG、wOBA、xwOBAなど） |
| savant_sprint_speed_2024 | Baseball Savant（Statcast） | 2024年のSprint Speedなどの走力データ |

- 対象期間：2023年・2024年レギュラーシーズン
- 取得日：【データ取得日】
- Baseball Reference、Baseball SavantからCSVをダウンロードして使用しています。

## 使用技術

- Python（pandas、sqlite3）
- SQLite
- Google Colab

## 分析の流れ

1. 5本のCSVを pandas で読み込む
2. sqlite3 でデータベース（`cabbage.db`）に登録する
3. SQLで必要な指標を抽出する（`SELECT`、別名（`AS`）、計算式など）
4. pandas でデータを整形し、2023年と2024年の比較表を作成する
5. Baseball SavantのStatcastデータから打球の質、スイング、期待値、走力を分析する

## ファイル構成

| ファイル | 内容 |
|---|---|
| cabbage_analysis.ipynb | 上記の分析一式（読み込み → DB登録 → SQL抽出 → 表の作成） |
| 【2023年Reference CSV】 | 2023年の年間打撃成績（Baseball Reference） |
| 【2024年Reference CSV】 | 2024年の年間打撃成績（Baseball Reference） |
| 【2023年Savant CSV】 | 2023年の年間打撃指標（Baseball Savant） |
| 【2024年Savant CSV】 | 2024年の年間打撃指標（Baseball Savant） |
| 【2024年Sprint Speed CSV】 | 2024年のSprint Speedデータ（Baseball Savant） |

## 実行方法

1. 使用するCSV5本を、ノートブックと同じ場所（Colabの作業フォルダ）に置く
2. `cabbage_analysis.ipynb` を Google Colab で開く
3. 上から順にセルを実行する

## 注意点・限界

- MLBでの出場機会が限られているため、2023年・2024年ともにサンプルサイズが小さく、数値の解釈には注意が必要です。
- 打球の質やスイングの変化については、2023年と2024年のデータを比較したものであり、変化の原因を特定するものではありません。
- 期待値（xBA、xSLG、xwOBA）は実際の結果とは異なる指標であり、打撃結果を完全に説明するものではありません。
- 本分析では統計的な検定や高度なモデル構築は行っておらず、主に基本的な集計・比較を行っています。
- 数値や解釈に誤りが含まれる可能性があります。

## 今後の改善予定

- MLBでのサンプルサイズを増やし、より長期的な打撃傾向を分析する
- MLB平均だけでなく、同ポジションや同程度の打席数の選手との比較を追加する
- スイング率、空振り率、ゾーン内外のアプローチなどをさらに細かく分析する
- Sprint Speedだけでなく、走塁結果や盗塁なども含めて走力を分析する
- より多くのStatcast指標を組み合わせ、打撃結果につながる要因を深掘りする
