---
title: "Azure Cosmos DB: rozpoczęcie pracy z interfejsem API usługi DocumentDB — samouczek | Microsoft Docs"
description: "Samouczek, który pokazuje tworzenie bazy danych w trybie online i aplikacji konsolowej C# przy użyciu interfejsu API usługi DocumentDB."
keywords: samouczek nosql, baza danych online, aplikacja konsolowa c#
services: cosmos-db
documentationcenter: .net
author: AndrewHoh
manager: jhubbard
editor: monicar
ms.assetid: bf08e031-718a-4a2a-89d6-91e12ff8797d
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/16/2017
ms.author: anhoh
ms.openlocfilehash: 72f66081a6409f980ec6bca5188f585489245a36
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-documentdb-api-getting-started-tutorial"></a><span data-ttu-id="1beb8-104">Azure Cosmos DB: rozpoczęcie pracy z interfejsem API usługi DocumentDB — samouczek</span><span class="sxs-lookup"><span data-stu-id="1beb8-104">Azure Cosmos DB: DocumentDB API getting started tutorial</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1beb8-105">.NET</span><span class="sxs-lookup"><span data-stu-id="1beb8-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="1beb8-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="1beb8-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="1beb8-107">Node.js dla MongoDB</span><span class="sxs-lookup"><span data-stu-id="1beb8-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="1beb8-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="1beb8-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="1beb8-109">Java</span><span class="sxs-lookup"><span data-stu-id="1beb8-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="1beb8-110">C++</span><span class="sxs-lookup"><span data-stu-id="1beb8-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="1beb8-111">Witamy w samouczku ułatwiającym rozpoczęcie pracy z interfejsem API usługi DocumentDB w usłudze Azure Cosmos DB!</span><span class="sxs-lookup"><span data-stu-id="1beb8-111">Welcome to the Azure Cosmos DB DocumentDB API getting started tutorial!</span></span> <span data-ttu-id="1beb8-112">W ramach tego samouczka zostanie utworzona aplikacja konsolowa, która tworzy zasoby usługi Azure Cosmos DB i wykonuje dla nich zapytania.</span><span class="sxs-lookup"><span data-stu-id="1beb8-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="1beb8-113">Omówione zostaną następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="1beb8-113">We'll cover:</span></span>

* <span data-ttu-id="1beb8-114">Tworzenie konta usługi Azure Cosmos DB i łączenie się z nim</span><span class="sxs-lookup"><span data-stu-id="1beb8-114">Creating and connecting to an Azure Cosmos DB account</span></span>
* <span data-ttu-id="1beb8-115">Konfigurowanie rozwiązania Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1beb8-115">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="1beb8-116">Tworzenie bazy danych w trybie online</span><span class="sxs-lookup"><span data-stu-id="1beb8-116">Creating an online database</span></span>
* <span data-ttu-id="1beb8-117">Tworzenie kolekcji</span><span class="sxs-lookup"><span data-stu-id="1beb8-117">Creating a collection</span></span>
* <span data-ttu-id="1beb8-118">Tworzenie dokumentów JSON</span><span class="sxs-lookup"><span data-stu-id="1beb8-118">Creating JSON documents</span></span>
* <span data-ttu-id="1beb8-119">Wykonywanie zapytań względem kolekcji</span><span class="sxs-lookup"><span data-stu-id="1beb8-119">Querying the collection</span></span>
* <span data-ttu-id="1beb8-120">Zastępowanie dokumentu</span><span class="sxs-lookup"><span data-stu-id="1beb8-120">Replacing a document</span></span>
* <span data-ttu-id="1beb8-121">Usuwanie dokumentu</span><span class="sxs-lookup"><span data-stu-id="1beb8-121">Deleting a document</span></span>
* <span data-ttu-id="1beb8-122">Usuwanie bazy danych</span><span class="sxs-lookup"><span data-stu-id="1beb8-122">Deleting the database</span></span>

