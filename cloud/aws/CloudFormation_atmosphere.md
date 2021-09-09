# CloudFormation

## 概要

* AWSのベーシックな構成管理サービス
* 人に書かせるのに味をしめて書いてこなかった

## CloudFormation用語

* テンプレート
  * リソースの状態を定義したテキスト
  * 依存関係はCloudFormationがいい感じに判別してくれる
  * スタックの設計図
* スタック
  * リソースの集合
  * ここから実際のリソースをまとめて作成、変更、削除する

## いい感じな作り方

* デザイナー
  * AWSコンソール上でグラフィカルにテンプレートを作成できる
* 既存リソースはFormer2という非公式サービスでテンプレート化できる
  * Webサービスに認証情報投げつけるのは嫌なのでDocker版をつかう

## テスト関連

* cfn-lint
  * linter
* TaskCat
* cfn-nag
  * サードパーティのOSS
  * セキュリティチェック
* CloudFormation Guard

## デプロイの道具

* CodePipeline
* ChangeSet
  * 変更箇所および影響を事前に確認
* StackSets
  * 一回の操作で複数のアカウント/リージョンへスタックを作成、更新、削除できる

## 参考

* [AWS CloudFormation とは - AWS CloudFormation](https://docs.aws.amazon.com/ja_jp/AWSCloudFormation/latest/UserGuide/Welcome.html)
* [20200826 AWS Black Belt Online Seminar AWS CloudFormation](https://www.slideshare.net/AmazonWebServicesJapan/20200826-aws-black-belt-online-seminar-aws-cloudformation-238501102)
  * [[AWS Black Belt Online Seminar] AWS CloudFormation 資料及び QA 公開 | Amazon Web Services ブログ](https://aws.amazon.com/jp/blogs/news/webinar-bb-aws-cloudformation-2020/)
* [AWS Hands-on for Beginners - AWS 環境のコード管理 AWS CloudFormationで Web システムを構築する | AWS](https://pages.awscloud.com/JAPAN-event-OE-Hands-on-for-Beginners-cfn-2020-reg-event-LP.html)
* [[レポート] AWS CloudFormation を作成するためのベストプラクティス #DOP302 #reInvent | DevelopersIO](https://dev.classmethod.jp/articles/best-practiceof-making-cfn-reinvent2019/)
