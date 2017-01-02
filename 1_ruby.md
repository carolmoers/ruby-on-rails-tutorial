# Agora sim, vamos falar de ruby?

Como já comentei, o Ruby on Rails é feito com a linguagem Ruby. Então, antes de começarmos a programar  , é legal entendermos algumas coisas básicas do ruby.
Durante o desenvolvimento, vamos ver coisas variáveis, array, métodos, etc. Então é legal darmos uma olhada em o que são cada um desses nomes e como podemos criar eles :)

## Tipos básicos no Ruby

Nas variáveis que guardamos nossos dados e eles podem ser de vários tipos:

* Palavras ou frases: **String**
* Números inteiros: **Integer**
* Números decimais: **Float**
* Valores lógicos (verdadeiro ou falso): **True** e **False**
* Lista de valores: **Array**

### Palavras ou frases

**Strings** sempre estarão entre aspas, podendo ser duplas:

```ruby
projeto = “Projeto Tutoras”
```

Ou aspas simples:

```ruby
projeto = “Projeto Tutoras”
```

### Números inteiros e decimais

**Integers** são números inteiros:

```ruby
numero_de_aprendizes = 100
```

**Floats** são números decimais:

```ruby
horas_de_aprendizado = 4.5
```

Sendo `4,5` o valor no exemplo, pois o Ruby representa esses valores com ponto.

**Obs**: Um ponto importante pra citar aqui, é sobre o nome que damos às
variáveis: elas não devem conter espaços, como podemos ver nas variáveis criadas
aqui o espaço foi substituído por *underline* (\_).

### Lógicos

Os valores lógicos, chamados de **Booleanos**, representam verdadeiro e falso.

```ruby
tutora_feliz = true
```

‘**True**’ é verdadeiro em inglês, idioma que a linguagem ruby utiliza.

```ruby
tutora_triste = false
```

‘**False**’ é falso em inglês.

### Listas de dados

As listas de dados são chamados de **Array** e serve para armazenarmos valores de
vários tipos:

Palavras ou frases:

```ruby
nomes_das_tutoras = [“Carol”, “Ana”, “Joana”]
```

Números:

```ruby
idades_das_tutoras = [23, 20, 35]
```

E tudo junto:

```ruby
dados = [10, true, "Carol"]
```

### Métodos

São uma forma de agrupar um conjunto de instruções, como se fosse uma receita
que podemos executar utilizando seu nome. Podem receber e retornar valores.

```ruby
def escrever_nome(nome)
  "Seu nome é " + nome
end
```

Ok, mas o que significa tudo isso?

* `def` \- estamos dizendo que estamos definindo um método
* `escrever_nome` \- esse é o nome do nosso método. note que nele subtituímos
  os espaços por traços (\_)
* `(nome)` \- é o parâmetro do nosso método, uma variável que mandamos para o
  método, para que ele faça algo com ela. Métodos podem receber nenhum, um ou
  mais paramêtros.
* `“Seu nome é #{nome}”` \- é o que o método vai retornar para a gente,
  note que usamos o paramêtro nome na frase
* `end` \- estamos dizendo que estamos finalizando o método

Assim o método retornaria `"Seu nome é Carol"` e `texto` agora tem essa frase
como valor.

Podemos agora utilizar o método `print` já disponibilizado pelo Ruby para
"imprimir" a frase na linha de comando:

```ruby
texto = escrever_nome("Carol")
print(texto)
```

### Controle de fluxo

Até então escrevemos código que é executado sequenciamente e nesta seção
mostraremos uma forma de controlar o fluxo do programa, a partir de alguma
condição. Com isso poderemos realizar decisões durante a execução da nossa
aplicação.

Por exemplo, vamos imprimir no método `escrever_nome` criado na seção anterior
apenas se o nome não estiver em branco.

```ruby
if nome != ''
  "Seu nome é " + nome
end
```

Outra forma de implementar seria utilizando o método `empty?`

```ruby
if !nome.empty?
  "Seu nome é " + nome
end
```

E nosso método ficaria assim:

```ruby
def escrever_nome(nome)
  if !nome.empty?
    "Seu nome é " + nome
  end
end
```

### Laço de repetição

Em algumas situações precisamos repetir um operação em elementos de um conjunto
de dados e podemos realizar tal tarefa utilizando laços.

Por exemplo, vamos podemos escrever os nomes de uma lista utilizando o `for`:

```ruby
lista_de_nomes = ["Juliana", "Enzo", "Roberto"]

for nome in lista_de_nomes
  escrever_nome(nome)
end

# Note que estamos utilizando o método escrever_nome do exemplo anterior.
```

### Comentários

São partes do código que não serão executados, podem ser usados pra lembrar de
algo naquela parte do código, por exemplo. São muito bons quando estamos
aprendendo, pois podemos comentar o que o código está fazendo:

```ruby
# Este é um comentário que não é executado

def linguagem_de_programacao
  "Ruby"
end
```

Para criarmos um comentário, iniciamos a frase com ‘#’, assim, o ruby sabe que
ali tem um comentário e ele não precisa executar nada.

### Onde aprender mais sobre Ruby?

Abaixo, alguns links que podem ajudar a ver mais sobre ruby, e a treinar um
pouquinho também :)

* [https://www.codecademy.com/pt-BR/courses/ruby-beginner-pt-BR](https://www.codecademy.com/pt-BR/courses/ruby-beginner-pt-BR)
* [http://howtocode.com.br/ebooks/ruby](http://howtocode.com.br/ebooks/ruby)
* [http://tryruby.org/levels/1/challenges/0](http://tryruby.org/levels/1/challenges/0)
  está em inglês, mas é um tutorial muito legal para experimentar a linguagem
