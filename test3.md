
# LAMP（Linux＋Apach＋MySQL＋PHP）の構築

## 【1】EC2インスタンス作成と基本設定

- **Amazon Linux 2023**でEC2インスタンスを新規起動
- **rootユーザー**に切り替え
  ```
  sudo -i
  ```
- **パッケージを最新化**
  ```
  sudo dnf update -y
  ```

## 【2】ApacheとPHPのインストールと設定

- **ApacheとPHPをインストール**
  ```
  sudo dnf install -y httpd wget php-fpm php-mysqli php-json php php-devel
  ```

- **バージョン確認**
  ```
  httpd -v
  php -v
  ```

- **Apacheを起動・ステータス確認**
  ```
  sudo systemctl start httpd
  sudo systemctl status httpd
  ```

- **Apache自動起動設定**
  ```
  sudo systemctl enable httpd
  ```

- **セキュリティグループでHTTP（ポート80）許可**
- **パブリックIPにアクセスしてApache起動確認**
<img width="1084" alt="Image" src="https://github.com/user-attachments/assets/e5911b16-a114-44f5-ad01-22c1bf227416" />

## 【3】ドキュメントルートのアクセス権限設定

- **Apacheドキュメントルート `/var/www` に権限を付与**
  ```
  sudo chmod 2775 /var/www && find /var/www -type d -exec sudo chmod 2775 {} \;
  ```
  > ※ 学習環境ではrootユーザーで操作しているが、通常ユーザーの場合は所有権変更も必要

- **HTMLファイルを作成して表示確認**
  ```
  touch /var/www/html/index.html
  ```
  ```
  vi /var/www/html/index.html
  ```
  内容に「Hello Linux!」と記述し保存。
<img width="1081" alt="Image" src="https://github.com/user-attachments/assets/ee03fa0f-e60c-4dc3-9e6b-5d0942427d2d" />

## 【4】PHP動作確認（phpinfoページ作成）

- **phpinfo()を表示させるファイルを作成**
  ```
  echo "<?php phpinfo(); ?>" > /var/www/html/phpinfo.php
  ```

- **ブラウザでアクセス**
  ```
  http://<パブリックIP>/phpinfo.php
  ```

- **注意**  
  公開されたままだと危険なため、確認後**削除**
  ```
  rm /var/www/html/phpinfo.php
  ```

## 【5】PHPでHello Worldページ作成

- **PHPファイルを作成**
  ```
  echo "<?php echo 'Hello World'; ?>" > /var/www/html/index.php
  ```

- **確認**
  ```
  cat /var/www/html/index.php
  ```

- **ブラウザでアクセス**
  ```
  http://<パブリックIP>/index.php
  ```
<img width="1082" alt="Image" src="https://github.com/user-attachments/assets/aa6e07d5-42ea-4853-a7e3-8dacc46789f9" />
### 【ここでの疑問点について】

- 最初の`index.html`は**HTML**、次の`index.php`は**PHPプログラム**。
- **ブラウザは通常「index.html」を優先して表示**するため、index.phpを表示したいならindex.htmlは消すか、明示的にindex.phpへアクセスする。
- `vi`で編集する方法でも良いが、学習では**echoコマンドで直接作成する方法**も紹介されているだけ。

## 【6】MariaDBのインストールと初期設定

- **MariaDBをインストール**
  ```
  sudo dnf install mariadb105-server -y
  ```

- **MariaDB起動・確認・停止**
  ```bash
  sudo systemctl start mariadb
  sudo systemctl status mariadb
  sudo systemctl stop mariadb
  ```

- **初期セキュリティ設定（パスワード設定など）**
  ```
  sudo mysql_secure_installation
  ```

- **起動時自動起動設定**
  ```
  sudo systemctl enable mariadb
  ```

## 【7】phpMyAdminのインストールとセットアップ

- **必要なPHPモジュールをインストール**
  ```
  sudo dnf install php-mbstring php-xml -y
  ```

- **Apacheとphp-fpmを再起動**
  ```
  sudo systemctl restart httpd
  sudo systemctl restart php-fpm
  ```

- **Apacheドキュメントルートへ移動**
  ```bash
  cd /var/www/html
  ```

- **phpMyAdminをダウンロード**
  ```
  wget https://www.phpmyadmin.net/downloads/phpMyAdmin-latest-all-languages.tar.gz
  ```

- **確認**
  ```
  ls
  ```

- **phpMyAdmin用のディレクトリ作成＆展開**
  ```
  mkdir phpMyAdmin
  tar -xvzf phpMyAdmin-latest-all-languages.tar.gz -C phpMyAdmin --strip-components 1
  ```

  > **ここ解説**  
  > - `mkdir phpMyAdmin`：ディレクトリを作る  
  > - `tar -xvzf ...`：ダウンロードした圧縮ファイルを展開して、phpMyAdminディレクトリの中に入れる  
  > - `--strip-components 1`：一番上のディレクトリを取り除いて中身だけを展開するオプション（=きれいに入る）

- **不要になったtar.gzファイル削除**
  ```
  rm phpMyAdmin-latest-all-languages.tar.gz
  ```

- **ディレクトリ確認**
  ```
  ls phpMyAdmin/
  ```

## 【8】phpMyAdminへのアクセス確認

- **ブラウザでアクセス**
  ```
  http://<パブリックIP>/phpMyAdmin/
  ```

- **ログイン画面が表示されることを確認**
<img width="1434" alt="Image" src="https://github.com/user-attachments/assets/55bf6540-c5a4-4b52-9146-b97c38a7197e" />

# 最後にまとめポイント！

| 項目 | 内容 |
|:---|:---|
| Webサーバー構築 | Apache, PHPインストールと起動 |
| アクセス権設定 | `/var/www`に権限設定してファイル編集 |
| PHP動作確認 | `phpinfo()`と`Hello World`ページ作成 |
| DBサーバー構築 | MariaDBインストールと初期設定 |
| 管理ツール導入 | phpMyAdminをセットアップしてブラウザ管理 |
