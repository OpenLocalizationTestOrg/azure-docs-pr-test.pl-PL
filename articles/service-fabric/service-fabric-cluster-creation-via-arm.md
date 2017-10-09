---
title: "Sieć szkieletowa usług Azure aaaCreate klastra z szablonu | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooset się bezpiecznej sieci szkieletowej usług klastra na platformie Azure przy użyciu usługi Azure Resource Manager, magazyn kluczy Azure i usługi Azure Active Directory (Azure AD) do uwierzytelniania klientów."
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: chackdan
ms.assetid: 15d0ab67-fc66-4108-8038-3584eeebabaa
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/22/2017
ms.author: chackdan
ms.openlocfilehash: a4563c58a68127720a8290c3be0df9d026833eb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster-by-using-azure-resource-manager"></a><span data-ttu-id="e121b-103">Tworzenie klastra sieci szkieletowej usług za pomocą usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e121b-103">Create a Service Fabric cluster by using Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e121b-104">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e121b-104">Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
> * [<span data-ttu-id="e121b-105">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e121b-105">Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
>
>

<span data-ttu-id="e121b-106">Ten przewodnik krok po kroku przeprowadzi Cię przez proces konfigurowania bezpiecznej klastra usługi sieć szkieletowa usług Azure na platformie Azure przy użyciu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e121b-106">This step-by-step guide walks you through setting up a secure Azure Service Fabric cluster in Azure by using Azure Resource Manager.</span></span> <span data-ttu-id="e121b-107">Potwierdzam, że artykułu hello jest długa.</span><span class="sxs-lookup"><span data-stu-id="e121b-107">We acknowledge that hello article is long.</span></span> <span data-ttu-id="e121b-108">Jeśli nie znasz już dokładnie hello zawartości, są toofollow się, że każdy krok uważnie.</span><span class="sxs-lookup"><span data-stu-id="e121b-108">Nevertheless, unless you are already thoroughly familiar with hello content, be sure toofollow each step carefully.</span></span>

<span data-ttu-id="e121b-109">Podręcznik Hello obejmuje hello następujące procedury:</span><span class="sxs-lookup"><span data-stu-id="e121b-109">hello guide covers hello following procedures:</span></span>

* <span data-ttu-id="e121b-110">Konfigurowanie usługi Azure key vault tooupload certyfikaty zabezpieczeń klastra i aplikacji</span><span class="sxs-lookup"><span data-stu-id="e121b-110">Setting up an Azure key vault tooupload certificates for cluster and application security</span></span>
* <span data-ttu-id="e121b-111">Tworzenie klastra zabezpieczonych na platformie Azure przy użyciu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e121b-111">Creating a secured cluster in Azure by using Azure Resource Manager</span></span>
* <span data-ttu-id="e121b-112">Uwierzytelnianie użytkowników przy użyciu usługi Azure Active Directory (Azure AD) do zarządzania klastrem</span><span class="sxs-lookup"><span data-stu-id="e121b-112">Authenticating users by using Azure Active Directory (Azure AD) for cluster management</span></span>

<span data-ttu-id="e121b-113">Bezpieczne klastra jest klastra, który uniemożliwia nieautoryzowanym dostępem toomanagement operacji.</span><span class="sxs-lookup"><span data-stu-id="e121b-113">A secure cluster is a cluster that prevents unauthorized access toomanagement operations.</span></span> <span data-ttu-id="e121b-114">W tym wdrażanie, uaktualnianie i usuwania aplikacji, usług i hello nich danych.</span><span class="sxs-lookup"><span data-stu-id="e121b-114">This includes deploying, upgrading, and deleting applications, services, and hello data they contain.</span></span> <span data-ttu-id="e121b-115">Niezabezpieczone klaster jest klastrem informujący o tym, czy każdy połączyć tooat w dowolnym momencie i wykonywać operacje zarządzania.</span><span class="sxs-lookup"><span data-stu-id="e121b-115">An unsecure cluster is a cluster that anyone can connect tooat any time and perform management operations.</span></span> <span data-ttu-id="e121b-116">Chociaż możliwe toocreate klastra niezabezpieczone, zdecydowanie zaleca się tworzenie bezpiecznej klastra z początku hello.</span><span class="sxs-lookup"><span data-stu-id="e121b-116">Although it is possible toocreate an unsecure cluster, we highly recommend that you create a secure cluster from hello outset.</span></span> <span data-ttu-id="e121b-117">Ponieważ niezabezpieczone klastra nie można zabezpieczyć później, należy utworzyć nowy klaster.</span><span class="sxs-lookup"><span data-stu-id="e121b-117">Because an unsecure cluster cannot be secured later, a new cluster must be created.</span></span>

<span data-ttu-id="e121b-118">pojęcie Hello tworzenia bezpiecznych klastrów hello jest takie same, czy są one klastrów systemu Linux lub Windows.</span><span class="sxs-lookup"><span data-stu-id="e121b-118">hello concept of creating secure clusters is hello same, whether they are Linux or Windows clusters.</span></span> <span data-ttu-id="e121b-119">Aby uzyskać więcej informacji i pomocnika skryptów tworzenia bezpiecznych klastrów systemu Linux, zobacz [tworzenia bezpiecznych klastrów w systemie Linux](#secure-linux-clusters).</span><span class="sxs-lookup"><span data-stu-id="e121b-119">For more information and helper scripts for creating secure Linux clusters, see [Creating secure clusters on Linux](#secure-linux-clusters).</span></span>

## <a name="sign-in-tooyour-azure-account"></a><span data-ttu-id="e121b-120">Zaloguj się tooyour konto platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e121b-120">Sign in tooyour Azure account</span></span>
<span data-ttu-id="e121b-121">Ten przewodnik po używa [programu Azure PowerShell][azure-powershell].</span><span class="sxs-lookup"><span data-stu-id="e121b-121">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="e121b-122">Po ponownym uruchomieniu nowej sesji programu PowerShell, zaloguj się tooyour konto platformy Azure i wybierz subskrypcję, przed wykonaniem polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e121b-122">When you start a new PowerShell session, sign in tooyour Azure account and select your subscription before you execute Azure commands.</span></span>

<span data-ttu-id="e121b-123">Zaloguj się tooyour konto platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="e121b-123">Sign in tooyour Azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="e121b-124">Wybierz subskrypcję:</span><span class="sxs-lookup"><span data-stu-id="e121b-124">Select your subscription:</span></span>

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-a-key-vault"></a><span data-ttu-id="e121b-125">Konfigurowanie magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="e121b-125">Set up a key vault</span></span>
<span data-ttu-id="e121b-126">W tej sekcji omówiono tworzenie magazynu kluczy dla klastra sieci szkieletowej usług platformy Azure i dla aplikacji sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="e121b-126">This section discusses creating a key vault for a Service Fabric cluster in Azure and for Service Fabric applications.</span></span> <span data-ttu-id="e121b-127">TooAzure kompletny przewodnik po klucz magazynu, można znaleźć w temacie toohello [Key Vault Wprowadzenie — przewodnik][key-vault-get-started].</span><span class="sxs-lookup"><span data-stu-id="e121b-127">For a complete guide tooAzure Key Vault, refer toohello [Key Vault getting started guide][key-vault-get-started].</span></span>

<span data-ttu-id="e121b-128">Sieć szkieletowa usług używa toosecure certyfikatów X.509 klastra i zapewnia funkcje zabezpieczeń aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e121b-128">Service Fabric uses X.509 certificates toosecure a cluster and provide application security features.</span></span> <span data-ttu-id="e121b-129">Używane certyfikaty toomanage Key Vault dla klastrów sieci szkieletowej usług platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e121b-129">You use Key Vault toomanage certificates for Service Fabric clusters in Azure.</span></span> <span data-ttu-id="e121b-130">Po wdrożeniu klastra w systemie Azure hello dostawcy zasobów platformy Azure, który jest odpowiedzialny za tworzenie klastrów usługi sieć szkieletowa ściąga certyfikaty z magazynu kluczy i instaluje je w klastrze hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="e121b-130">When a cluster is deployed in Azure, hello Azure resource provider that's responsible for creating Service Fabric clusters pulls certificates from Key Vault and installs them on hello cluster VMs.</span></span>

<span data-ttu-id="e121b-131">Witaj poniższym diagramie przedstawiono relację hello Azure Key Vault, klaster sieci szkieletowej usług i hello dostawcy zasobów platformy Azure, który wykorzystuje certyfikaty przechowywane w magazynie kluczy, podczas tworzenia klastra:</span><span class="sxs-lookup"><span data-stu-id="e121b-131">hello following diagram illustrates hello relationship between Azure Key Vault, a Service Fabric cluster, and hello Azure resource provider that uses certificates stored in a key vault when it creates a cluster:</span></span>

![Diagram instalacji certyfikatu][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a><span data-ttu-id="e121b-133">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="e121b-133">Create a resource group</span></span>
<span data-ttu-id="e121b-134">pierwszym krokiem Hello jest toocreate grupę zasobów, w szczególności dla magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="e121b-134">hello first step is toocreate a resource group specifically for your key vault.</span></span> <span data-ttu-id="e121b-135">Firma Microsoft zaleca umieścić hello magazynu kluczy w jego własnej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="e121b-135">We recommend that you put hello key vault into its own resource group.</span></span> <span data-ttu-id="e121b-136">Ta akcja umożliwia usunięcie hello obliczeniowej i pamięci masowej grup zasobów, tym hello grupy zasobów, zawierającą klaster sieci szkieletowej usług bez utraty z kluczy i kluczy tajnych.</span><span class="sxs-lookup"><span data-stu-id="e121b-136">This action lets you remove hello compute and storage resource groups, including hello resource group that contains your Service Fabric cluster, without losing your keys and secrets.</span></span> <span data-ttu-id="e121b-137">Hello grupę zasobów, która zawiera magazynu kluczy _musi być w hello tego samego regionu_ jako hello klastra, który jest używany.</span><span class="sxs-lookup"><span data-stu-id="e121b-137">hello resource group that contains your key vault _must be in hello same region_ as hello cluster that is using it.</span></span>

<span data-ttu-id="e121b-138">Jeśli planujesz toodeploy klastry w wielu regionach, zalecamy nadanie nazwy grupy zasobów hello i hello magazynu kluczy w sposób, który wskazuje regionu, do którego należy.</span><span class="sxs-lookup"><span data-stu-id="e121b-138">If you plan toodeploy clusters in multiple regions, we suggest that you name hello resource group and hello key vault in a way that indicates which region it belongs to.</span></span>  

```powershell

    New-AzureRmResourceGroup -Name westus-mykeyvault -Location 'West US'
```
<span data-ttu-id="e121b-139">dane wyjściowe Hello powinien wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="e121b-139">hello output should look like this:</span></span>

```powershell

    WARNING: hello output object type of this cmdlet is going toobe modified in a future release.

    ResourceGroupName : westus-mykeyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/westus-mykeyvault

```
<a id="new-key-vault"></a>

### <a name="create-a-key-vault-in-hello-new-resource-group"></a><span data-ttu-id="e121b-140">Tworzenie magazynu kluczy w hello nową grupę zasobów</span><span class="sxs-lookup"><span data-stu-id="e121b-140">Create a key vault in hello new resource group</span></span>
<span data-ttu-id="e121b-141">magazyn kluczy Hello _musi być włączona dla wdrożenia_ tooallow hello certyfikaty tooget dostawcy zasobów obliczeniowych od niego i zainstalować ją na wystąpieniu maszyny wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="e121b-141">hello key vault _must be enabled for deployment_ tooallow hello compute resource provider tooget certificates from it and install it on virtual machine instances:</span></span>

```powershell

    New-AzureRmKeyVault -VaultName 'mywestusvault' -ResourceGroupName 'westus-mykeyvault' -Location 'West US' -EnabledForDeployment

```

<span data-ttu-id="e121b-142">dane wyjściowe Hello powinien wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="e121b-142">hello output should look like this:</span></span>

```powershell

    Vault Name                       : mywestusvault
    Resource Group Name              : westus-mykeyvault
    Location                         : West US
    Resource ID                      : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault
    Vault URI                        : https://mywestusvault.vault.azure.net
    Tenant ID                        : <guid>
    SKU                              : Standard
    Enabled For Deployment?          : False
    Enabled For Template Deployment? : False
    Enabled For Disk Encryption?     : False
    Access Policies                  :
                                       Tenant ID                :    <guid>
                                       Object ID                :    <guid>
                                       Application ID           :
                                       Display Name             :    
                                       Permissions tooKeys      :    get, create, delete, list, update, import, backup, restore
                                       Permissions tooSecrets   :    all


    Tags                             :
```
<a id="existing-key-vault"></a>

## <a name="use-an-existing-key-vault"></a><span data-ttu-id="e121b-143">Użyj istniejącego magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="e121b-143">Use an existing key vault</span></span>

<span data-ttu-id="e121b-144">toouse istniejący magazyn kluczy, możesz _należy włączyć dla wdrożenia_ tooallow hello certyfikaty tooget dostawcy zasobów obliczeniowych od niego i zainstaluj go na węzłach klastra:</span><span class="sxs-lookup"><span data-stu-id="e121b-144">toouse an existing key vault, you _must enable it for deployment_ tooallow hello compute resource provider tooget certificates from it and install it on cluster nodes:</span></span>

```powershell

Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

```

<a id="add-certificate-to-key-vault"></a>

## <a name="add-certificates-tooyour-key-vault"></a><span data-ttu-id="e121b-145">Dodaj magazyn kluczy tooyour certyfikatów</span><span class="sxs-lookup"><span data-stu-id="e121b-145">Add certificates tooyour key vault</span></span>

<span data-ttu-id="e121b-146">Certyfikaty są używane w sieci szkieletowej usług tooprovide uwierzytelnianie i szyfrowanie toosecure różnych aspektów klastra i jego zastosowań.</span><span class="sxs-lookup"><span data-stu-id="e121b-146">Certificates are used in Service Fabric tooprovide authentication and encryption toosecure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="e121b-147">Aby uzyskać więcej informacji dotyczących używania certyfikatów w sieci szkieletowej usług, zobacz [scenariusze zabezpieczeń klastra sieci szkieletowej usług][service-fabric-cluster-security].</span><span class="sxs-lookup"><span data-stu-id="e121b-147">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios][service-fabric-cluster-security].</span></span>

### <a name="cluster-and-server-certificate-required"></a><span data-ttu-id="e121b-148">Klaster a serwera certyfikatów (wymagane)</span><span class="sxs-lookup"><span data-stu-id="e121b-148">Cluster and server certificate (required)</span></span>
<span data-ttu-id="e121b-149">Ten certyfikat jest wymagany toosecure klastra i zapobiec tooit nieautoryzowanego dostępu.</span><span class="sxs-lookup"><span data-stu-id="e121b-149">This certificate is required toosecure a cluster and prevent unauthorized access tooit.</span></span> <span data-ttu-id="e121b-150">Udostępnia ona zabezpieczeń klastra na dwa sposoby:</span><span class="sxs-lookup"><span data-stu-id="e121b-150">It provides cluster security in two ways:</span></span>

* <span data-ttu-id="e121b-151">Uwierzytelnianie klastra: uwierzytelnia komunikacji między węzłami w Federacji klastra.</span><span class="sxs-lookup"><span data-stu-id="e121b-151">Cluster authentication: Authenticates node-to-node communication for cluster federation.</span></span> <span data-ttu-id="e121b-152">Tylko węzły, które można potwierdzić swoją tożsamość, z tym certyfikatem może dołączać hello klastra.</span><span class="sxs-lookup"><span data-stu-id="e121b-152">Only nodes that can prove their identity with this certificate can join hello cluster.</span></span>
* <span data-ttu-id="e121b-153">Uwierzytelnianie serwera: uwierzytelnia hello klastra zarządzania punkty końcowe tooa zarządzania klienta, tak, aby hello klienta zarządzania zna jest mówić toohello rzeczywistych klastra.</span><span class="sxs-lookup"><span data-stu-id="e121b-153">Server authentication: Authenticates hello cluster management endpoints tooa management client, so that hello management client knows it is talking toohello real cluster.</span></span> <span data-ttu-id="e121b-154">Ten certyfikat zapewnia również SSL hello interfejsu API zarządzania HTTPS oraz Service Fabric Explorer, za pośrednictwem protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e121b-154">This certificate also provides an SSL for hello HTTPS management API and for Service Fabric Explorer over HTTPS.</span></span>

<span data-ttu-id="e121b-155">tooserve tych celów hello certyfikatu musi spełniać następujące wymagania hello:</span><span class="sxs-lookup"><span data-stu-id="e121b-155">tooserve these purposes, hello certificate must meet hello following requirements:</span></span>

* <span data-ttu-id="e121b-156">Witaj, certyfikat musi zawierać klucz prywatny.</span><span class="sxs-lookup"><span data-stu-id="e121b-156">hello certificate must contain a private key.</span></span>
* <span data-ttu-id="e121b-157">Witaj certyfikatu musi zostać utworzony dla wymiany kluczy, który jest możliwy do wyeksportowania tooa plik wymiany informacji osobistych (pfx).</span><span class="sxs-lookup"><span data-stu-id="e121b-157">hello certificate must be created for key exchange, which is exportable tooa Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="e121b-158">Nazwa podmiotu certyfikatu Hello musi odpowiadać domeny hello używanie klastra usługi sieć szkieletowa hello tooaccess.</span><span class="sxs-lookup"><span data-stu-id="e121b-158">hello certificate's subject name must match hello domain that you use tooaccess hello Service Fabric cluster.</span></span> <span data-ttu-id="e121b-159">To dopasowanie jest wymagana tooprovide SSL dla punktów końcowych zarządzania HTTPS hello klastra i Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="e121b-159">This matching is required tooprovide an SSL for hello cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="e121b-160">Nie można uzyskać certyfikatu SSL z urzędu certyfikacji (CA) w celu hello. cloudapp.azure.com domeny.</span><span class="sxs-lookup"><span data-stu-id="e121b-160">You cannot obtain an SSL certificate from a certificate authority (CA) for hello .cloudapp.azure.com domain.</span></span> <span data-ttu-id="e121b-161">Należy uzyskać niestandardowej nazwy domeny dla klastra.</span><span class="sxs-lookup"><span data-stu-id="e121b-161">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="e121b-162">Podczas żądania certyfikatu z urzędu certyfikacji, hello nazwa podmiotu certyfikatu musi odpowiadać hello niestandardowej nazwy domeny używanej dla klastra.</span><span class="sxs-lookup"><span data-stu-id="e121b-162">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name that you use for your cluster.</span></span>

### <a name="application-certificates-optional"></a><span data-ttu-id="e121b-163">Certyfikaty aplikacji (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="e121b-163">Application certificates (optional)</span></span>
<span data-ttu-id="e121b-164">Dowolna liczba dodatkowych certyfikatów można zainstalować w klastrze dla aplikacji ze względów bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="e121b-164">Any number of additional certificates can be installed on a cluster for application security purposes.</span></span> <span data-ttu-id="e121b-165">Przed utworzeniem klastra, należy wziąć pod uwagę scenariusze zabezpieczeń aplikacji hello, które wymagają toobe certyfikat zainstalowany na węzłach hello, takich jak:</span><span class="sxs-lookup"><span data-stu-id="e121b-165">Before creating your cluster, consider hello application security scenarios that require a certificate toobe installed on hello nodes, such as:</span></span>

* <span data-ttu-id="e121b-166">Szyfrowanie i odszyfrowywanie wartości konfiguracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e121b-166">Encryption and decryption of application configuration values.</span></span>
* <span data-ttu-id="e121b-167">Szyfrowanie danych w węzłach podczas replikacji.</span><span class="sxs-lookup"><span data-stu-id="e121b-167">Encryption of data across nodes during replication.</span></span>

### <a name="formatting-certificates-for-azure-resource-provider-use"></a><span data-ttu-id="e121b-168">Formatowanie certyfikatów do użytku dostawcy zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e121b-168">Formatting certificates for Azure resource provider use</span></span>
<span data-ttu-id="e121b-169">Można dodać i używać plików kluczy prywatnych (pfx) bezpośrednio za pomocą magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="e121b-169">You can add and use private key files (.pfx) directly through your key vault.</span></span> <span data-ttu-id="e121b-170">Dostawcy zasobów obliczeniowych Azure hello wymaga jednak toobe klucze przechowywane w formacie JavaScript Object Notation (JSON) specjalnych.</span><span class="sxs-lookup"><span data-stu-id="e121b-170">However, hello Azure compute resource provider requires keys toobe stored in a special JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="e121b-171">Hello format zawiera plik PFX hello jako ciąg zakodowany w formacie 64 bazy i hello hasło klucza prywatnego.</span><span class="sxs-lookup"><span data-stu-id="e121b-171">hello format includes hello .pfx file as a base 64-encoded string and hello private key password.</span></span> <span data-ttu-id="e121b-172">tooaccommodate tych wymagań, hello kluczy musi być umieszczona w ciągu JSON i następnie przechowywane jako "hasła" hello klucza magazynu.</span><span class="sxs-lookup"><span data-stu-id="e121b-172">tooaccommodate these requirements, hello keys must be placed in a JSON string and then stored as "secrets" in hello key vault.</span></span>

<span data-ttu-id="e121b-173">toomake to przetworzyć łatwiej, [moduł programu PowerShell jest dostępny w witrynie GitHub][service-fabric-rp-helpers].</span><span class="sxs-lookup"><span data-stu-id="e121b-173">toomake this process easier, a [PowerShell module is available on GitHub][service-fabric-rp-helpers].</span></span> <span data-ttu-id="e121b-174">Moduł hello toouse, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="e121b-174">toouse hello module, do hello following:</span></span>

1. <span data-ttu-id="e121b-175">Pobierz całą zawartość repozytorium hello hello do katalogu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="e121b-175">Download hello entire contents of hello repo into a local directory.</span></span>
2. <span data-ttu-id="e121b-176">Przejdź toohello katalogu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="e121b-176">Go toohello local directory.</span></span>
2. <span data-ttu-id="e121b-177">Zaimportuj moduł ServiceFabricRPHelpers hello w oknie programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="e121b-177">Import hello ServiceFabricRPHelpers module in your PowerShell window:</span></span>

```powershell

 Import-Module "C:\..\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

```

<span data-ttu-id="e121b-178">Witaj `Invoke-AddCertToKeyVault` polecenia w tym module środowiska PowerShell automatycznie formatuje klucz prywatny certyfikatu do ciągu JSON i przekazanie jej toohello magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="e121b-178">hello `Invoke-AddCertToKeyVault` command in this PowerShell module automatically formats a certificate private key into a JSON string and uploads it toohello key vault.</span></span> <span data-ttu-id="e121b-179">Użyj hello polecenia tooadd hello klastra certyfikat i wszelkie dodatkowe aplikacji certyfikaty toohello magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="e121b-179">Use hello command tooadd hello cluster certificate and any additional application certificates toohello key vault.</span></span> <span data-ttu-id="e121b-180">Powtórz ten krok dla wszystkich dodatkowych certyfikatów, które chcesz tooinstall w klastrze.</span><span class="sxs-lookup"><span data-stu-id="e121b-180">Repeat this step for any additional certificates you want tooinstall in your cluster.</span></span>

#### <a name="uploading-an-existing-certificate"></a><span data-ttu-id="e121b-181">Przekazywanie istniejącego certyfikatu</span><span class="sxs-lookup"><span data-stu-id="e121b-181">Uploading an existing certificate</span></span>

```powershell

 Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName westus-mykeyvault -Location "West US" -VaultName mywestusvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

```

<span data-ttu-id="e121b-182">Jeśli wystąpi błąd, takich jak hello przedstawionego poniżej, zwykle oznacza to, że występuje konflikt adresu URL zasobu.</span><span class="sxs-lookup"><span data-stu-id="e121b-182">If you get an error, such as hello one shown here, it usually means that you have a resource URL conflict.</span></span> <span data-ttu-id="e121b-183">tooresolve hello konflikt, Zmień nazwę magazynu kluczy hello.</span><span class="sxs-lookup"><span data-stu-id="e121b-183">tooresolve hello conflict, change hello key vault name.</span></span>

```
Set-AzureKeyVaultSecret : hello remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

<span data-ttu-id="e121b-184">Po hello konflikt został rozwiązany, dane wyjściowe hello powinien wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="e121b-184">After hello conflict is resolved, hello output should look like this:</span></span>

```

    Switching context tooSubscriptionId <guid>
    Ensuring ResourceGroup westus-mykeyvault in West US
    WARNING: hello output object type of this cmdlet is going toobe modified in a future release.
    Using existing value mywestusvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret toomywestusvault in vault mywestusvault


Name  : CertificateThumbprint
Value : E21DBC64B183B5BF355C34C46E03409FEEAEF58D

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault

Name  : CertificateURL
Value : https://mywestusvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

>[!NOTE]
><span data-ttu-id="e121b-185">Należy hello trzech poprzednich ciągów, CertificateThumbprint, SourceVault i CertificateURL, tooset bezpiecznego klastra sieci szkieletowej usług i tooobtain wszelkich certyfikatów aplikacji, które mogą używać zabezpieczeń aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e121b-185">You need hello three preceding strings, CertificateThumbprint, SourceVault, and CertificateURL, tooset up a secure Service Fabric cluster and tooobtain any application certificates that you might be using for application security.</span></span> <span data-ttu-id="e121b-186">Jeśli zapiszesz hello ciągów, może być tooretrieve trudno ich badając klucza hello później magazynu.</span><span class="sxs-lookup"><span data-stu-id="e121b-186">If you do not save hello strings, it can be difficult tooretrieve them by querying hello key vault later.</span></span>

<a id="add-self-signed-certificate-to-key-vault"></a>

#### <a name="creating-a-self-signed-certificate-and-uploading-it-toohello-key-vault"></a><span data-ttu-id="e121b-187">Tworzenie certyfikatu z podpisem własnym i przekazać go toohello magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="e121b-187">Creating a self-signed certificate and uploading it toohello key vault</span></span>

<span data-ttu-id="e121b-188">Jeśli zostały już przekazane magazynu kluczy toohello certyfikaty, Pomiń ten krok.</span><span class="sxs-lookup"><span data-stu-id="e121b-188">If you have already uploaded your certificates toohello key vault, skip this step.</span></span> <span data-ttu-id="e121b-189">Ten krok jest generowania nowego certyfikatu z podpisem własnym i przekazać go tooyour magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="e121b-189">This step is for generating a new self-signed certificate and uploading it tooyour key vault.</span></span> <span data-ttu-id="e121b-190">Po Zmień parametry hello w hello następującego skryptu, a następnie uruchom go, należy się monit o hasło certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="e121b-190">After you change hello parameters in hello following script and then run it, you should be prompted for a certificate password.</span></span>  

```powershell

$ResourceGroup = "chackowestuskv"
$VName = "chackokv2"
$SubID = "6c653126-e4ba-42cd-a1dd-f7bf96ae7a47"
$locationRegion = "westus"
$newCertName = "chackotestcertificate1"
$dnsName = "www.mycluster.westus.mydomain.com" #hello certificate's subject name must match hello domain used tooaccess hello Service Fabric cluster.
$localCertPath = "C:\MyCertificates" # location where you want hello .PFX toobe stored

 Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResourceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath

```

<span data-ttu-id="e121b-191">Jeśli wystąpi błąd, takich jak hello przedstawionego poniżej, zwykle oznacza to, że występuje konflikt adresu URL zasobu.</span><span class="sxs-lookup"><span data-stu-id="e121b-191">If you get an error, such as hello one shown here, it usually means that you have a resource URL conflict.</span></span> <span data-ttu-id="e121b-192">konflikt hello tooresolve, Zmień nazwę magazynu kluczy hello, nazwa grupy zasobów i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="e121b-192">tooresolve hello conflict, change hello key vault name, RG name, and so forth.</span></span>

```
Set-AzureKeyVaultSecret : hello remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

<span data-ttu-id="e121b-193">Po hello konflikt został rozwiązany, dane wyjściowe hello powinien wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="e121b-193">After hello conflict is resolved, hello output should look like this:</span></span>

```
PS C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers> Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResouceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -Password $certPassword -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath
Switching context tooSubscriptionId 6c343126-e4ba-52cd-a1dd-f8bf96ae7a47
Ensuring ResourceGroup chackowestuskv in westus
WARNING: hello output object type of this cmdlet will be modified in a future release.
Creating new vault westuskv1 in westus
Creating new self signed certificate at C:\MyCertificates\chackonewcertificate1.pfx
Reading pfx file from C:\MyCertificates\chackonewcertificate1.pfx
Writing secret toochackonewcertificate1 in vault westuskv1


Name  : CertificateThumbprint
Value : 96BB3CC234F9D43C25D4B547sd8DE7B569F413EE

Name  : SourceVault
Value : /subscriptions/6c653126-e4ba-52cd-a1dd-f8bf96ae7a47/resourceGroups/chackowestuskv/providers/Microsoft.KeyVault/vaults/westuskv1

Name  : CertificateURL
Value : https://westuskv1.vault.azure.net:443/secrets/chackonewcertificate1/ee247291e45d405b8c8bbf81782d12bd

```

>[!NOTE]
><span data-ttu-id="e121b-194">Należy hello trzech poprzednich ciągów, CertificateThumbprint, SourceVault i CertificateURL, tooset bezpiecznego klastra sieci szkieletowej usług i tooobtain wszelkich certyfikatów aplikacji, które mogą używać zabezpieczeń aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e121b-194">You need hello three preceding strings, CertificateThumbprint, SourceVault, and CertificateURL, tooset up a secure Service Fabric cluster and tooobtain any application certificates that you might be using for application security.</span></span> <span data-ttu-id="e121b-195">Jeśli zapiszesz hello ciągów, może być tooretrieve trudno ich badając klucza hello później magazynu.</span><span class="sxs-lookup"><span data-stu-id="e121b-195">If you do not save hello strings, it can be difficult tooretrieve them by querying hello key vault later.</span></span>

 <span data-ttu-id="e121b-196">W tym momencie powinny mieć następujące elementy w miejscu hello:</span><span class="sxs-lookup"><span data-stu-id="e121b-196">At this point, you should have hello following elements in place:</span></span>

* <span data-ttu-id="e121b-197">Witaj grupy zasobów magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="e121b-197">hello key vault resource group.</span></span>
* <span data-ttu-id="e121b-198">Witaj magazyn kluczy i adresu URL (o nazwie SourceVault hello poprzedzający dane wyjściowe programu PowerShell).</span><span class="sxs-lookup"><span data-stu-id="e121b-198">hello key vault and its URL (called SourceVault in hello preceding PowerShell output).</span></span>
* <span data-ttu-id="e121b-199">certyfikat uwierzytelniania serwera klastra Hello i jego adres URL w magazynie kluczy hello.</span><span class="sxs-lookup"><span data-stu-id="e121b-199">hello cluster server authentication certificate and its URL in hello key vault.</span></span>
* <span data-ttu-id="e121b-200">Certyfikaty aplikacji Hello i ich adresy URL w magazynie kluczy hello.</span><span class="sxs-lookup"><span data-stu-id="e121b-200">hello application certificates and their URLs in hello key vault.</span></span>


<a id="add-AAD-for-client"></a>

## <a name="set-up-azure-active-directory-for-client-authentication"></a><span data-ttu-id="e121b-201">Konfigurowanie usługi Azure Active Directory do uwierzytelniania klientów</span><span class="sxs-lookup"><span data-stu-id="e121b-201">Set up Azure Active Directory for client authentication</span></span>

<span data-ttu-id="e121b-202">Usługi Azure AD umożliwia tooapplications dostępu użytkownika toomanage organizacji (nazywane dzierżawców).</span><span class="sxs-lookup"><span data-stu-id="e121b-202">Azure AD enables organizations (known as tenants) toomanage user access tooapplications.</span></span> <span data-ttu-id="e121b-203">Aplikacje są podzielone na tych z opartą na sieci web interfejsu użytkownika logowania i te przy użyciu środowiska macierzystego klienta.</span><span class="sxs-lookup"><span data-stu-id="e121b-203">Applications are divided into those with a web-based sign-in UI and those with a native client experience.</span></span> <span data-ttu-id="e121b-204">W tym artykule przyjęto założenie, że utworzono już dzierżawcy.</span><span class="sxs-lookup"><span data-stu-id="e121b-204">In this article, we assume that you have already created a tenant.</span></span> <span data-ttu-id="e121b-205">Jeśli nie masz, Rozpocznij od przeczytania [jak dzierżawy usługi Azure Active Directory tooget][active-directory-howto-tenant].</span><span class="sxs-lookup"><span data-stu-id="e121b-205">If you have not, start by reading [How tooget an Azure Active Directory tenant][active-directory-howto-tenant].</span></span>

<span data-ttu-id="e121b-206">Klaster sieci szkieletowej usług oferuje kilka tooits punkty wejścia funkcje zarządzania, w tym hello opartych na sieci web [Service Fabric Explorer] [ service-fabric-visualizing-your-cluster] i [programu Visual Studio] [service-fabric-manage-application-in-visual-studio].</span><span class="sxs-lookup"><span data-stu-id="e121b-206">A Service Fabric cluster offers several entry points tooits management functionality, including hello web-based [Service Fabric Explorer][service-fabric-visualizing-your-cluster] and [Visual Studio][service-fabric-manage-application-in-visual-studio].</span></span> <span data-ttu-id="e121b-207">W związku z tym możesz utworzyć dwie usługi Azure AD aplikacji toocontrol dostępu toohello klastra, jednej aplikacji sieci web i jednej aplikacji natywnej.</span><span class="sxs-lookup"><span data-stu-id="e121b-207">As a result, you create two Azure AD applications toocontrol access toohello cluster, one web application and one native application.</span></span>

<span data-ttu-id="e121b-208">Niektóre kroki hello zaangażowane w konfigurowaniu usługi Azure AD z klastrem usługi sieć szkieletowa toosimplify, został utworzony zestaw skryptów programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e121b-208">toosimplify some of hello steps involved in configuring Azure AD with a Service Fabric cluster, we have created a set of Windows PowerShell scripts.</span></span>

> [!NOTE]
> <span data-ttu-id="e121b-209">Należy wykonać następujące kroki, przed utworzeniem klastra hello hello.</span><span class="sxs-lookup"><span data-stu-id="e121b-209">You must complete hello following steps before you create hello cluster.</span></span> <span data-ttu-id="e121b-210">Ponieważ skrypty hello oczekuje nazwy klastra i punkty końcowe, hello wartości powinny być planowane i nie wartości, które zostało już utworzone.</span><span class="sxs-lookup"><span data-stu-id="e121b-210">Because hello scripts expect cluster names and endpoints, hello values should be planned and not values that you have already created.</span></span>

1. <span data-ttu-id="e121b-211">[Pobierz skrypty hello] [ sf-aad-ps-script-download] tooyour komputera.</span><span class="sxs-lookup"><span data-stu-id="e121b-211">[Download hello scripts][sf-aad-ps-script-download] tooyour computer.</span></span>
2. <span data-ttu-id="e121b-212">Kliknij prawym przyciskiem myszy hello pliku zip, wybierz opcję **właściwości**, wybierz pozycję hello **Odblokuj** pole wyboru, a następnie kliknij przycisk **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="e121b-212">Right-click hello zip file, select **Properties**, select hello **Unblock** check box, and then click **Apply**.</span></span>
3. <span data-ttu-id="e121b-213">Wyodrębnij plik zip hello.</span><span class="sxs-lookup"><span data-stu-id="e121b-213">Extract hello zip file.</span></span>
4. <span data-ttu-id="e121b-214">Uruchom `SetupApplications.ps1`i podaj hello TenantId, ClusterName i WebApplicationReplyUrl jako parametry.</span><span class="sxs-lookup"><span data-stu-id="e121b-214">Run `SetupApplications.ps1`, and provide hello TenantId, ClusterName, and WebApplicationReplyUrl as parameters.</span></span> <span data-ttu-id="e121b-215">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="e121b-215">For example:</span></span>

    ```powershell
    .\SetupApplications.ps1 -TenantId '690ec069-8200-4068-9d01-5aaf188e557a' -ClusterName 'mycluster' -WebApplicationReplyUrl 'https://mycluster.westus.cloudapp.azure.com:19080/Explorer/index.html'
    ```

    <span data-ttu-id="e121b-216">Można znaleźć identyfikatora sieci dzierżawcy, wykonując polecenie programu PowerShell hello `Get-AzureSubscription`.</span><span class="sxs-lookup"><span data-stu-id="e121b-216">You can find your TenantId by executing hello PowerShell command `Get-AzureSubscription`.</span></span> <span data-ttu-id="e121b-217">Wykonywanie to polecenie wyświetla hello TenantId dla każdej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="e121b-217">Executing this command displays hello TenantId for every subscription.</span></span>

    <span data-ttu-id="e121b-218">ClusterName jest tooprefix używanych aplikacji hello Azure AD, które są tworzone przez skrypt hello.</span><span class="sxs-lookup"><span data-stu-id="e121b-218">ClusterName is used tooprefix hello Azure AD applications that are created by hello script.</span></span> <span data-ttu-id="e121b-219">Nie musi dokładnie toomatch hello rzeczywista nazwa klastra.</span><span class="sxs-lookup"><span data-stu-id="e121b-219">It does not need toomatch hello actual cluster name exactly.</span></span> <span data-ttu-id="e121b-220">Jest przeznaczone tylko toomake go łatwiejsze toomap usługi Azure AD artefakty toohello sieci szkieletowej usług klastra, który jest używany z.</span><span class="sxs-lookup"><span data-stu-id="e121b-220">It is intended only toomake it easier toomap Azure AD artifacts toohello Service Fabric cluster that they're being used with.</span></span>

    <span data-ttu-id="e121b-221">WebApplicationReplyUrl jest domyślny punkt końcowy hello, zwracające usługi Azure AD użytkownicy tooyour po kończyły się zalogować.</span><span class="sxs-lookup"><span data-stu-id="e121b-221">WebApplicationReplyUrl is hello default endpoint that Azure AD returns tooyour users after they finish signing in.</span></span> <span data-ttu-id="e121b-222">Ustaw ten punkt końcowy jako punkt końcowy Service Fabric Explorer powitania dla klastra, która domyślnie jest:</span><span class="sxs-lookup"><span data-stu-id="e121b-222">Set this endpoint as hello Service Fabric Explorer endpoint for your cluster, which by default is:</span></span>

    <span data-ttu-id="e121b-223">https://&lt;cluster_domain&gt;: 19080/Explorer</span><span class="sxs-lookup"><span data-stu-id="e121b-223">https://&lt;cluster_domain&gt;:19080/Explorer</span></span>

    <span data-ttu-id="e121b-224">Jesteś zostanie wyświetlony monit o toosign tooan konta, które ma uprawnienia administracyjne dla dzierżawy usługi Azure AD hello.</span><span class="sxs-lookup"><span data-stu-id="e121b-224">You are prompted toosign in tooan account that has administrative privileges for hello Azure AD tenant.</span></span> <span data-ttu-id="e121b-225">Po zalogowaniu w hello skrypt tworzy hello sieci web i toorepresent natywnych aplikacji klastra sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="e121b-225">After you sign in, hello script creates hello web and native applications toorepresent your Service Fabric cluster.</span></span> <span data-ttu-id="e121b-226">Jeśli przyjrzymy się aplikacji hello dzierżawy w hello [klasycznego portalu Azure][azure-classic-portal], powinny pojawić się dwa nowe wpisy:</span><span class="sxs-lookup"><span data-stu-id="e121b-226">If you look at hello tenant's applications in hello [Azure classic portal][azure-classic-portal], you should see two new entries:</span></span>

   * <span data-ttu-id="e121b-227">*ClusterName*\_klastra</span><span class="sxs-lookup"><span data-stu-id="e121b-227">*ClusterName*\_Cluster</span></span>
   * <span data-ttu-id="e121b-228">*ClusterName*\_klienta</span><span class="sxs-lookup"><span data-stu-id="e121b-228">*ClusterName*\_Client</span></span>

   <span data-ttu-id="e121b-229">skrypt Hello drukuje hello Otwórz wymagane przez szablon usługi Azure Resource Manager hello podczas tworzenia klastra hello w następnej sekcji hello, dzięki czemu okno programu PowerShell dobrze tookeep hello JSON.</span><span class="sxs-lookup"><span data-stu-id="e121b-229">hello script prints hello JSON required by hello Azure Resource Manager template when you create hello cluster in hello next section, so it's a good idea tookeep hello PowerShell window open.</span></span>

```json
"azureActiveDirectory": {
  "tenantId":"<guid>",
  "clusterApplication":"<guid>",
  "clientApplication":"<guid>"
},
```

## <a name="create-a-service-fabric-cluster-resource-manager-template"></a><span data-ttu-id="e121b-230">Utwórz szablon Menedżera zasobów klastra sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="e121b-230">Create a Service Fabric cluster Resource Manager template</span></span>
<span data-ttu-id="e121b-231">W tej sekcji hello produktów wyjściowych hello powyższych poleceń programu PowerShell są używane w szablonie usługi Resource Manager klastra sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="e121b-231">In this section, hello outputs of hello preceding PowerShell commands are used in a Service Fabric cluster Resource Manager template.</span></span>

<span data-ttu-id="e121b-232">Szablony Menedżera zasobów próbki są dostępne w hello [galerii szablonów szybki start Azure w serwisie GitHub][azure-quickstart-templates].</span><span class="sxs-lookup"><span data-stu-id="e121b-232">Sample Resource Manager templates are available in hello [Azure quick-start template gallery on GitHub][azure-quickstart-templates].</span></span> <span data-ttu-id="e121b-233">Te szablony może służyć jako punkt początkowy dla szablonu klastra.</span><span class="sxs-lookup"><span data-stu-id="e121b-233">These templates can be used as a starting point for your cluster template.</span></span>

### <a name="create-hello-resource-manager-template"></a><span data-ttu-id="e121b-234">Tworzenie szablonu usługi Resource Manager hello</span><span class="sxs-lookup"><span data-stu-id="e121b-234">Create hello Resource Manager template</span></span>
<span data-ttu-id="e121b-235">W tym przewodniku używa hello [5 węzłów klastra bezpiecznego] [ service-fabric-secure-cluster-5-node-1-nodetype] przykładowy szablon i parametrów szablonu.</span><span class="sxs-lookup"><span data-stu-id="e121b-235">This guide uses hello [5-node secure cluster][service-fabric-secure-cluster-5-node-1-nodetype] example template and template parameters.</span></span> <span data-ttu-id="e121b-236">Pobierz `azuredeploy.json` i `azuredeploy.parameters.json` tooyour komputera, a następnie otwórz oba pliki w edytorze tekstu.</span><span class="sxs-lookup"><span data-stu-id="e121b-236">Download `azuredeploy.json` and `azuredeploy.parameters.json` tooyour computer and open both files in your favorite text editor.</span></span>

### <a name="add-certificates"></a><span data-ttu-id="e121b-237">Dodaj certyfikaty</span><span class="sxs-lookup"><span data-stu-id="e121b-237">Add certificates</span></span>
<span data-ttu-id="e121b-238">Możesz dodać szablonu usługi Resource Manager klastra tooa certyfikatów za pomocą odwołań do magazynu kluczy hello, która zawiera klucze certyfikatów hello.</span><span class="sxs-lookup"><span data-stu-id="e121b-238">You add certificates tooa cluster Resource Manager template by referencing hello key vault that contains hello certificate keys.</span></span> <span data-ttu-id="e121b-239">Zaleca się umieszczenie hello usługi key vault wartości w pliku parametrów szablonu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e121b-239">We recommend that you place hello key-vault values in a Resource Manager template parameters file.</span></span> <span data-ttu-id="e121b-240">W ten sposób pozwala hello Menedżera zasobów pliku szablonu wielokrotnego użytku i wolnego wdrożenia tooa określonej wartości.</span><span class="sxs-lookup"><span data-stu-id="e121b-240">Doing so keeps hello Resource Manager template file reusable and free of values specific tooa deployment.</span></span>

#### <a name="add-all-certificates-toohello-virtual-machine-scale-set-osprofile"></a><span data-ttu-id="e121b-241">Dodaj wszystkie certyfikaty toohello maszyny wirtualnej zestawu skalowania maszyny wirtualnej osProfile</span><span class="sxs-lookup"><span data-stu-id="e121b-241">Add all certificates toohello virtual machine scale set osProfile</span></span>
<span data-ttu-id="e121b-242">Każdy certyfikat, który jest zainstalowany w klastrze hello muszą być skonfigurowane w sekcji osProfile hello zasób zestawu skali hello (Microsoft.Compute/virtualMachineScaleSets).</span><span class="sxs-lookup"><span data-stu-id="e121b-242">Every certificate that's installed in hello cluster must be configured in hello osProfile section of hello scale set resource (Microsoft.Compute/virtualMachineScaleSets).</span></span> <span data-ttu-id="e121b-243">Ta akcja powoduje, że certyfikat dostawcy zasobów hello hello tooinstall na powitania maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="e121b-243">This action instructs hello resource provider tooinstall hello certificate on hello VMs.</span></span> <span data-ttu-id="e121b-244">Ta instalacja obejmuje zarówno hello klastra certyfikat, jak i wszelkich certyfikatów zabezpieczeń aplikacji planowanie toouse aplikacji:</span><span class="sxs-lookup"><span data-stu-id="e121b-244">This installation includes both hello cluster certificate and any application security certificates that you plan toouse for your applications:</span></span>

```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  ...
  "properties": {
    ...
    "osProfile": {
      ...
      "secrets": [
        {
          "sourceVault": {
            "id": "[parameters('sourceVaultValue')]"
          },
          "vaultCertificates": [
            {
              "certificateStore": "[parameters('clusterCertificateStorevalue')]",
              "certificateUrl": "[parameters('clusterCertificateUrlValue')]"
            },
            {
              "certificateStore": "[parameters('applicationCertificateStorevalue')",
              "certificateUrl": "[parameters('applicationCertificateUrlValue')]"
            },
            ...
          ]
        }
      ]
    }
  }
}
```

#### <a name="configure-hello-service-fabric-cluster-certificate"></a><span data-ttu-id="e121b-245">Konfigurowanie certyfikatu klastra usługi sieć szkieletowa hello</span><span class="sxs-lookup"><span data-stu-id="e121b-245">Configure hello Service Fabric cluster certificate</span></span>
<span data-ttu-id="e121b-246">certyfikat uwierzytelniania Hello klastra muszą być skonfigurowane w obu zasobu klastra usługi sieć szkieletowa hello (Microsoft.ServiceFabric/clusters) i hello rozszerzenia sieci szkieletowej usług na potrzeby skalowania maszyny wirtualnej zestawy w zasób zestawu skali maszyny wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="e121b-246">hello cluster authentication certificate must be configured in both hello Service Fabric cluster resource (Microsoft.ServiceFabric/clusters) and hello Service Fabric extension for virtual machine scale sets in hello virtual machine scale set resource.</span></span> <span data-ttu-id="e121b-247">To rozmieszczenie umożliwia tooconfigure dostawcy zasobów usługi Service Fabric hello go dla uwierzytelniania klastra i uwierzytelniania serwera dla punktów końcowych zarządzania.</span><span class="sxs-lookup"><span data-stu-id="e121b-247">This arrangement allows hello Service Fabric resource provider tooconfigure it for use for cluster authentication and server authentication for management endpoints.</span></span>

##### <a name="virtual-machine-scale-set-resource"></a><span data-ttu-id="e121b-248">Zasób zestawu skalowania maszyn wirtualnych:</span><span class="sxs-lookup"><span data-stu-id="e121b-248">Virtual machine scale set resource:</span></span>
```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  ...
  "properties": {
    ...
    "virtualMachineProfile": {
      "extensionProfile": {
        "extensions": [
          {
            "name": "[concat('ServiceFabricNodeVmExt','_vmNodeType0Name')]",
            "properties": {
              ...
              "settings": {
                ...
                "certificate": {
                  "thumbprint": "[parameters('clusterCertificateThumbprint')]",
                  "x509StoreName": "[parameters('clusterCertificateStoreValue')]"
                },
                ...
              }
            }
          }
        ]
      }
    }
  }
}
```

##### <a name="service-fabric-resource"></a><span data-ttu-id="e121b-249">Zasobów sieci szkieletowej usług:</span><span class="sxs-lookup"><span data-stu-id="e121b-249">Service Fabric resource:</span></span>
```json
{
  "apiVersion": "2016-03-01",
  "type": "Microsoft.ServiceFabric/clusters",
  "name": "[parameters('clusterName')]",
  "location": "[parameters('clusterLocation')]",
  "dependsOn": [
    "[concat('Microsoft.Storage/storageAccounts/', variables('supportLogStorageAccountName'))]"
  ],
  "properties": {
    "certificate": {
      "thumbprint": "[parameters('clusterCertificateThumbprint')]",
      "x509StoreName": "[parameters('clusterCertificateStoreValue')]"
    },
    ...
  }
}
```

### <a name="insert-azure-ad-configuration"></a><span data-ttu-id="e121b-250">Wstaw konfiguracji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e121b-250">Insert Azure AD configuration</span></span>
<span data-ttu-id="e121b-251">mogą być wstawiane konfiguracji Hello Azure AD, który został utworzony wcześniej bezpośrednio do szablonu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e121b-251">hello Azure AD configuration that you created earlier can be inserted directly into your Resource Manager template.</span></span> <span data-ttu-id="e121b-252">Jednak zaleca się najpierw Wyodrębnij wartości hello do parametrów pliku tookeep hello Menedżera zasobów szablonu do ponownego użycia i zwolnij wdrożenia tooa określonej wartości.</span><span class="sxs-lookup"><span data-stu-id="e121b-252">However, we recommended that you first extract hello values into a parameters file tookeep hello Resource Manager template reusable and free of values specific tooa deployment.</span></span>

```json
{
  "apiVersion": "2016-03-01",
  "type": "Microsoft.ServiceFabric/clusters",
  "name": "[parameters('clusterName')]",
  ...
  "properties": {
    "certificate": {
      "thumbprint": "[parameters('clusterCertificateThumbprint')]",
      "x509StoreName": "[parameters('clusterCertificateStorevalue')]"
    },
    ...
    "azureActiveDirectory": {
      "tenantId": "[parameters('aadTenantId')]",
      "clusterApplication": "[parameters('aadClusterApplicationId')]",
      "clientApplication": "[parameters('aadClientApplicationId')]"
    },
    ...
  }
}
```

### <span data-ttu-id="e121b-253">< "Konfigurowanie ramię" ></a>parametry szablonu Konfigurowanie Menedżera zasobów</span><span class="sxs-lookup"><span data-stu-id="e121b-253"><a "configure-arm" ></a>Configure Resource Manager template parameters</span></span>
<!--- Loc Comment: It seems that <a "configure-arm" > must be replaced with <a name="configure-arm"></a> since hello link seems not toobe redirecting correctly --->
<span data-ttu-id="e121b-254">Na koniec użyj hello wartości danych wyjściowych z magazynu kluczy hello i pliku parametrów hello toopopulate poleceń programu PowerShell usługi Azure AD:</span><span class="sxs-lookup"><span data-stu-id="e121b-254">Finally, use hello output values from hello key vault and Azure AD PowerShell commands toopopulate hello parameters file:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        ...
        "clusterCertificateStoreValue": {
            "value": "My"
        },
        "clusterCertificateThumbprint": {
            "value": "<thumbprint>"
        },
        "clusterCertificateUrlValue": {
            "value": "https://myvault.vault.azure.net:443/secrets/myclustercert/4d087088df974e869f1c0978cb100e47"
        },
        "applicationCertificateStorevalue": {
            "value": "My"
        },
        "applicationCertificateUrlValue": {
            "value": "https://myvault.vault.azure.net:443/secrets/myapplicationcert/2e035058ae274f869c4d0348ca100f08"
        },
        "sourceVaultvalue": {
            "value": "/subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault"
        },
        "aadTenantId": {
            "value": "<guid>"
        },
        "aadClusterApplicationId": {
            "value": "<guid>"
        },
        "aadClientApplicationId": {
            "value": "<guid>"
        },
        ...
    }
}
```
<span data-ttu-id="e121b-255">W tym momencie powinny mieć następujące elementy w miejscu hello:</span><span class="sxs-lookup"><span data-stu-id="e121b-255">At this point, you should have hello following elements in place:</span></span>

