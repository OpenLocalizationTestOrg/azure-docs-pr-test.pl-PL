---
title: "Szyfrowanie dysków na Maszynę wirtualną systemu Linux z interfejsu wiersza polecenia platformy Azure w wersji 1.0 | Dokumentacja firmy Microsoft"
description: "Jak zaszyfrować dysków na Maszynę wirtualną systemu Linux przy użyciu 1.0 interfejsu wiersza polecenia platformy Azure i modelu wdrażania usługi Resource Manager"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/06/2017
ms.author: iainfou
ms.openlocfilehash: b436f2d43c41000f4385889edb3fa3983d4a8c66
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="encrypt-disks-on-a-linux-vm-using-the-azure-cli-10"></a><span data-ttu-id="29614-103">Szyfrowanie dysków na Maszynę wirtualną systemu Linux przy użyciu 1.0 interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="29614-103">Encrypt disks on a Linux VM using the Azure CLI 1.0</span></span>
<span data-ttu-id="29614-104">Ulepszone maszyny wirtualnej (VM) zabezpieczeń i zgodności dyski wirtualne na platformie Azure mogą być szyfrowane w stanie spoczynku.</span><span class="sxs-lookup"><span data-stu-id="29614-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted at rest.</span></span> <span data-ttu-id="29614-105">Dyski są szyfrowane za pomocą kluczy kryptograficznych, które są już zabezpieczone w usłudze Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="29614-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="29614-106">Kontrolowanie tych kluczy kryptograficznych i przeprowadzić inspekcję ich używania.</span><span class="sxs-lookup"><span data-stu-id="29614-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="29614-107">Ten artykuł zawiera szczegóły dotyczące sposobu szyfrowania dysków wirtualnych na Maszynę wirtualną systemu Linux przy użyciu 1.0 interfejsu wiersza polecenia platformy Azure i modelu wdrażania usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="29614-107">This article details how to encrypt virtual disks on a Linux VM using the Azure CLI 1.0 and the Resource Manager deployment model.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="29614-108">Wersje interfejsu wiersza polecenia umożliwiające wykonanie zadania</span><span class="sxs-lookup"><span data-stu-id="29614-108">CLI versions to complete the task</span></span>
<span data-ttu-id="29614-109">Zadanie można wykonać przy użyciu jednej z następujących wersji interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="29614-109">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="29614-110">[Azure CLI 1.0](#quick-commands) — nasze interfejsu wiersza polecenia dla klasycznego i zasobów zarządzania wdrażania modeli (w tym artykule)</span><span class="sxs-lookup"><span data-stu-id="29614-110">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="29614-111">[Interfejs wiersza polecenia platformy Azure w wersji 2.0](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) — nasz interfejs wiersza polecenia nowej generacji dla modelu wdrażania na potrzeby zarządzania zasobami</span><span class="sxs-lookup"><span data-stu-id="29614-111">[Azure CLI 2.0](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>

## <a name="quick-commands"></a><span data-ttu-id="29614-112">Szybkie polecenia</span><span class="sxs-lookup"><span data-stu-id="29614-112">Quick commands</span></span>
<span data-ttu-id="29614-113">Jeśli chcesz szybko wykonać zadanie, następujące szczegóły sekcji bazie polecenia do szyfrowania dysków wirtualnych w maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="29614-113">If you need to quickly accomplish the task, the following section details the base commands to encrypt virtual disks on your VM.</span></span> <span data-ttu-id="29614-114">Bardziej szczegółowe informacje i kontekst dla każdego kroku można znaleźć pozostałej części dokumentu, [uruchamiania tutaj](#overview-of-disk-encryption).</span><span class="sxs-lookup"><span data-stu-id="29614-114">More detailed information and context for each step can be found the rest of the document, [starting here](#overview-of-disk-encryption).</span></span>

<span data-ttu-id="29614-115">Należy [najnowsze Azure CLI 1.0](../../xplat-cli-install.md) zainstalowane i zarejestrowane w trybie Menedżera zasobów w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="29614-115">You need the [latest Azure CLI 1.0](../../xplat-cli-install.md) installed and logged in using the Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="29614-116">W poniższych przykładach Zastąp przykładowe nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="29614-116">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="29614-117">Przykład nazwy parametru zawierają `myResourceGroup`, `myKeyVault`, i `myVM`.</span><span class="sxs-lookup"><span data-stu-id="29614-117">Example parameter names include `myResourceGroup`, `myKeyVault`, and `myVM`.</span></span>

<span data-ttu-id="29614-118">Najpierw należy włączyć dostawcy usługi Azure Key Vault w ramach Twojej subskrypcji platformy Azure i Utwórz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="29614-118">First, enable the Azure Key Vault provider within your Azure subscription and create a resource group.</span></span> <span data-ttu-id="29614-119">Poniższy przykład tworzy nazwę grupy zasobów `myResourceGroup` w `WestUS` lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="29614-119">The following example creates a resource group name `myResourceGroup` in the `WestUS` location:</span></span>

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

<span data-ttu-id="29614-120">Tworzenie usługi Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="29614-120">Create an Azure Key Vault.</span></span> <span data-ttu-id="29614-121">Poniższy przykład tworzy magazyn kluczy o nazwie `myKeyVault`:</span><span class="sxs-lookup"><span data-stu-id="29614-121">The following example creates a Key Vault named `myKeyVault`:</span></span>

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

<span data-ttu-id="29614-122">Tworzenie klucza kryptograficznego w magazyn kluczy i Włącz szyfrowanie dysków.</span><span class="sxs-lookup"><span data-stu-id="29614-122">Create a cryptographic key in your Key Vault and enable it for disk encryption.</span></span> <span data-ttu-id="29614-123">W poniższym przykładzie jest tworzony klucz o nazwie `myKey`:</span><span class="sxs-lookup"><span data-stu-id="29614-123">The following example creates a key named `myKey`:</span></span>

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```

<span data-ttu-id="29614-124">Tworzenie punktu końcowego za pomocą usługi Azure Active Directory do obsługi uwierzytelniania i wymiany kluczy kryptograficznych z magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="29614-124">Create an endpoint using Azure Active Directory for handling the authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="29614-125">`--home-page` i `--identifier-uris` musi być rzeczywiste adresów obsługi routingu.</span><span class="sxs-lookup"><span data-stu-id="29614-125">The `--home-page` and `--identifier-uris` do not need to be actual routable address.</span></span> <span data-ttu-id="29614-126">W przypadku najwyższy poziom zabezpieczeń kluczy tajnych klientów należy użyć zamiast hasła.</span><span class="sxs-lookup"><span data-stu-id="29614-126">For the highest level of security, client secrets should be used instead of passwords.</span></span> <span data-ttu-id="29614-127">Interfejsu wiersza polecenia Azure aktualnie nie można wygenerować kluczy tajnych klientów.</span><span class="sxs-lookup"><span data-stu-id="29614-127">The Azure CLI cannot currently generate client secrets.</span></span> <span data-ttu-id="29614-128">Kluczy tajnych klientów mogą być generowane tylko w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="29614-128">Client secrets can only be generated in the Azure portal.</span></span> <span data-ttu-id="29614-129">Poniższy przykład tworzy punkt końcowy usługi Azure Active Directory o nazwie `myAADApp` i używa hasła `myPassword`.</span><span class="sxs-lookup"><span data-stu-id="29614-129">The following example creates an Azure Active Directory endpoint named `myAADApp` and uses a password of `myPassword`.</span></span> <span data-ttu-id="29614-130">Określ własnego hasła w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="29614-130">Specify your own password as follows:</span></span>

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

<span data-ttu-id="29614-131">Uwaga `applicationId` wyświetlany w danych wyjściowych z poprzedniego polecenia.</span><span class="sxs-lookup"><span data-stu-id="29614-131">Note the `applicationId` shown in the output from the preceding command.</span></span> <span data-ttu-id="29614-132">Ten identyfikator aplikacji jest używany w poniższych krokach:</span><span class="sxs-lookup"><span data-stu-id="29614-132">This application ID is used in the following steps:</span></span>

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```

<span data-ttu-id="29614-133">Dodaj dysk danych do istniejącej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="29614-133">Add a data disk to an existing VM.</span></span> <span data-ttu-id="29614-134">W poniższym przykładzie dodano dysk z danymi do maszyny Wirtualnej o nazwie `myVM`:</span><span class="sxs-lookup"><span data-stu-id="29614-134">The following example adds a data disk to a VM named `myVM`:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="29614-135">Przejrzyj szczegóły magazyn kluczy i klucza, który został utworzony.</span><span class="sxs-lookup"><span data-stu-id="29614-135">Review the details for your Key Vault and the key you created.</span></span> <span data-ttu-id="29614-136">Potrzebny jest identyfikator magazynu kluczy, identyfikator URI i klucz adresu URL w ostatnim kroku.</span><span class="sxs-lookup"><span data-stu-id="29614-136">You need the Key Vault ID, URI, and key URL in the final step.</span></span> <span data-ttu-id="29614-137">Poniższy przykład przegląda szczegóły dla usługi Key Vault o nazwie `myKeyVault` i klucz o nazwie `myKey`:</span><span class="sxs-lookup"><span data-stu-id="29614-137">The following example reviews the details for a Key Vault named `myKeyVault` and key named `myKey`:</span></span>

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

<span data-ttu-id="29614-138">Szyfrowanie dysków następujące wprowadzania własne nazwy parametru w całym:</span><span class="sxs-lookup"><span data-stu-id="29614-138">Encrypt your disks as follows, entering your own parameter names throughout:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

<span data-ttu-id="29614-139">Azure CLI nie zapewnia pełne błędy podczas procesu szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="29614-139">The Azure CLI doesn't provide verbose errors during the encryption process.</span></span> <span data-ttu-id="29614-140">Aby uzyskać dodatkowe informacje dotyczące rozwiązywania problemów, przejrzyj `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log`.</span><span class="sxs-lookup"><span data-stu-id="29614-140">For additional troubleshooting information, review `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log`.</span></span> <span data-ttu-id="29614-141">Poprzednie polecenie ma wiele zmiennych i nie może pobrać dużo wskazania przyczyny niepowodzenia procesu, przykład pełne polecenie będzie następujące:</span><span class="sxs-lookup"><span data-stu-id="29614-141">As the preceding command has many variables and you may not get much indication as to why the process fails, a complete command example would be as follows:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id 147bc426-595d-4bad-b267-58a7cbd8e0b6 \
  --aad-client-secret P@ssw0rd! \
  --disk-encryption-key-vault-url https://myKeyVault.vault.azure.net/ \
  --disk-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --key-encryption-key-url https://myKeyVault.vault.azure.net/keys/myKey/6f5fe9383f4e42d0a41553ebc6a82dd1 \
  --key-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResoureGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --volume-type Data
```

<span data-ttu-id="29614-142">Na koniec sprawdź stan szyfrowania ponownie, aby potwierdzić, że teraz został zaszyfrowany dysków wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="29614-142">Finally, review the encryption status again to confirm that your virtual disks have now been encrypted.</span></span> <span data-ttu-id="29614-143">Poniższy przykład umożliwia sprawdzenie stanu maszyny wirtualnej o nazwie `myVM` w `myResourceGroup` grupy zasobów:</span><span class="sxs-lookup"><span data-stu-id="29614-143">The following example checks the status of a VM named `myVM` in the `myResourceGroup` resource group:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="29614-144">Omówienie szyfrowania dysków</span><span class="sxs-lookup"><span data-stu-id="29614-144">Overview of disk encryption</span></span>
<span data-ttu-id="29614-145">Dyski wirtualne na maszynach wirtualnych systemu Linux są szyfrowane za pomocą rest [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span><span class="sxs-lookup"><span data-stu-id="29614-145">Virtual disks on Linux VMs are encrypted at rest using [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span></span> <span data-ttu-id="29614-146">Jest bezpłatna dla szyfrowania dysków wirtualnych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="29614-146">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="29614-147">Klucze szyfrowania są przechowywane w usługi Azure Key Vault przy użyciu ochrony oprogramowania, lub możesz zaimportować lub wygenerować klucze w sprzętowych modułach zabezpieczeń (HSM) certyfikowane do FIPS 140-2 poziom 2 standardów.</span><span class="sxs-lookup"><span data-stu-id="29614-147">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified to FIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="29614-148">Zachowanie kontroli nad tych kluczy kryptograficznych i przeprowadzić inspekcję ich używania.</span><span class="sxs-lookup"><span data-stu-id="29614-148">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="29614-149">Te klucze szyfrowania są używane do szyfrowania i odszyfrowywania wirtualnych dysków dołączonych do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="29614-149">These cryptographic keys are used to encrypt and decrypt virtual disks attached to your VM.</span></span> <span data-ttu-id="29614-150">Punkt końcowy usługi Azure Active Directory zapewnia mechanizm bezpiecznego do wystawiania tych kluczy kryptograficznych, ponieważ maszyny wirtualne są zasilane i wyłączanie.</span><span class="sxs-lookup"><span data-stu-id="29614-150">An Azure Active Directory endpoint provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="29614-151">Proces szyfrowania maszyny Wirtualnej jest następujący:</span><span class="sxs-lookup"><span data-stu-id="29614-151">The process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="29614-152">Tworzenie klucza kryptograficznego w usłudze Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="29614-152">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="29614-153">Skonfiguruj klucza kryptograficznego, który może być używany do szyfrowania dysków.</span><span class="sxs-lookup"><span data-stu-id="29614-153">Configure the cryptographic key to be usable for encrypting disks.</span></span>
3. <span data-ttu-id="29614-154">Aby odczytać klucza kryptograficznego z usługi Azure Key Vault, utworzyć punktu końcowego za pomocą usługi Azure Active Directory z odpowiednimi uprawnieniami.</span><span class="sxs-lookup"><span data-stu-id="29614-154">To read the cryptographic key from the Azure Key Vault, create an endpoint using Azure Active Directory with the appropriate permissions.</span></span>
4. <span data-ttu-id="29614-155">Wydaj polecenie dyski wirtualne, określenie punktu końcowego usługi Azure Active Directory i odpowiedniego klucza kryptograficznego używanego do szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="29614-155">Issue the command to encrypt your virtual disks, specifying the Azure Active Directory endpoint and appropriate cryptographic key to be used.</span></span>
5. <span data-ttu-id="29614-156">Punkt końcowy usługi Azure Active Directory żądań wymaganego klucza kryptograficznego z usługi Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="29614-156">The Azure Active Directory endpoint requests the required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="29614-157">Dyski wirtualne są szyfrowane za pomocą podanego klucza kryptograficznego.</span><span class="sxs-lookup"><span data-stu-id="29614-157">The virtual disks are encrypted using the provided cryptographic key.</span></span>

## <a name="supporting-services-and-encryption-process"></a><span data-ttu-id="29614-158">Obsługa usług i proces szyfrowania</span><span class="sxs-lookup"><span data-stu-id="29614-158">Supporting services and encryption process</span></span>
<span data-ttu-id="29614-159">Szyfrowanie dysków opiera się na następujące dodatkowe składniki:</span><span class="sxs-lookup"><span data-stu-id="29614-159">Disk encryption relies on the following additional components:</span></span>

* <span data-ttu-id="29614-160">**Usługa Azure Key Vault** — używane do ochrony kluczy kryptograficznych i kluczy tajnych używanych przez proces szyfrowania i odszyfrowywania dysku.</span><span class="sxs-lookup"><span data-stu-id="29614-160">**Azure Key Vault** - used to safeguard cryptographic keys and secrets used for the disk encryption/decryption process.</span></span>
  * <span data-ttu-id="29614-161">Jeśli istnieje, można użyć istniejącego magazynu kluczy Azure.</span><span class="sxs-lookup"><span data-stu-id="29614-161">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="29614-162">Nie trzeba przeznaczyć magazyn kluczy szyfrowania dysków.</span><span class="sxs-lookup"><span data-stu-id="29614-162">You do not have to dedicate a Key Vault to encrypting disks.</span></span>
  * <span data-ttu-id="29614-163">Aby rozdzielić granice administracyjne i widoczności klucza, możesz utworzyć dedykowany magazyn kluczy.</span><span class="sxs-lookup"><span data-stu-id="29614-163">To separate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="29614-164">**Usługa Azure Active Directory** — obsługuje bezpiecznej wymiany wymagane klucze szyfrowania i uwierzytelniania dla żądanej akcji.</span><span class="sxs-lookup"><span data-stu-id="29614-164">**Azure Active Directory** - handles the secure exchanging of required cryptographic keys and authentication for requested actions.</span></span>
  * <span data-ttu-id="29614-165">Zazwyczaj można użyć istniejącego wystąpienia usługi Azure Active Directory, do przechowywania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="29614-165">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="29614-166">Aplikacja jest jeden punkt końcowy usługi Magazyn kluczy i maszyny wirtualnej do żądania i pobrać wystawiony odpowiednich kluczy kryptograficznych.</span><span class="sxs-lookup"><span data-stu-id="29614-166">The application is more of an endpoint for the Key Vault and Virtual Machine services to request and get issued the appropriate cryptographic keys.</span></span> <span data-ttu-id="29614-167">Nie opracowujesz aplikację rzeczywista, która integruje się z usługą Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="29614-167">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="29614-168">Wymagania i ograniczenia</span><span class="sxs-lookup"><span data-stu-id="29614-168">Requirements and limitations</span></span>
<span data-ttu-id="29614-169">Obsługiwane scenariusze i wymagania dotyczące szyfrowania dysków:</span><span class="sxs-lookup"><span data-stu-id="29614-169">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="29614-170">Następujący serwer z systemem Linux jednostki SKU - Ubuntu, CentOS, SUSE i SUSE Linux Enterprise Server (SLES) i Red Hat Enterprise Linux.</span><span class="sxs-lookup"><span data-stu-id="29614-170">The following Linux server SKUs - Ubuntu, CentOS, SUSE and SUSE Linux Enterprise Server (SLES), and Red Hat Enterprise Linux.</span></span>
* <span data-ttu-id="29614-171">Wszystkie zasoby (na przykład usługi Key Vault, konta magazynu i maszyny Wirtualnej) muszą być w tym samym regionie Azure i subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="29614-171">All resources (such as Key Vault, Storage account, and VM) must be in the same Azure region and subscription.</span></span>
* <span data-ttu-id="29614-172">Standardowa A, D DS, G i GS seria maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="29614-172">Standard A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="29614-173">Szyfrowanie dysku nie jest obecnie obsługiwane w następujących scenariuszach:</span><span class="sxs-lookup"><span data-stu-id="29614-173">Disk encryption is not currently supported in the following scenarios:</span></span>

* <span data-ttu-id="29614-174">Maszyny wirtualne warstwy podstawowa.</span><span class="sxs-lookup"><span data-stu-id="29614-174">Basic tier VMs.</span></span>
* <span data-ttu-id="29614-175">Maszyny wirtualne utworzone przy użyciu klasycznego modelu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="29614-175">VMs created using the Classic deployment model.</span></span>
* <span data-ttu-id="29614-176">Wyłączenie szyfrowania dysku systemu operacyjnego na maszynach wirtualnych systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="29614-176">Disabling OS disk encryption on Linux VMs.</span></span>
* <span data-ttu-id="29614-177">Aktualizowanie kluczy kryptograficznych w już zaszyfrowany maszyny Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="29614-177">Updating the cryptographic keys on an already encrypted Linux VM.</span></span>

## <a name="create-the-azure-key-vault-and-keys"></a><span data-ttu-id="29614-178">Tworzenie usługi Azure Key Vault i kluczy</span><span class="sxs-lookup"><span data-stu-id="29614-178">Create the Azure Key Vault and keys</span></span>
<span data-ttu-id="29614-179">Aby zakończyć w dalszej części tego podręcznika, należy [najnowsze Azure CLI 1.0](../../xplat-cli-install.md) zainstalowane i zarejestrowane w trybie Menedżera zasobów w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="29614-179">To complete the remainder of this guide, you need the [latest Azure CLI 1.0](../../xplat-cli-install.md) installed and logged in using the Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="29614-180">W przykładach poleceń Zastąp wszystkie parametry przykład własne nazwy, lokalizacji i wartości klucza.</span><span class="sxs-lookup"><span data-stu-id="29614-180">Throughout the command examples, replace all example parameters with your own names, location, and key values.</span></span> <span data-ttu-id="29614-181">W poniższych przykładach użyto Konwencji `myResourceGroup`, `myKeyVault`, `myAADApp`itp.</span><span class="sxs-lookup"><span data-stu-id="29614-181">The following examples use a convention of `myResourceGroup`, `myKeyVault`, `myAADApp`, etc.</span></span>

<span data-ttu-id="29614-182">Pierwszym krokiem jest do utworzenia magazynu kluczy Azure do przechowywania kluczy kryptograficznych.</span><span class="sxs-lookup"><span data-stu-id="29614-182">The first step is to create an Azure Key Vault to store your cryptographic keys.</span></span> <span data-ttu-id="29614-183">Usługa Azure Key Vault można przechowywać kluczy, kluczy tajnych lub haseł, które umożliwiają bezpieczne wdrożenie ich w aplikacji i usług.</span><span class="sxs-lookup"><span data-stu-id="29614-183">Azure Key Vault can store keys, secrets, or passwords that allow you to securely implement them in your applications and services.</span></span> <span data-ttu-id="29614-184">Szyfrowanie dysków wirtualnych Key Vault służy do przechowywania klucza kryptograficznego używanego do szyfrowania lub odszyfrowywania dysków wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="29614-184">For virtual disk encryption, you use Key Vault to store a cryptographic key that is used to encrypt or decrypt your virtual disks.</span></span>

<span data-ttu-id="29614-185">Włącz dostawcy usługi Azure Key Vault w Twojej subskrypcji platformy Azure, a następnie utwórz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="29614-185">Enable the Azure Key Vault provider in your Azure subscription, then create a resource group.</span></span> <span data-ttu-id="29614-186">Poniższy przykład tworzy grupę zasobów o nazwie `myResourceGroup` w `WestUS` lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="29614-186">The following example creates a resource group named `myResourceGroup` in the `WestUS` location:</span></span>

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

<span data-ttu-id="29614-187">Usługa Azure Key Vault zawierający klucze kryptograficzne i zasoby obliczeniowe skojarzone, takie jak magazyn i samej maszyny Wirtualnej musi znajdować się w tym samym regionie.</span><span class="sxs-lookup"><span data-stu-id="29614-187">The Azure Key Vault containing the cryptographic keys and associated compute resources such as storage and the VM itself must reside in the same region.</span></span> <span data-ttu-id="29614-188">Poniższy przykład tworzy magazynu kluczy Azure o nazwie `myKeyVault`:</span><span class="sxs-lookup"><span data-stu-id="29614-188">The following example creates an Azure Key Vault named `myKeyVault`:</span></span>

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

<span data-ttu-id="29614-189">Mogą być przechowywane przy użyciu oprogramowania lub sprzętu modelu zabezpieczeń (HSM) ochronę kluczy kryptograficznych.</span><span class="sxs-lookup"><span data-stu-id="29614-189">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="29614-190">Użycie modułów HSM wymaga premium magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="29614-190">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="29614-191">Brak dodatkowych kosztów tworzenia premium magazynu kluczy, a nie standardowy magazyn kluczy, którego przechowuje klucze chronione przez oprogramowanie.</span><span class="sxs-lookup"><span data-stu-id="29614-191">There is an additional cost to creating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="29614-192">Aby utworzyć premium magazynu kluczy, w poprzednim kroku Dodaj `--sku Premium` do polecenia.</span><span class="sxs-lookup"><span data-stu-id="29614-192">To create a premium Key Vault, in the preceding step add `--sku Premium` to the command.</span></span> <span data-ttu-id="29614-193">W poniższym przykładzie użyto klucze chronione przez oprogramowanie, ponieważ utworzono standardowe magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="29614-193">The following example uses software-protected keys since we created a standard Key Vault.</span></span>

<span data-ttu-id="29614-194">W przypadku obu modeli ochrony platformy Azure musi otrzymać dostęp do żądania kluczy kryptograficznych, podczas rozruchu maszyny Wirtualnej do odszyfrowania dysków wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="29614-194">For both protection models, the Azure platform needs to be granted access to request the cryptographic keys when the VM boots to decrypt the virtual disks.</span></span> <span data-ttu-id="29614-195">Tworzenie klucza szyfrowania w ramach magazyn kluczy, a następnie włącz go do użytku z szyfrowania dysku wirtualnego.</span><span class="sxs-lookup"><span data-stu-id="29614-195">Create an encryption key within your Key Vault, then enable it for use with virtual disk encryption.</span></span> <span data-ttu-id="29614-196">W poniższym przykładzie jest tworzony klucz o nazwie `myKey` i umożliwia szyfrowanie dysków:</span><span class="sxs-lookup"><span data-stu-id="29614-196">The following example creates a key named `myKey` and then enables it for disk encryption:</span></span>

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```


## <a name="create-the-azure-active-directory-application"></a><span data-ttu-id="29614-197">Utwórz aplikację usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="29614-197">Create the Azure Active Directory application</span></span>
<span data-ttu-id="29614-198">Gdy dyski wirtualne są szyfrowane lub odszyfrować, służy do obsługi uwierzytelniania i wymiany kluczy kryptograficznych z usługi Key Vault punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="29614-198">When virtual disks are encrypted or decrypted, you use an endpoint to handle the authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="29614-199">Ten punkt końcowy, aplikację usługi Azure Active Directory umożliwia platformy Azure zażądać odpowiednich kluczy kryptograficznych w imieniu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="29614-199">This endpoint, an Azure Active Directory application, allows the Azure platform to request the appropriate cryptographic keys on behalf of the VM.</span></span> <span data-ttu-id="29614-200">Domyślne wystąpienie usługi Azure Active Directory jest dostępne w Twojej subskrypcji, chociaż w wielu organizacjach są wyposażone w dedykowane katalogów usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="29614-200">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="29614-201">Jak Pełna aplikacji usługi Azure Active Directory, nie są tworzone `--home-page` i `--identifier-uris` parametrów w poniższym przykładzie musi być rzeczywiste adresów obsługi routingu.</span><span class="sxs-lookup"><span data-stu-id="29614-201">As you are not creating a full Azure Active Directory application, the `--home-page` and `--identifier-uris` parameters in the following example do not need to be actual routable address.</span></span> <span data-ttu-id="29614-202">W poniższym przykładzie określa również klucz tajny opartego na hasłach zamiast generowania kluczy z w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="29614-202">The following example also specifies a password-based secret rather than generating keys from within the Azure portal.</span></span> <span data-ttu-id="29614-203">Teraz Generowanie kluczy nie można wykonać z wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="29614-203">As this time, generating keys cannot be done from the Azure CLI.</span></span>

<span data-ttu-id="29614-204">Tworzenie aplikacji usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="29614-204">Create your Azure Active Directory application.</span></span> <span data-ttu-id="29614-205">Poniższy przykład tworzy aplikację o nazwie `myAADApp` i używa hasła `myPassword`.</span><span class="sxs-lookup"><span data-stu-id="29614-205">The following example creates an application named `myAADApp` and uses a password of `myPassword`.</span></span> <span data-ttu-id="29614-206">Określ własnego hasła w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="29614-206">Specify your own password as follows:</span></span>

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

<span data-ttu-id="29614-207">Zanotuj `applicationId` który jest zwracany w danych wyjściowych z poprzedniego polecenia.</span><span class="sxs-lookup"><span data-stu-id="29614-207">Make a note of the `applicationId` that is returned in the output from the preceding command.</span></span> <span data-ttu-id="29614-208">Ten identyfikator aplikacji jest używany w niektórych z pozostałych kroków.</span><span class="sxs-lookup"><span data-stu-id="29614-208">This application ID is used in some of the remaining steps.</span></span> <span data-ttu-id="29614-209">Następnie należy utworzyć główną nazwę usługi (SPN), aby aplikacja jest dostępna w danym środowisku.</span><span class="sxs-lookup"><span data-stu-id="29614-209">Next, create a service principal name (SPN) so that the application is accessible within your environment.</span></span> <span data-ttu-id="29614-210">Pomyślnie szyfrowania lub odszyfrowywania dysków wirtualnych, uprawnienia do klucza kryptograficznego, przechowywane w magazynie kluczy należy wybrać opcję zezwalania na stosowanie usługi Azure Active Directory do odczytu klucze.</span><span class="sxs-lookup"><span data-stu-id="29614-210">To successfully encrypt or decrypt virtual disks, permissions on the cryptographic key stored in Key Vault must be set to permit the Azure Active Directory application to read the keys.</span></span>

<span data-ttu-id="29614-211">Utwórz nazwę SPN i ustawić odpowiednie uprawnienia w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="29614-211">Create the SPN and set the appropriate permissions as follows:</span></span>

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```


## <a name="add-a-virtual-disk-and-review-encryption-status"></a><span data-ttu-id="29614-212">Dodaj dysk wirtualny i sprawdzać stan szyfrowania</span><span class="sxs-lookup"><span data-stu-id="29614-212">Add a virtual disk and review encryption status</span></span>
<span data-ttu-id="29614-213">Do szyfrowania faktycznie niektóre dyski wirtualne, pozwala dodać dysk do istniejącej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="29614-213">To actually encrypt some virtual disks, lets add a disk to an existing VM.</span></span> <span data-ttu-id="29614-214">Dodaj dysk danych 5Gb do istniejącej maszyny Wirtualnej w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="29614-214">Add a 5Gb data disk to an existing VM as follows:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="29614-215">Dyski wirtualne nie są obecnie szyfrowane.</span><span class="sxs-lookup"><span data-stu-id="29614-215">The virtual disks are not currently encrypted.</span></span> <span data-ttu-id="29614-216">Sprawdź bieżący stan szyfrowania maszyny wirtualnej w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="29614-216">Review the current encryption status of your VM as follows:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="encrypt-virtual-disks"></a><span data-ttu-id="29614-217">Szyfrowanie dysków wirtualnych</span><span class="sxs-lookup"><span data-stu-id="29614-217">Encrypt virtual disks</span></span>
<span data-ttu-id="29614-218">Teraz szyfrowania dysków wirtualnych, można przenosić ze sobą wszystkie poprzednie składniki:</span><span class="sxs-lookup"><span data-stu-id="29614-218">To now encrypt the virtual disks, you bring together all the previous components:</span></span>

1. <span data-ttu-id="29614-219">Określ aplikację usługi Azure Active Directory i hasło.</span><span class="sxs-lookup"><span data-stu-id="29614-219">Specify the Azure Active Directory application and password.</span></span>
2. <span data-ttu-id="29614-220">Określ Key Vault w celu przechowywania metadanych dla zaszyfrowanych dysków.</span><span class="sxs-lookup"><span data-stu-id="29614-220">Specify the Key Vault to store the metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="29614-221">Określ klucze kryptograficzne służące do rzeczywistego szyfrowania i odszyfrowywania.</span><span class="sxs-lookup"><span data-stu-id="29614-221">Specify the cryptographic keys to use for the actual encryption and decryption.</span></span>
4. <span data-ttu-id="29614-222">Określ, czy chcesz zaszyfrować dysk systemu operacyjnego, dyski danych lub all.</span><span class="sxs-lookup"><span data-stu-id="29614-222">Specify whether you want to encrypt the OS disk, the data disks, or all.</span></span>

<span data-ttu-id="29614-223">Pozwala, przejrzyj szczegóły magazyn kluczy Azure i klawisz, który został utworzony, potrzebny jest identyfikator magazynu kluczy, identyfikator URI, a następnie klucza adresu URL w ostatnim kroku:</span><span class="sxs-lookup"><span data-stu-id="29614-223">Lets review the details for your Azure Key Vault and the key you created, as you need the Key Vault ID, URI, and then key URL in the final step:</span></span>

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

<span data-ttu-id="29614-224">Szyfrowanie dysków wirtualnych przy użyciu dane wyjściowe z `azure keyvault show` i `azure keyvault key show` polecenia w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="29614-224">Encrypt your virtual disks using the output from the `azure keyvault show` and `azure keyvault key show` commands as follows:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

<span data-ttu-id="29614-225">Poprzednie polecenie zawiera wiele zmiennych, poniższy przykład jest pełne polecenie odwołania:</span><span class="sxs-lookup"><span data-stu-id="29614-225">As the preceding command has many variables, the following example is the complete command for reference:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id 147bc426-595d-4bad-b267-58a7cbd8e0b6 \
  --aad-client-secret P@ssw0rd! \
  --disk-encryption-key-vault-url https://myKeyVault.vault.azure.net/ \
  --disk-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --key-encryption-key-url https://myKeyVault.vault.azure.net/keys/myKey/6f5fe9383f4e42d0a41553ebc6a82dd1 \
  --key-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResoureGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --volume-type Data
```

<span data-ttu-id="29614-226">Azure CLI nie zapewnia pełne błędy podczas procesu szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="29614-226">The Azure CLI doesn't provide verbose errors during the encryption process.</span></span> <span data-ttu-id="29614-227">Aby uzyskać dodatkowe informacje dotyczące rozwiązywania problemów, przejrzyj `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log` na Maszynie wirtualnej jest szyfrowany.</span><span class="sxs-lookup"><span data-stu-id="29614-227">For additional troubleshooting information, review `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log` on the VM you are encrypting.</span></span>

<span data-ttu-id="29614-228">Na koniec pozwala sprawdzać stan szyfrowania ponownie, aby potwierdzić, że teraz zostały zaszyfrowane dyski wirtualne:</span><span class="sxs-lookup"><span data-stu-id="29614-228">Finally, lets review the encryption status again to confirm that your virtual disks have now been encrypted:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="add-additional-data-disks"></a><span data-ttu-id="29614-229">Dodania dodatkowego dysku z danymi</span><span class="sxs-lookup"><span data-stu-id="29614-229">Add additional data disks</span></span>
<span data-ttu-id="29614-230">Po zaszyfrowanych dysków z danymi, możesz później dodać dodatkowych dysków wirtualnych do maszyny Wirtualnej i również ich szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="29614-230">Once you have encrypted your data disks, you can later add additional virtual disks to your VM and also encrypt them.</span></span> <span data-ttu-id="29614-231">Po uruchomieniu `azure vm enable-disk-encryption` polecenia, zwiększyć przy użyciu wersji sekwencji `--sequence-version` parametru.</span><span class="sxs-lookup"><span data-stu-id="29614-231">When you run the `azure vm enable-disk-encryption` command, increment the sequence version using the `--sequence-version` parameter.</span></span> <span data-ttu-id="29614-232">Ten parametr wersji sekwencji umożliwia wykonywanie operacji powtarzane na tej samej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="29614-232">This sequence version parameter allows you to perform repeated operations on the same VM.</span></span>

<span data-ttu-id="29614-233">Na przykład pozwala dodać drugi wirtualny dysk do maszyny Wirtualnej w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="29614-233">For example, lets add a second virtual disk to your VM as follows:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="29614-234">Ponownie uruchom polecenie do szyfrowania dysków wirtualnych, dodawanie tego czasu `--sequence-version` parametr i zwiększając wartość z naszym pierwszym uruchomieniu w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="29614-234">Rerun the command to encrypt the virtual disks, this time adding the `--sequence-version` parameter, and incrementing the value from our first run as follows:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
  --sequence-version 2
```


## <a name="next-steps"></a><span data-ttu-id="29614-235">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="29614-235">Next steps</span></span>
* <span data-ttu-id="29614-236">Aby uzyskać więcej informacji na temat zarządzania usługą Azure Key Vault, łącznie z usunięciem kluczy kryptograficznych i magazyny, zobacz [Zarządzanie Key Vault przy użyciu interfejsu wiersza polecenia](../../key-vault/key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="29614-236">For more information about managing Azure Key Vault, including deleting cryptographic keys and vaults, see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md).</span></span>
* <span data-ttu-id="29614-237">Aby uzyskać więcej informacji o szyfrowaniu dysków, takich jak przygotowywanie zaszyfrowanego niestandardowego maszyny Wirtualnej do przekazania do platformy Azure, zobacz [szyfrowania dysków Azure](../../security/azure-security-disk-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="29614-237">For more information about disk encryption, such as preparing an encrypted custom VM to upload to Azure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
