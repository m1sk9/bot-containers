# bot-containers

The repository that manages the Compose files for the Discord Bot running on my server.

![Overview](./bot-containers.drawio.svg)

- ユーザーはこのリポジトリ内の Docker Compose ファイルを編集したり, 追加したりすることができます.
- Docker Compose ファイルが編集されると GitHub Actions が Ubuntu で構築されたサーバー `dev-m1sk9-ubuntu-001` へのデプロイを行います.
- `dev-m1sk9-ubuntu-001` への接続には **直接SSHはせず**, Tailscale (Tailnet) 経由での接続を行います.
  - `dev-m1sk9-ubuntu-001` は自宅のネットワークに閉じ込めてあるため, 外部からの SSH はできません. 手持ちのデバイスからの SSH は事前に `@m1sk9` の Tailnet に端末を登録しておく必要があります.
- GitHub Actions は公式の Actions である [`tailscale/github-action`](https://github.com/tailscale/github-action) を使用します. 直接 Tailscale の CLI を使用することはありません.
- トークンなどの機密情報について:
  - Discord API へのログインなどに使用するトークン等は GitHub の Secrets に保存し, GitHub Actions でのデプロイ時に環境変数として渡します.
  - リポジトリでは扱いません.
