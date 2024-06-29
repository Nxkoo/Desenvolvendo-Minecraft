---
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# 🤖 Configurando o MDK

Após abrir a pasta, você poderá excluir esses 6 arquivos

1. <mark style="color:red;">CREDITS-fml.txt</mark>
2. <mark style="color:red;">forge-1.7.10-10.13.4.1614-1.7.10-changelog.txt</mark>
3. <mark style="color:red;">LICENSE-fml.txt</mark>
4. <mark style="color:red;">MinecraftForge-Credits.txt</mark>
5. <mark style="color:red;">MinecraftForge-License.txt</mark>
6. <mark style="color:red;">README.txt</mark>

<figure><img src="../../.gitbook/assets/image (26).png" alt=""><figcaption><p>Ficando assim apenas esses outros 6 arquivos.</p></figcaption></figure>

Agora você deve seguir esses passos:

1. Abra a pasta gradle e navegue até o arquivo chamado: _gradle-wrapper.properties_
2. E altere o "distributionUrll" para: `https\://services.gradle.org/distributions/gradle-4.4.1-bin.zip`
3. Ficará como no exemplo abaixo.

{% tabs %}
{% tab title="Antigo" %}
```properties
distributionBase=GRADLE_USER_HOME
distributionPath=wrapper/dists
zipStoreBase=GRADLE_USER_HOME
zipStorePath=wrapper/dists
distributionUrl=https\://services.gradle.org/distributions/gradle-2.0-bin.zip
```
{% endtab %}

{% tab title="Atualizado" %}
```properties
distributionBase=GRADLE_USER_HOME
distributionPath=wrapper/dists
zipStoreBase=GRADLE_USER_HOME
zipStorePath=wrapper/dists
distributionUrl=https\://services.gradle.org/distributions/gradle-4.4.1-bin.zip
```
{% endtab %}
{% endtabs %}

Depois de seguir esses passos, volte ao inicio e abra o arquivo chamado `build.gradle`

* E substitua o código **antigo** para o **atualizado** conforme indicado abaixo.

{% tabs %}
{% tab title="Antigo" %}
```gradle
buildscript {
    repositories {
        mavenCentral()
        maven {
            name = "forge"
            url = "http://files.minecraftforge.net/maven"
        }
        maven {
            name = "sonatype"
            url = "https://oss.sonatype.org/content/repositories/snapshots/"
        }
    }
    dependencies {
        classpath 'net.minecraftforge.gradle:ForgeGradle:1.2-SNAPSHOT'
    }
}

apply plugin: 'forge'

version = "1.0"
group= "com.yourname.modid" // http://maven.apache.org/guides/mini/guide-naming-conventions.html
archivesBaseName = "modid"

minecraft {
    version = "1.7.10-10.13.4.1614-1.7.10"
    runDir = "eclipse"
}

dependencies {
    // you may put jars on which you depend on in ./libs
    // or you may define them like so..
    //compile "some.group:artifact:version:classifier"
    //compile "some.group:artifact:version"
      
    // real examples
    //compile 'com.mod-buildcraft:buildcraft:6.0.8:dev'  // adds buildcraft to the dev env
    //compile 'com.googlecode.efficient-java-matrix-library:ejml:0.24' // adds ejml to the dev env

    // for more info...
    // http://www.gradle.org/docs/current/userguide/artifact_dependencies_tutorial.html
    // http://www.gradle.org/docs/current/userguide/dependency_management.html

}

processResources
{
    // this will ensure that this task is redone when the versions change.
    inputs.property "version", project.version
    inputs.property "mcversion", project.minecraft.version

    // replace stuff in mcmod.info, nothing else
    from(sourceSets.main.resources.srcDirs) {
        include 'mcmod.info'
                
        // replace version and mcversion
        expand 'version':project.version, 'mcversion':project.minecraft.version
    }
        
    // copy everything else, thats not the mcmod.info
    from(sourceSets.main.resources.srcDirs) {
        exclude 'mcmod.info'
    }
}

```
{% endtab %}

{% tab title="Atualizado" %}
```gradle
buildscript {
    repositories {
        mavenCentral()
        maven {
            name = "forge"
            url = "https://maven.minecraftforge.net"
        }
        maven {
            name = "sonatype"
            url = "https://oss.sonatype.org/content/repositories/snapshots/"
        }
    }
    dependencies {
        classpath ('com.anatawa12.forge:ForgeGradle:1.2-1.0.+') {
            changing = true
        }
    }
}

apply plugin: 'forge'

version = "1.0"
group= "com.yourname.modid" // http://maven.apache.org/guides/mini/guide-naming-conventions.html
archivesBaseName = "modid"

targetCompatibility = sourceCompatibility = JavaVersion.VERSION_1_8

minecraft {
    version = "1.7.10-10.13.4.1614-1.7.10"
    runDir = "eclipse"
}

tasks.withType(JavaCompile) {
options.encoding = 'UTF-8'
}

dependencies {
    implementation 'org.jetbrains:annotations:23.0.0'

    // you may put jars on which you depend on in ./libs
    // or you may define them like so..
    //compile "some.group:artifact:version:classifier"
    //compile "some.group:artifact:version"
      
    // real examples
    //compile 'com.mod-buildcraft:buildcraft:6.0.8:dev'  // adds buildcraft to the dev env
    //compile 'com.googlecode.efficient-java-matrix-library:ejml:0.24' // adds ejml to the dev env

    // for more info...
    // http://www.gradle.org/docs/current/userguide/artifact_dependencies_tutorial.html
    // http://www.gradle.org/docs/current/userguide/dependency_management.html

}

processResources
{
    // this will ensure that this task is redone when the versions change.
    inputs.property "version", project.version
    inputs.property "mcversion", project.minecraft.version

    // replace stuff in mcmod.info, nothing else
    from(sourceSets.main.resources.srcDirs) {
        include 'mcmod.info'
                
        // replace version and mcversion
        expand 'version':project.version, 'mcversion':project.minecraft.version
    }
        
    // copy everything else, thats not the mcmod.info
    from(sourceSets.main.resources.srcDirs) {
        exclude 'mcmod.info'
    }
}

```
{% endtab %}
{% endtabs %}

Agora tendo feito essas mudanças, você só precisará configurar o seu package e o modID[^1], siga o exemplo abaixo:

```gradle
group= "com.github.yourname.examplemod"
archivesBaseName = "examplemod"
```

Sucesso agora você tem seu MDK configurado e podemos passar para a próxima etapa. 🎊

[^1]: Identificação do seu mod
