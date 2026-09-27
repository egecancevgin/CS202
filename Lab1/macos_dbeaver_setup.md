# PostgreSQL + DBeaver on macOS

1. Get the [PostgreSQL macOS installer](https://www.postgresql.org/download/macosx/). Choose your Mac’s chip, run it, and save the `postgres` password you set.

2. Get **DBeaver Community** from the [official download page](https://dbeaver.io/download/). Open the macOS `.dmg` and drag DBeaver into **Applications**.

3. Open **DBeaver → New Database Connection → PostgreSQL**. Enter:

   | Field | Value |
   | --- | --- |
   | Host | `127.0.0.1` |
   | Port | `5432` |
   | Database | `postgres` |
   | Username | `postgres` |
   | Password | The password from step 1 |

   Click **Test Connection**, then **Finish**. Allow the driver download if asked.

4. Right-click the `postgres` database → **SQL Editor → New SQL Script**. Paste this and choose **SQL Editor → Execute SQL Script**:

   ```sql
   CREATE TABLE students (
       id integer GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
       name text NOT NULL
   );

   INSERT INTO students (name)
   VALUES ('Ada'), ('Deniz');

   SELECT * FROM students;
   ```
