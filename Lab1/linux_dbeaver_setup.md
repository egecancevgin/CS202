# PostgreSQL + DBeaver on Fedora

1. Install PostgreSQL:

   ```bash
   sudo dnf install postgresql-server
   sudo postgresql-setup --initdb
   sudo systemctl enable --now postgresql
   ```

   If PostgreSQL was already set up, skip `postgresql-setup --initdb`.

2. Open **Fedora Software**, search for **DBeaver Community**, and install it.

3. Set the database password:

   ```bash
   sudo -u postgres psql
   ```

   At `postgres=#`, type `\password postgres`, enter a password twice, then type `\q`.

4. Open the login settings:

   ```bash
   sudo nano /var/lib/pgsql/data/pg_hba.conf
   ```

   On the line containing `127.0.0.1/32`, change `ident` to `scram-sha-256`. Save with **Ctrl+O**, **Enter**, **Ctrl+X**.

5. Apply the change:

   ```bash
   sudo systemctl reload postgresql
   ```

6. Open **DBeaver Community → New Database Connection → PostgreSQL**. Enter:

   | Field | Value |
   | --- | --- |
   | Host | `127.0.0.1` |
   | Port | `5432` |
   | Database | `postgres` |
   | Username | `postgres` |
   | Password | The password from step 3 |

   Click **Test Connection**, then **Finish**.

7. Right-click the `postgres` database → **SQL Editor → New SQL Script**. Paste this and press **Alt+X**:

   ```sql
   CREATE TABLE students (
       id integer GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
       name text NOT NULL
   );

   INSERT INTO students (name)
   VALUES ('Ada'), ('Deniz');

   SELECT * FROM students;
   ```
