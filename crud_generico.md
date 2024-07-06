## Crud generico para tabelas com atributos semelhantes(com ajuda de IA)

Para criar um sistema CRUD genérico que possa ser aplicado a várias tabelas com atributos semelhantes em um aplicativo Ruby on Rails; para evitar duplicação de código e facilitar a manutenção, você pode usar a abordagem de geradores de código dinâmicos e parâmetros de rotas. A seguir, um guia para criar um único controller e views genéricos para lidar com múltiplas tabelas:

### 1 - Defina Rotas Dinâmicas:

#### No seu arquivo config/routes.rb, defina rotas dinâmicas que encaminham para um único controller, configuradas para aceitar o nome da tabela:

      # config/routes.rb
      Rails.application.routes.draw do
        resources :dynamic_tables, param: :table do
          collection do
            get ':table', to: 'dynamic_tables#index'
            get ':table/new', to: 'dynamic_tables#new'
            post ':table', to: 'dynamic_tables#create'
            get ':table/:id/edit', to: 'dynamic_tables#edit'
            get ':table/:id', to: 'dynamic_tables#show'
            patch ':table/:id', to: 'dynamic_tables#update'
            delete ':table/:id', to: 'dynamic_tables#destroy'
          end
        end
      end

### 2 - Crie um Controller Genérico:

#### Crie um controller que lida com múltiplas tabelas com base no parâmetro da URL:

      # app/controllers/dynamic_tables_controller.rb
      class DynamicTablesController < ApplicationController
        before_action :set_table
        before_action :set_record, only: %i[show edit update destroy]

        def index
          @records = @table_class.all
        end

        def show; end

        def new
          @record = @table_class.new
        end

        def edit; end

        def create
          @record = @table_class.new(record_params)

          if @record.save
            redirect_to table_index_path(table: params[:table]), notice: "#{@table_name.singularize.capitalize} was successfully created."
          else
            render :new
          end
        end

        def update
          if @record.update(record_params)
            redirect_to table_index_path(table: params[:table]), notice: "#{@table_name.singularize.capitalize} was successfully updated."
          else
            render :edit
          end
        end

        def destroy
          @record.destroy
          redirect_to table_index_path(table: params[:table]), notice: "#{@table_name.singularize.capitalize} was successfully destroyed."
        end

        private

        def set_table
            @table_name = params[:table].classify
            @table_class = @table_name.constantize
          rescue NameError
            redirect_to root_path, alert: "Table not found."
        end

        def set_record
            @record = @table_class.find(params[:id])
          rescue ActiveRecord::RecordNotFound
            redirect_to table_index_path(table: params[:table]), alert: "Record not found."
        end

        def record_params
          params.require(@table_name.underscore.to_sym).permit(:description)
        end
      end

### 3 - Crie Views Genéricos:

#### Crie as views que serão utilizadas por todas as tabelas. No diretório app/views/dynamic_tables, crie os arquivos de views como index.html.erb, show.html.erb, new.html.erb, edit.html.erb e \_form.html.erb.

Exemplo de index.html.erb:

      # app/views/dynamic_tables/index.html.erb
      <h1><%= @table_name.pluralize %></h1>
      <%= link_to "New #{@table_name.singularize}", new_dynamic_table_path(table: params[:table]) %>
      <table>
        <thead>
          <tr>
            <th>ID</th>
            <th>Description</th>
            <th>Actions</th>
          </tr>
        </thead>
        <tbody>
          <% @records.each do |record| %>
            <tr>
              <td><%= record.id %></td>
              <td><%= record.description %></td>
              <td>
                <%= link_to 'Show', dynamic_table_path(params[:table], record) %>
                <%= link_to 'Edit', edit_dynamic_table_path(params[:table], record) %>
                <%= link_to 'Destroy', dynamic_table_path(params[:table], record), method: :delete, data: { confirm: 'Are you sure?' } %>
              </td>
            </tr>
          <% end %>
        </tbody>
      </table>

Exemplo de edit.html.erb:

