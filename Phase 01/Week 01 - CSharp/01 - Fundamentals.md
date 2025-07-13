## 🧱 1. Introduction

```csharp
class Program
{
    static void Main()
    {
        Console.Write("Hello, World!");
    }
}
```

> `Console.Write` writes without a new line. Use `Console.WriteLine` to write with a line break.

---

## 💬 2. Reading & Writing to Console

```csharp
// Write text and stay on the same line
Console.Write("Enter your name: ");

// Write text with a line break
Console.WriteLine("Welcome!");

// Read a full line of input
string name = Console.ReadLine();

// Read a single character (returns ASCII code)
int keyCode = Console.Read();
```

❗ `Console.Read()` is rarely used directly for integers. Prefer `int.Parse(Console.ReadLine())`.

---

## 📦 3. Built-in Data Types

```csharp
bool b = true;
int i = 123456789;
float f = 3.4e38f;         // ~7 digits
double d = 1.7e308;        // ~15-16 digits
decimal m = 300.5m;        // ~28-29 digits (use for money)
```

✅ Use `m` for `decimal`, and `f` for `float`.

---

## 🧵 4. Strings

```csharp
string quoted = "\"Anas\""; // Escape quotes
string multiline = "One\nTwo\nThree"; // New lines
string path = @"D:\FullStack-Dev\03-JavaScript"; // Verbatim string
```

✅ Use `@` to write file paths without escaping `\\`.

---

## ❓ 5. Nullable Types

```csharp
int? numOfCars = 100;
int availableCars = numOfCars ?? 0; // null-coalescing operator
```

✅ Use `??` to provide fallback values when nullable variables are `null`.

---

## 🔄 6. Type Conversion

```csharp
int i = 100;
float f = i; // Implicit
int j = (int)f; // Explicit cast

string s = "100";
int k = int.Parse(s); // Throws if invalid

// Safe parsing
int.TryParse(s, out int result);
```

⚠️ `int.Parse` throws an exception if input is not valid. Use `TryParse` instead.

---

## 📚 7. Arrays

```csharp
int[] numbers = new int[3];

numbers[0] = 1;
numbers[1] = 2;
numbers[2] = 3;
```

✅ Arrays are fixed size and zero-indexed.

---

## 🔁 8. Conditionals

### `if` Statement

```csharp
int num = int.Parse(Console.ReadLine());

if (num == 10 || num == 20)
{
    Console.WriteLine("Number is 10 or 20");
}
```

### `switch` Statement

```csharp
int num = int.Parse(Console.ReadLine());

switch (num)
{
    case 10:
        Console.WriteLine("Number is 10");
        break;
    case 20:
        Console.WriteLine("Number is 20");
        break;
    default:
        Console.WriteLine("Not 10 or 20");
        break;
}
```

---

## 🔂 9. Loops

### `while` Loop

```csharp
int i = 0;
while (i <= 10)
{
    Console.WriteLine(i);
    i += 2;
}
```

### `do-while` Loop

```csharp
int i = 0;
do
{
    Console.WriteLine(i);
    i += 2;
} while (i <= 10);
```

### `for` & `foreach` Loops

```csharp
for (int i = 0; i < numbers.Length; i++)
{
    Console.WriteLine(numbers[i]);
}

foreach (int n in numbers)
{
    Console.WriteLine(n);
}
```

✅ Use `foreach` when you don’t need the index.

---

## 🧮 10. Methods

```csharp
public static void PrintNumbers()
{
    for (int i = 0; i < 10; i++)
    {
        Console.WriteLine(i);
    }
}
```

---

## 🧪 11. Method Parameters

```csharp
public static void Main()
{
    int i = 0;

    Value(i);
    Console.WriteLine("Value: " + i); // 0

    Reference(ref i);
    Console.WriteLine("Ref: " + i); // 1

    Calc(i, 2, out int sum, out int mul);
    Console.WriteLine($"Sum = {sum}, Product = {mul}"); // 3, 2

    ArrParam(1, 2, 3, 4);
}

public static void Value(int j) => j += 1;

public static void Reference(ref int j) => j += 1;

public static void Calc(int a, int b, out int sum, out int mul)
{
    sum = a + b;
    mul = a * b;
}

public static void ArrParam(params int[] values)
{
    Console.WriteLine($"Count = {values.Length}");
    foreach (int val in values)
        Console.Write($"[{val}] ");
}
```

✅ `ref` requires initialization.  
✅ `out` allows returning multiple values.  
✅ `params` allows variable-length arguments.

---

## 📦 12. Namespaces

```csharp
using ProjectA.TeamA;
using ProjectA.TeamB;

class Program
{
    static void Main()
    {
        ClassA.Print();
        ClassB.Print();
    }
}

namespace ProjectA
{
    namespace TeamA
    {
        class ClassA
        {
            public static void Print()
            {
                Console.WriteLine("Team A Print");
            }
        }
    }

    namespace TeamB
    {
        class ClassB
        {
            public static void Print()
            {
                Console.WriteLine("Team B Print");
            }
        }
    }
}
```

✅ Namespaces help organize code into logical groups.

---

## 📌 Summary of Best Practices

|✅ Do|⚠️ Avoid|
|---|---|
|Use `TryParse` over `Parse`|Using `Parse` without exception handling|
|Use `ref`, `out` and `params` properly|Changing parameters inside `ref` when unnecessary|
|Escape strings and paths properly|Forgetting `@` in Windows paths|
|Use meaningful variable/method names|Using generic names like `i`, `a`, `b` without context|
|Organize methods and logic into namespaces|Putting all code in `Main`|

---
**إِنَّ اللَّهَ وَمَلَائِكَتَهُ يُصَلُّونَ عَلَى النَّبِيِّ ۚ يَا أَيُّهَا الَّذِينَ آمَنُوا صَلُّوا عَلَيْهِ وَسَلِّمُوا تَسْلِيمًا (56)**
