---
title: "aaaPublish aplikacji Spring rozruchu, jako kontener Docker przy użyciu hello Azure Toolkit for IntelliJ | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toopublish tooMicrosoft aplikacji sieci web Azure jako kontener Docker przy użyciu hello Azure Toolkit for IntelliJ."
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
ms.openlocfilehash: 8964cb33fd8f61a39f091633ae9074d9658232fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-hello-azure-toolkit-for-intellij"></a><span data-ttu-id="52d68-103">Publikowanie aplikacji rozruchu Spring jako kontener Docker przy użyciu hello Azure Toolkit for IntelliJ</span><span class="sxs-lookup"><span data-stu-id="52d68-103">Publish a Spring Boot app as a Docker container by using hello Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="52d68-104">Witaj [Spring Framework] to rozwiązanie open source, które pomaga deweloperom języka Java, tworzenie aplikacji na poziomie przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="52d68-104">hello [Spring Framework] is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="52d68-105">Jednego z projektów innych popularnych hello, które jest wbudowane znajdujący się na platformie jest [rozruchu Spring], zapewniające uproszczone podejście do tworzenia autonomicznych aplikacji Java.</span><span class="sxs-lookup"><span data-stu-id="52d68-105">One of hello more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating standalone Java applications.</span></span>

<span data-ttu-id="52d68-106">[Docker] jest to rozwiązanie open source, które pomaga deweloperom automatyzację wdrażania hello, skalowania i zarządzania ich aplikacji, które są uruchomione w kontenerach.</span><span class="sxs-lookup"><span data-stu-id="52d68-106">[Docker] is an open-source solution that helps developers automate hello deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="52d68-107">W tym samouczku przedstawiono hello kroki toodeploy aplikacja rozruchu Spring jako Docker tooMicrosoft kontenera Azure za pomocą hello Azure Toolkit for IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="52d68-107">This tutorial walks you through hello steps toodeploy a Spring Boot application as a Docker container tooMicrosoft Azure by using hello Azure Toolkit for IntelliJ.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="clone-hello-default-spring-boot-docker-repo"></a><span data-ttu-id="52d68-108">Klonowanie repozytorium Docker rozruchu Spring domyślne hello</span><span class="sxs-lookup"><span data-stu-id="52d68-108">Clone hello default Spring Boot Docker repo</span></span>

<span data-ttu-id="52d68-109">Witaj kolejnych krokach objaśniono sposób za pomocą klonowania repozytorium Docker rozruchu Spring hello przy użyciu IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="52d68-109">hello following steps walk you through cloning hello Spring Boot Docker repo by using IntelliJ.</span></span> <span data-ttu-id="52d68-110">Jeśli chcesz toouse wiersza polecenia, zobacz [wdrażanie aplikacji Spring rozruchu w systemie Linux w usłudze kontenera platformy Azure][Deploy Spring Boot on Linux in ACS].</span><span class="sxs-lookup"><span data-stu-id="52d68-110">If you want toouse a command line, see [Deploy a Spring Boot application on Linux in Azure Container Service][Deploy Spring Boot on Linux in ACS].</span></span>

1. <span data-ttu-id="52d68-111">Otwórz środowisko IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="52d68-111">Open IntelliJ.</span></span>

1. <span data-ttu-id="52d68-112">Na ekranie powitalnym hello, wybierz hello **GitHub** opcję hello **wyewidencjonowania z kontroli wersji** listy.</span><span class="sxs-lookup"><span data-stu-id="52d68-112">On hello welcome screen, select hello **GitHub** option in hello **Check out from Version Control** list.</span></span>

   ![Opcja GitHub kontroli wersji][CL01]

1. <span data-ttu-id="52d68-114">Wprowadź swoje poświadczenia, jeśli zostanie wyświetlony monit o toolog w.</span><span class="sxs-lookup"><span data-stu-id="52d68-114">Enter your credentials if you are prompted toolog in.</span></span>

   * <span data-ttu-id="52d68-115">Jeśli używasz toolog nazwy użytkownika i hasła w tooGitHub:</span><span class="sxs-lookup"><span data-stu-id="52d68-115">If you are using a username/password toolog in tooGitHub:</span></span>

      ![Okno dialogowe wprowadzanie GitHub nazwy użytkownika i hasła][CL02a]

   * <span data-ttu-id="52d68-117">Jeśli używasz tokenu toolog w tooGitHub:</span><span class="sxs-lookup"><span data-stu-id="52d68-117">If you are using a token toolog in tooGitHub:</span></span>

      ![Okno dialogowe wprowadzanie GitHub token][CL02b]

