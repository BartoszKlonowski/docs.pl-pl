---
title: 'Instrukcje: Dodawanie lub usuwanie pozycji listy Access Control (tylko .NET Framework)'
ms.date: 01/14/2019
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- ACEs [.NET Framework]
- ACLs [.NET Framework]
- access control entries [.NET Framework]
- I/O [.NET Framework], access control list entries
- access control lists [.NET Framework]
ms.assetid: 53758b39-bd9b-4640-bb04-cad5ed8d0abf
ms.openlocfilehash: 53daa88b761f46dab26b1c12c73741e880512d8d
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95682695"
---
# <a name="how-to-add-or-remove-access-control-list-entries-net-framework-only"></a><span data-ttu-id="347fc-102">Instrukcje: Dodawanie lub usuwanie pozycji listy Access Control (tylko .NET Framework)</span><span class="sxs-lookup"><span data-stu-id="347fc-102">How to: Add or remove Access Control List entries (.NET Framework only)</span></span>

<span data-ttu-id="347fc-103">Aby dodać lub usunąć wpisy listy Access Control (ACL) do lub z pliku lub katalogu, Pobierz <xref:System.Security.AccessControl.FileSecurity> <xref:System.Security.AccessControl.DirectorySecurity> obiekt lub z pliku lub katalogu.</span><span class="sxs-lookup"><span data-stu-id="347fc-103">To add or remove Access Control List (ACL) entries to or from a file or directory, get the <xref:System.Security.AccessControl.FileSecurity> or <xref:System.Security.AccessControl.DirectorySecurity> object from the file or directory.</span></span> <span data-ttu-id="347fc-104">Zmodyfikuj obiekt, a następnie Zastosuj go z powrotem do pliku lub katalogu.</span><span class="sxs-lookup"><span data-stu-id="347fc-104">Modify the object, and then apply it back to the file or directory.</span></span>  
  
## <a name="add-or-remove-an-acl-entry-from-a-file"></a><span data-ttu-id="347fc-105">Dodawanie lub usuwanie wpisu listy ACL z pliku</span><span class="sxs-lookup"><span data-stu-id="347fc-105">Add or remove an ACL entry from a file</span></span>  
  
1. <span data-ttu-id="347fc-106">Wywołaj <xref:System.IO.File.GetAccessControl%2A?displayProperty=nameWithType> metodę, aby uzyskać <xref:System.Security.AccessControl.FileSecurity> obiekt zawierający bieżące wpisy listy ACL pliku.</span><span class="sxs-lookup"><span data-stu-id="347fc-106">Call the <xref:System.IO.File.GetAccessControl%2A?displayProperty=nameWithType> method to get a <xref:System.Security.AccessControl.FileSecurity> object that contains the current ACL entries of a file.</span></span>  
  
2. <span data-ttu-id="347fc-107">Dodaj lub Usuń wpisy listy ACL z <xref:System.Security.AccessControl.FileSecurity> obiektu zwróconego z kroku 1.</span><span class="sxs-lookup"><span data-stu-id="347fc-107">Add or remove ACL entries from the <xref:System.Security.AccessControl.FileSecurity> object returned from step 1.</span></span>  
  
3. <span data-ttu-id="347fc-108">Aby zastosować zmiany, Przekaż <xref:System.Security.AccessControl.FileSecurity> obiekt do <xref:System.IO.File.SetAccessControl%2A?displayProperty=nameWithType> metody.</span><span class="sxs-lookup"><span data-stu-id="347fc-108">To apply the changes, pass the <xref:System.Security.AccessControl.FileSecurity> object to the <xref:System.IO.File.SetAccessControl%2A?displayProperty=nameWithType> method.</span></span>  
  
## <a name="add-or-remove-an-acl-entry-from-a-directory"></a><span data-ttu-id="347fc-109">Dodawanie lub usuwanie wpisu listy ACL z katalogu</span><span class="sxs-lookup"><span data-stu-id="347fc-109">Add or remove an ACL entry from a directory</span></span>  
  
1. <span data-ttu-id="347fc-110">Wywołaj <xref:System.IO.Directory.GetAccessControl%2A?displayProperty=nameWithType> metodę, aby uzyskać <xref:System.Security.AccessControl.DirectorySecurity> obiekt zawierający bieżące wpisy listy ACL katalogu.</span><span class="sxs-lookup"><span data-stu-id="347fc-110">Call the <xref:System.IO.Directory.GetAccessControl%2A?displayProperty=nameWithType> method to get a <xref:System.Security.AccessControl.DirectorySecurity> object that contains the current ACL entries of a directory.</span></span>  
  
2. <span data-ttu-id="347fc-111">Dodaj lub Usuń wpisy listy ACL z <xref:System.Security.AccessControl.DirectorySecurity> obiektu zwróconego z kroku 1.</span><span class="sxs-lookup"><span data-stu-id="347fc-111">Add or remove ACL entries from the <xref:System.Security.AccessControl.DirectorySecurity> object returned from step 1.</span></span>  
  
3. <span data-ttu-id="347fc-112">Aby zastosować zmiany, Przekaż <xref:System.Security.AccessControl.DirectorySecurity> obiekt do <xref:System.IO.Directory.SetAccessControl%2A?displayProperty=nameWithType> metody.</span><span class="sxs-lookup"><span data-stu-id="347fc-112">To apply the changes, pass the <xref:System.Security.AccessControl.DirectorySecurity> object to the <xref:System.IO.Directory.SetAccessControl%2A?displayProperty=nameWithType> method.</span></span>  
  
## <a name="example"></a><span data-ttu-id="347fc-113">Przykład</span><span class="sxs-lookup"><span data-stu-id="347fc-113">Example</span></span>  

 <span data-ttu-id="347fc-114">Do uruchomienia tego przykładu należy użyć prawidłowego konta użytkownika lub grupy.</span><span class="sxs-lookup"><span data-stu-id="347fc-114">You must use a valid user or group account to run this example.</span></span> <span data-ttu-id="347fc-115">W przykładzie zastosowano <xref:System.IO.File> obiekt.</span><span class="sxs-lookup"><span data-stu-id="347fc-115">The example uses a <xref:System.IO.File> object.</span></span> <span data-ttu-id="347fc-116">Użyj tej samej procedury dla <xref:System.IO.FileInfo> klas, <xref:System.IO.Directory> i <xref:System.IO.DirectoryInfo> .</span><span class="sxs-lookup"><span data-stu-id="347fc-116">Use the same procedure for the <xref:System.IO.FileInfo>, <xref:System.IO.Directory>, and <xref:System.IO.DirectoryInfo> classes.</span></span>

 [!code-csharp[IO.File.GetAccessControl-SetAccessControl#1](../../../samples/snippets/csharp/VS_Snippets_CLR/IO.File.GetAccessControl-SetAccessControl/CS/sample.cs#1)]
 [!code-vb[IO.File.GetAccessControl-SetAccessControl#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/IO.File.GetAccessControl-SetAccessControl/VB/sample.vb#1)]  
