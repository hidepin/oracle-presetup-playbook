# oracle-presetup-playbook

1. /tmpにoracleのファイルを配置する。(oracleユーザで読めるように)

2. /home/oracleにファイルを展開する
   $ cd /home/oracle
   $ unzip /tmp/linux.x64_11gR2_database_1of2.zip
   $ unzip /tmp/linux.x64_11gR2_database_2of2.zip

3. RHEL6用の設定を実行する
   $ vi /home/oracle/database/stage/cvu/cv/admin/cvu_config
   ============================================================
   ###CV_ASSUME_DISTID=OEL4 <- ###を追記する
   CV_ASSUME_DISTID=OEL6 <- 追記する
   ============================================================

4. Oracleインストーラーの文字化けパッチを取得する。
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

5. 自動インストール
   $ /home/oracle/database/runInstaller -silent -responseFile /home/oracle/db.rsp

------------------------------------------------------------
(コマンド)
・リスナーの起動
  $ lsnrctl start

・リスナーの停止
  $ lsnrctl stop

・リスナーの状態確認
  $ lsnrctl status

・インスタンスの起動手順
  (ORACLE_SIDが設定されていること)
  $ sqlplus / as sysdba
  $ startup

・インスタンスの停止手順
  (ORACLE_SIDが設定されていること)
  $ sqlplus / as sysdba
  $ shutdown

・OEM(Database Control)の起動手順
  $ emctl start dbconsole

・OEM(Database Control)の停止手順
  $ emctl stop dbconsole

・OEM(Database Control)の状態確認
  $ emctl status dbconsole

・??
  $ dbstart/dbstop
    /etc/oratab