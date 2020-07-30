---
title: 'Przewodnik: utrwalanie obiektu przy użyciu języka C #'
description: W tym przykładzie tworzony jest podstawowy obiekt pożyczek w języku C# i utrwalał dane w pliku, a następnie tworzony jest nowy obiekt z danymi z pliku.
ms.date: 04/26/2018
ms.openlocfilehash: 9f165addc5b9b0d056936458e8529ec1912c417b
ms.sourcegitcommit: 6f58a5f75ceeb936f8ee5b786e9adb81a9a3bee9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/28/2020
ms.locfileid: "87302766"
---
# <a name="walkthrough-persisting-an-object-using-c"></a><span data-ttu-id="04798-103">Przewodnik: utrwalanie obiektu przy użyciu języka C\#</span><span class="sxs-lookup"><span data-stu-id="04798-103">Walkthrough: persisting an object using C\#</span></span>

<span data-ttu-id="04798-104">Możesz użyć serializacji, aby zachować dane obiektu między wystąpieniami, co umożliwia przechowywanie wartości i pobieranie ich przy następnym utworzeniu wystąpienia obiektu.</span><span class="sxs-lookup"><span data-stu-id="04798-104">You can use serialization to persist an object's data between instances, which enables you to store values and retrieve them the next time that the object is instantiated.</span></span>

<span data-ttu-id="04798-105">W tym instruktażu utworzysz `Loan` obiekt podstawowy i zachowasz jego dane do pliku.</span><span class="sxs-lookup"><span data-stu-id="04798-105">In this walkthrough, you will create a basic `Loan` object and persist its data to a file.</span></span> <span data-ttu-id="04798-106">Następnie dane zostaną pobrane z pliku po ponownym utworzeniu obiektu.</span><span class="sxs-lookup"><span data-stu-id="04798-106">You will then retrieve the data from the file when you re-create the object.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="04798-107">Ten przykład tworzy nowy plik, jeśli plik jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="04798-107">This example creates a new file if the file does not already exist.</span></span> <span data-ttu-id="04798-108">Jeśli aplikacja musi utworzyć plik, aplikacja musi mieć `Create` uprawnienie do tego folderu.</span><span class="sxs-lookup"><span data-stu-id="04798-108">If an application must create a file, that application must have `Create` permission for the folder.</span></span> <span data-ttu-id="04798-109">Uprawnienia są ustawiane przy użyciu list kontroli dostępu.</span><span class="sxs-lookup"><span data-stu-id="04798-109">Permissions are set by using access control lists.</span></span> <span data-ttu-id="04798-110">Jeśli plik już istnieje, aplikacja wymaga tylko `Write` uprawnień, ale jest to małe uprawnienie.</span><span class="sxs-lookup"><span data-stu-id="04798-110">If the file already exists, the application needs only `Write` permission, a lesser permission.</span></span> <span data-ttu-id="04798-111">Jeśli to możliwe, bezpieczniejsze jest tworzenie plików podczas wdrażania i udzielanie `Read` uprawnień tylko jednemu plikowi (zamiast tworzenia uprawnień dla folderu).</span><span class="sxs-lookup"><span data-stu-id="04798-111">Where possible, it's more secure to create the file during deployment and only grant `Read` permissions to a single file (instead of Create permissions for a folder).</span></span> <span data-ttu-id="04798-112">Ponadto bardziej bezpieczne jest zapisanie danych do folderów użytkowników niż folder główny lub folder Program Files.</span><span class="sxs-lookup"><span data-stu-id="04798-112">Also, it's more secure to write data to user folders than to the root folder or the Program Files folder.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="04798-113">Ten przykład zapisuje dane w pliku formatu binarnego.</span><span class="sxs-lookup"><span data-stu-id="04798-113">This example stores data in a binary format file.</span></span> <span data-ttu-id="04798-114">Tych formatów nie należy używać w przypadku poufnych danych, takich jak hasła lub informacje o kartach kredytowych.</span><span class="sxs-lookup"><span data-stu-id="04798-114">These formats should not be used for sensitive data, such as passwords or credit-card information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="04798-115">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="04798-115">Prerequisites</span></span>

