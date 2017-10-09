---
title: "Dodatek dla programu Eclipse sieci szkieletowej usług aaaAzure | Dokumentacja firmy Microsoft"
description: "Rozpoczynanie pracy z hello wtyczki sieci szkieletowej usług dla programu Eclipse."
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: bf84458f-4b87-4de1-9844-19909e368deb
ms.service: service-fabric
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/21/2016
ms.author: saysa
ms.openlocfilehash: 4ba5a28a6282387249a2bd4e62314e891ff04162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-plug-in-for-eclipse-java-application-development"></a><span data-ttu-id="cfde7-103">Wtyczka usługi Service Fabric na potrzeby tworzenia aplikacji Java w środowisku Eclipse</span><span class="sxs-lookup"><span data-stu-id="cfde7-103">Service Fabric plug-in for Eclipse Java application development</span></span>
<span data-ttu-id="cfde7-104">Środowisko Eclipse jest jednym z hello najczęściej używane zintegrowane środowisk deweloperskich (IDE) dla deweloperów języka Java.</span><span class="sxs-lookup"><span data-stu-id="cfde7-104">Eclipse is one of hello most widely used integrated development environments (IDEs) for Java developers.</span></span> <span data-ttu-id="cfde7-105">W tym artykule opisano sposób tooset się toowork środowisko rozwoju Eclipse, tak z sieci szkieletowej usług Azure.</span><span class="sxs-lookup"><span data-stu-id="cfde7-105">In this article, we describe how tooset up your Eclipse development environment toowork with Azure Service Fabric.</span></span> <span data-ttu-id="cfde7-106">Dowiedz się, jak utworzyć aplikację sieci szkieletowej usług hello tooinstall wtyczki sieci szkieletowej usług i wdrażanie z sieci szkieletowej usług aplikacji tooa lokalnego lub zdalnego klastra sieci szkieletowej usług w środowisku Eclipse Neon.</span><span class="sxs-lookup"><span data-stu-id="cfde7-106">Learn how tooinstall hello Service Fabric plug-in, create a Service Fabric application, and deploy your Service Fabric application tooa local or remote Service Fabric cluster in Eclipse Neon.</span></span>

## <a name="install-or-update-hello-service-fabric-plug-in-in-eclipse-neon"></a><span data-ttu-id="cfde7-107">Zainstaluj lub zaktualizuj hello wtyczki w środowisku Eclipse Neon sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="cfde7-107">Install or update hello Service Fabric plug-in in Eclipse Neon</span></span>
<span data-ttu-id="cfde7-108">W środowisku Eclipse można zainstalować wtyczkę usługi Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="cfde7-108">You can install a Service Fabric plug-in in Eclipse.</span></span> <span data-ttu-id="cfde7-109">Wtyczka Hello może ułatwić proces hello tworzenie i wdrażanie usług Java.</span><span class="sxs-lookup"><span data-stu-id="cfde7-109">hello plug-in can help simplify hello process of building and deploying Java services.</span></span>

1.  <span data-ttu-id="cfde7-110">Upewnij się, czy masz najnowszą wersję programu Eclipse Neon hello i hello najnowszą wersję Buildship zainstalowany (1.0.17 lub nowszy):</span><span class="sxs-lookup"><span data-stu-id="cfde7-110">Ensure that you have hello latest version of Eclipse Neon and hello latest version of Buildship (1.0.17 or a later version) installed:</span></span>
    -   <span data-ttu-id="cfde7-111">toocheck hello wersje zainstalowanych składników w Eclipse Neon Przejdź zbyt**pomocy** > **szczegółowe informacje dotyczące instalacji**.</span><span class="sxs-lookup"><span data-stu-id="cfde7-111">toocheck hello versions of installed components, in Eclipse Neon, go too**Help** > **Installation Details**.</span></span>
    -   <span data-ttu-id="cfde7-112">Zobacz tooupdate Buildship, [Eclipse Buildship: Eclipse wtyczek dla narzędzia Gradle][buildship-update].</span><span class="sxs-lookup"><span data-stu-id="cfde7-112">tooupdate Buildship, see [Eclipse Buildship: Eclipse Plug-ins for Gradle][buildship-update].</span></span>
    -   <span data-ttu-id="cfde7-113">toocheck dla i instalacja aktualizacji dla programu Eclipse Neon, go za**pomocy** > **Sprawdź aktualizacje**.</span><span class="sxs-lookup"><span data-stu-id="cfde7-113">toocheck for and install updates for Eclipse Neon, go too**Help** > **Check for Updates**.</span></span>

