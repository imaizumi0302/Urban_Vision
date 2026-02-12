# Urban Vision (Alpha Version)

### AI-powered Crowd Density Analysis & Risk Visualization Prototype

Urban Visionは、公共スペースやイベント会場での安全管理を支援するために開発された、AIベースの群衆解析プロトタイプです。単なる人数カウントではなく、**「密集度」と「物理的接触リスク」を定量化**し、直感的なヒートマップと統計グラフで可視化します。

> **Note**: 本プロジェクトは現在Alpha版であり、特定の検証用データセット（UCSD Peds Dataset）に最適化されたアルゴリズムの検証段階です。

---

## 1. 解決する課題

* **定性的判断の排除**: 「混んでいる」という主観的な判断を数値化し、客観的な評価指標を提供。
* **潜在的リスクの特定**: 人数だけでなく、人物同士の重なり（Overlap）から物理的接触リスクを算出。
* **データに基づく管理**: 解析結果をCSVおよびPDFレポートとして保存し、警備配置の最適化を支援。

## 2. 実装済みの主な機能

### ① 群衆リスク評価アルゴリズム

以下の3要素を統合した独自のスコアリングを実装しています：

* **People Count**: 画面内の総人数。
* **Density Score**: 画面面積に対する人物領域の占有率。
* **Overlap Score**: 人物同士のバウンディングボックスの重なり具合。
* **PCA（主成分分析）**: 密度と重なり度の重みを統計的に推定し、リスクスコアを算出。

### ② リアルタイム可視化

* **動的ヒートマップ**: 混雑箇所をカラーマップで映像にオーバーレイ。
* **時系列グラフ**: 映像下部にリスクスコアの推移グラフをリアルタイム合成。
* **ピーク動画抽出**: 混雑スコアが閾値を超えた前後のシーンを自動抽出。

### ③ データ出力

* **CSV Logging**: 全フレームの解析結果を構造化データとして保存。
* **PDF Report**: 解析の概要と統計結果を自動ドキュメント化（`fpdf2`使用）。

## 3. 技術スタック

* **Language**: Python
* **Object Detection**: YOLO (Ultralytics v11)
* **Image Processing**: OpenCV (cv2)
* **Data Analysis**: Pandas, NumPy
* **Statistics**: Scikit-learn (MinMaxScaler, PCA)
* **Environment**: Google Colab (T4 GPU)

## 4. 実行方法（Setup）

本ノートブックはGoogle Colabでの実行を想定しています。

1. **データセットの準備**:
[UCSD Anomaly Detection Dataset](https://www.google.com/search?q=http://www.svcl.ucsd.edu/datasets/anomaly/) からデータをダウンロードし、`ucsdpeds.zip` として配置してください。
2. **パスの設定**:
ノートブック内の `ZIP_PATH` および `DEST_DIR` をご自身の環境に合わせて設定してください。
```python
ZIP_PATH = "ucsdpeds.zip"
DEST_DIR = "/content/UCSD"

```


3. **実行**:
セルの指示に従い実行してください。解析結果の動画とレポートが出力されます。

## 5. 現在の課題と今後の展望

* **汎用化**: 現在は特定の画角に依存しているため、**ホモグラフィ変換（投影変換）**を用いた座標補正による汎用化を計画しています。
* **異常検知**: 単なる混雑だけでなく、逆走や転倒などの異常行動を検知する機能の追加。
* **行動予測**: 過去の時系列データに基づいた、数分後の混雑ピーク予測モデルの導入。

---

## Author

**今泉 元 / Hajime Imaizumi**
* [Portfolio (Notion)](https://www.notion.so/2e072e700087801f8b30f5199bd1ea11)
* [GitHub](https://github.com/imaizumi0302)

---

*このプロジェクトは研究・開発段階のプロトタイプであり、実地での運用には環境に合わせたパラメータ調整が必要です。*

