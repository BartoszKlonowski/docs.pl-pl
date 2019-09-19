---
title: 'Instrukcje: Utwórz podpisane zaprzyjaźnione zestawy'
ms.date: 08/19/2019
ms.assetid: bab62063-61e6-453f-905f-77673df9534e
dev_langs:
- csharp
- vb
ms.openlocfilehash: 19c301c6b96e1070447401af9105fba2e0f0837f
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/13/2019
ms.locfileid: "70973363"
---
# <a name="how-to-create-signed-friend-assemblies"></a><span data-ttu-id="3570b-102">Instrukcje: Utwórz podpisane zaprzyjaźnione zestawy</span><span class="sxs-lookup"><span data-stu-id="3570b-102">How to: Create signed friend assemblies</span></span>
<span data-ttu-id="3570b-103">Ten przykład pokazuje, jak używać zespołów zaprzyjaźnionych z zestawami o silnych nazwach.</span><span class="sxs-lookup"><span data-stu-id="3570b-103">This example shows how to use friend assemblies with assemblies that have strong names.</span></span> <span data-ttu-id="3570b-104">Oba zestawy muszą mieć silną nazwę.</span><span class="sxs-lookup"><span data-stu-id="3570b-104">Both assemblies must be strong named.</span></span> <span data-ttu-id="3570b-105">Chociaż oba zestawy w tym przykładzie używają tych samych kluczy, można użyć różnych kluczy dla dwóch zestawów.</span><span class="sxs-lookup"><span data-stu-id="3570b-105">Although both assemblies in this example use the same keys, you could use different keys for two assemblies.</span></span>  
  
## <a name="create-a-signed-assembly-and-a-friend-assembly"></a><span data-ttu-id="3570b-106">Tworzenie podpisanego zestawu i zestawu zaprzyjaźnionego</span><span class="sxs-lookup"><span data-stu-id="3570b-106">Create a signed assembly and a friend assembly</span></span>  
  
1. <span data-ttu-id="3570b-107">Otwórz wiersz polecenia.</span><span class="sxs-lookup"><span data-stu-id="3570b-107">Open a command prompt.</span></span>  
  
2. <span data-ttu-id="3570b-108">Użyj następującej sekwencji poleceń za pomocą narzędzia silnej nazwy, aby wygenerować KeyFile i wyświetlić jego klucz publiczny.</span><span class="sxs-lookup"><span data-stu-id="3570b-108">Use the following sequence of commands with the Strong Name tool to generate a keyfile and to display its public key.</span></span> <span data-ttu-id="3570b-109">Aby uzyskać więcej informacji, zobacz [SN. exe (Narzędzie silnej nazwy)](../../framework/tools/sn-exe-strong-name-tool.md).</span><span class="sxs-lookup"><span data-stu-id="3570b-109">For more information, see [Sn.exe (Strong Name tool)](../../framework/tools/sn-exe-strong-name-tool.md).</span></span>  
  
    1. <span data-ttu-id="3570b-110">Wygeneruj klucz o silnej nazwie dla tego przykładu i Zapisz go w pliku *FriendAssemblies. snk*:</span><span class="sxs-lookup"><span data-stu-id="3570b-110">Generate a strong-name key for this example and store it in the file *FriendAssemblies.snk*:</span></span>  
  
         `sn -k FriendAssemblies.snk`  
  
    2. <span data-ttu-id="3570b-111">Wyodrębnij klucz publiczny z *FriendAssemblies. snk* i umieść go w *FriendAssemblies. PublicKey*:</span><span class="sxs-lookup"><span data-stu-id="3570b-111">Extract the public key from *FriendAssemblies.snk* and put it into *FriendAssemblies.publickey*:</span></span>  
  
         `sn -p FriendAssemblies.snk FriendAssemblies.publickey`  
  
    3. <span data-ttu-id="3570b-112">Wyświetl klucz publiczny przechowywany w pliku *FriendAssemblies. PublicKey*:</span><span class="sxs-lookup"><span data-stu-id="3570b-112">Display the public key stored in the file *FriendAssemblies.publickey*:</span></span>  
  
         `sn -tp FriendAssemblies.publickey`  
  
