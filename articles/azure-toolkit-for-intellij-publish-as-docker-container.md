---
title: "aaaPublish kontener Docker przy użyciu hello Azure Toolkit for IntelliJ | Dokumentacja firmy Microsoft"
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
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: bee94cb269ea707ae7ad55232e23e915aec48c34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-hello-azure-toolkit-for-intellij"></a><span data-ttu-id="959a4-103">Publikowanie aplikacji sieci web jako kontener Docker przy użyciu hello Azure Toolkit for IntelliJ</span><span class="sxs-lookup"><span data-stu-id="959a4-103">Publish a web app as a Docker container by using hello Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="959a4-104">Kontenery docker jest powszechnie używaną metodą wdrażania aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="959a4-104">Docker containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="959a4-105">Przy użyciu rozwiązania Docker kontenerów, deweloperzy umożliwiającej obsługę wszystkich plików projektu i zależności w jeden pakiet wdrażania tooa serwera.</span><span class="sxs-lookup"><span data-stu-id="959a4-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment tooa server.</span></span> <span data-ttu-id="959a4-106">Hello Azure Toolkit for IntelliJ ułatwia ten proces dla deweloperów języka Java, dodając *Publikuj jako kontener Docker* funkcje tooMicrosoft wdrożenia usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="959a4-106">hello Azure Toolkit for IntelliJ simplifies this process for Java developers by adding *Publish as Docker Container* features for deployment tooMicrosoft Azure.</span></span> <span data-ttu-id="959a4-107">W tym artykule przedstawiono toopublish wymagane kroki hello tooAzure Twojej aplikacji jako kontenery Docker.</span><span class="sxs-lookup"><span data-stu-id="959a4-107">This article walks you through hello steps required toopublish your applications tooAzure as Docker containers.</span></span>

> [!NOTE]
>
> <span data-ttu-id="959a4-108">Więcej informacji na temat rozwiązania Docker jest dostępna na powitania [Docker witryny sieci Web].</span><span class="sxs-lookup"><span data-stu-id="959a4-108">More information about Docker is available on hello [Docker website].</span></span>
>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a><span data-ttu-id="959a4-109">Publikowanie tooAzure aplikacji sieci web przy użyciu kontenera Docker</span><span class="sxs-lookup"><span data-stu-id="959a4-109">Publish your web app tooAzure by using a Docker container</span></span>

