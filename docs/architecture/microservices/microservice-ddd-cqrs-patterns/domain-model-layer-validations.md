---
title: Projektowanie reguł weryfikacji w warstwie modelu domeny
description: Architektura mikrousług platformy .NET dla aplikacji platformy .NET w kontenerze | Poznaj kluczowe pojęcia związane z walidacją modelu domeny.
ms.date: 10/08/2018
ms.openlocfilehash: 1d3196d2130df33969ed231bccfe0fc6f0af2ad8
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/30/2019
ms.locfileid: "70295963"
---
# <a name="design-validations-in-the-domain-model-layer"></a><span data-ttu-id="1943b-103">Walidacje projektu w warstwie modelu domeny</span><span class="sxs-lookup"><span data-stu-id="1943b-103">Design validations in the domain model layer</span></span>

<span data-ttu-id="1943b-104">W DDD reguły walidacji mogą być traktowane jako nieposiadające wariantów.</span><span class="sxs-lookup"><span data-stu-id="1943b-104">In DDD, validation rules can be thought as invariants.</span></span> <span data-ttu-id="1943b-105">Główną odpowiedzialnością za zagregowaną jest wymuszenie niewariantów między zmianami stanu dla wszystkich jednostek w ramach tej agregacji.</span><span class="sxs-lookup"><span data-stu-id="1943b-105">The main responsibility of an aggregate is to enforce invariants across state changes for all the entities within that aggregate.</span></span>

<span data-ttu-id="1943b-106">Jednostki domeny powinny być zawsze prawidłowymi jednostkami.</span><span class="sxs-lookup"><span data-stu-id="1943b-106">Domain entities should always be valid entities.</span></span> <span data-ttu-id="1943b-107">Istnieje pewna liczba nieodmian dla obiektu, który powinien mieć zawsze wartość true.</span><span class="sxs-lookup"><span data-stu-id="1943b-107">There are a certain number of invariants for an object that should always be true.</span></span> <span data-ttu-id="1943b-108">Na przykład obiekt elementu Order zawsze musi mieć ilość, która musi być dodatnią liczbą całkowitą oraz nazwę artykułu i cenę.</span><span class="sxs-lookup"><span data-stu-id="1943b-108">For example, an order item object always has to have a quantity that must be a positive integer, plus an article name and price.</span></span> <span data-ttu-id="1943b-109">Z tego względu wymuszanie nieistniejące jest odpowiedzialne za jednostki domeny (zwłaszcza w przypadku agregacji głównej), a obiekt jednostki nie powinien być w stanie istnieć.</span><span class="sxs-lookup"><span data-stu-id="1943b-109">Therefore, invariants enforcement is the responsibility of the domain entities (especially of the aggregate root) and an entity object should not be able to exist without being valid.</span></span> <span data-ttu-id="1943b-110">Niezmienne reguły są po prostu wyrażone jako kontrakty, a wyjątki lub powiadomienia są zgłaszane, gdy są naruszane.</span><span class="sxs-lookup"><span data-stu-id="1943b-110">Invariant rules are simply expressed as contracts, and exceptions or notifications are raised when they are violated.</span></span>