* <span data-ttu-id="e121b-256">Grupa zasobów magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="e121b-256">Key vault resource group</span></span>
  * <span data-ttu-id="e121b-257">Magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="e121b-257">Key vault</span></span>
  * <span data-ttu-id="e121b-258">Certyfikat uwierzytelniania serwera klastra</span><span class="sxs-lookup"><span data-stu-id="e121b-258">Cluster server authentication certificate</span></span>
  * <span data-ttu-id="e121b-259">Certyfikat Szyfrowanie danych</span><span class="sxs-lookup"><span data-stu-id="e121b-259">Data encipherment certificate</span></span>
* <span data-ttu-id="e121b-260">Dzierżawy usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e121b-260">Azure Active Directory tenant</span></span>
  * <span data-ttu-id="e121b-261">Aplikacji usługi Azure AD dla zarządzania opartego na sieci web i Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="e121b-261">Azure AD application for web-based management and Service Fabric Explorer</span></span>
  * <span data-ttu-id="e121b-262">Aplikacji do zarządzania klientami z usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e121b-262">Azure AD application for native client management</span></span>
  * <span data-ttu-id="e121b-263">Użytkownicy i przypisane im role</span><span class="sxs-lookup"><span data-stu-id="e121b-263">Users and their assigned roles</span></span>
