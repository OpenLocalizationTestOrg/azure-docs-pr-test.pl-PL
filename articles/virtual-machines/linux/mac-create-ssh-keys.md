---
title: "Tworzenie i używanie pary kluczy SSH dla maszyn wirtualnych z systemem Linux na platformie Azure | Microsoft Docs"
description: "Jak utworzyć parę publicznych i prywatnych kluczy SSH dla maszyn wirtualnych z systemem Linux na platformie Azure i używać ich w celu zwiększenia bezpieczeństwa procesu uwierzytelniania."
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
ms.openlocfilehash: 0fb71d2ffe533afba6e1e527b727a7b085e7da14
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-create-and-use-an-ssh-public-and-private-key-pair-for-linux-vms-in-azure"></a><span data-ttu-id="39c31-103">Jak utworzyć parę publicznych i prywatnych kluczy SSH dla maszyn wirtualnych z systemem Linux i używać ich</span><span class="sxs-lookup"><span data-stu-id="39c31-103">How to create and use an SSH public and private key pair for Linux VMs in Azure</span></span>
<span data-ttu-id="39c31-104">Para kluczy Secure Shell (SSH) umożliwia tworzenie na platformie Azure maszyn wirtualnych, które używają kluczy SSH do uwierzytelniania, eliminując konieczność logowania przy użyciu haseł.</span><span class="sxs-lookup"><span data-stu-id="39c31-104">With a secure shell (SSH) key pair, you can create virtual machines (VMs) in Azure that use SSH keys for authentication, eliminating the need for passwords to log in.</span></span> <span data-ttu-id="39c31-105">W tym artykule przedstawiono sposób szybkiego generowania i używania pary plików prywatnych i publicznych kluczy RSA protokołu SSH w wersji 2 dla maszyn wirtualnych z systemem Linux.</span><span class="sxs-lookup"><span data-stu-id="39c31-105">This article shows you how to quickly generate and use an SSH protocol version 2 RSA public and private key file pair for Linux VMs.</span></span> <span data-ttu-id="39c31-106">Aby uzyskać bardziej szczegółowe instrukcje i dodatkowe przykłady, zobacz [szczegółowe instrukcje dotyczące tworzenia par kluczy SSH i certyfikatów](create-ssh-keys-detailed.md).</span><span class="sxs-lookup"><span data-stu-id="39c31-106">For more detailed steps and additional examples, see [detailed steps to create SSH key pairs and certificates](create-ssh-keys-detailed.md).</span></span>

## <a name="create-an-ssh-key-pair"></a><span data-ttu-id="39c31-107">Tworzenie pary kluczy SSH</span><span class="sxs-lookup"><span data-stu-id="39c31-107">Create an SSH key pair</span></span>
<span data-ttu-id="39c31-108">Przy użyciu polecenia `ssh-keygen` utwórz pliki publicznych i prywatnych kluczy SSH. Pliki te są zazwyczaj tworzone w katalogu `~/.ssh`, ale gdy zostanie wyświetlony monit, możesz określić inną lokalizację oraz dodatkowe hasło (umożliwiające dostęp do pliku klucza prywatnego).</span><span class="sxs-lookup"><span data-stu-id="39c31-108">Use the `ssh-keygen` command to create SSH public and private key files that are by default created in the `~/.ssh` directory, but you can specify a different location and additional passphrase (a password to access the private key file) when prompted.</span></span> <span data-ttu-id="39c31-109">Uruchom następujące polecenie z poziomu powłoki Bash, podając własne informacje w odpowiedzi na monity.</span><span class="sxs-lookup"><span data-stu-id="39c31-109">Run the following command from a Bash shell, answering the prompts with your own information.</span></span>

```bash
ssh-keygen -t rsa -b 2048
```

