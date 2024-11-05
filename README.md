# 吉里吉里Z 統合リポジトリ 開発用

本体のソースコード、プラグインのソースコード、各種TJS2スクリプト、ドキュメント等開発関係のもの全てが入ったリポジトリ。
各種ファイルはサブモジュールで参照されている。

CMake 構築用作業中

## 前準備

vcpkg を導入して外部ライブラリ参照を準備します
※Visual Studio 2022 の最新版では標準でインストール済みです。

https://github.com/microsoft/vcpkg
https://learn.microsoft.com/vcpkg/get_started/get-started

cmake を導入します。
※Visual studio 2019 以降では標準でインストール済みになります。

cygwin や msys2 などを導入して make が利用可能な場合は、定義済み Makefile が利用できます

## 作業手順

1. git clone
2. git submodule update --init --recursive

これでサブモジュール部分が展開されるので、全体の構成で作業できます。

## ビルド手順

cmake による構築になります。

環境別定義は、CMakePresets.json にあらかじめ定義されているので、
それを利用してビルドできます。

- 標準は Ninja の MultiConfig での定義での構築定義になっています
- preset 毎にビルドフォルダが別れるようになってます (build/プリセット名)

Visual Studio のコマンドラインで以下でビルドできます

```
# ビルドの準備
cmake --preset=x64-windows

# ビルド
cmake --build --preset=x64-windows

# ビルドタイプ指定してビルド
cmake --build --preset=x64-windows --config Debug

# インストール処理
# 未設定
```

ビルド作業用の Makefile が準備されています

    環境変数
    PRESET          cmakeのプリセット名を指定
    BUILD_TYPE      ビルド対象の config 指定 Debug/RelWithDebInfo/Release

    ビルドルール
    prebuild        cmake の構築呼び出し
    build           cmake のビルド呼び出し
    install         cmake のインストール呼び出し


win32版

```
make prebuild
make
```

win64版

```
export PRESET=x64-windows
make prebuild
make
```