# コーパス動画の配置

[English](README.md)

正式に取得したJSLコーパスの動画を、[元動画と追加注釈の対応表](../metadata/recordings.csv)の`corpus_video_filename`に記載された名前のまま、このディレクトリに配置してください。このリポジトリでは動画本体や元コーパスの既存注釈を配布しません。

`FO_09_10_AniN`（`Ani1`）の配置は次のとおりです。

```text
movies/FO_09_10_AniN.mp4
annotations/eaf/FO_09_10_AniN.eaf
```

動画を配置した後、`annotation_file`に指定されたEAFをELANで開きます。EAFは、`annotations/eaf/`からの相対パス`../../movies/FO_09_10_AniN.mp4`を参照します。リポジトリを移動するときも、この位置関係を保ってください。通常の利用でEAFの生成や手動のメディア紐付けは必要ありません。

コーパスの申請方法、対応表、注釈の説明は[リポジトリのREADME](../README_ja.md)を参照してください。
