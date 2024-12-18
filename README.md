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






English ver

Notion Study Management Tool, Todo List, and Weather Information Retrieval System

Overview

This project is a study management and Todo list system centered around Notion. Users can input study records and Todo lists using Notion’s GUI, with data stored in Notion databases. The backend is built with Python and utilizes the Google Cloud Natural Language API to summarize data, automatically reflecting daily reviews in Notion. The entire system operates within Docker containers and is automated using GitHub Codespaces and GitHub Actions. Data visualization is achieved through Notion’s charting features.

Features
	•	Study Record Management: Easily input and manage study records using Notion’s intuitive GUI.
	•	Todo List Management: Efficiently manage tasks and visualize progress.
	•	Automated Summarization: Leverage Google Cloud Natural Language API to summarize data and generate daily reviews automatically.
	•	Data Visualization: Use Notion’s charting features to visually track study and task progress.
	•	Automation: Utilize GitHub Codespaces and GitHub Actions for CI/CD pipeline automation.
	•	Containerization: Ensure consistency and ease of deployment with Docker.
	•	Beginner-Friendly: Designed for beginners with straightforward setup and implementation.

Technology Stack
	•	Frontend: Notion
	•	Backend: Python
	•	Database: Notion Database
	•	APIs: Notion API, Google Cloud Natural Language API
	•	Automation: GitHub Codespaces, GitHub Actions
	•	Containerization: Docker
	•	Visualization: Notion’s charting features

Demo

Setup Instructions

1. Prerequisites
	•	GitHub Account
	•	Notion Account
	•	Google Cloud Account
	•	Docker installed
	•	GitHub Codespaces enabled

2. Clone the Repository

git clone https://github.com/your-username/notion-study-todo-app.git
cd notion-study-todo-app

3. Set Up GitHub Codespaces
	1.	On the GitHub repository page, click the “Code” button and select the “Codespaces” tab.
	2.	Click “New codespace” to launch the development environment.
	3.	Install necessary extensions (Python, Docker, GitHub Actions, etc.).

4. Configure Notion API
	1.	Visit Notion Developers and click “+ New integration”.
	2.	Name your integration and set the required permissions.
	3.	Submit to receive the “Internal Integration Token” and copy it.
	4.	In Notion, create databases for study records and Todo lists, and note their URLs for later use.

5. Configure Google Cloud Natural Language API
	1.	Log in to Google Cloud Console.
	2.	Navigate to “API & Services” > “Library” and enable the “Natural Language API”.
	3.	Go to “IAM & Admin” > “Service Accounts” and create a new service account.
	4.	Assign appropriate roles (e.g., Project > Editor).
	5.	Add a key by selecting “Add Key” > “Create New Key” > “JSON” and download the key file.
	6.	Save the downloaded JSON file within your project and set the path in the .env file.

6. Set Up Environment Variables

Create a .env file in the project root with the following content:

NOTION_API_TOKEN=your_notion_api_token
NOTION_DATABASE_ID=your_notion_database_id
GOOGLE_APPLICATION_CREDENTIALS=path_to_your_google_credentials.json

Note: Ensure that the .env file is added to .gitignore to prevent sensitive information from being pushed to the repository.

7. Set Up the Backend
	1.	Install Dependencies

pip install -r backend/requirements.txt


	2.	Run the Script

python backend/app.py



8. Configure Docker
	1.	Build the Docker Image

docker build -t notion-study-todo-backend backend/


	2.	Run the Docker Container

docker run --env-file .env notion-study-todo-backend


	3.	Use Docker Compose (Optional)

docker-compose up --build



9. Set Up GitHub Actions
	1.	Configure GitHub Secrets
	•	Go to the repository’s “Settings” > “Secrets and variables” > “Actions” > “New repository secret”.
	•	Add NOTION_API_TOKEN and NOTION_DATABASE_ID.
	•	If necessary, add Google Cloud credentials as secrets.
	2.	Verify CI/CD Pipeline
	•	Push changes to the main branch to trigger GitHub Actions.
	•	Check the “Actions” tab in the repository to monitor workflow runs.

10. Configure Data Visualization
	1.	In your Notion database, click “Add a view” and create views like “Table” or “Board”.
	2.	Utilize widgets or integrations (e.g., Notion Charts) to enable chart displays as needed.

Usage
	1.	Input Data in Notion
	•	Enter study records and Todo lists through Notion’s GUI.
	•	Data is automatically saved in Notion databases.
	2.	Run the Backend
	•	The backend script retrieves data from Notion via the API, summarizes it using Google Cloud Natural Language API, and updates Notion with the summaries.
	3.	View Data Visualization
	•	Check Notion’s charting features to visualize your study progress and Todo list status.

Project Structure

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

Contribution
	1.	Fork the Repository
	2.	Create a New Branch (git checkout -b feature/new-feature)
	3.	Commit Your Changes (git commit -m 'Add new feature')
	4.	Push to the Branch (git push origin feature/new-feature)
	5.	Open a Pull Request

License

This project is licensed under the MIT License. See the LICENSE file for details.

Support

If you have any questions or issues, please open an Issue.

References
	•	Notion API Documentation
	•	Google Cloud Natural Language API Documentation
	•	Docker Documentation
	•	GitHub Actions Documentation

Wishing you success with your project! Good luck 😊
