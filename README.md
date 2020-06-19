# rails-cheatsheet
Cheatsheet of commands and other nuggets of knowledge for Ruby on Rails projects

## Console

Access the console
`$ rails console` or `$ rails c`

Show all records
`> Story.all`

Show specific records
`> Story.find(1)  # Find Story where id = 1`

Show errors after attempting to save an object (assume object name is t)
`> t.errors`

## Migrations

Run all migrations
`$ rails db:migrate`

Rollback to the most recent migration
`$ rails db:rollback`

Rollback to a specific migration
`$rails db:migrate VERSION=n`

Rollback to a blank, initial database
`$ rails db:migrate VERSION=0`

### Renaming a column

First generate a migration

`$ rails g migration ChangeColumnName`

Open the `/db/migrate/xxx.rb` migration and use `rename_column`
```
class ChangeColumnName < ActiveRecord::Migration[6.0]
  def change
    rename_column :table_name, :old_name, :new_name
  end
end
```

Run the migration (see above command)


## Views

Adding [Bootstrap](https://www.getbootstrap.com) to your project
Use the [Bootstrap Ruby Gem](https://github.com/twbs/bootstrap-rubygem)

## Routes
Show/update routes
`$ rails routes`

### Nested Resources
Create an index of a nested resource ([StackOverflow](https://stackoverflow.com/questions/31757006/rails-4-how-do-i-add-an-index-route-for-a-nested-resource-in-order-to-list-al)

routes.rb:
```
resources :blog_post do
  resources :comments
end

get 'comments' => 'comments#index', as :comments
```

## Miscellaenous

[Using enumerations in Rails](https://www.justinweiss.com/articles/creating-easy-readable-attributes-with-activerecord-enums/)
