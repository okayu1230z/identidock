# identidock

## まずは、Dockerが動くかHello World!

```
$ docker run --rm -it xaviervia/pokemonsay 'Hello World!'
```

## 立ち上げる

```
$ docker-compose up
```

## アプリケーションの配布

Docker Hub、GitHubによる自動化ビルド&配布が可能であるので、配布するときは試すこと

イメージサイズについて、まずは以下のように作成してみる

```
FROM debian:wheezy

RUN dd if=/dev/zero of=/bigfile count=1 bs=50mMB
RUN rm /bigfile
```

イメージサイズを確かめる。

```
$ docker build -t filetest .
$ docker images filetest
$ docker history filetest
```

以下のように変える

```
FROM debian:wheezy

RUN dd if=/dev/zero of=/bigfile count=1 bs=50mMB && rm /bigfile
```

すると、ベースイメージが小さくなる。
ファイルを、1つのレイヤの中で作成して削除していればそのファイルはイメージに含まれることはない。

同様の工夫がソースをダウンロードし、コンパイルしてバイナリを作成する場合などに使える。

## マイクロサービスアーキテクチャ

複数の独立した小さなサービス群からシステムを構築すること

全体を単一要素として作り上げるモノリシックな構成と対比をなす

コンポーネントの交換が素早く簡単に行え、システムの他の部分を落とすことなくロールバックできる

複数マシンにスケールアウトも容易

銀の弾丸ではなく、構成要素が分散していることによるオーバーヘッドも考える必要がある

## Dockerを使った継続的インテグレーションとテスト


