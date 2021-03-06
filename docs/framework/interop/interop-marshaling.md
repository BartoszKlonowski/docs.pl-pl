---
title: Organizowanie międzyoperacyjne
description: Rozpocznij pracę z kierowaniem międzyoperacyjnym, która określa, jak dane są przekazywane do argumentów metody i zwracają wartości między zarządzaną i niezarządzaną pamięcią podczas wywołań.
ms.date: 03/30/2017
helpviewer_keywords:
- marshaling, COM interop
- interop marshaling
- interop marshaling, about interop marshaling
ms.assetid: 115f7a2f-d422-4605-ab36-13a8dd28142a
ms.openlocfilehash: bd618714a9bd27bc309b7933b656de6bd139cfe7
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90554895"
---
# <a name="interop-marshaling"></a>Organizowanie międzyoperacyjne

Organizowanie międzyoperacyjności reguluje sposób przekazywania danych w argumentach metod i zwraca wartości między zarządzaną i niezarządzaną pamięcią podczas wywołań. Organizowanie międzyoperacyjności to działanie czasu wykonywania wykonywane przez usługę Marshaling środowiska uruchomieniowego języka wspólnego.

Większość typów danych ma wspólne reprezentacje w pamięci zarządzanej i niezarządzanej. Organizator międzyoperacyjny obsługuje te typy. Inne typy mogą być niejednoznaczne lub niereprezentowane w całości w pamięci zarządzanej.

Niejednoznaczny typ może mieć wiele niezarządzanych reprezentacji, które są mapowane na pojedynczy typ zarządzany lub brakujące informacje o typie, takie jak rozmiar tablicy. Dla niejednoznacznych typów, organizator udostępnia domyślną reprezentację i alternatywne reprezentacje, w których istnieje wiele reprezentacji. Możesz dostarczyć jawne instrukcje do organizatora, w jaki sposób ma on zorganizować niejednoznaczny typ.

## <a name="platform-invoke-and-com-interop-models"></a>Wywołania platformy i modele międzyoperacyjności modelu COM

Środowisko uruchomieniowe języka wspólnego udostępnia dwa mechanizmy współdziałania z niezarządzanym kodem:

- Wywołanie platformy, które umożliwia kodowi zarządzanemu wywoływanie funkcji wyeksportowanych z niezarządzanej biblioteki.
- Międzyoperacyjność modelu COM, która umożliwia współdziałanie kodu zarządzanego z obiektami Component Object Model (COM) za pomocą interfejsów.

Zarówno wywołanie platformy, jak i międzyoperacyjność modelu COM używają organizowania międzyoperacyjnego do dokładnego przenoszenia argumentów metody między obiektem wywołującym i wywoływanym z powrotem, w razie potrzeby. Jak widać na poniższej ilustracji, wywołanie metody wywołuje metodę przepływów z zarządzanego do kodu niezarządzanego i nigdy nie w inny sposób, z wyjątkiem sytuacji, gdy są używane [funkcje wywołania zwrotnego](callback-functions.md) . Mimo że wywołania wywołania platformy mogą przepływać tylko z kodu zarządzanego do niezarządzanego, dane mogą być przesyłane w obu kierunkach jako parametry wejściowe lub wyjściowe. Wywołania metod międzyoperacyjnych modelu COM mogą przepływać w dowolnym kierunku.

![Wywołanie platformy](./media/interop-marshaling/interop-marshaling-invoke-and-com.png "Wywołanie platformy i przepływ wywołań międzyoperacyjnych modelu COM")

Na najniższym poziomie oba mechanizmy korzystają z tej samej usługi organizowania międzyoperacyjnego. Niektóre typy danych są jednak obsługiwane wyłącznie przez międzyoperacyjność modelu COM lub wywołanie platformy. Aby uzyskać szczegółowe informacje, zobacz [domyślne zachowanie organizowania](default-marshaling-behavior.md).

## <a name="marshaling-and-com-apartments"></a>Organizowanie i apartamentach COM

Organizator międzyoperacyjny kierujący dane między stertą środowiska uruchomieniowego języka wspólnego i niezarządzaną stertą. Kierowanie odbywa się zawsze wtedy, gdy obiekt wywołujący i wywoływany nie mogą działać na tym samym wystąpieniu danych. Organizator międzyoperacyjny sprawia, że jest możliwe, że obiekt wywołujący i wywoływany przez nie działa na tych samych danych, nawet jeśli mają własną kopię danych.

Model COM ma również organizatora, który kierujący dane między modelami COM apartamentach lub różnymi procesami COM. Podczas wywoływania między kodem zarządzanym i niezarządzanym w ramach tej samej komórki COM Organizator międzyoperacyjny jest tym jedynym organizatorem. Podczas wywoływania kodu zarządzanego i niezarządzanego kodu w innej komórkowym modelu COM lub innym procesie, są to między innymi Organizator międzyoperacyjny i organizator COM.

### <a name="com-clients-and-managed-servers"></a>Klienci COM i serwery zarządzane

