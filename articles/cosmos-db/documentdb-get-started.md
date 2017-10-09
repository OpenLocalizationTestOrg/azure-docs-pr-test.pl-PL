---
title: "Azure Cosmos DB: rozpoczęcie pracy z interfejsem API usługi DocumentDB — samouczek | Microsoft Docs"
description: "Samouczek, który powoduje utworzenie bazy danych w trybie online i aplikacji konsolowej C# za pomocą hello interfejsu API usługi DocumentDB."
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
ms.openlocfilehash: 65a181f715a670987492ad7815ef2ec94498e84d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-documentdb-api-getting-started-tutorial"></a><span data-ttu-id="29139-104">Azure Cosmos DB: rozpoczęcie pracy z interfejsem API usługi DocumentDB — samouczek</span><span class="sxs-lookup"><span data-stu-id="29139-104">Azure Cosmos DB: DocumentDB API getting started tutorial</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="29139-105">.NET</span><span class="sxs-lookup"><span data-stu-id="29139-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="29139-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="29139-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="29139-107">Node.js dla MongoDB</span><span class="sxs-lookup"><span data-stu-id="29139-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="29139-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="29139-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="29139-109">Java</span><span class="sxs-lookup"><span data-stu-id="29139-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="29139-110">C++</span><span class="sxs-lookup"><span data-stu-id="29139-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="29139-111">Zapraszamy toohello interfejsu API Azure rozwiązania Cosmos bazy danych DocumentDB Samouczek wprowadzający!</span><span class="sxs-lookup"><span data-stu-id="29139-111">Welcome toohello Azure Cosmos DB DocumentDB API getting started tutorial!</span></span> <span data-ttu-id="29139-112">W ramach tego samouczka zostanie utworzona aplikacja konsolowa, która tworzy zasoby usługi Azure Cosmos DB i wykonuje dla nich zapytania.</span><span class="sxs-lookup"><span data-stu-id="29139-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="29139-113">Omówione zostaną następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="29139-113">We'll cover:</span></span>

* <span data-ttu-id="29139-114">Tworzenie i łączenie tooan konta bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="29139-114">Creating and connecting tooan Azure Cosmos DB account</span></span>
* <span data-ttu-id="29139-115">Konfigurowanie rozwiązania Visual Studio</span><span class="sxs-lookup"><span data-stu-id="29139-115">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="29139-116">Tworzenie bazy danych w trybie online</span><span class="sxs-lookup"><span data-stu-id="29139-116">Creating an online database</span></span>
* <span data-ttu-id="29139-117">Tworzenie kolekcji</span><span class="sxs-lookup"><span data-stu-id="29139-117">Creating a collection</span></span>
* <span data-ttu-id="29139-118">Tworzenie dokumentów JSON</span><span class="sxs-lookup"><span data-stu-id="29139-118">Creating JSON documents</span></span>
* <span data-ttu-id="29139-119">Wykonywanie zapytania hello kolekcji</span><span class="sxs-lookup"><span data-stu-id="29139-119">Querying hello collection</span></span>
* <span data-ttu-id="29139-120">Zastępowanie dokumentu</span><span class="sxs-lookup"><span data-stu-id="29139-120">Replacing a document</span></span>
* <span data-ttu-id="29139-121">Usuwanie dokumentu</span><span class="sxs-lookup"><span data-stu-id="29139-121">Deleting a document</span></span>
* <span data-ttu-id="29139-122">Usunięcie hello bazy danych</span><span class="sxs-lookup"><span data-stu-id="29139-122">Deleting hello database</span></span>

