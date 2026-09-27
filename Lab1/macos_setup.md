# PostgreSQL + pgAdmin on macOS

1. Open the [PostgreSQL macOS download page](https://www.postgresql.org/download/macosx/) and choose **Download the installer**. Pick the installer for your Mac’s chip.

2. Run the installer. Keep **PostgreSQL Server** and **pgAdmin 4** selected. Set and save the `postgres` password. You can skip **Stack Builder**.

3. Open **pgAdmin 4**. Expand the local server and enter your `postgres` password when asked. If no server appears, choose **Servers → Register → Server** and enter:

   | Field | Value |
   | --- | --- |
   | Host | `127.0.0.1` |
   | Port | `5432` |
   | Maintenance database | `postgres` |
   | Username | `postgres` |
   | Password | The password from step 2 |

4. Right-click **Databases → postgres → Query Tool**. Paste this and press **F5**:

   ```sql
   CREATE TABLE students (
       id integer GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
       name text NOT NULL
   );

   INSERT INTO students (name)
   VALUES ('Ada'), ('Deniz');

   SELECT * FROM students;
   ```
