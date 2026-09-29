# Signing Activity アノテーション

[English](README.md)

JSL Dialogue Corpus（日本手話話し言葉コーパス、JSLコーパス）を対象として作成した **Signing Activityの追加アノテーション**です。データは随時拡張を行う予定です。
公開対象は、新たに作成したSigning Activityの区間情報・ラベルと、元コーパスとの対応情報のみです。コーパス本体の動画・音声・画像・既存注釈は配布しません。元コーパスのデータそのものを復元できる情報も公開対象に含めません。追加注釈を対応する動画と併せて利用する場合は、NII-IDRの所定の手続きでJSLコーパスを別途取得してください。

## アノテーション定義

Signing Activityは、相手への伝達を目的とする手話表現の、最初の動作開始から最後の動作または言語的な保持の終了までを対象とします。伝達行為としての相づちや、表情・口型のみの表現も含みます。単なる準備動作、発話終了後の手の戻し、姿勢調整のための動作は含みません。同一発話の継続と判断される短い停止は同一区間に含め、発話が明確に終了した後に新しい発話が開始する場合は、別の区間として付与します。

tierは`LEFT_HUMAN_ANNOTATION`と`RIGHT_HUMAN_ANNOTATION`、ラベルは`SIGNING`です。LEFT/RIGHTは、通常の向きで見た動画の画面上の左右です。左右のtierには独立してラベルを付与します。

## JSLコーパスの取得方法