<span data-ttu-id="29139-123">Nie masz czasu?</span><span class="sxs-lookup"><span data-stu-id="29139-123">Don't have time?</span></span> <span data-ttu-id="29139-124">Nie martw się!</span><span class="sxs-lookup"><span data-stu-id="29139-124">Don't worry!</span></span> <span data-ttu-id="29139-125">Witaj kompletne rozwiązanie jest dostępne na [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="29139-125">hello complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span></span> <span data-ttu-id="29139-126">Przeskocz toohello [pobrać pełną sekcji rozwiązania samouczka NoSQL hello](#GetSolution) Aby uzyskać krótkie instrukcje.</span><span class="sxs-lookup"><span data-stu-id="29139-126">Jump toohello [Get hello complete NoSQL tutorial solution section](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="29139-127">Później należy głosowania hello użyj przycisków na powitania góry lub u dołu tej strony toogive nam opinii.</span><span class="sxs-lookup"><span data-stu-id="29139-127">Afterwards, please use hello voting buttons at hello top or bottom of this page toogive us feedback.</span></span> <span data-ttu-id="29139-128">Jeśli chcesz nam toocontact bezpośrednio, uważasz, że tooinclude wolnego adresu e-mail w komentarzach.</span><span class="sxs-lookup"><span data-stu-id="29139-128">If you'd like us toocontact you directly, feel free tooinclude your email address in your comments.</span></span>

<span data-ttu-id="29139-129">Teraz do dzieła!</span><span class="sxs-lookup"><span data-stu-id="29139-129">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="29139-130">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="29139-130">Prerequisites</span></span>
<span data-ttu-id="29139-131">Upewnij się, że masz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="29139-131">Please make sure you have hello following:</span></span>

* <span data-ttu-id="29139-132">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="29139-132">An active Azure account.</span></span> <span data-ttu-id="29139-133">Jeśli go nie masz, możesz zarejestrować się w celu [utworzenia bezpłatnego konta](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="29139-133">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="29139-134">Alternatywnie można użyć hello [Azure rozwiązania Cosmos DB emulatora](local-emulator.md) w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="29139-134">Alternatively, you can use hello [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="29139-135">[Visual Studio Community 2017](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="29139-135">[Visual Studio Community 2017](http://www.visualstudio.com/).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="29139-136">Krok 1. Tworzenie konta usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="29139-136">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="29139-137">Utwórzmy konto usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="29139-137">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="29139-138">Jeśli masz już konto ma toouse, możesz przejść od razu zbyt[konfigurowanie rozwiązania Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="29139-138">If you already have an account you want toouse, you can skip ahead too[Setup your Visual Studio Solution](#SetupVS).</span></span> <span data-ttu-id="29139-139">Jeśli używasz hello Azure rozwiązania Cosmos DB emulatora, należy wykonać czynności hello na [Azure rozwiązania Cosmos DB emulatora](local-emulator.md) toosetup hello emulatora i przejść od razu zbyt[konfigurowanie rozwiązania Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="29139-139">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Setup your Visual Studio Solution](#SetupVS).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="29139-140"><a id="SetupVS"></a>Krok 2. Konfigurowanie rozwiązania programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="29139-140"><a id="SetupVS"></a>Step 2: Setup your Visual Studio solution</span></span>
1. <span data-ttu-id="29139-141">Otwórz program **Visual Studio 2017** na komputerze.</span><span class="sxs-lookup"><span data-stu-id="29139-141">Open **Visual Studio 2017** on your computer.</span></span>
2. <span data-ttu-id="29139-142">Na powitania **pliku** menu, wybierz opcję **nowy**, a następnie wybierz pozycję **projektu**.</span><span class="sxs-lookup"><span data-stu-id="29139-142">On hello **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="29139-143">W hello **nowy projekt** okno dialogowe, wybierz opcję **szablony** / **Visual C#** / **aplikacji konsoli**, nazwa Projekt, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="29139-143">In hello **New Project** dialog, select **Templates** / **Visual C#** / **Console Application**, name your project, and then click **OK**.</span></span>
   <span data-ttu-id="29139-144">![Zrzut ekranu okna nowy projekt hello](./media/documentdb-get-started/nosql-tutorial-new-project-2.png)</span><span class="sxs-lookup"><span data-stu-id="29139-144">![Screen shot of hello New Project window](./media/documentdb-get-started/nosql-tutorial-new-project-2.png)</span></span>
4. <span data-ttu-id="29139-145">W hello **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy nową aplikację konsolową, która znajduje się w obrębie rozwiązania Visual Studio, a następnie kliknij przycisk **Zarządzaj pakietami NuGet...**</span><span class="sxs-lookup"><span data-stu-id="29139-145">In hello **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
    
    ![Zrzut ekranu przedstawiający hello prawo kliknięto element Menu hello projektu](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges.png)
5. <span data-ttu-id="29139-147">W hello **Nuget** , kliknij pozycję **Przeglądaj**i wpisz **usługa azure documentdb** hello pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="29139-147">In hello **Nuget** tab, click **Browse**, and type **azure documentdb** in hello search box.</span></span>
6. <span data-ttu-id="29139-148">W wynikach hello znaleźć **Microsoft.Azure.DocumentDB** i kliknij przycisk **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="29139-148">Within hello results, find **Microsoft.Azure.DocumentDB** and click **Install**.</span></span>
   <span data-ttu-id="29139-149">Identyfikator pakietu Hello hello biblioteki klienta interfejsu API Azure rozwiązania Cosmos bazy danych usługi DocumentDB jest [Biblioteka kliencka usługi Microsoft Azure DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/).</span><span class="sxs-lookup"><span data-stu-id="29139-149">hello package ID for hello Azure Cosmos DB DocumentDB API Client Library is [Microsoft Azure DocumentDB Client Library](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/).</span></span>
   <span data-ttu-id="29139-150">![Zrzut ekranu przedstawiający hello Nuget Menu do znajdowania zestawu SDK klienta usługi Azure rozwiązania Cosmos bazy danych](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)</span><span class="sxs-lookup"><span data-stu-id="29139-150">![Screen shot of hello Nuget Menu for finding Azure Cosmos DB Client SDK](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)</span></span>

    <span data-ttu-id="29139-151">Jeśli komunikaty o przegląd zmian toohello rozwiązania, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="29139-151">If you get a messages about reviewing changes toohello solution, click **OK**.</span></span> <span data-ttu-id="29139-152">Jeśli wyświetlany jest komunikat o akceptacji licencji, kliknij pozycję **Akceptuję**.</span><span class="sxs-lookup"><span data-stu-id="29139-152">If you get a message about license acceptance, click **I accept**.</span></span>

<span data-ttu-id="29139-153">Wspaniale!</span><span class="sxs-lookup"><span data-stu-id="29139-153">Great!</span></span> <span data-ttu-id="29139-154">Teraz, gdy zakończeniu hello instalacji, Zacznijmy pisanie kodu.</span><span class="sxs-lookup"><span data-stu-id="29139-154">Now that we finished hello setup, let's start writing some code.</span></span> <span data-ttu-id="29139-155">Ukończony projekt kodu z tego samouczka można znaleźć w witrynie [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="29139-155">You can find a completed code project of this tutorial at [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs).</span></span>

## <span data-ttu-id="29139-156"><a id="Connect"></a>Krok 3: Łączenie tooan konta bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="29139-156"><a id="Connect"></a>Step 3: Connect tooan Azure Cosmos DB account</span></span>
<span data-ttu-id="29139-157">Najpierw dodaj te odwołania toohello początku aplikacji C#, w pliku Program.cs hello:</span><span class="sxs-lookup"><span data-stu-id="29139-157">First, add these references toohello beginning of your C# application, in hello Program.cs file:</span></span>

    using System;
    using System.Linq;
    using System.Threading.Tasks;

    // ADD THIS PART tooYOUR CODE
    using System.Net;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Newtonsoft.Json;

> [!IMPORTANT]
> <span data-ttu-id="29139-158">W samouczku hello toocomplete kolejności upewnij się, że możesz dodać hello zależności powyżej.</span><span class="sxs-lookup"><span data-stu-id="29139-158">In order toocomplete hello tutorial, make sure you add hello dependencies above.</span></span>
> 
> 

<span data-ttu-id="29139-159">Dodaj teraz te dwie stałe i zmienną *client* poniżej klasy publicznej *Program*.</span><span class="sxs-lookup"><span data-stu-id="29139-159">Now, add these two constants and your *client* variable underneath your public class *Program*.</span></span>

    public class Program
    {
        // ADD THIS PART tooYOUR CODE
        private const string EndpointUrl = "<your endpoint URL>";
        private const string PrimaryKey = "<your primary key>";
        private DocumentClient client;

<span data-ttu-id="29139-160">Następnie head kopii toohello [Azure Portal](https://portal.azure.com) tooretrieve Twojego adresu URL punktu końcowego i klucz podstawowy.</span><span class="sxs-lookup"><span data-stu-id="29139-160">Next, head back toohello [Azure Portal](https://portal.azure.com) tooretrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="29139-161">adres URL punktu końcowego Hello i klucza podstawowego są niezbędne do Twojej aplikacji toounderstand gdzie tooconnect na oraz bazy danych Azure rozwiązania Cosmos tootrust połączeniu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="29139-161">hello endpoint URL and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span>

<span data-ttu-id="29139-162">W hello portalu Azure, przejdź do konta bazy danych Azure rozwiązania Cosmos tooyour, a następnie kliknij **klucze**.</span><span class="sxs-lookup"><span data-stu-id="29139-162">In hello Azure Portal, navigate tooyour Azure Cosmos DB account, and then click **Keys**.</span></span>

<span data-ttu-id="29139-163">Skopiuj hello identyfikatora URI z portalu hello i wklej ją do `<your endpoint URL>` w pliku program.cs hello.</span><span class="sxs-lookup"><span data-stu-id="29139-163">Copy hello URI from hello portal and paste it into `<your endpoint URL>` in hello program.cs file.</span></span> <span data-ttu-id="29139-164">Następnie kopiowania hello klucza podstawowego z portalu hello i wklej ją do `<your primary key>`.</span><span class="sxs-lookup"><span data-stu-id="29139-164">Then copy hello PRIMARY KEY from hello portal and paste it into `<your primary key>`.</span></span>

![Zrzut ekranu przedstawiający hello Portal Azure używany przez hello toocreate samouczka NoSQL aplikacji konsolowej C#.][keys]

<span data-ttu-id="29139-167">Następnie Zaczniemy aplikacji hello, tworząc nowe wystąpienie klasy hello **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="29139-167">Next, we'll start hello application by creating a new instance of hello **DocumentClient**.</span></span>

<span data-ttu-id="29139-168">Poniżej hello **Main** metody, dodaj to nowe zadanie asynchroniczne o nazwie **GetStartedDemo**, które zostaną nowe wystąpienie klasy **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="29139-168">Below hello **Main** method, add this new asynchronous task called **GetStartedDemo**, which will instantiate our new **DocumentClient**.</span></span>

    static void Main(string[] args)
    {
    }

    // ADD THIS PART tooYOUR CODE
    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);
    }

<span data-ttu-id="29139-169">Dodaj hello poniższy kod toorun zadania asynchronicznego z Twojej **Main** metody.</span><span class="sxs-lookup"><span data-stu-id="29139-169">Add hello following code toorun your asynchronous task from your **Main** method.</span></span> <span data-ttu-id="29139-170">Witaj **Main** metoda będzie przechwytywać wyjątki i zapisywać je toohello konsoli.</span><span class="sxs-lookup"><span data-stu-id="29139-170">hello **Main** method will catch exceptions and write them toohello console.</span></span>

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

<span data-ttu-id="29139-171">Naciśnij klawisz **F5** toorun aplikacji.</span><span class="sxs-lookup"><span data-stu-id="29139-171">Press **F5** toorun your application.</span></span> <span data-ttu-id="29139-172">dane wyjściowe z okna konsoli Hello wyświetla wiadomość hello `End of demo, press any key tooexit.` potwierdzenie, że nawiązano połączenie hello.</span><span class="sxs-lookup"><span data-stu-id="29139-172">hello console window output displays hello message `End of demo, press any key tooexit.` confirming that hello connection was made.</span></span>  <span data-ttu-id="29139-173">Następnie możesz zamknąć hello okna konsoli.</span><span class="sxs-lookup"><span data-stu-id="29139-173">You can then close hello console window.</span></span> 

<span data-ttu-id="29139-174">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="29139-174">Congratulations!</span></span> <span data-ttu-id="29139-175">Pomyślnie nawiązano połączenie konto bazy danych Azure rozwiązania Cosmos tooan, teraz Spójrzmy w pracy z zasobami Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="29139-175">You have successfully connected tooan Azure Cosmos DB account, let's now take a look at working with Azure Cosmos DB resources.</span></span>  

## <a name="step-4-create-a-database"></a><span data-ttu-id="29139-176">Krok 4. Tworzenie bazy danych</span><span class="sxs-lookup"><span data-stu-id="29139-176">Step 4: Create a database</span></span>
<span data-ttu-id="29139-177">Przed dodaniem hello kod służący do tworzenia bazy danych Dodaj metodę pomocnika na potrzeby zapisywania toohello konsoli.</span><span class="sxs-lookup"><span data-stu-id="29139-177">Before you add hello code for creating a database, add a helper method for writing toohello console.</span></span>

<span data-ttu-id="29139-178">Skopiuj i Wklej hello **WriteToConsoleAndPromptToContinue** metody po hello **GetStartedDemo** metody.</span><span class="sxs-lookup"><span data-stu-id="29139-178">Copy and paste hello **WriteToConsoleAndPromptToContinue** method after hello **GetStartedDemo** method.</span></span>

    // ADD THIS PART tooYOUR CODE
    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
            Console.WriteLine(format, args);
            Console.WriteLine("Press any key toocontinue ...");
            Console.ReadKey();
    }

<span data-ttu-id="29139-179">Bazy danych programu Azure rozwiązania Cosmos [bazy danych](documentdb-resources.md#databases) można tworzyć przy użyciu hello [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) metody hello **DocumentClient** klasy.</span><span class="sxs-lookup"><span data-stu-id="29139-179">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using hello [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="29139-180">Baza danych jest hello kontenerem logicznym magazynu dokumentów JSON podzielonym na partycje w kolekcjach.</span><span class="sxs-lookup"><span data-stu-id="29139-180">A database is hello logical container of JSON document storage partitioned across collections.</span></span>

<span data-ttu-id="29139-181">Kopiuj i wklej następujący hello kodu tooyour **GetStartedDemo** metody utworzoną powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="29139-181">Copy and paste hello following code tooyour **GetStartedDemo** method after hello client creation.</span></span> <span data-ttu-id="29139-182">Spowoduje to utworzenie bazy danych o nazwie *FamilyDB*.</span><span class="sxs-lookup"><span data-stu-id="29139-182">This will create a database named *FamilyDB*.</span></span>

    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        // ADD THIS PART tooYOUR CODE
        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

<span data-ttu-id="29139-183">Naciśnij klawisz **F5** toorun aplikacji.</span><span class="sxs-lookup"><span data-stu-id="29139-183">Press **F5** toorun your application.</span></span>

<span data-ttu-id="29139-184">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="29139-184">Congratulations!</span></span> <span data-ttu-id="29139-185">Pomyślnie utworzono bazę danych usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="29139-185">You have successfully created an Azure Cosmos DB database.</span></span>  

## <span data-ttu-id="29139-186"><a id="CreateColl"></a>Krok 5. Tworzenie kolekcji</span><span class="sxs-lookup"><span data-stu-id="29139-186"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="29139-187">Za pomocą metody **CreateDocumentCollectionIfNotExistsAsync** zostanie utworzona nowa kolekcja z zarezerwowaną przepływnością, co ma wpływ na cenę.</span><span class="sxs-lookup"><span data-stu-id="29139-187">**CreateDocumentCollectionIfNotExistsAsync** will create a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="29139-188">Aby uzyskać więcej informacji, odwiedź naszą [stronę cennika](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="29139-188">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="29139-189">A [kolekcji](documentdb-resources.md#collections) można tworzyć przy użyciu hello [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) metody hello **DocumentClient** klasy.</span><span class="sxs-lookup"><span data-stu-id="29139-189">A [collection](documentdb-resources.md#collections) can be created by using hello [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="29139-190">Kolekcja jest kontenerem dokumentów JSON i skojarzonej logiki aplikacji JavaScript.</span><span class="sxs-lookup"><span data-stu-id="29139-190">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="29139-191">Kopiuj i wklej następujący hello kodu tooyour **GetStartedDemo** metody po utworzeniu bazy danych hello.</span><span class="sxs-lookup"><span data-stu-id="29139-191">Copy and paste hello following code tooyour **GetStartedDemo** method after hello database creation.</span></span> <span data-ttu-id="29139-192">Spowoduje to utworzenie kolekcji dokumentów o nazwie *FamilyCollection*.</span><span class="sxs-lookup"><span data-stu-id="29139-192">This will create a document collection named *FamilyCollection*.</span></span>

        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

        // ADD THIS PART tooYOUR CODE
         await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });

<span data-ttu-id="29139-193">Naciśnij klawisz **F5** toorun aplikacji.</span><span class="sxs-lookup"><span data-stu-id="29139-193">Press **F5** toorun your application.</span></span>

<span data-ttu-id="29139-194">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="29139-194">Congratulations!</span></span> <span data-ttu-id="29139-195">Pomyślnie utworzono kolekcję dokumentów Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="29139-195">You have successfully created an Azure Cosmos DB document collection.</span></span>  

## <span data-ttu-id="29139-196"><a id="CreateDoc"></a>Krok 6. Tworzenie dokumentów JSON</span><span class="sxs-lookup"><span data-stu-id="29139-196"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="29139-197">A [dokumentu](documentdb-resources.md#documents) można tworzyć przy użyciu hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) metody hello **DocumentClient** klasy.</span><span class="sxs-lookup"><span data-stu-id="29139-197">A [document](documentdb-resources.md#documents) can be created by using hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="29139-198">Dokumenty są zawartością JSON zdefiniowaną przez użytkownika (dowolną).</span><span class="sxs-lookup"><span data-stu-id="29139-198">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="29139-199">Można teraz wstawić jeden lub więcej dokumentów.</span><span class="sxs-lookup"><span data-stu-id="29139-199">We can now insert one or more documents.</span></span> <span data-ttu-id="29139-200">Jeśli masz już dane, które chcesz toostore w bazie danych, możesz użyć hello Azure DB rozwiązania Cosmos [narzędzia migracji danych](import-data.md) tooimport hello danych do bazy danych.</span><span class="sxs-lookup"><span data-stu-id="29139-200">If you already have data you'd like toostore in your database, you can use hello Azure Cosmos DB [Data Migration tool](import-data.md) tooimport hello data into a database.</span></span>

<span data-ttu-id="29139-201">Najpierw należy toocreate **rodziny** klasy, która będzie reprezentowała obiekty przechowywane w usłudze Azure DB rozwiązania Cosmos w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="29139-201">First, we need toocreate a **Family** class that will represent objects stored within Azure Cosmos DB in this sample.</span></span> <span data-ttu-id="29139-202">Zostaną również utworzone podklasy **Parent**, **Child**, **Pet** i **Address**, które są używane w ramach klasy **Family**.</span><span class="sxs-lookup"><span data-stu-id="29139-202">We will also create **Parent**, **Child**, **Pet**, **Address** subclasses that are used within **Family**.</span></span> <span data-ttu-id="29139-203">Należy pamiętać, że dokumenty muszą mieć właściwość **Id** serializowaną jako **id** w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="29139-203">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span> <span data-ttu-id="29139-204">Utwórz te klasy, dodając następujące podklasy wewnętrzne po hello hello **GetStartedDemo** metody.</span><span class="sxs-lookup"><span data-stu-id="29139-204">Create these classes by adding hello following internal sub-classes after hello **GetStartedDemo** method.</span></span>

<span data-ttu-id="29139-205">Skopiuj i Wklej hello **rodziny**, **nadrzędnej**, **podrzędnych**, **Pet**, i **adres** klasy po hello **WriteToConsoleAndPromptToContinue** metody.</span><span class="sxs-lookup"><span data-stu-id="29139-205">Copy and paste hello **Family**, **Parent**, **Child**, **Pet**, and **Address** classes after hello **WriteToConsoleAndPromptToContinue** method.</span></span>

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

<span data-ttu-id="29139-206">Skopiuj i Wklej hello **CreateFamilyDocumentIfNotExists** poniżej metody z **adres** klasy.</span><span class="sxs-lookup"><span data-stu-id="29139-206">Copy and paste hello **CreateFamilyDocumentIfNotExists** method underneath your **Address** class.</span></span>

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

<span data-ttu-id="29139-207">I Wstaw dwa dokumenty, jeden dla rodziny Andersen hello i hello rodziny Wakefield.</span><span class="sxs-lookup"><span data-stu-id="29139-207">And insert two documents, one each for hello Andersen Family and hello Wakefield Family.</span></span>

<span data-ttu-id="29139-208">Kopiuj i wklej następujący hello kodu tooyour **GetStartedDemo** metody po utworzeniu kolekcji dokumentów hello.</span><span class="sxs-lookup"><span data-stu-id="29139-208">Copy and paste hello following code tooyour **GetStartedDemo** method after hello document collection creation.</span></span>

    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });
    
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });


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

<span data-ttu-id="29139-209">Naciśnij klawisz **F5** toorun aplikacji.</span><span class="sxs-lookup"><span data-stu-id="29139-209">Press **F5** toorun your application.</span></span>

<span data-ttu-id="29139-210">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="29139-210">Congratulations!</span></span> <span data-ttu-id="29139-211">Pomyślnie utworzono dwa dokumenty usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="29139-211">You have successfully created two Azure Cosmos DB documents.</span></span>  

![Diagram ilustrujący hello hierarchiczną relację między hello konta, baza danych online hello hello kolekcji i hello dokumentami używanymi przez hello toocreate samouczka NoSQL aplikacji konsolowej C#](./media/documentdb-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="29139-213"><a id="Query"></a>Krok 7. Wykonanie zapytania względem zasobów usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="29139-213"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="29139-214">Usługa Azure Cosmos DB obsługuje zaawansowane [zapytania](documentdb-sql-query.md) względem dokumentów JSON przechowywanych w każdej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="29139-214">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="29139-215">Witaj następujący przykładowy kod przedstawia różne zapytania — przy użyciu obu Azure rozwiązania Cosmos bazy danych SQL składnię, a także LINQ — które można uruchomić względem hello dokumenty, które firma Microsoft wstawione w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="29139-215">hello following sample code shows various queries - using both Azure Cosmos DB SQL syntax as well as LINQ - that we can run against hello documents we inserted in hello previous step.</span></span>

<span data-ttu-id="29139-216">Skopiuj i Wklej hello **ExecuteSimpleQuery** metody po Twoje **CreateFamilyDocumentIfNotExists** metody.</span><span class="sxs-lookup"><span data-stu-id="29139-216">Copy and paste hello **ExecuteSimpleQuery** method after your **CreateFamilyDocumentIfNotExists** method.</span></span>

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

<span data-ttu-id="29139-217">Kopiuj i wklej następujący hello kodu tooyour **GetStartedDemo** metody po tworzenia drugiego dokumentu hello.</span><span class="sxs-lookup"><span data-stu-id="29139-217">Copy and paste hello following code tooyour **GetStartedDemo** method after hello second document creation.</span></span>

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    // ADD THIS PART tooYOUR CODE
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

<span data-ttu-id="29139-218">Naciśnij klawisz **F5** toorun aplikacji.</span><span class="sxs-lookup"><span data-stu-id="29139-218">Press **F5** toorun your application.</span></span>

<span data-ttu-id="29139-219">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="29139-219">Congratulations!</span></span> <span data-ttu-id="29139-220">Pomyślnie wykonano zapytanie względem kolekcji usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="29139-220">You have successfully queried against an Azure Cosmos DB collection.</span></span>

<span data-ttu-id="29139-221">Witaj poniższym diagramie przedstawiono sposób hello Azure rozwiązania Cosmos DB kwerend SQL składni jest wywoływana względem kolekcji hello utworzony i hello sama logika dotyczy również zapytania LINQ toohello.</span><span class="sxs-lookup"><span data-stu-id="29139-221">hello following diagram illustrates how hello Azure Cosmos DB SQL query syntax is called against hello collection you created, and hello same logic applies toohello LINQ query as well.</span></span>

![Diagram pokazujący hello zakres i znaczenie zapytania hello używane przez toocreate samouczka NoSQL hello aplikacji konsolowej C#](./media/documentdb-get-started/nosql-tutorial-collection-documents.png)

<span data-ttu-id="29139-223">Witaj [FROM](documentdb-sql-query.md#FromClause) — słowo kluczowe jest opcjonalna w hello zapytania, ponieważ zapytania bazy danych Azure rozwiązania Cosmos jest już tooa zakresie jednej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="29139-223">hello [FROM](documentdb-sql-query.md#FromClause) keyword is optional in hello query because Azure Cosmos DB queries are already scoped tooa single collection.</span></span> <span data-ttu-id="29139-224">W związku z tym klauzula "FROM Families f" może być zamieniona na "FROM root r" lub dowolną inną wybraną nazwę zmiennej.</span><span class="sxs-lookup"><span data-stu-id="29139-224">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="29139-225">Azure DB rozwiązania Cosmos wywnioskuje rodziny, root lub nazwę zmiennej hello wybrane, odwołanie do bieżącej kolekcji hello domyślnie.</span><span class="sxs-lookup"><span data-stu-id="29139-225">Azure Cosmos DB will infer that Families, root, or hello variable name you chose, reference hello current collection by default.</span></span>

## <span data-ttu-id="29139-226"><a id="ReplaceDocument"></a>Krok 8. Zastępowanie dokumentu JSON</span><span class="sxs-lookup"><span data-stu-id="29139-226"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="29139-227">Usługa Azure Cosmos DB obsługuje zastępowanie dokumentów JSON.</span><span class="sxs-lookup"><span data-stu-id="29139-227">Azure Cosmos DB supports replacing JSON documents.</span></span>  

<span data-ttu-id="29139-228">Skopiuj i Wklej hello **ReplaceFamilyDocument** metody po Twoje **ExecuteSimpleQuery** metody.</span><span class="sxs-lookup"><span data-stu-id="29139-228">Copy and paste hello **ReplaceFamilyDocument** method after your **ExecuteSimpleQuery** method.</span></span>

    // ADD THIS PART tooYOUR CODE
    private async Task ReplaceFamilyDocument(string databaseName, string collectionName, string familyName, Family updatedFamily)
    {
         await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, familyName), updatedFamily);
         this.WriteToConsoleAndPromptToContinue("Replaced Family {0}", familyName);
    }

<span data-ttu-id="29139-229">Kopiuj i wklej następujący hello kodu tooyour **GetStartedDemo** metody po wykonaniu zapytania hello na końcu hello hello metody.</span><span class="sxs-lookup"><span data-stu-id="29139-229">Copy and paste hello following code tooyour **GetStartedDemo** method after hello query execution, at hello end of hello method.</span></span> <span data-ttu-id="29139-230">Po zastąpieniu dokumentu hello, spowoduje to uruchomienie hello sam ponowne przesłanie zapytania tooview hello zmieniony dokument.</span><span class="sxs-lookup"><span data-stu-id="29139-230">After replacing hello document, this will run hello same query again tooview hello changed document.</span></span>

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    // ADD THIS PART tooYOUR CODE
    // Update hello Grade of hello Andersen Family child
    andersenFamily.Children[0].Grade = 6;

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

<span data-ttu-id="29139-231">Naciśnij klawisz **F5** toorun aplikacji.</span><span class="sxs-lookup"><span data-stu-id="29139-231">Press **F5** toorun your application.</span></span>

<span data-ttu-id="29139-232">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="29139-232">Congratulations!</span></span> <span data-ttu-id="29139-233">Pomyślnie zastąpiono dokument usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="29139-233">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="29139-234"><a id="DeleteDocument"></a>Krok 9. Usuwanie dokumentu JSON</span><span class="sxs-lookup"><span data-stu-id="29139-234"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="29139-235">Usługa Azure Cosmos DB obsługuje usuwanie dokumentów JSON.</span><span class="sxs-lookup"><span data-stu-id="29139-235">Azure Cosmos DB supports deleting JSON documents.</span></span>  

<span data-ttu-id="29139-236">Skopiuj i Wklej hello **DeleteFamilyDocument** metody po Twoje **ReplaceFamilyDocument** metody.</span><span class="sxs-lookup"><span data-stu-id="29139-236">Copy and paste hello **DeleteFamilyDocument** method after your **ReplaceFamilyDocument** method.</span></span>

    // ADD THIS PART tooYOUR CODE
    private async Task DeleteFamilyDocument(string databaseName, string collectionName, string documentName)
    {
         await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName));
         Console.WriteLine("Deleted Family {0}", documentName);
    }

