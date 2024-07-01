---
description: >-
  Neste tópico iremos aprender mais sobre como os proxies funcionam e criaremos
  a nossa própria estrutura de proxy.
---

# 🛜 Proxies

## O que é um Proxy e como o Minecraft lida com ele?

A maneira como o Minecraft funciona em geral é que alguns pedaços de código são manipulados pelo lado do cliente e outros pelo lado do servidor. Isso ocorre até mesmo quando você está jogando localmente em um mundo singleplayer, pois há um servidor separado em execução e seu cliente está renderizando coisas desse servidor. Portanto, queremos que algumas partes do nosso código sejam executadas apenas no cliente, outras no servidor e, em alguns casos, em ambos os lados.

É por isso que criamos o Proxy. Com ele, podemos decidir em qual lado o código será registrado, garantindo que tudo funcione corretamente conforme esperado.

## Como um Proxy pode ser útil?

Os proxies são especialmente úteis para separar funcionalidades específicas de cada lado. Por exemplo, a renderização de gráficos e interfaces de usuário deve ser feita apenas no lado do cliente, enquanto a lógica de jogo e manipulação de dados deve ser tratada no lado do servidor. Isso evita problemas como tentativas de renderização no lado do servidor ou manipulação de dados sensíveis no lado do cliente, o que pode causar crashes ou exploits.

***

Com essa estrutura em mente, podemos avançar para a criação e configuração dos nossos proxies.

Vamos começar criando um novo pacote _proxy_ e criaremos 3 classes que são:

* **`CommonProxy`**
* **`ClientProxy`**
* **`ServerProxy`**

Na **`CommonProxy`**podemos colocar os mesmos 3 métodos que colocamos na nossa classe **`Core`**, pois é apenas para termos um controle mais preciso.

{% code title="CommonProxy.java" %}
```java
package com.github.nxkoo.devmine.minemod.proxy;

import cpw.mods.fml.common.event.FMLInitializationEvent;
import cpw.mods.fml.common.event.FMLPostInitializationEvent;
import cpw.mods.fml.common.event.FMLPreInitializationEvent;

public class CommonProxy {
    public void preInit(FMLPreInitializationEvent event) {
        // Código de inicialização comum
    }

    public void init(FMLInitializationEvent event) {
        // Código de inicialização comum
    }

    public void postInit(FMLPostInitializationEvent event) {
        // Código de pós-inicialização comum
    }
}
```
{% endcode %}

Na **`ClientProxy`** queremos que ela contenha todos os métodos do **`CommonProxy`** pois o cliente deve fazer tudo que está no proxy comum. Então precisamos estender o **`CommonProxy`**. O cliente vai herdar todos os métodos/funções do proxy comum, isso é o que chamamos de herança na Programação Orientada a Objetos.

Para garantir que esses métodos do **`CommonProxy`** sejam herdados no **`ClientProxy`**, basta apertar **Alt + Insert** no seu teclado e clicar em **Override Methods** ou simplesmente apertar **Ctrl + O** e selecionar todos os 3 métodos.

Repita o mesmo processo do **`ClientProxy`** no **`ServerProxy`**.

{% tabs %}
{% tab title="CommonProxy.java" %}
```java
package com.github.nxkoo.devmine.minemod.proxy;

import cpw.mods.fml.common.event.FMLInitializationEvent;
import cpw.mods.fml.common.event.FMLPostInitializationEvent;
import cpw.mods.fml.common.event.FMLPreInitializationEvent;

public class CommonProxy {
    public void preInit(FMLPreInitializationEvent event) {
        // Código de inicialização comum
    }

    public void init(FMLInitializationEvent event) {
        // Código de inicialização comum
    }

    public void postInit(FMLPostInitializationEvent event) {
        // Código de pós-inicialização comum
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
    public void preInit(FMLPreInitializationEvent event) {
        super.preInit(event);
        // Código específico do cliente
    }

    @Override
    public void init(FMLInitializationEvent event) {
        super.init(event);
        // Código específico do cliente
    }

    @Override
    public void postInit(FMLPostInitializationEvent event) {
        super.postInit(event);
        // Código específico do cliente
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
    public void preInit(FMLPreInitializationEvent event) {
        super.preInit(event);
        // Código específico do servidor
    }

    @Override
    public void init(FMLInitializationEvent event) {
        super.init(event);
        // Código específico do servidor
    }

    @Override
    public void postInit(FMLPostInitializationEvent event) {
        super.postInit(event);
        // Código específico do servidor
    }
}
```
{% endtab %}
{% endtabs %}

