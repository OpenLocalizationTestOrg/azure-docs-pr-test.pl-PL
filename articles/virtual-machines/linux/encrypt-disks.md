---
title: "aaaEncrypt dysków na Maszynę wirtualną systemu Linux na platformie Azure | Dokumentacja firmy Microsoft"
description: "Jak tooencrypt dysków wirtualnych na maszynę Wirtualną systemu Linux przy użyciu zwiększone zabezpieczenia hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 2a23b6fa-6941-4998-9804-8efe93b647b3
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: d6197742bc8562630e8395588c072093fc01d614
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencrypt-virtual-disks-on-a-linux-vm"></a><span data-ttu-id="ff81b-103">Jak tooencrypt dysków wirtualnych na Maszynę wirtualną systemu Linux</span><span class="sxs-lookup"><span data-stu-id="ff81b-103">How tooencrypt virtual disks on a Linux VM</span></span>
<span data-ttu-id="ff81b-104">Ulepszone maszyny wirtualnej (VM) zabezpieczeń i zgodności mogą być szyfrowane dyski wirtualne na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="ff81b-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted.</span></span> <span data-ttu-id="ff81b-105">Dyski są szyfrowane za pomocą kluczy kryptograficznych, które są już zabezpieczone w usłudze Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="ff81b-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="ff81b-106">Kontrolowanie tych kluczy kryptograficznych i przeprowadzić inspekcję ich używania.</span><span class="sxs-lookup"><span data-stu-id="ff81b-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="ff81b-107">W tym artykule szczegółowo sposób tooencrypt dysków wirtualnych na Maszynę wirtualną systemu Linux przy użyciu hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="ff81b-107">This article details how tooencrypt virtual disks on a Linux VM using hello Azure CLI 2.0.</span></span> <span data-ttu-id="ff81b-108">Można również wykonać te kroki hello [Azure CLI 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ff81b-108">You can also perform these steps with hello [Azure CLI 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="ff81b-109">Szybkie polecenia</span><span class="sxs-lookup"><span data-stu-id="ff81b-109">Quick commands</span></span>
<span data-ttu-id="ff81b-110">Jeśli potrzebujesz tooquickly hello zadania, powitania po sekcji Szczegóły hello podstawowej polecenia tooencrypt dyski wirtualne na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ff81b-110">If you need tooquickly accomplish hello task, hello following section details hello base commands tooencrypt virtual disks on your VM.</span></span> <span data-ttu-id="ff81b-111">Bardziej szczegółowe informacje i kontekst dla każdego kroku można znaleźć hello pozostałej części dokumentu hello [uruchamiania tutaj](#overview-of-disk-encryption).</span><span class="sxs-lookup"><span data-stu-id="ff81b-111">More detailed information and context for each step can be found hello rest of hello document, [starting here](#overview-of-disk-encryption).</span></span>

<span data-ttu-id="ff81b-112">Najnowsza wersja należy hello [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zarejestrowane za pomocą konta Azure tooan [logowania az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="ff81b-112">You need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="ff81b-113">Poniższe przykłady w hello Zastąp przykładowe nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="ff81b-113">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="ff81b-114">Przykład nazwy parametru zawierają *myResourceGroup*, *klucze*, i *myVM*.</span><span class="sxs-lookup"><span data-stu-id="ff81b-114">Example parameter names include *myResourceGroup*, *myKey*, and *myVM*.</span></span>

<span data-ttu-id="ff81b-115">Najpierw włączyć hello dostawcy usługi Azure Key Vault w ramach Twojej subskrypcji platformy Azure z [az dostawcy rejestru](/cli/azure/provider#register) i utworzyć nową grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="ff81b-115">First, enable hello Azure Key Vault provider within your Azure subscription with [az provider register](/cli/azure/provider#register) and create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="ff81b-116">Witaj poniższy przykład tworzy nazwę grupy zasobów *myResourceGroup* w hello *eastus* lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="ff81b-116">hello following example creates a resource group name *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="ff81b-117">Tworzenie usługi Azure Key Vault z [az keyvault utworzyć](/cli/azure/keyvault#create) i Włącz hello Key Vault służących do szyfrowania dysku.</span><span class="sxs-lookup"><span data-stu-id="ff81b-117">Create an Azure Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable hello Key Vault for use with disk encryption.</span></span> <span data-ttu-id="ff81b-118">Określ unikatową nazwę usługi Key Vault *keyvault_name* w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="ff81b-118">Specify a unique Key Vault name for *keyvault_name* as follows:</span></span>

```azurecli
keyvault_name=mykeyvaultikf
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

<span data-ttu-id="ff81b-119">Tworzenie klucza kryptograficznego w magazyn kluczy o [Utwórz klucz keyvault az](/cli/azure/keyvault/key#create).</span><span class="sxs-lookup"><span data-stu-id="ff81b-119">Create a cryptographic key in your Key Vault with [az keyvault key create](/cli/azure/keyvault/key#create).</span></span> <span data-ttu-id="ff81b-120">Witaj poniższym przykładzie jest tworzony klucz o nazwie *klucze*:</span><span class="sxs-lookup"><span data-stu-id="ff81b-120">hello following example creates a key named *myKey*:</span></span>

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```

<span data-ttu-id="ff81b-121">Tworzenie nazwy głównej usługi za pomocą usługi Azure Active Directory z [az ad sp utworzyć do rbac](/cli/azure/ad/sp#create-for-rbac).</span><span class="sxs-lookup"><span data-stu-id="ff81b-121">Create a service principal using Azure Active Directory with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span></span> <span data-ttu-id="ff81b-122">uchwyty główna usługi Hello hello uwierzytelniania i wymiany kluczy kryptograficznych z magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="ff81b-122">hello service principal handles hello authentication and exchange of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="ff81b-123">Poniższy przykład Hello odczytuje hello wartości dla nazwy głównej usługi hello Id i hasło do użycia w poleceniach nowsze:</span><span class="sxs-lookup"><span data-stu-id="ff81b-123">hello following example reads in hello values for hello service principal Id and password for use in later commands:</span></span>

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

<span data-ttu-id="ff81b-124">hasło Hello jest tylko dane wyjściowe w przypadku tworzenia hello nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="ff81b-124">hello password is only output when you create hello service principal.</span></span> <span data-ttu-id="ff81b-125">W razie potrzeby, widok i rejestrowanie hello hasła (`echo $sp_password`).</span><span class="sxs-lookup"><span data-stu-id="ff81b-125">If desired, view and record hello password (`echo $sp_password`).</span></span> <span data-ttu-id="ff81b-126">Możesz wyświetlić listę Twojej nazwy główne usług z [listy sp ad az](/cli/azure/ad/sp#list) i wyświetlić dodatkowe informacje o określonej usługi głównej z [az ad sp Pokaż](/cli/azure/ad/sp#show).</span><span class="sxs-lookup"><span data-stu-id="ff81b-126">You can list your service principals with [az ad sp list](/cli/azure/ad/sp#list) and view additional information about a specific service principal with [az ad sp show](/cli/azure/ad/sp#show).</span></span>

<span data-ttu-id="ff81b-127">Ustaw uprawnienia na magazyn kluczy o [keyvault az set-policy](/cli/azure/keyvault#set-policy).</span><span class="sxs-lookup"><span data-stu-id="ff81b-127">Set permissions on your Key Vault with [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span></span> <span data-ttu-id="ff81b-128">W hello poniższy przykład hello usługi identyfikator podmiotu zabezpieczeń jest dostarczana z hello poprzedzających polecenia:</span><span class="sxs-lookup"><span data-stu-id="ff81b-128">In hello following example, hello service principal ID is supplied from hello preceding command:</span></span>

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
    --key-permissions wrapKey \
    --secret-permissions set
```

<span data-ttu-id="ff81b-129">Utwórz maszynę Wirtualną z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) i dołączenie dysku danych 5 Gb.</span><span class="sxs-lookup"><span data-stu-id="ff81b-129">Create a VM with [az vm create](/cli/azure/vm#create) and attach a 5Gb data disk.</span></span> <span data-ttu-id="ff81b-130">Niektóre obrazy marketplace obsługuje szyfrowanie dysków.</span><span class="sxs-lookup"><span data-stu-id="ff81b-130">Only certain marketplace images support disk encryption.</span></span> <span data-ttu-id="ff81b-131">Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie `myVM` przy użyciu **CentOS 7.2n** obrazu:</span><span class="sxs-lookup"><span data-stu-id="ff81b-131">hello following example creates a VM named `myVM` using a **CentOS 7.2n** image:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

<span data-ttu-id="ff81b-132">SSH tooyour maszynę Wirtualną przy użyciu hello `publicIpAddress` wyświetlany w danych wyjściowych hello hello poprzedzających polecenia.</span><span class="sxs-lookup"><span data-stu-id="ff81b-132">SSH tooyour VM using hello `publicIpAddress` shown in hello output of hello preceding command.</span></span> <span data-ttu-id="ff81b-133">Tworzenie partycji i systemu plików, a następnie zainstalować dysk danych hello.</span><span class="sxs-lookup"><span data-stu-id="ff81b-133">Create a partition and filesystem, then mount hello data disk.</span></span> <span data-ttu-id="ff81b-134">Aby uzyskać więcej informacji, zobacz [połączyć tooa maszyny Wirtualnej systemu Linux toomount hello nowy dysk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span><span class="sxs-lookup"><span data-stu-id="ff81b-134">For more information, see [Connect tooa Linux VM toomount hello new disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> <span data-ttu-id="ff81b-135">Zamknij sesję SSH.</span><span class="sxs-lookup"><span data-stu-id="ff81b-135">Close your SSH session.</span></span>

<span data-ttu-id="ff81b-136">Szyfrowanie maszyny Wirtualnej z [włączyć szyfrowanie maszyny wirtualnej az](/cli/azure/vm/encryption#enable).</span><span class="sxs-lookup"><span data-stu-id="ff81b-136">Encrypt your VM with [az vm encryption enable](/cli/azure/vm/encryption#enable).</span></span> <span data-ttu-id="ff81b-137">Witaj poniższym przykładzie użyto hello `$sp_id` i `$sp_password` zmienne z poprzednim hello `ad sp create-for-rbac` polecenia:</span><span class="sxs-lookup"><span data-stu-id="ff81b-137">hello following example uses hello `$sp_id` and `$sp_password` variables from hello preceding `ad sp create-for-rbac` command:</span></span>

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```

<span data-ttu-id="ff81b-138">Trwa trochę czasu, zanim toocomplete proces szyfrowania dysku hello.</span><span class="sxs-lookup"><span data-stu-id="ff81b-138">It takes some time for hello disk encryption process toocomplete.</span></span> <span data-ttu-id="ff81b-139">Monitorowanie stanu hello hello procesu z [Pokaż szyfrowania maszyny wirtualnej az](/cli/azure/vm/encryption#show):</span><span class="sxs-lookup"><span data-stu-id="ff81b-139">Monitor hello status of hello process with [az vm encryption show](/cli/azure/vm/encryption#show):</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="ff81b-140">Witaj pokazuje stan **EncryptionInProgress**.</span><span class="sxs-lookup"><span data-stu-id="ff81b-140">hello status shows **EncryptionInProgress**.</span></span> <span data-ttu-id="ff81b-141">Zaczekaj na stan hello raportów dysku systemu operacyjnego hello **VMRestartPending**, ponowne uruchomienie maszyny Wirtualnej z [ponownego uruchomienia maszyny wirtualnej az](/cli/azure/vm#restart):</span><span class="sxs-lookup"><span data-stu-id="ff81b-141">Wait until hello status for hello OS disk reports **VMRestartPending**, then restart your VM with [az vm restart](/cli/azure/vm#restart):</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="ff81b-142">Witaj procesu szyfrowania dysku zostanie sfinalizowana podczas procesu rozruchu hello, więc odczekaj kilka minut przed sprawdzeniem stanu hello szyfrowania ponownie, podając **Pokaż szyfrowania maszyny wirtualnej az**:</span><span class="sxs-lookup"><span data-stu-id="ff81b-142">hello disk encryption process is finalized during hello boot process, so wait a few minutes before checking hello status of encryption again with **az vm encryption show**:</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="ff81b-143">Stan Hello teraz Zgłoś dyskach hello systemu operacyjnego i dysku danych jako **zaszyfrowane**.</span><span class="sxs-lookup"><span data-stu-id="ff81b-143">hello status should now report both hello OS disk and data disk as **Encrypted**.</span></span>

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="ff81b-144">Omówienie szyfrowania dysków</span><span class="sxs-lookup"><span data-stu-id="ff81b-144">Overview of disk encryption</span></span>
<span data-ttu-id="ff81b-145">Dyski wirtualne na maszynach wirtualnych systemu Linux są szyfrowane za pomocą rest [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span><span class="sxs-lookup"><span data-stu-id="ff81b-145">Virtual disks on Linux VMs are encrypted at rest using [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span></span> <span data-ttu-id="ff81b-146">Jest bezpłatna dla szyfrowania dysków wirtualnych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="ff81b-146">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="ff81b-147">Klucze szyfrowania są przechowywane w usługi Azure Key Vault przy użyciu ochrony oprogramowania, lub możesz zaimportować lub wygenerować klucze w sprzętowych modułach zabezpieczeń (HSM) certyfikowane tooFIPS 140-2 poziom 2 standardów.</span><span class="sxs-lookup"><span data-stu-id="ff81b-147">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified tooFIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="ff81b-148">Zachowanie kontroli nad tych kluczy kryptograficznych i przeprowadzić inspekcję ich używania.</span><span class="sxs-lookup"><span data-stu-id="ff81b-148">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="ff81b-149">Te klucze szyfrowania są używane tooencrypt i odszyfrowywania tooyour dołączonych dysków wirtualnych maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ff81b-149">These cryptographic keys are used tooencrypt and decrypt virtual disks attached tooyour VM.</span></span> <span data-ttu-id="ff81b-150">Nazwy głównej usługi Azure Active Directory zapewnia mechanizm bezpiecznego do wystawiania tych kluczy kryptograficznych, ponieważ maszyny wirtualne są zasilane i wyłączanie.</span><span class="sxs-lookup"><span data-stu-id="ff81b-150">An Azure Active Directory service principal provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="ff81b-151">proces Hello szyfrowania maszyny Wirtualnej przebiega w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="ff81b-151">hello process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="ff81b-152">Tworzenie klucza kryptograficznego w usłudze Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="ff81b-152">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="ff81b-153">Skonfiguruj hello kryptograficznych klucza toobe można używać do szyfrowania dysków.</span><span class="sxs-lookup"><span data-stu-id="ff81b-153">Configure hello cryptographic key toobe usable for encrypting disks.</span></span>
3. <span data-ttu-id="ff81b-154">klucz kryptograficzny hello tooread z hello Azure Key Vault, Utwórz usługę Azure Active Directory podmiotu zabezpieczeń z odpowiednimi uprawnieniami hello.</span><span class="sxs-lookup"><span data-stu-id="ff81b-154">tooread hello cryptographic key from hello Azure Key Vault, create an Azure Active Directory service principal with hello appropriate permissions.</span></span>
4. <span data-ttu-id="ff81b-155">Wystawiać tooencrypt polecenia hello wirtualnych dysków, określenie nazwy głównej usługi Azure Active Directory hello i odpowiednie toobe klucza kryptograficznego używane.</span><span class="sxs-lookup"><span data-stu-id="ff81b-155">Issue hello command tooencrypt your virtual disks, specifying hello Azure Active Directory service principal and appropriate cryptographic key toobe used.</span></span>
5. <span data-ttu-id="ff81b-156">główne żądania usługi Azure Active Directory Hello hello wymaganego klucza kryptograficznego z usługi Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="ff81b-156">hello Azure Active Directory service principal requests hello required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="ff81b-157">dyski wirtualne Hello są szyfrowane za pomocą klucza kryptograficznego hello podane.</span><span class="sxs-lookup"><span data-stu-id="ff81b-157">hello virtual disks are encrypted using hello provided cryptographic key.</span></span>

## <a name="encryption-process"></a><span data-ttu-id="ff81b-158">Proces szyfrowania</span><span class="sxs-lookup"><span data-stu-id="ff81b-158">Encryption process</span></span>
<span data-ttu-id="ff81b-159">Szyfrowanie dysków opiera się na powitania następujące dodatkowe składniki:</span><span class="sxs-lookup"><span data-stu-id="ff81b-159">Disk encryption relies on hello following additional components:</span></span>

* <span data-ttu-id="ff81b-160">**Usługa Azure Key Vault** — używane toosafeguard kluczy kryptograficznych i kluczy tajnych używane podczas procesu szyfrowania i odszyfrowywania dysku hello.</span><span class="sxs-lookup"><span data-stu-id="ff81b-160">**Azure Key Vault** - used toosafeguard cryptographic keys and secrets used for hello disk encryption/decryption process.</span></span>
  * <span data-ttu-id="ff81b-161">Jeśli istnieje, można użyć istniejącego magazynu kluczy Azure.</span><span class="sxs-lookup"><span data-stu-id="ff81b-161">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="ff81b-162">Nie masz toodedicate dysków tooencrypting magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="ff81b-162">You do not have toodedicate a Key Vault tooencrypting disks.</span></span>
  * <span data-ttu-id="ff81b-163">granice administracyjne tooseparate i widoczności klucza, można utworzyć dedykowane Key Vault.</span><span class="sxs-lookup"><span data-stu-id="ff81b-163">tooseparate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="ff81b-164">**Usługa Azure Active Directory** — Witaj uchwytów bezpiecznej wymiany kluczy kryptograficznych wymagane i uwierzytelniania dla żądanej akcji.</span><span class="sxs-lookup"><span data-stu-id="ff81b-164">**Azure Active Directory** - handles hello secure exchanging of required cryptographic keys and authentication for requested actions.</span></span>
  * <span data-ttu-id="ff81b-165">Zazwyczaj można użyć istniejącego wystąpienia usługi Azure Active Directory, do przechowywania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ff81b-165">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="ff81b-166">nazwy głównej usługi Hello zapewnia toorequest mechanizmu bezpiecznego i wydawane hello odpowiednich kluczy kryptograficznych.</span><span class="sxs-lookup"><span data-stu-id="ff81b-166">hello service principal provides a secure mechanism toorequest and be issued hello appropriate cryptographic keys.</span></span> <span data-ttu-id="ff81b-167">Nie opracowujesz aplikację rzeczywista, która integruje się z usługą Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ff81b-167">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="ff81b-168">Wymagania i ograniczenia</span><span class="sxs-lookup"><span data-stu-id="ff81b-168">Requirements and limitations</span></span>
<span data-ttu-id="ff81b-169">Obsługiwane scenariusze i wymagania dotyczące szyfrowania dysków:</span><span class="sxs-lookup"><span data-stu-id="ff81b-169">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="ff81b-170">powitania po Linux server jednostki SKU - Ubuntu, CentOS, SUSE i SUSE Linux Enterprise Server (SLES) i Red Hat Enterprise Linux.</span><span class="sxs-lookup"><span data-stu-id="ff81b-170">hello following Linux server SKUs - Ubuntu, CentOS, SUSE and SUSE Linux Enterprise Server (SLES), and Red Hat Enterprise Linux.</span></span>
* <span data-ttu-id="ff81b-171">Wszystkie zasoby (na przykład usługi Key Vault, konta magazynu i maszyny Wirtualnej) musi być w hello tego samego regionu Azure i subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="ff81b-171">All resources (such as Key Vault, Storage account, and VM) must be in hello same Azure region and subscription.</span></span>
* <span data-ttu-id="ff81b-172">Standardowa A, D DS, G i GS seria maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="ff81b-172">Standard A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="ff81b-173">Szyfrowanie dysków nie jest obecnie obsługiwane w hello następujące scenariusze:</span><span class="sxs-lookup"><span data-stu-id="ff81b-173">Disk encryption is not currently supported in hello following scenarios:</span></span>

* <span data-ttu-id="ff81b-174">Maszyny wirtualne warstwy podstawowa.</span><span class="sxs-lookup"><span data-stu-id="ff81b-174">Basic tier VMs.</span></span>
* <span data-ttu-id="ff81b-175">Maszyny wirtualne utworzone za pomocą hello klasycznego modelu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="ff81b-175">VMs created using hello Classic deployment model.</span></span>
* <span data-ttu-id="ff81b-176">Wyłączenie szyfrowania dysku systemu operacyjnego na maszynach wirtualnych systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="ff81b-176">Disabling OS disk encryption on Linux VMs.</span></span>
* <span data-ttu-id="ff81b-177">Aktualizowanie kluczy kryptograficznych hello na już zaszyfrowany maszyny Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="ff81b-177">Updating hello cryptographic keys on an already encrypted Linux VM.</span></span>

## <a name="create-azure-key-vault-and-keys"></a><span data-ttu-id="ff81b-178">Tworzenie usługi Azure Key Vault i kluczy</span><span class="sxs-lookup"><span data-stu-id="ff81b-178">Create Azure Key Vault and keys</span></span>
<span data-ttu-id="ff81b-179">Najnowsza wersja należy hello [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zarejestrowane za pomocą konta Azure tooan [logowania az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="ff81b-179">You need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="ff81b-180">Poniższe przykłady w hello Zastąp przykładowe nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="ff81b-180">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="ff81b-181">Przykład nazwy parametru zawierają *myResourceGroup*, *klucze*, i *myVM*.</span><span class="sxs-lookup"><span data-stu-id="ff81b-181">Example parameter names include *myResourceGroup*, *myKey*, and *myVM*.</span></span>

<span data-ttu-id="ff81b-182">pierwszym krokiem Hello jest toocreate toostore usługi Azure Key Vault kluczy kryptograficznych.</span><span class="sxs-lookup"><span data-stu-id="ff81b-182">hello first step is toocreate an Azure Key Vault toostore your cryptographic keys.</span></span> <span data-ttu-id="ff81b-183">Usługa Azure Key Vault może przechowywać klucze i klucze tajne, lub haseł, które pozwalają toosecurely wdrożyć je w aplikacji i usług.</span><span class="sxs-lookup"><span data-stu-id="ff81b-183">Azure Key Vault can store keys, secrets, or passwords that allow you toosecurely implement them in your applications and services.</span></span> <span data-ttu-id="ff81b-184">Szyfrowanie dysków wirtualnych Użyj toostore Key Vault klucza kryptograficznego, który jest używany tooencrypt lub odszyfrować wirtualnych dysków.</span><span class="sxs-lookup"><span data-stu-id="ff81b-184">For virtual disk encryption, you use Key Vault toostore a cryptographic key that is used tooencrypt or decrypt your virtual disks.</span></span>

<span data-ttu-id="ff81b-185">Włącz hello dostawcy usługi Azure Key Vault w ramach Twojej subskrypcji platformy Azure z [az dostawcy rejestru](/cli/azure/provider#register) i utworzyć nową grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="ff81b-185">Enable hello Azure Key Vault provider within your Azure subscription with [az provider register](/cli/azure/provider#register) and create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="ff81b-186">Witaj poniższy przykład tworzy nazwę grupy zasobów *myResourceGroup* w hello `eastus` lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="ff81b-186">hello following example creates a resource group name *myResourceGroup* in hello `eastus` location:</span></span>

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="ff81b-187">Hello Azure Key Vault zawierającego hello kluczy kryptograficznych i obliczeniowe skojarzone zasoby, takie jak magazyn i hello samej maszyny Wirtualnej musi znajdować się w hello tego samego regionu.</span><span class="sxs-lookup"><span data-stu-id="ff81b-187">hello Azure Key Vault containing hello cryptographic keys and associated compute resources such as storage and hello VM itself must reside in hello same region.</span></span> <span data-ttu-id="ff81b-188">Tworzenie usługi Azure Key Vault z [az keyvault utworzyć](/cli/azure/keyvault#create) i Włącz hello Key Vault służących do szyfrowania dysku.</span><span class="sxs-lookup"><span data-stu-id="ff81b-188">Create an Azure Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable hello Key Vault for use with disk encryption.</span></span> <span data-ttu-id="ff81b-189">Określ unikatową nazwę usługi Key Vault *keyvault_name* w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="ff81b-189">Specify a unique Key Vault name for *keyvault_name* as follows:</span></span>

```azurecli
keyvault_name=myUniqueKeyVaultName
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

<span data-ttu-id="ff81b-190">Mogą być przechowywane przy użyciu oprogramowania lub sprzętu modelu zabezpieczeń (HSM) ochronę kluczy kryptograficznych.</span><span class="sxs-lookup"><span data-stu-id="ff81b-190">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="ff81b-191">Użycie modułów HSM wymaga premium magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="ff81b-191">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="ff81b-192">Brak dodatkowych kosztów toocreating premium magazynu kluczy, a nie standardowy magazyn kluczy, którego przechowuje klucze chronione przez oprogramowanie.</span><span class="sxs-lookup"><span data-stu-id="ff81b-192">There is an additional cost toocreating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="ff81b-193">Dodaj premium usługi Key Vault w hello poprzedzających krok toocreate `--sku Premium` toohello polecenia.</span><span class="sxs-lookup"><span data-stu-id="ff81b-193">toocreate a premium Key Vault, in hello preceding step add `--sku Premium` toohello command.</span></span> <span data-ttu-id="ff81b-194">Witaj poniższym przykładzie użyto klucze chronione oprogramowaniem ponieważ utworzyliśmy standardowy magazyn kluczy.</span><span class="sxs-lookup"><span data-stu-id="ff81b-194">hello following example uses software-protected keys since we created a standard Key Vault.</span></span>

<span data-ttu-id="ff81b-195">W przypadku obu modeli ochrony hello platformy Azure musi toobe udzielać dostępu do kluczy kryptograficznych hello toorequest, w przypadku, gdy hello maszyny Wirtualnej wykonuje rozruch toodecrypt hello wirtualnych dysków.</span><span class="sxs-lookup"><span data-stu-id="ff81b-195">For both protection models, hello Azure platform needs toobe granted access toorequest hello cryptographic keys when hello VM boots toodecrypt hello virtual disks.</span></span> <span data-ttu-id="ff81b-196">Tworzenie klucza kryptograficznego w magazyn kluczy o [Utwórz klucz keyvault az](/cli/azure/keyvault/key#create).</span><span class="sxs-lookup"><span data-stu-id="ff81b-196">Create a cryptographic key in your Key Vault with [az keyvault key create](/cli/azure/keyvault/key#create).</span></span> <span data-ttu-id="ff81b-197">Witaj poniższym przykładzie jest tworzony klucz o nazwie *klucze*:</span><span class="sxs-lookup"><span data-stu-id="ff81b-197">hello following example creates a key named *myKey*:</span></span>

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```


## <a name="create-hello-azure-active-directory-service-principal"></a><span data-ttu-id="ff81b-198">Utwórz hello nazwy głównej usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ff81b-198">Create hello Azure Active Directory service principal</span></span>
<span data-ttu-id="ff81b-199">Gdy dyski wirtualne są szyfrowane lub odszyfrować, należy określić konto toohandle hello uwierzytelniania i wymiana kluczy kryptograficznych z magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="ff81b-199">When virtual disks are encrypted or decrypted, you specify an account toohandle hello authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="ff81b-200">To konto, nazwy głównej usługi Azure Active Directory umożliwia toorequest platformy Azure hello hello odpowiednich kluczy kryptograficznych imieniu hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ff81b-200">This account, an Azure Active Directory service principal, allows hello Azure platform toorequest hello appropriate cryptographic keys on behalf of hello VM.</span></span> <span data-ttu-id="ff81b-201">Domyślne wystąpienie usługi Azure Active Directory jest dostępne w Twojej subskrypcji, chociaż w wielu organizacjach są wyposażone w dedykowane katalogów usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ff81b-201">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="ff81b-202">Tworzenie nazwy głównej usługi za pomocą usługi Azure Active Directory z [az ad sp utworzyć do rbac](/cli/azure/ad/sp#create-for-rbac).</span><span class="sxs-lookup"><span data-stu-id="ff81b-202">Create a service principal using Azure Active Directory with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span></span> <span data-ttu-id="ff81b-203">Poniższy przykład Hello odczytuje hello wartości dla nazwy głównej usługi hello Id i hasło do użycia w poleceniach nowsze:</span><span class="sxs-lookup"><span data-stu-id="ff81b-203">hello following example reads in hello values for hello service principal Id and password for use in later commands:</span></span>

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

<span data-ttu-id="ff81b-204">hasło Hello jest wyświetlana tylko po utworzeniu usługi hello podmiotu zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="ff81b-204">hello password is only displayed when you create hello service principal.</span></span> <span data-ttu-id="ff81b-205">W razie potrzeby, widok i rejestrowanie hello hasła (`echo $sp_password`).</span><span class="sxs-lookup"><span data-stu-id="ff81b-205">If desired, view and record hello password (`echo $sp_password`).</span></span> <span data-ttu-id="ff81b-206">Możesz wyświetlić listę Twojej nazwy główne usług z [listy sp ad az](/cli/azure/ad/sp#list) i wyświetlić dodatkowe informacje o określonej usługi głównej z [az ad sp Pokaż](/cli/azure/ad/sp#show).</span><span class="sxs-lookup"><span data-stu-id="ff81b-206">You can list your service principals with [az ad sp list](/cli/azure/ad/sp#list) and view additional information about a specific service principal with [az ad sp show](/cli/azure/ad/sp#show).</span></span>

<span data-ttu-id="ff81b-207">toosuccessfully zaszyfrować lub odszyfrować dysków wirtualnych, uprawnienia do klucza kryptograficznego hello przechowywane w magazynie klucza musi być klucze hello tooread główną usługi Azure Active Directory zestaw toopermit hello.</span><span class="sxs-lookup"><span data-stu-id="ff81b-207">toosuccessfully encrypt or decrypt virtual disks, permissions on hello cryptographic key stored in Key Vault must be set toopermit hello Azure Active Directory service principal tooread hello keys.</span></span> <span data-ttu-id="ff81b-208">Ustaw uprawnienia na magazyn kluczy o [keyvault az set-policy](/cli/azure/keyvault#set-policy).</span><span class="sxs-lookup"><span data-stu-id="ff81b-208">Set permissions on your Key Vault with [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span></span> <span data-ttu-id="ff81b-209">W hello poniższy przykład hello usługi identyfikator podmiotu zabezpieczeń jest dostarczana z hello poprzedzających polecenia:</span><span class="sxs-lookup"><span data-stu-id="ff81b-209">In hello following example, hello service principal ID is supplied from hello preceding command:</span></span>

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
  --key-permissions wrapKey \
  --secret-permissions set
```


## <a name="create-virtual-machine"></a><span data-ttu-id="ff81b-210">Tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ff81b-210">Create virtual machine</span></span>
<span data-ttu-id="ff81b-211">tooactually szyfrowania niektóre dyski wirtualne, umożliwia tworzenie maszyny Wirtualnej i Dodaj dysk danych.</span><span class="sxs-lookup"><span data-stu-id="ff81b-211">tooactually encrypt some virtual disks, lets create a VM and add a data disk.</span></span> <span data-ttu-id="ff81b-212">Utwórz tooencrypt maszyny Wirtualnej, z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) i dołączenie dysku danych 5 Gb.</span><span class="sxs-lookup"><span data-stu-id="ff81b-212">Create a VM tooencrypt with [az vm create](/cli/azure/vm#create) and attach a 5Gb data disk.</span></span> <span data-ttu-id="ff81b-213">Niektóre obrazy marketplace obsługuje szyfrowanie dysków.</span><span class="sxs-lookup"><span data-stu-id="ff81b-213">Only certain marketplace images support disk encryption.</span></span> <span data-ttu-id="ff81b-214">Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie *myVM* przy użyciu **CentOS 7.2n** obrazu:</span><span class="sxs-lookup"><span data-stu-id="ff81b-214">hello following example creates a VM named *myVM* using a **CentOS 7.2n** image:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

<span data-ttu-id="ff81b-215">SSH tooyour maszynę Wirtualną przy użyciu hello `publicIpAddress` wyświetlany w danych wyjściowych hello hello poprzedzających polecenia.</span><span class="sxs-lookup"><span data-stu-id="ff81b-215">SSH tooyour VM using hello `publicIpAddress` shown in hello output of hello preceding command.</span></span> <span data-ttu-id="ff81b-216">Tworzenie partycji i systemu plików, a następnie zainstalować dysk danych hello.</span><span class="sxs-lookup"><span data-stu-id="ff81b-216">Create a partition and filesystem, then mount hello data disk.</span></span> <span data-ttu-id="ff81b-217">Aby uzyskać więcej informacji, zobacz [połączyć tooa maszyny Wirtualnej systemu Linux toomount hello nowy dysk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span><span class="sxs-lookup"><span data-stu-id="ff81b-217">For more information, see [Connect tooa Linux VM toomount hello new disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> <span data-ttu-id="ff81b-218">Zamknij sesję SSH.</span><span class="sxs-lookup"><span data-stu-id="ff81b-218">Close your SSH session.</span></span>


## <a name="encrypt-virtual-machine"></a><span data-ttu-id="ff81b-219">Szyfrowanie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ff81b-219">Encrypt virtual machine</span></span>
<span data-ttu-id="ff81b-220">dyski wirtualne hello tooencrypt, przełączeniem razem wszystkie poprzednie składniki hello:</span><span class="sxs-lookup"><span data-stu-id="ff81b-220">tooencrypt hello virtual disks, you bring together all hello previous components:</span></span>

1. <span data-ttu-id="ff81b-221">Określ hello nazwy głównej usługi Azure Active Directory i hasło.</span><span class="sxs-lookup"><span data-stu-id="ff81b-221">Specify hello Azure Active Directory service principal and password.</span></span>
2. <span data-ttu-id="ff81b-222">Określ hello Key Vault toostore hello metadanych dla zaszyfrowanych dysków.</span><span class="sxs-lookup"><span data-stu-id="ff81b-222">Specify hello Key Vault toostore hello metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="ff81b-223">Określ toouse kluczy kryptograficznych hello hello rzeczywiste szyfrowania i odszyfrowywania.</span><span class="sxs-lookup"><span data-stu-id="ff81b-223">Specify hello cryptographic keys toouse for hello actual encryption and decryption.</span></span>
4. <span data-ttu-id="ff81b-224">Określ, czy tooencrypt hello systemu operacyjnego, dysku dysków z danymi hello lub wszystkie.</span><span class="sxs-lookup"><span data-stu-id="ff81b-224">Specify whether you want tooencrypt hello OS disk, hello data disks, or all.</span></span>

<span data-ttu-id="ff81b-225">Szyfrowanie maszyny Wirtualnej z [włączyć szyfrowanie maszyny wirtualnej az](/cli/azure/vm/encryption#enable).</span><span class="sxs-lookup"><span data-stu-id="ff81b-225">Encrypt your VM with [az vm encryption enable](/cli/azure/vm/encryption#enable).</span></span> <span data-ttu-id="ff81b-226">Witaj poniższym przykładzie użyto hello `$sp_id` i `$sp_password` zmienne z poprzednim hello `ad sp create-for-rbac` polecenia:</span><span class="sxs-lookup"><span data-stu-id="ff81b-226">hello following example uses hello `$sp_id` and `$sp_password` variables from hello preceding `ad sp create-for-rbac` command:</span></span>

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```

<span data-ttu-id="ff81b-227">Trwa trochę czasu, zanim toocomplete proces szyfrowania dysku hello.</span><span class="sxs-lookup"><span data-stu-id="ff81b-227">It takes some time for hello disk encryption process toocomplete.</span></span> <span data-ttu-id="ff81b-228">Monitorowanie stanu hello hello procesu z [Pokaż szyfrowania maszyny wirtualnej az](/cli/azure/vm/encryption#show):</span><span class="sxs-lookup"><span data-stu-id="ff81b-228">Monitor hello status of hello process with [az vm encryption show](/cli/azure/vm/encryption#show):</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="ff81b-229">Witaj danych wyjściowych jest toohello podobnie poniższy przykład skrócona:</span><span class="sxs-lookup"><span data-stu-id="ff81b-229">hello output is similar toohello following truncated example:</span></span>

```json
[
  "dataDisk": "EncryptionInProgress",
  "osDisk": "EncryptionInProgress",
]
```

<span data-ttu-id="ff81b-230">Zaczekaj na stan hello raportów dysku systemu operacyjnego hello **VMRestartPending**, ponowne uruchomienie maszyny Wirtualnej z [ponownego uruchomienia maszyny wirtualnej az](/cli/azure/vm#restart):</span><span class="sxs-lookup"><span data-stu-id="ff81b-230">Wait until hello status for hello OS disk reports **VMRestartPending**, then restart your VM with [az vm restart](/cli/azure/vm#restart):</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="ff81b-231">Witaj procesu szyfrowania dysku zostanie sfinalizowana podczas procesu rozruchu hello, więc odczekaj kilka minut przed sprawdzeniem stanu hello szyfrowania ponownie, podając **Pokaż szyfrowania maszyny wirtualnej az**:</span><span class="sxs-lookup"><span data-stu-id="ff81b-231">hello disk encryption process is finalized during hello boot process, so wait a few minutes before checking hello status of encryption again with **az vm encryption show**:</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="ff81b-232">Stan Hello teraz Zgłoś dyskach hello systemu operacyjnego i dysku danych jako **zaszyfrowane**.</span><span class="sxs-lookup"><span data-stu-id="ff81b-232">hello status should now report both hello OS disk and data disk as **Encrypted**.</span></span>


## <a name="add-additional-data-disks"></a><span data-ttu-id="ff81b-233">Dodania dodatkowego dysku z danymi</span><span class="sxs-lookup"><span data-stu-id="ff81b-233">Add additional data disks</span></span>
<span data-ttu-id="ff81b-234">Po zaszyfrowanych dysków z danymi, możesz później dodać tooyour dodatkowych dysków wirtualnych maszyny Wirtualnej i również ich szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="ff81b-234">Once you have encrypted your data disks, you can later add additional virtual disks tooyour VM and also encrypt them.</span></span> <span data-ttu-id="ff81b-235">Na przykład pozwala dodać drugi tooyour dysku wirtualnego maszyny Wirtualnej w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="ff81b-235">For example, lets add a second virtual disk tooyour VM as follows:</span></span>

```azurecli
az vm disk attach-new --resource-group myResourceGroup --vm-name myVM --size-in-gb 5
```

<span data-ttu-id="ff81b-236">Ponownie uruchom dysków wirtualnych tooencrypt hello hello polecenia w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="ff81b-236">Re-run hello command tooencrypt hello virtual disks as follows:</span></span>

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```


## <a name="next-steps"></a><span data-ttu-id="ff81b-237">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ff81b-237">Next steps</span></span>
* <span data-ttu-id="ff81b-238">Aby uzyskać więcej informacji na temat zarządzania usługą Azure Key Vault, łącznie z usunięciem kluczy kryptograficznych i magazyny, zobacz [Zarządzanie Key Vault przy użyciu interfejsu wiersza polecenia](../../key-vault/key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="ff81b-238">For more information about managing Azure Key Vault, including deleting cryptographic keys and vaults, see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md).</span></span>
* <span data-ttu-id="ff81b-239">Aby uzyskać więcej informacji o szyfrowaniu dysków, takich jak przygotowywanie zaszyfrowanego niestandardowego wirtualna tooupload tooAzure, zobacz [szyfrowania dysków Azure](../../security/azure-security-disk-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="ff81b-239">For more information about disk encryption, such as preparing an encrypted custom VM tooupload tooAzure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
