---
description: -errorreport (opcje kompilatora C#)
title: -errorreport (opcje kompilatora C#)
ms.date: 07/20/2015
f1_keywords:
- /errorreport
helpviewer_keywords:
- -errorreport compiler option [C#]
- errorreport compiler option [C#]
- /errorreport compiler option [C#]
ms.assetid: bd0e7493-b79d-4369-9c3f-ba26ebdfbedf
ms.openlocfilehash: 6238ac392ff99d18d9cc7ea07e23b08ff235c14f
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "91173233"
---
# <a name="-errorreport-c-compiler-options"></a>-errorreport (opcje kompilatora C#)

Ta opcja zapewnia wygodny sposób raportowania wewnętrznego błędu kompilatora języka C# do firmy Microsoft.

> [!NOTE]
> W systemach Windows Vista i Windows Server 2008 ustawienia raportowania błędów wprowadzone dla programu Visual Studio nie przesłaniają ustawień wprowadzonych za pomocą Raportowanie błędów systemu Windows (raportowanie błędów). Ustawienia raportowanie błędów systemu Windows zawsze mają pierwszeństwo przed ustawieniami raportowania błędów programu Visual Studio.

## <a name="syntax"></a>Składnia

```console
-errorreport:{ none | prompt | queue | send }
```

## <a name="arguments"></a>Argumenty

 **brak**  
 Raporty o błędach wewnętrznych kompilatora nie będą zbierane ani wysyłane do firmy Microsoft.

 **Monituj** Wyświetlany jest komunikat z prośbą o wysłanie raportu po otrzymaniu wewnętrznego błędu kompilatora. **monit** jest wartością domyślną podczas kompilowania aplikacji w środowisku deweloperskim.

 **Kolejka** Kolejkuje raport o błędach. Po zalogowaniu się przy użyciu poświadczeń administracyjnych można zgłosić błędy od czasu ostatniego zalogowania. Nie zostanie wyświetlony monit o wysłanie raportów pod kątem błędów więcej niż raz na trzy dni. **Kolejka** jest wartością domyślną podczas kompilowania aplikacji w wierszu polecenia.

 **Wyślij** Automatycznie wysyła raporty wewnętrznych błędów kompilatora do firmy Microsoft. Aby włączyć tę opcję, musisz najpierw wyrazić zgodę na zasady zbierania danych firmy Microsoft. Podczas pierwszego określania **errorReport: Send** na komputerze komunikat kompilatora odwołuje się do witryny sieci Web zawierającej zasady zbierania danych firmy Microsoft.

## <a name="remarks"></a>Uwagi

 Wewnętrzny błąd kompilatora (lodem) powstaje, gdy kompilator nie może przetworzyć pliku kodu źródłowego. W przypadku wystąpienia lodu kompilator nie tworzy pliku wyjściowego ani żadnej przydatnej diagnostyki, której można użyć do naprawienia kodu.

 W poprzednich wersjach, gdy otrzymasz lód, zachęcamy do skontaktowania się z pomocą techniczną firmy Microsoft w celu zgłoszenia problemu. Za pomocą **-errorreport**, można podać informacje o lodem do zespołu Visual C#. Raporty o błędach mogą pomóc w ulepszaniu przyszłych wersji kompilatora.

 Możliwość wysyłania raportów zależy od uprawnień komputera i użytkownika.

### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Aby ustawić tę opcję kompilatora w środowisku programowania Visual Studio

1. Otwórz stronę **Właściwości** projektu. Aby uzyskać więcej informacji, zobacz [stronę Kompilacja, Projektant projektu (C#)](/visualstudio/ide/reference/build-page-project-designer-csharp).

2. Kliknij stronę właściwości **kompilacja** .

3. Kliknij przycisk **Zaawansowane** .

4. Zmodyfikuj właściwość **wewnętrznego raportowania błędów kompilatora** .

 Aby uzyskać informacje na temat sposobu, w jaki można programowo ustawić tę opcję kompilatora, zobacz <xref:VSLangProj80.CSharpProjectConfigurationProperties3.ErrorReport%2A> .

## <a name="see-also"></a>Zobacz też

- [Opcje kompilatora C#](./index.md)
