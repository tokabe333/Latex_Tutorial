# Latex_Tutorial
 Latex勉強用リポジトリ


## Tex Environments

| Subject | Text | 
| --- | --- |
| OS | Ubuntu 22.04 (WSL2) |
| Editor | Visual Studio Code |

<br>

## Installation(?) -- How to make the environment

<br>

#### 参考文献 : [VScodeでLaTeXの環境を整える](https://www.takameron.info/post/vscode_latex/ "hoge")

<br>

- 管理者権限でPowerShellを起動 <br>
	- ```wsl --install```

<br>

- Microsoft Storeを起動
	- Ubuntu22.04 を検索 & インストール

<br>

- Ubuntu22.04を起動
	- 以下のコマンドで環境必要なパッケージをインストール
		```
		sudo apt update
		sudo apt upgrade
		sudo apt install texlive-full
		``` 
	- ~/.latexmkrc 作成して以下をコピペ
		```
		#!/usr/bin/env perl
		$latex            = 'uplatex -shell-escape -kanji=utf8 -synctex=1 -halt-on-error -interaction=nonstopmode -file-line-error %O %S';
		$latex_silent     = 'uplatex -shell-escape -kanji=utf8 -synctex=1 -halt-on-error -interaction=batchmode %O %S';
		$bibtex           = 'pbibtex %O %S';
		$biber            = 'biber --bblencoding=utf8 -u -U --output_safechars';
		$dvipdf           = 'dvipdfmx %O -o %D %S';
		$makeindex        = 'mendex %O -o %D %S';
		$max_repeat       = 5;
		$pdf_mode         = 3;
		$pvc_view_file_via_temporary = 0;
		# clean up
		$clean_full_ext = "%R.synctex.gz"
		```

<br>

- VS Codeを起動
	- Remote WSLをインストール (ms-vscode-remote.remote-wsl)
	- WSLに接続
	- LaTeX Workshopをインストール (James-Yu.latex-workshop)
	- settings.jsonはこのリポジトリにあるので設定不要