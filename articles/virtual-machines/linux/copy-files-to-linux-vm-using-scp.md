---
title: "aaaMove pliki tooand z maszyn wirtualnych systemu Linux platformy Azure z punktu połączenia usługi | Dokumentacja firmy Microsoft"
description: "Bezpiecznie przenieść tooand plików z maszyny Wirtualnej systemu Linux na platformie Azure przy użyciu połączenia usługi i parę kluczy SSH."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: danlep
ms.openlocfilehash: 9e4dce667aa581df74aec3d45a6ba5e52f777d1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-files-tooand-from-a-linux-vm-using-scp"></a><span data-ttu-id="40592-103">Przenieś pliki tooand z maszyny Wirtualnej systemu Linux przy użyciu połączenia usługi</span><span class="sxs-lookup"><span data-stu-id="40592-103">Move files tooand from a Linux VM using SCP</span></span>

<span data-ttu-id="40592-104">W tym artykule opisano, jak toomove pliki z stacji roboczej w górę tooan maszyny Wirtualnej systemu Linux platformy Azure lub Azure maszyny Wirtualnej systemu Linux w dół tooyour stacji roboczej, przy użyciu bezpiecznego kopiowania (SCP).</span><span class="sxs-lookup"><span data-stu-id="40592-104">This article shows how toomove files from your workstation up tooan Azure Linux VM, or from an Azure Linux VM down tooyour workstation, using Secure Copy (SCP).</span></span> <span data-ttu-id="40592-105">Przenoszenie plików między tą stacją roboczą a Maszynę wirtualną systemu Linux, szybkie i bezpieczne, jest szczególnie ważne dla zarządzania infrastrukturą platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="40592-105">Moving files between your workstation and a Linux VM, quickly and securely, is critical for managing your Azure infrastructure.</span></span> 

