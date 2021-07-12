# heroku_crypto_alerts

Changing the Heroku Postgres Database:
- make model changes locally
- Run ‘flask db migrate’ locally
    - If this command fails run ‘flask db stamp head’ then run ‘flask db migrate’ again
    - see: https://stackoverflow.com/questions/17768940/target-database-is-not-up-to-date
- Run ‘flask db upgrade’, this allows you to continue making changes locally with a fresh migration, will break if you do not do this
- Run ‘git add .’ 
- Run ‘git commit -m ‘model change’’
- Run ‘git push heroku master’
- Run ‘heroku run flask db upgrade’
- Check to see that database changes were successful


If still having problems with model update here is a hard reset:
- Run ‘heroku psql’ to open a database shell
    - Run ‘delete from alembic_version;’ to remove the latest version
    - ‘\q’ to leave shell
- Locally delete the file in instance
- Locally delete the entire migrations folder
- Run ‘flask db init’ to recreate
- Run ‘flask db migrate’ to populate it
- Run ‘git add .’ 
- Run ‘git commit -m ‘model change’’
- Run ‘git push heroku master’
- Go back into psql shell and drop all tables except alembic_version
- Run ‘heroku run flask db upgrade’ and you should be set with an updated version of your db