* <span data-ttu-id="e121b-264">Szablon usługi Resource Manager klastra sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="e121b-264">Service Fabric cluster Resource Manager template</span></span>
  * <span data-ttu-id="e121b-265">Skonfigurowanych za pomocą magazynu kluczy certyfikatów</span><span class="sxs-lookup"><span data-stu-id="e121b-265">Certificates configured through key vault</span></span>
  * <span data-ttu-id="e121b-266">Usługa Azure Active Directory skonfigurowane</span><span class="sxs-lookup"><span data-stu-id="e121b-266">Azure Active Directory configured</span></span>

<span data-ttu-id="e121b-267">powitania po diagram ilustruje, gdy magazyn kluczy i konfiguracji usługi Azure AD mieści się w szablonie usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e121b-267">hello following diagram illustrates where your key vault and Azure AD configuration fit into your Resource Manager template.</span></span>

![Menedżer zasobów zależności mapy][cluster-security-arm-dependency-map]

## <a name="create-hello-cluster"></a><span data-ttu-id="e121b-269">Tworzenie klastra hello</span><span class="sxs-lookup"><span data-stu-id="e121b-269">Create hello cluster</span></span>
<span data-ttu-id="e121b-270">Wszystko jest teraz gotowy toocreate hello klastra przy użyciu [wdrażania szablonu zasobów platformy Azure][resource-group-template-deploy].</span><span class="sxs-lookup"><span data-stu-id="e121b-270">You are now ready toocreate hello cluster by using [Azure resource template deployment][resource-group-template-deploy].</span></span>

