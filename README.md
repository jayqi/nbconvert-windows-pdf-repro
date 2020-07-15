# Reproducible Example for nbconvert Windows and PDF Bug

This repo attempts to provide a minimal reproducible example for the bug reported in [jupyter/nbconvert Issue #974](https://github.com/jupyter/nbconvert/issues/974) by using GitHub Actions.

## Results

[Build #5](https://github.com/jayqi/nbconvert-windows-pdf-repro/actions/runs/169400753) demonstrates an example where `ubuntu-latest` and `macos-latest` pass as expected, but `windows-latest` fails. You can see the failed build log here: [link](https://github.com/jayqi/nbconvert-windows-pdf-repro/runs/871565528?check_suite_focus=true#step:10:14)

```
[NbConvertApp] Running xelatex 3 times: ['xelatex', '.\\notebook.tex', '-quiet']
[NbConvertApp] CRITICAL | x failed: xelatex .\notebook.tex -quiet
This is XeTeX, Version 3.14159265-2.6-0.999992 (TeX Live 2020/W32TeX) (preloaded format=xelatex)

 restricted \write18 enabled.

entering extended mode

! Undefined control sequence.

<*> .\notebook

              .tex -quiet

?

! Emergency stop.

<*> .\notebook

              .tex -quiet

No pages of output.

Transcript written on ?.
```

Artifacts from [build #5](https://github.com/jayqi/nbconvert-windows-pdf-repro/actions/runs/169400753) have been copied into `artifacts/` for reference.

Note that the `artifacts/windows-latest-the_notebook-latex/the_notebook.tex` file from Windows has Windows-style CRLF line endings. I converted it to Unix-style LF line endings (`artifacts/windows-latest-the_notebook-latex/the_notebook_lf.tex`), and this appears to produce identical files to the Ubuntu and MacOS runs.

```
03a09f34782ea7a18044f4a846eb753a  artifacts/macos-latest-the_notebook-latex/the_notebook_files/the_notebook_1_1.png
03a09f34782ea7a18044f4a846eb753a  artifacts/ubuntu-latest-the_notebook-latex/the_notebook_files/the_notebook_1_1.png
03a09f34782ea7a18044f4a846eb753a  artifacts/windows-latest-the_notebook-latex/the_notebook_files/the_notebook_1_1.png
0c6e074242f45693b5691122aec3950e  artifacts/macos-latest-the_notebook.pdf
43aef34985d51c5fcae20efef3b33b19  artifacts/ubuntu-latest-the_notebook.pdf
5da10de1a8757c9fdde8f74dbabc8c77  artifacts/macos-latest-the_notebook-latex/the_notebook.tex
5da10de1a8757c9fdde8f74dbabc8c77  artifacts/ubuntu-latest-the_notebook-latex/the_notebook.tex
5da10de1a8757c9fdde8f74dbabc8c77  artifacts/windows-latest-the_notebook-latex/the_notebook_lf.tex
e2d21840f02c1986fd71b3703fae6403  artifacts/windows-latest-the_notebook-latex/the_notebook.tex
```
