---
title: "Publikowanie kontenera Docker przy użyciu zestawu narzędzi platformy Azure dla programu Eclipse | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak opublikować aplikację sieci web do systemu Microsoft Azure jako kontener Docker przy użyciu zestawu narzędzi platformy Azure dla programu Eclipse."
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
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 746bb0a073396b84fa8592adda6748a2a5692ee8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="530ff-103">Publikowanie aplikacji sieci web jako kontener Docker przy użyciu zestawu narzędzi platformy Azure dla programu Eclipse</span><span class="sxs-lookup"><span data-stu-id="530ff-103">Publish a web app as a Docker container by using the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="530ff-104">Kontenery docker jest powszechnie używaną metodą wdrażania aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="530ff-104">Docker containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="530ff-105">Przy użyciu rozwiązania Docker kontenerów, deweloperzy mogą konsolidację wszystkie pliki projektu i zależności w jeden pakiet do wdrożenia na serwerze.</span><span class="sxs-lookup"><span data-stu-id="530ff-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment to a server.</span></span> <span data-ttu-id="530ff-106">Zestaw narzędzi platformy Azure dla programu Eclipse ułatwia ten proces dla deweloperów języka Java, dodając *Publikuj jako kontener Docker* funkcji dla wdrożenia do systemu Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="530ff-106">The Azure Toolkit for Eclipse simplifies this process for Java developers by adding *Publish as Docker Container* features for deployment to Microsoft Azure.</span></span> <span data-ttu-id="530ff-107">W tym artykule przedstawiono kroki wymagane do publikowania aplikacji na platformie Azure jako kontenery Docker.</span><span class="sxs-lookup"><span data-stu-id="530ff-107">This article walks you through the steps required to publish your applications to Azure as Docker containers.</span></span>

> [!NOTE]
> <span data-ttu-id="530ff-108">Więcej informacji na temat rozwiązania Docker jest dostępna na [Docker witryny sieci Web].</span><span class="sxs-lookup"><span data-stu-id="530ff-108">More information about Docker is available on the [Docker website].</span></span>
>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a><span data-ttu-id="530ff-109">Publikowanie aplikacji sieci web na platformie Azure przy użyciu kontenera Docker</span><span class="sxs-lookup"><span data-stu-id="530ff-109">Publish your web app to Azure by using a Docker container</span></span>

1. <span data-ttu-id="530ff-110">Otwórz projekt aplikacji sieci web w programie Eclipse.</span><span class="sxs-lookup"><span data-stu-id="530ff-110">Open your web app project in Eclipse.</span></span>

2. <span data-ttu-id="530ff-111">Aby uruchomić **Publikuj jako kontener Docker** kreatora, wykonaj jedną z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="530ff-111">To start the **Publish as Docker Container** wizard, do either of the following:</span></span>

   * <span data-ttu-id="530ff-112">W **Nawigator** wyświetlić, kliknij prawym przyciskiem myszy projekt, kliknij przycisk **Azure**, a następnie kliknij przycisk **Publikuj jako kontener Docker**.</span><span class="sxs-lookup"><span data-stu-id="530ff-112">In the **Navigator** view, right-click your project, click **Azure**, and then click **Publish as Docker Container**.</span></span>

      ![Nawigator widoku Publikuj jako polecenia w kontenerze Docker][PUB01]

   * <span data-ttu-id="530ff-114">Na pasku narzędzi Eclipse kliknij **publikowania** przycisk, a następnie kliknij przycisk **Publikuj jako kontener Docker**.</span><span class="sxs-lookup"><span data-stu-id="530ff-114">On the Eclipse toolbar, click the **Publish** button, and then click **Publish as Docker Container**.</span></span>

      ![Pasek narzędzi Eclipse Publikuj jako polecenia w kontenerze Docker][PUB02]
      
    <span data-ttu-id="530ff-116">**Wdrożenia kontenera Docker na platformie Azure** zostanie otwarty Kreator.</span><span class="sxs-lookup"><span data-stu-id="530ff-116">The **Deploy Docker Container on Azure** wizard opens.</span></span>

    ![Kontener Docker wdrażanie w Kreatorze Azure][PUB03]