1. <span data-ttu-id="52d68-119">Wprowadź **https://github.com/spring-guides/gs-spring-boot-docker.git** dla adresu URL repozytorium hello, określ informacje o Twoich ścieżka lokalna i folder, a następnie kliknij **klonowania**.</span><span class="sxs-lookup"><span data-stu-id="52d68-119">Enter **https://github.com/spring-guides/gs-spring-boot-docker.git** for hello repo URL, specify your local path and folder information, and then click **Clone**.</span></span>

   ![Okno dialogowe klonowanie repozytorium][CL03]

1. <span data-ttu-id="52d68-121">Gdy pojawi się monit toocreate IntelliJ projektu wybierz **nr**.</span><span class="sxs-lookup"><span data-stu-id="52d68-121">When you're prompted toocreate an IntelliJ project, select **No**.</span></span>

   ![Odrzucanie toocreate projektu IntelliJ][CL04]

1. <span data-ttu-id="52d68-123">Na stronie powitalnej powitania kliknij **Importowanie projektu**.</span><span class="sxs-lookup"><span data-stu-id="52d68-123">On hello welcome page, click **Import Project**.</span></span>

   ![Wybór projektu importu][CL05]

1. <span data-ttu-id="52d68-125">Znajdź ścieżki hello gdzie sklonować repozytorium rozruchu Spring hello, wybierz hello **pełną** folder główny hello, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="52d68-125">Locate hello path where you cloned hello Spring Boot repo, select hello **complete** folder under hello root, and then click **OK**.</span></span>

   ![Wybierz folder do zaimportowania][CL06]

1. <span data-ttu-id="52d68-127">Po wyświetleniu monitu wybierz **Tworzenie projektu z istniejących źródeł**.</span><span class="sxs-lookup"><span data-stu-id="52d68-127">When you're prompted, select **Create project from existing sources**.</span></span>

   ![Opcja toocreate projekt z istniejących źródeł][CL07]

1. <span data-ttu-id="52d68-129">Określ nazwę projektu lub zaakceptuj domyślną hello, sprawdź hello poprawną ścieżkę toohello **pełną** folder, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="52d68-129">Specify your project name or accept hello default, verify hello correct path toohello **complete** folder, and then click **Next**.</span></span>

   ![Określ nazwę projektu hello][CL08]

1. <span data-ttu-id="52d68-131">Dostosowywanie wszelkich katalogów do zaimportowania, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="52d68-131">Customize any directories for importing, and then click **Next**.</span></span>

   ![Wybierz katalogów][CL09]

1. <span data-ttu-id="52d68-133">Przejrzyj hello tooimport biblioteki, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="52d68-133">Review hello libraries tooimport, and then click **Next**.</span></span>

   ![Przegląd biblioteki projektu][CL10]

1. <span data-ttu-id="52d68-135">Przejrzyj hello struktury modułu, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="52d68-135">Review hello module structure, and then click **Next**.</span></span>

   ![Przejrzyj struktury modułu][CL11]

1. <span data-ttu-id="52d68-137">Określ użytkownika JDK, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="52d68-137">Specify your JDK, and then click **Next**.</span></span>

   ![Określ JDK][CL12]

1. <span data-ttu-id="52d68-139">Kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="52d68-139">Click **Finish**.</span></span>

   ![Przycisk Zakończ][CL13]

<span data-ttu-id="52d68-141">IntelliJ importuje hello rozruchu Spring aplikacji jako projekt i wyświetla struktury powitania po zakończeniu importowania hello.</span><span class="sxs-lookup"><span data-stu-id="52d68-141">IntelliJ imports hello Spring Boot app as a project and displays hello structure when hello import has finished.</span></span>

![Spring aplikacji rozruchu w IntelliJ][CL14]

## <a name="build-your-spring-boot-app"></a><span data-ttu-id="52d68-143">Tworzenie rozruchowych Spring aplikacji</span><span class="sxs-lookup"><span data-stu-id="52d68-143">Build your Spring Boot app</span></span>

