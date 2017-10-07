---
title: aaaUsing Docker rozszerzenia maszyny Wirtualnej dla systemu Linux | Dokumentacja firmy Microsoft
description: "Opisuje Docker i hello rozszerzeń maszyny wirtualnej Azure oraz jak hello toocreate maszyn wirtualnych Azure, które są hostami docker przy użyciu wiersza polecenia platformy Azure w klasycznym modelu wdrażania."
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
ms.openlocfilehash: 9d455b63c48b0c1b6f14862e072f899a73b46153
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-docker-vm-extension-with-hello-azure-classic-portal"></a><span data-ttu-id="436cb-103">Przy użyciu hello Docker rozszerzenia maszyny Wirtualnej z hello klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="436cb-103">Using hello Docker VM Extension with hello Azure classic portal</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="436cb-104">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="436cb-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="436cb-105">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="436cb-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="436cb-106">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="436cb-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="436cb-107">[Docker](https://www.docker.com/) jest jednym z hello najpopularniejszych podejść wirtualizacji, które używa [kontenery Linux](http://en.wikipedia.org/wiki/LXC) zamiast maszyn wirtualnych w sposób izolowanie danych i przetwarzania danych w udostępnionych zasobów.</span><span class="sxs-lookup"><span data-stu-id="436cb-107">[Docker](https://www.docker.com/) is one of hello most popular virtualization approaches that uses [Linux containers](http://en.wikipedia.org/wiki/LXC) rather than virtual machines as a way of isolating data and computing on shared resources.</span></span> <span data-ttu-id="436cb-108">Można użyć rozszerzenia maszyny Wirtualnej platformy Docker hello zarządza [agenta systemu Linux Azure] toocreate Docker maszyny Wirtualnej, który obsługuje dowolną liczbę kontenerów dla aplikacji na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="436cb-108">You can use hello Docker VM extension managed by [Azure Linux Agent] toocreate a Docker VM that hosts any number of containers for your applications on Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="436cb-109">W tym temacie opisano, jak toocreate a VM Docker z hello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="436cb-109">This topic describes how toocreate a Docker VM from hello Azure classic portal.</span></span> <span data-ttu-id="436cb-110">toosee toocreate maszyny Wirtualnej platformy Docker w wierszu polecenia hello, zobacz temat [jak toouse hello Docker rozszerzenia maszyny Wirtualnej z interfejsu wiersza polecenia platformy Azure (Azure CLI) hello].</span><span class="sxs-lookup"><span data-stu-id="436cb-110">toosee how toocreate a Docker VM at hello command line, see [How toouse hello Docker VM Extension from hello Azure Command-line Interface (Azure CLI)].</span></span> <span data-ttu-id="436cb-111">Ogólne omówienie kontenery i ich zalety toosee Zobacz hello [Docker wysoki poziom tablicy](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span><span class="sxs-lookup"><span data-stu-id="436cb-111">toosee a high-level discussion of containers and their advantages, see hello [Docker High Level Whiteboard](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span></span>
> 
> 

## <a name="create-a-new-vm-from-hello-image-gallery"></a><span data-ttu-id="436cb-112">Utwórz nową maszynę Wirtualną na podstawie hello Galeria obrazów</span><span class="sxs-lookup"><span data-stu-id="436cb-112">Create a new VM from hello Image Gallery</span></span>
<span data-ttu-id="436cb-113">pierwszym krokiem Hello wymaga maszyny Wirtualnej platformy Azure z obrazu systemu Linux, który obsługuje hello Docker rozszerzenia maszyny Wirtualnej, przy użyciu obrazu Ubuntu 14.04 LTS z hello Galeria obrazów jako przykład obrazu serwera i Ubuntu 14.04 pulpitu jako klienta.</span><span class="sxs-lookup"><span data-stu-id="436cb-113">hello first step requires an Azure VM from a Linux image that supports hello Docker VM Extension, using an Ubuntu 14.04 LTS image from hello Image Gallery as an example server image and Ubuntu 14.04 Desktop as a client.</span></span> <span data-ttu-id="436cb-114">W portalu powitania kliknij **+ nowy** w hello lewy dolny róg toocreate nowe wystąpienie maszyny Wirtualnej, a następnie wybierz obraz Ubuntu 14.04 LTS z dostępnych opcji hello lub hello ukończyć Galeria obrazów, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="436cb-114">In hello portal, click **+ New** in hello bottom left corner toocreate a new VM instance and select an Ubuntu 14.04 LTS image from hello selections available or from hello complete Image Gallery, as shown below.</span></span>

> [!NOTE]
> <span data-ttu-id="436cb-115">Obecnie tylko obrazy Ubuntu 14.04 LTS nowsza niż lipca 2014 obsługują hello Docker rozszerzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="436cb-115">Currently, only Ubuntu 14.04 LTS images more recent than July 2014 support hello Docker VM Extension.</span></span>
> 
> 

![Utwórz nowy obraz Ubuntu](./media/portal-use-docker/ChooseUbuntu.png)

## <a name="create-docker-certificates"></a><span data-ttu-id="436cb-117">Tworzenie certyfikatów Docker</span><span class="sxs-lookup"><span data-stu-id="436cb-117">Create Docker Certificates</span></span>
<span data-ttu-id="436cb-118">Po hello utworzenia maszyny Wirtualnej upewnij się, że Docker jest zainstalowany na komputerze klienckim.</span><span class="sxs-lookup"><span data-stu-id="436cb-118">After hello VM has been created, ensure that Docker is installed on your client computer.</span></span> <span data-ttu-id="436cb-119">(Aby uzyskać więcej informacji, zobacz [instrukcje dotyczące instalacji Docker](https://docs.docker.com/installation/#installation).)</span><span class="sxs-lookup"><span data-stu-id="436cb-119">(For details, see [Docker installation instructions](https://docs.docker.com/installation/#installation).)</span></span>

<span data-ttu-id="436cb-120">Utwórz hello certyfikat i klucz pliki komunikacji Docker zbyt zgodnie z[systemem Docker z protokołu https] i umieścić je w hello  **`~/.docker`**  katalogu na komputerze klienckim.</span><span class="sxs-lookup"><span data-stu-id="436cb-120">Create hello certificate and key files for Docker communication according too[Running Docker with https] and place them in hello **`~/.docker`** directory on your client computer.</span></span>

> [!NOTE]
> <span data-ttu-id="436cb-121">Witaj Docker rozszerzenia maszyny Wirtualnej w portalu hello obecnie wymaga poświadczeń kodowany w standardzie base64.</span><span class="sxs-lookup"><span data-stu-id="436cb-121">hello Docker VM Extension in hello portal currently requires credentials that are base64 encoded.</span></span>
> 
> 

<span data-ttu-id="436cb-122">W wierszu polecenia hello, użyj  **`base64`**  lub innego elementu ulubionego kodowanie tematy dotyczące narzędzia toocreate algorytmem Base64.</span><span class="sxs-lookup"><span data-stu-id="436cb-122">At hello command line, use **`base64`** or another favorite encoding tool toocreate base64-encoded topics.</span></span> <span data-ttu-id="436cb-123">W ten sposób z prostym zestawem plików certyfikat i klucz może wyglądać podobnie toothis:</span><span class="sxs-lookup"><span data-stu-id="436cb-123">Doing this with a simple set of certificate and key files might look similar toothis:</span></span>

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

## <a name="add-hello-docker-vm-extension"></a><span data-ttu-id="436cb-124">Dodaj hello Docker rozszerzenia maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="436cb-124">Add hello Docker VM Extension</span></span>
<span data-ttu-id="436cb-125">tooadd hello rozszerzenia maszyny Wirtualnej platformy Docker Znajdź hello wystąpienia maszyny Wirtualnej został utworzony i przewiń w dół za**rozszerzenia** i kliknij go toobring się rozszerzeń maszyny Wirtualnej, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="436cb-125">tooadd hello Docker VM Extension, locate hello VM instance you created and scroll down too**Extensions** and click it toobring up VM Extensions, as shown below.</span></span>

> [!NOTE]
> <span data-ttu-id="436cb-126">Ta funkcja jest obsługiwana w portalu w wersji zapoznawczej hello tylko: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="436cb-126">This functionality is supported in hello preview portal only: https://portal.azure.com/</span></span>
> 
> 

![](media/portal-use-docker/ClickExtensions.png)

### <a name="add-an-extension"></a><span data-ttu-id="436cb-127">Dodaj rozszerzenie</span><span class="sxs-lookup"><span data-stu-id="436cb-127">Add an Extension</span></span>
<span data-ttu-id="436cb-128">Kliknij przycisk hello **+ Dodaj** toodisplay hello możliwych rozszerzeń maszyny Wirtualnej można dodać toothis maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="436cb-128">Click hello **+ Add** toodisplay hello possible VM Extensions you can add toothis VM.</span></span>

![](media/portal-use-docker/ClickAdd.png)

### <a name="select-hello-docker-vm-extension"></a><span data-ttu-id="436cb-129">Wybierz hello Docker rozszerzenia maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="436cb-129">Select hello Docker VM Extension</span></span>
<span data-ttu-id="436cb-130">Wybierz hello Docker rozszerzenia maszyny Wirtualnej, który wywołuje hello Docker opis i ważne łącza, a następnie kliknij przycisk **Utwórz** na powitania dolnej toobegin hello instalacji procedurze.</span><span class="sxs-lookup"><span data-stu-id="436cb-130">Choose hello Docker VM Extension, which brings up hello Docker description and important links, and then click **Create** at hello bottom toobegin hello installation procedure.</span></span>

![](media/portal-use-docker/ChooseDockerExtension.png)

![](media/portal-use-docker/CreateButtonFocus.png)

### <a name="add-your-certificate-and-key-files"></a><span data-ttu-id="436cb-131">Dodaj certyfikat i pliki klucza:</span><span class="sxs-lookup"><span data-stu-id="436cb-131">Add your Certificate and Key Files:</span></span>
<span data-ttu-id="436cb-132">Hello pól formularza wprowadź hello algorytmem Base64 wersji certyfikat urzędu certyfikacji, certyfikat serwera i klucz serwera, jak pokazano w powitania po grafiki.</span><span class="sxs-lookup"><span data-stu-id="436cb-132">In hello form fields, enter hello base64-encoded versions of your CA Certificate, your Server Certificate, and your Server Key, as shown in hello following graphic.</span></span>

![](media/portal-use-docker/AddExtensionFormFilled.png)

> [!NOTE]
> <span data-ttu-id="436cb-133">Należy pamiętać, że (jak hello poprzedzające obraz) hello 2376 jest wypełniane domyślnie.</span><span class="sxs-lookup"><span data-stu-id="436cb-133">Note that (as in hello preceding image) hello 2376 is filled in by default.</span></span> <span data-ttu-id="436cb-134">Możesz wprowadzić tutaj dowolnego punktu końcowego, ale hello następnym krokiem będzie tooopen się hello dopasowania punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="436cb-134">You can enter any endpoint here, but hello next step will be tooopen up hello matching endpoint.</span></span> <span data-ttu-id="436cb-135">W przypadku zmiany domyślnego hello, upewnij się, że tooopen się hello dopasowania punktu końcowego w następnym kroku hello.</span><span class="sxs-lookup"><span data-stu-id="436cb-135">If you change hello default, make sure tooopen up hello matching endpoint in hello next step.</span></span>
> 
> 

## <a name="add-hello-docker-communication-endpoint"></a><span data-ttu-id="436cb-136">Dodaj hello punkt końcowy komunikacji Docker</span><span class="sxs-lookup"><span data-stu-id="436cb-136">Add hello Docker Communication Endpoint</span></span>
<span data-ttu-id="436cb-137">Podczas wyświetlania po utworzeniu grupy zasobów hello, wybierz hello grupy zabezpieczeń sieci skojarzonych z maszyny Wirtualnej i kliknij **reguły zabezpieczeń ruchu przychodzącego** tooview hello reguł, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="436cb-137">When viewing hello resource group you've created, select hello Network Security Group associated with your VM, and click **Inbound Security Rules** tooview hello rules as shown here.</span></span>

![](media/portal-use-docker/AddingEndpoint.png)

<span data-ttu-id="436cb-138">Kliknij przycisk **+ Dodaj** tooadd inną regułę, a w przypadku domyślnego hello, wprowadź nazwę dla punktu końcowego hello (w tym przykładzie **Docker**), a 2376 "zakres portów docelowych".</span><span class="sxs-lookup"><span data-stu-id="436cb-138">Click **+ Add** tooadd another rule, and in hello default case, enter a name for hello endpoint (in this example, **Docker**), and 2376 'Destination Port Range'.</span></span> <span data-ttu-id="436cb-139">Ustaw przedstawiający wartość protokołu hello **TCP**i kliknij przycisk **OK** toocreate hello reguły.</span><span class="sxs-lookup"><span data-stu-id="436cb-139">Set hello protocol value showing **TCP**, and Click **OK** toocreate hello rule.</span></span>

![](media/portal-use-docker/AddEndpointFormFilledOut.png)

## <a name="test-your-docker-client-and-azure-docker-host"></a><span data-ttu-id="436cb-140">Przetestować klienta Docker i hostów Azure Docker</span><span class="sxs-lookup"><span data-stu-id="436cb-140">Test your Docker Client and Azure Docker Host</span></span>
<span data-ttu-id="436cb-141">Zlokalizuj i skopiuj hello nazwy domeny maszyny Wirtualnej, a w wierszu polecenia hello komputera klienta typu `docker --tls -H tcp://` *dockerextension* `.cloudapp.net:2376 info` (gdzie *dockerextension* zastępuje hello poddomeny dla maszyny Wirtualnej).</span><span class="sxs-lookup"><span data-stu-id="436cb-141">Locate and copy hello name of your VM's domain, and at hello command line of your client computer, type `docker --tls -H tcp://`*dockerextension*`.cloudapp.net:2376 info` (where *dockerextension* is replaced by hello subdomain for your VM).</span></span>

<span data-ttu-id="436cb-142">wynik Hello powinna zostać wyświetlona toothis podobne:</span><span class="sxs-lookup"><span data-stu-id="436cb-142">hello result should appear similar toothis:</span></span>

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

<span data-ttu-id="436cb-143">Po zakończeniu hello powyżej kroki masz teraz funkcjonalnej hostów Docker uruchomione na maszynie Wirtualnej platformy Azure, skonfigurować toobe połączone tooremotely z innych klientów.</span><span class="sxs-lookup"><span data-stu-id="436cb-143">Once you complete hello above steps, you now have a fully functional Docker host running on an Azure VM, configured toobe connected tooremotely from other clients.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="436cb-144">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="436cb-144">Next steps</span></span>
<span data-ttu-id="436cb-145">Wszystko jest gotowe toogo toohello [Podręcznik użytkownika Docker] i użyć maszyny Wirtualnej platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="436cb-145">You are ready toogo toohello [Docker User Guide] and use your Docker VM.</span></span> <span data-ttu-id="436cb-146">Jeśli tooautomate tworzenie hostów Docker na maszynach wirtualnych Azure za pomocą interfejsu wiersza polecenia, zobacz [jak toouse hello Docker rozszerzenia maszyny Wirtualnej z interfejsu wiersza polecenia platformy Azure (Azure CLI) hello]</span><span class="sxs-lookup"><span data-stu-id="436cb-146">If you want tooautomate creating Docker hosts on Azure VMs through command line interface, see [How toouse hello Docker VM Extension from hello Azure Command-line Interface (Azure CLI)]</span></span>

<!--Anchors-->
[Create a new VM from hello Image Gallery]:#createvm
[Create Docker Certificates]:#dockercerts
[Add hello Docker VM Extension]:#adddockerextension
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
[jak toouse hello Docker rozszerzenia maszyny Wirtualnej z interfejsu wiersza polecenia platformy Azure (Azure CLI) hello]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-xplat-cli/
[agenta systemu Linux Azure]:../agent-user-guide.md
[Link 3 tooanother azure.microsoft.com documentation topic]:../storage-whatis-account.md

[systemem Docker z protokołu https]:http://docs.docker.com/articles/https/
[Podręcznik użytkownika Docker]:https://docs.docker.com/userguide/
