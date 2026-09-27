# Install PostgreSQL on Linux, open pgAdmin, and create your first table

Use the section for your system: **Ubuntu** or **Fedora**. The Fedora GUI steps below use **pgAdmin 4**. Open a terminal to run the commands.

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

## 2. Set up pgAdmin on Fedora

Fedora's PostgreSQL install does **not** include a GUI. Install the pgAdmin desktop app:

```bash
sudo rpm -i https://ftp.postgresql.org/pub/pgadmin/pgadmin4/yum/pgadmin4-fedora-repo-2-1.noarch.rpm
sudo dnf install pgadmin4-desktop
```

If the first command says the pgAdmin repository is already installed, skip it and run the second command.

### Give your local connection a password

Open the PostgreSQL terminal:

```bash
sudo -u postgres psql
```

At the `postgres=#` prompt, type `\password postgres`, enter a new password twice, then type `\q`. **Save this password.**

Fedora may use `ident` for local TCP connections. Check which file controls access:

```bash
sudo -u postgres psql -Atc 'SHOW hba_file;'
```

Open the path printed by that command with `sudo nano PATH` (replace `PATH` with the printed path). Find the active line for `127.0.0.1/32`. If its last word is `ident`, change **only that word** to `scram-sha-256`. The line should look like this:

```text
host    all    all    127.0.0.1/32    scram-sha-256
```

If it already says `scram-sha-256`, leave it alone. Save in nano with **Ctrl+O**, **Enter**, then **Ctrl+X**. Load the change and test your password:

```bash
sudo systemctl reload postgresql
psql -h 127.0.0.1 -U postgres -d postgres
```

Enter the password, then type `\q`. Keep the `local` lines in that file as they were; they let `sudo -u postgres psql` keep working.

### Connect in pgAdmin

1. Open **pgAdmin 4** from the app menu. If asked for a master password, set one; it is separate from the database password.
2. Right-click **Servers → Register → Server**.
3. On **General**, give it a name such as `Local PostgreSQL`.
4. On **Connection**, set **Host name/address** to `127.0.0.1`, **Port** to `5432`, **Maintenance database** to `postgres`, and **Username** to `postgres`.
5. Enter the database password you made above, then click **Save**.

## 3. Create your first table in pgAdmin (Fedora)

In the left panel, right-click **Servers → Local PostgreSQL → Databases → postgres**, then choose **Query Tool**. Paste and run the SQL in section 5 using the **Execute** (▶) button. The two rows will appear in **Data Output**.

To see the table in the sidebar, open **Databases → postgres → Schemas → public → Tables**. Right-click **Tables → Refresh** if needed.

## 4. Terminal option (Ubuntu or Fedora)

On either system, run:

```bash
sudo -u postgres psql
```

Your prompt should change to `postgres=#`. The `postgres` database and user are ready for this first exercise. You do not need to set a password to use this local terminal method.

## 5. Create a table and add two rows

Paste the SQL below into the pgAdmin Query Tool **or** at the `postgres=#` terminal prompt. The prompt itself is **not** part of the code.

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

In the terminal, type `\dt` to see your tables or `\q` to leave PostgreSQL. These two commands are for `psql`, not pgAdmin.

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
- [pgAdmin 4 desktop install for Fedora](https://www.pgadmin.org/download/pgadmin-4-rpm/)
- [PostgreSQL: Client authentication](https://www.postgresql.org/docs/current/auth-pg-hba-conf.html)
- [PostgreSQL: Creating a table](https://www.postgresql.org/docs/current/tutorial-table.html)
