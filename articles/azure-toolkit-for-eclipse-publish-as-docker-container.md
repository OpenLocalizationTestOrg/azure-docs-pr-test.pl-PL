---
title: "zestaw narzędzi platformy Azure dla programu Eclipse hello aaaPublish kontener Docker przy użyciu | Dokumentacja firmy Microsoft"
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
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 53ec3a7f7a171691024e03622fd48d6f1e257b50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-hello-azure-toolkit-for-eclipse"></a><span data-ttu-id="de3c5-103">Publikowanie aplikacji sieci web jako kontener Docker przy użyciu hello Azure zestawu narzędzi dla programu Eclipse</span><span class="sxs-lookup"><span data-stu-id="de3c5-103">Publish a web app as a Docker container by using hello Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="de3c5-104">Kontenery docker jest powszechnie używaną metodą wdrażania aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="de3c5-104">Docker containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="de3c5-105">Przy użyciu rozwiązania Docker kontenerów, deweloperzy umożliwiającej obsługę wszystkich plików projektu i zależności w jeden pakiet wdrażania tooa serwera.</span><span class="sxs-lookup"><span data-stu-id="de3c5-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment tooa server.</span></span> <span data-ttu-id="de3c5-106">Witaj zestawu narzędzi platformy Azure dla programu Eclipse ułatwia ten proces dla deweloperów języka Java, dodając *Publikuj jako kontener Docker* funkcje tooMicrosoft wdrożenia usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="de3c5-106">hello Azure Toolkit for Eclipse simplifies this process for Java developers by adding *Publish as Docker Container* features for deployment tooMicrosoft Azure.</span></span> <span data-ttu-id="de3c5-107">W tym artykule przedstawiono toopublish wymagane kroki hello tooAzure Twojej aplikacji jako kontenery Docker.</span><span class="sxs-lookup"><span data-stu-id="de3c5-107">This article walks you through hello steps required toopublish your applications tooAzure as Docker containers.</span></span>

> [!NOTE]
> <span data-ttu-id="de3c5-108">Więcej informacji na temat rozwiązania Docker jest dostępna na powitania [Docker witryny sieci Web].</span><span class="sxs-lookup"><span data-stu-id="de3c5-108">More information about Docker is available on hello [Docker website].</span></span>
>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a><span data-ttu-id="de3c5-109">Publikowanie tooAzure aplikacji sieci web przy użyciu kontenera Docker</span><span class="sxs-lookup"><span data-stu-id="de3c5-109">Publish your web app tooAzure by using a Docker container</span></span>

1. <span data-ttu-id="de3c5-110">Otwórz projekt aplikacji sieci web w programie Eclipse.</span><span class="sxs-lookup"><span data-stu-id="de3c5-110">Open your web app project in Eclipse.</span></span>

2. <span data-ttu-id="de3c5-111">Witaj toostart **Publikuj jako kontener Docker** kreatora, wykonaj jedną z następujących hello:</span><span class="sxs-lookup"><span data-stu-id="de3c5-111">toostart hello **Publish as Docker Container** wizard, do either of hello following:</span></span>

   * <span data-ttu-id="de3c5-112">W hello **Nawigator** wyświetlić, kliknij prawym przyciskiem myszy projekt, kliknij przycisk **Azure**, a następnie kliknij przycisk **Publikuj jako kontener Docker**.</span><span class="sxs-lookup"><span data-stu-id="de3c5-112">In hello **Navigator** view, right-click your project, click **Azure**, and then click **Publish as Docker Container**.</span></span>

      ![Nawigator widoku Publikuj jako polecenia w kontenerze Docker][PUB01]

   * <span data-ttu-id="de3c5-114">Na pasku narzędzi Eclipse hello, kliknij przycisk hello **publikowania** przycisk, a następnie kliknij przycisk **Publikuj jako kontener Docker**.</span><span class="sxs-lookup"><span data-stu-id="de3c5-114">On hello Eclipse toolbar, click hello **Publish** button, and then click **Publish as Docker Container**.</span></span>

      ![Pasek narzędzi Eclipse Publikuj jako polecenia w kontenerze Docker][PUB02]
      
    <span data-ttu-id="de3c5-116">Witaj **wdrożenia kontenera Docker na platformie Azure** zostanie otwarty Kreator.</span><span class="sxs-lookup"><span data-stu-id="de3c5-116">hello **Deploy Docker Container on Azure** wizard opens.</span></span>

    ![Witaj kontenera Docker Wdróż w Kreatorze Azure][PUB03]

