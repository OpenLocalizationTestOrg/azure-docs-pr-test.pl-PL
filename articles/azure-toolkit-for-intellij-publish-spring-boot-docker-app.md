---
title: "Publikowania aplikacji rozruchu Spring jako kontener Docker przy użyciu zestawu narzędzi platformy Azure dla IntelliJ | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak opublikować aplikację sieci web do systemu Microsoft Azure jako kontener Docker za pomocą narzędzi Azure for IntelliJ."
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
ms.openlocfilehash: b771238934183c953615ac33c42a275d80657556
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-the-azure-toolkit-for-intellij"></a><span data-ttu-id="3095a-103">Publikowania aplikacji rozruchu Spring jako kontener Docker przy użyciu zestawu narzędzi platformy Azure dla IntelliJ</span><span class="sxs-lookup"><span data-stu-id="3095a-103">Publish a Spring Boot app as a Docker container by using the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="3095a-104">[Spring Framework] to rozwiązanie open source, które pomaga deweloperom języka Java, tworzenie aplikacji na poziomie przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="3095a-104">The [Spring Framework] is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="3095a-105">Jeden z popularnych więcej projektów, które jest wbudowane znajdujący się na platformy jest [rozruchu Spring], zapewniające uproszczone podejście do tworzenia autonomicznych aplikacji Java.</span><span class="sxs-lookup"><span data-stu-id="3095a-105">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating standalone Java applications.</span></span>

<span data-ttu-id="3095a-106">[Docker] jest to rozwiązanie open source, które pomaga deweloperom automatyzację wdrażania, skalowania i zarządzania ich aplikacji, które są uruchomione w kontenerach.</span><span class="sxs-lookup"><span data-stu-id="3095a-106">[Docker] is an open-source solution that helps developers automate the deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="3095a-107">Ten samouczek przedstawia kroki wdrażania aplikacji rozruchu Spring jako kontener Docker do systemu Microsoft Azure przy użyciu zestawu narzędzi platformy Azure dla IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="3095a-107">This tutorial walks you through the steps to deploy a Spring Boot application as a Docker container to Microsoft Azure by using the Azure Toolkit for IntelliJ.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="clone-the-default-spring-boot-docker-repo"></a><span data-ttu-id="3095a-108">Sklonuj repozytorium Docker rozruchu Spring domyślne</span><span class="sxs-lookup"><span data-stu-id="3095a-108">Clone the default Spring Boot Docker repo</span></span>

<span data-ttu-id="3095a-109">W poniższych krokach objaśniono przez klonowanie repozytorium Spring Docker rozruch przy użyciu IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="3095a-109">The following steps walk you through cloning the Spring Boot Docker repo by using IntelliJ.</span></span> <span data-ttu-id="3095a-110">Jeśli chcesz użyć wiersza polecenia, zobacz [wdrażanie aplikacji Spring rozruchu w systemie Linux w usłudze kontenera platformy Azure][Deploy Spring Boot on Linux in ACS].</span><span class="sxs-lookup"><span data-stu-id="3095a-110">If you want to use a command line, see [Deploy a Spring Boot application on Linux in Azure Container Service][Deploy Spring Boot on Linux in ACS].</span></span>

1. <span data-ttu-id="3095a-111">Otwórz środowisko IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="3095a-111">Open IntelliJ.</span></span>

1. <span data-ttu-id="3095a-112">Na ekranie powitalnym zaznacz **GitHub** opcji **wyewidencjonowania z kontroli wersji** listy.</span><span class="sxs-lookup"><span data-stu-id="3095a-112">On the welcome screen, select the **GitHub** option in the **Check out from Version Control** list.</span></span>

   ![Opcja GitHub kontroli wersji][CL01]

1. <span data-ttu-id="3095a-114">Jeśli zostanie wyświetlony monit, aby się zalogować, wprowadź swoje poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="3095a-114">Enter your credentials if you are prompted to log in.</span></span>

   * <span data-ttu-id="3095a-115">Jeśli używane są nazwy użytkownika i hasła do logowania witrynie GitHub:</span><span class="sxs-lookup"><span data-stu-id="3095a-115">If you are using a username/password to log in to GitHub:</span></span>

      ![Okno dialogowe wprowadzanie GitHub nazwy użytkownika i hasła][CL02a]

   * <span data-ttu-id="3095a-117">Jeśli używasz tokenu do logowania witrynie GitHub:</span><span class="sxs-lookup"><span data-stu-id="3095a-117">If you are using a token to log in to GitHub:</span></span>

      ![Okno dialogowe wprowadzanie GitHub token][CL02b]

