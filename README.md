# oracle-presetup-playbook

1. rebootする
   # reboot

2. /tmpにoracleのファイルを配置する。(oracleユーザで読めるように)

3. /home/oracleにファイルを展開する
   $ cd /home/oracle
   $ unzip /tmp/linux.x64_11gR2_database_1of2.zip
   $ unzip /tmp/linux.x64_11gR2_database_2of2.zip

4. RHEL6用の設定を実行する
   $ vi /home/oracle/database/stage/cvu/cv/admin/cvu_config
   ============================================================
   ###CV_ASSUME_DISTID=OEL4 <- ###を追記する
   CV_ASSUME_DISTID=OEL6 <- 追記する
   ============================================================

5. Oracleインストーラーの文字化けパッチを取得する。
   (http://tamasaban.blog.fc2.com/blog-entry-39.html参照)
   $ wget http://sourceforge.jp/frs/redir.php\?m=jaist\&f=%2Fefont%2F10087%2Fsazanami-20040629.tar.bz2
   $ tar xvf sazanami-20040629.tar.bz2
   $ cd /home/oracle/database/stage/Components/oracle.jdk/1.5.0.17.0/1/DataFiles
   $ unzip /home/oracle/database/stage/Components/oracle.jdk/1.5.0.17.0/1/DataFiles/all.jar
   $ cd /home/oracle/database/stage/Components/oracle.jdk/1.5.0.17.0/1/DataFiles/jdk/jre/lib/fonts/
   $ mkdir fallback
   $ cp /home/oracle/sazanami-20040629/sazanami-* ./fallback/
   $ cd /home/oracle/database/stage/Components/oracle.jdk/1.5.0.17.0/1/DataFiles
   $ mv all.jar all.jar_old
   $ chown -R oracle:oinstall ./jdk
   $ zip -r all.jar ./jdk

6. X Window環境で下記項番以降の作業を実施する
   ORACLE_HOME環境変数を初期化する。
   $ unset ORACLE_HOME
