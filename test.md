# 学習内容

## ■ AWS

### 1. EC2インスタンス作成と接続
- EC2作成時にキーペアをダウンロード（Macではダウンロードフォルダに保存）
- ターミナルでの対応:
  - `.ssh`ディレクトリを作成（存在しない場合）
  - ダウンロードしたキーペア（`.pem`ファイル）を `.ssh` に移動
- 接続時の注意点:
  - `ssh -i ~/.ssh/<キーペア名>.pem ec2-user@<パブリックDNS>`
  - `.ssh`内のキーペアファイルを指定しないと「キーペアが見つからない」エラーが発生する

## ■ viエディタ学習

- `i` : 入力モードへ
- `esc` : コマンドモードへ戻る
- `dd` : 1行削除
- `yy` : 1行コピー
- `p` : コピーした行をペースト
- `o` : 次の行から入力
- `a` : カーソルの次の文字から入力
- `:w` : 編集を保存
- `:q` : 編集せずに終了
- `:wq` : 編集して終了

## ■ シェルスクリプト学習

### 1. 実行手順
```sh
touch /tmp/test.log
echo "aaa" > /tmp/test.log
cat /tmp/test.log
vi /tmp/test.sh  # スクリプトを入力し :wq! で保存
cat -v /tmp/test.sh  # 正常保存を確認
chmod 755 /tmp/test.sh  # 実行権限付与
/tmp/test.sh  # 実行
```

### 2. スクリプト内容 (`/tmp/test.sh`)
```sh
#!/bin/sh

# JOB固有の環境変数を設定する
export EXIT_NORMAL=0
export EXIT_CODE=$EXIT_NORMAL

# test.logの退避
cp -p /tmp/test.log /tmp/test.log.old

# test.logの0byte化
cp /dev/null /tmp/test.log

# test.logへの書き込み
echo "bbb" > /tmp/test.log

exit ${EXIT_CODE}
```

### 3. 実行後の確認内容
- `/tmp/test.log` の中身が `aaa` → `bbb` に変更されていることを `cat` で確認
- `/tmp/test.log.old` が作成されており、中に `aaa` が保存されていることを確認
- `chmod 755 /tmp/test.sh` を実行し、スクリプト実行権限を付与する必要がある
- **権限を与えないと `Permission denied` エラーが発生するため、実行前に必ず確認すること！**
