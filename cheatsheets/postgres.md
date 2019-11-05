# Postgre SQL

## Updated_at date

```sql
    ALTER TABLE table_name ADD COLUMN updated_at TIMESTAMP WITHOUT TIME ZONE; 
    CREATE FUNCTION updated_at() RETURNS trigger AS $$begin new.updated_at := now(); RETURN new; END;$$ LANGUAGE plpgsql;
    CREATE TRIGGER t_batiment_updated_at  BEFORE UPDATE ON table_name FOR EACH ROW EXECUTE PROCEDURE updated_at();

```
