---
title: "zestaw narzędzi platformy Azure dla programu Eclipse hello aaaPublish aplikacji Spring rozruchu, jako kontener Docker przy użyciu | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toopublish tooMicrosoft aplikacji sieci web Azure jako kontener Docker przy użyciu hello zestawu narzędzi platformy Azure dla programu Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 06/21/2017
ms.author: robmcm
ms.openlocfilehash: 29390c49c339a1ebb87cb3951b21cea01c0da15f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-hello-azure-toolkit-for-eclipse"></a><span data-ttu-id="62166-103">Publikowanie aplikacji rozruchu Spring jako kontener Docker przy użyciu hello Azure zestawu narzędzi dla programu Eclipse</span><span class="sxs-lookup"><span data-stu-id="62166-103">Publish a Spring Boot app as a Docker container by using hello Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="62166-104">Witaj [Spring Framework] to rozwiązanie open source, które pomaga deweloperom języka Java, tworzenie aplikacji na poziomie przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="62166-104">hello [Spring Framework] is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="62166-105">Jednego z projektów innych popularnych hello, które jest wbudowane znajdujący się na platformie jest [rozruchu Spring], zapewniające uproszczone podejście do tworzenia autonomicznych aplikacji Java.</span><span class="sxs-lookup"><span data-stu-id="62166-105">One of hello more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating standalone Java applications.</span></span>

<span data-ttu-id="62166-106">[Docker] jest to rozwiązanie open source, które pomaga deweloperom automatyzację wdrażania hello, skalowania i zarządzania ich aplikacji, które są uruchomione w kontenerach.</span><span class="sxs-lookup"><span data-stu-id="62166-106">[Docker] is an open-source solution that helps developers automate hello deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="62166-107">W tym samouczku przedstawiono hello kroki toodeploy aplikacja rozruchu Spring jako Docker tooMicrosoft kontenera Azure za pomocą hello Azure zestawu narzędzi dla programu Eclipse.</span><span class="sxs-lookup"><span data-stu-id="62166-107">This tutorial walks you through hello steps toodeploy a Spring Boot application as a Docker container tooMicrosoft Azure by using hello Azure Toolkit for Eclipse.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="clone-hello-default-spring-boot-docker-repository"></a><span data-ttu-id="62166-108">Klonuj repozytorium Docker rozruchu Spring domyślne hello</span><span class="sxs-lookup"><span data-stu-id="62166-108">Clone hello default Spring Boot Docker repository</span></span>

### <a name="import-hello-public-repository"></a><span data-ttu-id="62166-109">Importuj hello publicznego repozytorium</span><span class="sxs-lookup"><span data-stu-id="62166-109">Import hello public repository</span></span>

<span data-ttu-id="62166-110">Witaj kolejnych krokach objaśniono sposób przez klonowanie komputera lokalnego repozytorium tooyour hello Spring Docker rozruch przy użyciu IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="62166-110">hello following steps walk you through cloning hello Spring Boot Docker repository tooyour local computer by using IntelliJ.</span></span> <span data-ttu-id="62166-111">Jeśli chcesz toouse wiersza polecenia, zobacz [wdrażanie aplikacji Spring rozruchu w systemie Linux w usłudze kontenera platformy Azure][Deploy Spring Boot on Linux in ACS].</span><span class="sxs-lookup"><span data-stu-id="62166-111">If you want toouse a command line, see [Deploy a Spring Boot application on Linux in Azure Container Service][Deploy Spring Boot on Linux in ACS].</span></span>

1. <span data-ttu-id="62166-112">Otwórz środowisko Eclipse.</span><span class="sxs-lookup"><span data-stu-id="62166-112">Open Eclipse.</span></span>

1. <span data-ttu-id="62166-113">Kliknij przycisk **pliku** > **importu**.</span><span class="sxs-lookup"><span data-stu-id="62166-113">Click **File** > **Import**.</span></span>

   ![Menu Plik importu][CL01]