> [!NOTE]
> * <span data-ttu-id="959a4-110">toopublish aplikacji sieci web, należy utworzyć artefaktu gotowe do wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="959a4-110">toopublish your web app, you must create a deployment-ready artifact.</span></span> <span data-ttu-id="959a4-111">toolearn więcej, zobacz hello [dodatkowe informacje na temat tworzenia artefaktów](#artifacts) sekcji.</span><span class="sxs-lookup"><span data-stu-id="959a4-111">toolearn more, see hello [Additional information about creating artifacts](#artifacts) section.</span></span>
>
> * <span data-ttu-id="959a4-112">Po ukończeniu Kreatora wdrażania hello co najmniej raz, po uruchomieniu kreatora hello ponownie większość ustawień są używane jako domyślne.</span><span class="sxs-lookup"><span data-stu-id="959a4-112">After you have completed hello deployment wizard at least once, most of your settings are used as defaults when you run hello wizard again.</span></span>
>

1. <span data-ttu-id="959a4-113">Otwórz projekt aplikacji sieci web w środowisko IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="959a4-113">Open your web app project in IntelliJ.</span></span>

2. <span data-ttu-id="959a4-114">Witaj toostart **Publikuj jako kontener Docker** kreatora, wykonaj jedną z następujących hello:</span><span class="sxs-lookup"><span data-stu-id="959a4-114">toostart hello **Publish as Docker Container** wizard, do either of hello following:</span></span>

   * <span data-ttu-id="959a4-115">W hello **projektu** okna narzędzia, kliknij prawym przyciskiem myszy projekt, kliknij przycisk **Azure**, a następnie kliknij przycisk **Publikuj jako kontener Docker**:</span><span class="sxs-lookup"><span data-stu-id="959a4-115">In hello **Project** tool window, right-click your project, click **Azure**, and then click **Publish as Docker Container**:</span></span>

      ![Publikuj jako polecenia w kontenerze Docker Hello][PUB01]

   * <span data-ttu-id="959a4-117">Na pasku narzędzi IntelliJ hello, kliknij przycisk hello **grupy publikowania** przycisk, a następnie kliknij przycisk **Publikuj jako kontener Docker**:</span><span class="sxs-lookup"><span data-stu-id="959a4-117">On hello IntelliJ toolbar, click hello **Publish Group** button, and then click **Publish as Docker Container**:</span></span>

      <span data-ttu-id="959a4-118">![Publikuj jako polecenia w kontenerze Docker Hello][PUB02]</span><span class="sxs-lookup"><span data-stu-id="959a4-118">![hello Publish as Docker Container command][PUB02]</span></span>  
    <span data-ttu-id="959a4-119">Witaj **wdrożenia kontenera Docker na platformie Azure** zostanie otwarty Kreator.</span><span class="sxs-lookup"><span data-stu-id="959a4-119">hello **Deploy Docker Container on Azure** wizard opens.</span></span>

   ![Witaj kontenera Docker Wdróż w Kreatorze Azure][PUB03]

3. <span data-ttu-id="959a4-121">W hello **wpisz nazwę obrazu, wybierz artefakt hello ścieżkę i sprawdź toobe hostów Docker, używane** oknie hello następujące:</span><span class="sxs-lookup"><span data-stu-id="959a4-121">In hello **Type an image name, select hello artifact's path and check a Docker host toobe used** window, do hello following:</span></span> 

   <span data-ttu-id="959a4-122">a.</span><span class="sxs-lookup"><span data-stu-id="959a4-122">a.</span></span> <span data-ttu-id="959a4-123">W hello **nazwa obrazu Docker** wprowadź unikatową nazwę hosta Docker.</span><span class="sxs-lookup"><span data-stu-id="959a4-123">In hello **Docker image name** box, enter a unique name for your Docker host.</span></span> <span data-ttu-id="959a4-124">(hello Kreator automatycznie tworzy nazwę, ale można go zmodyfikować).</span><span class="sxs-lookup"><span data-stu-id="959a4-124">(hello wizard automatically creates a name, but you can modify it.)</span></span> 

   <span data-ttu-id="959a4-125">b.</span><span class="sxs-lookup"><span data-stu-id="959a4-125">b.</span></span> <span data-ttu-id="959a4-126">Witaj **hostów** obszar Wyświetla wszystkich hostach Docker, które zostały już utworzone.</span><span class="sxs-lookup"><span data-stu-id="959a4-126">hello **Hosts** area displays any Docker hosts that you have already created.</span></span> <span data-ttu-id="959a4-127">Wykonaj jedną z następujących hello:</span><span class="sxs-lookup"><span data-stu-id="959a4-127">Do either of hello following:</span></span> 
      * <span data-ttu-id="959a4-128">Jeśli masz istniejącą hosta Docker można wdrażać tooit aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="959a4-128">If you have an existing Docker host, you can deploy your web app tooit.</span></span>
      * <span data-ttu-id="959a4-129">toocreate Docker hosta, kliknij znak plus hello zielony (**+**).</span><span class="sxs-lookup"><span data-stu-id="959a4-129">toocreate a Docker host, click hello green plus sign (**+**).</span></span>  
       <span data-ttu-id="959a4-130">Witaj **hostów Docker Utwórz** zostanie otwarte okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="959a4-130">hello **Create Docker Host** dialog box opens.</span></span> 

      ![Wdrażanie kontenera Docker w Kreatorze Azure][PUB04a]

4. <span data-ttu-id="959a4-132">W hello **skonfigurować nową maszynę wirtualną hello** okna, podaj następujące informacje o hoście Docker hello.</span><span class="sxs-lookup"><span data-stu-id="959a4-132">In hello **Configure hello new virtual machine** window, provide hello following information about your Docker host.</span></span> <span data-ttu-id="959a4-133">(hello Kreator automatycznie generuje większość hello informacje dla Ciebie, ale można ich modyfikować.)</span><span class="sxs-lookup"><span data-stu-id="959a4-133">(hello wizard automatically generates most of hello information for you, but you can modify any of them.)</span></span> 

   <span data-ttu-id="959a4-134">a.</span><span class="sxs-lookup"><span data-stu-id="959a4-134">a.</span></span> <span data-ttu-id="959a4-135">W hello **nazwa** wprowadź unikatową nazwę hosta Docker hello.</span><span class="sxs-lookup"><span data-stu-id="959a4-135">In hello **Name** box, enter a unique name for hello Docker host.</span></span> <span data-ttu-id="959a4-136">(Jest taki sam, jak nazwa obrazu Docker określone wcześniej hello nie hello).</span><span class="sxs-lookup"><span data-stu-id="959a4-136">(It is not hello same as hello Docker image name that you specified earlier.)</span></span> 
    
   <span data-ttu-id="959a4-137">b.</span><span class="sxs-lookup"><span data-stu-id="959a4-137">b.</span></span> <span data-ttu-id="959a4-138">W hello **subskrypcji** wprowadź hello subskrypcji platformy Azure, której użyjesz dla hosta.</span><span class="sxs-lookup"><span data-stu-id="959a4-138">In hello **Subscription** box, enter hello Azure subscription that you use for your host.</span></span> 
      
   <span data-ttu-id="959a4-139">c.</span><span class="sxs-lookup"><span data-stu-id="959a4-139">c.</span></span> <span data-ttu-id="959a4-140">W hello **Region** wprowadź hello region geograficzny, gdzie znajduje się na hoście.</span><span class="sxs-lookup"><span data-stu-id="959a4-140">In hello **Region** box, enter hello geographical region where your host is located.</span></span>
      
   <span data-ttu-id="959a4-141">d.</span><span class="sxs-lookup"><span data-stu-id="959a4-141">d.</span></span> <span data-ttu-id="959a4-142">Na powitania **systemu operacyjnego i rozmiar** pozycję hello następujące:</span><span class="sxs-lookup"><span data-stu-id="959a4-142">On hello **OS and Size** tab, do hello following:</span></span>      
      * <span data-ttu-id="959a4-143">**System operacyjny hosta**: Wprowadź hello systemu operacyjnego dla maszyny wirtualnej hello zawierający hosta.</span><span class="sxs-lookup"><span data-stu-id="959a4-143">**Host OS**: Enter hello operating system for hello virtual machine that contains your host.</span></span> 
      * <span data-ttu-id="959a4-144">**Rozmiar**: wprowadź rozmiar maszyn wirtualnych powitania dla hosta.</span><span class="sxs-lookup"><span data-stu-id="959a4-144">**Size**: Enter hello virtual-machine size for your host.</span></span>   
       
   <span data-ttu-id="959a4-145">e.</span><span class="sxs-lookup"><span data-stu-id="959a4-145">e.</span></span> <span data-ttu-id="959a4-146">Na powitania **grupy zasobów** , a następnie wybierz jedną z następujących hello:</span><span class="sxs-lookup"><span data-stu-id="959a4-146">On hello **Resource Group** tab, select either of hello following:</span></span>      
      * <span data-ttu-id="959a4-147">**Nową grupę zasobów**: Utwórz grupę zasobów dla hosta.</span><span class="sxs-lookup"><span data-stu-id="959a4-147">**New resource group**: Create a resource group for your host.</span></span>
      * <span data-ttu-id="959a4-148">**Istniejąca grupa zasobów**: Określ istniejącą grupę zasobów z konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="959a4-148">**Existing resource group**: Specify an existing resource group from your Azure account.</span></span> 
       
   <span data-ttu-id="959a4-149">f.</span><span class="sxs-lookup"><span data-stu-id="959a4-149">f.</span></span> <span data-ttu-id="959a4-150">Na powitania **sieci** , a następnie wybierz jedną z następujących hello:</span><span class="sxs-lookup"><span data-stu-id="959a4-150">On hello **Network** tab, select either of hello following:</span></span>      
      * <span data-ttu-id="959a4-151">**Nowa sieć wirtualna**: tworzenie sieci wirtualnej dla hosta.</span><span class="sxs-lookup"><span data-stu-id="959a4-151">**New virtual network**: Create a virtual network for your host.</span></span>
      * <span data-ttu-id="959a4-152">**Istniejącej sieci wirtualnej**: Określ istniejącej sieci wirtualnej z konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="959a4-152">**Existing virtual network**: Specify an existing virtual network from your Azure account.</span></span> 
       
   <span data-ttu-id="959a4-153">g.</span><span class="sxs-lookup"><span data-stu-id="959a4-153">g.</span></span> <span data-ttu-id="959a4-154">Na powitania **magazynu** , a następnie wybierz jedną z następujących hello:</span><span class="sxs-lookup"><span data-stu-id="959a4-154">On hello **Storage** tab, select either of hello following:</span></span>      
      * <span data-ttu-id="959a4-155">**Nowe konto magazynu**: Tworzenie konta magazynu dla hosta.</span><span class="sxs-lookup"><span data-stu-id="959a4-155">**New storage account**: Create a storage account for your host.</span></span>
      * <span data-ttu-id="959a4-156">**Istniejące konto magazynu**: określenie istniejącego konta magazynu z konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="959a4-156">**Existing storage account**: Specify an existing storage account from your Azure account.</span></span>
       
5. <span data-ttu-id="959a4-157">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="959a4-157">Click **Next**.</span></span>  
     <span data-ttu-id="959a4-158">Witaj **skonfiguruj dziennika poświadczeń i ustawienia portu** zostanie otwarte okno.</span><span class="sxs-lookup"><span data-stu-id="959a4-158">hello **Configure log in credentials and port settings** window opens.</span></span>

      ![Hello dziennika Konfigurowanie poświadczeń i ustawienia portu][PUB05]

6. <span data-ttu-id="959a4-160">Wybierz jedną z hello następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="959a4-160">Select one of hello following options:</span></span>

      * <span data-ttu-id="959a4-161">**Importuj poświadczeń z usługi Azure Key Vault**: Określ wcześniej zapisany zestaw poświadczeń, które są przechowywane w Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="959a4-161">**Import credentials from Azure Key Vault**: Specify a previously saved set of credentials that are stored in your Azure subscription.</span></span>

          > [!NOTE]
          > <span data-ttu-id="959a4-162">Usługi Azure key vault, który jest tworzony za pomocą określonego konta lub nazwy głównej usługi nie jest automatycznie dostępny za pomocą innego konta lub nazwy głównej usługi, który współużytkuje hello subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="959a4-162">An Azure key vault that's created with a specific account or service principal is not automatically accessible by another account or service principal that shares hello subscription.</span></span> <span data-ttu-id="959a4-163">tooallow innego konta lub usługi klucza podmiotu zabezpieczeń toouse w hello magazynu, należy użyć hello konta hello tooadd portalu Azure lub nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="959a4-163">tooallow another account or service principal toouse hello key vault, you must use hello Azure portal tooadd hello account or service principal.</span></span>

      * <span data-ttu-id="959a4-164">**Nowy dziennik poświadczenia**: Tworzenie nowego zestawu poświadczeń logowania.</span><span class="sxs-lookup"><span data-stu-id="959a4-164">**New log in credentials**: Create a new set of login credentials.</span></span> <span data-ttu-id="959a4-165">Jeśli wybierzesz tę opcję, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="959a4-165">If you select this option, do hello following:</span></span>

        <span data-ttu-id="959a4-166">a.</span><span class="sxs-lookup"><span data-stu-id="959a4-166">a.</span></span> <span data-ttu-id="959a4-167">Na powitania **wirtualna poświadczenia** karcie, podaj następujące informacje dla poświadczeń logowania do maszyn wirtualnych hello hosta Docker hello: * **Username**: Wprowadź nazwę użytkownika hello logowania z maszyn wirtualnych poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="959a4-167">On hello **VM Credentials** tab, provide hello following information for hello virtual-machine login credentials of your Docker host: * **Username**: Enter hello username for your virtual-machine login credentials.</span></span>
             <span data-ttu-id="959a4-168">* **Hasło** i **Potwierdź**: Wprowadź hasło hello o podanie poświadczeń logowania do maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="959a4-168">* **Password** and **Confirm**: Enter hello password for your virtual-machine login credentials.</span></span>
             <span data-ttu-id="959a4-169">* **SSH**: Wprowadź hello ustawienia protokołu Secure Shell (SSH) dla hosta Docker.</span><span class="sxs-lookup"><span data-stu-id="959a4-169">* **SSH**: Enter hello Secure Shell (SSH) settings for your Docker host.</span></span> <span data-ttu-id="959a4-170">Można wybrać jedną z hello następujące opcje: * **Brak**: Określa, że maszyna wirtualna nie zezwala na połączenia SSH.</span><span class="sxs-lookup"><span data-stu-id="959a4-170">You can select one of hello following options: * **None**: Specifies that your virtual machine does not allow SSH connections.</span></span>
                <span data-ttu-id="959a4-171">* **Generuj automatycznie**: automatycznie tworzy hello ustawienia wymagane do łączenia za pośrednictwem protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="959a4-171">* **Auto-generate**: Automatically creates hello requisite settings for connecting via SSH.</span></span>
                <span data-ttu-id="959a4-172">* **Importuj z katalogu**: pozwala toospecify katalogu, który zawiera zestaw wcześniej zapisanych ustawień SSH.</span><span class="sxs-lookup"><span data-stu-id="959a4-172">* **Import from directory**: Allows you toospecify a directory that contains a set of previously saved SSH settings.</span></span> <span data-ttu-id="959a4-173">katalog Hello musi zawierać hello następujące dwa pliki:</span><span class="sxs-lookup"><span data-stu-id="959a4-173">hello directory must contain hello following two files:</span></span>
                
                  * *id_rsa*: Contains hello RSA identification for a user.
                  * *id_rsa.pub*: Contains hello RSA public key that is used for authentication.
            
        <span data-ttu-id="959a4-174">b.</span><span class="sxs-lookup"><span data-stu-id="959a4-174">b.</span></span> <span data-ttu-id="959a4-175">Na powitania **Docker demon dostępu** karcie, podaj hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="959a4-175">On hello **Docker Daemon Access** tab, provide hello following information:</span></span>

          ![Utwórz hosta Docker][PUB06]
    
             * **Docker Daemon port**: Enter hello unique TCP port for your Docker host.
             * **TLS Security**: Enter hello Transport Layer Security settings for your Docker host. You can choose from hello following options:
                * **None**: Specifies that your virtual machine does not allow TLS connections.
                * **Auto-generate**: Automatically creates hello requisite settings for connecting via TLS.
                * **Import from directory**: Specifies a directory that contains a set of previously saved TLS settings. hello directory must contain hello following six files: 
                   * *ca.pem* and *ca-key.pem*: Contain hello certificate and public key for hello TLS Certificate Authority.
                   * *cert.pem* and *key.pem*: Contain client certificate and public key which will be used for TLS authentication.
                   * *server.pem* and *server-key.pem*: Contain hello client certificate and public key that is used for TLS authentication.

7. <span data-ttu-id="959a4-177">Po wprowadzeniu hello wymaganych informacji, kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="959a4-177">After you have entered hello required information, click **Finish**.</span></span>  
    <span data-ttu-id="959a4-178">Witaj **wdrożenia kontenera Docker na platformie Azure** kreatora pojawi się ponownie.</span><span class="sxs-lookup"><span data-stu-id="959a4-178">hello **Deploy Docker Container on Azure** wizard reappears.</span></span>

   ![Wdrażanie kontenera Docker w Kreatorze Azure][PUB07]

8. <span data-ttu-id="959a4-180">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="959a4-180">Click **Next**.</span></span>  
    <span data-ttu-id="959a4-181">Witaj **skonfigurować toobe kontenera Docker hello utworzony** zostanie otwarte okno.</span><span class="sxs-lookup"><span data-stu-id="959a4-181">hello **Configure hello Docker container toobe created** window opens.</span></span>

   ![Witaj Konfiguruj hello Docker kontenera toobe utworzone okno][PUB08]

9. <span data-ttu-id="959a4-183">W hello **skonfigurować toobe kontenera Docker hello utworzony** okna, podaj hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="959a4-183">In hello **Configure hello Docker container toobe created** window, provide hello following information:</span></span> 

   <span data-ttu-id="959a4-184">a.</span><span class="sxs-lookup"><span data-stu-id="959a4-184">a.</span></span> <span data-ttu-id="959a4-185">W hello **nazwa kontenera Docker** wprowadź unikatową nazwę sieci kontenera Docker.</span><span class="sxs-lookup"><span data-stu-id="959a4-185">In hello **Docker container name** box, enter a unique name for your Docker container.</span></span>

   <span data-ttu-id="959a4-186">b.</span><span class="sxs-lookup"><span data-stu-id="959a4-186">b.</span></span> <span data-ttu-id="959a4-187">Wybierz jedną z hello następujące obrazy usługi Docker:</span><span class="sxs-lookup"><span data-stu-id="959a4-187">Choose one of hello following Docker images:</span></span> 

      * <span data-ttu-id="959a4-188">**Wstępnie zdefiniowane obrazu Docker**: Określ istniejącego obrazu platformy Docker na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="959a4-188">**Predefined Docker image**: Specify a pre-existing Docker image from Azure.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="959a4-189">Witaj lista obrazy usługi Docker w tym polu zawiera kilka obrazów tego hello zestawu narzędzi platformy Azure został skonfigurowany toopatch tak, aby Twoje artefaktu zostanie wdrożona automatycznie.</span><span class="sxs-lookup"><span data-stu-id="959a4-189">hello list of Docker images in this box consists of several images that hello Azure Toolkit has been configured toopatch so that your artifact is deployed automatically.</span></span> 

      * <span data-ttu-id="959a4-190">**Niestandardowy plik Dockerfile**: Określ wcześniej zapisany plik Dockerfile z komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="959a4-190">**Custom Dockerfile**: Specify a previously saved Dockerfile from your local computer.</span></span>

        > [!NOTE]
        > <span data-ttu-id="959a4-191">Jest to bardziej zaawansowanych funkcji dla deweloperów, którzy chcą toodeploy własny plik Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="959a4-191">This is a more advanced feature for developers who want toodeploy their own Dockerfile.</span></span> <span data-ttu-id="959a4-192">Jednak to maksymalnie toodevelopers korzystającym z tooensure tej opcji, ich plik Dockerfile korzysta z wbudowanej poprawnie.</span><span class="sxs-lookup"><span data-stu-id="959a4-192">However, it is up toodevelopers who use this option tooensure that their Dockerfile is built correctly.</span></span> <span data-ttu-id="959a4-193">Ponieważ hello Azure Toolkit nie można zweryfikować zawartości hello niestandardowy plik Dockerfile, hello wdrażania może się nie powieść Jeśli hello plik Dockerfile występują problemy.</span><span class="sxs-lookup"><span data-stu-id="959a4-193">Because hello Azure Toolkit does not validate hello content in a custom Dockerfile, hello deployment might fail if hello Dockerfile has issues.</span></span> <span data-ttu-id="959a4-194">Ponadto ponieważ hello Azure Toolkit oczekuje hello niestandardowy plik Dockerfile toocontain artefaktu aplikacji sieci web, podejmuje tooopen połączenia HTTP.</span><span class="sxs-lookup"><span data-stu-id="959a4-194">In addition, because hello Azure Toolkit expects hello custom Dockerfile toocontain a web app artifact, it attempts tooopen an HTTP connection.</span></span> <span data-ttu-id="959a4-195">Deweloperzy publikowania innego typu artefaktu, otrzymają może nieszkodliwe błędy po wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="959a4-195">If developers publish a different type of artifact, they might receive innocuous errors after deployment.</span></span>

   <span data-ttu-id="959a4-196">c.</span><span class="sxs-lookup"><span data-stu-id="959a4-196">c.</span></span> <span data-ttu-id="959a4-197">W hello **ustawienia portu** wprowadź hello unikatowe TCP port powiązanie z kontenera Docker.</span><span class="sxs-lookup"><span data-stu-id="959a4-197">In hello **Port settings** box, enter hello unique TCP port binding for your Docker container.</span></span> 

10. <span data-ttu-id="959a4-198">Po wykonaniu poprzednich krokach hello, kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="959a4-198">After you have completed hello preceding steps, click **Finish**.</span></span> 

<span data-ttu-id="959a4-199">Hello Azure Toolkit rozpoczyna wdrażanie Twojego tooAzure aplikacji sieci web w kontenerze Docker.</span><span class="sxs-lookup"><span data-stu-id="959a4-199">hello Azure Toolkit begins deploying your web app tooAzure in a Docker container.</span></span> <span data-ttu-id="959a4-200">Jeśli nie skonfigurowano wdrożone w tle hello toobe IntelliJ **wdrażanie tooAzure** zostanie wyświetlony pasek postępu.</span><span class="sxs-lookup"><span data-stu-id="959a4-200">Unless you have configured IntelliJ toobe deployed in hello background, a **Deploying tooAzure** progress bar appears.</span></span> 

![pasek postępu wdrożenia Hello][PUB09]

<a name="artifacts"></a>
## <a name="additional-information-about-creating-artifacts"></a><span data-ttu-id="959a4-202">Dodatkowe informacje na temat tworzenia artefaktów</span><span class="sxs-lookup"><span data-stu-id="959a4-202">Additional information about creating artifacts</span></span>

<span data-ttu-id="959a4-203">toocreate artefaktu gotowe do wdrożenia, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="959a4-203">toocreate a deployment-ready artifact, do hello following:</span></span>

1. <span data-ttu-id="959a4-204">Otwórz projekt aplikacji sieci web w środowisko IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="959a4-204">Open your web app project in IntelliJ.</span></span>

2. <span data-ttu-id="959a4-205">Kliknij przycisk **pliku**, a następnie kliknij przycisk **struktury projektu**.</span><span class="sxs-lookup"><span data-stu-id="959a4-205">Click **File**, and then click **Project Structure**.</span></span>

   ![Witaj polecenia struktury projektu][ART01]

3. <span data-ttu-id="959a4-207">tooadd jako artefaktu, kliknij znak plus hello zielony (**+**), a następnie kliknij przycisk **aplikacji sieci Web: archiwum**.</span><span class="sxs-lookup"><span data-stu-id="959a4-207">tooadd an artifact, click hello green plus sign (**+**), and then click **Web Application: Archive**.</span></span>

   ![polecenie "Archiwum: aplikacja sieci Web" Hello][ART02]

4. <span data-ttu-id="959a4-209">W hello **nazwa** wprowadź nazwę użytkownika artefaktu (nie dołączaj hello *.war* rozszerzenia), a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="959a4-209">In hello **Name** box, enter a name for your artifact (do not include hello *.war* extension), and then click **OK**.</span></span>

   ![pole Nazwa Hello artefaktów][ART03]

<span data-ttu-id="959a4-211">Aby uzyskać więcej informacji na temat tworzenia artefaktów w IntelliJ, zobacz [Konfigurowanie artefakty] na powitania JetBrains witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="959a4-211">For more information about creating artifacts in IntelliJ, see [Configuring artifacts] on hello JetBrains website.</span></span>

## <a name="next-steps"></a><span data-ttu-id="959a4-212">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="959a4-212">Next steps</span></span>
<span data-ttu-id="959a4-213">Aby uzyskać więcej informacji o hello narzędzi Azure Java IDEs zobacz następujące zasoby hello:</span><span class="sxs-lookup"><span data-stu-id="959a4-213">For more information about hello Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="959a4-214">[Azure zestawu narzędzi dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="959a4-214">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="959a4-215">[What's new in hello zestawu narzędzi platformy Azure dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="959a4-215">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="959a4-216">[Instalowanie hello zestawu narzędzi platformy Azure dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="959a4-216">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="959a4-217">[Instrukcje logowania hello zestawu narzędzi platformy Azure dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="959a4-217">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="959a4-218">[Tworzenie aplikacji sieci web Hello World na platformie Azure w programie Eclipse]</span><span class="sxs-lookup"><span data-stu-id="959a4-218">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="959a4-219">[Azure Toolkit for IntelliJ] (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="959a4-219">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="959a4-220">[What's new in hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="959a4-220">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="959a4-221">[Instalowanie hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="959a4-221">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="959a4-222">[Logowanie instrukcje dotyczące hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="959a4-222">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="959a4-223">[Tworzenie aplikacji sieci web Hello World na platformie Azure w IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="959a4-223">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="959a4-224">Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz hello [Azure Java Developer Center] i hello [Java Tools for Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="959a4-224">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="959a4-225">Aby uzyskać dodatkowe zasoby dla Docker, zobacz oficjalne hello [Docker witryny sieci Web].</span><span class="sxs-lookup"><span data-stu-id="959a4-225">For additional resources for Docker, see hello official [Docker website].</span></span>

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
[Konfigurowanie artefakty]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html

<!-- IMG List -->

[PUB01]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB01.png
[PUB02]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB02.png
[PUB03]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB03.png
[PUB04a]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04a.png
[PUB04b]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04b.png
[PUB04c]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04c.png
[PUB04d]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04d.png
[PUB05]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB05.png
[PUB06]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB06.png
[PUB07]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB07.png
[PUB08]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB08.png
[PUB09]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB09.png

[ART01]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART01.png
[ART02]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART02.png
[ART03]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART03.png
