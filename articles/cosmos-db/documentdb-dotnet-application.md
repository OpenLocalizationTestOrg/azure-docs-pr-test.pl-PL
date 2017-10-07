---
title: "Samouczek platformy ASP.NET MVC dla usługi Azure Cosmos DB: opracowywanie aplikacji internetowych | Microsoft Docs"
description: "Samouczek platformy ASP.NET MVC toocreate aplikacji sieci web MVC przy użyciu bazy danych Azure rozwiązania Cosmos. Zapiszesz dane w postaci kodu JSON i uzyskasz do nich dostęp za pomocą aplikacji listy rzeczy do zrobienia hostowanej w usłudze Azure Websites — szczegółowy samouczek dla platformy ASP.NET MVC."
keywords: samouczek asp.net mvc, programowanie aplikacji sieci web, aplikacja sieci web mvc, samouczek krok po kroku asp.net mvc
services: cosmos-db
documentationcenter: .net
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 52532d89-a40e-4fdf-9b38-aadb3a4cccbc
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/03/2017
ms.author: mimig
ms.openlocfilehash: dac2a9599b395524533e6fe14983789ff095331f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="eefa6-105"><a name="_Toc395809351"></a>Samouczek platformy ASP.NET MVC: Opracowywanie aplikacji internetowych za pomocą usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="eefa6-105"><a name="_Toc395809351"></a>ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="eefa6-106">.NET</span><span class="sxs-lookup"><span data-stu-id="eefa6-106">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="eefa6-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="eefa6-107">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="eefa6-108">Java</span><span class="sxs-lookup"><span data-stu-id="eefa6-108">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="eefa6-109">Python</span><span class="sxs-lookup"><span data-stu-id="eefa6-109">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="eefa6-110">toohighlight sposób mogą efektywnie korzystać z bazy danych Azure rozwiązania Cosmos toostore i wykonywać zapytania dokumentów JSON, w tym artykule przedstawiono end-to-end Przewodnik jak toobuild aplikacji todo, przy użyciu bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="eefa6-110">toohighlight how you can efficiently leverage Azure Cosmos DB toostore and query JSON documents, this article provides an end-to-end walk-through showing you how toobuild a todo app using Azure Cosmos DB.</span></span> <span data-ttu-id="eefa6-111">Witaj zadania będą przechowywane jako dokumenty JSON w usłudze Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="eefa6-111">hello tasks will be stored as JSON documents in Azure Cosmos DB.</span></span>

![Zrzut ekranu: Lista czynności do wykonania hello aplikacji sieci web MVC utworzone przez tego samouczka — samouczek platformy Asp.net MVC ASP krok po kroku](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-image01.png)

