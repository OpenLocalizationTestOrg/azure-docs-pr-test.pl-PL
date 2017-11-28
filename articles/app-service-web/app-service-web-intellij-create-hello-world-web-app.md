---
title: w aplikacji sieci web platformy Azure podstawowe w IntelliJ aaaCreate | Dokumentacja firmy Microsoft
description: "Ten samouczek pokazuje, jak toouse hello Azure zestawu narzędzi dla IntelliJ toocreate aplikacji Hello World sieci Web dla platformy Azure."
services: app-service\web
documentationcenter: java
author: selvasingh
manager: erikre
editor: 
ms.assetid: 75ce7b36-e3ae-491d-8305-4b42ce37db4e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 4667497213cac3ddf754d164e614c809f338cce5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-basic-azure-web-app-in-intellij"></a><span data-ttu-id="4e70c-103">Tworzenie aplikacji sieci web platformy Azure podstawowe w IntelliJ</span><span class="sxs-lookup"><span data-stu-id="4e70c-103">Create a basic Azure web app in IntelliJ</span></span>
<span data-ttu-id="4e70c-104">Ten samouczek pokazuje, jak toocreate i wdrażania podstawowych tooAzure aplikacji Hello World jako aplikacji sieci Web przy użyciu hello [narzędzi Azure dla IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="4e70c-104">This tutorial shows how toocreate and deploy a basic Hello World application tooAzure as a Web App by using hello [Azure Toolkit for IntelliJ].</span></span> <span data-ttu-id="4e70c-105">Podstawowy przykład JSP jest widoczna dla uproszczenia, ale podobne kroki będzie odpowiednia dla serwlet Java, jakim jest dotyczy wdrożenia usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="4e70c-105">A basic JSP example is shown for simplicity, but similar steps would be appropriate for a Java servlet, as far as Azure deployment is concerned.</span></span>

<span data-ttu-id="4e70c-106">Po ukończeniu tego samouczka, aplikacja będzie wyglądać podobnie toohello następującej ilustracji, podczas wyświetlania w przeglądarce sieci web:</span><span class="sxs-lookup"><span data-stu-id="4e70c-106">When you have completed this tutorial, your application will look similar toohello following illustration when you view it in a web browser:</span></span>

![Przykładowa strona sieci Web][01]

## <a name="prerequisites"></a><span data-ttu-id="4e70c-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4e70c-108">Prerequisites</span></span>
* <span data-ttu-id="4e70c-109">Java Developer Kit (JDK), v 1,8 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="4e70c-109">A Java Developer Kit (JDK), v 1.8 or later.</span></span>
* <span data-ttu-id="4e70c-110">IntelliJ IDEA Ultimate Edition.</span><span class="sxs-lookup"><span data-stu-id="4e70c-110">IntelliJ IDEA Ultimate Edition.</span></span> <span data-ttu-id="4e70c-111">Ten można pobrać z <https://www.jetbrains.com/idea/download/index.html>.</span><span class="sxs-lookup"><span data-stu-id="4e70c-111">This can be downloaded from <https://www.jetbrains.com/idea/download/index.html>.</span></span>
* <span data-ttu-id="4e70c-112">Dystrybucji serwera sieci web opartych na języku Java lub serwera aplikacji takich jak [Apache Tomcat] lub [Jetty].</span><span class="sxs-lookup"><span data-stu-id="4e70c-112">A distribution of a Java-based web server or application server, such as [Apache Tomcat] or [Jetty].</span></span>
* <span data-ttu-id="4e70c-113">Subskrypcję platformy Azure, która może zostać pobrany z <https://azure.microsoft.com/free/> lub <http://azure.microsoft.com/pricing/purchase-options/>.</span><span class="sxs-lookup"><span data-stu-id="4e70c-113">An Azure subscription, which can be acquired from <https://azure.microsoft.com/free/> or <http://azure.microsoft.com/pricing/purchase-options/>.</span></span>
* <span data-ttu-id="4e70c-114">Witaj [narzędzi Azure dla IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="4e70c-114">hello [Azure Toolkit for IntelliJ].</span></span> <span data-ttu-id="4e70c-115">Informacje o instalowaniu hello zestawu narzędzi platformy Azure, zobacz [hello Instalowanie narzędzi Azure dla IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="4e70c-115">For information about installing hello Azure Toolkit, see [Installing hello Azure Toolkit for IntelliJ].</span></span>

## <a name="toocreate-a-hello-world-application"></a><span data-ttu-id="4e70c-116">toocreate aplikacji Hello World</span><span class="sxs-lookup"><span data-stu-id="4e70c-116">toocreate a Hello World application</span></span>
<span data-ttu-id="4e70c-117">Po pierwsze Zaczniemy tworzenia projektu języka Java.</span><span class="sxs-lookup"><span data-stu-id="4e70c-117">First, we'll start off with creating a Java project.</span></span>

1. <span data-ttu-id="4e70c-118">Uruchom środowisko IntelliJ i kliknij przycisk hello **pliku** menu, następnie kliknij przycisk **nowy**, a następnie kliknij przycisk **projektu**.</span><span class="sxs-lookup"><span data-stu-id="4e70c-118">Start IntelliJ and click hello **File** menu, then click **New**, and then click **Project**.</span></span>
   
    ![Nowy projekt pliku][02]
2. <span data-ttu-id="4e70c-120">Okno dialogowe Nowy projekt hello, wybierz **Java**, następnie **aplikacji sieci Web**, a następnie kliknij przycisk **nowy** tooadd SDK projektu.</span><span class="sxs-lookup"><span data-stu-id="4e70c-120">In hello New Project dialog box, select **Java**, then **Web Application**, and then click **New** tooadd a Project SDK.</span></span>
   
    ![Okno dialogowe Nowy projekt][03a]
   
3. <span data-ttu-id="4e70c-122">W hello Wybieranie katalogu macierzystego dla okna dialogowego JDK, wybierz hello zainstalowanym JDK z folderu, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="4e70c-122">In hello Select Home Directory for JDK dialog box, select hello folder where your JDK is installed, and then click **OK**.</span></span> <span data-ttu-id="4e70c-123">Kliknij przycisk **dalej** w toocontinue okno dialogowe Nowy projekt hello.</span><span class="sxs-lookup"><span data-stu-id="4e70c-123">Click **Next** in hello New Project dialog box toocontinue.</span></span>
   
    ![Określ katalog macierzysty JDK][03b]
4. <span data-ttu-id="4e70c-125">Do celów tego samouczka, nazwa projektu hello **Java sieci Web-App-na-Azure**, a następnie kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="4e70c-125">For purposes of this tutorial, name hello project **Java-Web-App-On-Azure**, and then click **Finish**.</span></span>
   
    ![Okno dialogowe Nowy projekt][04]
5. <span data-ttu-id="4e70c-127">W widoku Project Explorer IntelliJ firmy, rozwiń węzeł **Java sieci Web-App-na-Azure**, następnie rozwiń węzeł **web**, a następnie kliknij dwukrotnie **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="4e70c-127">Within IntelliJ's Project Explorer view, expand **Java-Web-App-On-Azure**, then expand **web**, and then double-click **index.jsp**.</span></span>
   
    ![Otwórz indeks strony][05c]
6. <span data-ttu-id="4e70c-129">Po otwarciu pliku index.jsp w IntelliJ dodatek do wyświetlania tekstu toodynamically **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="4e70c-129">When your index.jsp file opens in IntelliJ, add in text toodynamically display **Hello World!**</span></span> <span data-ttu-id="4e70c-130">w ramach istniejącego hello `<body>` elementu.</span><span class="sxs-lookup"><span data-stu-id="4e70c-130">within hello existing `<body>` element.</span></span> <span data-ttu-id="4e70c-131">Zaktualizowana `<body>` zawartość powinna wyglądać hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="4e70c-131">Your updated `<body>` content should resemble hello following example:</span></span>
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
7. <span data-ttu-id="4e70c-132">Zapisz index.jsp.</span><span class="sxs-lookup"><span data-stu-id="4e70c-132">Save index.jsp.</span></span>

## <a name="toodeploy-your-application-tooan-azure-web-app-container"></a><span data-ttu-id="4e70c-133">toodeploy Twojego tooan aplikacji kontenera aplikacji sieci Web Azure</span><span class="sxs-lookup"><span data-stu-id="4e70c-133">toodeploy your application tooan Azure Web App Container</span></span>
<span data-ttu-id="4e70c-134">Istnieje kilka metod, które można wdrożyć tooAzure aplikacji sieci web Java.</span><span class="sxs-lookup"><span data-stu-id="4e70c-134">There are several ways by which you can deploy a Java web application tooAzure.</span></span> <span data-ttu-id="4e70c-135">Ten samouczek zawiera opis jednego z hello najprostszym: aplikacja będzie tooan wdrożony kontener aplikacji sieci Web platformy Azure — żadnych typ projektu ani dodatkowe narzędzia są niezbędne.</span><span class="sxs-lookup"><span data-stu-id="4e70c-135">This tutorial describes one of hello simplest: your application will be deployed tooan Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="4e70c-136">Hello JDK i hello kontenera oprogramowanie dla sieci web zostanie zostać dostarczony przez platformę Azure, więc nie ma żadnych tooupload potrzeby własne; potrzebna jest aplikacja sieci Web Java.</span><span class="sxs-lookup"><span data-stu-id="4e70c-136">hello JDK and hello web container software will be provided for you by Azure, so there is no need tooupload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="4e70c-137">W związku z tym hello proces publikowania aplikacji może zająć sekund, nie minut.</span><span class="sxs-lookup"><span data-stu-id="4e70c-137">As a result, hello publishing process for your application will take seconds, not minutes.</span></span>

<span data-ttu-id="4e70c-138">Przed opublikowaniem aplikacji, należy najpierw tooconfigure ustawienia modułu.</span><span class="sxs-lookup"><span data-stu-id="4e70c-138">Before you publish your application, you first need tooconfigure your module settings.</span></span> <span data-ttu-id="4e70c-139">toodo tak, użycie hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="4e70c-139">toodo so, use hello following steps:</span></span>

1. <span data-ttu-id="4e70c-140">W obszarze Eksplorator projektów w IntelliJ, kliknij prawym przyciskiem myszy hello **Java sieci Web-App-na-Azure** projektu.</span><span class="sxs-lookup"><span data-stu-id="4e70c-140">In IntelliJ's Project Explorer, right-click hello **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="4e70c-141">Po wyświetleniu menu kontekstowe powitania kliknij **Otwórz ustawienia modułu**.</span><span class="sxs-lookup"><span data-stu-id="4e70c-141">When hello context menu appears, click **Open Module Settings**.</span></span>

    ![Otwórz ustawienia modułu][05a]
2. <span data-ttu-id="4e70c-143">Gdy zostanie wyświetlone okno dialogowe hello struktury projektu:</span><span class="sxs-lookup"><span data-stu-id="4e70c-143">When hello Project Structure dialog box appears:</span></span>

   <span data-ttu-id="4e70c-144">a.</span><span class="sxs-lookup"><span data-stu-id="4e70c-144">a.</span></span> <span data-ttu-id="4e70c-145">Kliknij przycisk **artefakty** liście hello **ustawienia projektu**.</span><span class="sxs-lookup"><span data-stu-id="4e70c-145">Click **Artifacts** in hello list of **Project Settings**.</span></span>
   <span data-ttu-id="4e70c-146">b.</span><span class="sxs-lookup"><span data-stu-id="4e70c-146">b.</span></span> <span data-ttu-id="4e70c-147">Nazwa artefaktu hello zmian w hello **nazwa** , dzięki czemu nie zawiera spacji ani znaków specjalnych; jest to konieczne, ponieważ nazwa hello będą używane w hello jednolity identyfikator zasobów (URI).</span><span class="sxs-lookup"><span data-stu-id="4e70c-147">Change hello artifact name in hello **Name** box so that it doesn't contain whitespace or special characters; this is necessary since hello name will be used in hello Uniform Resource Identifier (URI).</span></span>
   <span data-ttu-id="4e70c-148">c.</span><span class="sxs-lookup"><span data-stu-id="4e70c-148">c.</span></span> <span data-ttu-id="4e70c-149">Zmień hello **typu** za**aplikacji sieci Web: archiwum**.</span><span class="sxs-lookup"><span data-stu-id="4e70c-149">Change hello **Type** too**Web Application: Archive**.</span></span>
   <span data-ttu-id="4e70c-150">d.</span><span class="sxs-lookup"><span data-stu-id="4e70c-150">d.</span></span> <span data-ttu-id="4e70c-151">Kliknij przycisk **OK** tooclose hello struktury projektu okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="4e70c-151">Click **OK** tooclose hello Project Structure dialog box.</span></span>

    ![Otwórz ustawienia modułu][05b]

<span data-ttu-id="4e70c-153">Po skonfigurowaniu ustawień modułu można opublikować tooAzure Twojej aplikacji za pomocą hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="4e70c-153">When you have configured your module settings, you can publish your application tooAzure by using hello following steps:</span></span>

1. <span data-ttu-id="4e70c-154">W obszarze Eksplorator projektów w IntelliJ, kliknij prawym przyciskiem myszy hello **Java sieci Web-App-na-Azure** projektu.</span><span class="sxs-lookup"><span data-stu-id="4e70c-154">In IntelliJ's Project Explorer, right-click hello **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="4e70c-155">Po wyświetleniu menu kontekstowe hello zaznacz **Azure**, a następnie kliknij przycisk **Publikuj jako aplikacji sieci Web platformy Azure...**</span><span class="sxs-lookup"><span data-stu-id="4e70c-155">When hello context menu appears, select **Azure**, and then click **Publish as Azure Web App...**</span></span>
   
    ![Menu kontekstowe publikowania na platformie Azure][06]
2. <span data-ttu-id="4e70c-157">Jeśli dany komputer nie ma już podpisany na platformie Azure z IntelliJ, będzie zostanie wyświetlony monit o toosign do konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4e70c-157">If you have not already signed into Azure from IntelliJ, you will be prompted toosign into your Azure account.</span></span> <span data-ttu-id="4e70c-158">(Jeśli masz wiele kont platformy Azure, część hello monity podczas logowania hello w procesie mogą być wyświetlane więcej niż raz, nawet wtedy, gdy pojawią się one toobe hello takie same.</span><span class="sxs-lookup"><span data-stu-id="4e70c-158">(If you have multiple Azure accounts, some of hello prompts during hello sign in process may be shown more than once, even if they appear toobe hello same.</span></span> <span data-ttu-id="4e70c-159">W takim przypadku należy kontynuować toofollow hello logowania w instrukcjach.)</span><span class="sxs-lookup"><span data-stu-id="4e70c-159">When this happens, continue toofollow hello sign in instructions.)</span></span>
   
    ![Azure dziennika w oknie dialogowym][07]
3. <span data-ttu-id="4e70c-161">Po pomyślnym zarejestrowaniu do konta platformy Azure, hello **Zarządzaj subskrypcjami** dialogowym zostanie wyświetlona lista subskrypcji, które są skojarzone z poświadczeniami użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4e70c-161">After you have successfully signed into your Azure account, hello **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="4e70c-162">(Jeśli istnieje wiele wymienionych subskrypcji i chcesz toowork z konkretnego podzestawu z nich, może opcjonalnie Usuń zaznaczenie hello subskrypcji nie mają toouse.) Po zakończeniu wybierania subskrypcji, kliknij przycisk **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="4e70c-162">(If there are multiple subscriptions listed and you want toowork with only a specific subset of them, you may optionally uncheck hello subscriptions you don't want toouse.) When you have selected your subscriptions, click **Close**.</span></span>
   
    ![Zarządzanie subskrypcjami][08]
4. <span data-ttu-id="4e70c-164">Gdy hello **wdrażanie tooAzure kontenera aplikacji sieci Web** zostanie wyświetlone okno dialogowe będzie ono żadnych kontenerów aplikacji sieci Web, które wcześniej zostały utworzone; Jeśli nie utworzono żadnych kontenerów, hello lista jest pusta.</span><span class="sxs-lookup"><span data-stu-id="4e70c-164">When hello **Deploy tooAzure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, hello list will be empty.</span></span>
   
    ![Kontenery aplikacji][09]
5. <span data-ttu-id="4e70c-166">Jeśli nie utworzono kontener aplikacji sieci Web Azure przed lub jeśli chcesz toopublish Twojej aplikacji tooa nowy kontener, użyj hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="4e70c-166">If you have not created an Azure Web App Container before, or if you would like toopublish your application tooa new container, use hello following steps.</span></span> <span data-ttu-id="4e70c-167">W przeciwnym razie wybierz kontener istniejących aplikacji sieci Web i pominąć toostep 6 poniżej.</span><span class="sxs-lookup"><span data-stu-id="4e70c-167">Otherwise, select an existing Web App Container and skip toostep 6 below.</span></span>
   
   1. <span data-ttu-id="4e70c-168">Kliknij przycisk**+**</span><span class="sxs-lookup"><span data-stu-id="4e70c-168">Click **+**</span></span>
      
       ![Dodawanie aplikacji kontenera][10]
   2. <span data-ttu-id="4e70c-170">Witaj **nowy kontener aplikacji sieci Web** można wyświetlić okna dialogowego, który będzie używany dla hello obok kilku kroków.</span><span class="sxs-lookup"><span data-stu-id="4e70c-170">hello **New Web App Container** dialog box will be displayed, which will be used for hello next several steps.</span></span>
      
       ![Nowy kontener aplikacji][11a]
   3. <span data-ttu-id="4e70c-172">Wprowadź **Etykieta DNS** dla kontener aplikacji sieci Web; to będzie stanowić etykietę DNS liścia hello hello hosta adres URL aplikacji sieci web na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="4e70c-172">Enter a **DNS Label** for your Web App Container; this will form hello leaf DNS label of hello host URL for your web application in Azure.</span></span> <span data-ttu-id="4e70c-173">Należy pamiętać, że nazwa hello musi być dostępny i jest zgodna z wymaganiami dotyczącymi nazw aplikacji sieci Web tooAzure.</span><span class="sxs-lookup"><span data-stu-id="4e70c-173">Note that hello name must be available and conform tooAzure Web App naming requirements.</span></span>
   4. <span data-ttu-id="4e70c-174">W hello **kontener sieci Web** menu rozwijanego, wybierz hello odpowiedniego oprogramowania dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4e70c-174">In hello **Web Container** drop-down menu, select hello appropriate software for your application.</span></span>
      
       <span data-ttu-id="4e70c-175">Obecnie można wybrać z Tomcat 8 Tomcat 7 lub Jetty 9.</span><span class="sxs-lookup"><span data-stu-id="4e70c-175">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="4e70c-176">Ostatnie dystrybucji oprogramowania hello wybrane będą udostępniane przez usługi Azure, a zostanie uruchomiony na ostatnie dystrybucji 8 JDK utworzone przez firmę Oracle i dostarczany przez platformę Azure.</span><span class="sxs-lookup"><span data-stu-id="4e70c-176">A recent distribution of hello selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span></span>
   5. <span data-ttu-id="4e70c-177">W hello **subskrypcji** menu rozwijanego, wybierz hello subskrypcję toouse dla tego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="4e70c-177">In hello **Subscription** drop-down menu, select hello subscription you want toouse for this deployment.</span></span>
   6. <span data-ttu-id="4e70c-178">W hello **grupy zasobów** menu rozwijane i wybierz hello grupy zasobów, z którą chcesz tooassociate aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="4e70c-178">In hello **Resource Group** drop-down menu, select hello Resource Group with which you want tooassociate your Web App.</span></span> <span data-ttu-id="4e70c-179">(Zezwalaj grup zasobów platformy azure możesz toogroup powiązane ze sobą zasoby, tak, aby na przykład je usunąć ze sobą.)</span><span class="sxs-lookup"><span data-stu-id="4e70c-179">(Azure Resource Groups allow you toogroup related resources together so that, for example, they can be deleted together.)</span></span>
      
       <span data-ttu-id="4e70c-180">Można wybrać istniejącą grupę zasobów (jeśli) i Pomiń toostep g poniżej lub użyj hello następujące kroki toocreate nową grupę zasobów:</span><span class="sxs-lookup"><span data-stu-id="4e70c-180">You can select an existing Resource Group (if you have any) and skip toostep g below, or use hello following steps toocreate a new Resource Group:</span></span>
      
      * <span data-ttu-id="4e70c-181">Wybierz  **&lt; &lt; Utwórz nową grupę zasobów &gt; &gt;**  w hello **grupy zasobów** menu rozwijanego.</span><span class="sxs-lookup"><span data-stu-id="4e70c-181">Select **&lt;&lt; Create new Resource Group &gt;&gt;** in hello **Resource Group** drop-down menu.</span></span>
      * <span data-ttu-id="4e70c-182">Witaj **nową grupę zasobów** wyświetli się okno dialogowe:</span><span class="sxs-lookup"><span data-stu-id="4e70c-182">hello **New Resource Group** dialog box will be displayed:</span></span>
        
          ![Nową grupę zasobów][12]
      * <span data-ttu-id="4e70c-184">W hello hello **nazwa** pole tekstowe, określ nazwę nowej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="4e70c-184">In hello hello **Name** textbox, specify a name for your new Resource Group.</span></span>
      * <span data-ttu-id="4e70c-185">W hello hello **Region** menu rozwijanego wybierz hello odpowiednie usługi Azure data center lokalizację dla grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="4e70c-185">In hello hello **Region** drop-down menu, select hello appropriate Azure data center location for your Resource Group.</span></span>
      * <span data-ttu-id="4e70c-186">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="4e70c-186">Click **OK**.</span></span>
   7. <span data-ttu-id="4e70c-187">Witaj **planu usługi App Service** hello planów usługi aplikacji, które są skojarzone z hello wybrana grupa zasobów zawiera menu rozwijanego.</span><span class="sxs-lookup"><span data-stu-id="4e70c-187">hello **App Service Plan** drop-down menu lists hello app service plans that are associated with hello Resource Group that you selected.</span></span> <span data-ttu-id="4e70c-188">(Plan usługi App Service określa informacje, takie jak lokalizacja hello aplikacji sieci Web, hello warstwa cenowa i rozmiar wystąpienia obliczeniowe hello.</span><span class="sxs-lookup"><span data-stu-id="4e70c-188">(An App Service Plan specifies information such as hello location of your Web App, hello pricing tier and hello compute instance size.</span></span> <span data-ttu-id="4e70c-189">Jeden Plan usługi App Service może służyć do wielu aplikacji sieci Web, dlatego jest obsługiwana oddzielnie od określonego wdrożenia aplikacji sieci Web.)</span><span class="sxs-lookup"><span data-stu-id="4e70c-189">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
       <span data-ttu-id="4e70c-190">Można wybrać istniejący Plan usługi App Service (jeśli) i Pomiń h toostep poniżej, lub użyj hello następujące kroki toocreate planu usługi aplikacji:</span><span class="sxs-lookup"><span data-stu-id="4e70c-190">You can select an existing App Service Plan (if you have any) and skip toostep h below, or use hello following steps toocreate a new App Service Plan:</span></span>
      
      * <span data-ttu-id="4e70c-191">Wybierz  **&lt; &lt; Utwórz nowy Plan usługi App Service &gt; &gt;**  w hello **planu usługi App Service** menu rozwijanego.</span><span class="sxs-lookup"><span data-stu-id="4e70c-191">Select **&lt;&lt; Create new App Service Plan &gt;&gt;** in hello **App Service Plan** drop-down menu.</span></span>
      * <span data-ttu-id="4e70c-192">Witaj **nowy Plan usługi App Service** wyświetli się okno dialogowe:</span><span class="sxs-lookup"><span data-stu-id="4e70c-192">hello **New App Service Plan** dialog box will be displayed:</span></span>
        
          ![Nowy Plan usługi aplikacji][13]
      * <span data-ttu-id="4e70c-194">W hello hello **nazwa** pole tekstowe, określ nazwę planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4e70c-194">In hello hello **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="4e70c-195">W hello hello **lokalizacji** menu rozwijanego wybierz hello odpowiednie usługi Azure data center lokalizacji dla planu hello.</span><span class="sxs-lookup"><span data-stu-id="4e70c-195">In hello hello **Location** drop-down menu, select hello appropriate Azure data center location for hello plan.</span></span>
      * <span data-ttu-id="4e70c-196">W hello hello **warstwy cenowej** menu rozwijanego, wybierz odpowiednie ceny dla planu hello hello.</span><span class="sxs-lookup"><span data-stu-id="4e70c-196">In hello hello **Pricing Tier** drop-down menu, select hello appropriate pricing for hello plan.</span></span> <span data-ttu-id="4e70c-197">Podczas testowania, możesz wybrać **wolne**.</span><span class="sxs-lookup"><span data-stu-id="4e70c-197">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="4e70c-198">W hello hello **rozmiar wystąpienia** menu rozwijanego, hello wybierz odpowiednie wystąpienie rozmiar hello planu.</span><span class="sxs-lookup"><span data-stu-id="4e70c-198">In hello hello **Instance Size** drop-down menu, select hello appropriate instance size for hello plan.</span></span> <span data-ttu-id="4e70c-199">Podczas testowania, możesz wybrać **małych**.</span><span class="sxs-lookup"><span data-stu-id="4e70c-199">For testing purposes you can choose **Small**.</span></span>
      * <span data-ttu-id="4e70c-200">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="4e70c-200">Click **OK**.</span></span>
   8. <span data-ttu-id="4e70c-201">(Opcjonalnie) Domyślnie ostatnie dystrybucji Java 8 będą automatycznie wdrażane jako sieci maszyny wirtualnej Java przez kontener aplikacji sieci web Azure tooyour.</span><span class="sxs-lookup"><span data-stu-id="4e70c-201">(Optional) By default, a recent distribution of Java 8 will be automatically deployed as your JVM by Azure tooyour web app container.</span></span> <span data-ttu-id="4e70c-202">Można jednak wybrać inną wersję i dystrybucji hello maszyny JVM.</span><span class="sxs-lookup"><span data-stu-id="4e70c-202">However, you can select a different version and distribution of hello JVM.</span></span> <span data-ttu-id="4e70c-203">toodo tak, użycie hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="4e70c-203">toodo so, use hello following steps:</span></span>
      
      * <span data-ttu-id="4e70c-204">Kliknij przycisk hello **JDK** kartę w hello **nowy kontener aplikacji sieci Web** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="4e70c-204">Click hello **JDK** tab in hello **New Web App Container** dialog box.</span></span>
      * <span data-ttu-id="4e70c-205">Można wybrać jedną z hello następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="4e70c-205">You can choose from one of hello following options:</span></span>
        
        * <span data-ttu-id="4e70c-206">Wdróż domyślne hello JDK, który jest oferowany na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="4e70c-206">Deploy hello default JDK which is offered by Azure</span></span>
        * <span data-ttu-id="4e70c-207">Wdrażanie 3 strona JDK z listy rozwijanej JDKs dodatkowe, które są dostępne w systemie Azure</span><span class="sxs-lookup"><span data-stu-id="4e70c-207">Deploy a 3rd party JDK from a drop-down list of additional JDKs which are available on Azure</span></span>
        * <span data-ttu-id="4e70c-208">Wdrażanie niestandardowych JDK, które muszą być spakowane jako plik ZIP i albo publicznie dostępnych lub na koncie magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="4e70c-208">Deploy a custom JDK, which must be packaged as a ZIP file and either publicly available or in your Azure storage account</span></span>
        
        ![Nowa karta JDK kontenera aplikacji][11b]
   9. <span data-ttu-id="4e70c-210">Po wykonaniu wszystkich hello powyżej kroki, okno dialogowe nowy kontener aplikacji sieci Web hello powinien wyglądać hello następującej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="4e70c-210">Once you have completed all of hello above steps, hello New Web App Container dialog box should resemble hello following illustration:</span></span>
      
       ![Nowy kontener aplikacji][14]
   10. <span data-ttu-id="4e70c-212">Kliknij przycisk **OK** tworzenie hello toocomplete Twojego nowego kontenera aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="4e70c-212">Click **OK** toocomplete hello creation of your new Web App container.</span></span>
       
        <span data-ttu-id="4e70c-213">Zaczekaj kilka sekund hello lista toobe kontenery sieci Web aplikacji hello odświeżyć, a kontener aplikacji sieci web nowo utworzony powinny teraz być zaznaczone na liście hello.</span><span class="sxs-lookup"><span data-stu-id="4e70c-213">Wait a few seconds for hello list of hello Web App containers toobe refreshed, and your newly-created web app container should now be selected in hello list.</span></span>
6. <span data-ttu-id="4e70c-214">Wszystko jest teraz gotowy toocomplete hello początkowe wdrożenie tooAzure Twojej aplikacji sieci Web; Kliknij przycisk **OK** toodeploy Twojego toohello aplikacji Java wybrany kontener aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="4e70c-214">You are now ready toocomplete hello initial deployment of your Web App tooAzure; click **OK** toodeploy your Java application toohello selected Web App container.</span></span> <span data-ttu-id="4e70c-215">Domyślnie aplikacja zostanie wdrożona jako podkatalog serwera aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="4e70c-215">By default, your application will be deployed as a subdirectory of hello application server.</span></span> <span data-ttu-id="4e70c-216">Jeśli chcesz toobe wdrożony jako aplikacja główna hello, sprawdź hello **wdrażanie tooroot** wyboru przed kliknięciem przycisku **OK**.</span><span class="sxs-lookup"><span data-stu-id="4e70c-216">If you want it toobe deployed as hello root application, check hello **Deploy tooroot** checkbox before clicking **OK**.</span></span>
   
    ![Wdrażanie tooAzure][15]
7. <span data-ttu-id="4e70c-218">Następnie powinna zostać wyświetlona hello **dziennika aktywności platformy Azure** widoku, który będzie wskazywać hello stan wdrożenia aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="4e70c-218">Next, you should see hello **Azure Activity Log** view, which will indicate hello deployment status of your Web App.</span></span>
   
    ![Wskaźnik postępu][16]
   
    <span data-ttu-id="4e70c-220">Hello proces wdrażania tooAzure Twojej aplikacji sieci Web powinien zająć tylko kilka sekund toocomplete.</span><span class="sxs-lookup"><span data-stu-id="4e70c-220">hello process of deploying your Web App tooAzure should take only a few seconds toocomplete.</span></span> <span data-ttu-id="4e70c-221">Jeśli możesz już aplikacji, zobaczysz łącze o nazwie **opublikowano** w hello **stan** kolumny.</span><span class="sxs-lookup"><span data-stu-id="4e70c-221">When your application ready, you will see a link named **Published** in hello **Status** column.</span></span> <span data-ttu-id="4e70c-222">Po kliknięciu łącza hello potrwa strony głównej aplikacji sieci Web tooyour wdrożona lub hello czynności można użyć w następującej aplikacji sieci web tooyour toobrowse sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="4e70c-222">When you click hello link, it will take you tooyour deployed Web App's home page, or you can use hello steps in hello following section toobrowse tooyour web app.</span></span>

## <a name="browsing-tooyour-web-app-on-azure"></a><span data-ttu-id="4e70c-223">Przeglądanie tooyour aplikacji sieci Web na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="4e70c-223">Browsing tooyour Web App on Azure</span></span>
<span data-ttu-id="4e70c-224">tooyour toobrowse aplikacji sieci Web na platformie Azure, można użyć hello **Eksploratora Azure** widoku.</span><span class="sxs-lookup"><span data-stu-id="4e70c-224">toobrowse tooyour Web App on Azure, you can use hello **Azure Explorer** view.</span></span>

<span data-ttu-id="4e70c-225">Jeśli hello **Eksploratora Azure** widoku nie jest jeszcze otwarty, otwórz go, klikając następnie **widoku** menu w IntelliJ, następnie kliknij przycisk **okna narzędzi**, a następnie kliknij przycisk  **Eksplorator usługi**.</span><span class="sxs-lookup"><span data-stu-id="4e70c-225">If hello **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="4e70c-226">Jeśli dany system nie zostały wcześniej zarejestrowane, go spowoduje wyświetlenie monitu toodo tak.</span><span class="sxs-lookup"><span data-stu-id="4e70c-226">If you have not previously logged in, it will prompt you toodo so.</span></span>

<span data-ttu-id="4e70c-227">Gdy hello **Eksploratora Azure** zostanie wyświetlony widok, użyj wykonaj te kroki toobrowse tooyour aplikacji sieci Web:</span><span class="sxs-lookup"><span data-stu-id="4e70c-227">When hello **Azure Explorer** view is displayed, use follow these steps toobrowse tooyour Web App:</span></span> 

1. <span data-ttu-id="4e70c-228">Rozwiń węzeł hello **Azure** węzła.</span><span class="sxs-lookup"><span data-stu-id="4e70c-228">Expand hello **Azure** node.</span></span>
2. <span data-ttu-id="4e70c-229">Rozwiń węzeł hello **aplikacje sieci Web** węzła.</span><span class="sxs-lookup"><span data-stu-id="4e70c-229">Expand hello **Web Apps** node.</span></span> 
3. <span data-ttu-id="4e70c-230">Kliknij prawym przyciskiem myszy hello żądana aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="4e70c-230">Right-click hello desired Web App.</span></span>
4. <span data-ttu-id="4e70c-231">Po wyświetleniu menu kontekstowe powitania kliknij **Otwórz w przeglądarce**.</span><span class="sxs-lookup"><span data-stu-id="4e70c-231">When hello context menu appears, click **Open in Browser**.</span></span>
   
    ![Przeglądanie aplikacji sieci Web][17]

## <a name="updating-your-web-app"></a><span data-ttu-id="4e70c-233">Aktualizowanie aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="4e70c-233">Updating your web app</span></span>
<span data-ttu-id="4e70c-234">Aktualizowanie istniejącej uruchamiania aplikacji sieci Web platformy Azure jest procesem szybkie i łatwe i dostępne są dwie opcje aktualizacji:</span><span class="sxs-lookup"><span data-stu-id="4e70c-234">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="4e70c-235">Można aktualizować hello wdrażania istniejącej aplikacji sieci Web Java.</span><span class="sxs-lookup"><span data-stu-id="4e70c-235">You can update hello deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="4e70c-236">Możesz opublikować dodatkowe toohello aplikacji Java tego samego kontenera aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="4e70c-236">You can publish an additional Java application toohello same Web App Container.</span></span>

<span data-ttu-id="4e70c-237">W obu przypadkach procesu hello jest identyczne i zajmuje tylko kilka sekund:</span><span class="sxs-lookup"><span data-stu-id="4e70c-237">In either case, hello process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="4e70c-238">W obszarze Eksplorator projektów IntelliJ hello kliknij prawym przyciskiem myszy aplikacji Java hello mają tooupdate lub Dodaj tooan istniejącego kontenera aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="4e70c-238">In hello IntelliJ project explorer, right-click hello Java application you want tooupdate or add tooan existing Web App Container.</span></span>
2. <span data-ttu-id="4e70c-239">Po wyświetleniu menu kontekstowe hello zaznacz **Azure** , a następnie **Publikuj jako aplikacji sieci Web platformy Azure...**</span><span class="sxs-lookup"><span data-stu-id="4e70c-239">When hello context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>
3. <span data-ttu-id="4e70c-240">Ponieważ użytkownik ma już zalogowany wcześniej, zostanie wyświetlona lista sieci kontenerów istniejących aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="4e70c-240">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="4e70c-241">Wybierz hello mają toopublish lub ponownie opublikować kliknięcia tooand aplikacji Java **OK**.</span><span class="sxs-lookup"><span data-stu-id="4e70c-241">Select hello one you want toopublish or re-publish your Java application tooand click **OK**.</span></span>

<span data-ttu-id="4e70c-242">Hello później za kilka sekund **dziennika aktywności platformy Azure** widoku wyświetli zaktualizowane wdrożenia jako **opublikowano** i będą mogli tooverify zaktualizowane aplikacji w przeglądarce sieci web.</span><span class="sxs-lookup"><span data-stu-id="4e70c-242">A few seconds later, hello **Azure Activity Log** view will show your updated deployment as **Published** and you will be able tooverify your updated application in a web browser.</span></span>

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="4e70c-243">Uruchamianie, zatrzymywanie lub ponowne uruchamianie istniejących aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="4e70c-243">Starting, stopping, or restarting an existing web app</span></span>
<span data-ttu-id="4e70c-244">toostart lub zatrzymać istniejącego kontenera aplikacji sieci Web platformy Azure (w tym wszystkich aplikacji Java hello wdrożone w nim), możesz użyć hello **Eksploratora Azure** widoku.</span><span class="sxs-lookup"><span data-stu-id="4e70c-244">toostart or stop an existing Azure Web App container, (including all hello deployed Java applications in it), you can use hello **Azure Explorer** view.</span></span>

<span data-ttu-id="4e70c-245">Jeśli hello **Eksploratora Azure** widoku nie jest jeszcze otwarty, otwórz go, klikając następnie **widoku** menu w IntelliJ, następnie kliknij przycisk **okna narzędzi**, a następnie kliknij przycisk  **Eksplorator usługi**.</span><span class="sxs-lookup"><span data-stu-id="4e70c-245">If hello **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="4e70c-246">Jeśli dany system nie zostały wcześniej zarejestrowane, go spowoduje wyświetlenie monitu toodo tak.</span><span class="sxs-lookup"><span data-stu-id="4e70c-246">If you have not previously logged in, it will prompt you toodo so.</span></span>

<span data-ttu-id="4e70c-247">Gdy hello **Eksploratora Azure** zostanie wyświetlony widok, użyj wykonaj te kroki toostart lub Zatrzymaj aplikację sieci Web:</span><span class="sxs-lookup"><span data-stu-id="4e70c-247">When hello **Azure Explorer** view is displayed, use follow these steps toostart or stop your Web App:</span></span> 

1. <span data-ttu-id="4e70c-248">Rozwiń węzeł hello **Azure** węzła.</span><span class="sxs-lookup"><span data-stu-id="4e70c-248">Expand hello **Azure** node.</span></span>
2. <span data-ttu-id="4e70c-249">Rozwiń węzeł hello **aplikacje sieci Web** węzła.</span><span class="sxs-lookup"><span data-stu-id="4e70c-249">Expand hello **Web Apps** node.</span></span> 
3. <span data-ttu-id="4e70c-250">Kliknij prawym przyciskiem myszy hello żądana aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="4e70c-250">Right-click hello desired Web App.</span></span>
4. <span data-ttu-id="4e70c-251">Po wyświetleniu menu kontekstowe powitania kliknij **Start**, **zatrzymać**, lub **ponownego uruchomienia**.</span><span class="sxs-lookup"><span data-stu-id="4e70c-251">When hello context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="4e70c-252">Należy zauważyć, że hello menu opcji kontekstu obsługujący, więc tylko zatrzymać uruchomionej aplikacji sieci web ani uruchomić aplikacji sieci web, która nie jest obecnie uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="4e70c-252">Note that hello menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
    ![Zatrzymać aplikacji sieci Web][18]

## <a name="next-steps"></a><span data-ttu-id="4e70c-254">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4e70c-254">Next Steps</span></span>
<span data-ttu-id="4e70c-255">Aby uzyskać więcej informacji na temat hello narzędzi Azure dla języka Java IDEs Zobacz hello następującego łącza:</span><span class="sxs-lookup"><span data-stu-id="4e70c-255">For more information about hello Azure Toolkits for Java IDEs, see hello following links:</span></span>

* <span data-ttu-id="4e70c-256">[Azure zestawu narzędzi dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="4e70c-256">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="4e70c-257">[Instalowanie hello zestawu narzędzi platformy Azure dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="4e70c-257">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="4e70c-258">[Tworzenie aplikacji sieci Web Hello World na platformie Azure w programie Eclipse]</span><span class="sxs-lookup"><span data-stu-id="4e70c-258">[Create a Hello World Web App for Azure in Eclipse]</span></span>
  * <span data-ttu-id="4e70c-259">[Nowości w hello zestawu narzędzi platformy Azure dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="4e70c-259">[What's New in hello Azure Toolkit for Eclipse]</span></span>
* <span data-ttu-id="4e70c-260">[narzędzi Azure dla IntelliJ] (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="4e70c-260">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="4e70c-261">[hello Instalowanie narzędzi Azure dla IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="4e70c-261">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="4e70c-262">*Tworzenie aplikacji sieci Web Hello World na platformie Azure w IntelliJ (w tym artykule)*</span><span class="sxs-lookup"><span data-stu-id="4e70c-262">*Create a Hello World Web App for Azure in IntelliJ (This Article)*</span></span>
  * <span data-ttu-id="4e70c-263">[Nowości w hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="4e70c-263">[What's New in hello Azure Toolkit for IntelliJ]</span></span>

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="4e70c-264">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="4e70c-264">See Also</span></span>
<span data-ttu-id="4e70c-265">Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz hello [Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="4e70c-265">For more information about using Azure with Java, see hello [Azure Java Developer Center].</span></span>

<span data-ttu-id="4e70c-266">Aby uzyskać dodatkowe informacje dotyczące tworzenia aplikacji sieci Web platformy Azure, zobacz hello [Omówienie aplikacji sieci Web].</span><span class="sxs-lookup"><span data-stu-id="4e70c-266">For additional information about creating Azure Web Apps, see hello [Web Apps Overview].</span></span>

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[Azure zestawu narzędzi dla programu Eclipse]: ../azure-toolkit-for-eclipse.md
[narzędzi Azure dla IntelliJ]: ../azure-toolkit-for-intellij.md (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)
[Tworzenie aplikacji sieci Web Hello World na platformie Azure w programie Eclipse]: ./app-service-web-eclipse-create-hello-world-web-app.md
[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web-intellij-create-hello-world-web-app.md
[Instalowanie hello zestawu narzędzi platformy Azure dla programu Eclipse]: ../azure-toolkit-for-eclipse-installation.md
[hello Instalowanie narzędzi Azure dla IntelliJ]: ../azure-toolkit-for-intellij-installation.md
[Nowości w hello zestawu narzędzi platformy Azure dla programu Eclipse]: ../azure-toolkit-for-eclipse-whats-new.md
[Nowości w hello Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij-whats-new.md

[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Omówienie aplikacji sieci Web]: ./app-service-web-overview.md
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/

<!-- IMG List -->

[01]: ./media/app-service-web-intellij-create-hello-world-web-app/01-Web-Page.png
[02]: ./media/app-service-web-intellij-create-hello-world-web-app/02-File-New-Project.png
[03a]: ./media/app-service-web-intellij-create-hello-world-web-app/03-New-Project-Dialog.png
[03b]: ./media/app-service-web-intellij-create-hello-world-web-app/03-New-Project-SDK-Dialog.png
[04]: ./media/app-service-web-intellij-create-hello-world-web-app/04-New-Project-Dialog.png
[05a]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Open-Module-Settings.png
[05b]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Project-Structure-Dialog.png
[05c]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Open-Index-Page.png
[06]: ./media/app-service-web-intellij-create-hello-world-web-app/06-Azure-Publish-Context-Menu.png
[07]: ./media/app-service-web-intellij-create-hello-world-web-app/07-Azure-Log-In-Dialog.png
[08]: ./media/app-service-web-intellij-create-hello-world-web-app/08-Manage-Subscriptions.png
[09]: ./media/app-service-web-intellij-create-hello-world-web-app/09-App-Containers.png
[10]: ./media/app-service-web-intellij-create-hello-world-web-app/10-Add-App-Container.png
[11a]: ./media/app-service-web-intellij-create-hello-world-web-app/11-New-App-Container.png
[11b]: ./media/app-service-web-intellij-create-hello-world-web-app/11-New-App-Container-JDK-Tab.png
[12]: ./media/app-service-web-intellij-create-hello-world-web-app/12-New-Resource-Group.png
[13]: ./media/app-service-web-intellij-create-hello-world-web-app/13-New-App-Service-Plan.png
[14]: ./media/app-service-web-intellij-create-hello-world-web-app/14-New-App-Container.png
[15]: ./media/app-service-web-intellij-create-hello-world-web-app/15-Deploy-To-Azure.png
[16]: ./media/app-service-web-intellij-create-hello-world-web-app/16-Progress-Indicator.png
[17]: ./media/app-service-web-intellij-create-hello-world-web-app/17-Browse-Web-App.png
[18]: ./media/app-service-web-intellij-create-hello-world-web-app/18-Stop-Web-App.png
