# AWS CDK 初期化チュートリアル

このページでは、`pnpm dlx aws-cdk init app --language typescript` を使って AWS CDK アプリを TypeScript で初期化する手順を説明します。

## 前提条件

- Node.js がインストールされている
- pnpm がインストールされている
- AWS CLI の認証・設定が済んでいる（必要に応じて）

## 手順

1. AWS 用の作業ディレクトリに移動する

```bash
cd docs/aws
```

2. CDK アプリを TypeScript で初期化する

```bash
pnpm dlx aws-cdk init app --language typescript
```

3. 初期化後の確認

- `package.json` が生成されている
- `cdk.json` が生成されている
- `lib/` と `bin/` フォルダーが生成されている

4. 依存関係をインストールする

```bash
pnpm install
```

5. CDK アプリのビルドと確認

```bash
pnpm run build
pnpm run cdk ls
```

## 追加メモ

- `pnpm dlx` は一時的にパッケージを実行するため、ローカルに CDK をインストールせずに実行できます。
- プロジェクトとして継続して開発する場合は、`pnpm install aws-cdk-lib constructs` などの依存関係を追加することを検討してください。
