# PostgreSQL + pgAdmin on Ubuntu

1. Install PostgreSQL:

   ```bash
   sudo apt update
   sudo apt install postgresql
   ```

2. Install pgAdmin Desktop:

   ```bash
   sudo apt install curl gnupg lsb-release ca-certificates
   sudo install -d /etc/apt/keyrings
   curl -fsS https://www.pgadmin.org/static/packages_pgadmin_org.pub | sudo gpg --dearmor -o /etc/apt/keyrings/packages-pgadmin-org.gpg
   sudo sh -c 'echo "deb [signed-by=/etc/apt/keyrings/packages-pgadmin-org.gpg] https://ftp.postgresql.org/pub/pgadmin/pgadmin4/apt/$(lsb_release -cs) pgadmin4 main" > /etc/apt/sources.list.d/pgadmin4.list'
   sudo apt update
   sudo apt install pgadmin4-desktop
   ```

3. Set the database password:

   ```bash
   sudo -u postgres psql
   ```

   Type `\password postgres`, enter a password twice, then type `\q`.

4. Open **pgAdmin 4 → Servers → Register → Server**. Name it `Local PostgreSQL`. In **Connection**, enter:

   | Field | Value |
   | --- | --- |
   | Host | `127.0.0.1` |
   | Port | `5432` |
   | Maintenance database | `postgres` |
   | Username | `postgres` |
   | Password | The password from step 3 |

   Click **Save**.

5. Right-click **Databases → postgres → Query Tool**. Paste this and press **F5**:

   ```sql
   CREATE TABLE students (
       id integer GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
       name text NOT NULL
   );

   INSERT INTO students (name)
   VALUES ('Ada'), ('Deniz');

   SELECT * FROM students;
   ```
