
# 大項目）開発プロセスの進め方＋django採用のリスク

## A. React＋Django の評価
-  React 導入したら Django フレームワークする旨味が減る＝「正解」の立場から
    -  React にルーティングさせたら Django のルーティング機能が無駄になる
    -  webpacker が難しい
    -  Stimulus.js がよく見える
        - Bootstrap との相性が心配

-  React 導入したら Django フレームワークする旨味が減る＝「不正解」の立場から
    -  frontend と backend で担当が明確に分けられる
    -  frontend と backend でデプロイが別々の作業できる
    -  SPA のデプロイは簡単


## B. Django vs Rails
- Rails にはあるけど Django には無いものを解決するのが役立つ の立場から
    - 調べてみたことをサンプルコードの形で記録しよう
        - 調べてみた印象としては Django にもその機能がある
- トランザクション
- 楽観ロック
- 単一テーブル継承(STI)
- validation 後のエラー表示
    - model.errors はあるのか？
- Asset Pipeline 的な Javascript 管理機能


## C. 重い処理を非同期で行う
- クライアント側（WEB）から機械学習推論を依頼してそのステータスも見たいという要件に備える
    - AWS Lambda だとステータスが見れない

## D. 開発環境の作り方
- WSL上のUbuntuを現状の正解としよう
   - WSL上のUbuntu上のDockerでやってたけどブラウザからアクセスできないしそもそもナンセンス
   - DockerDesktop＋Windowsターミナルが次点の選択肢
   - WSL上のUbuntuは入れ替えたり複数立てたりできる
- Python のバージョン管理は Pyenv で正解としよう


## E. GitHub Organization
-  チーム開発には GitHub Organization で正解としよう
-  導入手順

## F. GitHub Issue テンプレート
-  型なしでは進めにくい で正解としよう
-  導入手順


# 中項目）Rails にはあるけど Django には無いもの