<span data-ttu-id="1beb8-123">Nie masz czasu?</span><span class="sxs-lookup"><span data-stu-id="1beb8-123">Don't have time?</span></span> <span data-ttu-id="1beb8-124">Nie martw się!</span><span class="sxs-lookup"><span data-stu-id="1beb8-124">Don't worry!</span></span> <span data-ttu-id="1beb8-125">Kompletne rozwiązanie jest dostępne w witrynie [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="1beb8-125">The complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span></span> <span data-ttu-id="1beb8-126">Przeskocz do sekcji [Pobieranie kompletnego rozwiązania samouczka NoSQL](#GetSolution), aby uzyskać krótkie instrukcje.</span><span class="sxs-lookup"><span data-stu-id="1beb8-126">Jump to the [Get the complete NoSQL tutorial solution section](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="1beb8-127">Po wszystkim użyj przycisków głosowania u góry lub u dołu tej strony, aby wysłać nam swoją opinię.</span><span class="sxs-lookup"><span data-stu-id="1beb8-127">Afterwards, please use the voting buttons at the top or bottom of this page to give us feedback.</span></span> <span data-ttu-id="1beb8-128">Jeśli chcesz, abyśmy skontaktowali się z Tobą bezpośrednio, możesz w komentarzach podać swój adres e-mail.</span><span class="sxs-lookup"><span data-stu-id="1beb8-128">If you'd like us to contact you directly, feel free to include your email address in your comments.</span></span>

<span data-ttu-id="1beb8-129">Teraz do dzieła!</span><span class="sxs-lookup"><span data-stu-id="1beb8-129">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1beb8-130">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1beb8-130">Prerequisites</span></span>
<span data-ttu-id="1beb8-131">Upewnij się, że masz:</span><span class="sxs-lookup"><span data-stu-id="1beb8-131">Please make sure you have the following:</span></span>

* <span data-ttu-id="1beb8-132">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1beb8-132">An active Azure account.</span></span> <span data-ttu-id="1beb8-133">Jeśli go nie masz, możesz zarejestrować się w celu [utworzenia bezpłatnego konta](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="1beb8-133">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="1beb8-134">Na potrzeby tego samouczka możesz także użyć [emulatora usługi Azure Cosmos DB](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="1beb8-134">Alternatively, you can use the [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="1beb8-135">[Visual Studio Community 2017](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="1beb8-135">[Visual Studio Community 2017](http://www.visualstudio.com/).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="1beb8-136">Krok 1. Tworzenie konta usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="1beb8-136">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="1beb8-137">Utwórzmy konto usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1beb8-137">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="1beb8-138">Jeśli masz już konto, którego chcesz użyć, możesz przejść od razu do kroku [Konfigurowanie rozwiązania Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="1beb8-138">If you already have an account you want to use, you can skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span></span> <span data-ttu-id="1beb8-139">Jeśli używasz emulatora usługi Azure Cosmos DB, wykonaj czynności opisane w temacie [Emulator usługi Azure Cosmos DB](local-emulator.md), aby skonfigurować emulator, a następnie przejdź do sekcji [Konfigurowanie rozwiązania programu Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="1beb8-139">If you are using the Azure Cosmos DB Emulator, please follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="1beb8-140"><a id="SetupVS"></a>Krok 2. Konfigurowanie rozwiązania programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1beb8-140"><a id="SetupVS"></a>Step 2: Setup your Visual Studio solution</span></span>
1. <span data-ttu-id="1beb8-141">Otwórz program **Visual Studio 2017** na komputerze.</span><span class="sxs-lookup"><span data-stu-id="1beb8-141">Open **Visual Studio 2017** on your computer.</span></span>
2. <span data-ttu-id="1beb8-142">W menu **Plik** wybierz polecenie **Nowy**, a następnie wybierz pozycję **Projekt**.</span><span class="sxs-lookup"><span data-stu-id="1beb8-142">On the **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="1beb8-143">W oknie dialogowym **Nowy projekt** wybierz pozycję **Szablony** / **Visual C#** / **Aplikacja konsolowa**, podaj nazwę projektu, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="1beb8-143">In the **New Project** dialog, select **Templates** / **Visual C#** / **Console Application**, name your project, and then click **OK**.</span></span>
   <span data-ttu-id="1beb8-144">![Zrzut ekranu przedstawiający okno Nowy projekt](./media/documentdb-get-started/nosql-tutorial-new-project-2.png)</span><span class="sxs-lookup"><span data-stu-id="1beb8-144">![Screen shot of the New Project window](./media/documentdb-get-started/nosql-tutorial-new-project-2.png)</span></span>
4. <span data-ttu-id="1beb8-145">W **Eksploratorze rozwiązań** kliknij prawym przyciskiem myszy nową aplikację konsolową, która znajduje się w ramach rozwiązania Visual Studio, a następnie kliknij pozycję **Zarządzaj pakietami NuGet...**</span><span class="sxs-lookup"><span data-stu-id="1beb8-145">In the **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
    
    ![Zrzut ekranu przedstawiający menu projektu kliknięte prawym przyciskiem myszy](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges.png)
5. <span data-ttu-id="1beb8-147">Na karcie **NuGet** kliknij pozycję **Przeglądaj** i wpisz ciąg **azure documentdb** w polu wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="1beb8-147">In the **Nuget** tab, click **Browse**, and type **azure documentdb** in the search box.</span></span>
6. <span data-ttu-id="1beb8-148">W wynikach znajdź pozycję **Microsoft.Azure.DocumentDB** i kliknij przycisk **Zainstaluj**.</span><span class="sxs-lookup"><span data-stu-id="1beb8-148">Within the results, find **Microsoft.Azure.DocumentDB** and click **Install**.</span></span>
   <span data-ttu-id="1beb8-149">Identyfikator pakietu dla biblioteki klienta interfejsu API Azure rozwiązania Cosmos bazy danych usługi DocumentDB jest [Biblioteka kliencka usługi Microsoft Azure DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/).</span><span class="sxs-lookup"><span data-stu-id="1beb8-149">The package ID for the Azure Cosmos DB DocumentDB API Client Library is [Microsoft Azure DocumentDB Client Library](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/).</span></span>
   <span data-ttu-id="1beb8-150">![Zrzut ekranu przedstawiający menu NuGet służące do znajdowania zestawu SDK klienta usługi Azure Cosmos DB](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)</span><span class="sxs-lookup"><span data-stu-id="1beb8-150">![Screen shot of the Nuget Menu for finding Azure Cosmos DB Client SDK](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)</span></span>

    <span data-ttu-id="1beb8-151">Jeśli wyświetlane są komunikaty dotyczące przejrzenia zmian wprowadzonych w rozwiązaniu, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="1beb8-151">If you get a messages about reviewing changes to the solution, click **OK**.</span></span> <span data-ttu-id="1beb8-152">Jeśli wyświetlany jest komunikat o akceptacji licencji, kliknij pozycję **Akceptuję**.</span><span class="sxs-lookup"><span data-stu-id="1beb8-152">If you get a message about license acceptance, click **I accept**.</span></span>

<span data-ttu-id="1beb8-153">Wspaniale!</span><span class="sxs-lookup"><span data-stu-id="1beb8-153">Great!</span></span> <span data-ttu-id="1beb8-154">Teraz, po zakończeniu konfigurowania, zacznijmy pisanie kodu.</span><span class="sxs-lookup"><span data-stu-id="1beb8-154">Now that we finished the setup, let's start writing some code.</span></span> <span data-ttu-id="1beb8-155">Ukończony projekt kodu z tego samouczka można znaleźć w witrynie [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="1beb8-155">You can find a completed code project of this tutorial at [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs).</span></span>

## <span data-ttu-id="1beb8-156"><a id="Connect"></a>Krok 3. Łączenie się z kontem usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="1beb8-156"><a id="Connect"></a>Step 3: Connect to an Azure Cosmos DB account</span></span>
<span data-ttu-id="1beb8-157">Najpierw dodaj te odwołania na początku aplikacji C# w pliku Program.cs:</span><span class="sxs-lookup"><span data-stu-id="1beb8-157">First, add these references to the beginning of your C# application, in the Program.cs file:</span></span>

    using System;
    using System.Linq;
    using System.Threading.Tasks;

    // ADD THIS PART TO YOUR CODE
    using System.Net;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Newtonsoft.Json;

> [!IMPORTANT]
> <span data-ttu-id="1beb8-158">W celu ukończenia tego samouczka upewnij się, że dodano zależności opisane powyżej.</span><span class="sxs-lookup"><span data-stu-id="1beb8-158">In order to complete the tutorial, make sure you add the dependencies above.</span></span>
> 
> 

<span data-ttu-id="1beb8-159">Dodaj teraz te dwie stałe i zmienną *client* poniżej klasy publicznej *Program*.</span><span class="sxs-lookup"><span data-stu-id="1beb8-159">Now, add these two constants and your *client* variable underneath your public class *Program*.</span></span>

    public class Program
    {
        // ADD THIS PART TO YOUR CODE
        private const string EndpointUrl = "<your endpoint URL>";
        private const string PrimaryKey = "<your primary key>";
        private DocumentClient client;

<span data-ttu-id="1beb8-160">Następnie wróć do witryny [Azure Portal](https://portal.azure.com), aby pobrać adres URL punktu końcowego i klucz podstawowy.</span><span class="sxs-lookup"><span data-stu-id="1beb8-160">Next, head back to the [Azure Portal](https://portal.azure.com) to retrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="1beb8-161">Adres URL punktu końcowego i klucz podstawowy są niezbędne, aby aplikacja wiedziała, z jakim elementem ma się połączyć, oraz aby usługa Azure Cosmos DB ufała połączeniu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1beb8-161">The endpoint URL and primary key are necessary for your application to understand where to connect to, and for Azure Cosmos DB to trust your application's connection.</span></span>

<span data-ttu-id="1beb8-162">W witrynie Azure Portal przejdź do swojego konta usługi Azure Cosmos DB i kliknij pozycję **Klucze**.</span><span class="sxs-lookup"><span data-stu-id="1beb8-162">In the Azure Portal, navigate to your Azure Cosmos DB account, and then click **Keys**.</span></span>

<span data-ttu-id="1beb8-163">Skopiuj identyfikator URI z portalu i wklej go w miejsce `<your endpoint URL>` w pliku program.cs.</span><span class="sxs-lookup"><span data-stu-id="1beb8-163">Copy the URI from the portal and paste it into `<your endpoint URL>` in the program.cs file.</span></span> <span data-ttu-id="1beb8-164">Następnie skopiuj KLUCZ PODSTAWOWY z portalu i wklej go w miejsce `<your primary key>`.</span><span class="sxs-lookup"><span data-stu-id="1beb8-164">Then copy the PRIMARY KEY from the portal and paste it into `<your primary key>`.</span></span>

![Zrzut ekranu przedstawiający portal Azure używany przez samouczek NoSQL do tworzenia aplikacji konsolowej C#.][keys]

<span data-ttu-id="1beb8-167">Następnie zaczniemy budowanie aplikacji, tworząc nowe wystąpienie klasy **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="1beb8-167">Next, we'll start the application by creating a new instance of the **DocumentClient**.</span></span>

<span data-ttu-id="1beb8-168">Poniżej metody **Main** dodaj to nowe zadanie asynchroniczne o nazwie **GetStartedDemo**, które utworzy nowe wystąpienie klasy **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="1beb8-168">Below the **Main** method, add this new asynchronous task called **GetStartedDemo**, which will instantiate our new **DocumentClient**.</span></span>

    static void Main(string[] args)
    {
    }

    // ADD THIS PART TO YOUR CODE
    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);
    }

<span data-ttu-id="1beb8-169">Dodaj następujący kod w celu uruchomienia zadania asynchronicznego z metody **Main**.</span><span class="sxs-lookup"><span data-stu-id="1beb8-169">Add the following code to run your asynchronous task from your **Main** method.</span></span> <span data-ttu-id="1beb8-170">Metoda **Main** będzie przechwytywać wyjątki i zapisywać je w konsoli.</span><span class="sxs-lookup"><span data-stu-id="1beb8-170">The **Main** method will catch exceptions and write them to the console.</span></span>

    static void Main(string[] args)
    {
            // ADD THIS PART TO YOUR CODE
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
                    Console.WriteLine("End of demo, press any key to exit.");
                    Console.ReadKey();
            }

<span data-ttu-id="1beb8-171">Naciśnij klawisz **F5**, aby uruchomić aplikację.</span><span class="sxs-lookup"><span data-stu-id="1beb8-171">Press **F5** to run your application.</span></span> <span data-ttu-id="1beb8-172">W danych wyjściowych okna konsoli wyświetlany jest komunikat `End of demo, press any key to exit.` potwierdzający, że połączenie zostało nawiązane.</span><span class="sxs-lookup"><span data-stu-id="1beb8-172">The console window output displays the message `End of demo, press any key to exit.` confirming that the connection was made.</span></span>  <span data-ttu-id="1beb8-173">Następnie można zamknąć okno konsoli.</span><span class="sxs-lookup"><span data-stu-id="1beb8-173">You can then close the console window.</span></span> 

<span data-ttu-id="1beb8-174">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="1beb8-174">Congratulations!</span></span> <span data-ttu-id="1beb8-175">Pomyślnie nawiązano połączenie z kontem usługi Azure Cosmos DB. Teraz przyjrzyjmy się pracy z zasobami usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1beb8-175">You have successfully connected to an Azure Cosmos DB account, let's now take a look at working with Azure Cosmos DB resources.</span></span>  

## <a name="step-4-create-a-database"></a><span data-ttu-id="1beb8-176">Krok 4. Tworzenie bazy danych</span><span class="sxs-lookup"><span data-stu-id="1beb8-176">Step 4: Create a database</span></span>
<span data-ttu-id="1beb8-177">Przed dodaniem kodu na potrzeby tworzenia bazy danych dodaj metodę pomocnika na potrzeby pisania w konsoli.</span><span class="sxs-lookup"><span data-stu-id="1beb8-177">Before you add the code for creating a database, add a helper method for writing to the console.</span></span>

<span data-ttu-id="1beb8-178">Skopiuj i wklej metodę **WriteToConsoleAndPromptToContinue** poniżej metody **GetStartedDemo**.</span><span class="sxs-lookup"><span data-stu-id="1beb8-178">Copy and paste the **WriteToConsoleAndPromptToContinue** method after the **GetStartedDemo** method.</span></span>

    // ADD THIS PART TO YOUR CODE
    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
            Console.WriteLine(format, args);
            Console.WriteLine("Press any key to continue ...");
            Console.ReadKey();
    }

<span data-ttu-id="1beb8-179">[Bazę danych](documentdb-resources.md#databases) usługi Azure Cosmos DB można utworzyć za pomocą metody [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) klasy **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="1beb8-179">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using the [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="1beb8-180">Baza danych jest kontenerem logicznym magazynu dokumentów JSON podzielonym na partycje w kolekcjach.</span><span class="sxs-lookup"><span data-stu-id="1beb8-180">A database is the logical container of JSON document storage partitioned across collections.</span></span>

<span data-ttu-id="1beb8-181">Skopiuj i wklej następujący kod do metody **GetStartedDemo** poniżej kodu służącego do tworzenia klienta.</span><span class="sxs-lookup"><span data-stu-id="1beb8-181">Copy and paste the following code to your **GetStartedDemo** method after the client creation.</span></span> <span data-ttu-id="1beb8-182">Spowoduje to utworzenie bazy danych o nazwie *FamilyDB*.</span><span class="sxs-lookup"><span data-stu-id="1beb8-182">This will create a database named *FamilyDB*.</span></span>

    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        // ADD THIS PART TO YOUR CODE
        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

<span data-ttu-id="1beb8-183">Naciśnij klawisz **F5**, aby uruchomić aplikację.</span><span class="sxs-lookup"><span data-stu-id="1beb8-183">Press **F5** to run your application.</span></span>

<span data-ttu-id="1beb8-184">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="1beb8-184">Congratulations!</span></span> <span data-ttu-id="1beb8-185">Pomyślnie utworzono bazę danych usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1beb8-185">You have successfully created an Azure Cosmos DB database.</span></span>  

## <span data-ttu-id="1beb8-186"><a id="CreateColl"></a>Krok 5. Tworzenie kolekcji</span><span class="sxs-lookup"><span data-stu-id="1beb8-186"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="1beb8-187">Za pomocą metody **CreateDocumentCollectionIfNotExistsAsync** zostanie utworzona nowa kolekcja z zarezerwowaną przepływnością, co ma wpływ na cenę.</span><span class="sxs-lookup"><span data-stu-id="1beb8-187">**CreateDocumentCollectionIfNotExistsAsync** will create a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="1beb8-188">Aby uzyskać więcej informacji, odwiedź naszą [stronę cennika](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="1beb8-188">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="1beb8-189">[Kolekcję](documentdb-resources.md#collections) można utworzyć za pomocą metody [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) klasy **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="1beb8-189">A [collection](documentdb-resources.md#collections) can be created by using the [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="1beb8-190">Kolekcja jest kontenerem dokumentów JSON i skojarzonej logiki aplikacji JavaScript.</span><span class="sxs-lookup"><span data-stu-id="1beb8-190">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="1beb8-191">Skopiuj i wklej następujący kod do metody **GetStartedDemo** poniżej kodu służącego do tworzenia bazy danych.</span><span class="sxs-lookup"><span data-stu-id="1beb8-191">Copy and paste the following code to your **GetStartedDemo** method after the database creation.</span></span> <span data-ttu-id="1beb8-192">Spowoduje to utworzenie kolekcji dokumentów o nazwie *FamilyCollection*.</span><span class="sxs-lookup"><span data-stu-id="1beb8-192">This will create a document collection named *FamilyCollection*.</span></span>

        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

        // ADD THIS PART TO YOUR CODE
         await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });

<span data-ttu-id="1beb8-193">Naciśnij klawisz **F5**, aby uruchomić aplikację.</span><span class="sxs-lookup"><span data-stu-id="1beb8-193">Press **F5** to run your application.</span></span>

<span data-ttu-id="1beb8-194">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="1beb8-194">Congratulations!</span></span> <span data-ttu-id="1beb8-195">Pomyślnie utworzono kolekcję dokumentów Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1beb8-195">You have successfully created an Azure Cosmos DB document collection.</span></span>  

## <span data-ttu-id="1beb8-196"><a id="CreateDoc"></a>Krok 6. Tworzenie dokumentów JSON</span><span class="sxs-lookup"><span data-stu-id="1beb8-196"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="1beb8-197">[Dokument](documentdb-resources.md#documents) można utworzyć za pomocą metody [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) klasy **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="1beb8-197">A [document](documentdb-resources.md#documents) can be created by using the [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="1beb8-198">Dokumenty są zawartością JSON zdefiniowaną przez użytkownika (dowolną).</span><span class="sxs-lookup"><span data-stu-id="1beb8-198">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="1beb8-199">Można teraz wstawić jeden lub więcej dokumentów.</span><span class="sxs-lookup"><span data-stu-id="1beb8-199">We can now insert one or more documents.</span></span> <span data-ttu-id="1beb8-200">Jeśli masz już dane, które chcesz przechowywać w bazie danych, możesz użyć Azure DB rozwiązania Cosmos [narzędzia migracji danych](import-data.md) do importowania danych do bazy danych.</span><span class="sxs-lookup"><span data-stu-id="1beb8-200">If you already have data you'd like to store in your database, you can use the Azure Cosmos DB [Data Migration tool](import-data.md) to import the data into a database.</span></span>

<span data-ttu-id="1beb8-201">Najpierw należy utworzyć klasę **Family**, która będzie reprezentowała obiekty przechowywane w usłudze Azure Cosmos DB w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="1beb8-201">First, we need to create a **Family** class that will represent objects stored within Azure Cosmos DB in this sample.</span></span> <span data-ttu-id="1beb8-202">Zostaną również utworzone podklasy **Parent**, **Child**, **Pet** i **Address**, które są używane w ramach klasy **Family**.</span><span class="sxs-lookup"><span data-stu-id="1beb8-202">We will also create **Parent**, **Child**, **Pet**, **Address** subclasses that are used within **Family**.</span></span> <span data-ttu-id="1beb8-203">Należy pamiętać, że dokumenty muszą mieć właściwość **Id** serializowaną jako **id** w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="1beb8-203">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span> <span data-ttu-id="1beb8-204">Utwórz te klasy, dodając następujące podklasy wewnętrzne po metodzie **GetStartedDemo**.</span><span class="sxs-lookup"><span data-stu-id="1beb8-204">Create these classes by adding the following internal sub-classes after the **GetStartedDemo** method.</span></span>

<span data-ttu-id="1beb8-205">Skopiuj i wklej klasy **Family**, **Parent**, **Child**, **Pet** i **Address** poniżej metody **WriteToConsoleAndPromptToContinue**.</span><span class="sxs-lookup"><span data-stu-id="1beb8-205">Copy and paste the **Family**, **Parent**, **Child**, **Pet**, and **Address** classes after the **WriteToConsoleAndPromptToContinue** method.</span></span>

    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key to continue ...");
        Console.ReadKey();
    }

    // ADD THIS PART TO YOUR CODE
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

<span data-ttu-id="1beb8-206">Skopiuj i wklej metodę **CreateFamilyDocumentIfNotExists** poniżej klasy **Address**.</span><span class="sxs-lookup"><span data-stu-id="1beb8-206">Copy and paste the **CreateFamilyDocumentIfNotExists** method underneath your **Address** class.</span></span>

    // ADD THIS PART TO YOUR CODE
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

<span data-ttu-id="1beb8-207">Następnie wstaw dwa dokumenty, jeden dla rodziny Andersen i jeden dla rodziny Wakefield.</span><span class="sxs-lookup"><span data-stu-id="1beb8-207">And insert two documents, one each for the Andersen Family and the Wakefield Family.</span></span>

<span data-ttu-id="1beb8-208">Skopiuj i wklej następujący kod do metody **GetStartedDemo** poniżej kodu służącego do tworzenia kolekcji dokumentów.</span><span class="sxs-lookup"><span data-stu-id="1beb8-208">Copy and paste the following code to your **GetStartedDemo** method after the document collection creation.</span></span>

    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });
    
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });


    // ADD THIS PART TO YOUR CODE
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

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", andersenFamily);

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

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

