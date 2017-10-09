---
title: "Azure Cosmos DB: rozpoczęcie pracy z interfejsem API usługi DocumentDB na platformie .NET Core — samouczek | Microsoft Docs"
description: "Samouczek, który powoduje utworzenie bazy danych w trybie online i aplikacji konsolowej C# za pomocą hello Azure rozwiązania Cosmos bazy danych DocumentDB interfejsu API platformy .NET Core SDK."
services: cosmos-db
documentationcenter: .net
author: arramac
manager: jhubbard
editor: 
ms.assetid: 9f93e276-9936-4efb-a534-a9889fa7c7d2
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/15/2017
ms.author: arramac
ms.openlocfilehash: 5e7efb327252e9e73e9b2a340820eeecc6937fa5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-getting-started-with-hello-documentdb-api-and-net-core"></a><span data-ttu-id="ca9d1-103">Azure rozwiązania Cosmos bazy danych: Wprowadzenie do korzystania z hello interfejsu API usługi DocumentDB i .NET Core</span><span class="sxs-lookup"><span data-stu-id="ca9d1-103">Azure Cosmos DB: Getting started with hello DocumentDB API and .NET Core</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ca9d1-104">.NET</span><span class="sxs-lookup"><span data-stu-id="ca9d1-104">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="ca9d1-105">.NET Core</span><span class="sxs-lookup"><span data-stu-id="ca9d1-105">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="ca9d1-106">Node.js dla MongoDB</span><span class="sxs-lookup"><span data-stu-id="ca9d1-106">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="ca9d1-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="ca9d1-107">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="ca9d1-108">Java</span><span class="sxs-lookup"><span data-stu-id="ca9d1-108">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="ca9d1-109">C++</span><span class="sxs-lookup"><span data-stu-id="ca9d1-109">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="ca9d1-110">Interfejs API usługi DocumentDB dla bazy danych rozwiązania Cosmos Azure Wprowadzenie — samouczek platformy .NET Core toohello Zapraszamy!</span><span class="sxs-lookup"><span data-stu-id="ca9d1-110">Welcome toohello DocumentDB API for Azure Cosmos DB getting started with .NET Core tutorial!</span></span> <span data-ttu-id="ca9d1-111">W ramach tego samouczka zostanie utworzona aplikacja konsolowa, która tworzy zasoby usługi Azure Cosmos DB i wykonuje dla nich zapytania.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-111">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="ca9d1-112">Omówione zostaną następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ca9d1-112">We'll cover:</span></span>

* <span data-ttu-id="ca9d1-113">Tworzenie i łączenie tooan konta bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="ca9d1-113">Creating and connecting tooan Azure Cosmos DB account</span></span>
* <span data-ttu-id="ca9d1-114">Konfigurowanie rozwiązania Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ca9d1-114">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="ca9d1-115">Tworzenie bazy danych w trybie online</span><span class="sxs-lookup"><span data-stu-id="ca9d1-115">Creating an online database</span></span>
* <span data-ttu-id="ca9d1-116">Tworzenie kolekcji</span><span class="sxs-lookup"><span data-stu-id="ca9d1-116">Creating a collection</span></span>
* <span data-ttu-id="ca9d1-117">Tworzenie dokumentów JSON</span><span class="sxs-lookup"><span data-stu-id="ca9d1-117">Creating JSON documents</span></span>
* <span data-ttu-id="ca9d1-118">Wykonywanie zapytania hello kolekcji</span><span class="sxs-lookup"><span data-stu-id="ca9d1-118">Querying hello collection</span></span>
* <span data-ttu-id="ca9d1-119">Zastępowanie dokumentu</span><span class="sxs-lookup"><span data-stu-id="ca9d1-119">Replacing a document</span></span>
* <span data-ttu-id="ca9d1-120">Usuwanie dokumentu</span><span class="sxs-lookup"><span data-stu-id="ca9d1-120">Deleting a document</span></span>
* <span data-ttu-id="ca9d1-121">Usunięcie hello bazy danych</span><span class="sxs-lookup"><span data-stu-id="ca9d1-121">Deleting hello database</span></span>

