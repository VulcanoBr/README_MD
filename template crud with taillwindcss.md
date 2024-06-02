## Utilizando os Templates Customizados para Ruby on Rails

Com esses templates configurados com formatação TailwindCSS, ao rodar o comando scaffold, Rails usará os templates personalizados `index.html.erb`, edit.html.erb`, `new.html.erb`, `\_form.html.erb`e`showhtml.erb`. Para gerar um scaffold com os novos templates, utilize o comando scaffold normalmente:

```erb
rails generate scaffold User name:string age:integer birthday:date bio:text height:float price:decimal payment:float date_time: datetime agree_terms:boolean
```

### Passo a Passo:

**Crie a estrutura de diretórios para os templates personalizados:**

    No seu projeto Rails, crie a seguinte estrutura de diretórios:

    ```bash
    mkdir -p lib/templates/erb/scaffold

**Crie o template para a view `index`:**

    Dentro do diretório `lib/templates/erb/scaffold`, crie um arquivo chamado `index.html.erb`, ou atualize o existente: com o seguinte conteúdo:

### `index.html.erb` com icon para action edit, show, delete

```erb
<div class="w-full lg:w-12/12 flex justify-between items-center mt-3 mb-4">
  <h1 class="text-2xl font-bold">Listing <%= plural_table_name.titleize %></h1>
  <%%= link_to 'New <%= singular_table_name.titleize %>', new_<%= singular_table_name %>_path, class: "inline-block px-4 py-2 bg-blue-500 text-white rounded-md" %>
</div>

<table class="min-w-full bg-white border border-gray-300">
  <thead>
    <tr>
      <% attributes.reject(&:password_digest?).each do |attribute| -%>
        <th class="px-4 py-2 border-b"><%= attribute.human_name %></th>
      <% end -%>
      <th class="px-4 py-2 border-b">Actions</th>
    </tr>
  </thead>
  <tbody>
    <%% @<%= plural_table_name %>.each do |<%= singular_table_name %>| %>
      <tr>
        <% attributes.reject(&:password_digest?).each do |attribute| -%>
          <td class="px-4 py-2 border-b"><%%= <%= singular_table_name %>.<%= attribute.name %> %></td>
        <% end -%>
        <td class="flex justify-between">
          <%%= link_to edit_<%= singular_table_name %>_path(<%= singular_table_name %>), title: "Edit", alt: "edit"  do %>
              <%%= image_tag "icons/gray/edit.svg" %>
          <%% end %>

          <%%= link_to <%= singular_table_name %>, title: "Show", alt: "eye"  do %>
            <%%= image_tag "icons/gray/eye.svg" %>
          <%% end %>

          <%%= button_to <%= singular_table_name %>, method: :delete, data: {
                turbo_method: :delete, turbo_confirm: 'Are you sure?' },
                class: "text-red-500 hover:underline", title: "Delete", alt: "delete"   do  %>
            <%%= image_tag "icons/gray/close.svg" %>
          <%% end %>
        </td>
      </tr>
    <%% end %>
  </tbody>
</table>
```

#### Explicação do Código

1. **Div com Flexbox**: Utiliza uma div com `flex justify-between items-center mb-4` para criar um layout flexível que alinha o título e o botão "New" horizontalmente.
2. **Título e Botão**: O título (`<h1>`) e o link "New" estão dentro desta div, ficando alinhados lado a lado.
3. **Tabela**: A tabela permanece a mesma, listando os atributos e ações.

## OBS:

- Colocar os icons para Tailwindcss com extensão svg no caminho "assets/images/icons/gray"
- Opção para ter o codigo com texto para action edit, show, delete; subistituir por :

```erb
<%%= link_to 'Show', <%= singular_table_name %>, class: "ml-4 text-blue-500 hover:underline" %> |
<%%= link_to 'Edit', edit_<%= singular_table_name %>_path(<%= singular_table_name %>), class: "ml-4  text-blue-500 hover:underline" %> |
<%%= link_to 'Destroy', <%= singular_table_name %>, method: :delete, data: {
                turbo_method: :delete, turbo_confirm: 'Are you sure?' },
                class: "text-red-500 hover:underline" %>
```