<span data-ttu-id="1beb8-209">Naciśnij klawisz **F5**, aby uruchomić aplikację.</span><span class="sxs-lookup"><span data-stu-id="1beb8-209">Press **F5** to run your application.</span></span>

<span data-ttu-id="1beb8-210">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="1beb8-210">Congratulations!</span></span> <span data-ttu-id="1beb8-211">Pomyślnie utworzono dwa dokumenty usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1beb8-211">You have successfully created two Azure Cosmos DB documents.</span></span>  

![Diagram pokazujący hierarchiczną relację między kontem, bazą danych w trybie online, kolekcją i dokumentami używanymi przez samouczek NoSQL do tworzenia aplikacji konsolowej C#](./media/documentdb-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="1beb8-213"><a id="Query"></a>Krok 7. Wykonanie zapytania względem zasobów usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="1beb8-213"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="1beb8-214">Usługa Azure Cosmos DB obsługuje zaawansowane [zapytania](documentdb-sql-query.md) względem dokumentów JSON przechowywanych w każdej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="1beb8-214">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="1beb8-215">Następujący przykładowy kod przedstawia różne zapytania — przy użyciu składni SQL usługi Azure Cosmos DB oraz LINQ — które można uruchomić względem dokumentów wstawionych w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="1beb8-215">The following sample code shows various queries - using both Azure Cosmos DB SQL syntax as well as LINQ - that we can run against the documents we inserted in the previous step.</span></span>

<span data-ttu-id="1beb8-216">Skopiuj i wklej metodę **ExecuteSimpleQuery** poniżej metody **CreateFamilyDocumentIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="1beb8-216">Copy and paste the **ExecuteSimpleQuery** method after your **CreateFamilyDocumentIfNotExists** method.</span></span>

    // ADD THIS PART TO YOUR CODE
    private void ExecuteSimpleQuery(string databaseName, string collectionName)
    {
        // Set some common query options
        FeedOptions queryOptions = new FeedOptions { MaxItemCount = -1 };

            // Here we find the Andersen family via its LastName
            IQueryable<Family> familyQuery = this.client.CreateDocumentQuery<Family>(
                    UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), queryOptions)
                    .Where(f => f.LastName == "Andersen");

            // The query is executed synchronously here, but can also be executed asynchronously via the IDocumentQuery<T> interface
            Console.WriteLine("Running LINQ query...");
            foreach (Family family in familyQuery)
            {
                    Console.WriteLine("\tRead {0}", family);
            }

            // Now execute the same query via direct SQL
            IQueryable<Family> familyQueryInSql = this.client.CreateDocumentQuery<Family>(
                    UriFactory.CreateDocumentCollectionUri(databaseName, collectionName),
                    "SELECT * FROM Family WHERE Family.LastName = 'Andersen'",
                    queryOptions);

            Console.WriteLine("Running direct SQL query...");
            foreach (Family family in familyQueryInSql)
            {
                    Console.WriteLine("\tRead {0}", family);
            }

            Console.WriteLine("Press any key to continue ...");
            Console.ReadKey();
    }