## <a name="use-the-ssh-key-pair"></a><span data-ttu-id="39c31-110">Używanie pary kluczy SSH</span><span class="sxs-lookup"><span data-stu-id="39c31-110">Use the SSH key pair</span></span>
<span data-ttu-id="39c31-111">Klucz publiczny umieszczony na maszynie wirtualnej z systemem Linux na platformie Azure jest domyślnie przechowywany w katalogu `~/.ssh/id_rsa.pub`, chyba że podczas tworzenia klucza zmieniono tę lokalizację.</span><span class="sxs-lookup"><span data-stu-id="39c31-111">The public key that you place on your Linux VM in Azure is by default stored in `~/.ssh/id_rsa.pub`, unless you changed the location when you created them.</span></span> <span data-ttu-id="39c31-112">Jeśli tworzysz maszynę wirtualną za pomocą [interfejsu wiersza polecenia platformy Azure 2.0](/cli/azure), określ lokalizację tego klucza publicznego, używając polecenia [az vm create](/cli/azure/vm#create) z opcją `--ssh-key-path`.</span><span class="sxs-lookup"><span data-stu-id="39c31-112">If you use the [Azure CLI 2.0](/cli/azure) to create your VM, specify the location of this public key when you use the [az vm create](/cli/azure/vm#create) with the `--ssh-key-path` option.</span></span> <span data-ttu-id="39c31-113">Pamiętaj, aby podczas kopiowania i wklejania zawartości klucza publicznego do użycia w witrynie Azure Portal lub szablonie usługi Resource Manager nie kopiować dodatkowych spacji.</span><span class="sxs-lookup"><span data-stu-id="39c31-113">If you copy and paste the contents of the public key file to use in the Azure portal or a Resource Manager template, make sure you don't copy any additional whitespace.</span></span> <span data-ttu-id="39c31-114">Jeśli na przykład używasz systemu operacyjnego OS X, możesz potokować plik klucza publicznego (domyślnie **~/.ssh/id_rsa.pub**) do programu **pbcopy**, aby skopiować jego zawartość (dostępne są inne programy dla systemu Linux, które robią to samo, na przykład `xclip`).</span><span class="sxs-lookup"><span data-stu-id="39c31-114">For example, if you use OS X, you can pipe the public key file (by default, **~/.ssh/id_rsa.pub**) to **pbcopy** to copy the contents (there are other Linux programs that do the same thing, such as `xclip`).</span></span>

<span data-ttu-id="39c31-115">Jeśli nie znasz kluczy publicznych SSH, możesz wyświetlić swój klucz publiczny, uruchamiając polecenie `cat` w następujący sposób i zastępując ścieżkę `~/.ssh/id_rsa.pub` lokalizacją własnego pliku klucza publicznego:</span><span class="sxs-lookup"><span data-stu-id="39c31-115">If you're not familiar with SSH public keys, you can see your public key by running `cat` as follows, replacing `~/.ssh/id_rsa.pub` with your own public key file location:</span></span>

```bash
cat ~/.ssh/id_rsa.pub
```

<span data-ttu-id="39c31-116">Mając klucz publiczny na maszynie wirtualnej platformy Azure, nawiąż połączenie z maszyną wirtualną przez protokół SSH przy użyciu adresu IP lub nazwy DNS tej maszyny (pamiętaj, aby zastąpić poniższe ciągi `azureuser` i `myvm.westus.cloudapp.azure.com` nazwą użytkownika administratora i w pełni kwalifikowaną nazwą domeny lub adresem IP):</span><span class="sxs-lookup"><span data-stu-id="39c31-116">With the public key on your Azure VM, SSH to your VM using the IP address or DNS name of your VM (remember to replace `azureuser` and `myvm.westus.cloudapp.azure.com` below with the admin username and the fully qualified domain name -- or IP address):</span></span>

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

<span data-ttu-id="39c31-117">Jeśli podczas tworzenia pary kluczy podano hasło, wprowadź je, gdy podczas logowania zostanie wyświetlony odpowiedni monit.</span><span class="sxs-lookup"><span data-stu-id="39c31-117">If you provided a passphrase when you created your key pair, enter the passphrase when prompted during the login process.</span></span> <span data-ttu-id="39c31-118">(Serwer zostanie dodany do folderu `~/.ssh/known_hosts` i monit o ponowne połączenie nie zostanie wyświetlony, dopóki klucz publiczny na maszynie wirtualnej nie ulegnie zmianie lub nazwa serwera nie zostanie usunięta z folderu `~/.ssh/known_hosts`).</span><span class="sxs-lookup"><span data-stu-id="39c31-118">(The server is added to your `~/.ssh/known_hosts` folder, and you won't be asked to connect again until the public key on your Azure VM changes or the server name is removed from `~/.ssh/known_hosts`.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="39c31-119">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="39c31-119">Next steps</span></span>

<span data-ttu-id="39c31-120">W domyślnej konfiguracji maszyn wirtualnych utworzonych przy użyciu kluczy SSH hasła są wyłączone, aby próby odgadnięcia hasła za pomocą ataków siłowych były znacznie bardziej kosztowne, a przez to również trudniejsze.</span><span class="sxs-lookup"><span data-stu-id="39c31-120">VMs created using SSH keys are by default configured with passwords disabled, to make brute-forced guessing attempts vastly more expensive and therefore difficult.</span></span> <span data-ttu-id="39c31-121">W tym temacie opisano tworzenie prostej pary kluczy SSH do szybkiego używania.</span><span class="sxs-lookup"><span data-stu-id="39c31-121">This topic describes creating a simple SSH key pair for quick usage.</span></span> <span data-ttu-id="39c31-122">Jeśli potrzebujesz więcej pomocy przy tworzeniu pary kluczy SSH lub potrzebujesz dodatkowych certyfikatów, zobacz [Szczegółowe instrukcje dotyczące tworzenia par kluczy SSH i certyfikatów](create-ssh-keys-detailed.md).</span><span class="sxs-lookup"><span data-stu-id="39c31-122">If you need more assistance in creating your SSH key pair or require additional certificates, see [Detailed steps to create SSH key pairs and certificates](create-ssh-keys-detailed.md).</span></span>

<span data-ttu-id="39c31-123">Maszyny wirtualne korzystające z pary kluczy SSH możesz tworzyć za pomocą witryny Azure Portal, interfejsu wiersza polecenia oraz szablonów:</span><span class="sxs-lookup"><span data-stu-id="39c31-123">You can create VMs that use your SSH key pair using the Azure portal, CLI, and templates:</span></span>

* [<span data-ttu-id="39c31-124">Tworzenie bezpiecznej maszyny wirtualnej systemu Linux przy użyciu witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="39c31-124">Create a secure Linux VM using the Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="39c31-125">Tworzenie bezpiecznej maszyny wirtualnej systemu Linux przy użyciu interfejsu wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="39c31-125">Create a secure Linux VM using the Azure CLI 2.0)</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="39c31-126">Tworzenie bezpiecznej maszyny wirtualnej systemu Linux przy użyciu szablonu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="39c31-126">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