- Este arquivo renderiza o formulário de edição, reutilizando o formulário genérico form.html.erb:

      # app/views/dynamic_tables/edit.html.erb
      <h1>Editing <%= @table_name.singularize %></h1>

      <%= render 'form' %>

      <%= link_to 'Back', dynamic_tables_path(table: params[:table]) %>

Exemplo de new.html.erb:

- Este arquivo renderiza o formulário de criação, reutilizando o formulário genérico form.html.erb:

      # app/views/dynamic_tables/new.html.erb
      <h1>New <%= @table_name.singularize %></h1>

      <%= render 'form' %>

      <%= link_to 'Back', dynamic_tables_path(table: params[:table]) %>

Exemplo de show.html.erb:

- Este arquivo exibe os detalhes de um registro(criado/editado/visualização) específico:

      # app/views/dynamic_tables/show.html.erb
      <div id="<%= dom_id(@record) %>">
        <p>
          <strong>Description:</strong>
          <%= @record.description %>
        </p>
      </div>

      <%= link_to 'Edit', edit_generic_path(@table, @record) %> |
      <%= link_to 'Back', generic_index_path(@table) %>

Exemplo de _form_.html.erb:

- Este arquivo e compartilhado entre new e edit

      # app/views/dynamic_tables/_form_.html.erb
      <%= form_with model: [params[:table], @record], local: true do |form| %>
        <% if @record.errors.any? %>
          <div id="error_explanation">
            <h2><%= pluralize(@record.errors.count, "error") %> prohibited this <%= @table_name.singularize.downcase %> from being saved:</h2>

            <ul>
              <% @record.errors.full_messages.each do |message| %>
                <li><%= message %></li>
              <% end %>
            </ul>
          </div>
        <% end %>

        <div class="field">
          <%= form.label :description %>
          <%= form.text_field :description %>
        </div>

        <div class="actions">
          <%= form.submit %>
        </div>
      <% end %>

Aqui está um exemplo de um dropdown no seu navbar chamando as tabelas:

      <!-- app/views/layouts/application.html.erb -->
      <!DOCTYPE html>
      <html>
      <head>
        <title>YourAppName</title>
        <%= csrf_meta_tags %>
        <%= csp_meta_tag %>

        <%= stylesheet_link_tag 'application', media: 'all', 'data-turbolinks-track': 'reload' %>
        <%= javascript_pack_tag 'application', 'data-turbolinks-track': 'reload' %>
      </head>
      <body>
        <nav class="navbar navbar-expand-lg navbar-light bg-light">
          <a class="navbar-brand" href="#">YourAppName</a>
          <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNavDropdown" aria-controls="navbarNavDropdown" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
          </button>
          <div class="collapse navbar-collapse" id="navbarNavDropdown">
            <ul class="navbar-nav">
              <li class="nav-item active">
                <%= link_to 'Home', root_path, class: 'nav-link' %>
              </li>
              <li class="nav-item dropdown">
                <a class="nav-link dropdown-toggle" href="#" id="navbarDropdownMenuLink" role="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                  Tables
                </a>
                <div class="dropdown-menu" aria-labelledby="navbarDropdownMenuLink">
                  <%= link_to 'Products', table_index_path(table: 'products'), class: 'dropdown-item' %>
                  <%= link_to 'Categories', table_index_path(table: 'categories'), class: 'dropdown-item' %>
                  <%= link_to 'Orders', table_index_path(table: 'orders'), class: 'dropdown-item' %>
                </div>
              </li>
            </ul>
          </div>
        </nav>

        <div class="container">
          <%= yield %>
        </div>
      </body>
      </html>

Passo Final: Acesso às Tabelas

Com tudo configurado, ao clicar em um item no dropdown do navbar, o nome da tabela será passado como um parâmetro na URL. Por exemplo:

    Products: /dynamic_tables/products
    Categories: /dynamic_tables/categories
    Orders: /dynamic_tables/orders

O controller DynamicTablesController interpretará o parâmetro :table e carregará o modelo correto, permitindo que o CRUD genérico funcione para qualquer uma das tabelas.

### OBS: Caso encontre algum erro ou se tiver alguma sugestão, e só mandar, sera um prazer compartilhar conhecimento.
