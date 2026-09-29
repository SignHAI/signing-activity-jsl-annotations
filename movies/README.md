# Local corpus videos

[日本語](README_ja.md)

Place your formally obtained JSL corpus videos in this directory, keeping the
filenames listed in `corpus_video_filename` in
[the recording correspondence table](../metadata/recordings.csv) unchanged.
The repository does not distribute videos or existing corpus annotations.

For `FO_09_10_AniN` (`Ani1`), the layout is:

```text
movies/FO_09_10_AniN.mp4
annotations/eaf/FO_09_10_AniN.eaf
```

After placing the video, open the EAF specified by `annotation_file` in ELAN.
Its media reference is `../../movies/FO_09_10_AniN.mp4`, relative to
`annotations/eaf/`. Preserve this directory relationship when moving the
repository. Normal use does not require generating EAFs or manually linking
media.

See the [repository README](../README.md) for the corpus application
procedure, recording correspondence, and annotation information.
