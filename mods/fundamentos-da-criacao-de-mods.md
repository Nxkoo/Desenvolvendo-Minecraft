---
description: >-
  Neste capítulo , vamos explorar os conceitos básicos e a estrutura de um mod.
  Também criaremos nosso primeiro mod simples para que você possa entender como
  tudo funciona na prática.
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# 🔗 Fundamentos da Criação de Mods

Agora que você já instalou e configurou todas as ferramentas necessárias, vamos conhecer alguns conceitos importantes sobre a criação de mods.

### Estrutura Básica de um Mod

Para começar, é importante entender a estrutura básica de um mod no Minecraft (ao menos na versão 1.7.10). Quando você cria um mod usando o Forge, ele segue uma estrutura específica de diretórios e arquivos. Aqui estão os componentes principais:

* **build.gradle**: O arquivo de configuração do Gradle, que gerencia as dependências e a construção do projeto.
* **src/main/java**: O diretório onde você colocará todo o código-fonte Java do seu mod.
* **src/main/resources**: O diretório para recursos como texturas, arquivos de idioma e outros arquivos necessários para o mod.

### O Ciclo de Vida de um Mod

Entender o ciclo de vida de um mod é crucial para saber quando e onde inicializar suas funcionalidades, por exemplo, quando um mod está sendo iniciado, quando já iniciou e até mesmo antes de iniciar.&#x20;

Resumindo o Forge tem 3 fases na sua composição, que são elas, **preInit**, **init** e **postInit,** utilizadas para antes de inicializar o mod, quando inicializa e após inicializar, respectivamente.

* **preInit**: Usado para carregar configurações, registrar itens e blocos, e outras tarefas iniciais.
* **init**: Usado para registrar renderizações, eventos, e outros elementos que dependem dos recursos carregados em preInit.
* **postInit**: Usado para tarefas que dependem de outros mods estarem completamente carregados.

Entretanto não se preocupe com isso por agora, irei explicar mais tarde como devemos e utilizaremos esses métodos (com exemplos).

## Conceitos Importantes

Eu considero alguns conceitos cruciais para a criação de mods, mas eu irei apenas falar sobre 3 por enquanto, que são eles: modId, proxies e eventos. Estarei explicando brevemente sobre cada um deles.

#### 1. ModID&#x20;

O `modid` é um identificador único para o seu mod. Ele deve ser único para evitar conflitos com outros mods. Normalmente, é uma versão em minúsculas e sem espaços do nome do seu mod.

#### 2. Proxy

Você pode usar o proxy para separar o código do lado do servidor e do lado do cliente. O proxy pode ser usado para registrar coisas que precisam ser registradas apenas no lado do cliente ou do servidor e vice-versa. Existem 3 tipos de proxy e são eles:

* **CommonProxy**: será usado tanto no lado servidor quanto no lado do cliente.
* **ClientProxy**: será usado apenas no lado do cliente.
* **ServerProxy**: será usado apenas no lado do servidor.

#### 3. Eventos

O Forge ou melhor até mesmo o Minecraft, usam sistemas de eventos para controlar as ações do jogo, eles operam através de acontecimentos/eventos respondendo situações como, blocos sendo quebrados, itens sendo usados, jogadores entrando no jogo e entres outros. No forge você pode até mesmo criar seus próprios eventos, para manipular o jogo conforme a sua vontade.&#x20;



Agora que você já sabe os fundamentos de um mod, podemos começar a criação do nosso mod. 😉🎉🎊
