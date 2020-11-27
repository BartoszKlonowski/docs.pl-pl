---
title: Mgmtclassgen.exe (Zarządzanie generatorem silnie typizowanej klasy)
description: Informacje dotyczące Mgmtclassgen.exe, generatora klas o jednoznacznie określonym typie. To narzędzie umożliwia szybkie wygenerowanie wczesnej powiązanej klasy zarządzanej dla klasy WMI.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- CIM types
- Management Strongly Typed Class Generator
- WMI class
- Mgmtclassgen.exe
- early-bound managed classes
ms.assetid: 02ce6699-49b5-4a0b-b0d5-1003c491232e
ms.openlocfilehash: 1dea4b0b94053919169abb639ff48ecd3abbd66c
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96279158"
---
# <a name="mgmtclassgenexe-management-strongly-typed-class-generator"></a>Mgmtclassgen.exe (Zarządzanie generatorem silnie typizowanej klasy)

Narzędzie Management Strongly Typed Class Generator umożliwia szybkie generowanie wcześnie powiązanych klas zarządzanych dla określonej klasy Instrumentacji zarządzania Windows (WMI). Wygenerowana klasa upraszcza kod, który trzeba napisać, aby uzyskać dostęp do wystąpienia klasy WMI.  
  
## <a name="syntax"></a>Składnia  
  
```console  
mgmtclassgen
WMIClass [options]
```  
  
|Argument|Opis|  
|--------------|-----------------|  
|*WMIClass*|Klasa Instrumentacji zarządzania Windows, dla której jest generowana wcześnie powiązana klasa zarządzana.|  
  