3. <span data-ttu-id="530ff-118">W **wpisz nazwę obrazu, wybierz artefakt ścieżkę i sprawdź Docker hosta do użycia** okna, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="530ff-118">In the **Type an image name, select the artifact's path and check a Docker host to be used** window, do the following:</span></span>

    <span data-ttu-id="530ff-119">a.</span><span class="sxs-lookup"><span data-stu-id="530ff-119">a.</span></span> <span data-ttu-id="530ff-120">W **nazwa obrazu Docker** wprowadź unikatową nazwę hosta Docker.</span><span class="sxs-lookup"><span data-stu-id="530ff-120">In the **Docker image name** box, enter a unique name for your Docker host.</span></span> <span data-ttu-id="530ff-121">(Kreator automatycznie tworzy nazwę, ale można go zmodyfikować).</span><span class="sxs-lookup"><span data-stu-id="530ff-121">(The wizard automatically creates a name, but you can modify it.)</span></span>

    <span data-ttu-id="530ff-122">b.</span><span class="sxs-lookup"><span data-stu-id="530ff-122">b.</span></span> <span data-ttu-id="530ff-123">**Hostów** obszar Wyświetla wszystkich hostach Docker, które zostały już utworzone.</span><span class="sxs-lookup"><span data-stu-id="530ff-123">The **Hosts** area displays any Docker hosts that you have already created.</span></span> <span data-ttu-id="530ff-124">Wykonaj jedną z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="530ff-124">Do either of the following:</span></span>

    * <span data-ttu-id="530ff-125">Jeśli masz istniejącą hosta Docker można wdrożyć aplikację sieci web do niego.</span><span class="sxs-lookup"><span data-stu-id="530ff-125">If you have an existing Docker host, you can deploy your web app to it.</span></span>
    * <span data-ttu-id="530ff-126">Aby utworzyć nowy host platformy Docker, kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="530ff-126">To create a new Docker host, click **Add**.</span></span>  
      
    <span data-ttu-id="530ff-127">**Hostów Docker Utwórz** zostanie otwarte okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="530ff-127">The **Create Docker Host** dialog box opens.</span></span>

    ![Wdrażanie kontenera Docker w Kreatorze Azure][PUB04a]

