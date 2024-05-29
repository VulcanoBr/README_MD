# Params.merge (definição IA)

- O método `merge` em Ruby é utilizado para combinar dois hashes, criando um novo hash que 
contém as chaves e valores de ambos os hashes originais. Se houver chaves duplicadas, 
os valores do hash que está sendo mesclado (`merge`d) sobrescreverão os valores do 
hash original.

Vamos ilustrar com um exemplo básico de uso de `merge`:

### Exemplo Básico de `merge`

```ruby
hash1 = { a: 1, b: 2 }
hash2 = { b: 3, c: 4 }

result = hash1.merge(hash2)

puts result
# Output: {:a=>1, :b=>3, :c=>4}
```

Neste exemplo:
- `hash1` é `{ a: 1, b: 2 }`
- `hash2` é `{ b: 3, c: 4 }`
- O resultado da operação `hash1.merge(hash2)` é `{ a: 1, b: 3, c: 4 }`, onde o valor da chave `b` no `hash2` sobrescreveu o valor da mesma chave em `hash1`.

### Aplicação no Contexto do Devise e Rails

No contexto da aplicação Rails com Devise, vamos ver como `merge` é usado no exemplo 
do controlador:

```ruby
class PostsController < ApplicationController
  def update
    @post = Post.find(params[:id])
    if @post.update(post_params.merge(updated_by: current_user))
      redirect_to @post, notice: 'Post was successfully updated.'
    else
      render :edit
    end
  end

  private

  def post_params
    params.require(:post).permit(:title, :content)
  end
end
```

### Explicação Detalhada

1. **`post_params` Method:**
   ```ruby
   def post_params
     params.require(:post).permit(:title, :content)
   end
   ```
   Este método retorna um hash dos parâmetros permitidos para o modelo `Post`. 
   Suponha que `params[:post]` contenha `{ title: "New Title", content: "New Content" }`. 
   Então, `post_params` retornará `{ title: "New Title", content: "New Content" }`.

Vamos ilustrar com um exemplo básico de uso de `merge`:

### Exemplo Básico de `merge`

```ruby
hash1 = { a: 1, b: 2 }
hash2 = { b: 3, c: 4 }

result = hash1.merge(hash2)

puts result
# Output: {:a=>1, :b=>3, :c=>4}
```

Neste exemplo:
- `hash1` é `{ a: 1, b: 2 }`
- `hash2` é `{ b: 3, c: 4 }`
- O resultado da operação `hash1.merge(hash2)` é `{ a: 1, b: 3, c: 4 }`, onde o valor da chave `b` no `hash2` sobrescreveu o valor da mesma chave em `hash1`.

### Aplicação no Contexto do Devise e Rails

No contexto da aplicação Rails com Devise, vamos ver como `merge` é usado no exemplo do controlador:

```ruby
class PostsController < ApplicationController
  def update
    @post = Post.find(params[:id])
    if @post.update(post_params.merge(updated_by: current_user))
      redirect_to @post, notice: 'Post was successfully updated.'
    else
      render :edit
    end
  end

  private

  def post_params
    params.require(:post).permit(:title, :content)
  end
end
```

### Explicação Detalhada

1. **`post_params` Method:**
   ```ruby
   def post_params
     params.require(:post).permit(:title, :content)
   end
   ```
   Este método retorna um hash dos parâmetros permitidos para o modelo `Post`. Suponha que `params[:post]` contenha `{ title: "New Title", content: "New Content" }`. Então, `post_params` retornará `{ title: "New Title", content: "New Content" }`.

2. **`merge` para Adicionar `current_user`:**
   ```ruby
   @post.update(post_params.merge(updated_by: current_user))
   ```
   Aqui, `post_params` é um hash contendo os parâmetros permitidos. `current_user` é o usuário atualmente logado, que queremos associar à atualização do post.
   
    - O método `merge` em Ruby é utilizado para combinar dois hashes, criando um 
      novo hash que contém as chaves e valores de ambos os hashes originais. 
      Se houver chaves duplicadas, os valores do hash que está sendo 
        mesclado (`merge`d) sobrescreverão os valores do hash original.
    - No método post_params, você não precisa incluir :updated_by porque estamos adicionando 
      esse  parâmetro explicitamente no controlador com merge. O método permit é usado para filtrar os parâmetros que vêm diretamente do formulário enviado pelo usuário. Quando você usa merge, você está adicionando manualmente parâmetros adicionais que não precisam passar por permit. 

   O método `merge` combina esses dois hashes:
   
   - `post_params` retorna `{ title: "New Title", content: "New Content" }`
   - `updated_by: current_user` é `{ updated_by: current_user }`

   O resultado de `post_params.merge(updated_by: current_user)` será:
   ```ruby
   { title: "New Title", content: "New Content", updated_by: current_user }
   ```

### Exemplo Passo a Passo

Se `current_user` for um usuário com o ID 1, por exemplo:

1. `post_params` retorna `{ title: "New Title", content: "New Content" }`
2. `merge(updated_by: current_user)` adiciona `{ updated_by: current_user }` ao hash, resultando em:
   ```ruby
   { title: "New Title", content: "New Content", updated_by: #<User id: 1> }
   ```

Quando `@post.update` é chamado, ele tenta atualizar o registro `@post` no banco de dados com os atributos fornecidos pelo hash resultante.

### Considerações Finais

Usar `merge` dessa maneira permite que você adicione informações adicionais ao conjunto de parâmetros antes de enviar esses dados ao modelo para atualização. Isso é especialmente útil quando você precisa adicionar atributos que não são diretamente provenientes do formulário do usuário, como o usuário que está fazendo a atualização (`current_user`).

2. **`merge` para Adicionar `current_user`:**
   ```ruby
   @post.update(post_params.merge(updated_by: current_user))
   ```
   Aqui, `post_params` é um hash contendo os parâmetros permitidos. `current_user` 
   é o usuário atualmente logado, que queremos associar à atualização do post. 
   O método `merge` combina esses dois hashes:
   
   - `post_params` retorna `{ title: "New Title", content: "New Content" }`
   - `updated_by: current_user` é `{ updated_by: current_user }`

   O resultado de `post_params.merge(updated_by: current_user)` será:
   ```ruby
   { title: "New Title", content: "New Content", updated_by: current_user }
   ```

### Exemplo Passo a Passo

Se `current_user` for um usuário com o ID 1, por exemplo:

1. `post_params` retorna `{ title: "New Title", content: "New Content" }`
2. `merge(updated_by: current_user)` adiciona `{ updated_by: current_user }` ao hash, 
    resultando em:
   ```ruby
   { title: "New Title", content: "New Content", updated_by: #<User id: 1> }
   ```

Quando `@post.update` é chamado, ele tenta atualizar o registro `@post` no banco de dados 
com os atributos fornecidos pelo hash resultante.

### Considerações Finais

Usar `merge` dessa maneira permite que você adicione informações adicionais ao conjunto d
e parâmetros antes de enviar esses dados ao modelo para atualização. 
Isso é especialmente útil quando você precisa adicionar atributos que não são diretamente 
provenientes do formulário do usuário, como o usuário que está fazendo a 
atualização (`current_user`).