### <a name="build-hello-app-by-using-hello-maven-pom"></a><span data-ttu-id="52d68-144">Tworzenie aplikacji hello przy użyciu hello Maven POM</span><span class="sxs-lookup"><span data-stu-id="52d68-144">Build hello app by using hello Maven POM</span></span>

1. <span data-ttu-id="52d68-145">Otwórz okno narzędzia Maven hello, jeśli nie jest już otwarty.</span><span class="sxs-lookup"><span data-stu-id="52d68-145">Open hello Maven tool window if it is not already opened.</span></span> <span data-ttu-id="52d68-146">Kliknij przycisk **widoku** > **narzędzia systemu Windows** > **projekty Maven**.</span><span class="sxs-lookup"><span data-stu-id="52d68-146">Click **View** > **Tool Windows** > **Maven Projects**.</span></span>

   ![Polecenia narzędzia Windows i projekty Maven][BU01]

1. <span data-ttu-id="52d68-148">W oknie narzędzia Maven hello, kliknij prawym przyciskiem myszy **pakietu** i wybierz **Uruchom kompilacja Maven**.</span><span class="sxs-lookup"><span data-stu-id="52d68-148">In hello Maven tool window, right-click **package** and select **Run Maven Build**.</span></span> <span data-ttu-id="52d68-149">(Jeśli projekt Maven nie występuje automatycznie, kliknij przycisk hello **ponownie zaimportować** ikonę na pasku narzędzi Maven hello.)</span><span class="sxs-lookup"><span data-stu-id="52d68-149">(If your Maven project does not show up automatically, click hello **Reimport** icon on hello Maven toolbar.)</span></span>

   ![Uruchom polecenie kompilacja Maven][BU02]

1. <span data-ttu-id="52d68-151">Powinna zostać wyświetlona IntelliJ **BUDOWANIE powiodło** podczas rozruchu Spring aplikacji został utworzony pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="52d68-151">IntelliJ should display a **BUILD SUCCESS** message when your Spring Boot app is successfully created.</span></span>

   ![Komunikat BUDOWANIE powiodło się][BU03]

### <a name="create-a-deployment-ready-artifact"></a><span data-ttu-id="52d68-153">Tworzenie artefaktu gotowe do wdrożenia</span><span class="sxs-lookup"><span data-stu-id="52d68-153">Create a deployment-ready artifact</span></span>

<span data-ttu-id="52d68-154">toopublish aplikacji Spring rozruchu, należy toocreate artefaktu gotowe do wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="52d68-154">toopublish your Spring Boot app, you need toocreate a deployment-ready artifact.</span></span> <span data-ttu-id="52d68-155">Użyj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="52d68-155">Use hello following steps:</span></span>

1. <span data-ttu-id="52d68-156">Otwórz projekt aplikacji sieci web w środowisko IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="52d68-156">Open your web app project in IntelliJ.</span></span>

1. <span data-ttu-id="52d68-157">Kliknij przycisk **pliku**, a następnie kliknij przycisk **struktury projektu**.</span><span class="sxs-lookup"><span data-stu-id="52d68-157">Click **File**, and then click **Project Structure**.</span></span>

   ![Struktura projekt — polecenie][ART01]

1. <span data-ttu-id="52d68-159">Kliknij zielony oraz hello (**+**) symboli tooadd artefaktu, kliknij przycisk **JAR**, a następnie kliknij przycisk **pusty**.</span><span class="sxs-lookup"><span data-stu-id="52d68-159">Click hello green plus (**+**) symbol tooadd an artifact, click **JAR**, and then click **Empty**.</span></span>

   ![Dodaj artefaktów][ART02]

1. <span data-ttu-id="52d68-161">Nazwa Twojej artefaktu pamiętając nie tooadd rozszerzenia "JAR" hello, a następnie określ hello folderu docelowego dla danych wyjściowych Maven powitalne.</span><span class="sxs-lookup"><span data-stu-id="52d68-161">Name your artifact while making sure not tooadd hello ".jar" extension, and then specify hello target folder for hello Maven output.</span></span>

   ![Określ właściwości artefaktów][ART03]

