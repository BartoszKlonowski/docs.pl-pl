---
title: Wyrażenie cyklicznie wywołuje zawierającą właściwość „<propertyname>”
ms.date: 07/20/2015
f1_keywords:
- vbc42026
- BC42026
helpviewer_keywords:
- BC42026
ms.assetid: 4fde9db6-3bf3-48dc-8e05-981bf08969da
ms.openlocfilehash: f5b8b226d46afa0555559de0930f20025ba27f2b
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/17/2020
ms.locfileid: "92162768"
---
# <a name="bc42026-expression-recursively-calls-the-containing-property-propertyname"></a><span data-ttu-id="4efc6-102">BC42026: wyrażenie cyklicznie wywołuje zawierającą właściwość " \<propertyname> "</span><span class="sxs-lookup"><span data-stu-id="4efc6-102">BC42026: Expression recursively calls the containing property '\<propertyname>'</span></span>

<span data-ttu-id="4efc6-103">Instrukcja w `Set` procedurze definicji właściwości przechowuje wartość w nazwie właściwości.</span><span class="sxs-lookup"><span data-stu-id="4efc6-103">A statement in the `Set` procedure of a property definition stores a value into the name of the property.</span></span>

 <span data-ttu-id="4efc6-104">Zalecanym podejściem do przechowywania wartości właściwości jest definiowanie `Private` zmiennej w kontenerze właściwości i użycie jej w `Get` `Set` procedurach i.</span><span class="sxs-lookup"><span data-stu-id="4efc6-104">The recommended approach to holding the value of a property is to define a `Private` variable in the property's container and use it in both the `Get` and `Set` procedures.</span></span> <span data-ttu-id="4efc6-105">`Set`Procedura powinna następnie przechowywać wartość przychodzącą w tej `Private` zmiennej.</span><span class="sxs-lookup"><span data-stu-id="4efc6-105">The `Set` procedure should then store the incoming value in this `Private` variable.</span></span>

 <span data-ttu-id="4efc6-106">`Get`Procedura zachowuje się jak `Function` procedura, dlatego może przypisywać wartości do nazwy właściwości i kontroli powrotu przez napotkanie `End Get` instrukcji.</span><span class="sxs-lookup"><span data-stu-id="4efc6-106">The `Get` procedure behaves like a `Function` procedure, so it can assign a value to the property name and return control by encountering the `End Get` statement.</span></span> <span data-ttu-id="4efc6-107">Zalecanym podejściem jest jednak uwzględnienie `Private` zmiennej jako wartości w [instrukcji return](../statements/return-statement.md).</span><span class="sxs-lookup"><span data-stu-id="4efc6-107">The recommended approach, however, is to include the `Private` variable as the value in a [Return Statement](../statements/return-statement.md).</span></span>

 <span data-ttu-id="4efc6-108">`Set`Procedura zachowuje się jak `Sub` procedura, która nie zwraca wartości.</span><span class="sxs-lookup"><span data-stu-id="4efc6-108">The `Set` procedure behaves like a `Sub` procedure, which does not return a value.</span></span> <span data-ttu-id="4efc6-109">W związku z tym, procedura lub nazwa właściwości nie ma specjalnego znaczenia w ramach `Set` procedury i nie można zapisać w niej wartości.</span><span class="sxs-lookup"><span data-stu-id="4efc6-109">Therefore, the procedure or property name has no special meaning within a `Set` procedure, and you cannot store a value into it.</span></span>

 <span data-ttu-id="4efc6-110">Poniższy przykład ilustruje podejście, które może spowodować wystąpienie tego błędu, a następnie zalecane podejście.</span><span class="sxs-lookup"><span data-stu-id="4efc6-110">The following example illustrates the approach that can cause this error, followed by the recommended approach.</span></span>

```vb
Public Class illustrateProperties
' The code in the following property causes this error.
    Public Property badProp() As Char
        Get
            Dim charValue As Char
            ' Insert code to update charValue.
            badProp = charValue
        End Get
        Set(ByVal Value As Char)
            ' The following statement causes this error.
            badProp = Value
            ' The value stored in the local variable badProp
            ' is not used by the Get procedure in this property.
        End Set
    End Property
' The following code uses the recommended approach.
    Private propValue As Char
    Public Property goodProp() As Char
        Get
            ' Insert code to update propValue.
            Return propValue
        End Get
        Set(ByVal Value As Char)
            propValue = Value
        End Set
    End Property
End Class
```

 <span data-ttu-id="4efc6-111">Domyślnie ten komunikat jest ostrzeżeniem.</span><span class="sxs-lookup"><span data-stu-id="4efc6-111">By default, this message is a warning.</span></span> <span data-ttu-id="4efc6-112">Aby uzyskać więcej informacji na temat ukrywania ostrzeżeń lub leczenia ostrzeżeń jako błędów, zobacz [Konfigurowanie ostrzeżeń w Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic).</span><span class="sxs-lookup"><span data-stu-id="4efc6-112">For more information about hiding warnings or treating warnings as errors, please see [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic).</span></span>

 <span data-ttu-id="4efc6-113">**Identyfikator błędu:** BC42026</span><span class="sxs-lookup"><span data-stu-id="4efc6-113">**Error ID:** BC42026</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="4efc6-114">Aby poprawić ten błąd</span><span class="sxs-lookup"><span data-stu-id="4efc6-114">To correct this error</span></span>

- <span data-ttu-id="4efc6-115">Zapisz definicję właściwości, aby użyć zalecanego podejścia, jak pokazano w powyższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="4efc6-115">Rewrite the property definition to use the recommended approach as illustrated in the preceding example.</span></span>

## <a name="see-also"></a><span data-ttu-id="4efc6-116">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="4efc6-116">See also</span></span>

- [<span data-ttu-id="4efc6-117">Procedury własności</span><span class="sxs-lookup"><span data-stu-id="4efc6-117">Property Procedures</span></span>](../../programming-guide/language-features/procedures/property-procedures.md)
- [<span data-ttu-id="4efc6-118">Property — Instrukcja</span><span class="sxs-lookup"><span data-stu-id="4efc6-118">Property Statement</span></span>](../statements/property-statement.md)
- [<span data-ttu-id="4efc6-119">Set — Instrukcja</span><span class="sxs-lookup"><span data-stu-id="4efc6-119">Set Statement</span></span>](../statements/set-statement.md)
