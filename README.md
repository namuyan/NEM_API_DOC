# New Economy Movement(NEM) APIマニュアル和訳

NEM公式APIマニュアルの日本語訳。
New Economy Movement(NEM) APIマニュアル和訳
新経済運動(NEM - New Economy Movement)のAPIマニュアル和訳。

**この文章について、本来[pr1smさんのサイト](https://www.pr1sm.com/crypto-coin/nem-nis-api-documentation-in-japanese/)に掲載されていましたが削除されました。そこで残存していたキャッシュより復元しここに残します。**

## New Economy Movement

暗号通貨にはビットコインに追従する形で多くの代替コイン(オルトコイン)が存在し、これらコインはそれぞれ異なった性質を持ち、またそれぞれ別の目標や信念を掲げて開発が続けられています。

2017年3月6日現在で[時価総額が107,137,800ドル](https://coinmarketcap.com/currencies/nem/)(100億円以上)を突破した、新経済運動([NEM](https://www.nem.io/) – New Economy Movement)と呼ばれる暗号通貨もその内の一つです。

NEMはその名前が表すように、金銭の自由、分散化、公平と平等の原則に基づき、新たな経済圏を生み出す事を目標として[始まったプロジェクト](https://bitcointalk.org/index.php?topic=426303.0)です。

詳細を語ると非常に長くなるため、ここでは省きますが、気になった方は[http://www.cryptostream.jp/nem_xem/](http://www.cryptostream.jp/nem_xem/)にて詳細が記載されていますので、是非ご覧下さい。

さて、記事のタイトルにもあるように、今回はNEM公式APIマニュアルの日本語翻訳を行いました。

これはNEMの任意団体である[NEM UDON FOUNDATION](https://sites.google.com/view/udon-foundation/)によるNEM公式APIマニュアルの[和訳依頼](https://sites.google.com/view/udon-foundation/%E5%A0%B1%E5%A5%A8%E9%87%91%E5%88%B6%E5%BA%A6/wanted)を受けたものであり、ソフトウェアライセンスの[MIT Licence](https://opensource.org/licenses/MIT)に沿って公開されています。

読みやすさを考慮しつつもなるべく原文との正確性も保つよう和訳を行っていますが、多少ズレがある可能性も考えられるため、より正しい内容を求める方は[公式マニュアル](http://bob.nem.ninja/docs/)を読むことをおすすめします。

また、この記事は暫定的なものであるため、後に修正される場合があります。

※3月14日に[検証が開始](https://twitter.com/udon_crypto/status/841439749097234432)されています。

## (本文前に)簡単な3行まとめ

+ NEM公式APIマニュアルを和訳。
+ 正しい情報を求める場合は公式ページの閲覧を推奨。
+ 暫定的であるため、今後変更の可能性あり。

## NEM NIS API ドキュメンテーション

バージョン：1.18

作成日時(公式)：2015年11月6日16時43分

公式APIマニュアル：[http://bob.nem.ninja/docs/](http://bob.nem.ninja/docs/)

## 目次

1.  1.[イントロダクション](#introduction)

    1.  1.1.[一般情報](#general-information)
    2.  1.2.[インストール手順](#installation)
    3.  1.3.[リクエスト](#requests)
2.  2.[NISのステータスに関連するリクエスト](#NIS-status-related-requests)

    1.  2.1.[ハートビートリクエスト](#heart-beat-request)
    2.  2.2.[ステータスリクエスト](#status-request)
3.  3.[アカウントに関連するリクエスト](#account-related-requests)

    1.  3.1.[アカウントデータの取得](#retrieving-account-data)

    1.  3.1.1.[新しいアカウントデータの生成](#generating-new-account-data)
    2.  3.1.2.[アカウントデータのリクエスト](#requesting-the-account-data)
    3.  3.1.3.[委任アカウントのオリジナルデータリクエスト](#requesting-the-original-account-data-for-a-delegate-account)
    4.  3.1.4.[アカウントステータスのリクエスト](#requesting-the-account-status)
    5.  3.1.5.[アカウントのトランザクションデータリクエスト](#requesting-transaction-data-for-an-account)
    6.  3.1.6.[デコードされたメッセージによるトランザクションデータ](#transaction-data-with-decoded-messages)
    7.  3.1.7.[アカウントの収穫情報データリクエスト](#requesting-harvest-info-data-for-an-account)
    8.  3.1.8.[アカウントの重要度情報の取得](#retrieving-account-importances-for-accounts)
    9.  3.1.9.[アカウントが所有するネームスペースの取得](#retrieving-namespaces-that-an-account-owns)
    10.  3.1.10.[アカウントが作成したモザイク定義を取得](#retrieving-mosaic-definitions-that-an-account-has-created)
    11.  3.1.11.[アカウントが所有するモザイクを取得](#retrieving-mosaics-that-an-account-owns)
    12.  3.1.12.[アカウントのロックとロック解除](#locking-and-unlocking-accounts)
    13.  3.1.13.[ロック解除情報の取得](#retrieving-the-unlock-info)
    2.  3.2.[アカウントの履歴データ検索](#retrieving-historical-account-data)
4.  4.[ブロックチェーン関連のリクエスト](#block-chain-related-requests)

    1.  4.1.[ブロックチェーンステータス情報のリクエスト](#requesting-the-block-chain-status-information)

    1.  4.1.1.[ブロックチェーンの高さ](#block-chain-height)
    2.  4.1.2.[ブロックチェーンスコア](#block-chain-score)
    3.  4.1.3.[ブロックチェーンスコアラストブロック](#last-block-of-the-block-chain-score)
    2.  4.2.[ブロックチェーンの一部リクエスト](#requesting-parts-of-the-block-chain)

    1.  4.2.1.[指定されたハッシュでブロックを取得する](#getting-a-block-with-a-given-hash)
    2.  4.2.2.[指定した高さでブロックを取得する](#getting-a-block-with-a-given-height)
    3.  4.2.3.[チェーンの一部を取得する](#getting-part-of-a-chain)
5.  5.[ノード関連のリクエスト](#node-related-requests)

    1.  5.1.[ノードに関する情報のリクエスト](#requesting-information-about-a-node)

    1.  5.1.1.[基本ノード情報](#basic-node-information)
    2.  5.1.2.[拡張ノード情報](#extended-node-information)
    2.  5.2[ノードの近辺を発見するリクエスト](#request-for-discovering-the-neighborhood-of-a-node)

    1.  5.2.1.[完全な近辺](#complete-neighborhood)
    2.  5.2.2.[到達可能な近辺](#reachable-neighborhood)
    3.  5.2.3.[稼働中の近辺](#active-neighborhood)
    4.  5.2.4.[稼働している近辺の最大チェーンの高さ](#maximum-chain-height-in-the-active-neighborhood)
    3.  5.3.[ノードエクスペリエンスのリクエスト](#requesting-node-experiences)
    4.  5.4.[ローカルノードの起動](#booting-the-local-node)
6.  6.[ネームスペースとモザイク](#namespaces-and-mosaics)

    1.  6.1.[ネームスペース](#namespaces)

    1.  6.1.1.[ルートネームスペースの取得](#retrieving-root-namespaces)
    2.  6.1.2.[特定のネームスペースを取得](#retrieving-a-specific-namespace)
    2.  6.2.[モザイク](#mosaics)

    1.  6.2.1.[モザイク定義の取得](#retrieving-mosaic-definitions)
7.  7.[トランザクションの開始](#initiating-transactions)

    1.  7.1.[トランザクションの開始](#initiating-a-transaction)
    2.  7.2.[転送トランザクションの開始](#initiating-a-transfer-transaction)

    1.  7.2.1.[転送トランザクションバージョン1](#version-1-transfer-transactions)
    2.  7.2.2.[転送トランザクションバージョン2](#version-2-transfer-transactions)
    3.  7.3.[アカウントをマルチシグアカウントに変換する](#converting-an-account-to-a-multisig-account)
    4.  7.4.[マルチシグトランザクションの開始](#initiating-a-multisig-transaction)

    1.  7.4.1.[マルチシグトランザクションの署名](#cosigning-multisig-transaction)
    5.  7.5.[署名者の追加と削除](#adding-and-removing-cosignatories)
    6.  7.6.[マルチシグアカウントの使用方法](#how-to-use-a-multisig-account)
    7.  7.7.[ネームスペースの準備](#provisioning-a-namespace)
    8.  7.8.[モザイクの作成](#creating-mosaics)

    1.  7.8.1.[モザイク定義の作成](#creating-a-mosaic-definition)
    2.  7.8.2.[モザイク定義を変更する](#altering-a-mosaic-definition)
    3.  7.8.3.[モザイク供給の変更](#changing-the-mosaic-supply)
    9.  7.9.[署名付きトランザクションの作成](#creating-a-signed-transaction)

    1.  7.9.1.[署名用データの収集](#gathering-data-for-the-signature)
    2.  7.9.2.[NISにデータを送信する](#sending-the-data-to-NIS)
    10.  7.10.[トランザクション手数料](#transaction-fees) 
8.  8.[NISからの追加情報要求](#requests-for-additional-information-from-NIS)

    1.  8.1.[ネットワーク時間の監視](#monitoring-the-network-time)
    2.  8.2.[受信および送信コールの監視](#monitoring-incoming-and-outgoing-calls)
    3.  8.3.[時間監視](#monitoring-timers)
9.  9.[JSON構造の概要](#appendix-A:-description-of-the-JSON-structures)

    1.  9.1.[アカウント履歴データビューモデル](#accountHistoricalDataViewModel)
    2.  9.2.[アカウント重要度ビューモデル](#accountImportanceViewModel)
    3.  9.3.[アカウント情報](#accountInfo)
    4.  9.4.[アカウントメタデータ](#accountMetaData)
    5.  9.5.[アカウントメタデータペア](#accountMetaDataPair)
    6.  9.6.[アカウントメタデータペア](#accountPrivateKeyTransactionsPage)
    7.  9.7.[アプリケーションメタデータ](#applicationMetaData)
    8.  9.8.[監査収集](#auditCollection)
    9.  9.9.[ブロック](#block)
    10.  9.10.[ブロックチェーンスコア](#blockChainScore)
    11.  9.11.[ブロックの高さ](#blockHeight)
    12.  9.12.[ブートノードリクエスト](#bootNodeRequest)
    13.  9.13.[通信タイムスタンプ](#communicationTimeStamps)
    14.  9.14.[エクスプローラブロックビューモデル](#explorerBlockViewModel)
    15.  9.15.[エクスプローラ転送ビューモデル](#explorerTransferViewModel)
    16.  9.16.[拡張ノードエクスペリエンスペア](#extendedNodeExperiencePair)
    17.  9.17.[収穫情報](#harvestInfo)
    18.  9.18.[キーペアビューモデル](#keyPairViewModel)
    19.  9.19.[トランザクションオブジェクト](#transaction-objects)

    1.  9.19.1.[重要度転送トランザクション](#importanceTransferTransaction)
    2.  9.19.2.[モザイク定義作成トランザクション](#mosaicDefinitionCreationTransaction)
    3.  9.19.3.[モザイク供給変更トランザクション](#mosaicSupplyChangeTransaction)
    4.  9.19.4.[マルチシグ集計変更トランザクション](#multisigAggregateModificationTransaction)
    5.  9.19.5.[マルチシグ署名者変更](#multisigCosignatoryModification)
    6.  9.19.6.[マルチシグ署名トランザクション](#multisigSignatureTransaction)
    7.  9.19.7.[マルチシグトランザクション](#multisigTransaction)
    8.  9.19.8.[ネームスペーストランザクションの準備](#provisionNamespaceTransaction)
    9.  9.19.9.[転送トランザクション](#transferTransaction)
    20.  9.20.[モザイク](#mosaic)
    21.  9.21.[モザイク定義](#mosaicDefinition)
    22.  9.22.[モザイク定義メタデータペア](#mosaicDefinitionMetaDataPair)
    23.  9.23.[モザイクプロパティ](#mosaicProperties)
    24.  9.24.[モザイク徴収](#mosaicLevy)
    25.  9.25.[モザイクId](#mosaicId)
    26.  9.26.[ネームスペース](#namespace)
    27.  9.27.[ネームスペースメタデータペア](#namespaceMetaDataPair)
    28.  9.28.[Nemアナウンス結果](#nemAnnounceResult)
    29.  9.29.[Nem非同期タイマービジター](#nemAsyncTimerVisitor)
    30.  9.30.[Nemリクエストリザルト](#nemRequestResult)
    31.  9.31.[NISノード情報](#nisNodeInfo)
    32.  9.32.[ノード](#node)
    33.  9.33.[ノード収集](#nodeCollection)
    34.  9.34.[秘密鍵](#privateKey)
    35.  9.35.[リクエストアナウンス](#requestAnnounce)
    36.  9.36.[アナウンス準備のリクエスト](#requestPrepareAnnounce)
    37.  9.37.[時刻同期結果](#timeSynchronizationResult)
    38.  9.38.[トランザクションメタデータ](#transactionMetaData)
    39.  9.39.[トランザクションメタデータペア](#transactionMetaDataPair)
    40.  9.40.[未確認トランザクションメタデータ](#unconfirmedTransactionMetaData)
    41.  9.41.[未確認トランザクションメタデータペア](#unconfirmedTransactionMetaDataPair)
    42.  9.42.[エラーオブジェクト](#error-object)
10. 10.[NISエラー](#appendix-B:-NIS-errors)

    1.  10.1.[エラーメッセージ](#error-messages)

## 1.イントロダクション

公式情報：[Introduction](http://bob.nem.ninja/docs/#introduction)

### 1.1.一般情報

公式情報：[General Information](http://bob.nem.ninja/docs/#general-information)

NEMインフラストラクチャーサーバー(NIS – NEM Infrastructure Server)はJavaで記述されており、実行するにはJava 8が必要です。

Java仮想マシンの場合、少なくとも512MBのメモリで実行可能ですが、少なくとも1GBを推奨します。

### 1.2.インストール手順

公式情報：[Installation](http://bob.nem.ninja/docs/#installation)

NISは[http://bob.nem.ninja/installer/](http://bob.nem.ninja/installer/)からインストーラ経由でのインストール、もしくは[http://bob.nem.ninja/](http://bob.nem.ninja/)でホストされているスタンドアロンパッケージからそれぞれインストール出来ます。

インストーラはJavaの64ビットバージョンのみをサポートしています。

現在のスタンドアロンバージョンは、[nis-ncc-0.5.13.tgz](http://bob.nem.ninja/nis-ncc-0.5.13.tgz)です(**2017年3月7日現在の最新版は[http://bob.nem.ninja/nis-ncc-0.6.84.tgz](http://bob.nem.ninja/nis-ncc-0.6.84.tgz)です**)。

インストーラを使用する場合はソフトウェアのインストールと起動は自動的に行われます。

スタンドアロン版は選択したディレクトリに解凍する必要があります。コマンドプロンプトからrunNis.bat(windows)またはnix.runNis.sh(linux)を実行して起動します。

### 1.3.リクエスト

公式情報：[Requests](http://bob.nem.ninja/docs/#requests)

NISはクライアントと通信するためにポート7890番を使用します。また、HTTP GETとPOSTの両方のリクエストを受け付けています。

NISがローカルで実行されていると仮定すると、HTTP GETリクエストはブラウザから実行され次の形式になります。

*   例：`http://127.0.0.1:7890<path to API request>?<parameters>`
*   http://127.0.0.1:7890/account/get?address=TALICELCD3XPH4FFI5STGGNSNSWPOTG5E4DS2TOS

通常、HTTP POSTリクエストは実行可能なプラグインを使用しない限りブラウザ内では実行できません。

HTTP POSTリクエストはリクエスト本体のJSON構造を使用することでNISにデータを供給します。

JSON構造を使用してデータが返された場合、両方のリクエストタイプを返還します。

[JSON構造の概要](#appendix-A:-description-of-the-JSON-structures)ではこの文書で使用されている全てのJSONの構造について説明しています。

## 2.NISのステータスに関連するリクエスト

公式情報：[NIS status related requests](http://bob.nem.ninja/docs/#NIS-status-related-requests)

NISの状態に関する情報を得る方法として、2つのリクエストがあります。

ハートビート(/heartbeat)リクエストは、ノードが起動して応答性がある場合に情報を提供します。

ステータス(/status)リクエストは、NISの状態に関するより詳細な情報を提供します。

どちらの要求もNemリクエストリザルトオブジェクト(NemRequestResult)を返します。 

Nemリクエストリザルトの詳細については、[Nemリクエストリザルト](#nemRequestResult)を参照してください。

### 2.1.ハートビートリクエスト

公式情報：[Heart beat request](http://bob.nem.ninja/docs/#heart-beat-request)

*   APIパス：/heartbeat
*   リクエストタイプ：GET
*   概要：NISが稼動しているかどうかを判断します。
*   パラメータ：無し。
*   例：http://127.0.0.1:7890/heartbeat
*   返されるJSONオブジェクトの例

```json
{
    "code": 1,
    "type": 2,
    "message": "ok"
}
```

可能性のあるエラー：このリクエストに対する応答がない場合、NISは実行されていないか、リクエストを処理できない状態になっています。

### 2.2.ステータスリクエスト

公式情報：[Status Request](http://bob.nem.ninja/docs/#status-request)

*   APIパス：/status
*   リクエストタイプ：GET
*   概要：NISの状態を測定します。
*   パラメータ：無し。
*   例：http://127.0.0.1:7890/status
*   返されるJSONオブジェクトの例

```json
{
    "code": 6,
    "type": 4,
    "message": "status"
}
```

コードは次のように解釈出来ます。
*   *   0：不明なステータス。
    *   1：NISは停止しています。
    *   2：NISは起動しています。
    *   3：NISは動作しています。
    *   4：NISはローカルノードを起動しています(NISが実行中であることを意味します)。
    *   5：ローカルノードがブートされています(NISが実行中であることを意味します)。
    *   6：ローカルノードが同期しています(NISが実行中で、ローカルノードが起動していることを意味します)。
    *   7：NISローカルノードがリモートNISノードを認識しません(実行中および起動中を意味します)。
    *   8：現在NISはデータベースからブロックチェーンをロードしています。この状態ではNISはリクエストを処理できません。可能性のあるエラー：このリクエストに対する応答がない場合、NISは実行されていないか、リクエストを処理できない状態になっています。

## 3.アカウントに関連するリクエスト

公式情報：[Account related requests](http://bob.nem.ninja/docs/#account-related-requests)

この章ではNEMインフラストラクチャーサーバー(NEM Infrastructure Server)からアカウント情報を取得するプロセスについて説明します。

取得できる情報は永続的なアカウントデータそしてそのメタデータ、トランザクションおよびハーベストブロックに関する情報です。

また、NISは2つの異なる種類のアカウントをサポートしています：通常アカウントおよびマルチシグ(multsig – multi signature)アカウント。

*   通常アカウント
*   

通常アカウントは秘密鍵によって作成され、制御されます。

トランザクションの転送を経由して別のアカウントにNEMを送信するなど、アカウントごとのアクションはこの秘密鍵で署名されています。

もし攻撃者が秘密鍵の情報を得た場合はアカウントを奪うことができます。したがって秘密鍵は必ず秘密にしておく必要があります。
マルチシグアカウント
*   

マルチシグアカウントは通常アカウントを集計変更トランザクションを介してマルチシグアカウントに変換することで作成可能です。

これによってアカウントに署名者が追加されます。

変更後はその署名者だけがアカウントのアクションを開始することが出来ますが、どのようなアクションでも全ての署名者による著名が必要となります。

この結果、マルチシグアカウントは通常アカウントよりも大幅に安全がもたらされます。

恒久性のあるアカウントデータは他のデータベースに格納されるか、他のデータベースサーバから割り出されます。

対応するJSONオブジェクトについては[アカウント情報](#accountInfo)を参照してください。これにはフィールド値があります。

*   アドレス(address)：各アカウントには固有のアドレスがあります。 アドレスの最初の文字はアカウントが属するネットワークを示します。 現在アカウントアドレスが大文字Tで始まるテストネットワークと、アカウントアドレスが常に大文字Nで始まるメインネットワークの2つのネットワークが定義されています。アドレスの長さは常に40文字で、[base32](http://en.wikipedia.org/wiki/Base32)にエンコードされます。
*   balance：各アカウントにはゼロ以上の整数を持ったマイクロNEMの数を示す残高を所持しています。したがって、123456789の残高はアカウントが123.456789 NEMを所有していることを意味します。残高には確定部分および未確定部分に分かれており、確定部分のみが重要度計算に関連しています。ある残高から他の残高へ振替する場合には残高そのものが関連します。
*   importance：各アカウントには重要度が割り当てられており、重要度には0と1が用いられます。これはハーベスティングが有効になっている場合に次のブロックを収穫するアカウントの確率を示します。なお、重要度を計算するための正確な公式はまだ公開されておらず、またアカウントの重要度計算には最低10000のNEMを所持している必要があります。
*   publicKey：アカウントの公開鍵を使用してそのアカウントの署名を検証することができます。 すでにトランザクションを公開しているアカウントのみがそのアカウントに割り当てられた公開鍵を持っています。 それ以外の場合、フィールドはNULLとなっています。
*   ラベル(label)：このフィールドはまだ使用されておらず、常にnullです。
*   ハーベストブロック(harvestedBlocks)：ハーベスティングは新しいブロックを生成するプロセスです。フィールドはこれまでアカウントが収穫したブロックの数を示します。新しいアカウントの場合は数値は0です。

アカウントのメタデータはアカウントのハーベスティング状況を表し、アカウントが少なくとも1つのマルチシグアカウントの署名者である場合、そのマルチアカウントのリストも含まれます。

また、アカウントは現在の重要度でハーベスティングを行うか、リモートアカウントにハーベスティングを委任することができます。後者の場合は収穫する元の残高の重要性を使用します。

対応するJSONオブジェクトとstatus / remoteStatusの値については[アカウントメタデータペア](#accountMetaDataPair)を参照してください。 

メタデータは以下のフィールドで構成されています。

*   status：このフィールドはアカウントの収穫状況を示します。
*   remoteStatus：このフィールドにはリモートハーベスティングのステータスが表示されます。
*   cosignatoryOf：アカウントが署名しているマルチシグアカウントのアカウント情報(AccountInfo)構造の配列を表しています。

既知のアカウントには少なくとも1つの入力トランザクションがあります。対応するJSONオブジェクトについては[トランザクション](#transaction)、[トランザクションメタデータ](#transactionMetaData)、および[トランザクションメタデータペア](#transactionMetaDataPair)で説明しています。

トランザクションには常に次のフィールドがあります。

*   timeStamp：ネメシスブロックの作成から経過した秒数で、将来のタイムスタンプは許可されません。トランザクション検証は将来のタイムスタンプを検出した場合にエラーを返します。ネットワーク時間同期はトランザクションを作成するときにNEMソフトウェアコンポーネントが有効なタイムスタンプを使用することを保証します。
*   signature：トランザクション署名。トランザクション署名はフィールド署名者の提供された公開鍵を使用して検証されます。署名が有効でない場合にはエラーが返されます。
*   fee：トランザクションの手数料。料金が高いほどトランザクションの優先順位が高くなります。高優先度のトランザクションは優先度の低いトランザクションよりも前にブロックに含まれます。送信者に十分な残高がない場合はエラーが発生します。
*   type：トランザクションタイプ。 現在、次のタイプのトランザクションがサポートされています。
*   *   0x101：送信者から受信者のNEM転送。
    *   0x801：送信者からリモートアカウントへ重要度の転送。
    *   0x1001：集計変更トランザクション。通常アカウントをマルチシグアカウントに変換します。
    *   0x1002：マルチシグトランザクションに署名するために使用されるマルチシグ署名トランザクション。
    *   0x1003：マルチシグトランザクションで、マルチシグアカウントに使用されます。deadline：トランザクションの期限。deadlineはネメシスブロックの作成から経過した秒数で与えられます。締め切りに達する前にトランザクションがブロックに含まれない場合、トランザクションは削除されます。
*   version：構造のバージョン。 以下のバージョンが現在サポートされています。
*   *   0x68 < 24="" +="">
    *   0x98 < 24="" +="">signer：トランザクションを作成したアカウントの公開鍵。公開鍵は16進文字列としてエンコードされます。
*   トランザクションのタイプに応じて、特定のタイプに固有の追加フィールドがあります。例えば転送トランザクションには追加フィールドがあります。

recipient：受信者のアドレス。アドレスが有効でない場合はエラーが返されます。
*   message：オプションとして、トランザクション転送にメッセージを含めることができます。
*   payload：トランザクションにメッセージが含まれている場合のオプションフィールド。payloadは実際の(出来る限り暗号化された)メッセージデータです。payloadの最大サイズは512バイトです。トランザクションの検証では制限を超えたかどうかが検出され、超えた場合にはエラーが返されます。
*   type：トランザクションにメッセージが含まれている場合のオプションフィールド。 このフィールドはメッセージの情報を保持します。用意されたメッセージの種類は次のとおりです。
*   *   1：メッセージは暗号化されていません。(1: The message is not encrypted.)
    *   2：メッセージは暗号化されています。(2: The message is encrypted.)

それぞれのトランザクションタイプとその追加フィールドの詳細についてはJSON構造の概要([Description of the JSON Structures](#appendix-A:-description-of-the-JSON-structures))を参照して下さい。

トランザクションメタデータには、次のフィールドのみが含まれます。

*   height：トランザクションが含まれていたブロックの高さ。
*   id：トランザクションのID。
*   hash：トランザクションのハッシュ。

アカウント所有者は運が良ければ新しいブロックを収穫することができます。ブロックを収穫する残高はブロック内のトランザクションに含まれる料金を徴収します。

ブロックによっては収穫された情報をアカウントはリクエストすることができます。リクエストは収穫情報(HarvestInfo) JSONオブジェクトの配列を返します。

例については[ハーベスト情報](#harvestInfo)を参照して下さい。

収穫情報オブジェクトには、次のフィールドがあります。

*   timeStamp：ネメシスブロックの作成から経過した秒数。
*   id：ブロックのデータベースID。
*   difficulty：ブロックの難易度。
*   totalFee：ブロックを収穫して集められた合計手数料。
*   height：収穫されたブロックの高さ。

すべてのアカウントの重要度情報を配列にリクエストすることができます。 リクエストはアカウント重要度ビューモデル(AccountImportanceViewModel) JSONオブジェクトの配列を返します。例については[アカウント重要度ビューモデル](#accountImportanceViewModel)を参照して下さい。

アカウント重要度ビューモデルには、次のフィールドがあります。

*   address：アカウントのアドレス。
*   importance：アカウントの重要性を示す部分構造。
*   isSet：フィールド ”score” ”ev”および”height”が使用可能かどうかを示します。isSetの値は0または1です。isSetが0の場合はフィールドを使用できません。
*   score：アカウントの重要性を表します。重要度の範囲は0?1です。
*   ev：重要度のページランク部分。ページランクは0と1の間の範囲です。
*   height：重要度計算が実行された高さ。

### 3.1.アカウントデータの取得

公式情報：[Retrieving account data](http://bob.nem.ninja/docs/#retrieving-account-data)

#### 3.1.1.新しいアカウントデータの生成

公式情報：[Generating new account data](http://bob.nem.ninja/docs/#generating-new-account-data)

*   APIパス：/account/generate
*   リクエストタイプ：GET
*   概要：キーペアビューモデル([keyPairViewModel](#keyPairViewModel))を作成します。
*   パラメータ：無し。
*   例：http://127.0.0.1:7890/account/generate
*   返されるJSONオブジェクトの例

```json
{
    "privateKey": "0962c6505d02123c40e858ff8ef21e2b7b5466be12c4770e3bf557aae828390f",
    "address": "NCKMNCU3STBWBR7E3XD2LR7WSIXF5IVJIDBHBZQT",
    "publicKey": "c2e19751291d01140e62ece9ee3923120766c6302e1099b04014fe1009bc89d3"
}
```

可能性のあるエラー：無し。

#### 3.1.2.アカウントデータのリクエスト

公式情報：[Requesting the account data](http://bob.nem.ninja/docs/#requesting-the-account-data)

*   APIパス：/account/get
*   リクエストタイプ：GET
*   概要：アカウントメタデータペア([AccountMetaDataPair](#accountMetaDataPair))を取得します。
*   パラメータ：address：アカウントのアドレス。
*   例：http://127.0.0.1:7890/account/get?address=TALICELCD3XPH4FFI5STGGNSNSWPOTG5E4DS2TOS
*   返されるJSONオブジェクトの例

```json
{
	"account": {
		"address": "TALICELCD3XPH4FFI5STGGNSNSWPOTG5E4DS2TOS",
		"balance": 124446551689680,
		"vestedBalance": 104443451691625,
		"importance": 0.010263666447108395,
		"publicKey": "a11a1a6c17a24252e674d151713cdf51991ad101751e4af02a20c61b59f1fe1a",
		"label": null,
		"harvestedBlocks": 645
	},
	"meta": {
		"cosignatoryOf": [],
		"cosignatories": [],
		"status": "LOCKED",
		"remoteStatus": "ACTIVE"
	}
}
```

可能性のあるエラー：addressパラメータが有効でない場合、NISはエラーを返します。エラーの詳細についてはNISエラー([NIS Errors](#appendix-B:-NIS-errors))を参照してください。

また、アカウントの公開鍵を提供することで、アカウントデータを取得することもできます。

*   APIパス：/account/get/from-public-key
*   リクエストタイプ：GET
*   概要：アカウントメタデータペア([AccountMetaDataPair](#accountMetaDataPair))を取得します。
*   パラメータ：publicKey：アカウントの公開鍵を16進文字列として表します。
*   例：http://127.0.0.1:7890/account/get/from-public-key?publicKey=f9bd190dd0c364261f5c8a74870cc7f7374e631352293c62ecc437657e5de2cd
*   返されるJSONオブジェクトの例：返されるJSONオブジェクトの構造は、最初の例と同じです。
*   可能性のあるエラー：publicKeyパラメータが有効でない場合、NISはエラーを返します。エラーの詳細についてはNISエラー([NIS Errors](#appendix-B:-NIS-errors))を参照してください。

#### 3.1.3.委任アカウントのオリジナルデータリクエスト

公式情報：[Requesting the original account data for a delegate account](http://bob.nem.ninja/docs/#requesting-the-original-account-data-for-a-delegate-account)

*   APIパス：/account/get/forwarded
*   リクエストタイプ：GET
*   概要：委任(以前はリモート)アカウントのアドレスが与えられた場合、指定されたアカウントが委任アカウントであるアカウントのアカウントメタデータペア([AccountMetaDataPair](#accountMetaDataPair))を取得します。指定されたアカウントアドレスが任意のアカウントの委任アカウントでない場合、リクエストは指定されたアドレスのアカウントメタデータペアを返します。
*   パラメータ：address：委任アカウントのアドレス。

例：http://127.0.0.1:7890/account/get/forwarded?address=NC2ZQKEFQIL3JZEOB2OZPWXWPOR6LKYHIROCR7PK
*   返されるJSONオブジェクトの例

```json
{
	"account": {
		"address": "NALICE2A73DLYTP4365GNFCURAUP3XVBFO7YNYOW",
		"balance": 11793338398661,
		"vestedBalance": 10890953464862,
		"importance": 0.001264596432148395,
		"publicKey": "bdd8dd702acb3d88daf188be8d6d9c54b3a29a32561a068b25d2261b2b2b7f02",
		"label": null,
		"harvestedBlocks": 742
	},
	"meta": {
		"cosignatoryOf": [],
		"cosignatories": [],
		"status": "LOCKED",
		"remoteStatus": "ACTIVE"
	}
}
```

可能性のあるエラー：addressパラメータが有効でない場合、NISはエラーを返します。エラーの詳細についてはNISエラー([NIS Errors](#appendix-B:-NIS-errors))を参照してください。

代わりに委任アカウントの公開鍵を提供することでオリジナルのアカウントデータを取得することもできます。

*   APIパス：/account/get/forwarded/from-public-key
*   リクエストタイプ：GET
*   パラメータ：publicKey：アカウントの公開鍵を16進文字列として表します。
*   例：http://127.0.0.1:7890/account/get/forwarded/from-public-key?publicKey=bdd8dd702acb3d88daf188be8d6d9c54b3a29a32561a068b25d2261b2b2b7f02
*   返されるJSONオブジェクトの例：返されるJSONオブジェクトの構造は、最初の例と同じです。
*   可能性のあるエラー：publicKeyパラメータが有効でない場合、NISはエラーを返します。エラーの詳細についてはNISエラー([NIS Errors](#appendix-B:-NIS-errors))を参照してください。

#### 3.1.4.アカウントステータスのリクエスト

公式情報：[Requesting the account status](http://bob.nem.ninja/docs/#requesting-the-account-status)

*   APIパス：/account/status
*   リクエストタイプ：GET
*   概要：アカウントからアカウントメタデータ([AccountMetaData](#accountMetaData))を取得します。
*   パラメータ：Address：アカウントのアドレス。
*   例：http://127.0.0.1:7890/account/status?address=TALICELCD3XPH4FFI5STGGNSNSWPOTG5E4DS2TOS
*   返されるJSONオブジェクトの例

```json
{
	"cosignatoryOf": [],
	"status": "LOCKED",
	"remoteStatus": "ACTIVE"
}
```

可能性のあるエラー：addressパラメータが有効でない場合、NISはエラーを返します。エラーの詳細についてはNISエラー([NIS Errors](#appendix-B:-NIS-errors))を参照してください。

#### 3.1.5.アカウントのトランザクションデータリクエスト

公式情報：[Requesting transaction data for an account](http://bob.nem.ninja/docs/#requesting-transaction-data-for-an-account)

アカウントがトランザクションの受信者である場合、トランザクションは残高へ入金され、同様にトランザクションの送信はそのアカウントがトランザクションの送信者です。

確認されていないトランザクションは、まだブロックに含まれていないトランザクションです。 未確認のトランザクションは、どのブロックにも含まれないことが保証されています。

*   

**トランザクションの受信**APIパス：/account/transfers/incoming
*   リクエストタイプ：GET
*   概要：受信者がリクエストパラメータとして指定されたアドレスを持つトランザクションメタデータペア([TransactionMetaDataPair](#transactionMetaDataPair))オブジェクトの配列を取得します。これは最大25個のトランザクションメタデータペアが返されます。返されたトランザクションメタデータのペアは、データベースに書き込まれた降順でソートされます。
*   

2番目のパラメータはオプションです。存在しない場合には上記の基準に従って最新のトランザクションが返されます。ハッシュが2番目のパラメータとして指定されると、リクエストは上記の基準に従ってソートされたハッシュを持つトランザクションの直前に現れた最大25個のトランザクションを返します。

3番目のパラメータはオプションです。idが3番目のパラメータとして指定されると、リクエストは上記の基準に従ってソートされたidを持つトランザクションの直前に出現した最大25個のトランザクションを返します。

なお、25件未満のトランザクションが要件を満たす場合、それらのトランザクションのみが返されます。
パラメータ：address：アカウントのアドレス。
*   パラメータ：hash：トランザクションが返された256bitのsha3ハッシュ。
*   パラメータ：id：トランザクションが返されるまでのトランザクションID。
*   例：http://127.0.0.1:7890/account/transfers/incoming?address=TALICELCD3XPH4FFI5STGGNSNSWPOTG5E4DS2TOS&hash=949583a20ebdfdcb58277eb42fef3e66e9e6bbfc47304d8741a82c68f7c53a2
*   返されるJSONオブジェクトの例(テストネットワーク)

```json
{
	"data": [
		{
			"meta": {
				"id": 71245,
				"height": 40706,
				"hash": {
					"data": "15c373ad4c3fe6af47d1941379ff262f785bdcfa07c02ac3608bc10da27d5e82"
				}
			},
			"transaction": {
				"timeStamp": 9106400,
				"amount": 1000000000,
				"signature": "449cd76ea8bda2220b3d6ad6f8db5f81d4e68ad3d4b0c3db9a3c267355657639eabed3dbcef8e0cc22953ae2b36a22ee7dc6327484c9649cccd686a511eca105",
				"fee": 3000000,
				"recipient": "TALICELCD3XPH4FFI5STGGNSNSWPOTG5E4DS2TOS",
				"type": 257,
				"deadline": 9149600,
				"message": {
					"payload": "280000005444334b32493543524850595634425a5a5a4c335850454e4",
					"type": 2
				},
				"version": -1744830463,
				"signer": "c20a1dffe699c7a68328986273265e33fceebe074f274240ef890dd80ad55ed6"
			}
		},
		{
			"meta": {
				"id": 71356,
				"height": 40629,
				"hash": {
					"data": "37c34ead4c3fe6af42d994135798262f785ba2d807c02ac3608bc10da12e5f87"
				}
			},
			"transaction": {
				"timeStamp": 9101541,
				"amount": 49997995000000,
				"signature": "57c3c48d2ae8b24240b57d72493f498cfeb61e2ab87237dc0e08c51007d5c7f15847d0e08c0286e68a72028925db5fa809ca9d57e2cb6eebe11822176a834c0b",
				"fee": 2005000000,
				"recipient": "TALICELCD3XPH4FFI5STGGNSNSWPOTG5E4DS2TOS",
				"type": 257,
				"deadline": 9144741,
				"message": {
					"payload": "526f6262657279212121",
					"type": 1
				},
				"version": -1744830463,
				"signer": "546e4fb9c81db84e04d8e9e67380db0fe1f540df09a527fb995b589b5695ae24"
			}
		}
	]
}
```

可能性のあるエラー：addressパラメータが有効でないか、データベース内にidが見つからない場合、NISはエラーを返します。エラーの詳細についてはNISエラー([NIS Errors](#appendix-B:-NIS-errors))を参照してください。

*   

**トランザクションの送信**
APIパス：/account/transfers/outgoing
*   

受信者がリクエストパラメータとして指定されたアドレスを持つトランザクションメタデータペアの配列を取得します。

最大25個のトランザクションメタデータペアが返されます。2番目のパラメータソートと説明については、トランザクションの受信([Incoming transactions](#incoming-transactions))を参照してください。
リクエストタイプ：GET
*   概要：受信者がリクエストパラメータとして指定されたアドレスを持つトランザクションメタデータペア([TransactionMetaDataPair](#transactionMetaDataPair))オブジェクトの配列を取得します。これは最大25個のトランザクションメタデータペアが返されます。返されたトランザクションメタデータのペアは、データベースに書き込まれた降順でソートされます。
*   

2番目のパラメータはオプションです。存在しない場合には上記の基準に従って最新のトランザクションが返されます。ハッシュが2番目のパラメータとして指定されると、リクエストは上記の基準に従ってソートされたハッシュを持つトランザクションの直前に現れた最大25個のトランザクションを返します。

3番目のパラメータはオプションです。idが3番目のパラメータとして指定されると、リクエストは上記の基準に従ってソートされたidを持つトランザクションの直前に出現した最大25個のトランザクションを返します。

なお、25件未満のトランザクションが要件を満たす場合、それらのトランザクションのみが返されます。
パラメータ：address：アカウントのアドレス。
*   パラメータ：hash：トランザクションが返された256bitのsha3ハッシュ。
*   パラメータ：id：トランザクションが返されるまでのトランザクションID。
*   例：http://127.0.0.1:7890/account/transfers/outgoing?address=TALICELCD3XPH4FFI5STGGNSNSWPOTG5E4DS2TOS&hash=949583a20ebdfdcb58277eb42fef3e66e9e6bbfc47304d8741a82c68f7c53a22
*   返されるJSONオブジェクトの例(テストネットワーク)

```json
{
	"data": [
		{
			"meta": {
				"id": 70498,
				"height": 40803,
				"hash": {
					"data": "37c34ead4c3fe6af42d994135798262f785ba2d807c02ac3608bc10da12e5f87"
				}
			},
			"transaction": {
				"timeStamp": 9111526,
				"amount": 1000000000,
				"signature": "651a19ccd09c1e0f8b25f6a0aac5825b0a20f158ca4e0d78f2abd904a3966b6e3599a47b9ff199a3a6e1152231116fa4639fec684a56909c22cbf6db66613901",
				"fee": 3000000,
				"recipient": "TDGIMREMR5NSRFUOMPI5OOHLDATCABNPC5ID2SVA",
				"type": 257,
				"deadline": 9154726,
				"message": {
					"payload": "74657374207472616e73616374696f6e",
					"type": 1
				},
				"version": -1744830463,
				"signer": "a1aaca6c17a24252e674d155713cdf55996ad00175be4af02a20c67b59f9fe8a"
			}
		}
	]
}
```

可能性のあるエラー：addressパラメータが有効でないか、データベース内にidが見つからない場合、NISはエラーを返します。エラーの詳細についてはNISエラー([NIS Errors](#appendix-B:-NIS-errors))を参照してください。

*   

**全てのトランザクション**
APIパス：/account/transfers/all
*   

受信者がリクエストパラメータとして指定されたアドレスを持つトランザクションメタデータペアの配列を取得します。

最大25個のトランザクションメタデータペアが返されます。2番目のパラメータソートと説明については、トランザクションの受信([Incoming transactions](#incoming-transactions))を参照してください。
リクエストタイプ：GET
*   概要：受信者がリクエストパラメータとして指定されたアドレスを持つトランザクションメタデータペア([TransactionMetaDataPair](#transactionMetaDataPair))オブジェクトの配列を取得します。これは最大25個のトランザクションメタデータペアが返されます。返されたトランザクションメタデータのペアは、データベースに書き込まれた降順でソートされます。
*   

2番目のパラメータはオプションです。存在しない場合には上記の基準に従って最新のトランザクションが返されます。ハッシュが2番目のパラメータとして指定されると、リクエストは上記の基準に従ってソートされたハッシュを持つトランザクションの直前に現れた最大25個のトランザクションを返します。

3番目のパラメータはオプションです。idが3番目のパラメータとして指定されると、リクエストは上記の基準に従ってソートされたidを持つトランザクションの直前に出現した最大25個のトランザクションを返します。

なお、25件未満のトランザクションが要件を満たす場合、それらのトランザクションのみが返されます。
パラメータ：address：アカウントのアドレス。
*   パラメータ：hash：トランザクションが返された256bitのsha3ハッシュ。
*   パラメータ：id：トランザクションが返されるまでのトランザクションID。
*   例：http://127.0.0.1:7890/account/transfers/outgoing?address=TALICELCD3XPH4FFI5STGGNSNSWPOTG5E4DS2TOS&hash=949583a20ebdfdcb58277eb42fef3e66e9e6bbfc47304d8741a82c68f7c53a22
*   返されるJSONオブジェクトの例：[トランザクションの受信](#incoming-transactions)および[トランザクションの送信](#outgoing-transactions)を見て下さい。
*   可能性のあるエラー：addressパラメータが有効でないか、データベース内にidが見つからない場合、NISはエラーを返します。エラーの詳細についてはNISエラー([NIS Errors](#appendix-B:-NIS-errors))を参照してください。

*   

**未確認のトランザクション**
APIパス：/account/unconfirmedTransactions
*   

受信者がリクエストパラメータとして指定されたアドレスを持つトランザクションメタデータペアの配列を取得します。

最大25個のトランザクションメタデータペアが返されます。2番目のパラメータソートと説明については、トランザクションの受信([Incoming transactions](#incoming-transactions))を参照してください。
リクエストタイプ：GET
*   概要：アカウントが送信者または受信者であり、まだブロックに含まれていないトランザクションの配列を取得します。返される構造については未確認トランザクションメタデータペア([UnconfirmedTransactionMetaDataPair](#unconfirmedTransactionMetaDataPair))を参照して下さい。
*   パラメータ：address：アカウントのアドレス。
*   例：http://127.0.0.1:7890/account/unconfirmedTransactions?address=TALICELCD3XPH4FFI5STGGNSNSWPOTG5E4DS2TOS
*   返されるJSONオブジェクトの例(テストネットワーク)

```json
{
	"meta": {
		"data": "d7c9e33421e43bf4a5d6e21304c8096c599142755d581bd6e9037f41545a5873"
	},
	"data": [
		{
			"timeStamp": 9131839,
			"amount": 1000000000,
			"signature": "0acface77696a54340a7da8592750ea0410f62717d07e4df30e09718092521262465df5c4d98d32cd9d6e8699d66e016ec8db716d20090ad99cc16f7a6d13904",
			"fee": 2000000,
			"recipient": "TDGIMREMR5NSRFUOMPI5OOHLDATCABNPC5ID2SVA",
			"type": 257,
			"deadline": 9175039,
			"message": {
				"payload": "",
				"type": 1
			},
			"version": -1744830463,
			"signer": "a1aaca6c17a24252e674d155713cdf55996ad00175be4af02a20c67b59f9fe8a"
		}
	]
}
```

可能性のあるエラー：addressパラメータが有効でない場合、NISはエラーを返します。エラーの詳細についてはNISエラー([NIS Errors](#appendix-B:-NIS-errors))を参照してください。

#### 3.1.6.デコードされたメッセージによるトランザクションデータ

公式情報：[Transaction data with decoded messages](http://bob.nem.ninja/docs/#transaction-data-with-decoded-messages)

前項で説明したアカウントのトランザクションデータを取得するためのすべてのリクエストは、トランザクションに含まれるメッセージをデコードしません。

以下のリクエストは上記と同様ですが、デコードされたメッセージでトランザクションデータを返すことができます。

復号にはトランザクションが要求されるアカウントの秘密鍵が必要です。したがってNISがローカルで実行されている場合にのみ次のリクエストを行う必要があります。

*   

**受信/送信/全てのトランザクションによるデコードされたメッセージ**
APIパス：/local/account/transfers/incoming
*   APIパス：/local/account/transfers/outgoing
*   APIパス：/local/account/transfers/all
*   リクエストタイプ：POST(3種共に)
*   概要：前項で説明したように、リクエストは受信/送信/全てのトランザクションを返します。唯一の違いはトランザクションにエンコードされたメッセージが含まれている場合、このメッセージはリクエスターに送信される前にデコードされることです。
*   パラメータ：page：アカウント秘密鍵トランザクションページで説明されているアカウント秘密鍵トランザクションページ([AccountPrivateKeyTransactionsPage](#accountPrivateKeyTransactionsPage))JSONオブジェクト。
*   例：リクエストはブラウザでは実行できません。
*   返されるJSONオブジェクトの例：[アカウントのトランザクションデータリクエスト](#requesting-transaction-data-for-an-account)を見て下さい。
*   可能性のあるエラー：秘密鍵が提供されていない場合、NISはエラーを返します。エラーの詳細についてはNISエラー([NIS Errors](#appendix-B:-NIS-errors))を参照してください。

#### 3.1.7.アカウントの収穫情報データリクエスト

公式情報：[Requesting harvest info data for an account](http://bob.nem.ninja/docs/#requesting-harvest-info-data-for-an-account)

*   APIパス：/account/harvests
*   リクエストタイプ：GET
*   概要：アカウントの収穫情報オブジェクトの配列を取得します。
*   パラメータ：address：アカウントのアドレス。
*   パラメータ：hash：トランザクションが返された256bitのsha3ハッシュ。
*   例：http://127.0.0.1:7890/account/harvests?address=TALICELCD3XPH4FFI5STGGNSNSWPOTG5E4DS2TOS&hash=81d52a7df4abba8bb1613bcc42b6b93cf3114524939035d88ae8e864cd2c34c8
*   返されるJSONオブジェクトの例

```json
{
	"data": [
		{
			"timeStamp": 8879051,
			"blockHash": {
				"data": "be3bb308ce33625f0dab64fd31b9ebe1c50dd4b94b43b03c228f481ab82458c3"
			},
			"totalFee": 102585065,
			"height": 37015
		}
	]
}
```

可能性のあるエラー：addressパラメータが有効でないか、またはハッシュがデータベースに見つからない場合、NISはエラーを返します。エラーの詳細についてはNISエラー([NIS Errors](#appendix-B:-NIS-errors))を参照してください。

#### 3.1.8.アカウントの重要度情報の取得

公式情報：[Retrieving account importances for accounts](http://bob.nem.ninja/docs/#retrieving-account-importances-for-accounts)

*   APIパス：/account/importances
*   リクエストタイプ：GET
*   概要：アカウント重要度ビューモデルオブジェクトの配列を取得します。
*   パラメータ：無し。
*   例：http://127.0.0.1:7890/account/importances
*   返されるJSONオブジェクトの例

```json
{
	"data": [
		{
			"address": "TCYGT6GHZPNASMAXV7YCFCU5R5XTJKNNT66R4A4T",
			"importance": {
				"isSet": 0
			}
		},
		{
			"address": "TD2JJJVPKDZFXWK3N3ZJLN7A5TGNOTM3J5EVSTIG",
			"importance": {
				"score": 0.001222376902598832,
				"ev": 0.004252356221747241,
				"isSet": 1,
				"height": 40926
			}
		}
	]
}
```

可能性のあるエラー：無し。

#### 3.1.9.アカウントが所有するネームスペースの取得

公式情報：[Retrieving namespaces that an account owns](http://bob.nem.ninja/docs/#retrieving-namespaces-that-an-account-owns)

*   APIパス：/account/namespace/page
*   リクエストタイプ：GET
*   概要：指定されたアカウントアドレスのネームスペースオブジェクトの配列を取得します。親パラメータはオプションです。指定された場合には親ネームスペースのサブネームスペースのみが返されます。
*   パラメータ：address：アカウントのアドレス。
*   パラメータ：parent：オプションの親ネームスペースID。
*   パラメータ：id：オプションのネームスペースデータベースID。ネームスペースが返される。
*   パラメータ：pageSize：ネームスペースの(オプション)番号が返されます。
*   例：http://127.0.0.1:7890/account/namespace/page?address=TD3RXTHBLK6J3UD2BH2PXSOFLPWZOTR34WCG4HXH&parent=makoto.metal
*   返されるJSONオブジェクトの例

```json
{
	"data": [
		{
			"fqn": "makoto.metal.coins",
			"owner": "TD3RXTHBLK6J3UD2BH2PXSOFLPWZOTR34WCG4HXH",
			"height": 13465
		}
	]
}
```

可能性のあるエラー：アドレスまたは(提供されている)親が無効である場合、NISはエラーを返します。エラーの詳細についてはNISエラー([NIS Errors](#appendix-B:-NIS-errors))を参照してください。

#### 3.1.10.アカウントが作成したモザイク定義を取得

公式情報：[Retrieving mosaic definitions that an account has created](http://bob.nem.ninja/docs/#retrieving-mosaic-definitions-that-an-account-has-created)

*   APIパス：/account/mosaic/definition/page

リクエストタイプ：GET
*   概要：指定されたアカウントアドレスのモザイク定義オブジェクトの配列を取得します。親パラメータはオプションです。指定すると指定された親ネームスペースのモザイク定義のみが返されます。
*   

idパラメータはオプションであり、25のモザイク定義のバッチでモザイク定義を取得することができます。 idの使用方法の詳細については、トランザクションの受信([Incoming transactions](#incoming-transactions))を参照してください。
パラメータ：address：アカウントのアドレス。
*   パラメータ：parent：オプションの親ネームスペースID。
*   パラメータ：id：モザイク定義が返されるオプションのモザイク定義データベースID。
*   例：http://127.0.0.1:7890/account/mosaic/definition/page?address=TD3RXTHBLK6J3UD2BH2PXSOFLPWZOTR34WCG4HXH&parent=makoto.metal.coins
*   返されるJSONオブジェクトの例

```json
{
	"data": [
		{
			"creator": "10cfe522fe23c015b8ab24ef6a0c32c5de78eb55b2152ed07b6a092121187100",
			"id": {
				"namespaceId": "makoto.metal.coins",
				"name": "silver coin"
			},
			"description": "Real silver coins, pure silver",
			"properties": [
				{
					"name": "divisibility",
					"value": "0"
				},
				{
					"name": "initialSupply",
					"value": "1000"
				},
				{
					"name": "supplyMutable",
					"value": "false"
				},
				{
					"name": "transferable",
					"value": "true"
				}
			]
		}
	]
}
```

可能性のあるエラー：アドレスもしくは親(提供されている場合)またはID(提供されている場合)が無効な場合、NISはエラーを返します。エラーの詳細についてはNISエラー([NIS Errors](#appendix-B:-NIS-errors))を参照してください。

#### 3.1.11.アカウントが所有するモザイクを取得

公式情報：[Retrieving mosaics that an account owns](http://bob.nem.ninja/docs/#retrieving-mosaics-that-an-account-owns)

*   APIパス：/account/mosaic/owned
*   リクエストタイプ：GE
*   概要：指定されたアカウントアドレスのモザイクオブジェクトの配列を取得します。
*   パラメータ：address：アカウントのアドレス。
*   例：http://127.0.0.1:7890/account/mosaic/owned?address=TD3RXTHBLK6J3UD2BH2PXSOFLPWZOTR34WCG4HXH
*   返されるJSONオブジェクトの例

```json
{
	"data": [
		{
			"mosaicId": {
				"namespaceId": "alice.drinks",
				"name": "orange juice"
			},
			"quantity": 123
		},
		{
			"mosaicId": {
				"namespaceId": "makoto.metal.coins",
				"name": "silver coin"
			},
			"quantity": 8
		}
	]
}
```

可能性のあるエラー：アドレスが無効な場合、NISはエラーを返します。エラーの詳細についてはNISエラー([NIS Errors](#appendix-B:-NIS-errors))を参照してください。

#### 3.1.12.アカウントのロックとロック解除

公式情報：[Locking and unlocking accounts](http://bob.nem.ninja/docs/#locking-and-unlocking-accounts)

NEM残高が少なくとも10000を所有している残高はブロックを収穫することができます。

これを行うにはアカウントのロックを解除する必要があります。 NISの起動後、すべてのアカウントはデフォルトでロックされています。

*   *   

**アカウントのロックを解除する(収穫を可能にする)**
APIパス：/account/unlock
    *   リクエストタイプ：POST
    *   概要：アカウントのロックを解除する(収穫を可能にする)。
    *   パラメータ：privateKey：秘密鍵([PrivateKey](#privateKey))で説明されているPrivateKey JSONオブジェクト。
    *   例：リクエストはブラウザでは実行できません。
    *   返り値なし

    *   

**アカウントをロックする(収穫を停止する)**
APIパス：/account/lock
    *   リクエストタイプ：POST
    *   概要：アカウントをロックする(収穫を停止する)。
    *   パラメータ：privateKey：秘密鍵([PrivateKey](#privateKey))で説明されているPrivateKey JSONオブジェクト。
    *   例：リクエストはブラウザでは実行できません。
    *   返り値なし可能性のあるエラー：秘密鍵がアカウントに対応していないか、アカウントに対して収穫を許可されていない場合、両方のリクエストはエラーを返します。エラーの詳細についてはNISエラー([NIS Errors](#appendix-B:-NIS-errors))を参照してください。

#### 3.1.13.ロック解除情報の取得

公式情報：[Retrieving the unlock info](http://bob.nem.ninja/docs/#retrieving-the-unlock-info)

各ノードでは、委任されたキーを使用してユーザーがそのノードで収穫できるようにすることができます。

NIS構成には許可されたハーベスタの最大数を設定するためのエントリがあり、オプションで特定のアカウントアドレスに対してのみハーベスティングを許可することもできます。

アンロック情報は、許可されたハーベスタの最大数、およびノードをすでに使用しているハーベスタ数についての情報を提供します。

*   APIパス：/account/unlocked/info
*   リクエストタイプ：POST
*   パラメータ：無し。
*   例：リクエストはブラウザでは実行できません。
*   返されるJSONオブジェクトの例

```json
{
	"num-unlocked": 2,
	"max-unlocked": 3
}
```

可能性のあるエラー：無し。

### 3.2.アカウントの履歴データ検索

公式情報：[Retrieving historical account data](http://bob.nem.ninja/docs/#retrieving-historical-account-data)

NISの設定にはノードが他のノードには提供しない追加機能を公開することが出来ます。

これら機能の1つは残高や重要度情報などの履歴アカウントデータの提供です。

NISでこの機能を有効にするには、config.propertiesファイルのオプション機能のリストにHISTORICAL_ACCOUNT_DATAを追加する必要があります。

*   APIパス：/account/historical/get
*   リクエストタイプ：GET
*   概要：アカウントの履歴情報を取得します。
*   パラメータ：address：アカウントのアドレス。
*   パラメータ：startHeight：データのブロック高さを指定します。
*   パラメータ：endHeight：データが供給されるブロックの高さ。終わりの高さは開始の高さ以上でなければなりません。
*   パラメータ：increment：各データポイント間で高さが増加する値。値は0より大きくなければなりません。NISは1回の要求で最大1000のデータポイントを供給できます。1000を超えるデータポイントを要求すると、エラーが発生します。
*   例：http://bigalice3.nem.ninja:7890/account/historical/get?address=NALICELGU3IVY4DPJKHYLSSVYFFWYS5QPLYEZDJJ&startHeight=17592&endHeight=17592&increment=1
*   返されるJSONオブジェクトの例

```json
[
	{
		"height": 17592,
		"address": "NALICELGU3IVY4DPJKHYLSSVYFFWYS5QPLYEZDJJ",
		"balance": 509676000000,
		"vestedBalance": 100999147150,
		"unvestedBalance": 408676852850,
		"importance": 0.00008857563463531297,
		"pageRank": 0.0007605047835049349
	}
]
```

可能性のあるエラー：アドレスが無効であることや、開始の高さが終わりの高さより大きい場合、または増加数が正数でない場合、あるいはリクエストの結果が1000データを超える場合にエラーが返されます。

## 4.ブロックチェーン関連のリクエスト

公式情報：[Block chain related requests](http://bob.nem.ninja/docs/#block-chain-related-requests)

NEMは求められるあらゆる情報を含むブロックチェーンを構築します。ブロックチェーン内の後続ブロックの高さは1ずつ異なります。各ブロックはトランザクションを含むことができます。トランザクションはすべてのアカウントアクティビティの基礎を構築します。したがって、ブロックとトランザクションの概念と構造を理解することが重要です。

ブロックはアカウントによって生成されます。アカウントがブロックを生成し、そのブロックがブロックチェーンに含まれる場合、ハーベスタと呼ばれる生成アカウントはブロックに含まれるトランザクションのすべてのトランザクション手数料を取得します。したがって、ハーベスタには通常できるだけ多くのトランザクションが含まれます。

トランザクションはすべてのアカウントアクティビティを反映します。クライアントがすべてのアカウントに対して最新の残高を取るためには、発生したすべてのトランザクションについて知ることが重要であり、したがって、クライアントはチェーン内のすべてのブロックについての知識を持っていなければなりません(クライアントはブロックチェーンと同期しなければならない)。

タイムスタンプが使用されるたびにネットワークの時間は反映されます。NEMにはすべてのノードを一致させる時間同期機構があります。この共通の時間をネットワーク時間(network time)といいます。

以下の章ではまずブロックとトランザクション構造で使用されるフィールドを紹介し、次にクライアントがブロックチェーンの一部をリクエストする方法を説明します。

ブロックはJSONブロックオブジェクトを使用して転送されます。ブロック([block](#block))には、より多くの情報とJSONブロックオブジェクトの例があります。 次のフィールドが構造内にあります。

*   フィールド：timeStamp：ブロックが作成されたネットワークの時刻。
*   フィールド：signature：ブロックの署名。チェーン内のすべてのブロックはハーベスタによって署名されています。ブロックは何らかの悪意のある者によって変更されているかどうかをノードが確認できます。
*   フィールド：prevBlockHash：前のブロックのsha3-256ハッシュを16進数文字列として表します。
*   フィールド：type：ブロックタイプ。現在以下2つのブロックタイプが使用されています。
*   -1：ネメシス(Nemesis)ブロックタイプ。このブロックタイプはチェーン内に一度だけ表示されます。
*   1：通常のブロックタイプ。高さ> 1のブロックはすべてこのタイプです。
*   フィールド：transactions：トランザクションの配列。 詳細についてはトランザクション([Transactions](#transaction))を参照してください。ブロックには最大120のトランザクションを含めることができます。
*   フィールド：version：ブロックバージョン。 次のバージョンがサポートされています。
*   *   0x68 < 24="" +="">
    *   0x98 < 24="" +="">フィールド：signer：ブロックのハーベスタの公開鍵を16進数文字列として返します。
*   フィールド：height：ブロックの高さ。各ブロックには固有の高さがあります。後続のブロックの高さは1だけ異なります。

トランザクションは『3.[アカウントに関連するリクエスト](#account-related-requests)』で既に説明しました。JSONトランザクションオブジェクトの例についてはトランザクション([Transaction](#transaction))を参照してください。

### 4.1.ブロックチェーンステータス情報のリクエスト

公式情報：[Requesting the block chain status information](http://bob.nem.ninja/docs/#requesting-the-block-chain-status-information)

#### 4.1.1.ブロックチェーンの高さ

公式情報：[Block chain height](http://bob.nem.ninja/docs/#block-chain-height)

*   APIパス：/chain/height
*   リクエストタイプ：GET
*   概要：ブロックチェーンの現在の高さを取得します。
*   パラメータ：無し。
*   例：http://127.0.0.1:7890/chain/height
*   返されるJSONオブジェクトの例

```json
{
"height": 42799
}
```

可能性のあるエラー：無し。

#### 4.1.2.ブロックチェーンスコア

公式情報：[Block chain score](http://bob.nem.ninja/docs/#block-chain-score)

*   APIパス：/chain/score
*   リクエストタイプ：GET
*   概要：ブロックチェーンの現在のスコアを取得します。スコアが高いほどチェーンが良好になります。同期中ノードはネットワーク内で最良のブロックチェーンを取得しようとします。
*   パラメータ：無し。
*   例：http://127.0.0.1:7890/chain/score
*   返されるJSONオブジェクトの例

```json
{
    "score": "18722d5a7d590deb"
}
```

可能性のあるエラー：無し。

#### 4.1.3.ブロックチェーンスコアラストブロック

公式情報：[Last block of the block chain score](http://bob.nem.ninja/docs/#last-block-of-the-block-chain-score)

*   APIパス：/chain/last-block
*   リクエストタイプ：GET
*   概要：チェーンの現時点でのラストブロックを取得します。
*   パラメータ：無し。
*   例：http://127.0.0.1:7890/chain/last-block
*   返されるJSONオブジェクトの例

```json
{
	"timeStamp": 9232968,
	"signature": "0a1351ef3e9b19c601e804a6d329c9ade662051d1da2c12c3aec9934353e421c79de7d8e59b127a8ca9b9d764e3ca67daefcf1952f71bc36f747c8a738036b05",
	"prevBlockHash": {"data": "58efa578aea719b644e8d7c731852bb26d8505257e03a897c8102e8c894a99d6"},
	"type": 1,
	"transactions": [],
	"version": 1744830465,
	"signer": "2afca04d2cb8d16cf3656274bc55b95e60be823cfb7230d82f791ed42a309ee7",
	"height": 42804
}
```

可能性のあるエラー：無し。

### 4.2.ブロックチェーンの一部リクエスト

公式情報：[Requesting parts of the block chain](http://bob.nem.ninja/docs/#requesting-parts-of-the-block-chain)

NISはブロックの高さまたはブロックのハッシュによって識別される個々のブロックを供給することや、特定の高さから始まるブロックを最大10個まで供給することもできます。

#### 4.2.1.指定されたハッシュでブロックを取得する

公式情報：[Getting a block with a given hash](http://bob.nem.ninja/docs/#getting-a-block-with-a-given-hash)

*   APIパス：/block/get
*   リクエストタイプ：GET
*   概要：指定されたハッシュを持つブロックをチェーンから取得します。
*   パラメータ：blockHash：ブロックの256ビットsha3ハッシュ。ハッシュは16進数文字列として指定する必要があります。
*   例：http://127.0.0.1:7890/block/get?blockHash=58efa578aea719b644e8d7c731852bb26d8505257e03a897c8102e8c894a99d6
*   返されるJSONオブジェクトの例

```json
{
	"timeStamp": 9232942,
	"signature": "005f91b8908fc173a428ff8e8c4a0ee0d69e4004aed0d08f27690b6b6672ef74ccc6b89695bed5f29b0f4a812cb84bfa459f52a4e14a11e574793969f0e1a30f",
	"prevBlockHash": {
		"data": "f721e563b4431594c5af6f6be0a913f47f0aca6c3b8ee6a703bfe175ee54babf"
	},
	"type": 1,
	"transactions": [],
	"version": 1744830465,
	"signer": "78e121cc1cf63424651ec64251e78efda81386c9f5e9eb4cb08b2a2192c9dce5",
	"height": 42803
}
```

可能性のあるエラー：ブロックハッシュがデータベースに見つからない場合、NISはJSONエラーオブジェクトを返します。 エラーの詳細についてはエラーオブジェクト([Error object](#error-object))、もしくはNISエラー([NIS Errors](#appendix-B:-NIS-errors))を参照してください。

#### 4.2.2.指定した高さでブロックを取得する

公式情報：[Getting a block with a given height](http://bob.nem.ninja/docs/#getting-a-block-with-a-given-height)

*   APIパス：/block/at/public
*   リクエストタイプ：GET
*   概要：指定された高さを持つブロックをチェーンから取得します。
*   パラメータ：blockHeight：ブロックの高さ([BlockHeight](#blockHeight))で説明されているBlockHeight JSONオブジェクト。
*   例：リクエストはブラウザでは実行できません。
*   返されるJSONオブジェクトの例

```json
{
	"timeStamp": 9232942,
	"signature": "005f91b8908fc173a428ff8e8c4a0ee0d69e4004aed0d08f27690b6b6672ef74ccc6b89695bed5f29b0f4a812cb84bfa459f52a4e14a11e574793969f0e1a30f",
	"prevBlockHash": {
		"data": "f721e563b4431594c5af6f6be0a913f47f0aca6c3b8ee6a703bfe175ee54babf"
	},
	"type": 1,
	"transactions": [],
	"version": -1744830463,
	"signer": "78e121cc1cf63424651ec64251e78efda81386c9f5e9eb4cb08b2a2192c9dce5",
	"height": 42803
}
```

可能性のあるエラー：指定された高さのブロックがデータベースに見つからない場合、NISはJSONエラーオブジェクトを返します。エラーの詳細についてはエラーオブジェクト([Error object](#error-object))、もしくはNISエラー([NIS Errors](#appendix-B:-NIS-errors))を参照してください。

#### 4.2.3.チェーンの一部を取得する

公式情報：[Getting part of a chain](http://bob.nem.ninja/docs/#getting-part-of-a-chain)

*   APIパス：/local/chain/blocks-after
*   リクエストタイプ：POST
*   概要：チェーンから与えられたブロックの高さの後に最大10ブロックを取得します。 指定された高さの後にデータベースが10未満のブロックを含む場合、より少ないブロックが返されます。 返されるデータは、エクスプローラブロックビューモデル([ExplorerBlockViewModel](#explorerBlockViewModel)) JSONオブジェクトの配列です。
*   パラメータ：blockHeight：ブロックの高さ([BlockHeight](#blockHeight))で説明されているBlockHeight JSONオブジェクト。
*   例：リクエストはブラウザでは実行できません。
*   返されるJSONオブジェクトの例
*   

        {
            "data":[{
            "txes":[{
            "tx": <explorerviewmodeltransaction>
            "tx": <explorerviewmodeltransaction>
            }],
            "block": <block>
            "hash":"8ca8a3e01ac0eb482e668fda74141984ba118b027fc5f1f67d2d36a38bf48c49"
            }]
            }

可能性のあるエラー：指定されたブロックの高さが整数でない場合、NISはJSONエラーオブジェクトを返します。エラーの詳細についてはエラーオブジェクト([Error object](#error-object))、もしくはNISエラー([NIS Errors](#appendix-B:-NIS-errors))を参照してください。

## 5.ノード関連のリクエスト

公式情報：[Node related requests](http://bob.nem.ninja/docs/#node-related-requests)

ノードはネットワーク内でデータを交換する実体です。基本的にノードはコンピュータ上で動作するNISインスタンスで、ネットワークと通信できるようにするにはノードを起動する必要があります。ノードリクエストによってネットワーク内の他のノードを発見し、他のノードの経験について学習し、現在のチェーンの高さに関する情報を得ることが可能です。

ノード構造は、ID、エンドポイント、およびメタデータの3つの部分で構成されます。

すべてのノードはアカウントによって表される身元に結びついています。それにより、ノードを識別しやすくなります。ブートプロセス中にノードにはIDが与えられます。

ノードのエンドポイントは通信に使用されるIPアドレス、ポート、およびプロトコルに関する情報を保持します。

メタデータにはNISのバージョンとプラットフォームNISが実行されていることに関する追加情報が格納されています。

ノードは各ノードにステータスを割り当てることによって、隣接ノードのセットをいくつかのサブセットにグループ化します。可能なステータスは次のとおりです。

*   ステータス：active：この状態のノードは正常に通信できます。ノードが通信のためにノードを選択しているときは常にアクティブノードのセットからノードを選ぶでしょう。
*   ステータス：inactive：非アクティブノードは接続を確立できないノードです。
*   ステータス：busy：接続が確立されてもノードが特定の時間制限内で要求に応答しなかった場合には、ノードはステータス『busy』に設定されます。
*   ステータス：failure：状態障害は通信中に重大なエラーが発生した場合に備えて、リモートノードに割り当てられます。これは、例えば遠隔ノードが異なるプロトコルを使用しているか、または遠隔ノードが予想された身元と異なる身元を使用していることが原因である可能性があります。
*   ステータス：unknown：この状態は利用可能な状態に関する情報がない場合にノードに与えられます。

ノード([Node](#node))にはより多くの情報とJSON Nodeオブジェクトの例があります。ノードオブジェクトには、次のフィールドがあります。

*   フィールド：name：ノードの名前。これには任意の文字列を使用できます。
*   フィールド：public-key：ノードを識別するために使用される公開鍵。
*   フィールド：protocol：通信に使用されるプロトコル(現在はHTTPのみがサポートされています)。
*   フィールド：port：通信に使用されるポート。
*   フィールド：host：エンドポイントのIPアドレス。
*   フィールド：application：ノードを実行しているアプリケーションの名前。
*   フィールド：version：アプリケーションのバージョン。
*   フィールド：platform：基礎となるプラットフォーム(OS、javaバージョン)。

### 5.1.ノードに関する情報のリクエスト

公式情報：[Requesting information about a node](http://bob.nem.ninja/docs/#requesting-information-about-a-node)

#### 5.1.1.基本ノード情報

公式情報：[Basic node information](http://bob.nem.ninja/docs/#basic-node-information)

*   APIパス：/node/info
*   リクエストタイプ：GET
*   概要：ノードに関する基本情報を取得します。IP 127.0.0.1を使用するとローカルノードに関する情報が取得されます。
*   パラメータ：無し。
*   例：http://127.0.0.1:7890/node/info
*   返されるJSON[ノード](#node)の例

```json
{
	"metaData": {
		"application": "NIS",
		"version": "0.4.33-BETA",
		"platform": "Oracle Corporation (1.8.0_25) on Windows 8"
	},
	"endpoint": {
		"protocol": "http",
		"port": 7890,
		"host": "81.224.224.156"
	},
	"identity": {
		"name": "Alice",
		"public-key": "a1aaca6c17a24252e674d155713cdf55996ad00175be4af02a20c67b59f9fe8a"
	}
}
```

可能性のあるエラー：ノードがまだ起動されていない場合、NISはJSONエラーオブジェクトを返します。エラーの詳細についてはエラーオブジェクト([Error object](#error-object))、もしくはNISエラー([NIS Errors](#appendix-B:-NIS-errors))を参照してください。

#### 5.1.2.拡張ノード情報

公式情報：[Extended node information](http://bob.nem.ninja/docs/#extended-node-information)

*   APIパス：/node/extended-info
*   リクエストタイプ：GET
*   概要：ノードに関する拡張情報を取得します。IP 127.0.0.1を使用するとローカルノードに関する情報が取得されます。
*   パラメータ：無し。
*   例：http://127.0.0.1:7890/node/extended-info
*   返されるJSON[NISノード情報](#nisNodeInfo)の例

```json
{
	"node": {
		"metaData": {
			"application": "NIS",
			"version": "0.4.33-BETA",
			"platform": "Oracle Corporation (1.8.0_25) on Windows 8"
		},
		"endpoint": {
			"protocol": "http",
			"port": 7890,
			"host": "81.224.224.156"
		},
		"identity": {
			"name": "Alice",
			"public-key": "a1aaca6c17a24252e674d155713cdf55996ad00175be4af02a20c67b59f9fe8a"
		}
	},
	"nisInfo": {
		"currentTime": 9288341,
		"application": "NEM Infrastructure Server",
		"startTime": 9238484,
		"version": "0.4.33-BETA",
		"signer": "CN=VeriSign Class 3 Code Signing 2010 CA,OU=Terms of use at https://www.verisign.com/rpa (c)10,OU=VeriSign Trust Network,O=VeriSign\\,Inc.,C=US"
	}
}
```

可能性のあるエラー：ノードがまだ起動されていない場合、NISはJSONエラーオブジェクトを返します。エラーの詳細についてはエラーオブジェクト([Error object](#error-object))、もしくはNISエラー([NIS Errors](#appendix-B:-NIS-errors))を参照してください。

### 5.2.ノードの近辺を発見するリクエスト

公式情報：[Request for discovering the neighborhood of a node](http://bob.nem.ninja/docs/#request-for-discovering-the-neighborhood-of-a-node)

#### 5.2.1.完全な近辺

公式情報：[Complete neighborhood](http://bob.nem.ninja/docs/#complete-neighborhood)

*   APIパス：/node/peer-list/all
*   リクエストタイプ：GET
*   概要：近辺にあるすべての既知のノードの配列を取得します。
*   パラメータ：無し。
*   例：http://127.0.0.1:7890/node/peer-list/all
*   返されるJSON[ノードコレクション](#nodeCollection)の例(<Node>はNodeオブジェクトを表します。)
*   

        {
                "inactive": [
                <Node>,
                <Node>
                ],
                "active": [
                <Node>,
                <Node>
                ],
                "busy": [
                <Node>,
                <Node>
                ],
                "failure": [
                <Node>,
                <Node>
                ]
                }

可能性のあるエラー：ノードがまだ起動されていない場合、NISはJSONエラーオブジェクトを返します。エラーの詳細についてはエラーオブジェクト([Error object](#error-object))、もしくはNISエラー([NIS Errors](#appendix-B:-NIS-errors))を参照してください。

#### 5.2.2.到達可能な近辺

公式情報：[Reachable neighborhood](http://bob.nem.ninja/docs/#reachable-neighborhood)

*   APIパス：/node/peer-list/reachable
*   リクエストタイプ：GET
*   概要：近辺にステータスが『active』であるすべてのノードの配列を取得します。
*   パラメータ：無し。
*   例：http://127.0.0.1:7890/node/peer-list/reachable
*   返されるJSON[ノードコレクション](#nodeCollection)の例(<Node>はNodeオブジェクトを表します。)

```json
{
	"data": {
		"metaData": {
			"application": "NIS",
			"version": "0.4.33-BETA",
			"platform": "Oracle Corporation (1.8.0_25) on Windows 8"
		},
		"endpoint": {
			"protocol": "http",
			"port": 7890,
			"host": "81.224.224.156"
		},
		"identity": {
			"name": "Alice",
			"public-key": "a1aaca6c17a24252e674d155713cdf55996ad00175be4af02a20c67b59f9fe8a"
		}
	}
}
```

可能性のあるエラー：ノードがまだ起動されていない場合、NISはJSONエラーオブジェクトを返します。エラーの詳細についてはエラーオブジェクト([Error object](#error-object))、もしくはNISエラー([NIS Errors](#appendix-B:-NIS-errors))を参照してください。

#### 5.2.3.稼働中の近辺

公式情報：[Active neighborhood](http://bob.nem.ninja/docs/#active-neighborhood)

*   APIパス：/node/peer-list/active
*   リクエストタイプ：GET
*   概要：ブロードキャストのために選択された近辺のアクティブなノードの配列を取得します。
*   パラメータ：無し。
*   例：http://127.0.0.1:7890/node/peer-list/active
*   返されるJSON[ノードコレクション](#nodeCollection)の例(<Node>はNodeオブジェクトを表します。)

```json
{
	"data": {
		"metaData": {
			"application": "NIS",
			"version": "0.4.33-BETA",
			"platform": "Oracle Corporation (1.8.0_25) on Windows 8"
		},
		"endpoint": {
			"protocol": "http",
			"port": 7890,
			"host": "81.224.224.156"
		},
		"identity": {
			"name": "Alice",
			"public-key": "a1aaca6c17a24252e674d155713cdf55996ad00175be4af02a20c67b59f9fe8a"
		}
	}
}
```

可能性のあるエラー：ノードがまだ起動されていない場合、NISはJSONエラーオブジェクトを返します。エラーの詳細についてはエラーオブジェクト([Error object](#error-object))、もしくはNISエラー([NIS Errors](#appendix-B:-NIS-errors))を参照してください。

#### 5.2.4.稼働している近辺の最大チェーンの高さ

公式情報：[Maximum chain height in the active neighborhood](http://bob.nem.ninja/docs/#maximum-chain-height-in-the-active-neighborhood)

*   APIパス：/node/active-peers/max-chain-height
*   リクエストタイプ：GET
*   概要：アクティブなノードリスト([稼働している近辺](#active-neighborhood))にあるすべてのノードからチェーンの高さを要求し、表示されている最大の高さを返します。
*   パラメータ：無し。
*   例：http://127.0.0.1:7890/node/active-peers/max-chain-height
*   返されるJSON ブロックの高さ([BlockHeight](#blockHeight))オブジェクトの例

```json
{
    "height": 43920
}
```

可能性のあるエラー：ノードがまだ起動されていない場合、NISはJSONエラーオブジェクトを返します。エラーの詳細についてはエラーオブジェクト([Error object](#error-object))、もしくはNISエラー([NIS Errors](#appendix-B:-NIS-errors))を参照してください。

### 5.3.ノードエクスペリエンスのリクエスト

公式情報：[Requesting node experiences](http://bob.nem.ninja/docs/#requesting-node-experiences)

*   APIパス：/node/experiences
*   リクエストタイプ：GET
*   概要：別のノードからノードエクスペリエンスの配列を取得します。各ノードは他のノードとの経験を内部マップに保存します。経験を共有することにより、ノードはコミュニケーションのための正確なノードを選択するのに役立ちます。
*   パラメータ：無し。
*   例：http://127.0.0.1:7890/node/experiences
*   返されるJSON エクステンドノードエクスペリエンスペア([ExtendedNodeExperiencePair](#extendedNodeExperiencePair))オブジェクト配列の例

```json
{
	"data": {
		"node": {
			"metaData": {
				"application": "NIS",
				"version": "0.4.33-BETA",
				"platform": "Oracle Corporation (1.8.0_25) on Windows 8"
			},
			"endpoint": {
				"protocol": "http",
				"port": 7890,
				"host": "81.224.224.156"
			},
			"identity": {
				"name": "Alice",
				"public-key": "a1aaca6c17a24252e674d155713cdf55996ad00175be4af02a20c67b59f9fe8a"
			},
			"syncs": 3,
			"experience": {
				"s": 1,
				"f": 0
			}
		}
	}
}
```

可能性のあるエラー：ノードがまだ起動されていない場合、NISはJSONエラーオブジェクトを返します。エラーの詳細についてはエラーオブジェクト([Error object](#error-object))、もしくはNISエラー([NIS Errors](#appendix-B:-NIS-errors))を参照してください。

### 5.4.ローカルノードの起動

公式情報：[Booting the local node](http://bob.nem.ninja/docs/#booting-the-local-node)

*   APIパス：/node/boot
*   リクエストタイプ：POST
*   概要：ローカルノードを起動し、ローカルノードにアカウント(ID)を割り当てます。
*   パラメータ：bootNodeRequest：ブートノードリクエスト([Error object](#bootNodeRequest“>BootNodeRequest)で説明されている、ブートノードリクエスト JSONオブジェクト。
*   例：リクエストはブラウザでは実行できません。
*   返り値無し。
*   可能性のあるエラー：ノードが既にブートされている場合、NISはJSONエラーオブジェクトを返します。エラーの詳細についてはエラーオブジェクト(<a href=")" href=""></a>)、もしくはNISエラー([NIS Errors](#appendix-B:-NIS-errors))を参照してください。

## 6.ネームスペースとモザイク

公式情報：[Namespaces and Mosaics](http://bob.nem.ninja/docs/#namespaces-and-mosaics)

### 6.1.ネームスペース

公式情報：[Namespaces](http://bob.nem.ninja/docs/#namespaces)

NEMはインターネットドメイン名のNEMアナログであるネームスペース(Namespace)の概念をサポートしています。ネームスペースはドットで連結された1つ以上の部分で構成される識別文字列です(例： 『makoto.metals.silver』)。

すべてのネームスペースは唯一であり、一度に1人の所有者しか持てません。1つしかないネームスペースはルートネームスペースと呼ばれ、それ以外の場合はサブネームスペースと呼ばれます。

ルートネームスペースは1年間、アカウントでレンタルすることができ、ルートネームスペースが期限切れになる1か月前にレンタル契約をもう1年更新することができます。

ルートネームスペースのレンタル契約が更新された場合、すべてのサブネームスペースはもう1年有効です。ルートネームスペースが更新されない場合は、すべてのサブネームスペースとともに終了します。

ルートネームスペースの有効期限が切れてから1ヶ月後に別のアカウントでそのルートネームスペースをレンタルすることができます。ただし、新しい所有者は以前の所有者のサブネームスペースを継承しません。アカウントは、対応するルートネームスペースを所有している場合にのみサブネームスペースをレンタルすることができます。

ネームスペースにはパーツに許容される文字やパーツの長さに関して一定の制限があります。ルート名前空間の長さは16文字、サブネームスペースの長さは64文字です。

有効な文字は次のとおりです。ただし、ネームスペースはアルファベットの文字で始まる文字のみが許可され、『alice』はルートネームスペースの許可された文字ですが、 『1alice』は許可されません。
`a, b, c, ..., z, A, B, C, ..., Z, 0, 1, 2, ..., 9, _ , -`

使用不可リストは以下の通りです。
`nem, user, account, org, com, biz, net, edu, mil, gov and info.`

以上の使用不可リストは最終的なものではなく、将来追加される場合があります。

『user.alice』または 『alice.user』はNEMネームスペースシステムでは使用できません。ネームスペースには最大3つの部分であるため、 『makoto.metals.silver』は有効で、『makoto.metals.silver.coin』は有効ではありません。

ネームスペースのレンタル契約は、ネームスペーストランザクションの準備([ProvisionNamespaceTransaction](#provisionNamespaceTransaction))を介して行われます。通常のトランザクション手数料に加えて、賃貸料があります。この手数料はアドレスを持つ特別なアカウントである、レンタルフィーシンク(rental fee sink)に支払われます。

*   NAMESPACEWH4MKFMBCVFERDPOOP4FK7MTBXDPZZA (メインネット内)
*   TAMESPACEWH4MKFMBCVFERDPOOP4FK7MTDJEYP35 (テストネット内

1年間のネームスペースレンタル料は以下の通りです。

*   5000 XEM (ルートネームスペース)
*   200 XEM (サブネームスペース)

ハードフォーク(仕様変更)前のネームスペースレンタル料は以下の通りです(現在は使用されていない)。

*   50000 XEM (ルートネームスペース)
*   5000 XEM (サブネームスペース)

モザイクを作成するにはネームスペースの所有権が必要です。

#### 6.1.1.ルートネームスペースの取得

公式情報：[Retrieving root namespaces](http://bob.nem.ninja/docs/#retrieving-root-namespaces)

*   APIパス：/namespace/root/page
*   リクエストタイプ：GET
*   概要：ルートネームスペースを取得します。リクエストはページングをサポート、つまり指定されたサイズのバッチでルートネームスペースを検索します。リクエストはネームスペースメタデータペア([NamespaceMetaDataPair](#namespaceMetaDataPair))オブジェクトの配列を返します。
*   パラメータ：id：ルートネームスペースが返される最上位のネームスペースデータベースID。パラメータはオプションです。指定されていない場合には最新のレンダリングされたルートネームスペースが返されます。
*   パラメータ：pagesize：リクエストごとに返されるネームスペースオブジェクトの数。パラメータはオプションです。デフォルト値は25、最小値は5、最大値は100です。
*   例：http://127.0.0.1:7890/namespace/roots?id=26754&pageSize;=35
*   返されるJSON オブジェクトの例

```json
{
	"data": [
		{
			"meta": {
				"id": 26264
			},
			"namespace": {
				"fqn": "makoto.metal.coins",
				"owner": "TD3RXTHBLK6J3UD2BH2PXSOFLPWZOTR34WCG4HXH",
				"height": 13465
			}
		},
		{
			"meta": {
				"id": 25421
			},
			"namespace": {
				"fqn": "gimre.vouchers",
				"owner": "TDGIMREMR5NSRFUOMPI5OOHLDATCABNPC5ID2SVA",
				"height": 12392
			}
		}
	]
}
```

可能性のあるエラー：無し。

#### 6.1.2.特定のネームスペースを取得

公式情報：[Retrieving a specific namespace](http://bob.nem.ninja/docs/#retrieving-a-specific-namespace)

*   APIパス：/namespace
*   リクエストタイプ：GET
*   概要：指定されたIDを持つネームスペースを取得します。
*   パラメータ：namespace：ネームスペースのID。
*   例：http://127.0.0.1:7890/namespace?namespace=makoto.metal.coins
*   返されるJSON オブジェクトの例
*   

`{ "fqn": "makoto.metal.coins", "owner": TD3RXTHBLK6J3UD2BH2PXSOFLPWZOTR34WCG4HXH", "height": 13465 }`
可能性のあるエラー：ネームスペースパラメータがないか無効である場合、NISはエラーを返します。エラーの詳細についてはNISエラー([NIS Errors](#appendix-B:-NIS-errors))を参照してください。

### 6.2.モザイク

公式情報：[Mosaics](http://bob.nem.ninja/docs/#mosaics)

NEMモザイクは追加のプロパティおよびその他の機能を公開する資産(assets)です。各モザイクには基本的なモザイクの定義があります。モザイク定義を作成できるようにするには、アカウントにモザイク定義が参照できる少なくとも1つのルートネームスペースをレンタルする必要があります。

モザイク定義の基本データは以下の通りです。

mosaic id：モザイクIDはネームスペースIDとモザイク名の2つの部分で構成されます。文字列としてモザイクIDを表すとき、2つの部分は『*』で連結されます。例えば、名前空間idが 『makoto.metals.silver』でモザイク名が『coin』の場合、文字列表現は『makoto.metals.silver * coin』となります。 モザイクIDは唯一でなければならないので、モザイク名はモザイク定義が参照するネームスペース内で唯一でなければなりません。また、モザイク名の最大長は32文字です。

モザイクIDの有効な文字は次のとおりです。ただし最初の文字はアルファベットでなければなりません。
`a, b, c, ..., z, 0, 1, 2, ..., 9, ', _ , -`

description：各概要(description)にはモザイクの説明が必要です。説明は512文字を超えることはできません。なお、説明に使用される文字に制限はありません。

properties：モザイクの動作は一連のプロパティによってカスタマイズできます。プロパティが指定されていない場合はデフォルトのプロパティが適用されます。

サポートされているプロパティは以下のとおりです。

*   initialSupply：作成者は定義を作成するときにモザイクの初期供給を指定できます。供給は最小のサブユニットではなく、モザイクのユニット全体で行われます。初期供給量は0?9,000,000,000の範囲でなければなりません。デフォルト値は『1000』です。
*   divisibility：可分性(divisibility)はモザイクを小数点何以下に分割できるかを決定します。つまり、可分性が3の場合はモザイクが0.001モザイクまで分割出来る事を意味しています。また、ミリモザイクは最小のサブユニットです。転送トランザクションを介してモザイクを転送する場合、転送される数量はそれらの最小パーツの倍数で与えられます。
*   supplyMutable：作成者はモザイク供給を後に変更可能、あるいは供給不可を選択できます。プロパティの値は『true』もしくは『false”』です。デフォルト値は『false』です。
*   transferable：作成者はモザイク定義が作成者以外のアカウント間でモザイクの転送を許可する必要があるかどうかを選択できます。『transferable』プロパティが『false』に設定されている場合、送信者または受信者として作成者を持つ転送トランザクションのみがそのタイプのモザイクを転送できます。『true』に設定するとモザイクを任意のアカウントとの間でやりとりできます。プロパティの値は『true』と『false』です。デフォルト値は『true』です。
*   levy：作成者はそのタイプのモザイクを転送するたびに送信者から特別料金が徴収され、選択した口座への送信を要求することができます(この手数料の受領者として自分の残高を指定することができます)。
*   

levyデータは以下のとおりです。

*   fee type：絶対料金(absolute fee)とパーセンタイル料金(percentile fee)があります。
*   *   絶対料金：手数料は絶対量として指定されているため、転送される数量には依存しません。
*   パーセンタイル料金：料金は転送される数量のパーセンタイルの倍数として指定されます。 転送されたモザイクの量に応じて料金は直線的に増加します。recipient：課徴金の受領者。 これはどのアカウントでもかまいません。
*   mosaic id：料金を支払う必要があるモザイクのIDです。既存のモザイクIDを指定できます。作成者がXEMで料金を支払うことを希望する場合、モザイクID『nem:xem』を使用しなければなりません。
*   fee：この解釈はフィールド『fee type』に依存します(上記参照)。

モザイク定義はモザイク定義作成トランザクション([MosaicDefinitionCreationTransaction](#mosaicDefinitionCreationTransaction))によって作成することができます。通常のトランザクション手数料に加えて、作成料があります。この手数料はアドレスを持つ特別なアドレスであるクリエイションフィーシンク(creation fee sink)に支払われます。

*   NBMOSAICOD4F54EE5CDMR23CCBGOAM2XSIUX6TRS (メインネット内)
*   TBMOSAICOD4F54EE5CDMR23CCBGOAM2XSJBR5OLC (テストネット内)

モザイク定義の作成料は500XEMです(ハードフォーク前は50000XEM)。

なお、XEMコインを表す、事前に定義されたモザイクがあります。次のとおりです。

*   namespace: nem
*   name: xem
*   initial supply: 8,999,999,999
*   divisibility: 6
*   supply mutable: false
*   transferable: true
*   levy: none

#### 6.2.1モザイク定義の取得

公式情報：[Retrieving mosaic definitions](http://bob.nem.ninja/docs/#retrieving-mosaic-definitions)

*   APIパス：/namespace/mosaic/definition/page

リクエストタイプ：GET
*   概要：指定されたネームスペースのモザイク定義を取得します。リクエストはページングをサポートします。リクエストはモザイク定義メタデータペア([MosaicDefinitionMetaDataPair](#mosaicDefinitionMetaDataPair))オブジェクトの配列を返します。
*   パラメータ：namespace：ネームスペースのID。
*   パラメータ：id：ルートモザイク定義が返される最上位のモザイク定義データベースID。パラメータはオプションです。指定されていない場合、最新のモザイク定義が返されます。
*   パラメータ：pagesize：各要求に対して返されるモザイク定義のオブジェクト数。パラメータはオプションです。デフォルト値は25、最小値は5、最大値は100です。
*   例：http://127.0.0.1:7890/namespace/mosaic/definition/page?namespace=makoto.metal.coins
*   返されるJSON オブジェクトの例

```json
{
	"data": [
		{
			"meta": {
				"id": 3541
			},
			"mosaic": {
				"creator": "10cfe522fe23c015b8ab24ef6a0c32c5de78eb55b2152ed07b6a092121187100",
				"id": {
					"namespaceId": "makoto.metal.coins",
					"name": "silver coin"
				},
				"description": "Real silver coins, pure silver",
				"properties": [
					{
						"name": "divisibility",
						"value": "0"
					},
					{
						"name": "initialSupply",
						"value": "1000"
					},
					{
						"name": "supplyMutable",
						"value": "false"
					},
					{
						"name": "transferable",
						"value": "true"
					}
				]
			}
		}
	]
}
```

可能性のあるエラー：ネームスペースパラメータがないか無効である場合、NISはエラーを返します。エラーの詳細についてはNISエラー([NIS Errors](#appendix-B:-NIS-errors))を参照してください。

## 7.トランザクションの開始

公式情報：[Initiating transactions](http://bob.nem.ninja/docs/#initiating-transactions)

トランザクションとは、あるアカウントから別のアカウントにNEMやメッセージを転送する方法です。

トランザクションが開始された直前はまだ未確認であり、ネットワークによってまだ受け入れられていません。また、この時点でそれがブロックに含まれるかどうかはまだ明確ではありません。状態が『未確認(unconfirmed)』のトランザクションには決して依存しないでください。

ブロックに含まれるとトランザクションが処理され、転送トランザクションの場合、トランザクションで指定された金額が送信者のアカウントから受信者のアカウントに転送されます。さらにトランザクション手数料は送付者の口座から差し引かれます。この時点でトランザクションには0件の確認があります。

ブロックチェーンに別のブロックが追加されると、トランザクションは1つの確認を行い、チェーンに追加された次のブロックは2回の確認などを行います。

暗号通貨にはブロックチェーンの一部をロールバックする機能があります。これは、ブロックチェーンのフォーク(分岐)を解決するために不可欠です。ただし、ロールバックできるブロックの最大数があります。これは書き換え制限と呼ばれます。

したがって、フォークは特定の深さまでしか解決できません。NEMの書き換え限界は360ブロックです。トランザクションの確認が360回を超えると、それを元に戻すことはできません。

実際の運用では、コードのバグや何らかの攻撃など、ブロックチェーンに重大な問題がなければ、20ブロックよりも深いフォークは起こりません。

クライアントは、次の2つの方法でトランザクションを開始できます。

*   クライアントがトランザクションデータに署名できない場合、RequestPrepareAnnounce JSONオブジェクトをNISに送信することによって、ローカルNISが署名を行うことができます。 詳細については、アナウンス準備のリクエスト([RequestPrepareAnnounce](#requestPrepareAnnounce))を参照してください。
*   

**警告：/ transaction / prepare-announce APIは『TRUSTED』および『LOCAL』ノードでのみ使用されます。**

注：NCCはこのAPIを使用しないことに注意してください。それはそれ自身のすべてのトランザクション署名を行います。
クライアントがed25519の実装を持っている場合、トランザクションに署名することができれば、RequestAnnounce JSONオブジェクトをNISに送ることができます。これにより、信頼できないリモートNISを使用してトランザクションを送信できるという利点があります。 このオブジェクトの詳細については、リクエストのアナウンス([RequestAnnounce](#requestAnnounce))を参照してください。

ほとんどのクライアントはローカルのNISに依存してトランザクション署名を作成します。6.1章から6.6章ではトランザクション関連のアクションについて説明しています。

6.7章では署名が必要なデータを収集するための手順と、トランザクションを第2の方法で開始する方法について説明しています。ただし、署名の作成方法については説明していません。これはこのドキュメントの範囲外の暗号概念を含むためです。

### 7.1.トランザクションの開始

公式情報：[Initiating a transaction](http://bob.nem.ninja/docs/#initiating-a-transaction)

*   APIパス：/transaction/prepare-announce
*   リクエストタイプ：POST
*   概要：トランザクションを作成してブロードキャストします。このリクエストにはアカウントの秘密鍵が含まれるため、ローカルNISにのみ送信する必要があります。
*   パラメータ：requestPrepareAnnounce：リクエスト準備(RequestPrepare)は、アナウンス準備のリクエスト([RequestPrepareAnnounce](#requestPrepareAnnounce))の説明に従ってJSONオブジェクトをアナウンスします。
*   例：リクエストはブラウザでは実行できません。
*   返されるJSON Nemアナウンスリザルト([NemAnnounceResult](#nemAnnounceResult)) オブジェクトの例

```json
{
	"type": 1,
	"code": 1,
	"message": "SUCCESS",
	"transactionHash": {
		"data": "c1786437336da077cd572a27710c40c378610e8d33880bcb7bdb0a42e3d35586"
	},
	"innerTransactionHash": {
		"data": "cc317a7674d56352b4c711096a7594bd11908bf518293a191fc2faa12eac0fbb"
	}
}
```

可能性のあるエラー：トランザクションの検証が失敗が原因によるエラーはさまざまです。エラーの詳細についてはエラーオブジェクト([Error object](#error-object))、もしくはNISエラー([NIS Errors](#appendix-B:-NIS-errors))を参照してください。
*   

最も一般的なエラーは次のとおりです。

    *   送信者アカウントに十分な資金がありません。(The sender account has not enough funds.)
    *   タイムスタンプがあまりにも先のため無効です。(The timestamp is invalid because it lies too far in the future.)
    *   すでに通過しているためdeadlineは無効です。(The deadline is invalid because it has already been passed.)
    *   添付されたメッセージが大きすぎます。(The attached message is too large.)
    *   トランザクションは既に知られています。(The transaction is already known.)
    *   このトランザクションと競合する別のトランザクションがあります。これは重要度を別のアカウントに転送しようとしているときに発生します。(There is another transaction conflicting with this transaction. This can happen when trying to transfer the importance to another account.)

### 7.2.転送トランザクションの開始

公式情報：[Initiating a transfer transaction](http://bob.nem.ninja/docs/#initiating-a-transfer-transaction)

NISはバージョン1または2の転送トランザクションをサポートしています。バージョン1の転送トランザクションはメッセージとXEMコインのみを転送でき、バージョン2の転送トランザクションはモザイクセットも転送できます。

#### 7.2.1.転送トランザクションバージョン1

公式情報：[Version 1 transfer transactions](http://bob.nem.ninja/docs/#version-1-transfer-transactions)

送信者アカウント(TALICELCD3XPH4FFI5STGGNSNSWPOTG5E4DS2TOS)(以下『Alice』といいます)から受信者アカウントへ1000 NEMを送信するとします。

受信者アカウント(TBOBBSXX7BESJXDWGLP5Z7FM5HSTKUH5WIMPW562)です。

POSTリクエストを介してNISに送信する必要のあるアナウンス準備のリクエスト(RequestPrepareAnnounce) JSONオブジェクトは、これと同じようになります(テストネットワーク)。

```json
{
	"transaction": {
		"timeStamp": 9111526,
		"amount": 1000000000,
		"fee": 3000000,
		"recipient": "TBOBBSXX7BESJXDWGLP5Z7FM5HSTKUH5WIMPW562",
		"type": 257,
		"deadline": 9154726,
		"message": {
			"payload": "",
			"type": 1
		},
		"version": -1744830463,
		"signer": "a1aaca6c17a24252e674d155713cdf55996ad00175be4af02a20c67b59f9fe8a"
	},
	"privateKey": "00983bb01d05edecfaef55df9486c111abb6299c754a002069b1d0ef4537441bda"
}
```

NISは署名を作成するため、オブジェクトのトランザクション部分に署名がないことに注意してください。

また『version』フィールドには、値を16進数のシステムに変換するときに見られるネットワークバージョンとトランザクションバージョンの両方が含まれています(-1744830463 = 0x98000001(ネットワークバージョン0x98およびトランザクションバージョン0x01)。

送信者アカウントのトランザクションに十分な資金がある場合、NISはJSONオブジェクトで応答します。

```json
{
	"type": 1,
	"code": 1,
	"message": "SUCCESS",
	"transactionHash": {
		"data": "c1786437336da077cd572a27710c40c378610e8d33880bcb7bdb0a42e3d35586"
	},
	"innerTransactionHash": {}
}
```


#### 7.2.2.転送トランザクションバージョン2

公式情報：[Version 2 transfer transactions](http://bob.nem.ninja/docs/#version-2-transfer-transactions)

転送トランザクションバージョン2では、前の章で説明したようにメッセージとXEMを転送できますが、唯一の違いはテストネットでは-1744830462 = 0x98000002、メインネットでは1744830466 = 0x68000002です。

しかし、転送トランザクションバージョン2はモザイクも転送できるので、より強力です。

可分性0のid『makoto.metals.silver * coin』を持つモザイクをすでに作成していて、100 XEMの転送でそれらモザイクの転送を紐付けしたいとします。 3つのsilver coin モザイクと300 XEMを1回の転送トランザクションで転送するには、次のようなアナウンス準備のリクエスト(RequestPrepareAnnounce) JSONオブジェクトをNISに発行します。

```json
{
	"transaction": {
		"timeStamp": 9111526,
		"amount": 3000000,
		"fee": 30000000,
		"recipient": "TBOBBSXX7BESJXDWGLP5Z7FM5HSTKUH5WIMPW562",
		"type": 257,
		"deadline": 9154726,
		"message": {"payload": "", "type": 1},
		"version": -1744830462,
		"signer": "a1aaca6c17a24252e674d155713cdf55996ad00175be4af02a20c67b59f9fe8a",
		"mosaics": [
			{
				"mosaicId": {"namespaceId": "makoto.metals.silver", "name": "coin"},
				"quantity": 1
			},
			{
				"mosaicId": {"namespaceId": "nem", "name": "xem"},
				"quantity": 100000000
			}
		]
	},
	"privateKey": "00983bb01d05edecfaef55df9486c111abb6299c754a002069b1d0ef4537441bda"
}
```

転送トランザクションには2つのモザイクが添付されています。

*   『makoto.metals.silver * coin』というidを持つモザイク。モザイクに使用可能な最小単位の1を表します。そのモザイクの可分性は0であるので(上記で仮定したように)、その量は1単位、すなわち1コインを表します。
*   『id ‘nem * xem』(これは通常のXEMコインを表す特別なXEMモザイクです)を持つモザイクは、6の可分性を持つため、100000000の数量は100 XEMを表します。

この例ではアタッチメントを1つのsilverモザイクと100のXEMを保持するモザイクの袋であると見なすことができます。

トランザクションのamountフィールドは、添付物によるトランザクションにより異なって解釈されます。

アタッチメントに記載された数量を掛ける数は金額を1,000,000で割ることによって与えられます(このバージョンでは、NISは分数転送をサポートしていません)。この例では3,000,000 / 1,000,000 = 3であり、アタッチメントが3回送信され、3つのsilverモザイクと300XEMが受信者に送信されます。

トランザクションが拒否される一般的な理由は次のとおりです。

*   アタッチメントで指定された少なくとも1つのモザイクはNISで認識しません。
*   送信者はアタッチメントで指定された少なくとも1つのタイプに十分なモザイクを所有していません。
*   アタッチメントで指定された少なくとも1つのモザイクは転送不可と定義され、送信者と受信者の両方がその作成者ではありません

モザイク『makoto.metals.silver * coin』のモザイク定義に、silverモザイクを含む送信ごとにXEMをアドレス付きの受取人に支払わなければならない旨の課金(levy)セクションがある場合、『TDGOGOGOWZJ3HU4F6CUM5IKE7GHG4FFTF5BZ7JPW』は転送トランザクションによって、トランザクション転送者から10XEMの送信が『TDGOGOGOWZJ3HU4F6CUM5IKE7GHG4FFTF5BZ7JPW』に自動的に誘導されます。

### 7.3.アカウントをマルチシグアカウントに変換する

公式情報：[Converting an account to a multisig account](http://bob.nem.ninja/docs/#converting-an-account-to-a-multisig-account)

NISはn個のマルチシグ(multisig)アカウントのうちのm個をネイティブにサポートします。

これは残高がn個の共同署名を有するマルチシグ残高に変換され、これらの共同者のうちのm人がトランザクションを完了するためにマルチシグ残高からトランザクションに署名する必要があることを意味しています。

通常のアカウントをマルチシグアカウントに変換するには、マルチシグ集計変更トランザクション([MultisigAggregateModificationTransaction](#multisigAggregateModificationTransaction))をネットワークに送信する必要があります。

Aliceを公開鍵で変換したいと仮定した場合、以下のとおりです。

*   アカウント『Alice』：公開鍵：a1aaca6c17a24252e674d155713cdf55996ad00175be4af02a20c67b59f9fe8a
*   

3つのうち2つのマルチシグアカウントというのは、少なくとも2つの署名者がマルチシグトランザクションを完了するために署名する必要があることを意味します。
署名者『Bob』：アドレス：TBOBBSXX7BESJXDWGLP5Z7FM5HSTKUH5WIMPW562：公開鍵：6083df7119d43e815ed2967c795f806f6b73f8f92a56a7611e3848816ec50958
*   署名者『jusan』：アドレス：TBJUSANZ63AKNJ57XMK6Y2IBH55UNNRXJFZRDTRW：公開鍵：0662ed29cbfa7038530fb7f52df865eed6708d51bc7a24bcd05db35185b53c70
*   署名者『go』：アドレス：TDGOGOGOWZJ3HU4F6CUM5IKE7GHG4FFTF5BZ7JPW：公開鍵：cc61676a4275abcffd10a9ea1081091ff054a1a8a720429256aebf8034aab099

以下に似たJSONオブジェクト(テストネットワーク)を作成する必要があります。

```json
{
	"transaction": {
		"timeStamp": 9111526,
		"fee": 28000000,
		"type": 4097,
		"deadline": 9154726,
		"version": -1744830462,
		"signer": "a1aaca6c17a24252e674d155713cdf55996ad00175be4af02a20c67b59f9fe8a",
		"modifications": [
			{
				"modificationType": 1,
				"cosignatoryAccount": "6083df7119d43e815ed2967c795f806f6b73f8f92a56a7611e3848816ec50958"
			},
			{
				"modificationType": 1,
				"cosignatoryAccount": "0662ed29cbfa7038530fb7f52df865eed6708d51bc7a24bcd05db35185b53c70"
			},
			{
				"modificationType": 1,
				"cosignatoryAccount": "cc61676a4275abcffd10a9ea1081091ff054a1a8a720429256aebf8034aab099"
			}
		],
		"minCosignatories": {
			"relativeChange": 2
		}
	},
	"privateKey": "00983bb01d05edecfaef55df9486c111abb6299c754a002069b1d0ef4537441bda"
}
```

なお、NISによって署名されるため、署名はありません。

トランザクションがNISによって署名され、ブロックにそれを含めることによってネットワークに受け入れられた結果、アカウント『Alice』は2/3マルチシグアカウントになりました。

### 7.4.マルチシグトランザクションの開始

公式情報：[Initiating a multisig transaction](http://bob.nem.ninja/docs/#initiating-a-multisig-transaction)

上記で述べたように、署名者(Bob、Jusan、Go)のうちの一名のみが、アカウントAliceのトランザクションを作成することができます。

BobはアカウントAliceからアカウントJusanに1000NEMを送信する転送トランザクションを開始したいと考えます。

アカウントAliceはマルチシグアカウントなので、転送トランザクション(JSONオブジェクトの『otherTrans』構造)はマルチシグトランザクション([MultisigTransaction](#multisigTransaction))へ包括する必要があります。

対応するアナウンス準備のリクエスト(RequestPrepareAnnounce)オブジェクトは、次のようになります(テストネットワーク)。

```json
{
	"transaction": {
		"timeStamp": 9111526,
		"fee": 3000000,
		"type": 4100,
		"deadline": 9154726,
		"version": -1744830463,
		"signer": "6083df7119d43e815ed2967c795f806f6b73f8f92a56a7611e3848816ec50958",
		"otherTrans": {
			"timeStamp": 9111526,
			"amount": 1000000000,
			"fee": 4000000,
			"recipient": "TBJUSANZ63AKNJ57XMK6Y2IBH55UNNRXJFZRDTRW",
			"type": 257,
			"deadline": 9154726,
			"message": {
				"payload": "",
				"type": 1
			},
			"version": -1744830463,
			"signer": "a1aaca6c17a24252e674d155713cdf55996ad00175be4af02a20c67b59f9fe8a"
		},
		"signatures": []
	},
	"privateKey": "00a6e2526b5cc84f9174c4ff050ca352623061115951c649b36b08409c4ccb7b2e"
}
```

NISはトランザクションに署名し、それを公表します。

今回返されたNemアナウンスリザルト(NemAnnounceResult)オブジェクトには、内部トランザクションのハッシュ(上記構造のotherTrans)が含まれています。

```json
{
	"type": 1,
	"code": 1,
	"message": "SUCCESS",
	"transactionHash": {
		"data": "c1786437336da077cd572a27710c40c378610e8d33880bcb7bdb0a42e3d35586"
	},
	"innerTransactionHash": {
		"data": "44e4968e5aa35fe182d4def5958e23cf941c4bf809364afb4431ebbf6a18c039"
	}
}
```

ハッシュは上記のトランザクションのためにマルチシグ署名トランザクションを作成するノードによって必要とされます。

この時点でトランザクションをブロックに含めることはできません(そして、されないでしょう)。なぜなら、他の共同署名者のJusanとGoはまだいずれのトランザクションにも署名していないからです…

#### 7.4.1.マルチシグトランザクションの署名

公式情報：[Cosigning multisig transaction](http://bob.nem.ninja/docs/#cosigning-multisig-transaction)

…と、そうするためにはJusanまたはGoはマルチシグ署名トランザクション([MultisigSignatureTransaction](#multisigSignatureTransaction))を開始する必要があります。

Jusanはこれに似たアナウンス準備のリクエスト(equestPrepareAnnounce) JSONオブジェクト(テストネットワーク)を作成する必要があります。

```json
{
	"transaction": {
		"timeStamp": 9111526,
		"fee": 6000000,
		"type": 4098,
		"deadline": 9157365,
		"version": -1744830463,
		"signer": "0662ed29cbfa7038530fb7f52df865eed6708d51bc7a24bcd05db35185b53c70",
		"otherHash": {
			"data": "44e4968e5aa35fe182d4def5958e23cf941c4bf809364afb4431ebbf6a18c039"
		},
		"otherAccount": "TALICELCD3XPH4FFI5STGGNSNSWPOTG5E4DS2TOS"
	},
	"privateKey": "00be34fdb20a9f6fed51376f0bab9f25ea7a48d610324588a6b203d0a1a6db4bc1"
}
```

JusanはBobの要求からNISによって返されたハッシュ『otherHash』を使用したことに注意してください。

NISがトランザクションに署名してネットワークに送信した後、署名トランザクションはマルチシグトランザクションに付与されます。

JusanがBobが開始したマルチシグトランザクションに署名すると、3つの署名者のうちの2つが内部転送トランザクション(マルチシグトランザクションを開始することによって間接的に署名されたBob)に署名し、マルチシグトランザクションをブロックに含めることができます。

### 7.5.署名者の追加と削除

公式情報：[Adding and removing cosignatories](http://bob.nem.ninja/docs/#adding-and-removing-cosignatories)

マルチシグアカウントの署名者リストを変更することは可能です。これはマルチシグトランザクションで包括された集計変更トランザクションを介して行われます。

マルチシグアカウントAliceに新たな署名者『Hachi』を追加し、トランザクションを完了するために必要な署名者の最小値を2から3に増やしたいとします。

*   署名者『hachi』：アドレス：TDHACHIMHRBBRHR57SR3BDBFFWDTYVSLGMFKIDOR：公開鍵：6c66ea288522990db7a0a63c9c20f532cdcb68dc3c9544fb20f7322c92ceadbb

これを行うためには、既存の署名者の1人が(ここではJusanと仮定して)対応するマルチシグトランザクション(テストネットワーク)を開始する必要があります。

```json
{
	"transaction": {
		"timeStamp": 9111526,
		"fee": 6000000,
		"type": 4100,
		"deadline": 9154726,
		"version": -1744830462,
		"signer": "6083df7119d43e815ed2967c795f806f6b73f8f92a56a7611e3848816ec50958",
		"otherTrans": {
			"timeStamp": 9111526,
			"fee": 16000000,
			"type": 4097,
			"deadline": 9154726,
			"version": -1744830462,
			"signer": "a1aaca6c17a24252e674d155713cdf55996ad00175be4af02a20c67b59f9fe8a",
			"modifications": [
				{
					"modificationType": 1,
					"cosignatoryAccount": "6c66ea288522990db7a0a63c9c20f532cdcb68dc3c9544fb20f7322c92ceadbb"
				}
			],
			"minCosignatories": {
				"relativeChange": 1
			}
		},
		"signatures": []
	},
	"privateKey": "00be34fdb20a9f6fed51376f0bab9f25ea7a48d610324588a6b203d0a1a6db4bc1"
}
```

NISがネットワークに署名してそのトランザクションをネットワークにブロードキャストした後、他の2つの署名者のうち1人はトランザクションに署名する必要があります。

トランザクションがブロックに正常に挿入された後、アカウントAliceは3/4のマルチシグアカウントとなります。

後にBob、Jusan、Goが署名者『Hachi』を削除して2/3マルチシグアカウントにする場合は、署名者の1人が上記と同様のトランザクションを開始することができますが、今回は『modificationType』を2に設定し、署名者の最小相対変化値-1を使用します。

署名者を削除するためには削除済みを除いて、すべての署名者がトランザクションに署名する必要があります。 一度ネットワークによって承認されると、署名者『hachi』はもはやマルチシグアカウント『Alice』の署名者ではありません。

警告：**アカウントの削除は最終的なものではなく、変更の対象となる可能性があります。**

### 7.6.マルチシグアカウントの使用方法

公式情報：[How to use a multisig account](http://bob.nem.ninja/docs/#how-to-use-a-multisig-account)

マルチシグアカウントの目的はアカウントをより安全にすることです。 しかし、これはマルチシグアカウントを使用するときにミスをしていないユーザーに依存しています。

たとえば、マルチシグアカウントアカウントの署名者すべての秘密鍵が1台のコンピュータに存在する場合、マルチシグアカウントは本質的に通常アカウントと同じ状態です。もし、そのコンピュータが一度の攻撃で侵害された場合にはすべての秘密鍵が公開されます。

そのため、異なる場所にある別のコンピュータに署名者の秘密鍵を持つことが不可欠です。

[マルチシグトランザクションの開始](http://bob.nem.ninja/docs/#initiating-a-multisig-transaction)を読んでいれば、マルチシグトランザクションに署名できるようにするには、マルチシグトランザクションの署名者が内部トランザクションのハッシュを知っていなければならないことがわかります。

そのハッシュの知識を得るには2つの方法があります。

*   マルチシグトランザクションの作成者は(NISによって返されたJSONオブジェクトに含まれる)ハッシュを書き出し、そのハッシュを署名者に送信します。
*   署名者はローカルNISを使って未確認トランザクションを記録します。[未確認トランザクション](#unconfirmed-transactions)の章で説明したように、未確認トランザクション(unconfirmed transaction)JSONオブジェクトのメタデータ部分には、マルチシグトランザクションでの内部トランザクションハッシュが含まれています。

最初のケースでは、クライアント側のソフトウェアの実装者は、2番目のケースでNEMネットワークがあなたのためにそれを行う間、署名者にハッシュを転送する責任があります。

標準のクライアントNCCは2番目の方法を使用します。それは便利な方法でマルチシグアカウントを扱うことができます。

現在のところ、マルチシグアカウント機能を使用する場合いは異なる場所に少なくとも3つの署名者を使用することをお勧めします。

署名者の秘密鍵のいずれかが侵害された場合、そのアカウントを署名者リストから直ちに削除し、その後、新しい署名者を追加する必要があります(これについては[署名者の追加と削除](#adding-and-removing-cosignatories)の章を参照してください)。

**秘密鍵がコンピュータに保存されている場合、そのコンピュータはインターネットをサーフィンしたり、他の危険なことをしたりするために使用するべきではありません。**

### 7.7.ネームスペースのプロビジョニング

公式情報：[Provisioning a namespace](http://bob.nem.ninja/docs/#provisioning-a-namespace)

この章では、ネームスペースをプロビジョニング(すなわちレンタル)するために必要なアクションについて説明します。

ネームスペースの詳細については、[ネームスペース](#namespaces)の章を参照してください。 ルートネームスペース『alice』とサブネームスペース『alice.vouchers』をリクエストしたいとします。 最初のアクションは、ネームスペーストランザクションのプロビジョニング([ProvisionNamespaceTransaction](#provisionNamespaceTransaction))を発行することです。いつものように、これはアナウンス準備のリクエスト(RequestPrepareAnnounce) JSONオブジェクトをNISに送信することによって行われます。

この場合、次のようになります。

```json
{
	"transaction": {
		"timeStamp": 9111526,
		"fee": 108000000,
		"type": 8193,
		"deadline": 9154726,
		"version": -1744830463,
		"signer": "d99e88c90da71a4b0d848454e59e296c9ef7a8f018f3eaa3a198dc460b6621a4",
		"rentalFeeSink": "3e82e1c1e4a75adaa3cba8c101c3cd31d9817a2eb966eb3b511fb2ed45b8e262",
		"rentalFee": 50000000000,
		"newPart": "alice",
		"parent": null
	},
	"privateKey": "00983bb01d05edecfaef55df9486c111abb6299c754a002069b1d0ef4537441bda"
}
```

フィールド『parent』は、ルートネームスペースをレンタルすることを示すnullに設定されています。また、誰もそのルートネームスペースを既に借りていないことを確認する必要があります。そうでなければNISはエラーを返します。

高いレンタル料はユーザーがすべての種類のルートネームスペースの占領のを防ぐためです。

また、手数料はハーベスタには与えられていません。何故ならばこれはハーベスタがブロックを収穫できるようになるまで待つことを奨励しており、そのブロックにネームスペーストランザクションのプロビジョニング(provision namespace transaction)を含めることによって、本質的に無料のネームスペースを取得するためです。

代わりに、すべてのレンタル料は特別なマルチアカウントで収集されます。

NISからの最も一般的なエラー応答は次のとおりです。

*   ネームスペースは既に別のアカウントによって所有されています。
*   ネームスペースに不正な文字または予約されたネームスペースのパーツが含まれています。
*   レンタルフィーシンクの公開鍵が無効です。
*   レンタル料金は無効です(少なすぎます)。

NISが成功メッセージで応答すると、トランザクションはネットワークにブロードキャストされ、将来のブロックに含まれます。トランザクションがブロックに含まれた後、/ account / namespacesリクエストを発行して、そのネームスペースの所有者であることを確認できます。xyzの章を参照してください。

サブネームスペース『alice.vouchers』をレンタルするには、次のようなアナウンス準備のリクエスト(RequestPrepareAnnounce) JSONオブジェクトをNISに送信する必要があります。

```json
{
	"transaction": {
		"timeStamp": 9111526,
		"fee": 108000000,
		"type": 8193,
		"deadline": 9154726,
		"version": -1744830463,
		"signer": "d99e88c90da71a4b0d848454e59e296c9ef7a8f018f3eaa3a198dc460b6621a4",
		"rentalFeeSink": "3e82e1c1e4a75adaa3cba8c101c3cd31d9817a2eb966eb3b511fb2ed45b8e262",
		"rentalFee": 5000000000,
		"newPart": "vouchers",
		"parent": "alice"
	},
	"privateKey": "00983bb01d05edecfaef55df9486c111abb6299c754a002069b1d0ef4537441bda"
}
```

今回は親が親のネームスペースに設定されています。この場合、ルートのネームスペース『alice』に設定されています。サブネームスペースのレンタル料金はルートネームスペースの料金の10％、つまり500XEMです(**注：現在のサブネームスペースレンタル料金は200XEMです**)。ルートネームスペースを所有するまで待つか、NISがエラーメッセージで応答します。トランザクションがブロックに含まれると、ルートネームスペース『alice』が期限切れでない限り、サブネームスペース『alice.vouchers』を所有します。

サブネームスペース『alice.vouchers.special』をレンタルする場合は、アナウンス準備のリクエスト(RequestPrepareAnnounce)オブジェクトを再度発行する必要があります。このとき、親は『alice.vouchers』に設定されます。newPartは『special』です。

1年後、ルートネームスペースの有効期限が切れます。これが起こらないようにするには、有効期限が切れる1か月以内にルートネームスペースのネームスペーストランザクションのプロビジョニング(provision namespace transaction)を送信する必要があります。アナウンス準備のリクエスト(RequestPrepareAnnounce)オブジェクトは初めてネームスペースをレンタルする場合と同じです。ルートネームスペースの更新はアカウントが既に所有しているルートネームスペースのサブネームスペースも自動的に更新します。

### 7.8.モザイクの作成

公式情報：[Creating mosaics](http://bob.nem.ninja/docs/#creating-mosaics)

#### 7.8.1.モザイク定義の作成

公式情報：[Creating a mosaic definition](http://bob.nem.ninja/docs/#creating-a-mosaic-definition)

NEMモザイクの概念の基礎は[モザイク](#mosaics)の章にあります。

モザイクタイプを定義して作成するには、モザイク定義作成トランザクション(MosaicDefinitionCreationTransaction)を発行する必要があります。これは、アナウンス準備のリクエスト(RequestPrepareAnnounce)JSONオブジェクトをNISに送信することによって行われます。

内容は次のようになります。

```json
{
	"transaction": {
		"timeStamp": 9111526,
		"fee": 108000000,
		"type": 16385,
		"deadline": 9154726,
		"version": -1744830463,
		"signer": "cbda3edb771d42801a5c6ce0725f9374efade19a8933d6ac22ccfa50c777d0f9",
		"creationFee": 50000000000,
		"creationFeeSink": "53e140b5947f104cabc2d6fe8baedbc30ef9a0609c717d9613de593ec2a266d3",
		"mosaicDefinition": {
			"creator": "cbda3edb771d42801a5c6ce0725f9374efade19a8933d6ac22ccfa50c777d0f9",
			"description": "precious vouchers",
			"id": {
				"namespaceId": "alice.vouchers",
				"name": "Alice's gift vouchers"
			},
			"properties": [
				{
					"name": "divisibility",
					"value": "0"
				},
				{
					"name": "initialSupply",
					"value": "1000"
				},
				{
					"name": "supplyMutable",
					"value": "true"
				},
				{
					"name": "transferable",
					"value": "false"
				}
			],
			"levy": {
				"type": 1,
				"recipient": "TD3RXTHBLK6J3UD2BH2PXSOFLPWZOTR34WCG4HXH",
				"mosaicId": {
					"namespaceId": "nem",
					"name": "xem"
				},
				"fee": 10
			}
		}
	},
	"privateKey": "00983bb01d05edecfaef55df9486c111abb6299c754a002069b1d0ef4537441bda"
}
```

上記のトランザクションではid『alice.vouchers * Alice’s gift vouchers』という名前のモザイクがネームスペース『alice.vouchers』内に作成されます。アカウントにはそのネームスペースを所有して、モザイクを作成できるようにする必要があります。

不法占拠を阻止するために、モザイク定義を作成するために高い作成費用があります。前の章で述べたように料金はブロックハーベスタには転送されず『creationFeeSink』フィールドに公開鍵が提供される特別なアカウントに転送されます。

モザイクは次のプロパティを持ちます。

*   割り切れません。つまり、モザイクが表すバウチャー(伝票)は部分的ではなく全体としてのみ転送することができます。
*   当初1000枚のバウチャー(そのタイプのモザイク)があります。
*   供給(そのタイプのモザイクの数)は後で変更することができます。
*   バウチャーは残高間で譲渡できません。モザイクの作成者のみがバウチャーを他のアカウントに移すことができ、アカウントがバウチャーを所有すると、それは作成者に戻すことしかできません。
*   

この定義はまた、それぞれの移転に伴う徴収を意味しています。 徴収セクションには、各転送に10XEMの追加料金があると記載されています。その手数料は残高TD3RXTHBLK6J3UD2BH2PXSOFLPWZOTR34WCG4HXHで受信者に送信されます。

この徴収部分はオプションです。その部分が省略されている場合、モザイクを転送することにより追加料金は発生しません。

トランザクションを受け入れるNISの理由は以下が一般的です。

*   トランザクション署名者はモザイク定義で指定されたネームスペースを所有していないか、ネームスペースの有効期限が切れています。
*   指定されたモザイクIDを持つモザイク定義は既に存在します(モザイク定義の変更については後述の説明を参照してください)。
*   クリエイションフィーシンクの公開鍵が無効であるか、または作成費用が低すぎます。
*   トランザクションの課金部分のモザイクIDはNISには不明です。

トランザクションがブロックに含まれ、ブロックが実行されると『initialSupply』フィールド(例では1000)に記述されているモザイクの量が作成者に入金されます。

#### 7.8.2.モザイク定義を変更する

公式情報：[Altering a mosaic definition](http://bob.nem.ninja/docs/#altering-a-mosaic-definition)

説明を変更したい場合や、誤ったプロパティや欠陥のある徴収データを提供したためにモザイク定義を変更する必要があるかもしれません。これは同じモザイクIDであるが記述/プロパティ/徴収が異なる前述の別のモザイク定義作成トランザクションを発行することによって単純に行われます。ただし、その際にはいくつかの制限があります。

*   説明は作成者が全ての供給を所有していなくても、いつでも変更することができます。
*   プロパティと徴収データは、作成者がそのタイプのすべての単一モザイクを所有している場合にのみ変更できます。 これはクリエイターが秘密に徴収金を導入したり、供給を増やしてモザイクを膨らませたりするのを防ぐために必要です。

モザイク定義を更新すると500XEM(ハードフォーク前は50000XEM)のコストがかかりますので、トランザクションを発行する前にデータを再確認する必要があります。

#### 7.8.3.モザイク供給の変更

公式情報：[Changing the mosaic supply](http://bob.nem.ninja/docs/#changing-the-mosaic-supply)

『supplyMutable』をtrueに設定してモザイク定義を作成した場合は、モザイクの供給を変更することができます。これを行うにはモザイク供給変更トランザクション([MosaicSupplyChangeTransaction](#mosaicSupplyChangeTransaction))を発行する必要があります。これはアナウンス準備のリクエスト(RequestPrepareAnnounce) JSONオブジェクトをNISに送信することによって行われます。

このオブジェクトは、次のようになります。

```json
{
	"transaction": {
		"timeStamp": 9111526,
		"fee": 108000000,
		"type": 16386,
		"deadline": 9154726,
		"version": -1744830463,
		"signer": "d99e88c90da71a4b0d848454e59e296c9ef7a8f018f3eaa3a198dc460b6621a4",
		"supplyType": 1,
		"delta": 100,
		"mosaicId": {
			"namespaceId": "alice.vouchers",
			"name": "Alice's gift vouchers"
		}
	},
	"privateKey": "00983bb01d05edecfaef55df9486c111abb6299c754a002069b1d0ef4537441bda"
}
```

上記の例では、id『alice.vouchers * Alice’s gift vouchers』を持つ既存のモザイクの供給が変更されています。

*   『supplyType1』は供給が増加したことを意味します(供給タイプ2は供給減少を意味します)。
*   『delta100』とは作成者のアカウントに別の100単位が入金されたことを意味します。

トランザクションを受け入れるNISの理由は以下のとおりです。

*   トランザクション署名者は、モザイクの作成者ではありません。
*   モザイクの定義は、供給が不変であると述べています。
*   供給を増やそうとするとき、総供給は9,000,000,000モザイクを超えてはなりません。
*   供給を減らそうとするとき、作成者は自分が削除したいモザイクの数量を所有していなければなりません。

トランザクションがブロックチェーンに含まれると、供給の変更が実現されます。

### 7.9.署名付きトランザクションの作成

公式情報：[Creating a signed transaction](http://bob.nem.ninja/docs/#creating-a-signed-transaction)

この章ではトランザクションのどのデータを署名する必要があるのか、どのJSONオブジェクトをNISに送信するのかについて説明します。

#### 7.9.1.署名用データの収集

公式情報：[Gathering data for the signature](http://bob.nem.ninja/docs/#gathering-data-for-the-signature)

トランザクション署名を作成するには、トランザクションから抽出されたbyte配列に署名する必要があります。複数タイプのトランザクションが存在するため、byte配列は異なるタイプのトランザクションに対して異なる構造を持ちます。ですが、byte配列の最初の部分はすべてのトランザクションで同じ構造を持ちます。

*   フィールドが数字を表すとき、エンディアン(endianess)は重要です。
*   フィールドが連結される順序は重要です。

*   

**byte配列の共通トランザクション部分**

トランザクションタイプ：4bytes(整数)。以下のタイプがサポートされています。

    *   0x0101(転送トランザクション)
    *   0x0801(重要度転送トランザクション)
    *   0x1001(マルチシグ集計変更転送トランザクション)
    *   0x1002(マルチシグ署名トランザクション)
    *   0x1004(マルチシグトランザクション)
    *   0x2001(プロキシネームスペーストランザクション)
    *   0x4001(モザイク定義作成トランザクション)
    *   0x4002(モザイク供給変更トランザクション)
    *   

例(重要度転送トランザクション)：0x01、0x08、0x00、0x00

バージョン：4bytes(整数)。以下のタイプがサポートされています。

    *   

重要度転送トランザクション、マルチシグトランザクション、マルチシグ署名トランザクション、ネームスペーストランザクションのプロビジョニング、モザイク定義作成トランザクション、モザイク供給変更トランザクションは以下のとおりです。

    *   0x68 < 24="" +="">
    *   0x98 < 24="" +="">
    *   

例(メインネットワーク)：0x01、0x00、0x00、0x68

転送トランザクションとマルチシグ集計変更トランザクションではバージョンは以下のとおりです。

    *   0x68 < 24="" +="">
    *   0x98 < 24="" +="">
    *   

例(メインネットワーク)：0x02、0x00、0x00、0x68

タイムスタンプ：4bytes(整数)。

    *   例：(タイムスタンプ= 0x129623)：0x23,0x96,0x12,0x00

公開鍵byte配列の長さ(常に32)：4バイト(整数)。

    *   常に: 0x20, 0x00, 0x00, 0x00

署名者の公開鍵バイト：32バイト

    *   例：: 0x6d, 0xa3, 0x76, 0x07, 0x13, 0x01, 0x9e, 0x26, 0xb1, 0x86, 0x24, 0x3a, 0xb6, 0xec, 0xba, 0x9f, 0x70, 0x78, 0x4c, 0x59, 0x92, 0x3d, 0x68, 0x9a, 0xb5, 0x4d, 0x4b, 0x2b, 0xf0, 0xe2, 0x0f, 0x5d 

手数料(マイクロNEM)：8バイト(ロング)。

    *   例：(12 nem)：0x00, 0x1b, 0xb7, 0x00, 0x00, 0x00, 0x00, 0x00 

期限：4バイト(整数)。

    *   例：(deadline = 0x147824)：0x24, 0x78, 0x14, 0x00

*   

**転送トランザクション部分**

受信者アドレスの長さ(常に40)：4バイト(整数)。

    *   常に：0x28, 0x00, 0x00, 0x00

受信者アドレス：40バイト(UTF8エンコーディングを使用)。

    *   例：(『NACCH2WPJYVQ3PLGMVZVRK5JI6POTJXXHLUG3P4J』)： 0x4e, 0x41, 0x43, 0x43, 0x48, 0x32, 0x57, 0x50, 0x4a, 0x59, 0x56, 0x51, 0x33, 0x50, 0x4c, 0x47, 0x4d, 0x56, 0x5a, 0x56, 0x52, 0x4b, 0x35, 0x4a, 0x49, 0x36, 0x50, 0x4f, 0x54, 0x4a, 0x58, 0x58, 0x48, 0x4c, 0x55, 0x47, 0x33, 0x50, 0x34, 0x4a 

数量(マイクロNEM)：8バイト(ロング)。

    *   例：(1234 NEM)： 0x80, 0x58, 0x8d, 0x49, 0x00, 0x00, 0x00, 0x00

メッセージフィールドの長さ：4バイト(整数)。注：長さが0の場合、次の2つのフィールドは適用されません。

    *   例：: 0x24, 0x00, 0x00, 0x00 

メッセージタイプ：4バイト(整数)。次のメッセージタイプがサポートされています。

    *   0x01(プレーンメッセージ)
    *   0x02(暗号化されたメッセージ)
    *   例：0x01、0x00、0x00、0x00

ペイロードの長さ：4バイト(整数)。

    *   例：0x05、0x00、0x00、0x00

ペイロード：UTF8でエンコードされた文字列。

    *   例：(『Hello』)：0x48、0x65、0x6c、0x6c、0x6f

注：次の部分はオプションであり、アタッチメントを持つ転送トランザクションバージョン2でのみ使用できます。

モザイクの数：4バイト(整数)。

    *   例：(1モザイク)：0x01、0x00、0x00、0x00

次の部分はアタッチメント内のすべてのモザイクに対して繰り返されます。

モザイク構造の長さ：4バイト(整数)。

    *   例：0x1c、0x00、0x00、0x00

モザイクID構造の長さ：4バイト(整数)。

    *   例：0x10, 0x00, 0x00, 0x00

ネームスペースの文字列の長さ：4バイト(整数)。

    *   例：0x03, 0x00, 0x00, 0x00

ネームスペースのID文字列：UTF8でエンコードされた文字列。

    *   例：(『id9』)0x69, 0x64, 0x39

モザイク名の文字列の長さ：4バイト(整数)。

    *   例：0x05, 0x00, 0x00, 0x00

モザイク名の文字列：UTF8でエンコードされた文字列。

    *   例：(『name9』)0x6e, 0x61, 0x6d, 0x65, 0x39

数量：8バイト(ロング)。

    *   例：(24)0x18, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00

*   

**重要度転送トランザクション部分**

重要度転送モード：4バイト(整数)。次のモードがサポートされています。

    *   0x01(アクティブ)
    *   0x02(非アクティブ
    *   

例(アクティブモード)：0x01、0x00、0x00、0x00

リモートアカウントの公開鍵byte配列の長さ(常に32)：4バイト(整数)。

    *   常に：0x20, 0x00, 0x00, 0x00

リモートアカウントの公開鍵バイト：32バイト

    *   例：0x6d, 0xa3, 0x76, 0x07, 0x13, 0x01, 0x9e, 0x26, 0xb1, 0x86, 0x24, 0x3a, 0xb6, 0xec, 0xba, 0x9f, 0x70, 0x78, 0x4c, 0x59, 0x92, 0x3d, 0x68, 0x9a, 0xb5, 0x4d, 0x4b, 0x2b, 0xf0, 0xe2, 0x0f, 0x5d

*   

**集計変更トランザクション部分**

変更署名者数：4バイト(整数)。

    *   例：0x03, 0x00, 0x00, 0x00

次の部分はすべての署名者変更のために繰り返されます。

署名者変更の構造の長さ：4バイト(整数)。

    *   常に：0x28, 0x00, 0x00, 0x00

変更タイプ：4バイト(整数)。以下の変更タイプがサポートされています。

    *   0x01(署名者追加)
    *   0x02(署名者削除)
    *   例：(削除)：0x02, 0x00, 0x00, 0x00

署名者の公開鍵byte配列の長さ(常に32)：4バイト(整数)。

    *   常に：0x20, 0x00, 0x00, 0x00

署名者の公開鍵バイト：32バイト。

    *   例：0x6d, 0xa3, 0x76, 0x07, 0x13, 0x01, 0x9e, 0x26, 0xb1, 0x86, 0x24, 0x3a, 0xb6, 0xec, 0xba, 0x9f, 0x70, 0x78, 0x4c, 0x59, 0x92, 0x3d, 0x68, 0x9a, 0xb5, 0x4d, 0x4b, 0x2b, 0xf0, 0xe2, 0x0f, 0x5d

次の部分では、最小署名者の変更について説明します。この部分はオプションです。集計変更トランザクションバージョン1では、この部分を省略する必要があります。最小署名者変更がない集計変更トランザクションバージョン2では、値：0x00、0x00、0x00、0x00のフィールド長のみを書き込む必要があります。

最小署名者変更の構造の長さ：4バイト(整数)。

    *   常に：0x04,0x00,0x00,0x00

相対的な変更：4バイト(整数)。

    *   例：(2の相対的な変化)：0x02,0x00,0x00,0x00

*   

**マルチシグ署名トランザクション部分**

ハッシュオブジェクトの長さ(対応するマルチシグトランザクションのハッシュ)：4バイト(整数)。

    *   常に：0x24,0x00,0x00,0x00

ハッシュの長さ：4バイト(整数)。

    *   常に：0x20,0x00,0x00,0x00

SHA3ハッシュバイト：32バイト。

    *   例：0x7d, 0x76, 0xfe, 0x26, 0xc4, 0x54, 0x61, 0xf7, 0x4b, 0xcb, 0x76, 0xac, 0xae, 0xb0, 0x17, 0x39, 0x9e, 0xbe, 0x50, 0xaa, 0x71, 0x46, 0xe2, 0x62, 0x57, 0x39, 0x5f,0xbb,0xc0,0x25,0xac,0xb7 

対応するマルチシグアカウントのアドレスの長さ(常に40)：4バイト(整数)。

    *   常に：0x28, 0x00, 0x00, 0x00 

マルチシグアカウントアドレス：40バイト(UTF8エンコーディングを使用)。

    *   例：(『NACCH2WPJYVQ3PLGMVZVRK5JI6POTJXXHLUG3P4J』)：0x4e, 0x41, 0x43, 0x43, 0x48, 0x32, 0x57, 0x50, 0x4a, 0x59, 0x56, 0x51, 0x33, 0x50, 0x4c, 0x47, 0x4d, 0x56, 0x5a, 0x56, 0x52, 0x4b, 0x35, 0x4a, 0x49, 0x36, 0x50, 0x4f, 0x54, 0x4a, 0x58, 0x58, 0x48, 0x4c, 0x55, 0x47, 0x33, 0x50, 0x34, 0x4a

*   

**マルチシグトランザクション部分**

内部トランザクションオブジェクトの長さ。これは転送、重要度転送、または集計変更トランザクションです。

    *   例：0x74、0x00、0x00、0x00

以下は内部トランザクションオブジェクトです。構造は上記のトランザクション(署名トランザクションを除く)の構造の1つです。

*   

**ネームスペーストランザクションのプロビジョニング部分**

レンタルフィーシンクの公開鍵byte配列の長さ(常に32)：4バイト(整数)

    *   常に：0x20, 0x00, 0x00, 0x00

レンタルフィーシンクの公開鍵バイト：32バイト

    *   常に：0x3e, 0x82, 0xe1, 0xc1, 0xe4, 0xa7, 0x5a, 0xda, 0xa3, 0xcb, 0xa8, 0xc1, 0x01, 0xc3, 0xcd, 0x31, 0xd9, 0x81, 0x7a, 0x2e, 0xb9, 0x66, 0xeb, 0x3b, 0x51, 0x1f, 0xb2, 0xed, 0x45, 0xb8, 0xe2, 0x62

レンタルフィー(常に50000000000)：8バイト(ロング)。

    *   常に：0x00, 0x74, 0x3b, 0xa4, 0x0b, 0x00, 0x00, 0x00

新しい部分文字列の長さ：4バイト(整数)。

    *   例：0x03, 0x00, 0x00, 0x00

新しい部分文字列：UTF8でエンコードされた文字列。

    *   例：(『bar』)0x62, 0x61, 0x72

親stringの長さ：4バイト(整数)。注：親がnull(ルートネームスペースの準備)の必要がある場合、このフィールドは0xff、0xff、0xff、0xffに設定され、次のフィールドは省略されます。

    *   例： 0x03, 0x00, 0x00, 0x00

親ストリング：UTF8でエンコードされた文字列。

    *   例：(『foo)0x66、0x6f、0x6f

*   

**モザイク定義作成トランザクション部分**

モザイク定義構造の長さ：4バイト(整数)。

    *   例：0x29, 0x01, 0x00, 0x00

作成者の公開鍵バイト配列の長さ(常に32)：4バイト(整数)。

    *   例：0x20, 0x00, 0x00, 0x00

作成者の公開鍵バイト：32バイト。

    *   例：0x8f, 0xcd, 0xce, 0xd0, 0x85, 0xcb, 0x58, 0xe3, 0x62, 0x6e, 0x7e, 0xfb, 0xab, 0xc7, 0xa6, 0x3d, 0x87, 0x3e, 0x7d, 0xf5, 0xb6, 0x24, 0x6c, 0x65, 0x9b, 0x2c, 0x10, 0x8f, 0x90, 0xab, 0x44, 0xf2

モザイクID構造の長さ：4バイト(整数)。

    *   例：0x2b, 0x00, 0x00, 0x00

ネームスペースの文字列の長さ：4バイト(整数)。

    *   例：0x0e, 0x00, 0x00, 0x00

ネームスペースID文字列：UTF8でエンコードされた文字列。

    *   例：(『alice.vouchers』)0x61, 0x6c, 0x69, 0x63, 0x65, 0x2e, 0x76, 0x6f, 0x75, 0x63, 0x68, 0x65, 0x72, 0x7

モザイク名文字列の長さ：4バイト(整数)。

    *   例：0x15, 0x00, 0x00, 0x00

モザイク名文字列：UTF8でエンコードされた文字列。

    *   例：(『Alice’s gift vouchers』)0x41, 0x6c, 0x69, 0x63, 0x65, 0x27, 0x73, 0x20, 0x67, 0x69, 0x66, 0x74, 0x20, 0x76, 0x6f, 0x75, 0x63, 0x68, 0x65, 0x72, 0x73

説明文字列の長さ：4バイト(整数)。

    *   例：0x11, 0x00, 0x00, 0x00

説明文字列：UTF8でエンコードされた文字列。

    *   例：(『precious vouchers』)0x70, 0x72, 0x65, 0x63, 0x69, 0x6f, 0x75, 0x73, 0x20, 0x76, 0x6f, 0x75, 0x63, 0x68, 0x65, 0x72, 0x73

プロパティの数：4バイト(整数)。

    *   例：0x02, 0x00, 0x00, 0x00

次の5つのフィールドがすべてのプロパティに対して繰り返されます。注：プロパティ値は常にstringsです。

プロパティ構造の長さ：4バイト(整数)

    *   例：0x15, 0x00, 0x00, 0x00

プロパティ名の長さ：4バイト(整数)。

    *   例：0x0c, 0x00, 0x00, 0x00

プロパティ名：UTF8でエンコードされた文字列。

    *   例：(『divisibility』)0x64, 0x69, 0x76, 0x69, 0x73, 0x69, 0x62, 0x69, 0x6c, 0x69, 0x74, 0x79

プロパティ値の長さ：4バイト(整数)。

    *   例：0x01, 0x00, 0x00, 0x00

プロパティ値：UTF8でエンコードされた文字列。

    *   例：(『3』)0x33

プロパティ構造の長さ：4バイト(整数)。

    *   例：0x16, 0x00, 0x00, 0x00

プロパティ名の長さ：4バイト(整数)。

    *   例：0x0d, 0x00, 0x00, 0x00

プロパティ名：UTF8でエンコードされた文字列。

    *   例：(『initialSupply』)0x69, 0x6e, 0x69, 0x74, 0x69, 0x61, 0x6c, 0x53, 0x75, 0x70, 0x70, 0x6c, 0x79

プロパティ値の長さ：4バイト(整数)。

    *   例：0x01, 0x00, 0x00, 0x00

プロパティ値：UTF8でエンコードされた文字列。

    *   例：(『0』)0x30

プロパティー構造の長さ：4バイト(整数)。

    *   例：0x1a, 0x00, 0x00, 0x00

プロパティ名の長さ：4バイト(整数)。

    *   例：0x0d, 0x00, 0x00, 0x00

プロパティ名：UTF8でエンコードされた文字列。

    *   例：(『supplyMutable』)0x73, 0x75, 0x70, 0x70, 0x6c, 0x79, 0x4d, 0x75, 0x74, 0x61, 0x62, 0x6c, 0x65

プロパティ値の長さ：4バイト(整数)。

    *   例：0x05, 0x00, 0x00, 0x00

プロパティ値：UTF8でエンコードされた文字列。

    *   例：(『false』)0x66, 0x61, 0x6c, 0x73, 0x65

プロパティ構造の長さ：4バイト(整数)。

    *   例：0x18, 0x00, 0x00, 0x00

プロパティ名の長さ：4バイト(整数)。

    *   例：0x0c, 0x00, 0x00, 0x00

プロパティ名：UTF8でエンコードされた文字列。

    *   例：(『transferable』)0x74, 0x72, 0x61, 0x6e, 0x73, 0x66, 0x65, 0x72, 0x61, 0x62, 0x6c, 0x65

プロパティ値の長さ：4バイト(整数)。

    *   例：0x04, 0x00, 0x00, 0x00

プロパティ値：UTF8でエンコードされた文字列。

    *   例：(『true』)0x74, 0x72, 0x75, 0x65

注：以下の徴収オブジェクトはオプションです。モザイク定義に徴収がない場合はフィールド長を0に設定し、「徴収構造はここで終わります。(The levy structure ends here.)」というコメントまですべての後続フィールドを省略します。

徴収構造の長さ：4バイト(整数)。

    *   例：0x4c, 0x00, 0x00, 0x00

料金タイプ：4バイト(整数)。以下の料金タイプがサポートされています。

    *   0x01(絶対手数料)
    *   0x02(パーセンタイル手数料)
    *   例：0x01、0x00、0x00、0x00

受信者アドレスフィールドの長さ(常に40)：4バイト(整数)。

    *   例：0x28, 0x00, 0x00, 0x00

受信者アドレス：40バイト(UTF8エンコーディングを使用)。

    *   例：(『NACCH2WPJYVQ3PLGMVZVRK5JI6POTJXXHLUG3P4J』)：0x4e, 0x41, 0x43, 0x43, 0x48, 0x32, 0x57, 0x50, 0x4a, 0x59, 0x56, 0x51, 0x33, 0x50, 0x4c, 0x47, 0x4d, 0x56, 0x5a, 0x56, 0x52, 0x4b, 0x35, 0x4a, 0x49, 0x36, 0x50, 0x4f, 0x54, 0x4a, 0x58, 0x58, 0x48, 0x4c, 0x55, 0x47, 0x33, 0x50, 0x34, 0x4a

モザイクID構造の長さ：4バイト(整数)。

    *   例：0x10, 0x00, 0x00, 0x00

ネームスペースの文字列の長さ：4バイト(整数)
。

    *   例：0x03, 0x00, 0x00, 0x00

ネームスペースID文字列：UTF8でエンコードされた文字列。

    *   例：(『id2』)0x69, 0x64, 0x32

モザイク名の文字列の長さ：4バイト(整数)。

    *   例：0x05, 0x00, 0x00, 0x00

モザイク名の文字列：UTF8でエンコードされた文字列。

    *   例：(『name2』)0x6e, 0x61, 0x6d, 0x65, 0x32

手数料の数量：8バイト(ロング)。

    *   例：(123)0x7b, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00

徴収構造はここで終わりです。

レンタルフィーシンク作成の公開鍵byte配列(常に32)：4バイト(整数)。

    *   常に：0x20, 0x00, 0x00, 0x00 

クリエーションフィーシンクの公開鍵バイト：32バイト。

    *   常に：0x53, 0xe1, 0x40, 0xb5, 0x94, 0x7f, 0x10, 0x4c, 0xab, 0xc2, 0xd6, 0xfe, 0x8b, 0xae, 0xdb, 0xc3, 0x0e, 0xf9, 0xa0, 0x60, 0x9c, 0x71, 0x7d, 0x96, 0x13, 0xde, 0x59, 0x3e, 0xc2, 0xa2, 0x66, 0xd3

手数料の数量：8バイト(ロング)。

    *   常に：(50000000000)0x00, 0x74, 0x3b, 0xa4, 0x0b, 0x00, 0x00, 0x00

*   

**モザイク供給変更トランザクション部分**

モザイクID構造の長さ：4バイト(整数)。

    *   常に：0x12, 0x00, 0x00, 0x00

ネームスペースの文字列の長さ：4バイト(整数)。

    *   常に：0x07, 0x00, 0x00, 0x00

ネームスペースID文字列：UTF8でエンコードされた文字列。

    *   例：(『foo.bar』)0x66, 0x6f, 0x6f, 0x2e, 0x62, 0x61, 0x72

モザイク名文字列の長さ：4バイト(整数)。

    *   例：0x03, 0x00, 0x00, 0x00

モザイク名文字列：UTF8でエンコードされた文字列。

    *   例：(『baz』) 0x62, 0x61, 0x7a 

供給タイプ：4バイト(整数)。以下の電源タイプがサポートされています。

    *   0x01(供給を増やす)
    *   0x02(供給を減らす)
    *   例：0x01、0x00、0x00、0x00

デルタ(供給の変更)：8バイト(ロング)。

    *   0x01(供給を増やす)
    *   0x02(供給を減らす)
    *   例：(100)0x64, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00

*   

**byte配列の作成**

署名が必要な最終byte配列を作成するには、トランザクションの共通部分と型固有の部分を連結するだけです。たとえば、転送トランザクションのbyte配列を作成する場合は、次のような共通のものがあります。
`0x01, 0x01, 0x00, 0x00, 0x01, 0x00, 0x00, 0x00, 0x6f, 0x00, 0x00, 0x00, 0x20, 0x00, 0x00, 0x00, 0x68, 0x32, 0x03, 0xb4, 0x55, 0x09, 0x0e, 0x2f, 0xfe, 0xd6, 0x48, 0x53, 0x6c, 0x99, 0x01, 0x4d, 0x1c, 0xa9, 0x2c, 0x10, 0x47, 0xaf, 0xbc, 0xae, 0x58, 0x05, 0x7b, 0xb6, 0xa6, 0x98, 0xc8, 0x0b, 0x80, 0x84, 0x1e, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00`

転送トランザクション特定部分
`0x28, 0x00, 0x00, 0x00, 0x54, 0x41, 0x49, 0x34, 0x35, 0x32, 0x53, 0x37, 0x44, 0x4c, 0x36, 0x57, 0x48, 0x57, 0x54, 0x5a, 0x5a, 0x32, 0x57, 0x33, 0x44, 0x49, 0x4d, 0x34, 0x32, 0x36, 0x58, 0x57, 0x49, 0x4a, 0x4b, 0x4c, 0x55, 0x4e, 0x58, 0x4e, 0x4b, 0x54, 0x37, 0x4c, 0x40, 0x2f, 0x07, 0x2f, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00`

最終的な配列を与えます。
`0x01, 0x01, 0x00, 0x00, 0x01, 0x00, 0x00, 0x00, 0x6f, 0x00, 0x00, 0x00, 0x20, 0x00, 0x00, 0x00, 0x68, 0x32, 0x03, 0xb4, 0x55, 0x09, 0x0e, 0x2f, 0xfe, 0xd6, 0x48, 0x53, 0x6c, 0x99, 0x01, 0x4d, 0x1c, 0xa9, 0x2c, 0x10, 0x47, 0xaf, 0xbc, 0xae, 0x58, 0x05, 0x7b, 0xb6, 0xa6, 0x98, 0xc8, 0x0b, 0x80, 0x84, 0x1e, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00 0x28, 0x00, 0x00, 0x00, 0x54, 0x41, 0x49, 0x34, 0x35, 0x32, 0x53, 0x37, 0x44, 0x4c, 0x36, 0x57, 0x48, 0x57, 0x54, 0x5a, 0x5a, 0x32, 0x57, 0x33, 0x44, 0x49, 0x4d, 0x34, 0x32, 0x36, 0x58, 0x57, 0x49, 0x4a, 0x4b, 0x4c, 0x55, 0x4e, 0x58, 0x4e, 0x4b, 0x54, 0x37, 0x4c, 0x40, 0x2f, 0x07, 0x2f, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00`

以上の配列に署名すると、64バイトの署名が得られます。

*   

**トランザクションのハッシュ計算**

NISはSHA3-256ハッシュ関数を使用します。トランザクションのハッシュを作成するには、トランザクションのbyte配列をハッシュする必要があります。トランザクションからbyte配列を構築する方法については、上記セクションを参照してください。

#### 7.9.2.NISにデータを送信する

公式情報：[Sending the data to NIS](http://bob.nem.ninja/docs/#sending-the-data-to-NIS)

最後のセクションで説明したように、データを準備したあと、配列と対応する署名をRequestAnnounceリクエストで送信できます。

*   APIパス：/transaction/announce
*   リクエストタイプ：POST
*   概要：トランザクションを作成してブロードキャストします。秘密鍵は関与していません。
*   パラメータ：requestAnnounce：リクエストアナウンス([RequestAnnounce](#requestAnnounce))で説明されている、RequestAnnounce JSONオブジェクト。
*   例：リクエストはブラウザでは実行できません。
*   返されるJSON [NemAnnounceResult](#nemAnnounceResult)オブジェクトの例

```json
{
	"type": 1,
	"code": 1,
	"message": "SUCCESS",
	"transactionHash": {
		"data": "c1786437336da077cd572a27710c40c378610e8d33880bcb7bdb0a42e3d35586"
	},
	"innerTransactionHash": {
		"data": "cc317a7674d56352b4c711096a7594bd11908bf518293a191fc2faa12eac0fbb"
	}
}
```

可能性のあるエラー：可能性のあるエラーについては、6.1章で説明しています。

### 7.10.トランザクション手数料

公式情報：[Transaction fees](http://bob.nem.ninja/docs/#transaction-fees)

ハーベスタがブロックを収穫しているノードを実行する動機を持つためには、ブロックチェーンに含めるすべてのトランザクションに対して手数料を支払う必要があります。

異なるトランザクションタイプには異なる手数料があります。NISでトランザクションを有効にするには、最低手数料が必要です。

注：トランザクションの種類によっては、トランザクション実行中のアクション(たとえば、ネームスペースのレンタル)により追加料金がかかる可能性があります。

以下のチャートは各トランザクションタイプの最低手数料をまとめたものです。すべての計算はまとまった量のXEMで行われます(つまり、マイクロXEMは無視されます)。

*   転送トランザクション：手数料はXEMの金額を転送するための料金とトランザクションにメッセージを追加する料金の合計です。
*   *   1)XEMを別のアカウントに転送するための料金。
    *   a)移転金額が8XEM未満の場合、手数料は10XEMです。
    *   例：6XEMの転送には4XEMの料金がかかります。
    *   b)譲渡された金額が8 XEM以上の場合、手数料は max(2,99 * arctan(量/ 150000))XEM。
    *   例：100000XEMの転送コストは58XEM。
    *   2)トランザクションにメッセージを追加するための手数料：100000XEMの転送コストは58XEM。
    *   2)モザイクを別の残高に転送するための手数料：転送されるモザイクごとに、料金は以下のように計算されます。
    *   a)初期供給量s、分割可能性d、量qのモザイクが与えられた場合、XEMの等価物は(次の小さい整数に丸められる)xemEquivalent = (8,999,999,999 * q) / (s * 10^d) 
    *   その後、1)をxemEquivalentに適用し、最終ステップで25％を加算することによって料金が計算されます。
    *   fee = (apply 1) to xemEquivalent) * 1.25
    *   例：トランザクションに3,000,000マイクロxemの量があり、アタッチメント内のモザイクの初期供給が1,000,000であり、可分性が3であり、量が5,000であるとします。これは、15,000の数量が移転されることを意味します。 上記の式を適用すると、xemEquivalent =（8,999,999,999 * 15,000）/（1,000,000 * 1000）= 134999になり、結果は次の小さい整数にまとめられます。xemEquivalentに1)を適用すると、(まとめた後に)72が返されます。
    *   そのため、料金は72 * 1.25 XEM = 90 XEMです。
    *   3)トランザクションにメッセージを追加するための手数料：メッセージがない場合、または空のメッセージが追加された場合は0 XEMです。それ以外の場合、料金は2 * max(1、メッセージ長/ 16)です。
    *   例：暗号化されていないメッセージ『The New Economy Movement will change the world!!!』は49文字で、2 * 49/16 = 6XEMです。重要度転送トランザクション
*   *   6XEM集計変更トランザクション
*   *   10 + 6 *変更数+6(最小署名者変更が含まれている場合)
    *   例：最小署名者変更をせずにアカウントに3人の署名者を追加するには10 + 6×3 = 28XEM。
    *   アカウントに3つの署名者を追加し、最小署名者変更するとコストがかかります。10 + 6 * 3 + 6 = 34XEM。マルチシグトランザクション
*   *   6XEMマルチシグ署名トランザクション
*   *   6XEMネームスペーストランザクションのプロビジョニング
*   *   108XEMモザイク定義作成トランザクション
*   *   108XEMモザイク供給変更トランザクション
*   *   108XEM

## 8.NISからの追加情報要求

公式情報：[Requests for additional information from NIS](http://bob.nem.ninja/docs/#requests-for-additional-information-from-NIS)

いくつかのリクエストは、NISの内部ステータスに関する追加情報を提供します。

**警告：これらのリクエストは将来のバージョンのNISで今後予告なしに削除される可能性があります。その存在に頼るべきではありません。**

### 8.1.ネットワーク時間の監視

公式情報：[Monitoring the network time](http://bob.nem.ninja/docs/#monitoring-the-network-time)

*   APIパス：/debug/time-synchronization
*   リクエストタイプ：GET
*   概要：時刻同期結果([TimeSynchronizationResult](#timeSynchronizationResult))で説明されているTimeSynchronizationResultの配列を取得します。この情報を使用して、ネットワーク時間の変化を監視できます。
*   パラメータ：無し。
*   例：http://127.0.0.1:7890/debug/time-synchronization
*   返されるJSON [TimeSynchronizationResult](#timeSynchronizationResult)オブジェクトの例

```json
{
	"data": [
		{
			"dateTime": "2014-11-19 19:23:04",
			"currentTimeOffset": 1747,
			"change": 57
		},
		{
			"dateTime": "2014-11-19 19:24:17",
			"currentTimeOffset": 1776,
			"change": 29
		},
		{
			"dateTime": "2014-11-19 19:25:18",
			"currentTimeOffset": 1729,
			"change": -47
		}
	]
}
```

可能性のあるエラー：無し。

### 8.2.受信および送信コールの監視

公式情報：[Monitoring incoming and outgoing calls](http://bob.nem.ninja/docs/#monitoring-incoming-and-outgoing-calls)

*   APIパス：/debug/connections/incoming
*   リクエストタイプ：GET
*   概要：監査収集([AuditCollection](#auditCollection))の説明に従って、AuditCollectionの受信コールを取得します。この情報を使用して、未処理および最新の着信要求を監視できます。
*   パラメータ：無し。
*   例：http://127.0.0.1:7890/debug/connections/incoming
*   返されるJSON [AuditCollection](#auditCollection)オブジェクトの例

```json
{
	"outstanding": [
		{
			"path": "/debug/connections/incoming",
			"start-time": 9317306,
			"host": "127.0.0.1",
			"elapsed-time": 0,
			"id": 4070
		}
	],
	"most-recent": [
		{
			"path": "/debug/connections/incoming",
			"start-time": 9317306,
			"host": "127.0.0.1",
			"elapsed-time": 0,
			"id": 4070
		},
		{
			"path": "/chain/score",
			"start-time": 9317303,
			"host": "95.16.203.168",
			"elapsed-time": 3,
			"id": 4069
		}
	]
}
```


可能性のあるエラー：無し。
*   APIパス：/debug/connections/outgoing
*   リクエストタイプ：GET
*   概要：監査収集([AuditCollection](#auditCollection))の説明に従って、AuditCollectionの送信コールを取得します。この情報を使用して、未処理および最新の着信要求を監視できます。
*   パラメータ：無し。
*   例：http://127.0.0.1:7890/debug/connections/outgoing
*   返されるJSON [AuditCollection](#auditCollection)オブジェクトの例

```json
{
	"outstanding": [
		{
			"path": "/chain/blocks-after",
			"start-time": 9317511,
			"host": "88.12.55.125",
			"elapsed-time": 6,
			"id": 6452
		}
	],
	"most-recent": [
		{
			"path": "/chain/blocks-after",
			"start-time": 9317511,
			"host": "88.12.55.125",
			"elapsed-time": 6,
			"id": 6452
		},
		{
			"path": "/chain/hashes-from",
			"start-time": 9317511,
			"host": "88.12.55.125",
			"elapsed-time": 6,
			"id": 6451
		}
	]
}
```

可能性のあるエラー：無し。

### 8.3.時間監視

公式情報：[Monitoring timers](http://bob.nem.ninja/docs/#monitoring-timers)

*   APIパス：/debug/connections/timers
*   リクエストタイプ：GET
*   概要：Nem非同期タイマービジター([NemNemAsyncTimerVisitor](#nemAsyncTimerVisitor))で説明されているタスクモニター構造の配列を取得します。この情報を使用して、定期的なタスクの統計を監視できます。
*   パラメータ：無し。
*   例：http://127.0.0.1:7890/debug/timers
*   返されるJSON [NemAsyncTimerVisitor](#nemAsyncTimerVisitor)オブジェクトの例

```json
{
	"data": [
		{
			"last-delay-time": 3000,
			"executions": 1024,
			"failures": 0,
			"successes": 1024,
			"last-operation-start-time": 9317695,
			"is-executing": 0,
			"name": "FORAGING",
			"average-operation-time": 0,
			"last-operation-time": 0
		},
		{
			"last-delay-time": 74181,
			"executions": 71,
			"failures": 0,
			"successes": 71,
			"last-operation-start-time": 9317654,
			"is-executing": 0,
			"name": "REFRESH",
			"average-operation-time": 6,
			"last-operation-time": 7
		}
	]
}
```

可能性のあるエラー：無し。

## 9.JSON構造の概要

公式情報：[Appendix A: Description of the JSON Structures](http://bob.nem.ninja/docs/#appendix-A:-description-of-the-JSON-structures)

### 9.1.アカウント履歴データビューモデル

公式情報：[AccountHistoricalDataViewModel](http://bob.nem.ninja/docs/#accountHistoricalDataViewModel)

概要：ノードはアカウントの履歴データを取得するための機能をサポートできます。ノードがこの機能をサポートしている場合、AccountHistoricalDataViewModelオブジェクトの配列が返されます。

JSON構造の例

```json
{
	"height": 8976,
	"address": "NALICELGU3IVY4DPJKHYLSSVYFFWYS5QPLYEZDJJ",
	"balance": 80670000000,
	"vestedBalance": 13949175142,
	"unvestedBalance": 66720824858,
	"importance": 0.00008166760846617221,
	"pageRank": 0.0006944567083595363
}
```

フィールドの説明

*   height：データが有効な高さ。
*   address：アカウントのアドレス。
*   balance：アカウントの残高。
*   vestedBalance：残高の確定部分。
*   unvestedBalance：残高の未払部分。
*   importance：アカウントの重要度。
*   pageRank：重要度のページランク部分。

### 9.2.アカウント重要度ビューモデル

公式情報：[AccountImportanceViewModel](http://bob.nem.ninja/docs/#accountImportanceViewModel)

概要：各アカウントにはNEMネットワークの重要度が割り当てられます。新しいブロックを生成するアカウントの能力はその重要性に比例します。重要度は0と1の間の数値です。

JSON構造の例

```json
{
	"address": "TALICELCD3XPH4FFI5STGGNSNSWPOTG5E4DS2TOS",
	"importance": {
		"isSet": 1,
		"score": 0.0011561555164258449,
		"ev": 0.004367936531009263,
		"height": 38413
	}
}
```

フィールドの説明

*   address：アカウントのアドレス。
*   importance：アカウントの重要性を示す基礎。
*   isSet：フィールド 『score』『ev』および『height』でのavailable.isSetの値が0または1であるかどうかを示します。isSetが0の場合、フィールドは使用できません。
*   score：アカウントの重要性。重要度の範囲は0?1です。
*   ev：重要度のページランク部分。 ページランクは0と1の間の範囲です。
*   height：重要度計算が行われた高さ。

### 9.3.アカウント情報

公式情報：[AccountInfo](http://bob.nem.ninja/docs/#accountInfo)

概要：各アカウントにはNEMネットワークの重要度が割り当てられます。新しいブロックを生成するアカウントの能力はその重要性に比例します。重要度は0と1の間の数値です。

JSON構造の例

```json
{
	"address": "TALICELCD3XPH4FFI5STGGNSNSWPOTG5E4DS2TOS",
	"balance": 124446551689680,
	"vestedBalance": 1041345514976241,
	"importance": 0.010263666447108395,
	"publicKey": "a11a1a6c17a24252e674d151713cdf51991ad101751e4af02a20c61b59f1fe1a",
	"label": null,
	"harvestedBlocks": 645
}
```

フィールドの説明

*   address：アカウントのアドレス。
*   balance：マイクロNEMのアカウント残高。
*   vestedBalance：マイクロNEMのアカウント残高の既得確定部分。
*   importance：アカウントの重要性 
*   publicKey：アカウントの公開鍵。
*   label：アカウントのラベル(使用されていない、常にnull)。
*   harvestedBlocks：アカウントによってすでに収穫されているブロック数。

### 9.4.アカウントメタデータ

公式情報：[AccountMetaData](http://bob.nem.ninja/docs/#accountMetaData)

概要：アカウントメタデータは、アカウントの追加情報を記述します。 詳細については、アカウント関連のリクエスト([Account related requests](#account-related-requests)をご覧ください。

JSON構造の例

```json
{
    "status": "LOCKED",
    "remoteStatus": "ACTIVE",
    "cosignatoryOf" : [
        <accountinfo>,
        <accountinfo>
    ],
    "cosignatories" : [
        <accountinfo>,
        <accountinfo>
    ]
}
```


フィールドの説明

*   status：照会されたアカウントの収穫状況。収穫状況は、次のいずれかの値になります。『UNKNOWN』：アカウントの収穫状況は不明です。『LOCKED』：アカウントは収穫されていません。『UNLOCKED』：アカウントが収穫されています。
*   remoteStatus：照会されたアカウントのリモートハーベストのステータス。リモート収集ステータスは、次のいずれかの値になります。『ACTIVATING』：アカウントはリモートハーベストを有効にしましたが、まだアクティブではありません。『ACTIVE』：アカウントはリモートハーベスティングを有効にしており、リモートハーベスティングはアクティブです。『DEACTIVATING』：アカウントはリモートハーベスティングを無効にしましたが、リモートハーベスティングはまだ有効です。『INACTIVE』：アカウントは非アクティブなリモートハーベスティングを行っているか、リモートハーベスティングを無効にしており、非アクティブ化が動作しています。
*   cosignatoryOf：AccountInfo構造のJSON配列。このアカウントは配列内の各アカウントに共通して使用されます。
*   cosignatories：AccountInfo構造のJSON配列。この配列には該当アカウントの署名者すべてが格納されます。

### 9.5.アカウントメタデータペア

公式情報：[AccountMetaDataPair](http://bob.nem.ninja/docs/#accountMetaDataPair)

概要：アカウントメタデータのペアには、アカウントの永続的な情報とその状態に関する追加情報が含まれています。

JSON構造の例

```json
{
    "account": <AccountInfo>,
    "meta": <AccountMetaData>
}
```

フィールドの説明

*   account：アカウントオブジェクトを含みます。
*   <AccountInfo>：アカウント情報([AccountInfo](#accountInfo))で説明されているアカウントオブジェクト。
*   meta：アカウントメタデータオブジェクトが含まれます。
*   <AccountMetaData>：[AccountMetaData](#accountMetaData)で説明されているアカウントメタデータオブジェクト。

### 9.6.アカウントの秘密鍵トランザクションページ

公式情報：[AccountPrivateKeyTransactionsPage](http://bob.nem.ninja/docs/#accountPrivateKeyTransactionsPage)

概要：アカウントの秘密鍵トランザクションページには、NISがデータベースから一連のトランザクションを取得するために必要なデータが含まれています。データにはトランザクションが取得されるアカウントの秘密鍵が含まれます。NISがローカルで実行されている場合にのみ、この構造を使用する要求を使用します。フィールド『hash』と『id』はオプションです。

JSON構造の例

```json
{
    "value": "68e4f79f886927de698df4f857de2aada41ccca6617e56bb0d61623b35b08cc0",
    "hash": "44e4968e5aa35fe182d4def5958e23cf941c4bf809364afb4431ebbf6a18c039",
    "id": "12345"
}
```

フィールドの説明

*   value：秘密鍵は16進数文字列です。
*   hash：アカウント情報([AccountInfo](#accountInfo))で説明されているアカウントオブジェクト。
*   meta：オプションのハッシュ値。
*   id：オプションのトランザクションID。

### 9.7.アプリケーションメタデータ

公式情報：[ApplicationMetaData](http://bob.nem.ninja/docs/#applicationMetaData)

概要：アプリケーションメタデータオブジェクトはノード上で実行されているアプリケーションに関する追加情報を提供します。

JSON構造の例

```json
{
    "currentTime": 9189086,
    "application": "NEM Infrastructure Server",
    "startTime": 9060202,
    "version": "0.4.30-BETA",
    "signer": "CN=NEM Community,OU=Development Team,O=NEM,L=Internet,ST=web,C=WD"
}
```

フィールドの説明

*   currentTime：現在のネットワーク時間、つまり、ネメシスブロックの作成から経過した秒数。
*   application：ノード上で実行されているアプリケーションの名前。
*   startTime：アプリケーションが開始されたネットワーク時間。
*   version：アプリケーションのバージョン。
*   signer：アプリケーションで使用される証明書の署名者。

### 9.8.監査収集

公式情報：[AuditCollection](http://bob.nem.ninja/docs/#auditCollection)

概要：監査収集は他のノードからの受信リクエストに関する情報を含む2つの配列で構成されます。最初の配列には未処理のリクエストに関する情報が格納され、2番目の配列には最新のリクエストに関する情報が格納されます。監査収集はデバッグのためのものです。

JSON構造の例

```json
{
	"outstanding": [
		{
			"path": "/chain/score",
			"start-time": 9020618,
			"host": "86.124.91.183",
			"elapsed-time": 5,
			"id": 797725
		}
	],
	"most-recent": [
		{
			"path": "/push/transaction",
			"start-time": 9020621,
			"host": "hachi.nem.ninja",
			"elapsed-time": 2,
			"id": 797750
		}
	]
}
```

フィールドの説明

*   path：相対URLパス。
*   start-time：ネメシスブロックの作成から経過した秒数。
*   host：リクエストを開始したホスト。
*   elapsed-time：リクエストが受信されてから経過した時間(秒)。
*   id：リクエストの一意のID。

### 9.9.ブロック

公式情報：[Block](http://bob.nem.ninja/docs/#block)

概要：ブロックはトランザクション情報を含む構造です。ブロックには最大120のトランザクションを含めることができます。ブロックはアカウントによって生成および署名され、情報がネットワークに分散される手段です。

JSON構造の例(メインネットワーク)

```json
{
	"timeStamp": 9022656,
	"signature": "256ebcfa4f92e2881963359c51095a390b9f4d1b3fee75ae19f96d5e6bcf055abbcaae3e55bcc17e6214924e4e6a9ebbe77357236b1a235e944950b851bda804",
	"prevBlockHash": {
		"data": "0a3d6bea020bb1a503364c37d57392342f368389bb23b05799c54d536d94749b"
	},
	"type": 1,
	"transactions": [
		"Transaction1",
		"Transaction2",
		"…",
		"Transaction11"
	],
	"version": 1744830465,
	"signer": "6c66ea288522990db7a0a63c9c20f532cdcb68dc3c9544fb20f7322c92ceadbb",
	"height": 39324
}
```

フィールドの説明

*   timeStamp：相対URLパス。
*   Signature：ブロックの署名。署名は署名者によって生成され、ブロックデータがノードによって変更されていないことを検証するために使用できます。
*   prevBlockHash：最後のブロックのsha3-256ハッシュは16進数文字列です。
*   type：ブロックタイプ。現在、2つのブロックタイプが使用されています。『-1：敵対ブロックのみがこのタイプです。』『1：通常のブロックタイプ。』
*   transactions：トランザクション構造の配列。この構造の詳細については[トランザクション](#transaction)を参照してください。
*   version：ブロックバージョン。以下のバージョンがサポートされています。『0x68 < 24="" +="" 1（4バイト整数として1744830465）：メインネットワークのバージョン』『0x98="">< 24="" +="">
*   signer：ブロックのハーベスタの公開鍵は16進数で表します。
*   height：ブロックの高さ。各ブロックには固有の高さがあります。後続のブロックの高さは1だけ異なります。

### 9.10.ブロックチェーンスコア

公式情報：[BlockChainScore](http://bob.nem.ninja/docs/#blockChainScore)

概要：ブロックチェーンスコアは、ブロックチェーンがどれくらい良いかを示す指標です。スコアが高いほど、ブロックチェーンが優れています。

JSON構造の例

```json
{
    "score": "17a3077c927d9a7e"
}
```

フィールドの説明

*   score：スコアは0以上の整数です。これは16進数形式で提出されます。

### 9.11.ブロックの高さ

公式情報：[BlockHeight](http://bob.nem.ninja/docs/#blockHeight)

概要：ブロックの高さはブロックチェーン内のブロックの位置を表します。チェーンの最初のブロックの高さは1です。各後続ブロックの高さは、前のブロックよりも1つ高いです。

JSON構造の例

```json
{
    "height": 2649
}
```

フィールドの説明

*   height：高さは0より大きい整数です。

### 9.12.ブートノードリクエスト

公式情報：[BootNodeRequest](http://bob.nem.ninja/docs/#bootNodeRequest)

概要：ブートノード要求JSONオブジェクトは、ローカルノードを起動するための関連データをNISに転送するために使用されます。ブートデータを使用すると、NISはローカルノードオブジェクトを作成してネットワークに接続できます。

JSON構造の例

```json
{
	"metaData": {
		"application": "NIS"
	},
	"endpoint": {
		"protocol": "http",
		"port": 7890,
		"host": "localhost"
	},
	"identity": {
		"private-key": "a6cbd01d04edecfaef51df9486c111abb6299c764a00206eb1d01f4587491b3f",
		"name": "Alice"
	}
}
```

フィールドの説明

*   metaData：メタデータの下部構造の先頭を表します。
*   application：アプリケーション名。
*   endpoint：終点下部構造の始まりを表します。
*   protocol：使用するプロトコル(現在のところHTTPだけがサポートされています)。
*   port：使用するポート。
*   host：使用するIPアドレス。
*   identity：身元の基礎構造を表します。
*   private-key：IDを作成するために使用される秘密鍵。
*   name：ノードの名前(何でもかまいません)。

### 9.13.通信タイムスタンプ

公式情報：[CommunicationTimeStamps](http://bob.nem.ninja/docs/#communicationTimeStamps)

概要：通信タイムスタンプにはリモートNISのネットワーク時刻に関する情報が含まれています。NEMは時間同期メカニズムを使用してネットワーク全体の時間を同期させます。各ノードはコンピュータクロックの時間に加え、他のノードのコンピュータ時刻からの偏差を補償するオフセットであるネットワーク時間を維持します。

JSON構造の例

```json
{
    "sendTimeStamp": 9145477789,
    "receiveTimeStamp": 9145477789
}
```

フィールドの説明

*   sendTimeStamp：応答が送信された時点のネットワーク時間。
*   receiveTimeStamp：リクエストが受信された瞬間のネットワーク時間。

### 9.14.エクスプローラブロックビューモデル

公式情報：[ExplorerBlockViewModel](http://bob.nem.ninja/docs/#explorerBlockViewModel)

概要：以下の構造は便宜上、NEMブロックチェーンエクスプローラで使用されています。データは類似していますが、[ブロック](#block)と同じではありません。

JSON構造の例

```json
{
	"data": [
		{
			"txes": [
				"<explorertransferviewmodel>",
				"<explorertransferviewmodel>"
			],
			"block": "<block>",
			"hash": "a6f62c62eedf4fafe6991e5cf31eae440963577c919f4eae86b4db8f8e572dce",
			"difficulty": 23456345897
		}
	]
}
```


フィールドの説明

*   txes：ブロックのトランザクションを含む配列。
*   <ExplorerTransferViewModel>：エクスプローラ転送ビューモデル([ExplorerBlockViewModel](#explorerTransferViewModel))で説明されているExplorerBlockViewModelオブジェクト。
*   block：JSONブロックオブジェクトを含むエントリ。
*   <Block>：[ブロック](#block)で説明されているBlockオブジェクト。
*   hash：ブロックのハッシュを16進数文字列として表します。
*   difficulty：ブロックの難易度。

### 9.15.エクスプローラ転送ビューモデル

公式情報：[ExplorerTransferViewModel](http://bob.nem.ninja/docs/#explorerTransferViewModel)

概要：以下の構造は便宜上、NEMブロックチェーンエクスプローラで使用されています。データは[トランザクション](#transaction)構造のデータと似ていますが、同一ではありません。

JSON構造の例

```json
{
    "tx": <transaction>,
    "hash": "5cba4614e52af19417fb53c4bdf442a57b9f558aee17ece530a5220da55cf47d",
    "innerHash": "ae3b107f1216e1ccf12b6f3c3c555bc1d95311747338ce66f539ea2c18c0aa57"
}
```

フィールドの説明

*   tx：JSON Transactionオブジェクトを含むエントリ。
*   <Transaction>：トランザクションオブジェクト。トランザクションのタイプによって、構造が異なるように見えます。さまざまなトランザクションタイプについては、[トランザクションオブジェクト](#transaction-objects)を参照してください。
*   hash：トランザクションのハッシュ。
*   innerHash：内部トランザクションのハッシュ。このエントリはマルチシグトランザクションでのみ利用可能です。
*   hash：ブロックのハッシュを16進数文字列として表します。
*   difficulty：ブロックの難易度。

### 9.16.拡張ノードエクスペリエンスペア

公式情報：[ExtendedNodeExperiencePair](http://bob.nem.ninja/docs/#extendedNodeExperiencePair)

概要：他のノードとデータを交換する場合、通信の結果は成功(success)、中立(neutral)、失敗(failure)の3つの異なる結果に分けられます。成功と失敗の場合、ノードの品質を判断できるように結果が保存されます。これは特定のノードがパートナーとして選択される確率に影響します。

JSON構造の例

```json
{
    "node":
    {
        <Node>
    },
    "syncs": 822,
    "experience":
    {
        "s": 357,
        "f": 0
    }
}
```
                
フィールドの説明

*   node：JSON Transactionオブジェクトを含むエントリ。
*   <Transaction>：トランザクションオブジェクト。トランザクションのタイプによって、構造が異なるように見えます。さまざまなトランザクションタイプについては、[トランザクションオブジェクト](#transaction-objects)を参照してください。
*   hash：Nodeの下部構造の始まりを表します。
*   <Node>：ノード([Node](#node))で説明されているリモートノードオブジェクト。
*   syncs：ノードがリモートノードと持っていた同期試行の回数。
*   experience：ノードエクスペリエンスの下部構造の始まりを表します。
*   s：リモートノードとの正常な通信の数。
*   f：リモートノードとの通信に失敗した回数。

### 9.17.収穫情報

公式情報：[HarvestInfo](http://bob.nem.ninja/docs/#harvestInfo)

概要：収穫情報(HarvestInfo)オブジェクトには、アカウントが収穫したブロックに関する情報が含まれています。

JSON構造の例

```json
{
    "timeStamp": 8963798,
    "id": 254378,
    "difficulty": 46534789865332,
    "totalFee": 2041299054,
    "height": 38453
}
```

フィールドの説明

*   timeStamp：ネメシスブロックの作成から経過した秒数。
*   <Transaction>：トランザクションオブジェクト。トランザクションのタイプによって、構造が異なるように見えます。さまざまなトランザクションタイプについては、[トランザクションオブジェクト](#transaction-objects)を参照してください。
*   hash：Nodeの下部構造の始まりを表します。
*   id：収穫されたブロックのデータベースID。
*   difficulty：ブロックの難易度。最初の難易度は100000000000000に設定されました。ブロックの難易度は、常に難易度の10分の1から10倍の間です。
*   totalFee：ブロックを収穫して集められた合計料金。
*   height：収穫されたブロックの高さ。

### 9.18.キーペアビューモデル

公式情報：[KeyPairViewModel](http://bob.nem.ninja/docs/#keyPairViewModel)

概要：キーペアビューモデル(KeyPairViewModel)オブジェクトには、新しいアカウントに関する情報が含まれます。情報には、秘密鍵、公開鍵、およびアドレスが含まれます。

JSON構造の例

```json
{
    "privateKey": "0962c6505d02123c40e858ff8ef21e2b7b5466be12c4770e3bf557aae828390f",
    "publicKey": "c2e19751291d01140e62ece9ee3923120766c6302e1099b04014fe1009bc89d3",
    "address": "NCKMNCU3STBWBR7E3XD2LR7WSIXF5IVJIDBHBZQT"
}
```

フィールドの説明

*   privateKey：アカウントの秘密鍵を16進数文字列として表します。
*   publicKey：アカウントの公開鍵を16進数文字列として表します。
*   address：アカウントのアドレス。

### 9.19.トランザクションオブジェクト

公式情報：[Transaction objects](http://bob.nem.ninja/docs/#transaction-objects)

#### 9.19.1.重要度転送トランザクション

公式情報：[ImportanceTransferTransaction](http://bob.nem.ninja/docs/#importanceTransferTransaction)

概要：NISはあるアカウントの重要性をハーベスティングのために別のアカウントに移す機能を持っています。重要度を受け取ったアカウントはリモートアカウントと呼ばれます。重要性転送トランザクションは、NEMの安全な収穫機能の一部です。重要性トランザクションがブロックに含まれると、アクティブになるには6時間を要します。

JSON構造の例

```json
{
	"timeStamp": 9111526,
	"signature": "651a19ccd09c1e0f8b25f6a0aac5825b0a20f158ca4e0d78f2abd904a3966b6e3599a47b9ff199a3a6e1152231116fa4639fec684a56909c22cbf6db66613901",
	"fee": 3000000,
	"mode": 1,
	"remoteAccount": "cc6c9485d15b992501e57fe3799487e99de272f79c5442de94eeb998b45e0144",
	"type": 2049,
	"deadline": 9154726,
	"version": 1744830465,
	"signer": "a1aaca6c17a24252e674d155713cdf55996ad00175be4af02a20c67b59f9fe8a"
}
```

フィールドの説明

*   timeStamp：ネメシスブロックの作成から経過した秒数。
*   signature：トランザクション署名(マルチシグニチャトランザクションの一部である場合は失われます)。
*   fee：トランザクションの手数料。料金が高ければ高いほど、トランザクションの優先順位は高くなります。高優先度のトランザクションは、優先度の低いトランザクションよりも前にブロックに含まれます。
*   mode：モード。 可能な値は次のとおりです。『1：リモートハーベスティングを有効にします。』『2：リモートハーベスティングを無効にします。』
*   remoteAccount：受信アカウントの公開鍵を16進数文字列で表します。
*   type：トランザクションタイプ。
*   deadline：トランザクションの期限。deadlineは、ネメシスブロックの作成から経過した秒数で与えられます。締め切りに達する前にトランザクションがブロックに含まれない場合、トランザクションは削除されます。
*   version：構造のバージョン。
*   signer：トランザクションを作成したアカウントの公開鍵。

#### 9.19.2.モザイク定義作成トランザクション

公式情報：[MosaicDefinitionCreationTransaction](http://bob.nem.ninja/docs/#mosaicDefinitionCreationTransaction)

概要：モザイクを作成または転送する前に、対応するモザイクの定義を作成してネットワークに公開する必要があります。これはモザイク定義作成トランザクションを介して行われます。

JSON構造の例(テストネットワーク)

```json
{
	"timeStamp": 9111526,
	"signature": "651a19ccd09c1e0f8b25f6a0aac5825b0a20f158ca4e0d78f2abd904a3966b6e3599a47b9ff199a3a6e1152231116fa4639fec684a56909c22cbf6db66613901",
	"fee": 108000000,
	"type": 16385,
	"deadline": 9154726,
	"version": -1744830463,
	"signer": "cbda3edb771d42801a5c6ce0725f9374efade19a8933d6ac22ccfa50c777d0f9",
	"creationFee": 50000000000,
	"creationFeeSink": "53e140b5947f104cabc2d6fe8baedbc30ef9a0609c717d9613de593ec2a266d3",
	"mosaicDefinition": {
		"creator": "cbda3edb771d42801a5c6ce0725f9374efade19a8933d6ac22ccfa50c777d0f9",
		"description": "precious vouchers",
		"id": {
			"namespaceId": "alice.vouchers",
			"name": "Alice's gift vouchers"
		},
		"properties": [
			{
				"name": "divisibility",
				"value": "3"
			},
			{
				"name": "initialSupply",
				"value": "1000"
			},
			{
				"name": "supplyMutable",
				"value": "false"
			},
			{
				"name": "transferable",
				"value": "true"
			}
		],
		"levy": {
			"type": 1,
			"recipient": "TD3RXTHBLK6J3UD2BH2PXSOFLPWZOTR34WCG4HXH",
			"mosaicId": {
				"namespaceId": "nem",
				"name": "xem"
			},
			"fee": 1000
		}
	}
}
```

フィールドの説明

*   timeStamp：ネメシスブロックの作成から経過した秒数。
*   signature：トランザクション署名(マルチシグニチャトランザクションの一部である場合は失われます)。
*   fee：トランザクションの手数料。料金が高ければ高いほど、トランザクションの優先順位は高くなります。高優先度のトランザクションは、優先度の低いトランザクションよりも前にブロックに含まれます。
*   remoteAccount：受信アカウントの公開鍵を16進数文字列で表します。
*   type：トランザクションタイプ。
*   deadline：トランザクションの期限。deadlineは、ネメシスブロックの作成から経過した秒数で与えられます。締め切りに達する前にトランザクションがブロックに含まれない場合、トランザクションは削除されます。
*   version：構造のバージョン。
*   signer：トランザクションを作成したアカウントの公開鍵。
*   creationFee：モザイクの作成のための手数料。
*   creationFeeSink：作成手数料が転送される残高の公開鍵。
*   mosaicDefinition：実際のモザイクの定義。 詳細については、モザイク定義([MosaicDefinition](#mosaicDefinition))を参照してください。

#### 9.19.3.モザイク供給変更トランザクション

公式情報：[MosaicSupplyChangeTransaction](http://bob.nem.ninja/docs/#mosaicSupplyChangeTransaction)

概要：モザイク定義のプロパティ『supplyMutable』がtrueに設定されている場合、モザイク定義の作成者は供給を変更、つまり供給を増減することができます。

JSON構造の例(テストネットワーク)

```json
{
	"timeStamp": 9111526,
	"signature": "651a19ccd09c1e0f8b25f6a0aac5825b0a20f158ca4e0d78f2abd904a3966b6e3599a47b9ff199a3a6e1152231116fa4639fec684a56909c22cbf6db66613901",
	"fee": 108000000,
	"type": 16386,
	"deadline": 9154726,
	"version": -1744830463,
	"signer": "d99e88c90da71a4b0d848454e59e296c9ef7a8f018f3eaa3a198dc460b6621a4",
	"supplyType": 1,
	"delta": 123,
	"mosaicId": {
		"namespaceId": "alice.vouchers",
		"name": "gift vouchers"
	}
}
```

フィールドの説明

*   timeStamp：ネメシスブロックの作成から経過した秒数。
*   signature：トランザクション署名(マルチシグニチャトランザクションの一部である場合は失われます)。
*   fee：トランザクションの手数料。料金が高ければ高いほど、トランザクションの優先順位は高くなります。高優先度のトランザクションは、優先度の低いトランザクションよりも前にブロックに含まれます。
*   remoteAccount：受信アカウントの公開鍵を16進数文字列で表します。
*   type：トランザクションタイプ。
*   deadline：トランザクションの期限。deadlineは、ネメシスブロックの作成から経過した秒数で与えられます。締め切りに達する前にトランザクションがブロックに含まれない場合、トランザクションは削除されます。
*   version：構造のバージョン。
*   signer：トランザクションを作成したアカウントの公開鍵。
*   supplyType：供給タイプ。 サポートされている電源の種類は次のとおりです。『1：供給の増加。』『2：供給の減少。』
*   delta：モザイクの単位で供給が変化します。
*   mosaicId：モザイクID。 詳細については[MosaicId](#mosaicId)を参照してください。

#### 9.19.4.マルチシグ集計変更トランザクション

公式情報：[MultisigAggregateModificationTransaction](http://bob.nem.ninja/docs/#multisigAggregateModificationTransaction)

概要：マルチシグ集計変更トランザクションはNEMのマルチシグアカウントシステムの一部です。 マルチシグ集計変更トランザクションは、トランザクション内でマルチシグ署名者変更の配列と最小署名者の変更を保持します。マルチシグ集計変更トランザクションは、マルチシグトランザクションで包括することができます。最小署名者(minCosignatories)フィールドを使用する集計変更トランザクションでは、メインネットで『0x68000002(10進数1744830466)』testnetでは『0x98000002(10進数-1744830462)』のバージョンが必要です。

JSON構造の例(メインネットワーク)

```json
{
	"timeStamp": 9111526,
	"signature": "651a19ccd09c1e0f8b25f6a0aac5825b0a20f158ca4e0d78f2abd904a3966b6e3599a47b9ff199a3a6e1152231116fa4639fec684a56909c22cbf6db66613901",
	"fee": 3000000,
	"type": 257,
	"deadline": 9154726,
	"version": 1744830466,
	"signer": "a1aaca6c17a24252e674d155713cdf55996ad00175be4af02a20c67b59f9fe8a",
	"modifications": [
		"<multisigcosignatorymodification>",
		"<multisigcosignatorymodification>"
	],
	"minCosignatories": {
		"relativeChange": 2
	}
}
```

フィールドの説明

*   timeStamp：ネメシスブロックの作成から経過した秒数。
*   signature：トランザクション署名(マルチシグニチャトランザクションの一部である場合は失われます)。
*   fee：トランザクションの手数料。料金が高ければ高いほど、トランザクションの優先順位は高くなります。高優先度のトランザクションは、優先度の低いトランザクションよりも前にブロックに含まれます。
*   remoteAccount：受信アカウントの公開鍵を16進数文字列で表します。
*   type：トランザクションタイプ。
*   deadline：トランザクションの期限。deadlineは、ネメシスブロックの作成から経過した秒数で与えられます。締め切りに達する前にトランザクションがブロックに含まれない場合、トランザクションは削除されます。
*   version：構造のバージョン。
*   signer：トランザクションを作成したアカウントの公開鍵。
*   modifications：マルチシグ変更のJSON配列。
*   minCosignatories：最小署名者変更を保持するJSONオブジェクト。
*   relativeChange：最小署名者の相対的な変化を示す値。

#### 9.19.5.マルチシグ署名者変更

公式情報：[MultisigCosignatoryModification](http://bob.nem.ninja/docs/#multisigCosignatoryModification)

概要：マルチシグ署名者変更はNEMのマルチシグアカウントシステムの一部です。マルチシグ署名者変更では、署名者はマルチシグアカウントに追加または削除されます。マルチシグ署名者変更は、マルチシグ集計変更トランザクションの一部です(詳細は以下を参照してください)。

JSON構造の例

```json
{
    "modificationType": 1,
    "cosignatoryAccount": "213150649f51d6e9113316cbec5bf752ef7968c1e823a28f19821e91daf848be"
}
```

フィールドの説明

*   modificationType：変更の種類。 可能な値は次のとおりです。『1：新しい共通記号を追加する。』『2：既存の協会を削除する。』
*   cosignatoryAccount：署名者アカウントの公開鍵を16進数文字列で表します。

#### 9.19.6.マルチシグ署名トランザクション

公式情報：[MultisigSignatureTransaction](http://bob.nem.ninja/docs/#multisigSignatureTransaction)

概要：マルチシグ署名トランザクションはNEMのマルチシグアカウントシステムの一部です。マルチシグ署名トランザクションは対応するマルチシグトランザクションに含まれ、マルチシグアカウントの署名者がそのアカウントのマルチシグトランザクションに署名する方法です。

JSON構造の例(テストネットワーク)

```json
{
	"timeStamp": 9111526,
	"signature": "651a19ccd09c1e0f8b25f6a0aac5825b0a20f158ca4e0d78f2abd904a3966b6e3599a47b9ff199a3a6e1152231116fa4639fec684a56909c22cbf6db66613901",
	"fee": 3000000,
	"type": 257,
	"deadline": 9154726,
	"version": -1744830463,
	"signer": "a1aaca6c17a24252e674d155713cdf55996ad00175be4af02a20c67b59f9fe8a",
	"otherHash": {
		"data": "44e4968e5aa35fe182d4def5958e23cf941c4bf809364afb4431ebbf6a18c039"
	},
	"otherAccount": "TDGIMREMR5NSRFUOMPI5OOHLDATCABNPC5ID2SVA"
}
```

フィールドの説明

*   timeStamp：ネメシスブロックの作成から経過した秒数。
*   signature：トランザクション署名(マルチシグニチャトランザクションの一部である場合は失われます)。
*   fee：トランザクションの手数料。料金が高ければ高いほど、トランザクションの優先順位は高くなります。高優先度のトランザクションは、優先度の低いトランザクションよりも前にブロックに含まれます。
*   remoteAccount：受信アカウントの公開鍵を16進数文字列で表します。
*   type：トランザクションタイプ。
*   deadline：トランザクションの期限。deadlineは、ネメシスブロックの作成から経過した秒数で与えられます。締め切りに達する前にトランザクションがブロックに含まれない場合、トランザクションは削除されます。
*   version：構造のバージョン。
*   signer：トランザクションを作成したアカウントの公開鍵。
*   otherHash：対応するマルチシグトランザクションの内部トランザクションハッシュ。
*   otherAccount：対応するマルチシグアカウントのアドレス。

#### 9.19.7.マルチシグトランザクション

公式情報：[MultisigTransaction](http://bob.nem.ninja/docs/#multisigTransaction)

概要：マルチシグトランザクションは、マルチシグアカウントから別のアカウントへのトランザクションを行う唯一の方法です。マルチシグトランザクションでは、内部で別のトランザクションが行われます。内部トランザクションは、転送、重要度転送、または集計変更トランザクションです。また、マルチシグトランザクションは内部にマルチシグアカウントの署名者からのマルチシグ署名トランザクションを持っています。

JSON構造の例(テストネットワーク)

```json
{
	"timeStamp": 9111526,
	"signature": "651a19ccd09c1e0f8b25f6a0aac5825b0a20f158ca4e0d78f2abd904a3966b6e3599a47b9ff199a3a6e1152231116fa4639fec684a56909c22cbf6db66613901",
	"fee": 3000000,
	"type": 257,
	"deadline": 9154726,
	"version": -1744830463,
	"signer": "a1aaca6c17a24252e674d155713cdf55996ad00175be4af02a20c67b59f9fe8a",
	"otherTrans": "<inner transaction=\"\">",
	"signatures": [
		"<multisigsignaturetransaction>",
		"<multisigsignaturetransaction>"
	]
}
```

フィールドの説明

*   timeStamp：ネメシスブロックの作成から経過した秒数。
*   signature：トランザクション署名(マルチシグニチャトランザクションの一部である場合は失われます)。
*   fee：トランザクションの手数料。料金が高ければ高いほど、トランザクションの優先順位は高くなります。高優先度のトランザクションは、優先度の低いトランザクションよりも前にブロックに含まれます。
*   remoteAccount：受信アカウントの公開鍵を16進数文字列で表します。
*   type：トランザクションタイプ。
*   deadline：トランザクションの期限。deadlineは、ネメシスブロックの作成から経過した秒数で与えられます。締め切りに達する前にトランザクションがブロックに含まれない場合、トランザクションは削除されます。
*   version：構造のバージョン。
*   signer：トランザクションを作成したアカウントの公開鍵。
*   otherTrans：内部トランザクション。内部トランザクションは転送トランザクション、重要度転送トランザクション、またはマルチシグ集計変更トランザクションとすることができます。内部トランザクションに有効な署名はありません。
*   signatures：マルチシグ署名トランザクション(MulsigSignatureTransaction)オブジェクトのJSON配列。

#### 9.19.8.ネームスペーストランザクションのプロビジョニング

公式情報：[ProvisionNamespaceTransaction](http://bob.nem.ninja/docs/#provisionNamespaceTransaction)

概要：アカウントは1年間ネームスペースを借りることができ、1年後に契約を更新することができます。これは、ネームスペーストランザクションのプロビジョニング(ProvisionNamespaceTransaction)を介して行われます。

JSON構造の例(テストネットワーク)

```json
{
	"timeStamp": 9111526,
	"signature": "651a19ccd09c1e0f8b25f6a0aac5825b0a20f158ca4e0d78f2abd904a3966b6e3599a47b9ff199a3a6e1152231116fa4639fec684a56909c22cbf6db66613901",
	"fee": 108000000,
	"type": 8193,
	"deadline": 9154726,
	"version": -1744830463,
	"signer": "d99e88c90da71a4b0d848454e59e296c9ef7a8f018f3eaa3a198dc460b6621a4",
	"rentalFeeSink": "3e82e1c1e4a75adaa3cba8c101c3cd31d9817a2eb966eb3b511fb2ed45b8e262",
	"rentalFee": 5000000000,
	"newPart": "voucher",
	"parent": "alice"
}
```

フィールドの説明

*   timeStamp：ネメシスブロックの作成から経過した秒数。
*   signature：トランザクション署名(マルチシグニチャトランザクションの一部である場合は失われます)。
*   fee：トランザクションの手数料。料金が高ければ高いほど、トランザクションの優先順位は高くなります。高優先度のトランザクションは、優先度の低いトランザクションよりも前にブロックに含まれます。
*   mode：モード。 可能な値は次のとおりです。『1：リモートハーベスティングを有効にします。』『2：リモートハーベスティングを無効にします。』
*   remoteAccount：受信アカウントの公開鍵を16進数文字列で表します。
*   type：トランザクションタイプ。
*   deadline：トランザクションの期限。deadlineは、ネメシスブロックの作成から経過した秒数で与えられます。締め切りに達する前にトランザクションがブロックに含まれない場合、トランザクションは削除されます。
*   version：構造のバージョン。
*   signer：トランザクションを作成したアカウントの公開鍵。
*   rentalFeeSink：レンタル料が払い出されるアカウントの公開鍵。
*   rentalFee：ネームスペースをレンタルするための手数料。
*   newPart：親に連結された新しい部分は区切りとして『.』で始まります。
*   parent：親のネームスペース。トランザクションがルートネームスペースをレンタルする場合、これはnullになります。

#### 9.19.9.転送トランザクション

公式情報：[TransferTransaction](http://bob.nem.ninja/docs/#transferTransaction)

概要：転送トランザクションには、XEMまたはモザイクの別のアカウントへの転送に関するデータが含まれます。バージョン1とバージョン2の2つの転送トランザクションがあります。転送トランザクションバージョン1では、XEMとメッセージのみを転送でき、転送トランザクションバージョン2ではさらにモザイクのセットを転送できます。

JSON構造の例(転送トランザクションバージョン1)

```json
{
	"timeStamp": 9111526,
	"amount": 1000000000,
	"signature": "651a19ccd09c1e0f8b25f6a0aac5825b0a20f158ca4e0d78f2abd904a3966b6e3599a47b9ff199a3a6e1152231116fa4639fec684a56909c22cbf6db66613901",
	"fee": 3000000,
	"recipient": "TDGIMREMR5NSRFUOMPI5OOHLDATCABNPC5ID2SVA",
	"type": 257,
	"deadline": 9154726,
	"message": {
		"payload": "74657374207472616e73616374696f6e",
		"type": 1
	},
	"version": -1744830463,
	"signer": "a1aaca6c17a24252e674d155713cdf55996ad00175be4af02a20c67b59f9fe8a"
}
```

JSON構造の例(転送トランザクションバージョン2)

```json
{
	"timeStamp": 9111526,
	"amount": 123000000,
	"signature": "fad7ea2b5df5f7846f45fd9983a75ad8d333af3660f4f0d355864420f4482605d675e89d97177385338b226097342b4222add52c5397423f9eaf6b01fe3ef70c",
	"fee": 3000000,
	"recipient": "TBEH27FNRS43FNH3PXE4XN3H7HXA37H77APSZW46",
	"type": 257,
	"deadline": 9154726,
	"message": {
		"payload": "74657374207472616e73616374696f6e",
		"type": 1
	},
	"version": -1744830462,
	"signer": "cb4ef3709d25ccd0c022b2d53e4ce31478ebc4bf177b1b54482afb8e55692521",
	"mosaics": [
		{
			"mosaicId": {
				"namespaceId": "id0",
				"name": "name0"
			},
			"quantity": 10
		},
		{
			"mosaicId": {
				"namespaceId": "id1",
				"name": "name1"
			},
			"quantity": 11
		}
	]
}
```

フィールドの説明

*   timeStamp：ネメシスブロックの作成から経過した秒数。
*   amount：送信者から受信者に転送されるマイクロNEMの量。
*   signature：トランザクション署名(マルチシグニチャトランザクションの一部である場合は失われます)。
*   fee：トランザクションの手数料。料金が高ければ高いほど、トランザクションの優先順位は高くなります。高優先度のトランザクションは、優先度の低いトランザクションよりも前にブロックに含まれます。
*   recipient：受信者のアドレス。
*   remoteAccount：受信アカウントの公開鍵を16進数文字列で表します。
*   type：トランザクションタイプ。
*   deadline：トランザクションの期限。deadlineは、ネメシスブロックの作成から経過した秒数で与えられます。締め切りに達する前にトランザクションがブロックに含まれない場合、トランザクションは削除されます。
*   message：オプションでトランザクションにメッセージを含めることができます。この場合トランザクションにはメッセージの下部構造が含まれます。そうでない場合、フィールドはnullです。
*   payload：トランザクションにメッセージが含まれている場合のオプションフィールド。ペイロードは実際に(出来るだけ暗号化された)メッセージデータです。
*   mosaics：[モザイク](#mosaic)オブジェクトの配列。
*   version：構造のバージョン。
*   signer：トランザクションを作成したアカウントの公開鍵。

### 9.20.モザイク

公式情報：[Mosaic](http://bob.nem.ninja/docs/#mosaic)

概要：モザイクはモザイクの定義のインスタンスを表します。モザイクは転送トランザクションを使用して転送することができます。

JSON構造の例

        {
                "mosaicId": {
                "namespaceId": "alice.drinks",
                "name": "orange juice"
                },
                "quantity": 123000
                }

フィールドの説明

*   mosaicId：モザイクID。[MosaicId](#mosaicId)を参照してください。
*   quantity：モザイクの数量。量は常にモザイクの最小単位で与えられる。すなわち、それが3の分割可能性を有する場合、その量はミリ秒単位で与えられる。

### 9.21.モザイク定義

公式情報：[MosaicDefinition](http://bob.nem.ninja/docs/#mosaicDefinition)

概要：モザイク定義は資産(asset)クラスを記述します。一部のフィールドは必須フィールドでその他はオプションです。モザイク定義のプロパティは常にデフォルト値を持ち、デフォルト値と異なる場合にのみ提供する必要があります。

JSON構造の例

```json
{
	"creator": "10cfe522fe23c015b8ab24ef6a0c32c5de78eb55b2152ed07b6a092121187100",
	"id": {
		"namespaceId": "alice.drinks",
		"name": "orange juice"
	},
	"description": "A healthy drink with lots of vitamins",
	"properties": [
		{
			"name": "divisibility",
			"value": "3"
		},
		{
			"name": "initialSupply",
			"value": "1000"
		},
		{
			"name": "supplyMutable",
			"value": "false"
		},
		{
			"name": "transferable",
			"value": "true"
		}
	],
	"levy": {
		"type": 1,
		"recipient": "TD3RXTHBLK6J3UD2BH2PXSOFLPWZOTR34WCG4HXH",
		"mosaicId": {
			"namespaceId": "alice.drinks",
			"name": "orange juice"
		},
		"fee": 1000
	}
}
```

フィールドの説明

*   creator：モザイク定義作成者の公開鍵。
*   id：モザイクID。[MosaicId](#mosaicId)を参照してください。
*   description：モザイクの説明。 説明の長さは最大512文字で空であってはなりません。
*   properties：モザイクのプロパティ。プロパティはすべてのプロパティのデフォルト値が適用される空の配列です。詳細については[MosaicProperties](#mosaicProperties)を参照してください。
*   levy：モザイクのオプション徴収。 作成者はモザイク転送ごとに追加料金を請求することができます。詳細はモザイク徴収([MosaicLevy](#mosaicLevy))を参照してください。

### 9.22.モザイク定義メタデータペア

公式情報：[MosaicDefinitionMetaDataPair](http://bob.nem.ninja/docs/#mosaicDefinitionMetaDataPair)

概要：モザイク定義はデータベースIDとモザイク定義オブジェクトで構成されます。idはページングをサポートするリクエストに必要です。

JSON構造の例

```json
{
	"meta": {
		"id": 3541
	},
	"mosaic": {
		"creator": "10cfe522fe23c015b8ab24ef6a0c32c5de78eb55b2152ed07b6a092121187100",
		"id": {
			"namespaceId": "alice.drinks",
			"name": "orange juice"
		},
		"description": "A healthy drink with lots of vitamins",
		"properties": []
	}
}
```

フィールドの説明

*   meta：メタデータオブジェクトのラベル。
*   id：モザイク定義オブジェクトのID。
*   mosaic：モザイク定義オブジェクトのラベル。オブジェクトの詳細な説明についてはモザイク定義([MosaicDefinition](#mosaicDefinition))を参照してください。
*   creator：モザイク定義作成者の公開鍵。
*   id：モザイクID。[MosaicId](#mosaicId)を参照してください。
*   description：モザイクの説明。 説明の長さは最大512文字で空であってはなりません。
*   properties：モザイクのプロパティ。

### 9.23.モザイクプロパティ

公式情報：[MosaicProperties](http://bob.nem.ninja/docs/#mosaicProperties)

概要：各モザイク定義には一連のプロパティがあります。各プロパティには指定されていない場合に適用されるデフォルト値があります。将来のリリースでは利用可能なプロパティのセットに追加のプロパティが追加される可能性があります。利用可能なプロパティとそのデフォルト値は次のとおりです。

*   divisibility：モザイクを分割できる最小のサブユニットを定義します。可分性が0の場合はユニット全体のみが転送可能であり、可分性が3の場合はモザイクをミリ単位で転送できることを意味します。
*   initialSupply：最初に作成されるモザイクの単位数を定義します。これらのモザイクはモザイクの作成者に貸し出されます。最初の供給には9,000,000,000ユニットの上限があります。
*   supplyMutable：後でモザイク供給変更トランザクション([MosaicSupplyChangeTransaction](#mosaicSupplyChangeTransaction))を使用して作成者が供給を変更できるかどうかを決定します。可能な値は『true』と『false』であり、前者は供給を変更することができ、後者は供給が常に固定されていることを意味します。
*   transferable：モザイクを作成者以外のユーザーに転送できるかどうかを判断します。特定のシナリオではユーザーがモザイクを交換できるようにすることは望ましくありません(たとえば、モザイクは会社が他のユーザーに移転したくないボーナスポイントを表す場合など)。可能な値は『true』と『false』です。前者はユーザー間で任意に転送でき、後者は作成者との間でのみモザイクを転送できることを意味します。
* JSON構造の例

```json
[
	{
		"name": "divisibility",
		"value": "3"
	},
	{
		"name": "initialSupply",
		"value": "1000"
	},
	{
		"name": "supplyMutable",
		"value": "false"
	},
	{
		"name": "transferable",
		"value": "true"
	}
]
```

フィールドの説明

    *   name：モザイクプロパティの名前。
    *   value：モザイクプロパティの名前。

### 9.24.モザイク徴収

公式情報：[MosaicLevy](http://bob.nem.ninja/docs/#mosaicLevy)

概要：モザイク定義ではこれらのモザイクを転送するための徴収をオプションで指定できます。これは転送のためにいくつかの手数料を徴収する必要がある転送者によって必要となる可能性があります。

JSON構造の例

```json
{
	"type": 1,
	"recipient": "TD3RXTHBLK6J3UD2BH2PXSOFLPWZOTR34WCG4HXH",
	"mosaicId": {
		"namespaceId": "nem",
		"name": "xem"
	},
	"fee": 1000
}
```

フィールドの説明

*   type：課金タイプ。次のタイプがサポートされています：『1：課税は絶対料金です。フィールド『fee』は、指定されたモザイクのサブユニットの数を受信者に転送することを示します。』『2：徴収額は譲渡された金額から計算されます。項目『fee』には転送された数量のパーセンタイル数が受信者に転送される数量として記載されています。』
*   recipient：徴収の受領者。
*   mosaicId：徴収されたモザイク。
*   recipient：手数料。解釈は徴収の種類に依存する

### 9.25.モザイクId

公式情報：[MosaicId](http://bob.nem.ninja/docs/#mosaicId)

概要：モザイクIDは基本的なモザイク定義を一意に識別します。

JSON構造の例

        {
                "namespaceId": "alice.drinks",
                "name": "orange juice"
                }

フィールドの説明

*   namespaceId：対応するネームスペースID。詳細についてはネームスペース([Namespace](#namespace))構造の説明を参照してください。
*   name：モザイク定義の名前。

### 9.26.ネームスペース

公式情報：[Namespace](http://bob.nem.ninja/docs/#namespace)

概要：ネームスペースはドメインのNEMバージョンです。 料金を支払うことによって、1年間ネームスペースを借りることができます。ネームスペース部分の命名には一定の制限があります。対応するネームスペースの章を参照してください。

JSON構造の例

        {
                "fqn": "makoto.metal.coins",
                "owner": TD3RXTHBLK6J3UD2BH2PXSOFLPWZOTR34WCG4HXH",
                "height": 13465
                }

フィールドの説明

*   fqn：ネームスペースの完全修飾名。ネームスペースIDとも呼ばれます。
*   owner：ネームスペースの所有者。
*   height：所有権が始まる高さ。

### 9.27.ネームスペースメタデータペア

公式情報：[NamespaceMetaDataPair](http://bob.nem.ninja/docs/#namespaceMetaDataPair)

概要：ネームスペースはネームスペースオブジェクトとデータベースIDで構成されます。idはページングをサポートするリクエストに必要です。

JSON構造の例

```json
{
	"meta": {
		"id": 26264
	},
	"namespace": {
		"fqn": "makoto.metal.coins",
		"owner": "TD3RXTHBLK6J3UD2BH2PXSOFLPWZOTR34WCG4HXH",
		"height": 13465
	}
}
```

フィールドの説明

*   meta：メタデータオブジェクトのラベル。
*   id：ネームスペースオブジェクトのデータベースID。
*   namespace：ネームスペースオブジェクトのラベル。
*   fqn：ネームスペースの完全修飾名。ネームスペースIDとも呼ばれます。
*   owner：ネームスペースの所有者。
*   height：所有権が始まる高さ。

### 9.28.Nemアナウンス結果

公式情報：[NemAnnounceResult](http://bob.nem.ninja/docs/#nemAnnounceResult)

概要：Nemアナウンス結果(NemAnnounceResult)は追加のフィールド『transactionHash』、マルチシグトランザクションの場合は『innerTransactionHash』となり、Nemアナウンス結果を拡張します。

JSON構造の例

```json
{
	"type": 4,
	"code": 6,
	"message": "status",
	"transactionHash": {
		"data": "c1786437336da077cd572a27710c40c378610e8d33880bcb7bdb0a42e3d35586"
	},
	"innerTransactionHash": {
		"data": "44e4968e5aa35fe182d4def5958e23cf941c4bf809364afb4431ebbf6a18c039"
	}
}
```

フィールドの説明

*   type：Nemアナウンス結果([NemRequestResult](#nemRequestResult))の説明を参照してください。
*   code：Nemアナウンス結果([NemRequestResult](#nemRequestResult))の説明を参照してください。
*   message：Nemアナウンス結果([NemRequestResult](#nemRequestResult))の説明を参照してください。
*   transactionHash：トランザクションのJSONハッシュオブジェクト。
*   innerTransactionHash：内部トランザクションのJSONハッシュオブジェクト。トランザクションがマルチシグトランザクションでない場合はnull。

### 9.29.Nem非同期タイマービジター

公式情報：[NemAsyncTimerVisitor](http://bob.nem.ninja/docs/#nemAsyncTimerVisitor)

概要：NISはタイマーを使用して定期的なタスクをスケジュールします。これらのタスクは監視され、その結果が記憶されます。Nem非同期タイマービジター(NemAsyncTimeVisitor)構造は情報を保持します。

JSON構造の例

```json
{
	"last-delay-time": 3000,
	"executions": 1024,
	"failures": 0,
	"successes": 1024,
	"last-operation-start-time": 9317695,
	"is-executing": 0,
	"name": "FORAGING",
	"average-operation-time": 0,
	"last-operation-time": 0
}
```

フィールドの説明

*   last-delay-time：タイマーの最後の実行からのミリ秒数。
*   executions：タスクが実行された回数。
*   failures：タスクが失敗した回数。
*   successes：タスクが成功した回数。
*   last-operation-start-time：前回タスクが開始された時刻。
*   is-executing：タスクが実行中の場合はtrue、そうでない場合はfalse。
*   name：タスクの名前。
*   average-operation-time：タスクの名前。タスクが平均して必要な秒数。
*   last-operation-time：タスクが最後に必要な秒数。

### 9.30.Nemリクエストリザルト

公式情報：[NemRequestResult](http://bob.nem.ninja/docs/#nemRequestResult)

概要：新しいトランザクションをアナウンスするなど、リクエストによってはリクエストの結果に関する詳細情報が返されます。そのような場合、リクエストの結果はNemリクエストリザルト(NemRequestResult)という特別なJSONオブジェクトに返されます。この構造は通常、検証を実行したり、ステータスを返す要求に使用されます。

JSON構造の例

        {
                "type": 4,
                "code": 6,
                "message": "status"
                }

フィールドの説明

*   type：タイプは応答された要求に依存します。コードフィールドの解釈はタイプによって異なります。 現在、次のタイプがサポートされています：『1：結果は検証結果です。(The result is a validation result.)』『2：結果はheartbeatの結果です。(The result is a heart beat result.)』『4：結果はステータスを示します。(The result indicates a status.)』
*   code：コードの意味は型に依存します。タイプ1(検証結果)では、0と1だけが失敗しなかったことを意味します。検証結果の完全なリストについては、NISエラー([NIS Error](#appendix-B:-NIS-errors))を参照してください。次のコードが最も頻繁に発生します。
*   *   0：ニュートラルの結果。典型的な例はノードが受信トランザクションを検証し、それがトランザクションについて既知であることを認識することです。この場合、成功(ノード自体が新しいトランザクションを持つことを意味する)でも、トランザクション自体が有効であるために失敗ではありません。
    *   1：成功の結果。典型的な例はノードが新しい有効なトランザクションを検証することです。
    *   2：不明なエラー。検証が不明な理由で失敗しました。
    *   3：検証されたエンティティは既に期限を過ぎています。
    *   4：エンティティは、あまりにも遠すぎる将来の期限を使用した。
    *   5：操作に必要な残高が不足していたアカウントがありました。
    *   6：トランザクションで提供されたメッセージが大きすぎます。
    *   7：検証されたエンティティのハッシュがすでにデータベースにあります。
    *   8：エンティティの署名を検証できませんでした。
    *   9：エンティティは過去にあまりにも遠すぎるタイムスタンプを使用しました。
    *   10：エンティティは将来受け入れられないタイムスタンプを使用しました。
    *   11：エンティティは使用できません。
    *   12：リモートブロックチェーンのスコアは劣っています(優れたスコアが約束されていますが)。
    *   13：リモートブロックチェーンが検証に失敗しました。
    *   14：重要性の移転が重複して検出されました。
    *   15：提供されたブロックにトランザクションが多すぎます。
    *   16：ブロックには、ハーベスタによって署名されたトランザクションが含まれています。
    *   17：以前の重要度トランザクションは新しいトランザクションと競合します。
    *   18：重要度転送のアクティブ化が、前のアクティブ化中に試行されました。
    *   19：重要度転送の非アクティブ化が試行されましたが、アクティブではありません。

タイプ2では次のコードがサポートされています。

    *   1：正常なheartbeatが検出されました。

タイプ3では次のコードがサポートされています。

    *   0：不明なステータス。
    *   1：NISが停止しています。
    *   2：NISが開始されています。
    *   3：NISが動作しています。
    *   4：NISはローカルノードを起動しています(NISが実行中であることを意味します)。
    *   5：ローカルノードがブートされている(NISが実行中であることを意味します)。
    *   6：ローカルノードが同期している(NISが実行中で、ローカルノードが起動していることを意味します)。
    *   7：使用可能なリモートノードがありません(NISが実行され、ローカルノードが起動されていることを意味します)。
    *   8：NISは現在ブロックチェーンをロードしています。

### 9.31.NISノード情報

公式情報：[NisNodeInfo](http://bob.nem.ninja/docs/#nisNodeInfo)

概要：NISノード情報(NisNodeInfo)オブジェクトはノードに関する詳細情報を提供します。

JSON構造の例

        {
                "node": {
                <Node>
                },
                "nisInfo": {
                <ApplicationMetaData>
                }
                }

フィールドの説明

*   node：ノードの下部構造の始まりを示します。
*   <Node>：ノード([Node](#node))で説明されているNodeオブジェクト。
*   nisInfo：アプリケーションメタデータの下部構造の始まりを示します。
*   <ApplicationMetaData>：アプリケーションメタデータ([ApplicationMetaData](#applicationMetaData))で説明されているApplicationMetaDataオブジェクト。

### 9.32.ノード

公式情報：[Node](http://bob.nem.ninja/docs/#node)

概要：ノードはデータの送受信のようにネットワーク内で通信を行うエンティティです。ノードはノードがネットワークに自身を識別させることができるアカウントに結び付けられた識別情報を有します。通信はノードのエンドポイントを介して行われます。さらにノードはメタデータ情報を提供します。

JSON構造の例

```json
{
	"metaData": {
		"features": 1,
		"networkId": 104,
		"application": "NIS",
		"version": "0.4.30-BETA",
		"platform": "Oracle Corporation (1.8.0_05) on Windows 8.1"
	},
	"endpoint": {
		"protocol": "http",
		"port": 7890,
		"host": "85.25.36.97"
	},
	"identity": {
		"name": "Hi, I am Alice2",
		"public-key": "3302e7703ee9f364c25bbfebb9c12ac91fa9dcd69e09a5d4f3830d71505a2350"
	}
}
```

フィールドの説明

*   metaData：メタデータの部分構造の始まりを示します。
*   features：ノードが持つfeaturesの数。
*   networkId：ネットワークID。次のネットワークIDがサポートされています。『104（16進数0x68）：メインネットワークID。』『152（16進数0x98）：テストネットワークID。』
*   application：ノードを実行しているアプリケーションの名前。
*   version：アプリケーションのバージョン。
*   platform：基礎となるプラットフォーム(OS、javaバージョン)。
*   endpoint：終点下部構造の始まりを示します。
*   protocol：通信に使用されるプロトコル(HTTPまたはHTTPS)
*   port：通信に使用されるポート。
*   host：エンドポイントのIPアドレス。
*   identity：身元の下部構造の始まりを示す。
*   name：ノードの名前。
*   public-key：ノードを識別するために使用される公開鍵。

### 9.33.ノード収集

公式情報：[NodeCollection](http://bob.nem.ninja/docs/#nodeCollection)

概要：ノード収集(NodeCollection)オブジェクトは状態の異なるノードの配列を保持します。次のステータスがサポートされています。

フィールドの説明

*   inactive：ノードへの接続を確立できません。
*   active：接続が確立され、リモートノードが適時に応答する。
*   busy：接続は確立できますが、ノードはタイムアウト制限内で情報を提供できません。
*   failure：接続を確立しようとしたときに致命的なエラーが発生したか、ノードが正しく認証されませんでした。
*   data：ノード収集を示す一般的な状態は、ノードの状態について何も言わずにノードをリストするだけです。

JSON構造の例

        {
                "inactive": [
                <Node>,
                <Node>
                ],
                "active": [
                <Node>,
                <Node>
                ],
                "busy": [
                <Node>,
                <Node>
                ],
                "failure": [
                <Node>,
                <Node>
                ],
                }

フィールドの説明

*   inactive：非アクティブなノードの配列の先頭を示します。
*   active：アクティブなノードの配列の先頭を示します。
*   busy：ビジー状態のノードの配列の先頭を示します。
*   failure：失敗したノードの配列の先頭を示します。
*   <Node>：ノード([Node](#node))で説明されているNodeオブジェクト。

### 9.34.秘密鍵

公式情報：[PrivateKey](http://bob.nem.ninja/docs/#privateKey)

概要：秘密鍵はアカウントの鍵です。アカウントへの秘密鍵を持つ人は誰でもアカウント関連のアクションを開始できます。したがって秘密鍵はすべてのコストをかけて秘密にしておく必要があります。

JSON構造の例

        {
                "value": "68e4f79f886927de698df4f857de2aada41ccca6617e56bb0d61623b35b08cc0",
                }

フィールドの説明

*   value：秘密鍵の256ビット値を16進数文字列として表します。

### 9.35.リクエストアナウンス

公式情報：[RequestAnnounce](http://bob.nem.ninja/docs/#requestAnnounce)

概要：リクエストアナウンス(RequestAnnounce)オブジェクトはトランザクションデータと署名をNISに転送してトランザクションを開始し、ブロードキャストを行うために使用されます。

JSON構造の例

        {
                "data": "010100000100000000000000200000002b76078fa709bbe675
                2222b215abc7ec0152ffe831fb4f9aed3e7749a425900a0009
                3d0000000000000000002800000054444e46555946584f5353
                334e4e4c4f35465a5348535a49354c33374b4e514945485055
                4d584c54c0d45407000000000b00000001000000030000000c
                3215",
                "signature": "db2473513c7f0ce9f8de6345f0fbe773
                dc687eb571123d08eab4d98f96849eae
                b63fa8756fb6c59d9b9d0e551537c1cd
                ad4a564747ff9291db4a88b65c97c10d"
                }

フィールドの説明

*   data：文字列としてのトランザクションデータ。文字列は最初に対応するbyte配列を作成し(第6.7章を参照)、byte配列を16進数文字列に変換して作成されます。
*   signature：トランザクションの署名(16進数文字列)。

### 9.36.アナウンス準備のリクエスト

公式情報：[RequestPrepareAnnounce](http://bob.nem.ninja/docs/#requestPrepareAnnounce)

概要：アナウンス準備のリクエスト(RequestPrepareAnnounce)オブジェクトは、トランザクションデータと秘密鍵をNISに転送するために使用され、トランザクションを開始してブロードキャストします。

JSON構造の例(テストネットワーク)

```json
{
	"transaction": {
		"timeStamp": 9111526,
		"amount": 1000000000,
		"fee": 3000000,
		"recipient": "TDGIMREMR5NSRFUOMPI5OOHLDATCABNPC5ID2SVA",
		"type": 257,
		"deadline": 9154726,
		"message": {
			"payload": "74657374207472616e73616374696f6e",
			"type": 1
		},
		"version": -1744830463,
		"signer": "a1aaca6c17a24252e674d155713cdf55996ad00175be4af02a20c67b59f9fe8a"
	},
	"privateKey": "68e4f79f886927de698df4f857de2aada41ccca6617e56bb0d61623b35b08cc0"
}
```

フィールドの説明

*   transaction：トランザクションデータ部分の先頭を示します。トランザクションデータについては[Transaction](#transaction)で説明しています。この時点でトランザクションが署名されていないため、フィールドの署名がありません。
*   privateKey：NISがトランザクションに署名するために使用する秘密鍵。

### 9.37.時刻同期結果

公式情報：[TimeSynchronizationResult](http://bob.nem.ninja/docs/#timeSynchronizationResult)

概要：時間同期結果は他の遠隔ノードとのノードのネットワーク時間同期の結果です。共通の時間に合致させるためにノードは毎時の時間を同期させる必要があります。

JSON構造の例

        {
                "dateTime": "2014-11-16 20:47:06",
                "currentTimeOffset": 2786,
                "change": 36
                }

フィールドの説明

*   dateTime：同期が実行された日時。
*   currentTimeOffset：ミリ秒単位でのローカルコンピュータクロックへの現在のオフセット。
*   change：最後の同期と比較したミリ秒単位の変化。

### 9.38.トランザクションメタデータ

公式情報：[TransactionMetaData](http://bob.nem.ninja/docs/#transactionMetaData)

概要：トランザクションメタデータオブジェクトには、トランザクションに関する追加情報が含まれています。

JSON構造の例

        {
                "height": 40706,
                "id": 2769,
                "hash": {
                "data":"37c34ead4c3fe6af42d994135798262f785ba2d807c02ac3608bc10da12e5f87"
                }
                }

フィールドの説明

*   height：トランザクションが含まれていたブロックの高さ。
*   id：トランザクションのID。
*   hash：トランザクションハッシュ。

### 9.39.トランザクションメタデータペア

公式情報：[TransactionMetaDataPair](http://bob.nem.ninja/docs/#transactionMetaDataPair)

概要：トランザクションメタデータオブジェクトには、トランザクションに関する追加情報が含まれています。

JSON構造の例

        {
            "meta":
            <transactionmetadata>,
            "transaction":
            <transaction>
            }

フィールドの説明

*   meta：トランザクションメタデータオブジェクトが含まれます。
*   <TransactionMetaData>：トランザクションメタデータ([TransactionMetaData](#transactionMetaData))で説明されているトランザクションメタデータオブジェクト。
*   Transaction：トランザクションオブジェクトが含まれます。
*   <Transaction>：トランザクション([Transaction](#transaction))に記述されているトランザクションオブジェクト。

### 9.40.未確認トランザクションメタデータ

公式情報：[UnconfirmedTransactionMetaData](http://bob.nem.ninja/docs/#unconfirmedTransactionMetaData)

概要：未確認トランザクションメタデータにはトランザクションがマルチシグトランザクションである場合の内部トランザクションハッシュが含まれます。このデータはマルチシグ署名トランザクションを開始する必要があります。

JSON構造の例

        {
                data": "d7c9e33421e43bf4a5d6e21304c8096c599142755d581bd6e9037f41545a5873"
                }

フィールドの説明

*   data：内部トランザクションのハッシュ、またはトランザクションがマルチシグトランザクションでない場合はnull

### 9.41.未確認トランザクションメタデータペア

公式情報：[UnconfirmedTransactionMetaDataPair](http://bob.nem.ninja/docs/#unconfirmedTransactionMetaDataPair)

概要：未確認トランザクションメタデータにはトランザクションがマルチシグトランザクションである場合の内部トランザクションハッシュが含まれます。このデータはマルチシグ署名トランザクションを開始する必要があります。

JSON構造の例

        {
                "meta":
                <UnconfirmedTransactionMetaData>,
                "transaction":
                <Transaction>
                }

フィールドの説明

*   meta：トランザクションメタデータオブジェクトが含まれます。
*   <UnconfirmedTransactionMetaData>：未確認トランザクションメタデータ([UnconfirmedTransactionMetaData](#unconfirmedTransactionMetaData))で説明されているトランザクションメタデータオブジェクト。
*   transaction：トランザクションオブジェクトが含まれます。
*   <Transaction>：トランザクションに記述されているトランザクションオブジェクト。

### 9.42.エラーオブジェクト

公式情報：[Error object](http://bob.nem.ninja/docs/#error-object)

概要：無効な要求または内部の問題によりNISでエラーが発生すると、JSONエラーオブジェクトが返されます。エラーオブジェクトの解釈はコンテキストに依存します。考えられるエラーの詳細についてはNISエラー([NIS Error](#appendix-B:-NIS-errors))を参照してください。

JSON構造の例

        {
                "timeStamp": 9108808,
                "error": "Bad Request",
                "message": "address must be valid",
                "status": 400
                }

フィールドの説明。

*   timeStamp：ネメシスブロックの作成から経過した秒数。
*   error：エラーの一般的な説明。
*   message：詳細なエラーメッセージ。
*   Status：HTTPステータス。

## 10.NISエラー

公式情報：[Appendix B: NIS Errors](http://bob.nem.ninja/docs/#appendix-B:-NIS-errors)

リクエストの処理中にNISでエラーが発生した場合、その構造は[エラーオブジェクト](#error-object)で説明されているJSONエラーオブジェクトを返します。この章ではNISから返されるエラーメッセージについて説明します。

### 10.1.エラーメッセージ

公式情報：[Error messages](http://bob.nem.ninja/docs/#error-messages)

* **Request method ‘GET’ not supported**
リクエストはGETリクエストとして実行されましたが、POSTリクエストであると予想されていました。

* **address must be valid**
リクエストで指定されたアドレスが無効です。アドレスはリクエストを処理する前に検証されます。検証に失敗すると、このメッセージを含むエラーが返されます。

* **FAILURE_SERVER_LIMIT**
NISで収穫が許可されたアカウントの数を超えました。

* **JSON Object was expected**
リクエストにパラメータがありません。

* **FAILURE_UNKNOWN_ACCOUNT**
リクエストで指定されたアカウントが不明です。

*  **block not found in the db**
要求されたブロックはデータベースに見つかりませんでした。

*  **height must be positive**
リクエストで指定されたブロックの高さはゼロまたは負であった。 ブロックの高さは常にゼロより大きくなければなりません。

* **network has not been booted yet**
ほとんどのリクエストではすでに起動されているリクエストに応答するノードが必要です。ノードがまだ起動されていない場合はこのエラーメッセージが返されます。

* **network boot was already attempted**
既に起動されているノードを起動しようとしました。ノードは一度しかブートできません。

* **remote 123.45.67.89 attempted to call local /node/boot**
リモートノードをブートしようとしました。 ローカルノードだけが起動できます。

* **FAILURE_PAST_DEADLINE**
エンティティの期限はすでに切れています。 期限は常に将来の時刻でなければなりません。

* **FAILURE_FUTURE_DEADLINE**
期限があまりにも先になっています。 期限は将来24時間までしか許可されません。

* **FAILURE_INSUFFICIENT_BALANCE**
アカウントに十分な資金がありません。

* **FAILURE_MESSAGE_TOO_LARGE**
トランザクションのメッセージが512バイトの制限を超えています。

* **FAILURE_HASH_EXISTS**
エンティティのハッシュはすでにキャッシュまたはデータベースに存在します。

* **FAILURE_SIGNATURE_NOT_VERIFIABLE**
エンティティの署名が検証に失敗しました。

* **FAILURE_TIMESTAMP_TOO_FAR_IN_PAST**
エンティティのタイムスタンプが遥か先になっています。

* **FAILURE_TIMESTAMP_TOO_FAR_IN_PAST**
エンティティのタイムスタンプが遥か過去になっています。

* **FAILURE_TIMESTAMP_TOO_FAR_IN_FUTURE**
エンティティのタイムスタンプは、遥か先になっています。

* **FAILURE_INELIGIBLE_BLOCK_SIGNER**
ブロックに不適格な署名者が含まれているため、検証に失敗しました。これは通常、リモートハーベスティングがアクティブ化または非アクティブ化されているときに発生します。

* **FAILURE_ENTITY_UNUSABLE_OUT_OF_SYNC**
リモートノードがローカルノードと同期していないため、エンティティを処理できません。これはノードが完全に同期しておらず、自身のチェーンよりもはるかに高い新しいブロックを受け取った場合に頻繁に発生します。

* **FAILURE_INSUFFICIENT_FEE**
提供されたトランザクションに不十分な手数料があります。

* **FAILURE_NEMESIS_ACCOUNT_TRANSACTION_AFTER_NEMESIS_BLOCK**
提供されたトランザクションには送信者としてのネメシスアカウントがあり、通常のブロックに含めることはできません。

* **FAILURE_TRANSACTION_CACHE_TOO_FULL**
トランザクションキャッシュが限界であるため、トランザクションは拒否されました。これはアカウントが短時間に多すぎるトランザクションを送信しようとしたときに発生します。トランザクションが承認される可能性を高めるために、トランザクション手数料を引き上げることができます。

* **FAILURE_WRONG_NETWORK**
エンティティは間違ったネットワークが指定されていたため、拒否されました。

* **FAILURE_CANNOT_HARVEST_FROM_BLOCKED_ACCOUNT**
ブロックされたアカウント(通常は予約されているNEMファンド)によって収穫されたため、ブロックは拒否されました。

* **FAILURE_DESTINATION_ACCOUNT_HAS_NONZERO_BALANCE**
ゼロ以外の残高を持つアカウントには重要性を移すことはできません。

* **FAILURE_IMPORTANCE_TRANSFER_IN_PROGRESS**
進行中の重要性の移転が既に存在するため、トランザクションは競合しています。

* **FAILURE_IMPORTANCE_TRANSFER_NEEDS_TO_BE_DEACTIVATED**
重要性が既に移転されたため、トランザクションは競合しています。

* **FAILURE_IMPORTANCE_TRANSFER_IS_NOT_ACTIVE**
重要性がまだ移転されていないため、トランザクションは競合しています。

* **FAILURE_TRANSACTION_NOT_ALLOWED_FOR_REMOTE**
トランザクションが不適切な方法でリモートアカウントを使用しているため、検証に失敗しました。

* **FAILURE_MULTISIG_NOT_A_COSIGNER**
トランザクションの署名者が内部トランザクションの送信者アカウントのコーパスリーダではないため、マルチシグトランザクションは拒否されました。

* **FAILURE_MULTISIG_INVALID_COSIGNERS**
マルチシグトランザクションに接続された署名者が無効であるため、検証に失敗しました。

* **FAILURE_MULTISIG_NO_MATCHING_MULTISIG**
対応するマルチシグトランザクションが見つからなかったため、署名トランザクションは拒否されました。

* **FAILURE_TRANSACTION_NOT_ALLOWED_FOR_MULTISIG**
署名者はマルチシグ署名アカウントであるため、トランザクションは拒否されました。マルチシグアカウントはいかなるトランザクションも開始することができません(単一アカウントでは許可されています)。

* **FAILURE_MULTISIG_ALREADY_A_COSIGNER**
トランザクションは、すでにこの署名者を持つマルチシグ署名アカウントに署名者を追加しようとしたため、拒否されました。

* **FAILURE_MULTISIG_MODIFICATION_MULTIPLE_DELETES**
このトランザクションは一度に複数の署名者を削除しようとしたために却下されました。一度に1つの署名者を削除することのみ許可されています。

* **FAILURE_MULTISIG_MODIFICATION_REDUNDANT_MODIFICATIONS**
冗長な変更を行おうとしたためトランザクションは拒否されました。 これはトランザクションが同じ署名者を2回追加しようとした場合に発生します。

* **FAILURE_CONFLICTING_MULTISIG_MODIFICATION**
トランザクションにはマルチシグアカウントの矛盾した変更が含まれていたため拒否されました。 例えばトランザクションが同じ署名者を追加してから削除しようとすると、これが起こります。

* **FAILURE_TOO_MANY_MULTISIG_COSIGNERS**
トランザクションには余分な共約が含まれているため拒否されました。 マルチシグアカウントに許可されている署名者の最大数は32です。

* **FAILURE_MULTISIG_ACCOUNT_CANNOT_BE_COSIGNER**
マルチシグの変更により、マルチシグアカウントが署名者になるため、検証に失敗しました。

* **FAILURE_MULTISIG_MIN_COSIGNATORIES_OUT_OF_RANGE**
署名者の最小数が負であるか、署名者の数よりも大きいため、検証は失敗しました。

* **FAILURE_NAMESPACE_UNKNOWN**
ネームスペースが不明なため、検証に失敗しました。

* **FAILURE_NAMESPACE_ALREADY_EXISTS**
ネームスペースが既に存在するため、検証に失敗しました。

* **FAILURE_NAMESPACE_EXPIRED**
ネームスペースの有効期限が切れているため、検証に失敗しました。

* **FAILURE_NAMESPACE_OWNER_CONFLICT**
トランザクション署名者がネームスペースの所有者ではないため、検証に失敗しました。

* **FAILURE_NAMESPACE_INVALID_NAME(**
ネームスペースの名前が無効であるため、検証に失敗しました。

* **FAILURE_NAMESPACE_INVALID_RENTAL_FEE_SINK**
指定されたネームスペースレンタルフィーシンクが無効であるため、検証に失敗しました。

* **FAILURE_NAMESPACE_INVALID_RENTAL_FEE**
指定されたレンタル手数料が無効であるため、検証に失敗しました。

* **FAILURE_NAMESPACE_PROVISION_TOO_EARLY**
プロビジョニングが早過ぎたため、検証に失敗しました。

* **FAILURE_NAMESPACE_NOT_CLAIMABLE**
ネームスペースに予約された部分が含まれているため、検証ができませんでした。

* **FAILURE_MOSAIC_UNKNOWN**
モザイクが不明なため、検証に失敗しました。

* **FAILURE_MOSAIC_MODIFICATION_NOT_ALLOWED**
既存のモザイクの変更が許可されていないため、検証に失敗しました。

* **FAILURE_MOSAIC_CREATOR_CONFLICT**
トランザクション署名者がモザイクの作成者ではないため、検証に失敗しました。

* **FAILURE_MOSAIC_SUPPLY_IMMUTABLE**
モザイクの供給が不変であるため、検証に失敗しました。

* **FAILURE_MOSAIC_MAX_SUPPLY_EXCEEDED**
モザイク全体の最大供給量を超えているため、検証に失敗しました。

* **FAILURE_MOSAIC_NOT_TRANSFERABLE**
モザイクが転送できないため、検証に失敗しました。

* **FAILURE_MOSAIC_DIVISIBILITY_VIOLATED**
モザイクの分割可能性に違反しているため、検証に失敗しました。

* **FAILURE_CONFLICTING_MOSAIC_CREATION**
競合するモザイク作成が存在するため、検証に失敗しました。

* **FAILURE_MOSAIC_INVALID_CREATION_FEE_SINK**
モザイククリエーションシンクが無効であるため、検証に失敗しました。

* **FAILURE_MOSAIC_INVALID_CREATION_FEE**
指定された作成料金が無効であるため、検証に失敗しました。
  

* **FAILURE_TOO_MANY_MOSAIC_TRANSFERS**
転送トランザクションに添付されたモザイク転送が多すぎるため、検証に失敗しました。

タイトル：New Economy Movement(NEM) APIマニュアル和訳

### New Economy Movement(NEM) APIマニュアル和訳

https://www.pr1sm.com/crypto-coin/nem-nis-api-documentation-in-japanese/

NEM公式APIマニュアルの日本語訳。