#### <a name="test-it"></a><span data-ttu-id="e121b-271">należy przeprowadzić test</span><span class="sxs-lookup"><span data-stu-id="e121b-271">Test it</span></span>
<span data-ttu-id="e121b-272">Należy użyć szablonu usługi Resource Manager powitania po tootest polecenia programu PowerShell z pliku parametrów:</span><span class="sxs-lookup"><span data-stu-id="e121b-272">Use hello following PowerShell command tootest your Resource Manager template with a parameters file:</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

#### <a name="deploy-it"></a><span data-ttu-id="e121b-273">Wdróż go</span><span class="sxs-lookup"><span data-stu-id="e121b-273">Deploy it</span></span>
<span data-ttu-id="e121b-274">Przeszedł test szablonu usługi Resource Manager hello, należy użyć powitania po toodeploy polecenia programu PowerShell do szablonu usługi Resource Manager z pliku parametrów:</span><span class="sxs-lookup"><span data-stu-id="e121b-274">If hello Resource Manager template test passes, use hello following PowerShell command toodeploy your Resource Manager template with a parameters file:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

<a name="assign-roles"></a>

## <a name="assign-users-tooroles"></a><span data-ttu-id="e121b-275">Przypisywanie użytkowników tooroles</span><span class="sxs-lookup"><span data-stu-id="e121b-275">Assign users tooroles</span></span>
<span data-ttu-id="e121b-276">Po utworzeniu toorepresent aplikacji hello klastra, przypisywanie użytkownikom ról toohello obsługiwane przez usługi Service Fabric: tylko do odczytu i administratora. Można przypisać role hello za pomocą hello [klasycznego portalu Azure][azure-classic-portal].</span><span class="sxs-lookup"><span data-stu-id="e121b-276">After you have created hello applications toorepresent your cluster, assign your users toohello roles supported by Service Fabric: read-only and admin. You can assign hello roles by using hello [Azure classic portal][azure-classic-portal].</span></span>