3. <span data-ttu-id="de3c5-118">W hello **wpisz nazwę obrazu, wybierz artefakt hello ścieżkę i sprawdź toobe hostów Docker, używane** oknie hello następujące:</span><span class="sxs-lookup"><span data-stu-id="de3c5-118">In hello **Type an image name, select hello artifact's path and check a Docker host toobe used** window, do hello following:</span></span>

    <span data-ttu-id="de3c5-119">a.</span><span class="sxs-lookup"><span data-stu-id="de3c5-119">a.</span></span> <span data-ttu-id="de3c5-120">W hello **nazwa obrazu Docker** wprowadź unikatową nazwę hosta Docker.</span><span class="sxs-lookup"><span data-stu-id="de3c5-120">In hello **Docker image name** box, enter a unique name for your Docker host.</span></span> <span data-ttu-id="de3c5-121">(hello Kreator automatycznie tworzy nazwę, ale można go zmodyfikować).</span><span class="sxs-lookup"><span data-stu-id="de3c5-121">(hello wizard automatically creates a name, but you can modify it.)</span></span>

    <span data-ttu-id="de3c5-122">b.</span><span class="sxs-lookup"><span data-stu-id="de3c5-122">b.</span></span> <span data-ttu-id="de3c5-123">Witaj **hostów** obszar Wyświetla wszystkich hostach Docker, które zostały już utworzone.</span><span class="sxs-lookup"><span data-stu-id="de3c5-123">hello **Hosts** area displays any Docker hosts that you have already created.</span></span> <span data-ttu-id="de3c5-124">Wykonaj jedną z następujących hello:</span><span class="sxs-lookup"><span data-stu-id="de3c5-124">Do either of hello following:</span></span>

    * <span data-ttu-id="de3c5-125">Jeśli masz istniejącą hosta Docker można wdrażać tooit aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="de3c5-125">If you have an existing Docker host, you can deploy your web app tooit.</span></span>
    * <span data-ttu-id="de3c5-126">Kliknij toocreate nowego hosta platformy Docker **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="de3c5-126">toocreate a new Docker host, click **Add**.</span></span>  
      
    <span data-ttu-id="de3c5-127">Witaj **hostów Docker Utwórz** zostanie otwarte okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="de3c5-127">hello **Create Docker Host** dialog box opens.</span></span>

    ![Wdrażanie kontenera Docker w Kreatorze Azure][PUB04a]

