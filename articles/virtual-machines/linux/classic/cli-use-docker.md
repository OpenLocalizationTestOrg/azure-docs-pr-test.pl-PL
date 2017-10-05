---
title: "Dla systemu Linux na platformie Azure przy użyciu rozszerzenia maszyny Wirtualnej platformy Docker"
description: "Opisuje Docker i rozszerzenia maszyny wirtualnej platformy Azure i pokazuje, jak programowo Tworzenie maszyn wirtualnych na platformie Azure, które są hostów docker z poziomu wiersza polecenia przy użyciu wiersza polecenia platformy Azure."
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
ms.openlocfilehash: a542332c921862241f1f000e6a8f0a0ae0e8a934
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-docker-vm-extension-from-the-azure-command-line-interface-azure-cli"></a><span data-ttu-id="4c139-103">Korzystanie z rozszerzenia maszyny wirtualnej platformy Docker za pomocą interfejsu wiersza polecenia platformy (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="4c139-103">Using the Docker VM Extension from the Azure Command-line Interface (Azure CLI)</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="4c139-104">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="4c139-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="4c139-105">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="4c139-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="4c139-106">Firma Microsoft zaleca, aby w przypadku większości nowych wdrożeń korzystać z modelu opartego na programie Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4c139-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="4c139-107">Aby dowiedzieć się, jak za pomocą rozszerzenia maszyny Wirtualnej platformy Docker z modelu Resource Manager, zobacz [tutaj](../dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4c139-107">For information about using the Docker VM extension with the Resource Manager model, see [here](../dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="4c139-108">W tym temacie opisano sposób tworzenia maszyny Wirtualnej z rozszerzenia maszyny Wirtualnej platformy Docker niż tryb zarządzania (asm) usługi Azure CLI na dowolnej platformie.</span><span class="sxs-lookup"><span data-stu-id="4c139-108">This topic describes how to create a VM with the Docker VM Extension from the service management (asm) mode in Azure CLI on any platform.</span></span> <span data-ttu-id="4c139-109">[Docker](https://www.docker.com/) jest jednym z najpopularniejszych podejść wirtualizacji, które używa [kontenery Linux](http://en.wikipedia.org/wiki/LXC) zamiast maszyn wirtualnych w sposób izolowanie danych i przetwarzania danych w udostępnionych zasobów.</span><span class="sxs-lookup"><span data-stu-id="4c139-109">[Docker](https://www.docker.com/) is one of the most popular virtualization approaches that uses [Linux containers](http://en.wikipedia.org/wiki/LXC) rather than virtual machines as a way of isolating data and computing on shared resources.</span></span> <span data-ttu-id="4c139-110">Można użyć rozszerzenia maszyny Wirtualnej platformy Docker i [agenta systemu Linux Azure](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tworzenie Docker maszyny Wirtualnej, który obsługuje dowolną liczbę kontenerów dla aplikacji na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="4c139-110">You can use the Docker VM extension and the [Azure Linux Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to create a Docker VM that hosts any number of containers for your applications on Azure.</span></span> <span data-ttu-id="4c139-111">Aby wyświetlić ogólne omówienie kontenery i ich zalety, zobacz [Docker wysoki poziom tablicy](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span><span class="sxs-lookup"><span data-stu-id="4c139-111">To see a high-level discussion of containers and their advantages, see the [Docker High Level Whiteboard](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span></span>

## <a name="how-to-use-the-docker-vm-extension-with-azure"></a><span data-ttu-id="4c139-112">Jak użyć Docker rozszerzenia maszyny Wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="4c139-112">How to use the Docker VM Extension with Azure</span></span>
<span data-ttu-id="4c139-113">Aby użyć rozszerzenia Docker maszyny Wirtualnej platformy Azure, należy zainstalować wersję [interfejsu wiersza polecenia platformy Azure](https://github.com/Azure/azure-sdk-tools-xplat) (Azure CLI) wyższa niż 0.8.6 (zgodnie z tym bieżąca wersja to 0.10.0).</span><span class="sxs-lookup"><span data-stu-id="4c139-113">To use the Docker VM extension with Azure, you must install a version of the [Azure Command-Line Interface](https://github.com/Azure/azure-sdk-tools-xplat) (Azure CLI) higher than 0.8.6 (as of this writing the current version is 0.10.0).</span></span> <span data-ttu-id="4c139-114">Interfejs wiersza polecenia platformy Azure można zainstalować na Mac, Linux i Windows.</span><span class="sxs-lookup"><span data-stu-id="4c139-114">You can install the Azure CLI on Mac, Linux, and Windows.</span></span>

<span data-ttu-id="4c139-115">Zakończenie procesu do użycia Docker na platformie Azure jest prosty:</span><span class="sxs-lookup"><span data-stu-id="4c139-115">The complete process to use Docker on Azure is simple:</span></span>

* <span data-ttu-id="4c139-116">Instalowanie interfejsu wiersza polecenia Azure i jego zależności na komputerze, z którego chcesz kontrolować Azure (w systemie Windows, to będzie dystrybucji systemu Linux, uruchomione jako maszyny wirtualnej)</span><span class="sxs-lookup"><span data-stu-id="4c139-116">Install the Azure CLI and its dependencies on the computer from which you want to control Azure (on Windows, this will be a Linux distribution running as a virtual machine)</span></span>
* <span data-ttu-id="4c139-117">Utwórz hosta maszyny Wirtualnej platformy Docker na platformie Azure za pomocą poleceń Azure CLI Docker</span><span class="sxs-lookup"><span data-stu-id="4c139-117">Use the Azure CLI Docker commands to create a VM Docker host in Azure</span></span>
* <span data-ttu-id="4c139-118">Lokalne polecenia Docker umożliwia zarządzanie kontenerów Docker w maszynie Wirtualnej platformy Docker na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="4c139-118">Use the local Docker commands to manage your Docker containers in your Docker VM in Azure.</span></span>

### <a name="install-the-azure-command-line-interface-azure-cli"></a><span data-ttu-id="4c139-119">Instalowanie platformy Azure interfejsu wiersza polecenia (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="4c139-119">Install the Azure Command-Line Interface (Azure CLI)</span></span>
<span data-ttu-id="4c139-120">Aby zainstalować i skonfigurować interfejs wiersza polecenia Azure, zobacz [jak zainstalować interfejs wiersza polecenia Azure](../../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="4c139-120">To install and configure the Azure CLI, see [How to install the Azure Command-Line Interface](../../../cli-install-nodejs.md).</span></span> <span data-ttu-id="4c139-121">Aby sprawdzić instalację, wpisz `azure` w wierszu polecenia i po chwili krótkich powinna zostać wyświetlona grafikę ASCII interfejsu wiersza polecenia Azure, który zawiera listę poleceń podstawowe dostępne dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="4c139-121">To confirm the installation, type `azure` at the command prompt and after a short moment you should see the Azure CLI ASCII art, which lists the basic commands available to you.</span></span> <span data-ttu-id="4c139-122">Jeśli instalacja działał poprawnie, powinno być możliwe do typu `azure help vm` i sprawdzić, czy jest jedną z wymienionych polecenia "docker".</span><span class="sxs-lookup"><span data-stu-id="4c139-122">If the installation worked correctly, you should be able to type `azure help vm` and see that one of the listed commands is "docker".</span></span>

> [!NOTE]
> <span data-ttu-id="4c139-123">Docker ma narzędzi dla systemu Windows, [maszyny Docker](https://docs.docker.com/installation/windows/), którym można również zautomatyzować tworzenie klienta docker, który służy do pracy z maszyn wirtualnych platformy Azure jako hostów docker.</span><span class="sxs-lookup"><span data-stu-id="4c139-123">Docker has tools for Windows, [Docker Machine](https://docs.docker.com/installation/windows/), which you can also use to automate the creation of a docker client that you can use to work with Azure VMs as docker hosts.</span></span>
> 
> 

### <a name="connect-the-azure-cli-to-to-your-azure-account"></a><span data-ttu-id="4c139-124">Azure CLI do nawiązania połączenia konta platformy Azure</span><span class="sxs-lookup"><span data-stu-id="4c139-124">Connect the Azure CLI to to your Azure Account</span></span>
<span data-ttu-id="4c139-125">Przed użyciem wiersza polecenia platformy Azure poświadczenia konta Azure należy skojarzyć z wiersza polecenia platformy Azure na platformie.</span><span class="sxs-lookup"><span data-stu-id="4c139-125">Before you can use the Azure CLI you must associate your Azure account credentials with the Azure CLI on your platform.</span></span> <span data-ttu-id="4c139-126">Sekcja [sposób nawiązywania połączenia z subskrypcją platformy Azure](../../../xplat-cli-connect.md) wyjaśniono, jak pobrać i zaimportować Twojej **.publishsettings** plików lub kojarzenie z wiersza polecenia platformy Azure przy użyciu identyfikatora organizacyjnego.</span><span class="sxs-lookup"><span data-stu-id="4c139-126">The section [How to connect to your Azure subscription](../../../xplat-cli-connect.md) explains how to either download and import your **.publishsettings** file or associate your Azure CLI with an organizational id.</span></span>

> [!NOTE]
> <span data-ttu-id="4c139-127">Istnieją pewne różnice w zachowaniu, korzystając z jednego lub innych metod uwierzytelniania, dlatego zaleca się przeczytanie dokumentu powyżej, aby poznać różne funkcje.</span><span class="sxs-lookup"><span data-stu-id="4c139-127">There are some differences in behavior when using one or the other methods of authentication, so do be sure to read the document above to understand the different functionality.</span></span>
> 
> 

### <a name="install-docker-and-use-the-docker-vm-extension-for-azure"></a><span data-ttu-id="4c139-128">Zainstaluj Docker i użyj rozszerzenia maszyny Wirtualnej platformy Docker na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="4c139-128">Install Docker and use the Docker VM Extension for Azure</span></span>
<span data-ttu-id="4c139-129">Postępuj zgodnie z [instrukcje dotyczące instalacji Docker](https://docs.docker.com/installation/#installation) zainstalować Docker lokalnie na komputerze.</span><span class="sxs-lookup"><span data-stu-id="4c139-129">Follow the [Docker installation instructions](https://docs.docker.com/installation/#installation) to install Docker locally on your computer.</span></span>

<span data-ttu-id="4c139-130">Aby użyć Docker z maszyny wirtualnej platformy Azure, musi mieć obraz Linux używany dla maszyny Wirtualnej [Agent maszyny Wirtualnej systemu Linux](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="4c139-130">To use Docker with an Azure Virtual Machine, the Linux image used for the VM must have the [Azure Linux VM Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) installed.</span></span> <span data-ttu-id="4c139-131">Obecnie istnieją tylko dwa typy obrazów, które to zapewniają:</span><span class="sxs-lookup"><span data-stu-id="4c139-131">Currently, there are only two types of images that provide this:</span></span>

* <span data-ttu-id="4c139-132">Obraz Ubuntu z galerii obrazów Azure lub</span><span class="sxs-lookup"><span data-stu-id="4c139-132">An Ubuntu image from the Azure Image Gallery or</span></span>
* <span data-ttu-id="4c139-133">Niestandardowy obraz systemu Linux utworzone przy użyciu agenta maszyny Wirtualnej systemu Linux Azure zainstalowane i skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="4c139-133">A custom Linux image that you have created with the Azure Linux VM Agent installed and configured.</span></span> <span data-ttu-id="4c139-134">Zobacz [Agent maszyny Wirtualnej systemu Linux](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) Aby uzyskać więcej informacji o sposobie tworzenia niestandardowych maszyny Wirtualnej systemu Linux przy użyciu agenta maszyny Wirtualnej Azure.</span><span class="sxs-lookup"><span data-stu-id="4c139-134">See [Azure Linux VM Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information about how to build a custom Linux VM with the Azure VM Agent.</span></span>

### <a name="using-the-azure-image-gallery"></a><span data-ttu-id="4c139-135">Za pomocą galerii Azure obrazu</span><span class="sxs-lookup"><span data-stu-id="4c139-135">Using the Azure Image Gallery</span></span>
<span data-ttu-id="4c139-136">Z Bash lub sesję terminalu Użyj następującego polecenia wiersza polecenia platformy Azure można znaleźć najnowszy Ubuntu obraz w galerii maszyn wirtualnych do użycia przez wpisanie</span><span class="sxs-lookup"><span data-stu-id="4c139-136">From a Bash or Terminal session, use the following Azure CLI command to locate the most recent Ubuntu image in the VM gallery to use by typing</span></span>

`azure vm image list | grep Ubuntu-14_04`

<span data-ttu-id="4c139-137">i wybierz jedną z nazw obrazów, takich jak `b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB`i użyj następującego polecenia, aby utworzyć nową maszynę Wirtualną za pomocą tego obrazu.</span><span class="sxs-lookup"><span data-stu-id="4c139-137">and select one of the image names, such as `b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB`, and use the following command to create a new VM using that image.</span></span>

```
azure vm docker create -e 22 -l "West US" <vm-cloudservice name> "b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB" <username> <password>
```

<span data-ttu-id="4c139-138">Gdzie:</span><span class="sxs-lookup"><span data-stu-id="4c139-138">where:</span></span>

* <span data-ttu-id="4c139-139">*&lt;Nazwa maszyny wirtualnej cloudservice&gt;*  jest nazwa maszyny wirtualnej, który ma zostać komputera hosta kontenera Docker na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="4c139-139">*&lt;vm-cloudservice name&gt;* is the name of the VM that will become the Docker container host computer in Azure</span></span>
* <span data-ttu-id="4c139-140">*&lt;Nazwa użytkownika&gt;*  jest nazwa użytkownika głównych domyślnego maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="4c139-140">*&lt;username&gt;* is the username of the default root user of the VM</span></span>
* <span data-ttu-id="4c139-141">*&lt;hasło&gt;*  jest hasło *username* konta, które spełnia wymogi złożoności dla platformy Azure</span><span class="sxs-lookup"><span data-stu-id="4c139-141">*&lt;password&gt;* is the password of the *username* account that meets the standards of complexity for Azure</span></span>

> [!NOTE]
> <span data-ttu-id="4c139-142">Obecnie hasło musi być co najmniej 8 znaków, zawiera jeden małe litery i Wielka litera, liczbę i znaków specjalnych, takich jak jeden z następujących znaków: `!@#$%^&+=`.</span><span class="sxs-lookup"><span data-stu-id="4c139-142">Currently, a password must be at least 8 characters, contain one lower case and one upper case character, a number, and a special character such as one of the following characters: `!@#$%^&+=`.</span></span> <span data-ttu-id="4c139-143">Nie, okres na końcu poprzedniego zdania nie jest znak specjalny.</span><span class="sxs-lookup"><span data-stu-id="4c139-143">No, the period at the end of the preceding sentence is NOT a special character.</span></span>
> 
> 

<span data-ttu-id="4c139-144">Jeśli polecenie zostało zakończone pomyślnie, powinien zostać wyświetlony przypominać następujące polecenie, w zależności od argumentów dokładne i opcje używanego:</span><span class="sxs-lookup"><span data-stu-id="4c139-144">If the command was successful, you should see something like the following, depending on the precise arguments and options you used:</span></span>

![](media/cli-use-docker/dockercreateresults.png)

> [!NOTE]
> <span data-ttu-id="4c139-145">Tworzenie maszyny wirtualnej może potrwać kilka minut, ale po zostały udostępnione (wartość stanu jest `ReadyRole`) uruchamiania demona Docker (usługa Docker) i możesz połączyć się z hostem kontenera Docker.</span><span class="sxs-lookup"><span data-stu-id="4c139-145">Creating a virtual machine can take a few minutes, but after it has been provisioned (the state value is `ReadyRole`) the Docker daemon (the Docker service) starts and you can connect to the Docker container host.</span></span>
> 
> 

<span data-ttu-id="4c139-146">Aby przetestować Docker maszyny Wirtualnej zostały utworzone na platformie Azure, wpisz</span><span class="sxs-lookup"><span data-stu-id="4c139-146">To test the Docker VM you have created in Azure, type</span></span>

`docker --tls -H tcp://<vm-name-you-used>.cloudapp.net:2376 info`

<span data-ttu-id="4c139-147">gdzie  *&lt;vm nazwa--użyta&gt;*  jest nazwa maszyny wirtualnej, który został użyty w wywołania do `azure vm docker create`.</span><span class="sxs-lookup"><span data-stu-id="4c139-147">where *&lt;vm-name-you-used&gt;* is the name of the virtual machine that you used in your call to `azure vm docker create`.</span></span> <span data-ttu-id="4c139-148">Powinny zostać wyświetlone informacje podobne do następujących, co oznacza, że Host maszyny Wirtualnej platformy Docker działa i działających na platformie Azure i Oczekiwanie na poleceniach.</span><span class="sxs-lookup"><span data-stu-id="4c139-148">You should see something similar to the following, which indicates that your Docker Host VM is up and running in Azure and waiting for your commands.</span></span> 

<span data-ttu-id="4c139-149">Teraz możesz spróbować połączyć się przy użyciu klienta programu docker można uzyskać informacji o (w niektórych ustawień klienta Docker, takim jak dla komputerów Mac, może być konieczne użycie `sudo`):</span><span class="sxs-lookup"><span data-stu-id="4c139-149">Now you can try to connect using your docker client to obtain information (in some Docker client setups, such as that on Mac, you may have to use `sudo`):</span></span>

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

<span data-ttu-id="4c139-150">Chcemy mieć pewność, że jest ona wszystkie pracy, należy zbadać Docker rozszerzenia maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="4c139-150">Just to be certain that it's all working, you can examine the VM for the Docker extension:</span></span>

    azure vm extension get testsshasm
    info: Executing command vm extension get
    + Getting virtual machines
    data: Publisher Extension name ReferenceName Version State
    data: -------------------- --------------- ------------------------- ------- ------
    data: Microsoft.Azure.E... DockerExtension DockerExtension 1.* Enable
    info: vm extension get command OK

### <a name="docker-host-vm-authentication"></a><span data-ttu-id="4c139-151">Uwierzytelnianie programu docker hosta maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="4c139-151">Docker Host VM Authentication</span></span>
<span data-ttu-id="4c139-152">Oprócz tworzenia wirtualna Docker `azure vm docker create` polecenia automatycznie tworzy wymagane certyfikaty, aby zezwolić na komputerze klienckim Docker do połączenia z hostem kontenera platformy Azure przy użyciu protokołu HTTPS, a certyfikaty są przechowywane na klienta i Host maszyn, zależnie od potrzeb.</span><span class="sxs-lookup"><span data-stu-id="4c139-152">In addition to creating the Docker VM, the `azure vm docker create` command also automatically creates the necessary certificates to allow your Docker client computer to connect to the Azure container host using HTTPS, and the certificates are stored on both the client and host machines, as appropriate.</span></span> <span data-ttu-id="4c139-153">W kolejnych prób istniejących certyfikatów są ponownie i udostępniane z nowym hostem.</span><span class="sxs-lookup"><span data-stu-id="4c139-153">On subsequent attempts, the existing certificates are reused and shared with the new host.</span></span>

<span data-ttu-id="4c139-154">Domyślnie certyfikaty są umieszczane w `~/.docker`, i Docker zostanie skonfigurowany do uruchamiania na porcie **2376**.</span><span class="sxs-lookup"><span data-stu-id="4c139-154">By default, certificates are placed in `~/.docker`, and Docker will be configured to run on port **2376**.</span></span> <span data-ttu-id="4c139-155">Jeśli chcesz użyć innego portu lub katalog, a następnie można użyć jednego z następujących `azure vm docker create` opcji wiersza polecenia, aby skonfigurować Twoje kontenera Docker hosta maszyny Wirtualnej, aby użyć innego portu lub różnych certyfikatów klientów nawiązujących połączenie:</span><span class="sxs-lookup"><span data-stu-id="4c139-155">If you would like to use a different port or directory, then you may use one of the following `azure vm docker create` command line options to configure your Docker container host VM to use a different port or different certificates for connecting clients:</span></span>

```
-dp, --docker-port [port]              Port to use for docker [2376]
-dc, --docker-cert-dir [dir]           Directory containing docker certs [.docker/]
```

<span data-ttu-id="4c139-156">Demon Docker na hoście jest skonfigurowana do nasłuchiwania i uwierzytelnianie połączeń klienta na określonym porcie przy użyciu certyfikaty generowane przez `azure vm docker create` polecenia.</span><span class="sxs-lookup"><span data-stu-id="4c139-156">The Docker daemon on the host is configured to listen for and authenticate client connections on the specified port using the certificates generated by the `azure vm docker create` command.</span></span> <span data-ttu-id="4c139-157">Komputer kliencki musi mieć te certyfikaty w celu uzyskania dostępu do hostów Docker.</span><span class="sxs-lookup"><span data-stu-id="4c139-157">The client machine must have these certificates to gain access to the Docker host.</span></span>

> [!NOTE]
> <span data-ttu-id="4c139-158">Sieci hosta z systemem bez tych certyfikatów będzie narażony na każdy użytkownik może połączyć się z komputerem.</span><span class="sxs-lookup"><span data-stu-id="4c139-158">A networked host running without these certificates will be vulnerable to anyone that can to connect to the machine.</span></span> <span data-ttu-id="4c139-159">Aby zmodyfikować domyślną konfigurację, upewnij się, że rozumiesz zagrożeń dotyczących komputerów i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4c139-159">Before you modify the default configuration, ensure that you understand the risks to your computers and applications.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="4c139-160">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4c139-160">Next steps</span></span>
* <span data-ttu-id="4c139-161">Wszystko będzie gotowe przejść do [Podręcznik użytkownika Docker] i użyć maszyny Wirtualnej platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="4c139-161">You are ready to go to the [Docker User Guide] and use your Docker VM.</span></span> <span data-ttu-id="4c139-162">Aby utworzyć Maszynę wirtualną z włączonym Docker w nowego portalu, zobacz [jak Docker rozszerzenia maszyny Wirtualnej za pomocą portalu].</span><span class="sxs-lookup"><span data-stu-id="4c139-162">To create a Docker-enabled VM in the new portal, see [How to use the Docker VM Extension with the Portal].</span></span>
* <span data-ttu-id="4c139-163">Rozszerzenie maszyny Wirtualnej platformy Docker Azure obsługuje również rozwiązania Docker Compose, używający deklaratywne pliku yaml programu do podjęcia modelowane Deweloper aplikacji w każdym środowisku oraz do generowania spójne wdrażanie.</span><span class="sxs-lookup"><span data-stu-id="4c139-163">The Azure Docker VM extension also supports Docker Compose, which uses a declarative YAML file to take a developer-modeled application across any environment and generate a consistent deployment.</span></span> <span data-ttu-id="4c139-164">Zobacz [wprowadzenie Docker i wysyłanych do definiowania i uruchomić aplikację usługi kontenera na maszynie wirtualnej platformy Azure].</span><span class="sxs-lookup"><span data-stu-id="4c139-164">See [Get Started with Docker and Compose to define and run a multi-container application on an Azure virtual machine].</span></span>  

<!--Anchors-->
[Subheading 1]:#subheading-1
[Subheading 2]:#subheading-2
[Subheading 3]:#subheading-3
[Next steps]:#next-steps

[How to use the Docker VM Extension with Azure]:#How-to-use-the-Docker-VM-Extension-with-Azure
[Virtual Machine Extensions for Linux and Windows]:#Virtual-Machine-Extensions-For-Linux-and-Windows
[Container and Container Management Resources for Azure]:#Container-and-Container-Management-Resources-for-Azure



<!--Link references-->
[Link 1 to another azure.microsoft.com documentation topic]:../../virtual-machines-windows-hero-tutorial.md
[Link 2 to another azure.microsoft.com documentation topic]:../../../app-service-web/web-sites-custom-domain-name.md
[Link 3 to another azure.microsoft.com documentation topic]:../storage-whatis-account.md
<span data-ttu-id="4c139-165">[jak Docker rozszerzenia maszyny Wirtualnej za pomocą portalu]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-portal/</span><span class="sxs-lookup"><span data-stu-id="4c139-165">[How to use the Docker VM Extension with the Portal]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-portal/</span></span>

<span data-ttu-id="4c139-166">[Podręcznik użytkownika Docker]:https://docs.docker.com/userguide/</span><span class="sxs-lookup"><span data-stu-id="4c139-166">[Docker User Guide]:https://docs.docker.com/userguide/</span></span>

<span data-ttu-id="4c139-167">[wprowadzenie Docker i wysyłanych do definiowania i uruchomić aplikację usługi kontenera na maszynie wirtualnej platformy Azure]:../docker-compose-quickstart.md</span><span class="sxs-lookup"><span data-stu-id="4c139-167">[Get Started with Docker and Compose to define and run a multi-container application on an Azure virtual machine]:../docker-compose-quickstart.md</span></span>