Wyeksportowany serwer zarządzany z biblioteką typów zarejestrowanym przez [Regasm.exe (Narzędzie rejestracji zestawów)](../tools/regasm-exe-assembly-registration-tool.md) ma `ThreadingModel` wpis rejestru ustawiony na `Both` . Ta wartość wskazuje, że serwer można aktywować w komórce jednowątkowej (STA) lub w wielowątkowej komórce (MTA). Obiekt serwera jest tworzony w tej samej lokalu, co jego obiekt wywołujący, jak pokazano w poniższej tabeli:

|Klient COM|Serwer .NET|Wymagania dotyczące organizowania|
|----------------|-----------------|-----------------------------|
|STA|`Both` zmieni się na STA.|Kierowanie między komórkami.|
|MTA|`Both` przechodzi do MTA.|Kierowanie między komórkami.|

Ponieważ klient i serwer znajdują się w tej samej apartamentie, usługa Marshaling Interop automatycznie obsługuje wszystkie kierowanie danych. Na poniższej ilustracji przedstawiono usługę Marshaling Interop działającą między stertami zarządzanymi i niezarządzanymi w ramach tego samego apartamentu COM.

![Organizowanie międzyoperacyjnego między stertami zarządzanymi i niezarządzanymi](./media/interop-marshaling/interop-heaps-managed-and-unmanaged.gif "Proces organizowania tego samego typu Apartment")

Jeśli planujesz wyeksportować serwer zarządzany, należy pamiętać, że klient COM określa Apartament serwera. Zarządzany serwer wywoływany przez klienta COM zainicjowany w MTA musi zapewnić bezpieczeństwo wątku.

### <a name="managed-clients-and-com-servers"></a>Zarządzani klienci i serwery COM

Ustawieniem domyślnym dla zarządzanego klienta apartamentach jest MTA; Jednak typ aplikacji klienta .NET może zmienić ustawienie domyślne. Na przykład ustawienie Apartment Visual Basic Client to STA. <xref:System.STAThreadAttribute?displayProperty=nameWithType> <xref:System.MTAThreadAttribute?displayProperty=nameWithType> <xref:System.Threading.Thread.ApartmentState%2A?displayProperty=nameWithType> <xref:System.Web.UI.Page.AspCompatMode%2A?displayProperty=nameWithType> Aby przejrzeć i zmienić ustawienie apartamentu zarządzanego klienta, można użyć właściwości,, lub właściwości.

Autor składnika ustawia koligację wątku serwera COM. W poniższej tabeli przedstawiono kombinacje ustawień Apartment dla klientów .NET i serwerów COM. Przedstawiono w nim również wyniki związane z kierowaniem dla kombinacji.

|Klient .NET|Serwer COM|Wymagania dotyczące organizowania|
|-----------------|----------------|-----------------------------|
|MTA (domyślnie)|MTA<br /><br /> STA|Organizowanie międzyoperacyjnych.<br /><br /> Współdziałanie i kierowanie modelu COM.|
|STA|MTA<br /><br /> STA|Współdziałanie i kierowanie modelu COM.<br /><br /> Organizowanie międzyoperacyjnych.|

Gdy zarządzany klient i serwer niezarządzany znajdują się w tym samym elemencie Apartment, usługa Marshaling Interop obsługuje wszystkie dane dotyczące organizowania. Jednak po zainicjowaniu klienta i serwera w różnych apartamentach jest również wymagane kierowanie modelu COM. Na poniższej ilustracji przedstawiono elementy wywołania między komórkami:

![Kierowanie modelu COM](./media/interop-marshaling/single-process-across-multi-apartment.gif "Wywołanie między komórkami między klientem .NET a obiektem COM")

W przypadku organizowania między komórkami można wykonać następujące czynności:

- Zaakceptuj obciążenie związane z kierowaniem między komórkami, co jest zauważalne tylko wtedy, gdy na granicy występuje wiele wywołań. Należy zarejestrować bibliotekę typów składnika COM dla wywołań, aby pomyślnie przekroczyć granicę apartamentu.
- Zmień główny wątek przez ustawienie wątku klienta na STA lub MTA. Na przykład jeśli klient języka C# wywołuje wiele składników COM STA, można uniknąć organizowania między komórkami, ustawiając wątek główny na STA.

    > [!NOTE]
    > Gdy wątek klienta C# jest ustawiony na STA, wywołania do składników COM MTA będą wymagały organizowania między komórkami.

Aby uzyskać instrukcje dotyczące jawnego wybierania modelu Apartment, zobacz [wątki zarządzane i niezarządzane](/previous-versions/dotnet/netframework-4.0/5s8ee185(v=vs.100)).

## <a name="marshaling-remote-calls"></a>Kierowanie zdalnych wywołań

Podobnie jak w przypadku organizowania między komórkami, kierowanie odbywa się w każdym wywołaniu między kodem zarządzanym i niezarządzanym za każdym razem, gdy obiekty znajdują się w osobnych procesach. Na przykład:

