# Agora, vamos começar a criar nossa to do list

No terminal, escreva o comando abaixo:

```sh
rails generate scaffold Tarefa nome:string completo:boolean
```
Esse comando vai criar uma série de arquivos que já vão possibilitar a criação, atualização e exclusão de tarefas.

No terminal você verá algo como a imagem abaixo, estes são todos os arquivos que ele cria. Neles estão incluídos os arquivos com código ruby, que faŕa tudo funcionar, e também com HTML, que é o que veremos no navegador.

![Arquivos](images/6_iniciando_a_to_do_list/arquivos_to_do_list.png)

### Verificando se tudo está funcionando

Vamos ver o que temos aparece no navegador agora, no terminal digite:

```sh
rails server
```

E no navegador:

```
localhost:3000
```

![Erro](images/6_iniciando_a_to_do_list/erro.png)

Ooops, algo estranho aconteceu. Esse é o nosso primeiro erro, sempre que algo não estiver correto, o Rails irá avisar a gente com uma tela parecida com a da imagem, informando o erro que está acontecendo.

Como o idioma do Rails é inglês, essas mensagens serão em inglês, mas você sempre pode usar o Google Tradutor, se precisar.

### Ok, mas como resolver?

O que o Rails está nos dizendo é que nós criamos a Tarefa, mas não dissemos como e onde vamos salvá-la. A mensagem do início “Migration are pending”, significa que criamos um arquivo, dizendo o que criar no banco de dados, mas não executamos ele. Vamos fazer isso então, no terminal digite:

```sh
rake db:migrate
```

Esse comando, diz para o Rails executar todas as migrações que criamos, esse arquivos foi criado ao executarmos o comando **“rails generate scaffold Tarefa nome:string completo:boolean”**, que criou aquele monte de arquivos pra gente, lembra?

### Vamos ver o que aparece no navegador agora?

```sh
rails server
```

E no navegador:

```
localhost:3000
```

![To-do list funcionando](images/6_iniciando_a_to_do_list/funcionando.png)

Lindo!! Apareceu a tela de que indica que tudo está funcionando de novo! :D

Ok, mas onde estão as nossas tarefas?
