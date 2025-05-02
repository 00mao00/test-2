# LinuxサーバーにアプリケーションをインストールしLinux操作に慣れる

## 1. パッケージのインストール
- **PHPとMySQLの連携用パッケージをインストール**  
  ```bash
  sudo dnf install php-mysqlnd -y
  ```

## 2. Elastic IPアドレスを設定・管理
- **Elastic IPを割り当てる理由**  
  - インスタンス停止・起動でパブリックIPが変わる問題を防ぐ
  - WordPress設定への影響を防止
- **注意点**  
  - Elastic IPアドレスを使わず保持していると料金が発生
- **Elastic IPアドレスを解放する手順**  
  1. 関連付けを解除  
  2. Elastic IPアドレスの解放（課金停止）

## 3. WordPress用のMySQLデータベースとユーザーの作成
1. **サーバー起動確認**
   ```bash
   sudo systemctl status mariadb
   sudo systemctl status httpd
   ```
2. **MySQLにrootでログイン**
   ```bash
   sudo mysql -u root -p
   ```
3. **ユーザー作成・パスワード設定**
   ```sql
   CREATE USER '任意のUser名'@'localhost' IDENTIFIED BY '任意のパスワード';
   ```
4. **データベース作成**
   ```sql
   CREATE DATABASE `wp-db`;
   ```
5. **ユーザーに権限付与**
   ```sql
   GRANT ALL PRIVILEGES ON `データベース名`.* TO 'ユーザー名'@'localhost';
   FLUSH PRIVILEGES;
   ```
6. **MySQLを終了**
   ```sql
   exit
   ```

## 4. WordPressのダウンロードとインストール
1. **WordPressパッケージをダウンロード・解凍**
   ```bash
   wget https://ja.wordpress.org/latest-ja.tar.gz
   tar -xzf latest-ja.tar.gz
   ls wordpress/
   ```

## 5. WordPress設定ファイル（wp-config.php）を編集
1. **サンプル設定ファイルを確認・コピー・編集**
   ```bash
   less wordpress/wp-config-sample.php
   cp wordpress/wp-config-sample.php wordpress/wp-config.php
   vi wordpress/wp-config.php
   ```
2. **設定内容**
   - データベース名、ユーザー名、パスワードの修正
   - 認証用ユニークキーも取得して設定

## 6. ドキュメントルートにWordPressを配置
1. **ディレクトリ作成・WordPressファイル配置**
   ```bash
   mkdir /var/www/html/blog
   cp -r wordpress/* /var/www/html/blog/
   ls /var/www/html/blog/
   ```
2. **Apache設定ファイルの編集**
   ```bash
   sudo vi /etc/httpd/conf/httpd.conf
   ```
   - `<Directory "/var/www/html">` の `AllowOverride None` → `AllowOverride All` に変更
3. **必要パッケージ追加インストール**
   ```bash
   sudo dnf install php-gd -y
   ```
4. **ディレクトリの権限確認**
   ```bash
   ls -l /var/www
   ```

## 7. ブラウザからWordPressサイトにアクセス
1. **アクセス方法**
   - EC2のパブリックIPアドレス＋`/blog`
2. **初期設定画面**
   - サイトタイトル、ユーザー名、パスワード、メールアドレスを設定
   - インデックス設定は**公開まで無効化推奨**
3. **ログイン確認**
   - ログインできることをチェック
