# Dotter Dotfiles Management

このリポジトリは [dotter](https://github.com/SuperCuber/dotter) を使用してdotfilesを管理します。

Windows 11とLinuxの両方に対応しています。

## 構造

```
.
├── .dotter/
│   ├── global.toml    # グローバル設定（全システム共通）
│   └── local.toml     # ローカル設定（システム固有）
├── ssh/
│   └── config         # SSH設定ファイル
├── dotter.exe         # dotterバイナリ（Windows）
├── dotter             # dotterバイナリ（Linux）
└── README.md
```

## セットアップ

### 初回設定

1. サブモジュールを初期化（SSH hostsの取得）:

**Windows:**
```powershell
git submodule update --init --recursive
```

**Linux:**
```bash
git submodule update --init --recursive
```

または、クローン時に:
```bash
git clone --recurse-submodules <dotfiles-repo-url>
```

2. `.dotter/local.toml` を編集して、使用するシステムに合わせてパッケージを設定:

**Windows 11の場合:**
```toml
packages = ["windows"]
```

**Linuxの場合:**
```toml
packages = ["linux"]
```

### デプロイ

**Windows:**
```powershell
.\dotter.exe deploy
```

**Linux:**
```bash
./dotter deploy
```

特定のパッケージのみをデプロイする:
```powershell
# Windows
.\dotter.exe deploy -p ssh

# Linux
./dotter deploy -p ssh
```

### 現在の状態を確認

**Windows:**
```powershell
.\dotter.exe watch
```

**Linux:**
```bash
./dotter watch
```

## パッケージ

### ssh (共通)
SSH設定ファイルを `~/.ssh/config` にデプロイします。
Windows 11とLinuxの両方で使用されます。

### windows
Windows 11固有の設定ファイル用パッケージ。

### linux
Linux固有の設定ファイル用パッケージ。

## 新しいパッケージの追加

1. パッケージ用のディレクトリを作成
2. `.dotter/global.toml` にパッケージ設定を追加
3. 設定ファイルをパッケージディレクトリに配置

### 例: Git設定を追加

1. ディレクトリ作成:
```powershell
mkdir git
```

2. `.dotter/global.toml` に追加:
```toml
[git]
depends = []

[git.files]
"git/.gitconfig" = "~/.gitconfig"
```

3. 設定ファイルを配置:
```powershell
# git/.gitconfig ファイルを作成
```

## SSH Hosts サブモジュールのセットアップ

`ssh/conf.d/hosts` はプライベートなホスト設定を別リポジトリで管理するためのサブモジュールです。

### 初回セットアップ（サブモジュール追加）

1. hosts用のプライベートリポジトリを作成
2. サブモジュールとして追加:

```powershell
# Windows
git submodule add <your-private-repo-url> ssh/conf.d/hosts
git commit -m "Add SSH hosts as submodule"
git push
```

```bash
# Linux
git submodule add <your-private-repo-url> ssh/conf.d/hosts
git commit -m "Add SSH hosts as submodule"
git push
```

### hostsサブモジュールの更新

```powershell
# Windows
cd ssh\conf.d\hosts
git pull origin main
cd ..\..\..
git add ssh\conf.d\hosts
git commit -m "Update SSH hosts submodule"
git push
```

```bash
# Linux
cd ssh/conf.d/hosts
git pull origin main
cd ../../..
git add ssh/conf.d/hosts
git commit -m "Update SSH hosts submodule"
git push
```