1. <span data-ttu-id="3095a-119">Wprowadź **https://github.com/spring-guides/gs-spring-boot-docker.git** dla adresu URL repozytorium, określ informacje o Twoich ścieżka lokalna i folder, a następnie kliknij przycisk **klonowania**.</span><span class="sxs-lookup"><span data-stu-id="3095a-119">Enter **https://github.com/spring-guides/gs-spring-boot-docker.git** for the repo URL, specify your local path and folder information, and then click **Clone**.</span></span>

   ![Okno dialogowe klonowanie repozytorium][CL03]

1. <span data-ttu-id="3095a-121">Po wyświetleniu monitu, aby utworzyć projekt IntelliJ, wybierz **nr**.</span><span class="sxs-lookup"><span data-stu-id="3095a-121">When you're prompted to create an IntelliJ project, select **No**.</span></span>

   ![Odrzucanie do tworzenia projektu IntelliJ][CL04]

1. <span data-ttu-id="3095a-123">Na stronie powitalnej kliknij **Importowanie projektu**.</span><span class="sxs-lookup"><span data-stu-id="3095a-123">On the welcome page, click **Import Project**.</span></span>

   ![Wybór projektu importu][CL05]

1. <span data-ttu-id="3095a-125">Znajdź ścieżki, gdzie sklonować repozytorium Spring rozruchu, wybierz **pełną** folderu głównego, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="3095a-125">Locate the path where you cloned the Spring Boot repo, select the **complete** folder under the root, and then click **OK**.</span></span>

   ![Wybierz folder do zaimportowania][CL06]

1. <span data-ttu-id="3095a-127">Po wyświetleniu monitu wybierz **Tworzenie projektu z istniejących źródeł**.</span><span class="sxs-lookup"><span data-stu-id="3095a-127">When you're prompted, select **Create project from existing sources**.</span></span>

   ![Opcję, aby utworzyć projekt z istniejących źródeł][CL07]

1. <span data-ttu-id="3095a-129">Określ nazwę projektu lub zaakceptuj wartość domyślną, Sprawdź poprawną ścieżkę do **pełną** folder, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="3095a-129">Specify your project name or accept the default, verify the correct path to the **complete** folder, and then click **Next**.</span></span>

   ![Określ nazwę projektu][CL08]

1. <span data-ttu-id="3095a-131">Dostosowywanie wszelkich katalogów do zaimportowania, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="3095a-131">Customize any directories for importing, and then click **Next**.</span></span>

   ![Wybierz katalogów][CL09]

1. <span data-ttu-id="3095a-133">Przegląd biblioteki do zaimportowania, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="3095a-133">Review the libraries to import, and then click **Next**.</span></span>

   ![Przegląd biblioteki projektu][CL10]

1. <span data-ttu-id="3095a-135">Przejrzyj struktury modułu, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="3095a-135">Review the module structure, and then click **Next**.</span></span>

   ![Przejrzyj struktury modułu][CL11]

1. <span data-ttu-id="3095a-137">Określ użytkownika JDK, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="3095a-137">Specify your JDK, and then click **Next**.</span></span>

   ![Określ JDK][CL12]

1. <span data-ttu-id="3095a-139">Kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="3095a-139">Click **Finish**.</span></span>

   ![Przycisk Zakończ][CL13]

<span data-ttu-id="3095a-141">IntelliJ importuje aplikacji rozruchu Spring jako projekt i wyświetla strukturę po zakończeniu importowania.</span><span class="sxs-lookup"><span data-stu-id="3095a-141">IntelliJ imports the Spring Boot app as a project and displays the structure when the import has finished.</span></span>

![Spring aplikacji rozruchu w IntelliJ][CL14]

## <a name="build-your-spring-boot-app"></a><span data-ttu-id="3095a-143">Tworzenie rozruchowych Spring aplikacji</span><span class="sxs-lookup"><span data-stu-id="3095a-143">Build your Spring Boot app</span></span>