Agora voltaremos à nossa classe **`Core`** para registrar os nossos proxies. Precisamos criar uma variável pública e estática `proxy` que instancia o **`CommonProxy`** e adicionaremos uma anotação específica que informa ao Forge que este é um proxy de dois lados. Colocamos `@SidedProxy` acima da nossa variável.

Essa anotação leva dois parâmetros: `clientSide` e `serverSide`, que recebem o caminho "absoluto" do pacote com o nome da classe. Basicamente, essa anotação fornece ao Forge as classes que serão tratadas pelo lado do cliente e pelo lado do servidor, então não precisamos nos preocupar em com mais nada. Apenas em chamá-las na classe principal do mod.

```java
@SidedProxy(clientSide = "com.github.nxkoo.devmine.minemod.proxy.ClientProxy", serverSide = "com.github.nxkoo.devmine.minemod.proxy.ServerProxy")
public static CommonProxy proxy;
```

Depois que a variável `proxy` foi criada e anotada com **@SidedProxy**, precisamos agora utilizá-la chamando os métodos apropriados (`preInit()`, `init()`, `postInit()`) na classe principal do mod e passando os parâmetros dos eventos correspondentes. Isso garantirá que as ações específicas do cliente e do servidor sejam executadas corretamente.

Além disso, é importante anotar cada um desses métodos com **@Mod.EventHandler**. Essa anotação informa ao Forge que esses métodos devem ser chamados nos momentos apropriados durante o ciclo de vida do mod.

```java
public void preInit(FMLPreInitializationEvent event) {
    proxy.preInit(event);
}

public void init(FMLInitializationEvent event) {
    proxy.init(event);
}

public void postInit(FMLPostInitializationEvent event) {
    proxy.postInit(event);
}
```

A anotação **@Mod.EventHandler** é crucial porque o Forge utiliza essas anotações para saber quais métodos devem ser invocados durante as diferentes fases de inicialização do mod. Sem essas anotações, o Forge não saberia quais métodos chamar, e as etapas de inicialização do seu mod não seriam executadas corretamente.

***

Código completo disponível abaixo:

```java
package com.github.nxkoo.devmine.minemod;

import com.github.nxkoo.devmine.minemod.lib.Env;
import com.github.nxkoo.devmine.minemod.proxy.CommonProxy;
import cpw.mods.fml.common.Mod;
import cpw.mods.fml.common.SidedProxy;
import cpw.mods.fml.common.event.FMLInitializationEvent;
import cpw.mods.fml.common.event.FMLPostInitializationEvent;
import cpw.mods.fml.common.event.FMLPreInitializationEvent;

@Mod(modid = Env.MOD_ID, name = Env.MOD_NAME, version = Env.MOD_VERSION)
public class Core {

    @Mod.Instance
    public static Core instance = new Core();

    @SidedProxy(clientSide = "com.github.nxkoo.devmine.minemod.proxy.ClientProxy", serverSide = "com.github.nxkoo.devmine.minemod.proxy.ServerProxy")
    public static CommonProxy proxy;

    @Mod.EventHandler
    public void preInit(FMLPreInitializationEvent $e) {
        proxy.preInit($e);
    }

    @Mod.EventHandler
    public void init(FMLInitializationEvent $e) {
        proxy.init($e);
    }

    @Mod.EventHandler
    public void postInit(FMLPostInitializationEvent $e) {
        proxy.postInit($e);
    }
}
```

***

Ufaa 🤯 finalmente a parte do proxy terminou, agora podemos ir para a próxima parte: **ITEM**.
