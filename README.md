# rails_practice
Ruby on Rails 練習用

## 実行手順
0. フォルダ指定 *【Git Bash Here】*  

1. プル：  
  ```
  git clone https://github.com/k-matsuo-cmj/rails_practice.git
  ```  
  
2. Dockerコンテナ作成：  
  ```
  cd rails_practice  
  docker-compose build
  ```  
  
3. アプリケーション作成：  
  ```
  docker-compose run web rails new . --force --database=mysql --skip-bundle
  ```  
    
4. ファイル修正：  
  /config/database.yml(L.16-18)  
  ```
# 修正前
  username: root
  password:
  host: localhost
# 修正後
  username: <%= ENV.fetch("USER") %>
  password: <%= ENV.fetch("PASSWORD") %>
  host: db
  ```  
  
5. 再ビルド：  
  ```
  docker-compose build
  ```  

6. MySQL設定：  
  rails_practice_db_1 CLI
  ```
  mysql -u root -p  
  password  
  ALTER USER root IDENTIFIED WITH mysql_native_password BY 'password';  
  SELECT user, host, plugin FROM mysql.user;  
  exit;  
  ```

7. DB作成：
  ```
  docker-compose run web rails db:create
  ```  
  
8. コンテナ起動：
  ```
  docker-compose up
  ```  
  
9. ブラウザ起動：  
  http://localhost:3000/