<span data-ttu-id="eefa6-113">Ten przewodnik przedstawia, jak toouse hello Azure DB rozwiązania Cosmos usługi toostore i danymi dostępu z aplikacji sieci web platformy ASP.NET MVC hostowanej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="eefa6-113">This walk-through shows you how toouse hello Azure Cosmos DB service toostore and access data from an ASP.NET MVC web application hosted on Azure.</span></span> <span data-ttu-id="eefa6-114">Jeśli szukasz samouczka, który koncentruje się tylko dla bazy danych rozwiązania Cosmos Azure, a nie hello ASP.NET MVC, zobacz [tworzenie aplikacji konsoli Azure rozwiązania Cosmos DB C#](documentdb-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="eefa6-114">If you're looking for a tutorial that focuses only on Azure Cosmos DB, and not hello ASP.NET MVC components, see [Build an Azure Cosmos DB C# console application](documentdb-get-started.md).</span></span>

> [!TIP]
> <span data-ttu-id="eefa6-115">Ten samouczek zakłada, że masz już pewne doświadczenie w korzystaniu z platformy ASP.NET MVC i usługi Azure Websites.</span><span class="sxs-lookup"><span data-stu-id="eefa6-115">This tutorial assumes that you have prior experience using ASP.NET MVC and Azure Websites.</span></span> <span data-ttu-id="eefa6-116">W przypadku nowych tooASP.NET lub hello [wstępnie wymaganych narzędzi](#_Toc395637760), zalecamy pobranie hello kompletnego przykładowego projektu z [GitHub] [ GitHub] i instrukcjami hello w w przykładzie.</span><span class="sxs-lookup"><span data-stu-id="eefa6-116">If you are new tooASP.NET or hello [prerequisite tools](#_Toc395637760), we recommend downloading hello complete sample project from [GitHub][GitHub] and following hello instructions in this sample.</span></span> <span data-ttu-id="eefa6-117">Po jego skompilowaniu, możesz przejrzeć ten artykuł wglądu toogain na powitania kod w kontekście hello hello projektu.</span><span class="sxs-lookup"><span data-stu-id="eefa6-117">Once you have it built, you can review this article toogain insight on hello code in hello context of hello project.</span></span>
> 
> 

## <span data-ttu-id="eefa6-118"><a name="_Toc395637760"></a>Wymagania wstępne dotyczące tego samouczka bazy danych</span><span class="sxs-lookup"><span data-stu-id="eefa6-118"><a name="_Toc395637760"></a>Prerequisites for this database tutorial</span></span>
<span data-ttu-id="eefa6-119">Przed rozpoczęciem powitalne instrukcje w tym artykule, należy upewnij się, że masz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="eefa6-119">Before following hello instructions in this article, you should ensure that you have hello following:</span></span>

* <span data-ttu-id="eefa6-120">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="eefa6-120">An active Azure account.</span></span> <span data-ttu-id="eefa6-121">Jeśli jej nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="eefa6-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="eefa6-122">Aby uzyskać szczegółowe informacje, zobacz [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="eefa6-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

    <span data-ttu-id="eefa6-123">LUB</span><span class="sxs-lookup"><span data-stu-id="eefa6-123">OR</span></span>

    <span data-ttu-id="eefa6-124">Lokalna instalacja hello [Azure rozwiązania Cosmos DB emulatora](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="eefa6-124">A local installation of hello [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="eefa6-125">[Visual Studio 2017](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="eefa6-125">[Visual Studio 2017](http://www.visualstudio.com/).</span></span>  
* <span data-ttu-id="eefa6-126">Microsoft Azure SDK dla platformy .NET dla programu Visual Studio 2017 r, dostępne za pośrednictwem hello Instalator programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="eefa6-126">Microsoft Azure SDK for .NET for Visual Studio 2017, available through hello Visual Studio Installer.</span></span>

<span data-ttu-id="eefa6-127">Wszystkie zrzuty ekranu hello w tym artykule wykonano za pomocą programu Microsoft Visual Studio Community 2017.</span><span class="sxs-lookup"><span data-stu-id="eefa6-127">All hello screen shots in this article have been taken using Microsoft Visual Studio Community 2017.</span></span> <span data-ttu-id="eefa6-128">Jeśli system jest skonfigurowany za pomocą innej wersji jest możliwe, że Twoje ekrany i opcje nie będą całkiem zgodne, lecz jeśli spełniasz hello powyżej wymagań wstępnych to rozwiązanie powinno działać.</span><span class="sxs-lookup"><span data-stu-id="eefa6-128">If your system is configured with a different version it is possible that your screens and options won't match entirely, but if you meet hello above prerequisites this solution should work.</span></span>

## <span data-ttu-id="eefa6-129"><a name="_Toc395637761"></a>Krok 1. Tworzenie konta bazy danych usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="eefa6-129"><a name="_Toc395637761"></a>Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="eefa6-130">Zacznijmy od utworzenia konta usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="eefa6-130">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="eefa6-131">Jeśli już masz konto SQL (DocumentDB) dla bazy danych Azure rozwiązania Cosmos lub jeśli używasz hello Azure rozwiązania Cosmos DB emulatora w tym samouczku, można pominąć zbyt[Tworzenie nowej aplikacji ASP.NET MVC](#_Toc395637762).</span><span class="sxs-lookup"><span data-stu-id="eefa6-131">If you already have a SQL (DocumentDB) account for Azure Cosmos DB or if you are using hello Azure Cosmos DB Emulator for this tutorial, you can skip too[Create a new ASP.NET MVC application](#_Toc395637762).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

<br/>
<span data-ttu-id="eefa6-132">Teraz przejdziemy przez jak toocreate nowej aplikacji ASP.NET MVC z hello podstaw.</span><span class="sxs-lookup"><span data-stu-id="eefa6-132">We will now walk through how toocreate a new ASP.NET MVC application from hello ground-up.</span></span> 

## <span data-ttu-id="eefa6-133"><a name="_Toc395637762"></a>Krok 2. Tworzenie nowej aplikacji platformy ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="eefa6-133"><a name="_Toc395637762"></a>Step 2: Create a new ASP.NET MVC application</span></span>

1. <span data-ttu-id="eefa6-134">W programie Visual Studio na powitania **pliku** menu punktu zbyt**nowy**, a następnie kliknij przycisk **projektu**.</span><span class="sxs-lookup"><span data-stu-id="eefa6-134">In Visual Studio, on hello **File** menu, point too**New**, and then click **Project**.</span></span> <span data-ttu-id="eefa6-135">Witaj **nowy projekt** zostanie wyświetlone okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="eefa6-135">hello **New Project** dialog box appears.</span></span>

2. <span data-ttu-id="eefa6-136">W hello **typy projektów** okienku rozwiń **szablony**, **Visual C#**, **sieci Web**, a następnie wybierz **aplikacji sieci Web ASP.NET** .</span><span class="sxs-lookup"><span data-stu-id="eefa6-136">In hello **Project types** pane, expand **Templates**, **Visual C#**, **Web**, and then select **ASP.NET Web Application**.</span></span>

      ![Zrzut ekranu przedstawiający okno dialogowe Nowy projekt hello z wyróżnionym typem projektu aplikacja sieci Web ASP.NET hello](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-project-dialog.png)

3. <span data-ttu-id="eefa6-138">W hello **nazwa** okno, nazwa typu hello hello projektu.</span><span class="sxs-lookup"><span data-stu-id="eefa6-138">In hello **Name** box, type hello name of hello project.</span></span> <span data-ttu-id="eefa6-139">W tym samouczku używana hello nazwa "todo".</span><span class="sxs-lookup"><span data-stu-id="eefa6-139">This tutorial uses hello name "todo".</span></span> <span data-ttu-id="eefa6-140">Jeśli wybierzesz toouse coś innego niż ten, wszędzie tam, gdzie wspomniana przestrzeń nazw todo hello, należy tooadjust hello podany kod przykłady toouse nazwy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="eefa6-140">If you choose toouse something other than this, then wherever this tutorial talks about hello todo namespace, you need tooadjust hello provided code samples toouse whatever you named your application.</span></span> 
4. <span data-ttu-id="eefa6-141">Kliknij przycisk **Przeglądaj** toonavigate toohello folderu zawierającego czy toocreate hello projektu, takich jak, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="eefa6-141">Click **Browse** toonavigate toohello folder where you would like toocreate hello project, and then click **OK**.</span></span>
   
      <span data-ttu-id="eefa6-142">Witaj **nowej aplikacji sieci Web ASP.NET** zostanie wyświetlone okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="eefa6-142">hello **New ASP.NET Web Application** dialog box appears.</span></span>
   
    ![Zrzut ekranu przedstawiający okno dialogowe hello nowej aplikacji sieci Web platformy ASP.NET z wyróżnionym szablonem aplikacji MVC hello](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-MVC.png)
5. <span data-ttu-id="eefa6-144">Wybierz w okienku szablonów hello **MVC**.</span><span class="sxs-lookup"><span data-stu-id="eefa6-144">In hello templates pane, select **MVC**.</span></span>

6. <span data-ttu-id="eefa6-145">Kliknij przycisk **OK** program Visual Studio przygotowanie wokół szkieletów hello pustego szablonu platformy ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="eefa6-145">Click **OK** and let Visual Studio do its thing around scaffolding hello empty ASP.NET MVC template.</span></span> 

          
7. <span data-ttu-id="eefa6-146">Po zakończeniu programu Visual Studio, tworzenie aplikacji MVC umożliwiającego hello masz pustą aplikację ASP.NET, który można uruchomić lokalnie.</span><span class="sxs-lookup"><span data-stu-id="eefa6-146">Once Visual Studio has finished creating hello boilerplate MVC application you have an empty ASP.NET application that you can run locally.</span></span>
   
    <span data-ttu-id="eefa6-147">Pominiemy projektu hello uruchomionych lokalnie, ponieważ wiem, zablokowaliśmy wszystkich widziany powitania "Hello World" platformy ASP.NET aplikacji.</span><span class="sxs-lookup"><span data-stu-id="eefa6-147">We'll skip running hello project locally because I'm sure we've all seen hello ASP.NET "Hello World" application.</span></span> <span data-ttu-id="eefa6-148">Przejdźmy proste tooadding bazy danych Azure rozwiązania Cosmos toothis projektu i tworzenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="eefa6-148">Let's go straight tooadding Azure Cosmos DB toothis project and building our application.</span></span>

## <span data-ttu-id="eefa6-149"><a name="_Toc395637767"></a>Krok 3: Dodaj projekt aplikacji sieci web MVC tooyour bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="eefa6-149"><a name="_Toc395637767"></a>Step 3: Add Azure Cosmos DB tooyour MVC web application project</span></span>
<span data-ttu-id="eefa6-150">Teraz, gdy mamy większość hello ASP.NET MVC potrzebnych dla tego rozwiązania, załóż toohello rzeczywistego celu tego samouczka, Dodawanie aplikacji sieci web MVC tooour bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="eefa6-150">Now that we have most of hello ASP.NET MVC plumbing that we need for this solution, let's get toohello real purpose of this tutorial, adding Azure Cosmos DB tooour MVC web application.</span></span>

1. <span data-ttu-id="eefa6-151">Witaj zestawu .NET SDK usługi Azure rozwiązania Cosmos DB zostaje spakowany i dystrybuowanych jako pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="eefa6-151">hello Azure Cosmos DB .NET SDK is packaged and distributed as a NuGet package.</span></span> <span data-ttu-id="eefa6-152">tooget hello pakietu NuGet w programie Visual Studio, użyj Menedżera pakietów NuGet hello w programie Visual Studio, klikając prawym przyciskiem myszy projekt hello w **Eksploratora rozwiązań** , a następnie klikając polecenie **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="eefa6-152">tooget hello NuGet package in Visual Studio, use hello NuGet package manager in Visual Studio by right-clicking on hello project in **Solution Explorer** and then clicking **Manage NuGet Packages**.</span></span>
   
    ![Zrzut ekranu przedstawiający powitania kliknij prawym przyciskiem myszy opcje hello projektu aplikacji sieci web w Eksploratorze rozwiązań z Zarządzaj pakietami NuGet wyróżnione.](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-manage-nuget.png)
   
    <span data-ttu-id="eefa6-154">Witaj **Zarządzaj pakietami NuGet** zostanie wyświetlone okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="eefa6-154">hello **Manage NuGet Packages** dialog box appears.</span></span>
2. <span data-ttu-id="eefa6-155">W hello NuGet **Przeglądaj** wpisz ***Azure DocumentDB***.</span><span class="sxs-lookup"><span data-stu-id="eefa6-155">In hello NuGet **Browse** box, type ***Azure DocumentDB***.</span></span> <span data-ttu-id="eefa6-156">(nazwa pakietu hello nie został zaktualizowany tooAzure DB rozwiązania Cosmos.)</span><span class="sxs-lookup"><span data-stu-id="eefa6-156">(hello package name has not been updated tooAzure Cosmos DB.)</span></span>
   
    <span data-ttu-id="eefa6-157">Wyniki hello zainstalować hello **Microsoft.Azure.DocumentDB przez firmę Microsoft** pakietu.</span><span class="sxs-lookup"><span data-stu-id="eefa6-157">From hello results, install hello **Microsoft.Azure.DocumentDB by Microsoft** package.</span></span> <span data-ttu-id="eefa6-158">To pobierze i zainstaluje hello Azure DB rozwiązania Cosmos pakietu, a także wszystkie zależności, takich jak Newtonsoft.Json.</span><span class="sxs-lookup"><span data-stu-id="eefa6-158">This will download and install hello Azure Cosmos DB package as well as all dependencies, such as Newtonsoft.Json.</span></span> <span data-ttu-id="eefa6-159">Kliknij przycisk **OK** w hello **Podgląd** okno i **akceptuję** w hello **akceptacji licencji** okna toocomplete hello instalacji.</span><span class="sxs-lookup"><span data-stu-id="eefa6-159">Click **OK** in hello **Preview** window, and **I Accept** in hello **License Acceptance** window toocomplete hello install.</span></span>
   
    ![Zrzut ekranu okna Zarządzanie pakietami NuGet hello z hello Microsoft Azure DocumentDB wyróżnioną pozycją Biblioteka kliencka](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-install-nuget.png)
   
      <span data-ttu-id="eefa6-161">Możesz też użyć hello pakietu hello tooinstall Konsola Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="eefa6-161">Alternatively you can use hello Package Manager Console tooinstall hello package.</span></span> <span data-ttu-id="eefa6-162">toodo tak na powitania **narzędzia** menu, kliknij przycisk **Menedżera pakietów NuGet**, a następnie kliknij przycisk **Konsola Menedżera pakietów**.</span><span class="sxs-lookup"><span data-stu-id="eefa6-162">toodo so, on hello **Tools** menu, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span> <span data-ttu-id="eefa6-163">W wierszu hello wpisz następujące hello.</span><span class="sxs-lookup"><span data-stu-id="eefa6-163">At hello prompt, type hello following.</span></span>
   
        Install-Package Microsoft.Azure.DocumentDB
        
3. <span data-ttu-id="eefa6-164">Po zainstalowaniu pakietu hello rozwiązania Visual Studio powinno przypominać następujące hello z dwoma odwołaniami: Microsoft.Azure.Documents.Client i Newtonsoft.Json.</span><span class="sxs-lookup"><span data-stu-id="eefa6-164">Once hello package is installed, your Visual Studio solution should resemble hello following with two new references added, Microsoft.Azure.Documents.Client and Newtonsoft.Json.</span></span>
   
    ![Zrzut ekranu hello dwa odwołania dodane projektu danych JSON toohello w Eksploratorze rozwiązań](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-added-references.png)

## <span data-ttu-id="eefa6-166"><a name="_Toc395637763"></a>Krok 4: Konfigurowanie hello aplikacji ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="eefa6-166"><a name="_Toc395637763"></a>Step 4: Set up hello ASP.NET MVC application</span></span>
<span data-ttu-id="eefa6-167">Teraz Dodajmy hello modele, widoki i kontrolery toothis aplikacji MVC:</span><span class="sxs-lookup"><span data-stu-id="eefa6-167">Now let's add hello models, views, and controllers toothis MVC application:</span></span>

* <span data-ttu-id="eefa6-168">[Dodaj model](#_Toc395637764).</span><span class="sxs-lookup"><span data-stu-id="eefa6-168">[Add a model](#_Toc395637764).</span></span>
* <span data-ttu-id="eefa6-169">[Dodaj kontroler](#_Toc395637765).</span><span class="sxs-lookup"><span data-stu-id="eefa6-169">[Add a controller](#_Toc395637765).</span></span>
* <span data-ttu-id="eefa6-170">[Dodaj widoki](#_Toc395637766).</span><span class="sxs-lookup"><span data-stu-id="eefa6-170">[Add views](#_Toc395637766).</span></span>

### <span data-ttu-id="eefa6-171"><a name="_Toc395637764"></a>Dodawanie modelu danych JSON</span><span class="sxs-lookup"><span data-stu-id="eefa6-171"><a name="_Toc395637764"></a>Add a JSON data model</span></span>
<span data-ttu-id="eefa6-172">Zacznijmy od utworzenia hello **M** w nazwie wzorca MVC, hello modelu.</span><span class="sxs-lookup"><span data-stu-id="eefa6-172">Let's begin by creating hello **M** in MVC, hello model.</span></span> 

1. <span data-ttu-id="eefa6-173">W **Eksploratora rozwiązań**, powitania kliknij prawym przyciskiem myszy **modele** folderu, kliknij przycisk **Dodaj**, a następnie kliknij przycisk **klasy**.</span><span class="sxs-lookup"><span data-stu-id="eefa6-173">In **Solution Explorer**, right-click hello **Models** folder, click **Add**, and then click **Class**.</span></span>
   
      <span data-ttu-id="eefa6-174">Witaj **Dodaj nowy element** zostanie wyświetlone okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="eefa6-174">hello **Add New Item** dialog box appears.</span></span>
2. <span data-ttu-id="eefa6-175">Nadaj nowej klasie nazwę **Item.cs** i kliknij polecenie **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="eefa6-175">Name your new class **Item.cs** and click **Add**.</span></span> 
3. <span data-ttu-id="eefa6-176">W nowym **Item.cs** plików, Dodaj następujące powitania po hello ostatnio *za pomocą instrukcji*.</span><span class="sxs-lookup"><span data-stu-id="eefa6-176">In this new **Item.cs** file, add hello following after hello last *using statement*.</span></span>
   
        using Newtonsoft.Json;
4. <span data-ttu-id="eefa6-177">Teraz zastąp ten kod</span><span class="sxs-lookup"><span data-stu-id="eefa6-177">Now replace this code</span></span> 
   
        public class Item
        {
        }
   
    <span data-ttu-id="eefa6-178">z hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="eefa6-178">with hello following code.</span></span>
   
        public class Item
        {
            [JsonProperty(PropertyName = "id")]
            public string Id { get; set; }
   
            [JsonProperty(PropertyName = "name")]
            public string Name { get; set; }
   
            [JsonProperty(PropertyName = "description")]
            public string Description { get; set; }
   
            [JsonProperty(PropertyName = "isComplete")]
            public bool Completed { get; set; }
        }
   
    <span data-ttu-id="eefa6-179">Wszystkie dane w usłudze Azure DB rozwiązania Cosmos jest przekazywana hello przewodowy i zapisane w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="eefa6-179">All data in Azure Cosmos DB is passed over hello wire and stored as JSON.</span></span> <span data-ttu-id="eefa6-180">toocontrol hello sposób obiekty są serializacji/deserializacji przez JSON.NET, możesz użyć hello **JsonProperty** jak przedstawiono w hello **elementu** klasy właśnie utworzyliśmy.</span><span class="sxs-lookup"><span data-stu-id="eefa6-180">toocontrol hello way your objects are serialized/deserialized by JSON.NET you can use hello **JsonProperty** attribute as demonstrated in hello **Item** class we just created.</span></span> <span data-ttu-id="eefa6-181">Nie musisz **ma** toodo to ale mają tooensure, że właściwości są zgodne z konwencji nazewnictwa hello JSON (camelcase).</span><span class="sxs-lookup"><span data-stu-id="eefa6-181">You don't **have** toodo this but I want tooensure that my properties follow hello JSON camelCase naming conventions.</span></span> 
   
    <span data-ttu-id="eefa6-182">Mogą kontrolować nie tylko możesz hello format nazwy właściwości hello trafia do postaci JSON, ale należy całkowicie zmienić nazwy właściwości platformy .NET, tak jak to zrobiono z hello **opis** właściwości.</span><span class="sxs-lookup"><span data-stu-id="eefa6-182">Not only can you control hello format of hello property name when it goes into JSON, but you can entirely rename your .NET properties like I did with hello **Description** property.</span></span> 

### <span data-ttu-id="eefa6-183"><a name="_Toc395637765"></a>Dodawanie kontrolera</span><span class="sxs-lookup"><span data-stu-id="eefa6-183"><a name="_Toc395637765"></a>Add a controller</span></span>
<span data-ttu-id="eefa6-184">Która zajmuje się hello **M**, teraz Utwórzmy hello **C** w nazwie wzorca MVC, klasę kontrolera.</span><span class="sxs-lookup"><span data-stu-id="eefa6-184">That takes care of hello **M**, now let's create hello **C** in MVC, a controller class.</span></span>

1. <span data-ttu-id="eefa6-185">W **Eksploratora rozwiązań**, powitania kliknij prawym przyciskiem myszy **kontrolerów** folderu, kliknij przycisk **Dodaj**, a następnie kliknij przycisk **kontrolera**.</span><span class="sxs-lookup"><span data-stu-id="eefa6-185">In **Solution Explorer**, right-click hello **Controllers** folder, click **Add**, and then click **Controller**.</span></span>
   
    <span data-ttu-id="eefa6-186">Witaj **Dodawanie szkieletu** zostanie wyświetlone okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="eefa6-186">hello **Add Scaffold** dialog box appears.</span></span>
2. <span data-ttu-id="eefa6-187">Wybierz pozycję **Kontroler MVC 5 — pusty**, a następnie kliknij polecenie **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="eefa6-187">Select **MVC 5 Controller - Empty** and then click **Add**.</span></span>
   
    ![Zrzut ekranu przedstawiający okno dialogowe Dodawanie szkieletu hello z hello kontroler MVC 5 — pusty wyróżnioną opcją](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-controller-add-scaffold.png)
3. <span data-ttu-id="eefa6-189">Nadaj nowemu kontrolerowi nazwę **ItemController**.</span><span class="sxs-lookup"><span data-stu-id="eefa6-189">Name your new Controller, **ItemController.**</span></span>
   
    ![Zrzut ekranu: okno dialogowe Dodaj kontroler hello](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-controller.png)
   
    <span data-ttu-id="eefa6-191">Po utworzeniu pliku hello rozwiązania Visual Studio powinno przypominać następujące hello z nowym plikiem ItemController.cs hello w **Eksploratora rozwiązań**.</span><span class="sxs-lookup"><span data-stu-id="eefa6-191">Once hello file is created, your Visual Studio solution should resemble hello following with hello new ItemController.cs file in **Solution Explorer**.</span></span> <span data-ttu-id="eefa6-192">Witaj nowy plik Item.cs utworzony wcześniej jest także pokazany.</span><span class="sxs-lookup"><span data-stu-id="eefa6-192">hello new Item.cs file created earlier is also shown.</span></span>
   
    ![Zrzut ekranu przedstawiający hello Eksploratora rozwiązań z hello nowym plikiem ItemController.cs i Item.cs rozwiązania Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-item-solution-explorer.png)
   
    <span data-ttu-id="eefa6-194">Możesz zamknąć plik ItemController.cs, wrócimy tooit później.</span><span class="sxs-lookup"><span data-stu-id="eefa6-194">You can close ItemController.cs, we'll come back tooit later.</span></span> 

### <span data-ttu-id="eefa6-195"><a name="_Toc395637766"></a>Dodawanie widoków</span><span class="sxs-lookup"><span data-stu-id="eefa6-195"><a name="_Toc395637766"></a>Add views</span></span>
<span data-ttu-id="eefa6-196">Teraz Utwórzmy hello **V** w nazwie wzorca MVC, hello widoków:</span><span class="sxs-lookup"><span data-stu-id="eefa6-196">Now, let's create hello **V** in MVC, hello views:</span></span>

* <span data-ttu-id="eefa6-197">[Dodaj widok indeksu elementów](#AddItemIndexView).</span><span class="sxs-lookup"><span data-stu-id="eefa6-197">[Add an Item Index view](#AddItemIndexView).</span></span>
* <span data-ttu-id="eefa6-198">[Dodaj widok nowego elementu](#AddNewIndexView).</span><span class="sxs-lookup"><span data-stu-id="eefa6-198">[Add a New Item view](#AddNewIndexView).</span></span>
* <span data-ttu-id="eefa6-199">[Dodaj widok edycji elementu](#_Toc395888515).</span><span class="sxs-lookup"><span data-stu-id="eefa6-199">[Add an Edit Item view](#_Toc395888515).</span></span>

#### <span data-ttu-id="eefa6-200"><a name="AddItemIndexView"></a>Dodawanie widoku indeksu elementów</span><span class="sxs-lookup"><span data-stu-id="eefa6-200"><a name="AddItemIndexView"></a>Add an Item Index view</span></span>
1. <span data-ttu-id="eefa6-201">W **Eksploratora rozwiązań**, rozwiń węzeł hello **widoków** folder, kliknij prawym przyciskiem myszy hello pusty **elementu** folderu, który Visual Studio utworzone po dodaniu hello  **ItemController** , kliknij polecenie **Dodaj**, a następnie kliknij przycisk **widoku**.</span><span class="sxs-lookup"><span data-stu-id="eefa6-201">In **Solution Explorer**, expand hello **Views**  folder, right-click hello empty **Item** folder that Visual Studio created for you when you added hello **ItemController** earlier, click **Add**, and then click **View**.</span></span>
   
    ![Zrzut ekranu przedstawiający Eksploratora rozwiązań przedstawiający folder Item hello utworzony za pomocą polecenia Dodaj widok hello wyróżnione Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view.png)
2. <span data-ttu-id="eefa6-203">W hello **Dodaj widok** okna dialogowego pozycję hello następujące:</span><span class="sxs-lookup"><span data-stu-id="eefa6-203">In hello **Add View** dialog box, do hello following:</span></span>
   
   * <span data-ttu-id="eefa6-204">W hello **nazwy widoku** wpisz ***indeksu***.</span><span class="sxs-lookup"><span data-stu-id="eefa6-204">In hello **View name** box, type ***Index***.</span></span>
   * <span data-ttu-id="eefa6-205">W hello **szablonu** wybierz opcję ***listy***.</span><span class="sxs-lookup"><span data-stu-id="eefa6-205">In hello **Template** box, select ***List***.</span></span>
   * <span data-ttu-id="eefa6-206">W hello **klasa modelu** wybierz opcję ***elementu (todo. Modele)***.</span><span class="sxs-lookup"><span data-stu-id="eefa6-206">In hello **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="eefa6-207">W polu strony układu hello wpisz ***~/Views/Shared/_Layout.cshtml***.</span><span class="sxs-lookup"><span data-stu-id="eefa6-207">In hello layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
     
   ![Okno dialogowe dodawania widoku zrzut ekranu przedstawiający hello](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view-dialog.png)
3. <span data-ttu-id="eefa6-209">Gdy wszystkie te wartości są ustawione, kliknij przycisk **Dodaj**. Program Visual Studio utworzy nowy widok szablonu.</span><span class="sxs-lookup"><span data-stu-id="eefa6-209">Once all these values are set, click **Add** and let Visual Studio create a new template view.</span></span> <span data-ttu-id="eefa6-210">Po zakończeniu otworzy utworzony plik cshtml hello.</span><span class="sxs-lookup"><span data-stu-id="eefa6-210">Once it is done, it will open hello cshtml file  that was created.</span></span> <span data-ttu-id="eefa6-211">Możemy zamknąć ten plik w programie Visual Studio, ponieważ wrócimy tooit później.</span><span class="sxs-lookup"><span data-stu-id="eefa6-211">We can close that file in Visual Studio as we will come back tooit later.</span></span>

#### <span data-ttu-id="eefa6-212"><a name="AddNewIndexView"></a>Dodawanie widoku nowego elementu</span><span class="sxs-lookup"><span data-stu-id="eefa6-212"><a name="AddNewIndexView"></a>Add a New Item view</span></span>
<span data-ttu-id="eefa6-213">Podobne toohow utworzyliśmy **indeks elementu** widoku teraz utworzymy nowy widok na potrzeby tworzenia nowych **elementów**.</span><span class="sxs-lookup"><span data-stu-id="eefa6-213">Similar toohow we created an **Item Index** view, we will now create a new view for creating new **Items**.</span></span>

1. <span data-ttu-id="eefa6-214">W **Eksploratora rozwiązań**, powitania kliknij prawym przyciskiem myszy **elementu** ponownie, kliknij folder **Dodaj**, a następnie kliknij przycisk **widoku**.</span><span class="sxs-lookup"><span data-stu-id="eefa6-214">In **Solution Explorer**, right-click hello **Item** folder again, click **Add**, and then click **View**.</span></span>
2. <span data-ttu-id="eefa6-215">W hello **Dodaj widok** okna dialogowego pozycję hello następujące:</span><span class="sxs-lookup"><span data-stu-id="eefa6-215">In hello **Add View** dialog box, do hello following:</span></span>
   
   * <span data-ttu-id="eefa6-216">W hello **nazwy widoku** wpisz ***Utwórz***.</span><span class="sxs-lookup"><span data-stu-id="eefa6-216">In hello **View name** box, type ***Create***.</span></span>
   * <span data-ttu-id="eefa6-217">W hello **szablonu** wybierz opcję ***Utwórz***.</span><span class="sxs-lookup"><span data-stu-id="eefa6-217">In hello **Template** box, select ***Create***.</span></span>
   * <span data-ttu-id="eefa6-218">W hello **klasa modelu** wybierz opcję ***elementu (todo. Modele)***.</span><span class="sxs-lookup"><span data-stu-id="eefa6-218">In hello **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="eefa6-219">W polu strony układu hello wpisz ***~/Views/Shared/_Layout.cshtml***.</span><span class="sxs-lookup"><span data-stu-id="eefa6-219">In hello layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
   * <span data-ttu-id="eefa6-220">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="eefa6-220">Click **Add**.</span></span>
   
#### <span data-ttu-id="eefa6-221"><a name="_Toc395888515"></a>Dodawanie widoku edycji elementu</span><span class="sxs-lookup"><span data-stu-id="eefa6-221"><a name="_Toc395888515"></a>Add an Edit Item view</span></span>
<span data-ttu-id="eefa6-222">I w końcu dodaj ostatni widok edycji **elementu** w hello tak samo jak wcześniej.</span><span class="sxs-lookup"><span data-stu-id="eefa6-222">And finally, add one last view for editing an **Item** in hello same way as before.</span></span>

1. <span data-ttu-id="eefa6-223">W **Eksploratora rozwiązań**, powitania kliknij prawym przyciskiem myszy **elementu** ponownie, kliknij folder **Dodaj**, a następnie kliknij przycisk **widoku**.</span><span class="sxs-lookup"><span data-stu-id="eefa6-223">In **Solution Explorer**, right-click hello **Item** folder again, click **Add**, and then click **View**.</span></span>
2. <span data-ttu-id="eefa6-224">W hello **Dodaj widok** okna dialogowego pozycję hello następujące:</span><span class="sxs-lookup"><span data-stu-id="eefa6-224">In hello **Add View** dialog box, do hello following:</span></span>
   
   * <span data-ttu-id="eefa6-225">W hello **nazwy widoku** wpisz ***Edytuj***.</span><span class="sxs-lookup"><span data-stu-id="eefa6-225">In hello **View name** box, type ***Edit***.</span></span>
   * <span data-ttu-id="eefa6-226">W hello **szablonu** wybierz opcję ***Edytuj***.</span><span class="sxs-lookup"><span data-stu-id="eefa6-226">In hello **Template** box, select ***Edit***.</span></span>
   * <span data-ttu-id="eefa6-227">W hello **klasa modelu** wybierz opcję ***elementu (todo. Modele)***.</span><span class="sxs-lookup"><span data-stu-id="eefa6-227">In hello **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="eefa6-228">W polu strony układu hello wpisz ***~/Views/Shared/_Layout.cshtml***.</span><span class="sxs-lookup"><span data-stu-id="eefa6-228">In hello layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
   * <span data-ttu-id="eefa6-229">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="eefa6-229">Click **Add**.</span></span>

<span data-ttu-id="eefa6-230">Po zakończeniu zamknij wszystkie dokumenty cshtml hello w programie Visual Studio, wrócimy toothese widoków później.</span><span class="sxs-lookup"><span data-stu-id="eefa6-230">Once this is done, close all hello cshtml documents in Visual Studio as we will return toothese views later.</span></span>

## <span data-ttu-id="eefa6-231"><a name="_Toc395637769"></a>Krok 5. Podłączanie usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="eefa6-231"><a name="_Toc395637769"></a>Step 5: Wiring up Azure Cosmos DB</span></span>
<span data-ttu-id="eefa6-232">Teraz, gdy jest poświęcony na obsługę hello standard MVC rzeczy, możemy zacząć tooadding hello kodu dla bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="eefa6-232">Now that hello standard MVC stuff is taken care of, let's turn tooadding hello code for Azure Cosmos DB.</span></span> 

<span data-ttu-id="eefa6-233">W tej sekcji dodamy kod toohandle hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="eefa6-233">In this section, we'll add code toohandle hello following:</span></span>

* <span data-ttu-id="eefa6-234">[Wyświetlanie niezakończonych elementów](#_Toc395637770).</span><span class="sxs-lookup"><span data-stu-id="eefa6-234">[Listing incomplete Items](#_Toc395637770).</span></span>
* <span data-ttu-id="eefa6-235">[Dodawanie elementów](#_Toc395637771).</span><span class="sxs-lookup"><span data-stu-id="eefa6-235">[Adding Items](#_Toc395637771).</span></span>
* <span data-ttu-id="eefa6-236">[Edytowanie elementów](#_Toc395637772).</span><span class="sxs-lookup"><span data-stu-id="eefa6-236">[Editing Items](#_Toc395637772).</span></span>

### <span data-ttu-id="eefa6-237"><a name="_Toc395637770"></a>Wyświetlanie niezakończonych elementów w aplikacji sieci Web MVC</span><span class="sxs-lookup"><span data-stu-id="eefa6-237"><a name="_Toc395637770"></a>Listing incomplete Items in your MVC web application</span></span>
<span data-ttu-id="eefa6-238">Witaj pierwszy toodo operacją tutaj jest dodać klasę, która zawiera wszystkie hello logiki tooconnect tooand Użyj bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="eefa6-238">hello first thing toodo here is add a class that contains all hello logic tooconnect tooand use Azure Cosmos DB.</span></span> <span data-ttu-id="eefa6-239">W ramach tego samouczka umieściliśmy całą tę logikę w klasie repozytorium tooa o nazwie DocumentDBRepository.</span><span class="sxs-lookup"><span data-stu-id="eefa6-239">For this tutorial we'll encapsulate all this logic in tooa repository class called DocumentDBRepository.</span></span> 

1. <span data-ttu-id="eefa6-240">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy na powitania projektu, kliknij przycisk **Dodaj**, a następnie kliknij przycisk **klasy**.</span><span class="sxs-lookup"><span data-stu-id="eefa6-240">In **Solution Explorer**, right-click on hello project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="eefa6-241">Nazwa nowej klasy hello **DocumentDBRepository** i kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="eefa6-241">Name hello new class **DocumentDBRepository** and click **Add**.</span></span>
2. <span data-ttu-id="eefa6-242">W nowo utworzony hello **DocumentDBRepository** klasy i dodaj następujące hello *instrukcje using* powyżej hello *przestrzeni nazw* deklaracji</span><span class="sxs-lookup"><span data-stu-id="eefa6-242">In hello newly created **DocumentDBRepository** class and add hello following *using statements* above hello *namespace* declaration</span></span>
   
        using Microsoft.Azure.Documents; 
        using Microsoft.Azure.Documents.Client; 
        using Microsoft.Azure.Documents.Linq; 
        using System.Configuration;
        using System.Linq.Expressions;
        using System.Threading.Tasks;
        using System.Net
        
    <span data-ttu-id="eefa6-243">Teraz zastąp ten kod</span><span class="sxs-lookup"><span data-stu-id="eefa6-243">Now replace this code</span></span> 
   
        public class DocumentDBRepository
        {
        }
   
    <span data-ttu-id="eefa6-244">z hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="eefa6-244">with hello following code.</span></span>
   
        public static class DocumentDBRepository<T> where T : class
        {
            private static readonly string DatabaseId = ConfigurationManager.AppSettings["database"];
            private static readonly string CollectionId = ConfigurationManager.AppSettings["collection"];
            private static DocumentClient client;
   
            public static void Initialize()
            {
                client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpoint"]), ConfigurationManager.AppSettings["authKey"]);
                CreateDatabaseIfNotExistsAsync().Wait();
                CreateCollectionIfNotExistsAsync().Wait();
            }
   
            private static async Task CreateDatabaseIfNotExistsAsync()
            {
                try
                {
                    await client.ReadDatabaseAsync(UriFactory.CreateDatabaseUri(DatabaseId));
                }
                catch (DocumentClientException e)
                {
                    if (e.StatusCode == System.Net.HttpStatusCode.NotFound)
                    {
                        await client.CreateDatabaseAsync(new Database { Id = DatabaseId });
                    }
                    else
                    {
                        throw;
                    }
                }
            }
   
            private static async Task CreateCollectionIfNotExistsAsync()
            {
                try
                {
                    await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId));
                }
                catch (DocumentClientException e)
                {
                    if (e.StatusCode == System.Net.HttpStatusCode.NotFound)
                    {
                        await client.CreateDocumentCollectionAsync(
                            UriFactory.CreateDatabaseUri(DatabaseId),
                            new DocumentCollection { Id = CollectionId },
                            new RequestOptions { OfferThroughput = 1000 });
                    }
                    else
                    {
                        throw;
                    }
                }
            }
        }
   
    
3. <span data-ttu-id="eefa6-245">Firma Microsoft czytanej zawartości niektórych wartości z konfiguracji, otwórz hello **Web.config** pliku aplikacji i dodaj następujące wiersze w obszarze hello hello `<AppSettings>` sekcji.</span><span class="sxs-lookup"><span data-stu-id="eefa6-245">We're reading some values from configuration, so open hello **Web.config** file of your application and add hello following lines under hello `<AppSettings>` section.</span></span>
   
        <add key="endpoint" value="enter hello URI from hello Keys blade of hello Azure Portal"/>
        <add key="authKey" value="enter hello PRIMARY KEY, or hello SECONDARY KEY, from hello Keys blade of hello Azure  Portal"/>
        <add key="database" value="ToDoList"/>
        <add key="collection" value="Items"/>
4. <span data-ttu-id="eefa6-246">Teraz zaktualizuj wartości hello *punktu końcowego* i *authKey* za pomocą bloku klucze hello hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="eefa6-246">Now, update hello values for *endpoint* and *authKey* using hello Keys blade of hello Azure Portal.</span></span> <span data-ttu-id="eefa6-247">Użyj hello **URI** z hello bloku klucze jako wartości hello hello ustawienia punktu końcowego i użyj hello **klucza podstawowego**, lub **klucza POMOCNICZEGO** z hello bloku klucze jako wartości hello hello Ustawienia authKey.</span><span class="sxs-lookup"><span data-stu-id="eefa6-247">Use hello **URI** from hello Keys blade as hello value of hello endpoint setting, and use hello **PRIMARY KEY**, or **SECONDARY KEY** from hello Keys blade as hello value of hello authKey setting.</span></span>

    <span data-ttu-id="eefa6-248">Czy zajmuje opieki podłączyliśmy repozytorium Azure DB rozwiązania Cosmos hello, teraz załóżmy dodać logikę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="eefa6-248">That takes care of wiring up hello Azure Cosmos DB repository, now let's add our application logic.</span></span>

1. <span data-ttu-id="eefa6-249">Witaj po pierwsze chcemy toobe stanie toodo z aplikację listy zadań do wykonania jest toodisplay hello niezakończonych elementów.</span><span class="sxs-lookup"><span data-stu-id="eefa6-249">hello first thing we want toobe able toodo with a todo list application is toodisplay hello incomplete items.</span></span>  <span data-ttu-id="eefa6-250">Skopiuj i Wklej hello następującego fragmentu kodu w obrębie hello **DocumentDBRepository** klasy.</span><span class="sxs-lookup"><span data-stu-id="eefa6-250">Copy and paste hello following code snippet anywhere within hello **DocumentDBRepository** class.</span></span>
   
        public static async Task<IEnumerable<T>> GetItemsAsync(Expression<Func<T, bool>> predicate)
        {
            IDocumentQuery<T> query = client.CreateDocumentQuery<T>(
                UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId))
                .Where(predicate)
                .AsDocumentQuery();
   
            List<T> results = new List<T>();
            while (query.HasMoreResults)
            {
                results.AddRange(await query.ExecuteNextAsync<T>());
            }
   
            return results;
        }
2. <span data-ttu-id="eefa6-251">Otwórz hello **ItemController** możemy dodany wcześniej i dodaj następujące hello *instrukcje using* powyżej hello deklaracji przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="eefa6-251">Open hello **ItemController** we added earlier and add hello following *using statements* above hello namespace declaration.</span></span>
   
        using System.Net;
        using System.Threading.Tasks;
        using todo.Models;
   
    <span data-ttu-id="eefa6-252">Jeśli projekt nie ma nazwy "todo", następnie należy tooupdate za pomocą "todo. Modele"; Nazwa hello tooreflect Twojego projektu.</span><span class="sxs-lookup"><span data-stu-id="eefa6-252">If your project is not named "todo", then you need tooupdate using "todo.Models"; tooreflect hello name of your project.</span></span>
   
    <span data-ttu-id="eefa6-253">Teraz zastąp ten kod</span><span class="sxs-lookup"><span data-stu-id="eefa6-253">Now replace this code</span></span>
   
        //GET: Item
        public ActionResult Index()
        {
            return View();
        }
   
    <span data-ttu-id="eefa6-254">z hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="eefa6-254">with hello following code.</span></span>
   
        [ActionName("Index")]
        public async Task<ActionResult> IndexAsync()
        {
            var items = await DocumentDBRepository<Item>.GetItemsAsync(d => !d.Completed);
            return View(items);
        }
3. <span data-ttu-id="eefa6-255">Otwórz **Global.asax.cs** i Dodaj powitania po wierszu toohello **Application_Start** — metoda</span><span class="sxs-lookup"><span data-stu-id="eefa6-255">Open **Global.asax.cs** and add hello following line toohello **Application_Start** method</span></span> 
   
        DocumentDBRepository<todo.Models.Item>.Initialize();

<span data-ttu-id="eefa6-256">W tym momencie rozwiązanie powinno być możliwe toobuild bez żadnych błędów.</span><span class="sxs-lookup"><span data-stu-id="eefa6-256">At this point your solution should be able toobuild without any errors.</span></span>

<span data-ttu-id="eefa6-257">W przypadku uruchomienia aplikacji hello teraz przejdzie toohello **HomeController** i hello **indeksu** tego kontrolera.</span><span class="sxs-lookup"><span data-stu-id="eefa6-257">If you ran hello application now, you would go toohello **HomeController** and hello **Index** view of that controller.</span></span> <span data-ttu-id="eefa6-258">Jest to hello domyślne zachowanie dla projektu szablonu MVC hello wybranych na początku hello, ale nie!</span><span class="sxs-lookup"><span data-stu-id="eefa6-258">This is hello default behavior for hello MVC template project we chose at hello start but we don't want that!</span></span> <span data-ttu-id="eefa6-259">Zmieńmy routing na tym tooalter aplikacji MVC to zachowanie hello.</span><span class="sxs-lookup"><span data-stu-id="eefa6-259">Let's change hello routing on this MVC application tooalter this behavior.</span></span>

<span data-ttu-id="eefa6-260">Otwórz ***aplikacji\_Start\RouteConfig.cs*** i odszukaj wiersz hello począwszy od "wartości domyślne:" i zmień je po hello tooresemble.</span><span class="sxs-lookup"><span data-stu-id="eefa6-260">Open ***App\_Start\RouteConfig.cs*** and locate hello line starting with "defaults:" and change it tooresemble hello following.</span></span>

        defaults: new { controller = "Item", action = "Index", id = UrlParameter.Optional }

<span data-ttu-id="eefa6-261">To teraz poinformuje platformę ASP.NET MVC, że jeśli nie określono wartości w toocontrol adres URL hello hello zachowania routingu, to zamiast elementu **Home**, użyj **elementu** jako kontroler hello i użytkownika **indeksu** jako hello widoku.</span><span class="sxs-lookup"><span data-stu-id="eefa6-261">This now tells ASP.NET MVC that if you have not specified a value in hello URL toocontrol hello routing behavior that instead of **Home**, use **Item** as hello controller and user **Index** as hello view.</span></span>

<span data-ttu-id="eefa6-262">Teraz po uruchomieniu aplikacji hello zostanie wywołany z **ItemController** który wywoła w klasie repozytorium toohello i użyj wszystkich toohello niezakończonych elementów hello tooreturn metody GetItems hello **widoków** \\ **Elementu**\\**indeksu** widoku.</span><span class="sxs-lookup"><span data-stu-id="eefa6-262">Now if you run hello application, it will call into your **ItemController** which will call in toohello repository class and use hello GetItems method tooreturn all hello incomplete items toohello **Views**\\**Item**\\**Index** view.</span></span> 

<span data-ttu-id="eefa6-263">Jeśli skompilujesz i uruchomisz projekt teraz, zobaczysz stronę podobną do następującej.</span><span class="sxs-lookup"><span data-stu-id="eefa6-263">If you build and run this project now, you should now see something that looks this.</span></span>    

![Zrzut ekranu przedstawiający hello todo listy aplikacji sieci web utworzone przez tego samouczka bazy danych](./media/documentdb-dotnet-application/build-and-run-the-project-now.png)

### <span data-ttu-id="eefa6-265"><a name="_Toc395637771"></a>Dodawanie elementów</span><span class="sxs-lookup"><span data-stu-id="eefa6-265"><a name="_Toc395637771"></a>Adding Items</span></span>
<span data-ttu-id="eefa6-266">Umieśćmy kilka elementów w naszej bazie danych, dzięki czemu będziemy mogli zobaczyć coś więcej niż pustą siatkę toolook w.</span><span class="sxs-lookup"><span data-stu-id="eefa6-266">Let's put some items into our database so we have something more than an empty grid toolook at.</span></span>

<span data-ttu-id="eefa6-267">Dodajmy trochę kodu zbyt DBRepository rozwiązania Cosmos Azure i ItemController toopersist hello rekord w usłudze Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="eefa6-267">Let's add some code too Azure Cosmos DBRepository and ItemController toopersist hello record in Azure Cosmos DB.</span></span>

1. <span data-ttu-id="eefa6-268">Dodaj następujące metody tooyour hello **DocumentDBRepository** klasy.</span><span class="sxs-lookup"><span data-stu-id="eefa6-268">Add hello following method tooyour **DocumentDBRepository** class.</span></span>
   
       public static async Task<Document> CreateItemAsync(T item)
       {
           return await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId), item);
       }
   
   <span data-ttu-id="eefa6-269">Ta metoda po prostu przyjmuje przekazany tooit obiekt i utrwala go w usłudze Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="eefa6-269">This method simply takes an object passed tooit and persists it in Azure Cosmos DB.</span></span>
2. <span data-ttu-id="eefa6-270">Otwórz plik ItemController.cs hello i Dodaj hello następującego fragmentu kodu w klasie hello.</span><span class="sxs-lookup"><span data-stu-id="eefa6-270">Open hello ItemController.cs file and add hello following code snippet within hello class.</span></span> <span data-ttu-id="eefa6-271">Jest to, jak platformy ASP.NET MVC wie, jakiego toodo dla hello **Utwórz** akcji.</span><span class="sxs-lookup"><span data-stu-id="eefa6-271">This is how ASP.NET MVC knows what toodo for hello **Create** action.</span></span> <span data-ttu-id="eefa6-272">W takim przypadku tylko renderowanie Witaj skojarzony widok Create.cshtml utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="eefa6-272">In this case just render hello associated Create.cshtml view created earlier.</span></span>
   
        [ActionName("Create")]
        public async Task<ActionResult> CreateAsync()
        {
            return View();
        }
   
    <span data-ttu-id="eefa6-273">Teraz potrzebujemy kodu w tym kontrolerze, który będzie akceptować przesyłanie hello z hello **Utwórz** widoku.</span><span class="sxs-lookup"><span data-stu-id="eefa6-273">We now need some more code in this controller that will accept hello submission from hello **Create** view.</span></span>
3. <span data-ttu-id="eefa6-274">Dodaj hello kolejny blok kodu toohello klasy ItemController.cs, który poinformuje platformę ASP.NET MVC, jakie toodo z formularzem POST dla tego kontrolera.</span><span class="sxs-lookup"><span data-stu-id="eefa6-274">Add hello next block of code toohello ItemController.cs class that tells ASP.NET MVC what toodo with a form POST for this controller.</span></span>
   
        [HttpPost]
        [ActionName("Create")]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> CreateAsync([Bind(Include = "Id,Name,Description,Completed")] Item item)
        {
            if (ModelState.IsValid)
            {
                await DocumentDBRepository<Item>.CreateItemAsync(item);
                return RedirectToAction("Index");
            }
   
            return View(item);
        }
   
    <span data-ttu-id="eefa6-275">Ten kod wywołuje w toohello DocumentDBRepository i używa hello CreateItemAsync metody toopersist hello nowe todo elementu toohello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="eefa6-275">This code calls in toohello DocumentDBRepository and uses hello CreateItemAsync method toopersist hello new todo item toohello database.</span></span> 
   
    <span data-ttu-id="eefa6-276">**Uwaga dotycząca zabezpieczeń**: hello **ValidateAntiForgeryToken** atrybut jest używany w tym miejscu toohelp ochrony aplikacji przed fałszerstwie żądania międzywitrynowego.</span><span class="sxs-lookup"><span data-stu-id="eefa6-276">**Security Note**: hello **ValidateAntiForgeryToken** attribute is used here toohelp protect this application against cross-site request forgery attacks.</span></span> <span data-ttu-id="eefa6-277">Brak tooit więcej niż tylko dodanie tego atrybutu, widoków musi toowork z ten token zabezpieczający przed sfałszowaniem.</span><span class="sxs-lookup"><span data-stu-id="eefa6-277">There is more tooit than just adding this attribute, your views need toowork with this anti-forgery token as well.</span></span> <span data-ttu-id="eefa6-278">Aby uzyskać więcej informacji na temat hello i przykłady sposobu tooimplement to poprawnie, zobacz [zapobieganie fałszowaniu żądań Cross-Site][Preventing Cross-Site Request Forgery].</span><span class="sxs-lookup"><span data-stu-id="eefa6-278">For more on hello subject, and examples of how tooimplement this correctly, please see [Preventing Cross-Site Request Forgery][Preventing Cross-Site Request Forgery].</span></span> <span data-ttu-id="eefa6-279">Witaj kod źródłowy dostępny w [GitHub] [ GitHub] ma pełnej implementacji hello w miejscu.</span><span class="sxs-lookup"><span data-stu-id="eefa6-279">hello source code provided on [GitHub][GitHub] has hello full implementation in place.</span></span>
   
    <span data-ttu-id="eefa6-280">**Uwaga dotycząca zabezpieczeń**: korzystamy również hello **powiązać** atrybutu toohelp parametru metody hello ochronę przed zbyt księgowej ataków.</span><span class="sxs-lookup"><span data-stu-id="eefa6-280">**Security Note**: We also use hello **Bind** attribute on hello method parameter toohelp protect against over-posting attacks.</span></span> <span data-ttu-id="eefa6-281">Aby poznać więcej szczegółów, zobacz [Basic CRUD Operations in ASP.NET MVC][Basic CRUD Operations in ASP.NET MVC] (Podstawowe operacje CRUD na platformie ASP.NET MVC).</span><span class="sxs-lookup"><span data-stu-id="eefa6-281">For more details please see [Basic CRUD Operations in ASP.NET MVC][Basic CRUD Operations in ASP.NET MVC].</span></span>

<span data-ttu-id="eefa6-282">Zakończenie hello kod wymagany tooadd nowe elementy tooour bazy danych.</span><span class="sxs-lookup"><span data-stu-id="eefa6-282">This concludes hello code required tooadd new Items tooour database.</span></span>

### <span data-ttu-id="eefa6-283"><a name="_Toc395637772"></a>Edytowanie elementów</span><span class="sxs-lookup"><span data-stu-id="eefa6-283"><a name="_Toc395637772"></a>Editing Items</span></span>
<span data-ttu-id="eefa6-284">Brak ostatnia rzecz do nas toodo i jest tooadd hello możliwości tooedit **elementów** hello bazy danych i toomark je jako zakończenie.</span><span class="sxs-lookup"><span data-stu-id="eefa6-284">There is one last thing for us toodo, and that is tooadd hello ability tooedit **Items** in hello database and toomark them as complete.</span></span> <span data-ttu-id="eefa6-285">Witaj widok edycji został już dodany projekt toohello, dlatego potrzebujemy tooadd niektóre kod tooour kontrolera i toohello **DocumentDBRepository** ponownie.</span><span class="sxs-lookup"><span data-stu-id="eefa6-285">hello view for editing was already added toohello project, so we just need tooadd some code tooour controller and toohello **DocumentDBRepository** class again.</span></span>

1. <span data-ttu-id="eefa6-286">Dodaj następujące toohello hello **DocumentDBRepository** klasy.</span><span class="sxs-lookup"><span data-stu-id="eefa6-286">Add hello following toohello **DocumentDBRepository** class.</span></span>
   
        public static async Task<Document> UpdateItemAsync(string id, T item)
        {
            return await client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(DatabaseId, CollectionId, id), item);
        }
   
        public static async Task<T> GetItemAsync(string id)
        {
            try
            {
                Document document = await client.ReadDocumentAsync(UriFactory.CreateDocumentUri(DatabaseId, CollectionId, id));
                return (T)(dynamic)document;
            }
            catch (DocumentClientException e)
            {
                if (e.StatusCode == HttpStatusCode.NotFound)
                {
                    return null;
                }
                else
                {
                    throw;
                }
            }
        }
   
    <span data-ttu-id="eefa6-287">Witaj pierwsza z tych metod **GetItem** pobiera element z rozwiązania Cosmos bazy danych Azure, który jest przekazywany wstecz toohello **ItemController** , a następnie na toohello **Edytuj** widoku.</span><span class="sxs-lookup"><span data-stu-id="eefa6-287">hello first of these methods, **GetItem** fetches an Item from Azure Cosmos DB which is passed back toohello **ItemController** and then on toohello **Edit** view.</span></span>
   
    <span data-ttu-id="eefa6-288">Witaj sekundę metody hello właśnie dodaliśmy, zastępuje hello **dokumentu** w usłudze Azure DB rozwiązania Cosmos z wersją hello hello **dokumentu** przekazany z hello **ItemController**.</span><span class="sxs-lookup"><span data-stu-id="eefa6-288">hello second of hello methods we just added replaces hello **Document** in Azure Cosmos DB with hello version of hello **Document** passed in from hello **ItemController**.</span></span>
2. <span data-ttu-id="eefa6-289">Dodaj następujące toohello hello **ItemController** klasy.</span><span class="sxs-lookup"><span data-stu-id="eefa6-289">Add hello following toohello **ItemController** class.</span></span>
   
        [HttpPost]
        [ActionName("Edit")]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> EditAsync([Bind(Include = "Id,Name,Description,Completed")] Item item)
        {
            if (ModelState.IsValid)
            {
                await DocumentDBRepository<Item>.UpdateItemAsync(item.Id, item);
                return RedirectToAction("Index");
            }
   
            return View(item);
        }
   
        [ActionName("Edit")]
        public async Task<ActionResult> EditAsync(string id)
        {
            if (id == null)
            {
                return new HttpStatusCodeResult(HttpStatusCode.BadRequest);
            }
   
            Item item = await DocumentDBRepository<Item>.GetItemAsync(id);
            if (item == null)
            {
                return HttpNotFound();
            }
   
            return View(item);
        }
   
    <span data-ttu-id="eefa6-290">Witaj pierwszy dojścia metody hello GET protokołu Http, która jest wywoływana po kliknięciu hello na powitania **Edytuj** łącza z hello **indeksu** widoku.</span><span class="sxs-lookup"><span data-stu-id="eefa6-290">hello first method handles hello Http GET that happens when hello user clicks on hello **Edit** link from hello **Index** view.</span></span> <span data-ttu-id="eefa6-291">Ta metoda pobiera [ **dokumentu** ](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx) z bazy danych usługi Azure rozwiązania Cosmos i przekazuje je toohello **Edytuj** widoku.</span><span class="sxs-lookup"><span data-stu-id="eefa6-291">This method fetches a [**Document**](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx) from Azure Cosmos DB and passes it toohello **Edit** view.</span></span>
   
    <span data-ttu-id="eefa6-292">Witaj **Edytuj** widoku wykona następnie toohello Http POST **IndexController**.</span><span class="sxs-lookup"><span data-stu-id="eefa6-292">hello **Edit** view will then do an Http POST toohello **IndexController**.</span></span> 
   
    <span data-ttu-id="eefa6-293">Druga metoda Hello dodaliśmy uchwytów przekazywanie hello zaktualizowany obiekt tooAzure DB rozwiązania Cosmos toobe trwale hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="eefa6-293">hello second method we added handles passing hello updated object tooAzure Cosmos DB toobe persisted in hello database.</span></span>

<span data-ttu-id="eefa6-294">To wszystko, że wszystko, co jest potrzebne toorun naszej aplikacji jest, listy niekompletne **elementów**, Dodaj nowy **elementów**i edytować **elementów**.</span><span class="sxs-lookup"><span data-stu-id="eefa6-294">That's it, that is everything we need toorun our application, list incomplete **Items**, add new **Items**, and edit **Items**.</span></span>

## <span data-ttu-id="eefa6-295"><a name="_Toc395637773"></a>Krok 6: Uruchamianie aplikacji hello lokalnie</span><span class="sxs-lookup"><span data-stu-id="eefa6-295"><a name="_Toc395637773"></a>Step 6: Run hello application locally</span></span>
<span data-ttu-id="eefa6-296">Aplikacja hello tootest na komputerze lokalnym hello następujące:</span><span class="sxs-lookup"><span data-stu-id="eefa6-296">tootest hello application on your local machine, do hello following:</span></span>

1. <span data-ttu-id="eefa6-297">Naciśnij klawisz F5 w programie Visual Studio toobuild hello aplikacji w trybie debugowania.</span><span class="sxs-lookup"><span data-stu-id="eefa6-297">Hit F5 in Visual Studio toobuild hello application in debug mode.</span></span> <span data-ttu-id="eefa6-298">Powinna tworzenia aplikacji hello i przeglądarkę ze strony hello pustą siatką, którą widzieliśmy wcześniej:</span><span class="sxs-lookup"><span data-stu-id="eefa6-298">It should build hello application and launch a browser with hello empty grid page we saw before:</span></span>
   
    ![Zrzut ekranu przedstawiający hello todo listy aplikacji sieci web utworzone przez tego samouczka bazy danych](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item-a.png)
   
     
2. <span data-ttu-id="eefa6-300">Kliknij przycisk hello **Utwórz nowy** link i Dodaj wartości toohello **nazwa** i **opis** pola.</span><span class="sxs-lookup"><span data-stu-id="eefa6-300">Click hello **Create New** link and add values toohello **Name** and **Description** fields.</span></span> <span data-ttu-id="eefa6-301">Pozostaw hello **Ukończono** hello w przeciwnym razie nowy niezaznaczone pole wyboru **elementu** zostanie dodany jako zakończony i nie będą wyświetlane na liście początkowej hello.</span><span class="sxs-lookup"><span data-stu-id="eefa6-301">Leave hello **Completed** check box unselected otherwise hello new **Item** will be added in a completed state and will not appear on hello initial list.</span></span>
   
    ![Zrzut ekranu przedstawiający hello Utwórz widok](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-new-item.png)
3. <span data-ttu-id="eefa6-303">Kliknij przycisk **Utwórz** i są przekierowane wstecz toohello **indeksu** widoku i **elementu** jest widoczna na liście hello.</span><span class="sxs-lookup"><span data-stu-id="eefa6-303">Click **Create** and you are redirected back toohello **Index** view and your **Item** appears in hello list.</span></span>
   
    ![Zrzut ekranu przedstawiający hello widoku indeksu](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item.png)
   
    <span data-ttu-id="eefa6-305">Możesz wolnego tooadd kilka kolejnych **elementów** tooyour lista czynności do wykonania.</span><span class="sxs-lookup"><span data-stu-id="eefa6-305">Feel free tooadd a few more **Items** tooyour todo list.</span></span>
    
4. <span data-ttu-id="eefa6-306">Kliknij przycisk **Edytuj** dalej tooan **elementu** na liście hello, są pobierane toohello **Edytuj** widok, w którym można zaktualizować dowolną właściwość obiektu, w tym hello  **Ukończono** flagi.</span><span class="sxs-lookup"><span data-stu-id="eefa6-306">Click **Edit** next tooan **Item** on hello list and you are taken toohello **Edit** view where you can update any property of your object, including hello **Completed** flag.</span></span> <span data-ttu-id="eefa6-307">Po zaznaczeniu hello **Complete** Flaga, a następnie kliknij przycisk **zapisać**, hello **elementu** zostanie usunięty z listy niezakończonych zadań hello.</span><span class="sxs-lookup"><span data-stu-id="eefa6-307">If you mark hello **Complete** flag and click **Save**, hello **Item** is removed from hello list of incomplete tasks.</span></span>
   
    ![Zrzut ekranu przedstawiający widok indeksu z zaznaczonym polem Completed hello hello](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-completed-item.png)
5. <span data-ttu-id="eefa6-309">Po przetestowaniu aplikacji hello, naciśnij klawisze Ctrl + F5 toostop debugowania aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="eefa6-309">Once you've tested hello app, press Ctrl+F5 toostop debugging hello app.</span></span> <span data-ttu-id="eefa6-310">Wszystko jest gotowe toodeploy!</span><span class="sxs-lookup"><span data-stu-id="eefa6-310">You're ready toodeploy!</span></span>

## <span data-ttu-id="eefa6-311"><a name="_Toc395637774"></a>Krok 7: Wdrażanie tooAzure aplikacji hello usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="eefa6-311"><a name="_Toc395637774"></a>Step 7: Deploy hello application tooAzure App Service</span></span> 
<span data-ttu-id="eefa6-312">Teraz, gdy masz hello kompletna aplikacja działa poprawnie z bazy danych Azure rozwiązania Cosmos zamierzamy toodeploy tego tooAzure aplikacji sieci web usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="eefa6-312">Now that you have hello complete application working correctly with Azure Cosmos DB we're going toodeploy this web app tooAzure App Service.</span></span>  

1. <span data-ttu-id="eefa6-313">Kliknij prawym przyciskiem myszy na projekt hello w jest tej aplikacji wszystkie potrzebne toodo toopublish **Eksploratora rozwiązań** i kliknij przycisk **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="eefa6-313">toopublish this application all you need toodo is right-click on hello project in **Solution Explorer** and click **Publish**.</span></span>
   
    ![Zrzut ekranu przedstawiający hello opcji Publikuj w Eksploratorze rozwiązań](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish.png)

2. <span data-ttu-id="eefa6-315">W hello **publikowania** okno dialogowe, kliknij przycisk **Microsoft Azure App Service**, a następnie wybierz pozycję **Utwórz nowy** toocreate usługę aplikacji profilu, lub kliknij przycisk **wybierz Istniejące** toouse istniejącego profilu.</span><span class="sxs-lookup"><span data-stu-id="eefa6-315">In hello **Publish** dialog box, click **Microsoft Azure App Service**, then select **Create New** toocreate an App Service profile, or click **Select Existing** toouse an existing profile.</span></span>

    ![Opublikuj okno dialogowe w programie Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish-to-existing.png)

3. <span data-ttu-id="eefa6-317">Jeśli masz istniejący profil usługi Azure App Service, wprowadź nazwę subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="eefa6-317">If you have an existing Azure App Service profile, enter your subscription name.</span></span> <span data-ttu-id="eefa6-318">Użyj hello **widoku** filtrować toosort przez grupę zasobów lub typ zasobu, a następnie wybierz usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="eefa6-318">Use hello **View** filter toosort by resource group or resource type, then select your Azure App Service.</span></span> 
   
    ![Usługi aplikacji — okno dialogowe w programie Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-app-service.png)

4. <span data-ttu-id="eefa6-320">Kliknij toocreate nowy profil usługi Azure App Service, **Utwórz nowy** w hello **publikowania** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="eefa6-320">toocreate a new Azure App Service profile, click **Create New** in hello **Publish** dialog box.</span></span> <span data-ttu-id="eefa6-321">W hello **Tworzenie usługi App Service** okna dialogowego, wprowadź nazwę aplikacji sieci Web i odpowiednie subskrypcji, grupy zasobów i plan usługi aplikacji, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="eefa6-321">In hello **Create App Service** dialog, enter your Web App name and appropriate subscription, resource group, and App Service plan, then click **Create**.</span></span>

    ![Tworzenie aplikacji usługi — okno dialogowe w programie Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-app-service.png)

<span data-ttu-id="eefa6-323">W ciągu kilku sekund program Visual Studio zakończy publikowanie aplikacji sieci web i uruchomi przeglądarkę, w którym można zobaczyć Twojej handiwork działające na platformie Azure!</span><span class="sxs-lookup"><span data-stu-id="eefa6-323">In a few seconds, Visual Studio will finish publishing your web application and launch a browser where you can see your handiwork running in Azure!</span></span>



## <span data-ttu-id="eefa6-324"><a name="_Toc395637775"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="eefa6-324"><a name="_Toc395637775"></a>Next steps</span></span>
<span data-ttu-id="eefa6-325">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="eefa6-325">Congratulations!</span></span> <span data-ttu-id="eefa6-326">Po prostu wbudowany Twojego pierwszego ASP.NET MVC aplikacji sieci web przy użyciu bazy danych Azure rozwiązania Cosmos i opublikować ją tooAzure.</span><span class="sxs-lookup"><span data-stu-id="eefa6-326">You just built your first ASP.NET MVC web application using Azure Cosmos DB and published it tooAzure.</span></span> <span data-ttu-id="eefa6-327">Witaj kodu źródłowego dla pełnej aplikacji hello, w tym hello szczegółów i usuwania funkcji, które nie zostały uwzględnione w tym samouczku można pobrać lub sklonować z [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="eefa6-327">hello source code for hello complete application, including hello detail and delete functionality that were not included in this tutorial can be downloaded or cloned from [GitHub][GitHub].</span></span> <span data-ttu-id="eefa6-328">Więc jeśli chcesz dodać, aplikacja tooyour, wystarczy pobrać kod hello i dodać toothis aplikacji.</span><span class="sxs-lookup"><span data-stu-id="eefa6-328">So if you're interested in adding that tooyour app, grab hello code and add it toothis app.</span></span>

<span data-ttu-id="eefa6-329">tooadd dodatkowe funkcje tooyour aplikacji, przejrzyj hello interfejsami API dostępnymi w hello [biblioteki .NET DB rozwiązania Cosmos Azure](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) i uważasz toohello wolnego toocontribute biblioteki .NET DB rozwiązania Cosmos Azure na [GitHub] [GitHub].</span><span class="sxs-lookup"><span data-stu-id="eefa6-329">tooadd additional functionality tooyour application, review hello APIs available in hello [Azure Cosmos DB .NET Library](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) and feel free toocontribute toohello Azure Cosmos DB .NET Library on [GitHub][GitHub].</span></span> 

[\*]: https://microsoft.sharepoint.com/teams/DocDB/Shared%20Documents/Documentation/Docs.LatestVersions/PicExportError
[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Preventing Cross-Site Request Forgery]: http://go.microsoft.com/fwlink/?LinkID=517254
[Basic CRUD Operations in ASP.NET MVC]: http://go.microsoft.com/fwlink/?LinkId=317598
[GitHub]: https://github.com/Azure-Samples/documentdb-net-todo-app