**Crie o template para a view `new`:**

    Dentro do diretório `lib/templates/erb/scaffold`, crie um arquivo chamado `new.html.erb`, ou atualize o existente: com o seguinte conteúdo:

### `new.html.erb`

```erb
<h1 class="text-2xl font-bold mb-4">New <%= singular_table_name.titleize %></h1>

<%%= render 'form', <%= singular_table_name %>: @<%= singular_table_name %> %>

```

#### Explicação do Código

1. **new.html.erb**:
   - Exibe um título indicando que um novo registro está sendo criado.
   - Renderiza o partial `_form.html.erb` passando o objeto do modelo.

**Crie o template para a view `edit`:**

    Dentro do diretório `lib/templates/erb/scaffold`, crie um arquivo chamado `edit.html.erb`, ou atualize o existente: com o seguinte conteúdo:

### `edit.html.erb`

```erb
<h1 class="text-2xl font-bold mb-4">Editing <%= singular_table_name.titleize %></h1>

<%%= render 'form', <%= singular_table_name %>: @<%= singular_table_name %> %>

```

#### Explicação do Código

1. **edit.html.erb**:
   - Exibe um título indicando que o registro está sendo editado.
   - Renderiza o partial `_form.html.erb` passando o objeto do modelo.

**Crie o template para a view `_form`:**

    Dentro do diretório `lib/templates/erb/scaffold`, crie um arquivo chamado `_form.html.erb`, ou atualize o existente: com o seguinte conteúdo:

### `_form.html.erb`

```erb
<%%= form_with(model: <%= singular_table_name %>, local: true) do |form| %>
  <%% if <%= singular_table_name %>.errors.any? %>
    <div class="mb-4 p-4 border border-red-500 bg-red-100 text-red-700">
      <h3 class="text-lg font-bold"><%%= pluralize(<%= singular_table_name %>.errors.count, "error") %> prohibited this <%= singular_table_name %> from being saved:</h3>
      <ul class="list-disc pl-5">
        <%% <%= singular_table_name %>.errors.full_messages.each do |message| %>
          <li><%%= message %></li>
        <%% end %>
      </ul>
    </div>
  <%% end %>

  <% attributes.each do |attribute| -%>
    <% if attribute.type == :boolean || attribute.type == :checkbox -%>
      <div class="flex mb-4">
    <% else -%>
      <div class="mb-4">
    <% end -%>
      <%%= form.label :<%= attribute.column_name %>, class: "block text-gray-700" %>
      <% if attribute.type == :string -%>
        <%%= form.<%= attribute.field_type %> :<%= attribute.column_name %>, class: "mt-1 block w-full rounded-md border-gray-300 shadow-sm" %>
      <% elsif attribute.type == :integer -%>
        <%%= form.<%= attribute.field_type %> :<%= attribute.column_name %>, class: "mt-1 block w-full rounded-md border-gray-300 shadow-sm" %>
      <% elsif attribute.type == :date -%>
        <%%= form.<%= attribute.field_type %> :<%= attribute.column_name %>, class: "mt-1 block w-full rounded-md border-gray-300 shadow-sm" %>
      <% elsif attribute.type == :text -%>
        <%%= form.text_area :<%= attribute.column_name %>, class: "mt-1 block w-full rounded-md border-gray-300 shadow-sm" %>
      <% elsif attribute.type == :password -%>
        <%%= form.password_field :<%= attribute.column_name %>, class: "mt-1 w-full block w-full rounded-md border-gray-300 shadow-sm" %>
      <% elsif attribute.type == :float -%>
        <%%= form.number_field :<%= attribute.column_name %>, step: 0.01, class: "mt-1 block w-full rounded-md border-gray-300 shadow-sm" %>
      <% elsif attribute.type == :datetime -%>
        <%%= form.datetime_field :<%= attribute.column_name %>, class: "mt-1 block w-full rounded-md border-gray-300 shadow-sm" %>
      <% elsif attribute.type == :decimal -%>
        <%%= form.number_field :<%= attribute.column_name %>, step: 0.01, class: "mt-1 block w-full rounded-md border-gray-300 shadow-sm" %>
      <% elsif attribute.type == :boolean -%>
        <%%= form.check_box :<%= attribute.column_name %>, class: "ml-4 mt-1 block rounded-md border-gray-300 shadow-sm" %>
      <% elsif attribute.type == :checkbox -%>
        <%%= form.check_box :<%= attribute.column_name %>, class: "ml-4 mt-1 block rounded-md border-gray-300 shadow-sm" %>
      <% end -%>
    </div>
  <% end -%>

  <div class="mt-6 mb-4 flex items-center">
      <%%= link_to 'Cancel', <%= index_helper %>_path, class: "px-4 py-2 bg-gray-500 text-white rounded-md mr-2" %>
      <%%= form.submit "Save", class:"px-4 py-2 bg-blue-500 text-white rounded-md mr-4 ml-4" %>
  </div>
<%% end %>

```

