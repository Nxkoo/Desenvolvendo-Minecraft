---
description: >-
  Neste tópico iremos aprender mais como os proxies funcionam, e criaremos a
  nossa própria estrutura de proxy.
---

# 🛜 Proxies

## O que é um Proxy e como o minecraft lida com ele?

A maneira como o Minecraft funciona em geral é que alguns pedaços de código são manipulados pelo lado do cliente e outros pelo lado do servidor. Isso ocorre até mesmo quando você está jogando localmente em um mundo singleplayer, pois há um servidor separado em execução e seu cliente está renderizando coisas desse servidor. Portanto, queremos que algumas partes do nosso código sejam executadas apenas no cliente, outras no servidor e, em alguns casos, em ambos os lados.

É por isso que criamos o Proxy. Com ele, podemos decidir em qual lado o código será registrado, garantindo que tudo funcione corretamente conforme esperado.

## Como um Proxy pode ser útil?

Os proxies são especialmente úteis para separar funcionalidades específicas de cada lado. Por exemplo, a renderização de gráficos e interfaces de usuário deve ser feita apenas no lado do cliente, enquanto a lógica de jogo e manipulação de dados deve ser tratada no lado do servidor. Isso evita problemas como tentativas de renderização no lado do servidor ou manipulação de dados sensíveis no lado do cliente, o que pode causar crashes ou exploits.

***

Com esta estrutura em mente, podemos avançar para a criação e configuração dos nossos proxies.

Vamos começar criando um novo package `Proxy` e criaremos 3 classes que são elas:

* **CommonProxy**
* **ClientProxy**
* **ServerProxy**

Na _`CommonProxy`_ podemos colocar os mesmos 3 métodos que colocamos na nossa classe _`Core`_ , pois é apenas para termos controle mais preciso.

{% code title="CommonProxy.java" %}
```java
package com.github.nxkoo.devmine.minemod.proxy;

import cpw.mods.fml.common.event.FMLInitializationEvent;
import cpw.mods.fml.common.event.FMLPostInitializationEvent;
import cpw.mods.fml.common.event.FMLPreInitializationEvent;

public class CommonProxy {
    public void preInit(FMLPreInitializationEvent $e) {

    }

    public void init(FMLInitializationEvent $e) {

    }

    public void postInit(FMLPostInitializationEvent $e) {

    }
}
```
{% endcode %}

Já no _`ClientProxy`_ queremos que ela contenha todas os métodos do _`CommonProxy`_ pois o cliente deve fazer tudo que está no proxy comum. Então precisamos estender o _`CommonProxy`_ ou seja, o cliente vai herdar todas os métodos/funções do proxy comum, isso é o que chamamos de herança na Programação Orientada a Objetos.&#x20;

Mas agora precisamos que esses métodos do _`CommonProxy`_ sejam herdados no _`ClientProxy`_ também, para isso basta apertar `Alt + Insert` e clicar em Override Methods ou simplesmente apertar `Ctrl + O` e selecione todos os 3 métodos.

Repita o mesmo processo do _`ClientProxy`_ no _`ServerProxy`._

{% tabs %}
{% tab title="CommonProxy.java" %}
```java
package com.github.nxkoo.devmine.minemod.proxy;

import cpw.mods.fml.common.event.FMLInitializationEvent;
import cpw.mods.fml.common.event.FMLPostInitializationEvent;
import cpw.mods.fml.common.event.FMLPreInitializationEvent;

public class CommonProxy {
    public void preInit(FMLPreInitializationEvent $e) {

    }

    public void init(FMLInitializationEvent $e) {

    }

    public void postInit(FMLPostInitializationEvent $e) {

    }
}
```
{% endtab %}

{% tab title="ClientProxy.java" %}
```java
package com.github.nxkoo.devmine.minemod.proxy;

import cpw.mods.fml.common.event.FMLInitializationEvent;
import cpw.mods.fml.common.event.FMLPostInitializationEvent;
import cpw.mods.fml.common.event.FMLPreInitializationEvent;

public class ClientProxy extends CommonProxy {
    @Override
    public void preInit(FMLPreInitializationEvent $e) {
        super.preInit($e);
    }

    @Override
    public void init(FMLInitializationEvent $e) {
        super.init($e);
    }

    @Override
    public void postInit(FMLPostInitializationEvent $e) {
        super.postInit($e);
    }
}
```
{% endtab %}

{% tab title="ServerProxy.java" %}
```java
package com.github.nxkoo.devmine.minemod.proxy;

import cpw.mods.fml.common.event.FMLInitializationEvent;
import cpw.mods.fml.common.event.FMLPostInitializationEvent;
import cpw.mods.fml.common.event.FMLPreInitializationEvent;

public class ServerProxy extends CommonProxy {
    @Override
    public void preInit(FMLPreInitializationEvent $e) {
        super.preInit($e);
    }

    @Override
    public void init(FMLInitializationEvent $e) {
        super.init($e);
    }

    @Override
    public void postInit(FMLPostInitializationEvent $e) {
        super.postInit($e);
    }
}
```
{% endtab %}
{% endtabs %}

Agora voltaremos a nossa classe _`Core`_ para registrar os nossos proxies. Precisamos criar uma variável pública e estática **`proxy`** que instancia o _`CommonProxy`_ e adicionaremos uma anotação especifica que informa ao Forge que este é um proxy de dois lados. Colocamos **@SidedProxy** a cima da nossa variável.&#x20;

Essa anotação leva dois parâmetros: `clientSide` e `serverSide`, que recebem o caminho "real" do pacote com o nome da classe. Basicamente, essa anotação fornece ao Forge as classes que serão tratadas pelo lado do cliente e pelo lado do servidor, então não precisamos nos preocupar em mais nada. Apenas em chamá-las na classe principal do mod.

```java
@SidedProxy(clientSide = "com.github.nxkoo.devmine.minemod.proxy.ClientProxy", serverSide = "com.github.nxkoo.devmine.minemod.proxy.ServerProxy")
public static CommonProxy proxy;
```

Depois que a variável foi criada, precisamos agora chamar essa variável passando o nosso método e o parâmetro pegando do método que está na classe principal.

```java
public void preInit(FMLPreInitializationEvent $e) {
    proxy.preInit($e);
}

public void init(FMLInitializationEvent $e) {
    proxy.init($e);
}

public void postInit(FMLPostInitializationEvent $e) {
    proxy.postInit($e);
}
```