- <span data-ttu-id="04798-116">Aby skompilować i uruchomić, zainstaluj [zestaw .NET Core SDK](https://dotnet.microsoft.com/download).</span><span class="sxs-lookup"><span data-stu-id="04798-116">To build and run, install the [.NET Core SDK](https://dotnet.microsoft.com/download).</span></span>

- <span data-ttu-id="04798-117">Zainstaluj swój ulubiony Edytor kodu, jeśli jeszcze tego nie zrobiono.</span><span class="sxs-lookup"><span data-stu-id="04798-117">Install your favorite code editor, if you haven't already.</span></span>

> [!TIP]
> <span data-ttu-id="04798-118">Musisz zainstalować Edytor kodu?</span><span class="sxs-lookup"><span data-stu-id="04798-118">Need to install a code editor?</span></span> <span data-ttu-id="04798-119">Wypróbuj [program Visual Studio](https://visualstudio.com/downloads)!</span><span class="sxs-lookup"><span data-stu-id="04798-119">Try [Visual Studio](https://visualstudio.com/downloads)!</span></span>

- <span data-ttu-id="04798-120">Przykład wymaga języka C# 7,3.</span><span class="sxs-lookup"><span data-stu-id="04798-120">The example requires C# 7.3.</span></span> <span data-ttu-id="04798-121">Zobacz [Wybieranie wersji języka C#](../../../language-reference/configure-language-version.md)</span><span class="sxs-lookup"><span data-stu-id="04798-121">See [Select the C# language version](../../../language-reference/configure-language-version.md)</span></span>

<span data-ttu-id="04798-122">Przykładowy kod można przeanalizować w trybie online [w repozytorium usługi GitHub dla platformy .NET](https://github.com/dotnet/samples/tree/master/csharp/serialization).</span><span class="sxs-lookup"><span data-stu-id="04798-122">You can examine the sample code online [at the .NET samples GitHub repository](https://github.com/dotnet/samples/tree/master/csharp/serialization).</span></span>

## <a name="creating-the-loan-object"></a><span data-ttu-id="04798-123">Tworzenie obiektu pożyczek</span><span class="sxs-lookup"><span data-stu-id="04798-123">Creating the loan object</span></span>

<span data-ttu-id="04798-124">Pierwszym krokiem jest utworzenie `Loan` klasy i aplikacji konsolowej, która używa klasy:</span><span class="sxs-lookup"><span data-stu-id="04798-124">The first step is to create a `Loan` class and a console application that uses the class:</span></span>

1. <span data-ttu-id="04798-125">Utwórz nową aplikację.</span><span class="sxs-lookup"><span data-stu-id="04798-125">Create a new application.</span></span> <span data-ttu-id="04798-126">Wpisz, `dotnet new console -o serialization` Aby utworzyć nową aplikację konsolową w podkatalogu o nazwie `serialization` .</span><span class="sxs-lookup"><span data-stu-id="04798-126">Type `dotnet new console -o serialization` to create a new console application in a subdirectory named `serialization`.</span></span>
1. <span data-ttu-id="04798-127">Otwórz aplikację w edytorze i Dodaj nową klasę o nazwie `Loan.cs` .</span><span class="sxs-lookup"><span data-stu-id="04798-127">Open the application in your editor, and add a new class named `Loan.cs`.</span></span>
1. <span data-ttu-id="04798-128">Dodaj następujący kod do `Loan` klasy:</span><span class="sxs-lookup"><span data-stu-id="04798-128">Add the following code to your `Loan` class:</span></span>

[!code-csharp[Loan class definition](../../../../../samples/snippets/csharp/serialization/Loan.cs#1)]

<span data-ttu-id="04798-129">Należy również utworzyć aplikację, która używa `Loan` klasy.</span><span class="sxs-lookup"><span data-stu-id="04798-129">You will also have to create an application that uses the `Loan` class.</span></span>

## <a name="serialize-the-loan-object"></a><span data-ttu-id="04798-130">Serializacja obiektu pożyczek</span><span class="sxs-lookup"><span data-stu-id="04798-130">Serialize the loan object</span></span>

1. <span data-ttu-id="04798-131">Otwórz plik `Program.cs`.</span><span class="sxs-lookup"><span data-stu-id="04798-131">Open `Program.cs`.</span></span> <span data-ttu-id="04798-132">Dodaj następujący kod:</span><span class="sxs-lookup"><span data-stu-id="04798-132">Add the following code:</span></span>

[!code-csharp[Create a loan object](../../../../../samples/snippets/csharp/serialization/Program.cs#1)]

<span data-ttu-id="04798-133">Dodaj program obsługi zdarzeń dla `PropertyChanged` zdarzenia, a kilka wierszy, aby zmodyfikować `Loan` obiekt i wyświetlić zmiany.</span><span class="sxs-lookup"><span data-stu-id="04798-133">Add an event handler for the `PropertyChanged` event, and a few lines to modify the `Loan` object and display the changes.</span></span> <span data-ttu-id="04798-134">Można zobaczyć dodatki w następującym kodzie:</span><span class="sxs-lookup"><span data-stu-id="04798-134">You can see the additions in the following code:</span></span>

[!code-csharp[Listening for the PropertyChanged event](../../../../../samples/snippets/csharp/serialization/Program.cs#2)]

<span data-ttu-id="04798-135">W tym momencie można uruchomić kod i wyświetlić bieżące dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="04798-135">At this point, you can run the code, and see the current output:</span></span>

```console
New customer value: Henry Clay
7.5
7.1
```

<span data-ttu-id="04798-136">Aplikacja wielokrotnie uruchamiana zawsze zapisuje te same wartości.</span><span class="sxs-lookup"><span data-stu-id="04798-136">Running this application repeatedly always writes the same values.</span></span> <span data-ttu-id="04798-137">Nowy obiekt pożyczek jest tworzony za każdym razem, gdy uruchamiasz program.</span><span class="sxs-lookup"><span data-stu-id="04798-137">A new Loan object is created every time you run the program.</span></span> <span data-ttu-id="04798-138">W świecie rzeczywistym stawki odsetek zmieniają się okresowo, ale nie zawsze, gdy aplikacja jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="04798-138">In the real world, interest rates change periodically, but not necessarily every time that the application is run.</span></span> <span data-ttu-id="04798-139">Kod serializacji oznacza zachowywanie najnowszej stopy odsetek między wystąpieniami aplikacji.</span><span class="sxs-lookup"><span data-stu-id="04798-139">Serialization code means you preserve the most recent interest rate between instances of the application.</span></span> <span data-ttu-id="04798-140">W następnym kroku wystarczy dodać serializację do klasy pożyczek.</span><span class="sxs-lookup"><span data-stu-id="04798-140">In the next step, you will do just that by adding serialization to the Loan class.</span></span>

## <a name="using-serialization-to-persist-the-object"></a><span data-ttu-id="04798-141">Utrwalanie obiektu przy użyciu serializacji</span><span class="sxs-lookup"><span data-stu-id="04798-141">Using Serialization to Persist the Object</span></span>

<span data-ttu-id="04798-142">Aby zachować wartości dla klasy pożyczek, należy najpierw oznaczyć klasę `Serializable` atrybutem.</span><span class="sxs-lookup"><span data-stu-id="04798-142">In order to persist the values for the Loan class, you must first mark the class with the `Serializable` attribute.</span></span> <span data-ttu-id="04798-143">Dodaj następujący kod powyżej definicji klasy pożyczek:</span><span class="sxs-lookup"><span data-stu-id="04798-143">Add the following code above the Loan class definition:</span></span>

[!code-csharp[Loan class definition](../../../../../samples/snippets/csharp/serialization/Loan.cs#2)]

<span data-ttu-id="04798-144"><xref:System.SerializableAttribute>Informuje kompilator, że wszystko w klasie może być utrwalone w pliku.</span><span class="sxs-lookup"><span data-stu-id="04798-144">The <xref:System.SerializableAttribute> tells the compiler that everything in the class can be persisted to a file.</span></span> <span data-ttu-id="04798-145">Ponieważ `PropertyChanged` zdarzenie nie reprezentuje części grafu obiektów, która powinna być przechowywana, nie powinno być serializowane.</span><span class="sxs-lookup"><span data-stu-id="04798-145">Because the `PropertyChanged` event does not represent part of the object graph that should be stored, it should not be serialized.</span></span> <span data-ttu-id="04798-146">Dzięki temu można serializować wszystkie obiekty, które są dołączone do tego zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="04798-146">Doing so would serialize all objects that are attached to that event.</span></span> <span data-ttu-id="04798-147">Można dodać <xref:System.NonSerializedAttribute> do deklaracji pola dla `PropertyChanged` programu obsługi zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="04798-147">You can add the <xref:System.NonSerializedAttribute> to the field declaration for the `PropertyChanged` event handler.</span></span>

[!code-csharp[Disable serialization for the event handler](../../../../../samples/snippets/csharp/serialization/Loan.cs#3)]

<span data-ttu-id="04798-148">Począwszy od języka C# 7,3, można dołączyć atrybuty do pola zapasowego właściwości automatycznie zaimplementowane przy użyciu `field` wartości docelowej.</span><span class="sxs-lookup"><span data-stu-id="04798-148">Beginning with C# 7.3, you can attach attributes to the backing field of an auto-implemented property using the `field` target value.</span></span> <span data-ttu-id="04798-149">Poniższy kod dodaje `TimeLastLoaded` Właściwość i oznacza ją jako niemożliwy do serializacji:</span><span class="sxs-lookup"><span data-stu-id="04798-149">The following code adds a `TimeLastLoaded` property and marks it as not serializable:</span></span>

[!code-csharp[Disable serialization for an auto-implemented property](../../../../../samples/snippets/csharp/serialization/Loan.cs#4)]

<span data-ttu-id="04798-150">Następnym krokiem jest dodanie kodu serializacji do aplikacji LoanApp.</span><span class="sxs-lookup"><span data-stu-id="04798-150">The next step is to add the serialization code to the LoanApp application.</span></span> <span data-ttu-id="04798-151">Aby serializować klasę i zapisać ją w pliku, należy użyć <xref:System.IO> <xref:System.Runtime.Serialization.Formatters.Binary> przestrzeni nazw i.</span><span class="sxs-lookup"><span data-stu-id="04798-151">In order to serialize the class and write it to a file, you use the <xref:System.IO> and <xref:System.Runtime.Serialization.Formatters.Binary> namespaces.</span></span> <span data-ttu-id="04798-152">Aby uniknąć wpisywania w pełni kwalifikowanych nazw, można dodać odwołania do niezbędnych przestrzeni nazw, jak pokazano w poniższym kodzie:</span><span class="sxs-lookup"><span data-stu-id="04798-152">To avoid typing the fully qualified names, you can add references to the necessary namespaces as shown in the following code:</span></span>

[!code-csharp[Adding namespaces for serialization](../../../../../samples/snippets/csharp/serialization/Program.cs#3)]

<span data-ttu-id="04798-153">Następnym krokiem jest dodanie kodu w celu deserializacji obiektu z pliku po utworzeniu obiektu.</span><span class="sxs-lookup"><span data-stu-id="04798-153">The next step is to add code to deserialize the object from the file when the object is created.</span></span> <span data-ttu-id="04798-154">Dodaj stałą do klasy dla nazwy pliku serializowanej danych, jak pokazano w poniższym kodzie:</span><span class="sxs-lookup"><span data-stu-id="04798-154">Add a constant to the class for the serialized data's file name as shown in the following code:</span></span>

[!code-csharp[Define the name of the saved file](../../../../../samples/snippets/csharp/serialization/Program.cs#4)]

<span data-ttu-id="04798-155">Następnie Dodaj następujący kod po wierszu, który tworzy `TestLoan` obiekt:</span><span class="sxs-lookup"><span data-stu-id="04798-155">Next, add the following code after the line that creates the `TestLoan` object:</span></span>

[!code-csharp[Read from a file if it exists](../../../../../samples/snippets/csharp/serialization/Program.cs#5)]

<span data-ttu-id="04798-156">Najpierw należy sprawdzić, czy plik istnieje.</span><span class="sxs-lookup"><span data-stu-id="04798-156">You first must check that the file exists.</span></span> <span data-ttu-id="04798-157">Jeśli istnieje, Utwórz klasę, <xref:System.IO.Stream> Aby odczytać plik binarny i klasę, <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> Aby przetłumaczyć plik.</span><span class="sxs-lookup"><span data-stu-id="04798-157">If it exists, create a <xref:System.IO.Stream> class to read the binary file and a <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> class to translate the file.</span></span> <span data-ttu-id="04798-158">Należy również przekonwertować typ strumienia na typ obiektu pożyczki.</span><span class="sxs-lookup"><span data-stu-id="04798-158">You also need to convert from the stream type to the Loan object type.</span></span>

<span data-ttu-id="04798-159">Następnie musisz dodać kod, aby serializować klasę do pliku.</span><span class="sxs-lookup"><span data-stu-id="04798-159">Next you must add code to serialize the class to a file.</span></span> <span data-ttu-id="04798-160">Dodaj następujący kod po istniejącym kodzie w `Main` metodzie:</span><span class="sxs-lookup"><span data-stu-id="04798-160">Add the following code after the existing code in the `Main` method:</span></span>

[!code-csharp[Save the existing Loan object](../../../../../samples/snippets/csharp/serialization/Program.cs#6)]

<span data-ttu-id="04798-161">W tym momencie możesz ponownie skompilować i uruchomić aplikację.</span><span class="sxs-lookup"><span data-stu-id="04798-161">At this point, you can again build and run the application.</span></span> <span data-ttu-id="04798-162">Przy pierwszym uruchomieniu należy zauważyć, że stawki odsetek zaczynają się od 7,5, a następnie zmieniają się na 7,1.</span><span class="sxs-lookup"><span data-stu-id="04798-162">The first time it runs, notice that the interest rates starts at 7.5, and then changes to 7.1.</span></span> <span data-ttu-id="04798-163">Zamknij aplikację, a następnie uruchom ją ponownie.</span><span class="sxs-lookup"><span data-stu-id="04798-163">Close the application and then run it again.</span></span> <span data-ttu-id="04798-164">Teraz aplikacja drukuje wiadomość, która odczytała zapisany plik, a oprocentowanie to 7,1 nawet przed kodem, który go zmieni.</span><span class="sxs-lookup"><span data-stu-id="04798-164">Now, the application prints the message that it has read the saved file, and the interest rate is 7.1 even before the code that changes it.</span></span>

## <a name="see-also"></a><span data-ttu-id="04798-165">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="04798-165">See also</span></span>

- [<span data-ttu-id="04798-166">Serializacja (C#)</span><span class="sxs-lookup"><span data-stu-id="04798-166">Serialization (C#)</span></span>](index.md)
- [<span data-ttu-id="04798-167">Przewodnik programowania w języku C#</span><span class="sxs-lookup"><span data-stu-id="04798-167">C# Programming Guide</span></span>](../../index.md)
