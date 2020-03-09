    # イメージの指定
FROM node:10.14.1-alpine

# ワークディレクトリ設定
WORKDIR /app

# コマンド実行
# apk -> Alpine Linuxのパッケージマネージャ
RUN apk update && \
    apk add git && \
    npm install -g npm && \
    npm install -g vue-cli \
    npm install -g create-nuxt-app

ENV HOST 0.0.0.0
EXPOSE 8080