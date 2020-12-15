---
title: Migrowanie usługi żądania WCF-odpowiedź do gRPC-gRPC dla deweloperów WCF
description: Dowiedz się, jak migrować prostą usługę żądanie-odpowiedź z programu WCF do gRPC.
ms.date: 09/02/2019
ms.openlocfilehash: 29a7bc77bc3a4becd767fc7a50adff5b746f54bc
ms.sourcegitcommit: d0990c1c1ab2f81908360f47eafa8db9aa165137
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/15/2020
ms.locfileid: "97512700"
---
# <a name="migrate-a-wcf-request-reply-service-to-a-grpc-unary-rpc"></a><span data-ttu-id="95dc5-103">Migrowanie usługi żądania WCF-odpowiedź do gRPC jednoargumentowego wywołania procedury</span><span class="sxs-lookup"><span data-stu-id="95dc5-103">Migrate a WCF request-reply service to a gRPC unary RPC</span></span>

<span data-ttu-id="95dc5-104">W tej sekcji opisano sposób migrowania podstawowej usługi żądania-odpowiedzi w programie WCF do jednoargumentowej usługi RPC w ASP.NET Core gRPC.</span><span class="sxs-lookup"><span data-stu-id="95dc5-104">This section covers how to migrate a basic request-reply service in WCF to a unary RPC service in ASP.NET Core gRPC.</span></span> <span data-ttu-id="95dc5-105">Te usługi są najprostszymi typami usług w obu Windows Communication Foundation (WCF) i gRPC, więc jest to doskonałe miejsce do uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="95dc5-105">These services are the simplest service types in both Windows Communication Foundation (WCF) and gRPC, so it's an excellent place to start.</span></span> <span data-ttu-id="95dc5-106">Po przeprowadzeniu migracji usługi dowiesz się, jak wygenerować bibliotekę kliencką z tego samego `.proto` pliku, aby korzystać z usługi z aplikacji klienckiej platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="95dc5-106">After migrating the service, you'll learn how to generate a client library from the same `.proto` file to consume the service from a .NET client application.</span></span>

## <a name="the-wcf-solution"></a><span data-ttu-id="95dc5-107">Rozwiązanie WCF</span><span class="sxs-lookup"><span data-stu-id="95dc5-107">The WCF solution</span></span>