1. <span data-ttu-id="62166-115">Gdy hello **importu** zostanie otwarte okno dialogowe:</span><span class="sxs-lookup"><span data-stu-id="62166-115">When hello **Import** dialog box opens:</span></span>

   <span data-ttu-id="62166-116">a.</span><span class="sxs-lookup"><span data-stu-id="62166-116">a.</span></span> <span data-ttu-id="62166-117">Rozwiń węzeł **Git**.</span><span class="sxs-lookup"><span data-stu-id="62166-117">Expand **Git**.</span></span>

   <span data-ttu-id="62166-118">b.</span><span class="sxs-lookup"><span data-stu-id="62166-118">b.</span></span> <span data-ttu-id="62166-119">Wybierz **projekty z Git**.</span><span class="sxs-lookup"><span data-stu-id="62166-119">Select **Projects from Git**.</span></span>
   
   <span data-ttu-id="62166-120">c.</span><span class="sxs-lookup"><span data-stu-id="62166-120">c.</span></span> <span data-ttu-id="62166-121">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="62166-121">Click **Next**.</span></span>

   ![Okno dialogowe Importowanie][CL02]

1. <span data-ttu-id="62166-123">Na powitania **wybierz źródło repozytorium** strony:</span><span class="sxs-lookup"><span data-stu-id="62166-123">On hello **Select Repository Source** page:</span></span>

   <span data-ttu-id="62166-124">a.</span><span class="sxs-lookup"><span data-stu-id="62166-124">a.</span></span> <span data-ttu-id="62166-125">Wybierz **Clone URI**.</span><span class="sxs-lookup"><span data-stu-id="62166-125">Select **Clone URI**.</span></span>
   
   <span data-ttu-id="62166-126">b.</span><span class="sxs-lookup"><span data-stu-id="62166-126">b.</span></span> <span data-ttu-id="62166-127">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="62166-127">Click **Next**.</span></span>

   ![Wybierz źródło repozytorium strony][CL03]

1. <span data-ttu-id="62166-129">Na powitania **repozytorium Git źródła** strony:</span><span class="sxs-lookup"><span data-stu-id="62166-129">On hello **Source Git Repository** page:</span></span>

   <span data-ttu-id="62166-130">a.</span><span class="sxs-lookup"><span data-stu-id="62166-130">a.</span></span> <span data-ttu-id="62166-131">Aby uzyskać **URI**, wprowadź `https://github.com/spring-guides/gs-spring-boot-docker.git`.</span><span class="sxs-lookup"><span data-stu-id="62166-131">For **URI**, enter `https://github.com/spring-guides/gs-spring-boot-docker.git`.</span></span> <span data-ttu-id="62166-132">Ten krok powinien automatycznie wypełnić hello **hosta** i **ścieżki repozytorium** pola z hello Popraw wartości.</span><span class="sxs-lookup"><span data-stu-id="62166-132">This step should automatically populate hello **Host** and **Repository path** fields with hello correct values.</span></span>
   
   <span data-ttu-id="62166-133">b.</span><span class="sxs-lookup"><span data-stu-id="62166-133">b.</span></span> <span data-ttu-id="62166-134">repozytorium rozruchu Spring Hello jest publiczny, więc nie powinien mieć tooenter Git nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="62166-134">hello Spring Boot repository is public, so you should not have tooenter your Git username and password.</span></span>
   
   <span data-ttu-id="62166-135">c.</span><span class="sxs-lookup"><span data-stu-id="62166-135">c.</span></span> <span data-ttu-id="62166-136">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="62166-136">Click **Next**.</span></span>

   ![Źródło repozytorium Git strony][CL04]

1. <span data-ttu-id="62166-138">Na powitania **wybór gałęzi** kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="62166-138">On hello **Branch Selection** page, click **Next**.</span></span>

   ![Strona wybierania gałęzi][CL05]

1. <span data-ttu-id="62166-140">Na powitania **lokalne miejsce docelowe** strony:</span><span class="sxs-lookup"><span data-stu-id="62166-140">On hello **Local Destination** page:</span></span>

   <span data-ttu-id="62166-141">a.</span><span class="sxs-lookup"><span data-stu-id="62166-141">a.</span></span> <span data-ttu-id="62166-142">Określ folder lokalny hello miejscu użytkownika lokalnego repozytorium.</span><span class="sxs-lookup"><span data-stu-id="62166-142">Specify hello local folder where you want your local repo.</span></span>
   
   <span data-ttu-id="62166-143">b.</span><span class="sxs-lookup"><span data-stu-id="62166-143">b.</span></span> <span data-ttu-id="62166-144">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="62166-144">Click **Next**.</span></span>

   ![Strona docelowa lokalnego][CL06]