4. <span data-ttu-id="de3c5-129">W hello **skonfigurować nową maszynę wirtualną hello** okna, określ następujące opcje dla hosta Docker hello.</span><span class="sxs-lookup"><span data-stu-id="de3c5-129">In hello **Configure hello new virtual machine** window, specify hello following options for your Docker host.</span></span> <span data-ttu-id="de3c5-130">(hello Kreator automatycznie generuje większość opcji hello można, ale można ich modyfikować.)</span><span class="sxs-lookup"><span data-stu-id="de3c5-130">(hello wizard automatically generates most of hello options for you, but you can modify any of them.)</span></span>

   <span data-ttu-id="de3c5-131">a.</span><span class="sxs-lookup"><span data-stu-id="de3c5-131">a.</span></span> <span data-ttu-id="de3c5-132">**Nazwa**: wprowadź unikatową nazwę hosta Docker hello.</span><span class="sxs-lookup"><span data-stu-id="de3c5-132">**Name**: Enter a unique name for hello Docker host.</span></span> <span data-ttu-id="de3c5-133">(Jest taki sam, jak nazwa obrazu Docker określone wcześniej hello nie hello).</span><span class="sxs-lookup"><span data-stu-id="de3c5-133">(It is not hello same as hello Docker image name that you specified earlier.)</span></span>

   <span data-ttu-id="de3c5-134">b.</span><span class="sxs-lookup"><span data-stu-id="de3c5-134">b.</span></span> <span data-ttu-id="de3c5-135">**Subskrypcja**: Wprowadź hello subskrypcji platformy Azure, której użyjesz dla hosta.</span><span class="sxs-lookup"><span data-stu-id="de3c5-135">**Subscription**: Enter hello Azure subscription that you use for your host.</span></span>

   <span data-ttu-id="de3c5-136">c.</span><span class="sxs-lookup"><span data-stu-id="de3c5-136">c.</span></span> <span data-ttu-id="de3c5-137">**Region**: Wprowadź hello region geograficzny, gdzie znajduje się na hoście.</span><span class="sxs-lookup"><span data-stu-id="de3c5-137">**Region**: Enter hello geographical region where your host is located.</span></span>

   <span data-ttu-id="de3c5-138">d.</span><span class="sxs-lookup"><span data-stu-id="de3c5-138">d.</span></span> <span data-ttu-id="de3c5-139">Na powitania **systemu operacyjnego hosta i rozmiar** karty:</span><span class="sxs-lookup"><span data-stu-id="de3c5-139">On hello **Host OS and Size** tab:</span></span>
     * <span data-ttu-id="de3c5-140">**System operacyjny hosta**: Wprowadź hello systemu operacyjnego dla maszyny wirtualnej hello zawierający hosta.</span><span class="sxs-lookup"><span data-stu-id="de3c5-140">**Host OS**: Enter hello operating system for hello virtual machine that contains your host.</span></span>
     * <span data-ttu-id="de3c5-141">**Rozmiar**: wprowadź rozmiar maszyn wirtualnych powitania dla hosta.</span><span class="sxs-lookup"><span data-stu-id="de3c5-141">**Size**: Enter hello virtual-machine size for your host.</span></span>

   <span data-ttu-id="de3c5-142">e.</span><span class="sxs-lookup"><span data-stu-id="de3c5-142">e.</span></span> <span data-ttu-id="de3c5-143">Na powitania **grupy zasobów** karty:</span><span class="sxs-lookup"><span data-stu-id="de3c5-143">On hello **Resource Group** tab:</span></span>
     * <span data-ttu-id="de3c5-144">**Nową grupę zasobów**: Utwórz nową grupę zasobów dla hosta.</span><span class="sxs-lookup"><span data-stu-id="de3c5-144">**New resource group**: Create a new resource group for your host.</span></span>
     * <span data-ttu-id="de3c5-145">**Istniejąca grupa zasobów**: Wprowadź istniejącą grupę zasobów z konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="de3c5-145">**Existing resource group**: Enter an existing resource group from your Azure account.</span></span>

   <span data-ttu-id="de3c5-146">f.</span><span class="sxs-lookup"><span data-stu-id="de3c5-146">f.</span></span> <span data-ttu-id="de3c5-147">Na powitania **sieci** karty:</span><span class="sxs-lookup"><span data-stu-id="de3c5-147">On hello **Network** tab:</span></span>
     * <span data-ttu-id="de3c5-148">**Nowa sieć wirtualna**: Utwórz nową sieć wirtualną dla hosta.</span><span class="sxs-lookup"><span data-stu-id="de3c5-148">**New virtual network**: Create a new virtual network for your host.</span></span>
     * <span data-ttu-id="de3c5-149">**Istniejącej sieci wirtualnej**: Wprowadź istniejącą sieć wirtualną z konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="de3c5-149">**Existing virtual network**: Enter an existing virtual network from your Azure account.</span></span>

   <span data-ttu-id="de3c5-150">g.</span><span class="sxs-lookup"><span data-stu-id="de3c5-150">g.</span></span> <span data-ttu-id="de3c5-151">Na powitania **magazynu** karty:</span><span class="sxs-lookup"><span data-stu-id="de3c5-151">On hello **Storage** tab:</span></span>
     * <span data-ttu-id="de3c5-152">**Nowe konto magazynu**: Utwórz nowe konto magazynu dla hosta.</span><span class="sxs-lookup"><span data-stu-id="de3c5-152">**New storage account**: Create a new storage account for your host.</span></span>
     * <span data-ttu-id="de3c5-153">**Istniejące konto magazynu**: Wprowadź istniejącego konta magazynu z konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="de3c5-153">**Existing storage account**: Enter an existing storage account from your Azure account.</span></span>