<span data-ttu-id="29139-237">Kopiuj i wklej następujący hello kodu tooyour **GetStartedDemo** metody po hello drugiego wykonywania zapytania, na końcu hello hello metody.</span><span class="sxs-lookup"><span data-stu-id="29139-237">Copy and paste hello following code tooyour **GetStartedDemo** method after hello second query execution, at hello end of hello method.</span></span>

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);
    
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");
    
    // ADD THIS PART tooCODE
    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

<span data-ttu-id="29139-238">Naciśnij klawisz **F5** toorun aplikacji.</span><span class="sxs-lookup"><span data-stu-id="29139-238">Press **F5** toorun your application.</span></span>

<span data-ttu-id="29139-239">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="29139-239">Congratulations!</span></span> <span data-ttu-id="29139-240">Pomyślnie usunięto dokument usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="29139-240">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="29139-241"><a id="DeleteDatabase"></a>Krok 10: Usuwanie hello bazy danych</span><span class="sxs-lookup"><span data-stu-id="29139-241"><a id="DeleteDatabase"></a>Step 10: Delete hello database</span></span>
<span data-ttu-id="29139-242">Trwa usuwanie hello utworzył bazę danych spowoduje usunięcie hello bazy danych i wszystkich zasobów podrzędnych (kolekcji, dokumentów itd.).</span><span class="sxs-lookup"><span data-stu-id="29139-242">Deleting hello created database will remove hello database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="29139-243">Kopiuj i wklej następujący hello kodu tooyour **GetStartedDemo** metody po dokumentu hello usunąć toodelete hello całą bazę danych i wszystkie zasoby podrzędne.</span><span class="sxs-lookup"><span data-stu-id="29139-243">Copy and paste hello following code tooyour **GetStartedDemo** method after hello document delete toodelete hello entire database and all children resources.</span></span>

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

    // ADD THIS PART tooCODE
    // Clean up/delete hello database
    await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB"));

