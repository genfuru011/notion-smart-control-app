# notion-smart-control-app

Notion 勉強管理ツール・Todoリスト・天気情報取得システム

概要

このプロジェクトは、Notionを中心とした勉強管理ツールおよびTodoリスト管理システムです。ユーザーはNotionのGUIを利用して勉強記録やTodoリストを入力し、データはNotionデータベースに保存されます。バックエンドはPythonで構築され、Google Cloud Natural Language APIを用いてデータを要約し、1日の振り返りを自動的にNotionに反映します。システム全体はDockerコンテナ上で動作し、GitHub CodespacesとGitHub Actionsによって自動化されています。データの可視化はNotionのチャート機能を活用します。

特徴
	•	勉強記録管理: NotionのGUIを使用して簡単に勉強記録を入力・管理。
	•	Todoリスト管理: 効率的にタスクを管理し、進捗を可視化。
	•	自動要約機能: Google Cloud Natural Language APIを活用してデータを要約し、毎日の振り返りを自動生成。
	•	データ可視化: Notionのチャート機能を用いて勉強やタスクの進捗を視覚的に確認。
	•	自動化: GitHub CodespacesとGitHub Actionsを利用したCI/CDパイプラインによる自動化。
	•	コンテナ化: Dockerを使用して環境の一貫性を確保し、簡単にデプロイ可能。

技術スタック
	•	フロントエンド: Notion
	•	バックエンド: Python
	•	データベース: Notionデータベース
	•	API: Notion API, Google Cloud Natural Language API
	•	自動化: GitHub Codespaces, GitHub Actions
	•	コンテナ化: Docker
	•	可視化: Notionのチャート機能

デモ

セットアップ手順

1. 前提条件
	•	GitHub アカウント
	•	Notion アカウント
	•	Google Cloud アカウント
	•	Docker のインストール
	•	GitHub Codespaces の有効化

2. リポジトリのクローン

git clone https://github.com/your-username/notion-study-todo-app.git
cd notion-study-todo-app

3. GitHub Codespaces の設定
	1.	GitHubリポジトリページで「Code」ボタンをクリックし、「Codespaces」タブを選択。
	2.	「New codespace」をクリックして開発環境を起動。
	3.	必要な拡張機能（Python、Docker、GitHub Actionsなど）をインストール。

4. Notion API の設定
	1.	Notion Developers にアクセスし、「+ New integration」をクリック。
	2.	インテグレーションに名前を付け、必要な権限を設定。
	3.	「Internal Integration Token」をコピー。
	4.	Notion内で勉強記録用およびTodoリスト用のデータベースを作成し、各データベースのURLをメモ。

5. Google Cloud Natural Language API の設定
	1.	Google Cloud Console にログイン。
	2.	「API とサービス」→「ライブラリ」で「Natural Language API」を検索し、有効化。
	3.	「IAM と管理」→「サービスアカウント」→「サービスアカウントを作成」をクリック。
	4.	サービスアカウントに名前を付け、適切な役割（例: Project > Editor）を割り当て。
	5.	「キーを追加」→「新しいキーを作成」→「JSON」を選択し、キーをダウンロード。
	6.	ダウンロードしたJSONファイルをプロジェクト内に保存し、.env ファイルにパスを設定。

6. 環境変数の設定

プロジェクトルートに .env ファイルを作成し、以下の内容を追加：

NOTION_API_TOKEN=your_notion_api_token
NOTION_DATABASE_ID=your_notion_database_id
GOOGLE_APPLICATION_CREDENTIALS=path_to_your_google_credentials.json

7. バックエンドのセットアップ
	1.	依存関係のインストール

pip install -r backend/requirements.txt


	2.	スクリプトの実行

python backend/app.py



8. Docker の設定
	1.	Docker イメージのビルド

docker build -t notion-study-todo-backend backend/


	2.	Docker コンテナの実行

docker run --env-file .env notion-study-todo-backend


	3.	Docker Compose の使用（オプション）

docker-compose up --build



9. GitHub Actions の設定
	1.	GitHub Secrets の設定
	•	リポジトリの「Settings」→「Secrets and variables」→「Actions」→「New repository secret」をクリック。
	•	NOTION_API_TOKEN と NOTION_DATABASE_ID を追加。
	•	Google Cloudの認証情報も必要に応じて追加。
	2.	CI/CD パイプラインの確認
	•	コードを main ブランチにプッシュすると、GitHub Actionsが自動的にパイプラインを実行。
	•	「Actions」タブでワークフローの実行状況を確認。

10. データ可視化の設定
	1.	Notion データベース内で「Add a view」をクリックし、「Table」や「Board」などのビューを作成。
	2.	必要に応じてチャート表示が可能なウィジェットやインテグレーション（例: Notion Charts）を利用。

使用方法
	1.	Notionでデータ入力
	•	勉強記録やTodoリストをNotionのGUIから入力。
	•	データは自動的にNotionデータベースに保存されます。
	2.	バックエンドの実行
	•	バックエンドがNotion APIを介してデータを取得し、Google Cloud Natural Language APIで要約を生成。
	•	要約結果をNotionの該当ページに反映。
	3.	データの確認
	•	Notionのチャート機能で勉強記録やTodoリストの進捗を可視化。

プロジェクト構造

notion-study-todo-app/
├── backend/
│   ├── app.py
│   ├── requirements.txt
│   └── Dockerfile
├── .github/
│   └── workflows/
│       └── ci.yml
├── docker-compose.yml
├── .env
├── README.md
└── architecture_diagram.png

コントリビューション
	1.	Fork リポジトリ
	2.	ブランチを作成 (git checkout -b feature/新機能)
	3.	コミットを行う (git commit -m '新機能追加')
	4.	プッシュする (git push origin feature/新機能)
	5.	プルリクエストを作成

ライセンス

このプロジェクトはMITライセンスの下で公開されています。詳細は LICENSE を参照してください。

サポート

質問や問題がある場合は、Issue を開いてください。

参考資料
	•	Notion API ドキュメント
	•	Google Cloud Natural Language API ドキュメント
	•	Docker ドキュメント
	•	GitHub Actions ドキュメント

プロジェクトの成功を祈っています！頑張ってください😊
