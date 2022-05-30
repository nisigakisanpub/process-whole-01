
# 大項目）開発プロセスの進め方＋django 採用のリスク

Gistへのリンク（Django React session CSRF axios）
https://gist.github.com/nisigakisanpub/33bcd08f5d9b4cef613f916a303eacf8


## A. React＋Django の評価
-  React 導入したら Django フレームワークする旨味が減る＝「正解」の立場から
    -  React にルーティングさせたら Django のルーティング機能が無駄になる
    -  React も Django も Validation やることになるが折り合いがわからない
    -  React は、webpack が難しい
    -  React は、create-react-app をブラックボックスで使い続ける勇気がいる
        - いつの間にか node_modules にいっぱい入ってる 
    -  React やめるとしたら Stimulus.js がよく見える
        - Bootstrap との相性が心配
    - Django 側にはログがあるけど、React 側で情報取るのは無理だろう。
        - 「性能向上のためのレポート」にOKしてもらえたとしてもやりたくないだろう。
    - React が表示している画面と同じレイアウトで Django 側でPDF作るのは無理だろう
    
-  React 導入したら Django フレームワークする旨味が減る＝「不正解」の立場から
    -  frontend と backend で担当が明確に分けられる
    -  frontend と backend でデプロイが別々の作業できる
    -  SPA のデプロイは簡単

　
## B. Django vs Rails 
- Rails にはあるけど Django には無いものを解決するのが役立つ の立場から
    - 調べてみたことをサンプルコードの形で記録しよう
        - 調べてみた印象としては Django にもその機能がある
- トランザクション https://github.com/nisigakisanpub/process-whole-01/issues/2
- 単一テーブル継承(STI) https://github.com/nisigakisanpub/process-whole-01/issues/4
- 楽観ロック https://github.com/nisigakisanpub/process-whole-01/issues/3
    - React 側にも責務がある
- validation 後のエラー表示 https://github.com/nisigakisanpub/process-whole-01/issues/5
    - model.errors はあるのか？
    - React 側は何を受け取るのだろう？
- Asset Pipeline 的な Javascript 管理機能 https://github.com/nisigakisanpub/process-whole-01/issues/6
    - React 前提ならこの件はなし
- Ajax
    - React 前提ならこの件はなし
- テスト
    - React 側には Jest＋ Django 側には、django.test.TestCase
    - これらが全部OKでもリリースできる自信がない
    - React 側＋Django 側 全ロジックを通るテストは、Cypress でやるのか？
        - 両側の仕様を知ってないとテストケース書けないだろう
        - Cypress のコード自体はReact Javascruptだから、この知識も必要
        - テストケース実施前にDBレコード用意して実施後に消す、ってどうやるの？  
          テスト専用バックエンドが必要ということ？

- Credentials
    - Rails の config/credentials/ や、rails credentials:edit は、Django では？
    - Django DRF では settings.py SECRET_KEY が自動生成されて、GitHub に push すると警告される

- ログ
    - Rails で言うところの log/production.log は、Django では ？
        - Python logging を settings.py の LOGGING で設定して使う
- ルーティング
    - Rails の before_action は Django では？
    - クライアント側で許可しているルーティング以外は "/" にリダイレクトしたい。  
      他の方法はあるかな？
- i18n 多言語対応
    - むしろ React側？

　
## H. 選択とその根拠
- React の UI ライブラリ
    - React-Bootstrap が一番人気ではないらしい

- React の チャート ライブラリ
    - HIGHCHARTS すごそう

- デプロイ先のPaas
    - Heroku が始めやすい

- ログ運用 or リリース後のモニタリング には、どんなサービスをどんな設定で使うのだろう？
    - (セキュリティ) Django DRF 側に、来るはずのないリクエストが来たことを検知したい。
    - (性能) ユーザーに「なんか遅い」って言われたときに調査したい
        - いわれる前に、ログ Watch サービスにアラート上げてほしい
    - メトリクスは Heroku 等、各サービスがデフォルトで持ってるだろうし、それは興味ないだろう

　
