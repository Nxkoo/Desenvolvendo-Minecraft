# 🕹️ Configurando o mod no IntelliJ

Hahah achou que já sairia programando? Quase isso! Vamos então iniciar o **IntelliJ IDEA** e iniciar a nossa aventura nesse mundo 😉

Abra o seu IntelliJ, clique em `Open`, e localize a pasta que baixamos e configuramos. (forge-1.7.10-10.13.4.1614-1.7.10-src)

<figure><img src="../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

Após ter aberto deverá iniciar automaticamente o download do Gradle, e sua pasta ficará dessa maneira

<figure><img src="../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

Com seu gradle instalado e seu arquivo aberto no IntelliJ, podemos começar a configurar algumas coisas antes de irmos para o código.

Uma coisa importante para mencionar, o modID (explicado anteriormente em [Fundamentos da Criação de Mods](fundamentos-da-criacao-de-mods.md)) ele será usado no nosso package[^1], e também é o mesmo colocado no `build.gradle` e no `mcmod.info`, não se esqueça de alterar nos dois.

Caso não se lembre, no build.gradle atualizamos para uma versão mais recente, porém você não mexeu em nada, apenas copiou e colou, já agora devemos alterar para o nosso próprio mod, colocando as informações especificas. Aqui vai um exemplo:

```gradle
version = "1.0"
group= "com.nxkoo.devmine.minemod"
archivesBaseName = "minemod"
```

O `minemod` é o nosso modid, e todo o resto em `group`, é o nossa package[^2] que devemos alterar também no nosso projeto no IntelliJ.

Voltando ao mcmod.info, devemos altera-lo colocando as informações. Um outro exemplo seria:

```
[
{
  "modid": "minemod",
  "name": "DesenvolvendoMinecraftMod",
  "description": "Mod criado para o livro 'desenvolvendo minecraft'.",
  "version": "${version}",
  "mcversion": "${mcversion}",
  "url": "",
  "updateUrl": "",
  "authorList": ["NykooX"],
  "credits": "Agradecimentos ao Mestre Nykoo",
  "logoFile": "",
  "screenshots": [],
  "dependencies": []
}
]

```

Depois de atualizar seu build.gradle e seu mcmod.info, podemos finalmente alterar a nossa ultima coisa, que é o package do nosso mod. Atualmente o nosso package está `com.example.examplemod` e devemos alterar para como registramos no build.gradle `com.github.nxkoo.devmine.minemom`

Para poder renomear no IntelliJ, basta selecionar o arquivo e apertar as seguintes teclas: Shift + F6 e alterar.

<figure><img src="../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

Com tudo alterado, seu projeto deverá ficar dessa forma.

<figure><img src="../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

Aeee terminamos essa parte de configuração que crucial para o desenvolvimento de qualquer tipo de projeto, é como eu costumo falar.

> O básico bem feito é melhor que um avançado mal feito.
>
> &#x20;                                                                                           <mark style="color:red;">Nykoo.</mark>

[^1]: pacote

[^2]: pacote
