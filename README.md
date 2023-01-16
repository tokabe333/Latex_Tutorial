# LaTeX Tutorial

## 目次
- [Glossary](#glossary-用語解説)
- [TeX Environments](#tex-environments-動作確認済み)
- [Compile Command](#compile-command)
- [Windows Installation](#windows----how-to-make-latex-environment-on-your-pc)
- [Mac Installation](#mac----how-to-make-latex-environment-on-your-pc)

<br>

## Glossary (用語解説)

| 用語 | 解説 | 
| :-: | --- |
| TeX | 組版ソフトウェア<br>(それを扱うための基本的な命令を集めた言語・処理系)<br>C言語により実装| 
| LaTeX | TeXをより便利に扱うためのマクロ体系(TeXマクロの集合体)<br>TeX言語により実装| 
| Engine | マクロ体系の種類<br>platex, uplatex, pdftex 等
| TeX Live | エンジンをまとめたディストリビューション<br>TeX Liveを導入することで様々なエンジンでのコンパイルができる | 

<br>

## TeX Environments (動作確認済み)

| OS種類 | OSバージョン | 
| :-: | :-: |
| Windows | Windows10 + WSL2 (Ubuntu 22.04) |
| Mac | macOS ventura 13.01 |
| Linux | Ubuntu 22.04 | 

| 枠組み | TeX環境 | 
| :-: | :-: |
| Editor | Visual Studio Code |
| Distribution | TeX Live | 
| Engine | upLaTeX | 



<br>

## Compile Command
1. Texファイルを開く
2. ```ctrl + alt + v``` (PDFをプレビューしようとするが開けない)
3. ```ctrl + s``` (保存時にコンパイルされる，↑のコマンドを先に実行しないとコンパイルされない謎)
4. ```ctrl + alt + v``` (今度はコンパイルされているので開ける)
5. 以降は ```ctrl + s``` を押す度に自動でコンパイルされる <br>
	VS Codeを起動するたびにこの過程が必要です(良い方法があれば教えてください)

<br>

## Windows -- How to make LaTeX Environment on your PC.

**保存するたびに自動コンパイルされる環境を "ローカル" で作る** <br>

参考文献 : [VScodeでLaTeXの環境を整える](https://www.takameron.info/post/vscode_latex/ "hoge")


<br>

- 管理者権限でPowerShellを起動 <br>
	- ```wsl --install``` <br>
	(WSL2のインストール)

	- ```wsl --update``` <br>
	(すでにWSLをインストール済みの人はWSL2に更新することをオススメ)

<br>

- Microsoft Storeを起動
	- Ubuntu22.04 を検索 & インストール <br>
	(安定版は Ubuntu20.04 なのでそちらでもOK)

<br>

- Ubuntu22.04を起動
	- 以下のコマンドで必要なパッケージをインストール & フォント埋め込み設定 <br>
	  texlive-fullだと7GBぐらいあるので必要最小限のtexlive関連パッケージだけでも大丈夫です．
		```
		sudo apt update
		sudo apt upgrade
		sudo apt install texlive-full
		sudo kanji-config-updmap status
		sudo kanji-config-updmap-sys haranoaji
		``` 
	<!-- - ~/.latexmkrc 作成して以下をコピペ
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
		$ENV{TZ} = 'Asia/Tokyo';
		$ENV{OPENTYPEFONTS} = '/usr/share/fonts//:';
		$ENV{TTFONTS} = '/usr/share/fonts//:';
		
		# clean up
		$clean_full_ext = "%R.synctex.gz"
		``` -->

<br>

- VS Codeを起動
	- Remote WSLをインストール (ms-vscode-remote.remote-wsl)
	- WSLに接続
	- LaTeX Workshopをインストール (James-Yu.latex-workshop)
	- settings.jsonにRecipesやToolsは記載済みのため設定不要　<br>
	(bibtexを使わない場合はRecipesの"pbibtex"を削除すれば良い)

<br>

## Mac -- How to make LaTeX Environment on your PC.

MAC版のインストール関係

参考文献 : [Mac+VSCodeでLaTeX Workshopのフォーマットが動くようにする](https://zenn.dev/ganariya/articles/vscode-latex-indent)

- MacTeXをダウンロード & インストールする <br>
	https://www.tug.org/mactex/mactex-download.html

<!-- - ~/.latexmkrc 作成して以下をコピペ
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
	$ENV{TZ} = 'Asia/Tokyo';
	$ENV{OPENTYPEFONTS} = '/usr/share/fonts//:';
	$ENV{TTFONTS} = '/usr/share/fonts//:';
	
	# clean up
	$clean_full_ext = "%R.synctex.gz"
	``` -->

- latexindent を使用するために以下のコマンドを実行
	```
	brew install perl
	brew install cpanm
	cpanm Log::Log4perl Log::Dispatch::File YAML::Tiny File::HomeDir Unicode::GCString
	```

- VS Codeを起動
	- LaTeX Workshopをインストール (James-Yu.latex-workshop)
	- settings.jsonにRecipesやToolsは記載済みのため設定不要 <br>
	(bibtexを使わない場合はRecipesの"pbibtex"を削除すれば良い)
