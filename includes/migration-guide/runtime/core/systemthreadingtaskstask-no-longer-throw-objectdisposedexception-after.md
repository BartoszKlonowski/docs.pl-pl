---
ms.openlocfilehash: 58dbb54d42d89b450134758072e3133ae4e6b13d
ms.sourcegitcommit: cbacb5d2cebbf044547f6af6e74a9de866800985
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/05/2020
ms.locfileid: "89497515"
---
### <a name="systemthreadingtaskstask-no-longer-throw-objectdisposedexception-after-object-is-disposed"></a>System. Threading. Tasks. Task nie zgłasza już ObjectDisposedException po usunięciu obiektu

#### <a name="details"></a>Szczegóły

Z wyjątkiem <xref:System.Threading.Tasks.Task.System%23IAsyncResult%23AsyncWaitHandle> , <xref:System.Threading.Tasks.Task?displayProperty=fullName> metody nie zgłaszają <xref:System.ObjectDisposedException?displayProperty=fullName> wyjątku po usunięciu obiektu. Ta zmiana obsługuje używanie buforowanych zadań. Na przykład metoda może zwracać buforowane zadanie w celu reprezentowania już zakończonej operacji, zamiast przydzielać nowe zadanie. Było to niemożliwe w poprzednich wersjach programu .NET Framework, ponieważ każdy konsument zadania mógł je usunąć, co czyniło je bezużytecznym.

#### <a name="suggestion"></a>Sugestia

Należy pamiętać, że metody zadań nie mogą już zgłaszać <xref:System.ObjectDisposedException?displayProperty=fullName> w przypadkach, gdy obiekt zostanie usunięty. Jeśli aplikacja była zależna od tego wyjątku, aby wiedzieć, że zadanie zostało zlikwidowane, należy je zaktualizować, aby jawnie sprawdzić stan zadania przy użyciu <xref:System.Threading.Tasks.Task.Status> .

| Nazwa    | Wartość       |
|:--------|:------------|
| Zakres   |Mały|
|Wersja|4.5|
|Typ|Środowisko uruchomieniowe|

#### <a name="affected-apis"></a>Dotyczy interfejsów API

Nie wykrywalne za pośrednictwem analizy interfejsu API.

<!--

#### Affected APIs

Not detectable via API analysis.

-->