<span data-ttu-id="1beb8-217">Skopiuj i wklej następujący kod do metody **GetStartedDemo** poniżej kodu służącego do tworzenia drugiego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="1beb8-217">Copy and paste the following code to your **GetStartedDemo** method after the second document creation.</span></span>

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    // ADD THIS PART TO YOUR CODE
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

<span data-ttu-id="1beb8-218">Naciśnij klawisz **F5**, aby uruchomić aplikację.</span><span class="sxs-lookup"><span data-stu-id="1beb8-218">Press **F5** to run your application.</span></span>

<span data-ttu-id="1beb8-219">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="1beb8-219">Congratulations!</span></span> <span data-ttu-id="1beb8-220">Pomyślnie wykonano zapytanie względem kolekcji usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1beb8-220">You have successfully queried against an Azure Cosmos DB collection.</span></span>

<span data-ttu-id="1beb8-221">Na poniższym diagramie przedstawiono sposób, w jaki składnia zapytania SQL usługi Azure Cosmos DB jest wywoływana względem utworzonej kolekcji. Ta sama logika dotyczy również zapytania LINQ.</span><span class="sxs-lookup"><span data-stu-id="1beb8-221">The following diagram illustrates how the Azure Cosmos DB SQL query syntax is called against the collection you created, and the same logic applies to the LINQ query as well.</span></span>

