# rails-cheatsheet
Cheatsheet of commands and other nuggets of knowledge for Ruby on Rails projects

## Migrations

Run all migrations
`$ rails db:migrate`

Rollback to the most recent migration
`$ rails db:rollback`

Rollback to a specific migration
`$rails db:migrate VERSION=n`

Rollback to a blank, initial database
`$ rails db:migrate VERSION=0`
