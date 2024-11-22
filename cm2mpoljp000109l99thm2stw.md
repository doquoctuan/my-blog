---
title: "10 Advanced C# Snippets  Developer Productivity"
datePublished: Thu Oct 24 2024 02:56:08 GMT+0000 (Coordinated Universal Time)
cuid: cm2mpoljp000109l99thm2stw
slug: 10-advanced-c-snippets-developer-productivity
tags: csharp

---

### 1. Pattern Matching with `switch` Expressions

```
public string GetUserType(User user) =>
    user switch
    {
        { IsAdmin: true } => "Admin",
        { IsPremium: true } => "Premium",
        _ => "Regular"
    };
```

### 2. `Span<T>` for Memory-efficient Data Manipulation

```
Span<int> numbers = stackalloc int[] { 1, 2, 3, 4, 5 };
for (int i = 0; i < numbers.Length; i++)
{
    Console.WriteLine(numbers[i]);
}
```

### 3. Local functions for Better Code Structure

```
public void ProcessData()
{
    Validate();

    void Validate()
    {
        // Validation logic
    }
}
```

### 4. Async Stream with `IAsyncEnumerable<T>`

Efficiently handle large data streams asynchronously

```
public async IAsyncEnumerable<int> GetNumbersAsync()
{
    for (int i = 0; i < 10; i++)
    {
        await Task.Delay(100); // Simulate async work
        yield return i;
    }
}
```

### 5. Records for Immutable Data Structure

```
public record User(string Name, int Age);
```

### 6. `Task.WhenAll()` for Parallel Async Operations

```
public async Task ProcessDataAsync()
{
    var tasks = new List<Task>
    {
        Task1(),
        Task2(),
        Task3()
    };

    await Task.WhenAll(tasks);
}
```

### 7. Nullable Reference Types

```
public void ProcessUser(User? user)
{
    if (user is not null)
    {
        Console.WriteLine(user.Name);
    }
}
```

### 8. `Parallel.ForEach` for Multithreading

```
Parallel.ForEach(dataList, data =>
{
    ProcessData(data);
});
```

### 9. Dependency Injection in ASP.NET Core

```
public class Startup
{
    public void ConfigureServices(IServiceCollection services)
    {
        services.AddScoped<IMyService, MyService>();
    }
}
```

### 10. Expression Trees for Dynamic Code Generation

```
var param = Expression.Parameter(typeof(int), "x");
var body = Expression.Multiply(param, Expression.Constant(2));
var lambda = Expression.Lambda<Func<int, int>>(body, param).Compile();
Console.WriteLine(lambda(5)); // Outputs: 10
```