4. <span data-ttu-id="530ff-129">W **skonfigurować nową maszynę wirtualną** okna, określ następujące opcje dla hosta Docker.</span><span class="sxs-lookup"><span data-stu-id="530ff-129">In the **Configure the new virtual machine** window, specify the following options for your Docker host.</span></span> <span data-ttu-id="530ff-130">(Kreator automatycznie generuje większość opcji dla Ciebie, ale można ich modyfikować.)</span><span class="sxs-lookup"><span data-stu-id="530ff-130">(The wizard automatically generates most of the options for you, but you can modify any of them.)</span></span>

   <span data-ttu-id="530ff-131">a.</span><span class="sxs-lookup"><span data-stu-id="530ff-131">a.</span></span> <span data-ttu-id="530ff-132">**Nazwa**: wprowadź unikatową nazwę hosta Docker.</span><span class="sxs-lookup"><span data-stu-id="530ff-132">**Name**: Enter a unique name for the Docker host.</span></span> <span data-ttu-id="530ff-133">(Go nie jest taka sama jak nazwa obrazu Docker określone wcześniej.)</span><span class="sxs-lookup"><span data-stu-id="530ff-133">(It is not the same as the Docker image name that you specified earlier.)</span></span>

   <span data-ttu-id="530ff-134">b.</span><span class="sxs-lookup"><span data-stu-id="530ff-134">b.</span></span> <span data-ttu-id="530ff-135">**Subskrypcja**: Wprowadź subskrypcji platformy Azure, której użyjesz dla hosta.</span><span class="sxs-lookup"><span data-stu-id="530ff-135">**Subscription**: Enter the Azure subscription that you use for your host.</span></span>

   <span data-ttu-id="530ff-136">c.</span><span class="sxs-lookup"><span data-stu-id="530ff-136">c.</span></span> <span data-ttu-id="530ff-137">**Region**: Wprowadź region geograficzny, w którym znajduje się na hoście.</span><span class="sxs-lookup"><span data-stu-id="530ff-137">**Region**: Enter the geographical region where your host is located.</span></span>

   <span data-ttu-id="530ff-138">d.</span><span class="sxs-lookup"><span data-stu-id="530ff-138">d.</span></span> <span data-ttu-id="530ff-139">Na **systemu operacyjnego hosta i rozmiar** karty:</span><span class="sxs-lookup"><span data-stu-id="530ff-139">On the **Host OS and Size** tab:</span></span>
     * <span data-ttu-id="530ff-140">**System operacyjny hosta**: Wprowadź system operacyjny dla maszyny wirtualnej, która zawiera hosta.</span><span class="sxs-lookup"><span data-stu-id="530ff-140">**Host OS**: Enter the operating system for the virtual machine that contains your host.</span></span>
     * <span data-ttu-id="530ff-141">**Rozmiar**: wprowadź rozmiar maszyn wirtualnych dla hosta.</span><span class="sxs-lookup"><span data-stu-id="530ff-141">**Size**: Enter the virtual-machine size for your host.</span></span>

   <span data-ttu-id="530ff-142">e.</span><span class="sxs-lookup"><span data-stu-id="530ff-142">e.</span></span> <span data-ttu-id="530ff-143">Na **grupy zasobów** karty:</span><span class="sxs-lookup"><span data-stu-id="530ff-143">On the **Resource Group** tab:</span></span>
     * <span data-ttu-id="530ff-144">**Nową grupę zasobów**: Utwórz nową grupę zasobów dla hosta.</span><span class="sxs-lookup"><span data-stu-id="530ff-144">**New resource group**: Create a new resource group for your host.</span></span>
     * <span data-ttu-id="530ff-145">**Istniejąca grupa zasobów**: Wprowadź istniejącą grupę zasobów z konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="530ff-145">**Existing resource group**: Enter an existing resource group from your Azure account.</span></span>

   <span data-ttu-id="530ff-146">f.</span><span class="sxs-lookup"><span data-stu-id="530ff-146">f.</span></span> <span data-ttu-id="530ff-147">Na **sieci** karty:</span><span class="sxs-lookup"><span data-stu-id="530ff-147">On the **Network** tab:</span></span>
     * <span data-ttu-id="530ff-148">**Nowa sieć wirtualna**: Utwórz nową sieć wirtualną dla hosta.</span><span class="sxs-lookup"><span data-stu-id="530ff-148">**New virtual network**: Create a new virtual network for your host.</span></span>
     * <span data-ttu-id="530ff-149">**Istniejącej sieci wirtualnej**: Wprowadź istniejącą sieć wirtualną z konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="530ff-149">**Existing virtual network**: Enter an existing virtual network from your Azure account.</span></span>

   <span data-ttu-id="530ff-150">g.</span><span class="sxs-lookup"><span data-stu-id="530ff-150">g.</span></span> <span data-ttu-id="530ff-151">Na **magazynu** karty:</span><span class="sxs-lookup"><span data-stu-id="530ff-151">On the **Storage** tab:</span></span>
     * <span data-ttu-id="530ff-152">**Nowe konto magazynu**: Utwórz nowe konto magazynu dla hosta.</span><span class="sxs-lookup"><span data-stu-id="530ff-152">**New storage account**: Create a new storage account for your host.</span></span>
     * <span data-ttu-id="530ff-153">**Istniejące konto magazynu**: Wprowadź istniejącego konta magazynu z konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="530ff-153">**Existing storage account**: Enter an existing storage account from your Azure account.</span></span>

5. <span data-ttu-id="530ff-154">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="530ff-154">Click **Next**.</span></span>