<span data-ttu-id="29139-244">Naciśnij klawisz **F5** toorun aplikacji.</span><span class="sxs-lookup"><span data-stu-id="29139-244">Press **F5** toorun your application.</span></span>

<span data-ttu-id="29139-245">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="29139-245">Congratulations!</span></span> <span data-ttu-id="29139-246">Pomyślnie usunięto bazę danych usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="29139-246">You have successfully deleted an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="29139-247"><a id="Run"></a>Krok 11. Uruchamianie całej aplikacji konsolowej C#</span><span class="sxs-lookup"><span data-stu-id="29139-247"><a id="Run"></a>Step 11: Run your C# console application all together!</span></span>
<span data-ttu-id="29139-248">Naciśnij klawisz F5 w programie Visual Studio toobuild hello aplikacji w trybie debugowania.</span><span class="sxs-lookup"><span data-stu-id="29139-248">Hit F5 in Visual Studio toobuild hello application in debug mode.</span></span>

<span data-ttu-id="29139-249">Powinny pojawić się hello dane wyjściowe aplikacji rozpoczynania pracy w oknie konsoli.</span><span class="sxs-lookup"><span data-stu-id="29139-249">You should see hello output of your get started app in a console window.</span></span> <span data-ttu-id="29139-250">Witaj dane wyjściowe będą pokazywały wyniki hello hello dodanych zapytań i powinny odpowiadać tekstowi przykładu hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="29139-250">hello output will show hello results of hello queries we added and should match hello example text below.</span></span>

    Created FamilyDB
    Press any key toocontinue ...
    Created FamilyCollection
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

