# Install PostgreSQL on Linux and create your first table

Use the section for your system: **Ubuntu** or **Fedora**. The rest of the guide works for both. Open a terminal to run the commands.

## 1. Install PostgreSQL

### Ubuntu

```bash
sudo apt update
sudo apt install postgresql
sudo systemctl start postgresql
```

### Fedora

```bash
sudo dnf install postgresql-server
sudo postgresql-setup --initdb
sudo systemctl enable --now postgresql
```

**Fedora note:** Run `postgresql-setup --initdb` only for a fresh install. If PostgreSQL was already set up, skip that line so you keep your databases.

## 2. Open PostgreSQL

On either system, run:

```bash
sudo -u postgres psql
```

Your prompt should change to `postgres=#`. The `postgres` database and user are ready for this first exercise. You do not need to set a password to use this local terminal method.

## 3. Create a table and add two rows

Paste the SQL below at the `postgres=#` prompt. The prompt itself is **not** part of the code.

```sql
CREATE TABLE students (
    student_id integer GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    full_name text NOT NULL,
    email text UNIQUE
);

INSERT INTO students (full_name, email)
VALUES
    ('Ada Yilmaz', 'ada@example.com'),
    ('Deniz Kaya', 'deniz@example.com');

SELECT * FROM students;
```

You should see two rows. PostgreSQL makes each `student_id` for you. `PRIMARY KEY` makes IDs unique; `NOT NULL` requires a name; `UNIQUE` stops duplicate emails.

To see your tables, type `\dt`. To leave PostgreSQL, type `\q`.

**Tip:** The table stays on your computer after you close the terminal. Next time, run `sudo -u postgres psql` and then `SELECT * FROM students;`. Do not repeat `CREATE TABLE students`, because the table already exists.

## If the connection fails

If you see a message about a missing socket or a server that is not running, start it and try again:

```bash
sudo systemctl start postgresql
sudo -u postgres psql
```

## Sources

- [PostgreSQL: Ubuntu installation](https://www.postgresql.org/download/linux/ubuntu/)
- [PostgreSQL: Fedora installation](https://www.postgresql.org/download/linux/redhat/)
- [PostgreSQL: Creating a table](https://www.postgresql.org/docs/current/tutorial-table.html)
