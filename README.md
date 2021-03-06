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

### Database Console

Creating a new Rails app using the default configuration will use SQLite3 as the database. The database files are available in the `db` directory.

There may be times where you want to access the raw database rather than working through ActiveRecord in the Rails console. To launch the SQLite3 console:

```
$ sqlite3 db/development.sqlite3
```

#### Common SQLite3 Console Commands

`.exit` Quites the console
`.database` Shows all databases in the current connection
`.tables` Shows all tables in the databaase
`.schema TABLE` Describe the structure/schema of the specified table

## Generators

Create a scaffold (all the stuff you normally need) **note this is singular**
`$ rails generate scaffold underlying`

Rollback whatever you just generated
`$ rails destroy scaffold underlying`

## Migrations

Run all migrations
`$ rails db:migrate`

Rollback to the most recent migration
`$ rails db:rollback`

Rollback to a specific migration
`$rails db:migrate VERSION=n`

Rollback to a blank, initial database
`$ rails db:migrate VERSION=0`

### SQLite3 datatypes

[Source](https://stackoverflow.com/questions/17918117/rails-4-list-of-available-datatypes)

* :string - is for small data types such as a title
* :text - is for longer pieces of textual data, such as a paragraph of information
* :binary - is for storing data such as images, audio, or movies
* :boolean - is for storing true or false values
* :date - store only the date
* :datetime - store both the date and time
* :time - is for time only
* :timestamp - for storing date and time into a column
* :decimal - is for decimals (use for currency)
* :float - is for decimals (use for scientific purposes)
* :integer - is for whole numbers
* :primary_key - unique key that can uniquely identify each row in a table

### Adding a foreign key to an existing table

Generate a migration

`$ rails g migration AddForeignKeyToTable`

Add the foreign key and change the parent id column so it cannot be null

`add foreign_key :parents, :childs`
`change_column :childs, :parent_id, :integer, null :false`

Run the migration

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

## Controllers

### Permit parameters (example)

```
def underlying_params
  params.fetch(:underlying).permit(:symbol, :description, :beta, :correlation)
end
```

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
resources :book do
  resources :chapter
end

get 'chapters' => 'chapters#index', as :chapters
```

## Testing

### Testing nested routes

If you generated the tests via `rails generate`, you must update the HTTP calls to include the ID of the parent. Also be sure to redirect to the appropriate page and include the necessary IDs

<pre> 
test 'should create chapter' do
    assert_difference('Chapter.count') do
      post(book_chapter_url(<b>book_id: @chapter.book_id</b>),
           params: { chapter: { ... } })
    end

    assert_redirected_to book_chapters_url(@book)
  end
</pre>

## Debugging

### Prepend log messages with timestamp

Add to `config/environment.rb`:

```
class Logger
  def format_message(severity, timestamp, progname, msg)
    "#{timestamp} (#{$$}) #{msg}\n"
  end
end
```
## Miscellaenous

[Using enumerations in Rails](https://www.justinweiss.com/articles/creating-easy-readable-attributes-with-activerecord-enums/)

### Editing they secret key file
`EDITOR="atom --wait" rails credentials:edit`