1. <span data-ttu-id="e121b-277">W hello portalu Azure, przejdź do pozycji tooyour dzierżawy, a następnie wybierz **aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="e121b-277">In hello Azure portal, go tooyour tenant, and then select **Applications**.</span></span>
2. <span data-ttu-id="e121b-278">Wybierz aplikację sieci web hello mający nazwę jak `myTestCluster_Cluster`.</span><span class="sxs-lookup"><span data-stu-id="e121b-278">Select hello web application, which has a name like `myTestCluster_Cluster`.</span></span>
3. <span data-ttu-id="e121b-279">Kliknij przycisk hello **użytkowników** kartę.</span><span class="sxs-lookup"><span data-stu-id="e121b-279">Click hello **Users** tab.</span></span>
4. <span data-ttu-id="e121b-280">Wybierz tooassign użytkownika, a następnie kliknij przycisk hello **przypisać** przycisk u dołu hello hello ekranu.</span><span class="sxs-lookup"><span data-stu-id="e121b-280">Select a user tooassign, and then click hello **Assign** button at hello bottom of hello screen.</span></span>

    ![Przypisywanie użytkowników tooroles przycisku][assign-users-to-roles-button]
5. <span data-ttu-id="e121b-282">Wybierz hello roli tooassign toohello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e121b-282">Select hello role tooassign toohello user.</span></span>

    ![Okno dialogowe "Przypisywanie użytkowników"][assign-users-to-roles-dialog]

