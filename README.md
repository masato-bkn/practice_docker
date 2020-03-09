## dockerコマンド
■ Dockerビルド
> Dockerイメージを作成するコマンド

■ コンテナの生成/起動
> docker run イメージ名

■ イメージ一覧
> docker images

■ イメージ詳細
> docker inspect イメージ名

■ イメージのプル
> docker pull イメージ名

■ イメージの作成    
> docker build [オプション] -t イメージ名 コンテキストエリア
* ビルドコンテキストに置いてあるファイルは全てdockeデーモンに送信される。
* 実行されるファイルはデフォルトで`Dockerfile`と言う名前のファイル。
* build時にキャッシュが使用されるので、実行のたびに異なる結果となるコマンドの場合は注意。apt-get -y update とか
* --no-cache で キャッシュを使わないでビルド

■ イメージ削除
> docker rmi -f イメージ名

■ docker hubにログイン
> docker login 

■ ローカルリポジトリにイメージ追加
> docker tag イメージ名 Docker ID/イメージ名:タグ名
✴︎ タグ付けは省略可能。省略した場合はlatestタグになる

■ docker hubにイメージをプッシュ
> docker push Docker ID/イメージ名:タグ名

■ コンテナ立ち上げ(nginx)
> docker run --name コンテナ名 -d -p ホスト側のポート:コンテナ側のポート イメージ名

|  オプション |  役割  |
| ---- | ---- |
|  --name  |  起動するコンテナに名前をつける、エイリアス  |
|  -d  |  バックグラウンドでコンテナを動かす  | 
|  -p ホスト側ポート:コンテナ側ポート  |  外部に公開するポート番号を指定  | 
|  -v ホスト側ディレクトリ:コンテナ側マウントポイント:オプション |  静的htmlのマウント  | 
|  --rm  |  コンテナ停止時にコンテナを削除  |


■ コンテナ停止
> docker stop コンテナ名

■ コンテナ削除
> docker rm コンテナ名

■ ファイルのコピー
> docker cp ホスト上のパス コンテナ名:コピー先のパス
*コンテナからホスト状にファイルをもっってくる場合は逆

■ コンテナのリスト表示
> docker ps
|  オプション |  役割  |
| ---- | ---- |
|  -a  |  起動していないコンテナも表示  |


■ dockerのライフサイクル
1. created コンテナが作成されてスタートされる前の状態
2. running コンテナがスタートした状態
3. pause   コンテナが一時停止した状態
4. restarting コンテナ再起動中の状態
5. exited コンテナが終了した状態
6. removing コンテナ削除中
7. dead 正常に終了できなかったコンテナ


■ コンテナ作成
> docker create --name コンテナ名 

■ コンテナ実行
> docker start コンテナ名 

■　コンテナ一時停止
> docker pause  コンテナ名

■　コンテナ一時停止解除
> docker unpause  コンテナ名

■ コンテナのシェルに接続
> docker attach コンテナ名

|  オプション |  役割  |
| ---- | ---- |
|  --link  |  エイリアス作成  |

> docker exec -it コンテナ名
* コンテナでシェルを実行している時だけ

■ コンテナからイメージを作成
> docker commit コンテナ名　イメージ名:タグ名
* どのような操作で作成された方不明になる。

■ imageに対する変更履歴
> docker history イメージ名

■ Automated Build(自動ビルド)
> ビルドコンテキストにあるファイルに変更があった場合に自動でビルドを行う

■ Dockerマシーン
> Docker Engineを搭載した仮想マシンの管理(作成、起動、停止、再起動など)をコマンドラインから実行できるツール

■ Dockerマシーンの一覧
> docker-machine ls

■ Dockerマシーン作成
> docker-machine create --driver ドライバ名 ホスト名

■ AWS上にDcokerマシーン(EC2)を作成する
> docker-machine create --driver amazonec2 --amazonec2-open-port ポート番号 --amazonec2-region リージョン ホスト名

■ 操作対象Dockerマシーンの設定
> docker-machine env deafult
-> eval "$(docker-machine env default)"

■　ActiveなDockerマシーンの解除
> docker-machine env -u
-> eval $(docker-machine env -u)

■ ip確認
> docker-machine ip default

■ Dockerマシーン 開始
> docker-machine start ホスト名

■ Dockerマシーン 停止
> docker-machine stop ホスト名

■ Dockerのネットワーク
ブリッジドライバー

■ ネットワーク関連コマンド
> docker network ls

■ ネットワーク詳細
> docker network inspect bridge


■ Docker compose
複数のコンテナで構成されるアプリケーションについて、Dockerイメージのビルドや各コンテナの起動・停止などをより簡単に行えるようにするツールです。

よく使われるシチュエーションとしては開発環境やテスト環境の立ち上げに利用される。

■ 実行コマンド
> docker run --name first-nginx -v /Users/XXX/Documents/DEV/docker/practice_docker_run_contena:/usr/share/nginx/html:ro -d -p 8080:80 nginx

> docker cp tmp-nginx:/etc/nginx/conf.d/default.conf ./

> docker run --name connect-test -it -d ubuntu /bin/bash

>  docker run --name reverse-proxy -p 8080:8080 --link static-site:ss -d  reverse-proxy

> docker-machine create --driver virtualbox default

> docker-machine create --driver amazonec2 --amazonec2-open-port 8000 --amazonec2-region ap-northeast-1 aws-sandbox