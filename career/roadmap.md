# 学習ロードマップ（実践寄り）

### フェーズ1: 土台づくり（基礎文法と最小アプリ）

* **プログラミング言語**

  * TypeScript と Python を並行（TSはフロントエンド、Pythonは自動化やスクリプト用途）
  * PHPはLaravelに入る前でOK
* **フロントエンド**

  * React の基本（状態管理・イベント処理まで）
* **データベース**

  * PostgreSQLでCRUD操作を習得
* **実践課題**: Next.js＋PostgreSQLで「1行メモアプリ」をDockerで動かす

---

### フェーズ2: Webアプリの全体像を掴む

* **バックエンド**

  * Node.js/ExpressでREST APIを構築
  * Django or Laravelは後回しでも良いが、どちらか触ってみてフレームワークの流儀を知る
* **フロントエンド**

  * Next.jsのルーティング・SSR/SSGを学習
  * SEOの基礎を押さえながら自作アプリに組み込む
* **Dev/Ops**

  * Docker Composeでバックエンド＋DB＋フロントを連携
* **実践課題**: 認証つきのタスク管理アプリ（Next.js＋Express＋PostgreSQL＋Docker）

---

### フェーズ3: 運用を意識した拡張

* **Dev/Ops**

  * GitHub Actionsでテスト＋自動デプロイ
  * Kubernetesの基本（ローカルでのMinikube程度でOK）
* **クラウド**

  * AWS Lambda（小さなAPIを作る）
  * ECS/EKSにDocker化アプリをデプロイ
* **データベース強化**

  * Redisを導入してキャッシュやセッション管理を組み込む
* **実践課題**: 小規模チーム開発を想定しCI/CD＋AWSデプロイまで含めた「習慣トラッキングアプリ」

---

### フェーズ4: インフラ自動化・高度化

* **Dev/Ops**

  * Terraform or CloudFormationでインフラをコード化
* **クラウド**

  * ECS/EKS本格運用
* **バックエンド深掘り**

  * DjangoやLaravelで中規模アプリを構築して比較
* **実践課題**: 「目標達成支援アプリ」を本番レベルのインフラで運用

---

## 並行学習のおすすめ

* **セットで学ぶと効果的な組み合わせ**

  * TypeScript ↔ React/Next.js（文法とUI構築は一緒に進めるのが効率的）
  * PostgreSQL ↔ バックエンド（CRUDとAPI開発は同時にやったほうが自然）
  * Docker ↔ どのフェーズでも（常に環境構築に絡めて練習）
  * CI/CD ↔ クラウド（アプリをクラウドに出す段階で自然に必要になる）

---
