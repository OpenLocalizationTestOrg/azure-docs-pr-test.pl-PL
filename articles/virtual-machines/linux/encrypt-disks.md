---
title: "Szyfrowanie dysków na Maszynę wirtualną systemu Linux na platformie Azure | Dokumentacja firmy Microsoft"
description: "Jak zaszyfrować dysków wirtualnych w maszyny Wirtualnej systemu Linux, aby zwiększyć bezpieczeństwo, za pomocą 2.0 interfejsu wiersza polecenia platformy Azure"
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
ms.openlocfilehash: 172b4c8f5c098d776cb689543f5d8f163b8895b4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-encrypt-virtual-disks-on-a-linux-vm"></a><span data-ttu-id="10014-103">Jak zaszyfrować dyski wirtualne na maszynie Wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="10014-103">How to encrypt virtual disks on a Linux VM</span></span>
<span data-ttu-id="10014-104">Ulepszone maszyny wirtualnej (VM) zabezpieczeń i zgodności mogą być szyfrowane dyski wirtualne na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="10014-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted.</span></span> <span data-ttu-id="10014-105">Dyski są szyfrowane za pomocą kluczy kryptograficznych, które są już zabezpieczone w usłudze Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="10014-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="10014-106">Kontrolowanie tych kluczy kryptograficznych i przeprowadzić inspekcję ich używania.</span><span class="sxs-lookup"><span data-stu-id="10014-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="10014-107">Ten artykuł zawiera szczegóły dotyczące sposobu szyfrowania dysków wirtualnych na Maszynę wirtualną systemu Linux przy użyciu 2.0 interfejsu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="10014-107">This article details how to encrypt virtual disks on a Linux VM using the Azure CLI 2.0.</span></span> <span data-ttu-id="10014-108">Czynności te można również wykonać przy użyciu [interfejsu wiersza polecenia platformy Azure w wersji 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="10014-108">You can also perform these steps with the [Azure CLI 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="10014-109">Szybkie polecenia</span><span class="sxs-lookup"><span data-stu-id="10014-109">Quick commands</span></span>
<span data-ttu-id="10014-110">Jeśli chcesz szybko wykonać zadanie, następujące szczegóły sekcji bazie polecenia do szyfrowania dysków wirtualnych w maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="10014-110">If you need to quickly accomplish the task, the following section details the base commands to encrypt virtual disks on your VM.</span></span> <span data-ttu-id="10014-111">Bardziej szczegółowe informacje i kontekst dla każdego kroku można znaleźć pozostałej części dokumentu, [uruchamiania tutaj](#overview-of-disk-encryption).</span><span class="sxs-lookup"><span data-stu-id="10014-111">More detailed information and context for each step can be found the rest of the document, [starting here](#overview-of-disk-encryption).</span></span>

<span data-ttu-id="10014-112">Należy najnowszej [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zalogowany do konta platformy Azure przy użyciu [logowania az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="10014-112">You need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="10014-113">W poniższych przykładach Zastąp przykładowe nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="10014-113">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="10014-114">Przykład nazwy parametru zawierają *myResourceGroup*, *klucze*, i *myVM*.</span><span class="sxs-lookup"><span data-stu-id="10014-114">Example parameter names include *myResourceGroup*, *myKey*, and *myVM*.</span></span>

<span data-ttu-id="10014-115">Najpierw włączyć dostawcy usługi Azure Key Vault w ramach Twojej subskrypcji platformy Azure z [az dostawcy rejestru](/cli/azure/provider#register) i utworzyć nową grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="10014-115">First, enable the Azure Key Vault provider within your Azure subscription with [az provider register](/cli/azure/provider#register) and create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="10014-116">Poniższy przykład tworzy nazwę grupy zasobów *myResourceGroup* w *eastus* lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="10014-116">The following example creates a resource group name *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="10014-117">Tworzenie usługi Azure Key Vault z [az keyvault utworzyć](/cli/azure/keyvault#create) i włączyć usługi Key Vault służących do szyfrowania dysku.</span><span class="sxs-lookup"><span data-stu-id="10014-117">Create an Azure Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable the Key Vault for use with disk encryption.</span></span> <span data-ttu-id="10014-118">Określ unikatową nazwę usługi Key Vault *keyvault_name* w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="10014-118">Specify a unique Key Vault name for *keyvault_name* as follows:</span></span>

```azurecli
keyvault_name=mykeyvaultikf
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

<span data-ttu-id="10014-119">Tworzenie klucza kryptograficznego w magazyn kluczy o [Utwórz klucz keyvault az](/cli/azure/keyvault/key#create).</span><span class="sxs-lookup"><span data-stu-id="10014-119">Create a cryptographic key in your Key Vault with [az keyvault key create](/cli/azure/keyvault/key#create).</span></span> <span data-ttu-id="10014-120">W poniższym przykładzie jest tworzony klucz o nazwie *klucze*:</span><span class="sxs-lookup"><span data-stu-id="10014-120">The following example creates a key named *myKey*:</span></span>

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```

<span data-ttu-id="10014-121">Tworzenie nazwy głównej usługi za pomocą usługi Azure Active Directory z [az ad sp utworzyć do rbac](/cli/azure/ad/sp#create-for-rbac).</span><span class="sxs-lookup"><span data-stu-id="10014-121">Create a service principal using Azure Active Directory with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span></span> <span data-ttu-id="10014-122">Nazwy głównej usługi obsługuje uwierzytelnianie i wymiany kluczy kryptograficznych z magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="10014-122">The service principal handles the authentication and exchange of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="10014-123">Poniższy przykład odczytuje wartości dla nazwy głównej usługi Id i hasło do wykorzystania w późniejszym polecenia:</span><span class="sxs-lookup"><span data-stu-id="10014-123">The following example reads in the values for the service principal Id and password for use in later commands:</span></span>

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

<span data-ttu-id="10014-124">Hasło jest tylko dane wyjściowe w przypadku tworzenia nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="10014-124">The password is only output when you create the service principal.</span></span> <span data-ttu-id="10014-125">W razie potrzeby można wyświetlać i Zapisz hasło (`echo $sp_password`).</span><span class="sxs-lookup"><span data-stu-id="10014-125">If desired, view and record the password (`echo $sp_password`).</span></span> <span data-ttu-id="10014-126">Możesz wyświetlić listę Twojej nazwy główne usług z [listy sp ad az](/cli/azure/ad/sp#list) i wyświetlić dodatkowe informacje o określonej usługi głównej z [az ad sp Pokaż](/cli/azure/ad/sp#show).</span><span class="sxs-lookup"><span data-stu-id="10014-126">You can list your service principals with [az ad sp list](/cli/azure/ad/sp#list) and view additional information about a specific service principal with [az ad sp show](/cli/azure/ad/sp#show).</span></span>

<span data-ttu-id="10014-127">Ustaw uprawnienia na magazyn kluczy o [keyvault az set-policy](/cli/azure/keyvault#set-policy).</span><span class="sxs-lookup"><span data-stu-id="10014-127">Set permissions on your Key Vault with [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span></span> <span data-ttu-id="10014-128">W poniższym przykładzie identyfikator podmiotu zabezpieczeń usługi jest dostarczana przez poprzednie polecenie:</span><span class="sxs-lookup"><span data-stu-id="10014-128">In the following example, the service principal ID is supplied from the preceding command:</span></span>

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
    --key-permissions wrapKey \
    --secret-permissions set
```

<span data-ttu-id="10014-129">Utwórz maszynę Wirtualną z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) i dołączenie dysku danych 5 Gb.</span><span class="sxs-lookup"><span data-stu-id="10014-129">Create a VM with [az vm create](/cli/azure/vm#create) and attach a 5Gb data disk.</span></span> <span data-ttu-id="10014-130">Niektóre obrazy marketplace obsługuje szyfrowanie dysków.</span><span class="sxs-lookup"><span data-stu-id="10014-130">Only certain marketplace images support disk encryption.</span></span> <span data-ttu-id="10014-131">Poniższy przykład tworzy Maszynę wirtualną o nazwie `myVM` przy użyciu **CentOS 7.2n** obrazu:</span><span class="sxs-lookup"><span data-stu-id="10014-131">The following example creates a VM named `myVM` using a **CentOS 7.2n** image:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

<span data-ttu-id="10014-132">SSH przy użyciu maszyny Wirtualnej `publicIpAddress` wyświetlany w danych wyjściowych poprzednie polecenie.</span><span class="sxs-lookup"><span data-stu-id="10014-132">SSH to your VM using the `publicIpAddress` shown in the output of the preceding command.</span></span> <span data-ttu-id="10014-133">Tworzenie partycji i systemu plików, a następnie zainstalować dysk z danymi.</span><span class="sxs-lookup"><span data-stu-id="10014-133">Create a partition and filesystem, then mount the data disk.</span></span> <span data-ttu-id="10014-134">Aby uzyskać więcej informacji, zobacz [Połącz z maszyny Wirtualnej systemu Linux, aby zainstalować nowy dysk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span><span class="sxs-lookup"><span data-stu-id="10014-134">For more information, see [Connect to a Linux VM to mount the new disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> <span data-ttu-id="10014-135">Zamknij sesję SSH.</span><span class="sxs-lookup"><span data-stu-id="10014-135">Close your SSH session.</span></span>

<span data-ttu-id="10014-136">Szyfrowanie maszyny Wirtualnej z [włączyć szyfrowanie maszyny wirtualnej az](/cli/azure/vm/encryption#enable).</span><span class="sxs-lookup"><span data-stu-id="10014-136">Encrypt your VM with [az vm encryption enable](/cli/azure/vm/encryption#enable).</span></span> <span data-ttu-id="10014-137">W poniższym przykładzie użyto `$sp_id` i `$sp_password` zmienne z poprzednim `ad sp create-for-rbac` polecenie:</span><span class="sxs-lookup"><span data-stu-id="10014-137">The following example uses the `$sp_id` and `$sp_password` variables from the preceding `ad sp create-for-rbac` command:</span></span>

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

<span data-ttu-id="10014-138">Trwa pewien czas na ukończenie procesu szyfrowania dysku.</span><span class="sxs-lookup"><span data-stu-id="10014-138">It takes some time for the disk encryption process to complete.</span></span> <span data-ttu-id="10014-139">Monitorowanie stanu procesu z [Pokaż szyfrowania maszyny wirtualnej az](/cli/azure/vm/encryption#show):</span><span class="sxs-lookup"><span data-stu-id="10014-139">Monitor the status of the process with [az vm encryption show](/cli/azure/vm/encryption#show):</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="10014-140">Pokazuje stan **EncryptionInProgress**.</span><span class="sxs-lookup"><span data-stu-id="10014-140">The status shows **EncryptionInProgress**.</span></span> <span data-ttu-id="10014-141">Poczekaj, aż stan systemu operacyjnego na dysku raporty **VMRestartPending**, ponowne uruchomienie maszyny Wirtualnej z [ponownego uruchomienia maszyny wirtualnej az](/cli/azure/vm#restart):</span><span class="sxs-lookup"><span data-stu-id="10014-141">Wait until the status for the OS disk reports **VMRestartPending**, then restart your VM with [az vm restart](/cli/azure/vm#restart):</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="10014-142">Proces szyfrowania dysku zostanie sfinalizowana podczas rozruchu, więc odczekaj kilka minut przed sprawdzeniem stanu szyfrowania ponownie, podając **Pokaż szyfrowania maszyny wirtualnej az**:</span><span class="sxs-lookup"><span data-stu-id="10014-142">The disk encryption process is finalized during the boot process, so wait a few minutes before checking the status of encryption again with **az vm encryption show**:</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="10014-143">Stan Zgłoś teraz dysk systemu operacyjnego i dysku danych jako **zaszyfrowane**.</span><span class="sxs-lookup"><span data-stu-id="10014-143">The status should now report both the OS disk and data disk as **Encrypted**.</span></span>

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="10014-144">Omówienie szyfrowania dysków</span><span class="sxs-lookup"><span data-stu-id="10014-144">Overview of disk encryption</span></span>
<span data-ttu-id="10014-145">Dyski wirtualne na maszynach wirtualnych systemu Linux są szyfrowane za pomocą rest [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span><span class="sxs-lookup"><span data-stu-id="10014-145">Virtual disks on Linux VMs are encrypted at rest using [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span></span> <span data-ttu-id="10014-146">Jest bezpłatna dla szyfrowania dysków wirtualnych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="10014-146">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="10014-147">Klucze szyfrowania są przechowywane w usługi Azure Key Vault przy użyciu ochrony oprogramowania, lub możesz zaimportować lub wygenerować klucze w sprzętowych modułach zabezpieczeń (HSM) certyfikowane do FIPS 140-2 poziom 2 standardów.</span><span class="sxs-lookup"><span data-stu-id="10014-147">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified to FIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="10014-148">Zachowanie kontroli nad tych kluczy kryptograficznych i przeprowadzić inspekcję ich używania.</span><span class="sxs-lookup"><span data-stu-id="10014-148">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="10014-149">Te klucze szyfrowania są używane do szyfrowania i odszyfrowywania wirtualnych dysków dołączonych do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="10014-149">These cryptographic keys are used to encrypt and decrypt virtual disks attached to your VM.</span></span> <span data-ttu-id="10014-150">Nazwy głównej usługi Azure Active Directory zapewnia mechanizm bezpiecznego do wystawiania tych kluczy kryptograficznych, ponieważ maszyny wirtualne są zasilane i wyłączanie.</span><span class="sxs-lookup"><span data-stu-id="10014-150">An Azure Active Directory service principal provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="10014-151">Proces szyfrowania maszyny Wirtualnej jest następujący:</span><span class="sxs-lookup"><span data-stu-id="10014-151">The process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="10014-152">Tworzenie klucza kryptograficznego w usłudze Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="10014-152">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="10014-153">Skonfiguruj klucza kryptograficznego, który może być używany do szyfrowania dysków.</span><span class="sxs-lookup"><span data-stu-id="10014-153">Configure the cryptographic key to be usable for encrypting disks.</span></span>
3. <span data-ttu-id="10014-154">Aby odczytać klucza kryptograficznego z usługi Azure Key Vault, utworzyć usługę Azure Active Directory podmiot z odpowiednimi uprawnieniami.</span><span class="sxs-lookup"><span data-stu-id="10014-154">To read the cryptographic key from the Azure Key Vault, create an Azure Active Directory service principal with the appropriate permissions.</span></span>
4. <span data-ttu-id="10014-155">Wydaj polecenie wirtualnych dysków, określając usługi Azure Active Directory usługa podmiotu zabezpieczeń i odpowiednie klucza kryptograficznego używanego do szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="10014-155">Issue the command to encrypt your virtual disks, specifying the Azure Active Directory service principal and appropriate cryptographic key to be used.</span></span>
5. <span data-ttu-id="10014-156">Nazwy głównej usługi Azure Active Directory żądań wymaganego klucza kryptograficznego z usługi Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="10014-156">The Azure Active Directory service principal requests the required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="10014-157">Dyski wirtualne są szyfrowane za pomocą podanego klucza kryptograficznego.</span><span class="sxs-lookup"><span data-stu-id="10014-157">The virtual disks are encrypted using the provided cryptographic key.</span></span>

## <a name="encryption-process"></a><span data-ttu-id="10014-158">Proces szyfrowania</span><span class="sxs-lookup"><span data-stu-id="10014-158">Encryption process</span></span>
<span data-ttu-id="10014-159">Szyfrowanie dysków opiera się na następujące dodatkowe składniki:</span><span class="sxs-lookup"><span data-stu-id="10014-159">Disk encryption relies on the following additional components:</span></span>

* <span data-ttu-id="10014-160">**Usługa Azure Key Vault** — używane do ochrony kluczy kryptograficznych i kluczy tajnych używanych przez proces szyfrowania i odszyfrowywania dysku.</span><span class="sxs-lookup"><span data-stu-id="10014-160">**Azure Key Vault** - used to safeguard cryptographic keys and secrets used for the disk encryption/decryption process.</span></span>
  * <span data-ttu-id="10014-161">Jeśli istnieje, można użyć istniejącego magazynu kluczy Azure.</span><span class="sxs-lookup"><span data-stu-id="10014-161">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="10014-162">Nie trzeba przeznaczyć magazyn kluczy szyfrowania dysków.</span><span class="sxs-lookup"><span data-stu-id="10014-162">You do not have to dedicate a Key Vault to encrypting disks.</span></span>
  * <span data-ttu-id="10014-163">Aby rozdzielić granice administracyjne i widoczności klucza, możesz utworzyć dedykowany magazyn kluczy.</span><span class="sxs-lookup"><span data-stu-id="10014-163">To separate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="10014-164">**Usługa Azure Active Directory** — obsługuje bezpiecznej wymiany wymagane klucze szyfrowania i uwierzytelniania dla żądanej akcji.</span><span class="sxs-lookup"><span data-stu-id="10014-164">**Azure Active Directory** - handles the secure exchanging of required cryptographic keys and authentication for requested actions.</span></span>
  * <span data-ttu-id="10014-165">Zazwyczaj można użyć istniejącego wystąpienia usługi Azure Active Directory, do przechowywania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="10014-165">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="10014-166">Nazwy głównej usługi zapewnia mechanizm bezpiecznego do żądania i wydawane odpowiednich kluczy kryptograficznych.</span><span class="sxs-lookup"><span data-stu-id="10014-166">The service principal provides a secure mechanism to request and be issued the appropriate cryptographic keys.</span></span> <span data-ttu-id="10014-167">Nie opracowujesz aplikację rzeczywista, która integruje się z usługą Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="10014-167">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="10014-168">Wymagania i ograniczenia</span><span class="sxs-lookup"><span data-stu-id="10014-168">Requirements and limitations</span></span>
<span data-ttu-id="10014-169">Obsługiwane scenariusze i wymagania dotyczące szyfrowania dysków:</span><span class="sxs-lookup"><span data-stu-id="10014-169">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="10014-170">Następujący serwer z systemem Linux jednostki SKU - Ubuntu, CentOS, SUSE i SUSE Linux Enterprise Server (SLES) i Red Hat Enterprise Linux.</span><span class="sxs-lookup"><span data-stu-id="10014-170">The following Linux server SKUs - Ubuntu, CentOS, SUSE and SUSE Linux Enterprise Server (SLES), and Red Hat Enterprise Linux.</span></span>
* <span data-ttu-id="10014-171">Wszystkie zasoby (na przykład usługi Key Vault, konta magazynu i maszyny Wirtualnej) muszą być w tym samym regionie Azure i subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="10014-171">All resources (such as Key Vault, Storage account, and VM) must be in the same Azure region and subscription.</span></span>
* <span data-ttu-id="10014-172">Standardowa A, D DS, G i GS seria maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="10014-172">Standard A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="10014-173">Szyfrowanie dysku nie jest obecnie obsługiwane w następujących scenariuszach:</span><span class="sxs-lookup"><span data-stu-id="10014-173">Disk encryption is not currently supported in the following scenarios:</span></span>

* <span data-ttu-id="10014-174">Maszyny wirtualne warstwy podstawowa.</span><span class="sxs-lookup"><span data-stu-id="10014-174">Basic tier VMs.</span></span>
* <span data-ttu-id="10014-175">Maszyny wirtualne utworzone przy użyciu klasycznego modelu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="10014-175">VMs created using the Classic deployment model.</span></span>
* <span data-ttu-id="10014-176">Wyłączenie szyfrowania dysku systemu operacyjnego na maszynach wirtualnych systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="10014-176">Disabling OS disk encryption on Linux VMs.</span></span>
* <span data-ttu-id="10014-177">Aktualizowanie kluczy kryptograficznych w już zaszyfrowany maszyny Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="10014-177">Updating the cryptographic keys on an already encrypted Linux VM.</span></span>

## <a name="create-azure-key-vault-and-keys"></a><span data-ttu-id="10014-178">Tworzenie usługi Azure Key Vault i kluczy</span><span class="sxs-lookup"><span data-stu-id="10014-178">Create Azure Key Vault and keys</span></span>
<span data-ttu-id="10014-179">Należy najnowszej [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zalogowany do konta platformy Azure przy użyciu [logowania az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="10014-179">You need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="10014-180">W poniższych przykładach Zastąp przykładowe nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="10014-180">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="10014-181">Przykład nazwy parametru zawierają *myResourceGroup*, *klucze*, i *myVM*.</span><span class="sxs-lookup"><span data-stu-id="10014-181">Example parameter names include *myResourceGroup*, *myKey*, and *myVM*.</span></span>

<span data-ttu-id="10014-182">Pierwszym krokiem jest do utworzenia magazynu kluczy Azure do przechowywania kluczy kryptograficznych.</span><span class="sxs-lookup"><span data-stu-id="10014-182">The first step is to create an Azure Key Vault to store your cryptographic keys.</span></span> <span data-ttu-id="10014-183">Usługa Azure Key Vault można przechowywać kluczy, kluczy tajnych lub haseł, które umożliwiają bezpieczne wdrożenie ich w aplikacji i usług.</span><span class="sxs-lookup"><span data-stu-id="10014-183">Azure Key Vault can store keys, secrets, or passwords that allow you to securely implement them in your applications and services.</span></span> <span data-ttu-id="10014-184">Szyfrowanie dysków wirtualnych Key Vault służy do przechowywania klucza kryptograficznego używanego do szyfrowania lub odszyfrowywania dysków wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="10014-184">For virtual disk encryption, you use Key Vault to store a cryptographic key that is used to encrypt or decrypt your virtual disks.</span></span>

<span data-ttu-id="10014-185">Włącz dostawcy usługi Azure Key Vault w ramach Twojej subskrypcji platformy Azure z [az dostawcy rejestru](/cli/azure/provider#register) i utworzyć nową grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="10014-185">Enable the Azure Key Vault provider within your Azure subscription with [az provider register](/cli/azure/provider#register) and create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="10014-186">Poniższy przykład tworzy nazwę grupy zasobów *myResourceGroup* w `eastus` lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="10014-186">The following example creates a resource group name *myResourceGroup* in the `eastus` location:</span></span>

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="10014-187">Usługa Azure Key Vault zawierający klucze kryptograficzne i zasoby obliczeniowe skojarzone, takie jak magazyn i samej maszyny Wirtualnej musi znajdować się w tym samym regionie.</span><span class="sxs-lookup"><span data-stu-id="10014-187">The Azure Key Vault containing the cryptographic keys and associated compute resources such as storage and the VM itself must reside in the same region.</span></span> <span data-ttu-id="10014-188">Tworzenie usługi Azure Key Vault z [az keyvault utworzyć](/cli/azure/keyvault#create) i włączyć usługi Key Vault służących do szyfrowania dysku.</span><span class="sxs-lookup"><span data-stu-id="10014-188">Create an Azure Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable the Key Vault for use with disk encryption.</span></span> <span data-ttu-id="10014-189">Określ unikatową nazwę usługi Key Vault *keyvault_name* w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="10014-189">Specify a unique Key Vault name for *keyvault_name* as follows:</span></span>

```azurecli
keyvault_name=myUniqueKeyVaultName
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

<span data-ttu-id="10014-190">Mogą być przechowywane przy użyciu oprogramowania lub sprzętu modelu zabezpieczeń (HSM) ochronę kluczy kryptograficznych.</span><span class="sxs-lookup"><span data-stu-id="10014-190">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="10014-191">Użycie modułów HSM wymaga premium magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="10014-191">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="10014-192">Brak dodatkowych kosztów tworzenia premium magazynu kluczy, a nie standardowy magazyn kluczy, którego przechowuje klucze chronione przez oprogramowanie.</span><span class="sxs-lookup"><span data-stu-id="10014-192">There is an additional cost to creating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="10014-193">Aby utworzyć premium magazynu kluczy, w poprzednim kroku Dodaj `--sku Premium` do polecenia.</span><span class="sxs-lookup"><span data-stu-id="10014-193">To create a premium Key Vault, in the preceding step add `--sku Premium` to the command.</span></span> <span data-ttu-id="10014-194">W poniższym przykładzie użyto klucze chronione przez oprogramowanie, ponieważ utworzono standardowe magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="10014-194">The following example uses software-protected keys since we created a standard Key Vault.</span></span>

<span data-ttu-id="10014-195">W przypadku obu modeli ochrony platformy Azure musi otrzymać dostęp do żądania kluczy kryptograficznych, podczas rozruchu maszyny Wirtualnej do odszyfrowania dysków wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="10014-195">For both protection models, the Azure platform needs to be granted access to request the cryptographic keys when the VM boots to decrypt the virtual disks.</span></span> <span data-ttu-id="10014-196">Tworzenie klucza kryptograficznego w magazyn kluczy o [Utwórz klucz keyvault az](/cli/azure/keyvault/key#create).</span><span class="sxs-lookup"><span data-stu-id="10014-196">Create a cryptographic key in your Key Vault with [az keyvault key create](/cli/azure/keyvault/key#create).</span></span> <span data-ttu-id="10014-197">W poniższym przykładzie jest tworzony klucz o nazwie *klucze*:</span><span class="sxs-lookup"><span data-stu-id="10014-197">The following example creates a key named *myKey*:</span></span>

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```


## <a name="create-the-azure-active-directory-service-principal"></a><span data-ttu-id="10014-198">Tworzenie nazwy głównej usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="10014-198">Create the Azure Active Directory service principal</span></span>
<span data-ttu-id="10014-199">Podczas dyski wirtualne są zaszyfrowanie lub odszyfrowanie, należy określić konto w celu obsługi uwierzytelniania i wymiany kluczy kryptograficznych z magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="10014-199">When virtual disks are encrypted or decrypted, you specify an account to handle the authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="10014-200">To konto, nazwy głównej usługi Azure Active Directory umożliwia platformy Azure zażądać odpowiednich kluczy kryptograficznych w imieniu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="10014-200">This account, an Azure Active Directory service principal, allows the Azure platform to request the appropriate cryptographic keys on behalf of the VM.</span></span> <span data-ttu-id="10014-201">Domyślne wystąpienie usługi Azure Active Directory jest dostępne w Twojej subskrypcji, chociaż w wielu organizacjach są wyposażone w dedykowane katalogów usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="10014-201">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="10014-202">Tworzenie nazwy głównej usługi za pomocą usługi Azure Active Directory z [az ad sp utworzyć do rbac](/cli/azure/ad/sp#create-for-rbac).</span><span class="sxs-lookup"><span data-stu-id="10014-202">Create a service principal using Azure Active Directory with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span></span> <span data-ttu-id="10014-203">Poniższy przykład odczytuje wartości dla nazwy głównej usługi Id i hasło do wykorzystania w późniejszym polecenia:</span><span class="sxs-lookup"><span data-stu-id="10014-203">The following example reads in the values for the service principal Id and password for use in later commands:</span></span>

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

<span data-ttu-id="10014-204">Hasło jest wyświetlane tylko, tworząc usługę podmiotu zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="10014-204">The password is only displayed when you create the service principal.</span></span> <span data-ttu-id="10014-205">W razie potrzeby można wyświetlać i Zapisz hasło (`echo $sp_password`).</span><span class="sxs-lookup"><span data-stu-id="10014-205">If desired, view and record the password (`echo $sp_password`).</span></span> <span data-ttu-id="10014-206">Możesz wyświetlić listę Twojej nazwy główne usług z [listy sp ad az](/cli/azure/ad/sp#list) i wyświetlić dodatkowe informacje o określonej usługi głównej z [az ad sp Pokaż](/cli/azure/ad/sp#show).</span><span class="sxs-lookup"><span data-stu-id="10014-206">You can list your service principals with [az ad sp list](/cli/azure/ad/sp#list) and view additional information about a specific service principal with [az ad sp show](/cli/azure/ad/sp#show).</span></span>

<span data-ttu-id="10014-207">Pomyślnie szyfrowania lub odszyfrowywania dysków wirtualnych, uprawnienia do klucza kryptograficznego, przechowywane w magazynie klucz musi mieć ustawioną zezwolenie na nazwę główną usługi Azure Active Directory do odczytu kluczy.</span><span class="sxs-lookup"><span data-stu-id="10014-207">To successfully encrypt or decrypt virtual disks, permissions on the cryptographic key stored in Key Vault must be set to permit the Azure Active Directory service principal to read the keys.</span></span> <span data-ttu-id="10014-208">Ustaw uprawnienia na magazyn kluczy o [keyvault az set-policy](/cli/azure/keyvault#set-policy).</span><span class="sxs-lookup"><span data-stu-id="10014-208">Set permissions on your Key Vault with [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span></span> <span data-ttu-id="10014-209">W poniższym przykładzie identyfikator podmiotu zabezpieczeń usługi jest dostarczana przez poprzednie polecenie:</span><span class="sxs-lookup"><span data-stu-id="10014-209">In the following example, the service principal ID is supplied from the preceding command:</span></span>

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
  --key-permissions wrapKey \
  --secret-permissions set
```


## <a name="create-virtual-machine"></a><span data-ttu-id="10014-210">Tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="10014-210">Create virtual machine</span></span>
<span data-ttu-id="10014-211">Do szyfrowania faktycznie niektóre dyski wirtualne, umożliwia tworzenie maszyny Wirtualnej i Dodaj dysk danych.</span><span class="sxs-lookup"><span data-stu-id="10014-211">To actually encrypt some virtual disks, lets create a VM and add a data disk.</span></span> <span data-ttu-id="10014-212">Utwórz maszynę Wirtualną do szyfrowania z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) i dołączenie dysku danych 5 Gb.</span><span class="sxs-lookup"><span data-stu-id="10014-212">Create a VM to encrypt with [az vm create](/cli/azure/vm#create) and attach a 5Gb data disk.</span></span> <span data-ttu-id="10014-213">Niektóre obrazy marketplace obsługuje szyfrowanie dysków.</span><span class="sxs-lookup"><span data-stu-id="10014-213">Only certain marketplace images support disk encryption.</span></span> <span data-ttu-id="10014-214">Poniższy przykład tworzy Maszynę wirtualną o nazwie *myVM* przy użyciu **CentOS 7.2n** obrazu:</span><span class="sxs-lookup"><span data-stu-id="10014-214">The following example creates a VM named *myVM* using a **CentOS 7.2n** image:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

<span data-ttu-id="10014-215">SSH przy użyciu maszyny Wirtualnej `publicIpAddress` wyświetlany w danych wyjściowych poprzednie polecenie.</span><span class="sxs-lookup"><span data-stu-id="10014-215">SSH to your VM using the `publicIpAddress` shown in the output of the preceding command.</span></span> <span data-ttu-id="10014-216">Tworzenie partycji i systemu plików, a następnie zainstalować dysk z danymi.</span><span class="sxs-lookup"><span data-stu-id="10014-216">Create a partition and filesystem, then mount the data disk.</span></span> <span data-ttu-id="10014-217">Aby uzyskać więcej informacji, zobacz [Połącz z maszyny Wirtualnej systemu Linux, aby zainstalować nowy dysk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span><span class="sxs-lookup"><span data-stu-id="10014-217">For more information, see [Connect to a Linux VM to mount the new disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> <span data-ttu-id="10014-218">Zamknij sesję SSH.</span><span class="sxs-lookup"><span data-stu-id="10014-218">Close your SSH session.</span></span>


## <a name="encrypt-virtual-machine"></a><span data-ttu-id="10014-219">Szyfrowanie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="10014-219">Encrypt virtual machine</span></span>
<span data-ttu-id="10014-220">Do szyfrowania dysków wirtualnych, można przenosić ze sobą wszystkie poprzednie składniki:</span><span class="sxs-lookup"><span data-stu-id="10014-220">To encrypt the virtual disks, you bring together all the previous components:</span></span>

1. <span data-ttu-id="10014-221">Podaj nazwę główną usługi Azure Active Directory i hasło.</span><span class="sxs-lookup"><span data-stu-id="10014-221">Specify the Azure Active Directory service principal and password.</span></span>
2. <span data-ttu-id="10014-222">Określ Key Vault w celu przechowywania metadanych dla zaszyfrowanych dysków.</span><span class="sxs-lookup"><span data-stu-id="10014-222">Specify the Key Vault to store the metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="10014-223">Określ klucze kryptograficzne służące do rzeczywistego szyfrowania i odszyfrowywania.</span><span class="sxs-lookup"><span data-stu-id="10014-223">Specify the cryptographic keys to use for the actual encryption and decryption.</span></span>
4. <span data-ttu-id="10014-224">Określ, czy chcesz zaszyfrować dysk systemu operacyjnego, dyski danych lub all.</span><span class="sxs-lookup"><span data-stu-id="10014-224">Specify whether you want to encrypt the OS disk, the data disks, or all.</span></span>

<span data-ttu-id="10014-225">Szyfrowanie maszyny Wirtualnej z [włączyć szyfrowanie maszyny wirtualnej az](/cli/azure/vm/encryption#enable).</span><span class="sxs-lookup"><span data-stu-id="10014-225">Encrypt your VM with [az vm encryption enable](/cli/azure/vm/encryption#enable).</span></span> <span data-ttu-id="10014-226">W poniższym przykładzie użyto `$sp_id` i `$sp_password` zmienne z poprzednim `ad sp create-for-rbac` polecenie:</span><span class="sxs-lookup"><span data-stu-id="10014-226">The following example uses the `$sp_id` and `$sp_password` variables from the preceding `ad sp create-for-rbac` command:</span></span>

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

<span data-ttu-id="10014-227">Trwa pewien czas na ukończenie procesu szyfrowania dysku.</span><span class="sxs-lookup"><span data-stu-id="10014-227">It takes some time for the disk encryption process to complete.</span></span> <span data-ttu-id="10014-228">Monitorowanie stanu procesu z [Pokaż szyfrowania maszyny wirtualnej az](/cli/azure/vm/encryption#show):</span><span class="sxs-lookup"><span data-stu-id="10014-228">Monitor the status of the process with [az vm encryption show](/cli/azure/vm/encryption#show):</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="10014-229">Wynik jest podobny do poniższego przykładu skrócona:</span><span class="sxs-lookup"><span data-stu-id="10014-229">The output is similar to the following truncated example:</span></span>

```json
[
  "dataDisk": "EncryptionInProgress",
  "osDisk": "EncryptionInProgress",
]
```

<span data-ttu-id="10014-230">Poczekaj, aż stan systemu operacyjnego na dysku raporty **VMRestartPending**, ponowne uruchomienie maszyny Wirtualnej z [ponownego uruchomienia maszyny wirtualnej az](/cli/azure/vm#restart):</span><span class="sxs-lookup"><span data-stu-id="10014-230">Wait until the status for the OS disk reports **VMRestartPending**, then restart your VM with [az vm restart](/cli/azure/vm#restart):</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="10014-231">Proces szyfrowania dysku zostanie sfinalizowana podczas rozruchu, więc odczekaj kilka minut przed sprawdzeniem stanu szyfrowania ponownie, podając **Pokaż szyfrowania maszyny wirtualnej az**:</span><span class="sxs-lookup"><span data-stu-id="10014-231">The disk encryption process is finalized during the boot process, so wait a few minutes before checking the status of encryption again with **az vm encryption show**:</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="10014-232">Stan Zgłoś teraz dysk systemu operacyjnego i dysku danych jako **zaszyfrowane**.</span><span class="sxs-lookup"><span data-stu-id="10014-232">The status should now report both the OS disk and data disk as **Encrypted**.</span></span>


## <a name="add-additional-data-disks"></a><span data-ttu-id="10014-233">Dodania dodatkowego dysku z danymi</span><span class="sxs-lookup"><span data-stu-id="10014-233">Add additional data disks</span></span>
<span data-ttu-id="10014-234">Po zaszyfrowanych dysków z danymi, możesz później dodać dodatkowych dysków wirtualnych do maszyny Wirtualnej i również ich szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="10014-234">Once you have encrypted your data disks, you can later add additional virtual disks to your VM and also encrypt them.</span></span> <span data-ttu-id="10014-235">Na przykład pozwala dodać drugi wirtualny dysk do maszyny Wirtualnej w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="10014-235">For example, lets add a second virtual disk to your VM as follows:</span></span>

```azurecli
az vm disk attach-new --resource-group myResourceGroup --vm-name myVM --size-in-gb 5
```

<span data-ttu-id="10014-236">Uruchom ponownie polecenie do szyfrowania dysków wirtualnych w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="10014-236">Re-run the command to encrypt the virtual disks as follows:</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="10014-237">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="10014-237">Next steps</span></span>
* <span data-ttu-id="10014-238">Aby uzyskać więcej informacji na temat zarządzania usługą Azure Key Vault, łącznie z usunięciem kluczy kryptograficznych i magazyny, zobacz [Zarządzanie Key Vault przy użyciu interfejsu wiersza polecenia](../../key-vault/key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="10014-238">For more information about managing Azure Key Vault, including deleting cryptographic keys and vaults, see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md).</span></span>
* <span data-ttu-id="10014-239">Aby uzyskać więcej informacji o szyfrowaniu dysków, takich jak przygotowywanie zaszyfrowanego niestandardowego maszyny Wirtualnej do przekazania do platformy Azure, zobacz [szyfrowania dysków Azure](../../security/azure-security-disk-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="10014-239">For more information about disk encryption, such as preparing an encrypted custom VM to upload to Azure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
