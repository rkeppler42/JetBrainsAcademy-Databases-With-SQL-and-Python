# 🖥️ Computer Store – SQL Project

Small SQL project based on a fictional **computer store**.

This project is part of the **SQL + Python** track on Hyperskill.

------

## 🧾 Scenario

As a computer store manager, you need to keep track of your inventory and understand which products are more expensive, more powerful, or more specialized.

------

## 🗃️ Database Schema

The database is called `Computer_Store` and has four tables:

### `Product`

Stores generic information about all models in the catalog.

```

CREATE TABLE Product (
    maker VARCHAR(50) NOT NULL,
    model INT NOT NULL,
    type VARCHAR(50) NOT NULL,
    PRIMARY KEY (model)
);
```

- `maker` – manufacturer (Apple, Dell, Lenovo, etc.)
- `model` – unique model identifier across the whole catalog
- `type` – type of product: `'PC'`, `'Laptop'`, `'Printer'`, etc.

------

### `PC`

Represents desktop computers.

```

CREATE TABLE PC (
    code INT NOT NULL,
    model INT NOT NULL,
    speed INT NOT NULL,
    ram INT NOT NULL,
    hd INT NOT NULL,
    cd VARCHAR(50) NOT NULL,
    price DECIMAL(10, 2) NOT NULL,
    PRIMARY KEY (code),
    FOREIGN KEY (model) REFERENCES Product(model)
);
```

- `code` – unique PC identifier
- `model` – foreign key to `Product(model)`
- `speed` – CPU speed (GHz or MHz, depending on the dataset convention)
- `ram` – RAM in MB
- `hd` – hard disk capacity in GB
- `cd` – optical drive type (`DVD`, `Blu-ray`, `None`)
- `price` – price in dollars

------

### `Laptop`

Represents laptop computers.

```

CREATE TABLE Laptop (
    code INT NOT NULL,
    model INT NOT NULL,
    speed INT NOT NULL,
    ram INT NOT NULL,
    hd INT NOT NULL,
    screen INT NOT NULL,
    price DECIMAL(10, 2) NOT NULL,
    PRIMARY KEY (code),
    FOREIGN KEY (model) REFERENCES Product(model)
);
```

- `code` – unique laptop identifier
- `model` – foreign key to `Product(model)`
- `screen` – screen size in inches
- The other fields have the same meaning as in `PC`.

------

### `Printer`

Represents printers in the catalog.

```

CREATE TABLE Printer (
    code INT NOT NULL,
    model INT NOT NULL,
    color CHAR(1) NOT NULL,
    type VARCHAR(50) NOT NULL,
    price DECIMAL(10, 2) NOT NULL,
    PRIMARY KEY (code),
    FOREIGN KEY (model) REFERENCES Product(model)
);
```

- `code` – unique printer identifier
- `model` – foreign key to `Product(model)`
- `color` – `'C'` for color printers, `'B'` for black & white
- `type` – `'Laser'`, `'Inkjet'`, `'Matrix'`, etc.
- `price` – price in dollars

> A single **model** in `Product` can be used by multiple rows in `PC`, `Laptop` or `Printer`, representing different physical items of the same model.

------

## 📂 Project Structure

```

computer-store-database/
├── README.md
└── sql/
    ├── computer_store.sql           # DDL + INSERTs (database creation script)
    └── 01_expensive_printers.sql    # Query for the first task
```

- `computer_store.sql` contains:
  - `CREATE DATABASE Computer_Store;`
  - `CREATE TABLE ...` for all tables
  - `INSERT INTO ...` with sample data

------

## ▶️ How to Run Locally (MySQL)

### 1. Create the database

From a terminal / PowerShell, using MySQL:

```

mysql -u root -p < sql/computer_store.sql
```

Or, inside the MySQL client:

```

SOURCE /absolute/path/to/sql/computer_store.sql;
```

This will:

- Create the database `Computer_Store`;
- Create all tables;
- Insert all sample records.

Then select the database:

```

USE Computer_Store;
```

------

## ✅ Task 1 – Find Expensive Printers

### 📝 Description

For this step, the goal is to identify printers in the inventory that are **priced over $200**.

You should display:

1. `model`
2. `type`
3. `price`

in exactly this order.

### 🎯 Requirements

- Work with the `Printer` table;
- Filter only rows where `price > 200`;
- Return only the columns `model`, `type`, and `price`.

### 💡 Solution

File: `sql/01_expensive_printers.sql`

You can test it in MySQL Workbench or directly in the terminal:

```

USE Computer_Store;
SOURCE sql/01_expensive_printers.sql;
```