JSLコーパスは[NIIの公式申請手続き](https://www.nii.ac.jp/dsc/idr/rdata/JSL/)で取得できます。最新の公式案内に従ってください。

JSLコーパスは大学・公的研究機関の研究者を対象に、学術研究目的で無償提供されています。申請では、研究室の代表者がWord形式の利用申請書をIDRへメールで提出します。利用が認められた後、IDRから届く正式な同意書に公印で押印して郵送してください。確認後にデータが提供されます。対象者、必要書類、手続きの詳細は公式案内を参照してください。

利用においては、[コーパス利用規約](https://www.nii.ac.jp/dsc/idr/rdata/JSL/documents/JSL-policy.html)と、申請案内からリンクされたサービス規約を確認してください。[利用者向け案内](https://www.nii.ac.jp/dsc/idr/rdata/JSL/user.html)には報告・出典表記の要件が記載されています。コーパスの顔画像・動画を外部の生成AIサービスに入力することは禁止されています。

## コーパス動画との接続

次の手順で、追加アノテーションを対応する動画と併せて利用できます。

1. 上記の正式な手続きでコーパスを取得します。
2. [元動画と追加注釈の対応表](metadata/recordings.csv)で対応するコーパス動画を確認し、`corpus_video_filename`に記載された名前のまま、そのコピーを`movies/`に置きます。
3. `annotation_file`に対応する`annotations/eaf/`内のEAFをELANで開きます。

たとえば、`FO_09_10_AniN`（`Ani1`）の指定配置は次のとおりです。

```text
signing-activity-jsl-annotations/
  movies/
    FO_09_10_AniN.mp4
  annotations/
    eaf/
      FO_09_10_AniN.eaf
```

EAFは、自身のディレクトリから見た`../../movies/FO_09_10_AniN.mp4`を参照します。リポジトリを移動するときも、この位置関係を保ってください。配布するEAFが動画を直接参照する構成であり、通常の利用でEAFの生成や手動のメディア紐付けは必要ありません。詳細は[動画の配置案内](movies/README_ja.md)を参照してください。

## 対応表

[recordings.csv](metadata/recordings.csv)には、収録識別子と略称、EAFの配置先、元動画のファイル名、左右の話者IDを記載しています。注釈区間を記載したCSVとは別の対応表です。UTF-8のカンマ区切りCSVで、先頭行がヘッダーです。

| 列名 | 内容 |
| --- | --- |
| `recording_id` | JSLコーパスの収録識別子 |
| `display_id` | 各対話の略称（例：`Ani1`、`Cur1`）。 |
| `annotation_file` | リポジトリのルートからの相対パスで指定した、`annotations/eaf/`内のEAF配置先。 |
| `corpus_video_filename` | 元コーパスの正式配布版における対応動画のファイル名。この名前のまま`movies/`に配置します。 |
| `left_participant_id` | 通常の向きで見た動画の画面左側にいる話者のコーパス内ID。 |
| `right_participant_id` | 通常の向きで見た動画の画面右側にいる話者のコーパス内ID。 |

## 配布ファイル

| 場所 | 内容 |
| --- | --- |
| `annotations/` | 追加アノテーション（EAF、CSV） |
| [movies/](movies/README_ja.md) | 取得したJSLコーパス動画の配置位置 |
| [recordings.csv](metadata/recordings.csv) | 元動画との対応、EAFの配置先、左右の話者IDを記載したテーブル |
| [LICENSE](LICENSE) | 追加注釈・対応情報に適用するCC BY-NC 4.0の範囲と全文 |
| [変更履歴](CHANGELOG.md) | データの追加・修正履歴 |

プログラムから利用する場合は、`annotations/csv/<recording_id>.csv`を使用できます。対応するEAFと同じ区間を、人手注釈の1区間につき1行で記載しています。CSVは1対話につき1ファイルで、ファイル名の`recording_id`を使って`metadata/recordings.csv`の対応する行を確認できます。UTF-8のカンマ区切りCSVで、先頭行は次のヘッダーです。

```csv
tier,start_ms,end_ms,label
```

`tier`は`LEFT_HUMAN_ANNOTATION`または`RIGHT_HUMAN_ANNOTATION`、`label`は`SIGNING`です。`start_ms`と`end_ms`は、EAFの時間軸における区間の開始・終了時刻を整数のミリ秒で表します。

## 出典・利用条件

追加注釈の区間情報・ラベル（`annotations/eaf/`と`annotations/csv/`）と元コーパスとの対応情報（`metadata/recordings.csv`）は、[Creative Commons 表示–非営利 4.0 国際（CC BY-NC 4.0）](https://creativecommons.org/licenses/by-nc/4.0/)で提供します。非営利目的で、必要な出典表示、ライセンスへのリンク、変更の明示など、同ライセンスの条件に従って利用してください。適用範囲とライセンス全文は[LICENSE](LICENSE)を参照してください。

このライセンスは元コーパス本体には適用されません。JSL Dialogue Corpus本体はこのGitHubリポジトリに含まれず、[NII-IDRから別途取得](https://www.nii.ac.jp/dsc/idr/rdata/JSL/)する必要があります。元コーパスの利用には、NII-IDRが定める[コーパス利用規約](https://www.nii.ac.jp/dsc/idr/rdata/JSL/documents/JSL-policy.html)と申請案内に記載されたサービス規約が適用されます。[報告・出典表記の案内](https://www.nii.ac.jp/dsc/idr/rdata/JSL/user.html)にも従ってください。

元コーパスの正式名称は「日本手話話し言葉コーパス（JSLコーパス）」、公式の英語引用名は *A Colloquial Corpus of Sign Languages in Japan (JSL)* です。国立情報学研究所・筑波技術大学が提供し、国立情報学研究所のIDRデータセット提供サービスを通じて配布されています。

元コーパスのデータセット引用は、[DSCリファレンスポータルの公式記載](https://dsc.repo.nii.ac.jp/?action=repository_uri&item_id=5155&lang=japanese)に従います。

> 坊農真弓，大杉豊 (2026): 日本手話話し言葉コーパス（JSLコーパス）. 国立情報学研究所情報学研究データリポジトリ. (データセット). [https://doi.org/10.32130/rdata.13.1](https://doi.org/10.32130/rdata.13.1)

## 引用

推奨する引用形式は、書誌情報が確定次第、掲載します。