<span data-ttu-id="40592-106">W tym artykule należy Linux maszyn wirtualnych wdrożonych w Azure przy użyciu [SSH publiczne i prywatne pliki klucza](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="40592-106">For this article, you need a Linux VM deployed in Azure using [SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="40592-107">Należy również połączenia klienta dla komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="40592-107">You also need an SCP client for your local computer.</span></span> <span data-ttu-id="40592-108">Jest oparty na SSH i zawarte w powłoki Bash domyślne hello większość komputerów z systemami Linux i komputerów Mac i niektóre powłoki systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="40592-108">It is built on top of SSH and included in hello default Bash shell of most Linux and Mac computers and some Windows shells.</span></span>

## <a name="quick-commands"></a><span data-ttu-id="40592-109">Szybkie polecenia</span><span class="sxs-lookup"><span data-stu-id="40592-109">Quick commands</span></span>

<span data-ttu-id="40592-110">Skopiuj plik się toohello maszyny Wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="40592-110">Copy a file up toohello Linux VM</span></span>

```bash
scp file azureuser@azurehost:directory/targetfile
```

<span data-ttu-id="40592-111">Skopiuj plik w dół z hello maszyny Wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="40592-111">Copy a file down from hello Linux VM</span></span>

```bash
scp azureuser@azurehost:directory/file targetfile
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="40592-112">Szczegółowy przewodnik</span><span class="sxs-lookup"><span data-stu-id="40592-112">Detailed walkthrough</span></span>

<span data-ttu-id="40592-113">Jako przykład możemy przenieść pliku konfiguracji platformy Azure w górę tooa maszyny Wirtualnej systemu Linux i rozwiń katalog pliku dziennika używają kluczy punkt połączenia usługi oraz SSH.</span><span class="sxs-lookup"><span data-stu-id="40592-113">As examples, we move an Azure configuration file up tooa Linux VM and pull down a log file directory, both using SCP and SSH keys.</span></span>   

## <a name="ssh-key-pair-authentication"></a><span data-ttu-id="40592-114">Uwierzytelnianie pary kluczy SSH</span><span class="sxs-lookup"><span data-stu-id="40592-114">SSH key pair authentication</span></span>

<span data-ttu-id="40592-115">Punkt połączenia usługi używa SSH hello warstwy transportowej.</span><span class="sxs-lookup"><span data-stu-id="40592-115">SCP uses SSH for hello transport layer.</span></span> <span data-ttu-id="40592-116">SSH uchwytów hello uwierzytelniania na hoście docelowym hello i przenosi plik hello w tunelu zaszyfrowanych domyślnie dostępne przy użyciu protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="40592-116">SSH handles hello authentication on hello destination host, and it moves hello file in an encrypted tunnel provided by default with SSH.</span></span> <span data-ttu-id="40592-117">W przypadku uwierzytelniania SSH można użyć nazwy użytkowników i hasła.</span><span class="sxs-lookup"><span data-stu-id="40592-117">For SSH authentication, usernames and passwords can be used.</span></span> <span data-ttu-id="40592-118">Jednak najlepszym rozwiązaniem bezpieczeństwa zaleca się SSH publicznego i prywatnego klucza uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="40592-118">However, SSH public and private key authentication are recommended as a security best practice.</span></span> <span data-ttu-id="40592-119">Po uwierzytelnieniu hello połączenia SSH SCP następnie rozpoczyna się kopiowanie pliku hello.</span><span class="sxs-lookup"><span data-stu-id="40592-119">Once SSH has authenticated hello connection, SCP then begins copying hello file.</span></span> <span data-ttu-id="40592-120">Przy użyciu poprawnego skonfigurowania `~/.ssh/config` i publicznymi i prywatnymi kluczy SSH, połączenie hello punkt połączenia usługi można nawiązać za pomocą tylko nazwa serwera (lub adres IP).</span><span class="sxs-lookup"><span data-stu-id="40592-120">Using a properly configured `~/.ssh/config` and SSH public and private keys, hello SCP connection can be established by just using a server name (or IP address).</span></span> <span data-ttu-id="40592-121">Jeśli masz tylko jeden klucz SSH, punkt połączenia usługi szuka go w hello `~/.ssh/` katalogu i używa go przez domyślny toolog w toohello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="40592-121">If you only have one SSH key, SCP looks for it in hello `~/.ssh/` directory, and uses it by default toolog in toohello VM.</span></span>

<span data-ttu-id="40592-122">Aby uzyskać więcej informacji na temat konfigurowania sieci `~/.ssh/config` i kluczy publicznych i prywatnych SSH, zobacz [utworzyć SSH klucze](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="40592-122">For more information on configuring your `~/.ssh/config` and SSH public and private keys, see [Create SSH keys](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="scp-a-file-tooa-linux-vm"></a><span data-ttu-id="40592-123">Punkt połączenia usługi tooa plików maszyny Wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="40592-123">SCP a file tooa Linux VM</span></span>

<span data-ttu-id="40592-124">Na przykład pierwszy hello firma Microsoft skopiuj plik konfiguracji platformy Azure się tooa maszyny Wirtualnej systemu Linux, który jest używany toodeploy automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="40592-124">For hello first example, we copy an Azure configuration file up tooa Linux VM that is used toodeploy automation.</span></span> <span data-ttu-id="40592-125">Ponieważ ten plik zawiera interfejsu API Azure poświadczenia, których klucze tajne, ważne jest zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="40592-125">Because this file contains Azure API credentials, which include secrets, security is important.</span></span> <span data-ttu-id="40592-126">szyfrowany tunel Hello udostępniane przez SSH chroni zawartość hello hello pliku.</span><span class="sxs-lookup"><span data-stu-id="40592-126">hello encrypted tunnel provided by SSH protects hello contents of hello file.</span></span>

<span data-ttu-id="40592-127">Witaj następujące lokalne powitania kopie polecenia *.azure/config* pliku tooan maszyny Wirtualnej platformy Azure z nazwą FQDN *myserver.eastus.cloudapp.azure.com*. nazwa użytkownika administratora hello na powitania maszyny Wirtualnej platformy Azure jest *azureuser* .</span><span class="sxs-lookup"><span data-stu-id="40592-127">hello following command copies hello local *.azure/config* file tooan Azure VM with FQDN *myserver.eastus.cloudapp.azure.com*. hello admin user name on hello Azure VM is *azureuser*.</span></span> <span data-ttu-id="40592-128">Hello plik jest docelowe toohello */home/azureuser/* katalogu.</span><span class="sxs-lookup"><span data-stu-id="40592-128">hello file is targeted toohello */home/azureuser/* directory.</span></span> <span data-ttu-id="40592-129">Zastąp wartości w tym poleceniu.</span><span class="sxs-lookup"><span data-stu-id="40592-129">Substitute your own values in this command.</span></span>

```bash
scp ~/.azure/config azureuser@myserver.eastus.cloudapp.com:/home/azureuser/config
```

## <a name="scp-a-directory-from-a-linux-vm"></a><span data-ttu-id="40592-130">Punkt połączenia usługi katalogu z maszyny Wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="40592-130">SCP a directory from a Linux VM</span></span>

<span data-ttu-id="40592-131">Na przykład firma Microsoft Skopiuj katalog plików dziennika z hello maszyny Wirtualnej systemu Linux w dół tooyour stacji roboczej.</span><span class="sxs-lookup"><span data-stu-id="40592-131">For this example, we copy a directory of log files from hello Linux VM down tooyour workstation.</span></span> <span data-ttu-id="40592-132">Plik dziennika może lub nie mogą zawierać poufne dane.</span><span class="sxs-lookup"><span data-stu-id="40592-132">A log file may or may not contain sensitive or secret data.</span></span> <span data-ttu-id="40592-133">Jednak przy użyciu połączenia usługi gwarantuje, że zawartość hello hello pliki dziennika są szyfrowane.</span><span class="sxs-lookup"><span data-stu-id="40592-133">However, using SCP ensures hello contents of hello log files are encrypted.</span></span> <span data-ttu-id="40592-134">Przy użyciu plików hello tootransfer punkt połączenia usługi jest hello Najprostszym sposobem tooget hello katalogu dziennika i plików w dół stacji roboczej tooyour podczas również jest bezpieczne.</span><span class="sxs-lookup"><span data-stu-id="40592-134">Using SCP tootransfer hello files is hello easiest way tooget hello log directory and files down tooyour workstation while also being secure.</span></span>

<span data-ttu-id="40592-135">Witaj następujące polecenie skopiuje pliki hello */home/azureuser/dzienniki/* katalogu na powitania maszyny Wirtualnej Azure toohello lokalnego tmp:</span><span class="sxs-lookup"><span data-stu-id="40592-135">hello following command copies files in hello */home/azureuser/logs/* directory on hello Azure VM toohello local /tmp directory:</span></span>

```bash
scp -r azureuser@myserver.eastus.cloudapp.com:/home/azureuser/logs/. /tmp/
```

<span data-ttu-id="40592-136">Witaj `-r` flagi interfejsu wiersza polecenia powoduje, że punkt połączenia usługi toorecursively kopiowania hello pliki i katalogi z punktu hello katalogu hello polecenia hello na liście.</span><span class="sxs-lookup"><span data-stu-id="40592-136">hello `-r` cli flag instructs SCP toorecursively copy hello files and directories from hello point of hello directory listed in hello command.</span></span>  <span data-ttu-id="40592-137">Należy zauważyć, że hello składni wiersza polecenia jest także podobne tooa `cp` skopiować polecenia.</span><span class="sxs-lookup"><span data-stu-id="40592-137">Also notice that hello command-line syntax is similar tooa `cp` copy command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="40592-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="40592-138">Next steps</span></span>

* [<span data-ttu-id="40592-139">Zarządzanie użytkownikami, SSH i wyboru lub naprawy dysków na maszynach wirtualnych systemu Linux platformy Azure przy użyciu hello rozszerzenia VMAccess</span><span class="sxs-lookup"><span data-stu-id="40592-139">Manage users, SSH, and check or repair disks on Azure Linux VMs using hello VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