<span data-ttu-id="1943b-111">Przyczyną tego jest fakt, że występuje wiele usterek, ponieważ obiekty są w stanie, w którym nigdy nie powinny.</span><span class="sxs-lookup"><span data-stu-id="1943b-111">The reasoning behind this is that many bugs occur because objects are in a state they should never have been in.</span></span> <span data-ttu-id="1943b-112">Poniżej znajduje się dobre wyjaśnienie od Grega młodych w [dyskusji online](https://jeffreypalermo.com/2009/05/the-fallacy-of-the-always-valid-entity/):</span><span class="sxs-lookup"><span data-stu-id="1943b-112">The following is a good explanation from Greg Young in an [online discussion](https://jeffreypalermo.com/2009/05/the-fallacy-of-the-always-valid-entity/):</span></span>

<span data-ttu-id="1943b-113">Zaproponujemy teraz SendUserCreationEmailService, który zajmuje profil użytkownika... Jak możemy usprawnić działanie tej usługi, która nie ma wartości null?</span><span class="sxs-lookup"><span data-stu-id="1943b-113">Let's propose we now have a SendUserCreationEmailService that takes a UserProfile ... how can we rationalize in that service that Name is not null?</span></span> <span data-ttu-id="1943b-114">Czy sprawdzimy ją ponownie?</span><span class="sxs-lookup"><span data-stu-id="1943b-114">Do we check it again?</span></span> <span data-ttu-id="1943b-115">Lub najkorzystniej... nie bother do sprawdzenia i "Mam nadzieję, że masz nadzieję, że ktoś bothered go przed wysłaniem do Ciebie.</span><span class="sxs-lookup"><span data-stu-id="1943b-115">Or more likely ... you just don't bother to check and "hope for the best"—you hope that someone bothered to validate it before sending it to you.</span></span> <span data-ttu-id="1943b-116">Oczywiście przy użyciu usługi TDD jednym z pierwszych testów, które powinny być napisane, jest to, że jeśli wysyłam klientowi nazwę o wartości null, która powinna zgłosić błąd.</span><span class="sxs-lookup"><span data-stu-id="1943b-116">Of course, using TDD one of the first tests we should be writing is that if I send a customer with a null name that it should raise an error.</span></span> <span data-ttu-id="1943b-117">Jednak po rozpoczęciu pisania tych rodzajów testów w tym czasie zostanie to zrealizowane... "Zaczekaj, jeśli nigdy nie zezwolisz na przełączenie nazwy do wartości null, nie będziemy mieć wszystkich tych testów"</span><span class="sxs-lookup"><span data-stu-id="1943b-117">But once we start writing these kinds of tests over and over again we realize ... "wait if we never allowed name to become null we wouldn't have all of these tests"</span></span>

## <a name="implement-validations-in-the-domain-model-layer"></a><span data-ttu-id="1943b-118">Implementowanie walidacji w warstwie modelu domeny</span><span class="sxs-lookup"><span data-stu-id="1943b-118">Implement validations in the domain model layer</span></span>

<span data-ttu-id="1943b-119">Walidacje są zwykle implementowane w konstruktorach jednostek domeny lub w metodach, które mogą aktualizować jednostkę.</span><span class="sxs-lookup"><span data-stu-id="1943b-119">Validations are usually implemented in domain entity constructors or in methods that can update the entity.</span></span> <span data-ttu-id="1943b-120">Istnieje wiele sposobów implementacji walidacji, takich jak Weryfikowanie danych i wywoływanie wyjątków, jeśli sprawdzanie poprawności zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="1943b-120">There are multiple ways to implement validations, such as verifying data and raising exceptions if the validation fails.</span></span> <span data-ttu-id="1943b-121">Istnieją także bardziej zaawansowane wzorce, takie jak użycie wzorca specyfikacji dla walidacji, oraz wzorzec powiadomienia do zwrócenia kolekcji błędów zamiast zwracać wyjątek dla każdej walidacji w miarę ich występowania.</span><span class="sxs-lookup"><span data-stu-id="1943b-121">There are also more advanced patterns such as using the Specification pattern for validations, and the Notification pattern to return a collection of errors instead of returning an exception for each validation as it occurs.</span></span>

### <a name="validate-conditions-and-throw-exceptions"></a><span data-ttu-id="1943b-122">Sprawdzanie poprawności warunków i zgłaszanie wyjątków</span><span class="sxs-lookup"><span data-stu-id="1943b-122">Validate conditions and throw exceptions</span></span>

<span data-ttu-id="1943b-123">Poniższy przykład kodu pokazuje najprostszą metodę weryfikacji w jednostce domeny przez podnoszenie wyjątku.</span><span class="sxs-lookup"><span data-stu-id="1943b-123">The following code example shows the simplest approach to validation in a domain entity by raising an exception.</span></span> <span data-ttu-id="1943b-124">W tabeli odwołań na końcu tej sekcji można zobaczyć linki do bardziej zaawansowanych implementacji na podstawie wzorców, które zostały wcześniej omówione.</span><span class="sxs-lookup"><span data-stu-id="1943b-124">In the references table at the end of this section you can see links to more advanced implementations based on the patterns we have discussed previously.</span></span>

```csharp
public void SetAddress(Address address)
{
    _shippingAddress = address?? throw new ArgumentNullException(nameof(address));
}
```

<span data-ttu-id="1943b-125">Lepszy przykład pokazuje konieczność zapewnienia, że stan wewnętrzny nie został zmieniony lub że wszystkie mutacje dla metody wystąpią.</span><span class="sxs-lookup"><span data-stu-id="1943b-125">A better example would demonstrate the need to ensure that either the internal state did not change, or that all the mutations for a method occurred.</span></span> <span data-ttu-id="1943b-126">Na przykład następująca implementacja pozostawia obiekt w nieprawidłowym stanie:</span><span class="sxs-lookup"><span data-stu-id="1943b-126">For example, the following implementation would leave the object in an invalid state:</span></span>

```csharp
public void SetAddress(string line1, string line2,
    string city, string state, int zip)
{
    _shippingAddress.line1 = line1 ?? throw new ...
    _shippingAddress.line2 = line2;
    _shippingAddress.city = city ?? throw new ...
    _shippingAddress.state = (IsValid(state) ? state : throw new …);
}
```

<span data-ttu-id="1943b-127">Jeśli wartość stanu jest nieprawidłowa, pierwszy wiersz adresu i miasto zostały już zmienione.</span><span class="sxs-lookup"><span data-stu-id="1943b-127">If the value of the state is invalid, the first address line and the city have already been changed.</span></span> <span data-ttu-id="1943b-128">Może to oznaczać, że adres jest nieprawidłowy.</span><span class="sxs-lookup"><span data-stu-id="1943b-128">That might make the address invalid.</span></span>

<span data-ttu-id="1943b-129">Podobne podejście można użyć w konstruktorze jednostki, wywołując wyjątek, aby upewnić się, że jednostka jest ważna po utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="1943b-129">A similar approach can be used in the entity’s constructor, raising an exception to make sure that the entity is valid once it is created.</span></span>

### <a name="use-validation-attributes-in-the-model-based-on-data-annotations"></a><span data-ttu-id="1943b-130">Używanie atrybutów walidacji w modelu na podstawie adnotacji danych</span><span class="sxs-lookup"><span data-stu-id="1943b-130">Use validation attributes in the model based on data annotations</span></span>

<span data-ttu-id="1943b-131">Adnotacje danych, takie jak atrybuty wymagane lub MaxLength, mogą służyć do konfigurowania właściwości pola EF Core bazy danych, jak wyjaśniono szczegółowo w sekcji [Mapowanie tabeli](infrastructure-persistence-layer-implemenation-entity-framework-core.md#table-mapping) , ale [nie będą już działać do sprawdzania poprawności jednostek w EF Core](https://github.com/aspnet/EntityFrameworkCore/issues/3680) (nie są one <xref:System.ComponentModel.DataAnnotations.IValidatableObject.Validate%2A?displayProperty=nameWithType> metody), jak to zrobiono od Ef 4. x w .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="1943b-131">Data annotations, like the Required or MaxLength attributes, can be used to configure EF Core database field properties, as explained in detail in the [Table mapping](infrastructure-persistence-layer-implemenation-entity-framework-core.md#table-mapping) section, but [they no longer work for entity validation in EF Core](https://github.com/aspnet/EntityFrameworkCore/issues/3680) (neither does the <xref:System.ComponentModel.DataAnnotations.IValidatableObject.Validate%2A?displayProperty=nameWithType> method), as they have done since EF 4.x in .NET Framework.</span></span>

<span data-ttu-id="1943b-132">Adnotacje danych i <xref:System.ComponentModel.DataAnnotations.IValidatableObject> interfejs nadal mogą być używane na potrzeby walidacji modelu podczas powiązania modelu przed wywoływaniem akcji kontrolera w zwykły sposób, ale ten model jest przeznaczony dla ViewModel lub DTO, a to nie dotyczy modelu MVC lub interfejsu API. szczególne.</span><span class="sxs-lookup"><span data-stu-id="1943b-132">Data annotations and the <xref:System.ComponentModel.DataAnnotations.IValidatableObject> interface can still be used for model validation during model binding, prior to the controller’s actions invocation as usual, but that model is meant to be a ViewModel or DTO and that’s an MVC or API concern not a domain model concern.</span></span>

<span data-ttu-id="1943b-133">Po wyczyszczeniu różnicy pojęciowej można nadal używać adnotacji danych i `IValidatableObject` w klasie jednostki do walidacji, jeśli akcje odbierają parametr obiektu klasy jednostki, co nie jest zalecane.</span><span class="sxs-lookup"><span data-stu-id="1943b-133">Having made the conceptual difference clear, you can still use data annotations and `IValidatableObject` in the entity class for validation, if your actions receive an entity class object parameter, which is not recommended.</span></span> <span data-ttu-id="1943b-134">W takim przypadku Walidacja zostanie wykonana po powiązaniu modelu przed wywołaniem akcji i można sprawdzić Właściwość ModelState. IsValid kontrolera, aby sprawdzić wynik, ale następnie ponownie, dzieje się w kontrolerze, a nie przed utrwalaniem obiektu Entity w DbContext, jak zrobiono od EF 4. x.</span><span class="sxs-lookup"><span data-stu-id="1943b-134">In that case, validation will occur upon model binding, just before invoking the action and you can check the controller’s ModelState.IsValid property to check the result, but then again, it happens in the controller, not before persisting the entity object in the DbContext, as it had done since EF 4.x.</span></span>

<span data-ttu-id="1943b-135">Nadal można zaimplementować niestandardowe sprawdzanie poprawności w klasie Entity przy użyciu adnotacji danych i `IValidatableObject.Validate` metody, zastępując metodę metody SaveChanges DbContext.</span><span class="sxs-lookup"><span data-stu-id="1943b-135">You can still implement custom validation in the entity class using data annotations and the `IValidatableObject.Validate` method, by overriding the DbContext’s SaveChanges method.</span></span>

<span data-ttu-id="1943b-136">W witrynie GitHub można zobaczyć przykładową implementację sprawdzania poprawności `IValidatableObject` jednostek w [tym komentarzu](https://github.com/aspnet/EntityFrameworkCore/issues/3680#issuecomment-155502539).</span><span class="sxs-lookup"><span data-stu-id="1943b-136">You can see a sample implementation for validating `IValidatableObject` entities in [this comment on GitHub](https://github.com/aspnet/EntityFrameworkCore/issues/3680#issuecomment-155502539).</span></span> <span data-ttu-id="1943b-137">Ten przykład nie wykonuje walidacji opartych na atrybutach, ale powinien być łatwy do wdrożenia przy użyciu odbicia w tym samym przesłonięciu.</span><span class="sxs-lookup"><span data-stu-id="1943b-137">That sample doesn’t do attribute-based validations, but they should be easy to implement using reflection in the same override.</span></span>

<span data-ttu-id="1943b-138">Jednak z punktu widzenia, model domeny najlepiej utrzymuje się oszczędne przy użyciu wyjątków w metodach zachowań jednostki lub implementując wzorce specyfikacji i powiadomień w celu wymuszenia reguł walidacji.</span><span class="sxs-lookup"><span data-stu-id="1943b-138">However, from a DDD point of view, the domain model is best kept lean with the use of exceptions in your entity’s behavior methods, or by implementing the Specification and Notification patterns to enforce validation rules.</span></span>

<span data-ttu-id="1943b-139">Warto mieć sens, aby użyć adnotacji danych w warstwie aplikacji w klasach ViewModel (zamiast jednostek domeny), które będą akceptować dane wejściowe, aby umożliwić weryfikację modelu w warstwie interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1943b-139">It can make sense to use data annotations at the application layer in ViewModel classes (instead of domain entities) that will accept input, to allow for model validation within the UI layer.</span></span> <span data-ttu-id="1943b-140">Jednak nie należy tego robić podczas wykluczania walidacji w modelu domeny.</span><span class="sxs-lookup"><span data-stu-id="1943b-140">However, this should not be done at the exclusion of validation within the domain model.</span></span>

### <a name="validate-entities-by-implementing-the-specification-pattern-and-the-notification-pattern"></a><span data-ttu-id="1943b-141">Weryfikuj jednostki przez implementację wzorca specyfikacji i wzorzec powiadomienia</span><span class="sxs-lookup"><span data-stu-id="1943b-141">Validate entities by implementing the Specification pattern and the Notification pattern</span></span>

<span data-ttu-id="1943b-142">Na koniec bardziej rozbudowane podejście do implementowania walidacji w modelu domeny jest przez implementację wzorca specyfikacji w połączeniu ze wzorcem powiadomienia, jak wyjaśniono w niektórych dodatkowych zasobach wymienionych w dalszej części.</span><span class="sxs-lookup"><span data-stu-id="1943b-142">Finally, a more elaborate approach to implementing validations in the domain model is by implementing the Specification pattern in conjunction with the Notification pattern, as explained in some of the additional resources listed later.</span></span>

<span data-ttu-id="1943b-143">Warto zauważyć, że można również użyć tylko jednego z tych wzorców — na przykład walidacji ręcznie przy użyciu instrukcji kontroli, ale przy użyciu wzorca powiadomienia, aby układać i zwracać listę błędów walidacji.</span><span class="sxs-lookup"><span data-stu-id="1943b-143">It is worth mentioning that you can also use just one of those patterns—for example, validating manually with control statements, but using the Notification pattern to stack and return a list of validation errors.</span></span>

### <a name="use-deferred-validation-in-the-domain"></a><span data-ttu-id="1943b-144">Korzystanie z odroczonego sprawdzania poprawności w domenie</span><span class="sxs-lookup"><span data-stu-id="1943b-144">Use deferred validation in the domain</span></span>

<span data-ttu-id="1943b-145">Istnieją różne podejścia do postępowania z odroczonymi walidacjami w domenie.</span><span class="sxs-lookup"><span data-stu-id="1943b-145">There are various approaches to deal with deferred validations in the domain.</span></span> <span data-ttu-id="1943b-146">W swojej książce [implementującej Projektowanie oparte na domenie](https://www.amazon.com/Implementing-Domain-Driven-Design-Vaughn-Vernon/dp/0321834577)Vaughn Vernon omawia te w sekcji dotyczącej weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="1943b-146">In his book [Implementing Domain-Driven Design](https://www.amazon.com/Implementing-Domain-Driven-Design-Vaughn-Vernon/dp/0321834577), Vaughn Vernon discusses these in the section on validation.</span></span>

### <a name="two-step-validation"></a><span data-ttu-id="1943b-147">Weryfikacja dwuetapowa</span><span class="sxs-lookup"><span data-stu-id="1943b-147">Two-step validation</span></span>

<span data-ttu-id="1943b-148">Należy również rozważyć weryfikację dwuetapową.</span><span class="sxs-lookup"><span data-stu-id="1943b-148">Also consider two-step validation.</span></span> <span data-ttu-id="1943b-149">Przy użyciu walidacji na poziomie pola Transfer danych obiektów (DTO) i walidacji na poziomie domeny wewnątrz jednostek.</span><span class="sxs-lookup"><span data-stu-id="1943b-149">Use field-level validation on your command Data Transfer Objects (DTOs) and domain-level validation inside your entities.</span></span> <span data-ttu-id="1943b-150">Można to zrobić, zwracając obiekt wyniku zamiast wyjątków, aby ułatwić rozproszenie z błędami walidacji.</span><span class="sxs-lookup"><span data-stu-id="1943b-150">You can do this by returning a result object instead of exceptions in order to make it easier to deal with the validation errors.</span></span>

<span data-ttu-id="1943b-151">Używanie weryfikacji pola z adnotacjami danych, na przykład, nie duplikuje definicji walidacji.</span><span class="sxs-lookup"><span data-stu-id="1943b-151">Using field validation with data annotations, for example, you do not duplicate the validation definition.</span></span> <span data-ttu-id="1943b-152">Wykonanie, chociaż, może być zarówno po stronie serwera, jak i po stronie klienta w przypadku DTO (polecenia i modele widoków, na przykład).</span><span class="sxs-lookup"><span data-stu-id="1943b-152">The execution, though, can be both server-side and client-side in the case of DTOs (commands and ViewModels, for instance).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1943b-153">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="1943b-153">Additional resources</span></span>

- <span data-ttu-id="1943b-154">**Rachel Appel. Wprowadzenie do walidacji modelu w ASP.NET Core MVC** </span><span class="sxs-lookup"><span data-stu-id="1943b-154">**Rachel Appel. Introduction to model validation in ASP.NET Core MVC** </span></span>\
  <https://docs.microsoft.com/aspnet/core/mvc/models/validation>

- <span data-ttu-id="1943b-155">**Rick Anderson. Dodawanie walidacji** </span><span class="sxs-lookup"><span data-stu-id="1943b-155">**Rick Anderson. Adding validation** </span></span>\
  <https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/validation>

- <span data-ttu-id="1943b-156">**Fowlera Martin. Zastępowanie zgłaszania wyjątków przy użyciu powiadomień w walidacji** </span><span class="sxs-lookup"><span data-stu-id="1943b-156">**Martin Fowler. Replacing Throwing Exceptions with Notification in Validations** </span></span>\
  <https://martinfowler.com/articles/replaceThrowWithNotification.html>

- <span data-ttu-id="1943b-157">**Wzorce specyfikacji i powiadomień** </span><span class="sxs-lookup"><span data-stu-id="1943b-157">**Specification and Notification Patterns** </span></span>\
  <https://www.codeproject.com/Tips/790758/Specification-and-Notification-Patterns>

- <span data-ttu-id="1943b-158">**Lew Gorodinski. Walidacja w projekcie opartym na domenie (DDD)**  </span><span class="sxs-lookup"><span data-stu-id="1943b-158">**Lev Gorodinski. Validation in Domain-Driven Design (DDD)** </span></span>\
  <http://gorodinski.com/blog/2012/05/19/validation-in-domain-driven-design-ddd/>

- <span data-ttu-id="1943b-159">**Wtyczka Colin. Walidacja modelu domeny** </span><span class="sxs-lookup"><span data-stu-id="1943b-159">**Colin Jack. Domain Model Validation** </span></span>\
  <https://colinjack.blogspot.com/2008/03/domain-model-validation.html>

- <span data-ttu-id="1943b-160">**Jimmy Bogard. Walidacja w DDD** </span><span class="sxs-lookup"><span data-stu-id="1943b-160">**Jimmy Bogard. Validation in a DDD world** </span></span>\
  <https://lostechies.com/jimmybogard/2009/02/15/validation-in-a-ddd-world/>

> [!div class="step-by-step"]
> <span data-ttu-id="1943b-161">[Poprzedni](enumeration-classes-over-enum-types.md)Następny
> [](client-side-validation.md)</span><span class="sxs-lookup"><span data-stu-id="1943b-161">[Previous](enumeration-classes-over-enum-types.md)
[Next](client-side-validation.md)</span></span>