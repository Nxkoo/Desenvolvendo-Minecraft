---
description: >-
  Neste tópico iremos construir a classe principal do mod e configurar os
  proxies do nosso mod.
---

# 📶 Mod Class & Proxies

Começaremos primeiro apagando o arquivo atual que veio de exemplo, `ExampleMod`. E criaremos um novo arquivo chamado `Core` para ser a classe principal do nosso mod.

Logo após criar o arquivo, vamos criar um novo package _`lib`_ e colocaremos um arquivo _`Env`_.

<figure><img src="../../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

E será neste arquivo que vamos registrar as nossas variáveis (outrora chamadas de Constantes) que serão utilizadas em uma boa parte do código. As variáveis são `MOD_ID`, `MOD_NAME`, `MOD_VERSION`, com as respectivas informações de cada uma.

{% code title="Env.java" %}
```java
package com.github.nxkoo.devmine.minemod.lib;

public class Env {
    public static final String MOD_NAME = "DesenvolvendoMinecraftMod";
    public static final String MOD_ID = "minemod";
    public static final String MOD_VERSION = "1.0";
}

```
{% endcode %}

Na nossa classe `Core` precisaremos declarar que ela é a nossa classe principal para o Forge, e como fazemos isso? Simples, colocando uma anotação fornecida pelo próprio Forge, e indicando as informações do nosso mod, anteriormente colocadas em `Env` .

A anotação em especifico é o **@Mod**, nela vai 3 parâmetros para colocarmos as nossas informações. Que são elas

1. **modid**: O id do nosso mod, que registramos em mcmod.info e build.gradle
2. **name**: O nome do nosso mod, que registramos em mcmod.info
3. **version**: A versão do nosso mod, por exemplo _1.0_

Sua classe deverá ficar assim, após os importes e as informações adicionadas:

{% code title="Core.java" %}
```java
package com.github.nxkoo.devmine.minemod;

import com.github.nxkoo.devmine.minemod.lib.Env;
import cpw.mods.fml.common.Mod;

@Mod(modid = Env.MOD_ID, name = Env.MOD_NAME, version = Env.MOD_VERSION)
public class Core {
    
}

```
{% endcode %}

Como eu expliquei anteriormente na seção de "[Fundamentos da Criação de Mods](../fundamentos-da-criacao-de-mods.md)" o forge tem 3 fases na sua composição, que são elas **preInit**, **init** e **postInit**, e precisamos registrá-las para podermos utilizar.

```java
public void preInit(FMLPreInitializationEvent $e) {

}

public void init(FMLInitializationEvent $e) {

}

public void postInit(FMLPostInitializationEvent $e) {
        
}
```

Mas ainda existe uma coisa a se fazer antes de irmos aos nossos **Proxies**, que é a **instância**. Na orientação a objetos, existem várias maneiras de acessar uma classe, mas para acessar uma classe diretamente, todas as suas funções e variáveis precisam ser estáticas. No entanto, se uma classe não possui variáveis estáticas, precisamos de uma instância para poder acessá-la por outras classes.

Então vamos criar a nossa instância. O próprio Forge disponibiliza uma anotação chamada **`@Instance`**, e é com ela que iremos criar a nossa instância. Para isso, basta criar uma variável pública e estática chamada `instance`, que retorna a própria classe, e depois colocarmos a anotação **`@Instance`**.

```java
@Mod.Instance
public static Core instance = new Core();
```

> Com isso podemos instanciar a nossa classe de qualquer outra parte do código.

Já dissemos ao Forge que esta classe é a classe principal do nosso mod, ele vai executar cada parte dessa classe, mas nada acontecerá, porque não tem funções ou qualquer coisa para ser executado nesses métodos. Então a próxima coisa que devemos fazer é a estrutura de proxy.

Código final:

```java
package com.github.nxkoo.devmine.minemod;

import com.github.nxkoo.devmine.minemod.lib.Env;
import cpw.mods.fml.common.Mod;
import cpw.mods.fml.common.event.FMLInitializationEvent;
import cpw.mods.fml.common.event.FMLPostInitializationEvent;
import cpw.mods.fml.common.event.FMLPreInitializationEvent;

@Mod(modid = Env.MOD_ID, name = Env.MOD_NAME, version = Env.MOD_VERSION)
public class Core {

    @Mod.Instance
    public static Core instance = new Core();

    public void preInit(FMLPreInitializationEvent $e) {

    }

    public void init(FMLInitializationEvent $e) {

    }

    public void postInit(FMLPostInitializationEvent $e) {

    }
}
```

Haha 😅 Ficou um pouco grande, né? Então irei abordar mais sobre Proxy no próximo tópico.