## J. React の難しさ
- v18 になった
```
React v18.0
March 29, 2022 by The React Team
https://reactjs.org/blog/2022/03/29/react-v18.html
```

- こんなエラーが出た
```
npm install --save firebase
====
npm ERR! code ERESOLVE
npm ERR! ERESOLVE could not resolve
npm ERR!
npm ERR! While resolving: @mui/styles@5.8.0
npm ERR! Found: react@18.1.0
npm ERR! node_modules/react
npm ERR!   peer react@">=16.8.0" from @emotion/react@11.9.0
npm ERR!   node_modules/@emotion/react
npm ERR!     peer @emotion/react@"^11.0.0-rc.0" from @emotion/styled@11.8.1
npm ERR!     node_modules/@emotion/styled
npm ERR!       peerOptional @emotion/styled@"^11.3.0" from @mui/material@5.8.0
npm ERR!       node_modules/@mui/material
npm ERR!         peer @mui/material@"^5.0.0" from @mui/icons-material@5.8.0
npm ERR!         node_modules/@mui/icons-material
npm ERR!         1 more (the root project)
npm ERR!       3 more (@mui/styled-engine, @mui/system, the root project)
npm ERR!     peerOptional @emotion/react@"^11.5.0" from @mui/material@5.8.0
npm ERR!     node_modules/@mui/material
npm ERR!       peer @mui/material@"^5.0.0" from @mui/icons-material@5.8.0
npm ERR!       node_modules/@mui/icons-material
npm ERR!         @mui/icons-material@"^5.8.0" from the root project
npm ERR!       1 more (the root project)
npm ERR!     3 more (@mui/styled-engine, @mui/system, the root project)
npm ERR!   peer react@">=16.8.0" from @emotion/styled@11.8.1
npm ERR!   node_modules/@emotion/styled
npm ERR!     peerOptional @emotion/styled@"^11.3.0" from @mui/material@5.8.0
npm ERR!     node_modules/@mui/material
npm ERR!       peer @mui/material@"^5.0.0" from @mui/icons-material@5.8.0
npm ERR!       node_modules/@mui/icons-material
npm ERR!         @mui/icons-material@"^5.8.0" from the root project
npm ERR!       1 more (the root project)
npm ERR!     peerOptional @emotion/styled@"^11.3.0" from @mui/styled-engine@5.8.0
npm ERR!     node_modules/@mui/styled-engine
npm ERR!       @mui/styled-engine@"^5.8.0" from @mui/system@5.8.0
npm ERR!       node_modules/@mui/system
npm ERR!         @mui/system@"^5.8.0" from @mui/material@5.8.0
npm ERR!         node_modules/@mui/material
npm ERR!     2 more (@mui/system, the root project)
npm ERR!   14 more (@mui/base, @mui/icons-material, @mui/material, ...)
npm ERR!
npm ERR! Could not resolve dependency:
npm ERR! peer react@"^17.0.0" from @mui/styles@5.8.0
npm ERR! node_modules/@mui/styles
npm ERR!   @mui/styles@"^5.8.0" from the root project
npm ERR!
npm ERR! Conflicting peer dependency: react@17.0.2
npm ERR! node_modules/react
npm ERR!   peer react@"^17.0.0" from @mui/styles@5.8.0
npm ERR!   node_modules/@mui/styles
npm ERR!     @mui/styles@"^5.8.0" from the root project
npm ERR!
npm ERR! Fix the upstream dependency conflict, or retry
npm ERR! this command with --force, or --legacy-peer-deps
npm ERR! to accept an incorrect (and potentially broken) dependency resolution.
npm ERR!
npm ERR! See /home/nisigaki/.npm/eresolve-report.txt for a full report.

npm ERR! A complete log of this run can be found in:
npm ERR!     /home/nisigaki/.npm/_logs/2022-05-21T11_44_53_746Z-debug-0.log
```

- ワークアラウンドはあるので動かすことはできるが、リリースする自信がない。
- リリース用の安定バージョンで開発、リリース後新バージョン対応、この作業のスケジュールが必要だろう

　
## G. React＋Django REST Framework
- この構成なら何が難しそうか、と考えた方が良いのか？

　
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