|Opcja|Opis|  
|------------|-----------------|  
|**/l**—*Język*  |Określa język, w którym ma zostać wygenerowana wcześnie powiązana klasa zarządzana. Jako argumentu języka można określić **CS** (C#; default), **VB** (Visual Basic),  **MC** (C++) lub **js** (JScript).|  
|**/m**  *komputer*|Określa komputer, z którym należy nawiązać połączenie (na tym komputerze znajduje się klasa WMI). Wartością domyślną jest komputer lokalny.|  
|**/n***ścieżka* /n  |Określa ścieżkę do przestrzeni nazw usługi WMI zawierającej odpowiednią klasę WMI. Jeśli ta opcja nie zostanie określona, narzędzie generuje kod dla *WMIClass* w domyślnej przestrzeni nazw **root\cimv2** .|  
|**/o**  *classnamespace*|Określa przestrzeń nazw platformy .NET, w której ma zostać wygenerowana klasa kodu zarządzanego. Jeśli ta opcja nie zostanie określona, narzędzie wygeneruje przestrzeń nazw, używając przestrzeni nazw usługi WMI i prefiksu schematu. Prefiks schematu jest częścią nazwy klasy poprzedzającą znak podkreślenia. Na przykład dla klasy **Win32_OperatingSystem** w przestrzeni nazw **root\cimv2** narzędzie wygeneruje klasę w **katalogu głównym. CIMV2. Win32**.|  
|**/p**  *FilePath*|Określa ścieżkę do pliku, w którym ma zostać zapisany wygenerowany kod. Jeśli ta opcja nie zostanie określona, narzędzie utworzy plik w bieżącym katalogu. Nazwa klasy i pliku, w którym generuje klasę przy użyciu argumentu *WMIClass* . Nazwa klasy i pliku jest taka sama jak nazwa *WMIClass.* Jeśli *WMIClass* zawiera znak podkreślenia, narzędzie używa części nazwy klasy po znaku podkreślenia. Na przykład jeśli nazwa *WMIClass* ma format **Win32_LogicalDisk**, wygenerowana Klasa i plik o nazwie "dysk logiczny". Jeżeli plik już istnieje, narzędzie zastąpi istniejący plik.|  
|**/PW**  *hasło*|Określa hasło, które ma być używane podczas logowania do komputera określonego przez **/m** Option.|  
|**/u**  *Nazwa użytkownika*|Określa nazwę użytkownika, która ma być używana podczas logowania do komputera określonego przez **/m** Option.|  
|**/?**|Wyświetla składnię polecenia i opcje narzędzia.|  
  
## <a name="remarks"></a>Uwagi  

 Mgmtclassgen.exe używa <xref:System.Management.ManagementClass.GetStronglyTypedClassCode%2A?displayProperty=nameWithType> metody. Dzięki temu można użyć dowolnego niestandardowego dostawcy kodu, aby wygenerować kod w zarządzanych językach innych niż C#, Visual Basic i JScript.  
  
 Należy zauważyć, że wygenerowane klasy są powiązane ze schematem, dla którego są generowane. Jeśli schemat źródłowy ulegnie zmianie, trzeba ponownie wygenerować klasę, jeśli chce się odzwierciedlić zmiany w schemacie.  
  
 W poniższej tabeli pokazano mapowanie typów modelu wspólnych informacji (CIM) usługi WMI na typy danych w generowanej klasie:  
  
|Typ modelu CIM|Typ danych w generowanej klasie|  
|--------------|--------------------------------------|  
|CIM_SINT8|**SByte**|  
|CIM_UINT8|**Bajc**|  
|CIM_SINT16|**Int16**|  
|CIM_UINT16|**UInt16**|  
|CIM_SINT32|**Int32**|  
|SIM_UINT32|**UInt32**|  
|CIM_SINT64|**Int64**|  
|CIM_UINT64|**UInt64**|  
|CIM_REAL32|**Pojedyncze**|  
|CIM_REAL64|**Double**|  
|CIM_BOOLEAN|**Boolean**|  
|CIM_String|**Ciąg**|  
|CIM_DATETIME|**DateTime** lub **TimeSpan**|  
|CIM_REFERENCE|**ManagementPath**|  
|CIM_CHAR16|**Delikatn**|  
|CIM_OBJECT|**ManagementBaseObject**|  
|CIM_IUNKNOWN|**Stream**|  
|CIM_ARRAY|Tablica wymienionych powyżej obiektów|  
  
 Podczas generowania klasy WMI należy zwrócić uwagę na następujące zachowania:  
  
- Możliwe jest, że standardowa publiczna właściwość lub metoda będzie miała taką samą nazwę jak istniejąca właściwość lub metoda. Jeśli tak się zdarzy, narzędzie zmieni nazwę właściwości lub metody w generowanej klasie w celu uniknięcia konfliktu nazw.  
  
- Możliwe jest, że nazwa właściwości lub metody w generowanej klasie będzie słowem kluczowym w docelowym języku programowania. Jeśli tak się zdarzy, narzędzie zmieni nazwę właściwości lub metody w generowanej klasie w celu uniknięcia konfliktu nazw.  
  
- W usłudze WMI kwalifikatory to modyfikatory zawierające informacje opisujące klasę, wystąpienie, właściwość lub metodę. Usługa WMI używa kwalifikatorów standardowych, takich jak **Odczyt**, **zapis** i **klucz** , aby opisać właściwość w wygenerowanej klasie. Na przykład właściwość, która jest modyfikowana przy użyciu kwalifikatora **odczytu** , jest definiowana tylko przy użyciu metody dostępu **Get** właściwości w wygenerowanej klasie. Ponieważ właściwość oznaczona kwalifikatorem **odczytu** jest przeznaczona tylko do odczytu, metoda dostępu **Set** nie jest zdefiniowana.  
  
- Właściwość numeryczna może być modyfikowana przez kwalifikatory **wartości** i **ValueMaps** , aby wskazać, że właściwość można ustawić tylko dla określonych dozwolonych wartości. Wyliczenie jest generowane z tymi **wartościami** i **ValueMaps** , a właściwość jest zamapowana na Wyliczenie.  
  
- Usługa WMI używa pojedynczego terminu w celu opisania klasy, która ma tylko jedno wystąpienie. W związku z tym, Konstruktor bez parametrów dla klasy pojedynczej będzie inicjować klasę tylko do wystąpienia klasy.  
  
- Klasa WMI może mieć właściwości, które są obiektami. W przypadku generowania klasy silnie określonej dla tego typu klasy WMI należy rozważyć wygenerowanie klas o jednoznacznie określonym typie dla typów właściwości osadzonego obiektu. Pozwoli to na dostęp do osadzonych obiektów w sposób silnie określony. Należy zauważyć, że wygenerowany kod może nie być w stanie wykryć typu osadzonego obiektu. W takim przypadku w wygenerowanym kodzie zostanie utworzony komentarz powiadamiający o problemie. Następnie można zmodyfikować wygenerowany kod, tak aby właściwość miała typ innej generowanej klasy.  
  
- W usłudze WMI wartość danych typu CIM_DATETIME może przedstawiać określoną datę i godzinę albo interwał czasu. Jeśli wartość danych reprezentuje datę i godzinę, typem danych w generowanej klasie jest **DateTime**. Jeśli wartość danych reprezentuje przedział czasu, typem danych w generowanej klasie jest **TimeSpan**.  
  
 Alternatywnie można wygenerować klasę o jednoznacznie określonym typie przy użyciu rozszerzenia zarządzania Eksplorator serwera w programie Visual Studio .NET.  
  
 Aby uzyskać więcej informacji na temat usługi WMI, zobacz temat **Instrumentacja zarządzania Windows** w dokumentacji zestawu SDK platformy.  
  
## <a name="examples"></a>Przykłady  

 Następujące polecenie generuje klasę zarządzaną w kodzie C# dla klasy WMI **Win32_LogicalDisk** w przestrzeni nazw **root\cimv2** . Narzędzie zapisuje klasę zarządzaną w pliku źródłowym w c:\disk.cs w **katalogu głównym. CIMV2.** Przestrzeń nazw Win32.  
  
```console  
mgmtclassgen Win32_LogicalDisk /n root\cimv2 /l CS /p c:\disk.cs  
```  
  
 W poniższym przykładzie kodu pokazano, w jaki sposób można programowo używać wygenerowanej klasy. Najpierw jest wyliczane wystąpienie klasy i jest drukowana ścieżka. Następnie za pomocą wystąpienia usługi WMI jest tworzone wystąpienie wygenerowanej klasy, które ma zostać zainicjowane. `Process` jest klasą wygenerowaną dla **Win32_Process** i `LogicalDisk` jest klasą wygenerowaną dla **Win32_LogicalDisk** w przestrzeni nazw **root\cimv2** .  
  
```vb  
Imports System  
Imports System.Management  
Imports ROOT.CIMV2.Win32  
  
Public Class App
   Public Shared Sub Main()
      ' Enumerate instances of the Win32_process.  
      ' Print the Name property of the instance.  
      Dim ps As Process
      For Each ps In  Process.GetInstances()  
         Console.WriteLine(ps.Name)  
      Next ps  
  
      ' Initialize the instance of LogicalDisk with  
      ' the WMI instance pointing to logical drive d:.  
      Dim dskD As New LogicalDisk(New _  
         ManagementPath("win32_LogicalDisk.DeviceId=""d:"""))  
      Console.WriteLine(dskD.Caption)  
   End Sub  
End Class  
```  
  
```csharp  
using System;  
using System.Management;  
using ROOT.CIMV2.Win32;  
  
public class App  
{  
   public static void Main()  
   {  
      // Enumerate instances of the Win32_process.  
      // Print the Name property of the instance.  
      foreach(Process ps in Process.GetInstances())  
      {  
         Console.WriteLine(ps.Name);  
      }  
  
      // Initialize the instance of LogicalDisk with  
      // the WMI instance pointing to logical drive d:.  
      LogicalDisk dskD = new LogicalDisk(new ManagementPath(  
        "win32_LogicalDisk.DeviceId=\"d:\""));  
      Console.WriteLine(dskD.Caption);  
   }  
}  
```  
  
## <a name="see-also"></a>Zobacz też

- <xref:System.Management>
- <xref:System.Management.ManagementClass.GetStronglyTypedClassCode%2A?displayProperty=nameWithType>
- <xref:System.CodeDom.Compiler.CodeDomProvider?displayProperty=nameWithType>
- [Narzędzia](index.md)
- [Wiersze poleceń](developer-command-prompt-for-vs.md)