1. <span data-ttu-id="52d68-163">Tworzenie manifestu dla Twojego artefaktu (opcjonalnie):</span><span class="sxs-lookup"><span data-stu-id="52d68-163">Create a manifest for your artifact (optional):</span></span>

   <span data-ttu-id="52d68-164">a.</span><span class="sxs-lookup"><span data-stu-id="52d68-164">a.</span></span> <span data-ttu-id="52d68-165">Kliknij przycisk **tworzenie manifestu**.</span><span class="sxs-lookup"><span data-stu-id="52d68-165">Click **Create Manifest**.</span></span>

      ![Kliknij przycisk Utwórz manifestu hello][ART04a]

   <span data-ttu-id="52d68-167">b.</span><span class="sxs-lookup"><span data-stu-id="52d68-167">b.</span></span> <span data-ttu-id="52d68-168">Wybierz hello domyślną ścieżkę dla artefaktu hello, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="52d68-168">Choose hello default path for hello artifact, and then click **OK**.</span></span>

      ![Określ ścieżkę artefaktów][ART04b]

   <span data-ttu-id="52d68-170">c.</span><span class="sxs-lookup"><span data-stu-id="52d68-170">c.</span></span> <span data-ttu-id="52d68-171">Kliknij przycisk wielokropka hello (**...** ) klasy głównym hello toolocate.</span><span class="sxs-lookup"><span data-stu-id="52d68-171">Click hello ellipsis (**...**) toolocate hello main class.</span></span>

      ![Zlokalizuj klasy głównym][ART04c]

   <span data-ttu-id="52d68-173">d.</span><span class="sxs-lookup"><span data-stu-id="52d68-173">d.</span></span> <span data-ttu-id="52d68-174">Wybierz klasy głównym, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="52d68-174">Choose your main class, and then click **OK**.</span></span>

      ![Określ klasy głównym][ART04d]

1. <span data-ttu-id="52d68-176">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="52d68-176">Click **OK**.</span></span>

   ![Zamknij okno dialogowe hello struktury projektu][ART05]

> [!NOTE]
> <span data-ttu-id="52d68-178">Aby uzyskać więcej informacji na temat tworzenia artefaktów w IntelliJ, zobacz [Konfigurowanie artefakty] na powitania JetBrains witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="52d68-178">For more information about creating artifacts in IntelliJ, see [Configuring Artifacts] on hello JetBrains website.</span></span>
>

### <a name="build-hello-artifact-for-deployment"></a><span data-ttu-id="52d68-179">Tworzenie artefaktu hello wdrożenia</span><span class="sxs-lookup"><span data-stu-id="52d68-179">Build hello artifact for deployment</span></span>

1. <span data-ttu-id="52d68-180">Kliknij przycisk **kompilacji**, a następnie kliknij przycisk **artefakty**.</span><span class="sxs-lookup"><span data-stu-id="52d68-180">Click **Build**, and then click **Artifacts**.</span></span>

   ![Polecenie artefaktów kompilacji][BU04]

1. <span data-ttu-id="52d68-182">Gdy hello **artefaktów kompilacji** zostanie wyświetlone menu kontekstowego, kliknij przycisk **kompilacji**.</span><span class="sxs-lookup"><span data-stu-id="52d68-182">When hello **Build Artifact** context menu appears, click **Build**.</span></span>

   ![Tworzenie artefaktu menu kontekstowe][BU05]

<span data-ttu-id="52d68-184">IntelliJ artefaktu ukończyć powitalnych dla aplikacji rozruchu Spring powinien być wyświetlany w oknie narzędzia projektu hello.</span><span class="sxs-lookup"><span data-stu-id="52d68-184">IntelliJ should display hello completed artifact for your Spring Boot app in hello project tool window.</span></span>

   ![Utworzony artefaktów][BU06]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a><span data-ttu-id="52d68-186">Publikowanie tooAzure aplikacji sieci web przy użyciu kontenera Docker</span><span class="sxs-lookup"><span data-stu-id="52d68-186">Publish your web app tooAzure by using a Docker container</span></span>

