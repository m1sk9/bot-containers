# bot-containers

[![Deploy](https://github.com/m1sk9/bot-containers/actions/workflows/deploy.yaml/badge.svg)](https://github.com/m1sk9/bot-containers/actions/workflows/deploy.yaml)

The repository that manages the Compose files for the Discord Bot running on my server.

![Overview](./bot-containers.drawio.svg)

- ユーザーはこのリポジトリ内の Docker Compose ファイルを編集したり, 追加したりすることができます.
- Docker Compose ファイルが編集されると GitHub Actions が Ubuntu で構築されたサーバー `dev-m1sk9-s1` へのデプロイを行います.
- `dev-m1sk9-s1` への接続には **直接SSHはせず**, Tailscale (Tailnet) 経由での接続を行います.
  - `dev-m1sk9-s1` は自宅のネットワークに閉じ込めてあるため, 外部からの SSH はできません. 手持ちのデバイスからの SSH は事前に `@m1sk9` の Tailnet に端末を登録しておく必要があります.
  - また `@m1sk9` の Tailnet では現状 `m1sk9@github` のアカウントのみ SSH が可能です. それ以外のアカウントは全端末へのアクセスが出来ません.
- GitHub Actions は公式の Actions である [`tailscale/github-action`](https://github.com/tailscale/github-action) を使用します. 直接 Tailscale の CLI を使用することはありません.
- トークンなどの機密情報は直接サーバーに保存しています. GitHub へ環境変数として配置するよりも前述の通り Tailscale で保護しているコンピューターに保存することでセキュリティを向上させています.
