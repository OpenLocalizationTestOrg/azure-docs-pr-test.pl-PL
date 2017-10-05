---
title: Tworzenie aplikacji sieci web platformy Azure podstawowe w IntelliJ | Dokumentacja firmy Microsoft
description: "Ten samouczek pokazuje, jak używać narzędzi Azure dla IntelliJ do utworzenia Hello World aplikacji sieci Web dla platformy Azure."
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
ms.openlocfilehash: 20b2c3d86f5bde9302647f345aa99b030d78613a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-basic-azure-web-app-in-intellij"></a><span data-ttu-id="d40c8-103">Tworzenie aplikacji sieci web platformy Azure podstawowe w IntelliJ</span><span class="sxs-lookup"><span data-stu-id="d40c8-103">Create a basic Azure web app in IntelliJ</span></span>
<span data-ttu-id="d40c8-104">W tym samouczku przedstawiono sposób tworzenia i wdrażania podstawowej aplikacji Hello World na platformie Azure jako aplikacji sieci Web przy użyciu [narzędzi Azure dla IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="d40c8-104">This tutorial shows how to create and deploy a basic Hello World application to Azure as a Web App by using the [Azure Toolkit for IntelliJ].</span></span> <span data-ttu-id="d40c8-105">Podstawowy przykład JSP jest widoczna dla uproszczenia, ale podobne kroki będzie odpowiednia dla serwlet Java, jakim jest dotyczy wdrożenia usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="d40c8-105">A basic JSP example is shown for simplicity, but similar steps would be appropriate for a Java servlet, as far as Azure deployment is concerned.</span></span>

<span data-ttu-id="d40c8-106">Po ukończeniu tego samouczka, aplikacja będzie wyglądać podobnie do poniższej ilustracji, podczas wyświetlania w przeglądarce sieci web:</span><span class="sxs-lookup"><span data-stu-id="d40c8-106">When you have completed this tutorial, your application will look similar to the following illustration when you view it in a web browser:</span></span>

![Przykładowa strona sieci Web][01]

## <a name="prerequisites"></a><span data-ttu-id="d40c8-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d40c8-108">Prerequisites</span></span>
* <span data-ttu-id="d40c8-109">Java Developer Kit (JDK), v 1,8 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="d40c8-109">A Java Developer Kit (JDK), v 1.8 or later.</span></span>
* <span data-ttu-id="d40c8-110">IntelliJ IDEA Ultimate Edition.</span><span class="sxs-lookup"><span data-stu-id="d40c8-110">IntelliJ IDEA Ultimate Edition.</span></span> <span data-ttu-id="d40c8-111">Ten można pobrać z <https://www.jetbrains.com/idea/download/index.html>.</span><span class="sxs-lookup"><span data-stu-id="d40c8-111">This can be downloaded from <https://www.jetbrains.com/idea/download/index.html>.</span></span>
* <span data-ttu-id="d40c8-112">Dystrybucji serwera sieci web opartych na języku Java lub serwera aplikacji takich jak [Apache Tomcat] lub [Jetty].</span><span class="sxs-lookup"><span data-stu-id="d40c8-112">A distribution of a Java-based web server or application server, such as [Apache Tomcat] or [Jetty].</span></span>
* <span data-ttu-id="d40c8-113">Subskrypcję platformy Azure, która może zostać pobrany z <https://azure.microsoft.com/free/> lub <http://azure.microsoft.com/pricing/purchase-options/>.</span><span class="sxs-lookup"><span data-stu-id="d40c8-113">An Azure subscription, which can be acquired from <https://azure.microsoft.com/free/> or <http://azure.microsoft.com/pricing/purchase-options/>.</span></span>
* <span data-ttu-id="d40c8-114">[narzędzi Azure dla IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="d40c8-114">The [Azure Toolkit for IntelliJ].</span></span> <span data-ttu-id="d40c8-115">Aby uzyskać informacje o instalowaniu zestawu narzędzi platformy Azure, zobacz [Instalowanie zestawu narzędzi platformy Azure dla IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="d40c8-115">For information about installing the Azure Toolkit, see [Installing the Azure Toolkit for IntelliJ].</span></span>

## <a name="to-create-a-hello-world-application"></a><span data-ttu-id="d40c8-116">Do tworzenia aplikacji Hello World</span><span class="sxs-lookup"><span data-stu-id="d40c8-116">To create a Hello World application</span></span>
<span data-ttu-id="d40c8-117">Po pierwsze Zaczniemy tworzenia projektu języka Java.</span><span class="sxs-lookup"><span data-stu-id="d40c8-117">First, we'll start off with creating a Java project.</span></span>

1. <span data-ttu-id="d40c8-118">Uruchom środowisko IntelliJ i kliknij przycisk **pliku** menu, następnie kliknij przycisk **nowy**, a następnie kliknij przycisk **projektu**.</span><span class="sxs-lookup"><span data-stu-id="d40c8-118">Start IntelliJ and click the **File** menu, then click **New**, and then click **Project**.</span></span>
   
    ![Nowy projekt pliku][02]
2. <span data-ttu-id="d40c8-120">W oknie dialogowym Nowy projekt, wybierz **Java**, następnie **aplikacji sieci Web**, a następnie kliknij przycisk **nowy** można dodać SDK projektu.</span><span class="sxs-lookup"><span data-stu-id="d40c8-120">In the New Project dialog box, select **Java**, then **Web Application**, and then click **New** to add a Project SDK.</span></span>
   
    ![Okno dialogowe Nowy projekt][03a]
   
3. <span data-ttu-id="d40c8-122">Wybierz katalog macierzysty dla JDK — okno dialogowe, wybierz folder, w którym zainstalowano JDK użytkownika, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="d40c8-122">In the Select Home Directory for JDK dialog box, select the folder where your JDK is installed, and then click **OK**.</span></span> <span data-ttu-id="d40c8-123">Kliknij przycisk **dalej** w oknie dialogowym Nowy projekt, aby kontynuować.</span><span class="sxs-lookup"><span data-stu-id="d40c8-123">Click **Next** in the New Project dialog box to continue.</span></span>
   
    ![Określ katalog macierzysty JDK][03b]
4. <span data-ttu-id="d40c8-125">Do celów tego samouczka, nazwij projekt **Java sieci Web-App-na-Azure**, a następnie kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="d40c8-125">For purposes of this tutorial, name the project **Java-Web-App-On-Azure**, and then click **Finish**.</span></span>
   
    ![Okno dialogowe Nowy projekt][04]
5. <span data-ttu-id="d40c8-127">W widoku Project Explorer IntelliJ firmy, rozwiń węzeł **Java sieci Web-App-na-Azure**, następnie rozwiń węzeł **web**, a następnie kliknij dwukrotnie **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="d40c8-127">Within IntelliJ's Project Explorer view, expand **Java-Web-App-On-Azure**, then expand **web**, and then double-click **index.jsp**.</span></span>
   
    ![Otwórz indeks strony][05c]
6. <span data-ttu-id="d40c8-129">Po otwarciu pliku index.jsp w IntelliJ, Dodaj tekst do wyświetlenia dynamicznie **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="d40c8-129">When your index.jsp file opens in IntelliJ, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="d40c8-130">wewnątrz istniejącego elementu `<body>`.</span><span class="sxs-lookup"><span data-stu-id="d40c8-130">within the existing `<body>` element.</span></span> <span data-ttu-id="d40c8-131">Zaktualizowana `<body>` zawartości powinien wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="d40c8-131">Your updated `<body>` content should resemble the following example:</span></span>
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
7. <span data-ttu-id="d40c8-132">Zapisz index.jsp.</span><span class="sxs-lookup"><span data-stu-id="d40c8-132">Save index.jsp.</span></span>

## <a name="to-deploy-your-application-to-an-azure-web-app-container"></a><span data-ttu-id="d40c8-133">Aby wdrożyć aplikację na kontenerem aplikacji sieci Web Azure</span><span class="sxs-lookup"><span data-stu-id="d40c8-133">To deploy your application to an Azure Web App Container</span></span>
<span data-ttu-id="d40c8-134">Istnieje kilka metod, które można wdrożyć aplikację sieci web Java na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="d40c8-134">There are several ways by which you can deploy a Java web application to Azure.</span></span> <span data-ttu-id="d40c8-135">Ten samouczek zawiera opis jednego z najprostszą: aplikacja zostanie wdrożona do kontenera aplikacji sieci Web platformy Azure — żadnych typ projektu ani dodatkowe narzędzia są niezbędne.</span><span class="sxs-lookup"><span data-stu-id="d40c8-135">This tutorial describes one of the simplest: your application will be deployed to an Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="d40c8-136">Zestaw JDK i oprogramowania kontenera sieci web będzie zostać dostarczony przez platformę Azure, a więc nie trzeba przekazać własny; potrzebna jest aplikacja sieci Web Java.</span><span class="sxs-lookup"><span data-stu-id="d40c8-136">The JDK and the web container software will be provided for you by Azure, so there is no need to upload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="d40c8-137">W związku z tym proces publikowania aplikacji może zająć sekund, nie minut.</span><span class="sxs-lookup"><span data-stu-id="d40c8-137">As a result, the publishing process for your application will take seconds, not minutes.</span></span>

<span data-ttu-id="d40c8-138">Przed opublikowaniem aplikacji, należy najpierw skonfigurować ustawienia modułu.</span><span class="sxs-lookup"><span data-stu-id="d40c8-138">Before you publish your application, you first need to configure your module settings.</span></span> <span data-ttu-id="d40c8-139">Aby to zrobić, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="d40c8-139">To do so, use the following steps:</span></span>

1. <span data-ttu-id="d40c8-140">W obszarze Eksplorator projektów w IntelliJ, kliknij prawym przyciskiem myszy **Java sieci Web-App-na-Azure** projektu.</span><span class="sxs-lookup"><span data-stu-id="d40c8-140">In IntelliJ's Project Explorer, right-click the **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="d40c8-141">W menu kontekstowym kliknij **Otwórz ustawienia modułu**.</span><span class="sxs-lookup"><span data-stu-id="d40c8-141">When the context menu appears, click **Open Module Settings**.</span></span>

    ![Otwórz ustawienia modułu][05a]
2. <span data-ttu-id="d40c8-143">Kiedy wyświetli się okno dialogowe struktury projektu:</span><span class="sxs-lookup"><span data-stu-id="d40c8-143">When the Project Structure dialog box appears:</span></span>

   <span data-ttu-id="d40c8-144">a.</span><span class="sxs-lookup"><span data-stu-id="d40c8-144">a.</span></span> <span data-ttu-id="d40c8-145">Kliknij przycisk **artefakty** na liście **ustawienia projektu**.</span><span class="sxs-lookup"><span data-stu-id="d40c8-145">Click **Artifacts** in the list of **Project Settings**.</span></span>
   <span data-ttu-id="d40c8-146">b.</span><span class="sxs-lookup"><span data-stu-id="d40c8-146">b.</span></span> <span data-ttu-id="d40c8-147">Zmień nazwę artefaktów w **nazwa** , dzięki czemu nie zawiera spacji ani znaków specjalnych; jest to konieczne, ponieważ nazwa będzie używana w jednolity identyfikator zasobów (URI).</span><span class="sxs-lookup"><span data-stu-id="d40c8-147">Change the artifact name in the **Name** box so that it doesn't contain whitespace or special characters; this is necessary since the name will be used in the Uniform Resource Identifier (URI).</span></span>
   <span data-ttu-id="d40c8-148">c.</span><span class="sxs-lookup"><span data-stu-id="d40c8-148">c.</span></span> <span data-ttu-id="d40c8-149">Zmień **typu** do **aplikacji sieci Web: archiwum**.</span><span class="sxs-lookup"><span data-stu-id="d40c8-149">Change the **Type** to **Web Application: Archive**.</span></span>
   <span data-ttu-id="d40c8-150">d.</span><span class="sxs-lookup"><span data-stu-id="d40c8-150">d.</span></span> <span data-ttu-id="d40c8-151">Kliknij przycisk **OK** aby zamknąć okno dialogowe struktury projektu.</span><span class="sxs-lookup"><span data-stu-id="d40c8-151">Click **OK** to close the Project Structure dialog box.</span></span>

    ![Otwórz ustawienia modułu][05b]

<span data-ttu-id="d40c8-153">Po skonfigurowaniu ustawień modułu można opublikować aplikacji na platformie Azure przy użyciu następujących kroków:</span><span class="sxs-lookup"><span data-stu-id="d40c8-153">When you have configured your module settings, you can publish your application to Azure by using the following steps:</span></span>

1. <span data-ttu-id="d40c8-154">W obszarze Eksplorator projektów w IntelliJ, kliknij prawym przyciskiem myszy **Java sieci Web-App-na-Azure** projektu.</span><span class="sxs-lookup"><span data-stu-id="d40c8-154">In IntelliJ's Project Explorer, right-click the **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="d40c8-155">Po wyświetleniu menu kontekstowego wybierz **Azure**, a następnie kliknij przycisk **Publikuj jako aplikacji sieci Web platformy Azure...**</span><span class="sxs-lookup"><span data-stu-id="d40c8-155">When the context menu appears, select **Azure**, and then click **Publish as Azure Web App...**</span></span>
   
    ![Menu kontekstowe publikowania na platformie Azure][06]
2. <span data-ttu-id="d40c8-157">Jeśli dany komputer nie ma już podpisany na platformie Azure z IntelliJ, pojawi się monit do logowania się do konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d40c8-157">If you have not already signed into Azure from IntelliJ, you will be prompted to sign into your Azure account.</span></span> <span data-ttu-id="d40c8-158">(Jeśli masz wiele kont platformy Azure, niektóre monity podczas logowania w procesie mogą być wyświetlane więcej niż raz, nawet wtedy, gdy pojawią się one być takie same.</span><span class="sxs-lookup"><span data-stu-id="d40c8-158">(If you have multiple Azure accounts, some of the prompts during the sign in process may be shown more than once, even if they appear to be the same.</span></span> <span data-ttu-id="d40c8-159">W takim przypadku, postępuj zgodnie z logowania w instrukcjach).</span><span class="sxs-lookup"><span data-stu-id="d40c8-159">When this happens, continue to follow the sign in instructions.)</span></span>
   
    ![Azure dziennika w oknie dialogowym][07]
3. <span data-ttu-id="d40c8-161">Po pomyślnym zarejestrowaniu do konta platformy Azure, **Zarządzaj subskrypcjami** dialogowym zostanie wyświetlona lista subskrypcji, które są skojarzone z poświadczeniami użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d40c8-161">After you have successfully signed into your Azure account, the **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="d40c8-162">(Jeśli istnieje wiele subskrypcji wymieniono i chcesz używać konkretnego podzestawu z nich, może opcjonalnie Usuń zaznaczenie subskrypcje, do których nie chcesz używać.) Po zakończeniu wybierania subskrypcji, kliknij przycisk **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="d40c8-162">(If there are multiple subscriptions listed and you want to work with only a specific subset of them, you may optionally uncheck the subscriptions you don't want to use.) When you have selected your subscriptions, click **Close**.</span></span>
   
    ![Zarządzanie subskrypcjami][08]
4. <span data-ttu-id="d40c8-164">Gdy **Wdróż do kontenera aplikacji sieci Web Azure** zostanie wyświetlone okno dialogowe będzie ono żadnych kontenerów aplikacji sieci Web, które wcześniej zostały utworzone; Jeśli nie utworzono żadnych kontenerów, lista jest pusta.</span><span class="sxs-lookup"><span data-stu-id="d40c8-164">When the **Deploy to Azure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, the list will be empty.</span></span>
   
    ![Kontenery aplikacji][09]
5. <span data-ttu-id="d40c8-166">Kontenera aplikacji sieci Web Azure przed nie zostały utworzone lub jeśli chcesz opublikować aplikację do nowego kontenera, wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="d40c8-166">If you have not created an Azure Web App Container before, or if you would like to publish your application to a new container, use the following steps.</span></span> <span data-ttu-id="d40c8-167">W przeciwnym razie wybierz kontener istniejących aplikacji sieci Web i przejdź do kroku 6 poniżej.</span><span class="sxs-lookup"><span data-stu-id="d40c8-167">Otherwise, select an existing Web App Container and skip to step 6 below.</span></span>
   
   1. <span data-ttu-id="d40c8-168">Kliknij przycisk**+**</span><span class="sxs-lookup"><span data-stu-id="d40c8-168">Click **+**</span></span>
      
       ![Dodawanie aplikacji kontenera][10]
   2. <span data-ttu-id="d40c8-170">**Nowy kontener aplikacji sieci Web** można wyświetlić okna dialogowego, które będzie służyć do następnych krokach.</span><span class="sxs-lookup"><span data-stu-id="d40c8-170">The **New Web App Container** dialog box will be displayed, which will be used for the next several steps.</span></span>
      
       ![Nowy kontener aplikacji][11a]
   3. <span data-ttu-id="d40c8-172">Wprowadź **Etykieta DNS** dla kontener aplikacji sieci Web; to będzie stanowić liścia Etykieta DNS adresu URL hosta aplikacji sieci web na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="d40c8-172">Enter a **DNS Label** for your Web App Container; this will form the leaf DNS label of the host URL for your web application in Azure.</span></span> <span data-ttu-id="d40c8-173">Należy pamiętać, że nazwa musi być dostępny i jest zgodna z wymaganiami nazewnictwa aplikację sieci Web Azure.</span><span class="sxs-lookup"><span data-stu-id="d40c8-173">Note that the name must be available and conform to Azure Web App naming requirements.</span></span>
   4. <span data-ttu-id="d40c8-174">W **kontener sieci Web** menu rozwijanego wybierz odpowiedniego oprogramowania dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d40c8-174">In the **Web Container** drop-down menu, select the appropriate software for your application.</span></span>
      
       <span data-ttu-id="d40c8-175">Obecnie można wybrać z Tomcat 8 Tomcat 7 lub Jetty 9.</span><span class="sxs-lookup"><span data-stu-id="d40c8-175">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="d40c8-176">Ostatnie dystrybucji wybranego oprogramowania, które będą udostępniane przez usługi Azure, a zostanie uruchomiony na ostatnie dystrybucji 8 JDK utworzone przez firmę Oracle i dostarczany przez platformę Azure.</span><span class="sxs-lookup"><span data-stu-id="d40c8-176">A recent distribution of the selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span></span>
   5. <span data-ttu-id="d40c8-177">W **subskrypcji** menu rozwijanego Wybierz subskrypcję, którego chcesz użyć dla tego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="d40c8-177">In the **Subscription** drop-down menu, select the subscription you want to use for this deployment.</span></span>
   6. <span data-ttu-id="d40c8-178">W **grupy zasobów** menu rozwijanego wybierz grupę zasobów, z którą chcesz skojarzyć aplikację sieci Web.</span><span class="sxs-lookup"><span data-stu-id="d40c8-178">In the **Resource Group** drop-down menu, select the Resource Group with which you want to associate your Web App.</span></span> <span data-ttu-id="d40c8-179">(Grup zasobów platformy azure umożliwiają grupowania powiązanych zasobów, tak aby na przykład je usunąć ze sobą.)</span><span class="sxs-lookup"><span data-stu-id="d40c8-179">(Azure Resource Groups allow you to group related resources together so that, for example, they can be deleted together.)</span></span>
      
       <span data-ttu-id="d40c8-180">Wybierz istniejącą grupę zasobów (jeśli) i Pomiń krok g poniżej lub wykonaj następujące kroki, aby utworzyć nową grupę zasobów:</span><span class="sxs-lookup"><span data-stu-id="d40c8-180">You can select an existing Resource Group (if you have any) and skip to step g below, or use the following steps to create a new Resource Group:</span></span>
      
      * <span data-ttu-id="d40c8-181">Wybierz  **&lt; &lt; Utwórz nową grupę zasobów &gt; &gt;**  w **grupy zasobów** menu rozwijanego.</span><span class="sxs-lookup"><span data-stu-id="d40c8-181">Select **&lt;&lt; Create new Resource Group &gt;&gt;** in the **Resource Group** drop-down menu.</span></span>
      * <span data-ttu-id="d40c8-182">**Nową grupę zasobów** wyświetli się okno dialogowe:</span><span class="sxs-lookup"><span data-stu-id="d40c8-182">The **New Resource Group** dialog box will be displayed:</span></span>
        
          ![Nową grupę zasobów][12]
      * <span data-ttu-id="d40c8-184">W **nazwa** pole tekstowe, określ nazwę nowej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="d40c8-184">In the the **Name** textbox, specify a name for your new Resource Group.</span></span>
      * <span data-ttu-id="d40c8-185">W **Region** menu rozwijanego wybierz lokalizację dla grupy zasobów Centrum danych Azure.</span><span class="sxs-lookup"><span data-stu-id="d40c8-185">In the the **Region** drop-down menu, select the appropriate Azure data center location for your Resource Group.</span></span>
      * <span data-ttu-id="d40c8-186">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="d40c8-186">Click **OK**.</span></span>
   7. <span data-ttu-id="d40c8-187">**Planu usługi App Service** menu rozwijanego listy planów usługi aplikacji, które są skojarzone z wybranej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="d40c8-187">The **App Service Plan** drop-down menu lists the app service plans that are associated with the Resource Group that you selected.</span></span> <span data-ttu-id="d40c8-188">(Plan usługi App Service określa informacje takie jak lokalizacja aplikacji sieci Web, warstwy cenowej i rozmiar wystąpienia obliczeniowe.</span><span class="sxs-lookup"><span data-stu-id="d40c8-188">(An App Service Plan specifies information such as the location of your Web App, the pricing tier and the compute instance size.</span></span> <span data-ttu-id="d40c8-189">Jeden Plan usługi App Service może służyć do wielu aplikacji sieci Web, dlatego jest obsługiwana oddzielnie od określonego wdrożenia aplikacji sieci Web.)</span><span class="sxs-lookup"><span data-stu-id="d40c8-189">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
       <span data-ttu-id="d40c8-190">Wybierz istniejący Plan usługi App Service (jeśli) i Pomiń krok h poniżej lub wykonaj następujące kroki, aby utworzyć nowy Plan usługi App Service:</span><span class="sxs-lookup"><span data-stu-id="d40c8-190">You can select an existing App Service Plan (if you have any) and skip to step h below, or use the following steps to create a new App Service Plan:</span></span>
      
      * <span data-ttu-id="d40c8-191">Wybierz  **&lt; &lt; Utwórz nowy Plan usługi App Service &gt; &gt;**  w **planu usługi App Service** menu rozwijanego.</span><span class="sxs-lookup"><span data-stu-id="d40c8-191">Select **&lt;&lt; Create new App Service Plan &gt;&gt;** in the **App Service Plan** drop-down menu.</span></span>
      * <span data-ttu-id="d40c8-192">**Nowy Plan usługi App Service** wyświetli się okno dialogowe:</span><span class="sxs-lookup"><span data-stu-id="d40c8-192">The **New App Service Plan** dialog box will be displayed:</span></span>
        
          ![Nowy Plan usługi aplikacji][13]
      * <span data-ttu-id="d40c8-194">W **nazwa** pole tekstowe, określ nazwę planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d40c8-194">In the the **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="d40c8-195">W **lokalizacji** menu rozwijanego wybierz lokalizację dla planu Centrum odpowiednich danych Azure.</span><span class="sxs-lookup"><span data-stu-id="d40c8-195">In the the **Location** drop-down menu, select the appropriate Azure data center location for the plan.</span></span>
      * <span data-ttu-id="d40c8-196">W **warstwy cenowej** menu rozwijanego wybierz odpowiednie ceny dla planu.</span><span class="sxs-lookup"><span data-stu-id="d40c8-196">In the the **Pricing Tier** drop-down menu, select the appropriate pricing for the plan.</span></span> <span data-ttu-id="d40c8-197">Podczas testowania, możesz wybrać **wolne**.</span><span class="sxs-lookup"><span data-stu-id="d40c8-197">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="d40c8-198">W **rozmiar wystąpienia** menu rozwijanego, wybierz odpowiednie wystąpienie rozmiaru planu.</span><span class="sxs-lookup"><span data-stu-id="d40c8-198">In the the **Instance Size** drop-down menu, select the appropriate instance size for the plan.</span></span> <span data-ttu-id="d40c8-199">Podczas testowania, możesz wybrać **małych**.</span><span class="sxs-lookup"><span data-stu-id="d40c8-199">For testing purposes you can choose **Small**.</span></span>
      * <span data-ttu-id="d40c8-200">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="d40c8-200">Click **OK**.</span></span>
   8. <span data-ttu-id="d40c8-201">(Opcjonalnie) Domyślnie ostatnie dystrybucji Java 8 zostanie automatycznie wdrożone jako sieci maszyny wirtualnej Java na platformie Azure do kontener aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="d40c8-201">(Optional) By default, a recent distribution of Java 8 will be automatically deployed as your JVM by Azure to your web app container.</span></span> <span data-ttu-id="d40c8-202">Można jednak wybrać inną wersję i dystrybucji maszyna JVM.</span><span class="sxs-lookup"><span data-stu-id="d40c8-202">However, you can select a different version and distribution of the JVM.</span></span> <span data-ttu-id="d40c8-203">Aby to zrobić, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="d40c8-203">To do so, use the following steps:</span></span>
      
      * <span data-ttu-id="d40c8-204">Kliknij przycisk **JDK** karcie **nowy kontener aplikacji sieci Web** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="d40c8-204">Click the **JDK** tab in the **New Web App Container** dialog box.</span></span>
      * <span data-ttu-id="d40c8-205">Można wybrać jedną z następujących opcji:</span><span class="sxs-lookup"><span data-stu-id="d40c8-205">You can choose from one of the following options:</span></span>
        
        * <span data-ttu-id="d40c8-206">Wdróż domyślne JDK, który jest oferowany na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="d40c8-206">Deploy the default JDK which is offered by Azure</span></span>
        * <span data-ttu-id="d40c8-207">Wdrażanie 3 strona JDK z listy rozwijanej JDKs dodatkowe, które są dostępne w systemie Azure</span><span class="sxs-lookup"><span data-stu-id="d40c8-207">Deploy a 3rd party JDK from a drop-down list of additional JDKs which are available on Azure</span></span>
        * <span data-ttu-id="d40c8-208">Wdrażanie niestandardowych JDK, które muszą być spakowane jako plik ZIP i albo publicznie dostępnych lub na koncie magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="d40c8-208">Deploy a custom JDK, which must be packaged as a ZIP file and either publicly available or in your Azure storage account</span></span>
        
        ![Nowa karta JDK kontenera aplikacji][11b]
   9. <span data-ttu-id="d40c8-210">Po zakończeniu wszystkich kroków opisanych powyżej, okno dialogowe nowy kontener aplikacji sieci Web powinien wyglądać poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="d40c8-210">Once you have completed all of the above steps, the New Web App Container dialog box should resemble the following illustration:</span></span>
      
       ![Nowy kontener aplikacji][14]
   10. <span data-ttu-id="d40c8-212">Kliknij przycisk **OK** aby zakończyć tworzenie użytkownika nowy kontener aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="d40c8-212">Click **OK** to complete the creation of your new Web App container.</span></span>
       
        <span data-ttu-id="d40c8-213">Poczekaj kilka sekund na liście kontenery aplikacji sieci Web należy odświeżyć, a kontener aplikacji sieci web nowo utworzony powinny teraz być zaznaczone na liście.</span><span class="sxs-lookup"><span data-stu-id="d40c8-213">Wait a few seconds for the list of the Web App containers to be refreshed, and your newly-created web app container should now be selected in the list.</span></span>
6. <span data-ttu-id="d40c8-214">Teraz można przystąpić do ukończenia pierwszego wdrożenia aplikacji sieci Web na platformie Azure; Kliknij przycisk **OK** do wdrożenia aplikacji do wybranego kontenera aplikacji sieci Web w języku Java.</span><span class="sxs-lookup"><span data-stu-id="d40c8-214">You are now ready to complete the initial deployment of your Web App to Azure; click **OK** to deploy your Java application to the selected Web App container.</span></span> <span data-ttu-id="d40c8-215">Domyślnie aplikacja zostanie wdrożona jako podkatalog serwera aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d40c8-215">By default, your application will be deployed as a subdirectory of the application server.</span></span> <span data-ttu-id="d40c8-216">Sprawdź, czy ma to być wdrożony jako aplikacja główna **Wdróż głównym** wyboru przed kliknięciem przycisku **OK**.</span><span class="sxs-lookup"><span data-stu-id="d40c8-216">If you want it to be deployed as the root application, check the **Deploy to root** checkbox before clicking **OK**.</span></span>
   
    ![Wdrażanie na platformie Azure][15]
7. <span data-ttu-id="d40c8-218">Następnie zostanie wyświetlony **dziennika aktywności platformy Azure** widoku, który wskazuje stan wdrożenia aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="d40c8-218">Next, you should see the **Azure Activity Log** view, which will indicate the deployment status of your Web App.</span></span>
   
    ![Wskaźnik postępu][16]
   
    <span data-ttu-id="d40c8-220">Proces wdrażania aplikacji sieci Web na platformie Azure powinien zająć tylko kilka sekund.</span><span class="sxs-lookup"><span data-stu-id="d40c8-220">The process of deploying your Web App to Azure should take only a few seconds to complete.</span></span> <span data-ttu-id="d40c8-221">Jeśli możesz już aplikacji, zobaczysz łącze o nazwie **opublikowano** w **stan** kolumny.</span><span class="sxs-lookup"><span data-stu-id="d40c8-221">When your application ready, you will see a link named **Published** in the **Status** column.</span></span> <span data-ttu-id="d40c8-222">Po kliknięciu łącza spowoduje przejście do strony głównej wdrożonej aplikacji sieci Web lub aby przejść do aplikacji sieci web służy kroki opisane w poniższej sekcji.</span><span class="sxs-lookup"><span data-stu-id="d40c8-222">When you click the link, it will take you to your deployed Web App's home page, or you can use the steps in the following section to browse to your web app.</span></span>

## <a name="browsing-to-your-web-app-on-azure"></a><span data-ttu-id="d40c8-223">Przeglądanie do aplikacji sieci Web na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="d40c8-223">Browsing to your Web App on Azure</span></span>
<span data-ttu-id="d40c8-224">Aby przejść do aplikacji sieci Web na platformie Azure, można użyć **Eksploratora Azure** widoku.</span><span class="sxs-lookup"><span data-stu-id="d40c8-224">To browse to your Web App on Azure, you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="d40c8-225">Jeśli **Eksploratora Azure** widoku nie jest jeszcze otwarty, otwórz go, klikając następnie **widoku** menu w IntelliJ, następnie kliknij przycisk **okna narzędzi**, a następnie kliknij przycisk  **Eksplorator usługi**.</span><span class="sxs-lookup"><span data-stu-id="d40c8-225">If the **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="d40c8-226">Jeśli dany system nie zostały wcześniej zarejestrowane, monit podczas wykonywania.</span><span class="sxs-lookup"><span data-stu-id="d40c8-226">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="d40c8-227">Gdy **Eksploratora Azure** zostanie wyświetlony widok, użyj wykonaj następujące kroki, aby przejść do aplikacji sieci Web:</span><span class="sxs-lookup"><span data-stu-id="d40c8-227">When the **Azure Explorer** view is displayed, use follow these steps to browse to your Web App:</span></span> 

1. <span data-ttu-id="d40c8-228">Rozwiń węzeł **Azure** węzła.</span><span class="sxs-lookup"><span data-stu-id="d40c8-228">Expand the **Azure** node.</span></span>
2. <span data-ttu-id="d40c8-229">Rozwiń węzeł **aplikacje sieci Web** węzła.</span><span class="sxs-lookup"><span data-stu-id="d40c8-229">Expand the **Web Apps** node.</span></span> 
3. <span data-ttu-id="d40c8-230">Kliknij prawym przyciskiem myszy odpowiednią aplikację sieci Web.</span><span class="sxs-lookup"><span data-stu-id="d40c8-230">Right-click the desired Web App.</span></span>
4. <span data-ttu-id="d40c8-231">W menu kontekstowym kliknij **Otwórz w przeglądarce**.</span><span class="sxs-lookup"><span data-stu-id="d40c8-231">When the context menu appears, click **Open in Browser**.</span></span>
   
    ![Przeglądanie aplikacji sieci Web][17]

## <a name="updating-your-web-app"></a><span data-ttu-id="d40c8-233">Aktualizowanie aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="d40c8-233">Updating your web app</span></span>
<span data-ttu-id="d40c8-234">Aktualizowanie istniejącej uruchamiania aplikacji sieci Web platformy Azure jest procesem szybkie i łatwe i dostępne są dwie opcje aktualizacji:</span><span class="sxs-lookup"><span data-stu-id="d40c8-234">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="d40c8-235">Można aktualizować wdrażania istniejącej aplikacji sieci Web Java.</span><span class="sxs-lookup"><span data-stu-id="d40c8-235">You can update the deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="d40c8-236">Możesz opublikować aplikację Java dodatkowe do tego samego kontenera aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="d40c8-236">You can publish an additional Java application to the same Web App Container.</span></span>

<span data-ttu-id="d40c8-237">W obu przypadkach proces jest identyczne i zajmuje tylko kilka sekund:</span><span class="sxs-lookup"><span data-stu-id="d40c8-237">In either case, the process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="d40c8-238">W obszarze Eksplorator projektów IntelliJ kliknij prawym przyciskiem myszy aplikację Java, który chcesz zaktualizować, lub Dodaj do istniejącego kontenera aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="d40c8-238">In the IntelliJ project explorer, right-click the Java application you want to update or add to an existing Web App Container.</span></span>
2. <span data-ttu-id="d40c8-239">Po wyświetleniu menu kontekstowego wybierz **Azure** , a następnie **Publikuj jako aplikacji sieci Web platformy Azure...**</span><span class="sxs-lookup"><span data-stu-id="d40c8-239">When the context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>
3. <span data-ttu-id="d40c8-240">Ponieważ użytkownik ma już zalogowany wcześniej, zostanie wyświetlona lista sieci kontenerów istniejących aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="d40c8-240">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="d40c8-241">Wybierz ten, który chcesz opublikować lub ponownie opublikować aplikację Java i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="d40c8-241">Select the one you want to publish or re-publish your Java application to and click **OK**.</span></span>

<span data-ttu-id="d40c8-242">Później, gdzie po kilku sekundach **dziennika aktywności platformy Azure** widoku wyświetli zaktualizowane wdrożenia jako **opublikowano** i będzie mógł zweryfikować zaktualizowane aplikacji w przeglądarce sieci web.</span><span class="sxs-lookup"><span data-stu-id="d40c8-242">A few seconds later, the **Azure Activity Log** view will show your updated deployment as **Published** and you will be able to verify your updated application in a web browser.</span></span>

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="d40c8-243">Uruchamianie, zatrzymywanie lub ponowne uruchamianie istniejących aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="d40c8-243">Starting, stopping, or restarting an existing web app</span></span>
<span data-ttu-id="d40c8-244">Aby rozpocząć lub zatrzymać istniejącego kontenera aplikacji sieci Web platformy Azure (w tym wszystkich wdrożonych aplikacji Java w nim), można użyć **Eksploratora Azure** widoku.</span><span class="sxs-lookup"><span data-stu-id="d40c8-244">To start or stop an existing Azure Web App container, (including all the deployed Java applications in it), you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="d40c8-245">Jeśli **Eksploratora Azure** widoku nie jest jeszcze otwarty, otwórz go, klikając następnie **widoku** menu w IntelliJ, następnie kliknij przycisk **okna narzędzi**, a następnie kliknij przycisk  **Eksplorator usługi**.</span><span class="sxs-lookup"><span data-stu-id="d40c8-245">If the **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="d40c8-246">Jeśli dany system nie zostały wcześniej zarejestrowane, monit podczas wykonywania.</span><span class="sxs-lookup"><span data-stu-id="d40c8-246">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="d40c8-247">Gdy **Eksploratora Azure** zostanie wyświetlony widok, użyj wykonaj następujące kroki, aby uruchomić lub zatrzymać aplikacji sieci Web:</span><span class="sxs-lookup"><span data-stu-id="d40c8-247">When the **Azure Explorer** view is displayed, use follow these steps to start or stop your Web App:</span></span> 

1. <span data-ttu-id="d40c8-248">Rozwiń węzeł **Azure** węzła.</span><span class="sxs-lookup"><span data-stu-id="d40c8-248">Expand the **Azure** node.</span></span>
2. <span data-ttu-id="d40c8-249">Rozwiń węzeł **aplikacje sieci Web** węzła.</span><span class="sxs-lookup"><span data-stu-id="d40c8-249">Expand the **Web Apps** node.</span></span> 
3. <span data-ttu-id="d40c8-250">Kliknij prawym przyciskiem myszy odpowiednią aplikację sieci Web.</span><span class="sxs-lookup"><span data-stu-id="d40c8-250">Right-click the desired Web App.</span></span>
4. <span data-ttu-id="d40c8-251">W menu kontekstowym kliknij **Start**, **zatrzymać**, lub **ponownego uruchomienia**.</span><span class="sxs-lookup"><span data-stu-id="d40c8-251">When the context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="d40c8-252">Należy zauważyć, że opcji menu kontekstowe obsługujący, więc tylko zatrzymać uruchomionej aplikacji sieci web ani uruchomić aplikacji sieci web, która nie jest obecnie uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="d40c8-252">Note that the menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
    ![Zatrzymać aplikacji sieci Web][18]

## <a name="next-steps"></a><span data-ttu-id="d40c8-254">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d40c8-254">Next Steps</span></span>
<span data-ttu-id="d40c8-255">Aby uzyskać więcej informacji o zestawach narzędzi platformy Azure dla środowisk IDE języka Java, skorzystaj z następujących linków:</span><span class="sxs-lookup"><span data-stu-id="d40c8-255">For more information about the Azure Toolkits for Java IDEs, see the following links:</span></span>

* <span data-ttu-id="d40c8-256">[Azure zestawu narzędzi dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="d40c8-256">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="d40c8-257">[Installing the Azure Toolkit for Eclipse] (Instalowanie zestawu narzędzi platformy Azure dla środowiska Eclipse)</span><span class="sxs-lookup"><span data-stu-id="d40c8-257">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="d40c8-258">[Tworzenie aplikacji sieci Web Hello World na platformie Azure w programie Eclipse]</span><span class="sxs-lookup"><span data-stu-id="d40c8-258">[Create a Hello World Web App for Azure in Eclipse]</span></span>
  * <span data-ttu-id="d40c8-259">[What's New in the Azure Toolkit for Eclipse] (Co nowego w zestawie narzędzi platformy Azure dla środowiska Eclipse)</span><span class="sxs-lookup"><span data-stu-id="d40c8-259">[What's New in the Azure Toolkit for Eclipse]</span></span>
* <span data-ttu-id="d40c8-260">[narzędzi Azure dla IntelliJ] (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="d40c8-260">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="d40c8-261">[Instalowanie zestawu narzędzi platformy Azure dla IntelliJ] (Instalowanie zestawu narzędzi platformy Azure dla środowiska IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="d40c8-261">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="d40c8-262">*Tworzenie aplikacji sieci Web Hello World na platformie Azure w IntelliJ (w tym artykule)*</span><span class="sxs-lookup"><span data-stu-id="d40c8-262">*Create a Hello World Web App for Azure in IntelliJ (This Article)*</span></span>
  * <span data-ttu-id="d40c8-263">[What's New in the Azure Toolkit for IntelliJ] (Co nowego w zestawie narzędzi platformy Azure dla środowiska IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="d40c8-263">[What's New in the Azure Toolkit for IntelliJ]</span></span>

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="d40c8-264">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="d40c8-264">See Also</span></span>
<span data-ttu-id="d40c8-265">Aby uzyskać więcej informacji o używaniu platformy Azure z językiem Java, zobacz [Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="d40c8-265">For more information about using Azure with Java, see the [Azure Java Developer Center].</span></span>

<span data-ttu-id="d40c8-266">Aby uzyskać dodatkowe informacje dotyczące tworzenia aplikacji sieci Web platformy Azure, zobacz [Omówienie aplikacji sieci Web].</span><span class="sxs-lookup"><span data-stu-id="d40c8-266">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[Azure zestawu narzędzi dla programu Eclipse]: ../azure-toolkit-for-eclipse.md
[narzędzi Azure dla IntelliJ]: ../azure-toolkit-for-intellij.md (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)
[Tworzenie aplikacji sieci Web Hello World na platformie Azure w programie Eclipse]: ./app-service-web-eclipse-create-hello-world-web-app.md
[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web-intellij-create-hello-world-web-app.md
[Installing the Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse-installation.md (Instalowanie zestawu narzędzi platformy Azure dla środowiska Eclipse)
[Instalowanie zestawu narzędzi platformy Azure dla IntelliJ]: ../azure-toolkit-for-intellij-installation.md (Instalowanie zestawu narzędzi platformy Azure dla środowiska IntelliJ)
[What's New in the Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse-whats-new.md (Co nowego w zestawie narzędzi platformy Azure dla środowiska Eclipse)
[What's New in the Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij-whats-new.md (Co nowego w zestawie narzędzi platformy Azure dla środowiska IntelliJ)

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
