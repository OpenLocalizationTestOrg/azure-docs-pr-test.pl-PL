---
title: "Zaćmienie-aaaCreate aplikacji sieci web platformy Azure podstawowe przy użyciu | Dokumentacja firmy Microsoft"
description: "Ten samouczek pokazuje, jak toouse hello zestawu narzędzi platformy Azure dla programu Eclipse toocreate aplikacji Hello World sieci Web dla platformy Azure."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 20d41e88-9eab-462e-8ee3-89da71e7a33f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm;asirveda
ms.openlocfilehash: b2f42e0e7a5b98760ec02fab2fc38f9f07b1156b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-basic-azure-web-app-using-eclipse"></a><span data-ttu-id="cece2-103">Tworzenie aplikacji sieci web platformy Azure podstawowe za pomocą programu Eclipse</span><span class="sxs-lookup"><span data-stu-id="cece2-103">Create a basic Azure web app using Eclipse</span></span>
<span data-ttu-id="cece2-104">Ten samouczek pokazuje, jak toocreate i wdrażania podstawowych tooAzure aplikacji Hello World jako aplikacji sieci Web przy użyciu hello [zestawu narzędzi platformy Azure dla programu Eclipse].</span><span class="sxs-lookup"><span data-stu-id="cece2-104">This tutorial shows how toocreate and deploy a basic Hello World application tooAzure as a Web App by using hello [Azure Toolkit for Eclipse].</span></span> <span data-ttu-id="cece2-105">Podstawowy przykład JSP jest widoczna dla uproszczenia, ale podobne kroki będzie odpowiednia dla serwlet Java, jakim jest dotyczy wdrożenia usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="cece2-105">A basic JSP example is shown for simplicity, but similar steps would be appropriate for a Java servlet, as far as Azure deployment is concerned.</span></span>

<span data-ttu-id="cece2-106">Po ukończeniu tego samouczka, aplikacja będzie wyglądać podobnie toohello następującej ilustracji, podczas wyświetlania w przeglądarce sieci web:</span><span class="sxs-lookup"><span data-stu-id="cece2-106">When you have completed this tutorial, your application will look similar toohello following illustration when you view it in a web browser:</span></span>

![Podgląd Hello World aplikacji][01]

## <a name="prerequisites"></a><span data-ttu-id="cece2-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="cece2-108">Prerequisites</span></span>
* <span data-ttu-id="cece2-109">Java Developer Kit (JDK), v 1,8 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="cece2-109">A Java Developer Kit (JDK), v 1.8 or later.</span></span>
* <span data-ttu-id="cece2-110">Zaćmienie-IDE for Java EE Developers Luna lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="cece2-110">Eclipse IDE for Java EE Developers, Luna or later.</span></span> <span data-ttu-id="cece2-111">Ten można pobrać z <http://www.eclipse.org/downloads/>.</span><span class="sxs-lookup"><span data-stu-id="cece2-111">This can be downloaded from <http://www.eclipse.org/downloads/>.</span></span>
* <span data-ttu-id="cece2-112">Dystrybucji serwera sieci web opartych na języku Java lub serwera aplikacji takich jak [Apache Tomcat] lub [Jetty].</span><span class="sxs-lookup"><span data-stu-id="cece2-112">A distribution of a Java-based web server or application server, such as [Apache Tomcat] or [Jetty].</span></span>
* <span data-ttu-id="cece2-113">Subskrypcję platformy Azure, która może zostać pobrany z <https://azure.microsoft.com/free/> lub <http://azure.microsoft.com/pricing/purchase-options/>.</span><span class="sxs-lookup"><span data-stu-id="cece2-113">An Azure subscription, which can be acquired from <https://azure.microsoft.com/free/> or <http://azure.microsoft.com/pricing/purchase-options/>.</span></span>
* <span data-ttu-id="cece2-114">Witaj [zestawu narzędzi platformy Azure dla programu Eclipse].</span><span class="sxs-lookup"><span data-stu-id="cece2-114">hello [Azure Toolkit for Eclipse].</span></span> <span data-ttu-id="cece2-115">Informacje o instalowaniu hello zestawu narzędzi platformy Azure, zobacz [hello Instalowanie zestawu narzędzi platformy Azure dla programu Eclipse].</span><span class="sxs-lookup"><span data-stu-id="cece2-115">For information about installing hello Azure Toolkit, see [Installing hello Azure Toolkit for Eclipse].</span></span>

## <a name="toocreate-a-hello-world-application"></a><span data-ttu-id="cece2-116">toocreate aplikacji Hello World</span><span class="sxs-lookup"><span data-stu-id="cece2-116">toocreate a Hello World application</span></span>
<span data-ttu-id="cece2-117">Po pierwsze Zaczniemy tworzenia projektu języka Java.</span><span class="sxs-lookup"><span data-stu-id="cece2-117">First, we'll start off with creating a Java project.</span></span>

