---
title: "Samouczek tworzenia aplikacji w języku Java za pomocą usługi Azure Cosmos DB | Microsoft Docs"
description: "W tym samouczku aplikacji sieci web Java pokazano, jak używać bazy danych rozwiązania Cosmos Azure i interfejsu API usługi DocumentDB do przechowywania i uzyskiwanie dostępu do danych z aplikacji w języku Java hostowanej przez usługę Azure Websites."
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
ms.openlocfilehash: 292115b5603c6f05a5eab3492d4b3e2096b58ed2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="build-a-java-web-application-using-azure-cosmos-db-and-the-documentdb-api"></a><span data-ttu-id="0fd82-104">Tworzenie aplikacji sieci web Java, przy użyciu bazy danych rozwiązania Cosmos Azure i interfejsu API usługi DocumentDB</span><span class="sxs-lookup"><span data-stu-id="0fd82-104">Build a Java web application using Azure Cosmos DB and the DocumentDB API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0fd82-105">.NET</span><span class="sxs-lookup"><span data-stu-id="0fd82-105">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="0fd82-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="0fd82-106">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="0fd82-107">Java</span><span class="sxs-lookup"><span data-stu-id="0fd82-107">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="0fd82-108">Python</span><span class="sxs-lookup"><span data-stu-id="0fd82-108">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="0fd82-109">W tym samouczku aplikacji sieci web Java przedstawia sposób użycia [bazy danych programu Microsoft Azure rozwiązania Cosmos](https://azure.microsoft.com/services/cosmos-db/) Usługa do przechowywania i uzyskać dostęp do danych z poziomu aplikacji Java hostowanej przez aplikacje sieci Web usługi aplikacji Azure.</span><span class="sxs-lookup"><span data-stu-id="0fd82-109">This Java web application tutorial shows you how to use the [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service to store and access data from a Java application hosted on Azure App Service Web Apps.</span></span> <span data-ttu-id="0fd82-110">W tym artykule przedstawiono:</span><span class="sxs-lookup"><span data-stu-id="0fd82-110">In this topic, you will learn:</span></span>

* <span data-ttu-id="0fd82-111">Jak utworzyć prostą aplikację JavaServer stron (JSP) w programie Eclipse.</span><span class="sxs-lookup"><span data-stu-id="0fd82-111">How to build a basic JavaServer Pages (JSP) application in Eclipse.</span></span>
* <span data-ttu-id="0fd82-112">Jak pracować z usługą Azure Cosmos DB przy użyciu [zestawu SDK języka Java dla usługi Azure Cosmos DB](https://github.com/Azure/azure-documentdb-java).</span><span class="sxs-lookup"><span data-stu-id="0fd82-112">How to work with the Azure Cosmos DB service using the [Azure Cosmos DB Java SDK](https://github.com/Azure/azure-documentdb-java).</span></span>

<span data-ttu-id="0fd82-113">W tym samouczku aplikacji w języku Java pokazano, jak utworzyć aplikację do zarządzania zadaniami opartą na sieci Web, która pozwala na tworzenie, pobieranie i oznaczanie zadań jako ukończonych, jak pokazano na poniższej ilustracji.</span><span class="sxs-lookup"><span data-stu-id="0fd82-113">This Java application tutorial shows you how to create a web-based task-management application that enables you to create, retrieve, and mark tasks as complete, as shown in the following image.</span></span> <span data-ttu-id="0fd82-114">Każde z zadań z listy zadań do wykonania będzie przechowywane jako dokument JSON w usłudze Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0fd82-114">Each of the tasks in the ToDo list are stored as JSON documents in Azure Cosmos DB.</span></span>

![Aplikacja My ToDo List w języku Java](./media/documentdb-java-application/image1.png)

> [!TIP]
> <span data-ttu-id="0fd82-116">Ten samouczek tworzenia aplikacji zakłada, że masz już pewne doświadczenie w korzystaniu z języka Java.</span><span class="sxs-lookup"><span data-stu-id="0fd82-116">This application development tutorial assumes that you have prior experience using Java.</span></span> <span data-ttu-id="0fd82-117">Jeśli nie znasz języka Java lub [wstępnie wymaganych narzędzi](#Prerequisites), zalecamy pobranie kompletnego projektu [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) z usługi GitHub i skompilowanie go zgodnie z [instrukcjami znajdującymi się na końcu artykułu](#GetProject).</span><span class="sxs-lookup"><span data-stu-id="0fd82-117">If you are new to Java or the [prerequisite tools](#Prerequisites), we recommend downloading the complete [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) project from GitHub and building it using [the instructions at the end of this article](#GetProject).</span></span> <span data-ttu-id="0fd82-118">Po jego skompilowaniu możesz przejrzeć ten artykuł, aby przeanalizować kod w kontekście projektu.</span><span class="sxs-lookup"><span data-stu-id="0fd82-118">Once you have it built, you can review the article to gain insight on the code in the context of the project.</span></span>  
> 
> 

## <span data-ttu-id="0fd82-119"><a id="Prerequisites"></a>Wymagania wstępne dotyczące tego samouczka aplikacji sieci Web w języku Java</span><span class="sxs-lookup"><span data-stu-id="0fd82-119"><a id="Prerequisites"></a>Prerequisites for this Java web application tutorial</span></span>
<span data-ttu-id="0fd82-120">Przed rozpoczęciem korzystania z tego samouczka tworzenia aplikacji należy dysponować następującymi elementami:</span><span class="sxs-lookup"><span data-stu-id="0fd82-120">Before you begin this application development tutorial, you must have the following:</span></span>

* <span data-ttu-id="0fd82-121">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0fd82-121">An active Azure account.</span></span> <span data-ttu-id="0fd82-122">Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="0fd82-122">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="0fd82-123">Aby uzyskać szczegółowe informacje, zobacz [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="0fd82-123">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/)</span></span>

    <span data-ttu-id="0fd82-124">LUB</span><span class="sxs-lookup"><span data-stu-id="0fd82-124">OR</span></span>

    <span data-ttu-id="0fd82-125">Lokalna instalacja [emulatora usługi Azure Cosmos DB](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="0fd82-125">A local installation of the [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="0fd82-126">[Zestaw Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="0fd82-126">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
* [<span data-ttu-id="0fd82-127">Środowisko Eclipse IDE for Java EE Developers.</span><span class="sxs-lookup"><span data-stu-id="0fd82-127">Eclipse IDE for Java EE Developers.</span></span>](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunasr1)
* [<span data-ttu-id="0fd82-128">Witryna sieci Web Azure ze środowiskiem uruchomieniowym Java (np. Tomcat lub Jetty) włączone.</span><span class="sxs-lookup"><span data-stu-id="0fd82-128">An Azure Web Site with a Java runtime environment (e.g. Tomcat or Jetty) enabled.</span></span>](../app-service-web/web-sites-java-get-started.md)

<span data-ttu-id="0fd82-129">Jeśli instalujesz te narzędzia po raz pierwszy, witryna coreservlets.com zawiera omówienie procesu instalacji w artykule [Tutorial: Installing TomCat7 and Using it with Eclipse](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) (Samouczek: Instalacja środowiska TomCat7 i używanie go ze środowiskiem Eclipse) w sekcji Quick Start (Szybki start).</span><span class="sxs-lookup"><span data-stu-id="0fd82-129">If you're installing these tools for the first time, coreservlets.com provides a walk-through of the installation process in the Quick Start section of their [Tutorial: Installing TomCat7 and Using it with Eclipse](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) article.</span></span>

## <span data-ttu-id="0fd82-130"><a id="CreateDB"></a>Krok 1: Tworzenie konta bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="0fd82-130"><a id="CreateDB"></a>Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="0fd82-131">Zacznijmy od utworzenia konta usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0fd82-131">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="0fd82-132">Jeśli masz już konto lub jeśli korzystasz z emulatora usługi Azure Cosmos DB na potrzeby tego samouczka, możesz od razu przejść do sekcji [Krok 2. Tworzenie aplikacji Java JSP](#CreateJSP).</span><span class="sxs-lookup"><span data-stu-id="0fd82-132">If you already have an account or if you are using the Azure Cosmos DB Emulator for this tutorial, you can skip to [Step 2: Create the Java JSP application](#CreateJSP).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

## <span data-ttu-id="0fd82-133"><a id="CreateJSP"></a>Krok 2. Tworzenie aplikacji Java JSP</span><span class="sxs-lookup"><span data-stu-id="0fd82-133"><a id="CreateJSP"></a>Step 2: Create the Java JSP application</span></span>
<span data-ttu-id="0fd82-134">Aby utworzyć aplikację JSP:</span><span class="sxs-lookup"><span data-stu-id="0fd82-134">To create the JSP application:</span></span>

1. <span data-ttu-id="0fd82-135">Zacznijmy od utworzenia projektu języka Java.</span><span class="sxs-lookup"><span data-stu-id="0fd82-135">First, we’ll start off by creating a Java project.</span></span> <span data-ttu-id="0fd82-136">Uruchom środowisko Eclipse, a następnie w menu **File** (Plik) kliknij polecenie **New** (Nowy), a potem kliknij polecenie **Dynamic Web Project** (Dynamiczny projekt sieci Web).</span><span class="sxs-lookup"><span data-stu-id="0fd82-136">Start Eclipse, then click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="0fd82-137">Jeśli nie widzisz polecenia **Dynamic Web Project** (Dynamiczny projekt sieci Web) na liście dostępnych projektów, wykonaj następujące czynności: w menu **File** (Plik) kliknij polecenie **New** (Nowy), kliknij polecenie **Project**... (Projekt...), rozwiń pozycję **Web** (Sieć Web), kliknij pozycję **Dynamic Web Project** (Dynamiczny projekt sieci Web) i kliknij przycisk **Next** (Dalej).</span><span class="sxs-lookup"><span data-stu-id="0fd82-137">If you don’t see **Dynamic Web Project** listed as an available project, do the following: click **File**, click **New**, click **Project**…, expand **Web**, click **Dynamic Web Project**, and click **Next**.</span></span>
   
    ![Tworzenie aplikacji Java JSP](./media/documentdb-java-application/image10.png)
2. <span data-ttu-id="0fd82-139">Wprowadź nazwę projektu w polu **Project name** (Nazwa projektu) i z menu rozwijanego **Target Runtime** (Docelowe środowisko uruchomieniowe) opcjonalnie wybierz wartość (np. Apache Tomcat v7.0), a następnie kliknij przycisk **Finish** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="0fd82-139">Enter a project name in the **Project name** box, and in the **Target Runtime** drop-down menu, optionally select a value (e.g. Apache Tomcat v7.0), and then click **Finish**.</span></span> <span data-ttu-id="0fd82-140">Wybranie docelowego środowiska uruchomieniowego umożliwia uruchamianie projektu lokalnie za pośrednictwem środowiska Eclipse.</span><span class="sxs-lookup"><span data-stu-id="0fd82-140">Selecting a target runtime enables you to run your project locally through Eclipse.</span></span>
3. <span data-ttu-id="0fd82-141">W środowisku Eclipse w widoku Project Explorer (Eksplorator projektów) rozwiń projekt.</span><span class="sxs-lookup"><span data-stu-id="0fd82-141">In Eclipse, in the Project Explorer view, expand your project.</span></span> <span data-ttu-id="0fd82-142">Kliknij prawym przyciskiem myszy folder **WebContent**, kliknij polecenie **New** (Nowy), a następnie kliknij polecenie **JSP File** (Plik JSP).</span><span class="sxs-lookup"><span data-stu-id="0fd82-142">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>
4. <span data-ttu-id="0fd82-143">W oknie dialogowym **New JSP File** (Nowy plik JSP) nazwij plik **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="0fd82-143">In the **New JSP File** dialog box, name the file **index.jsp**.</span></span> <span data-ttu-id="0fd82-144">Pozostaw folder **WebContent** jako folder nadrzędny, w sposób pokazany na poniższej ilustracji, a następnie kliknij przycisk **Next** (Dalej).</span><span class="sxs-lookup"><span data-stu-id="0fd82-144">Keep the parent folder as **WebContent**, as shown in the following illustration, and then click **Next**.</span></span>
   
    ![Tworzenie nowego pliku JSP — samouczek aplikacji sieci Web w języku Java](./media/documentdb-java-application/image11.png)
5. <span data-ttu-id="0fd82-146">W oknie dialogowym **Select JSP Template** (Wybierz szablon pliku JSP) na potrzeby tego samouczka wybierz szablon **New JSP File (html)**, a następnie kliknij przycisk **Finish** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="0fd82-146">In the **Select JSP Template** dialog box, for the purpose of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>
6. <span data-ttu-id="0fd82-147">Po otwarciu pliku index.jsp w środowisku Eclipse dodaj tekst do wyświetlenia **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="0fd82-147">When the index.jsp file opens in Eclipse, add text to display **Hello World!**</span></span> <span data-ttu-id="0fd82-148">wewnątrz istniejącego elementu <body>.</span><span class="sxs-lookup"><span data-stu-id="0fd82-148">within the existing <body> element.</span></span> <span data-ttu-id="0fd82-149">Zaktualizowana zawartość elementu <body> powinna wyglądać podobnie do następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="0fd82-149">Your updated <body> content should look like the following code:</span></span>
   
        <body>
            <% out.println("Hello World!"); %>
        </body>
7. <span data-ttu-id="0fd82-150">Zapisz plik index.jsp.</span><span class="sxs-lookup"><span data-stu-id="0fd82-150">Save the index.jsp file.</span></span>
8. <span data-ttu-id="0fd82-151">Jeśli docelowe środowisko uruchomieniowe zostało ustawione w kroku 2, możesz kliknąć pozycję **Project** (Projekt), a następnie pozycję **Run** (Uruchom), aby uruchomić aplikację JSP lokalnie:</span><span class="sxs-lookup"><span data-stu-id="0fd82-151">If you set a target runtime in step 2, you can click **Project** and then **Run** to run your JSP application locally:</span></span>
   
    ![Witaj świecie – samouczek aplikacji w języku Java](./media/documentdb-java-application/image12.png)

## <span data-ttu-id="0fd82-153"><a id="InstallSDK"></a>Krok 3. Instalacja zestawu SDK Java usługi DocumentDB</span><span class="sxs-lookup"><span data-stu-id="0fd82-153"><a id="InstallSDK"></a>Step 3: Install the DocumentDB Java SDK</span></span>
<span data-ttu-id="0fd82-154">Najprostszym sposobem pobrania zestawu SDK Java usługi DocumentDB i jego zależności jest skorzystanie z usługi [Apache Maven](http://maven.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="0fd82-154">The easiest way to pull in the DocumentDB Java SDK and its dependencies is through [Apache Maven](http://maven.apache.org/).</span></span>

<span data-ttu-id="0fd82-155">Aby to zrobić, należy przekonwertować projekt na projekt maven, wykonując następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="0fd82-155">To do this, you will need to convert your project to a maven project by completing the following steps:</span></span>

1. <span data-ttu-id="0fd82-156">Kliknij prawym przyciskiem myszy projekt w widoku Project Explorer (Eksplorator projektów), kliknij polecenie **Configure** (Konfiguruj), kliknij pozycję **Convert to Maven Project** (Konwertuj na projekt Maven).</span><span class="sxs-lookup"><span data-stu-id="0fd82-156">Right-click your project in the Project Explorer, click **Configure**, click **Convert to Maven Project**.</span></span>
2. <span data-ttu-id="0fd82-157">W oknie **Create new POM** (Utwórz nowy plik POM) zaakceptuj wartości domyślne i kliknij przycisk **Finish** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="0fd82-157">In the **Create new POM** window, accept the defaults and click **Finish**.</span></span>
3. <span data-ttu-id="0fd82-158">W widoku **Project Explorer** (Eksplorator projektów) otwórz plik pom.xml.</span><span class="sxs-lookup"><span data-stu-id="0fd82-158">In **Project Explorer**, open the pom.xml file.</span></span>
4. <span data-ttu-id="0fd82-159">Na karcie **Dependencies** (Zależności) w okienku **Dependencies** (Zależności) kliknij pozycję **Add** (Dodaj).</span><span class="sxs-lookup"><span data-stu-id="0fd82-159">On the **Dependencies** tab, in the **Dependencies** pane, click **Add**.</span></span>
5. <span data-ttu-id="0fd82-160">W oknie **Select Dependency** (Wybierz zależność) wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="0fd82-160">In the **Select Dependency** window, do the following:</span></span>
   
   * <span data-ttu-id="0fd82-161">W **identyfikator grupy** wprowadź com.microsoft.azure.</span><span class="sxs-lookup"><span data-stu-id="0fd82-161">In the **Group Id** box, enter com.microsoft.azure.</span></span>
   * <span data-ttu-id="0fd82-162">W **identyfikator artefaktu** wprowadź azure-documentdb.</span><span class="sxs-lookup"><span data-stu-id="0fd82-162">In the **Artifact Id** box, enter azure-documentdb.</span></span>
   * <span data-ttu-id="0fd82-163">W **wersji** wprowadź 1.5.1.</span><span class="sxs-lookup"><span data-stu-id="0fd82-163">In the **Version** box, enter 1.5.1.</span></span>
     
   ![Instalacja zestawu SDK Java usługi DocumentDB](./media/documentdb-java-application/image13.png)
     
   * <span data-ttu-id="0fd82-165">Lub Dodaj kod XML zależności dla identyfikatora grupy i identyfikator artefaktu bezpośrednio do pliku pom.xml za pomocą edytora tekstu:</span><span class="sxs-lookup"><span data-stu-id="0fd82-165">Or add the dependency XML for Group Id and Artifact Id directly to the pom.xml via a text editor:</span></span>
     
        <span data-ttu-id="0fd82-166"><dependency><groupId>com.microsoft.azure</groupId> <artifactId>azure-documentdb</artifactId> <version>1.9.1</version></dependency></span><span class="sxs-lookup"><span data-stu-id="0fd82-166"><dependency> <groupId>com.microsoft.azure</groupId> <artifactId>azure-documentdb</artifactId> <version>1.9.1</version> </dependency></span></span>
6. <span data-ttu-id="0fd82-167">Kliknij przycisk **OK** i Maven zostanie zainstalowany zestaw SDK Java usługi DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="0fd82-167">Click **OK** and Maven will install the DocumentDB Java SDK.</span></span>
7. <span data-ttu-id="0fd82-168">Zapisz plik pom.xml.</span><span class="sxs-lookup"><span data-stu-id="0fd82-168">Save the pom.xml file.</span></span>

## <span data-ttu-id="0fd82-169"><a id="UseService"></a>Krok 4. Korzystanie z usługi Azure Cosmos DB w aplikacji Java</span><span class="sxs-lookup"><span data-stu-id="0fd82-169"><a id="UseService"></a>Step 4: Using the Azure Cosmos DB service in a Java application</span></span>
1. <span data-ttu-id="0fd82-170">Najpierw zdefiniujmy obiekt TodoItem w TodoItem.java:</span><span class="sxs-lookup"><span data-stu-id="0fd82-170">First, let's define the TodoItem object in TodoItem.java:</span></span>
   
        @Data
        @Builder
        public class TodoItem {
            private String category;
            private boolean complete;
            private String id;
            private String name;
        }
   
    <span data-ttu-id="0fd82-171">W tym projekcie użyto [Projektu Lombok](http://projectlombok.org/), aby wygenerować konstruktor, metody pobierające, metody ustawiające i budowniczego.</span><span class="sxs-lookup"><span data-stu-id="0fd82-171">In this project, we are using [Project Lombok](http://projectlombok.org/) to generate the constructor, getters, setters, and a builder.</span></span> <span data-ttu-id="0fd82-172">Można też ręcznie napisać ten kod lub wygenerować go za pomocą środowiska IDE.</span><span class="sxs-lookup"><span data-stu-id="0fd82-172">Alternatively, you can write this code manually or have the IDE generate it.</span></span>
2. <span data-ttu-id="0fd82-173">Aby wywołać usługę Azure Cosmos DB, trzeba utworzyć obiekt klasy **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="0fd82-173">To invoke the Azure Cosmos DB service, you must instantiate a new **DocumentClient**.</span></span> <span data-ttu-id="0fd82-174">Ogólnie rzecz biorąc, lepiej jest użyć ponownie obiektu **DocumentClient** niż konstruować nowego klienta dla kolejnych żądań.</span><span class="sxs-lookup"><span data-stu-id="0fd82-174">In general, it is best to reuse the **DocumentClient** - rather than construct a new client for each subsequent request.</span></span> <span data-ttu-id="0fd82-175">Klienta można ponownie użyć, opakowując go w **DocumentClientFactory**.</span><span class="sxs-lookup"><span data-stu-id="0fd82-175">We can reuse the client by wrapping the client in a **DocumentClientFactory**.</span></span> <span data-ttu-id="0fd82-176">W DocumentClientFactory.java, należy wkleić wartości URI oraz PRIMARY KEY, zapisane do Schowka w [krok 1](#CreateDB).</span><span class="sxs-lookup"><span data-stu-id="0fd82-176">In DocumentClientFactory.java, you need to paste the URI and PRIMARY KEY value you saved to your clipboard in [step 1](#CreateDB).</span></span> <span data-ttu-id="0fd82-177">Zastąp [YOUR\_ENDPOINT\_HERE] wartością URI, a [YOUR\_KEY\_HERE] zastąp wartością PRIMARY KEY.</span><span class="sxs-lookup"><span data-stu-id="0fd82-177">Replace [YOUR\_ENDPOINT\_HERE] with your URI and replace [YOUR\_KEY\_HERE] with your PRIMARY KEY.</span></span>
   
        private static final String HOST = "[YOUR_ENDPOINT_HERE]";
        private static final String MASTER_KEY = "[YOUR_KEY_HERE]";
   
        private static DocumentClient documentClient = new DocumentClient(HOST, MASTER_KEY,
                        ConnectionPolicy.GetDefault(), ConsistencyLevel.Session);
   
        public static DocumentClient getDocumentClient() {
            return documentClient;
        }
3. <span data-ttu-id="0fd82-178">Teraz utwórzmy obiekt dostępu do danych (DAO, Data Access Object), aby uabstrakcyjnić utrwalanie zadań do wykonania w usłudze Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0fd82-178">Now let's create a Data Access Object (DAO) to abstract persisting our ToDo items to Azure Cosmos DB.</span></span>
   
    <span data-ttu-id="0fd82-179">Aby zapisać zadania do wykonania w kolekcji, klient musi wiedzieć, w której bazie danych i kolekcji powinien je zachowywać (jak to jest wskazane przez linki do samego siebie).</span><span class="sxs-lookup"><span data-stu-id="0fd82-179">In order to save ToDo items to a collection, the client needs to know which database and collection to persist to (as referenced by self-links).</span></span> <span data-ttu-id="0fd82-180">Ogólnie rzecz biorąc, najlepiej jest zapisać w pamięci podręcznej obiekty bazy danych i kolekcji, tam gdzie to jest możliwe, aby uniknąć dodatkowych połączeń do bazy danych.</span><span class="sxs-lookup"><span data-stu-id="0fd82-180">In general, it is best to cache the database and collection when possible to avoid additional round-trips to the database.</span></span>
   
    <span data-ttu-id="0fd82-181">Poniższy kod ilustruje, w jaki sposób pobrać bazę danych i kolekcję, jeśli one istnieją, lub utworzyć nowe obiekty, jeśli nie istnieją:</span><span class="sxs-lookup"><span data-stu-id="0fd82-181">The following code illustrates how to retrieve our database and collection, if it exists, or create a new one if it doesn't exist:</span></span>
   
        public class DocDbDao implements TodoDao {
            // The name of our database.
            private static final String DATABASE_ID = "TodoDB";
   
            // The name of our collection.
            private static final String COLLECTION_ID = "TodoCollection";
   
            // The Azure Cosmos DB Client
            private static DocumentClient documentClient = DocumentClientFactory
                    .getDocumentClient();
   
            // Cache for the database object, so we don't have to query for it to
            // retrieve self links.
            private static Database databaseCache;
   
            // Cache for the collection object, so we don't have to query for it to
            // retrieve self links.
            private static DocumentCollection collectionCache;
   
            private Database getTodoDatabase() {
                if (databaseCache == null) {
                    // Get the database if it exists
                    List<Database> databaseList = documentClient
                            .queryDatabases(
                                    "SELECT * FROM root r WHERE r.id='" + DATABASE_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (databaseList.size() > 0) {
                        // Cache the database object so we won't have to query for it
                        // later to retrieve the selfLink.
                        databaseCache = databaseList.get(0);
                    } else {
                        // Create the database if it doesn't exist.
                        try {
                            Database databaseDefinition = new Database();
                            databaseDefinition.setId(DATABASE_ID);
   
                            databaseCache = documentClient.createDatabase(
                                    databaseDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - the app wasn't
                            // able to query or create the collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return databaseCache;
            }
   
            private DocumentCollection getTodoCollection() {
                if (collectionCache == null) {
                    // Get the collection if it exists.
                    List<DocumentCollection> collectionList = documentClient
                            .queryCollections(
                                    getTodoDatabase().getSelfLink(),
                                    "SELECT * FROM root r WHERE r.id='" + COLLECTION_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (collectionList.size() > 0) {
                        // Cache the collection object so we won't have to query for it
                        // later to retrieve the selfLink.
                        collectionCache = collectionList.get(0);
                    } else {
                        // Create the collection if it doesn't exist.
                        try {
                            DocumentCollection collectionDefinition = new DocumentCollection();
                            collectionDefinition.setId(COLLECTION_ID);
   
                            collectionCache = documentClient.createCollection(
                                    getTodoDatabase().getSelfLink(),
                                    collectionDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - the app wasn't
                            // able to query or create the collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return collectionCache;
            }
        }
4. <span data-ttu-id="0fd82-182">Następnym krokiem jest napisanie kodu, który zachowuje obiekty TodoItem w kolekcji.</span><span class="sxs-lookup"><span data-stu-id="0fd82-182">The next step is to write some code to persist the TodoItems in to the collection.</span></span> <span data-ttu-id="0fd82-183">W tym przykładzie używamy narzędzia [Gson](https://code.google.com/p/google-gson/) do serializacji i deserializacji obiektów TodoItem typu Plain Old Java Objects (POJO) do dokumentów JSON.</span><span class="sxs-lookup"><span data-stu-id="0fd82-183">In this example, we will use [Gson](https://code.google.com/p/google-gson/) to serialize and de-serialize TodoItem Plain Old Java Objects (POJOs) to JSON documents.</span></span>
   
        // We'll use Gson for POJO <=> JSON serialization for this example.
        private static Gson gson = new Gson();
   
        @Override
        public TodoItem createTodoItem(TodoItem todoItem) {
            // Serialize the TodoItem as a JSON Document.
            Document todoItemDocument = new Document(gson.toJson(todoItem));
   
            // Annotate the document as a TodoItem for retrieval (so that we can
            // store multiple entity types in the collection).
            todoItemDocument.set("entityType", "todoItem");
   
            try {
                // Persist the document using the DocumentClient.
                todoItemDocument = documentClient.createDocument(
                        getTodoCollection().getSelfLink(), todoItemDocument, null,
                        false).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
5. <span data-ttu-id="0fd82-184">Podobnie jak do baz danych i kolekcji usługi Azure Cosmos DB, również do dokumentów można odwoływać się za pomocą linków do samego siebie.</span><span class="sxs-lookup"><span data-stu-id="0fd82-184">Like Azure Cosmos DB databases and collections, documents are also referenced by self-links.</span></span> <span data-ttu-id="0fd82-185">Poniższa funkcja pomocnicza pozwala nam pobrać dokumenty przy użyciu innego atrybutu (np. „id”), zamiast linku do samego siebie:</span><span class="sxs-lookup"><span data-stu-id="0fd82-185">The following helper function lets us retrieve documents by another attribute (e.g. "id") rather than self-link:</span></span>
   
        private Document getDocumentById(String id) {
            // Retrieve the document using the DocumentClient.
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
6. <span data-ttu-id="0fd82-186">Możemy użyć metody pomocniczej z kroku 5 do pobrania dokumentu TodoItem typu JSON przy użyciu atrybutu id, a następnie do deserializacji do obiektu typu POJO:</span><span class="sxs-lookup"><span data-stu-id="0fd82-186">We can use the helper method in step 5 to retrieve a TodoItem JSON document by id and then deserialize it to a POJO:</span></span>
   
        @Override
        public TodoItem readTodoItem(String id) {
            // Retrieve the document by id using our helper method.
            Document todoItemDocument = getDocumentById(id);
   
            if (todoItemDocument != null) {
                // De-serialize the document in to a TodoItem.
                return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
            } else {
                return null;
            }
        }
7. <span data-ttu-id="0fd82-187">Możemy również użyć obiektu DocumentClient, aby uzyskać kolekcję lub listę obiektów TodoItem przy użyciu usługi DocumentDB SQL:</span><span class="sxs-lookup"><span data-stu-id="0fd82-187">We can also use the DocumentClient to get a collection or list of TodoItems using DocumentDB SQL:</span></span>
   
        @Override
        public List<TodoItem> readTodoItems() {
            List<TodoItem> todoItems = new ArrayList<TodoItem>();
   
            // Retrieve the TodoItem documents
            List<Document> documentList = documentClient
                    .queryDocuments(getTodoCollection().getSelfLink(),
                            "SELECT * FROM root r WHERE r.entityType = 'todoItem'",
                            null).getQueryIterable().toList();
   
            // De-serialize the documents in to TodoItems.
            for (Document todoItemDocument : documentList) {
                todoItems.add(gson.fromJson(todoItemDocument.toString(),
                        TodoItem.class));
            }
   
            return todoItems;
        }
8. <span data-ttu-id="0fd82-188">Istnieje wiele sposobów, aby zaktualizować dokument za pomocą obiektu DocumentClient.</span><span class="sxs-lookup"><span data-stu-id="0fd82-188">There are many ways to update a document with the DocumentClient.</span></span> <span data-ttu-id="0fd82-189">W aplikacji zarządzającej listą zadań do wykonania chcemy mieć możliwość przełączania, czy zadanie zostało ukończone.</span><span class="sxs-lookup"><span data-stu-id="0fd82-189">In our Todo list application, we want to be able to toggle whether a TodoItem is complete.</span></span> <span data-ttu-id="0fd82-190">Można to osiągnąć przez zaktualizowanie atrybutu „complete” w dokumencie:</span><span class="sxs-lookup"><span data-stu-id="0fd82-190">This can be achieved by updating the "complete" attribute within the document:</span></span>
   
        @Override
        public TodoItem updateTodoItem(String id, boolean isComplete) {
            // Retrieve the document from the database
            Document todoItemDocument = getDocumentById(id);
   
            // You can update the document as a JSON document directly.
            // For more complex operations - you could de-serialize the document in
            // to a POJO, update the POJO, and then re-serialize the POJO back in to
            // a document.
            todoItemDocument.set("complete", isComplete);
   
            try {
                // Persist/replace the updated document.
                todoItemDocument = documentClient.replaceDocument(todoItemDocument,
                        null).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
9. <span data-ttu-id="0fd82-191">Wreszcie chcemy mieć możliwość usunięcia zadania do wykonania z naszej listy.</span><span class="sxs-lookup"><span data-stu-id="0fd82-191">Finally, we want the ability to delete a TodoItem from our list.</span></span> <span data-ttu-id="0fd82-192">W tym celu możemy użyć metody pomocniczej, którą napisaliśmy wcześniej, aby pobrać link do samego siebie, a następnie usunąć go za pomocą klienta:</span><span class="sxs-lookup"><span data-stu-id="0fd82-192">To do this, we can use the helper method we wrote earlier to retrieve the self-link and then tell the client to delete it:</span></span>
   
        @Override
        public boolean deleteTodoItem(String id) {
            // Azure Cosmos DB refers to documents by self link rather than id.
   
            // Query for the document to retrieve the self link.
            Document todoItemDocument = getDocumentById(id);
   
            try {
                // Delete the document by self link.
                documentClient.deleteDocument(todoItemDocument.getSelfLink(), null);
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return false;
            }
   
            return true;
        }

## <span data-ttu-id="0fd82-193"><a id="Wire"></a>Krok 5. Dołączenie pozostałej części projektu tworzenia aplikacji w języku Java</span><span class="sxs-lookup"><span data-stu-id="0fd82-193"><a id="Wire"></a>Step 5: Wiring the rest of the of Java application development project together</span></span>
<span data-ttu-id="0fd82-194">Teraz, gdy już zakończyliśmy fun bits - pozostało jest tworzenie interfejsu użytkownika szybki i połączenie go z obiektem DAO.</span><span class="sxs-lookup"><span data-stu-id="0fd82-194">Now that we've finished the fun bits - all that's left is to build a quick user interface and wire it up to our DAO.</span></span>

1. <span data-ttu-id="0fd82-195">Zacznijmy od utworzenia kontrolera do wywoływania obiektu DAO:</span><span class="sxs-lookup"><span data-stu-id="0fd82-195">First, let's start with building a controller to call our DAO:</span></span>
   
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
   
    <span data-ttu-id="0fd82-196">W bardziej złożonej aplikacji kontroler może zawierać skomplikowaną logikę biznesową nałożoną na obiekt DAO.</span><span class="sxs-lookup"><span data-stu-id="0fd82-196">In a more complex application, the controller may house complicated business logic on top of the DAO.</span></span>
2. <span data-ttu-id="0fd82-197">Następnie utworzymy serwlet do rozsyłania żądań HTTP do kontrolera:</span><span class="sxs-lookup"><span data-stu-id="0fd82-197">Next, we'll create a servlet to route HTTP requests to the controller:</span></span>
   
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
3. <span data-ttu-id="0fd82-198">Potrzebujemy interfejsu użytkownika sieci web do wyświetlenia dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0fd82-198">We'll need a web user interface to display to the user.</span></span> <span data-ttu-id="0fd82-199">Napiszmy od nowa utworzony wcześniej plik index.jsp:</span><span class="sxs-lookup"><span data-stu-id="0fd82-199">Let's re-write the index.jsp we created earlier:</span></span>
    ```html
        <html>
        <head>
          <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
          <meta http-equiv="X-UA-Compatible" content="IE=edge;" />
          <title>Azure Cosmos DB Java Sample</title>
   
          <!-- Bootstrap -->
          <link href="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css" rel="stylesheet">
   
          <style>
            /* Add padding to body for fixed nav bar */
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
   
            <!-- The ToDo List -->
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
   
          <!-- Placed at the end of the document so the pages load faster -->
          <script src="//ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js"></script>
          <script src="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js"></script>
          <script src="assets/todo.js"></script>
        </body>
        </html>
    ```
4. <span data-ttu-id="0fd82-200">I na koniec fragmentów kodu JavaScript po stronie klienta powiązać interfejs użytkownika sieci web i serwlet razem:</span><span class="sxs-lookup"><span data-stu-id="0fd82-200">And finally, write some client-side JavaScript to tie the web user interface and the servlet together:</span></span>
   
        var todoApp = {
          /*
           * API methods to call Java backend.
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
   
              // Call api to update todo items.
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
           * Install the TodoApp
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
5. <span data-ttu-id="0fd82-201">Fantastycznie!</span><span class="sxs-lookup"><span data-stu-id="0fd82-201">Awesome!</span></span> <span data-ttu-id="0fd82-202">Teraz pozostało już tylko przetestować aplikację.</span><span class="sxs-lookup"><span data-stu-id="0fd82-202">Now all that's left is to test the application.</span></span> <span data-ttu-id="0fd82-203">Uruchom aplikację lokalnie, a następnie dodaj jakieś zadania do wykonania, wpisując nazwę zadania oraz jego kategorię i klikając przycisk **Add Task** (Dodaj zadanie).</span><span class="sxs-lookup"><span data-stu-id="0fd82-203">Run the application locally, and add some Todo items by filling in the item name and category and clicking **Add Task**.</span></span>
6. <span data-ttu-id="0fd82-204">Gdy zadanie zostanie wyświetlone, można zaktualizować, czy jest ono ukończone, klikając pole wyboru, a następnie klikając przycisk **Update Tasks** (Zaktualizuj zadania).</span><span class="sxs-lookup"><span data-stu-id="0fd82-204">Once the item appears, you can update whether it's complete by toggling the checkbox and clicking **Update Tasks**.</span></span>

## <span data-ttu-id="0fd82-205"><a id="Deploy"></a>Krok 6: Wdrażanie aplikacji w języku Java do witryn sieci Web Azure</span><span class="sxs-lookup"><span data-stu-id="0fd82-205"><a id="Deploy"></a>Step 6: Deploy your Java application to Azure Web Sites</span></span>
<span data-ttu-id="0fd82-206">Witryny sieci Web Azure sprawia, że wdrożenie aplikacji Java sprowadza wyeksportowania aplikacji jako plik WAR i przesłania go na serwer za pomocą kontroli źródła (np. Git) lub FTP.</span><span class="sxs-lookup"><span data-stu-id="0fd82-206">Azure Web Sites makes deploying Java applications as simple as exporting your application as a WAR file and either uploading it via source control (e.g. Git) or FTP.</span></span>

1. <span data-ttu-id="0fd82-207">Aby wyeksportować aplikację jako plik WAR, kliknij prawym przyciskiem myszy projekt w **Eksplorator projektów**, kliknij przycisk **wyeksportować**, a następnie kliknij przycisk **pliku WAR**.</span><span class="sxs-lookup"><span data-stu-id="0fd82-207">To export your application as a WAR file, right-click on your project in **Project Explorer**, click **Export**, and then click **WAR File**.</span></span>
2. <span data-ttu-id="0fd82-208">W oknie **WAR Export** (Eksport pliku WAR) wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="0fd82-208">In the **WAR Export** window, do the following:</span></span>
   
   * <span data-ttu-id="0fd82-209">W polu Projekt sieci Web wprowadź tekst azure-documentdb-java-sample.</span><span class="sxs-lookup"><span data-stu-id="0fd82-209">In the Web project box, enter azure-documentdb-java-sample.</span></span>
   * <span data-ttu-id="0fd82-210">W polu Miejsce docelowe wybierz miejsce zapisania pliku WAR.</span><span class="sxs-lookup"><span data-stu-id="0fd82-210">In the Destination box, choose a destination to save the WAR file.</span></span>
   * <span data-ttu-id="0fd82-211">Kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="0fd82-211">Click **Finish**.</span></span>
3. <span data-ttu-id="0fd82-212">Teraz, gdy masz na plik WAR, możesz po prostu przekazać go do platformy Azure witryny sieci Web **webapps** katalogu.</span><span class="sxs-lookup"><span data-stu-id="0fd82-212">Now that you have a WAR file in hand, you can simply upload it to your Azure Web Site's **webapps** directory.</span></span> <span data-ttu-id="0fd82-213">Aby uzyskać instrukcje dotyczące przekazywania pliku, zobacz [dodawania aplikacji Java do aplikacji sieci Web usługi aplikacji Azure](../app-service-web/web-sites-java-add-app.md).</span><span class="sxs-lookup"><span data-stu-id="0fd82-213">For instructions on uploading the file, see [Add a Java application to Azure App Service Web Apps](../app-service-web/web-sites-java-add-app.md).</span></span>
   
    <span data-ttu-id="0fd82-214">Po przesłaniu pliku WAR do katalogu webapps środowisko uruchomieniowe wykryje, że plik został dodany, i załaduje go automatycznie.</span><span class="sxs-lookup"><span data-stu-id="0fd82-214">Once the WAR file is uploaded to the webapps directory, the runtime environment will detect that you've added it and will automatically load it.</span></span>
4. <span data-ttu-id="0fd82-215">Aby wyświetlić Zakończono produktu, przejdź do http://YOUR\_LOKACJI\_NAME.azurewebsites.net/azure-java-sample/ i zacznij dodawać zadania!</span><span class="sxs-lookup"><span data-stu-id="0fd82-215">To view your finished product, navigate to http://YOUR\_SITE\_NAME.azurewebsites.net/azure-java-sample/ and start adding your tasks!</span></span>

## <span data-ttu-id="0fd82-216"><a id="GetProject"></a>Pobieranie projektu z usługi GitHub</span><span class="sxs-lookup"><span data-stu-id="0fd82-216"><a id="GetProject"></a>Get the project from GitHub</span></span>
<span data-ttu-id="0fd82-217">Wszystkie przykłady w tym samouczku są zawarte w projekcie [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) w usłudze GitHub.</span><span class="sxs-lookup"><span data-stu-id="0fd82-217">All the samples in this tutorial are included in the [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) project on GitHub.</span></span> <span data-ttu-id="0fd82-218">Aby zaimportować projekt todo do środowiska Eclipse, upewnij się, że dysponujesz oprogramowaniem i zasobami wymienionymi w sekcji [Wymagania wstępne](#Prerequisites), a następnie wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="0fd82-218">To import the todo project into Eclipse, ensure you have the software and resources listed in the [Prerequisites](#Prerequisites) section, then do the following:</span></span>

1. <span data-ttu-id="0fd82-219">Zainstaluj [Projekt Lombok](http://projectlombok.org/).</span><span class="sxs-lookup"><span data-stu-id="0fd82-219">Install [Project Lombok](http://projectlombok.org/).</span></span> <span data-ttu-id="0fd82-220">Lombok służy w projekcie do generowania konstruktorów, metod pobierających i ustawiających.</span><span class="sxs-lookup"><span data-stu-id="0fd82-220">Lombok is used to generate constructors, getters, setters in the project.</span></span> <span data-ttu-id="0fd82-221">Po pobraniu pliku lombok.jar kliknij go dwukrotnie, aby go zainstalować, lub zainstaluj go przy użyciu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="0fd82-221">Once you have downloaded the lombok.jar file, double-click it to install it or install it from the command line.</span></span>
2. <span data-ttu-id="0fd82-222">Jeśli środowisko Eclipse jest otwarte, zamknij je i uruchom ponownie, aby załadować Lombok.</span><span class="sxs-lookup"><span data-stu-id="0fd82-222">If Eclipse is open, close it and restart it to load Lombok.</span></span>
3. <span data-ttu-id="0fd82-223">W środowisku Eclipse w menu **File** (Plik) kliknij pozycję **Import** (Importuj).</span><span class="sxs-lookup"><span data-stu-id="0fd82-223">In Eclipse, on the **File** menu, click **Import**.</span></span>
4. <span data-ttu-id="0fd82-224">W okienku **Import** (Import), kliknij pozycję **Git** (Usługa Git), kliknij pozycję **Projects from Git** (Projekty z usługi Git), a następnie kliknij przycisk **Next** (Dalej).</span><span class="sxs-lookup"><span data-stu-id="0fd82-224">In the **Import** window, click **Git**, click **Projects from Git**, and then click **Next**.</span></span>
5. <span data-ttu-id="0fd82-225">Na ekranie **Select Repository Source** (Wybierz źródło repozytorium) kliknij pozycję **Clone URI** (Klonuj URI).</span><span class="sxs-lookup"><span data-stu-id="0fd82-225">On the **Select Repository Source** screen, click **Clone URI**.</span></span>
6. <span data-ttu-id="0fd82-226">Na **źródło repozytorium Git** ekranu w **URI** wprowadź https://github.com/Azure-Samples/java-todo-app.git, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="0fd82-226">On the **Source Git Repository** screen, in the **URI** box, enter https://github.com/Azure-Samples/java-todo-app.git, and then click **Next**.</span></span>
7. <span data-ttu-id="0fd82-227">Na ekranie **Branch Selection** (Wybór gałęzi) upewnij się, że jest wybrana gałąź **master**, a następnie kliknij przycisk **Next** (Dalej).</span><span class="sxs-lookup"><span data-stu-id="0fd82-227">On the **Branch Selection** screen, ensure that **master** is selected, and then click **Next**.</span></span>
8. <span data-ttu-id="0fd82-228">Na ekranie **Local Destination** (Lokalne miejsce docelowe) kliknij przycisk **Browse** (Przeglądaj), aby wybrać folder, do którego można skopiować repozytorium, a następnie kliknij przycisk **Next** (Dalej).</span><span class="sxs-lookup"><span data-stu-id="0fd82-228">On the **Local Destination** screen, click **Browse** to select a folder where the repository can be copied, and then click **Next**.</span></span>
9. <span data-ttu-id="0fd82-229">Na ekranie **Select a wizard to use for importing projects** (Wybór kreatora importującego projekty) upewnij się, że jest zaznaczona opcja **Import existing projects** (Importuj istniejące projekty), a następnie kliknij przycisk **Next** (Dalej).</span><span class="sxs-lookup"><span data-stu-id="0fd82-229">On the **Select a wizard to use for importing projects** screen, ensure that **Import existing projects** is selected, and then click **Next**.</span></span>
10. <span data-ttu-id="0fd82-230">Na ekranie **Import Projects** (Import projektów) usuń zaznaczenie przy projekcie **DocumentDB**, a następnie kliknij przycisk **Finish** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="0fd82-230">On the **Import Projects** screen, unselect the **DocumentDB** project, and then click **Finish**.</span></span> <span data-ttu-id="0fd82-231">Projekt DocumentDB zawiera Azure rozwiązania Cosmos DB Java SDK, który zostanie dodany jako zależność zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="0fd82-231">The DocumentDB project contains the Azure Cosmos DB Java SDK, which we will add as a dependency instead.</span></span>
11. <span data-ttu-id="0fd82-232">W **Eksplorator projektów**, przejdź do azure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java i Zastąp wartości HOST oraz MASTER_KEY URI oraz PRIMARY KEY dla użytkownika Azure DB rozwiązania Cosmos konta, a następnie zapisz plik.</span><span class="sxs-lookup"><span data-stu-id="0fd82-232">In **Project Explorer**, navigate to azure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java and replace the HOST and MASTER_KEY values with the URI and PRIMARY KEY for your Azure Cosmos DB account, and then save the file.</span></span> <span data-ttu-id="0fd82-233">Aby uzyskać więcej informacji, zobacz [Krok 1. Tworzenie konta bazy danych Azure DB rozwiązania Cosmos](#CreateDB).</span><span class="sxs-lookup"><span data-stu-id="0fd82-233">For more information, see [Step 1. Create an Azure Cosmos DB database account](#CreateDB).</span></span>
12. <span data-ttu-id="0fd82-234">W widoku **Project Explorer** (Eksplorator projektów) kliknij prawym przyciskiem myszy pozycję **azure-documentdb-java-sample**, kliknij pozycję **Build Path** (Ścieżka kompilacji), a następnie kliknij pozycję **Configure Build Path** (Konfiguruj ścieżkę kompilacji).</span><span class="sxs-lookup"><span data-stu-id="0fd82-234">In **Project Explorer**, right click the **azure-documentdb-java-sample**, click **Build Path**, and then click **Configure Build Path**.</span></span>
13. <span data-ttu-id="0fd82-235">Na ekranie **Java Build Path** (Ścieżka kompilacji języka Java) w oknie po prawej stronie wybierz kartę **Libraries** (Biblioteki), a następnie kliknij pozycję **Add External JARs** (Dodaj zewnętrzne pliki JAR).</span><span class="sxs-lookup"><span data-stu-id="0fd82-235">On the **Java Build Path** screen, in the right pane, select the **Libraries** tab, and then click **Add External JARs**.</span></span> <span data-ttu-id="0fd82-236">Przejdź do lokalizacji pliku lombok.jar, kliknij przycisk **Open** (Otwórz), a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="0fd82-236">Navigate to the location of the lombok.jar file, and click **Open**, and then click **OK**.</span></span>
14. <span data-ttu-id="0fd82-237">Użyj kroku 12, aby otworzyć ponownie okno **Properties** (Właściwości), a następnie w oknie po lewej stronie kliknij pozycję **Targeted Runtimes** (Docelowe środowiska uruchomieniowe).</span><span class="sxs-lookup"><span data-stu-id="0fd82-237">Use step 12 to open the **Properties** window again, and then in the left pane click **Targeted Runtimes**.</span></span>
15. <span data-ttu-id="0fd82-238">Na ekranie **Targeted Runtimes** (Docelowe środowiska uruchomieniowe) kliknij pozycję **New** (Nowy), wybierz pozycję **Apache Tomcat v7.0**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="0fd82-238">On the **Targeted Runtimes** screen, click **New**, select **Apache Tomcat v7.0**, and then click **OK**.</span></span>
16. <span data-ttu-id="0fd82-239">Użyj kroku 12, aby otworzyć ponownie okno **Properties** (Właściwości), a następnie w oknie po lewej stronie kliknij pozycję **Project Facets** (Aspekty projektu).</span><span class="sxs-lookup"><span data-stu-id="0fd82-239">Use step 12 to open the **Properties** window again, and then in the left pane click **Project Facets**.</span></span>
17. <span data-ttu-id="0fd82-240">Na ekranie **Project Facets** (Aspekty projektu) wybierz pozycję **Dynamic Web Module** (Dynamiczny moduł sieci Web) oraz pozycję **Java**, a następnie kliknij pozycję **OK**.</span><span class="sxs-lookup"><span data-stu-id="0fd82-240">On the **Project Facets** screen, select **Dynamic Web Module** and **Java**, and then click **OK**.</span></span>
18. <span data-ttu-id="0fd82-241">Na karcie **Servers** (Serwery) w dolnej części ekranu kliknij prawym przyciskiem myszy pozycję **Tomcat v7.0 Server at localhost**, a następnie kliknij pozycję **Add and Remove** (Dodaj i usuń).</span><span class="sxs-lookup"><span data-stu-id="0fd82-241">On the **Servers** tab at the bottom of the screen, right-click **Tomcat v7.0 Server at localhost** and then click **Add and Remove**.</span></span>
19. <span data-ttu-id="0fd82-242">W oknie **Add and Remove** (Dodaj i usuń) przenieś pozycję **azure-documentdb-java-sample** w pole **Configured** (Skonfigurowane), a następnie kliknij przycisk **Finish** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="0fd82-242">On the **Add and Remove** window, move **azure-documentdb-java-sample** to the **Configured** box, and then click **Finish**.</span></span>
20. <span data-ttu-id="0fd82-243">W **serwerów** kliknij prawym przyciskiem myszy **Tomcat v7.0 Server at localhost**, a następnie kliknij przycisk **ponownego uruchomienia**.</span><span class="sxs-lookup"><span data-stu-id="0fd82-243">In the **Servers** tab, right-click **Tomcat v7.0 Server at localhost**, and then click **Restart**.</span></span>
21. <span data-ttu-id="0fd82-244">W przeglądarce przejdź do http://localhost:8080/azure-documentdb-java-sample/ i zacznij dodawać zadania do listy.</span><span class="sxs-lookup"><span data-stu-id="0fd82-244">In a browser, navigate to http://localhost:8080/azure-documentdb-java-sample/ and start adding to your task list.</span></span> <span data-ttu-id="0fd82-245">Należy pamiętać, że jeśli zmieniono domyślne wartości portów, zmień 8080 na wybraną wartość.</span><span class="sxs-lookup"><span data-stu-id="0fd82-245">Note that if you changed your default port values, change 8080 to the value you selected.</span></span>
22. <span data-ttu-id="0fd82-246">Aby wdrożyć projekt w witrynie sieci Web platformy Azure, zobacz [Krok 6. Wdrażanie aplikacji do witryny sieci Web Azure](#Deploy).</span><span class="sxs-lookup"><span data-stu-id="0fd82-246">To deploy your project to an Azure web site, see [Step 6. Deploy your application to Azure Web Sites](#Deploy).</span></span>

[1]: media/documentdb-java-application/keys.png