1. <span data-ttu-id="62166-146">Na powitania **wybierz toouse Kreatora importowania projektów** strony:</span><span class="sxs-lookup"><span data-stu-id="62166-146">On hello **Select a wizard toouse for importing projects** page:</span></span>

   <span data-ttu-id="62166-147">a.</span><span class="sxs-lookup"><span data-stu-id="62166-147">a.</span></span> <span data-ttu-id="62166-148">Wybierz **importu jako ogólne projekt**.</span><span class="sxs-lookup"><span data-stu-id="62166-148">Select **Import as a general project**.</span></span>
   
   <span data-ttu-id="62166-149">b.</span><span class="sxs-lookup"><span data-stu-id="62166-149">b.</span></span> <span data-ttu-id="62166-150">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="62166-150">Click **Next**.</span></span>

   ![Strony "Wybierz toouse Kreatora importowania projektów"][CL07]

1. <span data-ttu-id="62166-152">Na powitania **Import projektów** strony:</span><span class="sxs-lookup"><span data-stu-id="62166-152">On hello **Import Projects** page:</span></span>

   <span data-ttu-id="62166-153">a.</span><span class="sxs-lookup"><span data-stu-id="62166-153">a.</span></span> <span data-ttu-id="62166-154">Określ nazwę projektu.</span><span class="sxs-lookup"><span data-stu-id="62166-154">Specify your project name.</span></span>
   
   <span data-ttu-id="62166-155">b.</span><span class="sxs-lookup"><span data-stu-id="62166-155">b.</span></span> <span data-ttu-id="62166-156">Kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="62166-156">Click **Finish**.</span></span>

   ![Importowanie projektów][CL08]

1. <span data-ttu-id="62166-158">W repozytorium hello został pomyślnie sklonowany, widoczne wszystkie pliki hello na liście w programie Eclipse.</span><span class="sxs-lookup"><span data-stu-id="62166-158">When hello repository is cloned successfully, you see all hello files listed in Eclipse.</span></span>

   ![Lokalne repozytorium][CL09]

### <a name="create-a-maven-project-from-your-local-repository"></a><span data-ttu-id="62166-160">Utwórz projekt Maven z lokalnym repozytorium</span><span class="sxs-lookup"><span data-stu-id="62166-160">Create a Maven project from your local repository</span></span>

<span data-ttu-id="62166-161">repozytorium Docker rozruchu Spring Hello zawiera ukończone projekt Maven, który będzie używany na potrzeby tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="62166-161">hello Spring Boot Docker repository contains a completed Maven project, which you will use for this tutorial.</span></span> 

1. <span data-ttu-id="62166-162">Kliknij przycisk **pliku** > **importu**.</span><span class="sxs-lookup"><span data-stu-id="62166-162">Click **File** > **Import**.</span></span>

   ![Zaimportuj polecenia menu Plik hello][CL01]

1. <span data-ttu-id="62166-164">Gdy hello **importu** zostanie otwarte okno dialogowe:</span><span class="sxs-lookup"><span data-stu-id="62166-164">When hello **Import** dialog box opens:</span></span>

   <span data-ttu-id="62166-165">a.</span><span class="sxs-lookup"><span data-stu-id="62166-165">a.</span></span> <span data-ttu-id="62166-166">Rozwiń węzeł **Maven**.</span><span class="sxs-lookup"><span data-stu-id="62166-166">Expand **Maven**.</span></span>
   
   <span data-ttu-id="62166-167">b.</span><span class="sxs-lookup"><span data-stu-id="62166-167">b.</span></span> <span data-ttu-id="62166-168">Wybierz **istniejące projekty Maven**.</span><span class="sxs-lookup"><span data-stu-id="62166-168">Select **Existing Maven Projects**.</span></span>
   
   <span data-ttu-id="62166-169">c.</span><span class="sxs-lookup"><span data-stu-id="62166-169">c.</span></span> <span data-ttu-id="62166-170">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="62166-170">Click **Next**.</span></span>

   ![Okno dialogowe Importowanie][MV01]

