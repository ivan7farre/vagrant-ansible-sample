# Ansible Postgres Role

A simple role to create a Database with a new Postgres user. Optional activate HStore Extension for the new Database.

## Role Variables

```yaml
pg_db: # The name of the Database you want to create 
pg_user: # Postgres User 
pg_password: # Password for the Postgres User 
pg_hstore: # True | False default is False 
```

## ToDo
- Add config files via templates
- Posibility to add more Extensions

## License

MIT