#### Explicação do Código

1. **\_form.html.erb**:
   - Gera espaço para mostra os erros, quando houver
   - Utiliza condicionais para identificar o tipo de atributo e gerar o campo de input apropriado, mantendo a estilização com TailwindCSS.

**Crie o template para a view `show`:**

    Dentro do diretório `lib/templates/erb/scaffold`, crie um arquivo chamado `show.html.erb`, ou atualize o existente: com o seguinte conteúdo:

### `show.html.erb`

```erb
<h1 class="text-2xl font-bold mb-4"><%= singular_table_name.titleize %> Details</h1>

<%%= render partial: '<%= singular_table_name %>', locals: { <%= singular_table_name %>: @<%= singular_table_name %> } %>

<div class="mt-4 mb-4">
  <%%= link_to 'Edit', edit_<%= singular_table_name %>_path(@<%= singular_table_name %>), class: "mr-4 inline-block px-4 py-2 bg-blue-500 text-white rounded-md" %>
  <%%= link_to '<%= plural_table_name.titleize %>', <%= index_helper %>_path, class: "mr-4 inline-block px-4 py-2 bg-gray-500 text-white rounded-md" %>
  <%%= link_to 'Delete', @<%= singular_table_name %>, method: :delete, data: {
        turbo_method: :delete, turbo_confirm: 'Are you sure?' },
        class: "inline-block px-4 py-2 bg-red-500 text-white rounded-md" %>
</div>
```

#### Explicação do Código

1. **Título**: Exibe o título da página com o nome do modelo.
2. **RenderTabela**: Cria uma tabela para exibir cada atributo do modelo.
   - **Label e Valor**: Para cada atributo, exibe seu nome humanizado na coluna da esquerda e seu valor na coluna da direita.
3. **Ações**: Inclui links para editar, listar todos os registros e deletar o registro atual.

**Crie o template para a view `partial`:**

    Dentro do diretório `lib/templates/erb/scaffold`, crie um arquivo chamado `partial.html.erb`, ou atualize o existente: com o seguinte conteúdo:

### `partial.html.erb`

```erb
<article id="<%%= dom_id <%= singular_name %> %>" class="py-6 prose prose-zinc dark:prose-invert">
  <%- attributes.reject(&:password_digest?).each do |attribute| -%>
  <%- if attribute.attachment? -%>
    <%= singular_name %>.<%= attribute.column_name %>.filename, <%= singular_name %>.<%= attribute.column_name %> if <%= singular_name %>.<%= attribute.column_name %>.attached? %>
  <%- elsif attribute.attachments? -%>
    <%% <%= singular_name %>.<%= attribute.column_name %>.each do |<%= attribute.singular_name %>| %>
    <div><%= attribute.singular_name %>.filename, <%= attribute.singular_name %></div>
    <%% end %>
  <%- else -%>
    <div class="flex">
      <p class="mb-0 font-heading font-medium">
        <%= attribute.human_name %>:
      </p>
      <p class="mb-4 ml-4">
        <%%= <%= singular_name %>.<%= attribute.column_name %> %>
      </p>
    </div>
    <%- end -%>
  <%- end -%>
</article>

```

#### Explicação do Código

1. **Título**: Exibe o título da página com o nome do modelo.
2. **Tabela**: Cria um article para exibir cada atributo do modelo.
   - **Label e Valor**: Para cada atributo, exibe seu nome humanizado na coluna da esquerda e seu valor na coluna da direita.