<span data-ttu-id="95dc5-108">[Rozwiązanie PortfoliosSample](https://github.com/dotnet-architecture/grpc-for-wcf-developers/tree/master/PortfoliosSample/wcf/TraderSys) obejmuje prostą usługę portfolio żądanie-odpowiedź do pobrania pojedynczego portfolio lub wszystkich portfolio dla danego podmiotu gospodarczego.</span><span class="sxs-lookup"><span data-stu-id="95dc5-108">The [PortfoliosSample solution](https://github.com/dotnet-architecture/grpc-for-wcf-developers/tree/master/PortfoliosSample/wcf/TraderSys) includes a simple request-reply Portfolio service to download either a single portfolio or all portfolios for a given trader.</span></span> <span data-ttu-id="95dc5-109">Usługa jest zdefiniowana w interfejsie `IPortfolioService` z `ServiceContract` atrybutem:</span><span class="sxs-lookup"><span data-stu-id="95dc5-109">The service is defined in the interface `IPortfolioService` with a `ServiceContract` attribute:</span></span>

```csharp
[ServiceContract]
public interface IPortfolioService
{
    [OperationContract]
    Task<Portfolio> Get(Guid traderId, int portfolioId);

    [OperationContract]
    Task<List<Portfolio>> GetAll(Guid traderId);
}
```

<span data-ttu-id="95dc5-110">`Portfolio`Model to prosta Klasa języka C# oznaczona przy użyciu [schematu DataContract](xref:System.Runtime.Serialization.DataContractAttribute) , która obejmuje listę `PortfolioItem` obiektów.</span><span class="sxs-lookup"><span data-stu-id="95dc5-110">The `Portfolio` model is a simple C# class marked with [DataContract](xref:System.Runtime.Serialization.DataContractAttribute) and including a list of `PortfolioItem` objects.</span></span> <span data-ttu-id="95dc5-111">Modele te są zdefiniowane w `TraderSys.PortfolioData` projekcie wraz z klasą repozytorium, która reprezentuje abstrakcję dostępu do danych.</span><span class="sxs-lookup"><span data-stu-id="95dc5-111">These models are defined in the `TraderSys.PortfolioData` project along with a repository class that represents a data access abstraction.</span></span>

```csharp
[DataContract]
public class Portfolio
{
    [DataMember]
    public int Id { get; set; }

    [DataMember]
    public Guid TraderId { get; set; }

    [DataMember]
    public List<PortfolioItem> Items { get; set; }
}

[DataContract]
public class PortfolioItem
{
    [DataMember]
    public int Id { get; set; }

    [DataMember]
    public int ShareId { get; set; }

    [DataMember]
    public int Holding { get; set; }

    [DataMember]
    public decimal Cost { get; set; }
}
```

<span data-ttu-id="95dc5-112">`ServiceContract`Implementacja używa klasy repozytorium dostarczonej za pośrednictwem iniekcji zależności, która zwraca wystąpienia `DataContract` typów:</span><span class="sxs-lookup"><span data-stu-id="95dc5-112">The `ServiceContract` implementation uses a repository class provided via dependency injection that returns instances of the `DataContract` types:</span></span>

```csharp
public class PortfolioService : IPortfolioService
{
    private readonly IPortfolioRepository _repository;

    public PortfolioService(IPortfolioRepository repository)
    {
        _repository = repository;
    }

    public async Task<Portfolio> Get(Guid traderId, int portfolioId)
    {
        return await _repository.GetAsync(traderId, portfolioId);
    }

    public async Task<List<Portfolio>> GetAll(Guid traderId)
    {
        return await _repository.GetAllAsync(traderId);
    }
}
```

## <a name="the-portfoliosproto-file"></a><span data-ttu-id="95dc5-113">Plik portfolio. proto</span><span class="sxs-lookup"><span data-stu-id="95dc5-113">The portfolios.proto file</span></span>

<span data-ttu-id="95dc5-114">Jeśli wykonano instrukcje w poprzedniej sekcji, powinien istnieć projekt gRPC z `portfolios.proto` plikiem, który wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="95dc5-114">If you followed the instructions in the previous section, you should have a gRPC project with a `portfolios.proto` file that looks like this:</span></span>

```protobuf
syntax = "proto3";

option csharp_namespace = "TraderSys.Portfolios.Protos";

package PortfolioServer;

service Portfolios {
  // RPCs will go here
}
```

<span data-ttu-id="95dc5-115">Pierwszym krokiem jest Migrowanie `DataContract` klas do ich odpowiedników protobuf.</span><span class="sxs-lookup"><span data-stu-id="95dc5-115">The first step is to migrate the `DataContract` classes to their Protobuf equivalents.</span></span>

## <a name="convert-the-datacontract-classes-to-grpc-messages"></a><span data-ttu-id="95dc5-116">Konwertowanie klas DataContract na komunikaty gRPC</span><span class="sxs-lookup"><span data-stu-id="95dc5-116">Convert the DataContract classes to gRPC messages</span></span>

<span data-ttu-id="95dc5-117">`PortfolioItem`Klasa zostanie najpierw przekonwertowana na komunikat protobuf, ponieważ `Portfolio` zależy od niej Klasa.</span><span class="sxs-lookup"><span data-stu-id="95dc5-117">The `PortfolioItem` class will be converted to a Protobuf message first, because the `Portfolio` class depends on it.</span></span> <span data-ttu-id="95dc5-118">Klasa jest prosta i trzy właściwości są mapowane bezpośrednio do typów danych gRPC.</span><span class="sxs-lookup"><span data-stu-id="95dc5-118">The class is simple, and three of the properties map directly to gRPC data types.</span></span> <span data-ttu-id="95dc5-119">`Cost`Właściwość, która przedstawia cenę płatną za udział w zakupie, jest `decimal` polem.</span><span class="sxs-lookup"><span data-stu-id="95dc5-119">The `Cost` property, which represents the price paid for the shares at purchase, is a `decimal` field.</span></span> <span data-ttu-id="95dc5-120">gRPC obsługuje tylko `float` lub `double` dla liczb rzeczywistych, które nie są odpowiednie dla waluty.</span><span class="sxs-lookup"><span data-stu-id="95dc5-120">gRPC supports only `float` or `double` for real numbers, which aren't suitable for currency.</span></span> <span data-ttu-id="95dc5-121">Ze względu na to, że ceny udziałów są różne dla co najmniej jednego centa, koszt może być wyrażony jako `int32` procent.</span><span class="sxs-lookup"><span data-stu-id="95dc5-121">Because share prices vary by a minimum of one cent, the cost can be expressed as an `int32` of cents.</span></span>

> [!NOTE]
> <span data-ttu-id="95dc5-122">Pamiętaj o używaniu `snake_case` nazw pól w `.proto` pliku.</span><span class="sxs-lookup"><span data-stu-id="95dc5-122">Remember to use `snake_case` for field names in your `.proto` file.</span></span> <span data-ttu-id="95dc5-123">Generator kodu w języku C# przekonwertuje je na `PascalCase` użytkownika, a użytkownicy innych języków poinformują Cię o poszanowaniu różnych standardów kodowania.</span><span class="sxs-lookup"><span data-stu-id="95dc5-123">The C# code generator will convert them to `PascalCase` for you, and users of other languages will thank you for respecting their different coding standards.</span></span>

```protobuf
message PortfolioItem {
    int32 id = 1;
    int32 share_id = 2;
    int32 holding = 3;
    int32 cost_cents = 4;
}
```

<span data-ttu-id="95dc5-124">`Portfolio`Klasa jest nieco bardziej skomplikowana.</span><span class="sxs-lookup"><span data-stu-id="95dc5-124">The `Portfolio` class is a little more complicated.</span></span> <span data-ttu-id="95dc5-125">W kodzie WCF deweloper użył `Guid` dla `TraderId` właściwości i zawiera `List<PortfolioItem>` .</span><span class="sxs-lookup"><span data-stu-id="95dc5-125">In the WCF code, the developer used a `Guid` for the `TraderId` property, and contains a `List<PortfolioItem>`.</span></span> <span data-ttu-id="95dc5-126">W protobuf, który nie ma typu pierwszej klasy `UUID` , należy użyć `string` dla `traderId` pola i przeanalizować go w własnym kodzie.</span><span class="sxs-lookup"><span data-stu-id="95dc5-126">In Protobuf, which doesn't have a first-class `UUID` type, you should use a `string` for the `traderId` field and parse it in your own code.</span></span> <span data-ttu-id="95dc5-127">Aby uzyskać listę elementów, użyj `repeated` słowa kluczowego w polu.</span><span class="sxs-lookup"><span data-stu-id="95dc5-127">For the list of items, use the `repeated` keyword on the field.</span></span>

```protobuf
message Portfolio {
    int32 id = 1;
    string trader_id = 2;
    repeated PortfolioItem items = 3;
}
```

<span data-ttu-id="95dc5-128">Teraz, gdy masz komunikaty dotyczące danych, możesz zadeklarować punkty końcowe usługi RPC.</span><span class="sxs-lookup"><span data-stu-id="95dc5-128">Now that you have the data messages, you can declare the service RPC endpoints.</span></span>

## <a name="convert-servicecontract-to-a-grpc-service"></a><span data-ttu-id="95dc5-129">Konwertuj kontrakt ServiceContract na usługę gRPC</span><span class="sxs-lookup"><span data-stu-id="95dc5-129">Convert ServiceContract to a gRPC service</span></span>

<span data-ttu-id="95dc5-130">Metoda WCF `Get` przyjmuje dwa parametry: `Guid traderId` i `int portfolioId` .</span><span class="sxs-lookup"><span data-stu-id="95dc5-130">The WCF `Get` method takes two parameters: `Guid traderId` and `int portfolioId`.</span></span> <span data-ttu-id="95dc5-131">metody usługi gRPC mogą przyjmować tylko jeden parametr, dlatego należy utworzyć komunikat, aby przechowywać dwie wartości.</span><span class="sxs-lookup"><span data-stu-id="95dc5-131">gRPC service methods can take only a single parameter, so you need to create a message to hold the two values.</span></span> <span data-ttu-id="95dc5-132">Typowym podejściem jest nazwa tych obiektów żądania o tej samej nazwie co metoda, po której następuje sufiks `Request` .</span><span class="sxs-lookup"><span data-stu-id="95dc5-132">It's common practice to name these request objects with the same name as the method followed by the suffix `Request`.</span></span> <span data-ttu-id="95dc5-133">Ponownie `string` jest używany dla `traderId` pola zamiast `Guid` .</span><span class="sxs-lookup"><span data-stu-id="95dc5-133">Again, `string` is being used for the `traderId` field instead of `Guid`.</span></span>

<span data-ttu-id="95dc5-134">Usługa może po prostu zwrócić `Portfolio` komunikat bezpośrednio, ale może to mieć wpływ na zgodność z poprzednimi wersjami w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="95dc5-134">The service could just return a `Portfolio` message directly, but again, this could affect backward compatibility in the future.</span></span> <span data-ttu-id="95dc5-135">Dobrym sposobem jest zdefiniowanie oddzielnych `Request` i `Response` komunikatów dla każdej metody w usłudze, nawet jeśli wiele z nich jest teraz tego samego.</span><span class="sxs-lookup"><span data-stu-id="95dc5-135">It's a good practice to define separate `Request` and `Response` messages for every method in a service, even if many of them are the same right now.</span></span> <span data-ttu-id="95dc5-136">Należy więc zadeklarować `GetResponse` komunikat przy użyciu pojedynczego `Portfolio` pola.</span><span class="sxs-lookup"><span data-stu-id="95dc5-136">So declare a `GetResponse` message with a single `Portfolio` field.</span></span>

<span data-ttu-id="95dc5-137">Ten przykład przedstawia deklarację metody usługi gRPC z `GetRequest` komunikatem:</span><span class="sxs-lookup"><span data-stu-id="95dc5-137">This example shows the declaration of the gRPC service method with the `GetRequest` message:</span></span>

```protobuf
message GetRequest {
    string trader_id = 1;
    int32 portfolio_id = 2;
}

message GetResponse {
    Portfolio portfolio = 1;
}

service Portfolios {
    rpc Get(GetRequest) returns (GetResponse);
}
```

<span data-ttu-id="95dc5-138">Metoda WCF `GetAll` przyjmuje tylko jeden parametr, `traderId` dlatego może wydawać się, że można określić `string` jako typ parametru.</span><span class="sxs-lookup"><span data-stu-id="95dc5-138">The WCF `GetAll` method takes only a single parameter, `traderId`, so it might seem that you could specify `string` as the parameter type.</span></span> <span data-ttu-id="95dc5-139">Ale gRPC wymaga zdefiniowanego typu wiadomości.</span><span class="sxs-lookup"><span data-stu-id="95dc5-139">But gRPC requires a defined message type.</span></span> <span data-ttu-id="95dc5-140">To wymaganie umożliwia wymuszenie użycia niestandardowych komunikatów dla wszystkich danych wejściowych i wyjściowych w celu zachowania zgodności z poprzednimi wersjami.</span><span class="sxs-lookup"><span data-stu-id="95dc5-140">This requirement helps to enforce the practice of using custom messages for all inputs and outputs, for future backward compatibility.</span></span>

<span data-ttu-id="95dc5-141">Metoda WCF zwraca również `List<Portfolio>` , ale z tego samego powodu nie zezwala na proste typy parametrów, gRPC nie będzie zezwalać `repeated Portfolio` jako zwracany typ.</span><span class="sxs-lookup"><span data-stu-id="95dc5-141">The WCF method also returns a `List<Portfolio>`, but for the same reason it doesn't allow simple parameter types, gRPC won't allow `repeated Portfolio` as a return type.</span></span> <span data-ttu-id="95dc5-142">Zamiast tego Utwórz `GetAllResponse` Typ, aby otoczyć listę.</span><span class="sxs-lookup"><span data-stu-id="95dc5-142">Instead, create a `GetAllResponse` type to wrap the list.</span></span>

> [!WARNING]
> <span data-ttu-id="95dc5-143">Być może wiesz, że tworzysz `PortfolioList` wiadomość lub podobną i używaj jej w wielu metodach usług, ale należy Odpornie na ten Temptation.</span><span class="sxs-lookup"><span data-stu-id="95dc5-143">You might be tempted to create a `PortfolioList` message or something similar and use it across multiple service methods, but you should resist this temptation.</span></span> <span data-ttu-id="95dc5-144">Nie jest możliwe, aby wiedzieć, w jaki sposób różne metody w usłudze zostaną rozłączone, dlatego należy zapewnić ich obsługę i czyszczenie ich komunikatów.</span><span class="sxs-lookup"><span data-stu-id="95dc5-144">It's impossible to know how the various methods on a service will evolve, so keep their messages specific and cleanly separated.</span></span>

```protobuf
message GetAllRequest {
    string trader_id = 1;
}

message PortfolioList {
    repeated Portfolio portfolios = 1;
}

service Portfolios {
    rpc Get(GetRequest) returns (Portfolio);
    rpc GetAll(GetAllRequest) returns (GetAllResponse);
}
```

<span data-ttu-id="95dc5-145">Jeśli zapiszesz projekt z tymi zmianami, obiekt docelowy kompilacji gRPC zostanie uruchomiony w tle i wygeneruje wszystkie typy komunikatów protobuf i klasę bazową, którą można odziedziczyć w celu zaimplementowania usługi.</span><span class="sxs-lookup"><span data-stu-id="95dc5-145">If you save your project with these changes, the gRPC build target will run in the background and generate all the Protobuf message types and a base class that you can inherit to implement the service.</span></span>

<span data-ttu-id="95dc5-146">Otwórz `Services/GreeterService.cs` klasę i Usuń przykładowy kod.</span><span class="sxs-lookup"><span data-stu-id="95dc5-146">Open the `Services/GreeterService.cs` class and delete the example code.</span></span> <span data-ttu-id="95dc5-147">Teraz możesz dodać implementację usługi portfolio.</span><span class="sxs-lookup"><span data-stu-id="95dc5-147">Now you can add the Portfolio service implementation.</span></span> <span data-ttu-id="95dc5-148">Wygenerowana Klasa bazowa będzie w `Protos` przestrzeni nazw i jest generowana jako Klasa zagnieżdżona.</span><span class="sxs-lookup"><span data-stu-id="95dc5-148">The generated base class will be in the `Protos` namespace and is generated as a nested class.</span></span> <span data-ttu-id="95dc5-149">gRPC tworzy klasę statyczną o takiej samej nazwie jak usługa w `.proto` pliku i klasie bazowej z sufiksem `Base` wewnątrz tej klasy statycznej, więc pełny identyfikator dla typu podstawowego to `TraderSys.Portfolios.Protos.Portfolios.PortfoliosBase` .</span><span class="sxs-lookup"><span data-stu-id="95dc5-149">gRPC creates a static class with the same name as the service in the `.proto` file and a base class with the suffix `Base` inside that static class, so the full identifier for the base type is `TraderSys.Portfolios.Protos.Portfolios.PortfoliosBase`.</span></span>

```csharp
namespace TraderSys.Portfolios.Services
{
    public class PortfolioService : Protos.Portfolios.PortfoliosBase
    {
    }
}
```

<span data-ttu-id="95dc5-150">Klasa bazowa deklaruje `virtual` metody dla `Get` i `GetAll` , które mogą zostać zastąpione w celu zaimplementowania usługi.</span><span class="sxs-lookup"><span data-stu-id="95dc5-150">The base class declares `virtual` methods for `Get` and `GetAll` that can be overridden to implement the service.</span></span> <span data-ttu-id="95dc5-151">Metody są `virtual` zamiast tego, `abstract` Jeśli nie zostaną zaimplementowane, usługa może zwrócić jawny `Unimplemented` kod stanu gRPC, podobnie jak w przypadku `NotImplementedException` zwykłego kodu w języku C#.</span><span class="sxs-lookup"><span data-stu-id="95dc5-151">The methods are `virtual` rather than `abstract` so that if you don't implement them, the service can return an explicit gRPC `Unimplemented` status code, much like you might throw a `NotImplementedException` in regular C# code.</span></span>

<span data-ttu-id="95dc5-152">Sygnatura wszystkich jednoargumentowych metod usługi gRPC w ASP.NET Core jest spójna.</span><span class="sxs-lookup"><span data-stu-id="95dc5-152">The signature for all gRPC unary service methods in ASP.NET Core is consistent.</span></span> <span data-ttu-id="95dc5-153">Istnieją dwa parametry: pierwszy to typ komunikatu zadeklarowany w `.proto` pliku, a drugi to `ServerCallContext` , który działa podobnie do `HttpContext` ASP.NET Core od.</span><span class="sxs-lookup"><span data-stu-id="95dc5-153">There are two parameters: the first is the message type declared in the `.proto` file, and the second is a `ServerCallContext` that works similarly to the `HttpContext` from ASP.NET Core.</span></span> <span data-ttu-id="95dc5-154">W rzeczywistości istnieje metoda rozszerzająca wywołana `GetHttpContext` na `ServerCallContext` klasie, która może być używana do uzyskiwania bazowego elementu `HttpContext` , chociaż nie trzeba go często używać.</span><span class="sxs-lookup"><span data-stu-id="95dc5-154">In fact, there's an extension method called `GetHttpContext` on the `ServerCallContext` class that you can use to get the underlying `HttpContext`, although you shouldn't need to use it often.</span></span> <span data-ttu-id="95dc5-155">Zapoznajemy się w `ServerCallContext` dalszej części tego rozdziału, a także w rozdziale zawierającym Opis uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="95dc5-155">We'll take a look at `ServerCallContext` later in this chapter, and also in the chapter that discusses authentication.</span></span>

<span data-ttu-id="95dc5-156">Zwracany typ metody to `Task<T>` , gdzie `T` jest typem komunikatu odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="95dc5-156">The method's return type is a `Task<T>`, where `T` is the response message type.</span></span> <span data-ttu-id="95dc5-157">Wszystkie metody usługi gRPC są asynchroniczne.</span><span class="sxs-lookup"><span data-stu-id="95dc5-157">All gRPC service methods are asynchronous.</span></span>

## <a name="migrate-the-portfoliodata-library-to-net-core"></a><span data-ttu-id="95dc5-158">Migrowanie biblioteki PortfolioData do platformy .NET Core</span><span class="sxs-lookup"><span data-stu-id="95dc5-158">Migrate the PortfolioData library to .NET Core</span></span>

<span data-ttu-id="95dc5-159">W tym momencie projekt wymaga repozytorium portfolio i modeli zawartych w `TraderSys.PortfolioData` bibliotece klas w rozwiązaniu WCF.</span><span class="sxs-lookup"><span data-stu-id="95dc5-159">At this point, the project needs the Portfolio repository and models contained in the `TraderSys.PortfolioData` class library in the WCF solution.</span></span> <span data-ttu-id="95dc5-160">Najprostszym sposobem na ich przełączenie jest utworzenie nowej biblioteki klas przy użyciu okna dialogowego **Nowy projekt** programu Visual Studio z szablonem Biblioteka klas (.NET standard) lub z wiersza polecenia przy użyciu interfejs wiersza polecenia platformy .NET Core, uruchomienie tych poleceń z katalogu zawierającego `TraderSys.sln` plik:</span><span class="sxs-lookup"><span data-stu-id="95dc5-160">The easiest way to bring them across is to create a new class library by using either the Visual Studio **New project** dialog box with the Class Library (.NET Standard) template, or from the command line by using the .NET Core CLI, running these commands from the directory that contains the `TraderSys.sln` file:</span></span>

```dotnetcli
dotnet new classlib -o src/TraderSys.PortfolioData
dotnet sln add src/TraderSys.PortfolioData
```

<span data-ttu-id="95dc5-161">Po utworzeniu biblioteki i dodaniu jej do rozwiązania Usuń wygenerowany `Class1.cs` plik i skopiuj pliki z biblioteki rozwiązania WCF do folderu nowej biblioteki klas, utrzymując strukturę folderów:</span><span class="sxs-lookup"><span data-stu-id="95dc5-161">After you've created the library and added it to the solution, delete the generated `Class1.cs` file and copy the files from the WCF solution's library into the new class library's folder, keeping the folder structure:</span></span>

```
Models
  Portfolio.cs
  PortfolioItem.cs
IPortfolioRepository.cs
PortfolioRepository.cs
```

<span data-ttu-id="95dc5-162">Projekty platformy .NET w stylu zestawu SDK automatycznie zawierają wszystkie `.cs` pliki w ich własnym katalogu, dlatego nie trzeba jawnie dodawać ich do projektu.</span><span class="sxs-lookup"><span data-stu-id="95dc5-162">SDK-style .NET projects automatically include any `.cs` files in or under their own directory, so you don't need to explicitly add them to the project.</span></span> <span data-ttu-id="95dc5-163">Jedyne pozostała czynność polega na usunięciu `DataContract` `DataMember` atrybutów i `Portfolio` z `PortfolioItem` klas i, tak aby były one zwykłymi klasami C#:</span><span class="sxs-lookup"><span data-stu-id="95dc5-163">The only step remaining is to remove the `DataContract` and `DataMember` attributes from the `Portfolio` and `PortfolioItem` classes so they're plain old C# classes:</span></span>

```csharp
public class Portfolio
{
    public int Id { get; set; }
    public Guid TraderId { get; set; }
    public List<PortfolioItem> Items { get; set; }
}

public class PortfolioItem
{
    public int Id { get; set; }
    public int ShareId { get; set; }
    public int Holding { get; set; }
    public decimal Cost { get; set; }
}
```

## <a name="use-aspnet-core-dependency-injection"></a><span data-ttu-id="95dc5-164">Użyj iniekcji zależności ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="95dc5-164">Use ASP.NET Core dependency injection</span></span>

<span data-ttu-id="95dc5-165">Teraz można dodać odwołanie do tej biblioteki do projektu aplikacji gRPC i użyć `PortfolioRepository` klasy przy użyciu iniekcji zależności w implementacji usługi gRPC.</span><span class="sxs-lookup"><span data-stu-id="95dc5-165">Now you can add a reference to this library to the gRPC application project and consume the `PortfolioRepository` class by using dependency injection in the gRPC service implementation.</span></span> <span data-ttu-id="95dc5-166">W aplikacji WCF funkcja wstrzykiwania zależności została dostarczona przez kontener Autofac IoC.</span><span class="sxs-lookup"><span data-stu-id="95dc5-166">In the WCF application, dependency injection was provided by the Autofac IoC container.</span></span> <span data-ttu-id="95dc5-167">ASP.NET Core ma iniekcję zależności rozszerzania w.</span><span class="sxs-lookup"><span data-stu-id="95dc5-167">ASP.NET Core has dependency injection baked in.</span></span> <span data-ttu-id="95dc5-168">Repozytorium można zarejestrować w `ConfigureServices` metodzie w `Startup` klasie:</span><span class="sxs-lookup"><span data-stu-id="95dc5-168">You can register the repository in the `ConfigureServices` method in the `Startup` class:</span></span>

```csharp
public class Startup
{
    public void ConfigureServices(IServiceCollection services)
    {
        // Register the repository class as a scoped service (instance per request)
        services.AddScoped<IPortfolioRepository, PortfolioRepository>();

        services.AddGrpc();
    }

    // ...
}
```

<span data-ttu-id="95dc5-169">`IPortfolioRepository`Implementację można teraz określić jako parametr konstruktora w `PortfolioService` klasie w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="95dc5-169">The `IPortfolioRepository` implementation can now be specified as a constructor parameter in the `PortfolioService` class, as follows:</span></span>

```csharp
public class PortfolioService : Protos.Portfolios.PortfoliosBase
{
    private readonly IPortfolioRepository _repository;

    public PortfolioService(IPortfolioRepository repository)
    {
        _repository = repository;
    }
}
```

## <a name="implement-the-grpc-service"></a><span data-ttu-id="95dc5-170">Implementowanie usługi gRPC</span><span class="sxs-lookup"><span data-stu-id="95dc5-170">Implement the gRPC service</span></span>

<span data-ttu-id="95dc5-171">Po zadeklarowaniu komunikatów i usługi w `portfolios.proto` pliku należy zaimplementować metody usługi w `PortfolioService` klasie, która dziedziczy z klasy generowanej przez gRPC `Portfolios.PortfoliosBase` .</span><span class="sxs-lookup"><span data-stu-id="95dc5-171">Now that you've declared your messages and your service in the `portfolios.proto` file, you have to implement the service methods in the `PortfolioService` class that inherits from the gRPC-generated `Portfolios.PortfoliosBase` class.</span></span> <span data-ttu-id="95dc5-172">Metody są zadeklarowane jako `virtual` w klasie bazowej.</span><span class="sxs-lookup"><span data-stu-id="95dc5-172">The methods are declared as `virtual` in the base class.</span></span> <span data-ttu-id="95dc5-173">Jeśli ich nie zastąpisz, domyślnie zwróci kod stanu gRPC "nie zaimplementowana".</span><span class="sxs-lookup"><span data-stu-id="95dc5-173">If you don't override them, they'll return a gRPC "Not Implemented" status code by default.</span></span>

<span data-ttu-id="95dc5-174">Zacznij od wprowadzenia `Get` metody.</span><span class="sxs-lookup"><span data-stu-id="95dc5-174">Start by implementing the `Get` method.</span></span> <span data-ttu-id="95dc5-175">Domyślne przesłonięcie wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="95dc5-175">The default override looks like this example:</span></span>

```csharp
public override Task<GetResponse> Get(GetRequest request, ServerCallContext context)
{
    return base.Get(request, context);
}
```

<span data-ttu-id="95dc5-176">Pierwszym problemem jest `request.TraderId` ciąg, a usługa wymaga `Guid` .</span><span class="sxs-lookup"><span data-stu-id="95dc5-176">The first problem is that `request.TraderId` is a string, and the service requires a `Guid`.</span></span> <span data-ttu-id="95dc5-177">Mimo że oczekiwany format ciągu to `UUID` , kod musi zajmować się możliwością, że obiekt wywołujący wysłał nieprawidłową wartość i odpowiada odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="95dc5-177">Even though the expected format for the string is `UUID`, the code has to deal with the possibility that a caller has sent an invalid value and respond appropriately.</span></span> <span data-ttu-id="95dc5-178">Usługa może odpowiedzieć z błędami przez wyrzucanie `RpcException` i użycie standardowego `InvalidArgument` kodu stanu do wyznaczania problemu:</span><span class="sxs-lookup"><span data-stu-id="95dc5-178">The service can respond with errors by throwing an `RpcException` and use the standard `InvalidArgument` status code to express the problem:</span></span>

```csharp
public override Task<GetResponse> Get(GetRequest request, ServerCallContext context)
{
    if (!Guid.TryParse(request.TraderId, out var traderId))
    {
        throw new RpcException(new Status(StatusCode.InvalidArgument, "traderId must be a UUID"));
    }

    return base.Get(request, context);
}
```

<span data-ttu-id="95dc5-179">Po poprawnym ustawieniu `Guid` wartości można `traderId` użyć repozytorium, aby pobrać portfolio i zwrócić go do klienta:</span><span class="sxs-lookup"><span data-stu-id="95dc5-179">After there's a proper `Guid` value for `traderId`, you can use the repository to retrieve the Portfolio and return it to the client:</span></span>

```csharp
    var response = new GetResponse
    {
        Portfolio = await _repository.GetAsync(request.TraderId, request.PortfolioId)
    };
```

### <a name="map-internal-models-to-grpc-messages"></a><span data-ttu-id="95dc5-180">Mapowanie wewnętrznych modeli na komunikaty gRPC</span><span class="sxs-lookup"><span data-stu-id="95dc5-180">Map internal models to gRPC messages</span></span>

<span data-ttu-id="95dc5-181">Poprzedni kod nie działa, ponieważ repozytorium zwraca własny model POCO `Portfolio` , ale gRPC wymaga własnego komunikatu protobuf `Portfolio` .</span><span class="sxs-lookup"><span data-stu-id="95dc5-181">The previous code doesn't actually work because the repository is returning its own POCO model `Portfolio`, but gRPC needs its own Protobuf message `Portfolio`.</span></span> <span data-ttu-id="95dc5-182">Podobnie jak podczas mapowania typów Entity Framework na typy transferu danych najlepszym rozwiązaniem jest zapewnienie konwersji między nimi.</span><span class="sxs-lookup"><span data-stu-id="95dc5-182">As when you map Entity Framework types to data transfer types, the best solution is to provide a conversion between the two.</span></span> <span data-ttu-id="95dc5-183">Dobrym miejscem do umieszczenia kodu dla tej konwersji jest Klasa wygenerowana protobuf, która jest zadeklarowana jako `partial` Klasa, aby można ją było rozszerzyć:</span><span class="sxs-lookup"><span data-stu-id="95dc5-183">A good place to put the code for this conversion is in the Protobuf-generated class, which is declared as a `partial` class so it can be extended:</span></span>

```csharp
namespace TraderSys.Portfolios.Protos
{
    public partial class PortfolioItem
    {
        public static PortfolioItem FromRepositoryModel(PortfolioData.Models.PortfolioItem source)
        {
            if (source is null) return null;

            return new PortfolioItem
            {
                Id = source.Id,
                ShareId = source.ShareId,
                Holding = source.Holding,
                CostCents = (int)(source.Cost * 100)
            };
        }
    }

    public partial class Portfolio
    {
        public static Portfolio FromRepositoryModel(PortfolioData.Models.Portfolio source)
        {
            if (source is null) return null;

            var target = new Portfolio
            {
                Id = source.Id,
                TraderId = source.TraderId.ToString(),
            };

            target.Items.AddRange(source.Items.Select(PortfolioItem.FromRepositoryModel));

            return target;
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="95dc5-184">Można użyć biblioteki, takiej jak [automapowania](https://automapper.org/) , do obsługi tej konwersji z klas wewnętrznych modelu do typów protobuf, o ile nie skonfigurowano konwersji typu niższego poziomu, takich jak `string` / `Guid` lub `decimal` / `double` i mapowania listy.</span><span class="sxs-lookup"><span data-stu-id="95dc5-184">You could use a library like [AutoMapper](https://automapper.org/) to handle this conversion from internal model classes to Protobuf types, as long as you configure the lower-level type conversions like `string`/`Guid` or `decimal`/`double` and the list mapping.</span></span>

<span data-ttu-id="95dc5-185">Teraz, gdy masz kod konwersji, możesz wykonać `Get` implementację metody:</span><span class="sxs-lookup"><span data-stu-id="95dc5-185">Now that you have the conversion code in place, you can complete the `Get` method implementation:</span></span>

```csharp
public override async Task<GetResponse> Get(GetRequest request, ServerCallContext context)
{
    if (!Guid.TryParse(request.TraderId, out var traderId))
    {
        throw new RpcException(new Status(StatusCode.InvalidArgument, "traderId must be a UUID"));
    }

    var portfolio = await _repository.GetAsync(traderId, request.PortfolioId);

    return new GetResponse
    {
        Portfolio = Portfolio.FromRepositoryModel(portfolio)
    };
}

```

<span data-ttu-id="95dc5-186">Implementacja `GetAll` metody jest podobna.</span><span class="sxs-lookup"><span data-stu-id="95dc5-186">The implementation of the `GetAll` method is similar.</span></span> <span data-ttu-id="95dc5-187">Należy zauważyć, że `repeated` pola w komunikatach protobuf są generowane jako `readonly` właściwości typu `RepeatedField<T>` , dlatego należy dodać do nich elementy przy użyciu `AddRange` metody, jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="95dc5-187">Note that the `repeated` fields on Protobuf messages are generated as `readonly` properties of type `RepeatedField<T>`, so you have to add items to them by using the `AddRange` method, like in this example:</span></span>

```csharp
public override async Task<GetAllResponse> GetAll(GetAllRequest request, ServerCallContext context)
{
    if (!Guid.TryParse(request.TraderId, out var traderId))
    {
        throw new RpcException(new Status(StatusCode.InvalidArgument, "traderId must be a UUID"));
    }

    var portfolios = await _repository.GetAllAsync(traderId);

    var response = new GetAllResponse();
    response.Portfolios.AddRange(portfolios.Select(Portfolio.FromRepositoryModel));

    return response;
}
```

<span data-ttu-id="95dc5-188">Pomyślnie przeprowadzono migrację usługi żądania WCF-odpowiedź do gRPC, przyjrzyjmy się tworzeniu klienta dla tego `.proto` pliku.</span><span class="sxs-lookup"><span data-stu-id="95dc5-188">Having successfully migrated the WCF request-reply service to gRPC, let's look at creating a client for it from the `.proto` file.</span></span>

## <a name="generate-client-code"></a><span data-ttu-id="95dc5-189">Generuj kod klienta</span><span class="sxs-lookup"><span data-stu-id="95dc5-189">Generate client code</span></span>

<span data-ttu-id="95dc5-190">Utwórz bibliotekę klas .NET Standard w tym samym rozwiązaniu, aby zawierała klienta.</span><span class="sxs-lookup"><span data-stu-id="95dc5-190">Create a .NET Standard class library in the same solution to contain the client.</span></span> <span data-ttu-id="95dc5-191">Jest to przede wszystkim przykład tworzenia kodu klienta, ale można go spakować przy użyciu NuGet i rozpowszechniać w ramach wewnętrznego repozytorium dla innych zespołów .NET do użycia.</span><span class="sxs-lookup"><span data-stu-id="95dc5-191">This is primarily an example of creating client code, but you could package such a library by using NuGet and distribute it on an internal repository for other .NET teams to consume.</span></span> <span data-ttu-id="95dc5-192">Przejdź dalej i Dodaj nową bibliotekę klas .NET Standard wywołana `TraderSys.Portfolios.Client` do rozwiązania i Usuń `Class1.cs` plik.</span><span class="sxs-lookup"><span data-stu-id="95dc5-192">Go ahead and add a new .NET Standard class library called `TraderSys.Portfolios.Client` to the solution and delete the `Class1.cs` file.</span></span>

> [!CAUTION]
> <span data-ttu-id="95dc5-193">Pakiet NuGet [GRPC .NET. Client](https://www.nuget.org/packages/Grpc.Net.Client) wymaga platformy .net Core 3,0 (lub innego środowiska uruchomieniowego zgodnego z .NET Standard 2,1).</span><span class="sxs-lookup"><span data-stu-id="95dc5-193">The [Grpc.Net.Client](https://www.nuget.org/packages/Grpc.Net.Client) NuGet package requires .NET Core 3.0 (or another .NET Standard 2.1-compliant runtime).</span></span> <span data-ttu-id="95dc5-194">Starsze wersje .NET Framework i .NET Core są obsługiwane przez pakiet NuGet [GRPC. Core](https://www.nuget.org/packages/Grpc.Core) .</span><span class="sxs-lookup"><span data-stu-id="95dc5-194">Earlier versions of .NET Framework and .NET Core are supported by the [Grpc.Core](https://www.nuget.org/packages/Grpc.Core) NuGet package.</span></span>

<span data-ttu-id="95dc5-195">W programie Visual Studio 2019 można dodać odwołania do usług gRPC w sposób podobny do sposobu dodawania odwołań do usług do projektów WCF we wcześniejszych wersjach programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="95dc5-195">In Visual Studio 2019, you can add references to gRPC services in a way that's similar to how you'd add service references to WCF projects in earlier versions of Visual Studio.</span></span> <span data-ttu-id="95dc5-196">Odwołania do usług i połączone usługi są teraz zarządzane w tym samym interfejsie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="95dc5-196">Service references and connected services are all managed under the same UI now.</span></span> <span data-ttu-id="95dc5-197">Aby uzyskać dostęp do interfejsu użytkownika, kliknij prawym przyciskiem myszy węzeł **zależności** w `TraderSys.Portfolios.Client` projekcie w Eksplorator rozwiązań i wybierz polecenie **Dodaj podłączoną usługę**.</span><span class="sxs-lookup"><span data-stu-id="95dc5-197">You can access the UI by right-clicking the **Dependencies** node in the `TraderSys.Portfolios.Client` project in Solution Explorer and selecting **Add Connected Service**.</span></span> <span data-ttu-id="95dc5-198">W wyświetlonym oknie narzędzi wybierz sekcję odwołania do **usługi** , a następnie wybierz pozycję **Dodaj nowe odwołanie do usługi gRPC**:</span><span class="sxs-lookup"><span data-stu-id="95dc5-198">In the tool window that appears, select the **Service References** section and then select **Add new gRPC service reference**:</span></span>

![Interfejs użytkownika usług połączonych w programie Visual Studio 2019](media/migrate-request-reply/add-connected-service.png)

<span data-ttu-id="95dc5-200">Przejdź do `portfolios.proto` pliku w `TraderSys.Portfolios` projekcie, pozostaw **Klient** w obszarze **Wybierz typ klasy do wygenerowania**, a następnie wybierz przycisk **OK**:</span><span class="sxs-lookup"><span data-stu-id="95dc5-200">Browse to the `portfolios.proto` file in the `TraderSys.Portfolios` project, leave **Client** under **Select the type of class to be generated**, and then select **OK**:</span></span>

![Okno dialogowe Dodawanie nowego odwołania do usługi gRPC w programie Visual Studio 2019](media/migrate-request-reply/add-new-grpc-service-reference.png)

> [!TIP]
> <span data-ttu-id="95dc5-202">Zwróć uwagę, że to okno dialogowe zawiera również pole adresu URL.</span><span class="sxs-lookup"><span data-stu-id="95dc5-202">Notice that this dialog box also provides a URL field.</span></span> <span data-ttu-id="95dc5-203">Jeśli Twoja organizacja utrzymuje katalog plików dostępny dla sieci Web `.proto` , możesz utworzyć klientów bezpośrednio, ustawiając ten adres URL.</span><span class="sxs-lookup"><span data-stu-id="95dc5-203">If your organization maintains a web-accessible directory of `.proto` files, you can create clients just by setting this URL address.</span></span>

<span data-ttu-id="95dc5-204">W przypadku korzystania z funkcji **Dodaj podłączoną usługę** programu Visual Studio `portfolios.proto` plik jest dodawany do projektu biblioteki klas jako *plik połączony* , a nie skopiowane, więc zmiany w pliku w projekcie usługi zostaną automatycznie zastosowane w projekcie klienta.</span><span class="sxs-lookup"><span data-stu-id="95dc5-204">When you use the Visual Studio **Add Connected Service** feature, the `portfolios.proto` file is added to the class library project as a *linked file* rather than copied, so changes to the file in the service project will automatically be applied in the client project.</span></span> <span data-ttu-id="95dc5-205">`<Protobuf>`Element w `csproj` pliku wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="95dc5-205">The `<Protobuf>` element in the `csproj` file looks like this:</span></span>

```xml
<Protobuf Include="..\TraderSys.Portfolios\Protos\portfolios.proto" GrpcServices="Client">
  <Link>Protos\portfolios.proto</Link>
</Protobuf>
```

> [!TIP]
> <span data-ttu-id="95dc5-206">Jeśli nie używasz programu Visual Studio lub wolisz pracować z wiersza polecenia, możesz użyć `dotnet-grpc` globalnego narzędzia do zarządzania odwołaniami protobuf w projekcie .NET gRPC.</span><span class="sxs-lookup"><span data-stu-id="95dc5-206">If you're not using Visual Studio or prefer to work from the command line, you can use the `dotnet-grpc` global tool to manage Protobuf references in a .NET gRPC project.</span></span> <span data-ttu-id="95dc5-207">Aby uzyskać więcej informacji, zapoznaj się z [ `dotnet-grpc` dokumentacją](/aspnet/core/grpc/dotnet-grpc).</span><span class="sxs-lookup"><span data-stu-id="95dc5-207">For more information, see the [`dotnet-grpc` documentation](/aspnet/core/grpc/dotnet-grpc).</span></span>

### <a name="use-the-portfolios-service-from-a-client-application"></a><span data-ttu-id="95dc5-208">Korzystanie z usługi portfolio w aplikacji klienckiej</span><span class="sxs-lookup"><span data-stu-id="95dc5-208">Use the Portfolios service from a client application</span></span>

<span data-ttu-id="95dc5-209">Poniższy kod stanowi krótki przykład korzystania z wygenerowanego klienta w aplikacji konsolowej.</span><span class="sxs-lookup"><span data-stu-id="95dc5-209">The following code is a brief example of how to use the generated client in a console application.</span></span> <span data-ttu-id="95dc5-210">Bardziej szczegółowa Eksploracja kodu klienta gRPC znajduje się na końcu tego rozdziału.</span><span class="sxs-lookup"><span data-stu-id="95dc5-210">A more detailed exploration of the gRPC client code is at the end of this chapter.</span></span>

```csharp
public class Program
{
    public async Task Main(string[] args)
    {
        GetResponse response;

        using (var channel = GrpcChannel.ForAddress("https://localhost:5001"))
        {
            var client = new Protos.Portfolios.PortfoliosClient(channel);

            response = await client.GetAsync(new GetRequest
            {
                TraderId = args[0],
                PortfolioId = int.Parse(args[1])
            });
        }

        foreach (var item in response.Portfolio.Items)
        {
            Console.WriteLine($"Holding {item.Holding} of Share ID {item.ShareId}.");
        }
    }
}
```

<span data-ttu-id="95dc5-211">Przeprowadzono migrację podstawowej aplikacji WCF do ASP.NET Core usługi gRPC i utworzono klienta w celu korzystania z usługi z poziomu aplikacji .NET.</span><span class="sxs-lookup"><span data-stu-id="95dc5-211">You've now migrated a basic WCF application to an ASP.NET Core gRPC service and created a client to consume the service from a .NET application.</span></span> <span data-ttu-id="95dc5-212">Następna sekcja będzie obejmować więcej procesów usług dupleksowych.</span><span class="sxs-lookup"><span data-stu-id="95dc5-212">The next section will cover the more involved duplex services.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="95dc5-213">[Poprzedni](create-project.md) 
> [Dalej](migrate-duplex-services.md)</span><span class="sxs-lookup"><span data-stu-id="95dc5-213">[Previous](create-project.md)
[Next](migrate-duplex-services.md)</span></span>
