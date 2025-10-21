# SSH Hosts Configuration (Submodule)

このディレクトリはサブモジュールとして管理される予定のディレクトリです。

## 構造例

各ホストごとに個別のファイルを作成することを推奨します：

```
hosts/
├── work-server
├── personal-server
├── cloud-instances
└── README.md
```

## ファイル例

### hosts/work-server
```
Host work
    HostName work.example.com
    User username
    Port 22
    IdentityFile ~/.ssh/keys/id_ed25519
    ForwardAgent yes
```

### hosts/personal-server
```
Host home
    HostName home.example.com
    User admin
    Port 2222
    IdentityFile ~/.ssh/keys/personal_rsa
```

## 注意事項

- 機密情報（IPアドレス、ユーザー名など）を含むため、このディレクトリは**プライベートリポジトリ**で管理してください
- 各ファイルは `ssh/config` から `Include conf.d/hosts/*` で読み込まれます
