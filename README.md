
For more example of running DBs and GUIs with Docker:
https://www.codeproject.com/Tips/5336563/Run-Database-and-GUI-Clients-in-Docker


# Working with containers

To access bash / terminal, exec the name of the service with 'bash':
docker-compose exec postgres bash


# Access DB from within container

If you want to setup a connection from one container to a DB (eg. Postgres), do NOT user localhost or 127.0.0.1 but the name of the Docker service, eg. postgres or db (see docker-compose.yml)



# Simple SQL statements for quick tests

From:
https://gvwilson.github.io/sql-tutorial/


## Create tables 

create table job (
    name text not null,
    billable real not null
);
create table work (
    person text not null,
    job text not null
);

## Insert data

insert into job values
('calibrate', 1.5),
('clean', 0.5);

insert into work values
('mik', 'calibrate'),
('mik', 'clean'),
('mik', 'complain'),
('po', 'clean'),
('po', 'complain'),
('tay', 'complain');




# Import CSV data into Postgres (via Pandas)

# Example: Dataset 'penguins.csv' from https://gvwilson.github.io/sql-tutorial/

!pip install psycopg2-binary

import pandas as pd
df = pd.read_csv('penguins.csv')
df.columns = [c.lower() for c in df.columns] # PostgreSQL doesn't like capitals or spaces

from sqlalchemy import create_engine
engine = create_engine('postgresql://demo_user:secret@localhost:5432/demo_db')
df.to_sql("little_penguins", engine)