2.  <span data-ttu-id="cfde7-114">tooinstall hello usługi sieć szkieletowa wtyczki w Eclipse Neon Przejdź zbyt**pomocy** > **zainstalować nowe oprogramowanie**.</span><span class="sxs-lookup"><span data-stu-id="cfde7-114">tooinstall hello Service Fabric plug-in, in Eclipse Neon, go too**Help** > **Install New Software**.</span></span>
  1.    <span data-ttu-id="cfde7-115">W hello **pracować z** wprowadź **http://dl.microsoft.com/eclipse**.</span><span class="sxs-lookup"><span data-stu-id="cfde7-115">In hello **Work with** box, enter **http://dl.microsoft.com/eclipse**.</span></span>
  2.    <span data-ttu-id="cfde7-116">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="cfde7-116">Click **Add**.</span></span>

         ![Wtyczka usługi Service Fabric dla środowiska Eclipse Neon][sf-eclipse-plugin-install]
  3.    <span data-ttu-id="cfde7-118">Wybierz hello wtyczki sieci szkieletowej usług, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="cfde7-118">Select hello Service Fabric plug-in, and then click **Next**.</span></span>
  4.    <span data-ttu-id="cfde7-119">Wykonaj kroki instalacji hello, a następnie zaakceptuj postanowienia licencyjne dotyczące oprogramowania firmy Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="cfde7-119">Complete hello installation steps, and then accept hello Microsoft Software License Terms.</span></span>

<span data-ttu-id="cfde7-120">Jeśli masz już hello usługi sieć szkieletowa wtyczki zainstalowane, upewnij się, że masz hello najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="cfde7-120">If you already have hello Service Fabric plug-in installed, make sure that you have hello latest version.</span></span> <span data-ttu-id="cfde7-121">toocheck dostępnych aktualizacji, przejdź zbyt**pomocy** > **szczegółowe informacje dotyczące instalacji**.</span><span class="sxs-lookup"><span data-stu-id="cfde7-121">toocheck for available updates, go too**Help** > **Installation Details**.</span></span> <span data-ttu-id="cfde7-122">Witaj listy zainstalowanych wtyczek, wybierz sieć szkieletowa usług, a następnie kliknij **aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="cfde7-122">In hello list of installed plug-ins, select Service Fabric, and then click **Update**.</span></span> <span data-ttu-id="cfde7-123">Dostępne aktualizacje zostaną zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="cfde7-123">Available updates will be installed.</span></span>

