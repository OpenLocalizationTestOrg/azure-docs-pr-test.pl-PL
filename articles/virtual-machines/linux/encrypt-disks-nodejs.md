---
title: "aaaEncrypt dysków na Maszynę wirtualną systemu Linux z hello Azure CLI 1.0 | Dokumentacja firmy Microsoft"
description: "Jak tooencrypt dysków na Maszynę wirtualną systemu Linux przy użyciu hello Azure CLI 1.0 i modelu wdrażania usługi Resource Manager hello"
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
ms.openlocfilehash: 68a0394d366c3c6941e2c6db0d4263123f951946
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-disks-on-a-linux-vm-using-hello-azure-cli-10"></a><span data-ttu-id="71f4a-103">Szyfrowanie dysków na Maszynę wirtualną systemu Linux przy użyciu hello Azure CLI w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="71f4a-103">Encrypt disks on a Linux VM using hello Azure CLI 1.0</span></span>
<span data-ttu-id="71f4a-104">Ulepszone maszyny wirtualnej (VM) zabezpieczeń i zgodności dyski wirtualne na platformie Azure mogą być szyfrowane w stanie spoczynku.</span><span class="sxs-lookup"><span data-stu-id="71f4a-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted at rest.</span></span> <span data-ttu-id="71f4a-105">Dyski są szyfrowane za pomocą kluczy kryptograficznych, które są już zabezpieczone w usłudze Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="71f4a-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="71f4a-106">Kontrolowanie tych kluczy kryptograficznych i przeprowadzić inspekcję ich używania.</span><span class="sxs-lookup"><span data-stu-id="71f4a-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="71f4a-107">W tym artykule szczegółowo sposób tooencrypt dysków wirtualnych na Maszynę wirtualną systemu Linux przy użyciu hello Azure CLI 1.0 i modelu wdrażania usługi Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="71f4a-107">This article details how tooencrypt virtual disks on a Linux VM using hello Azure CLI 1.0 and hello Resource Manager deployment model.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="71f4a-108">Zadanie hello toocomplete wersje interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="71f4a-108">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="71f4a-109">Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="71f4a-109">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="71f4a-110">[Azure CLI 1.0](#quick-commands) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania wdrażania modeli (w tym artykule)</span><span class="sxs-lookup"><span data-stu-id="71f4a-110">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="71f4a-111">[Azure CLI 2.0](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello</span><span class="sxs-lookup"><span data-stu-id="71f4a-111">[Azure CLI 2.0](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="quick-commands"></a><span data-ttu-id="71f4a-112">Szybkie polecenia</span><span class="sxs-lookup"><span data-stu-id="71f4a-112">Quick commands</span></span>
<span data-ttu-id="71f4a-113">Jeśli potrzebujesz tooquickly hello zadania, powitania po sekcji Szczegóły hello podstawowej polecenia tooencrypt dyski wirtualne na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="71f4a-113">If you need tooquickly accomplish hello task, hello following section details hello base commands tooencrypt virtual disks on your VM.</span></span> <span data-ttu-id="71f4a-114">Bardziej szczegółowe informacje i kontekst dla każdego kroku można znaleźć hello pozostałej części dokumentu hello [uruchamiania tutaj](#overview-of-disk-encryption).</span><span class="sxs-lookup"><span data-stu-id="71f4a-114">More detailed information and context for each step can be found hello rest of hello document, [starting here](#overview-of-disk-encryption).</span></span>

<span data-ttu-id="71f4a-115">Należy hello [najnowsze Azure CLI 1.0](../../xplat-cli-install.md) zainstalowane i rejestrowane w trybie hello Resource Manager w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="71f4a-115">You need hello [latest Azure CLI 1.0](../../xplat-cli-install.md) installed and logged in using hello Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="71f4a-116">Poniższe przykłady w hello Zastąp przykładowe nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="71f4a-116">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="71f4a-117">Przykład nazwy parametru zawierają `myResourceGroup`, `myKeyVault`, i `myVM`.</span><span class="sxs-lookup"><span data-stu-id="71f4a-117">Example parameter names include `myResourceGroup`, `myKeyVault`, and `myVM`.</span></span>

<span data-ttu-id="71f4a-118">Najpierw należy włączyć hello dostawcy usługi Azure Key Vault w ramach Twojej subskrypcji platformy Azure i Utwórz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="71f4a-118">First, enable hello Azure Key Vault provider within your Azure subscription and create a resource group.</span></span> <span data-ttu-id="71f4a-119">Witaj poniższy przykład tworzy nazwę grupy zasobów `myResourceGroup` w hello `WestUS` lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="71f4a-119">hello following example creates a resource group name `myResourceGroup` in hello `WestUS` location:</span></span>

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

<span data-ttu-id="71f4a-120">Tworzenie usługi Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="71f4a-120">Create an Azure Key Vault.</span></span> <span data-ttu-id="71f4a-121">Witaj poniższy przykład tworzy magazyn kluczy o nazwie `myKeyVault`:</span><span class="sxs-lookup"><span data-stu-id="71f4a-121">hello following example creates a Key Vault named `myKeyVault`:</span></span>

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

<span data-ttu-id="71f4a-122">Tworzenie klucza kryptograficznego w magazyn kluczy i Włącz szyfrowanie dysków.</span><span class="sxs-lookup"><span data-stu-id="71f4a-122">Create a cryptographic key in your Key Vault and enable it for disk encryption.</span></span> <span data-ttu-id="71f4a-123">Witaj poniższym przykładzie jest tworzony klucz o nazwie `myKey`:</span><span class="sxs-lookup"><span data-stu-id="71f4a-123">hello following example creates a key named `myKey`:</span></span>

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```

<span data-ttu-id="71f4a-124">Tworzenie punktu końcowego za pomocą usługi Azure Active Directory do obsługi uwierzytelniania hello i wymiana kluczy kryptograficznych z magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="71f4a-124">Create an endpoint using Azure Active Directory for handling hello authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="71f4a-125">Witaj `--home-page` i `--identifier-uris` nie ma potrzeby toobe rzeczywiste adresów obsługi routingu.</span><span class="sxs-lookup"><span data-stu-id="71f4a-125">hello `--home-page` and `--identifier-uris` do not need toobe actual routable address.</span></span> <span data-ttu-id="71f4a-126">W przypadku hello najwyższy poziom zabezpieczeń kluczy tajnych klientów należy użyć zamiast hasła.</span><span class="sxs-lookup"><span data-stu-id="71f4a-126">For hello highest level of security, client secrets should be used instead of passwords.</span></span> <span data-ttu-id="71f4a-127">Witaj interfejsu wiersza polecenia Azure aktualnie nie można wygenerować kluczy tajnych klientów.</span><span class="sxs-lookup"><span data-stu-id="71f4a-127">hello Azure CLI cannot currently generate client secrets.</span></span> <span data-ttu-id="71f4a-128">Kluczy tajnych klientów mogą być generowane tylko w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="71f4a-128">Client secrets can only be generated in hello Azure portal.</span></span> <span data-ttu-id="71f4a-129">Witaj poniższy przykład tworzy punkt końcowy usługi Azure Active Directory o nazwie `myAADApp` i używa hasła `myPassword`.</span><span class="sxs-lookup"><span data-stu-id="71f4a-129">hello following example creates an Azure Active Directory endpoint named `myAADApp` and uses a password of `myPassword`.</span></span> <span data-ttu-id="71f4a-130">Określ własnego hasła w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="71f4a-130">Specify your own password as follows:</span></span>

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

<span data-ttu-id="71f4a-131">Uwaga hello `applicationId` wyświetlany w danych wyjściowych hello z hello poprzedzających polecenia.</span><span class="sxs-lookup"><span data-stu-id="71f4a-131">Note hello `applicationId` shown in hello output from hello preceding command.</span></span> <span data-ttu-id="71f4a-132">Ten identyfikator aplikacji jest używany w hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="71f4a-132">This application ID is used in hello following steps:</span></span>

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```

<span data-ttu-id="71f4a-133">Dodawanie danych tooan dysku, istniejącej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="71f4a-133">Add a data disk tooan existing VM.</span></span> <span data-ttu-id="71f4a-134">Witaj poniższy przykład umożliwia dodanie tooa dysku danych maszyny Wirtualnej o nazwie `myVM`:</span><span class="sxs-lookup"><span data-stu-id="71f4a-134">hello following example adds a data disk tooa VM named `myVM`:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="71f4a-135">Przejrzyj szczegóły hello klucza magazynu kluczy i hello utworzony.</span><span class="sxs-lookup"><span data-stu-id="71f4a-135">Review hello details for your Key Vault and hello key you created.</span></span> <span data-ttu-id="71f4a-136">Należy hello identyfikator magazynu kluczy, identyfikator URI i klucz adres URL w ostatnim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="71f4a-136">You need hello Key Vault ID, URI, and key URL in hello final step.</span></span> <span data-ttu-id="71f4a-137">Witaj poniższy przykład przegląda hello szczegółów dla usługi Key Vault o nazwie `myKeyVault` i klucz o nazwie `myKey`:</span><span class="sxs-lookup"><span data-stu-id="71f4a-137">hello following example reviews hello details for a Key Vault named `myKeyVault` and key named `myKey`:</span></span>

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

<span data-ttu-id="71f4a-138">Szyfrowanie dysków następujące wprowadzania własne nazwy parametru w całym:</span><span class="sxs-lookup"><span data-stu-id="71f4a-138">Encrypt your disks as follows, entering your own parameter names throughout:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

<span data-ttu-id="71f4a-139">Hello Azure CLI nie zapewnia pełne błędy podczas procesu szyfrowania hello.</span><span class="sxs-lookup"><span data-stu-id="71f4a-139">hello Azure CLI doesn't provide verbose errors during hello encryption process.</span></span> <span data-ttu-id="71f4a-140">Aby uzyskać dodatkowe informacje dotyczące rozwiązywania problemów, przejrzyj `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log`.</span><span class="sxs-lookup"><span data-stu-id="71f4a-140">For additional troubleshooting information, review `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log`.</span></span> <span data-ttu-id="71f4a-141">Jako hello poprzedzających polecenie ma wiele zmiennych i nie może pobrać dużo oznaczenie toowhy hello proces zakończy się niepowodzeniem, przykład pełne polecenie będzie następujące:</span><span class="sxs-lookup"><span data-stu-id="71f4a-141">As hello preceding command has many variables and you may not get much indication as toowhy hello process fails, a complete command example would be as follows:</span></span>

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

<span data-ttu-id="71f4a-142">Na koniec, sprawdź stan szyfrowania hello ponownie tooconfirm czy dyski wirtualne teraz zostały zaszyfrowane.</span><span class="sxs-lookup"><span data-stu-id="71f4a-142">Finally, review hello encryption status again tooconfirm that your virtual disks have now been encrypted.</span></span> <span data-ttu-id="71f4a-143">Witaj poniższy przykład umożliwia sprawdzenie hello stanu maszyny wirtualnej o nazwie `myVM` w hello `myResourceGroup` grupy zasobów:</span><span class="sxs-lookup"><span data-stu-id="71f4a-143">hello following example checks hello status of a VM named `myVM` in hello `myResourceGroup` resource group:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="71f4a-144">Omówienie szyfrowania dysków</span><span class="sxs-lookup"><span data-stu-id="71f4a-144">Overview of disk encryption</span></span>
<span data-ttu-id="71f4a-145">Dyski wirtualne na maszynach wirtualnych systemu Linux są szyfrowane za pomocą rest [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span><span class="sxs-lookup"><span data-stu-id="71f4a-145">Virtual disks on Linux VMs are encrypted at rest using [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span></span> <span data-ttu-id="71f4a-146">Jest bezpłatna dla szyfrowania dysków wirtualnych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="71f4a-146">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="71f4a-147">Klucze szyfrowania są przechowywane w usługi Azure Key Vault przy użyciu ochrony oprogramowania, lub możesz zaimportować lub wygenerować klucze w sprzętowych modułach zabezpieczeń (HSM) certyfikowane tooFIPS 140-2 poziom 2 standardów.</span><span class="sxs-lookup"><span data-stu-id="71f4a-147">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified tooFIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="71f4a-148">Zachowanie kontroli nad tych kluczy kryptograficznych i przeprowadzić inspekcję ich używania.</span><span class="sxs-lookup"><span data-stu-id="71f4a-148">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="71f4a-149">Te klucze szyfrowania są używane tooencrypt i odszyfrowywania tooyour dołączonych dysków wirtualnych maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="71f4a-149">These cryptographic keys are used tooencrypt and decrypt virtual disks attached tooyour VM.</span></span> <span data-ttu-id="71f4a-150">Punkt końcowy usługi Azure Active Directory zapewnia mechanizm bezpiecznego do wystawiania tych kluczy kryptograficznych, ponieważ maszyny wirtualne są zasilane i wyłączanie.</span><span class="sxs-lookup"><span data-stu-id="71f4a-150">An Azure Active Directory endpoint provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="71f4a-151">proces Hello szyfrowania maszyny Wirtualnej przebiega w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="71f4a-151">hello process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="71f4a-152">Tworzenie klucza kryptograficznego w usłudze Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="71f4a-152">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="71f4a-153">Skonfiguruj hello kryptograficznych klucza toobe można używać do szyfrowania dysków.</span><span class="sxs-lookup"><span data-stu-id="71f4a-153">Configure hello cryptographic key toobe usable for encrypting disks.</span></span>
3. <span data-ttu-id="71f4a-154">klucz kryptograficzny hello tooread z hello Azure Key Vault, tworzenie punktu końcowego za pomocą usługi Azure Active Directory z odpowiednimi uprawnieniami hello.</span><span class="sxs-lookup"><span data-stu-id="71f4a-154">tooread hello cryptographic key from hello Azure Key Vault, create an endpoint using Azure Active Directory with hello appropriate permissions.</span></span>
4. <span data-ttu-id="71f4a-155">Wystawiać tooencrypt polecenia hello wirtualnych dysków, określając punkt końcowy usługi Azure Active Directory hello i odpowiednie toobe klucza kryptograficznego używane.</span><span class="sxs-lookup"><span data-stu-id="71f4a-155">Issue hello command tooencrypt your virtual disks, specifying hello Azure Active Directory endpoint and appropriate cryptographic key toobe used.</span></span>
5. <span data-ttu-id="71f4a-156">punkt końcowy usługi Azure Active Directory Hello żądań hello wymaganego klucza kryptograficznego z usługi Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="71f4a-156">hello Azure Active Directory endpoint requests hello required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="71f4a-157">dyski wirtualne Hello są szyfrowane za pomocą klucza kryptograficznego hello podane.</span><span class="sxs-lookup"><span data-stu-id="71f4a-157">hello virtual disks are encrypted using hello provided cryptographic key.</span></span>

## <a name="supporting-services-and-encryption-process"></a><span data-ttu-id="71f4a-158">Obsługa usług i proces szyfrowania</span><span class="sxs-lookup"><span data-stu-id="71f4a-158">Supporting services and encryption process</span></span>
<span data-ttu-id="71f4a-159">Szyfrowanie dysków opiera się na powitania następujące dodatkowe składniki:</span><span class="sxs-lookup"><span data-stu-id="71f4a-159">Disk encryption relies on hello following additional components:</span></span>

* <span data-ttu-id="71f4a-160">**Usługa Azure Key Vault** — używane toosafeguard kluczy kryptograficznych i kluczy tajnych używane podczas procesu szyfrowania i odszyfrowywania dysku hello.</span><span class="sxs-lookup"><span data-stu-id="71f4a-160">**Azure Key Vault** - used toosafeguard cryptographic keys and secrets used for hello disk encryption/decryption process.</span></span>
  * <span data-ttu-id="71f4a-161">Jeśli istnieje, można użyć istniejącego magazynu kluczy Azure.</span><span class="sxs-lookup"><span data-stu-id="71f4a-161">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="71f4a-162">Nie masz toodedicate dysków tooencrypting magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="71f4a-162">You do not have toodedicate a Key Vault tooencrypting disks.</span></span>
  * <span data-ttu-id="71f4a-163">granice administracyjne tooseparate i widoczności klucza, można utworzyć dedykowane Key Vault.</span><span class="sxs-lookup"><span data-stu-id="71f4a-163">tooseparate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="71f4a-164">**Usługa Azure Active Directory** — Witaj uchwytów bezpiecznej wymiany kluczy kryptograficznych wymagane i uwierzytelniania dla żądanej akcji.</span><span class="sxs-lookup"><span data-stu-id="71f4a-164">**Azure Active Directory** - handles hello secure exchanging of required cryptographic keys and authentication for requested actions.</span></span>
  * <span data-ttu-id="71f4a-165">Zazwyczaj można użyć istniejącego wystąpienia usługi Azure Active Directory, do przechowywania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="71f4a-165">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="71f4a-166">Aplikacja Hello jest więcej punktu końcowego dla hello magazyn kluczy i maszyny wirtualnej usługi toorequest i pobrać wystawiony hello odpowiednich kluczy kryptograficznych.</span><span class="sxs-lookup"><span data-stu-id="71f4a-166">hello application is more of an endpoint for hello Key Vault and Virtual Machine services toorequest and get issued hello appropriate cryptographic keys.</span></span> <span data-ttu-id="71f4a-167">Nie opracowujesz aplikację rzeczywista, która integruje się z usługą Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="71f4a-167">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="71f4a-168">Wymagania i ograniczenia</span><span class="sxs-lookup"><span data-stu-id="71f4a-168">Requirements and limitations</span></span>
<span data-ttu-id="71f4a-169">Obsługiwane scenariusze i wymagania dotyczące szyfrowania dysków:</span><span class="sxs-lookup"><span data-stu-id="71f4a-169">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="71f4a-170">powitania po Linux server jednostki SKU - Ubuntu, CentOS, SUSE i SUSE Linux Enterprise Server (SLES) i Red Hat Enterprise Linux.</span><span class="sxs-lookup"><span data-stu-id="71f4a-170">hello following Linux server SKUs - Ubuntu, CentOS, SUSE and SUSE Linux Enterprise Server (SLES), and Red Hat Enterprise Linux.</span></span>
* <span data-ttu-id="71f4a-171">Wszystkie zasoby (na przykład usługi Key Vault, konta magazynu i maszyny Wirtualnej) musi być w hello tego samego regionu Azure i subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="71f4a-171">All resources (such as Key Vault, Storage account, and VM) must be in hello same Azure region and subscription.</span></span>
* <span data-ttu-id="71f4a-172">Standardowa A, D DS, G i GS seria maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="71f4a-172">Standard A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="71f4a-173">Szyfrowanie dysków nie jest obecnie obsługiwane w hello następujące scenariusze:</span><span class="sxs-lookup"><span data-stu-id="71f4a-173">Disk encryption is not currently supported in hello following scenarios:</span></span>

* <span data-ttu-id="71f4a-174">Maszyny wirtualne warstwy podstawowa.</span><span class="sxs-lookup"><span data-stu-id="71f4a-174">Basic tier VMs.</span></span>
* <span data-ttu-id="71f4a-175">Maszyny wirtualne utworzone za pomocą hello klasycznego modelu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="71f4a-175">VMs created using hello Classic deployment model.</span></span>
* <span data-ttu-id="71f4a-176">Wyłączenie szyfrowania dysku systemu operacyjnego na maszynach wirtualnych systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="71f4a-176">Disabling OS disk encryption on Linux VMs.</span></span>
* <span data-ttu-id="71f4a-177">Aktualizowanie kluczy kryptograficznych hello na już zaszyfrowany maszyny Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="71f4a-177">Updating hello cryptographic keys on an already encrypted Linux VM.</span></span>

## <a name="create-hello-azure-key-vault-and-keys"></a><span data-ttu-id="71f4a-178">Utwórz hello Azure Key Vault i kluczy</span><span class="sxs-lookup"><span data-stu-id="71f4a-178">Create hello Azure Key Vault and keys</span></span>
<span data-ttu-id="71f4a-179">toocomplete hello pozostałej części tego przewodnika, należy hello [najnowsze Azure CLI 1.0](../../xplat-cli-install.md) zainstalowane i rejestrowane w trybie hello Resource Manager w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="71f4a-179">toocomplete hello remainder of this guide, you need hello [latest Azure CLI 1.0](../../xplat-cli-install.md) installed and logged in using hello Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="71f4a-180">W przykładach poleceń hello Zamień wszystkie parametry przykład własne nazwy, lokalizacji i wartości klucza.</span><span class="sxs-lookup"><span data-stu-id="71f4a-180">Throughout hello command examples, replace all example parameters with your own names, location, and key values.</span></span> <span data-ttu-id="71f4a-181">Witaj następujących przykładach użyto Konwencji `myResourceGroup`, `myKeyVault`, `myAADApp`itp.</span><span class="sxs-lookup"><span data-stu-id="71f4a-181">hello following examples use a convention of `myResourceGroup`, `myKeyVault`, `myAADApp`, etc.</span></span>

<span data-ttu-id="71f4a-182">pierwszym krokiem Hello jest toocreate toostore usługi Azure Key Vault kluczy kryptograficznych.</span><span class="sxs-lookup"><span data-stu-id="71f4a-182">hello first step is toocreate an Azure Key Vault toostore your cryptographic keys.</span></span> <span data-ttu-id="71f4a-183">Usługa Azure Key Vault może przechowywać klucze i klucze tajne, lub haseł, które pozwalają toosecurely wdrożyć je w aplikacji i usług.</span><span class="sxs-lookup"><span data-stu-id="71f4a-183">Azure Key Vault can store keys, secrets, or passwords that allow you toosecurely implement them in your applications and services.</span></span> <span data-ttu-id="71f4a-184">Szyfrowanie dysków wirtualnych Użyj toostore Key Vault klucza kryptograficznego, który jest używany tooencrypt lub odszyfrować wirtualnych dysków.</span><span class="sxs-lookup"><span data-stu-id="71f4a-184">For virtual disk encryption, you use Key Vault toostore a cryptographic key that is used tooencrypt or decrypt your virtual disks.</span></span>

<span data-ttu-id="71f4a-185">Włącz hello dostawcy usługi Azure Key Vault w Twojej subskrypcji platformy Azure, a następnie utwórz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="71f4a-185">Enable hello Azure Key Vault provider in your Azure subscription, then create a resource group.</span></span> <span data-ttu-id="71f4a-186">Witaj poniższy przykład tworzy grupę zasobów o nazwie `myResourceGroup` w hello `WestUS` lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="71f4a-186">hello following example creates a resource group named `myResourceGroup` in hello `WestUS` location:</span></span>

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

<span data-ttu-id="71f4a-187">Hello Azure Key Vault zawierającego hello kluczy kryptograficznych i obliczeniowe skojarzone zasoby, takie jak magazyn i hello samej maszyny Wirtualnej musi znajdować się w hello tego samego regionu.</span><span class="sxs-lookup"><span data-stu-id="71f4a-187">hello Azure Key Vault containing hello cryptographic keys and associated compute resources such as storage and hello VM itself must reside in hello same region.</span></span> <span data-ttu-id="71f4a-188">Witaj poniższy przykład tworzy magazynu kluczy Azure o nazwie `myKeyVault`:</span><span class="sxs-lookup"><span data-stu-id="71f4a-188">hello following example creates an Azure Key Vault named `myKeyVault`:</span></span>

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

<span data-ttu-id="71f4a-189">Mogą być przechowywane przy użyciu oprogramowania lub sprzętu modelu zabezpieczeń (HSM) ochronę kluczy kryptograficznych.</span><span class="sxs-lookup"><span data-stu-id="71f4a-189">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="71f4a-190">Użycie modułów HSM wymaga premium magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="71f4a-190">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="71f4a-191">Brak dodatkowych kosztów toocreating premium magazynu kluczy, a nie standardowy magazyn kluczy, którego przechowuje klucze chronione przez oprogramowanie.</span><span class="sxs-lookup"><span data-stu-id="71f4a-191">There is an additional cost toocreating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="71f4a-192">Dodaj premium usługi Key Vault w hello poprzedzających krok toocreate `--sku Premium` toohello polecenia.</span><span class="sxs-lookup"><span data-stu-id="71f4a-192">toocreate a premium Key Vault, in hello preceding step add `--sku Premium` toohello command.</span></span> <span data-ttu-id="71f4a-193">Witaj poniższym przykładzie użyto klucze chronione oprogramowaniem ponieważ utworzyliśmy standardowy magazyn kluczy.</span><span class="sxs-lookup"><span data-stu-id="71f4a-193">hello following example uses software-protected keys since we created a standard Key Vault.</span></span>

<span data-ttu-id="71f4a-194">W przypadku obu modeli ochrony hello platformy Azure musi toobe udzielać dostępu do kluczy kryptograficznych hello toorequest, w przypadku, gdy hello maszyny Wirtualnej wykonuje rozruch toodecrypt hello wirtualnych dysków.</span><span class="sxs-lookup"><span data-stu-id="71f4a-194">For both protection models, hello Azure platform needs toobe granted access toorequest hello cryptographic keys when hello VM boots toodecrypt hello virtual disks.</span></span> <span data-ttu-id="71f4a-195">Tworzenie klucza szyfrowania w ramach magazyn kluczy, a następnie włącz go do użytku z szyfrowania dysku wirtualnego.</span><span class="sxs-lookup"><span data-stu-id="71f4a-195">Create an encryption key within your Key Vault, then enable it for use with virtual disk encryption.</span></span> <span data-ttu-id="71f4a-196">Witaj poniższym przykładzie jest tworzony klucz o nazwie `myKey` i umożliwia szyfrowanie dysków:</span><span class="sxs-lookup"><span data-stu-id="71f4a-196">hello following example creates a key named `myKey` and then enables it for disk encryption:</span></span>

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```


## <a name="create-hello-azure-active-directory-application"></a><span data-ttu-id="71f4a-197">Utwórz aplikację usługi Azure Active Directory hello</span><span class="sxs-lookup"><span data-stu-id="71f4a-197">Create hello Azure Active Directory application</span></span>
<span data-ttu-id="71f4a-198">Dyski wirtualne są szyfrowane lub odszyfrować, możesz korzystać z uwierzytelniania hello toohandle punktu końcowego i wymiana kluczy kryptograficznych z magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="71f4a-198">When virtual disks are encrypted or decrypted, you use an endpoint toohandle hello authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="71f4a-199">Ten punkt końcowy, aplikację usługi Azure Active Directory umożliwia toorequest platformy Azure hello hello odpowiednich kluczy kryptograficznych imieniu hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="71f4a-199">This endpoint, an Azure Active Directory application, allows hello Azure platform toorequest hello appropriate cryptographic keys on behalf of hello VM.</span></span> <span data-ttu-id="71f4a-200">Domyślne wystąpienie usługi Azure Active Directory jest dostępne w Twojej subskrypcji, chociaż w wielu organizacjach są wyposażone w dedykowane katalogów usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="71f4a-200">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="71f4a-201">Jak Pełna aplikacji usługi Azure Active Directory nie jest tworzony, hello `--home-page` i `--identifier-uris` parametry w poniższy przykład hello nie wymagają toobe rzeczywiste adresów obsługi routingu.</span><span class="sxs-lookup"><span data-stu-id="71f4a-201">As you are not creating a full Azure Active Directory application, hello `--home-page` and `--identifier-uris` parameters in hello following example do not need toobe actual routable address.</span></span> <span data-ttu-id="71f4a-202">Witaj poniższy przykład również określa klucz tajny opartego na hasłach zamiast generowania kluczy z wewnątrz hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="71f4a-202">hello following example also specifies a password-based secret rather than generating keys from within hello Azure portal.</span></span> <span data-ttu-id="71f4a-203">Teraz Generowanie kluczy nie można wykonać z hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="71f4a-203">As this time, generating keys cannot be done from hello Azure CLI.</span></span>

<span data-ttu-id="71f4a-204">Tworzenie aplikacji usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="71f4a-204">Create your Azure Active Directory application.</span></span> <span data-ttu-id="71f4a-205">Witaj poniższy przykład tworzy aplikację o nazwie `myAADApp` i używa hasła `myPassword`.</span><span class="sxs-lookup"><span data-stu-id="71f4a-205">hello following example creates an application named `myAADApp` and uses a password of `myPassword`.</span></span> <span data-ttu-id="71f4a-206">Określ własnego hasła w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="71f4a-206">Specify your own password as follows:</span></span>

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

<span data-ttu-id="71f4a-207">Zanotuj hello `applicationId` który jest zwracany w danych wyjściowych hello z hello poprzedzających polecenia.</span><span class="sxs-lookup"><span data-stu-id="71f4a-207">Make a note of hello `applicationId` that is returned in hello output from hello preceding command.</span></span> <span data-ttu-id="71f4a-208">Ten identyfikator aplikacji jest używany w niektórych hello pozostałe kroki.</span><span class="sxs-lookup"><span data-stu-id="71f4a-208">This application ID is used in some of hello remaining steps.</span></span> <span data-ttu-id="71f4a-209">Następnie należy utworzyć główną nazwę usługi (SPN), aby aplikacja hello jest dostępny w danym środowisku.</span><span class="sxs-lookup"><span data-stu-id="71f4a-209">Next, create a service principal name (SPN) so that hello application is accessible within your environment.</span></span> <span data-ttu-id="71f4a-210">toosuccessfully zaszyfrować lub odszyfrować dysków wirtualnych, uprawnienia do klucza kryptograficznego hello przechowywane w magazynie klucza musi być kluczy hello tooread zestaw toopermit hello Azure Active Directory aplikacji.</span><span class="sxs-lookup"><span data-stu-id="71f4a-210">toosuccessfully encrypt or decrypt virtual disks, permissions on hello cryptographic key stored in Key Vault must be set toopermit hello Azure Active Directory application tooread hello keys.</span></span>

<span data-ttu-id="71f4a-211">Utwórz hello SPN i ustaw odpowiednie uprawnienia hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="71f4a-211">Create hello SPN and set hello appropriate permissions as follows:</span></span>

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```


## <a name="add-a-virtual-disk-and-review-encryption-status"></a><span data-ttu-id="71f4a-212">Dodaj dysk wirtualny i sprawdzać stan szyfrowania</span><span class="sxs-lookup"><span data-stu-id="71f4a-212">Add a virtual disk and review encryption status</span></span>
<span data-ttu-id="71f4a-213">tooactually szyfrowania niektóre dyski wirtualne, umożliwia dodawanie tooan dysku, istniejącej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="71f4a-213">tooactually encrypt some virtual disks, lets add a disk tooan existing VM.</span></span> <span data-ttu-id="71f4a-214">Dodaj 5Gb tooan dysku danych istniejących maszyn wirtualnych w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="71f4a-214">Add a 5Gb data disk tooan existing VM as follows:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="71f4a-215">obecnie nie są szyfrowane Hello dysków wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="71f4a-215">hello virtual disks are not currently encrypted.</span></span> <span data-ttu-id="71f4a-216">Przejrzyj hello bieżącego stanu szyfrowania maszyny Wirtualnej w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="71f4a-216">Review hello current encryption status of your VM as follows:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="encrypt-virtual-disks"></a><span data-ttu-id="71f4a-217">Szyfrowanie dysków wirtualnych</span><span class="sxs-lookup"><span data-stu-id="71f4a-217">Encrypt virtual disks</span></span>
<span data-ttu-id="71f4a-218">toonow szyfrowania dysków wirtualnych hello, zebranie wszystkich hello poprzednie składniki:</span><span class="sxs-lookup"><span data-stu-id="71f4a-218">toonow encrypt hello virtual disks, you bring together all hello previous components:</span></span>

1. <span data-ttu-id="71f4a-219">Określ aplikację usługi Azure Active Directory hello i hasło.</span><span class="sxs-lookup"><span data-stu-id="71f4a-219">Specify hello Azure Active Directory application and password.</span></span>
2. <span data-ttu-id="71f4a-220">Określ hello Key Vault toostore hello metadanych dla zaszyfrowanych dysków.</span><span class="sxs-lookup"><span data-stu-id="71f4a-220">Specify hello Key Vault toostore hello metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="71f4a-221">Określ toouse kluczy kryptograficznych hello hello rzeczywiste szyfrowania i odszyfrowywania.</span><span class="sxs-lookup"><span data-stu-id="71f4a-221">Specify hello cryptographic keys toouse for hello actual encryption and decryption.</span></span>
4. <span data-ttu-id="71f4a-222">Określ, czy tooencrypt hello systemu operacyjnego, dysku dysków z danymi hello lub wszystkie.</span><span class="sxs-lookup"><span data-stu-id="71f4a-222">Specify whether you want tooencrypt hello OS disk, hello data disks, or all.</span></span>

<span data-ttu-id="71f4a-223">Umożliwia szczegółowe hello klucza usługi Azure Key Vault i hello utworzoną przez siebie jako hello identyfikator magazynu kluczy, identyfikator URI, a następnie klucza adresu URL w ostatnim kroku hello:</span><span class="sxs-lookup"><span data-stu-id="71f4a-223">Lets review hello details for your Azure Key Vault and hello key you created, as you need hello Key Vault ID, URI, and then key URL in hello final step:</span></span>

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

<span data-ttu-id="71f4a-224">Szyfrowanie dysków wirtualnych przy użyciu hello dane wyjściowe hello `azure keyvault show` i `azure keyvault key show` polecenia w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="71f4a-224">Encrypt your virtual disks using hello output from hello `azure keyvault show` and `azure keyvault key show` commands as follows:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

<span data-ttu-id="71f4a-225">Witaj poprzednie polecenie zawiera wiele zmiennych, hello poniższy przykład jest pełne polecenie hello odwołania:</span><span class="sxs-lookup"><span data-stu-id="71f4a-225">As hello preceding command has many variables, hello following example is hello complete command for reference:</span></span>

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

<span data-ttu-id="71f4a-226">Hello Azure CLI nie zapewnia pełne błędy podczas procesu szyfrowania hello.</span><span class="sxs-lookup"><span data-stu-id="71f4a-226">hello Azure CLI doesn't provide verbose errors during hello encryption process.</span></span> <span data-ttu-id="71f4a-227">Aby uzyskać dodatkowe informacje dotyczące rozwiązywania problemów, przejrzyj `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log` na powitania Szyfrujesz maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="71f4a-227">For additional troubleshooting information, review `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log` on hello VM you are encrypting.</span></span>

<span data-ttu-id="71f4a-228">Ponadto pozwala sprawdzać stan szyfrowania hello ponownie tooconfirm czy teraz zostały zaszyfrowane dyski wirtualne:</span><span class="sxs-lookup"><span data-stu-id="71f4a-228">Finally, lets review hello encryption status again tooconfirm that your virtual disks have now been encrypted:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="add-additional-data-disks"></a><span data-ttu-id="71f4a-229">Dodania dodatkowego dysku z danymi</span><span class="sxs-lookup"><span data-stu-id="71f4a-229">Add additional data disks</span></span>
<span data-ttu-id="71f4a-230">Po zaszyfrowanych dysków z danymi, możesz później dodać tooyour dodatkowych dysków wirtualnych maszyny Wirtualnej i również ich szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="71f4a-230">Once you have encrypted your data disks, you can later add additional virtual disks tooyour VM and also encrypt them.</span></span> <span data-ttu-id="71f4a-231">Po uruchomieniu hello `azure vm enable-disk-encryption` polecenia, wersję sekwencji hello przyrostu za pomocą hello `--sequence-version` parametru.</span><span class="sxs-lookup"><span data-stu-id="71f4a-231">When you run hello `azure vm enable-disk-encryption` command, increment hello sequence version using hello `--sequence-version` parameter.</span></span> <span data-ttu-id="71f4a-232">Ten parametr wersji sekwencji umożliwia tooperform powtarzających się operacjach na hello tej samej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="71f4a-232">This sequence version parameter allows you tooperform repeated operations on hello same VM.</span></span>

<span data-ttu-id="71f4a-233">Na przykład pozwala dodać drugi tooyour dysku wirtualnego maszyny Wirtualnej w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="71f4a-233">For example, lets add a second virtual disk tooyour VM as follows:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="71f4a-234">Uruchom ponownie teraz Dodawanie hello hello polecenia tooencrypt hello dysków wirtualnych, `--sequence-version` parametr i zwiększającą wartość hello z naszych najpierw uruchomić w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="71f4a-234">Rerun hello command tooencrypt hello virtual disks, this time adding hello `--sequence-version` parameter, and incrementing hello value from our first run as follows:</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="71f4a-235">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="71f4a-235">Next steps</span></span>
* <span data-ttu-id="71f4a-236">Aby uzyskać więcej informacji na temat zarządzania usługą Azure Key Vault, łącznie z usunięciem kluczy kryptograficznych i magazyny, zobacz [Zarządzanie Key Vault przy użyciu interfejsu wiersza polecenia](../../key-vault/key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="71f4a-236">For more information about managing Azure Key Vault, including deleting cryptographic keys and vaults, see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md).</span></span>
* <span data-ttu-id="71f4a-237">Aby uzyskać więcej informacji o szyfrowaniu dysków, takich jak przygotowywanie zaszyfrowanego niestandardowego wirtualna tooupload tooAzure, zobacz [szyfrowania dysków Azure](../../security/azure-security-disk-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="71f4a-237">For more information about disk encryption, such as preparing an encrypted custom VM tooupload tooAzure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
