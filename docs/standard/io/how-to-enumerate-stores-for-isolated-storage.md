---
title: 'Instrukcje: Wykazywanie magazynów dla izolowanego magazynu'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- enumerating stores
- data storage using isolated storage, enumerating stores
- storing data using isolated storage, enumerating stores
- stores, enumerating
- isolated storage, enumerating stores
- data stores, enumerating
ms.assetid: 0fcf279a-f241-48f0-8034-2e3d331f1fcb
ms.openlocfilehash: f01ca70b3fd5b778274ef5bd7fcb63e26d9916a8
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95734650"
---
# <a name="how-to-enumerate-stores-for-isolated-storage"></a>Instrukcje: Wykazywanie magazynów dla izolowanego magazynu

Wszystkie magazyny izolowane dla bieżącego użytkownika można wyliczyć przy użyciu  <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetEnumerator%2A?displayProperty=nameWithType> metody statycznej. Ta metoda przyjmuje <xref:System.IO.IsolatedStorage.IsolatedStorageScope> wartość i zwraca <xref:System.IO.IsolatedStorage.IsolatedStorageFile> moduł wyliczający. Aby wyliczyć magazyny, musisz mieć <xref:System.Security.Permissions.IsolatedStorageFilePermission> uprawnienie określające <xref:System.Security.Permissions.IsolatedStorageContainment.AdministerIsolatedStorageByUser> wartość. W przypadku wywołania <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetEnumerator%2A> metody z <xref:System.IO.IsolatedStorage.IsolatedStorageScope.User> wartością zwraca tablicę <xref:System.IO.IsolatedStorage.IsolatedStorageFile> obiektów, które są zdefiniowane dla bieżącego użytkownika.  
  
## <a name="example"></a>Przykład  

 Poniższy przykład kodu pobiera magazyn izolowany przez użytkownika i zestaw, tworzy kilka plików i pobiera te pliki przy użyciu <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetEnumerator%2A> metody.  
  
 [!code-csharp[Conceptual.IsolatedStorage#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source2.cs#2)]
 [!code-vb[Conceptual.IsolatedStorage#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source2.vb#2)]  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.IO.IsolatedStorage.IsolatedStorageFile>
- [Magazyn izolowany](isolated-storage.md)