### <a name="build-the-app-by-using-the-maven-pom"></a><span data-ttu-id="3095a-144">Tworzenie aplikacji przy użyciu Maven POM</span><span class="sxs-lookup"><span data-stu-id="3095a-144">Build the app by using the Maven POM</span></span>

1. <span data-ttu-id="3095a-145">Otwórz okno narzędzia Maven, jeśli nie jest już otwarty.</span><span class="sxs-lookup"><span data-stu-id="3095a-145">Open the Maven tool window if it is not already opened.</span></span> <span data-ttu-id="3095a-146">Kliknij przycisk **widoku** > **narzędzia systemu Windows** > **projekty Maven**.</span><span class="sxs-lookup"><span data-stu-id="3095a-146">Click **View** > **Tool Windows** > **Maven Projects**.</span></span>

   ![Polecenia narzędzia Windows i projekty Maven][BU01]

1. <span data-ttu-id="3095a-148">W oknie narzędzia Maven, kliknij prawym przyciskiem myszy **pakietu** i wybierz **Uruchom kompilacja Maven**.</span><span class="sxs-lookup"><span data-stu-id="3095a-148">In the Maven tool window, right-click **package** and select **Run Maven Build**.</span></span> <span data-ttu-id="3095a-149">(Jeśli projekt Maven nie występuje automatycznie, kliknij przycisk **ponownie zaimportować** ikonę na pasku narzędzi Maven.)</span><span class="sxs-lookup"><span data-stu-id="3095a-149">(If your Maven project does not show up automatically, click the **Reimport** icon on the Maven toolbar.)</span></span>

   ![Uruchom polecenie kompilacja Maven][BU02]

1. <span data-ttu-id="3095a-151">Powinna zostać wyświetlona IntelliJ **BUDOWANIE powiodło** podczas rozruchu Spring aplikacji został utworzony pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="3095a-151">IntelliJ should display a **BUILD SUCCESS** message when your Spring Boot app is successfully created.</span></span>

   ![Komunikat BUDOWANIE powiodło się][BU03]

### <a name="create-a-deployment-ready-artifact"></a><span data-ttu-id="3095a-153">Tworzenie artefaktu gotowe do wdrożenia</span><span class="sxs-lookup"><span data-stu-id="3095a-153">Create a deployment-ready artifact</span></span>

<span data-ttu-id="3095a-154">Aby opublikować aplikację Spring rozruchu, należy utworzyć artefaktu gotowe do wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="3095a-154">To publish your Spring Boot app, you need to create a deployment-ready artifact.</span></span> <span data-ttu-id="3095a-155">Wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="3095a-155">Use the following steps:</span></span>

1. <span data-ttu-id="3095a-156">Otwórz projekt aplikacji sieci web w środowisko IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="3095a-156">Open your web app project in IntelliJ.</span></span>

1. <span data-ttu-id="3095a-157">Kliknij przycisk **pliku**, a następnie kliknij przycisk **struktury projektu**.</span><span class="sxs-lookup"><span data-stu-id="3095a-157">Click **File**, and then click **Project Structure**.</span></span>

   ![Struktura projekt — polecenie][ART01]

1. <span data-ttu-id="3095a-159">Kliknij zielony plus (**+**) symbolu, aby dodać artefaktu, kliknij polecenie **JAR**, a następnie kliknij przycisk **pusty**.</span><span class="sxs-lookup"><span data-stu-id="3095a-159">Click the green plus (**+**) symbol to add an artifact, click **JAR**, and then click **Empty**.</span></span>

   ![Dodaj artefaktów][ART02]

1. <span data-ttu-id="3095a-161">Nazwa użytkownika artefaktu pamiętając nie można dodać rozszerzenia "JAR", a następnie określ folder docelowy dla danych wyjściowych Maven.</span><span class="sxs-lookup"><span data-stu-id="3095a-161">Name your artifact while making sure not to add the ".jar" extension, and then specify the target folder for the Maven output.</span></span>

   ![Określ właściwości artefaktów][ART03]