6. <span data-ttu-id="530ff-155">W **skonfiguruj dziennika poświadczeń i ustawienia portu** okna, wybierz jedną z następujących opcji:</span><span class="sxs-lookup"><span data-stu-id="530ff-155">In the **Configure log in credentials and port settings** window, select one of the following options:</span></span>

    * <span data-ttu-id="530ff-156">**Importuj poświadczeń z usługi Azure Key Vault**: Określa wcześniej zapisany zestaw poświadczeń, które są przechowywane w ramach subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="530ff-156">**Import credentials from Azure Key Vault**: Specifies a previously saved set of credentials that are stored in your Azure subscription.</span></span>

      >[!NOTE]
      ><span data-ttu-id="530ff-157">Usługa Azure Key Vault, który jest tworzony za pomocą określonego konta lub nazwy głównej usługi nie jest automatycznie dostępny za pomocą innego konta lub nazwy głównej usługi, które współużytkują subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="530ff-157">An Azure Key Vault that's created with a specific account or service principal is not automatically accessible by another account or service principal that shares the subscription.</span></span> <span data-ttu-id="530ff-158">Aby umożliwić podmiotu zabezpieczeń do użycia usługi Key Vault innego konta lub usługi, musi użyć portalu Azure i Dodaj konto lub nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="530ff-158">To allow another account or service principal to use the Key Vault, you must use the Azure portal to add the account or service principal.</span></span>

    * <span data-ttu-id="530ff-159">**Nowy dziennik poświadczenia**: tworzy nowy zestaw poświadczeń logowania.</span><span class="sxs-lookup"><span data-stu-id="530ff-159">**New log in credentials**: Creates a new set of login credentials.</span></span> <span data-ttu-id="530ff-160">Jeśli wybierzesz tę opcję, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="530ff-160">If you select this option, do the following:</span></span>
    
      * <span data-ttu-id="530ff-161">Na **poświadczenia wirtualna** , wybierz pozycję jedną z następujących opcji z poświadczeniami logowania maszyn wirtualnych na hoście Docker:</span><span class="sxs-lookup"><span data-stu-id="530ff-161">On the **VM Credentials** tab, choose one of the following options for the virtual-machine login credentials of your Docker host:</span></span>

          * <span data-ttu-id="530ff-162">**Nazwa użytkownika**: Wprowadź nazwę użytkownika o podanie poświadczeń logowania maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="530ff-162">**Username**: Enter the username for your virtual machine login credentials.</span></span>
          * <span data-ttu-id="530ff-163">**Hasło** i **Potwierdź**: Wprowadź hasło dla poświadczeń logowania maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="530ff-163">**Password** and **Confirm**: Enter the password for your virtual machine login credentials.</span></span>
          * <span data-ttu-id="530ff-164">**SSH**: Wprowadź ustawienia protokołu Secure Shell (SSH) dla hosta Docker.</span><span class="sxs-lookup"><span data-stu-id="530ff-164">**SSH**: Enter the Secure Shell (SSH) settings for your Docker host.</span></span> <span data-ttu-id="530ff-165">Możesz wybrać spośród następujących opcji:</span><span class="sxs-lookup"><span data-stu-id="530ff-165">You can choose from the following options:</span></span>
            * <span data-ttu-id="530ff-166">**Brak**: Określa, że maszyna wirtualna nie zezwala na połączenia SSH.</span><span class="sxs-lookup"><span data-stu-id="530ff-166">**None**: Specifies that your virtual machine will not allow SSH connections.</span></span>
            * <span data-ttu-id="530ff-167">**Generuj automatycznie**: automatycznie tworzy ustawienia wymagane do łączenia za pośrednictwem protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="530ff-167">**Auto-generate**: Automatically creates the requisite settings for connecting via SSH.</span></span>
            * <span data-ttu-id="530ff-168">**Importuj z katalogu**: Określa katalog, który zawiera zbiór wcześniej zapisanych ustawień SSH.</span><span class="sxs-lookup"><span data-stu-id="530ff-168">**Import from directory**: Specifies a directory that contains a set of previously saved SSH settings.</span></span> <span data-ttu-id="530ff-169">Katalog musi zawierać następujące dwa pliki:</span><span class="sxs-lookup"><span data-stu-id="530ff-169">The directory must contain the following two files:</span></span>
                * <span data-ttu-id="530ff-170">*id_rsa*: zawiera identyfikator RSA dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="530ff-170">*id_rsa*: Contains the RSA identification for a user.</span></span>
                * <span data-ttu-id="530ff-171">*id_rsa.pub*: zawiera klucza publicznego RSA, który jest używany do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="530ff-171">*id_rsa.pub*: Contains the RSA public key that is used for authentication.</span></span>
        
        ![Utwórz hosta Docker][PUB05]

      * <span data-ttu-id="530ff-173">Na **Docker demon poświadczenia** karcie, określ następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="530ff-173">On the **Docker Daemon Credentials** tab, specify the following options:</span></span>

          * <span data-ttu-id="530ff-174">**Port demon docker**: wprowadź unikatowy port TCP dla hosta Docker.</span><span class="sxs-lookup"><span data-stu-id="530ff-174">**Docker Daemon port**: Enter the unique TCP port for your Docker host.</span></span>
          * <span data-ttu-id="530ff-175">**Zabezpieczeń TLS**: Wprowadź ustawienia Transport Layer Security dla platformy Docker hosta.</span><span class="sxs-lookup"><span data-stu-id="530ff-175">**TLS Security**: Enter the Transport Layer Security settings for your Docker host.</span></span> <span data-ttu-id="530ff-176">Możesz wybrać spośród następujących opcji:</span><span class="sxs-lookup"><span data-stu-id="530ff-176">You can choose from the following options:</span></span>
            * <span data-ttu-id="530ff-177">**Brak**: Określa, że maszyna wirtualna nie zezwala na połączenia TLS.</span><span class="sxs-lookup"><span data-stu-id="530ff-177">**None**: Specifies that your virtual machine will not allow TLS connections.</span></span>
            * <span data-ttu-id="530ff-178">**Generuj automatycznie**: automatycznie tworzy ustawienia wymagane do łączenia za pośrednictwem protokołu TLS.</span><span class="sxs-lookup"><span data-stu-id="530ff-178">**Auto-generate**: Automatically creates the requisite settings for connecting via TLS.</span></span>
            * <span data-ttu-id="530ff-179">**Importuj z katalogu**: Określa katalog, który zawiera zbiór wcześniej zapisanych ustawień protokołu TLS.</span><span class="sxs-lookup"><span data-stu-id="530ff-179">**Import from directory**: Specifies a directory that contains a set of previously saved TLS settings.</span></span> <span data-ttu-id="530ff-180">W szczególności katalogu musi zawierać następujące pliki sześć:</span><span class="sxs-lookup"><span data-stu-id="530ff-180">More specifically, the directory must contain the following six files:</span></span>
                * <span data-ttu-id="530ff-181">*CA.PEM* i *key.pem urzędu certyfikacji*: zawiera certyfikat i klucz publiczny certyfikatu urzędu certyfikacji TLS.</span><span class="sxs-lookup"><span data-stu-id="530ff-181">*ca.pem* and *ca-key.pem*: Contain the certificate and public key for the TLS Certificate Authority.</span></span>
                * <span data-ttu-id="530ff-182">*CERT.PEM* i *key.pem*: zawierają certyfikat klienta i klucz publiczny, który jest używany do uwierzytelniania protokołu TLS.</span><span class="sxs-lookup"><span data-stu-id="530ff-182">*cert.pem* and *key.pem*: Contain the client certificate and public key that is used for TLS authentication.</span></span>
                * <span data-ttu-id="530ff-183">*Server.PEM* i *key.pem serwera*: zawierają certyfikat i klucz publiczny dla hosta.</span><span class="sxs-lookup"><span data-stu-id="530ff-183">*server.pem* and *server-key.pem*: Contain the server certificate and public key for the host.</span></span>

        ![Utwórz hosta Docker][PUB06]

