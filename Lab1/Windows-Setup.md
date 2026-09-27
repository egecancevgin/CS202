# Install PostgreSQL on Windows and create your first table

This guide uses **pgAdmin**, the visual tool included with the PostgreSQL installer. You do not need a terminal.

## 1. Install PostgreSQL

1. Open the [official PostgreSQL Windows download page](https://www.postgresql.org/download/windows/).
2. Click **Download the installer** and choose the current supported Windows version from EDB.
3. Run the downloaded `.exe` file. Leave **PostgreSQL Server**, **pgAdmin 4**, and **Command Line Tools** selected.
4. Choose an install folder and data folder, or keep the defaults.
5. Set a password for the `postgres` user. **Save it**; you will need it to connect.
6. Keep the default port **5432** unless another program already uses it. Keep the default locale, then finish the install.
7. If **Stack Builder** opens at the end, close it. It is not needed for this guide.

## 2. Connect in pgAdmin

1. Open **pgAdmin 4** from the Windows Start menu.
2. If pgAdmin asks you to set a master password, choose one. This is separate from the `postgres` password you set during install.
3. In the left panel, open **Servers → PostgreSQL**. Enter the `postgres` password if asked.
4. Open **Databases → postgres**. This is the default database that you will use for practice.

If the server is not listed, right-click **Servers → Register → Server**. Give it a name, then set **Host name/address** to `localhost`, **Port** to `5432`, **Maintenance database** to `postgres`, and **Username** to `postgres`. Enter the password you saved.

## 3. Create a table and add two rows

1. Right-click the **postgres** database and choose **Query Tool**.
2. Paste this SQL into the editor and click **Execute** (the ▶ button).

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

The **Data Output** panel should show two rows. PostgreSQL fills in `student_id` for you. `PRIMARY KEY` makes each ID unique; `NOT NULL` requires a name; `UNIQUE` prevents duplicate emails.

To find the table in the left panel, open **Databases → postgres → Schemas → public → Tables**, then right-click **Tables → Refresh** if it does not appear.

**Tip:** Run the whole block only once. For later checks, highlight just `SELECT * FROM students;` and click **Execute**. Running the whole block again will try to create a table that already exists.

## Sources

- [PostgreSQL Windows installer](https://www.postgresql.org/download/windows/)
- [PostgreSQL: Creating a New Table](https://www.postgresql.org/docs/current/tutorial-table.html)
- [PostgreSQL: Inserting Data](https://www.postgresql.org/docs/current/tutorial-populate.html)