3. <span data-ttu-id="3570b-113">Utwórz plik C# lub Visual Basic o nazwie *friend_signed_A* , który zawiera poniższy kod.</span><span class="sxs-lookup"><span data-stu-id="3570b-113">Create a C# or Visual Basic file named *friend_signed_A* that contains the following code.</span></span> <span data-ttu-id="3570b-114">Kod używa <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> atrybutu, aby zadeklarować *friend_signed_B* jako zestaw zaprzyjaźniony.</span><span class="sxs-lookup"><span data-stu-id="3570b-114">The code uses the <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> attribute to declare *friend_signed_B* as a friend assembly.</span></span>  
   
   <span data-ttu-id="3570b-115">Narzędzie silnej nazwy generuje nowy klucz publiczny przy każdym uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="3570b-115">The Strong Name tool generates a new public key every time it runs.</span></span> <span data-ttu-id="3570b-116">W związku z tym należy zastąpić klucz publiczny w poniższym kodzie kluczem publicznym, który został właśnie wygenerowany, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="3570b-116">Therefore, you must replace the public key in the following code with the public key you just generated, as shown in the following example.</span></span>  
   
   ```csharp  
   // friend_signed_A.cs  
   // Compile with:   
   // csc /target:library /keyfile:FriendAssemblies.snk friend_signed_A.cs  
   using System.Runtime.CompilerServices;  
   
   [assembly: InternalsVisibleTo("friend_signed_B, PublicKey=0024000004800000940000000602000000240000525341310004000001000100e3aedce99b7e10823920206f8e46cd5558b4ec7345bd1a5b201ffe71660625dcb8f9a08687d881c8f65a0dcf042f81475d2e88f3e3e273c8311ee40f952db306c02fbfc5d8bc6ee1e924e6ec8fe8c01932e0648a0d3e5695134af3bb7fab370d3012d083fa6b83179dd3d031053f72fc1f7da8459140b0af5afc4d2804deccb6")]  
   class Class1  
   {  
       public void Test()  
       {  
           System.Console.WriteLine("Class1.Test");  
           System.Console.ReadLine();  
       }  
   }  
   ```  
   
   ```vb  
   ' friend_signed_A.vb  
   ' Compile with:   
   ' Vbc -target:library -keyfile:FriendAssemblies.snk friend_signed_A.vb  
   Imports System.Runtime.CompilerServices  
   
   <Assembly: InternalsVisibleTo("friend_signed_B, PublicKey=0024000004800000940000000602000000240000525341310004000001000100e3aedce99b7e10823920206f8e46cd5558b4ec7345bd1a5b201ffe71660625dcb8f9a08687d881c8f65a0dcf042f81475d2e88f3e3e273c8311ee40f952db306c02fbfc5d8bc6ee1e924e6ec8fe8c01932e0648a0d3e5695134af3bb7fab370d3012d083fa6b83179dd3d031053f72fc1f7da8459140b0af5afc4d2804deccb6")>   
   Public Class Class1  
       Public Sub Test()  
           System.Console.WriteLine("Class1.Test")  
           System.Console.ReadLine()  
       End Sub  
   End Class  
   ```  
   
4. <span data-ttu-id="3570b-117">Kompiluj i podpisz *friend_signed_A* za pomocą następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="3570b-117">Compile and sign *friend_signed_A* by using the following command.</span></span>  
   
   ```csharp
   csc /target:library /keyfile:FriendAssemblies.snk friend_signed_A.cs  
   ```  
   
   ```vb
   Vbc -target:library -keyfile:FriendAssemblies.snk friend_signed_A.vb  
   ```  
   
5. <span data-ttu-id="3570b-118">Utwórz plik C# lub Visual Basic o nazwie *friend_signed_B* , który zawiera poniższy kod.</span><span class="sxs-lookup"><span data-stu-id="3570b-118">Create a C# or Visual Basic file named *friend_signed_B* that contains the following code.</span></span> <span data-ttu-id="3570b-119">Ponieważ *friend_signed_A* określa *friend_signed_B* jako zestaw zaprzyjaźniony, kod w *friend_signed_B* ma `internal` dostęp (C#) lub `Friend` (Visual Basic) typów i członków z *friend_signed_A*.</span><span class="sxs-lookup"><span data-stu-id="3570b-119">Because *friend_signed_A* specifies *friend_signed_B* as a friend assembly, the code in *friend_signed_B* can access `internal` (C#) or `Friend` (Visual Basic) types and members from *friend_signed_A*.</span></span> <span data-ttu-id="3570b-120">Plik zawiera poniższy kod.</span><span class="sxs-lookup"><span data-stu-id="3570b-120">The file contains the following code.</span></span>  
   
   ```csharp  
   // friend_signed_B.cs  
   // Compile with:   
   // csc /keyfile:FriendAssemblies.snk /r:friend_signed_A.dll /out:friend_signed_B.exe friend_signed_B.cs  
   public class Program  
   {  
       static void Main()  
       {  
           Class1 inst = new Class1();  
           inst.Test();  
       }  
   }  
   ```  
   
   ```vb  
   ' friend_signed_B.vb  
   ' Compile with:   
   ' Vbc -keyfile:FriendAssemblies.snk -r:friend_signed_A.dll friend_signed_B.vb  
   Module Sample  
       Public Sub Main()  
           Dim inst As New Class1  
           inst.Test()  
       End Sub  
   End Module  
   ```  
   
