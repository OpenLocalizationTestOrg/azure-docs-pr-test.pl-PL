---
title: "aaaCreate i używanie SSH parę kluczy dla maszyn wirtualnych systemu Linux na platformie Azure | Dokumentacja firmy Microsoft"
description: "Jak toocreate i używanie SSH publiczne i prywatne parę kluczy dla maszyn wirtualnych systemu Linux w Azure tooimprove hello zabezpieczeń hello procesu uwierzytelniania."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 34ae9482-da3e-4b2d-9d0d-9d672aa42498
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/14/2017
ms.author: iainfou
ms.openlocfilehash: 7fb94841d34d5bc006f3134adf91102ddce5f174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-use-an-ssh-public-and-private-key-pair-for-linux-vms-in-azure"></a><span data-ttu-id="581b6-103">Jak skojarzyć toocreate i użyj klucz publiczny i prywatny SSH dla maszyn wirtualnych systemu Linux na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="581b6-103">How toocreate and use an SSH public and private key pair for Linux VMs in Azure</span></span>
<span data-ttu-id="581b6-104">Z pary kluczy bezpiecznej powłoki (SSH) można utworzyć na platformie Azure, która używania kluczy SSH w celu uwierzytelniania, eliminując konieczność hello toolog haseł w maszynach wirtualnych (VM).</span><span class="sxs-lookup"><span data-stu-id="581b6-104">With a secure shell (SSH) key pair, you can create virtual machines (VMs) in Azure that use SSH keys for authentication, eliminating hello need for passwords toolog in.</span></span> <span data-ttu-id="581b6-105">W tym artykule opisano, jak tooquickly Generowanie i używanie parę pliku klucza publicznego i prywatnego RSA w wersji 2 protokołu SSH dla maszyn wirtualnych systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="581b6-105">This article shows you how tooquickly generate and use an SSH protocol version 2 RSA public and private key file pair for Linux VMs.</span></span> <span data-ttu-id="581b6-106">Aby uzyskać bardziej szczegółowe kroki i dodatkowe przykłady, zobacz [szczegółowe kroki par kluczy SSH toocreate i certyfikaty](create-ssh-keys-detailed.md).</span><span class="sxs-lookup"><span data-stu-id="581b6-106">For more detailed steps and additional examples, see [detailed steps toocreate SSH key pairs and certificates](create-ssh-keys-detailed.md).</span></span>

## <a name="create-an-ssh-key-pair"></a><span data-ttu-id="581b6-107">Tworzenie pary kluczy SSH</span><span class="sxs-lookup"><span data-stu-id="581b6-107">Create an SSH key pair</span></span>
<span data-ttu-id="581b6-108">Użyj hello `ssh-keygen` polecenia toocreate SSH publicznego i prywatnego klucza pliki, które są domyślnie tworzone w hello `~/.ssh` katalogu, ale można określić inną lokalizację i hasło dodatkowe (hasło tooaccess hello plik klucza prywatnego) po zostanie wyświetlony monit.</span><span class="sxs-lookup"><span data-stu-id="581b6-108">Use hello `ssh-keygen` command toocreate SSH public and private key files that are by default created in hello `~/.ssh` directory, but you can specify a different location and additional passphrase (a password tooaccess hello private key file) when prompted.</span></span> <span data-ttu-id="581b6-109">Uruchom następujące polecenie z powłoki Bash hello, udzielenie odpowiedzi na powitania monity z odpowiednimi informacjami.</span><span class="sxs-lookup"><span data-stu-id="581b6-109">Run hello following command from a Bash shell, answering hello prompts with your own information.</span></span>

```bash
ssh-keygen -t rsa -b 2048
```

