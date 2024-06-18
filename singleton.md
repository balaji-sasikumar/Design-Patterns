### Singleton Design Pattern
- Singleton is a creational design pattern that lets you ensure that a class has only `one instance`, while providing a `global access point` to this instance.
- Singleton pattern is used when a class in your program should have just a single instance available to all clients; for example, a single database object shared by different parts of the program.
- Singleton pattern is used for logging, driver objects, caching, thread pool, database connections.
  
#### Implementation
- The Singleton pattern is implemented by creating a class with a method that creates a new instance of the class if one doesn't exist. If an instance already exists, it simply returns a reference to that object.
  
```ts
class Singleton {
  private static instance: Singleton; // private static instance of the class

  private constructor() {} // private constructor to prevent instantiation of the class

  public static getInstance(): Singleton {
    if (!Singleton.instance) {
      Singleton.instance = new Singleton();
    }
    return Singleton.instance;
  }
}
```

#### Usage
```ts
const instance1 = Singleton.getInstance();
const instance2 = Singleton.getInstance();

console.log(instance1 === instance2); // Output: true
```

#### Real-world analogy
- The President of a country is a Singleton. There can only be one president for a country at a time. The same president is accessible from anywhere in the country.
- The Singleton pattern is used in the logging class. The logging class needs to write logs to the same file. A single file is created and written by multiple objects.
- The Singleton pattern is used in the database connections. A single database connection is shared by multiple objects.
- The Singleton pattern is used in the configuration classes. A single configuration object is used to read configuration values from the configuration file.