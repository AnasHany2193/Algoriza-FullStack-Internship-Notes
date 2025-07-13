## 📦 1. Classes & Objects

```csharp
class Customer
{
    string _firstName;
    string _lastName;

    // Default constructor chaining to parameterized one
    public Customer() : this("No FirstName", "No LastName") {}

    public Customer(string firstName, string lastName)
    {
        _firstName = firstName;
        _lastName = lastName;
    }

    public void PrintFullName()
    {
        Console.WriteLine($"Full Name: {_firstName} {_lastName}");
    }

    //~Customer() { ... } // Optional: Finalizer (avoid unless needed)
}
```

### 💡 Notes:

- Constructors can be chained using `: this(...)`
- Destructors (`~ClassName`) are called by the **garbage collector** and should be avoided unless managing unmanaged resources

---

## 🔄 2. Static vs. Instance Members

```csharp
class Circle
{
    static float _PI;
    int _radius;

    static Circle() => _PI = 3.14F;

    public Circle(int radius) => _radius = radius;

    public float CalculateArea() => _PI * _radius * _radius;
}
```

### 💡 Notes:

- Static constructor runs **once** when the class is first used
    
- Static fields are **shared** between all instances
    

---

## 🧬 3. Inheritance

```csharp
public class Employee {
    public string FirstName;
    public string LastName;

    public void PrintFullName() => Console.WriteLine($"{FirstName} {LastName}");
}

public class FullTimeEmployee : Employee {
    public float YearSalary;
}

public class PartTimeEmployee : Employee {
    public float HourlyRate;
}
```

### ✅ Best Practice:

Use inheritance when you have a **"is-a"** relationship.

---

## 🧯 4. Method Hiding (`new`)

```csharp
public class FullTimeEmployee : Employee {
    public new void PrintFullName() {
        Console.WriteLine($"{FirstName} {LastName} - Contractor");
    }
}
```

### ⚠️ Pitfall:

- `new` hides base method but does **not override** it.
- Avoid `new` unless intentional.

---

## 🔁 5. Polymorphism (Method Overriding)

```csharp
public class Employee {
    public virtual void PrintFullName() => Console.WriteLine("Base Print");
}

public class FullTimeEmployee : Employee {
    public override void PrintFullName() => Console.WriteLine("Full Time");
}
```

```csharp
Employee e = new FullTimeEmployee();
e.PrintFullName(); // "Full Time"
```

✅ Use `virtual` + `override` for **runtime polymorphism**

---

## 🆚 6. Override vs. Hidden

```csharp
BaseClass obj = new DerivedClass();
obj.OverridedPrint(); // Derived override
obj.HiddenPrint();    // Base version
```

- `override` respects runtime type
- `new` respects compile-time type

---

## ➕ 7. Method Overloading

```csharp
public static void Add(int a, int b) {...}
public static void Add(float a, float b) {...}
public static void Add(int a, int b, int c) {...}
```

✅ Use when method behavior is the same but parameter **types/quantity** differ.

---

## 🔐 8. Properties & Encapsulation

```csharp
public class Student {
    private int _id;
    private string _name;
    private readonly int _passMark = 35;

    public int Id {
        get => _id;
        set {
            if (value < 0)
                throw new Exception("Id can't be negative");
            _id = value;
        }
    }

    public string Name {
        get => string.IsNullOrEmpty(_name) ? "No Name" : _name;
        set {
            if (string.IsNullOrEmpty(value))
                throw new Exception("Name can't be empty");
            _name = value;
        }
    }

    public int PassMark => _passMark; // Read-only
}
```

---

## 🧱 9. Structs

```csharp
public struct Customer {
    public int Id { get; set; }
    public string Name { get; set; }

    public Customer(int id, string name) {
        Id = id;
        Name = name;
    }

    public void Print() => Console.WriteLine($"{Id} - {Name}");
}
```

### ✅ Struct vs Class

|Struct (Value Type)|Class (Reference Type)|
|---|---|
|Stored on **stack**|Stored on **heap**|
|Copied by value|Copied by reference|
|No inheritance|Supports inheritance|
|Default constructor not allowed|Allowed|

---

## 🔌 10. Interfaces

```csharp
interface ILogger {
    void Log();
}

class ConsoleLogger : ILogger {
    public void Log() => Console.WriteLine("Logged to Console");
}
```

### 💡 Explicit Interface Implementation

```csharp
void ILogger.Log() => Console.WriteLine("Logged explicitly");
```

✅ Use interfaces for **contract-based design** and **multiple inheritance**.

---

## 🧩 11. Abstract Classes

```csharp
public abstract class Customer {
    public abstract void Print();
}

public class GoldCustomer : Customer {
    public override void Print() => Console.WriteLine("Gold customer");
}
```

✅ Use when you want:

- Base class functionality
- Some methods enforced (`abstract`)

---

## ⚔️ 12. Abstract vs Interface

|Feature|Abstract Class|Interface|
|---|---|---|
|Can have fields|✅|❌|
|Constructors|✅|❌|
|Multiple inheritance|❌|✅|
|Method implementation|✅ (optional)|✅ (from C# 8)|
|Access modifiers|✅|❌|

---

## 🧨 13. Multiple Inheritance Problem

```csharp
// class D : B, C {} // ❌ Not allowed: multiple base classes
```

✅ Solution: Use interfaces

```csharp
class AB : IA, IB
{
    A a = new A();
    B b = new B();

    public void AMethod() => a.AMethod();
    public void BMethod() => b.BMethod();
}
```

---

## ✅ Best Practices Summary

| 👍 Good Practice                                     | ⚠️ Avoid                                          |
| ---------------------------------------------------- | ------------------------------------------------- |
| Use `properties` instead of public fields            | Exposing fields directly                          |
| Prefer `virtual/override` for polymorphism           | Using `new` unless needed                         |
| Use `interface` for multiple inheritance             | Using multiple base classes                       |
| Use `abstract` when you want partial implementations | Implementing everything in child classes manually |


---
**إِنَّ اللَّهَ وَمَلَائِكَتَهُ يُصَلُّونَ عَلَى النَّبِيِّ ۚ يَا أَيُّهَا الَّذِينَ آمَنُوا صَلُّوا عَلَيْهِ وَسَلِّمُوا تَسْلِيمًا (56)**