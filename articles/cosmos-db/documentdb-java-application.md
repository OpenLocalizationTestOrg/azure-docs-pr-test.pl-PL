---
title: "samouczek tworzenia aplikacji aaaJava przy użyciu bazy danych Azure rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "W tym samouczku aplikacji sieci web Java pokazano, jak toouse hello Azure DB rozwiązania Cosmos hello toostore interfejsu API usługi DocumentDB i uzyskać dostęp do danych z aplikacji w języku Java hostowanej przez usługę Azure Websites."
keywords: Programowanie aplikacji, samouczek bazy danych, aplikacja Java, samouczek aplikacji sieci Web Java, DocumentDB, Azure, Microsoft Azure
services: cosmos-db
documentationcenter: java
author: dennyglee
manager: jhubbard
editor: mimig
ms.assetid: 0867a4a2-4bf5-4898-a1f4-44e3868f8725
ms.service: cosmos-db
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 08/22/2017
ms.author: denlee
ms.openlocfilehash: e073de23beb0037ee1e37b48a69e8fe7cdc3fc1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-java-web-application-using-azure-cosmos-db-and-hello-documentdb-api"></a><span data-ttu-id="4e401-104">Tworzenie aplikacji sieci web Java, przy użyciu bazy danych Azure rozwiązania Cosmos i hello interfejsu API usługi DocumentDB</span><span class="sxs-lookup"><span data-stu-id="4e401-104">Build a Java web application using Azure Cosmos DB and hello DocumentDB API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4e401-105">.NET</span><span class="sxs-lookup"><span data-stu-id="4e401-105">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="4e401-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="4e401-106">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="4e401-107">Java</span><span class="sxs-lookup"><span data-stu-id="4e401-107">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="4e401-108">Python</span><span class="sxs-lookup"><span data-stu-id="4e401-108">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="4e401-109">W tym samouczku aplikacji sieci web Java przedstawiono sposób toouse hello [bazy danych programu Microsoft Azure rozwiązania Cosmos](https://azure.microsoft.com/services/cosmos-db/) usługi toostore i danymi dostępu z poziomu aplikacji Java hostowanej przez aplikacje sieci Web usługi aplikacji Azure.</span><span class="sxs-lookup"><span data-stu-id="4e401-109">This Java web application tutorial shows you how toouse hello [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service toostore and access data from a Java application hosted on Azure App Service Web Apps.</span></span> <span data-ttu-id="4e401-110">W tym artykule przedstawiono:</span><span class="sxs-lookup"><span data-stu-id="4e401-110">In this topic, you will learn:</span></span>