> [!NOTE]
> <span data-ttu-id="e121b-284">Aby uzyskać więcej informacji na temat ról w sieci szkieletowej usług, zobacz [kontroli dostępu opartej na rolach dla klientów usługi sieć szkieletowa](service-fabric-cluster-security-roles.md).</span><span class="sxs-lookup"><span data-stu-id="e121b-284">For more information about roles in Service Fabric, see [Role-based access control for Service Fabric clients](service-fabric-cluster-security-roles.md).</span></span>
>
>

 <a name="secure-linux-clusters"></a>
 <!--- Loc Comment: It seems that letter S in cluster was missing, which caused hello wrong redirection of hello link --->

## <a name="create-secure-clusters-on-linux"></a><span data-ttu-id="e121b-285">Tworzenie bezpiecznych klastrów w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="e121b-285">Create secure clusters on Linux</span></span>
<span data-ttu-id="e121b-286">proces hello toomake jest łatwiejsze, firma Microsoft umieściła [skryptu Pomocnika](http://github.com/ChackDan/Service-Fabric/tree/master/Scripts/CertUpload4Linux).</span><span class="sxs-lookup"><span data-stu-id="e121b-286">toomake hello process easier, we have provided a [helper script](http://github.com/ChackDan/Service-Fabric/tree/master/Scripts/CertUpload4Linux).</span></span> <span data-ttu-id="e121b-287">Przed użyciem tego skryptu pomocnika, upewnij się, że masz już Azure interfejsu wiersza polecenia (CLI) zainstalowany i znajduje się w ścieżce.</span><span class="sxs-lookup"><span data-stu-id="e121b-287">Before you use this helper script, ensure that you already have Azure command-line interface (CLI) installed, and it is in your path.</span></span> <span data-ttu-id="e121b-288">Upewnij się, że skrypt hello ma tooexecute uprawnienia, uruchamiając `chmod +x cert_helper.py` po ją pobrać.</span><span class="sxs-lookup"><span data-stu-id="e121b-288">Make sure that hello script has permissions tooexecute by running `chmod +x cert_helper.py` after downloading it.</span></span> <span data-ttu-id="e121b-289">pierwszym krokiem Hello jest toosign w tooyour konto platformy Azure przy użyciu interfejsu wiersza polecenia z hello `azure login` polecenia.</span><span class="sxs-lookup"><span data-stu-id="e121b-289">hello first step is toosign in tooyour Azure account by using CLI with hello `azure login` command.</span></span> <span data-ttu-id="e121b-290">Po zalogowaniu się tooyour konto platformy Azure, użyj hello pomocnika skryptu z urzędu certyfikacji certyfikatu z podpisem, jako powitania po pokazuje polecenia:</span><span class="sxs-lookup"><span data-stu-id="e121b-290">After signing in tooyour Azure account, use hello helper script with your CA signed certificate, as hello following command shows:</span></span>

```sh
./cert_helper.py [-h] CERT_TYPE [-ifile INPUT_CERT_FILE] [-sub SUBSCRIPTION_ID] [-rgname RESOURCE_GROUP_NAME] [-kv KEY_VAULT_NAME] [-sname CERTIFICATE_NAME] [-l LOCATION] [-p PASSWORD]
```

<span data-ttu-id="e121b-291">Parametr - ifile Hello może zająć plik pfx lub plik PEM jako dane wejściowe z hello typ certyfikatu (pfx lub pem lub ss, jeśli certyfikat z podpisem własnym).</span><span class="sxs-lookup"><span data-stu-id="e121b-291">hello -ifile parameter can take a .pfx file or a .pem file as input, with hello certificate type (pfx or pem, or ss if it is a self-signed certificate).</span></span>
<span data-ttu-id="e121b-292">Witaj parametr -h drukowania hello tekst pomocy.</span><span class="sxs-lookup"><span data-stu-id="e121b-292">hello parameter -h prints out hello help text.</span></span>


<span data-ttu-id="e121b-293">To polecenie zwraca następujące trzy ciągi jako dane wyjściowe hello hello:</span><span class="sxs-lookup"><span data-stu-id="e121b-293">This command returns hello following three strings as hello output:</span></span>

* <span data-ttu-id="e121b-294">SourceVaultID, który jest identyfikator hello hello nowe KeyVault ResourceGroup on utworzony</span><span class="sxs-lookup"><span data-stu-id="e121b-294">SourceVaultID, which is hello ID for hello new KeyVault ResourceGroup it created for you</span></span>
* <span data-ttu-id="e121b-295">CertificateUrl do uzyskiwania dostępu do certyfikatu hello</span><span class="sxs-lookup"><span data-stu-id="e121b-295">CertificateUrl for accessing hello certificate</span></span>
* <span data-ttu-id="e121b-296">CertificateThumbprint, który jest używany do uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="e121b-296">CertificateThumbprint, which is used for authentication</span></span>

<span data-ttu-id="e121b-297">Witaj poniższy przykład pokazuje, jak toouse hello polecenia:</span><span class="sxs-lookup"><span data-stu-id="e121b-297">hello following example shows how toouse hello command:</span></span>

```sh
./cert_helper.py pfx -sub "fffffff-ffff-ffff-ffff-ffffffffffff"  -rgname "mykvrg" -kv "mykevname" -ifile "/home/test/cert.pfx" -sname "mycert" -l "East US" -p "pfxtest"
```
<span data-ttu-id="e121b-298">Wykonywanie hello poprzedzających daje polecenie hello trzy ciągi w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="e121b-298">Executing hello preceding command gives you hello three strings as follows:</span></span>

```sh
SourceVault: /subscriptions/fffffff-ffff-ffff-ffff-ffffffffffff/resourceGroups/mykvrg/providers/Microsoft.KeyVault/vaults/mykvname
CertificateUrl: https://myvault.vault.azure.net/secrets/mycert/00000000000000000000000000000000
CertificateThumbprint: 0xfffffffffffffffffffffffffffffffffffffffff
```

<span data-ttu-id="e121b-299">Nazwa podmiotu certyfikatu Hello musi odpowiadać domeny hello używanie klastra usługi sieć szkieletowa hello tooaccess.</span><span class="sxs-lookup"><span data-stu-id="e121b-299">hello certificate's subject name must match hello domain that you use tooaccess hello Service Fabric cluster.</span></span> <span data-ttu-id="e121b-300">To dopasowanie jest wymagana tooprovide SSL dla punktów końcowych zarządzania HTTPS hello klastra i Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="e121b-300">This match is required tooprovide an SSL for hello cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="e121b-301">Nie można uzyskać certyfikatu SSL z urzędu certyfikacji dla hello `.cloudapp.azure.com` domeny.</span><span class="sxs-lookup"><span data-stu-id="e121b-301">You cannot obtain an SSL certificate from a CA for hello `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="e121b-302">Należy uzyskać niestandardowej nazwy domeny dla klastra.</span><span class="sxs-lookup"><span data-stu-id="e121b-302">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="e121b-303">Podczas żądania certyfikatu z urzędu certyfikacji, hello nazwa podmiotu certyfikatu musi odpowiadać hello niestandardowej nazwy domeny używanej dla klastra.</span><span class="sxs-lookup"><span data-stu-id="e121b-303">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name that you use for your cluster.</span></span>

<span data-ttu-id="e121b-304">Te nazwy podmiotu są hello wpisy toocreate bezpiecznego klastra sieci szkieletowej usług (bez usługi Azure AD), zgodnie z opisem w [parametrów szablonu usługi Resource Manager skonfigurować](#configure-arm).</span><span class="sxs-lookup"><span data-stu-id="e121b-304">These subject names are hello entries you need toocreate a secure Service Fabric cluster (without Azure AD), as described at [Configure Resource Manager template parameters](#configure-arm).</span></span> <span data-ttu-id="e121b-305">Możesz połączyć toohello bezpiecznego klastra, wykonując instrukcje hello [uwierzytelniania klientów dostępu tooa klastra](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="e121b-305">You can connect toohello secure cluster by following hello instructions for [authenticating client access tooa cluster](service-fabric-connect-to-secure-cluster.md).</span></span> <span data-ttu-id="e121b-306">Klastry z systemem Linux w wersji zapoznawczej nie obsługują uwierzytelniania usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e121b-306">Linux preview clusters do not support Azure AD authentication.</span></span> <span data-ttu-id="e121b-307">Można przypisać role administratora, jak i klienta, zgodnie z opisem w hello [przypisać role toousers](#assign-roles) sekcji.</span><span class="sxs-lookup"><span data-stu-id="e121b-307">You can assign admin and client roles as described in hello [Assign roles toousers](#assign-roles) section.</span></span> <span data-ttu-id="e121b-308">Po określeniu ról administratora, jak i klienta dla systemu Linux klastra w wersji zapoznawczej, masz tooprovide odciski palców certyfikatów do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="e121b-308">When you specify admin and client roles for a Linux preview cluster, you have tooprovide certificate thumbprints for authentication.</span></span> <span data-ttu-id="e121b-309">(Nie zostanie określona nazwa podmiotu hello, ponieważ nie weryfikacji łańcucha lub odwołania jest wykonywane w tej wersji zapoznawczej.)</span><span class="sxs-lookup"><span data-stu-id="e121b-309">(You do not provide hello subject name, because no chain validation or revocation is being performed in this preview release.)</span></span>

<span data-ttu-id="e121b-310">Jeśli chcesz toouse certyfikatu z podpisem własnym do testowania, możesz użyć hello tego samego toogenerate skryptu jeden.</span><span class="sxs-lookup"><span data-stu-id="e121b-310">If you want toouse a self-signed certificate for testing, you can use hello same script toogenerate one.</span></span> <span data-ttu-id="e121b-311">Można następnie przekaż magazynu kluczy tooyour certyfikatu hello zapewniając flagi hello `ss` zamiast podanie certyfikatu hello nazwy ścieżki i certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="e121b-311">You can then upload hello certificate tooyour key vault by providing hello flag `ss` instead of providing hello certificate path and certificate name.</span></span> <span data-ttu-id="e121b-312">Na przykład zobacz hello następujące polecenia umożliwiające tworzenie i przekazywanie certyfikatu z podpisem własnym:</span><span class="sxs-lookup"><span data-stu-id="e121b-312">For example, see hello following command for creating and uploading a self-signed certificate:</span></span>

```sh
./cert_helper.py ss -rgname "mykvrg" -sub "fffffff-ffff-ffff-ffff-ffffffffffff" -kv "mykevname"   -sname "mycert" -l "East US" -p "selftest" -subj "mytest.eastus.cloudapp.net"
```
<span data-ttu-id="e121b-313">To polecenie zwraca hello tego samego trzy ciągi: SourceVault, CertificateUrl i CertificateThumbprint.</span><span class="sxs-lookup"><span data-stu-id="e121b-313">This command returns hello same three strings: SourceVault, CertificateUrl, and CertificateThumbprint.</span></span> <span data-ttu-id="e121b-314">Następnie można toocreate ciągów hello bezpiecznego klastra systemu Linux i z lokalizacji, gdzie jest umieszczony certyfikat z podpisem własnym hello.</span><span class="sxs-lookup"><span data-stu-id="e121b-314">You can then use hello strings toocreate both a secure Linux cluster and a location where hello self-signed certificate is placed.</span></span> <span data-ttu-id="e121b-315">Należy hello certyfikatu z podpisem własnym tooconnect toohello klastra.</span><span class="sxs-lookup"><span data-stu-id="e121b-315">You need hello self-signed certificate tooconnect toohello cluster.</span></span> <span data-ttu-id="e121b-316">Możesz połączyć toohello bezpiecznego klastra, wykonując instrukcje hello [uwierzytelniania klientów dostępu tooa klastra](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="e121b-316">You can connect toohello secure cluster by following hello instructions for [authenticating client access tooa cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

<span data-ttu-id="e121b-317">Nazwa podmiotu certyfikatu Hello musi odpowiadać domeny hello używanie klastra usługi sieć szkieletowa hello tooaccess.</span><span class="sxs-lookup"><span data-stu-id="e121b-317">hello certificate's subject name must match hello domain that you use tooaccess hello Service Fabric cluster.</span></span> <span data-ttu-id="e121b-318">To dopasowanie jest wymagana tooprovide SSL dla punktów końcowych zarządzania HTTPS hello klastra i Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="e121b-318">This match is required tooprovide an SSL for hello cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="e121b-319">Nie można uzyskać certyfikatu SSL z urzędu certyfikacji dla hello `.cloudapp.azure.com` domeny.</span><span class="sxs-lookup"><span data-stu-id="e121b-319">You cannot obtain an SSL certificate from a CA for hello `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="e121b-320">Należy uzyskać niestandardowej nazwy domeny dla klastra.</span><span class="sxs-lookup"><span data-stu-id="e121b-320">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="e121b-321">Podczas żądania certyfikatu z urzędu certyfikacji, hello nazwa podmiotu certyfikatu musi odpowiadać hello niestandardowej nazwy domeny używanej dla klastra.</span><span class="sxs-lookup"><span data-stu-id="e121b-321">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name that you use for your cluster.</span></span>

<span data-ttu-id="e121b-322">Możesz wpisać parametry hello ze skryptu pomocnika hello w hello portalu Azure, zgodnie z opisem w hello [tworzenia klastra w portalu Azure hello](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal) sekcji.</span><span class="sxs-lookup"><span data-stu-id="e121b-322">You can fill hello parameters from hello helper script in hello Azure portal, as described in hello [Create a cluster in hello Azure portal](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal) section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e121b-323">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e121b-323">Next steps</span></span>
<span data-ttu-id="e121b-324">W tym momencie masz bezpiecznego klaster o udostępnienie uwierzytelniania zarządzania usługą Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e121b-324">At this point, you have a secure cluster with Azure Active Directory providing management authentication.</span></span> <span data-ttu-id="e121b-325">Następnie [połączenia klastra tooyour](service-fabric-connect-to-secure-cluster.md) i Dowiedz się, jak za[Zarządzanie klucze tajne aplikacji](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="e121b-325">Next, [connect tooyour cluster](service-fabric-connect-to-secure-cluster.md) and learn how too[manage application secrets](service-fabric-application-secret-management.md).</span></span>

## <a name="troubleshoot-setting-up-azure-active-directory-for-client-authentication"></a><span data-ttu-id="e121b-326">Rozwiązywanie problemów z Konfigurowanie usługi Azure Active Directory do uwierzytelniania klientów</span><span class="sxs-lookup"><span data-stu-id="e121b-326">Troubleshoot setting up Azure Active Directory for client authentication</span></span>
<span data-ttu-id="e121b-327">Jeśli napotkasz problem podczas podczas konfigurowania usługi Azure AD do uwierzytelniania klientów, przejrzyj hello potencjalne rozwiązania w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="e121b-327">If you run into an issue while you're setting up Azure AD for client authentication, review hello potential solutions in this section.</span></span>

### <a name="service-fabric-explorer-prompts-you-tooselect-a-certificate"></a><span data-ttu-id="e121b-328">Service Fabric Explorer monituje tooselect certyfikatu</span><span class="sxs-lookup"><span data-stu-id="e121b-328">Service Fabric Explorer prompts you tooselect a certificate</span></span>
#### <a name="problem"></a><span data-ttu-id="e121b-329">Problem</span><span class="sxs-lookup"><span data-stu-id="e121b-329">Problem</span></span>
<span data-ttu-id="e121b-330">Po zalogowaniu pomyślnie tooAzure AD w narzędziu Service Fabric Explorer przeglądarki hello zwraca toohello strony głównej, ale komunikat monituje tooselect certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="e121b-330">After you sign in successfully tooAzure AD in Service Fabric Explorer, hello browser returns toohello home page but a message prompts you tooselect a certificate.</span></span>

![Wybierz certyfikat SFX w oknie dialogowym][sfx-select-certificate-dialog]

#### <a name="reason"></a><span data-ttu-id="e121b-332">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="e121b-332">Reason</span></span>
<span data-ttu-id="e121b-333">Hello użytkownika nie jest przypisana rola hello aplikacji klastra usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e121b-333">hello user isn’t assigned a role in hello Azure AD cluster application.</span></span> <span data-ttu-id="e121b-334">W związku z tym niepowodzenia uwierzytelniania usługi Azure AD w klastrze usługi sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="e121b-334">Thus, Azure AD authentication fails on Service Fabric cluster.</span></span> <span data-ttu-id="e121b-335">Service Fabric Explorer powraca toocertificate uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="e121b-335">Service Fabric Explorer falls back toocertificate authentication.</span></span>

#### <a name="solution"></a><span data-ttu-id="e121b-336">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="e121b-336">Solution</span></span>
<span data-ttu-id="e121b-337">Wykonaj hello instrukcje dotyczące konfigurowania usługi Azure AD i przypisz role użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e121b-337">Follow hello instructions for setting up Azure AD, and assign user roles.</span></span> <span data-ttu-id="e121b-338">Ponadto zalecamy włączenie "Użytkownika przypisania tooaccess wymagana aplikacja" jako `SetupApplications.ps1` jest.</span><span class="sxs-lookup"><span data-stu-id="e121b-338">Also, we recommend that you turn on “User assignment required tooaccess app,” as `SetupApplications.ps1` does.</span></span>

### <a name="connection-with-powershell-fails-with-an-error-hello-specified-credentials-are-invalid"></a><span data-ttu-id="e121b-339">Połączenie przy użyciu programu PowerShell zakończy się niepowodzeniem z powodu błędu: "hello określone poświadczenia są nieprawidłowe"</span><span class="sxs-lookup"><span data-stu-id="e121b-339">Connection with PowerShell fails with an error: "hello specified credentials are invalid"</span></span>
#### <a name="problem"></a><span data-ttu-id="e121b-340">Problem</span><span class="sxs-lookup"><span data-stu-id="e121b-340">Problem</span></span>
<span data-ttu-id="e121b-341">Gdy używasz programu PowerShell tooconnect toohello klastra przy użyciu trybu zabezpieczeń "Usługi AzureActiveDirectory", po zalogowaniu się pomyślnie tooAzure AD hello połączenia zakończy się niepowodzeniem z powodu błędu: "hello określone poświadczenia są nieprawidłowe."</span><span class="sxs-lookup"><span data-stu-id="e121b-341">When you use PowerShell tooconnect toohello cluster by using “AzureActiveDirectory” security mode, after you sign in successfully tooAzure AD, hello connection fails with an error: "hello specified credentials are invalid."</span></span>

#### <a name="solution"></a><span data-ttu-id="e121b-342">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="e121b-342">Solution</span></span>
<span data-ttu-id="e121b-343">To rozwiązanie jest powitalne identyczny hello poprzedzających jeden.</span><span class="sxs-lookup"><span data-stu-id="e121b-343">This solution is hello same as hello preceding one.</span></span>

### <a name="service-fabric-explorer-returns-a-failure-when-you-sign-in-aadsts50011"></a><span data-ttu-id="e121b-344">Service Fabric Explorer zwróci błąd podczas logowania: "AADSTS50011"</span><span class="sxs-lookup"><span data-stu-id="e121b-344">Service Fabric Explorer returns a failure when you sign in: "AADSTS50011"</span></span>
#### <a name="problem"></a><span data-ttu-id="e121b-345">Problem</span><span class="sxs-lookup"><span data-stu-id="e121b-345">Problem</span></span>
<span data-ttu-id="e121b-346">Podczas próby toosign w tooAzure AD w narzędziu Service Fabric Explorer strony hello zwraca błąd: "AADSTS50011: hello adres zwrotny &lt;adres url&gt; jest niezgodny z adresów odpowiedzi hello skonfigurowanych dla aplikacji hello: &lt;guid&gt;."</span><span class="sxs-lookup"><span data-stu-id="e121b-346">When you try toosign in tooAzure AD in Service Fabric Explorer, hello page returns a failure: "AADSTS50011: hello reply address &lt;url&gt; does not match hello reply addresses configured for hello application: &lt;guid&gt;."</span></span>

![Adres zwrotny SFX jest niezgodny.][sfx-reply-address-not-match]

#### <a name="reason"></a><span data-ttu-id="e121b-348">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="e121b-348">Reason</span></span>
<span data-ttu-id="e121b-349">Witaj aplikacji klastra (sieć web), która reprezentuje Eksploratora usługi sieć szkieletowa podejmuje tooauthenticate w usłudze Azure AD, a jako część żądania hello zapewnia zwrotny adres URL przekierowania hello.</span><span class="sxs-lookup"><span data-stu-id="e121b-349">hello cluster (web) application that represents Service Fabric Explorer attempts tooauthenticate against Azure AD, and as part of hello request it provides hello redirect return URL.</span></span> <span data-ttu-id="e121b-350">Ale hello adres URL nie jest wymieniony w aplikacji hello Azure AD **adres URL odpowiedzi** listy.</span><span class="sxs-lookup"><span data-stu-id="e121b-350">But hello URL is not listed in hello Azure AD application **REPLY URL** list.</span></span>

#### <a name="solution"></a><span data-ttu-id="e121b-351">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="e121b-351">Solution</span></span>
<span data-ttu-id="e121b-352">Na powitania **Konfiguruj** kartę hello klastra aplikacji (aplikacji sieci web), należy dodać hello adresu URL Service Fabric Explorer toohello **adres URL odpowiedzi** listy lub Zastąp hello elementów na liście hello.</span><span class="sxs-lookup"><span data-stu-id="e121b-352">On hello **Configure** tab of hello cluster (web) application, add hello URL of Service Fabric Explorer toohello **REPLY URL** list or replace one of hello items in hello list.</span></span> <span data-ttu-id="e121b-353">Po zakończeniu zapisz zmianę.</span><span class="sxs-lookup"><span data-stu-id="e121b-353">When you have finished, save your change.</span></span>

![Adres url odpowiedzi aplikacji sieci Web][web-application-reply-url]

### <a name="connect-hello-cluster-by-using-azure-ad-authentication-via-powershell"></a><span data-ttu-id="e121b-355">Połącz hello klastra przy użyciu uwierzytelniania usługi Azure AD za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="e121b-355">Connect hello cluster by using Azure AD authentication via PowerShell</span></span>
<span data-ttu-id="e121b-356">Witaj tooconnect klastra sieci szkieletowej usług Użyj hello poniższy przykład polecenia programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="e121b-356">tooconnect hello Service Fabric cluster, use hello following PowerShell command example:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <endpoint> -KeepAliveIntervalInSec 10 -AzureActiveDirectory -ServerCertThumbprint <thumbprint>
```

<span data-ttu-id="e121b-357">toolearn temat hello Connect-ServiceFabricCluster polecenia cmdlet, zobacz [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx).</span><span class="sxs-lookup"><span data-stu-id="e121b-357">toolearn about hello Connect-ServiceFabricCluster cmdlet, see [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx).</span></span>

### <a name="can-i-reuse-hello-same-azure-ad-tenant-in-multiple-clusters"></a><span data-ttu-id="e121b-358">Czy można ponownie użyć dzierżawy hello tej samej usługi Azure AD w wielu klastrach?</span><span class="sxs-lookup"><span data-stu-id="e121b-358">Can I reuse hello same Azure AD tenant in multiple clusters?</span></span>
<span data-ttu-id="e121b-359">Tak.</span><span class="sxs-lookup"><span data-stu-id="e121b-359">Yes.</span></span> <span data-ttu-id="e121b-360">Należy jednak pamiętać tooadd hello adresu URL Service Fabric Explorer tooyour klastra (sieć web) aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e121b-360">But remember tooadd hello URL of Service Fabric Explorer tooyour cluster (web) application.</span></span> <span data-ttu-id="e121b-361">W przeciwnym razie Eksploratora usługi sieć szkieletowa nie działa.</span><span class="sxs-lookup"><span data-stu-id="e121b-361">Otherwise, Service Fabric Explorer doesn’t work.</span></span>

### <a name="why-do-i-still-need-a-server-certificate-while-azure-ad-is-enabled"></a><span data-ttu-id="e121b-362">Dlaczego nadal należy certyfikat serwera po włączeniu usługi Azure AD?</span><span class="sxs-lookup"><span data-stu-id="e121b-362">Why do I still need a server certificate while Azure AD is enabled?</span></span>
<span data-ttu-id="e121b-363">Klienta fabricclient z rolą i FabricGateway wykonać uwierzytelnianie wzajemne.</span><span class="sxs-lookup"><span data-stu-id="e121b-363">FabricClient and FabricGateway perform a mutual authentication.</span></span> <span data-ttu-id="e121b-364">Podczas uwierzytelniania usługi Azure AD integracji z usługą Azure AD zapewnia klienta serwera toohello tożsamości i tożsamości serwera hello tooverify używany jest certyfikat serwera hello.</span><span class="sxs-lookup"><span data-stu-id="e121b-364">During Azure AD authentication, Azure AD integration provides a client identity toohello server, and hello server certificate is used tooverify hello server identity.</span></span> <span data-ttu-id="e121b-365">Aby uzyskać więcej informacji na temat sieci szkieletowej usług certyfikatów, zobacz [certyfikatów X.509 i sieci szkieletowej usług][x509-certificates-and-service-fabric].</span><span class="sxs-lookup"><span data-stu-id="e121b-365">For more information about Service Fabric certificates, see [X.509 certificates and Service Fabric][x509-certificates-and-service-fabric].</span></span>

<!-- Links -->
[azure-powershell]:https://azure.microsoft.com/documentation/articles/powershell-install-configure/
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[aad-graph-api-docs]:https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog
[azure-classic-portal]: https://manage.windowsazure.com
[service-fabric-rp-helpers]: https://github.com/ChackDan/Service-Fabric/tree/master/Scripts/ServiceFabricRPHelpers
[service-fabric-cluster-security]: service-fabric-cluster-security.md
[active-directory-howto-tenant]: ../active-directory/active-directory-howto-tenant.md
[service-fabric-visualizing-your-cluster]: service-fabric-visualizing-your-cluster.md
[service-fabric-manage-application-in-visual-studio]: service-fabric-manage-application-in-visual-studio.md
[sf-aad-ps-script-download]:http://servicefabricsdkstorage.blob.core.windows.net/publicrelease/MicrosoftAzureServiceFabric-AADHelpers.zip
[azure-quickstart-templates]: https://github.com/Azure/azure-quickstart-templates
[service-fabric-secure-cluster-5-node-1-nodetype]: https://github.com/Azure/azure-quickstart-templates/blob/master/service-fabric-secure-cluster-5-node-1-nodetype/
[resource-group-template-deploy]: https://azure.microsoft.com/documentation/articles/resource-group-template-deploy/
[x509-certificates-and-service-fabric]: service-fabric-cluster-security.md#x509-certificates-and-service-fabric

<!-- Images -->
[cluster-security-arm-dependency-map]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-arm-dependency-map.png
[cluster-security-cert-installation]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-cert-installation.png
[assign-users-to-roles-button]: ./media/service-fabric-cluster-creation-via-arm/assign-users-to-roles-button.png
[assign-users-to-roles-dialog]: ./media/service-fabric-cluster-creation-via-arm/assign-users-to-roles.png
[sfx-select-certificate-dialog]: ./media/service-fabric-cluster-creation-via-arm/sfx-select-certificate-dialog.png
[sfx-reply-address-not-match]: ./media/service-fabric-cluster-creation-via-arm/sfx-reply-address-not-match.png
[web-application-reply-url]: ./media/service-fabric-cluster-creation-via-arm/web-application-reply-url.png

