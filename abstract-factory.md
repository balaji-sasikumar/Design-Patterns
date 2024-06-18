### Abstract Factory
The Abstract Factory pattern provides an `interface for creating families` of related or dependent objects `without specifying their concrete classes`.


#### Implementation

- The Abstract Factory pattern is implemented by defining an interface for creating objects, but let the subclasses decide which class to instantiate.
```ts
interface DatabaseFactory {
    database(): Database;
    createConnection(): Connection;
}

interface Database {
    getAvailableDatabases(): string[];
    getTables(database: string): string[];
    getColumns(database: string, table: string): string[];
}

interface Connection {
    connect(): void;
    disconnect(): void;
}

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

class MySQLConnection implements Connection {
    connect(): void {
        console.log("Connected to MySQL");
    }
    disconnect(): void {
        console.log("Disconnected from MySQL");
    }
}

class MySQLFactory implements DatabaseFactory {
    database(): Database {
        return new MySQLDatabase();
    }
    createConnection(): Connection {
        return new MySQLConnection();
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

class PostgreSQLConnection implements Connection {
    connect(): void {
        console.log("Connected to PostgreSQL");
    }
    disconnect(): void {
        console.log("Disconnected from PostgreSQL");
    }
}

class PostgreSQLFactory implements DatabaseFactory {
    database(): Database {
        return new PostgreSQLDatabase();
    }
    createConnection(): Connection {
        return new PostgreSQLConnection();
    }
}
```

#### Usage

```ts
let dbType = "mysql";
let factory: DatabaseFactory;

if (dbType === "mysql") {
    factory = new MySQLFactory();
} else if (dbType === "postgres") {
    factory = new PostgreSQLFactory();
}

let database = factory.database();
let connection = factory.createConnection();

connection.connect();
console.log(database.getAvailableDatabases()); // Output: ['mysql_db1', 'mysql_db2']
```

#### Real-world analogy
- The Abstract Factory pattern is used in the `frameworks` to define the `interface` for creating an object, but let the `subclasses` decide which class to instantiate.
- For example, the `DatabaseFactory` interface defines the methods to create a `Database` and a `Connection`, but the `MySQLFactory` and `PostgreSQLFactory` subclasses decide which classes to instantiate.
- The `MySQLFactory` creates a `MySQLDatabase` and a `MySQLConnection`, while the `PostgreSQLFactory` creates a `PostgreSQLDatabase` and a `PostgreSQLConnection`.
- The client code can use the `Database` and `Connection` objects without knowing the concrete classes that are instantiated by the factories.
- This allows the client code to be independent of the concrete classes and promotes consistency among the objects created by the factories.
- The Abstract Factory pattern is used in frameworks to provide a library of objects that does not reveal implementation details and only reveals interfaces.