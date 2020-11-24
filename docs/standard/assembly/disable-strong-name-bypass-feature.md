---
title: 'Instrukcje: wyłączanie funkcji pomijania silnej nazwy'
description: Obejście silnej nazwy pomija sprawdzanie poprawności podpisu w w pełni zaufanych domenach w programie .NET. Tę funkcję można zastąpić dla jednej aplikacji lub wszystkich aplikacji.
ms.date: 08/20/2019
helpviewer_keywords:
- strong-name bypass feature
- strong-named assemblies, loading into trusted application domains
ms.assetid: 234e088c-3b11-495a-8817-e0962be79d82
ms.openlocfilehash: 2846efbbd76cf677a42a7031e53661d302c6c964
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95687466"
---
# <a name="how-to-disable-the-strong-name-bypass-feature"></a>Instrukcje: wyłączanie funkcji pomijania silnej nazwy

Począwszy od wersji 3,5 .NET Framework programu Service Pack 1 (SP1), sygnatury silnej nazwy nie są sprawdzane, gdy zestaw jest ładowany do obiektu pełnego zaufania <xref:System.AppDomain> , takiego jak domyślny <xref:System.AppDomain> dla `MyComputer` strefy. Jest to nazywane funkcją pomijania silnej nazwy. W środowisku z pełnym zaufaniem wymagania dotyczące <xref:System.Security.Permissions.StrongNameIdentityPermission> zawsze powiodło się w przypadku podpisanych, pełnego zaufania zestawów niezależnie od ich sygnatury. Jedynym ograniczeniem jest to, że zestaw musi być w pełni zaufany, ponieważ jego strefa jest w pełni zaufana. Ponieważ silna nazwa nie jest czynnikiem decydującym w tych warunkach, nie ma powodów, dla których nie można jej zweryfikować. Pomijanie sprawdzania poprawności sygnatur silnych nazw zapewnia znaczną poprawę wydajności.  
  
 Funkcja Bypass ma zastosowanie do dowolnego zestawu pełnego zaufania, który nie jest podpisany z opóźnieniem i który jest ładowany do dowolnego pełnego zaufania <xref:System.AppDomain> z katalogu określonego przez jego <xref:System.AppDomainSetup.ApplicationBase%2A> Właściwość.  
  
 Można zastąpić funkcję pomijania dla wszystkich aplikacji na komputerze przez ustawienie wartości klucza rejestru. Można zastąpić ustawienie pojedynczej aplikacji przy użyciu pliku konfiguracyjnego aplikacji. Nie można przywrócić funkcji pomijania dla pojedynczej aplikacji, jeśli została ona wyłączona przez klucz rejestru.  
  
 Gdy zastąpisz funkcję pomijania, silna nazwa jest weryfikowana tylko pod kątem poprawności; nie jest ona sprawdzana dla <xref:System.Security.Permissions.StrongNameIdentityPermission> . Jeśli chcesz potwierdzić konkretną silną nazwę, musisz wykonać to sprawdzenie oddzielnie.  
  
> [!IMPORTANT]
> Możliwość wymuszenia weryfikacji silnej nazwy zależy od klucza rejestru, zgodnie z opisem w poniższej procedurze. Jeśli aplikacja jest uruchomiona w ramach konta, które nie ma uprawnień do uzyskiwania dostępu do tego klucza rejestru na liście kontroli dostępu (ACL), to ustawienie jest nieskuteczne. Musisz się upewnić, że dla tego klucza są skonfigurowane uprawnienia ACL, aby można było je odczytać dla wszystkich zestawów.  
  
## <a name="disable-the-strong-name-bypass-feature-for-all-applications"></a>Wyłącz funkcję pomijania silnej nazwy dla wszystkich aplikacji  
  
- Na komputerach 32-bitowych w rejestrze systemowym Utwórz wpis DWORD z wartością 0 o nazwie `AllowStrongNameBypass` w obszarze HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\\ . Klucz NETFramework.  
  
- Na komputerach 64-bitowych w rejestrze systemowym Utwórz wpis DWORD z wartością 0 o nazwie `AllowStrongNameBypass` w obszarze HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\\ . NETFramework i HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\\ . Klucze NETFramework.  
  
## <a name="disable-the-strong-name-bypass-feature-for-a-single-application"></a>Wyłączenie funkcji pomijania silnej nazwy dla pojedynczej aplikacji  
  
1. Otwórz lub Utwórz plik konfiguracji aplikacji.  
  
    Aby uzyskać więcej informacji na temat tego pliku, zapoznaj się z sekcją pliki konfiguracyjne aplikacji w artykule [Konfigurowanie aplikacji](../../framework/configure-apps/index.md).  
  
2. Dodaj następujący wpis:  
  
    ```xml  
    <configuration>  
      <runtime>  
        <bypassTrustedAppStrongNames enabled="false" />  
      </runtime>  
    </configuration>  
    ```  
  
 Można przywrócić funkcję pomijania dla aplikacji, usuwając ustawienia pliku konfiguracji lub ustawiając atrybut na `true` .  
  
> [!NOTE]
> Można włączać i wyłączać sprawdzanie silnej nazwy dla aplikacji tylko wtedy, gdy Funkcja pomijania jest włączona dla komputera. Jeśli funkcja pomijania została wyłączona dla komputera, silne nazwy są weryfikowane dla wszystkich aplikacji i nie można pominąć walidacji dla pojedynczej aplikacji.  
  
## <a name="see-also"></a>Zobacz także

- [Sn.exe (Narzędzie silnej nazwy)](../../framework/tools/sn-exe-strong-name-tool.md)
- [\<bypassTrustedAppStrongNames> postaci](../../framework/configure-apps/file-schema/runtime/bypasstrustedappstrongnames-element.md)
- [Tworzenie i używanie zestawów o silnej nazwie](create-use-strong-named.md)