1. <span data-ttu-id="3095a-163">Tworzenie manifestu dla Twojego artefaktu (opcjonalnie):</span><span class="sxs-lookup"><span data-stu-id="3095a-163">Create a manifest for your artifact (optional):</span></span>

   <span data-ttu-id="3095a-164">a.</span><span class="sxs-lookup"><span data-stu-id="3095a-164">a.</span></span> <span data-ttu-id="3095a-165">Kliknij przycisk **tworzenie manifestu**.</span><span class="sxs-lookup"><span data-stu-id="3095a-165">Click **Create Manifest**.</span></span>

      ![Kliknij przycisk Utwórz manifestu][ART04a]

   <span data-ttu-id="3095a-167">b.</span><span class="sxs-lookup"><span data-stu-id="3095a-167">b.</span></span> <span data-ttu-id="3095a-168">Wybierz domyślną ścieżkę dla artefaktu, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="3095a-168">Choose the default path for the artifact, and then click **OK**.</span></span>

      ![Określ ścieżkę artefaktów][ART04b]

   <span data-ttu-id="3095a-170">c.</span><span class="sxs-lookup"><span data-stu-id="3095a-170">c.</span></span> <span data-ttu-id="3095a-171">Kliknij przycisk wielokropka (**...** ) można znaleźć klasy głównym.</span><span class="sxs-lookup"><span data-stu-id="3095a-171">Click the ellipsis (**...**) to locate the main class.</span></span>

      ![Zlokalizuj klasy głównym][ART04c]

   <span data-ttu-id="3095a-173">d.</span><span class="sxs-lookup"><span data-stu-id="3095a-173">d.</span></span> <span data-ttu-id="3095a-174">Wybierz klasy głównym, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="3095a-174">Choose your main class, and then click **OK**.</span></span>

      ![Określ klasy głównym][ART04d]

1. <span data-ttu-id="3095a-176">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="3095a-176">Click **OK**.</span></span>

   ![Zamknij okno dialogowe struktury projektu][ART05]

> [!NOTE]
> <span data-ttu-id="3095a-178">Aby uzyskać więcej informacji na temat tworzenia artefaktów w IntelliJ, zobacz [Konfigurowanie artefakty] na JetBrains witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="3095a-178">For more information about creating artifacts in IntelliJ, see [Configuring Artifacts] on the JetBrains website.</span></span>
>

### <a name="build-the-artifact-for-deployment"></a><span data-ttu-id="3095a-179">Tworzenie artefaktu dla wdrożenia</span><span class="sxs-lookup"><span data-stu-id="3095a-179">Build the artifact for deployment</span></span>

1. <span data-ttu-id="3095a-180">Kliknij przycisk **kompilacji**, a następnie kliknij przycisk **artefakty**.</span><span class="sxs-lookup"><span data-stu-id="3095a-180">Click **Build**, and then click **Artifacts**.</span></span>

   ![Polecenie artefaktów kompilacji][BU04]

1. <span data-ttu-id="3095a-182">Gdy **artefaktów kompilacji** zostanie wyświetlone menu kontekstowego, kliknij przycisk **kompilacji**.</span><span class="sxs-lookup"><span data-stu-id="3095a-182">When the **Build Artifact** context menu appears, click **Build**.</span></span>

   ![Tworzenie artefaktu menu kontekstowe][BU05]

<span data-ttu-id="3095a-184">IntelliJ ukończone artefaktu dla aplikacji rozruchu Spring powinien być wyświetlany w oknie narzędzia projektu.</span><span class="sxs-lookup"><span data-stu-id="3095a-184">IntelliJ should display the completed artifact for your Spring Boot app in the project tool window.</span></span>

   ![Utworzony artefaktów][BU06]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a><span data-ttu-id="3095a-186">Publikowanie aplikacji sieci web na platformie Azure przy użyciu kontenera Docker</span><span class="sxs-lookup"><span data-stu-id="3095a-186">Publish your web app to Azure by using a Docker container</span></span>

