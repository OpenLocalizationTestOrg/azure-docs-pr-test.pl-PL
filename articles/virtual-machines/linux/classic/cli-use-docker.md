---
title: Witaj aaaUsing Docker rozszerzenia maszyny Wirtualnej dla systemu Linux na platformie Azure
description: "Opisuje Docker i rozszerzeń maszyny wirtualnej Azure hello i pokazuje, jak tooprogrammatically Tworzenie maszyn wirtualnych na platformie Azure, która hostów docker z wiersza polecenia hello przy użyciu interfejsu wiersza polecenia Azure hello."
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: eaff75e3-d929-4931-a4a1-8c377a8e7302
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/29/2016
ms.author: rasquill
ms.openlocfilehash: 1e192ad7c273aa9c997ea7bfa53b7de0b41a43c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-docker-vm-extension-from-hello-azure-command-line-interface-azure-cli"></a><span data-ttu-id="52393-103">Przy użyciu hello Docker rozszerzenia maszyny Wirtualnej z hello interfejsu wiersza polecenia platformy Azure (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="52393-103">Using hello Docker VM Extension from hello Azure Command-line Interface (Azure CLI)</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="52393-104">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="52393-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="52393-105">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="52393-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="52393-106">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="52393-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="52393-107">Aby dowiedzieć się, jak przy użyciu rozszerzenia maszyny Wirtualnej platformy Docker hello hello modelu Resource Manager, zobacz [tutaj](../dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="52393-107">For information about using hello Docker VM extension with hello Resource Manager model, see [here](../dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="52393-108">W tym temacie opisano, jak toocreate maszyny Wirtualnej z hello Docker rozszerzenia maszyny Wirtualnej z hello usługi zarządzania (asm) trybu w wiersza polecenia platformy Azure na dowolnej platformie.</span><span class="sxs-lookup"><span data-stu-id="52393-108">This topic describes how toocreate a VM with hello Docker VM Extension from hello service management (asm) mode in Azure CLI on any platform.</span></span> <span data-ttu-id="52393-109">[Docker](https://www.docker.com/) jest jednym z hello najpopularniejszych podejść wirtualizacji, które używa [kontenery Linux](http://en.wikipedia.org/wiki/LXC) zamiast maszyn wirtualnych w sposób izolowanie danych i przetwarzania danych w udostępnionych zasobów.</span><span class="sxs-lookup"><span data-stu-id="52393-109">[Docker](https://www.docker.com/) is one of hello most popular virtualization approaches that uses [Linux containers](http://en.wikipedia.org/wiki/LXC) rather than virtual machines as a way of isolating data and computing on shared resources.</span></span> <span data-ttu-id="52393-110">Można użyć rozszerzenia maszyny Wirtualnej platformy Docker hello i hello [agenta systemu Linux Azure](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate Docker maszyny Wirtualnej, który obsługuje dowolną liczbę kontenerów dla aplikacji na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="52393-110">You can use hello Docker VM extension and hello [Azure Linux Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate a Docker VM that hosts any number of containers for your applications on Azure.</span></span> <span data-ttu-id="52393-111">Ogólne omówienie kontenery i ich zalety toosee Zobacz hello [Docker wysoki poziom tablicy](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span><span class="sxs-lookup"><span data-stu-id="52393-111">toosee a high-level discussion of containers and their advantages, see hello [Docker High Level Whiteboard](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span></span>

## <a name="how-toouse-hello-docker-vm-extension-with-azure"></a><span data-ttu-id="52393-112">Jak toouse hello Docker rozszerzenia maszyny Wirtualnej z platformy Azure</span><span class="sxs-lookup"><span data-stu-id="52393-112">How toouse hello Docker VM Extension with Azure</span></span>
<span data-ttu-id="52393-113">toouse rozszerzenia maszyny Wirtualnej platformy Docker hello Azure, należy zainstalować wersję hello [interfejsu wiersza polecenia platformy Azure](https://github.com/Azure/azure-sdk-tools-xplat) (Azure CLI) wyższa niż 0.8.6 (zgodnie z tym hello pisania bieżąca wersja to 0.10.0).</span><span class="sxs-lookup"><span data-stu-id="52393-113">toouse hello Docker VM extension with Azure, you must install a version of hello [Azure Command-Line Interface](https://github.com/Azure/azure-sdk-tools-xplat) (Azure CLI) higher than 0.8.6 (as of this writing hello current version is 0.10.0).</span></span> <span data-ttu-id="52393-114">Witaj wiersza polecenia platformy Azure można zainstalować na Mac, Linux i Windows.</span><span class="sxs-lookup"><span data-stu-id="52393-114">You can install hello Azure CLI on Mac, Linux, and Windows.</span></span>

<span data-ttu-id="52393-115">Witaj Zakończ proces toouse Docker na platformie Azure jest prosty:</span><span class="sxs-lookup"><span data-stu-id="52393-115">hello complete process toouse Docker on Azure is simple:</span></span>

* <span data-ttu-id="52393-116">Zainstaluj na komputerze hello, z którego mają zostać toocontrol Azure hello wiersza polecenia platformy Azure i jego zależności (w systemie Windows, to będzie dystrybucji systemu Linux, uruchomione jako maszyny wirtualnej)</span><span class="sxs-lookup"><span data-stu-id="52393-116">Install hello Azure CLI and its dependencies on hello computer from which you want toocontrol Azure (on Windows, this will be a Linux distribution running as a virtual machine)</span></span>
* <span data-ttu-id="52393-117">Użyj hello Azure CLI Docker polecenia toocreate hosta maszyny Wirtualnej platformy Docker na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="52393-117">Use hello Azure CLI Docker commands toocreate a VM Docker host in Azure</span></span>
* <span data-ttu-id="52393-118">W maszynie Wirtualnej platformy Docker na platformie Azure, należy użyć toomanage polecenia Docker lokalne powitania kontenerów Docker.</span><span class="sxs-lookup"><span data-stu-id="52393-118">Use hello local Docker commands toomanage your Docker containers in your Docker VM in Azure.</span></span>

### <a name="install-hello-azure-command-line-interface-azure-cli"></a><span data-ttu-id="52393-119">Zainstaluj hello interfejsu wiersza polecenia platformy Azure (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="52393-119">Install hello Azure Command-Line Interface (Azure CLI)</span></span>
<span data-ttu-id="52393-120">tooinstall oraz konfigurowania hello wiersza polecenia platformy Azure, zobacz [jak tooinstall hello interfejsu wiersza polecenia platformy Azure](../../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="52393-120">tooinstall and configure hello Azure CLI, see [How tooinstall hello Azure Command-Line Interface](../../../cli-install-nodejs.md).</span></span> <span data-ttu-id="52393-121">tooconfirm hello instalacji, typ `azure` hello wiersza polecenia i po chwili krótkich powinna zostać wyświetlona hello grafikę ASCII interfejsu wiersza polecenia Azure, której znajduje się lista hello basic polecenia tooyou dostępne.</span><span class="sxs-lookup"><span data-stu-id="52393-121">tooconfirm hello installation, type `azure` at hello command prompt and after a short moment you should see hello Azure CLI ASCII art, which lists hello basic commands available tooyou.</span></span> <span data-ttu-id="52393-122">Jeśli instalacja hello działał poprawnie, należy tootype stanie `azure help vm` i sprawdzić, czy jest jedno z poleceń hello wymienione "docker".</span><span class="sxs-lookup"><span data-stu-id="52393-122">If hello installation worked correctly, you should be able tootype `azure help vm` and see that one of hello listed commands is "docker".</span></span>

> [!NOTE]
> <span data-ttu-id="52393-123">Docker ma narzędzi dla systemu Windows, [maszyny Docker](https://docs.docker.com/installation/windows/), która umożliwia także tworzenie hello tooautomate klienta docker czy toowork można używać z maszynami wirtualnymi Azure jako hostów docker.</span><span class="sxs-lookup"><span data-stu-id="52393-123">Docker has tools for Windows, [Docker Machine](https://docs.docker.com/installation/windows/), which you can also use tooautomate hello creation of a docker client that you can use toowork with Azure VMs as docker hosts.</span></span>
> 
> 

### <a name="connect-hello-azure-cli-tootooyour-azure-account"></a><span data-ttu-id="52393-124">Połącz hello Azure CLI tootooyour konto platformy Azure</span><span class="sxs-lookup"><span data-stu-id="52393-124">Connect hello Azure CLI tootooyour Azure Account</span></span>
<span data-ttu-id="52393-125">Przed użyciem hello Azure CLI poświadczenia konta Azure należy skojarzyć z hello Azure CLI na platformie.</span><span class="sxs-lookup"><span data-stu-id="52393-125">Before you can use hello Azure CLI you must associate your Azure account credentials with hello Azure CLI on your platform.</span></span> <span data-ttu-id="52393-126">Witaj sekcji [jak tooyour tooconnect subskrypcji platformy Azure](../../../xplat-cli-connect.md) wyjaśniono, jak tooeither pobierać i importować z **.publishsettings** plików lub kojarzenie z wiersza polecenia platformy Azure przy użyciu identyfikatora organizacyjnego.</span><span class="sxs-lookup"><span data-stu-id="52393-126">hello section [How tooconnect tooyour Azure subscription](../../../xplat-cli-connect.md) explains how tooeither download and import your **.publishsettings** file or associate your Azure CLI with an organizational id.</span></span>

> [!NOTE]
> <span data-ttu-id="52393-127">Istnieją pewne różnice w zachowaniu, korzystając z jednego lub hello innych metod uwierzytelniania, dlatego należy się, że dokument hello tooread powyżej toounderstand hello różne funkcje.</span><span class="sxs-lookup"><span data-stu-id="52393-127">There are some differences in behavior when using one or hello other methods of authentication, so do be sure tooread hello document above toounderstand hello different functionality.</span></span>
> 
> 

### <a name="install-docker-and-use-hello-docker-vm-extension-for-azure"></a><span data-ttu-id="52393-128">Zainstaluj Docker i użyj hello rozszerzenia maszyny Wirtualnej platformy Docker na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="52393-128">Install Docker and use hello Docker VM Extension for Azure</span></span>
<span data-ttu-id="52393-129">Wykonaj hello [instrukcje dotyczące instalacji Docker](https://docs.docker.com/installation/#installation) tooinstall Docker lokalnie na komputerze.</span><span class="sxs-lookup"><span data-stu-id="52393-129">Follow hello [Docker installation instructions](https://docs.docker.com/installation/#installation) tooinstall Docker locally on your computer.</span></span>

<span data-ttu-id="52393-130">toouse Docker z maszyny wirtualnej platformy Azure, hello Linux obraz powitania maszyna wirtualna musi mieć hello [Agent maszyny Wirtualnej systemu Linux](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="52393-130">toouse Docker with an Azure Virtual Machine, hello Linux image used for hello VM must have hello [Azure Linux VM Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) installed.</span></span> <span data-ttu-id="52393-131">Obecnie istnieją tylko dwa typy obrazów, które to zapewniają:</span><span class="sxs-lookup"><span data-stu-id="52393-131">Currently, there are only two types of images that provide this:</span></span>

* <span data-ttu-id="52393-132">Obraz Ubuntu z hello Galeria obrazów Azure lub</span><span class="sxs-lookup"><span data-stu-id="52393-132">An Ubuntu image from hello Azure Image Gallery or</span></span>
* <span data-ttu-id="52393-133">Niestandardowy obraz systemu Linux utworzone hello Agent maszyny Wirtualnej systemu Linux jest zainstalowana i skonfigurowana.</span><span class="sxs-lookup"><span data-stu-id="52393-133">A custom Linux image that you have created with hello Azure Linux VM Agent installed and configured.</span></span> <span data-ttu-id="52393-134">Zobacz [Agent maszyny Wirtualnej systemu Linux](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) Aby uzyskać więcej informacji o tym, jak toobuild niestandardowych maszyny Wirtualnej systemu Linux z hello Agent maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="52393-134">See [Azure Linux VM Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information about how toobuild a custom Linux VM with hello Azure VM Agent.</span></span>

### <a name="using-hello-azure-image-gallery"></a><span data-ttu-id="52393-135">Przy użyciu Galeria obrazów hello Azure</span><span class="sxs-lookup"><span data-stu-id="52393-135">Using hello Azure Image Gallery</span></span>
<span data-ttu-id="52393-136">Bash lub sesję terminalu Użyj funkcji powitania po toolocate hello najnowszy obraz Ubuntu w hello wirtualna galerii toouse, wpisując polecenie wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="52393-136">From a Bash or Terminal session, use hello following Azure CLI command toolocate hello most recent Ubuntu image in hello VM gallery toouse by typing</span></span>

`azure vm image list | grep Ubuntu-14_04`

<span data-ttu-id="52393-137">i wybierz jedną z nazw obraz powitania, takich jak `b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB`, i użyj hello następujące polecenie toocreate nowej maszyny Wirtualnej za pomocą tego obrazu.</span><span class="sxs-lookup"><span data-stu-id="52393-137">and select one of hello image names, such as `b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB`, and use hello following command toocreate a new VM using that image.</span></span>

```
azure vm docker create -e 22 -l "West US" <vm-cloudservice name> "b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB" <username> <password>
```

<span data-ttu-id="52393-138">Gdzie:</span><span class="sxs-lookup"><span data-stu-id="52393-138">where:</span></span>

* <span data-ttu-id="52393-139">*&lt;Nazwa maszyny wirtualnej cloudservice&gt;*  jest nazwą hello hello maszyny Wirtualnej, który ma zostać komputerze hosta kontenera Docker hello na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="52393-139">*&lt;vm-cloudservice name&gt;* is hello name of hello VM that will become hello Docker container host computer in Azure</span></span>
* <span data-ttu-id="52393-140">*&lt;Nazwa użytkownika&gt;*  jest nazwa hello hello domyślnego katalogu głównego użytkownika hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="52393-140">*&lt;username&gt;* is hello username of hello default root user of hello VM</span></span>
* <span data-ttu-id="52393-141">*&lt;hasło&gt;*  jest hasło hello hello *username* konta, spełniającej standardy hello złożoności dla platformy Azure</span><span class="sxs-lookup"><span data-stu-id="52393-141">*&lt;password&gt;* is hello password of hello *username* account that meets hello standards of complexity for Azure</span></span>

> [!NOTE]
> <span data-ttu-id="52393-142">Obecnie hasło musi być co najmniej 8 znaków, zawiera jeden małe litery i Wielka litera, liczbę i znaków specjalnych, takich jak jeden z następujących znaków hello: `!@#$%^&+=`.</span><span class="sxs-lookup"><span data-stu-id="52393-142">Currently, a password must be at least 8 characters, contain one lower case and one upper case character, a number, and a special character such as one of hello following characters: `!@#$%^&+=`.</span></span> <span data-ttu-id="52393-143">Nie, okres hello na końcu hello hello zdaniu poprzedzającym nie jest znak specjalny.</span><span class="sxs-lookup"><span data-stu-id="52393-143">No, hello period at hello end of hello preceding sentence is NOT a special character.</span></span>
> 
> 

<span data-ttu-id="52393-144">Jeśli polecenie hello zakończyło się pomyślnie, powinien zostać wyświetlony przypominać następujące hello, w zależności od hello dokładne argumentów i opcji, których użyto:</span><span class="sxs-lookup"><span data-stu-id="52393-144">If hello command was successful, you should see something like hello following, depending on hello precise arguments and options you used:</span></span>

![](media/cli-use-docker/dockercreateresults.png)

> [!NOTE]
> <span data-ttu-id="52393-145">Tworzenie maszyny wirtualnej może potrwać kilka minut, ale po zostały udostępnione (wartość stanu hello jest `ReadyRole`) hello uruchamiania demona (hello usługi Docker) Docker i możesz połączyć hosta kontenera Docker toohello.</span><span class="sxs-lookup"><span data-stu-id="52393-145">Creating a virtual machine can take a few minutes, but after it has been provisioned (hello state value is `ReadyRole`) hello Docker daemon (hello Docker service) starts and you can connect toohello Docker container host.</span></span>
> 
> 

<span data-ttu-id="52393-146">Witaj tootest Docker maszyny Wirtualnej zostały utworzone na platformie Azure, typ</span><span class="sxs-lookup"><span data-stu-id="52393-146">tootest hello Docker VM you have created in Azure, type</span></span>

`docker --tls -H tcp://<vm-name-you-used>.cloudapp.net:2376 info`

<span data-ttu-id="52393-147">gdzie  *&lt;vm nazwa--użyta&gt;*  jest nazwą hello hello maszyny wirtualnej, używany w połączeniu zbyt`azure vm docker create`.</span><span class="sxs-lookup"><span data-stu-id="52393-147">where *&lt;vm-name-you-used&gt;* is hello name of hello virtual machine that you used in your call too`azure vm docker create`.</span></span> <span data-ttu-id="52393-148">Powinny pojawić się coś podobnego następujące toohello, co oznacza, że Host maszyny Wirtualnej platformy Docker działa i działających na platformie Azure i Oczekiwanie na poleceniach.</span><span class="sxs-lookup"><span data-stu-id="52393-148">You should see something similar toohello following, which indicates that your Docker Host VM is up and running in Azure and waiting for your commands.</span></span> 

<span data-ttu-id="52393-149">Teraz możesz spróbować tooconnect przy użyciu informacji tooobtain docker klienta (w niektórych ustawień klienta Docker, takim jak dla komputerów Mac, konieczne może być toouse `sudo`):</span><span class="sxs-lookup"><span data-stu-id="52393-149">Now you can try tooconnect using your docker client tooobtain information (in some Docker client setups, such as that on Mac, you may have toouse `sudo`):</span></span>

    sudo docker --tls -H tcp://testsshasm.cloudapp.net:2376 info
    Password:
    Containers: 0
    Images: 0
    Storage Driver: devicemapper
    Pool Name: docker-8:1-131781-pool
    Pool Blocksize: 65.54 kB
    Backing Filesystem: extfs
    Data file: /dev/loop0
    Metadata file: /dev/loop1
    Data Space Used: 1.821 GB
    Data Space Total: 107.4 GB
    Data Space Available: 28 GB
    Metadata Space Used: 1.479 MB
    Metadata Space Total: 2.147 GB
    Metadata Space Available: 2.146 GB
    Udev Sync Supported: true
    Deferred Removal Enabled: false
    Data loop file: /var/lib/docker/devicemapper/devicemapper/data
    Metadata loop file: /var/lib/docker/devicemapper/devicemapper/metadata
    Library Version: 1.02.77 (2012-10-15)
    Execution Driver: native-0.2
    Logging Driver: json-file
    Kernel Version: 3.19.0-28-generic
    Operating System: Ubuntu 14.04.3 LTS
    CPUs: 1
    Total Memory: 1.637 GiB
    Name: testsshasm
    WARNING: No swap limit support

<span data-ttu-id="52393-150">Po prostu toobe pewność, że jest ona wszystkie pracy, można sprawdzić hello maszyny Wirtualnej dla hello Docker rozszerzenia:</span><span class="sxs-lookup"><span data-stu-id="52393-150">Just toobe certain that it's all working, you can examine hello VM for hello Docker extension:</span></span>

    azure vm extension get testsshasm
    info: Executing command vm extension get
    + Getting virtual machines
    data: Publisher Extension name ReferenceName Version State
    data: -------------------- --------------- ------------------------- ------- ------
    data: Microsoft.Azure.E... DockerExtension DockerExtension 1.* Enable
    info: vm extension get command OK

### <a name="docker-host-vm-authentication"></a><span data-ttu-id="52393-151">Uwierzytelnianie programu docker hosta maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="52393-151">Docker Host VM Authentication</span></span>
<span data-ttu-id="52393-152">Ponadto hello toocreating hello wirtualna Docker `azure vm docker create` polecenia automatycznie tworzy hello wymagane certyfikaty tooallow Docker klienta komputera tooconnect toohello kontenera platformy Azure hosta przy użyciu protokołu HTTPS i hello certyfikaty są przechowywane na serwerze Witaj klientem i hostem maszyny, zależnie od potrzeb.</span><span class="sxs-lookup"><span data-stu-id="52393-152">In addition toocreating hello Docker VM, hello `azure vm docker create` command also automatically creates hello necessary certificates tooallow your Docker client computer tooconnect toohello Azure container host using HTTPS, and hello certificates are stored on both hello client and host machines, as appropriate.</span></span> <span data-ttu-id="52393-153">Na kolejnych prób hello istniejących certyfikatów są ponownie i udostępniać hello nowego hosta.</span><span class="sxs-lookup"><span data-stu-id="52393-153">On subsequent attempts, hello existing certificates are reused and shared with hello new host.</span></span>

<span data-ttu-id="52393-154">Domyślnie certyfikaty są umieszczane w `~/.docker`, i Docker zostaną skonfigurowane toorun na porcie **2376**.</span><span class="sxs-lookup"><span data-stu-id="52393-154">By default, certificates are placed in `~/.docker`, and Docker will be configured toorun on port **2376**.</span></span> <span data-ttu-id="52393-155">Jeśli chcesz toouse inny port lub katalog, a następnie możesz skorzystać z jednej z następujących hello `azure vm docker create` wiersza polecenia Opcje tooconfigure Twojego Docker kontenera hosta maszyny Wirtualnej toouse inny port lub różnych certyfikatów klientów nawiązujących połączenie:</span><span class="sxs-lookup"><span data-stu-id="52393-155">If you would like toouse a different port or directory, then you may use one of hello following `azure vm docker create` command line options tooconfigure your Docker container host VM toouse a different port or different certificates for connecting clients:</span></span>

```
-dp, --docker-port [port]              Port toouse for docker [2376]
-dc, --docker-cert-dir [dir]           Directory containing docker certs [.docker/]
```

<span data-ttu-id="52393-156">Hello demon Docker na hoście hello jest toolisten skonfigurowanych dla i uwierzytelniania klienta połączeń na powitania określony port przy użyciu certyfikatów hello generowane przez hello `azure vm docker create` polecenia.</span><span class="sxs-lookup"><span data-stu-id="52393-156">hello Docker daemon on hello host is configured toolisten for and authenticate client connections on hello specified port using hello certificates generated by hello `azure vm docker create` command.</span></span> <span data-ttu-id="52393-157">komputer kliencki Hello muszą mieć te certyfikaty toogain dostępu toohello Docker hosta.</span><span class="sxs-lookup"><span data-stu-id="52393-157">hello client machine must have these certificates toogain access toohello Docker host.</span></span>

> [!NOTE]
> <span data-ttu-id="52393-158">Sieci hosta z systemem bez tych certyfikatów będzie tooanyone narażony, który można tooconnect toohello maszyny.</span><span class="sxs-lookup"><span data-stu-id="52393-158">A networked host running without these certificates will be vulnerable tooanyone that can tooconnect toohello machine.</span></span> <span data-ttu-id="52393-159">Przed zmodyfikowaniem hello domyślnej konfiguracji upewnij się, że rozumiesz hello ryzyka tooyour komputery i aplikacje.</span><span class="sxs-lookup"><span data-stu-id="52393-159">Before you modify hello default configuration, ensure that you understand hello risks tooyour computers and applications.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="52393-160">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="52393-160">Next steps</span></span>
* <span data-ttu-id="52393-161">Wszystko jest gotowe toogo toohello [Podręcznik użytkownika Docker] i użyć maszyny Wirtualnej platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="52393-161">You are ready toogo toohello [Docker User Guide] and use your Docker VM.</span></span> <span data-ttu-id="52393-162">Zobacz toocreate włączone Docker maszyny Wirtualnej w ramach nowego portalu hello [jak toouse hello Docker rozszerzenia maszyny Wirtualnej z hello Portal].</span><span class="sxs-lookup"><span data-stu-id="52393-162">toocreate a Docker-enabled VM in hello new portal, see [How toouse hello Docker VM Extension with hello Portal].</span></span>
* <span data-ttu-id="52393-163">Hello rozszerzenia maszyny Wirtualnej Azure Docker również obsługuje rozwiązania Docker Compose, który używa deklaratywne tootake pliku yaml programu modelowane Deweloper aplikacji w każdym środowisku i wygenerować spójne wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="52393-163">hello Azure Docker VM extension also supports Docker Compose, which uses a declarative YAML file tootake a developer-modeled application across any environment and generate a consistent deployment.</span></span> <span data-ttu-id="52393-164">Zobacz [Rozpoczynanie pracy z rozwiązaniem Docker tworzą toodefine i uruchomić aplikację usługi kontenera na maszynie wirtualnej platformy Azure].</span><span class="sxs-lookup"><span data-stu-id="52393-164">See [Get Started with Docker and Compose toodefine and run a multi-container application on an Azure virtual machine].</span></span>  

<!--Anchors-->
[Subheading 1]:#subheading-1
[Subheading 2]:#subheading-2
[Subheading 3]:#subheading-3
[Next steps]:#next-steps

[How toouse hello Docker VM Extension with Azure]:#How-to-use-the-Docker-VM-Extension-with-Azure
[Virtual Machine Extensions for Linux and Windows]:#Virtual-Machine-Extensions-For-Linux-and-Windows
[Container and Container Management Resources for Azure]:#Container-and-Container-Management-Resources-for-Azure



<!--Link references-->
[Link 1 tooanother azure.microsoft.com documentation topic]:../../virtual-machines-windows-hero-tutorial.md
[Link 2 tooanother azure.microsoft.com documentation topic]:../../../app-service-web/web-sites-custom-domain-name.md
[Link 3 tooanother azure.microsoft.com documentation topic]:../storage-whatis-account.md
[jak toouse hello Docker rozszerzenia maszyny Wirtualnej z hello Portal]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-portal/

[Podręcznik użytkownika Docker]:https://docs.docker.com/userguide/

[Rozpoczynanie pracy z rozwiązaniem Docker tworzą toodefine i uruchomić aplikację usługi kontenera na maszynie wirtualnej platformy Azure]:../docker-compose-quickstart.md
