## 1. Delegates 🎯

### 🔹 Basics

```csharp
public delegate void HelloDelegate(string message);

HelloDelegate del = Hello;
del("Hello, World!");

static void Hello(string msg) => Console.WriteLine(msg);
```

- **Delegate** = safe function pointer; must match the method signature ([Medium](https://medium.com/c-sharp-programming/mastering-delegates-in-c-a-developers-guide-to-best-practices-fc0d29ed9da2?utm_source=chatgpt.com "Mastering Delegates in C#: A Developer's Guide to Best Practices"), [Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/delegates/using-delegates?utm_source=chatgpt.com "Using Delegates (C# Programming Guide) - Learn Microsoft")).
    
- Useful for **callbacks, events, and strategy patterns**.
    

### 🔹 Usage & Multicast

```csharp
public delegate bool IsPromotable(Employee emp);
Employee.PromoteEmployee(employees, Promote);

public delegate void SampleDelegate();
SampleDelegate sd = SampleMethod1;
sd += SampleMethod2;
sd();
```

- For passing behavior as parameters. Equivalent to `Func<T, bool>` or `Action<>` in many cases ([ScholarHat](https://www.scholarhat.com/tutorial/csharp/reflection-in-csharp?utm_source=chatgpt.com "Understanding Reflection in C#: A Comprehensive Guide - ScholarHat"), [Stack Overflow](https://stackoverflow.com/questions/1295358/best-practices-when-should-i-use-a-delegate-in-net?utm_source=chatgpt.com "Best practices: When should I use a delegate in .NET? [duplicate]")).
    
- **Multicast delegates** invoke multiple methods; exceptions in one stop following calls — handle carefully ([Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/csharp/delegates-patterns?utm_source=chatgpt.com "Common Patterns for Delegates - C# | Microsoft Learn")).
    

### 💡 Best Practices & Pitfalls

- ✅ Prefer `Func<>` and `Action<>` for simple use cases ([Medium](https://medium.com/c-sharp-programming/mastering-delegates-in-c-a-developers-guide-to-best-practices-fc0d29ed9da2?utm_source=chatgpt.com "Mastering Delegates in C#: A Developer's Guide to Best Practices")).
    
- ⚠️ Don’t overuse delegates when a simple method call would suffice; they can reduce readability ([Software Engineering Stack Exchange](https://softwareengineering.stackexchange.com/questions/250079/are-the-over-usage-of-delegates-a-bad-thing?utm_source=chatgpt.com "c# - Are the over-usage of delegates a bad thing?")).
    
- ⚠️ Make sure to check for null before invocation: `del?.Invoke(...)` ([Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/csharp/delegates-patterns?utm_source=chatgpt.com "Common Patterns for Delegates - C# | Microsoft Learn")).
    

---

## 2. Exception Handling 🛠️

```csharp
try {
    using var reader = new StreamReader(path);
    Console.WriteLine(reader.ReadToEnd());
}
catch (FileNotFoundException ex) {
    Console.WriteLine($"File not found: {ex.FileName}");
}
catch (Exception ex) {
    Console.WriteLine(ex.Message);
}
finally {
    Console.WriteLine("Cleanup, if needed");
}
```

### 🔹 Inner Exceptions

- Wrap exceptions to preserve detailed errors:
    
    ```csharp
    catch (Exception ex) {
        Console.WriteLine(ex.InnerException?.GetType());
    }
    ```
    

### 🔹 Custom Exceptions

```csharp
public class UserAlreadyLoggedInException : Exception
{
    public UserAlreadyLoggedInException(string msg) : base(msg) { }
    // Include innerException and serialization constructors
}
```

### 💡 Best Practices

- ✅ Catch specific exceptions, do not catch generic `Exception` unless rethrowing.
    
- ✅ Use `using` where possible instead of manual `finally` cleanup.
    
- ⚠️ Rethrow exceptions using `throw;` — not `throw ex;` — to preserve the stack trace.
    
- ⚠️ Provide meaningful exception messages and optionally include inner exceptions.
    

---

## 3. Enums & Attributes

### 🔹 Enums

```csharp
public enum Gender { Unknown, Male, Female }
Gender g = (Gender)3; // Valid numeric cast
int code = (int)Gender.Unknown;
```

✅ Use enums to represent named constants.

### 🔹 Attributes

```csharp
[Obsolete("Use Add(List<int>)")]
public static int Add(int a, int b) => a + b;
```

⚠️ Fine-grained control at compile-time; avoid deprecated methods.

---

## 4. Reflection & Late Binding

### 🔹 Reflection

```csharp
Type type = obj.GetType();
Console.WriteLine(type.Name);
foreach (var p in type.GetProperties())
    Console.WriteLine($"{p.Name} = {p.GetValue(obj)}");
```

- Like a **backstage pass** to inspect types at runtime ([Reddit](https://www.reddit.com/r/csharp/comments/bj14ea/reflection/?utm_source=chatgpt.com "Reflection : r/csharp - Reddit"), [Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/csharp/delegates-patterns?utm_source=chatgpt.com "Common Patterns for Delegates - C# | Microsoft Learn"), [dotnetfullstackdev.medium.com](https://dotnetfullstackdev.medium.com/what-is-reflection-in-c-86240d96d8b4?utm_source=chatgpt.com "What is Reflection in C#. Reflection emerges as a powerful tool…")).
    
- Powerful but **slow**; use only when necessary ([Level Up Coding](https://levelup.gitconnected.com/reflection-in-c-when-and-why-you-should-or-shouldnt-use-it-37bb3efa130d?utm_source=chatgpt.com "Reflection in C#: When and Why You Should (or Shouldn't) Use It")).
    

### 🔹 Late & Dynamic Binding

```csharp
object plugin = new PluginA();
var method = plugin.GetType().GetMethod("Execute");
method?.Invoke(plugin, null);

dynamic pluginDyn = new PluginA();
pluginDyn.Execute();
```

✅ Use reflection for plugin systems, dynamic object mapping, and test frameworks; fallback to interfaces and generics when possible.

---

## 5. Generics

```csharp
public static bool AreEqual<T>(T a, T b) => a.Equals(b);
```

- Enables **type-safe, reusable** code structures.
    
- ✅ Use generics over `object` casting when type flexibility is needed.
    

---

## 6. Partial Classes & Methods

### 🔹 Partial Classes

```csharp
// File A
public partial class UserManager { public void Save(User u) { } }

// File B
public partial class UserManager { public bool Validate(User u){...} }
```

### 🔹 Partial Methods

```csharp
public partial class MyClass {
    partial void OnCreated();
    public MyClass() => OnCreated();
}

// In another file:
public partial class MyClass {
    partial void OnCreated() => Console.WriteLine("Created");
}
```

✅ Great for code generation and splitting responsibilities.

---

## 7. Indexers

```csharp
public string this[int id] {
    get => employees.First(emp => emp.Id == id).Name;
    set => employees.First(emp => emp.Id == id).Name = value;
}
```

✅ Clean syntax for custom collection access.

---

## 8. Collections: List & Dictionary

### 🔹 List

```csharp
List<Customer> lst = new() { c1, c2 };
foreach (var c in lst) Console.WriteLine(c.Name);
```

### 🔹 Dictionary<TKey, TValue>

```csharp
var dict = new Dictionary<int, Customer> { [c1.Id] = c1 };
if (dict.TryGetValue(101, out var cust))
    Console.WriteLine(cust.Name);
else Console.WriteLine("Key not found");
```

✅ Prefer `TryGetValue`, avoid exceptions for missing keys.

---
## 9. Optional Parameters 🧮

### 🔹 What Are They?

Optional parameters allow you to **omit** some arguments when calling a method. These parameters must have **default values**.

```csharp
public void Greet(string name = "Guest", int times = 1) {
    for (int i = 0; i < times; i++)
        Console.WriteLine($"Hello, {name}!");
}

// Usage
Greet();                     // Hello, Guest!
Greet("Anas");               // Hello, Anas!
Greet("Anoos", 3);           // Hello, Anoos! (3 times)
```

### 🔸 Rules

- Optional parameters **must come last**.
    
- Default values must be **compile-time constants**.
    

```csharp
// ❌ Invalid
// public void Test(int x = 5, string name);  // Error: non-optional cannot follow optional

// ✅ Valid
public void Test(string name, int x = 5) { ... }
```

### 💡 Best Practices

- ✅ Use when the overload doesn’t justify a separate method.
    
- ✅ Great for APIs and helper methods.
    
- ⚠️ Don’t overuse — too many optional parameters make code hard to read and maintain.
    
- ⚠️ Be careful with **method overloading** + optional parameters — compiler may get confused.
    

### 📎 Alternative: Named Parameters

```csharp
Greet(times: 2);         // Hello, Guest! (2 times)
Greet(name: "Anas");     // Hello, Anas!
```

---

## 10. Overriding `ToString()` & `Equals()` 🎯

### 🔹 `ToString()` — Object to String

Override this method to provide a **meaningful string representation** of your object.

```csharp
public class Customer {
    public int Id { get; set; }
    public string Name { get; set; }

    public override string ToString() {
        return $"Customer [Id={Id}, Name={Name}]";
    }
}

// Usage
Customer c = new Customer { Id = 1, Name = "Anas" };
Console.WriteLine(c); // Customer [Id=1, Name=Anas]
```

### 💡 Best Practices

- ✅ Always override `ToString()` in models, DTOs, and logs.
- ⚠️ Avoid exposing sensitive data (like passwords or tokens).

### 🔹 `Equals()` — Object Equality

Override `Equals()` to define **custom equality** logic between instances.

```csharp
public class Point {
    public int X { get; set; }
    public int Y { get; set; }

    public override bool Equals(object obj) {
        if (obj is not Point other) return false;
        return this.X == other.X && this.Y == other.Y;
    }

    public override int GetHashCode() {
        return HashCode.Combine(X, Y); // or use a manual XOR for older versions
    }
}

// Usage
var p1 = new Point { X = 1, Y = 2 };
var p2 = new Point { X = 1, Y = 2 };
Console.WriteLine(p1.Equals(p2)); // True
```

### ✅ Always override both `Equals()` and `GetHashCode()` **together**.

Why?

- `Equals()` checks for logical equality.
- `GetHashCode()` is used in hash-based collections like `Dictionary`, `HashSet`.

### 🔸 Shortcut in C# 9+ — `record` Type

```csharp
public record Person(string Name, int Age);

var p1 = new Person("Anas", 25);
var p2 = new Person("Anas", 25);
Console.WriteLine(p1 == p2); // True — structural equality
```

### 📌 Summary

| Method          | Purpose                         | Override When...                                   |
| --------------- | ------------------------------- | -------------------------------------------------- |
| `ToString()`    | Convert object to string        | You want readable/loggable output                  |
| `Equals()`      | Compare object content equality | You want custom logic for comparing objects        |
| `GetHashCode()` | Used in hash-based collections  | You override `Equals()` — always override this too |

---
### ✅ Summary of Best Practices

| Feature          | Use When...                                  | Avoid...                                  |
| ---------------- | -------------------------------------------- | ----------------------------------------- |
| Delegates/Func<> | Passing behavior as parameter or callbacks   | Overuse—simple calls work better          |
| Exception        | Specific handling, rethrow with stack intact | Catch-all and swallow exceptions          |
| Reflection       | Dynamic loading, plugin, metadata discovery  | Reflection in performance-critical loops  |
| Generics         | Type-safe reusable code                      | Casting from object                       |
| Partial          | Splitting auto-generated and manual code     | Overuse—can make codebase confusing       |
| Indexers         | Friendly collection access syntax            | Indexers doing heavy or side-effect logic |
| Collections      | Use generic collections                      | Avoid non-generic or manual collections   |
| Overrides        | Provide meaningful comparisons               | Overrides without updating GetHashCode    |

---
**إِنَّ اللَّهَ وَمَلَائِكَتَهُ يُصَلُّونَ عَلَى النَّبِيِّ ۚ يَا أَيُّهَا الَّذِينَ آمَنُوا صَلُّوا عَلَيْهِ وَسَلِّمُوا تَسْلِيمًا (56)**