1. <span data-ttu-id="3095a-187">Jeśli użytkownik nie ma zalogowany do konta platformy Azure, postępuj zgodnie z instrukcjami [logowania instrukcje dotyczące zestawu narzędzi Azure for IntelliJ][Azure Sign In for IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="3095a-187">If you have not signed in to your Azure account, follow the steps in [Sign-in instructions for the Azure Toolkit for IntelliJ][Azure Sign In for IntelliJ].</span></span>

1. <span data-ttu-id="3095a-188">W oknie narzędzia Eksplorator projektów kliknij prawym przyciskiem myszy projekt, a następnie wybierz **Azure** > **Publikuj jako kontener Docker**.</span><span class="sxs-lookup"><span data-stu-id="3095a-188">In the Project Explorer tool window, right-click the project, and then select **Azure** > **Publish as Docker Container**.</span></span>

   ![Publikuj jako polecenia w kontenerze Docker][PU01]

1. <span data-ttu-id="3095a-190">Gdy **wdrożenia kontenera Docker na platformie Azure** zostanie wyświetlone okno dialogowe, wyświetlane są wszystkie istniejące hosty Docker.</span><span class="sxs-lookup"><span data-stu-id="3095a-190">When the **Deploy Docker Container on Azure** dialog box appears, any existing Docker hosts are displayed.</span></span> <span data-ttu-id="3095a-191">Jeśli chcesz wdrożyć istniejącą hosta można przejdź do kroku 4.</span><span class="sxs-lookup"><span data-stu-id="3095a-191">If you choose to deploy to an existing host, you can skip to step 4.</span></span> <span data-ttu-id="3095a-192">W przeciwnym razie wykonaj następujące kroki, aby utworzyć hosta:</span><span class="sxs-lookup"><span data-stu-id="3095a-192">Otherwise, use the following steps to create a host:</span></span>

   <span data-ttu-id="3095a-193">a.</span><span class="sxs-lookup"><span data-stu-id="3095a-193">a.</span></span> <span data-ttu-id="3095a-194">Kliknij przycisk plus zielony (**+**) symbolu.</span><span class="sxs-lookup"><span data-stu-id="3095a-194">Click the green plus (**+**) symbol.</span></span>

      ![Dodaj nowy host platformy Docker][PU02]

   <span data-ttu-id="3095a-196">b.</span><span class="sxs-lookup"><span data-stu-id="3095a-196">b.</span></span> <span data-ttu-id="3095a-197">Gdy **hostów Docker Utwórz** zostanie wyświetlone okno dialogowe, użytkownik może zaakceptować wartości domyślne lub można określić wszystkie niestandardowe ustawienia dla nowego hosta platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="3095a-197">When the **Create Docker Host** dialog box appears, you can choose to accept the defaults, or you can specify any custom settings for your new Docker host.</span></span> <span data-ttu-id="3095a-198">(Aby uzyskać szczegółowe opisy różnych ustawień, zobacz [opublikować aplikację sieci web jako kontener Docker za pomocą narzędzi Azure for IntelliJ][Publish Container with Azure Toolkit].) Kliknij przycisk **dalej** po określeniu ustawień.</span><span class="sxs-lookup"><span data-stu-id="3095a-198">(For detailed descriptions of the various settings, see [Publish a web app as a Docker container by using the Azure Toolkit for IntelliJ][Publish Container with Azure Toolkit].) Click **Next** when you have specified which settings to use.</span></span>

      ![Określ opcje hostów Docker][PU03a]

   <span data-ttu-id="3095a-200">c.</span><span class="sxs-lookup"><span data-stu-id="3095a-200">c.</span></span> <span data-ttu-id="3095a-201">Istnieje możliwość używania istniejących poświadczeń logowania z usługi Azure key vault, lub użytkownik może wprowadzić nowe poświadczenia logowania Docker.</span><span class="sxs-lookup"><span data-stu-id="3095a-201">You can choose to use existing login credentials from an Azure key vault, or you can choose to enter new Docker login credentials.</span></span> <span data-ttu-id="3095a-202">Kliknij przycisk **Zakończ** po określeniu opcji.</span><span class="sxs-lookup"><span data-stu-id="3095a-202">Click **Finish** when you have specified your options.</span></span>

      ![Określ poświadczenia hostów Docker][PU03b]

1. <span data-ttu-id="3095a-204">Wybierz hosta Docker, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="3095a-204">Select your Docker host, and then click **Next**.</span></span>

   ![Wybierz host Docker do użycia][PU04]

1. <span data-ttu-id="3095a-206">Na ostatniej stronie **wdrożenia kontenera Docker na platformie Azure** oknie dialogowym określ następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="3095a-206">On the last page of the **Deploy Docker Container on Azure** dialog box, specify the following options:</span></span>

   <span data-ttu-id="3095a-207">a.</span><span class="sxs-lookup"><span data-stu-id="3095a-207">a.</span></span> <span data-ttu-id="3095a-208">Użytkownik może określić niestandardową nazwę kontenera, który będzie hostem z kontenera Docker lub zaakceptować ustawienia domyślne.</span><span class="sxs-lookup"><span data-stu-id="3095a-208">You can choose to specify a custom name for the container that will host your Docker container, or you can accept the default.</span></span>

   <span data-ttu-id="3095a-209">b.</span><span class="sxs-lookup"><span data-stu-id="3095a-209">b.</span></span> <span data-ttu-id="3095a-210">Wprowadź porty TCP dla hosta docker przy użyciu następującej składni: *[portu zewnętrznego]*:*[wewnętrznego portu]*.</span><span class="sxs-lookup"><span data-stu-id="3095a-210">Enter the TCP ports for your docker host by using the following syntax: *[external port]*:*[internal port]*.</span></span> <span data-ttu-id="3095a-211">Na przykład **80:8080** określa zewnętrznego portu 80 oraz domyślnego portu rozruchu Spring wewnętrzny 8080.</span><span class="sxs-lookup"><span data-stu-id="3095a-211">For example, **80:8080** specifies an external port of 80 and the default internal Spring Boot port of 8080.</span></span>
   
      <span data-ttu-id="3095a-212">Jeśli dostosowano wewnętrzny port (na przykład, edytując plik application.yml), należy określić numer portu dla poprawne routingu w usłudze Azure.</span><span class="sxs-lookup"><span data-stu-id="3095a-212">If you have customized your internal port (for example, by editing the application.yml file), you need to specify the port number for the correct routing to occur in Azure.</span></span>

   <span data-ttu-id="3095a-213">c.</span><span class="sxs-lookup"><span data-stu-id="3095a-213">c.</span></span> <span data-ttu-id="3095a-214">Po skonfigurowaniu tych opcji, kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="3095a-214">After you have configured these options, click **Finish**.</span></span>

   ![Wdrażanie kontenera Docker na platformie Azure][PU05]

1. <span data-ttu-id="3095a-216">Po zakończeniu publikowania narzędzi Azure dziennika aktywności platformy Azure Wyświetla **opublikowano** stanu.</span><span class="sxs-lookup"><span data-stu-id="3095a-216">When the Azure Toolkit has finished publishing, the Azure Activity Log displays **Published** for the status.</span></span>

   ![Pomyślnie wdrożono hostów Docker][PU06]

## <a name="next-steps"></a><span data-ttu-id="3095a-218">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3095a-218">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<span data-ttu-id="3095a-219">Informacje na temat dodatkowych metod do tworzenia aplikacji Spring rozruch przy użyciu IntelliJ, zobacz [tworzenia projektów rozruchu Spring](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) na JetBrains witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="3095a-219">To learn about additional methods for creating Spring Boot apps by using IntelliJ, see [Creating Spring Boot Projects](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) on the JetBrains website.</span></span>

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Sign In for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
<span data-ttu-id="3095a-220">[Konfigurowanie artefakty]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html</span><span class="sxs-lookup"><span data-stu-id="3095a-220">[Configuring Artifacts]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html</span></span>
[Deploy Spring Boot on Linux in ACS]:container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md
<span data-ttu-id="3095a-221">[Docker]: https://www.docker.com/</span><span class="sxs-lookup"><span data-stu-id="3095a-221">[Docker]: https://www.docker.com/</span></span>
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
<span data-ttu-id="3095a-222">[rozruchu Spring]: http://projects.spring.io/spring-boot/</span><span class="sxs-lookup"><span data-stu-id="3095a-222">[Spring Boot]: http://projects.spring.io/spring-boot/</span></span>
<span data-ttu-id="3095a-223">[Spring Framework]: https://spring.io/</span><span class="sxs-lookup"><span data-stu-id="3095a-223">[Spring Framework]: https://spring.io/</span></span>

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