![Diagram pokazujący zakres i znaczenie zapytania używanego przez samouczek NoSQL do utworzenia aplikacji konsolowej C#](./media/documentdb-get-started/nosql-tutorial-collection-documents.png)

<span data-ttu-id="1beb8-223">[FROM](documentdb-sql-query.md#FromClause) — słowo kluczowe jest opcjonalne w zapytaniu, ponieważ zapytania bazy danych Azure rozwiązania Cosmos mają już zakres określony jako jedna kolekcja.</span><span class="sxs-lookup"><span data-stu-id="1beb8-223">The [FROM](documentdb-sql-query.md#FromClause) keyword is optional in the query because Azure Cosmos DB queries are already scoped to a single collection.</span></span> <span data-ttu-id="1beb8-224">W związku z tym klauzula "FROM Families f" może być zamieniona na "FROM root r" lub dowolną inną wybraną nazwę zmiennej.</span><span class="sxs-lookup"><span data-stu-id="1beb8-224">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="1beb8-225">Azure DB rozwiązania Cosmos będzie wywnioskować, że zmienne Families, root lub wybrana nazwa zmiennej, domyślnie odwołują się bieżącej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="1beb8-225">Azure Cosmos DB will infer that Families, root, or the variable name you chose, reference the current collection by default.</span></span>

## <span data-ttu-id="1beb8-226"><a id="ReplaceDocument"></a>Krok 8. Zastępowanie dokumentu JSON</span><span class="sxs-lookup"><span data-stu-id="1beb8-226"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="1beb8-227">Usługa Azure Cosmos DB obsługuje zastępowanie dokumentów JSON.</span><span class="sxs-lookup"><span data-stu-id="1beb8-227">Azure Cosmos DB supports replacing JSON documents.</span></span>  

<span data-ttu-id="1beb8-228">Skopiuj i wklej metodę **ReplaceFamilyDocument** poniżej metody **ExecuteSimpleQuery**.</span><span class="sxs-lookup"><span data-stu-id="1beb8-228">Copy and paste the **ReplaceFamilyDocument** method after your **ExecuteSimpleQuery** method.</span></span>

    // ADD THIS PART TO YOUR CODE
    private async Task ReplaceFamilyDocument(string databaseName, string collectionName, string familyName, Family updatedFamily)
    {
         await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, familyName), updatedFamily);
         this.WriteToConsoleAndPromptToContinue("Replaced Family {0}", familyName);
    }