5. <span data-ttu-id="de3c5-154">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="de3c5-154">Click **Next**.</span></span>

6. <span data-ttu-id="de3c5-155">W hello **skonfiguruj dziennika poświadczeń i ustawienia portu** okna, wybierz jedną z hello następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="de3c5-155">In hello **Configure log in credentials and port settings** window, select one of hello following options:</span></span>

    * <span data-ttu-id="de3c5-156">**Importuj poświadczeń z usługi Azure Key Vault**: Określa wcześniej zapisany zestaw poświadczeń, które są przechowywane w ramach subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="de3c5-156">**Import credentials from Azure Key Vault**: Specifies a previously saved set of credentials that are stored in your Azure subscription.</span></span>

      >[!NOTE]
      ><span data-ttu-id="de3c5-157">Usługa Azure Key Vault, który jest tworzony za pomocą określonego konta lub nazwy głównej usługi nie jest automatycznie dostępny za pomocą innego konta lub nazwy głównej usługi, który współużytkuje hello subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="de3c5-157">An Azure Key Vault that's created with a specific account or service principal is not automatically accessible by another account or service principal that shares hello subscription.</span></span> <span data-ttu-id="de3c5-158">tooallow innego konta lub usługa główna toouse hello magazyn kluczy, należy użyć hello konta hello tooadd portalu Azure lub nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="de3c5-158">tooallow another account or service principal toouse hello Key Vault, you must use hello Azure portal tooadd hello account or service principal.</span></span>

    * <span data-ttu-id="de3c5-159">**Nowy dziennik poświadczenia**: tworzy nowy zestaw poświadczeń logowania.</span><span class="sxs-lookup"><span data-stu-id="de3c5-159">**New log in credentials**: Creates a new set of login credentials.</span></span> <span data-ttu-id="de3c5-160">Jeśli wybierzesz tę opcję, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="de3c5-160">If you select this option, do hello following:</span></span>
    
      * <span data-ttu-id="de3c5-161">Na powitania **poświadczenia wirtualna** , wybierz pozycję Opcje jedną z następujących hello hello poświadczeń logowania do maszyn wirtualnych z hosta Docker:</span><span class="sxs-lookup"><span data-stu-id="de3c5-161">On hello **VM Credentials** tab, choose one of hello following options for hello virtual-machine login credentials of your Docker host:</span></span>

          * <span data-ttu-id="de3c5-162">**Nazwa użytkownika**: Wprowadź nazwę hello użytkownika o podanie poświadczeń logowania maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="de3c5-162">**Username**: Enter hello username for your virtual machine login credentials.</span></span>
          * <span data-ttu-id="de3c5-163">**Hasło** i **Potwierdź**: Wprowadź hasło hello poświadczenia logowania maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="de3c5-163">**Password** and **Confirm**: Enter hello password for your virtual machine login credentials.</span></span>
          * <span data-ttu-id="de3c5-164">**SSH**: Wprowadź hello ustawienia protokołu Secure Shell (SSH) dla hosta Docker.</span><span class="sxs-lookup"><span data-stu-id="de3c5-164">**SSH**: Enter hello Secure Shell (SSH) settings for your Docker host.</span></span> <span data-ttu-id="de3c5-165">Możesz wybrać hello następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="de3c5-165">You can choose from hello following options:</span></span>
            * <span data-ttu-id="de3c5-166">**Brak**: Określa, że maszyna wirtualna nie zezwala na połączenia SSH.</span><span class="sxs-lookup"><span data-stu-id="de3c5-166">**None**: Specifies that your virtual machine will not allow SSH connections.</span></span>
            * <span data-ttu-id="de3c5-167">**Generuj automatycznie**: automatycznie tworzy hello ustawienia wymagane do łączenia za pośrednictwem protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="de3c5-167">**Auto-generate**: Automatically creates hello requisite settings for connecting via SSH.</span></span>
            * <span data-ttu-id="de3c5-168">**Importuj z katalogu**: Określa katalog, który zawiera zbiór wcześniej zapisanych ustawień SSH.</span><span class="sxs-lookup"><span data-stu-id="de3c5-168">**Import from directory**: Specifies a directory that contains a set of previously saved SSH settings.</span></span> <span data-ttu-id="de3c5-169">katalog Hello musi zawierać hello następujące dwa pliki:</span><span class="sxs-lookup"><span data-stu-id="de3c5-169">hello directory must contain hello following two files:</span></span>
                * <span data-ttu-id="de3c5-170">*id_rsa*: zawiera hello RSA identyfikacji użytkownika.</span><span class="sxs-lookup"><span data-stu-id="de3c5-170">*id_rsa*: Contains hello RSA identification for a user.</span></span>
                * <span data-ttu-id="de3c5-171">*id_rsa.pub*: zawiera hello klucza publicznego RSA, który jest używany do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="de3c5-171">*id_rsa.pub*: Contains hello RSA public key that is used for authentication.</span></span>
        
        ![Utwórz hosta Docker][PUB05]

      * <span data-ttu-id="de3c5-173">Na powitania **Docker demon poświadczenia** karcie, określ hello następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="de3c5-173">On hello **Docker Daemon Credentials** tab, specify hello following options:</span></span>

          * <span data-ttu-id="de3c5-174">**Port demon docker**: Wprowadź hello unikatowy port TCP dla hosta Docker.</span><span class="sxs-lookup"><span data-stu-id="de3c5-174">**Docker Daemon port**: Enter hello unique TCP port for your Docker host.</span></span>
          * <span data-ttu-id="de3c5-175">**Zabezpieczeń TLS**: Wprowadź hello Transport Layer Security ustawienia dla hosta Docker.</span><span class="sxs-lookup"><span data-stu-id="de3c5-175">**TLS Security**: Enter hello Transport Layer Security settings for your Docker host.</span></span> <span data-ttu-id="de3c5-176">Możesz wybrać hello następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="de3c5-176">You can choose from hello following options:</span></span>
            * <span data-ttu-id="de3c5-177">**Brak**: Określa, że maszyna wirtualna nie zezwala na połączenia TLS.</span><span class="sxs-lookup"><span data-stu-id="de3c5-177">**None**: Specifies that your virtual machine will not allow TLS connections.</span></span>
            * <span data-ttu-id="de3c5-178">**Generuj automatycznie**: automatycznie tworzy hello ustawienia wymagane do łączenia za pośrednictwem protokołu TLS.</span><span class="sxs-lookup"><span data-stu-id="de3c5-178">**Auto-generate**: Automatically creates hello requisite settings for connecting via TLS.</span></span>
            * <span data-ttu-id="de3c5-179">**Importuj z katalogu**: Określa katalog, który zawiera zbiór wcześniej zapisanych ustawień protokołu TLS.</span><span class="sxs-lookup"><span data-stu-id="de3c5-179">**Import from directory**: Specifies a directory that contains a set of previously saved TLS settings.</span></span> <span data-ttu-id="de3c5-180">W szczególności katalog hello musi zawierać następujące pliki sześciu hello:</span><span class="sxs-lookup"><span data-stu-id="de3c5-180">More specifically, hello directory must contain hello following six files:</span></span>
                * <span data-ttu-id="de3c5-181">*CA.PEM* i *key.pem urzędu certyfikacji*: zawierają hello certyfikat i klucz publiczny dla hello TLS urzędu certyfikacji.</span><span class="sxs-lookup"><span data-stu-id="de3c5-181">*ca.pem* and *ca-key.pem*: Contain hello certificate and public key for hello TLS Certificate Authority.</span></span>
                * <span data-ttu-id="de3c5-182">*CERT.PEM* i *key.pem*: zawierają hello certyfikatu klienta i klucz publiczny, który jest używany do uwierzytelniania protokołu TLS.</span><span class="sxs-lookup"><span data-stu-id="de3c5-182">*cert.pem* and *key.pem*: Contain hello client certificate and public key that is used for TLS authentication.</span></span>
                * <span data-ttu-id="de3c5-183">*Server.PEM* i *key.pem serwera*: zawierają hello certyfikat i klucz publiczny hello hosta.</span><span class="sxs-lookup"><span data-stu-id="de3c5-183">*server.pem* and *server-key.pem*: Contain hello server certificate and public key for hello host.</span></span>

        ![Utwórz hosta Docker][PUB06]

