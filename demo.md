# Attribute trong C#

---

## 1 Định nghĩa:

> Attribute được sử dụng trong c# để truyền đạt thông tin khai báo hoặc metadata về các phần tử mã khác nhay như method, asemblies, properties. Các thuộc tính được thêm vào bằng cách sử dụng thẻ khai báo được đặt bằng dấu ngoặc vuông.

## 2 Xác đinh một Attribute:

Cú pháp:

```csharp
[attribute(positional_parameter, name_parameter = giá_trị, ...)]
element
```

## 3 Attibute được định nghĩa trong c#

### 3.1 AtributeUsage

> Attribute được định nghĩa trước AttributeUsage miêu tả cách một lớp custom Attribute có thể được sử dụng. Nó xác định kiểu của các item, mà từ đó Attribute có thể áp dụng cho.

```csharp
- Cú pháp
[AttributeUsage(
   validon,
   AllowMultiple=allowmultiple,
   Inherited=inherited
)]
```

### 3.2 Conditional

> Attribute tiền định nghĩa này đánh dấu một phương thức có điều kiện mà sự thực thi của nó phụ thuộc vào một tiến trình tiền xử lý định danh đã cho.

- Cú pháp:

````csharp
[Conditional(
   conditionalSymbol
)]
> Ví dụ
- Lớp TestAttribute:
```csharp
#define DEBUG
using System;
using System.Diagnostics;

namespace DemoCondtional
{
    class TestAttribute
    {
        [Conditional("DEBUG")]
        public static void Message(string msg)
        {
            Console.WriteLine(msg);
        }
    }
}
````

- Lớp TestC#:

```csharp
using System;

namespace DemoCondtional
{
    class TestCsharp
    {
        static void function1()
        {
            TestAttribute.Message("Trong Function 1.");
            function2();
        }
        static void function2()
        {
            TestAttribute.Message("Trong Function 2.");
        }

        public static void Main()
        {
            Console.WriteLine("Attribute trong C#");
            Console.WriteLine("-----------------------");

            TestAttribute.Message("Trong ham Main.");
            function1();
            Console.ReadKey();
        }
    }
}
```

### 3.3 Obsolete

> Obsolete attribute được sử dụng để đánh dấu các phương thức, lớp hoặc thuộc tính đã bị lỗi thời hoặc không nên sử dụng nữa.
> Ví dụ: Giả sử có một lớp Calculator với phương thức Add() đã bị lỗi thời và không được khuyến khích sử dụng nữa. Ta đánh dấu phuowgn thức này với Absolete attribute như sau:

```csharp
public class Calculator
{
    [Obsolete("The Add() method is deprecated, please use the AddNumbers() method instead.")]
    public int Add(int x, int y)
    {
        return x + y;
    }

    public int AddNumbers(int x, int y)
    {
        return x + y;
    }
}
```

## 4 Custom Attribute trong c#:

> Custom Attribute là Attribute tùy biến hay Attribute do người dùng tự định nghĩa.

- Tạo Custom Attribute trong c# bao gồm 4 bước sau:

* Khai báo một Custom Attribute
* Xây dựng Custom Attribute
* Áp dụng Custom Attribute trên một phần tử chương trình target
* Truy cập các Attribute thông qua Reflection

- Ví dụ: Tạo 1 Custom Attribute được kế thừa từ lớp System.Attribute trong c#.

* Bước 1, Khai báo Attribute:

```csharp
//a custom attribute BugFix to be assigned to a class and its members
[AttributeUsage(AttributeTargets.Class |
AttributeTargets.Constructor |
AttributeTargets.Field |
AttributeTargets.Method |
AttributeTargets.Property,
AllowMultiple = true)]

public class DeBugInfo : System.Attribute
```

- Bước 2, Xây dựng Attribute:
  > Mỗi Attribute phải có ít nhất một contructor. Các tham số vị trí tương ứng của lớp nên được truyền thông qua contructor đó.

```csharp
//Vi du minh hoa mot custom attribute BugFix
[AttributeUsage(AttributeTargets.Class |
AttributeTargets.Constructor |
AttributeTargets.Field |
AttributeTargets.Method |
AttributeTargets.Property,
AllowMultiple = true)]

public class DeBugInfo : System.Attribute
{
   private int bugNo;
   private string developer;
   private string lastReview;
   public string message;

   public DeBugInfo(int bg, string dev, string d)
   {
      this.bugNo = bg;
      this.developer = dev;
      this.lastReview = d;
   }

   public int BugNo
   {
      get
      {
         return bugNo;
      }
   }

   public string Developer
   {
      get
      {
         return developer;
      }
   }

   public string LastReview
   {
      get
      {
         return lastReview;
      }
   }

   public string Message
   {
      get
      {
         return message;
      }
      set
      {
         message = value;
      }
   }
}
```

- Bước 3, Áp dụng:
  > Áp dụng bằng việc đặt nó ngay trước tartget của nó.

```csharp
//Vi du minh hoa mot custom attribute BugFix
[AttributeUsage(AttributeTargets.Class |
AttributeTargets.Constructor |
AttributeTargets.Field |
AttributeTargets.Method |
AttributeTargets.Property,
AllowMultiple = true)]

public class DeBugInfo : System.Attribute
{
   private int bugNo;
   private string developer;
   private string lastReview;
   public string message;

   public DeBugInfo(int bg, string dev, string d)
   {
      this.bugNo = bg;
      this.developer = dev;
      this.lastReview = d;
   }

   public int BugNo
   {
      get
      {
         return bugNo;
      }
   }

   public string Developer
   {
      get
      {
         return developer;
      }
   }

   public string LastReview
   {
      get
      {
         return lastReview;
      }
   }

   public string Message
   {
      get
      {
         return message;
      }
      set
      {
         message = value;
      }
   }
}
```
