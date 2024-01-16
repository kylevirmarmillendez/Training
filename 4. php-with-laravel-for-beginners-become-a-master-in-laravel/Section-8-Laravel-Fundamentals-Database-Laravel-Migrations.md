# Laravel Fundamentals Database - Laravel Migrations

**Migrations** - Table generators where we can define tables and columns inside the table.

**Migrations Setup** 
- Go to .env file and change the DB_DATABASE value to the your database.
- Change the DB_USERNAME value to root
- Leave the DB_PASSWORB blank.
- GO to the terminal the type "php artisan migrate"


### Creating Custom Migrations
- Got to the terminal, input "php artisan make:migration name_of_migration --create=name_table
- You can create your own Schema for you table.
- after that hit "php artisan migrate"


### Adding Columns to the tables
- Got to the terminal, input "php artisan make:migration name_of_the_migration ==table="name_of_table"
- Got to the migration file the setup the column that you want to insert
- then hit "php artisan migrate"