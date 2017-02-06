### To drop the current database, and begin with clean one: 
Method1: 
  1. delete current database or update your connectionstring to point to a new one
  2. delete migrations folder
  3. from Nuget Console, run: 
      i.   Enable-Migrations
      ii.  Add-Migration Initial
      iii. Update-Database
      
Method2:
  1. update-database -TargetMigration:0 | update-database -force | update-database -force [taken from SO link: http://stackoverflow.com/a/32808843/618220]