7. <span data-ttu-id="de3c5-185">Po wprowadzeniu wszystkich hello poprzedzających informacji, kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="de3c5-185">After you have entered all of hello preceding information, click **Finish**.</span></span>

8. <span data-ttu-id="de3c5-186">W hello **wdrożenia kontenera Docker na platformie Azure** kreatora, kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="de3c5-186">In hello **Deploy Docker Container on Azure** wizard, click **Next**.</span></span>

   ![Witaj kontenera Docker Wdróż w Kreatorze Azure][PUB07]

9. <span data-ttu-id="de3c5-188">W hello **skonfigurować toobe kontenera Docker hello utworzony** oknie hello następujące:</span><span class="sxs-lookup"><span data-stu-id="de3c5-188">In hello **Configure hello Docker container toobe created** window, do hello following:</span></span>

   <span data-ttu-id="de3c5-189">a.</span><span class="sxs-lookup"><span data-stu-id="de3c5-189">a.</span></span> <span data-ttu-id="de3c5-190">W hello **nazwa kontenera Docker** wprowadź unikatową nazwę sieci kontenera Docker.</span><span class="sxs-lookup"><span data-stu-id="de3c5-190">In hello **Docker container name** box, enter a unique name for your Docker container.</span></span>

   <span data-ttu-id="de3c5-191">b.</span><span class="sxs-lookup"><span data-stu-id="de3c5-191">b.</span></span> <span data-ttu-id="de3c5-192">Wybierz jedną z hello następujące obrazy usługi Docker:</span><span class="sxs-lookup"><span data-stu-id="de3c5-192">Choose one of hello following Docker images:</span></span>
     * <span data-ttu-id="de3c5-193">**Wstępnie zdefiniowane obrazu Docker**: Określa istniejącego obrazu platformy Docker na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="de3c5-193">**Predefined Docker image**: Specifies a pre-existing Docker image from Azure.</span></span>

       >[!NOTE]
       ><span data-ttu-id="de3c5-194">Witaj lista obrazy usługi Docker w tym polu zawiera kilka obrazów tego hello zestawu narzędzi platformy Azure został skonfigurowany toopatch tak, aby Twoje artefaktu zostanie wdrożona automatycznie.</span><span class="sxs-lookup"><span data-stu-id="de3c5-194">hello list of Docker images in this box consists of several images that hello Azure Toolkit has been configured toopatch so that your artifact is deployed automatically.</span></span>

     * <span data-ttu-id="de3c5-195">**Niestandardowy plik Dockerfile**: Określa wcześniej zapisany plik Dockerfile z komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="de3c5-195">**Custom Dockerfile**: Specifies a previously saved Dockerfile from your local computer.</span></span>

       >[!NOTE]
       ><span data-ttu-id="de3c5-196">Jest to bardziej zaawansowanych funkcji dla deweloperów, którzy chcą toodeploy własny plik Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="de3c5-196">This is a more advanced feature for developers who want toodeploy their own Dockerfile.</span></span> <span data-ttu-id="de3c5-197">Jednak to maksymalnie toodevelopers korzystającym z tooensure tej opcji, ich plik Dockerfile korzysta z wbudowanej poprawnie.</span><span class="sxs-lookup"><span data-stu-id="de3c5-197">However, it is up toodevelopers who use this option tooensure that their Dockerfile is built correctly.</span></span> <span data-ttu-id="de3c5-198">Hello Azure Toolkit nie można zweryfikować zawartości hello niestandardowy plik Dockerfile tak hello wdrażania może się nie powieść, jeśli hello plik Dockerfile występują problemy.</span><span class="sxs-lookup"><span data-stu-id="de3c5-198">hello Azure Toolkit does not validate hello content in a custom Dockerfile, so hello deployment might fail if hello Dockerfile has issues.</span></span> <span data-ttu-id="de3c5-199">Ponadto hello Azure Toolkit oczekuje hello niestandardowy plik Dockerfile toocontain artefaktu aplikacji sieci web i będzie podejmować tooopen połączenia HTTP.</span><span class="sxs-lookup"><span data-stu-id="de3c5-199">In addition, hello Azure Toolkit expects hello custom Dockerfile toocontain a web app artifact, and it will attempt tooopen an HTTP connection.</span></span> <span data-ttu-id="de3c5-200">Deweloperzy publikowania innego typu artefaktu, mogą otrzymywać nieszkodliwe błędy po wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="de3c5-200">If developers publish a different type of artifact, they may receive innocuous errors after deployment.</span></span>

   <span data-ttu-id="de3c5-201">c.</span><span class="sxs-lookup"><span data-stu-id="de3c5-201">c.</span></span> <span data-ttu-id="de3c5-202">**Ustawienia portów**: Wprowadź hello unikatowe TCP port powiązanie z kontenera Docker.</span><span class="sxs-lookup"><span data-stu-id="de3c5-202">**Port settings**: Enter hello unique TCP port binding for your Docker container.</span></span>

     ![Witaj Konfiguruj hello Docker kontenera toobe utworzone okno][PUB08]