> [!NOTE]
> <span data-ttu-id="cfde7-124">Jeśli instalację lub aktualizację hello wtyczki sieci szkieletowej usług przebiega powoli, może to być spowodowane tooan Eclipse ustawienie.</span><span class="sxs-lookup"><span data-stu-id="cfde7-124">If installing or updating hello Service Fabric plug-in is slow, it might be due tooan Eclipse setting.</span></span> <span data-ttu-id="cfde7-125">Eclipse zbiera metadanych we wszystkich lokacjach tooupdate zmiany, które są zarejestrowane z wystąpieniem programu Eclipse.</span><span class="sxs-lookup"><span data-stu-id="cfde7-125">Eclipse collects metadata on all changes tooupdate sites that are registered with your Eclipse instance.</span></span> <span data-ttu-id="cfde7-126">toospeed proces hello wyszukiwanie i instalowanie aktualizacji wtyczki w sieci szkieletowej usług Przejdź zbyt**dostępnych lokacji oprogramowania**.</span><span class="sxs-lookup"><span data-stu-id="cfde7-126">toospeed up hello process of checking for and installing a Service Fabric plug-in update, go too**Available Software Sites**.</span></span> <span data-ttu-id="cfde7-127">Usuń zaznaczenie pól wyboru hello dla wszystkich lokacji, z wyjątkiem hello, który wskazuje lokalizację wtyczki toohello sieci szkieletowej usług (http://dl.microsoft.com/eclipse/azure/servicefabric).</span><span class="sxs-lookup"><span data-stu-id="cfde7-127">Clear hello check boxes for all sites except for hello one that points toohello Service Fabric plug-in location (http://dl.microsoft.com/eclipse/azure/servicefabric).</span></span>

## <a name="create-a-service-fabric-application-in-eclipse"></a><span data-ttu-id="cfde7-128">Tworzenie aplikacji usługi Service Fabric w środowisku Eclipse</span><span class="sxs-lookup"><span data-stu-id="cfde7-128">Create a Service Fabric application in Eclipse</span></span>

1.  <span data-ttu-id="cfde7-129">Eclipse Neon zbyt Przejdź**pliku** > **nowy** > **innych**.</span><span class="sxs-lookup"><span data-stu-id="cfde7-129">In Eclipse Neon, go too**File** > **New** > **Other**.</span></span> <span data-ttu-id="cfde7-130">Wybierz pozycję **Service Fabric Project** (Projekt usługi Service Fabric), a następnie kliknij przycisk **Next** (Dalej).</span><span class="sxs-lookup"><span data-stu-id="cfde7-130">Select  **Service Fabric Project**, and then click **Next**.</span></span>

    ![Nowy projekt usługi Service Fabric — strona 1][create-application/p1]

2.  <span data-ttu-id="cfde7-132">Wprowadź nazwę projektu, a następnie kliknij przycisk **Next** (Dalej).</span><span class="sxs-lookup"><span data-stu-id="cfde7-132">Enter a name for your project, and then click **Next**.</span></span>

    ![Nowy projekt usługi Service Fabric — strona 2][create-application/p2]

3.  <span data-ttu-id="cfde7-134">Witaj listy szablonów, wybierz **szablonu usługi**.</span><span class="sxs-lookup"><span data-stu-id="cfde7-134">In hello list of templates, select **Service Template**.</span></span> <span data-ttu-id="cfde7-135">Wybierz typ szablonu usługi — Actor (Aktor), Stateless (Bezstanowa), Container (Kontener) lub Guest Binary (Binarna gościa) — a następnie kliknij przycisk **Next** (Dalej).</span><span class="sxs-lookup"><span data-stu-id="cfde7-135">Select your service template type (Actor, Stateless, Container, or Guest Binary), and then click **Next**.</span></span>

    ![Nowy projekt usługi Service Fabric — strona 3][create-application/p3]

4.  <span data-ttu-id="cfde7-137">Wprowadź nazwę usługi hello i szczegóły dotyczące usługi, a następnie kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="cfde7-137">Enter hello service name and service details, and then click **Finish**.</span></span>

    ![Nowy projekt usługi Service Fabric — strona 4][create-application/p4]

5. <span data-ttu-id="cfde7-139">Po utworzeniu pierwszego projektu sieci szkieletowej usług, hello **perspektywy skojarzonych Otwórz** okno dialogowe, kliknij przycisk **tak**.</span><span class="sxs-lookup"><span data-stu-id="cfde7-139">When you create your first Service Fabric project, in hello **Open Associated Perspective** dialog box, click **Yes**.</span></span>

    ![Nowy projekt usługi Service Fabric — strona 5][create-application/p5]

6.  <span data-ttu-id="cfde7-141">Nowy projekt wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="cfde7-141">Your new project looks like this:</span></span>

    ![Nowy projekt usługi Service Fabric — strona 6][create-application/p6]

## <a name="build-and-deploy-a-service-fabric-application-in-eclipse"></a><span data-ttu-id="cfde7-143">Kompilowanie i wdrażanie aplikacji usługi Service Fabric w środowisku Eclipse</span><span class="sxs-lookup"><span data-stu-id="cfde7-143">Build and deploy a Service Fabric application in Eclipse</span></span>

1.  <span data-ttu-id="cfde7-144">Kliknij prawym przyciskiem myszy nową aplikację usługi Service Fabric, a następnie wybierz polecenie **Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="cfde7-144">Right-click your new Service Fabric application, and then select **Service Fabric**.</span></span>

    ![Menu prawego przycisku myszy usługi Service Fabric][publish/RightClick]

2. <span data-ttu-id="cfde7-146">Wybierz odpowiednią opcję hello podmenu hello:</span><span class="sxs-lookup"><span data-stu-id="cfde7-146">In hello submenu, select hello option you want:</span></span>
    -   <span data-ttu-id="cfde7-147">Aplikacja hello toobuild bez czyszczenia, kliknij przycisk **kompilacji aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="cfde7-147">toobuild hello application without cleaning, click **Build Application**.</span></span>
    -   <span data-ttu-id="cfde7-148">Kliknij przycisk toodo czystą kompilację aplikacji hello **odbudować aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="cfde7-148">toodo a clean build of hello application, click **Rebuild Application**.</span></span>
    -   <span data-ttu-id="cfde7-149">Kliknij aplikacji hello tooclean wbudowanych artefaktów **czystą aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="cfde7-149">tooclean hello application of built artifacts, click **Clean Application**.</span></span>

3.  <span data-ttu-id="cfde7-150">To menu umożliwia także wdrożenie, cofnięcie wdrożenia i opublikowanie aplikacji:</span><span class="sxs-lookup"><span data-stu-id="cfde7-150">From this menu, you also can deploy, undeploy, and publish your application:</span></span>
    -   <span data-ttu-id="cfde7-151">Klaster lokalny tooyour toodeploy, kliknij przycisk **wdrażanie aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="cfde7-151">toodeploy tooyour local cluster, click **Deploy Application**.</span></span>
    -   <span data-ttu-id="cfde7-152">W hello **publikowania aplikacji** oknie dialogowym Wybierz profil publikowania:</span><span class="sxs-lookup"><span data-stu-id="cfde7-152">In hello **Publish Application** dialog box, select a publish profile:</span></span>
        -  <span data-ttu-id="cfde7-153">**Local.json**</span><span class="sxs-lookup"><span data-stu-id="cfde7-153">**Local.json**</span></span>
        -  <span data-ttu-id="cfde7-154">**Cloud.json**</span><span class="sxs-lookup"><span data-stu-id="cfde7-154">**Cloud.json**</span></span>

     <span data-ttu-id="cfde7-155">Te pliki JavaScript Object Notation (JSON) przechowywania informacji (takich jak punkty końcowe połączenia i informacji o zabezpieczeniach), która jest wymagana tooconnect tooyour lokalnego lub w klastrze chmury (Azure).</span><span class="sxs-lookup"><span data-stu-id="cfde7-155">These JavaScript Object Notation (JSON) files store information (such as connection endpoints and security information) that is required tooconnect tooyour local or cloud (Azure) cluster.</span></span>

  ![Menu publikowania usługi Service Fabric][publish/Publish]

<span data-ttu-id="cfde7-157">Toodeploy alternatywny sposób aplikacji sieci szkieletowej usług za pomocą programu Eclipse uruchomieniu konfiguracje.</span><span class="sxs-lookup"><span data-stu-id="cfde7-157">An alternate way toodeploy your Service Fabric application is by using Eclipse run configurations.</span></span>

  1.    <span data-ttu-id="cfde7-158">Przejdź za**Uruchom** > **konfiguracje wykonywania**.</span><span class="sxs-lookup"><span data-stu-id="cfde7-158">Go too**Run** > **Run Configurations**.</span></span>
  2.    <span data-ttu-id="cfde7-159">W obszarze **projektu Gradle**, wybierz pozycję hello **ServiceFabricDeployer** Uruchom konfigurację.</span><span class="sxs-lookup"><span data-stu-id="cfde7-159">Under **Gradle Project**, select hello **ServiceFabricDeployer** run configuration.</span></span>
  3.    <span data-ttu-id="cfde7-160">W prawym okienku hello na powitania **argumenty** karcie dla **publishProfile**, wybierz pozycję **lokalnego** lub **chmury**.</span><span class="sxs-lookup"><span data-stu-id="cfde7-160">In hello right pane, on hello **Arguments** tab, for **publishProfile**, select **local** or **cloud**.</span></span>  <span data-ttu-id="cfde7-161">Domyślnie Hello **lokalnego**.</span><span class="sxs-lookup"><span data-stu-id="cfde7-161">hello default is **local**.</span></span> <span data-ttu-id="cfde7-162">tooa toodeploy zdalnego lub chmury klastra, wybierz opcję **chmury**.</span><span class="sxs-lookup"><span data-stu-id="cfde7-162">toodeploy tooa remote or cloud cluster, select **cloud**.</span></span>
  4.    <span data-ttu-id="cfde7-163">tooensure czy hello odpowiednie informacje są umieszczane w hello profilów publikowania, Edytuj **Local.json** lub **Cloud.json** zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="cfde7-163">tooensure that hello proper information is populated in hello publish profiles, edit **Local.json** or **Cloud.json** as needed.</span></span> <span data-ttu-id="cfde7-164">Możesz dodać lub zaktualizować szczegóły punktu końcowego i poświadczenia zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="cfde7-164">You can add or update endpoint details and security credentials.</span></span>
  5.    <span data-ttu-id="cfde7-165">Upewnij się, że **katalog roboczy** punktów toohello aplikacji ma toodeploy.</span><span class="sxs-lookup"><span data-stu-id="cfde7-165">Ensure that **Working Directory** points toohello application you want toodeploy.</span></span> <span data-ttu-id="cfde7-166">toochange hello aplikacji, kliknij przycisk hello **obszaru roboczego** przycisk, a następnie wybierz aplikację hello.</span><span class="sxs-lookup"><span data-stu-id="cfde7-166">toochange hello application, click hello **Workspace** button, and then select hello application you want.</span></span>
  6.    <span data-ttu-id="cfde7-167">Kliknij przycisk **Apply** (Zastosuj), a następnie kliknij przycisk **Run** (Uruchom).</span><span class="sxs-lookup"><span data-stu-id="cfde7-167">Click **Apply**, and then click **Run**.</span></span>

<span data-ttu-id="cfde7-168">Aplikacja zostanie skompilowana i wdrożona w ciągu kilku minut.</span><span class="sxs-lookup"><span data-stu-id="cfde7-168">Your application builds and deploys within a few moments.</span></span> <span data-ttu-id="cfde7-169">Można monitorować stan wdrożenia hello w narzędziu Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="cfde7-169">You can monitor hello deployment status in Service Fabric Explorer.</span></span>  

## <a name="add-a-service-fabric-service-tooyour-service-fabric-application"></a><span data-ttu-id="cfde7-170">Dodaj tooyour usługi sieć szkieletowa usług aplikacji sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="cfde7-170">Add a Service Fabric service tooyour Service Fabric application</span></span>

<span data-ttu-id="cfde7-171">tooadd sieci szkieletowej usług tooan istniejącej sieci szkieletowej usług aplikacji usługi, hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="cfde7-171">tooadd a Service Fabric service tooan existing Service Fabric application, do hello following steps:</span></span>

1.  <span data-ttu-id="cfde7-172">Kliknij prawym przyciskiem myszy hello projektu mają tooadd usługi, a następnie kliknij przycisk **sieci szkieletowej usług**.</span><span class="sxs-lookup"><span data-stu-id="cfde7-172">Right-click hello project you want tooadd a service to, and then click **Service Fabric**.</span></span>

    ![Dodawanie usługi Service Fabric — strona 1][add-service/p1]

2.  <span data-ttu-id="cfde7-174">Kliknij przycisk **dodać Usługa sieci szkieletowej usług**, i hello pełny zestaw tooadd kroki projekt toohello usługi.</span><span class="sxs-lookup"><span data-stu-id="cfde7-174">Click **Add Service Fabric Service**, and complete hello set of steps tooadd a service toohello project.</span></span>
3.  <span data-ttu-id="cfde7-175">Hello wybierz szablon usługi ma tooadd tooyour projektu, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="cfde7-175">Select hello service template you want tooadd tooyour project, and then click **Next**.</span></span>

    ![Dodawanie usługi Service Fabric — strona 2][add-service/p2]

4.  <span data-ttu-id="cfde7-177">Wprowadź nazwę usługi hello (i inne szczegóły, w razie potrzeby), a następnie kliknij przycisk hello **Dodaj usługę** przycisku.</span><span class="sxs-lookup"><span data-stu-id="cfde7-177">Enter hello service name (and other details, as needed), and then click hello **Add Service** button.</span></span>  

    ![Dodawanie usługi Service Fabric — strona 3][add-service/p3]

5.  <span data-ttu-id="cfde7-179">Po dodaniu usługi hello ogólną strukturę projektu wygląda podobnie toohello następującego projektu:</span><span class="sxs-lookup"><span data-stu-id="cfde7-179">After hello service is added, your overall project structure looks similar toohello following project:</span></span>

    ![Dodawanie usługi Service Fabric — strona 4][add-service/p4]

## <a name="edit-manifest-versions-of-your-service-fabric-java-application"></a><span data-ttu-id="cfde7-181">Edytowanie wersji manifestu aplikacji Java usługi Service Fabric</span><span class="sxs-lookup"><span data-stu-id="cfde7-181">Edit Manifest versions of your Service Fabric Java application</span></span>

<span data-ttu-id="cfde7-182">tooedit wersji manifestu, kliknij prawym przyciskiem myszy projekt hello, przejdź zbyt**sieci szkieletowej usług** i wybierz **edytować wersji manifestu...**  z hello menu rozwijanym.</span><span class="sxs-lookup"><span data-stu-id="cfde7-182">tooedit manifest versions, right click on hello project, go too**Service Fabric** and select **Edit Manifest Versions...** from hello menu dropdown.</span></span> <span data-ttu-id="cfde7-183">W Kreatorze hello można aktualizować hello wersji manifestu dla manifest usługi manifestu, aplikacji i wersji hello **kod**, **Config** i **danych** pakietów.</span><span class="sxs-lookup"><span data-stu-id="cfde7-183">In hello wizard, you can update hello manifest versions for application manifest, service manifest and hello versions for **Code**, **Config** and **Data** packages.</span></span>

<span data-ttu-id="cfde7-184">Jeśli zaznaczysz opcję hello **automatycznie Aktualizuj wersje aplikacji i usługi** , a następnie zaktualizuj wersję, następnie wersji manifestu hello zostanie automatycznie zaktualizowana.</span><span class="sxs-lookup"><span data-stu-id="cfde7-184">If you check hello option **Automatically update application and service versions** and then update a version, then hello manifest versions will be automatically updated.</span></span> <span data-ttu-id="cfde7-185">toogive przykładem, należy najpierw wybrać hello pole wyboru, a następnie aktualizacji wersji hello **kod** wersji z 0.0.0 too0.0.1 i kliknij pozycję **Zakończ**, następnie usługi wersji manifestu i manifest aplikacji wersja będzie too0.0.1 automatycznie aktualizowane.</span><span class="sxs-lookup"><span data-stu-id="cfde7-185">toogive an example, you first select hello check-box, then update hello version of **Code** version from 0.0.0 too0.0.1 and click on **Finish**, then service manifest version and application manifest version will be automatically updated too0.0.1.</span></span>

## <a name="upgrade-your-service-fabric-java-application"></a><span data-ttu-id="cfde7-186">Uaktualnianie aplikacji Java usługi Service Fabric</span><span class="sxs-lookup"><span data-stu-id="cfde7-186">Upgrade your Service Fabric Java application</span></span>

<span data-ttu-id="cfde7-187">Scenariusz uaktualnienia, powiedz utworzone hello **App1** projektu przy użyciu hello wtyczki w środowisku Eclipse sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="cfde7-187">For an upgrade scenario, say you created hello **App1** project by using hello Service Fabric plug-in in Eclipse.</span></span> <span data-ttu-id="cfde7-188">Wdrożono go za pomocą wtyczki toocreate hello aplikacji o nazwie **fabric: / App1Application**.</span><span class="sxs-lookup"><span data-stu-id="cfde7-188">You deployed it by using hello plug-in toocreate an application named **fabric:/App1Application**.</span></span> <span data-ttu-id="cfde7-189">Typ aplikacji Hello jest **App1AppicationType**, i wersja aplikacji hello jest 1.0.</span><span class="sxs-lookup"><span data-stu-id="cfde7-189">hello application type is **App1AppicationType**, and hello application version is 1.0.</span></span> <span data-ttu-id="cfde7-190">Teraz ma tooupgrade aplikacji bez zakłócania ich dostępności.</span><span class="sxs-lookup"><span data-stu-id="cfde7-190">Now, you want tooupgrade your application without interrupting availability.</span></span>

<span data-ttu-id="cfde7-191">Najpierw należy wprowadzać żadnych zmian w aplikacji tooyour i skompiluj go ponownie zmodyfikować hello usługi.</span><span class="sxs-lookup"><span data-stu-id="cfde7-191">First, make any changes tooyour application, and then rebuild hello modified service.</span></span> <span data-ttu-id="cfde7-192">Aktualizacja hello modyfikacji pliku manifestu usługi (ServiceManifest.xml) z hello zaktualizowane wersje hello usługi (i kodu, konfiguracji lub danych w formie odpowiednich).</span><span class="sxs-lookup"><span data-stu-id="cfde7-192">Update hello modified service’s manifest file (ServiceManifest.xml) with hello updated versions for hello service (and Code, Config, or Data, as relevant).</span></span> <span data-ttu-id="cfde7-193">Ponadto zmodyfikuj manifest aplikacji hello (ApplicationManifest.xml) z numerem wersji hello zaktualizowane dla aplikacji hello i hello modyfikacji usługi.</span><span class="sxs-lookup"><span data-stu-id="cfde7-193">Also, modify hello application’s manifest (ApplicationManifest.xml) with hello updated version number for hello application and hello modified service.</span></span>  

<span data-ttu-id="cfde7-194">tooupgrade aplikacji przy użyciu Eclipse Neon, możesz utworzyć profil zduplikowane wykonywania konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="cfde7-194">tooupgrade your application by using Eclipse Neon, you can create a duplicate run configuration profile.</span></span> <span data-ttu-id="cfde7-195">Następnie należy użyć go tooupgrade aplikacji zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="cfde7-195">Then, use it tooupgrade your application as needed.</span></span>

1.  <span data-ttu-id="cfde7-196">Przejdź za**Uruchom** > **konfiguracje wykonywania**.</span><span class="sxs-lookup"><span data-stu-id="cfde7-196">Go too**Run** > **Run Configurations**.</span></span> <span data-ttu-id="cfde7-197">W okienku po lewej stronie powitania kliknij hello małą strzałkę toohello lewej strony **projektu Gradle**.</span><span class="sxs-lookup"><span data-stu-id="cfde7-197">In hello left pane, click hello small arrow toohello left of **Gradle Project**.</span></span>
2.  <span data-ttu-id="cfde7-198">Kliknij prawym przyciskiem myszy pozycję **ServiceFabricDeployer** i wybierz polecenie **Duplicate** (Duplikuj).</span><span class="sxs-lookup"><span data-stu-id="cfde7-198">Right-click **ServiceFabricDeployer**, and then select **Duplicate**.</span></span> <span data-ttu-id="cfde7-199">Wprowadź nową nazwę dla tej konfiguracji, na przykład **ServiceFabricUpgrader**.</span><span class="sxs-lookup"><span data-stu-id="cfde7-199">Enter a new name for this configuration, for example, **ServiceFabricUpgrader**.</span></span>
3.  <span data-ttu-id="cfde7-200">W prawym panelu hello na powitania **argumenty** Zmień **- Pconfig = "wdrażania"** za**- Pconfig = "Uaktualnij"**, a następnie kliknij przycisk **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="cfde7-200">In hello right panel, on hello **Arguments** tab, change **-Pconfig='deploy'** too**-Pconfig='upgrade'**, and then click **Apply**.</span></span>

<span data-ttu-id="cfde7-201">Ten proces tworzy i zapisuje profil uruchamiania konfiguracji można w dowolnym tooupgrade czasu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cfde7-201">This process creates and saves a run configuration profile you can use at any time tooupgrade your application.</span></span> <span data-ttu-id="cfde7-202">Zapewnia również hello najnowsze wersje typu aplikacji zaktualizowane z pliku manifestu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="cfde7-202">It also gets hello latest updated application type version from hello application manifest file.</span></span>

<span data-ttu-id="cfde7-203">Uaktualnianie aplikacji Hello zajmuje kilka minut.</span><span class="sxs-lookup"><span data-stu-id="cfde7-203">hello application upgrade takes a few minutes.</span></span> <span data-ttu-id="cfde7-204">Można monitorować hello uaktualniania aplikacji w narzędziu Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="cfde7-204">You can monitor hello application upgrade in Service Fabric Explorer.</span></span>

## <a name="migrating-old-service-fabric-java-applications-toobe-used-with-maven"></a><span data-ttu-id="cfde7-205">Migrowanie starego toobe aplikacji Java sieci szkieletowej usług używany z Maven</span><span class="sxs-lookup"><span data-stu-id="cfde7-205">Migrating old Service Fabric Java applications toobe used with Maven</span></span>
<span data-ttu-id="cfde7-206">Biblioteki usługi sieć szkieletowa Java niedawno został przeniesiony z repozytorium tooMaven zestawu SDK Java sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="cfde7-206">We have recently moved Service Fabric Java libraries from Service Fabric Java SDK tooMaven repository.</span></span> <span data-ttu-id="cfde7-207">Gdy hello nowe aplikacje, które można wygenerować za pomocą programu Eclipse, spowoduje wygenerowanie najnowsze zaktualizowane projekty (które będą mogli toowork z Maven), można aktualizacji istniejącej sieci szkieletowej usług bezstanowych lub aplikacji Java aktora, które były używane hello zestawu SDK Java sieci szkieletowej usług wcześniej, toouse hello usługi sieć szkieletowa Java zależności z Maven.</span><span class="sxs-lookup"><span data-stu-id="cfde7-207">While hello new applications you generate using Eclipse, will generate latest updated projects (which will be able toowork with Maven), you can update your existing Service Fabric stateless or actor Java applications, which were using hello Service Fabric Java SDK earlier, toouse hello Service Fabric Java dependencies from Maven.</span></span> <span data-ttu-id="cfde7-208">Wykonaj kroki hello wymienione [tutaj](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure starszych aplikacji współdziała z Maven.</span><span class="sxs-lookup"><span data-stu-id="cfde7-208">Please follow hello steps mentioned [here](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure your older application works with Maven.</span></span>

<!-- Images -->

[sf-eclipse-plugin-install]: ./media/service-fabric-get-started-eclipse/service-fabric-eclipse-plugin.png

[create-application/p1]:./media/service-fabric-get-started-eclipse/create-application/p1.png
[create-application/p2]:./media/service-fabric-get-started-eclipse/create-application/p2.png
[create-application/p3]:./media/service-fabric-get-started-eclipse/create-application/p3.png
[create-application/p4]:./media/service-fabric-get-started-eclipse/create-application/p4.png
[create-application/p5]:./media/service-fabric-get-started-eclipse/create-application/p5.png
[create-application/p6]:./media/service-fabric-get-started-eclipse/create-application/p6.png

[publish/Publish]: ./media/service-fabric-get-started-eclipse/publish/Publish.png
[publish/RightClick]: ./media/service-fabric-get-started-eclipse/publish/RightClick.png

[add-service/p1]: ./media/service-fabric-get-started-eclipse/add-service/p1.png
[add-service/p2]: ./media/service-fabric-get-started-eclipse/add-service/p2.png
[add-service/p3]: ./media/service-fabric-get-started-eclipse/add-service/p3.png
[add-service/p4]: ./media/service-fabric-get-started-eclipse/add-service/p4.png

<!-- Links -->
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship
