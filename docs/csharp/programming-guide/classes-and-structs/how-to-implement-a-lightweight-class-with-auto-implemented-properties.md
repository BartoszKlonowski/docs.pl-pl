---
title: Jak zaimplementować klasę uproszczoną przy użyciu właściwości, które są implementowane — Przewodnik programowania w języku C#
description: Informacje o sposobie tworzenia niezmiennej klasy lekkiej w języku C#, która hermetyzuje zaimplementowane właściwości. Istnieją dwie podejścia implementacji.
ms.date: 07/20/2015
helpviewer_keywords:
- auto-implemented properties [C#]
- properties [C#], auto-implemented
ms.topic: how-to
ms.custom: contperf-fy21q2
ms.assetid: 1dc5a8ad-a4f7-4f32-8506-3fc6d8c8bfed
ms.openlocfilehash: 4b28ee17f4be2b933373cce0d3670cbfa9a12895
ms.sourcegitcommit: d0990c1c1ab2f81908360f47eafa8db9aa165137
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/15/2020
ms.locfileid: "97513045"
---
# <a name="how-to-implement-a-lightweight-class-with-auto-implemented-properties-c-programming-guide"></a>Jak zaimplementować klasę uproszczoną z właściwościami, które są implementowane przez autoimplementację (Przewodnik programowania w języku C#)

Ten przykład przedstawia sposób tworzenia niezmiennej klasy lekkiej, która służy tylko do hermetyzacji zestawu właściwości, które są implementowane. Użyj tego rodzaju konstrukcji zamiast struktury, gdy musisz użyć semantyki typu odwołania.

Można wprowadzić niemodyfikowalną właściwość na dwa sposoby:

- Można zadeklarować metodę dostępu [Set](../../language-reference/keywords/set.md) jako [prywatną](../../language-reference/keywords/private.md).  Właściwość jest tylko settable w obrębie typu, ale jest niezmienna dla odbiorców.

  W przypadku deklarowania prywatnej `set` metody dostępu nie można użyć inicjatora obiektów do zainicjowania właściwości. Musisz użyć konstruktora lub metody fabryki.
- Można zadeklarować tylko metodę dostępu [Get](../../language-reference/keywords/get.md) , która sprawia, że właściwość jest niezmienna wszędzie z wyjątkiem konstruktora typu.

W poniższym przykładzie pokazano, w jaki sposób właściwość z akcesorem Get różni się od typu GET i Private.

```csharp
class Contact
{
    public string Name { get; }
    public string Address { get; private set; }

    public Contact(string contactName, string contactAddress)
    {
        // Both properties are accessible in the constructor.
        Name = contactName;
        Address = contactAddress;
    }

    // Name isn't assignable here. This will generate a compile error.
    //public void ChangeName(string newName) => Name = newName;

    // Address is assignable here.
    public void ChangeAddress(string newAddress) => Address = newAddress
}
```

## <a name="example"></a>Przykład

Poniższy przykład przedstawia dwa sposoby implementacji niezmiennej klasy, która ma właściwości, które są implementowane. Każdy ze sposobów deklaruje jedną z właściwości z prywatną `set` i jedną z właściwości tylko z `get` .  Pierwsza klasa używa konstruktora tylko w celu zainicjowania właściwości, a druga Klasa używa metody fabryki statycznej, która wywołuje konstruktora.

```csharp
// This class is immutable. After an object is created,
// it cannot be modified from outside the class. It uses a
// constructor to initialize its properties.
class Contact
{
    // Read-only property.
    public string Name { get; }

    // Read-write property with a private set accessor.
    public string Address { get; private set; }

    // Public constructor.
    public Contact(string contactName, string contactAddress)
    {
        Name = contactName;
        Address = contactAddress;
    }
}

// This class is immutable. After an object is created,
// it cannot be modified from outside the class. It uses a
// static method and private constructor to initialize its properties.
public class Contact2
{
    // Read-write property with a private set accessor.
    public string Name { get; private set; }

    // Read-only property.
    public string Address { get; }

    // Private constructor.
    private Contact2(string contactName, string contactAddress)
    {
        Name = contactName;
        Address = contactAddress;
    }

    // Public factory method.
    public static Contact2 CreateContact(string name, string address)
    {
        return new Contact2(name, address);
    }
}

public class Program
{
    static void Main()
    {
        // Some simple data sources.
        string[] names = {"Terry Adams","Fadi Fakhouri", "Hanying Feng",
                            "Cesar Garcia", "Debra Garcia"};
        string[] addresses = {"123 Main St.", "345 Cypress Ave.", "678 1st Ave",
                                "12 108th St.", "89 E. 42nd St."};

        // Simple query to demonstrate object creation in select clause.
        // Create Contact objects by using a constructor.
        var query1 = from i in Enumerable.Range(0, 5)
                    select new Contact(names[i], addresses[i]);

        // List elements cannot be modified by client code.
        var list = query1.ToList();
        foreach (var contact in list)
        {
            Console.WriteLine("{0}, {1}", contact.Name, contact.Address);
        }

        // Create Contact2 objects by using a static factory method.
        var query2 = from i in Enumerable.Range(0, 5)
                        select Contact2.CreateContact(names[i], addresses[i]);

        // Console output is identical to query1.
        var list2 = query2.ToList();

        // List elements cannot be modified by client code.
        // CS0272:
        // list2[0].Name = "Eugene Zabokritski";

        // Keep the console open in debug mode.
        Console.WriteLine("Press any key to exit.");
        Console.ReadKey();
    }
}

/* Output:
    Terry Adams, 123 Main St.
    Fadi Fakhouri, 345 Cypress Ave.
    Hanying Feng, 678 1st Ave
    Cesar Garcia, 12 108th St.
    Debra Garcia, 89 E. 42nd St.
*/
```

Kompilator tworzy pola kopii zapasowej dla każdej automatycznie zaimplementowanej właściwości. Pola są niedostępne bezpośrednio z kodu źródłowego.

## <a name="see-also"></a>Zobacz też

- [Właściwości](./properties.md)
- [konstrukcja](../../language-reference/builtin-types/struct.md)
- [Inicjatory obiektów i kolekcji](./object-and-collection-initializers.md)
