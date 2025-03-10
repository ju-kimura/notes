# AI-102 ラボ9 会話言語理解(CLU)

Cognitive Servicesの「言語サービス」に含まれる「会話言語理解(CLU)」を使用して、現在の日付や時刻を尋ねる質問を理解できるモデルを作ります。また、それを利用して、日付や時刻を答えることができる簡単なアプリを作成します。

## .NET 7等のセットアップ

Windowsのスタートボタンを右クリックし、`Windows PowerShell (管理者)`を起動し、以下を実行します。

```ps
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://raw.githubusercontent.com/hiryamada/ai-102-lab9/main/init.ps1'))
```

これにより以下が行われます。

- .NET SDK 7.0 がインストールされます。
- OSのタイムゾーンが日本時間に設定されます。

セットアップ完了まで5分程度かかります。完了を待たず、次のステップを進めます。

## Visual Studio Codeでプロジェクトをクローン

- Visual Studio Codeを起動します。
- サンプルコードのGitリポジトリ `https://github.com/hiryamada/ai-102-lab09.git`を、任意のフォルダーへクローンします。
- クローンが完了したらOpenをクリックします。

## Azure portalを開く

- Azure portal `https://portal.azure.com` を開き、画面右「リソース」タブに表示されたユーザー名・パスワードでサインインします。
- 画面上部歯車アイコンをクリックして、表示を日本語化します。
- 以降、右側の手順書・リソース表示部分は使用しないため、画面右上の三本線アイコンをクリックして「分割ウィンドウ」をクリックし、左側のメインのウィンドウを広げると作業しやすいです。

## Langリソース作成

- 画面上部の検索で `cognitive services`を検索し、移動します。
- 画面左のメニューで「言語サービス」を選び、「作成」、「リソースの作成を続行する」をクリックします。以下を指定します。
  -  リソースグループ: 作成済みのものを選択
  - リージョン: East US
  - 名前: 任意のものを指定
  - 価格レベル: S
  - 責任あるAI通知: チェック
- 「確認と作成」、「作成」をクリックします。

## Language Studioでモデルをトレーニング、デプロイ

- `https://language.cognitive.azure.com/` を開きます。
- 画面上部歯車アイコンをクリックして、表示を日本語化します。
- 画面上部「サインイン」をクリックしてサインインします。
- 作成済みの「言語サービス」リソースを選択して「完了」をクリックします。
- 「会話言語理解を開く」をクリックします。
- 「インポート」をクリックします。
- 「ファイルの選択」をクリックし、クローンしたプロジェクト内にある`datetime.json`を選択します。
- 「完了」をクリックします
- 画面左の「トレーニングジョブ」をクリックし、「トレーニングジョブを開始する」をクリックします。
  - 「新しいモデルのトレーニング」に`datetime`を指定します。
  - 「トレーニングモード」で「高度なトレーニング」を選びます。
  - 「トレーニング」をクリックします。
- トレーニングが終わるまで10分ほどかかります。※休憩を取るとよいでしょう。
  - 「状態」に「Job in queue. Starting soon ...」と表示された場合、トレーニングジョブの開始を待っています。
  - 「状態」に「Training - NN% complete. Evaluation - NN% complete.」と表示された場合、トレーニングジョブが進行中です。
  - 「状態」に「トレーニングに成功しました」と表示された場合、トレーニングジョブは完了しています。
- 画面左の「モデルをデプロイ」をクリックします。
  - 「デプロイの追加」をクリックし、デプロイ名に`datetime`を入力します。
  - トレーニング済みモデルで`datetime`を選択します。
  - 「デプロイ」をクリックします。デプロイは10秒ほどで完了します。

## エンドポイントとキーを設定

- Visual Studio Codeに切り替えます。
- パレットから`Terminal: Create New Integrated Terminal (With Profile)`を選択し、`Git Bash`を選択します。
- `Git Bash`ターミナル内で以下を実行します。
  - `az login`
  - `bash set-secrets.sh`

## 実行

- `Git Bash`ターミナル内で以下を実行します。
  - `bash datetime-sample.sh`
- 現在の日付や時刻を尋ねる質問の文章が「言語サービス」に送信されます。「会話言語理解(CLU)」を使用して、質問の文章から意図（Intent）を取得します。意図に基づき、対応する処理（日付または時刻を答える）が実行されます。

## 以上です。お疲れ様でした！
