# cadentian-conlang

Solresol みたいな人工言語を作ってみたいプロジェクト。

Cadentia とはラテン語で「落ちている状態・落下」を意味する名詞で機能和声の終止形を意味する Kadenz（独）、Cadence（英）、Cadenza（伊）の語源。

Markdown テキストを Github Pages で閲覧できる。

ABC Notation をコードブロックで埋め込みが可能。

## ローカル確認

Windows環境にRubyとJekyllを導入しローカルサーバーを起動するまでの手順です。

### **Ruby+Devkit をダウンロード・インストールする:** RubyInstaller 公式サイト.
1. [RubyInstaller for Windows](https://rubyinstaller.org/downloads/) にアクセスします。
2. **「Ruby+Devkit 3.2.x」** または **「Ruby+Devkit 3.1.x」** をダウンロードします（※ Devkitがついている版を必ず選択してください）。
3. ダウンロードした `.exe` ファイルを実行し、画面の指示に従ってインストールを進めます。
4. インストール完了画面にある **「Run 'ridk install' to set up MSYS2 and development toolchain」** のチェックを入れたまま **Finish** をクリックします。


### **MSYS2 (Devkit) をセットアップする:** 自動で開く黒い画面（コマンドプロンプト）.
1. インストール直後、自動的にコンソール画面が立ち上がり、数字を選択するメニューが表示されます。
2. キーボードで `1,3` と入力して **Enter** を押します（ベース環境とビルドツールの両方がインストールされます）。
3. 処理が完了したら **Enter** を押して画面を閉じます。

> **※ 画面が開かなかった場合**
> コマンドプロンプトを開き、`ridk install` と入力して実行すれば同じ画面が開きます。


### **Bundler と Jekyll をインストールする:** ターミナル.
ターミナルで以下のコマンドを実行します。

```bash
gem install bundler jekyll
```

正常に完了したら、以下のコマンドでバージョンが表示されるか確認します。

```bash
ruby -v
gem -v
```


### **Windows向けの Gemfile 設定と動作確認:** プロジェクト直下.

JekyllがWindowsのファイル変更を高速に検知できるように、`Gemfile` に `wdm` というライブラリを追加しておきます。

**`Gemfile` の記述内容:**

```ruby
source "https://rubygems.org"

gem "github-pages", group: :jekyll_plugins

# Windows環境でのファイル監視用（CPU高負荷を防止）
gem "wdm", ">= 0.1.0", :platforms => [:x64_mingw, :mingw]
```

準備ができたら、ターミナルで以下を実行します。

```bash
# 依存ライブラリのインストール
bundle install

# ローカルサーバーの起動
bundle exec jekyll serve
```

ブラウザで `http://localhost:4000` にアクセスできれば成功です。


---

## Windows環境でよくあるエラーと対処法

### 1. 日本語（文字化け・エンコーディングエラー）が出る場合

Markdown内に日本語が含まれるとエラー（`invalid byte sequence in UTF-8` 等）になることがあります。その場合は、ターミナルで文字コードを UTF-8 に固定してから実行してください。

* **Command Prompt の場合:**
```cmd
chcp 65001
```


* **PowerShell の場合:**
```powershell
$OutputEncoding = [System.Text.Encoding]::UTF8
```



### 2. ポート `4000` が使用中と言われる場合

他のアプリがポート4000を使用している場合は、ポート番号を変更して起動できます。

```bash
bundle exec jekyll serve --port 4001
```
