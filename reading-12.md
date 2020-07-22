# Dependency Injection

### Dependency: any object that another object requires.

##### Example:
public class MyDependency
{
    public MyDependency()
    {
    }

    public Task WriteMessage(string message)
    {
        Console.WriteLine(
            $"MyDependency.WriteMessage called. Message: {message}");

        return Task.FromResult(0);
    }
}

##### Dependency injection addresses several problems:

##### The use of an interface or base class to abstract the dependency implementation.
##### Registration of the dependency in a service container. 
##### Injection of the service into the constructor of the class where it's used.

##### Example:
public interface IMyDependency
{
    Task WriteMessage(string message);
}

##### Further:
public class MyDependency : IMyDependency
{
    private readonly ILogger<MyDependency> _logger;

    public MyDependency(ILogger<MyDependency> logger)
    {
        _logger = logger;
    }

    public Task WriteMessage(string message)
    {
        _logger.LogInformation(
            "MyDependency.WriteMessage called. Message: {MESSAGE}", 
            message);

        return Task.FromResult(0);
    }
}

##### Further examples are found at: https://docs.microsoft.com/en-us/aspnet/core/fundamentals/dependency-injection?view=aspnetcore-3.1

### Repositories

##### They are classes or components that encapsulate the logic required to access data sources.
##### If you use an Object-Relational Mapper like Entity Framework, the code that must be implemented is simplified due to Linq
##### For each aggregate or aggregate root, you should create one repository class.
##### A repository allows you to populate data in memory that comes from the database in the form of the domain entities.
##### Code Examples:
namespace Microsoft.eShopOnContainers.Services.Ordering.Infrastructure.Repositories
{
    public class OrderRepository : IOrderRepository
    {
      // ...
    }
}

##### Further:
public interface IOrderRepository : IRepository<Order>
{
    Order Add(Order order);
    // ...
}

### Repository Design Pattern

##### Data Access Objects: 
##### Example:
public interface ArticleDao {

    List<Article> readAll();

    List<Article> readLatest();

    List<Article> readByTags(Tag... tags);

    Article readById(long id);

    Article create(Article article);

    Article update(Article article);

    Article delete(Article article);

}

##### Abstraction: a generic abstract way for the app to work with the data layer.
##### Example:
public interface Repository<T> {
    List<T> readAll();

    T read(Criteria criteria);
    T create(T entity);
    T update(T entity);
    T delete(T entity);
}

### SOLID

##### Five Principles
##### Single Responsibility Principle
###### the idea that every method or class in your application should have exactly one reason to change

##### The Open/Close Principle
###### It states that software, be it a method or a class, should be open for extension, but closed to modification.

##### The Liskov Substitution Principle
###### Says an object in your application should be able to be replaced with a type derived from it without breaking the application. 

##### The Interface Segregation Principle
###### It makes fine grained interfaces that are specific to the functions and needs of the client.

##### The Dependency Inversion Principle
###### Says code should depend on abstractions; not concrete implementations. Furthermore, those abstractions should not depend on the details.

### The S.O.L.I.D Principles in Pictures

##### Link for illustrations is found here: https://medium.com/backticks-tildes/the-s-o-l-i-d-principles-in-pictures-b34ce2f1e898
