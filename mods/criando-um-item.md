---
description: Neste tópico iremos finalmente configurar e criar o nosso primeiro item.
---

# ⚔️ Items

## O que é um item?

Item pode ser qualquer coisa, desde uma maçã até uma espada. No Minecraft, existe uma classe principal chamada **`Item`**. Esta classe é responsável por estruturar um item no jogo, definindo métodos e atributos como [`maxStackSize`](#user-content-fn-1)[^1], [`maxDamage`](#user-content-fn-2)[^2] e entre outros.

A classe **`Item`** também é responsável por definir em qual **`CreativeTab`** o item ficará. Existem muitas "tabs" na versão 1.7.10, como `tabCombat`, `tabFood`, `tabRedstone`, `tabTools`, entre outras. E você pode criar a sua própria, ou apenas colocar o seu item em uma das existentes.

Itens como espadas, comidas e ferramentas, todos eles estendem da classe principal **`Item`**. Existem classes como **`ItemFood`**, **`ItemSword`** e **`ItemArmor`**, que são classes mais específicas pois determinam os tipos específicos para seu próprio objetivo. Por exemplo, a **`ItemSword`** possui métodos e variáveis específicas para uma espada no Minecraft.

Todavia, existem classes ainda mais específicas, como **`ItemBed`** (Cama), **`ItemAxe`** (Machado), etc. Todas elas estendem da classe "Pai", que é a classe **`Item`**, ou seja, todas elas herdam os métodos e variáveis da classe **`Item`**.

***

## Criando o nosso primeiro item

Antes de tudo, você irá precisar da textura que eu criei para esta aula, você pode baixar abaixo, e se quiser também pode modificá-la.

{% file src="../.gitbook/assets/amethyst_sword.png" %}

### Estrutura Inicial

Começaremos criando um novo pacote chamado _item_ e, logo após, a classe **`AmethystSword`**, que será o nosso primeiro item, uma espada. Nesta classe, iremos estender uma outra classe chamada **`ItemSword`**, que contém funcionalidades específicas para espadas.

```java
package com.github.nxkoo.devmine.minemod.item;

import net.minecraft.item.ItemSword;

public class AmethystSword extends ItemSword {
    // O nome do parâmetro no seu código será "p_i45356_1_"
    public AmethystSword(ToolMaterial material, String unlocalizedName) { 
        super(material);                      
    }
}
```

#### Construtor da Classe

O construtor da classe **`AmethystSword`** precisa de um **`ToolMaterial`** como parâmetro, que define o material da espada, e uma **`String`** com o nome `unlocalizedName`. Detalhe importante: no método `super()`, passaremos apenas o parâmetro `material`.

#### Atribuindo Valores Importantes

Depois de definir o construtor, precisamos atribuir alguns valores essenciais à nossa espada. Esses valores configuram a textura, o nome e a aba criativa em que o item aparecerá.

**Configurações Essenciais**

* **setTextureName**: Método responsável por especificar onde a textura está localizada.
* **setUnlocalizedName**: Método responsável por definir o nome do item. Lembre-se de que o nome deve estar em minúsculas, e se for um nome composto, deve ser separado por underscores `_`.
* **setCreativeTab**: Define em qual aba do inventário criativo o item será colocado.

#### Exemplo Completo

A sua classe **`AmethystSword`** com todas as configurações necessárias deve ficar assim:

```java
package com.github.nxkoo.devmine.minemod.item;

import net.minecraft.creativetab.CreativeTabs;
import net.minecraft.item.ItemSword;

public class AmethystSword extends ItemSword {
    // O nome do parâmetro no seu código será "p_i45356_1_"
    public AmethystSword(ToolMaterial material, String unlocalizedName) { 
        super(material);  
        this.setCreativeTab(CreativeTabs.tabCombat);
        this.setTextureName(Env.MOD_ID + ":" + unlocalizedName);
        this.setUnlocalizedName(unlocalizedName);
    }
}
```

#### Explicação dos Métodos

* **this.setCreativeTab(CreativeTabs.tabCombat)**:
  * Coloca a espada na aba de combate do inventário criativo.
* **this.setTextureName(Env.MOD\_ID + ":" + unlocalizedName)**:
  * Define o caminho da textura do item. Neste método, ele tentará encontrar a textura na pasta `resources/assets/seuModID/textures/items`. Portanto, a sua textura deve estar lá. Por isso, passamos o `mod_id` e o `":"` para especificar onde exatamente procurar, por exemplo, "minemod" seria _`"minemod:amethyst_sword"`_. Ele vai procurar exatamente essa textura, e o `.png` não precisa ser incluído no nome.
* **this.setUnlocalizedName(unlocalizedName)**:
  * Define o nome não-localizado do item, usado internamente pelo Minecraft para identificar o item. Esse nome é utilizado no código e pode ser referenciado em arquivos de tradução para suportar múltiplos idiomas.

### Lidando com os itens

Depois de ter criado a estrutura inicial, precisamos agora iniciá-los e registrá-los no Minecraft. Vamos primeiro lidar com a iniciação deles.

Para isso, precisamos criar uma nova classe chamada **`ItemHandler`**. Este será o nosso gerenciador de itens, ou seja, ele vai lidar com todas as inicializações dos itens. Esta classe estará localizada em um pacote _handlers_ e iremos criar um novo método `init()` que será público e estático e retornará `void`.

```java
package com.github.nxkoo.devmine.minemod.handlers;

public class ItemHandler {
    public static void init() {
        // Aqui ficará a inicialização dos itens.
    }
}
```

### Inicialização dos Itens

Agora precisamos registrar os itens, e isso pode ser feito dentro do método `init()`. Começaremos primeiro instanciando a classe que acabamos de criar, **`AmethystSword`**, Em uma variável pública e estática `amethystSword`.&#x20;

```java
public static AmethystSword amethystSword;
```

No método `init()`, iremos inicializar essa variável. Entretanto, ela precisará de um `ToolMaterial`, e para isso vamos precisar de outra variável instanciando o `ToolMaterial`. Vamos inicializá-la imediatamente, utilizando a classe `EnumHelper` e o método `addToolMaterial()`, que nos ajudará a criar esse material.

***

#### Mas antes disso precisamos saber o que é um Tool Material

Um **Tool Material** define as propriedades de uma ferramenta, como durabilidade, eficiência de mineração, nível de mineração e encantabilidade. Os parâmetros aceitos são:

1. `name`: Nome do novo material.
2. `harvestLevel`: Nível de colheita (0 = madeira, 1 = pedra, 2 = ferro, 3 = diamante, etc.).
3. `maxUses`: Durabilidade máxima.
4. `efficiency`: Velocidade de mineração.
5. `damage`: Dano de ataque adicional.
6. `enchantability`: Facilidade de encantamento.

***

Agora que você sabe o que é um Tool Material, podemos criar o nosso. Podemos deixar a nossa variável como privada, estática e final para indicar que é uma constante. E utilizamos o EnumHelper para criar o nosso material.

```java
private static final Item.ToolMaterial AMETHYST_MATERIAL = EnumHelper.addToolMaterial("AMETHYST_MATERIAL", 3, 1561, 8.0F, 77.7F, 10);
```

Com a variável criada,  no método `init()` iremos iniciar a nossa **`AmethystSword`**. Para isso basta atribuir a ela uma nova instancia de **`AmethystSword`**, passando o `AMETHYST_MATERIAL` e o `unlocalizedName`, que nesse caso será "**amethyst\_sword"**.

```java
amethystSword = new AmethystSword(AMETHYST_MATERIAL, "amethyst_sword");
```

Logo após precisamos registrar este Item no Minecraft, e para isso o Forge tem uma método específico `registerItem()` que é um método estático que vem da classe **`GameRegistry`** e ele recebe dois paramêtros que é o próprio item e o nome "não-localizado".

```java
GameRegistry.registerItem(amethystSword, amethystSword.getUnlocalizedName().substring(5));
```

Eu utilizo o método `substring(5)` para remover o prefixo "item." do nome não localizado (unlocalized name) do item. O nome não localizado é tipicamente algo como "item.amethyst\_sword", onde "item." é um prefixo padrão adicionado pelo Minecraft para todos os itens. Ao usar `substring(5)`, você está removendo os primeiros cinco caracteres ("item."), resultando em "amethyst\_sword", que é o nome mais limpo e apropriado para registrar o item.&#x20;

{% code title="ItemHandler.java" %}
```java
package com.github.nxkoo.devmine.minemod.handlers;

import com.github.nxkoo.devmine.minemod.item.AmethystSword;
import net.minecraft.item.Item;
import net.minecraftforge.common.util.EnumHelper;

public class ItemHandler {
    public static AmethystSword amethystSword;
    private static final Item.ToolMaterial AMETHYST_MATERIAL = EnumHelper.addToolMaterial("AMETHYST_MATERIAL", 3, 1561, 8.0F, 77.7F, 10);
    public static void init() {
        amethystSword = new AmethystSword(AMETHYST_MATERIAL, "amethyst_sword");
        GameRegistry.registerItem(amethystSword, amethystSword.getUnlocalizedName().substring(5));
    }
}
```
{% endcode %}

### Registrando o Item no ClientProxy

Como o título já diz, iremos agora registrar o item no **`ClientProxy`**, para que ele seja registrado no Minecraft. Para isso, precisamos primeiro ir ao **`ClientProxy`** e chamar o nosso método `init()` de **`ItemHandler`** no método `preInit()`, pois queremos que o item seja inicializado antes mesmo de entrar no jogo e que seja registrado apenas pela parte do cliente.

```java
import com.github.nxkoo.devmine.minemod.handlers.ItemHandler;

@Override
public void preInit(FMLPreInitializationEvent $e) {
    super.preInit($e);
    ItemHandler.init();
}
```

### Adicionando a Textura para o Item

Para adicionar a textura ao seu item, siga estas etapas:

1.  **Estrutura de Pastas**: Certifique-se de que a estrutura de pastas esteja correta. Crie as seguintes pastas no diretório do seu mod:

    ```
    /resources/assets/MODID/textures/items/
    ```

    Substitua `MODID` pelo ID do seu mod.
2.  **Adicionar a Textura**: Coloque a imagem da textura do item, por exemplo, `amethyst_sword.png`, dentro da pasta `items`. O caminho completo deve ser:

    ```
    /resources/assets/MODID/textures/items/amethyst_sword.png
    ```

{% hint style="warning" %}
O caminho sempre vai ser "_assets/modid/textures/items_" para a textura dos seus itens!
{% endhint %}

### Adicionando o nome para o Item

Para garantir que seu item tenha o nome correto exibido no jogo, você precisa criar um arquivo `.lang` na pasta _**lang**_. Na mesma estrutura de pasta de antes, antes de _**textures/items**_, você criará um diretório chamado _**lang**_ e criará um arquivo chamado `en_US.lang` e nele colocará:

```erlang
item.amethyst_sword.name=§5Amethyst Sword
```

Pronto agora seu Item está pronto para uso. 🎊

[^1]: 

    Quantidade que o item pode ser armazenado no inventário. Por exemplo, uma <mark style="color:yellow;">maçã dourada</mark> pode ser armazenada em pilhas de até 64 itens no mesmo slot, enquanto uma <mark style="color:green;">ender pearl</mark> pode ser armazenada apenas em pilhas de até 16. \


    O valor inicial de `maxStackSize` é 64, mas você pode alterá-lo.

[^2]: Dano máximo que um item pode suportar.
