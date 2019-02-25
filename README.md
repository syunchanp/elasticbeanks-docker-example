# elasticbeanks-docker-example

# beanstalk
https://qiita.com/drafts/9e01d9aaaa733c96b5bf

# case 1.
## This case is docker component on tomcat exclude webapps link

newrelicをインストールすると共に、Dockerのシングル構成を構築します
volume optionを使用しないので、Docker内でのみアプリケーションが完結します
```
 ─docker-tomcat
   │  .gitignore
   │  Dockerfile
   │  Dockerrun.aws.json
   │
   └─.ebextensions
           98newrelic.config
```

# case 2.
## This case is docker component with volume link option  on tomcat's webapps

newrelicをインストールすると共に、Dockerのシングル構成を構築します
volume optionを使用してwar形式のアプリも併せてdeployする、Dockerコンポーネントです
webapps配下にwarファイルを置くことで、deployされます
webapps がvolumeでリンクされるので汎用的な利用が出来る代わり、Docker内のwebappsは
置き換わります

サンプルとして、tomcatのdocsを一部参照できるようにされています
```
 ─docker-tomcat-volume
     │  .gitignore
     │  Dockerfile
     │  Dockerrun.aws.json
     │  
     ├─.ebextensions
     │      98newrelic.config
     │      
     └─webapps
         ├─docs
         │  │  index.html
         │  ├─WEB-INF
         │  │      web.xml
         │  └─websocketapi
         │          index.html
         │              
         └─ROOT
             │  
             └─WEB-INF
                     web.xml
```

# extract options
1. newrelic
When it use newrelic extension, please replace NEWRELIC_LICENSE.
refer:
https://newrelic.degica.com/docs/infrastructure/new-relic-infrastructure/installation/install-infrastructure-agent-aws-elastic-beanstalk
こちらの記事を元に設定を作成しております

2. Dockerfile
tomcat9のDockerfileは、https://hub.docker.com/_/tomcat から取得しています
