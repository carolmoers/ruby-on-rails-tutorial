# Completando tarefas

Pra começar, vamos criar um método para atualizar o status da nossa tarefa para completo. Novamente no arquivo **tarefas_controller.rb**, vamos adicionar as linhas de código abaixo:

```ruby
	def completa_tarefa
	    @tarefa.completo = !@tarefa.completo

	    respond_to do |format|
	      if @tarefa.save
	        format.html { redirect_to tarefas_url, notice: 'uhuul, tarefa atualizada!' }
	        format.json { head :no_content }
	      else
	        format.html { redirect_to tarefas_url, notice: 'Algum erro aconteceu ao tentar finalizar a tarefa :(' }
	        format.json { head :no_content }
	      end
	    end
	  end
```

**Obs:** Você pode adicionar essa parte do código logo depois do método destroy, logo vamos explicar o que esse método faz.

Antes de explicarmos o código, temos que adicionar só mais uma coisa no arquivo **tarefas_controller.rb**, você deve ter uma linha parecida com a abaixo no seu arquivo:

```ruby
before_action :set_tarefa, only: [:show, :edit, :update, :destroy]
```

Substitua ela pela linha abaixo:

```ruby
before_action :set_tarefa, only: [:show, :edit, :update, :destroy, :completa_tarefa]
```

Com essa alteração, estamos dizendo que antes de chamar o método **completa_tarefa**, vamos chamar o método **set_tarefa**, como mostra abaixo:

```ruby
 def set_tarefa
    @tarefa = Tarefa.find(params[:id])
 end
```

Esse método, vai sempre procurar uma tarefa com o _identificador(params[:id])_ que mandamos para ele, e colocar dentro da variável _@tarefa_

### Agora vamos olhar de novo o método que criamos:

Então, antes de chamarmos esse métodos, já vimos que o método **set_tarefa** será chamado, que colocará uma Tarefa na variável _@tarefa_, que podemos ver na primeira linha do método.
Nessa linha, estamos alterando o valor do atributo completo da tarefa. Aqui temos algo novo:

```ruby
 @tarefa.completo = !@tarefa.completo
```

Estamos dizendo que **@tarefa.completo** vai receber a negação do valor atual dela mesma (@tarefa.completo), e isso se dá pelo uso da exclamação **(!)**, então, sempre que usarmos _‘!’_ na frente de algo, estamos dizendo que é a negação daquilo.

Após alterarmos o valor de **@tarefa.completo**, já iniciamos o código para retornar para o html. Isso fazemos com a linha **respond_to do |format|**, depois testamos se a tarefa foi salva com o valor novo, isso com a linha **if @tarefa.save**, caso isso ocorra, direcionamos para a tela principal, a **index**, ou **tarefas_url** (para o Rails):

```ruby
format.html { redirect_to tarefas_url, notice: 'uhuul, tarefa atualizada!' }
```

Caso não dê certo, direcionamos para a tela inicial também, com uma mensagem de erro:

```ruby
format.html { redirect_to tarefas_url, notice: 'Algum erro aconteceu ao tentar atualizar a tarefa :(' }
```

O método completo deve ficar assim:

```ruby
def completa_tarefa
    @tarefa.completo = !@tarefa.completo

    respond_to do |format|
      if @tarefa.save
        format.html { redirect_to tarefas_url, notice: 'uhuul, tarefa atualizada!' }
        format.json { head :no_content }
      else
        format.html { redirect_to tarefas_url, notice: 'Algum erro aconteceu ao tentar atualizar a tarefa :(' }
        format.json { head :no_content }
      end
    end
  end
```

### Com o método criado, vamos criar o link!

Assim para quando queremos excluir e atualizar, devemos criar um link para podermos alterar o estado da nossa tarefa. Primeiro, vamos criar uma rota nova. Você lembra do **routes.rb**?
Vamos adiconar a linha abaixo nele, pode ser bem abaixo de **resources :tarefas**

```ruby
get 'completar-tarefa/:id' => 'tarefas#completa_tarefa', as: 'completar_tarefa'
```

Essa linha cria uma nova rota, para podermos chegar no método **completar_tarefa** que criamos em **tarefas_controller.rb**.

Estamos dizendo que vamos chamar o controller **TarefasController**, na ação **completar_tarefa**, enviando um **id**, a identificação da tarefa no banco de dados.

Depois de criar a rota, vamos criar o link no html. Agora vamos ver mais uma coisa nova do Rails, as **Views**.

As views são basicamente o html onde vamos mostrar nossos dados, ou seja, o que o controller mandar para nós, é nas views que iremos mostrar.
Vamos abrir o arquivo **app/views/tarefas/index.html.erb**:

```ruby
<p id="notice"><%= notice %></p>
<h1>Listing Tarefas</h1>
<table>
  <thead>
    <tr>
      <th>Nome</th>
      <th>completo</th>
      <th colspan="3"></th>
    </tr>
  </thead>
  <tbody>
    <% @tarefas.each do |tarefa| %>
      <tr>
        <td><%= tarefa.nome %></td>
        <td><%= tarefa.completo %></td>
        <td><%= link_to 'Show', tarefa %></td>
        <td><%= link_to 'Edit', edit_tarefa_path(tarefa) %></td>
        <td><%= link_to 'Destroy', tarefa, method: :delete, data: { confirm: 'Are you sure?' } %></td>
      </tr>
    <% end %>
  </tbody>
</table>
<br>
<%= link_to 'New Tarefa', new_tarefa_path %>
```

#### Mas antes de criar o link… vamos entender umas coisinhas
Note que o arquivo não é total html, ele termina com extensão erb, que serve para que ele entenda código ruby. ,e para fazermos isso, usamos os seguintes sinais:

* `<%` \- que mostra que código ruby está começando
* `%>` \- que mostra que código ruby está terminando
* `<%= … %>` \- contém um código ruby que vai só mostrar algo, não executar

No index.html.erb, podemos ver isso acontecendo muito, como na linha abaixo:

```ruby
<p id="notice"><%= notice %></p>
```

Nessa linha temos um parágrafo em html, que irá mostrar a mensagem (variável notice) que vem da controller, lembra?

Temos também, outra coisa nova no **index.html.erb**, são os laços de repetição em ruby, podemos ver ele sendo iniciado no seguinte linha:

```ruby
<% @tarefas.each do |tarefa| %>
  <tr>
    <td><%= tarefa.nome %></td>
    <td><%= tarefa.completo %></td>
    <td><%= link_to 'Show', tarefa %></td>
    <td><%= link_to 'Edit', edit_tarefa_path(tarefa) %></td>
    <td><%= link_to 'Destroy', tarefa, method: :delete, data: { confirm: 'Are you sure?' } %></td>
  </tr>
<% end %>
```

Note que nessa linha usamos o **<%** para iniciar o laço de repetição. Mas então, o que isso faz?
**@tarefas** é uma lista, então estamos iterando cada item da lista e criando uma nova variável, chamada tarefa, após, dentro da **<tr>**, estamos mostrando os dados dessa tarefa, e criando os links para atualizar, excluir, e mostrar ela. Finalizando o laço de repetição com a linha **<% end %>**
