---
description: >-
  Neste tópico iremos abordar sobre a configuração do ambiente e a instalação do
  Java.
---

# ⚙️ Configurando o ambiente de desenvolvimento

Antes de tudo, precisamos saber o que é o JDK. Falarei brevemente sobre o que é e o que ele faz.

Como o nome já diz, é um Kit de Desenvolvimento Java. Com esse "Kit" podemos desenvolver aplicações em Java. O Java possui algumas versões e edições, que no momento não entraremos no mérito, porém, o JDK é a versão/edição necessária para criar coisas em Java.

O Java possui duas versões principais: a JRE (Java Runtime Environment) e o JDK (Java Development Kit). A JRE é necessária para rodar/executar programas feitos em Java, enquanto o JDK é a versão/edição que permite que você desenvolva aplicações em Java.

Iremos instalar a versão JDK. Siga as instruções abaixo e configure-a corretamente no seu sistema operacional (Windows, Linux ou MacOS).

## 🚀 Instalando o JDK

{% hint style="success" %}
Algumas IDEs como o [IntelliJ](https://www.jetbrains.com/pt-br/idea/download/?section=windows) já consegue baixar e instalar o JDK e realizar a configuração de forma mais fácil.
{% endhint %}

A primeira coisa que precisamos fazer é busca no Google por Java [JDK 8](https://www.oracle.com/br/java/technologies/javase/javase8-archive-downloads.html) versão esta que iremos utilizar. Logo após selecione a opção apropriada de acordo com o seu sistema operacional.

Logo abaixo, você pode escolher qual sistema está usando, e configurar-lo na sua maquina de acordo com o seu sistema.

{% tabs %}
{% tab title="Windows" %}
* Busque no Google por Java [JDK 8](https://www.oracle.com/br/java/technologies/javase/javase8-archive-downloads.html).
* Ou baixe a versão do JDK que já deixei pronta para você baixar:&#x20;
  * [Windows 86x (32 bits)](https://download.oracle.com/otn/java/jdk/8u202-b08/1961070e4c9b4e26a04e7f5a083f551e/jdk-8u202-windows-i586.exe?AuthParam=1719515246\_30cc244d7039bfb8a73f23c021b5a29b)
  * [Windows 64x (64 bits)](https://download.oracle.com/otn/java/jdk/8u202-b08/1961070e4c9b4e26a04e7f5a083f551e/jdk-8u202-windows-x64.exe?AuthParam=1719515392\_f8c40749f2e167936a8818efb343b589)

{% hint style="info" %}
Para ver qual é o seu tipo de sistema, basta seguir os seguintes passos:

1. Pressione as teclas `Windows + Pause/Break` no seu teclado.
2. Em "**Especificações do dispositivo**" você procura **Tipo de sistema**:
3. E deverá aparecer algo como: Sistema operacional de 64 bits ou 32 Bits.
{% endhint %}

* Após realizar o download, execute o instalador para instalar o Java no Windows. Este processo instalará tanto o **JDK** quanto a **JRE**.

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
Evite mudar o diretório de instalação.
{% endhint %}

* Em seu Explorador de Arquivos, deve ter algo mais ou menos assim:

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

* Precisamos agora, validar se a instalação também já configurou nossa variável de ambiente, para poder executar o Java pelo Prompt de comando ou PowerShell do Windows.
* Abra o Prompt de comando e execute o comando `java -version`.

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption><p>Precisa aparecer exatamente assim.</p></figcaption></figure>

{% hint style="danger" %}
Caso não apareça da mesma forma que a imagem, então precisaremos configurar a nossa variável de ambiente.
{% endhint %}
{% endtab %}

{% tab title="MacOS/Linux" %}
Instalação no MacOS/Linux

1. Acesse o site oficial do [Java SE Development Kit 8](https://www.oracle.com/java/technologies/javase/javase-jdk8-downloads.html).
2. Faça o download da versão apropriada para o seu sistema operacional.
3. Abra o terminal e navegue até o diretório onde o arquivo foi baixado.
4. Siga as instruções de instalação fornecidas pelo instalador, que geralmente envolve descompactar o arquivo e mover os conteúdos para o diretório apropriado (por exemplo, `/usr/lib/jvm`).

Para MacOS:

```sh
sudo mv jdk-8uXXX-macosx-x64 /Library/Java/JavaVirtualMachines/
```

Substitua `jdk-8uXXX` pela versão específica que você instalou.

Para Linux:

```sh
sudo tar -xvf jdk-8uXXX-linux-x64.tar.gz
sudo mv jdk-8uXXX /usr/lib/jvm/
```
{% endtab %}
{% endtabs %}



## ⚙️ Configurando as variáveis de ambiente

{% tabs %}
{% tab title="Windows" %}
* Primeiro aperte o botão Windows e escreva `Editar as variáveis de ambiente do sistema`&#x20;

<figure><img src="../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

* Logo em seguida você deverá apertar em **Variáveis de Ambiente**

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

* Em Variáveis do sistema, clique em **Novo...**

<figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

* E escreva **`JAVA_HOME`**em Nome da variável
* E logo abaixo especifique o caminho que colocou o **JDK**

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

* Logo depois encontre onde está escrito **Path** e clique em editar

<figure><img src="../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

* Ao lado você encontrará algumas opções e clique em **Novo** e escreva: `C:\Program Files\Java\jdk1.8.0_202\bin`
* Depois apenas clique em _**OK -> OK -> Aplicar**_ e seu ambiente Java estará configurado.
{% endtab %}

{% tab title="MacOS/Linux" %}
1. Configure as variáveis de ambiente adicionando as seguintes linhas ao seu arquivo `~/.bash_profile`, `~/.bashrc` ou `~/.zshrc` (dependendo do shell que você está usando):

```sh
export JAVA_HOME=/usr/lib/jvm/jdk-8uXXX
export PATH=$JAVA_HOME/bin:$PATH
```

Lembre-se de substituir`jdk-8uXXX` pela versão específica que você instalou.

1.  Salve o arquivo e execute o seguinte comando para aplicar as mudanças:

    ```sh
    source ~/.bash_profile
    ```

    ou

    ```sh
    source ~/.bashrc
    ```

    ou

    ```sh
    source ~/.zshrc
    ```
2.  Verifique se a instalação foi bem-sucedida executando:

    ```sh
    java -version
    ```

    Isso deve mostrar a versão do Java instalada, confirmando que a instalação e configuração foram realizadas corretamente.
{% endtab %}
{% endtabs %}

> Caso você se perca na instalação/configuração, lembre que o Google é seu amigo 😉👍

Boa você baixou! Agora seu Java Development Kit está instalado e só falta apenas mais alguns passos para começarmos a escrever nossa primeira linha de código. 🎊🎉