<span data-ttu-id="29139-251">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="29139-251">Congratulations!</span></span> <span data-ttu-id="29139-252">Po ukończeniu samouczka hello i mieć pracy aplikacji konsolowej C#!</span><span class="sxs-lookup"><span data-stu-id="29139-252">You've completed hello tutorial and have a working C# console application!</span></span>

## <span data-ttu-id="29139-253"><a id="GetSolution"></a>Pobierz hello kompletnego rozwiązania samouczka</span><span class="sxs-lookup"><span data-stu-id="29139-253"><a id="GetSolution"></a> Get hello complete tutorial solution</span></span>
<span data-ttu-id="29139-254">Jeśli nie masz czasu toocomplete hello kroków w tym samouczku lub po prostu chcesz toodownload hello przykłady kodu, możesz pobrać go z [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="29139-254">If you didn't have time toocomplete hello steps in this tutorial, or just want toodownload hello code samples, you can get it from [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span></span> 

<span data-ttu-id="29139-255">rozwiązania GetStarted hello toobuild, potrzebne są następujące hello:</span><span class="sxs-lookup"><span data-stu-id="29139-255">toobuild hello GetStarted solution, you will need hello following:</span></span>

* <span data-ttu-id="29139-256">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="29139-256">An active Azure account.</span></span> <span data-ttu-id="29139-257">Jeśli go nie masz, możesz zarejestrować się w celu [utworzenia bezpłatnego konta](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="29139-257">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="29139-258">[Konta bazy danych Azure rozwiązania Cosmos][cosmos-db-create-account].</span><span class="sxs-lookup"><span data-stu-id="29139-258">An [Azure Cosmos DB account][cosmos-db-create-account].</span></span>
* <span data-ttu-id="29139-259">Witaj [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) rozwiązanie jest dostępne w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="29139-259">hello [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="29139-260">toorestore hello odwołania toohello zestawu SDK .NET DB rozwiązania Cosmos Azure w programie Visual Studio, kliknij prawym przyciskiem myszy hello **GetStarted** rozwiązania w Eksploratorze rozwiązań, a następnie kliknij przycisk **Włącz Przywracanie pakietu NuGet**.</span><span class="sxs-lookup"><span data-stu-id="29139-260">toorestore hello references toohello Azure Cosmos DB .NET SDK in Visual Studio, right-click hello **GetStarted** solution in Solution Explorer, and then click **Enable NuGet Package Restore**.</span></span> <span data-ttu-id="29139-261">Następnie w pliku App.config hello, zaktualizuj wartości EndpointUrl i AuthorizationKey hello zgodnie z opisem w [połączyć konto bazy danych Azure rozwiązania Cosmos tooan](#Connect).</span><span class="sxs-lookup"><span data-stu-id="29139-261">Next, in hello App.config file, update hello EndpointUrl and AuthorizationKey values as described in [Connect tooan Azure Cosmos DB account](#Connect).</span></span>

<span data-ttu-id="29139-262">To wszystko — skompiluj projekt i gotowe!</span><span class="sxs-lookup"><span data-stu-id="29139-262">That's it, build it and you're on your way!</span></span>


## <a name="next-steps"></a><span data-ttu-id="29139-263">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="29139-263">Next steps</span></span>
* <span data-ttu-id="29139-264">Potrzebujesz bardziej złożonego samouczka platformy ASP.NET MVC?</span><span class="sxs-lookup"><span data-stu-id="29139-264">Want a more complex ASP.NET MVC tutorial?</span></span> <span data-ttu-id="29139-265">Zobacz [samouczek programu ASP.NET MVC: opracowywanie aplikacji z bazy danych Azure rozwiązania Cosmos sieci Web](documentdb-dotnet-application.md).</span><span class="sxs-lookup"><span data-stu-id="29139-265">See [ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB](documentdb-dotnet-application.md).</span></span>
* <span data-ttu-id="29139-266">Chcesz testowanie z bazy danych Azure rozwiązania Cosmos wydajności i skalowania tooperform?</span><span class="sxs-lookup"><span data-stu-id="29139-266">Want tooperform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="29139-267">Zobacz [wydajności i skalowania testowania z bazy danych Azure rozwiązania Cosmos](performance-testing.md)</span><span class="sxs-lookup"><span data-stu-id="29139-267">See [Performance and scale testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="29139-268">Dowiedz się, jak za[monitorowanie żądań, użycia i magazynu bazy danych Azure rozwiązania Cosmos](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="29139-268">Learn how too[monitor Azure Cosmos DB requests, usage, and storage](monitor-accounts.md).</span></span>
* <span data-ttu-id="29139-269">Uruchom zapytania względem naszego przykładowego zestawu danych w hello [Plac zabaw dla zapytań](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="29139-269">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="29139-270">toolearn więcej informacji na temat bazy danych rozwiązania Cosmos platformy Azure, zobacz [Witamy tooAzure DB rozwiązania Cosmos](https://docs.microsoft.com/azure/cosmos-db/introduction).</span><span class="sxs-lookup"><span data-stu-id="29139-270">toolearn more about Azure Cosmos DB, see [Welcome tooAzure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).</span></span>

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
[cosmos-db-create-account]: create-documentdb-dotnet.md#create-account