6. <span data-ttu-id="3570b-121">Kompiluj i podpisz *friend_signed_B* za pomocą następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="3570b-121">Compile and sign *friend_signed_B* by using the following command.</span></span>  
   
   ```csharp
   csc /keyfile:FriendAssemblies.snk /r:friend_signed_A.dll /out:friend_signed_B.exe friend_signed_B.cs  
   ```  
   
   ```vb
   vbc -keyfile:FriendAssemblies.snk -r:friend_signed_A.dll friend_signed_B.vb  
   ```  
   
   <span data-ttu-id="3570b-122">Nazwa zestawu wygenerowanego przez kompilator musi być zgodna z nazwą znajomego zestawu przekazaną <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> do atrybutu.</span><span class="sxs-lookup"><span data-stu-id="3570b-122">The name of the assembly generated by the compiler must match the friend assembly name passed to the <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> attribute.</span></span> <span data-ttu-id="3570b-123">Należy jawnie określić nazwę zestawu wyjściowego ( *. exe* lub *. dll*) przy użyciu `/out` opcji kompilatora.</span><span class="sxs-lookup"><span data-stu-id="3570b-123">You must explicitly specify the name of the output assembly (*.exe* or *.dll*) by using the `/out` compiler option.</span></span> <span data-ttu-id="3570b-124">Aby uzyskać więcej informacji, zobacz [/outC# (opcje kompilatora)](../../csharp/language-reference/compiler-options/out-compiler-option.md) lub [-out (Visual Basic)](../../visual-basic/reference/command-line-compiler/out.md).</span><span class="sxs-lookup"><span data-stu-id="3570b-124">For more information, see [/out (C# compiler options)](../../csharp/language-reference/compiler-options/out-compiler-option.md) or [-out (Visual Basic)](../../visual-basic/reference/command-line-compiler/out.md).</span></span>  
   
7. <span data-ttu-id="3570b-125">Uruchom plik *friend_signed_B. exe* .</span><span class="sxs-lookup"><span data-stu-id="3570b-125">Run the *friend_signed_B.exe* file.</span></span>  
   
   <span data-ttu-id="3570b-126">Program wyprowadza ciąg **Class1. test**.</span><span class="sxs-lookup"><span data-stu-id="3570b-126">The program outputs the string **Class1.Test**.</span></span>  
  
## <a name="net-security"></a><span data-ttu-id="3570b-127">Zabezpieczenia platformy .NET</span><span class="sxs-lookup"><span data-stu-id="3570b-127">.NET security</span></span>  
 <span data-ttu-id="3570b-128">Istnieją podobieństwa między <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> atrybutem <xref:System.Security.Permissions.StrongNameIdentityPermission> a klasą.</span><span class="sxs-lookup"><span data-stu-id="3570b-128">There are similarities between the <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> attribute and the <xref:System.Security.Permissions.StrongNameIdentityPermission> class.</span></span> <span data-ttu-id="3570b-129">Główną różnicą jest to <xref:System.Security.Permissions.StrongNameIdentityPermission> , że może to wymagać uprawnień zabezpieczeń do uruchomienia określonej sekcji kodu, <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> natomiast `internal` atrybut kontroluje widoczność (C#) lub `Friend` (Visual Basic) typów i elementów członkowskich.</span><span class="sxs-lookup"><span data-stu-id="3570b-129">The main difference is that <xref:System.Security.Permissions.StrongNameIdentityPermission> can demand security permissions to run a particular section of code, whereas the <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> attribute controls the visibility of `internal` (C#) or `Friend` (Visual Basic) types and members.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="3570b-130">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="3570b-130">See also</span></span>

- <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>
- [<span data-ttu-id="3570b-131">Zestawy w środowisku .NET</span><span class="sxs-lookup"><span data-stu-id="3570b-131">Assemblies in .NET</span></span>](index.md)
- [<span data-ttu-id="3570b-132">Zaprzyjaźnione zestawy</span><span class="sxs-lookup"><span data-stu-id="3570b-132">Friend assemblies</span></span>](friend.md)
- [<span data-ttu-id="3570b-133">Instrukcje: Utwórz niepodpisane zestawy zaprzyjaźnione</span><span class="sxs-lookup"><span data-stu-id="3570b-133">How to: Create unsigned friend assemblies</span></span>](create-unsigned-friend.md)
- [<span data-ttu-id="3570b-134">/keyfile (C#)</span><span class="sxs-lookup"><span data-stu-id="3570b-134">/keyfile (C#)</span></span>](../../csharp/language-reference/compiler-options/keyfile-compiler-option.md)
- [<span data-ttu-id="3570b-135">-keyfile (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="3570b-135">-keyfile (Visual Basic)</span></span>](../../visual-basic/reference/command-line-compiler/keyfile.md)
- [<span data-ttu-id="3570b-136">SN. exe (Narzędzie silnej nazwy)</span><span class="sxs-lookup"><span data-stu-id="3570b-136">Sn.exe (Strong Name tool)</span></span>](../../framework/tools/sn-exe-strong-name-tool.md)
- [<span data-ttu-id="3570b-137">Tworzenie i używanie zestawów o silnych nazwach</span><span class="sxs-lookup"><span data-stu-id="3570b-137">Create and use strong-named assemblies</span></span>](create-use-strong-named.md)
- [<span data-ttu-id="3570b-138">C#Przewodnik programowania</span><span class="sxs-lookup"><span data-stu-id="3570b-138">C# programming guide</span></span>](../../csharp/programming-guide/index.md)
- [<span data-ttu-id="3570b-139">Koncepcje programowania (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="3570b-139">Programming concepts (Visual Basic)</span></span>](../../visual-basic/programming-guide/concepts/index.md)