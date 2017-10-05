---
title: "Przy użyciu rozszerzenia maszyny Wirtualnej platformy Docker dla systemu Linux | Dokumentacja firmy Microsoft"
description: "Opisuje Docker i rozszerzenia maszyn wirtualnych platformy Azure i sposobu tworzenia maszyn wirtualnych Azure, które są hostów docker w klasycznym modelu wdrażania przy użyciu wiersza polecenia platformy Azure."
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 19cf64e8-f92c-43ad-a120-8976cd9102ac
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/27/2016
ms.author: rasquill
ms.openlocfilehash: 932744208d9d53c87e31dcdf9e34539750be4bdb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-docker-vm-extension-with-the-azure-classic-portal"></a><span data-ttu-id="46aed-103">Korzystanie z rozszerzenia maszyny wirtualnej platformy Docker z klasycznym portalem Azure</span><span class="sxs-lookup"><span data-stu-id="46aed-103">Using the Docker VM Extension with the Azure classic portal</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="46aed-104">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="46aed-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="46aed-105">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="46aed-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="46aed-106">Firma Microsoft zaleca, aby w przypadku większości nowych wdrożeń korzystać z modelu opartego na programie Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="46aed-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="46aed-107">[Docker](https://www.docker.com/) jest jednym z najpopularniejszych podejść wirtualizacji, które używa [kontenery Linux](http://en.wikipedia.org/wiki/LXC) zamiast maszyn wirtualnych w sposób izolowanie danych i przetwarzania danych w udostępnionych zasobów.</span><span class="sxs-lookup"><span data-stu-id="46aed-107">[Docker](https://www.docker.com/) is one of the most popular virtualization approaches that uses [Linux containers](http://en.wikipedia.org/wiki/LXC) rather than virtual machines as a way of isolating data and computing on shared resources.</span></span> <span data-ttu-id="46aed-108">Można użyć rozszerzenia maszyny Wirtualnej platformy Docker zarządza [agenta systemu Linux Azure] tworzenie Docker maszyny Wirtualnej, który obsługuje dowolną liczbę kontenerów dla aplikacji na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="46aed-108">You can use the Docker VM extension managed by [Azure Linux Agent] to create a Docker VM that hosts any number of containers for your applications on Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="46aed-109">W tym temacie opisano sposób tworzenia maszyny Wirtualnej platformy Docker z klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="46aed-109">This topic describes how to create a Docker VM from the Azure classic portal.</span></span> <span data-ttu-id="46aed-110">Aby sprawdzić, jak można utworzyć maszyny Wirtualnej platformy Docker w wierszu polecenia, zobacz [sposobu użycia Docker rozszerzenia maszyny Wirtualnej z interfejsu wiersza polecenia platformy Azure (Azure CLI)].</span><span class="sxs-lookup"><span data-stu-id="46aed-110">To see how to create a Docker VM at the command line, see [How to use the Docker VM Extension from the Azure Command-line Interface (Azure CLI)].</span></span> <span data-ttu-id="46aed-111">Aby wyświetlić ogólne omówienie kontenery i ich zalety, zobacz [Docker wysoki poziom tablicy](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span><span class="sxs-lookup"><span data-stu-id="46aed-111">To see a high-level discussion of containers and their advantages, see the [Docker High Level Whiteboard](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span></span>
> 
> 

## <a name="create-a-new-vm-from-the-image-gallery"></a><span data-ttu-id="46aed-112">Utwórz nową maszynę Wirtualną z galerii obrazów</span><span class="sxs-lookup"><span data-stu-id="46aed-112">Create a new VM from the Image Gallery</span></span>
<span data-ttu-id="46aed-113">Pierwszym krokiem wymaga maszyny Wirtualnej platformy Azure z obrazu systemu Linux, który obsługuje Docker rozszerzenia maszyny Wirtualnej, używając obrazu Ubuntu 14.04 LTS z galerii obrazów jako przykład obrazu serwera i Ubuntu 14.04 pulpitu jako klienta.</span><span class="sxs-lookup"><span data-stu-id="46aed-113">The first step requires an Azure VM from a Linux image that supports the Docker VM Extension, using an Ubuntu 14.04 LTS image from the Image Gallery as an example server image and Ubuntu 14.04 Desktop as a client.</span></span> <span data-ttu-id="46aed-114">W portalu kliknij **+ nowy** w lewym dolnym rogu do utworzenia nowego wystąpienia maszyny Wirtualnej, a następnie wybierz obraz Ubuntu 14.04 LTS z dostępnych opcji lub pełną Galeria obrazów, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="46aed-114">In the portal, click **+ New** in the bottom left corner to create a new VM instance and select an Ubuntu 14.04 LTS image from the selections available or from the complete Image Gallery, as shown below.</span></span>

> [!NOTE]
> <span data-ttu-id="46aed-115">Obecnie tylko obrazy Ubuntu 14.04 LTS nowsza niż lipca 2014 obsługują Docker rozszerzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="46aed-115">Currently, only Ubuntu 14.04 LTS images more recent than July 2014 support the Docker VM Extension.</span></span>
> 
> 

![Utwórz nowy obraz Ubuntu](./media/portal-use-docker/ChooseUbuntu.png)

## <a name="create-docker-certificates"></a><span data-ttu-id="46aed-117">Tworzenie certyfikatów Docker</span><span class="sxs-lookup"><span data-stu-id="46aed-117">Create Docker Certificates</span></span>
<span data-ttu-id="46aed-118">Po utworzeniu maszyny Wirtualnej, upewnij się, że Docker jest zainstalowany na komputerze klienckim.</span><span class="sxs-lookup"><span data-stu-id="46aed-118">After the VM has been created, ensure that Docker is installed on your client computer.</span></span> <span data-ttu-id="46aed-119">(Aby uzyskać więcej informacji, zobacz [instrukcje dotyczące instalacji Docker](https://docs.docker.com/installation/#installation).)</span><span class="sxs-lookup"><span data-stu-id="46aed-119">(For details, see [Docker installation instructions](https://docs.docker.com/installation/#installation).)</span></span>

<span data-ttu-id="46aed-120">Tworzenie plików certyfikat i klucz do komunikacji Docker zgodnie z [systemem Docker z protokołu https] i umieścić je w  **`~/.docker`**  katalogu na komputerze klienckim.</span><span class="sxs-lookup"><span data-stu-id="46aed-120">Create the certificate and key files for Docker communication according to [Running Docker with https] and place them in the **`~/.docker`** directory on your client computer.</span></span>

> [!NOTE]
> <span data-ttu-id="46aed-121">Rozszerzenia maszyny Wirtualnej platformy Docker w portalu obecnie wymagane poświadczenia, które są kodowany w standardzie base64.</span><span class="sxs-lookup"><span data-stu-id="46aed-121">The Docker VM Extension in the portal currently requires credentials that are base64 encoded.</span></span>
> 
> 

<span data-ttu-id="46aed-122">W wierszu polecenia, użyj  **`base64`**  lub innego ulubionego narzędzia kodowania, aby utworzyć tematy algorytmem Base64.</span><span class="sxs-lookup"><span data-stu-id="46aed-122">At the command line, use **`base64`** or another favorite encoding tool to create base64-encoded topics.</span></span> <span data-ttu-id="46aed-123">W ten sposób z prostym zestawem plików certyfikat i klucz może wyglądać podobnie do poniższego:</span><span class="sxs-lookup"><span data-stu-id="46aed-123">Doing this with a simple set of certificate and key files might look similar to this:</span></span>

```
 ~/.docker$ ls
 ca-key.pem  ca.pem  cert.pem  key.pem  server-cert.pem  server-key.pem
 ~/.docker$ base64 ca.pem > ca64.pem
 ~/.docker$ base64 server-cert.pem > server-cert64.pem
 ~/.docker$ base64 server-key.pem > server-key64.pem
 ~/.docker$ ls
 ca64.pem    ca.pem    key.pem            server-cert.pem   server-key.pem
 ca-key.pem  cert.pem  server-cert64.pem  server-key64.pem
```

## <a name="add-the-docker-vm-extension"></a><span data-ttu-id="46aed-124">Dodawanie rozszerzenia maszyny Wirtualnej platformy Docker</span><span class="sxs-lookup"><span data-stu-id="46aed-124">Add the Docker VM Extension</span></span>
<span data-ttu-id="46aed-125">Aby dodać Docker rozszerzenia maszyny Wirtualnej, zlokalizować wystąpienia maszyny Wirtualnej utworzone, a następnie przewiń w dół do **rozszerzenia** i kliknij go, aby wyświetlić rozszerzeń maszyny Wirtualnej, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="46aed-125">To add the Docker VM Extension, locate the VM instance you created and scroll down to **Extensions** and click it to bring up VM Extensions, as shown below.</span></span>

> [!NOTE]
> <span data-ttu-id="46aed-126">Ta funkcja jest obsługiwana w portalu w wersji zapoznawczej tylko: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="46aed-126">This functionality is supported in the preview portal only: https://portal.azure.com/</span></span>
> 
> 

![](media/portal-use-docker/ClickExtensions.png)

### <a name="add-an-extension"></a><span data-ttu-id="46aed-127">Dodaj rozszerzenie</span><span class="sxs-lookup"><span data-stu-id="46aed-127">Add an Extension</span></span>
<span data-ttu-id="46aed-128">Kliknij przycisk **+ Dodaj** do wyświetlenia możliwych rozszerzeń maszyny Wirtualnej, można dodać do tej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="46aed-128">Click the **+ Add** to display the possible VM Extensions you can add to this VM.</span></span>

![](media/portal-use-docker/ClickAdd.png)

### <a name="select-the-docker-vm-extension"></a><span data-ttu-id="46aed-129">Wybierz rozszerzenia maszyny Wirtualnej platformy Docker</span><span class="sxs-lookup"><span data-stu-id="46aed-129">Select the Docker VM Extension</span></span>
<span data-ttu-id="46aed-130">Wybierz Docker rozszerzenia maszyny Wirtualnej, który wywołuje Docker opis i ważne łącza, a następnie kliknij polecenie **Utwórz** na dole, aby rozpocząć procedurę instalacji.</span><span class="sxs-lookup"><span data-stu-id="46aed-130">Choose the Docker VM Extension, which brings up the Docker description and important links, and then click **Create** at the bottom to begin the installation procedure.</span></span>

![](media/portal-use-docker/ChooseDockerExtension.png)

![](media/portal-use-docker/CreateButtonFocus.png)

### <a name="add-your-certificate-and-key-files"></a><span data-ttu-id="46aed-131">Dodaj certyfikat i pliki klucza:</span><span class="sxs-lookup"><span data-stu-id="46aed-131">Add your Certificate and Key Files:</span></span>
<span data-ttu-id="46aed-132">Do pól formularza wprowadź algorytmem Base64 wersje certyfikat urzędu certyfikacji, certyfikat serwera i klucz serwera, jak pokazano na poniższym rysunku.</span><span class="sxs-lookup"><span data-stu-id="46aed-132">In the form fields, enter the base64-encoded versions of your CA Certificate, your Server Certificate, and your Server Key, as shown in the following graphic.</span></span>

![](media/portal-use-docker/AddExtensionFormFilled.png)

> [!NOTE]
> <span data-ttu-id="46aed-133">Należy pamiętać, czy (tak jak w poprzednim obrazu) 2376 wypełnieniu domyślnie.</span><span class="sxs-lookup"><span data-stu-id="46aed-133">Note that (as in the preceding image) the 2376 is filled in by default.</span></span> <span data-ttu-id="46aed-134">Możesz wprowadzić tutaj dowolnego punktu końcowego, ale następnym krokiem będzie otwarcie punktu końcowego pasującego.</span><span class="sxs-lookup"><span data-stu-id="46aed-134">You can enter any endpoint here, but the next step will be to open up the matching endpoint.</span></span> <span data-ttu-id="46aed-135">Wartość domyślna w przypadku zmiany, upewnij się, że otwarcie punktu końcowego pasującego w następnym kroku.</span><span class="sxs-lookup"><span data-stu-id="46aed-135">If you change the default, make sure to open up the matching endpoint in the next step.</span></span>
> 
> 

## <a name="add-the-docker-communication-endpoint"></a><span data-ttu-id="46aed-136">Dodaj punkt końcowy komunikacji Docker</span><span class="sxs-lookup"><span data-stu-id="46aed-136">Add the Docker Communication Endpoint</span></span>
<span data-ttu-id="46aed-137">Podczas wyświetlania po utworzeniu grupy zasobów, wybierz grupy zabezpieczeń sieci skojarzonych z maszyny Wirtualnej i kliknij przycisk **reguły zabezpieczeń ruchu przychodzącego** Aby wyświetlić reguły, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="46aed-137">When viewing the resource group you've created, select the Network Security Group associated with your VM, and click **Inbound Security Rules** to view the rules as shown here.</span></span>

![](media/portal-use-docker/AddingEndpoint.png)

<span data-ttu-id="46aed-138">Kliknij przycisk **+ Dodaj** dodanie inną regułę, a w przypadku domyślny, wprowadź nazwę dla punktu końcowego (w tym przykładzie **Docker**), a 2376 "zakres portów docelowych".</span><span class="sxs-lookup"><span data-stu-id="46aed-138">Click **+ Add** to add another rule, and in the default case, enter a name for the endpoint (in this example, **Docker**), and 2376 'Destination Port Range'.</span></span> <span data-ttu-id="46aed-139">Ustaw przedstawiający wartość protokołu **TCP**i kliknij przycisk **OK** do utworzenia reguły.</span><span class="sxs-lookup"><span data-stu-id="46aed-139">Set the protocol value showing **TCP**, and Click **OK** to create the rule.</span></span>

![](media/portal-use-docker/AddEndpointFormFilledOut.png)

## <a name="test-your-docker-client-and-azure-docker-host"></a><span data-ttu-id="46aed-140">Przetestować klienta Docker i hostów Azure Docker</span><span class="sxs-lookup"><span data-stu-id="46aed-140">Test your Docker Client and Azure Docker Host</span></span>
<span data-ttu-id="46aed-141">Zlokalizuj i skopiuj nazwę domeny maszyny Wirtualnej, a w wierszu polecenia na komputerze klienckim typu `docker --tls -H tcp://` *dockerextension* `.cloudapp.net:2376 info` (gdzie *dockerextension* zastępuje poddomeny dla maszyny Wirtualnej).</span><span class="sxs-lookup"><span data-stu-id="46aed-141">Locate and copy the name of your VM's domain, and at the command line of your client computer, type `docker --tls -H tcp://`*dockerextension*`.cloudapp.net:2376 info` (where *dockerextension* is replaced by the subdomain for your VM).</span></span>

<span data-ttu-id="46aed-142">Wynik powinien być podobny do poniższego:</span><span class="sxs-lookup"><span data-stu-id="46aed-142">The result should appear similar to this:</span></span>

```
$ docker --tls -H tcp://dockerextension.cloudapp.net:2376 info
Containers: 0
Images: 0
Storage Driver: devicemapper
 Pool Name: docker-8:1-131214-pool
 Pool Blocksize: 65.54 kB
 Data file: /var/lib/docker/devicemapper/devicemapper/data
 Metadata file: /var/lib/docker/devicemapper/devicemapper/metadata
 Data Space Used: 305.7 MB
 Data Space Total: 107.4 GB
 Metadata Space Used: 729.1 kB
 Metadata Space Total: 2.147 GB
 Library Version: 1.02.82-git (2013-10-04)
Execution Driver: native-0.2
Kernel Version: 3.13.0-36-generic
WARNING: No swap limit support
```

<span data-ttu-id="46aed-143">Po wykonaniu powyższych czynności masz teraz funkcjonalnej hostów Docker uruchomione na maszynie Wirtualnej platformy Azure, skonfigurować połączyć się zdalnie z innych klientów.</span><span class="sxs-lookup"><span data-stu-id="46aed-143">Once you complete the above steps, you now have a fully functional Docker host running on an Azure VM, configured to be connected to remotely from other clients.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="46aed-144">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="46aed-144">Next steps</span></span>
<span data-ttu-id="46aed-145">Wszystko będzie gotowe przejść do [Podręcznik użytkownika Docker] i użyć maszyny Wirtualnej platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="46aed-145">You are ready to go to the [Docker User Guide] and use your Docker VM.</span></span> <span data-ttu-id="46aed-146">Jeśli chcesz zautomatyzować tworzenie hostów Docker na maszynach wirtualnych Azure za pomocą interfejsu wiersza polecenia, zobacz [sposobu użycia Docker rozszerzenia maszyny Wirtualnej z interfejsu wiersza polecenia platformy Azure (Azure CLI)]</span><span class="sxs-lookup"><span data-stu-id="46aed-146">If you want to automate creating Docker hosts on Azure VMs through command line interface, see [How to use the Docker VM Extension from the Azure Command-line Interface (Azure CLI)]</span></span>

<!--Anchors-->
[Create a new VM from the Image Gallery]:#createvm
[Create Docker Certificates]:#dockercerts
[Add the Docker VM Extension]:#adddockerextension
[Test Docker Client and Azure Docker Host]:#testclientandserver
[Next steps]:#next-steps

<!--Image references-->
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[6]:./media/markdown-template-for-new-articles/pretty49.png
[7]:./media/markdown-template-for-new-articles/channel-9.png


<!--Link references-->
<span data-ttu-id="46aed-147">[sposobu użycia Docker rozszerzenia maszyny Wirtualnej z interfejsu wiersza polecenia platformy Azure (Azure CLI)]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-xplat-cli/</span><span class="sxs-lookup"><span data-stu-id="46aed-147">[How to use the Docker VM Extension from the Azure Command-line Interface (Azure CLI)]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-xplat-cli/</span></span>
<span data-ttu-id="46aed-148">[agenta systemu Linux Azure]:../agent-user-guide.md</span><span class="sxs-lookup"><span data-stu-id="46aed-148">[Azure Linux Agent]:../agent-user-guide.md</span></span>
[Link 3 to another azure.microsoft.com documentation topic]:../storage-whatis-account.md

<span data-ttu-id="46aed-149">[systemem Docker z protokołu https]:http://docs.docker.com/articles/https/</span><span class="sxs-lookup"><span data-stu-id="46aed-149">[Running Docker with https]:http://docs.docker.com/articles/https/</span></span>
<span data-ttu-id="46aed-150">[Podręcznik użytkownika Docker]:https://docs.docker.com/userguide/</span><span class="sxs-lookup"><span data-stu-id="46aed-150">[Docker User Guide]:https://docs.docker.com/userguide/</span></span>
