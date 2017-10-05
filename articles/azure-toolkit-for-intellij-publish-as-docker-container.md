---
title: "Publikowanie kontenera Docker przy użyciu zestawu narzędzi Azure for IntelliJ | Dokumentacja firmy Microsoft"
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
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 96680319a6c4c0f0a4673cd6303a5b172f428797
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-the-azure-toolkit-for-intellij"></a><span data-ttu-id="2b769-103">Publikowanie aplikacji sieci web jako kontener Docker przy użyciu zestawu narzędzi Azure for IntelliJ</span><span class="sxs-lookup"><span data-stu-id="2b769-103">Publish a web app as a Docker container by using the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="2b769-104">Kontenery docker jest powszechnie używaną metodą wdrażania aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="2b769-104">Docker containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="2b769-105">Przy użyciu rozwiązania Docker kontenerów, deweloperzy mogą konsolidację wszystkie pliki projektu i zależności w jeden pakiet do wdrożenia na serwerze.</span><span class="sxs-lookup"><span data-stu-id="2b769-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment to a server.</span></span> <span data-ttu-id="2b769-106">Zestaw narzędzi platformy Azure dla IntelliJ ułatwia ten proces dla deweloperów języka Java, dodając *Publikuj jako kontener Docker* funkcji dla wdrożenia do systemu Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="2b769-106">The Azure Toolkit for IntelliJ simplifies this process for Java developers by adding *Publish as Docker Container* features for deployment to Microsoft Azure.</span></span> <span data-ttu-id="2b769-107">W tym artykule przedstawiono kroki wymagane do publikowania aplikacji na platformie Azure jako kontenery Docker.</span><span class="sxs-lookup"><span data-stu-id="2b769-107">This article walks you through the steps required to publish your applications to Azure as Docker containers.</span></span>

> [!NOTE]
>
> <span data-ttu-id="2b769-108">Więcej informacji na temat rozwiązania Docker jest dostępna na [Docker witryny sieci Web].</span><span class="sxs-lookup"><span data-stu-id="2b769-108">More information about Docker is available on the [Docker website].</span></span>
>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a><span data-ttu-id="2b769-109">Publikowanie aplikacji sieci web na platformie Azure przy użyciu kontenera Docker</span><span class="sxs-lookup"><span data-stu-id="2b769-109">Publish your web app to Azure by using a Docker container</span></span>