10. <span data-ttu-id="de3c5-204">Po wykonaniu wszystkich poprzednich krokach powitania kliknij **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="de3c5-204">After you have completed all of hello preceding steps, click **Finish**.</span></span>

<span data-ttu-id="de3c5-205">Hello Azure Toolkit rozpoczyna wdrażanie Twojego tooAzure aplikacji sieci web w kontenerze Docker.</span><span class="sxs-lookup"><span data-stu-id="de3c5-205">hello Azure Toolkit begins deploying your web app tooAzure in a Docker container.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="de3c5-206">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="de3c5-206">Next steps</span></span>
<span data-ttu-id="de3c5-207">Aby uzyskać więcej informacji o hello narzędzi Azure Java IDEs zobacz następujące zasoby hello:</span><span class="sxs-lookup"><span data-stu-id="de3c5-207">For more information about hello Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="de3c5-208">[Azure zestawu narzędzi dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="de3c5-208">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="de3c5-209">[What's new in hello zestawu narzędzi platformy Azure dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="de3c5-209">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="de3c5-210">[Instalowanie hello zestawu narzędzi platformy Azure dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="de3c5-210">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="de3c5-211">[Instrukcje logowania hello zestawu narzędzi platformy Azure dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="de3c5-211">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="de3c5-212">[Tworzenie aplikacji sieci web Hello World na platformie Azure w programie Eclipse]</span><span class="sxs-lookup"><span data-stu-id="de3c5-212">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="de3c5-213">[Azure Toolkit for IntelliJ] (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="de3c5-213">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="de3c5-214">[What's new in hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="de3c5-214">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="de3c5-215">[Instalowanie hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="de3c5-215">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="de3c5-216">[Logowanie instrukcje dotyczące hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="de3c5-216">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="de3c5-217">[Tworzenie aplikacji sieci web Hello World na platformie Azure w IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="de3c5-217">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="de3c5-218">Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz [Azure Java Developer Center] i [Java Tools for Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="de3c5-218">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="de3c5-219">Aby uzyskać dodatkowe zasoby dla Docker, zobacz oficjalne hello [Docker witryny sieci Web].</span><span class="sxs-lookup"><span data-stu-id="de3c5-219">For additional resources for Docker, see hello official [Docker website].</span></span>

<!-- URL List -->

[Azure zestawu narzędzi dla programu Eclipse]: ./azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)
[Tworzenie aplikacji sieci web Hello World na platformie Azure w programie Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Tworzenie aplikacji sieci web Hello World na platformie Azure w IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Instalowanie hello zestawu narzędzi platformy Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Instalowanie hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Instrukcje logowania hello zestawu narzędzi platformy Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Logowanie instrukcje dotyczące hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[What's new in hello zestawu narzędzi platformy Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[What's new in hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/

[Docker witryny sieci Web]: https://www.docker.com/

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