1. <span data-ttu-id="62166-172">Na powitania **projekty Maven** strony:</span><span class="sxs-lookup"><span data-stu-id="62166-172">On hello **Maven Projects** page:</span></span>

   <span data-ttu-id="62166-173">a.</span><span class="sxs-lookup"><span data-stu-id="62166-173">a.</span></span> <span data-ttu-id="62166-174">Dla **katalog główny**, określ hello **pełną** folderu w lokalnym repozytorium.</span><span class="sxs-lookup"><span data-stu-id="62166-174">For **Root Directory**, specify hello **complete** folder in your local repository.</span></span>
   
   <span data-ttu-id="62166-175">b.</span><span class="sxs-lookup"><span data-stu-id="62166-175">b.</span></span> <span data-ttu-id="62166-176">Rozwiń węzeł hello **zaawansowane** , a następnie wprowadź niestandardową nazwę **szablon nazwy**.</span><span class="sxs-lookup"><span data-stu-id="62166-176">Expand hello **Advanced** section, and enter a custom name for **Name template**.</span></span>
   
   <span data-ttu-id="62166-177">c.</span><span class="sxs-lookup"><span data-stu-id="62166-177">c.</span></span> <span data-ttu-id="62166-178">Wybierz hello pole hello **pom.xml** plik w projekcie hello.</span><span class="sxs-lookup"><span data-stu-id="62166-178">Select hello box for hello **pom.xml** file in hello project.</span></span>
   
   <span data-ttu-id="62166-179">d.</span><span class="sxs-lookup"><span data-stu-id="62166-179">d.</span></span> <span data-ttu-id="62166-180">Kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="62166-180">Click **Finish**.</span></span>

   ![Strona Projekty maven][MV02]

1. <span data-ttu-id="62166-182">Otwarcie projekt Maven hello pomyślnie, zostanie wyświetlony drugi projektu Eclipse na liście.</span><span class="sxs-lookup"><span data-stu-id="62166-182">When hello Maven project is opened successfully, you see a second project listed in Eclipse.</span></span>

   ![Projekt Maven lokalnego][MV03]

## <a name="build-your-spring-boot-app-by-using-maven"></a><span data-ttu-id="62166-184">Tworzenie aplikacji Spring rozruch przy użyciu narzędzia Maven</span><span class="sxs-lookup"><span data-stu-id="62166-184">Build your Spring Boot app by using Maven</span></span>

1. <span data-ttu-id="62166-185">Wybierz projekt Maven hello hello Eksplorator projektów programu Eclipse.</span><span class="sxs-lookup"><span data-stu-id="62166-185">In hello Eclipse Project Explorer, select hello Maven project.</span></span>

1. <span data-ttu-id="62166-186">Kliknij przycisk **Uruchom** > **Uruchom jako** > **kompilacja Maven**.</span><span class="sxs-lookup"><span data-stu-id="62166-186">Click **Run** > **Run As** > **Maven build**.</span></span>

   ![Polecenia toorun jako kompilacja Maven][BU01]

1. <span data-ttu-id="62166-188">Po pomyślnym utworzeniu aplikacji hello okna konsoli Pokazuje stan hello.</span><span class="sxs-lookup"><span data-stu-id="62166-188">When your application is successfully built, hello console window shows hello status.</span></span>

   ![Pomyślne kompilacja Maven][BU02]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a><span data-ttu-id="62166-190">Publikowanie tooAzure aplikacji sieci web przy użyciu kontenera Docker</span><span class="sxs-lookup"><span data-stu-id="62166-190">Publish your web app tooAzure by using a Docker container</span></span>

1. <span data-ttu-id="62166-191">Wybierz projekt Maven hello hello Eksplorator projektów programu Eclipse.</span><span class="sxs-lookup"><span data-stu-id="62166-191">In hello Eclipse Project Explorer, select hello Maven project.</span></span>

