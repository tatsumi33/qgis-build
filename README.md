# QGIS / GDAL / PROJ 作業用コンテナ

QGIS / GDAL / PROJ その他いくつかの GIS 関連プロダクトをビルドして、QGIS の動作確認するためのコンテナです。

開発などに利用するためのものなので、普通に利用するだけであれば公式リリースを利用してください。

- [QGIS](https://qgis.org/)
- [GDAL](https://gdal.org/)
- [PROJ](https://proj.org/)

## ビルド方法

```sh
$ docker build -t qgis-build .
```

[Dockerfile](Dockerfile) を確認し、何をしているか把握してから実行することをお勧めします。
やりたいことに合わせて変更してください。

i7-10510U、メモリ 16 GB で 1 時間半以上かかります。
Docker ARG の PARALLEL を make 実行時の並列実行オプション `-j` に渡していますので、環境に合わせて調整してください。（例： `--build-arg=PARALLEL=4`）


## 実行方法

コンテナーから QGIS を直接実行するには次のようにします。

```sh
$ xhost local:                   
$ docker run -it --rm --privileged \
    -e DISPLAY=${DISPLAY} \
    -e LD_LIBRARY_PATH=/usr/local/lib \
    -v "/tmp/.X11-unix:/tmp/.X11-unix:rw" \
    -v "$HOME/<gis-data-folder>:/root/data:ro" \
    qgis-build bash
> qgis
```