1. <span data-ttu-id="52d68-187">Jeśli użytkownik nie ma zarejestrowany tooyour konto platformy Azure, wykonaj kroki hello w [logowania instrukcje dotyczące hello Azure Toolkit for IntelliJ][Azure Sign In for IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="52d68-187">If you have not signed in tooyour Azure account, follow hello steps in [Sign-in instructions for hello Azure Toolkit for IntelliJ][Azure Sign In for IntelliJ].</span></span>

1. <span data-ttu-id="52d68-188">W oknie narzędzia hello Eksplorator projektów kliknij prawym przyciskiem myszy projekt hello, a następnie wybierz **Azure** > **Publikuj jako kontener Docker**.</span><span class="sxs-lookup"><span data-stu-id="52d68-188">In hello Project Explorer tool window, right-click hello project, and then select **Azure** > **Publish as Docker Container**.</span></span>

   ![Publikuj jako polecenia w kontenerze Docker][PU01]

1. <span data-ttu-id="52d68-190">Gdy hello **wdrożenia kontenera Docker na platformie Azure** zostanie wyświetlone okno dialogowe, wyświetlane są wszystkie istniejące hosty Docker.</span><span class="sxs-lookup"><span data-stu-id="52d68-190">When hello **Deploy Docker Container on Azure** dialog box appears, any existing Docker hosts are displayed.</span></span> <span data-ttu-id="52d68-191">Jeśli wybierzesz toodeploy tooan istniejącą hosta, możesz pominąć toostep 4.</span><span class="sxs-lookup"><span data-stu-id="52d68-191">If you choose toodeploy tooan existing host, you can skip toostep 4.</span></span> <span data-ttu-id="52d68-192">W przeciwnym razie użyj hello następujące kroki toocreate hosta:</span><span class="sxs-lookup"><span data-stu-id="52d68-192">Otherwise, use hello following steps toocreate a host:</span></span>

   <span data-ttu-id="52d68-193">a.</span><span class="sxs-lookup"><span data-stu-id="52d68-193">a.</span></span> <span data-ttu-id="52d68-194">Kliknij zielony oraz hello (**+**) symbolu.</span><span class="sxs-lookup"><span data-stu-id="52d68-194">Click hello green plus (**+**) symbol.</span></span>

      ![Dodaj nowy host platformy Docker][PU02]

   <span data-ttu-id="52d68-196">b.</span><span class="sxs-lookup"><span data-stu-id="52d68-196">b.</span></span> <span data-ttu-id="52d68-197">Gdy hello **hostów Docker Utwórz** zostanie wyświetlone okno dialogowe, możesz wybrać domyślne hello tooaccept lub można określić wszystkie niestandardowe ustawienia dla nowego hosta platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="52d68-197">When hello **Create Docker Host** dialog box appears, you can choose tooaccept hello defaults, or you can specify any custom settings for your new Docker host.</span></span> <span data-ttu-id="52d68-198">(Aby uzyskać szczegółowe opisy hello różne ustawienia, zobacz [opublikować aplikację sieci web jako kontener Docker za pomocą hello Azure Toolkit for IntelliJ][Publish Container with Azure Toolkit].) Kliknij przycisk **dalej** po określeniu które toouse ustawienia.</span><span class="sxs-lookup"><span data-stu-id="52d68-198">(For detailed descriptions of hello various settings, see [Publish a web app as a Docker container by using hello Azure Toolkit for IntelliJ][Publish Container with Azure Toolkit].) Click **Next** when you have specified which settings toouse.</span></span>

      ![Określ opcje hostów Docker][PU03a]

   <span data-ttu-id="52d68-200">c.</span><span class="sxs-lookup"><span data-stu-id="52d68-200">c.</span></span> <span data-ttu-id="52d68-201">Możesz wybrać toouse istniejących poświadczeń logowania usługi Azure key vault lub tooenter można wybrać nowe poświadczenia logowania Docker.</span><span class="sxs-lookup"><span data-stu-id="52d68-201">You can choose toouse existing login credentials from an Azure key vault, or you can choose tooenter new Docker login credentials.</span></span> <span data-ttu-id="52d68-202">Kliknij przycisk **Zakończ** po określeniu opcji.</span><span class="sxs-lookup"><span data-stu-id="52d68-202">Click **Finish** when you have specified your options.</span></span>

      ![Określ poświadczenia hostów Docker][PU03b]

1. <span data-ttu-id="52d68-204">Wybierz hosta Docker, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="52d68-204">Select your Docker host, and then click **Next**.</span></span>

   ![Wybierz toouse hostów Docker hello][PU04]

1. <span data-ttu-id="52d68-206">Na ostatniej stronie powitania hello **wdrożenia kontenera Docker na platformie Azure** oknie dialogowym Określ hello następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="52d68-206">On hello last page of hello **Deploy Docker Container on Azure** dialog box, specify hello following options:</span></span>

   <span data-ttu-id="52d68-207">a.</span><span class="sxs-lookup"><span data-stu-id="52d68-207">a.</span></span> <span data-ttu-id="52d68-208">Można wybrać toospecify niestandardową nazwę kontenera hello, który będzie obsługiwał z kontenera Docker lub możesz zaakceptować domyślną hello.</span><span class="sxs-lookup"><span data-stu-id="52d68-208">You can choose toospecify a custom name for hello container that will host your Docker container, or you can accept hello default.</span></span>

   <span data-ttu-id="52d68-209">b.</span><span class="sxs-lookup"><span data-stu-id="52d68-209">b.</span></span> <span data-ttu-id="52d68-210">Wprowadź porty TCP powitania dla hosta docker przy użyciu składni hello: *[portu zewnętrznego]*:*[wewnętrznego portu]*.</span><span class="sxs-lookup"><span data-stu-id="52d68-210">Enter hello TCP ports for your docker host by using hello following syntax: *[external port]*:*[internal port]*.</span></span> <span data-ttu-id="52d68-211">Na przykład **80:8080** określa zewnętrznego portu 80 i hello domyślnego wewnętrzny rozruchu Spring portu 8080.</span><span class="sxs-lookup"><span data-stu-id="52d68-211">For example, **80:8080** specifies an external port of 80 and hello default internal Spring Boot port of 8080.</span></span>
   
      <span data-ttu-id="52d68-212">Jeśli dostosowano wewnętrzny port (na przykład, edytując plik application.yml hello), należy numer portu hello toospecify dla hello poprawne toooccur routingu na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="52d68-212">If you have customized your internal port (for example, by editing hello application.yml file), you need toospecify hello port number for hello correct routing toooccur in Azure.</span></span>

   <span data-ttu-id="52d68-213">c.</span><span class="sxs-lookup"><span data-stu-id="52d68-213">c.</span></span> <span data-ttu-id="52d68-214">Po skonfigurowaniu tych opcji, kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="52d68-214">After you have configured these options, click **Finish**.</span></span>

   ![Wdrażanie kontenera Docker na platformie Azure][PU05]

1. <span data-ttu-id="52d68-216">Po zakończeniu publikowania hello Azure Toolkit hello Wyświetla dziennika aktywności platformy Azure **opublikowano** hello stanu.</span><span class="sxs-lookup"><span data-stu-id="52d68-216">When hello Azure Toolkit has finished publishing, hello Azure Activity Log displays **Published** for hello status.</span></span>

   ![Pomyślnie wdrożono hostów Docker][PU06]

## <a name="next-steps"></a><span data-ttu-id="52d68-218">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="52d68-218">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<span data-ttu-id="52d68-219">toolearn o dodatkowe metody do tworzenia aplikacji Spring rozruch przy użyciu IntelliJ, zobacz [tworzenia projektów rozruchu Spring](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) na powitania JetBrains witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="52d68-219">toolearn about additional methods for creating Spring Boot apps by using IntelliJ, see [Creating Spring Boot Projects](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) on hello JetBrains website.</span></span>

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Sign In for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Konfigurowanie artefakty]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html
[Deploy Spring Boot on Linux in ACS]:container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[rozruchu Spring]: http://projects.spring.io/spring-boot/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[CL01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL01.png
[CL02a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02a.png
[CL02b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02b.png
[CL03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL03.png
[CL04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL04.png
[CL05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL05.png
[CL06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL06.png
[CL07]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL07.png
[CL08]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL08.png
[CL09]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL09.png
[CL10]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL10.png
[CL11]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL11.png
[CL12]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL12.png
[CL13]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL13.png
[CL14]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL14.png

[ART01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART01.png
[ART02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART02.png
[ART03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART03.png
[ART04a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04a.png
[ART04b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04b.png
[ART04c]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04c.png
[ART04d]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04d.png
[ART05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART05.png

[BU01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU01.png
[BU02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU02.png
[BU03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU03.png
[BU04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU04.png
[BU05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU05.png
[BU06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU06.png

[PU01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU01.png
[PU02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU02.png
[PU03a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03a.png
[PU03b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03b.png
[PU04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU04.png
[PU05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU05.png
[PU06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU06.png
