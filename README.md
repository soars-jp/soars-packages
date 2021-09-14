# SOARS用パッケージ置き場

## 環境設定

Mavenがインストールされていなければ，Mavenをインストールする．
以下では，UbuntuなどのDebian系の場合を想定して説明する．

`Mavenのインストール`

```
sudo apt install maven
```

Personal access tokenを作る．https://github.com/settings/tokens からPersonal access tokenをつくる．

下記の~/.m2/settings.xml を作成して，デプロイ先となるMavenリポジトリの認証情報を記述する．
Github-Account-Nameを自分のGitHubアカウント名，Github-Account-Tokenを上記で入手したPersonal access tokenに置き換えること．

`~/.m2/settings.xml`

```xml
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0
                      http://maven.apache.org/xsd/settings-1.0.0.xsd">

  <servers>
    <server>
      <id>github</id>
      <username>Github-Account-Name</username>
      <password>Github-Account-Token</password>
    </server>
  </servers>

</settings>

```

## パッケージの説明

- [soars-coreパッケージ](https://github.com/soars-jp/soars-packages/packages/984890)  
soarsライブラリである．

- [soars-d2jパッケージ](https://github.com/soars-jp/soars-packages/packages/984906)  
d2jライブラリである．このパッケージは，soars-coreパッケージに依存している．

## パッケージの利用方法

### soars-coreパッケージ

#### pom.xmlの修正

JDKのバージョンとして11を指定する．

`pom.xmlにおけるJDKのバージョン指定`

```
  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <java.version>11</java.version>
    <maven.compiler.source>${java.version}</maven.compiler.source>
    <maven.compiler.target>${java.version}</maven.compiler.target>
  </properties>
```

リポジトリ情報を追加する．

`pom.xmlへのリポジトリ情報の追加`

```
  <repositories>
    <repository>
        <id>github</id>
        <name>GitHub OWNER Apache Maven Packages</name>
        <url>https://maven.pkg.github.com/soars-jp/soars-packages</url>
        <releases>
            <enabled>true</enabled>
        </releases>
        <snapshots>
            <enabled>true</enabled>
        </snapshots>
    </repository>
  </repositories>
```

soars-coreパッケージ利用の記述を追加する．具体的には，dependenciesセクションの中に追加する．dependenciesセクションには，元からjunitの記述があることに注意する．

`pom.xmlへのsoars-coreパッケージ利用の記述の追加`

```
  <dependencies>
      <dependency>
        <groupId>jp.soars</groupId>
        <artifactId>soars-core</artifactId>
        <version>210912_01</version>
    </dependency>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.11</version>
      <scope>test</scope>
    </dependency>
  </dependencies>
```

#### soars-coreパッケージの利用例
soars-coreパッケージの利用例として，[soarsサンプル](https://github.com/soars-jp/covid19)，[d2j](https://github.com/soars-jp/d2j)がある．

### soars-d2jパッケージ

#### pom.xmlの修正

JDKのバージョンとして11を指定する．

`pom.xmlにおけるJDKのバージョン指定`

```
  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <java.version>11</java.version>
    <maven.compiler.source>${java.version}</maven.compiler.source>
    <maven.compiler.target>${java.version}</maven.compiler.target>
  </properties>
```

リポジトリ情報を追加する．

`pom.xmlへのリポジトリ情報の追加`

```
  <repositories>
    <repository>
        <id>github</id>
        <name>GitHub OWNER Apache Maven Packages</name>
        <url>https://maven.pkg.github.com/soars-jp/soars-packages</url>
        <releases>
            <enabled>true</enabled>
        </releases>
        <snapshots>
            <enabled>true</enabled>
        </snapshots>
    </repository>
  </repositories>
```

soars-coreパッケージおよびsoars-d2j利用の記述を追加する．具体的には，dependenciesセクションの中に追加する．dependenciesセクションには，元からjunitの記述があることに注意する．

`pom.xmlへのsoars-coreパッケージとsoars-d2jの利用の記述の追加`

```
  <dependencies>
    <dependency>
      <groupId>jp.soars</groupId>
      <artifactId>soars-core</artifactId>
      <version>210912_01</version>
    </dependency>
    <dependency>
      <groupId>jp.soars</groupId>
      <artifactId>soars-d2j</artifactId>
      <version>210912_01</version>
    </dependency>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.11</version>
      <scope>test</scope>
    </dependency>
  </dependencies>
```

#### soars-d2jパッケージの利用例

soars-d2jパッケージの利用例として，[COVID19のシミュレーション](https://github.com/soars-jp/covid19)がある．
