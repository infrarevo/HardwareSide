### ローカルマシン（Windows10）からホストマシン（ESXi）のストレージ（datastore1）へファイルコピー
インターネットからWindows10でDownloadしたファイル（ISO）をESXiホストマシンのdatastore1にコピーする方法

#### １・web管理画面からESXiホスト　→　管理　→　サービス　→　『TSM-SSH』　「停止」を「実行中」へ変更。

#### ２・ローカルマシン上からsshを使用してroot（管理者）でログイン
 　例：  
###### 　C:\users\CurrentUser\Downloads>ssh root@ESXiServerHost  
###### 　Password:  
###### 　★ワーニングが出力  
###### 　[root@ESXiServerHost:~]  

#### ３・datastore1（ストレージ）のディレクトリと残量を確認。
###### 　例：
###### 　[root@ESXiServerHost:~] df -h
######   FileSystem  Size  Used Available Use% Mounted on
###### 　～～～～～～～～～～～～～～～～～～～～～～～～～～～
###### 　VMFS-6    456.2G 378.8G    79.4G 83%  /vmfs/volumes/datasore1
###### 　～～～～～～～～～～～～～～～～～～～～～～～～～～～
###### 　[root@ESXiServerHost:~]

#### ４・ローカルマシン上でもう１つコンソールを用意して、Downloadしたファイル（ISO）をSCPでコピー
###### 　例：
###### 　C:\users\CurrentUser\Downloads>scp rhel-8.3-x86_64-dvd.iso root@ESXiServerHost:/vmfs/volumes/datasore1
###### 　Password:
###### 　rhel-8.3-x86_64-dvd.iso                                 100% 7488MB  10.3MB/s      12:06
###### 　C:\users\CurrentUser\Downloads>

#### ５・データのコピーを確認。
###### 　[root@ESXiServerHost:~] ls -la /vmfs/volumes/datasore1/rhel-8.3-x86_64-dvd.iso
###### 　-rw-r--r--        1 root      root      7851737088 Oct 12 14:37 /vmfs/volumes/datasore1/rhel-8.3-x86_64-dvd.iso
###### 　[root@ESXiServerHost:~]

#### ６・web管理画面からESXiホスト　→　管理　→　サービス　→　『TSM-SSH』　「実行中」を「停止」へ。

#### ※Windows10（1803）以降、OpenSSHが導入されていて、以下のコマンドが使用可能。
###### 　C:\Windows\system32\OpenSSH\scp.exe
###### 　C:\Windows\system32\OpenSSH\sftp.exe
###### 　C:\Windows\system32\OpenSSH\ssh-add.exe
###### 　C:\Windows\system32\OpenSSH\ssh-agent.exe
###### 　C:\Windows\system32\OpenSSH\ssh-keygen.exe
###### 　C:\Windows\system32\OpenSSH\ssh-keyscan.exe
###### 　C:\Windows\system32\OpenSSH\ssh.exe
