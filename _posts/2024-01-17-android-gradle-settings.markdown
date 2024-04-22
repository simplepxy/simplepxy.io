---
layout: post
title:  "android工程中gradle配置"
date:   2024-01-17 23:10:00 +0800
categories: tech android gradle
---
最近网络环境越来越差，android studio默认的gradle版本已经到了8.0，下载下来经常出现timeout的问题。所以就找了下国内是否有gradle安装包的软件源，看了下腾讯的软件源下载速度还不错。

#### 1. 配置gradle的下载地址

在gradle-wrapper.properties文件中配置腾讯的gradle源。

[腾讯源](https://mirrors.cloud.tencent.com/)

#### 2. 配置build.gradle

```groovy
buildscript {
    repositories {
        maven { url 'http://maven.aliyun.com/nexus/content/groups/public/' }
        maven{ url 'http://maven.aliyun.com/nexus/content/repositories/jcenter'}
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:2.2.3'
    }        
}

allprojects {
    repositories {
        maven { url 'http://maven.aliyun.com/nexus/content/groups/public/' }
        maven{ url 'http://maven.aliyun.com/nexus/content/repositories/jcenter'}
    }
}
```

#### 3. 配置本机的gradle源

在USER_HOME/.gradle/下创建init.gradle文件

```groovy

allprojects{
    repositories {
        def ALIYUN_REPOSITORY_URL = 'http://maven.aliyun.com/nexus/content/groups/public'
        def GRADLE_LOCAL_RELEASE_URL = 'https://repo.gradle.org/gradle/libs-releases-local'
        
        all { ArtifactRepository repo ->
            if(repo instanceof MavenArtifactRepository){
                def url = repo.url.toString()
                if (url.startsWith('https://repo1.maven.org/maven2')) {
                    project.logger.lifecycle "Repository ${repo.url} replaced by $ALIYUN_REPOSITORY_URL."
                    remove repo
                }
            }
        }
        maven {
            url ALIYUN_REPOSITORY_URL     
        }
        maven {
            url GRADLE_LOCAL_RELEASE_URL
        }   
    }

}
```