## <a name="use-hello-ssh-key-pair"></a><span data-ttu-id="581b6-110">Para kluczy SSH hello</span><span class="sxs-lookup"><span data-stu-id="581b6-110">Use hello SSH key pair</span></span>
<span data-ttu-id="581b6-111">Witaj klucz publiczny, który można umieścić na maszynie Wirtualnej systemu Linux na platformie Azure są domyślnie przechowywane w `~/.ssh/id_rsa.pub`, chyba że zostaną zmienione lokalizacji powitania po ich utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="581b6-111">hello public key that you place on your Linux VM in Azure is by default stored in `~/.ssh/id_rsa.pub`, unless you changed hello location when you created them.</span></span> <span data-ttu-id="581b6-112">Jeśli używasz hello [Azure CLI 2.0](/cli/azure) toocreate maszyny Wirtualnej, określ lokalizację hello tego klucza publicznego, gdy używasz hello [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) z hello `--ssh-key-path` — opcja.</span><span class="sxs-lookup"><span data-stu-id="581b6-112">If you use hello [Azure CLI 2.0](/cli/azure) toocreate your VM, specify hello location of this public key when you use hello [az vm create](/cli/azure/vm#create) with hello `--ssh-key-path` option.</span></span> <span data-ttu-id="581b6-113">Jeśli skopiuj i Wklej zawartość hello hello toouse pliku klucza publicznego w hello portalu Azure lub w szablonie usługi Resource Manager, upewnij się, że nie należy skopiować wszystkie dodatkowe odstępu.</span><span class="sxs-lookup"><span data-stu-id="581b6-113">If you copy and paste hello contents of hello public key file toouse in hello Azure portal or a Resource Manager template, make sure you don't copy any additional whitespace.</span></span> <span data-ttu-id="581b6-114">Na przykład, jeśli używasz OS X, można przekazać pliku klucza publicznego hello (domyślnie **~/.ssh/id_rsa.pub**) zbyt**pbcopy** toocopy hello zawartość (istnieją inne programy systemu Linux, które hello samo, takich jak `xclip`).</span><span class="sxs-lookup"><span data-stu-id="581b6-114">For example, if you use OS X, you can pipe hello public key file (by default, **~/.ssh/id_rsa.pub**) too**pbcopy** toocopy hello contents (there are other Linux programs that do hello same thing, such as `xclip`).</span></span>

<span data-ttu-id="581b6-115">Jeśli nie znasz kluczy publicznych SSH, możesz wyświetlić swój klucz publiczny, uruchamiając polecenie `cat` w następujący sposób i zastępując ścieżkę `~/.ssh/id_rsa.pub` lokalizacją własnego pliku klucza publicznego:</span><span class="sxs-lookup"><span data-stu-id="581b6-115">If you're not familiar with SSH public keys, you can see your public key by running `cat` as follows, replacing `~/.ssh/id_rsa.pub` with your own public key file location:</span></span>

```bash
cat ~/.ssh/id_rsa.pub
```

<span data-ttu-id="581b6-116">Z użyciem klucza publicznego hello na maszynie Wirtualnej Azure, SSH tooyour maszynę Wirtualną przy użyciu hello adres IP lub nazwę DNS maszyny wirtualnej (Pamiętaj tooreplace `azureuser` i `myvm.westus.cloudapp.azure.com` poniżej z hello nazwa użytkownika i nazwy FQDN hello--lub adres IP adresów):</span><span class="sxs-lookup"><span data-stu-id="581b6-116">With hello public key on your Azure VM, SSH tooyour VM using hello IP address or DNS name of your VM (remember tooreplace `azureuser` and `myvm.westus.cloudapp.azure.com` below with hello admin username and hello fully qualified domain name -- or IP address):</span></span>

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

<span data-ttu-id="581b6-117">Jeśli podano hasło podczas tworzenia Twojej parę kluczy, wprowadź hasło powitania po wyświetleniu monitu w procesie logowania hello.</span><span class="sxs-lookup"><span data-stu-id="581b6-117">If you provided a passphrase when you created your key pair, enter hello passphrase when prompted during hello login process.</span></span> <span data-ttu-id="581b6-118">(hello serwer jest dodawany tooyour `~/.ssh/known_hosts` folderu, a nie będzie pytany tooconnect ponownie do czasu klucza publicznego hello na zmiany maszyny Wirtualnej platformy Azure lub nazwa serwera hello jest usuwany z `~/.ssh/known_hosts`.)</span><span class="sxs-lookup"><span data-stu-id="581b6-118">(hello server is added tooyour `~/.ssh/known_hosts` folder, and you won't be asked tooconnect again until hello public key on your Azure VM changes or hello server name is removed from `~/.ssh/known_hosts`.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="581b6-119">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="581b6-119">Next steps</span></span>

<span data-ttu-id="581b6-120">Maszyny wirtualne utworzone za pomocą kluczy SSH są domyślnie skonfigurowane przy użyciu haseł wyłączone, toomake metodą siłową odgadnięcie prób znacznie droższe i w związku z tym trudne.</span><span class="sxs-lookup"><span data-stu-id="581b6-120">VMs created using SSH keys are by default configured with passwords disabled, toomake brute-forced guessing attempts vastly more expensive and therefore difficult.</span></span> <span data-ttu-id="581b6-121">W tym temacie opisano tworzenie prostej pary kluczy SSH do szybkiego używania.</span><span class="sxs-lookup"><span data-stu-id="581b6-121">This topic describes creating a simple SSH key pair for quick usage.</span></span> <span data-ttu-id="581b6-122">Jeśli potrzebujesz więcej pomocy podczas tworzenia Twojej pary kluczy SSH, lub wymagać dodatkowych certyfikatów, zobacz [szczegółowe kroki par kluczy SSH toocreate i certyfikaty](create-ssh-keys-detailed.md).</span><span class="sxs-lookup"><span data-stu-id="581b6-122">If you need more assistance in creating your SSH key pair or require additional certificates, see [Detailed steps toocreate SSH key pairs and certificates](create-ssh-keys-detailed.md).</span></span>

<span data-ttu-id="581b6-123">Można tworzyć maszyn wirtualnych korzystających z pary kluczy SSH za pomocą hello portalu Azure, interfejsu wiersza polecenia i szablony:</span><span class="sxs-lookup"><span data-stu-id="581b6-123">You can create VMs that use your SSH key pair using hello Azure portal, CLI, and templates:</span></span>

* [<span data-ttu-id="581b6-124">Tworzenie bezpiecznej maszyny Wirtualnej systemu Linux przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="581b6-124">Create a secure Linux VM using hello Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="581b6-125">Tworzenie bezpiecznej maszyny Wirtualnej systemu Linux przy użyciu hello Azure CLI 2.0)</span><span class="sxs-lookup"><span data-stu-id="581b6-125">Create a secure Linux VM using hello Azure CLI 2.0)</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="581b6-126">Tworzenie bezpiecznej maszyny wirtualnej systemu Linux przy użyciu szablonu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="581b6-126">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