<span data-ttu-id="ca9d1-122">Nie masz czasu?</span><span class="sxs-lookup"><span data-stu-id="ca9d1-122">Don't have time?</span></span> <span data-ttu-id="ca9d1-123">Nie martw się!</span><span class="sxs-lookup"><span data-stu-id="ca9d1-123">Don't worry!</span></span> <span data-ttu-id="ca9d1-124">Witaj kompletne rozwiązanie jest dostępne na [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span><span class="sxs-lookup"><span data-stu-id="ca9d1-124">hello complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span></span> <span data-ttu-id="ca9d1-125">Przeskocz toohello [pobrać sekcji kompletnego rozwiązania hello](#GetSolution) Aby uzyskać krótkie instrukcje.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-125">Jump toohello [Get hello complete solution section](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="ca9d1-126">Mają toobuild Xamarin iOS, Android lub formularzy przy użyciu aplikacji hello interfejsu API usługi DocumentDB i .NET Core SDK?</span><span class="sxs-lookup"><span data-stu-id="ca9d1-126">Want toobuild a Xamarin iOS, Android, or Forms application using hello DocumentDB API and .NET Core SDK?</span></span> <span data-ttu-id="ca9d1-127">Zobacz [tworzenie aplikacji dla urządzeń przenośnych dzięki platformie Xamarin i usłudze Azure DB rozwiązania Cosmos](mobile-apps-with-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="ca9d1-127">See [Build mobile applications with Xamarin and Azure Cosmos DB](mobile-apps-with-xamarin.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ca9d1-128">Hello Azure rozwiązania Cosmos DB .NET Core SDK używany w tym samouczku nie jest jeszcze zgodne z aplikacjami systemu Windows platformy Uniwersalnej.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-128">hello Azure Cosmos DB .NET Core SDK used in this tutorial is not yet compatible with Universal Windows Platform (UWP) apps.</span></span> <span data-ttu-id="ca9d1-129">Dla wersji preview hello .NET Core SDK, który obsługuje aplikacje platformy uniwersalnej systemu Windows, Wyślij wiadomość e-mail zbyt[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="ca9d1-129">For a preview version of hello .NET Core SDK that does support UWP apps, send email too[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

<span data-ttu-id="ca9d1-130">Teraz do dzieła!</span><span class="sxs-lookup"><span data-stu-id="ca9d1-130">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ca9d1-131">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ca9d1-131">Prerequisites</span></span>
<span data-ttu-id="ca9d1-132">Upewnij się, że masz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="ca9d1-132">Please make sure you have hello following:</span></span>

* <span data-ttu-id="ca9d1-133">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-133">An active Azure account.</span></span> <span data-ttu-id="ca9d1-134">Jeśli go nie masz, możesz zarejestrować się w celu [utworzenia bezpłatnego konta](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="ca9d1-134">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="ca9d1-135">Alternatywnie można użyć hello [Azure rozwiązania Cosmos DB emulatora](local-emulator.md) w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-135">Alternatively, you can use hello [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* [<span data-ttu-id="ca9d1-136">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="ca9d1-136">Visual Studio 2017</span></span>](https://www.visualstudio.com/vs/) 
    * <span data-ttu-id="ca9d1-137">Jeśli pracujesz nad MacOS lub Linux, można tworzyć aplikacje .NET Core z wiersza polecenia hello instalując hello [.NET Core SDK](https://www.microsoft.com/net/core#macos) platformy hello wybranych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-137">If you're working on MacOS or Linux, you can develop .NET Core apps from hello command-line by installing hello [.NET Core SDK](https://www.microsoft.com/net/core#macos) for hello platform of your choice.</span></span> 
    * <span data-ttu-id="ca9d1-138">Podczas pracy w systemie Windows, instalując hello można tworzyć aplikacje .NET Core z wiersza polecenia hello [.NET Core SDK](https://www.microsoft.com/net/core#windows).</span><span class="sxs-lookup"><span data-stu-id="ca9d1-138">If you're working on Windows, you can develop .NET Core apps from hello command-line by installing hello [.NET Core SDK](https://www.microsoft.com/net/core#windows).</span></span> 
    * <span data-ttu-id="ca9d1-139">Możesz użyć własnego edytora lub pobrać bezpłatny program [Visual Studio Code](https://code.visualstudio.com/) działający na komputerach z systemem Windows, Linux i MacOS.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-139">You can use your own editor, or download [Visual Studio Code](https://code.visualstudio.com/) which is free and works on Windows, Linux, and MacOS.</span></span> 

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="ca9d1-140">Krok 1. Tworzenie konta usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ca9d1-140">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="ca9d1-141">Utwórzmy konto usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-141">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="ca9d1-142">Jeśli masz już konto ma toouse, możesz przejść od razu zbyt[konfigurowanie rozwiązania Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="ca9d1-142">If you already have an account you want toouse, you can skip ahead too[Setup your Visual Studio Solution](#SetupVS).</span></span> <span data-ttu-id="ca9d1-143">Jeśli używasz hello Azure rozwiązania Cosmos DB emulatora, należy wykonać czynności hello na [Azure rozwiązania Cosmos DB emulatora](local-emulator.md) toosetup hello emulatora i przejść od razu zbyt[konfigurowanie rozwiązania Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="ca9d1-143">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Setup your Visual Studio Solution](#SetupVS).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="ca9d1-144"><a id="SetupVS"></a>Krok 2. Konfigurowanie rozwiązania programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ca9d1-144"><a id="SetupVS"></a>Step 2: Setup your Visual Studio solution</span></span>
1. <span data-ttu-id="ca9d1-145">Otwórz program **Visual Studio 2017** na komputerze.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-145">Open **Visual Studio 2017** on your computer.</span></span>
2. <span data-ttu-id="ca9d1-146">Na powitania **pliku** menu, wybierz opcję **nowy**, a następnie wybierz pozycję **projektu**.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-146">On hello **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="ca9d1-147">W hello **nowy projekt** okno dialogowe, wybierz opcję **szablony** / **Visual C#** / **.NET Core** / **Aplikacji konsoli (.NET Core)**, nazwy projektu **DocumentDBGettingStarted**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-147">In hello **New Project** dialog, select **Templates** / **Visual C#** / **.NET Core**/**Console Application (.NET Core)**, name your project **DocumentDBGettingStarted**, and then click **OK**.</span></span>

   ![Zrzut ekranu okna nowy projekt hello](./media/documentdb-dotnetcore-get-started/nosql-tutorial-new-project-2.png)
4. <span data-ttu-id="ca9d1-149">W hello **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy **DocumentDBGettingStarted**.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-149">In hello **Solution Explorer**, right click on **DocumentDBGettingStarted**.</span></span>
5. <span data-ttu-id="ca9d1-150">Następnie bez opuszczania hello menu, kliknij przycisk **Zarządzaj pakietami NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="ca9d1-150">Then without leaving hello menu, click on **Manage NuGet Packages...**.</span></span>

   ![Zrzut ekranu przedstawiający hello prawo kliknięto element Menu hello projektu](./media/documentdb-dotnetcore-get-started/nosql-tutorial-manage-nuget-pacakges.png)
6. <span data-ttu-id="ca9d1-152">W hello **NuGet** , kliknij pozycję **Przeglądaj** u góry okna hello i typ hello **usługa azure documentdb** w polu wyszukiwania hello.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-152">In hello **NuGet** tab, click **Browse** at hello top of hello window, and type **azure documentdb** in hello search box.</span></span>
7. <span data-ttu-id="ca9d1-153">W wynikach hello znaleźć **Microsoft.Azure.DocumentDB.Core** i kliknij przycisk **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-153">Within hello results, find **Microsoft.Azure.DocumentDB.Core** and click **Install**.</span></span>
   <span data-ttu-id="ca9d1-154">Identyfikator pakietu Hello hello biblioteki klienta usługi DocumentDB dla platformy .NET Core jest [Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core).</span><span class="sxs-lookup"><span data-stu-id="ca9d1-154">hello package ID for hello DocumentDB Client Library for .NET Core is [Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core).</span></span> <span data-ttu-id="ca9d1-155">Jeśli elementem docelowym jest wersja programu .NET Framework (na przykład net461), która nie jest obsługiwana przez ten pakiet .NET Core NuGet, użyj elementu [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB) obsługującego wszystkie wersje programu .NET Framework, począwszy od wersji .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-155">If you are targeting a .NET Framework version (like net461) that is not supported by this .NET Core NuGet package, then use [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB) that supports all .NET Framework versions starting .NET Framework 4.5.</span></span>
8. <span data-ttu-id="ca9d1-156">Na monitach hello Zaakceptuj instalacji pakietu NuGet hello hello umowy licencyjnej.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-156">At hello prompts, accept hello NuGet package installations and hello license agreement.</span></span>

<span data-ttu-id="ca9d1-157">Wspaniale!</span><span class="sxs-lookup"><span data-stu-id="ca9d1-157">Great!</span></span> <span data-ttu-id="ca9d1-158">Teraz, gdy zakończeniu hello instalacji, Zacznijmy pisanie kodu.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-158">Now that we finished hello setup, let's start writing some code.</span></span> <span data-ttu-id="ca9d1-159">Ukończony projekt kodu z tego samouczka można znaleźć w witrynie [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span><span class="sxs-lookup"><span data-stu-id="ca9d1-159">You can find a completed code project of this tutorial at [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span></span>

## <span data-ttu-id="ca9d1-160"><a id="Connect"></a>Krok 3: Łączenie tooan konta bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="ca9d1-160"><a id="Connect"></a>Step 3: Connect tooan Azure Cosmos DB account</span></span>
<span data-ttu-id="ca9d1-161">Najpierw dodaj te odwołania toohello początku aplikacji C#, w pliku Program.cs hello:</span><span class="sxs-lookup"><span data-stu-id="ca9d1-161">First, add these references toohello beginning of your C# application, in hello Program.cs file:</span></span>

```csharp
using System;

// ADD THIS PART tooYOUR CODE
using System.Linq;
using System.Threading.Tasks;
using System.Net;
using Microsoft.Azure.Documents;
using Microsoft.Azure.Documents.Client;
using Newtonsoft.Json;
```

> [!IMPORTANT]
> <span data-ttu-id="ca9d1-162">W kolejności toocomplete tego samouczka, upewnij się, że dodano zależności hello powyżej.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-162">In order toocomplete this tutorial, make sure you add hello dependencies above.</span></span>

<span data-ttu-id="ca9d1-163">Dodaj teraz te dwie stałe i zmienną *client* poniżej klasy publicznej *Program*.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-163">Now, add these two constants and your *client* variable underneath your public class *Program*.</span></span>

```csharp
class Program
{
    // ADD THIS PART tooYOUR CODE
    private const string EndpointUri = "<your endpoint URI>";
    private const string PrimaryKey = "<your key>";
    private DocumentClient client;
```

<span data-ttu-id="ca9d1-164">Następnie przejdź toohello [Azure Portal](https://portal.azure.com) tooretrieve identyfikator URI i klucz podstawowy.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-164">Next, head toohello [Azure Portal](https://portal.azure.com) tooretrieve your URI and primary key.</span></span> <span data-ttu-id="ca9d1-165">Hello Azure rozwiązania Cosmos DB URI oraz primary key są niezbędne dla twojej aplikacji toounderstand gdzie tooconnect na oraz bazy danych Azure rozwiązania Cosmos tootrust połączeniu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-165">hello Azure Cosmos DB URI and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span>

<span data-ttu-id="ca9d1-166">W hello portalu Azure, przejdź do konta bazy danych Azure rozwiązania Cosmos tooyour, a następnie kliknij **klucze**.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-166">In hello Azure Portal, navigate tooyour Azure Cosmos DB account, and then click **Keys**.</span></span>

<span data-ttu-id="ca9d1-167">Skopiuj hello identyfikatora URI z portalu hello i wklej ją do `<your endpoint URI>` w pliku program.cs hello.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-167">Copy hello URI from hello portal and paste it into `<your endpoint URI>` in hello program.cs file.</span></span> <span data-ttu-id="ca9d1-168">Następnie kopiowania hello klucza podstawowego z portalu hello i wklej ją do `<your key>`.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-168">Then copy hello PRIMARY KEY from hello portal and paste it into `<your key>`.</span></span> <span data-ttu-id="ca9d1-169">Jeśli używasz hello Azure rozwiązania Cosmos DB emulatora, użyj `https://localhost:8081` jako punktu końcowego hello i hello autoryzacji dobrze zdefiniowany klucz z [jak przy użyciu toodevelop hello Azure rozwiązania Cosmos DB emulatora](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="ca9d1-169">If you are using hello Azure Cosmos DB Emulator, use `https://localhost:8081` as hello endpoint, and hello well-defined authorization key from [How toodevelop using hello Azure Cosmos DB Emulator](local-emulator.md).</span></span> <span data-ttu-id="ca9d1-170">Upewnij się, że hello tooremove < i >, ale pozostawić hello cudzysłowów wokół punktu końcowego, a klucz.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-170">Make sure tooremove hello < and > but leave hello double quotes around your endpoint and key.</span></span>

![Zrzut ekranu przedstawiający hello Portal Azure używany przez hello toocreate samouczka NoSQL aplikacji konsolowej C#.][keys]

<span data-ttu-id="ca9d1-173">Zaczniemy aplikacji hello rozpoczynania pracy, tworząc nowe wystąpienie klasy hello **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-173">We'll start hello getting started application by creating a new instance of hello **DocumentClient**.</span></span>

<span data-ttu-id="ca9d1-174">Poniżej hello **Main** metody, dodaj to nowe zadanie asynchroniczne o nazwie **GetStartedDemo**, które zostaną nowe wystąpienie klasy **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-174">Below hello **Main** method, add this new asynchronous task called **GetStartedDemo**, which will instantiate our new **DocumentClient**.</span></span>

```csharp
static void Main(string[] args)
{
}

// ADD THIS PART tooYOUR CODE
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);
}
```

<span data-ttu-id="ca9d1-175">Dodaj hello poniższy kod toorun zadania asynchronicznego z Twojej **Main** metody.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-175">Add hello following code toorun your asynchronous task from your **Main** method.</span></span> <span data-ttu-id="ca9d1-176">Witaj **Main** metoda będzie przechwytywać wyjątki i zapisywać je toohello konsoli.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-176">hello **Main** method will catch exceptions and write them toohello console.</span></span>

```csharp
static void Main(string[] args)
{
        // ADD THIS PART tooYOUR CODE
        try
        {
                Program p = new Program();
                p.GetStartedDemo().Wait();
        }
        catch (DocumentClientException de)
        {
                Exception baseException = de.GetBaseException();
                Console.WriteLine("{0} error occurred: {1}, Message: {2}", de.StatusCode, de.Message, baseException.Message);
        }
        catch (Exception e)
        {
                Exception baseException = e.GetBaseException();
                Console.WriteLine("Error: {0}, Message: {1}", e.Message, baseException.Message);
        }
        finally
        {
                Console.WriteLine("End of demo, press any key tooexit.");
                Console.ReadKey();
        }
```

<span data-ttu-id="ca9d1-177">Naciśnij klawisz hello **DocumentDBGettingStarted** przycisk toobuild i uruchamianie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-177">Press hello **DocumentDBGettingStarted** button toobuild and run hello application.</span></span>

<span data-ttu-id="ca9d1-178">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="ca9d1-178">Congratulations!</span></span> <span data-ttu-id="ca9d1-179">Pomyślnie nawiązano połączenie konto bazy danych Azure rozwiązania Cosmos tooan, teraz Spójrzmy w pracy z zasobami Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-179">You have successfully connected tooan Azure Cosmos DB account, let's now take a look at working with Azure Cosmos DB resources.</span></span>  

## <a name="step-4-create-a-database"></a><span data-ttu-id="ca9d1-180">Krok 4. Tworzenie bazy danych</span><span class="sxs-lookup"><span data-stu-id="ca9d1-180">Step 4: Create a database</span></span>
<span data-ttu-id="ca9d1-181">Przed dodaniem hello kod służący do tworzenia bazy danych Dodaj metodę pomocnika na potrzeby zapisywania toohello konsoli.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-181">Before you add hello code for creating a database, add a helper method for writing toohello console.</span></span>

<span data-ttu-id="ca9d1-182">Skopiuj i Wklej hello **WriteToConsoleAndPromptToContinue** poniżej hello **GetStartedDemo** metody.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-182">Copy and paste hello **WriteToConsoleAndPromptToContinue** method underneath hello **GetStartedDemo** method.</span></span>

```csharp
// ADD THIS PART tooYOUR CODE
private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
{
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key toocontinue ...");
        Console.ReadKey();
}
```

<span data-ttu-id="ca9d1-183">Bazy danych programu Azure rozwiązania Cosmos [bazy danych](documentdb-resources.md#databases) można tworzyć przy użyciu hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) metody hello **DocumentClient** klasy.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-183">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="ca9d1-184">Baza danych jest hello kontenerem logicznym magazynu dokumentów JSON podzielonym na partycje w kolekcjach.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-184">A database is hello logical container of JSON document storage partitioned across collections.</span></span>

<span data-ttu-id="ca9d1-185">Kopiuj i wklej następujący hello kodu tooyour **GetStartedDemo** poniżej powitania klienta tworzenia metody.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-185">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello client creation.</span></span> <span data-ttu-id="ca9d1-186">Spowoduje to utworzenie bazy danych o nazwie *FamilyDB*.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-186">This will create a database named *FamilyDB*.</span></span>

```csharp
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    // ADD THIS PART tooYOUR CODE
    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB_oa" });
```

<span data-ttu-id="ca9d1-187">Naciśnij klawisz hello **DocumentDBGettingStarted** przycisk toorun aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-187">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="ca9d1-188">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="ca9d1-188">Congratulations!</span></span> <span data-ttu-id="ca9d1-189">Pomyślnie utworzono bazę danych usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-189">You have successfully created an Azure Cosmos DB database.</span></span>  

## <span data-ttu-id="ca9d1-190"><a id="CreateColl"></a>Krok 5. Tworzenie kolekcji</span><span class="sxs-lookup"><span data-stu-id="ca9d1-190"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="ca9d1-191">Metoda **CreateDocumentCollectionAsync** utworzy nową kolekcję z zarezerwowaną przepływnością, co ma wpływ na cenę.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-191">**CreateDocumentCollectionAsync** will create a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="ca9d1-192">Aby uzyskać więcej informacji, odwiedź naszą [stronę cennika](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="ca9d1-192">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>

<span data-ttu-id="ca9d1-193">A [kolekcji](documentdb-resources.md#collections) można tworzyć przy użyciu hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) metody hello **DocumentClient** klasy.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-193">A [collection](documentdb-resources.md#collections) can be created by using hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="ca9d1-194">Kolekcja jest kontenerem dokumentów JSON i skojarzonej logiki aplikacji JavaScript.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-194">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="ca9d1-195">Kopiuj i wklej następujący hello kodu tooyour **GetStartedDemo** poniżej hello tworzenie bazy danych.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-195">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello database creation.</span></span> <span data-ttu-id="ca9d1-196">Spowoduje to utworzenie kolekcji dokumentów o nazwie *FamilyCollection_oa*.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-196">This will create a document collection named *FamilyCollection_oa*.</span></span>

```csharp
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    await this.client.CreateDatabaseIfNotExists("FamilyDB_oa");

    // ADD THIS PART tooYOUR CODE
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"), new DocumentCollection { Id = "FamilyCollection_oa" });
```

<span data-ttu-id="ca9d1-197">Naciśnij klawisz hello **DocumentDBGettingStarted** przycisk toorun aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-197">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="ca9d1-198">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="ca9d1-198">Congratulations!</span></span> <span data-ttu-id="ca9d1-199">Pomyślnie utworzono kolekcję dokumentów Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-199">You have successfully created an Azure Cosmos DB document collection.</span></span>  

## <span data-ttu-id="ca9d1-200"><a id="CreateDoc"></a>Krok 6. Tworzenie dokumentów JSON</span><span class="sxs-lookup"><span data-stu-id="ca9d1-200"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="ca9d1-201">A [dokumentu](documentdb-resources.md#documents) można tworzyć przy użyciu hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) metody hello **DocumentClient** klasy.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-201">A [document](documentdb-resources.md#documents) can be created by using hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="ca9d1-202">Dokumenty są zawartością JSON zdefiniowaną przez użytkownika (dowolną).</span><span class="sxs-lookup"><span data-stu-id="ca9d1-202">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="ca9d1-203">Można teraz wstawić jeden lub więcej dokumentów.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-203">We can now insert one or more documents.</span></span> <span data-ttu-id="ca9d1-204">Jeśli masz już dane, które chcesz toostore w bazie danych, możesz użyć Azure rozwiązania Cosmos DB [narzędzia migracji danych](import-data.md).</span><span class="sxs-lookup"><span data-stu-id="ca9d1-204">If you already have data you'd like toostore in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md).</span></span>

<span data-ttu-id="ca9d1-205">Najpierw należy toocreate **rodziny** klasy, która będzie reprezentowała obiekty przechowywane w usłudze Azure DB rozwiązania Cosmos w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-205">First, we need toocreate a **Family** class that will represent objects stored within Azure Cosmos DB in this sample.</span></span> <span data-ttu-id="ca9d1-206">Zostaną również utworzone podklasy **Parent**, **Child**, **Pet** i **Address**, które są używane w ramach klasy **Family**.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-206">We will also create **Parent**, **Child**, **Pet**, **Address** subclasses that are used within **Family**.</span></span> <span data-ttu-id="ca9d1-207">Należy pamiętać, że dokumenty muszą mieć właściwość **Id** serializowaną jako **id** w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-207">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span> <span data-ttu-id="ca9d1-208">Utwórz te klasy, dodając następujące podklasy wewnętrzne po hello hello **GetStartedDemo** metody.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-208">Create these classes by adding hello following internal sub-classes after hello **GetStartedDemo** method.</span></span>

<span data-ttu-id="ca9d1-209">Skopiuj i Wklej hello **rodziny**, **nadrzędnej**, **podrzędnych**, **Pet**, i **adres** poniżej Witaj **WriteToConsoleAndPromptToContinue** metody.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-209">Copy and paste hello **Family**, **Parent**, **Child**, **Pet**, and **Address** classes underneath hello **WriteToConsoleAndPromptToContinue** method.</span></span>

```csharp
private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
{
    Console.WriteLine(format, args);
    Console.WriteLine("Press any key toocontinue ...");
    Console.ReadKey();
}

// ADD THIS PART tooYOUR CODE
public class Family
{
    [JsonProperty(PropertyName = "id")]
    public string Id { get; set; }
    public string LastName { get; set; }
    public Parent[] Parents { get; set; }
    public Child[] Children { get; set; }
    public Address Address { get; set; }
    public bool IsRegistered { get; set; }
    public override string ToString()
    {
            return JsonConvert.SerializeObject(this);
    }
}

public class Parent
{
    public string FamilyName { get; set; }
    public string FirstName { get; set; }
}

public class Child
{
    public string FamilyName { get; set; }
    public string FirstName { get; set; }
    public string Gender { get; set; }
    public int Grade { get; set; }
    public Pet[] Pets { get; set; }
}

public class Pet
{
    public string GivenName { get; set; }
}

public class Address
{
    public string State { get; set; }
    public string County { get; set; }
    public string City { get; set; }
}
```

<span data-ttu-id="ca9d1-210">Skopiuj i Wklej hello **CreateFamilyDocumentIfNotExists** poniżej metody z **CreateDocumentCollectionIfNotExists** metody.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-210">Copy and paste hello **CreateFamilyDocumentIfNotExists** method underneath your **CreateDocumentCollectionIfNotExists** method.</span></span>

```csharp
// ADD THIS PART tooYOUR CODE
private async Task CreateFamilyDocumentIfNotExists(string databaseName, string collectionName, Family family)
{
    try
    {
        await this.client.ReadDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, family.Id));
        this.WriteToConsoleAndPromptToContinue("Found {0}", family.Id);
    }
    catch (DocumentClientException de)
    {
        if (de.StatusCode == HttpStatusCode.NotFound)
        {
            await this.client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), family);
            this.WriteToConsoleAndPromptToContinue("Created Family {0}", family.Id);
        }
        else
        {
            throw;
        }
    }
}
```

<span data-ttu-id="ca9d1-211">I Wstaw dwa dokumenty, jeden dla rodziny Andersen hello i hello rodziny Wakefield.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-211">And insert two documents, one each for hello Andersen Family and hello Wakefield Family.</span></span>

<span data-ttu-id="ca9d1-212">Skopiuj i Wklej kod hello, który następuje `// ADD THIS PART tooYOUR CODE` tooyour **GetStartedDemo** poniżej tworzenia kolekcji dokumentów hello metody.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-212">Copy and paste hello code that follows `// ADD THIS PART tooYOUR CODE` tooyour **GetStartedDemo** method underneath hello document collection creation.</span></span>

```csharp
await this.CreateDatabaseIfNotExists("FamilyDB_oa");

await this.CreateDocumentCollectionIfNotExists("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART tooYOUR CODE
Family andersenFamily = new Family
{
        Id = "Andersen.1",
        LastName = "Andersen",
        Parents = new Parent[]
        {
                new Parent { FirstName = "Thomas" },
                new Parent { FirstName = "Mary Kay" }
        },
        Children = new Child[]
        {
                new Child
                {
                        FirstName = "Henriette Thaulow",
                        Gender = "female",
                        Grade = 5,
                        Pets = new Pet[]
                        {
                                new Pet { GivenName = "Fluffy" }
                        }
                }
        },
        Address = new Address { State = "WA", County = "King", City = "Seattle" },
        IsRegistered = true
};

await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", andersenFamily);

Family wakefieldFamily = new Family
{
        Id = "Wakefield.7",
        LastName = "Wakefield",
        Parents = new Parent[]
        {
                new Parent { FamilyName = "Wakefield", FirstName = "Robin" },
                new Parent { FamilyName = "Miller", FirstName = "Ben" }
        },
        Children = new Child[]
        {
                new Child
                {
                        FamilyName = "Merriam",
                        FirstName = "Jesse",
                        Gender = "female",
                        Grade = 8,
                        Pets = new Pet[]
                        {
                                new Pet { GivenName = "Goofy" },
                                new Pet { GivenName = "Shadow" }
                        }
                },
                new Child
                {
                        FamilyName = "Miller",
                        FirstName = "Lisa",
                        Gender = "female",
                        Grade = 1
                }
        },
        Address = new Address { State = "NY", County = "Manhattan", City = "NY" },
        IsRegistered = false
};

await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);
```

<span data-ttu-id="ca9d1-213">Naciśnij klawisz hello **DocumentDBGettingStarted** przycisk toorun aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-213">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="ca9d1-214">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="ca9d1-214">Congratulations!</span></span> <span data-ttu-id="ca9d1-215">Pomyślnie utworzono dwa dokumenty usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-215">You have successfully created two Azure Cosmos DB documents.</span></span>  

![Diagram ilustrujący hello hierarchiczną relację między hello konta, baza danych online hello hello kolekcji i hello dokumentami używanymi przez hello toocreate samouczka NoSQL aplikacji konsolowej C#](./media/documentdb-dotnetcore-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="ca9d1-217"><a id="Query"></a>Krok 7. Wykonanie zapytania względem zasobów usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ca9d1-217"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="ca9d1-218">Usługa Azure Cosmos DB obsługuje zaawansowane [zapytania](documentdb-sql-query.md) względem dokumentów JSON przechowywanych w każdej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-218">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="ca9d1-219">Witaj następujący przykładowy kod przedstawia różne zapytania — przy użyciu obu Azure rozwiązania Cosmos bazy danych SQL składnię, a także LINQ — które można uruchomić względem hello dokumenty, które firma Microsoft wstawione w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-219">hello following sample code shows various queries - using both Azure Cosmos DB SQL syntax as well as LINQ - that we can run against hello documents we inserted in hello previous step.</span></span>

<span data-ttu-id="ca9d1-220">Skopiuj i Wklej hello **ExecuteSimpleQuery** poniżej metody z **CreateFamilyDocumentIfNotExists** metody.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-220">Copy and paste hello **ExecuteSimpleQuery** method underneath your **CreateFamilyDocumentIfNotExists** method.</span></span>

```csharp
// ADD THIS PART tooYOUR CODE
private void ExecuteSimpleQuery(string databaseName, string collectionName)
{
    // Set some common query options
    FeedOptions queryOptions = new FeedOptions { MaxItemCount = -1 };

        // Here we find hello Andersen family via its LastName
        IQueryable<Family> familyQuery = this.client.CreateDocumentQuery<Family>(
                UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), queryOptions)
                .Where(f => f.LastName == "Andersen");

        // hello query is executed synchronously here, but can also be executed asynchronously via hello IDocumentQuery<T> interface
        Console.WriteLine("Running LINQ query...");
        foreach (Family family in familyQuery)
        {
            Console.WriteLine("\tRead {0}", family);
        }

        // Now execute hello same query via direct SQL
        IQueryable<Family> familyQueryInSql = this.client.CreateDocumentQuery<Family>(
                UriFactory.CreateDocumentCollectionUri(databaseName, collectionName),
                "SELECT * FROM Family WHERE Family.LastName = 'Andersen'",
                queryOptions);

        Console.WriteLine("Running direct SQL query...");
        foreach (Family family in familyQueryInSql)
        {
                Console.WriteLine("\tRead {0}", family);
        }

        Console.WriteLine("Press any key toocontinue ...");
        Console.ReadKey();
}
```

<span data-ttu-id="ca9d1-221">Kopiuj i wklej następujący hello kodu tooyour **GetStartedDemo** poniżej tworzenia drugiego dokumentu hello metody.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-221">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello second document creation.</span></span>

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

// ADD THIS PART tooYOUR CODE
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

<span data-ttu-id="ca9d1-222">Naciśnij klawisz hello **DocumentDBGettingStarted** przycisk toorun aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-222">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="ca9d1-223">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="ca9d1-223">Congratulations!</span></span> <span data-ttu-id="ca9d1-224">Pomyślnie wykonano zapytanie względem kolekcji usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-224">You have successfully queried against an Azure Cosmos DB collection.</span></span>

<span data-ttu-id="ca9d1-225">Witaj poniższym diagramie przedstawiono sposób hello Azure rozwiązania Cosmos DB kwerend SQL składni jest wywoływana względem kolekcji hello utworzony i hello sama logika dotyczy również zapytania LINQ toohello.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-225">hello following diagram illustrates how hello Azure Cosmos DB SQL query syntax is called against hello collection you created, and hello same logic applies toohello LINQ query as well.</span></span>

![Diagram pokazujący hello zakres i znaczenie zapytania hello używane przez toocreate samouczka NoSQL hello aplikacji konsolowej C#](./media/documentdb-dotnetcore-get-started/nosql-tutorial-collection-documents.png)

<span data-ttu-id="ca9d1-227">Witaj [FROM](documentdb-sql-query.md#FromClause) — słowo kluczowe jest opcjonalna w hello zapytania, ponieważ zapytania bazy danych Azure rozwiązania Cosmos jest już tooa zakresie jednej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-227">hello [FROM](documentdb-sql-query.md#FromClause) keyword is optional in hello query because Azure Cosmos DB queries are already scoped tooa single collection.</span></span> <span data-ttu-id="ca9d1-228">W związku z tym klauzula "FROM Families f" może być zamieniona na "FROM root r" lub dowolną inną wybraną nazwę zmiennej.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-228">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="ca9d1-229">Usługa DocumentDB wywnioskuje rodziny, root lub nazwę zmiennej hello wybrane, odwołanie do bieżącej kolekcji hello domyślnie.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-229">DocumentDB will infer that Families, root, or hello variable name you chose, reference hello current collection by default.</span></span>

## <span data-ttu-id="ca9d1-230"><a id="ReplaceDocument"></a>Krok 8. Zastępowanie dokumentu JSON</span><span class="sxs-lookup"><span data-stu-id="ca9d1-230"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="ca9d1-231">Usługa Azure Cosmos DB obsługuje zastępowanie dokumentów JSON.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-231">Azure Cosmos DB supports replacing JSON documents.</span></span>  

<span data-ttu-id="ca9d1-232">Skopiuj i Wklej hello **ReplaceFamilyDocument** poniżej metody z **ExecuteSimpleQuery** metody.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-232">Copy and paste hello **ReplaceFamilyDocument** method underneath your **ExecuteSimpleQuery** method.</span></span>

```csharp
// ADD THIS PART tooYOUR CODE
private async Task ReplaceFamilyDocument(string databaseName, string collectionName, string familyName, Family updatedFamily)
{
    try
    {
        await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, familyName), updatedFamily);
        this.WriteToConsoleAndPromptToContinue("Replaced Family {0}", familyName);
    }
    catch (DocumentClientException de)
    {
        throw;
    }
}
```

<span data-ttu-id="ca9d1-233">Kopiuj i wklej następujący hello kodu tooyour **GetStartedDemo** poniżej hello wykonywania zapytania.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-233">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello query execution.</span></span> <span data-ttu-id="ca9d1-234">Po zastąpieniu dokumentu hello, spowoduje to uruchomienie hello sam ponowne przesłanie zapytania tooview hello zmieniony dokument.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-234">After replacing hello document, this will run hello same query again tooview hello changed document.</span></span>

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART tooYOUR CODE
// Update hello Grade of hello Andersen Family child
andersenFamily.Children[0].Grade = 6;

await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

<span data-ttu-id="ca9d1-235">Naciśnij klawisz hello **DocumentDBGettingStarted** przycisk toorun aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-235">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="ca9d1-236">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="ca9d1-236">Congratulations!</span></span> <span data-ttu-id="ca9d1-237">Pomyślnie zastąpiono dokument usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-237">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="ca9d1-238"><a id="DeleteDocument"></a>Krok 9. Usuwanie dokumentu JSON</span><span class="sxs-lookup"><span data-stu-id="ca9d1-238"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="ca9d1-239">Usługa Azure Cosmos DB obsługuje usuwanie dokumentów JSON.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-239">Azure Cosmos DB supports deleting JSON documents.</span></span>  

<span data-ttu-id="ca9d1-240">Skopiuj i Wklej hello **DeleteFamilyDocument** poniżej metody z **ReplaceFamilyDocument** metody.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-240">Copy and paste hello **DeleteFamilyDocument** method underneath your **ReplaceFamilyDocument** method.</span></span>

```csharp
// ADD THIS PART tooYOUR CODE
private async Task DeleteFamilyDocument(string databaseName, string collectionName, string documentName)
{
    try
    {
        await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName));
        Console.WriteLine("Deleted Family {0}", documentName);
    }
    catch (DocumentClientException de)
    {
        throw;
    }
}
```

<span data-ttu-id="ca9d1-241">Kopiuj i wklej następujący hello kodu tooyour **GetStartedDemo** poniżej hello drugiego wykonywania zapytania.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-241">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello second query execution.</span></span>

```csharp
await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART tooCODE
await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");
```

<span data-ttu-id="ca9d1-242">Naciśnij klawisz hello **DocumentDBGettingStarted** przycisk toorun aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-242">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="ca9d1-243">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="ca9d1-243">Congratulations!</span></span> <span data-ttu-id="ca9d1-244">Pomyślnie usunięto dokument usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-244">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="ca9d1-245"><a id="DeleteDatabase"></a>Krok 10: Usuwanie hello bazy danych</span><span class="sxs-lookup"><span data-stu-id="ca9d1-245"><a id="DeleteDatabase"></a>Step 10: Delete hello database</span></span>
<span data-ttu-id="ca9d1-246">Trwa usuwanie hello utworzył bazę danych spowoduje usunięcie hello bazy danych i wszystkich zasobów podrzędnych (kolekcji, dokumentów itd.).</span><span class="sxs-lookup"><span data-stu-id="ca9d1-246">Deleting hello created database will remove hello database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="ca9d1-247">Kopiuj i wklej następujący hello kodu tooyour **GetStartedDemo** poniżej dokumentu hello usunąć toodelete hello całą bazę danych i wszystkie zasoby podrzędne.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-247">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello document delete toodelete hello entire database and all children resources.</span></span>

```csharp
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");

// ADD THIS PART tooCODE
// Clean up/delete hello database
await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"));
```

<span data-ttu-id="ca9d1-248">Naciśnij klawisz hello **DocumentDBGettingStarted** przycisk toorun aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-248">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="ca9d1-249">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="ca9d1-249">Congratulations!</span></span> <span data-ttu-id="ca9d1-250">Pomyślnie usunięto bazę danych usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-250">You have successfully deleted an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="ca9d1-251"><a id="Run"></a>Krok 11. Uruchamianie całej aplikacji konsolowej C#</span><span class="sxs-lookup"><span data-stu-id="ca9d1-251"><a id="Run"></a>Step 11: Run your C# console application all together!</span></span>
<span data-ttu-id="ca9d1-252">Naciśnij klawisz hello **DocumentDBGettingStarted** przycisk w aplikacji hello toobuild programu Visual Studio w trybie debugowania.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-252">Press hello **DocumentDBGettingStarted** button in Visual Studio toobuild hello application in debug mode.</span></span>

<span data-ttu-id="ca9d1-253">Powinny pojawić się dane wyjściowe aplikacji rozpoczynania pracy w oknie konsoli hello hello.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-253">You should see hello output of your get started app in hello console window.</span></span> <span data-ttu-id="ca9d1-254">Witaj dane wyjściowe będą pokazywały wyniki hello hello dodanych zapytań i powinny odpowiadać tekstowi przykładu hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-254">hello output will show hello results of hello queries we added and should match hello example text below.</span></span>

```
Created FamilyDB_oa
Press any key toocontinue ...
Created FamilyCollection_oa
Press any key toocontinue ...
Created Family Andersen.1
Press any key toocontinue ...
Created Family Wakefield.7
Press any key toocontinue ...
Running LINQ query...
    Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
Running direct SQL query...
    Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
Replaced Family Andersen.1
Press any key toocontinue ...
Running LINQ query...
    Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
Running direct SQL query...
    Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
Deleted Family Andersen.1
End of demo, press any key tooexit.
```

<span data-ttu-id="ca9d1-255">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="ca9d1-255">Congratulations!</span></span> <span data-ttu-id="ca9d1-256">Po ukończeniu samouczka hello i mieć pracy aplikacji konsolowej C#!</span><span class="sxs-lookup"><span data-stu-id="ca9d1-256">You've completed hello tutorial and have a working C# console application!</span></span>

## <span data-ttu-id="ca9d1-257"><a id="GetSolution"></a>Pobierz hello kompletnego rozwiązania samouczka</span><span class="sxs-lookup"><span data-stu-id="ca9d1-257"><a id="GetSolution"></a> Get hello complete tutorial solution</span></span>
<span data-ttu-id="ca9d1-258">rozwiązania GetStarted hello toobuild, który zawiera wszystkie przykłady hello w tym artykule, będą potrzebne następujące hello:</span><span class="sxs-lookup"><span data-stu-id="ca9d1-258">toobuild hello GetStarted solution that contains all hello samples in this article, you will need hello following:</span></span>

* <span data-ttu-id="ca9d1-259">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-259">An active Azure account.</span></span> <span data-ttu-id="ca9d1-260">Jeśli go nie masz, możesz zarejestrować się w celu [utworzenia bezpłatnego konta](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="ca9d1-260">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="ca9d1-261">[Konta bazy danych Azure rozwiązania Cosmos][create-documentdb-dotnet.md#create-account].</span><span class="sxs-lookup"><span data-stu-id="ca9d1-261">An [Azure Cosmos DB account][create-documentdb-dotnet.md#create-account].</span></span>
* <span data-ttu-id="ca9d1-262">Witaj [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) rozwiązanie jest dostępne w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-262">hello [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="ca9d1-263">toorestore hello odwołania toohello interfejsu API usługi DocumentDB dla platformy Azure rozwiązania Cosmos DB .NET Core SDK w programie Visual Studio, kliknij prawym przyciskiem myszy hello **GetStarted** rozwiązania w Eksploratorze rozwiązań, a następnie kliknij przycisk **Włącz Przywracanie pakietu NuGet**.</span><span class="sxs-lookup"><span data-stu-id="ca9d1-263">toorestore hello references toohello DocumentDB API for Azure Cosmos DB .NET Core SDK in Visual Studio, right-click hello **GetStarted** solution in Solution Explorer, and then click **Enable NuGet Package Restore**.</span></span> <span data-ttu-id="ca9d1-264">Następnie w pliku Program.cs hello, zaktualizuj wartości EndpointUrl i AuthorizationKey hello zgodnie z opisem w [połączyć konto bazy danych Azure rozwiązania Cosmos tooan](#Connect).</span><span class="sxs-lookup"><span data-stu-id="ca9d1-264">Next, in hello Program.cs file, update hello EndpointUrl and AuthorizationKey values as described in [Connect tooan Azure Cosmos DB account](#Connect).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ca9d1-265">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ca9d1-265">Next steps</span></span>
* <span data-ttu-id="ca9d1-266">Potrzebujesz bardziej złożonego samouczka platformy ASP.NET MVC?</span><span class="sxs-lookup"><span data-stu-id="ca9d1-266">Want a more complex ASP.NET MVC tutorial?</span></span> <span data-ttu-id="ca9d1-267">Zobacz [samouczek programu ASP.NET MVC: opracowywanie aplikacji z bazy danych Azure rozwiązania Cosmos sieci Web](documentdb-dotnet-application.md).</span><span class="sxs-lookup"><span data-stu-id="ca9d1-267">See [ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB](documentdb-dotnet-application.md).</span></span>
* <span data-ttu-id="ca9d1-268">Mają toodevelop Xamarin iOS, Android lub formularzy przy użyciu aplikacji hello interfejsu API usługi DocumentDB dla platformy Azure rozwiązania Cosmos DB .NET Core SDK?</span><span class="sxs-lookup"><span data-stu-id="ca9d1-268">Want toodevelop a Xamarin iOS, Android, or Forms application using hello DocumentDB API for Azure Cosmos DB .NET Core SDK?</span></span> <span data-ttu-id="ca9d1-269">Zobacz [tworzenie aplikacji dla urządzeń przenośnych dzięki platformie Xamarin i usłudze Azure DB rozwiązania Cosmos](mobile-apps-with-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="ca9d1-269">See [Build mobile applications with Xamarin and Azure Cosmos DB](mobile-apps-with-xamarin.md).</span></span>
* <span data-ttu-id="ca9d1-270">Chcesz testowanie z bazy danych Azure rozwiązania Cosmos wydajności i skalowania tooperform?</span><span class="sxs-lookup"><span data-stu-id="ca9d1-270">Want tooperform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="ca9d1-271">Zobacz [wydajności i skalowania testowania z bazy danych Azure rozwiązania Cosmos](performance-testing.md)</span><span class="sxs-lookup"><span data-stu-id="ca9d1-271">See [Performance and scale testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="ca9d1-272">Dowiedz się, jak za[żądań, użycia i magazynu bazy danych rozwiązania Cosmos Azure Monitor](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="ca9d1-272">Learn how too[Monitor Azure Cosmos DB requests, usage, and storage](monitor-accounts.md).</span></span>
* <span data-ttu-id="ca9d1-273">Uruchom zapytania względem naszego przykładowego zestawu danych w hello [Plac zabaw dla zapytań](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="ca9d1-273">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="ca9d1-274">Zobacz toolearn więcej informacji na temat modelu programowania hello [bazy danych Azure rozwiązania Cosmos](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="ca9d1-274">toolearn more about hello programming model, see [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span>

[create-documentdb-dotnet.md#create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-dotnetcore-get-started/nosql-tutorial-keys.png
