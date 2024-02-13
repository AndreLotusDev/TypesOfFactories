# C# Factory Design Patterns

This repository is dedicated to exploring the Factory Design Patterns in C#, specifically focusing on the Factory Method and Abstract Factory patterns. These patterns are instrumental in object-oriented design, allowing for the creation of objects without specifying the exact class of object that will be created. This promotes more flexible and scalable code. Below, you will find an overview of each pattern followed by C# examples demonstrating their use.

## Factory Method Pattern

The Factory Method Pattern defines an interface for creating an object but lets subclasses alter the type of objects that will be created. This pattern is particularly useful when a class cannot anticipate the class of objects it needs to create beforehand.

### Example

```csharp
// Product Interface
public interface IProduct
{
    string Operation();
}

// Concrete Products
public class ConcreteProductA : IProduct
{
    public string Operation()
    {
        return "Result of ConcreteProductA";
    }
}

public class ConcreteProductB : IProduct
{
    public string Operation()
    {
        return "Result of ConcreteProductB";
    }
}

// Creator Class
public abstract class Creator
{
    public abstract IProduct FactoryMethod();

    public string SomeOperation()
    {
        var product = FactoryMethod();
        return $"Creator: The same creator's code has just worked with {product.Operation()}";
    }
}

// Concrete Creators
public class ConcreteCreatorA : Creator
{
    public override IProduct FactoryMethod() => new ConcreteProductA();
}

public class ConcreteCreatorB : Creator
{
    public override IProduct FactoryMethod() => new ConcreteProductB();
}
```

## Abstract Factory Pattern

The Abstract Factory Pattern provides an interface for creating families of related or dependent objects without specifying their concrete classes. This pattern is useful for systems that need to be independent from how its products are created, composed, and represented.

### Example

```csharp
// Abstract Products
public interface IAbstractProductA
{
    string UsefulFunctionA();
}

public interface IAbstractProductB
{
    string AnotherUsefulFunctionB(IAbstractProductA collaborator);
}

// Concrete Products
public class ConcreteProductA1 : IAbstractProductA
{
    public string UsefulFunctionA() => "The result of the product A1.";
}

public class ConcreteProductB1 : IAbstractProductB
{
    public string AnotherUsefulFunctionB(IAbstractProductA collaborator) =>
        $"The result of the B1 collaborating with the ({collaborator.UsefulFunctionA()})";
}

// Abstract Factory
public interface IAbstractFactory
{
    IAbstractProductA CreateProductA();
    IAbstractProductB CreateProductB();
}

// Concrete Factory
public class ConcreteFactory1 : IAbstractFactory
{
    public IAbstractProductA CreateProductA() => new ConcreteProductA1();
    public IAbstractProductB CreateProductB() => new ConcreteProductB1();
}
```

## Usage

This repository contains implementations of both the Factory Method and Abstract Factory patterns. To run these examples, clone the repository, navigate to the respective project folder, and follow the instructions in each project's README for building and running the examples.

![image](https://user-images.githubusercontent.com/54090940/195242591-765ca150-3103-4038-b707-9a5e40a9d173.png)
![image](https://user-images.githubusercontent.com/54090940/195242599-2e38d7b3-f9ea-438e-8033-80dafaccbc11.png)
