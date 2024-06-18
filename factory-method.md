### Factory Method

- Factory Method is a creational design pattern that provides an `interface for creating objects in a superclass`, but allows `subclasses to alter the type of objects` that will be created.
- Factory Method pattern is used when a `class wants to allow subclasses to make the decision of what objects to create`.

#### Implementation

- The Factory Method pattern is implemented by defining an interface for creating objects, but let the subclasses decide which class to instantiate.

```ts
// common interface for all products
interface Database {
  getAvailableDatabases(): string[];
  getTables(database: string): string[];
  getColumns(database: string, table: string): string[];
}

// concrete products
class MySQLDatabase implements Database {
  getAvailableDatabases(): string[] {
    return ["mysql_db1", "mysql_db2"];
  }
  getTables(database: string): string[] {
    return ["table1", "table2"];
  }
  getColumns(database: string, table: string): string[] {
    return ["column1", "column2"];
  }
}

class PostgreSQLDatabase implements Database {
  getAvailableDatabases(): string[] {
    return ["postgres_db1", "postgres_db2"];
  }
  getTables(database: string): string[] {
    return ["table1", "table2"];
  }
  getColumns(database: string, table: string): string[] {
    return ["column1", "column2"];
  }
}

// creator interface

abstract class Creator {
  abstract factoryMethod(): Database;

  getAvailableDatabases(): string[] {
    return this.factoryMethod().getAvailableDatabases();
  }

  getTables(database: string): string[] {
    return this.factoryMethod().getTables(database);
  }

  getColumns(database: string, table: string): string[] {
    return this.factoryMethod().getColumns(database, table);
  }
}

// concrete creators

class MySQLCreator extends Creator {
  factoryMethod(): Database {
    return new MySQLDatabase();
  }
}

class PostgreSQLCreator extends Creator {
  factoryMethod(): Database {
    return new PostgreSQLDatabase();
  }
}
```

#### Usage

```ts
let dbType = "mysql";
let creator: Creator;

if (dbType === "mysql") {
  creator = new MySQLCreator();
} else if (dbType === "postgres") {
  creator = new PostgreSQLCreator();
}

console.log(creator.getAvailableDatabases()); // Output: ['mysql_db1', 'mysql_db2']
```

#### Real-world analogy

- The Factory Method pattern is used in the `frameworks` to define the `interface` for creating an object, but let the `subclasses` decide which class to instantiate.
