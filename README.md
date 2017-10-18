## MEMO
- コンテナへのログイン  
`$ ./manage login (app または db)`
- コンテナ間のファイル転送  
https://qiita.com/gologo13/items/7e4e404af80377b48fd5


## MountedVolumes
|名称|host|client|
|:--|:--|:--|
|DocumentRoot|app:/var/www/html|/general_enviroment/documentRoot|
|application|app:/var/src/app|/general_enviroment/application|


## TODO
- 参考元記事の記載  
https://qiita.com/yousan/items/f05fa03c1f3951971f2f

- application/へのソースGit clone
- DNSコンテナの活用
- composer, npm, FTP, redis, storageのコンテナ追加
- windows考慮
- manage scriptの考慮追加 ガシガシ
- 開発howto 記載
- GUIクライアントでの接続例


## 使い方
1. BASEコンテナのセットアップ (以下を参考に)
2. docker-compose build
3. docker-compose up
4. http://localhost/ にアクセス。

## <事前準備> baseコンテナに関して **＊初回だけ**
参考記事 : https://stackoverflow.com/questions/20481225/how-can-i-use-a-local-image-as-the-base-image-with-a-dockerfile  

web.db等のコンテナはcentOSベースのコンテナ(以降BC)を元に生成されます。  
このBCの取り扱いは本来dockerhubに挙げられているpublicimageを参照すべきだが、
しょはんの理由により、まず各位のPCでBCのimageをlocalにセットし、そのイメージを参照する様にします。
以下の手順でlocalのimagesにBCをセットしてある前提でdocker-compose up する必要があります。

#### 手順
1. BCをビルド 
```
$ cd general_enviroment/container/base
$ docker build .
Successfully built 0e9c7c83bb9a
```
2. BCのIMAGE_IDを確認
```
$ docker images (または、build時の出力されたID)
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
none        latest              0e9c7c83bb9a        9 minutes ago       1.03GB
```  
3. 生成したimageの名称を更新
```
$ docker tag 0e9c7c83bb9a ktahara-base
```
4. 確認 
```
% docker images                                                                                                                                    ✹ ✭
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
ktahara-base        latest              0e9c7c83bb9a        9 minutes ago       1.03GB
```