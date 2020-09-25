---
title: Przetwarzanie transakcji
description: Przejrzyj przetwarzanie transakcji w programie .NET. Transakcje zapewniają, że zasoby zorientowane na dane nie są trwale aktualizowane, chyba że wszystkie operacje zakończą się pomyślnie.
ms.date: 03/30/2017
ms.assetid: effdc8e6-accf-41eb-98a5-431603ba218b
ms.openlocfilehash: bbf2448128da7df8af415ff5dea7e3cd8af24d1e
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91186812"
---
# <a name="transaction-processing"></a><span data-ttu-id="9fe88-104">Przetwarzanie transakcji</span><span class="sxs-lookup"><span data-stu-id="9fe88-104">Transaction Processing</span></span>

<span data-ttu-id="9fe88-105">Kupując książki z księgarni online, wymieniać się pieniądze (w formie kredytu) książki.</span><span class="sxs-lookup"><span data-stu-id="9fe88-105">When you purchase a book from an online bookstore, you exchange money (in the form of credit) for a book.</span></span> <span data-ttu-id="9fe88-106">Jeśli Twój kredytowej jest dobra, serii powiązanych operacji zapewnia, że Pobierz książkę o i księgarni pobiera pieniądze.</span><span class="sxs-lookup"><span data-stu-id="9fe88-106">If your credit is good, a series of related operations ensures that you get the book and the bookstore gets your money.</span></span> <span data-ttu-id="9fe88-107">Jednak w przypadku niepowodzenia podczas wymiany jednej operacji w serii całego exchange nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="9fe88-107">However, if a single operation in the series fails during the exchange, the entire exchange fails.</span></span> <span data-ttu-id="9fe88-108">Użytkownik nie może korzystać książki i księgarni nie otrzymać pieniądze.</span><span class="sxs-lookup"><span data-stu-id="9fe88-108">You do not get the book and the bookstore does not get your money.</span></span>  
  
 <span data-ttu-id="9fe88-109">Technologia odpowiedzialnych za udostępnianie wymiany zrównoważona i przewidywalne jest wywoływana przetwarzania transakcji.</span><span class="sxs-lookup"><span data-stu-id="9fe88-109">The technology responsible for making the exchange balanced and predictable is called transaction processing.</span></span> <span data-ttu-id="9fe88-110">Transakcje zapewniają, że zasoby zorientowane na dane nie są trwale aktualizowane, chyba że wszystkie operacje w ramach jednostki transakcyjnej zakończą się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="9fe88-110">Transactions ensure that data-oriented resources are not permanently updated unless all operations within the transactional unit complete successfully.</span></span> <span data-ttu-id="9fe88-111">Łącząc zestaw powiązanych operacji w jednostkę, która całkowicie kończy się powodzeniem lub całkowicie niepowodzeniem, można uprościć odzyskiwanie błędów i zwiększyć niezawodność aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9fe88-111">By combining a set of related operations into a unit that either completely succeeds or completely fails, you can simplify error recovery and make your application more reliable.</span></span>  
  
 <span data-ttu-id="9fe88-112">Systemy przetwarzania transakcji składają się ze sprzętu komputerowego i oprogramowania hostującym aplikację zorientowaną na transakcje, która wykonuje rutynowe transakcje niezbędne do prowadzenia działalności.</span><span class="sxs-lookup"><span data-stu-id="9fe88-112">Transaction processing systems consist of computer hardware and software hosting a transaction-oriented application that performs the routine transactions necessary to conduct business.</span></span> <span data-ttu-id="9fe88-113">Przykłady obejmują systemy zarządzające wpisami zamówienia sprzedaży, rezerwacjami lotniczymi, płacami, rekordami pracowników, produkcją i wysyłką.</span><span class="sxs-lookup"><span data-stu-id="9fe88-113">Examples include systems that manage sales order entry, airline reservations, payroll, employee records, manufacturing, and shipping.</span></span>  
  
 <span data-ttu-id="9fe88-114">Ta sekcja zawiera ogólne informacje o przetwarzaniu transakcji oraz informacje dotyczące sposobu pisania transakcyjnych aplikacji i menedżerów zasobów przy użyciu platformy Microsoft .NET.</span><span class="sxs-lookup"><span data-stu-id="9fe88-114">This section provides both general information on transaction processing, and specific information on how to write transactional applications and resource managers using the Microsoft .NET Framework.</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="9fe88-115">W tej sekcji</span><span class="sxs-lookup"><span data-stu-id="9fe88-115">In This Section</span></span>  

 [<span data-ttu-id="9fe88-116">Podstawowe informacje dotyczące transakcji</span><span class="sxs-lookup"><span data-stu-id="9fe88-116">Transaction Fundamentals</span></span>](transaction-fundamentals.md)  
 <span data-ttu-id="9fe88-117">Wprowadzono podstawowe transakcji przetwarzania terminy i pojęcia.</span><span class="sxs-lookup"><span data-stu-id="9fe88-117">Introduces basic transaction processing terms and concepts.</span></span>  
  
 [<span data-ttu-id="9fe88-118">Funkcje oferowane przez bibliotekę System.Transactions</span><span class="sxs-lookup"><span data-stu-id="9fe88-118">Features Provided by System.Transactions</span></span>](features-provided-by-system-transactions.md)  
 <span data-ttu-id="9fe88-119">W tym artykule omówiono sposób używania funkcji w ramach programu System. Transactions do pisania własnej aplikacji transakcyjnej.</span><span class="sxs-lookup"><span data-stu-id="9fe88-119">Discusses how you can use features in System.Transactions to write your own transactional application.</span></span>  
  
## <a name="reference"></a><span data-ttu-id="9fe88-120">Tematy pomocy</span><span class="sxs-lookup"><span data-stu-id="9fe88-120">Reference</span></span>  

 <xref:System.Transactions>  
 <span data-ttu-id="9fe88-121">Udostępnia klasy, które pozwalają na uczestniczenie w transakcjach kodu.</span><span class="sxs-lookup"><span data-stu-id="9fe88-121">Provides classes that allow your code to participate in transactions.</span></span> <span data-ttu-id="9fe88-122">Klasy obsługują transakcje z wieloma uczestnikami rozproszonymi, wieloma powiadomieniami fazowymi i trwałymi rejestracjami.</span><span class="sxs-lookup"><span data-stu-id="9fe88-122">The classes support transactions with multiple distributed participants, multiple phase notifications, and durable enlistments.</span></span>