7. <span data-ttu-id="530ff-185">Po wprowadzeniu wszystkich powyższych informacji, kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="530ff-185">After you have entered all of the preceding information, click **Finish**.</span></span>

8. <span data-ttu-id="530ff-186">W **wdrożenia kontenera Docker na platformie Azure** kreatora, kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="530ff-186">In the **Deploy Docker Container on Azure** wizard, click **Next**.</span></span>

   ![Kontener Docker wdrażanie w Kreatorze Azure][PUB07]

9. <span data-ttu-id="530ff-188">W **skonfigurować w celu utworzenia kontenera Docker** okna, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="530ff-188">In the **Configure the Docker container to be created** window, do the following:</span></span>

   <span data-ttu-id="530ff-189">a.</span><span class="sxs-lookup"><span data-stu-id="530ff-189">a.</span></span> <span data-ttu-id="530ff-190">W **nazwa kontenera Docker** wprowadź unikatową nazwę sieci kontenera Docker.</span><span class="sxs-lookup"><span data-stu-id="530ff-190">In the **Docker container name** box, enter a unique name for your Docker container.</span></span>

   <span data-ttu-id="530ff-191">b.</span><span class="sxs-lookup"><span data-stu-id="530ff-191">b.</span></span> <span data-ttu-id="530ff-192">Wybierz jedną z poniższych ilustracjach Docker:</span><span class="sxs-lookup"><span data-stu-id="530ff-192">Choose one of the following Docker images:</span></span>
     * <span data-ttu-id="530ff-193">**Wstępnie zdefiniowane obrazu Docker**: Określa istniejącego obrazu platformy Docker na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="530ff-193">**Predefined Docker image**: Specifies a pre-existing Docker image from Azure.</span></span>

       >[!NOTE]
       ><span data-ttu-id="530ff-194">Lista obrazy usługi Docker w tym polu zawiera kilka obrazów, które zestawu narzędzi platformy Azure został skonfigurowany do stosowania poprawek, aby Twoje artefaktu zostanie wdrożona automatycznie.</span><span class="sxs-lookup"><span data-stu-id="530ff-194">The list of Docker images in this box consists of several images that the Azure Toolkit has been configured to patch so that your artifact is deployed automatically.</span></span>

     * <span data-ttu-id="530ff-195">**Niestandardowy plik Dockerfile**: Określa wcześniej zapisany plik Dockerfile z komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="530ff-195">**Custom Dockerfile**: Specifies a previously saved Dockerfile from your local computer.</span></span>

       >[!NOTE]
       ><span data-ttu-id="530ff-196">Jest to bardziej zaawansowanych funkcji dla deweloperów, którzy chcą wdrożyć własny plik Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="530ff-196">This is a more advanced feature for developers who want to deploy their own Dockerfile.</span></span> <span data-ttu-id="530ff-197">Jednak jest deweloperzy, którzy używają tę opcję, aby upewnić się, że ich plik Dockerfile jest poprawnie zbudowany.</span><span class="sxs-lookup"><span data-stu-id="530ff-197">However, it is up to developers who use this option to ensure that their Dockerfile is built correctly.</span></span> <span data-ttu-id="530ff-198">Zestaw narzędzi platformy Azure nie można zweryfikować zawartości niestandardowy plik Dockerfile, wdrożenie może się nie powieść, jeśli plik Dockerfile występują problemy.</span><span class="sxs-lookup"><span data-stu-id="530ff-198">The Azure Toolkit does not validate the content in a custom Dockerfile, so the deployment might fail if the Dockerfile has issues.</span></span> <span data-ttu-id="530ff-199">Ponadto zestaw narzędzi Azure oczekuje niestandardowy plik Dockerfile zawiera artefaktu aplikacji sieci web i będzie podejmować próby otwarcia połączenia HTTP.</span><span class="sxs-lookup"><span data-stu-id="530ff-199">In addition, the Azure Toolkit expects the custom Dockerfile to contain a web app artifact, and it will attempt to open an HTTP connection.</span></span> <span data-ttu-id="530ff-200">Deweloperzy publikowania innego typu artefaktu, mogą otrzymywać nieszkodliwe błędy po wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="530ff-200">If developers publish a different type of artifact, they may receive innocuous errors after deployment.</span></span>

   <span data-ttu-id="530ff-201">c.</span><span class="sxs-lookup"><span data-stu-id="530ff-201">c.</span></span> <span data-ttu-id="530ff-202">**Ustawienia portów**: Wprowadź unikatowe powiązanie port TCP dla Twojego kontenera Docker.</span><span class="sxs-lookup"><span data-stu-id="530ff-202">**Port settings**: Enter the unique TCP port binding for your Docker container.</span></span>

     ![Konfiguruj kontenera Docker można utworzyć okna][PUB08]