<span data-ttu-id="1beb8-229">Skopiuj i wklej następujący kod do metody **GetStartedDemo** poniżej kodu służącego do wykonywania zapytania (na końcu metody).</span><span class="sxs-lookup"><span data-stu-id="1beb8-229">Copy and paste the following code to your **GetStartedDemo** method after the query execution, at the end of the method.</span></span> <span data-ttu-id="1beb8-230">Po zastąpieniu dokumentu spowoduje to ponowne uruchomienie tego samego zapytania, aby wyświetlić zmieniony dokument.</span><span class="sxs-lookup"><span data-stu-id="1beb8-230">After replacing the document, this will run the same query again to view the changed document.</span></span>

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    // ADD THIS PART TO YOUR CODE
    // Update the Grade of the Andersen Family child
    andersenFamily.Children[0].Grade = 6;

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

<span data-ttu-id="1beb8-231">Naciśnij klawisz **F5**, aby uruchomić aplikację.</span><span class="sxs-lookup"><span data-stu-id="1beb8-231">Press **F5** to run your application.</span></span>

<span data-ttu-id="1beb8-232">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="1beb8-232">Congratulations!</span></span> <span data-ttu-id="1beb8-233">Pomyślnie zastąpiono dokument usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1beb8-233">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="1beb8-234"><a id="DeleteDocument"></a>Krok 9. Usuwanie dokumentu JSON</span><span class="sxs-lookup"><span data-stu-id="1beb8-234"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="1beb8-235">Usługa Azure Cosmos DB obsługuje usuwanie dokumentów JSON.</span><span class="sxs-lookup"><span data-stu-id="1beb8-235">Azure Cosmos DB supports deleting JSON documents.</span></span>  