1. <span data-ttu-id="62166-192">Kliknij przycisk hello Azure **publikowania** menu, a następnie kliknij przycisk **Publikuj jako kontener Docker**.</span><span class="sxs-lookup"><span data-stu-id="62166-192">Click hello Azure **Publish** menu, and then click **Publish as Docker Container**.</span></span>

   ![Publikuj jako polecenia w kontenerze Docker][PU01]

1. <span data-ttu-id="62166-194">Gdy hello **wdrażanie kontenera Docker na platformie Azure** zostanie wyświetlone okno dialogowe:</span><span class="sxs-lookup"><span data-stu-id="62166-194">When hello **Deploying Docker Container on Azure** dialog box appears:</span></span>

   <span data-ttu-id="62166-195">a.</span><span class="sxs-lookup"><span data-stu-id="62166-195">a.</span></span> <span data-ttu-id="62166-196">Wprowadź nazwę niestandardowego obrazu Docker.</span><span class="sxs-lookup"><span data-stu-id="62166-196">Enter a custom Docker image name.</span></span>
   
   <span data-ttu-id="62166-197">b.</span><span class="sxs-lookup"><span data-stu-id="62166-197">b.</span></span> <span data-ttu-id="62166-198">Dla **toodeploy artefaktu**, określ hello ścieżki toohello **gs-spring — rozruchu docker-0.1.0.jar** plików, które zostały utworzone.</span><span class="sxs-lookup"><span data-stu-id="62166-198">For **Artifact toodeploy**, specify hello path toohello **gs-spring-boot-docker-0.1.0.jar** file you just built.</span></span>

   ![Określ opcje Docker][PU02]

   <span data-ttu-id="62166-200">Wyświetlane są wszystkie istniejące hosty Docker.</span><span class="sxs-lookup"><span data-stu-id="62166-200">Any existing Docker hosts are displayed.</span></span> 

1. <span data-ttu-id="62166-201">Jeśli wybierzesz toodeploy tooan istniejącą hosta, możesz pominąć toostep 5.</span><span class="sxs-lookup"><span data-stu-id="62166-201">If you choose toodeploy tooan existing host, you can skip toostep 5.</span></span> <span data-ttu-id="62166-202">W przeciwnym razie użyj hello następujące kroki toocreate hosta:</span><span class="sxs-lookup"><span data-stu-id="62166-202">Otherwise, use hello following steps toocreate a host:</span></span>

   <span data-ttu-id="62166-203">a.</span><span class="sxs-lookup"><span data-stu-id="62166-203">a.</span></span> <span data-ttu-id="62166-204">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="62166-204">Click **Add**.</span></span>

      ![Dodaj nowy host platformy Docker][PU03]

   <span data-ttu-id="62166-206">b.</span><span class="sxs-lookup"><span data-stu-id="62166-206">b.</span></span> <span data-ttu-id="62166-207">Gdy hello **hostów Docker Utwórz** zostanie wyświetlone okno dialogowe, możesz wybrać domyślne hello tooaccept lub można określić wszystkie niestandardowe ustawienia dla nowego hosta platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="62166-207">When hello **Create Docker Host** dialog box appears, you can choose tooaccept hello defaults, or you can specify any custom settings for your new Docker host.</span></span> <span data-ttu-id="62166-208">(Aby uzyskać szczegółowe opisy hello różne ustawienia, zobacz [opublikować aplikację sieci web jako kontener Docker za pomocą hello Azure Toolkit for IntelliJ][Publish Container with Azure Toolkit].) Kliknij przycisk **dalej** po określeniu które toouse ustawienia.</span><span class="sxs-lookup"><span data-stu-id="62166-208">(For detailed descriptions of hello various settings, see [Publish a web app as a Docker container by using hello Azure Toolkit for IntelliJ][Publish Container with Azure Toolkit].) Click **Next** when you have specified which settings toouse.</span></span>

      ![Określ opcje hostów Docker][PU04]

   <span data-ttu-id="62166-210">c.</span><span class="sxs-lookup"><span data-stu-id="62166-210">c.</span></span> <span data-ttu-id="62166-211">Możesz wybrać toouse istniejących poświadczeń logowania usługi Azure key vault lub tooenter można wybrać nowe poświadczenia logowania Docker.</span><span class="sxs-lookup"><span data-stu-id="62166-211">You can choose toouse existing login credentials from an Azure key vault, or you can choose tooenter new Docker login credentials.</span></span> <span data-ttu-id="62166-212">Kliknij przycisk **Zakończ** po określeniu opcji.</span><span class="sxs-lookup"><span data-stu-id="62166-212">Click **Finish** when you have specified your options.</span></span>

      ![Określ poświadczenia hostów Docker][PU05]

