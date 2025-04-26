## Linux基礎コマンド

| コマンド | 意味・用途 | 使用例 |
|---------|------------|--------|
| ls | ファイルやフォルダの一覧を表示 | `ls` / `ls -l` |
| cd | ディレクトリの移動 | `cd /home/user` |
| pwd | 現在のディレクトリを表示 | `pwd` |
| mkdir | 新しいフォルダを作成 | `mkdir new_folder` |
| touch | 新しい空のファイルを作成 | `touch file.txt` |
| cp | ファイルやフォルダをコピー | `cp file.txt backup.txt` |
| mv | ファイルやフォルダの移動・名前変更 | `mv old.txt new.txt` |
| rm | ファイルやフォルダを削除 | `rm file.txt` / `rm -r folder` |
| cat | ファイルの中身を表示 | `cat file.txt` |
| nano / vi | ファイルの編集 | `nano file.txt` / `vi file.txt` |
| chmod | ファイルの権限を変更 | `chmod 755 script.sh` |
| chown | 所有者を変更 | `chown user:group file.txt` |
| top | 実行中のプロセスを表示 | `top` |
| ps | 実行中プロセスの確認 | `ps aux` |
| kill | プロセスを終了させる | `kill 1234` |
| df | ディスク使用状況の確認 | `df -h` |
| free | メモリ使用状況を確認 | `free -m` |
| ifconfig / ip a | ネットワークの情報確認 | `ip a` |

| コマンド | 説明 | 使用例 |
|---------|------|--------|
| man | マニュアルを表示 | `man ls` |
| grep | テキストの中から検索 | `grep "error" log.txt` |
| find | ファイルやフォルダを探す | `find / -name "file.txt"` |
| locate | 高速にファイルを探す | `locate file.txt` |
| history | コマンド履歴を見る | `history` |
| !! | 直前のコマンドを再実行 | `!!` |
| sudo | 管理者権限で実行 | `sudo apt update` |
| wget | URLからファイルをダウンロード | `wget https://example.com/file.txt` |
| curl | Web情報取得（APIなど） | `curl https://example.com` |
| tar | アーカイブ操作 | `tar -czvf archive.tar.gz folder/` |
| unzip | zipファイルを解凍 | `unzip file.zip` |
| df -h | ディスク空き容量確認 | `df -h` |
| du -sh | ディレクトリのサイズ確認 | `du -sh /home/user` |
| uptime | サーバの稼働時間表示 | `uptime` |
| whoami | ログインユーザー名表示 | `whoami` |
| uname -a | OS情報表示 | `uname -a` |
| scp | リモート間でファイル送受信 | `scp file.txt user@host:/path/` |
| ssh | リモート接続 | `ssh ec2-user@xx.xx.xx.xx` |
| alias | コマンド短縮を作成 | `alias ll='ls -alF'` |
| reboot / shutdown | 再起動 / 電源オフ | `sudo reboot` / `sudo shutdown now` |

| コマンド | オプション | 意味 | 使用例 |
|---------|----------|------|--------|
| rm | -r | 再帰的に削除 | `rm -r my_folder/` |
| rm | -f | 強制削除 | `rm -rf my_folder/` |
| cp | -r | ディレクトリをコピー | `cp -r folder1 folder2` |
| mkdir | -p | 階層付きで作成 | `mkdir -p /tmp/dir1/dir2` |
| ls | -l | 詳細表示 | `ls -l` |
| ls | -a | 隠しファイルも表示 | `ls -a` |
| ls | -la | 詳細＋隠しファイル | `ls -la` |
| tar | -czvf | 圧縮アーカイブ作成 | `tar -czvf archive.tar.gz folder/` |
| tar | -xzvf | アーカイブ解凍 | `tar -xzvf archive.tar.gz` |
| chmod | -R | 再帰的に権限変更 | `chmod -R 755 my_folder/` |
| scp | -r | ディレクトリ送信 | `scp -r my_folder user@host:/path/` |
| grep | -i | 大文字小文字無視 | `grep -i "error" log.txt` |
| grep | -r | フォルダ内を検索 | `grep -r "ERROR" ./logs` |
