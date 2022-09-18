# 第3回課題
## MySQLのセットアップ
* MySQL互換のDBサーバーとMariaDBの削除
1.  `sudo yum remove -y mysql-server`
2.  `sudo yum remove -y mariadb*`
* MySQLのインストール
1. `MYSQL_PACKAGE_URL="https://dev.mysql.com/get/mysql80-community-release-el7-3.noarch.rpm"`
2. `sudo yum localinstall -y $MYSQL_PACKAGE_URL`
3. `sudo yum install -y mysql-community-devel`
4. `sudo yum install -y mysql-community-server`  
**MySQLのGPGキーの有効期限切れのためMysqlがインストールされていないことがある**  
=``sudo rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2022``
* MySQLサーバーの起動＆確認  
`sudo service mysqld start && sudo service mysqld status`  
Activeが「active (running)」であることを確認。
* 初期パスワードの確認  
`sudo cat /var/log/mysqld.log | grep "temporary password" | awk '{print $13}'`
* ログイン確認　パスワード要求が出るので控えたパスワードを入力  
`mysql -u root -p`
* 初期パスワードの変更  
mysql>`ALTER USER 'root'@'localhost' IDENTIFIED BY '********';`  
変更したパスワードを[config/database.yml]へ入力
* sokcetの変更  
[config/database.yml]のsocketを/var/lib/mysql/mysql.sockへ変更
* bundleのインストール  
`bundle install`
* データベースの作成|連結  
`bundle exec rails db:create`  
`bundle exec rails db:migrate`  
## サンプルアプリケーションの起動
* リポジトリからコードをclone  
`git clone https://github.com/yuta-ushijima/raisetech-live8-sample-app.git`
* Rubyのインストール  
**[アプリケーションによってはバージョンを合わせないといけないので注意]**
* bundleのインストール  
`gem install bundler:2.2.3`←バージョンに関してはgemfail.lockを確認  
`bundle install`
* アプリケーションの起動  
`rails s`
* エラー画面[Bloked host:.....]  
下記の（config.hosts<<.....)をconfig/development.rbへペースト。アプリケーション再起動
* エラー画面  
![エラー画面](https://i.imgur.com/uthj1DZ.jpeg) 
 
 webpackerのインストールが必要だが、nodeのバージョンエラーでインストールできないことがある  
 1. nodeのバージョン変更 `nvm install v(インストールしたいバージョン)`  
 2. `nvm use (使用したいバージョン)`  
 3. `npm install -g yarn`  
 4. `bundle exec rails webpacker:install`  
 5. `rails s`   
## サンプルアプリケーション起動完了
![サンプルアプリケーション](https://i.imgur.com/HTvAqxQ.jpeg)