1. <span data-ttu-id="cece2-118">Uruchom środowisko Eclipse, a następnie w menu powitania kliknij **pliku**, kliknij przycisk **nowy**, a następnie kliknij przycisk **dynamiczny projekt sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="cece2-118">Start Eclipse, and at hello menu click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="cece2-119">(Jeśli nie widzisz **dynamiczny projekt sieci Web** wymienione jako projekt dostępne po kliknięciu przycisku **pliku** i **nowy**, następnie hello następujące: kliknij **pliku**, kliknij przycisk **nowy**, kliknij przycisk **projektu...** , rozwiń węzeł **Web**, kliknij przycisk **dynamiczny projekt sieci Web**i kliknij przycisk **dalej**.)</span><span class="sxs-lookup"><span data-stu-id="cece2-119">(If you don't see **Dynamic Web Project** listed as an available project after clicking **File** and **New**, then do hello following: click **File**, click **New**, click **Project...**, expand **Web**, click **Dynamic Web Project**, and click **Next**.)</span></span>
2. <span data-ttu-id="cece2-120">Do celów tego samouczka, nazwa projektu hello **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="cece2-120">For purposes of this tutorial, name hello project **MyWebApp**.</span></span> <span data-ttu-id="cece2-121">Na ekranie pojawi się podobne toohello następujące:</span><span class="sxs-lookup"><span data-stu-id="cece2-121">Your screen will appear similar toohello following:</span></span>
   
    ![Tworzenie nowego projektu sieci Web dynamiczne][02]
3. <span data-ttu-id="cece2-123">Kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="cece2-123">Click **Finish**.</span></span>
4. <span data-ttu-id="cece2-124">W widoku Eksplorator projektów w środowisku Eclipse, rozwiń węzeł **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="cece2-124">Within Eclipse's Project Explorer view, expand **MyWebApp**.</span></span> <span data-ttu-id="cece2-125">Kliknij prawym przyciskiem myszy folder **WebContent**, kliknij polecenie **New** (Nowy), a następnie kliknij polecenie **JSP File** (Plik JSP).</span><span class="sxs-lookup"><span data-stu-id="cece2-125">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>
5. <span data-ttu-id="cece2-126">W hello **New JSP File** okno dialogowe, nazwa pliku hello **index.jsp**, przechowuj folder nadrzędny hello jako **MyWebApp/WebContent**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="cece2-126">In hello **New JSP File** dialog box, name hello file **index.jsp**, keep hello parent folder as **MyWebApp/WebContent**, and then click **Next**.</span></span>
6. <span data-ttu-id="cece2-127">W hello **wybierz szablon JSP** okno dialogowe do celów tego samouczka wybierz **New JSP File (html)**, a następnie kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="cece2-127">In hello **Select JSP Template** dialog box, for purposes of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>
7. <span data-ttu-id="cece2-128">Po otwarciu pliku index.jsp w środowisku Eclipse Dodaj tekst toodynamically wyświetlania **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="cece2-128">When your index.jsp file opens in Eclipse, add in text toodynamically display **Hello World!**</span></span> <span data-ttu-id="cece2-129">w ramach istniejącego hello `<body>` elementu.</span><span class="sxs-lookup"><span data-stu-id="cece2-129">within hello existing `<body>` element.</span></span> <span data-ttu-id="cece2-130">Zaktualizowana `<body>` zawartość powinna wyglądać hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="cece2-130">Your updated `<body>` content should resemble hello following example:</span></span>
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
8. <span data-ttu-id="cece2-131">Zapisz index.jsp.</span><span class="sxs-lookup"><span data-stu-id="cece2-131">Save index.jsp.</span></span>

## <a name="toodeploy-your-application-tooan-azure-web-app-container"></a><span data-ttu-id="cece2-132">toodeploy Twojego tooan aplikacji kontenera aplikacji sieci Web Azure</span><span class="sxs-lookup"><span data-stu-id="cece2-132">toodeploy your application tooan Azure Web App Container</span></span>
<span data-ttu-id="cece2-133">Istnieje kilka metod, które można wdrożyć tooAzure aplikacji sieci web Java.</span><span class="sxs-lookup"><span data-stu-id="cece2-133">There are several ways by which you can deploy a Java web application tooAzure.</span></span> <span data-ttu-id="cece2-134">Ten samouczek zawiera opis jednego z hello najprostszym: aplikacja będzie tooan wdrożony kontener aplikacji sieci Web platformy Azure — żadnych typ projektu ani dodatkowe narzędzia są niezbędne.</span><span class="sxs-lookup"><span data-stu-id="cece2-134">This tutorial describes one of hello simplest: your application will be deployed tooan Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="cece2-135">Hello JDK i hello kontenera oprogramowanie dla sieci web zostanie zostać dostarczony przez platformę Azure, więc nie ma żadnych tooupload potrzeby własne; potrzebna jest aplikacja sieci Web Java.</span><span class="sxs-lookup"><span data-stu-id="cece2-135">hello JDK and hello web container software will be provided for you by Azure, so there is no need tooupload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="cece2-136">W związku z tym hello proces publikowania aplikacji może zająć sekund, nie minut.</span><span class="sxs-lookup"><span data-stu-id="cece2-136">As a result, hello publishing process for your application will take seconds, not minutes.</span></span>

1. <span data-ttu-id="cece2-137">W obszarze Eksplorator projektów w środowisku Eclipse, kliknij prawym przyciskiem myszy **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="cece2-137">In Eclipse's Project Explorer, right-click **MyWebApp**.</span></span>
2. <span data-ttu-id="cece2-138">W menu kontekstowym hello, wybierz **Azure**, następnie kliknij przycisk **Publikuj jako aplikacji sieci Web platformy Azure...**</span><span class="sxs-lookup"><span data-stu-id="cece2-138">In hello context menu, select **Azure**, then click **Publish as Azure Web App...**</span></span>
   
    ![Publikowanie aplikacji sieci Web jako platformy Azure][03]
   
    <span data-ttu-id="cece2-140">Alternatywnie podczas projektu aplikacji sieci web jest zaznaczone hello Eksplorator projektów, można kliknąć hello **publikowania** rozwijany przycisk na powitania narzędzi i wybierz **Publikuj jako aplikacji sieci Web Azure** stamtąd:</span><span class="sxs-lookup"><span data-stu-id="cece2-140">Alternatively, while your web application project is selected in hello Project Explorer, you can click hello **Publish** dropdown button on hello toolbar and select **Publish as Azure Web App** from there:</span></span>
   
    ![Publikowanie aplikacji sieci Web jako platformy Azure][14]
3. <span data-ttu-id="cece2-142">Jeśli dany komputer nie ma już podpisany na platformie Azure z Eclipse, będzie toosign zostanie wyświetlony monit o do konta platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="cece2-142">If you have not already signed into Azure from Eclipse, you will be prompted toosign into your Azure account:</span></span>
   
    ![Azure logowania — okno dialogowe][04]
   
    <span data-ttu-id="cece2-144">Jeśli masz wiele kont platformy Azure, zaloguj się niektóre hello monity podczas hello procesu mogą być wyświetlane więcej niż raz, nawet wtedy, gdy pojawią się one toobe hello takie same.</span><span class="sxs-lookup"><span data-stu-id="cece2-144">If you have multiple Azure accounts, some of hello prompts during hello sign in process may be shown more than once, even if they appear toobe hello same.</span></span> <span data-ttu-id="cece2-145">W takim przypadku należy kontynuować, następujące hello logowania instrukcje.</span><span class="sxs-lookup"><span data-stu-id="cece2-145">When this happens, continue following hello sign in instructions.</span></span>
4. <span data-ttu-id="cece2-146">Po pomyślnym zarejestrowaniu do konta platformy Azure, hello **Zarządzaj subskrypcjami** dialogowym zostanie wyświetlona lista subskrypcji, które są skojarzone z poświadczeniami użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cece2-146">After you have successfully signed into your Azure account, hello **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="cece2-147">Jeśli istnieje wiele wymienionych subskrypcji i chcesz toowork z konkretnego podzestawu z nich, może opcjonalnie Usuń zaznaczenie pola hello mają toouse z nich.</span><span class="sxs-lookup"><span data-stu-id="cece2-147">If there are multiple subscriptions listed and you want toowork with only a specific subset of them, you may optionally uncheck hello ones you do want toouse.</span></span> <span data-ttu-id="cece2-148">Po zakończeniu wybierania subskrypcji, kliknij przycisk **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="cece2-148">When you have selected your subscriptions, click **Close**.</span></span>
   
    ![Zarządzaj subskrypcjami, okno dialogowe][05]
5. <span data-ttu-id="cece2-150">Gdy hello **wdrażanie tooAzure kontenera aplikacji sieci Web** zostanie wyświetlone okno dialogowe będzie ono żadnych kontenerów aplikacji sieci Web, które wcześniej zostały utworzone; Jeśli nie utworzono żadnych kontenerów, hello lista jest pusta.</span><span class="sxs-lookup"><span data-stu-id="cece2-150">When hello **Deploy tooAzure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, hello list will be empty.</span></span>
   
    ![Wdrażanie tooAzure kontenera aplikacji sieci Web, okno dialogowe][06]
6. <span data-ttu-id="cece2-152">Jeśli nie utworzono kontener aplikacji sieci Web Azure przed lub jeśli chcesz toopublish Twojej aplikacji tooa nowy kontener, użyj hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="cece2-152">If you have not created an Azure Web App Container before, or if you would like toopublish your application tooa new container, use hello following steps.</span></span> <span data-ttu-id="cece2-153">W przeciwnym razie wybierz kontener istniejących aplikacji sieci Web i pominąć toostep 7 poniżej.</span><span class="sxs-lookup"><span data-stu-id="cece2-153">Otherwise, select an existing Web App Container and skip toostep 7 below.</span></span>
   
   1. <span data-ttu-id="cece2-154">Kliknij przycisk **nowych...**</span><span class="sxs-lookup"><span data-stu-id="cece2-154">Click **New...**</span></span>
      
       ![Wdrażanie tooAzure kontenera aplikacji sieci Web, okno dialogowe][15]
   2. <span data-ttu-id="cece2-156">Witaj **nowy kontener aplikacji sieci Web** wyświetli się okno dialogowe:</span><span class="sxs-lookup"><span data-stu-id="cece2-156">hello **New Web App Container** dialog box will be displayed:</span></span>
      
       ![Okno dialogowe nowy kontener aplikacji sieci Web][07a]
   3. <span data-ttu-id="cece2-158">Wprowadź **Etykieta DNS** dla kontener aplikacji sieci Web; to będzie stanowić etykietę DNS liścia hello hello hosta adres URL aplikacji sieci web na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="cece2-158">Enter a **DNS Label** for your Web App Container; this will form hello leaf DNS label of hello host URL for your web application in Azure.</span></span> <span data-ttu-id="cece2-159">(Należy zauważyć, że nazwa hello musi być dostępny i jest zgodna z wymaganiami dotyczącymi nazw aplikacji sieci Web tooAzure).</span><span class="sxs-lookup"><span data-stu-id="cece2-159">(Note that hello name must be available and conform tooAzure Web App naming requirements.)</span></span>
   4. <span data-ttu-id="cece2-160">W hello **kontener sieci Web** menu rozwijanego, wybierz hello odpowiedniego oprogramowania dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cece2-160">In hello **Web Container** drop-down menu, select hello appropriate software for your application.</span></span>
      
       <span data-ttu-id="cece2-161">Obecnie można wybrać z Tomcat 8 Tomcat 7 lub Jetty 9.</span><span class="sxs-lookup"><span data-stu-id="cece2-161">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="cece2-162">Ostatnie dystrybucji oprogramowania hello wybrane będą udostępniane przez usługi Azure, a zostanie uruchomiony na ostatnie dystrybucji 8 JDK utworzone przez firmę Oracle i dostarczany przez platformę Azure.</span><span class="sxs-lookup"><span data-stu-id="cece2-162">A recent distribution of hello selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span></span>
   5. <span data-ttu-id="cece2-163">W hello **subskrypcji** menu rozwijanego, wybierz hello subskrypcję toouse dla tego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="cece2-163">In hello **Subscription** drop-down menu, select hello subscription you want toouse for this deployment.</span></span>
   6. <span data-ttu-id="cece2-164">W hello **grupy zasobów** menu rozwijane i wybierz hello grupy zasobów, z którą chcesz tooassociate aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="cece2-164">In hello **Resource Group** drop-down menu, select hello Resource Group with which you want tooassociate your Web App.</span></span> <span data-ttu-id="cece2-165">(Zezwalaj grup zasobów platformy azure możesz toogroup powiązane ze sobą zasoby, tak, aby na przykład je usunąć ze sobą.)</span><span class="sxs-lookup"><span data-stu-id="cece2-165">(Azure Resource Groups allow you toogroup related resources together so that, for example, they can be deleted together.)</span></span>
      
       <span data-ttu-id="cece2-166">Można wybrać istniejącą grupę zasobów (jeśli) i Pomiń toostep g poniżej lub hello Użyj następującego te kroki toocreate nową grupę zasobów:</span><span class="sxs-lookup"><span data-stu-id="cece2-166">You can select an existing Resource Group (if you have any) and skip toostep g below, or use hello following these steps toocreate a new Resource Group:</span></span>
      
      * <span data-ttu-id="cece2-167">Kliknij przycisk **nowych...**</span><span class="sxs-lookup"><span data-stu-id="cece2-167">Click **New...**</span></span>
      * <span data-ttu-id="cece2-168">Witaj **nową grupę zasobów** wyświetli się okno dialogowe:</span><span class="sxs-lookup"><span data-stu-id="cece2-168">hello **New Resource Group** dialog box will be displayed:</span></span>
        
          ![Okno dialogowe nowej grupy zasobów][08]
      * <span data-ttu-id="cece2-170">W hello hello **nazwa** pole tekstowe, określ nazwę nowej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="cece2-170">In hello hello **Name** textbox, specify a name for your new Resource Group.</span></span>
      * <span data-ttu-id="cece2-171">W hello hello **Region** menu rozwijanego wybierz hello odpowiednie usługi Azure data center lokalizację dla grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="cece2-171">In hello hello **Region** drop-down menu, select hello appropriate Azure data center location for your Resource Group.</span></span>
      * <span data-ttu-id="cece2-172">OPCJONALNIE: Domyślnie ostatnie dystrybucji Java 8 będą wdrażane przez platformę Azure automatycznie tooyour kontenera aplikacji sieci web jako sieci maszyny wirtualnej Java.</span><span class="sxs-lookup"><span data-stu-id="cece2-172">OPTIONAL: By default, a recent distribution of Java 8 will be deployed by Azure automatically tooyour web app container as your JVM.</span></span> <span data-ttu-id="cece2-173">Jednak można określić inną wersję i dystrybucji hello JVM, jeśli aplikacja sieci Web wymaga.</span><span class="sxs-lookup"><span data-stu-id="cece2-173">However, you can specify a different version and distribution of hello JVM if your Web App requires it.</span></span> <span data-ttu-id="cece2-174">Witaj toospecify JDK dla aplikacji sieci Web, kliknij przycisk hello **JDK** i wybierz jedną z hello następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="cece2-174">toospecify hello JDK for your Web App, click hello **JDK** tab, and select one of hello following options:</span></span>
        
        * <span data-ttu-id="cece2-175">**Wdróż domyślne hello JDK oferowane przez usługę Azure Web Apps**: Ta opcja zostanie wdrożona ostatnie dystrybucji Java 8.</span><span class="sxs-lookup"><span data-stu-id="cece2-175">**Deploy hello default JDK offered by Azure Web Apps service**: This option will deploy a recent distribution of Java 8.</span></span>
        * <span data-ttu-id="cece2-176">**Wdrażanie 3 strona JDK dostępnych na platformie Azure**: Ta opcja umożliwia toochoose z listy hello JDKs, które są udostępniane przez Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="cece2-176">**Deploy a 3rd party JDK available on Azure**: This option allows you toochoose from hello list of JDKs which are provided by Microsoft Azure.</span></span>
        * <span data-ttu-id="cece2-177">**Wdrażanie własnych JDK z tej lokalizacji pobierania**: Ta opcja umożliwia toospecify własne dystrybucji JDK, które muszą być spakowane jako plik ZIP i przekazać tooeither lokalizacji pobierania publicznie dostępnych lub magazynu Azure konta, dla którego należy masz dostęp.</span><span class="sxs-lookup"><span data-stu-id="cece2-177">**Deploy my own JDK from this download location**: This option allows you toospecify your own JDK distribution, which must be packaged as a ZIP file and uploaded tooeither a publicly available download location or an Azure storage account for which you have access.</span></span>
          
          ![Okno dialogowe nowy kontener aplikacji sieci Web][07b]
   7. <span data-ttu-id="cece2-179">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="cece2-179">Click **OK**.</span></span>
   8. <span data-ttu-id="cece2-180">Witaj **planu usługi App Service** hello planów usługi aplikacji, które są skojarzone z hello wybrana grupa zasobów zawiera menu rozwijanego.</span><span class="sxs-lookup"><span data-stu-id="cece2-180">hello **App Service Plan** drop-down menu lists hello app service plans that are associated with hello Resource Group that you selected.</span></span> <span data-ttu-id="cece2-181">(Informacje, takie jak lokalizacja hello aplikacji sieci Web, hello warstwa cenowa i rozmiar wystąpienia obliczeniowe hello Określ planów usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cece2-181">(App Service Plans specify information such as hello location of your Web App, hello pricing tier and hello compute instance size.</span></span> <span data-ttu-id="cece2-182">Jeden Plan usługi App Service może służyć do wielu aplikacji sieci Web, dlatego jest obsługiwana oddzielnie od określonego wdrożenia aplikacji sieci Web.)</span><span class="sxs-lookup"><span data-stu-id="cece2-182">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
       <span data-ttu-id="cece2-183">Można wybrać istniejący Plan usługi App Service (jeśli) i Pomiń h toostep poniżej, lub użyj powitania po toocreate te kroki, planu usługi aplikacji:</span><span class="sxs-lookup"><span data-stu-id="cece2-183">You can select an existing App Service Plan (if you have any) and skip toostep h below, or use hello following these steps toocreate a new App Service Plan:</span></span>
      
      * <span data-ttu-id="cece2-184">Kliknij przycisk **nowych...**</span><span class="sxs-lookup"><span data-stu-id="cece2-184">Click **New...**</span></span>
      * <span data-ttu-id="cece2-185">Witaj **nowy Plan usługi App Service** wyświetli się okno dialogowe:</span><span class="sxs-lookup"><span data-stu-id="cece2-185">hello **New App Service Plan** dialog box will be displayed:</span></span>
        
          ![Okno dialogowe Nowy Plan usługi App Service][09]
      * <span data-ttu-id="cece2-187">W hello hello **nazwa** pole tekstowe, określ nazwę planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cece2-187">In hello hello **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="cece2-188">W hello hello **lokalizacji** menu rozwijanego wybierz hello odpowiednie usługi Azure data center lokalizacji dla planu hello.</span><span class="sxs-lookup"><span data-stu-id="cece2-188">In hello hello **Location** drop-down menu, select hello appropriate Azure data center location for hello plan.</span></span>
      * <span data-ttu-id="cece2-189">W hello hello **warstwy cenowej** menu rozwijanego, wybierz odpowiednie ceny dla planu hello hello.</span><span class="sxs-lookup"><span data-stu-id="cece2-189">In hello hello **Pricing Tier** drop-down menu, select hello appropriate pricing for hello plan.</span></span> <span data-ttu-id="cece2-190">Podczas testowania, możesz wybrać **wolne**.</span><span class="sxs-lookup"><span data-stu-id="cece2-190">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="cece2-191">W hello hello **rozmiar wystąpienia** menu rozwijanego, hello wybierz odpowiednie wystąpienie rozmiar hello planu.</span><span class="sxs-lookup"><span data-stu-id="cece2-191">In hello hello **Instance Size** drop-down menu, select hello appropriate instance size for hello plan.</span></span> <span data-ttu-id="cece2-192">Podczas testowania, możesz wybrać **małych**.</span><span class="sxs-lookup"><span data-stu-id="cece2-192">For testing purposes you can choose **Small**.</span></span>
   9. <span data-ttu-id="cece2-193">Po wykonaniu wszystkich hello powyżej kroki, okno dialogowe nowy kontener aplikacji sieci Web hello powinien wyglądać hello następującej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="cece2-193">Once you have completed all of hello above steps, hello New Web App Container dialog box should resemble hello following illustration:</span></span>
      
       ![Okno dialogowe nowy kontener aplikacji sieci Web][10]
   10. <span data-ttu-id="cece2-195">Kliknij przycisk **OK** tworzenie hello toocomplete Twojego nowego kontenera aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="cece2-195">Click **OK** toocomplete hello creation of your new Web App container.</span></span>
       
        <span data-ttu-id="cece2-196">Zaczekaj kilka sekund hello lista toobe kontenery sieci Web aplikacji hello odświeżyć, a kontener aplikacji sieci web nowo utworzony powinny teraz być zaznaczone na liście hello.</span><span class="sxs-lookup"><span data-stu-id="cece2-196">Wait a few seconds for hello list of hello Web App containers toobe refreshed, and your newly-created web app container should now be selected in hello list.</span></span>
7. <span data-ttu-id="cece2-197">Wszystko jest teraz gotowy toocomplete hello początkowe wdrożenie tooAzure Twojej aplikacji sieci Web:</span><span class="sxs-lookup"><span data-stu-id="cece2-197">You are now ready toocomplete hello initial deployment of your Web App tooAzure:</span></span>
   
    ![Wdrażanie tooAzure kontenera aplikacji sieci Web, okno dialogowe][11]
   
    <span data-ttu-id="cece2-199">Kliknij przycisk **OK** toodeploy Twojego toohello aplikacji Java wybrany kontener aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="cece2-199">Click **OK** toodeploy your Java application toohello selected Web App container.</span></span>
   
    <span data-ttu-id="cece2-200">Domyślnie aplikacja zostanie wdrożona jako podkatalog serwera aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="cece2-200">By default, your application will be deployed as a subdirectory of hello application server.</span></span> <span data-ttu-id="cece2-201">Jeśli chcesz toobe wdrożony jako aplikacja główna hello, sprawdź hello **wdrażanie tooroot** wyboru przed kliknięciem przycisku **OK**.</span><span class="sxs-lookup"><span data-stu-id="cece2-201">If you want it toobe deployed as hello root application, check hello **Deploy tooroot** checkbox before clicking **OK**.</span></span>
8. <span data-ttu-id="cece2-202">Następnie powinna zostać wyświetlona hello **dziennika aktywności platformy Azure** widoku, który będzie wskazywać hello stan wdrożenia aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="cece2-202">Next, you should see hello **Azure Activity Log** view, which will indicate hello deployment status of your Web App.</span></span>
   
    ![Dziennik aktywności platformy Azure][12]
   
    <span data-ttu-id="cece2-204">Hello proces wdrażania tooAzure Twojej aplikacji sieci Web powinien zająć tylko kilka sekund toocomplete.</span><span class="sxs-lookup"><span data-stu-id="cece2-204">hello process of deploying your Web App tooAzure should take only a few seconds toocomplete.</span></span> <span data-ttu-id="cece2-205">Jeśli możesz już aplikacji, zobaczysz łącze o nazwie **opublikowano** w hello **stan** kolumny.</span><span class="sxs-lookup"><span data-stu-id="cece2-205">When your application ready, you will see a link named **Published** in hello **Status** column.</span></span> <span data-ttu-id="cece2-206">Po kliknięciu łącza hello spowoduje przejście strony głównej aplikacji sieci Web tooyour wdrożone.</span><span class="sxs-lookup"><span data-stu-id="cece2-206">When you click hello link, it will take you tooyour deployed Web App's home page.</span></span>

## <a name="updating-your-web-app"></a><span data-ttu-id="cece2-207">Aktualizowanie aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="cece2-207">Updating your web app</span></span>
<span data-ttu-id="cece2-208">Aktualizowanie istniejącej uruchamiania aplikacji sieci Web platformy Azure jest procesem szybkie i łatwe i dostępne są dwie opcje aktualizacji:</span><span class="sxs-lookup"><span data-stu-id="cece2-208">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="cece2-209">Można aktualizować hello wdrażania istniejącej aplikacji sieci Web Java.</span><span class="sxs-lookup"><span data-stu-id="cece2-209">You can update hello deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="cece2-210">Możesz opublikować dodatkowe toohello aplikacji Java tego samego kontenera aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="cece2-210">You can publish an additional Java application toohello same Web App Container.</span></span>

<span data-ttu-id="cece2-211">W obu przypadkach procesu hello jest identyczne i zajmuje tylko kilka sekund:</span><span class="sxs-lookup"><span data-stu-id="cece2-211">In either case, hello process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="cece2-212">W obszarze Eksplorator projektów programu Eclipse hello kliknij prawym przyciskiem myszy aplikacji Java hello mają tooupdate lub Dodaj tooan istniejącego kontenera aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="cece2-212">In hello Eclipse project explorer, right-click hello Java application you want tooupdate or add tooan existing Web App Container.</span></span>
2. <span data-ttu-id="cece2-213">Po wyświetleniu menu kontekstowe hello zaznacz **Azure** , a następnie **Publikuj jako aplikacji sieci Web platformy Azure...**</span><span class="sxs-lookup"><span data-stu-id="cece2-213">When hello context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>
3. <span data-ttu-id="cece2-214">Ponieważ użytkownik ma już zalogowany wcześniej, zostanie wyświetlona lista sieci kontenerów istniejących aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="cece2-214">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="cece2-215">Wybierz hello mają toopublish lub ponownie opublikować kliknięcia tooand aplikacji Java **OK**.</span><span class="sxs-lookup"><span data-stu-id="cece2-215">Select hello one you want toopublish or re-publish your Java application tooand click **OK**.</span></span>

<span data-ttu-id="cece2-216">Hello później za kilka sekund **dziennika aktywności platformy Azure** widoku wyświetli zaktualizowane wdrożenia jako **opublikowano** i będą mogli tooverify zaktualizowane aplikacji w przeglądarce sieci web.</span><span class="sxs-lookup"><span data-stu-id="cece2-216">A few seconds later, hello **Azure Activity Log** view will show your updated deployment as **Published** and you will be able tooverify your updated application in a web browser.</span></span>

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="cece2-217">Uruchamianie, zatrzymywanie lub ponowne uruchamianie istniejących aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="cece2-217">Starting, stopping, or restarting an existing web app</span></span>
<span data-ttu-id="cece2-218">toostart lub zatrzymać istniejącego kontenera aplikacji sieci Web platformy Azure (w tym wszystkich aplikacji Java hello wdrożone w nim), możesz użyć hello **Eksploratora Azure** widoku.</span><span class="sxs-lookup"><span data-stu-id="cece2-218">toostart or stop an existing Azure Web App container, (including all hello deployed Java applications in it), you can use hello **Azure Explorer** view.</span></span>

<span data-ttu-id="cece2-219">Jeśli hello **Eksploratora Azure** widoku nie jest jeszcze otwarty, otwórz go, klikając następnie **okna** menu w środowisku Eclipse, następnie kliknij przycisk **Pokaż widok**, następnie **innych...** , następnie **Azure**, a następnie kliknij przycisk **Eksploratora Azure**.</span><span class="sxs-lookup"><span data-stu-id="cece2-219">If hello **Azure Explorer** view is not already open, you can open it by clicking then **Window** menu in Eclipse, then click **Show View**, then **Other...**, then **Azure**, and then click **Azure Explorer**.</span></span> <span data-ttu-id="cece2-220">Jeśli dany system nie zostały wcześniej zarejestrowane, go spowoduje wyświetlenie monitu toodo tak.</span><span class="sxs-lookup"><span data-stu-id="cece2-220">If you have not previously logged in, it will prompt you toodo so.</span></span>

<span data-ttu-id="cece2-221">Gdy hello **Eksploratora Azure** zostanie wyświetlony widok, użyj wykonaj te kroki toostart lub Zatrzymaj aplikację sieci Web:</span><span class="sxs-lookup"><span data-stu-id="cece2-221">When hello **Azure Explorer** view is displayed, use follow these steps toostart or stop your Web App:</span></span> 

1. <span data-ttu-id="cece2-222">Rozwiń węzeł hello **Azure** węzła.</span><span class="sxs-lookup"><span data-stu-id="cece2-222">Expand hello **Azure** node.</span></span>
2. <span data-ttu-id="cece2-223">Rozwiń węzeł hello **aplikacje sieci Web** węzła.</span><span class="sxs-lookup"><span data-stu-id="cece2-223">Expand hello **Web Apps** node.</span></span> 
3. <span data-ttu-id="cece2-224">Kliknij prawym przyciskiem myszy hello żądana aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="cece2-224">Right-click hello desired Web App.</span></span>
4. <span data-ttu-id="cece2-225">Po wyświetleniu menu kontekstowe powitania kliknij **Start**, **zatrzymać**, lub **ponownego uruchomienia**.</span><span class="sxs-lookup"><span data-stu-id="cece2-225">When hello context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="cece2-226">Należy zauważyć, że hello menu opcji kontekstu obsługujący, więc tylko zatrzymać uruchomionej aplikacji sieci web ani uruchomić aplikacji sieci web, która nie jest obecnie uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="cece2-226">Note that hello menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
    ![Zatrzymanie istniejącej aplikacji sieci Web][13]

## <a name="next-steps"></a><span data-ttu-id="cece2-228">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cece2-228">Next Steps</span></span>
<span data-ttu-id="cece2-229">Aby uzyskać więcej informacji na temat hello narzędzi Azure dla języka Java IDEs Zobacz hello następującego łącza:</span><span class="sxs-lookup"><span data-stu-id="cece2-229">For more information about hello Azure Toolkits for Java IDEs, see hello following links:</span></span>

* <span data-ttu-id="cece2-230">[zestawu narzędzi platformy Azure dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="cece2-230">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="cece2-231">[hello Instalowanie zestawu narzędzi platformy Azure dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="cece2-231">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="cece2-232">*Tworzenie aplikacji sieci Web Hello World na platformie Azure w programie Eclipse (w tym artykule)*</span><span class="sxs-lookup"><span data-stu-id="cece2-232">*Create a Hello World Web App for Azure in Eclipse (This Article)*</span></span>
  * <span data-ttu-id="cece2-233">[Nowości w hello zestawu narzędzi platformy Azure dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="cece2-233">[What's New in hello Azure Toolkit for Eclipse]</span></span>
* <span data-ttu-id="cece2-234">[Azure Toolkit for IntelliJ] (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="cece2-234">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="cece2-235">[Instalowanie hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="cece2-235">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="cece2-236">[Tworzenie aplikacji sieci Web Hello World na platformie Azure w IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="cece2-236">[Create a Hello World Web App for Azure in IntelliJ]</span></span>
  * <span data-ttu-id="cece2-237">[Nowości w hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="cece2-237">[What's New in hello Azure Toolkit for IntelliJ]</span></span>

<span data-ttu-id="cece2-238">Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz hello [Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="cece2-238">For more information about using Azure with Java, see hello [Azure Java Developer Center].</span></span>

<span data-ttu-id="cece2-239">Aby uzyskać dodatkowe informacje dotyczące tworzenia aplikacji sieci Web platformy Azure, zobacz hello [Omówienie aplikacji sieci Web].</span><span class="sxs-lookup"><span data-stu-id="cece2-239">For additional information about creating Azure Web Apps, see hello [Web Apps Overview].</span></span>

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[zestawu narzędzi platformy Azure dla programu Eclipse]: ../azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij.md (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)
[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web-eclipse-create-hello-world-web-app.md
[Tworzenie aplikacji sieci Web Hello World na platformie Azure w IntelliJ]: ./app-service-web-intellij-create-hello-world-web-app.md
[hello Instalowanie zestawu narzędzi platformy Azure dla programu Eclipse]: ../azure-toolkit-for-eclipse-installation.md
[Instalowanie hello Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij-installation.md
[Nowości w hello zestawu narzędzi platformy Azure dla programu Eclipse]: ../azure-toolkit-for-eclipse-whats-new.md
[Nowości w hello Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij-whats-new.md

[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Omówienie aplikacji sieci Web]: ./app-service-web-overview.md
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/

<!-- IMG List -->

[01]: ./media/app-service-web-eclipse-create-hello-world-web-app/01-Web-Page.png
[02]: ./media/app-service-web-eclipse-create-hello-world-web-app/02-Dynamic-Web-Project.png
[03]: ./media/app-service-web-eclipse-create-hello-world-web-app/03-Context-Menu.png
[04]: ./media/app-service-web-eclipse-create-hello-world-web-app/04-Log-In-Dialog.png
[05]: ./media/app-service-web-eclipse-create-hello-world-web-app/05-Manage-Subscriptions-Dialog.png
[06]: ./media/app-service-web-eclipse-create-hello-world-web-app/06-Deploy-To-Azure-Web-Container.png
[07a]: ./media/app-service-web-eclipse-create-hello-world-web-app/07a-New-Web-App-Container-Dialog.png
[07b]: ./media/app-service-web-eclipse-create-hello-world-web-app/07b-New-Web-App-Container-Dialog.png
[08]: ./media/app-service-web-eclipse-create-hello-world-web-app/08-New-Resource-Group-Dialog.png
[09]: ./media/app-service-web-eclipse-create-hello-world-web-app/09-New-Service-Plan-Dialog.png
[10]: ./media/app-service-web-eclipse-create-hello-world-web-app/10-Completed-Web-App-Container-Dialog.png
[11]: ./media/app-service-web-eclipse-create-hello-world-web-app/11-Completed-Deploy-Dialog.png
[12]: ./media/app-service-web-eclipse-create-hello-world-web-app/12-Activity-Log-View.png
[13]: ./media/app-service-web-eclipse-create-hello-world-web-app/13-Azure-Explorer-Web-App.png
[14]: ./media/app-service-web-eclipse-create-hello-world-web-app/14-publishDropdownButton.png
[15]: ./media/app-service-web-eclipse-create-hello-world-web-app/15-New-Azure-Web-Container.png