10. <span data-ttu-id="530ff-204">Po wykonaniu wszystkich poprzednich kroków, kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="530ff-204">After you have completed all of the preceding steps, click **Finish**.</span></span>

<span data-ttu-id="530ff-205">Zestaw narzędzi Azure rozpoczyna wdrażanie aplikacji sieci web na platformie Azure w kontenerze Docker.</span><span class="sxs-lookup"><span data-stu-id="530ff-205">The Azure Toolkit begins deploying your web app to Azure in a Docker container.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="530ff-206">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="530ff-206">Next steps</span></span>
<span data-ttu-id="530ff-207">Aby uzyskać więcej informacji o narzędzi Azure Java IDEs zobacz następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="530ff-207">For more information about the Azure Toolkits for Java IDEs, see the following resources:</span></span>

* <span data-ttu-id="530ff-208">[Azure zestawu narzędzi dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="530ff-208">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="530ff-209">[Nowości w zestawie narzędzi programu Azure dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="530ff-209">[What's new in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="530ff-210">[Installing the Azure Toolkit for Eclipse] (Instalowanie zestawu narzędzi platformy Azure dla środowiska Eclipse)</span><span class="sxs-lookup"><span data-stu-id="530ff-210">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="530ff-211">[Instrukcje logowania dla zestawu narzędzi platformy Azure dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="530ff-211">[Sign-in instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="530ff-212">[Tworzenie aplikacji sieci web Hello World na platformie Azure w programie Eclipse]</span><span class="sxs-lookup"><span data-stu-id="530ff-212">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="530ff-213">[Azure Toolkit for IntelliJ] (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="530ff-213">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="530ff-214">[Nowości w zestawie narzędzi programu Azure for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="530ff-214">[What's new in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="530ff-215">[Installing the Azure Toolkit for IntelliJ] (Instalowanie zestawu narzędzi platformy Azure dla środowiska IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="530ff-215">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="530ff-216">[Logowanie instrukcje dotyczące zestawu narzędzi Azure for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="530ff-216">[Sign-in instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="530ff-217">[Tworzenie aplikacji sieci web Hello World na platformie Azure w IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="530ff-217">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="530ff-218">Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz [Azure Java Developer Center] i [Java Tools for Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="530ff-218">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="530ff-219">Aby uzyskać dodatkowe zasoby dla Docker można znaleźć w oficjalnej [Docker witryny sieci Web].</span><span class="sxs-lookup"><span data-stu-id="530ff-219">For additional resources for Docker, see the official [Docker website].</span></span>

<!-- URL List -->

<span data-ttu-id="530ff-220">[Azure zestawu narzędzi dla programu Eclipse]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="530ff-220">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="530ff-221">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="530ff-221">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="530ff-222">[Tworzenie aplikacji sieci web Hello World na platformie Azure w programie Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="530ff-222">[Create a Hello World web app for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="530ff-223">[Tworzenie aplikacji sieci web Hello World na platformie Azure w IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="530ff-223">[Create a Hello World web app for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="530ff-224">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md (Instalowanie zestawu narzędzi platformy Azure dla środowiska Eclipse)</span><span class="sxs-lookup"><span data-stu-id="530ff-224">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
<span data-ttu-id="530ff-225">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md (Instalowanie zestawu narzędzi platformy Azure dla środowiska IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="530ff-225">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
<span data-ttu-id="530ff-226">[Instrukcje logowania dla zestawu narzędzi platformy Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="530ff-226">[Sign-in instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
<span data-ttu-id="530ff-227">[Logowanie instrukcje dotyczące zestawu narzędzi Azure for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="530ff-227">[Sign-in instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="530ff-228">[Nowości w zestawie narzędzi programu Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="530ff-228">[What's new in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="530ff-229">[Nowości w zestawie narzędzi programu Azure for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="530ff-229">[What's new in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="530ff-230">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="530ff-230">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="530ff-231">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="530ff-231">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>

<span data-ttu-id="530ff-232">[Docker witryny sieci Web]: https://www.docker.com/</span><span class="sxs-lookup"><span data-stu-id="530ff-232">[Docker website]: https://www.docker.com/</span></span>

<!-- IMG List -->

[PUB01]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB01.png
[PUB02]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB02.png
[PUB03]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB03.png
[PUB04a]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04a.png
[PUB04b]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04b.png
[PUB04c]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04c.png
[PUB04d]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04d.png
[PUB05]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB05.png
[PUB06]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB06.png
[PUB07]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB07.png
[PUB08]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB08.png