<span data-ttu-id="1beb8-236">Skopiuj i wklej metodę **DeleteFamilyDocument** poniżej metody **ReplaceFamilyDocument**.</span><span class="sxs-lookup"><span data-stu-id="1beb8-236">Copy and paste the **DeleteFamilyDocument** method after your **ReplaceFamilyDocument** method.</span></span>

    // ADD THIS PART TO YOUR CODE
    private async Task DeleteFamilyDocument(string databaseName, string collectionName, string documentName)
    {
         await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName));
         Console.WriteLine("Deleted Family {0}", documentName);
    }

<span data-ttu-id="1beb8-237">Skopiuj i wklej następujący kod do metody **GetStartedDemo** poniżej kodu służącego do wykonywania drugiego zapytania (na końcu metody).</span><span class="sxs-lookup"><span data-stu-id="1beb8-237">Copy and paste the following code to your **GetStartedDemo** method after the second query execution, at the end of the method.</span></span>

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);
    
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");
    
    // ADD THIS PART TO CODE
    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

<span data-ttu-id="1beb8-238">Naciśnij klawisz **F5**, aby uruchomić aplikację.</span><span class="sxs-lookup"><span data-stu-id="1beb8-238">Press **F5** to run your application.</span></span>

<span data-ttu-id="1beb8-239">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="1beb8-239">Congratulations!</span></span> <span data-ttu-id="1beb8-240">Pomyślnie usunięto dokument usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1beb8-240">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="1beb8-241"><a id="DeleteDatabase"></a>Krok 10. Usuwanie bazy danych</span><span class="sxs-lookup"><span data-stu-id="1beb8-241"><a id="DeleteDatabase"></a>Step 10: Delete the database</span></span>
<span data-ttu-id="1beb8-242">Usunięcie utworzonej bazy danych spowoduje usunięcie bazy danych i wszystkich zasobów podrzędnych (kolekcji, dokumentów itd.).</span><span class="sxs-lookup"><span data-stu-id="1beb8-242">Deleting the created database will remove the database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="1beb8-243">Skopiuj i wklej następujący kod do metody **GetStartedDemo** poniżej kodu służącego do usuwania dokumentu, aby usunąć całą bazę danych i wszystkie zasoby podrzędne.</span><span class="sxs-lookup"><span data-stu-id="1beb8-243">Copy and paste the following code to your **GetStartedDemo** method after the document delete to delete the entire database and all children resources.</span></span>

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

    // ADD THIS PART TO CODE
    // Clean up/delete the database
    await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB"));

<span data-ttu-id="1beb8-244">Naciśnij klawisz **F5**, aby uruchomić aplikację.</span><span class="sxs-lookup"><span data-stu-id="1beb8-244">Press **F5** to run your application.</span></span>

<span data-ttu-id="1beb8-245">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="1beb8-245">Congratulations!</span></span> <span data-ttu-id="1beb8-246">Pomyślnie usunięto bazę danych usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1beb8-246">You have successfully deleted an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="1beb8-247"><a id="Run"></a>Krok 11. Uruchamianie całej aplikacji konsolowej C#</span><span class="sxs-lookup"><span data-stu-id="1beb8-247"><a id="Run"></a>Step 11: Run your C# console application all together!</span></span>
<span data-ttu-id="1beb8-248">Naciśnij klawisz F5 w programie Visual Studio, aby skompilować aplikację w trybie debugowania.</span><span class="sxs-lookup"><span data-stu-id="1beb8-248">Hit F5 in Visual Studio to build the application in debug mode.</span></span>

<span data-ttu-id="1beb8-249">Powinny pojawić się dane wyjściowe aplikacji rozpoczynania pracy w oknie konsoli.</span><span class="sxs-lookup"><span data-stu-id="1beb8-249">You should see the output of your get started app in a console window.</span></span> <span data-ttu-id="1beb8-250">Dane wyjściowe będą pokazywały wyniki dodanych zapytań i powinny odpowiadać poniższemu przykładowemu tekstowi.</span><span class="sxs-lookup"><span data-stu-id="1beb8-250">The output will show the results of the queries we added and should match the example text below.</span></span>

    Created FamilyDB
    Press any key to continue ...
    Created FamilyCollection
    Press any key to continue ...
    Created Family Andersen.1
    Press any key to continue ...
    Created Family Wakefield.7
    Press any key to continue ...
    Running LINQ query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Running direct SQL query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Replaced Family Andersen.1
    Press any key to continue ...
    Running LINQ query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Running direct SQL query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Deleted Family Andersen.1
    End of demo, press any key to exit.

