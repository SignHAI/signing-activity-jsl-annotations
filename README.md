# Signing Activity Annotations

[日本語](README_ja.md)

Additional **Signing Activity annotations** created for the JSL Dialogue Corpus (日本手話話し言葉コーパス; JSL corpus). Further additions to the dataset are planned.
Distribution is limited to the newly created Signing Activity intervals and labels, and their correspondence with the original corpus. Corpus videos, audio, images, and existing corpus annotations are not distributed here. Information that would allow reconstruction of the original corpus data is also outside the distribution scope. To use the additional annotations alongside the corresponding videos, obtain the JSL corpus separately through the prescribed NII-IDR procedure.

## Annotation definition

Signing Activity covers sign-language expressions intended to communicate with the other participant, from the onset of the first expression's movement to the end of the final movement or linguistic hold. Communicative backchannels and expressions consisting only of facial expressions or mouth patterns are included. Mere preparation, post-utterance hand retraction, and movements for posture adjustment are excluded. Short pauses judged to be a continuation of the same utterance are included within the same interval. When an utterance clearly ends and a new utterance begins, separate intervals are annotated.

The tiers are `LEFT_HUMAN_ANNOTATION` and `RIGHT_HUMAN_ANNOTATION`, with the label `SIGNING`. LEFT/RIGHT refer to screen sides when the video is viewed in its normal orientation. Labels are assigned independently to the left and right tiers.

## Obtain the JSL corpus

The JSL corpus is available through [NII's official application procedure](https://www.nii.ac.jp/dsc/idr/rdata/JSL/). Follow the current official instructions.

The JSL corpus is provided free of charge for academic research by researchers at universities and public research institutions. A laboratory representative submits the Word application form to IDR by email. Once the application is accepted, stamp the formal agreement sent by IDR with the official institutional seal and return it by post. The data are provided after the agreement is checked. Consult the official guidance for eligibility, required documents, and procedural details.

Read the [corpus policy](https://www.nii.ac.jp/dsc/idr/rdata/JSL/documents/JSL-policy.html) and the service terms linked from the application page. The [user guidance](https://www.nii.ac.jp/dsc/idr/rdata/JSL/user.html) describes reporting and attribution requirements. Sending corpus face images or videos to external generative AI services is prohibited.

## Connect the annotations to corpus videos

Follow these steps to use the additional annotations alongside the corresponding videos:

1. Obtain the corpus through the official procedure above.
2. Check the corresponding corpus video in [the video–annotation correspondence table](metadata/recordings.csv), and place a copy in `movies/`, keeping the filename exactly as listed in `corpus_video_filename`.
3. Open the EAF specified by `annotation_file` in `annotations/eaf/` with ELAN.

For example, the specified layout for `FO_09_10_AniN` (`Ani1`) is:

```text
signing-activity-jsl-annotations/
  movies/
    FO_09_10_AniN.mp4
  annotations/
    eaf/
      FO_09_10_AniN.eaf
```

The EAF refers to `../../movies/FO_09_10_AniN.mp4` relative to its own directory. Keep this directory relationship when moving the repository. The distribution layout lets EAFs reference their videos directly, so normal use does not require generating EAFs or manually linking media. See the [video placement guide](movies/README.md) for details.

## Recording correspondence

[recordings.csv](metadata/recordings.csv) lists recording identifiers and abbreviations, EAF locations, original video filenames, and left/right participant IDs. It is a correspondence table, not a table of annotation intervals. It uses UTF-8, comma-separated columns, and one header row.

| Column | Meaning |
| --- | --- |
| `recording_id` | Recording identifier in the JSL corpus. |
| `display_id` | Abbreviation for each dialogue (e.g., `Ani1`, `Cur1`). |
| `annotation_file` | EAF location under `annotations/eaf/`, expressed as a path relative to the repository root. |
| `corpus_video_filename` | Corresponding video filename in the official corpus distribution. Place it in `movies/` without changing this name. |
| `left_participant_id` | Corpus participant ID on the left of the screen when the video is viewed in its normal orientation. |
| `right_participant_id` | Corpus participant ID on the right of the screen when the video is viewed in its normal orientation. |

## Distribution files

| Location | Contents |
| --- | --- |
| `annotations/` | Additional annotations (EAF, CSV). |
| [movies/](movies/README.md) | Location for locally obtained JSL corpus videos. |
| [recordings.csv](metadata/recordings.csv) | Video correspondence, EAF locations, and left/right participant IDs. |
| [LICENSE](LICENSE) | Scope and full text of CC BY-NC 4.0 for the additional annotations and correspondence information. |
| [Changelog](CHANGELOG.md) | Data additions and corrections. |

For programmatic use, `annotations/csv/<recording_id>.csv` contains the same intervals as the corresponding EAF, with one row per human-annotated interval. There is one CSV file per dialogue; the `recording_id` in its filename identifies the corresponding row in `metadata/recordings.csv`. Each file uses UTF-8, comma-separated columns, and the following header:

```csv
tier,start_ms,end_ms,label
```

`tier` is `LEFT_HUMAN_ANNOTATION` or `RIGHT_HUMAN_ANNOTATION`, and `label` is `SIGNING`. `start_ms` and `end_ms` are the interval's start and end times in integer milliseconds on the EAF timeline.

## Source and terms

The additional annotation intervals and labels (`annotations/eaf/` and `annotations/csv/`) and their correspondence with the original corpus (`metadata/recordings.csv`) are licensed under [Creative Commons Attribution-NonCommercial 4.0 International (CC BY-NC 4.0)](https://creativecommons.org/licenses/by-nc/4.0/). Use them for noncommercial purposes in accordance with the license, including appropriate attribution, a license link, and an indication of changes. See [LICENSE](LICENSE) for the scope and full license text.

This license does not apply to the original corpus. The JSL Dialogue Corpus itself is not included in this GitHub repository and must be [obtained separately from NII-IDR](https://www.nii.ac.jp/dsc/idr/rdata/JSL/). Its use is subject to the [corpus policy](https://www.nii.ac.jp/dsc/idr/rdata/JSL/documents/JSL-policy.html) and the service terms specified in the NII-IDR application guidance. Follow the [reporting and attribution guidance](https://www.nii.ac.jp/dsc/idr/rdata/JSL/user.html) as well.

The corpus's formal Japanese name is 日本手話話し言葉コーパス（JSLコーパス）, and its official English citation title is *A Colloquial Corpus of Sign Languages in Japan (JSL)*. It is provided by the National Institute of Informatics and Tsukuba University of Technology, and distributed through the National Institute of Informatics' IDR Dataset Service.

The source dataset citation follows the [official DSC Reference Portal entry](https://dsc.repo.nii.ac.jp/?action=repository_uri&item_id=5155&lang=japanese).

> Mayumi Bono, Yutaka Osugi (2026): A Colloquial Corpus of Sign Languages in Japan (JSL). Informatics Research Data Repository, National Institute of Informatics. (dataset). [https://doi.org/10.32130/rdata.13.1](https://doi.org/10.32130/rdata.13.1)

## Citation

The recommended citation will be provided once the bibliographic details are finalized.
