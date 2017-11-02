## MEMO
- コンテナへのログイン  
`$ ./manage login (app または db)`
- コンテナ間のファイル転送  
https://qiita.com/gologo13/items/7e4e404af80377b48fd5
- Windowsでの動作に関して  
https://docs.docker.com/docker-for-windows/install/  
https://docs.microsoft.com/ja-jp/virtualization/hyper-v-on-windows/reference/hyper-v-requirements  
http://www.vwnet.jp/Windows/w10/Hyper-V/Enablew10Hyper-V.htm  
所有しているWindowsPCにdokcer for windowsをセットし確認したところ、  
OSがWindows10HomeEditionだったためかMicrosoftHyper-Vを有効化できなかった。  
このため未だWindowsでの動作検証はできていない状況。

## TODO
- 参考元記事の記載  
https://qiita.com/yousan/items/f05fa03c1f3951971f2f


## MountedVolumes
|名称|host|client|
|:--|:--|:--|
|DocumentRoot|app:/var/www/html|/enviroment/documentRoot|
|application|app:/var/src/app|/enviroment/application|

## Application setup
1. /application 配下にapplicationを丸ごと配置
2. (appコンテナ内) DocumentRootからappplicationにsimboliclink
```
- ログイン 
$ docker exec -it app bash
- simbolic link
$ ln -snf /usr/src/application/laravel/MyFirstLaravel/public /var/www/html/laravel5
```
3. http://localhost/laravel5 にアクセス

## how to use
1. BASEコンテナのセットアップ (以下を参考に)
2. docker-compose build
3. docker-compose up
4. http://localhost/ にアクセス。

#### アクセスURL
|||
|:--|:--|
|WEB|http://localhost|
|phpmyadmin|http://localhost:8080|

## <事前準備> baseコンテナに関して **＊初回だけ**
参考記事 : https://stackoverflow.com/questions/20481225/how-can-i-use-a-local-image-as-the-base-image-with-a-dockerfile  

web.db等のコンテナはcentOSベースのコンテナ(以降BC)を元に生成されます。  
このBCの取り扱いは本来dockerhubに挙げられているpublicimageを参照すべきだが、
しょはんの理由により、まず各位のPCでBCのimageをlocalにセットし、そのイメージを参照する様にします。
以下の手順でlocalのimagesにBCをセットしてある前提でdocker-compose up する必要があります。

#### 手順
1. BCをビルド 
```
$ cd enviroment/container/base
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