- Klient COM, który wywołuje serwer zarządzany na hoście zdalnym, używa rozproszonego modelu COM (DCOM).
- Zarządzany klient, który wywołuje serwer COM na hoście zdalnym, korzysta z modelu DCOM.

Na poniższej ilustracji przedstawiono, jak kierowanie międzyoperacyjności i kierowanie modelu COM zapewniają kanały komunikacji między procesami i granicami hosta:

![Kierowanie modelu COM](./media/interop-marshaling/interop-and-com-marshaling.gif "Kierowanie między procesami")

### <a name="preserving-identity"></a>Zachowanie tożsamości

Środowisko uruchomieniowe języka wspólnego zachowuje tożsamość odwołań zarządzanych i niezarządzanych. Na poniższej ilustracji przedstawiono przepływ bezpośrednich odwołań niezarządzanych (górny wiersz) i bezpośrednie zarządzane odwołania (ostatni wiersz) między procesem i granicami hosta.

![Otoka, która umożliwia wywoływanie COM](./media/interop-marshaling/interop-direct-ref-across-process.gif "Przekazywanie odwołań między procesami i granicami hosta")

Na tej ilustracji:

- Niezarządzany Klient pobiera odwołanie do obiektu COM z zarządzanego obiektu, który pobiera to odwołanie z hosta zdalnego. Mechanizm komunikacji zdalnej jest modelem DCOM.
- Zarządzany Klient pobiera odwołanie do obiektu zarządzanego z obiektu COM, który pobiera to odwołanie z hosta zdalnego. Mechanizm komunikacji zdalnej jest modelem DCOM.

    > [!NOTE]
    > Eksportowana biblioteka typów serwera zarządzanego musi być zarejestrowana.

Liczba granic procesów między obiektem wywołującym i wywoływanym jest istotna; ten sam bezpośredni odwołujący występuje dla wywołań przetwarzanych i pozaprocesowych.

### <a name="managed-remoting"></a>Zarządzane komunikacja zdalna

Środowisko uruchomieniowe zapewnia również zarządzane połączenia zdalne, których można użyć do ustanowienia kanału komunikacyjnego między obiektami zarządzanymi w granicach procesu i hosta. Zarządzane komunikacja zdalna może obsługiwać zaporę między składnikami komunikacji, jak pokazano na poniższej ilustracji:

![Protokół SOAP lub TcpChannel](./media/interop-marshaling/interop-remote-soap-or-tcp.gif "Zdalne wywołania między zaporami przy użyciu protokołu SOAP lub klasy TcpChannel") Zdalne wywołania między zaporami przy użyciu protokołu SOAP lub klasy TcpChannel

Niektóre niezarządzane wywołania można obsłużyć za pośrednictwem protokołu SOAP, takiego jak wywołania między składnikami usług i COM.

## <a name="related-topics"></a>Tematy pokrewne

|Tytuł|Opis|
|-----------|-----------------|
|[Domyślne zachowanie marshalingu](default-marshaling-behavior.md)|Opisuje reguły, których usługa Marshaling Interop używa do organizowania danych.|
|[Organizowanie danych w wywołaniu platformy](marshaling-data-with-platform-invoke.md)|Opisuje sposób deklarowania parametrów metody i przekazywania argumentów do funkcji wyeksportowanych przez niezarządzane biblioteki.|
|[Organizowanie danych za pomocą modelu COM](marshaling-data-with-com-interop.md)|Opisuje sposób dostosowywania otok COM w celu zmiany sposobu organizowania zachowań.|
|[Instrukcje: Migrowanie zarządzanego kodu DCOM do WCF](how-to-migrate-managed-code-dcom-to-wcf.md)|Opisuje sposób migrowania z modelu DCOM do programu WCF.|
|[Instrukcje: Mapowanie wyników HRESULT i wyjątków](how-to-map-hresults-and-exceptions.md)|Opisuje sposób mapowania niestandardowych wyjątków na HRESULTs i zapewnia pełne mapowanie z każdego HRESULT do jego porównywalnej klasy wyjątku w .NET Framework.|
|[Współdziałanie przy użyciu typów ogólnych](/previous-versions/dotnet/netframework-4.0/ms229590(v=vs.100))|Opisuje, które akcje są obsługiwane w przypadku używania typów ogólnych do współdziałania z modelem COM.|
|[Współdziałanie z kodem niezarządzanym](index.md)|Opisuje usługi współdziałania udostępniane przez środowisko uruchomieniowe języka wspólnego.|
|[Zaawansowana współdziałanie COM](/previous-versions/dotnet/netframework-4.0/bd9cdfyx(v=vs.100))|Zawiera łącza do dodatkowych informacji na temat dołączania składników COM do aplikacji .NET Framework.|
|[Zagadnienia dotyczące projektowania operacji międzyoperacyjnych](/previous-versions/dotnet/netframework-4.0/61aax4kh(v=vs.100))|Zawiera wskazówki dotyczące pisania zintegrowanych składników COM.|

## <a name="reference"></a>Tematy pomocy

<xref:System.Runtime.InteropServices?displayProperty=nameWithType>