1. <span data-ttu-id="62166-214">Wybierz hosta Docker, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="62166-214">Select your Docker host, and then click **Next**.</span></span>

   ![Wybierz toouse hostów Docker][PU06]

1. <span data-ttu-id="62166-216">Na ostatniej stronie powitania hello **wdrażanie kontenera Docker na platformie Azure** oknie dialogowym Określ hello następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="62166-216">On hello last page of hello **Deploying Docker Container on Azure** dialog box, specify hello following options:</span></span>

   <span data-ttu-id="62166-217">a.</span><span class="sxs-lookup"><span data-stu-id="62166-217">a.</span></span> <span data-ttu-id="62166-218">Można wybrać toospecify niestandardową nazwę kontenera hello, który będzie obsługiwał z kontenera Docker lub możesz zaakceptować domyślną hello.</span><span class="sxs-lookup"><span data-stu-id="62166-218">You can choose toospecify a custom name for hello container that will host your Docker container, or you can accept hello default.</span></span>

   <span data-ttu-id="62166-219">b.</span><span class="sxs-lookup"><span data-stu-id="62166-219">b.</span></span> <span data-ttu-id="62166-220">Wprowadź porty TCP powitania dla hosta docker przy użyciu składni hello: *[portu zewnętrznego]*:*[wewnętrznego portu]*.</span><span class="sxs-lookup"><span data-stu-id="62166-220">Enter hello TCP ports for your docker host by using hello following syntax: *[external port]*:*[internal port]*.</span></span> <span data-ttu-id="62166-221">Na przykład **80:8080** określa zewnętrznego portu 80 i hello domyślnego wewnętrzny rozruchu Spring portu 8080.</span><span class="sxs-lookup"><span data-stu-id="62166-221">For example, **80:8080** specifies an external port of 80 and hello default internal Spring Boot port of 8080.</span></span>
   
      <span data-ttu-id="62166-222">Jeśli dostosowano wewnętrzny port (na przykład, edytując plik application.yml hello), należy numer portu hello toospecify dla hello poprawne toooccur routingu na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="62166-222">If you have customized your internal port (for example, by editing hello application.yml file), you need toospecify hello port number for hello correct routing toooccur in Azure.</span></span>

   <span data-ttu-id="62166-223">c.</span><span class="sxs-lookup"><span data-stu-id="62166-223">c.</span></span> <span data-ttu-id="62166-224">Po skonfigurowaniu tych opcji, kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="62166-224">After you configure these options, click **Finish**.</span></span>

   ![Wdrażanie kontenera Docker na platformie Azure][PU07]

1. <span data-ttu-id="62166-226">Po zakończeniu publikowania hello Azure Toolkit hello Wyświetla dziennika aktywności platformy Azure **opublikowano** hello stanu.</span><span class="sxs-lookup"><span data-stu-id="62166-226">When hello Azure Toolkit has finished publishing, hello Azure Activity Log displays **Published** for hello status.</span></span>

   ![Pomyślnie wdrożono hostów Docker][PU08]

## <a name="next-steps"></a><span data-ttu-id="62166-228">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="62166-228">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Deploy Spring Boot on Linux in ACS]:container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[rozruchu Spring]: http://projects.spring.io/spring-boot/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[CL01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL01.png
[CL02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL02.png
[CL03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL03.png
[CL04]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL04.png
[CL05]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL05.png
[CL06]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL06.png
[CL07]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL07.png
[CL08]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL08.png
[CL09]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL09.png

[MV01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV01.png
[MV02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV02.png
[MV03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV03.png

[BU01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU01.png
[BU02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU02.png

[PU01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU01.png
[PU02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU02.png
[PU03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU03.png
[PU04]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU04.png
[PU05]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU05.png
[PU06]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU06.png
[PU07]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU07.png
[PU08]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU08.png