> [!NOTE]
> * <span data-ttu-id="2b769-110">Aby opublikować aplikację sieci web, należy utworzyć artefaktu gotowe do wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="2b769-110">To publish your web app, you must create a deployment-ready artifact.</span></span> <span data-ttu-id="2b769-111">Aby dowiedzieć się więcej, zobacz [dodatkowe informacje na temat tworzenia artefaktów](#artifacts) sekcji.</span><span class="sxs-lookup"><span data-stu-id="2b769-111">To learn more, see the [Additional information about creating artifacts](#artifacts) section.</span></span>
>
> * <span data-ttu-id="2b769-112">Po ukończeniu Kreatora wdrażania co najmniej raz, większość ustawień są używane jako domyślne podczas uruchom kreatora ponownie.</span><span class="sxs-lookup"><span data-stu-id="2b769-112">After you have completed the deployment wizard at least once, most of your settings are used as defaults when you run the wizard again.</span></span>
>

1. <span data-ttu-id="2b769-113">Otwórz projekt aplikacji sieci web w środowisko IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="2b769-113">Open your web app project in IntelliJ.</span></span>

2. <span data-ttu-id="2b769-114">Aby uruchomić **Publikuj jako kontener Docker** kreatora, wykonaj jedną z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="2b769-114">To start the **Publish as Docker Container** wizard, do either of the following:</span></span>

   * <span data-ttu-id="2b769-115">W **projektu** okna narzędzia, kliknij prawym przyciskiem myszy projekt, kliknij przycisk **Azure**, a następnie kliknij przycisk **Publikuj jako kontener Docker**:</span><span class="sxs-lookup"><span data-stu-id="2b769-115">In the **Project** tool window, right-click your project, click **Azure**, and then click **Publish as Docker Container**:</span></span>

      ![Publikuj jako polecenia w kontenerze Docker][PUB01]

   * <span data-ttu-id="2b769-117">Kliknij na pasku narzędzi IntelliJ **grupy publikowania** przycisk, a następnie kliknij przycisk **Publikuj jako kontener Docker**:</span><span class="sxs-lookup"><span data-stu-id="2b769-117">On the IntelliJ toolbar, click the **Publish Group** button, and then click **Publish as Docker Container**:</span></span>

      <span data-ttu-id="2b769-118">![Publikuj jako polecenia w kontenerze Docker][PUB02]</span><span class="sxs-lookup"><span data-stu-id="2b769-118">![The Publish as Docker Container command][PUB02]</span></span>  
    <span data-ttu-id="2b769-119">**Wdrożenia kontenera Docker na platformie Azure** zostanie otwarty Kreator.</span><span class="sxs-lookup"><span data-stu-id="2b769-119">The **Deploy Docker Container on Azure** wizard opens.</span></span>

   ![Kontener Docker wdrażanie w Kreatorze Azure][PUB03]

3. <span data-ttu-id="2b769-121">W **wpisz nazwę obrazu, wybierz artefakt ścieżkę i sprawdź Docker hosta do użycia** okna, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="2b769-121">In the **Type an image name, select the artifact's path and check a Docker host to be used** window, do the following:</span></span> 

   <span data-ttu-id="2b769-122">a.</span><span class="sxs-lookup"><span data-stu-id="2b769-122">a.</span></span> <span data-ttu-id="2b769-123">W **nazwa obrazu Docker** wprowadź unikatową nazwę hosta Docker.</span><span class="sxs-lookup"><span data-stu-id="2b769-123">In the **Docker image name** box, enter a unique name for your Docker host.</span></span> <span data-ttu-id="2b769-124">(Kreator automatycznie tworzy nazwę, ale można go zmodyfikować).</span><span class="sxs-lookup"><span data-stu-id="2b769-124">(The wizard automatically creates a name, but you can modify it.)</span></span> 

   <span data-ttu-id="2b769-125">b.</span><span class="sxs-lookup"><span data-stu-id="2b769-125">b.</span></span> <span data-ttu-id="2b769-126">**Hostów** obszar Wyświetla wszystkich hostach Docker, które zostały już utworzone.</span><span class="sxs-lookup"><span data-stu-id="2b769-126">The **Hosts** area displays any Docker hosts that you have already created.</span></span> <span data-ttu-id="2b769-127">Wykonaj jedną z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="2b769-127">Do either of the following:</span></span> 
      * <span data-ttu-id="2b769-128">Jeśli masz istniejącą hosta Docker można wdrożyć aplikację sieci web do niego.</span><span class="sxs-lookup"><span data-stu-id="2b769-128">If you have an existing Docker host, you can deploy your web app to it.</span></span>
      * <span data-ttu-id="2b769-129">Aby utworzyć hostów Docker, kliknij zielony znak plus (**+**).</span><span class="sxs-lookup"><span data-stu-id="2b769-129">To create a Docker host, click the green plus sign (**+**).</span></span>  
       <span data-ttu-id="2b769-130">**Hostów Docker Utwórz** zostanie otwarte okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="2b769-130">The **Create Docker Host** dialog box opens.</span></span> 

      ![Wdrażanie kontenera Docker w Kreatorze Azure][PUB04a]

4. <span data-ttu-id="2b769-132">W **skonfigurować nową maszynę wirtualną** okna, podaj następujące informacje o hoście Docker.</span><span class="sxs-lookup"><span data-stu-id="2b769-132">In the **Configure the new virtual machine** window, provide the following information about your Docker host.</span></span> <span data-ttu-id="2b769-133">(Kreator automatycznie generuje większość informacji dla Ciebie, ale można ich modyfikować.)</span><span class="sxs-lookup"><span data-stu-id="2b769-133">(The wizard automatically generates most of the information for you, but you can modify any of them.)</span></span> 

   <span data-ttu-id="2b769-134">a.</span><span class="sxs-lookup"><span data-stu-id="2b769-134">a.</span></span> <span data-ttu-id="2b769-135">W **nazwa** wprowadź unikatową nazwę hosta Docker.</span><span class="sxs-lookup"><span data-stu-id="2b769-135">In the **Name** box, enter a unique name for the Docker host.</span></span> <span data-ttu-id="2b769-136">(Go nie jest taka sama jak nazwa obrazu Docker określone wcześniej.)</span><span class="sxs-lookup"><span data-stu-id="2b769-136">(It is not the same as the Docker image name that you specified earlier.)</span></span> 
    
   <span data-ttu-id="2b769-137">b.</span><span class="sxs-lookup"><span data-stu-id="2b769-137">b.</span></span> <span data-ttu-id="2b769-138">W **subskrypcji** wprowadź subskrypcji platformy Azure, której użyjesz dla hosta.</span><span class="sxs-lookup"><span data-stu-id="2b769-138">In the **Subscription** box, enter the Azure subscription that you use for your host.</span></span> 
      
   <span data-ttu-id="2b769-139">c.</span><span class="sxs-lookup"><span data-stu-id="2b769-139">c.</span></span> <span data-ttu-id="2b769-140">W **Region** wprowadź region geograficzny, w którym znajduje się na hoście.</span><span class="sxs-lookup"><span data-stu-id="2b769-140">In the **Region** box, enter the geographical region where your host is located.</span></span>
      
   <span data-ttu-id="2b769-141">d.</span><span class="sxs-lookup"><span data-stu-id="2b769-141">d.</span></span> <span data-ttu-id="2b769-142">Na **systemu operacyjnego i rozmiar** karcie, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="2b769-142">On the **OS and Size** tab, do the following:</span></span>      
      * <span data-ttu-id="2b769-143">**System operacyjny hosta**: Wprowadź system operacyjny dla maszyny wirtualnej, która zawiera hosta.</span><span class="sxs-lookup"><span data-stu-id="2b769-143">**Host OS**: Enter the operating system for the virtual machine that contains your host.</span></span> 
      * <span data-ttu-id="2b769-144">**Rozmiar**: wprowadź rozmiar maszyn wirtualnych dla hosta.</span><span class="sxs-lookup"><span data-stu-id="2b769-144">**Size**: Enter the virtual-machine size for your host.</span></span>   
       
   <span data-ttu-id="2b769-145">e.</span><span class="sxs-lookup"><span data-stu-id="2b769-145">e.</span></span> <span data-ttu-id="2b769-146">Na **grupy zasobów** , a następnie wybierz jedną z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="2b769-146">On the **Resource Group** tab, select either of the following:</span></span>      
      * <span data-ttu-id="2b769-147">**Nową grupę zasobów**: Utwórz grupę zasobów dla hosta.</span><span class="sxs-lookup"><span data-stu-id="2b769-147">**New resource group**: Create a resource group for your host.</span></span>
      * <span data-ttu-id="2b769-148">**Istniejąca grupa zasobów**: Określ istniejącą grupę zasobów z konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2b769-148">**Existing resource group**: Specify an existing resource group from your Azure account.</span></span> 
       
   <span data-ttu-id="2b769-149">f.</span><span class="sxs-lookup"><span data-stu-id="2b769-149">f.</span></span> <span data-ttu-id="2b769-150">Na **sieci** , a następnie wybierz jedną z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="2b769-150">On the **Network** tab, select either of the following:</span></span>      
      * <span data-ttu-id="2b769-151">**Nowa sieć wirtualna**: tworzenie sieci wirtualnej dla hosta.</span><span class="sxs-lookup"><span data-stu-id="2b769-151">**New virtual network**: Create a virtual network for your host.</span></span>
      * <span data-ttu-id="2b769-152">**Istniejącej sieci wirtualnej**: Określ istniejącej sieci wirtualnej z konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2b769-152">**Existing virtual network**: Specify an existing virtual network from your Azure account.</span></span> 
       
   <span data-ttu-id="2b769-153">g.</span><span class="sxs-lookup"><span data-stu-id="2b769-153">g.</span></span> <span data-ttu-id="2b769-154">Na **magazynu** , a następnie wybierz jedną z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="2b769-154">On the **Storage** tab, select either of the following:</span></span>      
      * <span data-ttu-id="2b769-155">**Nowe konto magazynu**: Tworzenie konta magazynu dla hosta.</span><span class="sxs-lookup"><span data-stu-id="2b769-155">**New storage account**: Create a storage account for your host.</span></span>
      * <span data-ttu-id="2b769-156">**Istniejące konto magazynu**: określenie istniejącego konta magazynu z konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2b769-156">**Existing storage account**: Specify an existing storage account from your Azure account.</span></span>
       
5. <span data-ttu-id="2b769-157">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="2b769-157">Click **Next**.</span></span>  
     <span data-ttu-id="2b769-158">**Skonfiguruj dziennika poświadczeń i ustawienia portu** zostanie otwarte okno.</span><span class="sxs-lookup"><span data-stu-id="2b769-158">The **Configure log in credentials and port settings** window opens.</span></span>

      ![Dziennika Konfigurowanie poświadczeń i ustawienia portu][PUB05]

6. <span data-ttu-id="2b769-160">Wybierz jedną z następujących opcji:</span><span class="sxs-lookup"><span data-stu-id="2b769-160">Select one of the following options:</span></span>

      * <span data-ttu-id="2b769-161">**Importuj poświadczeń z usługi Azure Key Vault**: Określ wcześniej zapisany zestaw poświadczeń, które są przechowywane w Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2b769-161">**Import credentials from Azure Key Vault**: Specify a previously saved set of credentials that are stored in your Azure subscription.</span></span>

          > [!NOTE]
          > <span data-ttu-id="2b769-162">Usługi Azure key vault, który jest tworzony za pomocą określonego konta lub nazwy głównej usługi nie jest automatycznie dostępny za pomocą innego konta lub nazwy głównej usługi, które współużytkują subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="2b769-162">An Azure key vault that's created with a specific account or service principal is not automatically accessible by another account or service principal that shares the subscription.</span></span> <span data-ttu-id="2b769-163">Aby umożliwić głównych do używania magazynu kluczy innego konta lub usługi, musi użyć portalu Azure, aby dodać konto lub nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="2b769-163">To allow another account or service principal to use the key vault, you must use the Azure portal to add the account or service principal.</span></span>

      * <span data-ttu-id="2b769-164">**Nowy dziennik poświadczenia**: Tworzenie nowego zestawu poświadczeń logowania.</span><span class="sxs-lookup"><span data-stu-id="2b769-164">**New log in credentials**: Create a new set of login credentials.</span></span> <span data-ttu-id="2b769-165">Jeśli wybierzesz tę opcję, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="2b769-165">If you select this option, do the following:</span></span>

        <span data-ttu-id="2b769-166">a.</span><span class="sxs-lookup"><span data-stu-id="2b769-166">a.</span></span> <span data-ttu-id="2b769-167">Na **poświadczenia wirtualna** karcie, podaj następujące informacje dotyczące poświadczeń logowania do maszyn wirtualnych z hosta Docker: * **Username**: Wprowadź nazwę użytkownika dla nazwy logowania użytkownika maszyny wirtualnej poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="2b769-167">On the **VM Credentials** tab, provide the following information for the virtual-machine login credentials of your Docker host: * **Username**: Enter the username for your virtual-machine login credentials.</span></span>
             <span data-ttu-id="2b769-168">* **Hasło** i **Potwierdź**: Wprowadź hasło dla poświadczeń logowania do maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="2b769-168">* **Password** and **Confirm**: Enter the password for your virtual-machine login credentials.</span></span>
             <span data-ttu-id="2b769-169">* **SSH**: Wprowadź ustawienia protokołu Secure Shell (SSH) dla hosta Docker.</span><span class="sxs-lookup"><span data-stu-id="2b769-169">* **SSH**: Enter the Secure Shell (SSH) settings for your Docker host.</span></span> <span data-ttu-id="2b769-170">Można wybrać jedną z następujących opcji: * **Brak**: Określa, że maszyna wirtualna nie zezwala na połączenia SSH.</span><span class="sxs-lookup"><span data-stu-id="2b769-170">You can select one of the following options: * **None**: Specifies that your virtual machine does not allow SSH connections.</span></span>
                <span data-ttu-id="2b769-171">* **Generuj automatycznie**: automatycznie tworzy ustawienia wymagane do łączenia za pośrednictwem protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="2b769-171">* **Auto-generate**: Automatically creates the requisite settings for connecting via SSH.</span></span>
                <span data-ttu-id="2b769-172">* **Importuj z katalogu**: można określić katalogu, który zawiera zestaw wcześniej zapisanych ustawień SSH.</span><span class="sxs-lookup"><span data-stu-id="2b769-172">* **Import from directory**: Allows you to specify a directory that contains a set of previously saved SSH settings.</span></span> <span data-ttu-id="2b769-173">Katalog musi zawierać następujące dwa pliki:</span><span class="sxs-lookup"><span data-stu-id="2b769-173">The directory must contain the following two files:</span></span>
                
                  * *id_rsa*: Contains the RSA identification for a user.
                  * *id_rsa.pub*: Contains the RSA public key that is used for authentication.
            
        <span data-ttu-id="2b769-174">b.</span><span class="sxs-lookup"><span data-stu-id="2b769-174">b.</span></span> <span data-ttu-id="2b769-175">Na **Docker demon dostępu** karcie, podaj następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="2b769-175">On the **Docker Daemon Access** tab, provide the following information:</span></span>

          ![Utwórz hosta Docker][PUB06]
    
             * **Docker Daemon port**: Enter the unique TCP port for your Docker host.
             * **TLS Security**: Enter the Transport Layer Security settings for your Docker host. You can choose from the following options:
                * **None**: Specifies that your virtual machine does not allow TLS connections.
                * **Auto-generate**: Automatically creates the requisite settings for connecting via TLS.
                * **Import from directory**: Specifies a directory that contains a set of previously saved TLS settings. The directory must contain the following six files: 
                   * *ca.pem* and *ca-key.pem*: Contain the certificate and public key for the TLS Certificate Authority.
                   * *cert.pem* and *key.pem*: Contain client certificate and public key which will be used for TLS authentication.
                   * *server.pem* and *server-key.pem*: Contain the client certificate and public key that is used for TLS authentication.

7. <span data-ttu-id="2b769-177">Po wprowadzeniu wymaganych informacji kliknij **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="2b769-177">After you have entered the required information, click **Finish**.</span></span>  
    <span data-ttu-id="2b769-178">**Wdrożenia kontenera Docker na platformie Azure** kreatora pojawi się ponownie.</span><span class="sxs-lookup"><span data-stu-id="2b769-178">The **Deploy Docker Container on Azure** wizard reappears.</span></span>

   ![Wdrażanie kontenera Docker w Kreatorze Azure][PUB07]

8. <span data-ttu-id="2b769-180">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="2b769-180">Click **Next**.</span></span>  
    <span data-ttu-id="2b769-181">**Skonfigurować w celu utworzenia kontenera Docker** zostanie otwarte okno.</span><span class="sxs-lookup"><span data-stu-id="2b769-181">The **Configure the Docker container to be created** window opens.</span></span>

   ![Konfiguruj kontenera Docker można utworzyć okna][PUB08]

9. <span data-ttu-id="2b769-183">W **skonfigurować w celu utworzenia kontenera Docker** okna, podaj następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="2b769-183">In the **Configure the Docker container to be created** window, provide the following information:</span></span> 

   <span data-ttu-id="2b769-184">a.</span><span class="sxs-lookup"><span data-stu-id="2b769-184">a.</span></span> <span data-ttu-id="2b769-185">W **nazwa kontenera Docker** wprowadź unikatową nazwę sieci kontenera Docker.</span><span class="sxs-lookup"><span data-stu-id="2b769-185">In the **Docker container name** box, enter a unique name for your Docker container.</span></span>

   <span data-ttu-id="2b769-186">b.</span><span class="sxs-lookup"><span data-stu-id="2b769-186">b.</span></span> <span data-ttu-id="2b769-187">Wybierz jedną z poniższych ilustracjach Docker:</span><span class="sxs-lookup"><span data-stu-id="2b769-187">Choose one of the following Docker images:</span></span> 

      * <span data-ttu-id="2b769-188">**Wstępnie zdefiniowane obrazu Docker**: Określ istniejącego obrazu platformy Docker na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="2b769-188">**Predefined Docker image**: Specify a pre-existing Docker image from Azure.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="2b769-189">Lista obrazy usługi Docker w tym polu zawiera kilka obrazów, które zestawu narzędzi platformy Azure został skonfigurowany do stosowania poprawek, aby Twoje artefaktu zostanie wdrożona automatycznie.</span><span class="sxs-lookup"><span data-stu-id="2b769-189">The list of Docker images in this box consists of several images that the Azure Toolkit has been configured to patch so that your artifact is deployed automatically.</span></span> 

      * <span data-ttu-id="2b769-190">**Niestandardowy plik Dockerfile**: Określ wcześniej zapisany plik Dockerfile z komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="2b769-190">**Custom Dockerfile**: Specify a previously saved Dockerfile from your local computer.</span></span>

        > [!NOTE]
        > <span data-ttu-id="2b769-191">Jest to bardziej zaawansowanych funkcji dla deweloperów, którzy chcą wdrożyć własny plik Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="2b769-191">This is a more advanced feature for developers who want to deploy their own Dockerfile.</span></span> <span data-ttu-id="2b769-192">Jednak jest deweloperzy, którzy używają tę opcję, aby upewnić się, że ich plik Dockerfile jest poprawnie zbudowany.</span><span class="sxs-lookup"><span data-stu-id="2b769-192">However, it is up to developers who use this option to ensure that their Dockerfile is built correctly.</span></span> <span data-ttu-id="2b769-193">Ponieważ zestaw narzędzi platformy Azure nie można zweryfikować zawartości niestandardowy plik Dockerfile, wdrożenie może się nie powieść, jeśli plik Dockerfile występują problemy.</span><span class="sxs-lookup"><span data-stu-id="2b769-193">Because the Azure Toolkit does not validate the content in a custom Dockerfile, the deployment might fail if the Dockerfile has issues.</span></span> <span data-ttu-id="2b769-194">Ponadto ponieważ zestaw narzędzi Azure oczekuje niestandardowy plik Dockerfile zawiera artefaktu aplikacji sieci web, próbuje otworzyć połączenie HTTP.</span><span class="sxs-lookup"><span data-stu-id="2b769-194">In addition, because the Azure Toolkit expects the custom Dockerfile to contain a web app artifact, it attempts to open an HTTP connection.</span></span> <span data-ttu-id="2b769-195">Deweloperzy publikowania innego typu artefaktu, otrzymają może nieszkodliwe błędy po wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="2b769-195">If developers publish a different type of artifact, they might receive innocuous errors after deployment.</span></span>

   <span data-ttu-id="2b769-196">c.</span><span class="sxs-lookup"><span data-stu-id="2b769-196">c.</span></span> <span data-ttu-id="2b769-197">W **ustawienia portu** wprowadź unikatowe powiązanie port TCP dla Twojego kontenera Docker.</span><span class="sxs-lookup"><span data-stu-id="2b769-197">In the **Port settings** box, enter the unique TCP port binding for your Docker container.</span></span> 

10. <span data-ttu-id="2b769-198">Po wykonaniu powyższych kroków, kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="2b769-198">After you have completed the preceding steps, click **Finish**.</span></span> 

<span data-ttu-id="2b769-199">Zestaw narzędzi Azure rozpoczyna wdrażanie aplikacji sieci web na platformie Azure w kontenerze Docker.</span><span class="sxs-lookup"><span data-stu-id="2b769-199">The Azure Toolkit begins deploying your web app to Azure in a Docker container.</span></span> <span data-ttu-id="2b769-200">Jeśli nie skonfigurowano IntelliJ wdrażanych w tle, **wdrażanie na platformie Azure** zostanie wyświetlony pasek postępu.</span><span class="sxs-lookup"><span data-stu-id="2b769-200">Unless you have configured IntelliJ to be deployed in the background, a **Deploying to Azure** progress bar appears.</span></span> 

![Pasek postępu wdrożenia][PUB09]

<a name="artifacts"></a>
## <a name="additional-information-about-creating-artifacts"></a><span data-ttu-id="2b769-202">Dodatkowe informacje na temat tworzenia artefaktów</span><span class="sxs-lookup"><span data-stu-id="2b769-202">Additional information about creating artifacts</span></span>

<span data-ttu-id="2b769-203">Aby utworzyć artefaktu gotowe do wdrożenia, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="2b769-203">To create a deployment-ready artifact, do the following:</span></span>

1. <span data-ttu-id="2b769-204">Otwórz projekt aplikacji sieci web w środowisko IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="2b769-204">Open your web app project in IntelliJ.</span></span>

2. <span data-ttu-id="2b769-205">Kliknij przycisk **pliku**, a następnie kliknij przycisk **struktury projektu**.</span><span class="sxs-lookup"><span data-stu-id="2b769-205">Click **File**, and then click **Project Structure**.</span></span>

   ![Polecenie struktury projektu][ART01]

3. <span data-ttu-id="2b769-207">Aby dodać artefaktu, kliknij zielony znak plus (**+**), a następnie kliknij przycisk **aplikacji sieci Web: archiwum**.</span><span class="sxs-lookup"><span data-stu-id="2b769-207">To add an artifact, click the green plus sign (**+**), and then click **Web Application: Archive**.</span></span>

   ![Polecenie "Archiwum sieci Web aplikacji:"][ART02]

4. <span data-ttu-id="2b769-209">W **nazwa** wprowadź nazwę użytkownika artefaktu (nie dołączaj *.war* rozszerzenia), a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="2b769-209">In the **Name** box, enter a name for your artifact (do not include the *.war* extension), and then click **OK**.</span></span>

   ![Pole Nazwa artefaktów][ART03]

<span data-ttu-id="2b769-211">Aby uzyskać więcej informacji na temat tworzenia artefaktów w IntelliJ, zobacz [Konfigurowanie artefakty] na JetBrains witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="2b769-211">For more information about creating artifacts in IntelliJ, see [Configuring artifacts] on the JetBrains website.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b769-212">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2b769-212">Next steps</span></span>
<span data-ttu-id="2b769-213">Aby uzyskać więcej informacji o narzędzi Azure Java IDEs zobacz następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="2b769-213">For more information about the Azure Toolkits for Java IDEs, see the following resources:</span></span>

* <span data-ttu-id="2b769-214">[Azure zestawu narzędzi dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="2b769-214">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="2b769-215">[Nowości w zestawie narzędzi programu Azure dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="2b769-215">[What's new in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="2b769-216">[Installing the Azure Toolkit for Eclipse] (Instalowanie zestawu narzędzi platformy Azure dla środowiska Eclipse)</span><span class="sxs-lookup"><span data-stu-id="2b769-216">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="2b769-217">[Instrukcje logowania dla zestawu narzędzi platformy Azure dla programu Eclipse]</span><span class="sxs-lookup"><span data-stu-id="2b769-217">[Sign-in instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="2b769-218">[Tworzenie aplikacji sieci web Hello World na platformie Azure w programie Eclipse]</span><span class="sxs-lookup"><span data-stu-id="2b769-218">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="2b769-219">[Azure Toolkit for IntelliJ] (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="2b769-219">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="2b769-220">[Nowości w zestawie narzędzi programu Azure for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="2b769-220">[What's new in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="2b769-221">[Installing the Azure Toolkit for IntelliJ] (Instalowanie zestawu narzędzi platformy Azure dla środowiska IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="2b769-221">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="2b769-222">[Logowanie instrukcje dotyczące zestawu narzędzi Azure for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="2b769-222">[Sign-in instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="2b769-223">[Tworzenie aplikacji sieci web Hello World na platformie Azure w IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="2b769-223">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="2b769-224">Aby uzyskać więcej informacji o używaniu platformy Azure z językiem Java, zobacz [Centrum deweloperów języka Java dla platformy Azure] i [Java Tools for Visual Studio Team Services] (Narzędzia języka Java dla usługi Visual Studio Team Services).</span><span class="sxs-lookup"><span data-stu-id="2b769-224">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="2b769-225">Aby uzyskać dodatkowe zasoby dla Docker można znaleźć w oficjalnej [Docker witryny sieci Web].</span><span class="sxs-lookup"><span data-stu-id="2b769-225">For additional resources for Docker, see the official [Docker website].</span></span>

<!-- URL List -->

<span data-ttu-id="2b769-226">[Azure zestawu narzędzi dla programu Eclipse]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="2b769-226">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="2b769-227">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="2b769-227">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="2b769-228">[Tworzenie aplikacji sieci web Hello World na platformie Azure w programie Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="2b769-228">[Create a Hello World web app for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="2b769-229">[Tworzenie aplikacji sieci web Hello World na platformie Azure w IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="2b769-229">[Create a Hello World web app for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="2b769-230">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md (Instalowanie zestawu narzędzi platformy Azure dla środowiska Eclipse)</span><span class="sxs-lookup"><span data-stu-id="2b769-230">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
<span data-ttu-id="2b769-231">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md (Instalowanie zestawu narzędzi platformy Azure dla środowiska IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="2b769-231">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
<span data-ttu-id="2b769-232">[Instrukcje logowania dla zestawu narzędzi platformy Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="2b769-232">[Sign-in instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
<span data-ttu-id="2b769-233">[Logowanie instrukcje dotyczące zestawu narzędzi Azure for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="2b769-233">[Sign-in instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="2b769-234">[Nowości w zestawie narzędzi programu Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="2b769-234">[What's new in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="2b769-235">[Nowości w zestawie narzędzi programu Azure for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="2b769-235">[What's new in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="2b769-236">[Centrum deweloperów języka Java dla platformy Azure]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="2b769-236">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="2b769-237">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="2b769-237">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>

<span data-ttu-id="2b769-238">[Docker witryny sieci Web]: https://www.docker.com/</span><span class="sxs-lookup"><span data-stu-id="2b769-238">[Docker website]: https://www.docker.com/</span></span>
<span data-ttu-id="2b769-239">[Konfigurowanie artefakty]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html</span><span class="sxs-lookup"><span data-stu-id="2b769-239">[Configuring artifacts]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html</span></span>

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