<span data-ttu-id="1beb8-251">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="1beb8-251">Congratulations!</span></span> <span data-ttu-id="1beb8-252">Pomyślnie ukończono ten samouczek i utworzono działającą aplikację konsolową C#.</span><span class="sxs-lookup"><span data-stu-id="1beb8-252">You've completed the tutorial and have a working C# console application!</span></span>

## <span data-ttu-id="1beb8-253"><a id="GetSolution"></a> Pobieranie kompletnego rozwiązania samouczka</span><span class="sxs-lookup"><span data-stu-id="1beb8-253"><a id="GetSolution"></a> Get the complete tutorial solution</span></span>
<span data-ttu-id="1beb8-254">Jeśli nie masz czasu na ukończenie tego samouczka lub po prostu chcesz pobrać przykłady kodu, możesz uzyskać je w serwisie [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="1beb8-254">If you didn't have time to complete the steps in this tutorial, or just want to download the code samples, you can get it from [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span></span> 

<span data-ttu-id="1beb8-255">Aby skompilować rozwiązanie GetStarted, niezbędne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="1beb8-255">To build the GetStarted solution, you will need the following:</span></span>

* <span data-ttu-id="1beb8-256">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1beb8-256">An active Azure account.</span></span> <span data-ttu-id="1beb8-257">Jeśli go nie masz, możesz zarejestrować się w celu [utworzenia bezpłatnego konta](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="1beb8-257">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="1beb8-258">[Konta bazy danych Azure rozwiązania Cosmos][cosmos-db-create-account].</span><span class="sxs-lookup"><span data-stu-id="1beb8-258">An [Azure Cosmos DB account][cosmos-db-create-account].</span></span>
* <span data-ttu-id="1beb8-259">Rozwiązanie [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) dostępne w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="1beb8-259">The [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="1beb8-260">Aby przywrócić odwołania do zestawu SDK .NET usługi Azure rozwiązania Cosmos bazy danych w programie Visual Studio, kliknij prawym przyciskiem myszy **GetStarted** rozwiązania w Eksploratorze rozwiązań, a następnie kliknij przycisk **Włącz Przywracanie pakietu NuGet**.</span><span class="sxs-lookup"><span data-stu-id="1beb8-260">To restore the references to the Azure Cosmos DB .NET SDK in Visual Studio, right-click the **GetStarted** solution in Solution Explorer, and then click **Enable NuGet Package Restore**.</span></span> <span data-ttu-id="1beb8-261">Następnie w pliku App.config zaktualizuj wartości EndpointUrl i AuthorizationKey zgodnie z opisem w kroku [Łączenie się z kontem usługi Azure Cosmos DB](#Connect).</span><span class="sxs-lookup"><span data-stu-id="1beb8-261">Next, in the App.config file, update the EndpointUrl and AuthorizationKey values as described in [Connect to an Azure Cosmos DB account](#Connect).</span></span>

<span data-ttu-id="1beb8-262">To wszystko — skompiluj projekt i gotowe!</span><span class="sxs-lookup"><span data-stu-id="1beb8-262">That's it, build it and you're on your way!</span></span>


## <a name="next-steps"></a><span data-ttu-id="1beb8-263">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1beb8-263">Next steps</span></span>
* <span data-ttu-id="1beb8-264">Potrzebujesz bardziej złożonego samouczka platformy ASP.NET MVC?</span><span class="sxs-lookup"><span data-stu-id="1beb8-264">Want a more complex ASP.NET MVC tutorial?</span></span> <span data-ttu-id="1beb8-265">Zobacz [samouczek programu ASP.NET MVC: opracowywanie aplikacji z bazy danych Azure rozwiązania Cosmos sieci Web](documentdb-dotnet-application.md).</span><span class="sxs-lookup"><span data-stu-id="1beb8-265">See [ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB](documentdb-dotnet-application.md).</span></span>
* <span data-ttu-id="1beb8-266">Czy chcesz wykonać testowanie wydajności i skalowania przy użyciu usługi Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="1beb8-266">Want to perform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="1beb8-267">Zobacz [wydajności i skalowania testowania z bazy danych Azure rozwiązania Cosmos](performance-testing.md)</span><span class="sxs-lookup"><span data-stu-id="1beb8-267">See [Performance and scale testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="1beb8-268">Dowiedz się, jak [monitorowanie żądań, użycia i magazynu bazy danych Azure rozwiązania Cosmos](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="1beb8-268">Learn how to [monitor Azure Cosmos DB requests, usage, and storage](monitor-accounts.md).</span></span>
* <span data-ttu-id="1beb8-269">Uruchom zapytania względem naszego przykładowego zestawu danych na [placu zabaw dla zapytań](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="1beb8-269">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="1beb8-270">Aby dowiedzieć się więcej na temat bazy danych rozwiązania Cosmos Azure, zobacz [Zapraszamy do bazy danych Azure rozwiązania Cosmos](https://docs.microsoft.com/azure/cosmos-db/introduction).</span><span class="sxs-lookup"><span data-stu-id="1beb8-270">To learn more about Azure Cosmos DB, see [Welcome to Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).</span></span>

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
[cosmos-db-create-account]: create-documentdb-dotnet.md#create-account
