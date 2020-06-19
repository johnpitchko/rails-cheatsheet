# rails-cheatsheet
Cheatsheet of commands and other nuggets of knowledge for Ruby on Rails projects

## Console

Access the console
`$ rails console` or `$ rails c`

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

## Routes
Show/update routes
`$ rails routes`

### Nested Resources
Create an index of a nested resource

routes.rb:
```
resources :blog_post do
  resources :comments
end

get 'comments' => 'comments#index', as :comments
```
