## 使用した技術
サーバーサイド：PHP7.4、Laravel6系  
フロント周り：HTML、CSS、Vue.js  
ソース管理：Git、Github  
インフラ：AWS  

## 技術詳細
### バックエンドLaravelで使用したライブラリ
`fruitcake/laravel-cors`：認証で外部からのアクセスを許可するために使用  
`laravel/sanctum`：SPA認証で使用  
`intervention/image`：画像をリサイズして保存する際に使用  
`laravel/ui`：フロントエンド開発のベース  
`league/flysystem-aws-s3-v3`：AmazonS3画像アップロード用  
`pusher/pusher-php-server`：イベントをPusherでブロードキャスト  
`phpunit/phpunit`：テストコード用  
### フロントエンドVue.jsで使用したライブラリ
`vue`：フロントエンド用Vue.jsベース素材  
`vue-router`：SPA構築のためのルーティングを行う  
`laravel-mix`：フロントエンド素材をコンパイル  
`vue-click-outside`：要素の外側のクリックを探知  
`laravel-echo`：Pusherの利用に必要  
`pusher-js`：Pusherの利用に必要  
### インフラAWS
`VPC`：領域作成。パブリックサブネットにEC2、プライベートサブネットにRDSを配置。  
`EC2`：Laravelアプリ、Nginxサーバー  
`RDS`：MySQLデータベース  
`Route53`：独自ドメイン作成  
`ACM`：SSL化  
`ALB`：「https」のURLでEC2に接続させる

## 実装した機能一覧
* ログイン認証。
* シングルページアプリケーション化。
* なるべくSQLの発行回数を抑え、N+1問題が発生しないよう意識してコードを書きました。
* レスポンシブ対応。
### 投稿
* 投稿のCRUD。
* ジャンル選択。
* 多対多のリレーションでタグ付け。
* 複数枚画像アップロード（プレビュー可）。

### いいね・コメント
* いいね（当アプリでは「どんまい」と呼んでいます）。
* コメント。コメントへの返信。コメントと返信へのいいね。
* コメントはモーダルにて無限スクロールで取得。
* 各投稿にいいね（どんまい）したユーザー一覧。無限スクロールで取得。

### 投稿取得
* 無限スクロールで取得。
* ホームではフォローしたユーザーの投稿（自分の投稿も含む）を優先的に取得。
* ジャンル別投稿一覧。
* ここ１週間以内の投稿に紐つけられたタグ数のランキング表示。
* タグ別投稿一覧（新着順・人気順）。
* ここ１週間以内の投稿をいいね（どんまい）数が多い順で取得。

### チャットルーム
* チャットルーム（当サービスでは「グチ部屋」と呼ぶ）の作成・削除。ジャンル選択、アイコン画像設定が可能。
* チャットルームを新着順・人気順・ジャンル別で取得。
* チャットルーム一覧のページネーション。
* チャットルームのブックマーク。

### リアルタイムチャット
* 作成したチャットルーム内でページリロードなしでのリアルタイムチャット。
* 匿名・非匿名の選択可能。
* 複数枚画像アップロード。
* 各チャット（当サービスでは「グチ」と呼ぶ）へのいいね。
* 過去のチャットは無限スクロールで取得。

### ユーザー関連
* フォロー。
* 各ユーザーのフォロー、フォロワー一覧。
* 各ユーザーの投稿、いいね（どんまい）した投稿、ブックマークしたチャットルーム（グチ部屋）の閲覧。
* プロフィール編集。
* パスワード変更。

### テストコード
* factoryなどを使って、コントローラーの各メソッドのテストを書きました。