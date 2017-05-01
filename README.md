# CentOS 7とdockerをセットアップする手順

    [Server B] -- ssh --> [Server A] -- 8080 --> internet  
    
   プロキシを利用できるServerAがあり、ServerBからServerAにssh接続できる環境(*)で、  
   ServerAを踏み台にしてServerBにCentOS7とdockerをインストールする手順


====
＃ ServerBのCentOS7の設定  
1. IPの設定などを普通に  
　　　　`nmtui`
 
2. ssh踏み台プロキシの起動  
    `ssh -g -L8080:proxy.example.local:8080 userA@ServerA`  
    `export http_proxy=http://localhost:8080`  
    `export https_proxy=$http_proxy`

3. パッケージインストール  
    `yum update`  
    `yum install nc`  
    `yum install screen`  
    `yum install docker`

4. docker起動  
    `systemctl enable docker`  
    `systemctl start docker`  
    `systemctl status docker`

5. docker用のfirewalld設定(docker0 -> local:8080を通す)  
    `firewall-cmd --list-all-zones`  
    `firewall-cmd --permanent --new-zone=docker`  
    `firewall-cmd --permanent --zone=docker --add-source=172.17.0.0/16`  
    `firewall-cmd --permanent --zone=docker --add-port=8080/tcp`
    