* <span data-ttu-id="4e401-111">Jak toobuild prostą aplikację JavaServer stron (JSP) w programie Eclipse.</span><span class="sxs-lookup"><span data-stu-id="4e401-111">How toobuild a basic JavaServer Pages (JSP) application in Eclipse.</span></span>
* <span data-ttu-id="4e401-112">Jak toowork z hello Azure DB rozwiązania Cosmos usługi przy użyciu hello [Azure rozwiązania Cosmos DB Java SDK](https://github.com/Azure/azure-documentdb-java).</span><span class="sxs-lookup"><span data-stu-id="4e401-112">How toowork with hello Azure Cosmos DB service using hello [Azure Cosmos DB Java SDK](https://github.com/Azure/azure-documentdb-java).</span></span>

<span data-ttu-id="4e401-113">W tym samouczku aplikacji Java przedstawiono sposób aplikację do zarządzania zadaniami toocreate opartą na sieci web, możesz toocreate, pobieranie i oznacz zadań jako ukończonych, pokazane na powitania po obrazu.</span><span class="sxs-lookup"><span data-stu-id="4e401-113">This Java application tutorial shows you how toocreate a web-based task-management application that enables you toocreate, retrieve, and mark tasks as complete, as shown in hello following image.</span></span> <span data-ttu-id="4e401-114">Wszystkie zadania hello na liście ToDo hello są przechowywane jako dokumenty JSON w usłudze Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="4e401-114">Each of hello tasks in hello ToDo list are stored as JSON documents in Azure Cosmos DB.</span></span>

![Aplikacja My ToDo List w języku Java](./media/documentdb-java-application/image1.png)

> [!TIP]
> <span data-ttu-id="4e401-116">Ten samouczek tworzenia aplikacji zakłada, że masz już pewne doświadczenie w korzystaniu z języka Java.</span><span class="sxs-lookup"><span data-stu-id="4e401-116">This application development tutorial assumes that you have prior experience using Java.</span></span> <span data-ttu-id="4e401-117">Nowe tooJava lub hello [wstępnie wymaganych narzędzi](#Prerequisites), zalecamy pobranie hello pełną [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) projektu z usługi GitHub i skompilowanie go za pomocą [hello instrukcje na końcu hello to artykuł](#GetProject).</span><span class="sxs-lookup"><span data-stu-id="4e401-117">If you are new tooJava or hello [prerequisite tools](#Prerequisites), we recommend downloading hello complete [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) project from GitHub and building it using [hello instructions at hello end of this article](#GetProject).</span></span> <span data-ttu-id="4e401-118">Po jego skompilowaniu, można przejrzeć hello artykułu toogain wglądu na powitania kod w kontekście hello hello projektu.</span><span class="sxs-lookup"><span data-stu-id="4e401-118">Once you have it built, you can review hello article toogain insight on hello code in hello context of hello project.</span></span>  
> 
> 

## <span data-ttu-id="4e401-119"><a id="Prerequisites"></a>Wymagania wstępne dotyczące tego samouczka aplikacji sieci Web w języku Java</span><span class="sxs-lookup"><span data-stu-id="4e401-119"><a id="Prerequisites"></a>Prerequisites for this Java web application tutorial</span></span>
<span data-ttu-id="4e401-120">Przed rozpoczęciem tego samouczka tworzenia aplikacji, musi mieć następujące hello:</span><span class="sxs-lookup"><span data-stu-id="4e401-120">Before you begin this application development tutorial, you must have hello following:</span></span>

* <span data-ttu-id="4e401-121">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4e401-121">An active Azure account.</span></span> <span data-ttu-id="4e401-122">Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="4e401-122">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="4e401-123">Aby uzyskać szczegółowe informacje, zobacz [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="4e401-123">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/)</span></span>

    <span data-ttu-id="4e401-124">LUB</span><span class="sxs-lookup"><span data-stu-id="4e401-124">OR</span></span>

    <span data-ttu-id="4e401-125">Lokalna instalacja hello [Azure rozwiązania Cosmos DB emulatora](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="4e401-125">A local installation of hello [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="4e401-126">[Zestaw Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="4e401-126">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
* [<span data-ttu-id="4e401-127">Środowisko Eclipse IDE for Java EE Developers.</span><span class="sxs-lookup"><span data-stu-id="4e401-127">Eclipse IDE for Java EE Developers.</span></span>](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunasr1)
* [<span data-ttu-id="4e401-128">Witryna sieci Web Azure ze środowiskiem uruchomieniowym Java (np. Tomcat lub Jetty) włączone.</span><span class="sxs-lookup"><span data-stu-id="4e401-128">An Azure Web Site with a Java runtime environment (e.g. Tomcat or Jetty) enabled.</span></span>](../app-service-web/web-sites-java-get-started.md)

<span data-ttu-id="4e401-129">Jeśli instalujesz te narzędzia dla powitania po raz pierwszy, witryna coreservlets.com zawiera omówienie procesu instalacji hello hello Szybki Start część ich [samouczek: zainstalowanie TomCat7 i używanie go z Eclipse](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) artykułu.</span><span class="sxs-lookup"><span data-stu-id="4e401-129">If you're installing these tools for hello first time, coreservlets.com provides a walk-through of hello installation process in hello Quick Start section of their [Tutorial: Installing TomCat7 and Using it with Eclipse](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) article.</span></span>

## <span data-ttu-id="4e401-130"><a id="CreateDB"></a>Krok 1: Tworzenie konta bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="4e401-130"><a id="CreateDB"></a>Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="4e401-131">Zacznijmy od utworzenia konta usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="4e401-131">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="4e401-132">Jeśli już masz konto lub jeśli używasz hello Azure rozwiązania Cosmos DB emulatora w tym samouczku, można pominąć zbyt[krok 2: tworzenie aplikacji Java JSP hello](#CreateJSP).</span><span class="sxs-lookup"><span data-stu-id="4e401-132">If you already have an account or if you are using hello Azure Cosmos DB Emulator for this tutorial, you can skip too[Step 2: Create hello Java JSP application](#CreateJSP).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

## <span data-ttu-id="4e401-133"><a id="CreateJSP"></a>Krok 2: Tworzenie aplikacji Java JSP hello</span><span class="sxs-lookup"><span data-stu-id="4e401-133"><a id="CreateJSP"></a>Step 2: Create hello Java JSP application</span></span>
<span data-ttu-id="4e401-134">Witaj toocreate aplikację JSP:</span><span class="sxs-lookup"><span data-stu-id="4e401-134">toocreate hello JSP application:</span></span>

1. <span data-ttu-id="4e401-135">Zacznijmy od utworzenia projektu języka Java.</span><span class="sxs-lookup"><span data-stu-id="4e401-135">First, we’ll start off by creating a Java project.</span></span> <span data-ttu-id="4e401-136">Uruchom środowisko Eclipse, a następnie w menu **File** (Plik) kliknij polecenie **New** (Nowy), a potem kliknij polecenie **Dynamic Web Project** (Dynamiczny projekt sieci Web).</span><span class="sxs-lookup"><span data-stu-id="4e401-136">Start Eclipse, then click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="4e401-137">Jeśli nie widzisz **dynamiczny projekt sieci Web** na liście dostępnych projektów, hello następujące: kliknij **pliku**, kliknij przycisk **nowy**, kliknij przycisk **projektu**..., rozwiń węzeł **Web**, kliknij przycisk **dynamiczny projekt sieci Web**i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="4e401-137">If you don’t see **Dynamic Web Project** listed as an available project, do hello following: click **File**, click **New**, click **Project**…, expand **Web**, click **Dynamic Web Project**, and click **Next**.</span></span>
   
    ![Tworzenie aplikacji Java JSP](./media/documentdb-java-application/image10.png)
2. <span data-ttu-id="4e401-139">Wprowadź nazwę projektu w hello **Nazwa projektu** pola w hello **docelowe środowisko uruchomieniowe** menu rozwijanego, opcjonalnie wybierz wartość (np. Apache Tomcat v7.0), a następnie kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="4e401-139">Enter a project name in hello **Project name** box, and in hello **Target Runtime** drop-down menu, optionally select a value (e.g. Apache Tomcat v7.0), and then click **Finish**.</span></span> <span data-ttu-id="4e401-140">Wybranie docelowego środowiska uruchomieniowego włącza toorun możesz projektu lokalnie za pośrednictwem środowiska Eclipse.</span><span class="sxs-lookup"><span data-stu-id="4e401-140">Selecting a target runtime enables you toorun your project locally through Eclipse.</span></span>
3. <span data-ttu-id="4e401-141">W środowisku Eclipse w widoku Project Explorer hello rozwiń projekt.</span><span class="sxs-lookup"><span data-stu-id="4e401-141">In Eclipse, in hello Project Explorer view, expand your project.</span></span> <span data-ttu-id="4e401-142">Kliknij prawym przyciskiem myszy folder **WebContent**, kliknij polecenie **New** (Nowy), a następnie kliknij polecenie **JSP File** (Plik JSP).</span><span class="sxs-lookup"><span data-stu-id="4e401-142">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>
4. <span data-ttu-id="4e401-143">W hello **New JSP File** okno dialogowe, nazwa pliku hello **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="4e401-143">In hello **New JSP File** dialog box, name hello file **index.jsp**.</span></span> <span data-ttu-id="4e401-144">Zachowaj folder nadrzędny hello **WebContent**, jak pokazano w hello następującej ilustracji, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="4e401-144">Keep hello parent folder as **WebContent**, as shown in hello following illustration, and then click **Next**.</span></span>
   
    ![Tworzenie nowego pliku JSP — samouczek aplikacji sieci Web w języku Java](./media/documentdb-java-application/image11.png)
5. <span data-ttu-id="4e401-146">W hello **wybierz szablon JSP** okno dialogowe hello w celu tego samouczka wybierz **New JSP File (html)**, a następnie kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="4e401-146">In hello **Select JSP Template** dialog box, for hello purpose of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>
6. <span data-ttu-id="4e401-147">Po otwarciu pliku index.jsp hello w środowisku Eclipse Dodaj tekst toodisplay **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="4e401-147">When hello index.jsp file opens in Eclipse, add text toodisplay **Hello World!**</span></span> <span data-ttu-id="4e401-148">w ramach istniejącego hello <body> elementu.</span><span class="sxs-lookup"><span data-stu-id="4e401-148">within hello existing <body> element.</span></span> <span data-ttu-id="4e401-149">Zaktualizowana <body> zawartość powinna wyglądać hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="4e401-149">Your updated <body> content should look like hello following code:</span></span>
   
        <body>
            <% out.println("Hello World!"); %>
        </body>
7. <span data-ttu-id="4e401-150">Zapisz plik index.jsp hello.</span><span class="sxs-lookup"><span data-stu-id="4e401-150">Save hello index.jsp file.</span></span>
8. <span data-ttu-id="4e401-151">Jeśli ustawisz docelowe środowisko uruchomieniowe w kroku 2, możesz kliknąć **projektu** , a następnie **Uruchom** toorun aplikację JSP lokalnie:</span><span class="sxs-lookup"><span data-stu-id="4e401-151">If you set a target runtime in step 2, you can click **Project** and then **Run** toorun your JSP application locally:</span></span>
   
    ![Witaj świecie – samouczek aplikacji w języku Java](./media/documentdb-java-application/image12.png)

## <span data-ttu-id="4e401-153"><a id="InstallSDK"></a>Krok 3: Instalowanie hello zestawu SDK Java usługi DocumentDB</span><span class="sxs-lookup"><span data-stu-id="4e401-153"><a id="InstallSDK"></a>Step 3: Install hello DocumentDB Java SDK</span></span>
<span data-ttu-id="4e401-154">Witaj Najprostszym sposobem toopull hello zestawu SDK Java usługi DocumentDB i jego zależności jest użycie [Apache Maven](http://maven.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="4e401-154">hello easiest way toopull in hello DocumentDB Java SDK and its dependencies is through [Apache Maven](http://maven.apache.org/).</span></span>

<span data-ttu-id="4e401-155">toodo, konieczne będzie tooconvert maven tooa projekt, wykonując następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="4e401-155">toodo this, you will need tooconvert your project tooa maven project by completing hello following steps:</span></span>

1. <span data-ttu-id="4e401-156">Kliknij prawym przyciskiem myszy projekt w hello Eksplorator projektów, kliknij przycisk **Konfiguruj**, kliknij przycisk **przekonwertować tooMaven projektu**.</span><span class="sxs-lookup"><span data-stu-id="4e401-156">Right-click your project in hello Project Explorer, click **Configure**, click **Convert tooMaven Project**.</span></span>
2. <span data-ttu-id="4e401-157">W hello **tworzenie nowych POM** okna, zaakceptuj ustawienia domyślne hello i kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="4e401-157">In hello **Create new POM** window, accept hello defaults and click **Finish**.</span></span>
3. <span data-ttu-id="4e401-158">W **Eksplorator projektów**, otwórz plik pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="4e401-158">In **Project Explorer**, open hello pom.xml file.</span></span>
4. <span data-ttu-id="4e401-159">Na powitania **zależności** na karcie hello **zależności** okienku, kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="4e401-159">On hello **Dependencies** tab, in hello **Dependencies** pane, click **Add**.</span></span>
5. <span data-ttu-id="4e401-160">W hello **wybierz zależności** oknie hello następujące:</span><span class="sxs-lookup"><span data-stu-id="4e401-160">In hello **Select Dependency** window, do hello following:</span></span>
   
   * <span data-ttu-id="4e401-161">W hello **identyfikator grupy** wprowadź com.microsoft.azure.</span><span class="sxs-lookup"><span data-stu-id="4e401-161">In hello **Group Id** box, enter com.microsoft.azure.</span></span>
   * <span data-ttu-id="4e401-162">W hello **identyfikator artefaktu** wprowadź azure-documentdb.</span><span class="sxs-lookup"><span data-stu-id="4e401-162">In hello **Artifact Id** box, enter azure-documentdb.</span></span>
   * <span data-ttu-id="4e401-163">W hello **wersji** wprowadź 1.5.1.</span><span class="sxs-lookup"><span data-stu-id="4e401-163">In hello **Version** box, enter 1.5.1.</span></span>
     
   ![Instalacja zestawu SDK Java usługi DocumentDB](./media/documentdb-java-application/image13.png)
     
   * <span data-ttu-id="4e401-165">Lub Dodaj zależności hello XML dla identyfikatora grupy i identyfikator artefaktu bezpośrednio toohello pom.xml za pomocą edytora tekstu:</span><span class="sxs-lookup"><span data-stu-id="4e401-165">Or add hello dependency XML for Group Id and Artifact Id directly toohello pom.xml via a text editor:</span></span>
     
        <span data-ttu-id="4e401-166"><dependency><groupId>com.microsoft.azure</groupId> <artifactId>azure-documentdb</artifactId> <version>1.9.1</version></dependency></span><span class="sxs-lookup"><span data-stu-id="4e401-166"><dependency> <groupId>com.microsoft.azure</groupId> <artifactId>azure-documentdb</artifactId> <version>1.9.1</version> </dependency></span></span>
6. <span data-ttu-id="4e401-167">Kliknij przycisk **OK** i Maven zainstaluje hello zestawu SDK Java usługi DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="4e401-167">Click **OK** and Maven will install hello DocumentDB Java SDK.</span></span>
7. <span data-ttu-id="4e401-168">Zapisz plik pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="4e401-168">Save hello pom.xml file.</span></span>

## <span data-ttu-id="4e401-169"><a id="UseService"></a>Krok 4: Przy użyciu usługi Azure DB rozwiązania Cosmos hello w aplikacji Java</span><span class="sxs-lookup"><span data-stu-id="4e401-169"><a id="UseService"></a>Step 4: Using hello Azure Cosmos DB service in a Java application</span></span>
1. <span data-ttu-id="4e401-170">Najpierw zdefiniujmy obiekt TodoItem hello w TodoItem.java:</span><span class="sxs-lookup"><span data-stu-id="4e401-170">First, let's define hello TodoItem object in TodoItem.java:</span></span>
   
        @Data
        @Builder
        public class TodoItem {
            private String category;
            private boolean complete;
            private String id;
            private String name;
        }
   
    <span data-ttu-id="4e401-171">W tym projekcie użyto [projektu Lombok](http://projectlombok.org/) toogenerate hello konstruktora, metody pobierające, metody ustawiające i konstruktora.</span><span class="sxs-lookup"><span data-stu-id="4e401-171">In this project, we are using [Project Lombok](http://projectlombok.org/) toogenerate hello constructor, getters, setters, and a builder.</span></span> <span data-ttu-id="4e401-172">Możesz też ręcznie napisać ten kod lub ma wygenerowania hello IDE.</span><span class="sxs-lookup"><span data-stu-id="4e401-172">Alternatively, you can write this code manually or have hello IDE generate it.</span></span>
2. <span data-ttu-id="4e401-173">usługi bazy danych Azure rozwiązania Cosmos hello tooinvoke, trzeba utworzyć wystąpienie nowego **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="4e401-173">tooinvoke hello Azure Cosmos DB service, you must instantiate a new **DocumentClient**.</span></span> <span data-ttu-id="4e401-174">Ogólnie rzecz biorąc, jest najlepszym hello tooreuse **DocumentClient** — zamiast niż konstruować nowego klienta dla kolejnych żądań.</span><span class="sxs-lookup"><span data-stu-id="4e401-174">In general, it is best tooreuse hello **DocumentClient** - rather than construct a new client for each subsequent request.</span></span> <span data-ttu-id="4e401-175">Powitania klienta można ponownie użyć, opakowując powitania klienta w **DocumentClientFactory**.</span><span class="sxs-lookup"><span data-stu-id="4e401-175">We can reuse hello client by wrapping hello client in a **DocumentClientFactory**.</span></span> <span data-ttu-id="4e401-176">W DocumentClientFactory.java, potrzebujesz toopaste hello URI oraz PRIMARY KEY wartości zapisane tooyour Schowka w [krok 1](#CreateDB).</span><span class="sxs-lookup"><span data-stu-id="4e401-176">In DocumentClientFactory.java, you need toopaste hello URI and PRIMARY KEY value you saved tooyour clipboard in [step 1](#CreateDB).</span></span> <span data-ttu-id="4e401-177">Zastąp [YOUR\_ENDPOINT\_HERE] wartością URI, a [YOUR\_KEY\_HERE] zastąp wartością PRIMARY KEY.</span><span class="sxs-lookup"><span data-stu-id="4e401-177">Replace [YOUR\_ENDPOINT\_HERE] with your URI and replace [YOUR\_KEY\_HERE] with your PRIMARY KEY.</span></span>
   
        private static final String HOST = "[YOUR_ENDPOINT_HERE]";
        private static final String MASTER_KEY = "[YOUR_KEY_HERE]";
   
        private static DocumentClient documentClient = new DocumentClient(HOST, MASTER_KEY,
                        ConnectionPolicy.GetDefault(), ConsistencyLevel.Session);
   
        public static DocumentClient getDocumentClient() {
            return documentClient;
        }
3. <span data-ttu-id="4e401-178">Teraz Utwórzmy tooabstract obiekt DAO (Data Access), utrwalanie naszych tooAzure elementów ToDo DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="4e401-178">Now let's create a Data Access Object (DAO) tooabstract persisting our ToDo items tooAzure Cosmos DB.</span></span>
   
    <span data-ttu-id="4e401-179">W celu wykonania (ToDo) toosave tooa kolekcji należy powitania klienta tooknow które toopersist bazę danych i kolekcję zbyt (wskazywanej przez linki do samego siebie).</span><span class="sxs-lookup"><span data-stu-id="4e401-179">In order toosave ToDo items tooa collection, hello client needs tooknow which database and collection toopersist too(as referenced by self-links).</span></span> <span data-ttu-id="4e401-180">Ogólnie rzecz biorąc, jest najlepszym toocache hello w bazie danych i kolekcji, jeśli to możliwe tooavoid dodatkowych połączeń toohello w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="4e401-180">In general, it is best toocache hello database and collection when possible tooavoid additional round-trips toohello database.</span></span>
   
    <span data-ttu-id="4e401-181">Witaj poniższy kod ilustruje sposób tooretrieve bazę danych i kolekcji, jeśli istnieje, lub utworzyć nową, jeśli nie istnieje:</span><span class="sxs-lookup"><span data-stu-id="4e401-181">hello following code illustrates how tooretrieve our database and collection, if it exists, or create a new one if it doesn't exist:</span></span>
   
        public class DocDbDao implements TodoDao {
            // hello name of our database.
            private static final String DATABASE_ID = "TodoDB";
   
            // hello name of our collection.
            private static final String COLLECTION_ID = "TodoCollection";
   
            // hello Azure Cosmos DB Client
            private static DocumentClient documentClient = DocumentClientFactory
                    .getDocumentClient();
   
            // Cache for hello database object, so we don't have tooquery for it to
            // retrieve self links.
            private static Database databaseCache;
   
            // Cache for hello collection object, so we don't have tooquery for it to
            // retrieve self links.
            private static DocumentCollection collectionCache;
   
            private Database getTodoDatabase() {
                if (databaseCache == null) {
                    // Get hello database if it exists
                    List<Database> databaseList = documentClient
                            .queryDatabases(
                                    "SELECT * FROM root r WHERE r.id='" + DATABASE_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (databaseList.size() > 0) {
                        // Cache hello database object so we won't have tooquery for it
                        // later tooretrieve hello selfLink.
                        databaseCache = databaseList.get(0);
                    } else {
                        // Create hello database if it doesn't exist.
                        try {
                            Database databaseDefinition = new Database();
                            databaseDefinition.setId(DATABASE_ID);
   
                            databaseCache = documentClient.createDatabase(
                                    databaseDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - hello app wasn't
                            // able tooquery or create hello collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return databaseCache;
            }
   
            private DocumentCollection getTodoCollection() {
                if (collectionCache == null) {
                    // Get hello collection if it exists.
                    List<DocumentCollection> collectionList = documentClient
                            .queryCollections(
                                    getTodoDatabase().getSelfLink(),
                                    "SELECT * FROM root r WHERE r.id='" + COLLECTION_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (collectionList.size() > 0) {
                        // Cache hello collection object so we won't have tooquery for it
                        // later tooretrieve hello selfLink.
                        collectionCache = collectionList.get(0);
                    } else {
                        // Create hello collection if it doesn't exist.
                        try {
                            DocumentCollection collectionDefinition = new DocumentCollection();
                            collectionDefinition.setId(COLLECTION_ID);
   
                            collectionCache = documentClient.createCollection(
                                    getTodoDatabase().getSelfLink(),
                                    collectionDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - hello app wasn't
                            // able tooquery or create hello collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return collectionCache;
            }
        }
4. <span data-ttu-id="4e401-182">Witaj, następnym krokiem jest toowrite niektórych kodu toopersist hello TodoItems w kolekcji toohello.</span><span class="sxs-lookup"><span data-stu-id="4e401-182">hello next step is toowrite some code toopersist hello TodoItems in toohello collection.</span></span> <span data-ttu-id="4e401-183">W tym przykładzie używamy [Gson](https://code.google.com/p/google-gson/) tooserialize i zdeserializować dokumenty tooJSON TodoItem zwykły stare Java obiekty (Pojo).</span><span class="sxs-lookup"><span data-stu-id="4e401-183">In this example, we will use [Gson](https://code.google.com/p/google-gson/) tooserialize and de-serialize TodoItem Plain Old Java Objects (POJOs) tooJSON documents.</span></span>
   
        // We'll use Gson for POJO <=> JSON serialization for this example.
        private static Gson gson = new Gson();
   
        @Override
        public TodoItem createTodoItem(TodoItem todoItem) {
            // Serialize hello TodoItem as a JSON Document.
            Document todoItemDocument = new Document(gson.toJson(todoItem));
   
            // Annotate hello document as a TodoItem for retrieval (so that we can
            // store multiple entity types in hello collection).
            todoItemDocument.set("entityType", "todoItem");
   
            try {
                // Persist hello document using hello DocumentClient.
                todoItemDocument = documentClient.createDocument(
                        getTodoCollection().getSelfLink(), todoItemDocument, null,
                        false).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
5. <span data-ttu-id="4e401-184">Podobnie jak do baz danych i kolekcji usługi Azure Cosmos DB, również do dokumentów można odwoływać się za pomocą linków do samego siebie.</span><span class="sxs-lookup"><span data-stu-id="4e401-184">Like Azure Cosmos DB databases and collections, documents are also referenced by self-links.</span></span> <span data-ttu-id="4e401-185">Witaj następujących pomocnika funkcja pozwala nam pobierania dokumentów przez inny atrybut (np. "id"), zamiast link do samego siebie:</span><span class="sxs-lookup"><span data-stu-id="4e401-185">hello following helper function lets us retrieve documents by another attribute (e.g. "id") rather than self-link:</span></span>
   
        private Document getDocumentById(String id) {
            // Retrieve hello document using hello DocumentClient.
            List<Document> documentList = documentClient
                    .queryDocuments(getTodoCollection().getSelfLink(),
                            "SELECT * FROM root r WHERE r.id='" + id + "'", null)
                    .getQueryIterable().toList();
   
            if (documentList.size() > 0) {
                return documentList.get(0);
            } else {
                return null;
            }
        }
6. <span data-ttu-id="4e401-186">Możemy użyć metody pomocniczej hello w kroku 5 tooretrieve dokumentu todoitem typu JSON przez identyfikator, a następnie do deserializacji tooa typu POJO:</span><span class="sxs-lookup"><span data-stu-id="4e401-186">We can use hello helper method in step 5 tooretrieve a TodoItem JSON document by id and then deserialize it tooa POJO:</span></span>
   
        @Override
        public TodoItem readTodoItem(String id) {
            // Retrieve hello document by id using our helper method.
            Document todoItemDocument = getDocumentById(id);
   
            if (todoItemDocument != null) {
                // De-serialize hello document in tooa TodoItem.
                return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
            } else {
                return null;
            }
        }
7. <span data-ttu-id="4e401-187">Możemy również użyć hello DocumentClient tooget kolekcję lub listę obiektów Todoitem przy użyciu usługi DocumentDB SQL:</span><span class="sxs-lookup"><span data-stu-id="4e401-187">We can also use hello DocumentClient tooget a collection or list of TodoItems using DocumentDB SQL:</span></span>
   
        @Override
        public List<TodoItem> readTodoItems() {
            List<TodoItem> todoItems = new ArrayList<TodoItem>();
   
            // Retrieve hello TodoItem documents
            List<Document> documentList = documentClient
                    .queryDocuments(getTodoCollection().getSelfLink(),
                            "SELECT * FROM root r WHERE r.entityType = 'todoItem'",
                            null).getQueryIterable().toList();
   
            // De-serialize hello documents in tooTodoItems.
            for (Document todoItemDocument : documentList) {
                todoItems.add(gson.fromJson(todoItemDocument.toString(),
                        TodoItem.class));
            }
   
            return todoItems;
        }
8. <span data-ttu-id="4e401-188">Istnieje wiele sposobów tooupdate dokument z hello DocumentClient.</span><span class="sxs-lookup"><span data-stu-id="4e401-188">There are many ways tooupdate a document with hello DocumentClient.</span></span> <span data-ttu-id="4e401-189">W aplikacji zarządzającej listą chcemy tootoggle stanie toobe czy zadanie zostało ukończone.</span><span class="sxs-lookup"><span data-stu-id="4e401-189">In our Todo list application, we want toobe able tootoggle whether a TodoItem is complete.</span></span> <span data-ttu-id="4e401-190">Można to osiągnąć przez zaktualizowanie atrybutu "complete" hello w dokumencie hello:</span><span class="sxs-lookup"><span data-stu-id="4e401-190">This can be achieved by updating hello "complete" attribute within hello document:</span></span>
   
        @Override
        public TodoItem updateTodoItem(String id, boolean isComplete) {
            // Retrieve hello document from hello database
            Document todoItemDocument = getDocumentById(id);
   
            // You can update hello document as a JSON document directly.
            // For more complex operations - you could de-serialize hello document in
            // tooa POJO, update hello POJO, and then re-serialize hello POJO back in to
            // a document.
            todoItemDocument.set("complete", isComplete);
   
            try {
                // Persist/replace hello updated document.
                todoItemDocument = documentClient.replaceDocument(todoItemDocument,
                        null).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
9. <span data-ttu-id="4e401-191">Wreszcie chcemy mieć hello możliwości toodelete czynność do wykonania z naszej listy.</span><span class="sxs-lookup"><span data-stu-id="4e401-191">Finally, we want hello ability toodelete a TodoItem from our list.</span></span> <span data-ttu-id="4e401-192">toodo, możemy użyć metody pomocnika hello napisaliśmy wcześniej tooretrieve hello link do samego siebie, a następnie powitania klienta toodelete go:</span><span class="sxs-lookup"><span data-stu-id="4e401-192">toodo this, we can use hello helper method we wrote earlier tooretrieve hello self-link and then tell hello client toodelete it:</span></span>
   
        @Override
        public boolean deleteTodoItem(String id) {
            // Azure Cosmos DB refers toodocuments by self link rather than id.
   
            // Query for hello document tooretrieve hello self link.
            Document todoItemDocument = getDocumentById(id);
   
            try {
                // Delete hello document by self link.
                documentClient.deleteDocument(todoItemDocument.getSelfLink(), null);
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return false;
            }
   
            return true;
        }

## <span data-ttu-id="4e401-193"><a id="Wire"></a>Krok 5: Dołączenie razem pozostałe hello hello projektu tworzenia aplikacji Java</span><span class="sxs-lookup"><span data-stu-id="4e401-193"><a id="Wire"></a>Step 5: Wiring hello rest of hello of Java application development project together</span></span>
<span data-ttu-id="4e401-194">Teraz, gdy już zakończyliśmy hello fun bits - pozostało jest toobuild interfejs użytkownika szybki i połączenie go z zapasowej tooour DAO.</span><span class="sxs-lookup"><span data-stu-id="4e401-194">Now that we've finished hello fun bits - all that's left is toobuild a quick user interface and wire it up tooour DAO.</span></span>

1. <span data-ttu-id="4e401-195">Po pierwsze Zacznijmy od utworzenia toocall kontrolera DAO:</span><span class="sxs-lookup"><span data-stu-id="4e401-195">First, let's start with building a controller toocall our DAO:</span></span>
   
        public class TodoItemController {
            public static TodoItemController getInstance() {
                if (todoItemController == null) {
                    todoItemController = new TodoItemController(TodoDaoFactory.getDao());
                }
                return todoItemController;
            }
   
            private static TodoItemController todoItemController;
   
            private final TodoDao todoDao;
   
            TodoItemController(TodoDao todoDao) {
                this.todoDao = todoDao;
            }
   
            public TodoItem createTodoItem(@NonNull String name,
                    @NonNull String category, boolean isComplete) {
                TodoItem todoItem = TodoItem.builder().name(name).category(category)
                        .complete(isComplete).build();
                return todoDao.createTodoItem(todoItem);
            }
   
            public boolean deleteTodoItem(@NonNull String id) {
                return todoDao.deleteTodoItem(id);
            }
   
            public TodoItem getTodoItemById(@NonNull String id) {
                return todoDao.readTodoItem(id);
            }
   
            public List<TodoItem> getTodoItems() {
                return todoDao.readTodoItems();
            }
   
            public TodoItem updateTodoItem(@NonNull String id, boolean isComplete) {
                return todoDao.updateTodoItem(id, isComplete);
            }
        }
   
    <span data-ttu-id="4e401-196">W przypadku bardziej złożonych aplikacji hello kontroler może zawierać skomplikowaną logikę biznesową na powitania DAO.</span><span class="sxs-lookup"><span data-stu-id="4e401-196">In a more complex application, hello controller may house complicated business logic on top of hello DAO.</span></span>
2. <span data-ttu-id="4e401-197">Następnie utworzymy kontrolera toohello serwlet tooroute HTTP żądania:</span><span class="sxs-lookup"><span data-stu-id="4e401-197">Next, we'll create a servlet tooroute HTTP requests toohello controller:</span></span>
   
        public class TodoServlet extends HttpServlet {
            // API Keys
            public static final String API_METHOD = "method";
   
            // API Methods
            public static final String CREATE_TODO_ITEM = "createTodoItem";
            public static final String GET_TODO_ITEMS = "getTodoItems";
            public static final String UPDATE_TODO_ITEM = "updateTodoItem";
   
            // API Parameters
            public static final String TODO_ITEM_ID = "todoItemId";
            public static final String TODO_ITEM_NAME = "todoItemName";
            public static final String TODO_ITEM_CATEGORY = "todoItemCategory";
            public static final String TODO_ITEM_COMPLETE = "todoItemComplete";
   
            public static final String MESSAGE_ERROR_INVALID_METHOD = "{'error': 'Invalid method'}";
   
            private static final long serialVersionUID = 1L;
            private static final Gson gson = new Gson();
   
            @Override
            protected void doGet(HttpServletRequest request,
                    HttpServletResponse response) throws ServletException, IOException {
   
                String apiResponse = MESSAGE_ERROR_INVALID_METHOD;
   
                TodoItemController todoItemController = TodoItemController
                        .getInstance();
   
                String id = request.getParameter(TODO_ITEM_ID);
                String name = request.getParameter(TODO_ITEM_NAME);
                String category = request.getParameter(TODO_ITEM_CATEGORY);
                boolean isComplete = StringUtils.equalsIgnoreCase("true",
                        request.getParameter(TODO_ITEM_COMPLETE)) ? true : false;
   
                switch (request.getParameter(API_METHOD)) {
                case CREATE_TODO_ITEM:
                    apiResponse = gson.toJson(todoItemController.createTodoItem(name,
                            category, isComplete));
                    break;
                case GET_TODO_ITEMS:
                    apiResponse = gson.toJson(todoItemController.getTodoItems());
                    break;
                case UPDATE_TODO_ITEM:
                    apiResponse = gson.toJson(todoItemController.updateTodoItem(id,
                            isComplete));
                    break;
                default:
                    break;
                }
   
                response.getWriter().println(apiResponse);
            }
   
            @Override
            protected void doPost(HttpServletRequest request,
                    HttpServletResponse response) throws ServletException, IOException {
                doGet(request, response);
            }
        }
3. <span data-ttu-id="4e401-198">Potrzebujemy użytkownika toohello toodisplay interfejs użytkownika sieci web.</span><span class="sxs-lookup"><span data-stu-id="4e401-198">We'll need a web user interface toodisplay toohello user.</span></span> <span data-ttu-id="4e401-199">Napiszmy hello index.jsp utworzony wcześniej:</span><span class="sxs-lookup"><span data-stu-id="4e401-199">Let's re-write hello index.jsp we created earlier:</span></span>
    ```html
        <html>
        <head>
          <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
          <meta http-equiv="X-UA-Compatible" content="IE=edge;" />
          <title>Azure Cosmos DB Java Sample</title>
   
          <!-- Bootstrap -->
          <link href="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css" rel="stylesheet">
   
          <style>
            /* Add padding toobody for fixed nav bar */
            body {
              padding-top: 50px;
            }
          </style>
        </head>
        <body>
          <!-- Nav Bar -->
          <div class="navbar navbar-inverse navbar-fixed-top" role="navigation">
            <div class="container">
              <div class="navbar-header">
                <a class="navbar-brand" href="#">My Tasks</a>
              </div>
            </div>
          </div>
   
          <!-- Body -->
          <div class="container">
            <h1>My ToDo List</h1>
   
            <hr/>
   
            <!-- hello ToDo List -->
            <div class = "todoList">
              <table class="table table-bordered table-striped" id="todoItems">
                <thead>
                  <tr>
                    <th>Name</th>
                    <th>Category</th>
                    <th>Complete</th>
                  </tr>
                </thead>
                <tbody>
                </tbody>
              </table>
   
              <!-- Update Button -->
              <div class="todoUpdatePanel">
                <form class="form-horizontal" role="form">
                  <button type="button" class="btn btn-primary">Update Tasks</button>
                </form>
              </div>
   
            </div>
   
            <hr/>
   
            <!-- Item Input Form -->
            <div class="todoForm">
              <form class="form-horizontal" role="form">
                <div class="form-group">
                  <label for="inputItemName" class="col-sm-2">Task Name</label>
                  <div class="col-sm-10">
                    <input type="text" class="form-control" id="inputItemName" placeholder="Enter name">
                  </div>
                </div>
   
                <div class="form-group">
                  <label for="inputItemCategory" class="col-sm-2">Task Category</label>
                  <div class="col-sm-10">
                    <input type="text" class="form-control" id="inputItemCategory" placeholder="Enter category">
                  </div>
                </div>
   
                <button type="button" class="btn btn-primary">Add Task</button>
              </form>
            </div>
   
          </div>
   
          <!-- Placed at hello end of hello document so hello pages load faster -->
          <script src="//ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js"></script>
          <script src="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js"></script>
          <script src="assets/todo.js"></script>
        </body>
        </html>
    ```
4. <span data-ttu-id="4e401-200">Na koniec, zapisywania i niektóre po stronie klienta JavaScript tootie hello interfejsem użytkownika, a hello serwlet razem:</span><span class="sxs-lookup"><span data-stu-id="4e401-200">And finally, write some client-side JavaScript tootie hello web user interface and hello servlet together:</span></span>
   
        var todoApp = {
          /*
           * API methods toocall Java backend.
           */
          apiEndpoint: "api",
   
          createTodoItem: function(name, category, isComplete) {
            $.post(todoApp.apiEndpoint, {
                "method": "createTodoItem",
                "todoItemName": name,
                "todoItemCategory": category,
                "todoItemComplete": isComplete
              },
              function(data) {
                var todoItem = data;
                todoApp.addTodoItemToTable(todoItem.id, todoItem.name, todoItem.category, todoItem.complete);
              },
              "json");
          },
   
          getTodoItems: function() {
            $.post(todoApp.apiEndpoint, {
                "method": "getTodoItems"
              },
              function(data) {
                var todoItemArr = data;
                $.each(todoItemArr, function(index, value) {
                  todoApp.addTodoItemToTable(value.id, value.name, value.category, value.complete);
                });
              },
              "json");
          },
   
          updateTodoItem: function(id, isComplete) {
            $.post(todoApp.apiEndpoint, {
                "method": "updateTodoItem",
                "todoItemId": id,
                "todoItemComplete": isComplete
              },
              function(data) {},
              "json");
          },
   
          /*
           * UI Methods
           */
          addTodoItemToTable: function(id, name, category, isComplete) {
            var rowColor = isComplete ? "active" : "warning";
   
            todoApp.ui_table().append($("<tr>")
              .append($("<td>").text(name))
              .append($("<td>").text(category))
              .append($("<td>")
                .append($("<input>")
                  .attr("type", "checkbox")
                  .attr("id", id)
                  .attr("checked", isComplete)
                  .attr("class", "isComplete")
                ))
              .addClass(rowColor)
            );
          },
   
          /*
           * UI Bindings
           */
          bindCreateButton: function() {
            todoApp.ui_createButton().click(function() {
              todoApp.createTodoItem(todoApp.ui_createNameInput().val(), todoApp.ui_createCategoryInput().val(), false);
              todoApp.ui_createNameInput().val("");
              todoApp.ui_createCategoryInput().val("");
            });
          },
   
          bindUpdateButton: function() {
            todoApp.ui_updateButton().click(function() {
              // Disable button temporarily.
              var myButton = $(this);
              var originalText = myButton.text();
              $(this).text("Updating...");
              $(this).prop("disabled", true);
   
              // Call api tooupdate todo items.
              $.each(todoApp.ui_updateId(), function(index, value) {
                todoApp.updateTodoItem(value.name, value.value);
                $(value).remove();
              });
   
              // Re-enable button.
              setTimeout(function() {
                myButton.prop("disabled", false);
                myButton.text(originalText);
              }, 500);
            });
          },
   
          bindUpdateCheckboxes: function() {
            todoApp.ui_table().on("click", ".isComplete", function(event) {
              var checkboxElement = $(event.currentTarget);
              var rowElement = $(event.currentTarget).parents('tr');
              var id = checkboxElement.attr('id');
              var isComplete = checkboxElement.is(':checked');
   
              // Toggle table row color
              if (isComplete) {
                rowElement.addClass("active");
                rowElement.removeClass("warning");
              } else {
                rowElement.removeClass("active");
                rowElement.addClass("warning");
              }
   
              // Update hidden inputs for update panel.
              todoApp.ui_updateForm().children("input[name='" + id + "']").remove();
   
              todoApp.ui_updateForm().append($("<input>")
                .attr("type", "hidden")
                .attr("class", "updateComplete")
                .attr("name", id)
                .attr("value", isComplete));
   
            });
          },
   
          /*
           * UI Elements
           */
          ui_createNameInput: function() {
            return $(".todoForm #inputItemName");
          },
   
          ui_createCategoryInput: function() {
            return $(".todoForm #inputItemCategory");
          },
   
          ui_createButton: function() {
            return $(".todoForm button");
          },
   
          ui_table: function() {
            return $(".todoList table tbody");
          },
   
          ui_updateButton: function() {
            return $(".todoUpdatePanel button");
          },
   
          ui_updateForm: function() {
            return $(".todoUpdatePanel form");
          },
   
          ui_updateId: function() {
            return $(".todoUpdatePanel .updateComplete");
          },
   
          /*
           * Install hello TodoApp
           */
          install: function() {
            todoApp.bindCreateButton();
            todoApp.bindUpdateButton();
            todoApp.bindUpdateCheckboxes();
   
            todoApp.getTodoItems();
          }
        };
   
        $(document).ready(function() {
          todoApp.install();
        });
5. <span data-ttu-id="4e401-201">Fantastycznie!</span><span class="sxs-lookup"><span data-stu-id="4e401-201">Awesome!</span></span> <span data-ttu-id="4e401-202">Teraz pozostało to aplikacja hello tootest.</span><span class="sxs-lookup"><span data-stu-id="4e401-202">Now all that's left is tootest hello application.</span></span> <span data-ttu-id="4e401-203">Uruchamianie aplikacji hello lokalnie, a następnie dodaj jakieś zadania do wykonania wypełnianie nazwa elementu hello i kategorii, a następnie klikając polecenie **Dodaj zadanie**.</span><span class="sxs-lookup"><span data-stu-id="4e401-203">Run hello application locally, and add some Todo items by filling in hello item name and category and clicking **Add Task**.</span></span>
6. <span data-ttu-id="4e401-204">Gdy pojawi się element hello, możesz zaktualizować czy jest ono ukończone przełączanie hello wyboru, a następnie klikając polecenie **zadania aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="4e401-204">Once hello item appears, you can update whether it's complete by toggling hello checkbox and clicking **Update Tasks**.</span></span>

## <span data-ttu-id="4e401-205"><a id="Deploy"></a>Krok 6: Wdrażanie programu Java application tooAzure witryn sieci Web</span><span class="sxs-lookup"><span data-stu-id="4e401-205"><a id="Deploy"></a>Step 6: Deploy your Java application tooAzure Web Sites</span></span>
<span data-ttu-id="4e401-206">Witryny sieci Web Azure sprawia, że wdrożenie aplikacji Java sprowadza wyeksportowania aplikacji jako plik WAR i przesłania go na serwer za pomocą kontroli źródła (np. Git) lub FTP.</span><span class="sxs-lookup"><span data-stu-id="4e401-206">Azure Web Sites makes deploying Java applications as simple as exporting your application as a WAR file and either uploading it via source control (e.g. Git) or FTP.</span></span>

1. <span data-ttu-id="4e401-207">tooexport aplikacji jako plik WAR, kliknij prawym przyciskiem myszy projekt w **Eksplorator projektów**, kliknij przycisk **wyeksportować**, a następnie kliknij przycisk **pliku WAR**.</span><span class="sxs-lookup"><span data-stu-id="4e401-207">tooexport your application as a WAR file, right-click on your project in **Project Explorer**, click **Export**, and then click **WAR File**.</span></span>
2. <span data-ttu-id="4e401-208">W hello **wyeksportować plik WAR** oknie hello następujące:</span><span class="sxs-lookup"><span data-stu-id="4e401-208">In hello **WAR Export** window, do hello following:</span></span>
   
   * <span data-ttu-id="4e401-209">W polu Projekt sieci Web hello wprowadź azure-documentdb-java-sample.</span><span class="sxs-lookup"><span data-stu-id="4e401-209">In hello Web project box, enter azure-documentdb-java-sample.</span></span>
   * <span data-ttu-id="4e401-210">W polu miejsce docelowe hello wybierz plik WAR hello toosave docelowego.</span><span class="sxs-lookup"><span data-stu-id="4e401-210">In hello Destination box, choose a destination toosave hello WAR file.</span></span>
   * <span data-ttu-id="4e401-211">Kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="4e401-211">Click **Finish**.</span></span>
3. <span data-ttu-id="4e401-212">Teraz, gdy masz na plik WAR, możesz po prostu przekazać go tooyour witryny sieci Web Azure **webapps** katalogu.</span><span class="sxs-lookup"><span data-stu-id="4e401-212">Now that you have a WAR file in hand, you can simply upload it tooyour Azure Web Site's **webapps** directory.</span></span> <span data-ttu-id="4e401-213">Aby uzyskać instrukcje dotyczące przekazywania pliku hello, zobacz [dodać tooAzure aplikacji Java aplikacji usługi sieci Web aplikacji](../app-service-web/web-sites-java-add-app.md).</span><span class="sxs-lookup"><span data-stu-id="4e401-213">For instructions on uploading hello file, see [Add a Java application tooAzure App Service Web Apps](../app-service-web/web-sites-java-add-app.md).</span></span>
   
    <span data-ttu-id="4e401-214">Pliku WAR powitania po przekazane toohello katalogu webapps środowisko uruchomieniowe hello wykryje został dodany i załaduje go automatycznie.</span><span class="sxs-lookup"><span data-stu-id="4e401-214">Once hello WAR file is uploaded toohello webapps directory, hello runtime environment will detect that you've added it and will automatically load it.</span></span>
4. <span data-ttu-id="4e401-215">tooview Zakończono produktu, przejdź toohttp://YOUR\_LOKACJI\_NAME.azurewebsites.net/azure-java-sample/ i zacznij dodawać zadania!</span><span class="sxs-lookup"><span data-stu-id="4e401-215">tooview your finished product, navigate toohttp://YOUR\_SITE\_NAME.azurewebsites.net/azure-java-sample/ and start adding your tasks!</span></span>

## <span data-ttu-id="4e401-216"><a id="GetProject"></a>Pobierz hello projektu z usługi GitHub</span><span class="sxs-lookup"><span data-stu-id="4e401-216"><a id="GetProject"></a>Get hello project from GitHub</span></span>
<span data-ttu-id="4e401-217">Wszystkie przykłady hello w tym samouczku są objęte hello [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) projektu w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="4e401-217">All hello samples in this tutorial are included in hello [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) project on GitHub.</span></span> <span data-ttu-id="4e401-218">Projekt todo hello tooimport do środowiska Eclipse, upewnij się, masz hello oprogramowanie i zasobów wymienionych w hello [wymagania wstępne](#Prerequisites) sekcji, a następnie hello następujące:</span><span class="sxs-lookup"><span data-stu-id="4e401-218">tooimport hello todo project into Eclipse, ensure you have hello software and resources listed in hello [Prerequisites](#Prerequisites) section, then do hello following:</span></span>

1. <span data-ttu-id="4e401-219">Zainstaluj [Projekt Lombok](http://projectlombok.org/).</span><span class="sxs-lookup"><span data-stu-id="4e401-219">Install [Project Lombok](http://projectlombok.org/).</span></span> <span data-ttu-id="4e401-220">Lombok jest używane toogenerate konstruktorów, metod pobierających i ustawiających w projekcie hello.</span><span class="sxs-lookup"><span data-stu-id="4e401-220">Lombok is used toogenerate constructors, getters, setters in hello project.</span></span> <span data-ttu-id="4e401-221">Po pobraniu pliku lombok.jar hello, kliknij go dwukrotnie tooinstall go lub go zainstalować z wiersza polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="4e401-221">Once you have downloaded hello lombok.jar file, double-click it tooinstall it or install it from hello command line.</span></span>
2. <span data-ttu-id="4e401-222">Jeśli środowisko Eclipse jest otwarte, zamknij ją i uruchom go ponownie tooload Lombok.</span><span class="sxs-lookup"><span data-stu-id="4e401-222">If Eclipse is open, close it and restart it tooload Lombok.</span></span>
3. <span data-ttu-id="4e401-223">W środowisku Eclipse na powitania **pliku** menu, kliknij przycisk **importu**.</span><span class="sxs-lookup"><span data-stu-id="4e401-223">In Eclipse, on hello **File** menu, click **Import**.</span></span>
4. <span data-ttu-id="4e401-224">W hello **importu** okna, kliknij przycisk **Git**, kliknij przycisk **projekty z Git**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="4e401-224">In hello **Import** window, click **Git**, click **Projects from Git**, and then click **Next**.</span></span>
5. <span data-ttu-id="4e401-225">Na powitania **wybierz źródło repozytorium** kliknij **identyfikatora URI w klonowania**.</span><span class="sxs-lookup"><span data-stu-id="4e401-225">On hello **Select Repository Source** screen, click **Clone URI**.</span></span>
6. <span data-ttu-id="4e401-226">Na powitania **źródło repozytorium Git** ekranie powitania **URI** wprowadź https://github.com/Azure-Samples/java-todo-app.git, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="4e401-226">On hello **Source Git Repository** screen, in hello **URI** box, enter https://github.com/Azure-Samples/java-todo-app.git, and then click **Next**.</span></span>
7. <span data-ttu-id="4e401-227">Na powitania **wybór gałęzi** ekranu, upewnij się, że **wzorca** jest zaznaczone, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="4e401-227">On hello **Branch Selection** screen, ensure that **master** is selected, and then click **Next**.</span></span>
8. <span data-ttu-id="4e401-228">Na powitania **lokalne miejsce docelowe** kliknij **Przeglądaj** tooselect folder, w którym mogą zostać skopiowane hello repozytorium, a następnie kliknij **dalej**.</span><span class="sxs-lookup"><span data-stu-id="4e401-228">On hello **Local Destination** screen, click **Browse** tooselect a folder where hello repository can be copied, and then click **Next**.</span></span>
9. <span data-ttu-id="4e401-229">Na powitania **wybierz toouse Kreatora importowania projektów** ekranu, upewnij się, że **importowanie istniejących projektów** jest zaznaczone, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="4e401-229">On hello **Select a wizard toouse for importing projects** screen, ensure that **Import existing projects** is selected, and then click **Next**.</span></span>
10. <span data-ttu-id="4e401-230">Na powitania **Import projektów** ekranu, usuń zaznaczenie hello **DocumentDB** projektu, a następnie kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="4e401-230">On hello **Import Projects** screen, unselect hello **DocumentDB** project, and then click **Finish**.</span></span> <span data-ttu-id="4e401-231">Projekt DocumentDB Hello zawiera hello Azure rozwiązania Cosmos DB Java SDK, który zostanie dodany jako zależność zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="4e401-231">hello DocumentDB project contains hello Azure Cosmos DB Java SDK, which we will add as a dependency instead.</span></span>
11. <span data-ttu-id="4e401-232">W **Eksplorator projektów**, przejdź tooazure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java i Zastąp wartości HOST oraz MASTER_KEY hello hello URI oraz PRIMARY KEY dla Twoje konto bazy danych Azure rozwiązania Cosmos, a następnie zapisz plik hello.</span><span class="sxs-lookup"><span data-stu-id="4e401-232">In **Project Explorer**, navigate tooazure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java and replace hello HOST and MASTER_KEY values with hello URI and PRIMARY KEY for your Azure Cosmos DB account, and then save hello file.</span></span> <span data-ttu-id="4e401-233">Aby uzyskać więcej informacji, zobacz [Krok 1. Tworzenie konta bazy danych Azure DB rozwiązania Cosmos](#CreateDB).</span><span class="sxs-lookup"><span data-stu-id="4e401-233">For more information, see [Step 1. Create an Azure Cosmos DB database account](#CreateDB).</span></span>
12. <span data-ttu-id="4e401-234">W **Eksplorator projektów**, powitania kliknij prawym przyciskiem myszy **azure-documentdb-java-sample**, kliknij przycisk **ścieżkę kompilacji**, a następnie kliknij przycisk **Konfigurowanie kompilacji ścieżki**.</span><span class="sxs-lookup"><span data-stu-id="4e401-234">In **Project Explorer**, right click hello **azure-documentdb-java-sample**, click **Build Path**, and then click **Configure Build Path**.</span></span>
13. <span data-ttu-id="4e401-235">Na powitania **ścieżka kompilacji języka Java** ekranu w okienku po prawej stronie powitania, wybierz hello **biblioteki** , a następnie kliknij pozycję **Dodaj zewnętrzne JARs**.</span><span class="sxs-lookup"><span data-stu-id="4e401-235">On hello **Java Build Path** screen, in hello right pane, select hello **Libraries** tab, and then click **Add External JARs**.</span></span> <span data-ttu-id="4e401-236">Przejdź do lokalizacji pliku lombok.jar hello toohello, a następnie kliknij przycisk **Otwórz**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="4e401-236">Navigate toohello location of hello lombok.jar file, and click **Open**, and then click **OK**.</span></span>
14. <span data-ttu-id="4e401-237">Użyj kroku 12 tooopen hello **właściwości** okna ponownie, a następnie w okienku po lewej stronie powitania kliknij **docelowe środowiska uruchomieniowe**.</span><span class="sxs-lookup"><span data-stu-id="4e401-237">Use step 12 tooopen hello **Properties** window again, and then in hello left pane click **Targeted Runtimes**.</span></span>
15. <span data-ttu-id="4e401-238">Na powitania **docelowe środowiska uruchomieniowe** kliknij **nowy**, wybierz pozycję **Apache Tomcat v7.0**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="4e401-238">On hello **Targeted Runtimes** screen, click **New**, select **Apache Tomcat v7.0**, and then click **OK**.</span></span>
16. <span data-ttu-id="4e401-239">Użyj kroku 12 tooopen hello **właściwości** okna ponownie, a następnie w okienku po lewej stronie powitania kliknij **aspekty projektu**.</span><span class="sxs-lookup"><span data-stu-id="4e401-239">Use step 12 tooopen hello **Properties** window again, and then in hello left pane click **Project Facets**.</span></span>
17. <span data-ttu-id="4e401-240">Na powitania **aspekty projektu** ekranu wybierz **dynamiczny moduł sieci Web** i **Java**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="4e401-240">On hello **Project Facets** screen, select **Dynamic Web Module** and **Java**, and then click **OK**.</span></span>
18. <span data-ttu-id="4e401-241">Na powitania **serwerów** u dołu ekranu hello powitania kliknij prawym przyciskiem myszy **Tomcat v7.0 Server at localhost** , a następnie kliknij przycisk **Dodawanie i usuwanie**.</span><span class="sxs-lookup"><span data-stu-id="4e401-241">On hello **Servers** tab at hello bottom of hello screen, right-click **Tomcat v7.0 Server at localhost** and then click **Add and Remove**.</span></span>
19. <span data-ttu-id="4e401-242">Na powitania **Dodawanie i usuwanie** okna, Przenieś **azure-documentdb-java-sample** toohello **skonfigurowana** , a następnie kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="4e401-242">On hello **Add and Remove** window, move **azure-documentdb-java-sample** toohello **Configured** box, and then click **Finish**.</span></span>
20. <span data-ttu-id="4e401-243">W hello **serwerów** kliknij prawym przyciskiem myszy **Tomcat v7.0 Server at localhost**, a następnie kliknij przycisk **ponownego uruchomienia**.</span><span class="sxs-lookup"><span data-stu-id="4e401-243">In hello **Servers** tab, right-click **Tomcat v7.0 Server at localhost**, and then click **Restart**.</span></span>
21. <span data-ttu-id="4e401-244">W przeglądarce Przejdź toohttp://localhost:8080 / azure-documentdb-java-sample / i zacznij dodawać tooyour listy zadań.</span><span class="sxs-lookup"><span data-stu-id="4e401-244">In a browser, navigate toohttp://localhost:8080/azure-documentdb-java-sample/ and start adding tooyour task list.</span></span> <span data-ttu-id="4e401-245">Należy pamiętać, że jeśli zmieniono domyślne wartości portów, Zmień wybraną wartość toohello 8080.</span><span class="sxs-lookup"><span data-stu-id="4e401-245">Note that if you changed your default port values, change 8080 toohello value you selected.</span></span>
22. <span data-ttu-id="4e401-246">toodeploy tooan Twojego projektu witryny sieci web platformy Azure, zobacz [krok 6. Wdrażanie programu tooAzure aplikacji witryny sieci Web](#Deploy).</span><span class="sxs-lookup"><span data-stu-id="4e401-246">toodeploy your project tooan Azure web site, see [Step 6. Deploy your application tooAzure Web Sites](#Deploy).</span></span>

[1]: media/documentdb-java-application/keys.png
