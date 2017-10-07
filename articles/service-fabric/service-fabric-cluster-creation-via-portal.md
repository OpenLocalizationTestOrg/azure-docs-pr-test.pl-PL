---
title: "aaaCreate sieci szkieletowej usług dla klastra w hello portalu Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak hello tooset zapasowej bezpiecznego klastra sieci szkieletowej usług za pomocą usługi Azure w portalu Azure i usługi Azure Key Vault."
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: vturecek
ms.assetid: 426c3d13-127a-49eb-a54c-6bde7c87a83b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/21/2017
ms.author: chackdan
ms.openlocfilehash: 045f71b491260e741ce7a54a75c440e1b33059a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster-in-azure-using-hello-azure-portal"></a><span data-ttu-id="dda6d-103">Tworzenie klastra sieci szkieletowej usług na platformie Azure przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="dda6d-103">Create a Service Fabric cluster in Azure using hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="dda6d-104">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="dda6d-104">Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
> * [<span data-ttu-id="dda6d-105">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="dda6d-105">Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
> 
> 

<span data-ttu-id="dda6d-106">Jest to przewodnik krok po kroku, który przeprowadzi Cię przez kolejne hello procedurę konfigurowania klastra sieci szkieletowej usług bezpiecznej platformie Azure przy użyciu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="dda6d-106">This is a step-by-step guide that walks you through hello steps of setting up a secure Service Fabric cluster in Azure using hello Azure portal.</span></span> <span data-ttu-id="dda6d-107">Ten przewodnik przeprowadzi Cię przez hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="dda6d-107">This guide walks you through hello following steps:</span></span>

* <span data-ttu-id="dda6d-108">Konfigurowanie usługi Key Vault toomanage klucze dla zabezpieczenia klastra.</span><span class="sxs-lookup"><span data-stu-id="dda6d-108">Set up Key Vault toomanage keys for cluster security.</span></span>
* <span data-ttu-id="dda6d-109">Tworzenie klastra zabezpieczonych na platformie Azure za pośrednictwem hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="dda6d-109">Create a secured cluster in Azure through hello Azure portal.</span></span>
* <span data-ttu-id="dda6d-110">Uwierzytelnianie za pomocą certyfikatów Administratorzy.</span><span class="sxs-lookup"><span data-stu-id="dda6d-110">Authenticate administrators using certificates.</span></span>

> [!NOTE]
> <span data-ttu-id="dda6d-111">Dla bardziej zaawansowanych opcji zabezpieczeń, takich jak uwierzytelnianie użytkowników w usłudze Azure Active Directory oraz konfigurowania certyfikatów do zabezpieczenia aplikacji [tworzenia klastra przy użyciu usługi Azure Resource Manager][create-cluster-arm].</span><span class="sxs-lookup"><span data-stu-id="dda6d-111">For more advanced security options, such as user authentication with Azure Active Directory and setting up certificates for application security, [create your cluster using Azure Resource Manager][create-cluster-arm].</span></span>
> 
> 

<span data-ttu-id="dda6d-112">Bezpieczne klaster jest klastrem uniemożliwiający operacji toomanagement nieautoryzowanym dostępem, w tym wdrażanie, uaktualnianie i usuwanie aplikacji, usług i danych hello, które zawierają.</span><span class="sxs-lookup"><span data-stu-id="dda6d-112">A secure cluster is a cluster that prevents unauthorized access toomanagement operations, which includes deploying, upgrading, and deleting applications, services, and hello data they contain.</span></span> <span data-ttu-id="dda6d-113">Niezabezpieczone klaster jest klastrem informujący o tym, czy każdy połączyć tooat w dowolnym momencie i wykonywać operacje zarządzania.</span><span class="sxs-lookup"><span data-stu-id="dda6d-113">An unsecure cluster is a cluster that anyone can connect tooat any time and perform management operations.</span></span> <span data-ttu-id="dda6d-114">Chociaż jest to możliwe toocreate niezabezpieczone klastra, jest **zdecydowanie zalecane toocreate bezpiecznego klastra**.</span><span class="sxs-lookup"><span data-stu-id="dda6d-114">Although it is possible toocreate an unsecure cluster, it is **highly recommended toocreate a secure cluster**.</span></span> <span data-ttu-id="dda6d-115">Niezabezpieczone klastra **nie można zabezpieczyć później** — należy utworzyć nowy klaster.</span><span class="sxs-lookup"><span data-stu-id="dda6d-115">An unsecure cluster **cannot be secured later** - a new cluster must be created.</span></span>

<span data-ttu-id="dda6d-116">Pojęcia dotyczące Hello są hello identyczne tworzenia bezpiecznych klastrów, czy klastry hello są klastry z systemem Linux lub klastry z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="dda6d-116">hello concepts are hello same for creating secure clusters, whether hello clusters are Linux clusters or Windows clusters.</span></span> <span data-ttu-id="dda6d-117">Aby uzyskać więcej informacji i pomocnika skryptów tworzenia bezpiecznych klastrów systemu Linux, zobacz [tworzenia bezpiecznych klastrów w systemie Linux](service-fabric-cluster-creation-via-arm.md#secure-linux-clusters).</span><span class="sxs-lookup"><span data-stu-id="dda6d-117">For more information and helper scripts for creating secure Linux clusters, please see [Creating secure clusters on Linux](service-fabric-cluster-creation-via-arm.md#secure-linux-clusters).</span></span> <span data-ttu-id="dda6d-118">Hello uzyskany przez skrypt pomocnika hello podane parametry mogą wprowadzać bezpośrednio w portalu hello zgodnie z opisem w sekcji hello [tworzenia klastra w portalu Azure hello](#create-cluster-portal).</span><span class="sxs-lookup"><span data-stu-id="dda6d-118">hello parameters obtained by hello helper script provided can be input directly into hello portal as described in hello section [Create a cluster in hello Azure portal](#create-cluster-portal).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="dda6d-119">Zaloguj się za tooAzure</span><span class="sxs-lookup"><span data-stu-id="dda6d-119">Log in tooAzure</span></span>
<span data-ttu-id="dda6d-120">Ten przewodnik po używa [programu Azure PowerShell][azure-powershell].</span><span class="sxs-lookup"><span data-stu-id="dda6d-120">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="dda6d-121">Przy uruchamianiu nowej sesji programu PowerShell, zaloguj się za tooyour konto platformy Azure i wyboru subskrypcji przed wykonaniem polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="dda6d-121">When starting a new PowerShell session, log in tooyour Azure account and select your subscription before executing Azure commands.</span></span>

<span data-ttu-id="dda6d-122">Zaloguj się na koncie tooyour azure:</span><span class="sxs-lookup"><span data-stu-id="dda6d-122">Log in tooyour azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="dda6d-123">Wybierz subskrypcję:</span><span class="sxs-lookup"><span data-stu-id="dda6d-123">Select your subscription:</span></span>

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-key-vault"></a><span data-ttu-id="dda6d-124">Konfigurowanie usługi Key Vault</span><span class="sxs-lookup"><span data-stu-id="dda6d-124">Set up Key Vault</span></span>
<span data-ttu-id="dda6d-125">Ta część przewodnika hello przeprowadzi Cię przez utworzenie klucza magazynu dla klastra sieci szkieletowej usług platformy Azure i dla aplikacji sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="dda6d-125">This part of hello guide walks you through creating a Key Vault for a Service Fabric cluster in Azure and for Service Fabric applications.</span></span> <span data-ttu-id="dda6d-126">Aby uzyskać pełne informacje na Key Vault, zobacz hello [Key Vault Wprowadzenie — przewodnik][key-vault-get-started].</span><span class="sxs-lookup"><span data-stu-id="dda6d-126">For a complete guide on Key Vault, see hello [Key Vault getting started guide][key-vault-get-started].</span></span>

<span data-ttu-id="dda6d-127">Platforma Service Fabric korzysta toosecure certyfikatów X.509 klastra.</span><span class="sxs-lookup"><span data-stu-id="dda6d-127">Service Fabric uses X.509 certificates toosecure a cluster.</span></span> <span data-ttu-id="dda6d-128">Usługa Azure Key Vault jest toomanage używane certyfikaty dla klastrów sieci szkieletowej usług platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="dda6d-128">Azure Key Vault is used toomanage certificates for Service Fabric clusters in Azure.</span></span> <span data-ttu-id="dda6d-129">Po wdrożeniu klastra w systemie Azure hello dostawcy zasobów platformy Azure jest odpowiedzialny za tworzenie klastrów usługi sieć szkieletowa ściąga certyfikaty z magazynu kluczy i instaluje je w klastrze hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="dda6d-129">When a cluster is deployed in Azure, hello Azure resource provider responsible for creating Service Fabric clusters pulls certificates from Key Vault and installs them on hello cluster VMs.</span></span>

<span data-ttu-id="dda6d-130">Witaj poniższym diagramie przedstawiono relację hello Key Vault, klaster sieci szkieletowej usług i hello dostawcy zasobów platformy Azure, który wykorzystuje certyfikaty przechowywane w magazynie kluczy, podczas tworzenia klastra:</span><span class="sxs-lookup"><span data-stu-id="dda6d-130">hello following diagram illustrates hello relationship between Key Vault, a Service Fabric cluster, and hello Azure resource provider that uses certificates stored in Key Vault when it creates a cluster:</span></span>

![Instalacja certyfikatu][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a><span data-ttu-id="dda6d-132">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="dda6d-132">Create a Resource Group</span></span>
<span data-ttu-id="dda6d-133">pierwszym krokiem Hello jest toocreate nową grupę zasobów dla usługi Key Vault.</span><span class="sxs-lookup"><span data-stu-id="dda6d-133">hello first step is toocreate a new resource group specifically for Key Vault.</span></span> <span data-ttu-id="dda6d-134">Wprowadzenie klucza magazynu do własnego grupy zasobów jest zalecane, dzięki czemu można usunąć grup zasobów obliczeniowych i przestrzeni dyskowej — takich jak grupy zasobów hello ma klastra usługi sieć szkieletowa — bez utraty z kluczy i kluczy tajnych.</span><span class="sxs-lookup"><span data-stu-id="dda6d-134">Putting Key Vault into its own resource group is recommended so that you can remove compute and storage resource groups - such as hello resource group that has your Service Fabric cluster - without losing your keys and secrets.</span></span> <span data-ttu-id="dda6d-135">Witaj grupę zasobów, która ma magazyn kluczy musi należeć do hello hello klastra, który go używa tego samego regionu.</span><span class="sxs-lookup"><span data-stu-id="dda6d-135">hello resource group that has your Key Vault must be in hello same region as hello cluster that is using it.</span></span>

```powershell

    PS C:\Users\vturecek> New-AzureRmResourceGroup -Name mycluster-keyvault -Location 'West US'
    WARNING: hello output object type of this cmdlet will be modified in a future release.

    ResourceGroupName : mycluster-keyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/mycluster-keyvault

```

### <a name="create-key-vault"></a><span data-ttu-id="dda6d-136">Utwórz magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="dda6d-136">Create Key Vault</span></span>
<span data-ttu-id="dda6d-137">Utwórz magazyn kluczy w hello nową grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="dda6d-137">Create a Key Vault in hello new resource group.</span></span> <span data-ttu-id="dda6d-138">Witaj Key Vault **musi być włączona dla wdrożenia** tooallow hello certyfikaty tooget dostawcy zasobów sieci szkieletowej usług z niego i zainstalować na węzłach klastra:</span><span class="sxs-lookup"><span data-stu-id="dda6d-138">hello Key Vault **must be enabled for deployment** tooallow hello Service Fabric resource provider tooget certificates from it and install on cluster nodes:</span></span>

```powershell

    PS C:\Users\vturecek> New-AzureRmKeyVault -VaultName 'myvault' -ResourceGroupName 'mycluster-keyvault' -Location 'West US' -EnabledForDeployment


    Vault Name                       : myvault
    Resource Group Name              : mycluster-keyvault
    Location                         : West US
    Resource ID                      : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault
    Vault URI                        : https://myvault.vault.azure.net
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

<span data-ttu-id="dda6d-139">Jeśli masz istniejący magazyn kluczy, możesz je włączyć, wdrożenie przy użyciu wiersza polecenia platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="dda6d-139">If you have an existing Key Vault, you can enable it for deployment using Azure CLI:</span></span>

```cli
> azure login
> azure account set "your account"
> azure config mode arm 
> azure keyvault list
> azure keyvault set-policy --vault-name "your vault name" --enabled-for-deployment true
```


## <a name="add-certificates-tookey-vault"></a><span data-ttu-id="dda6d-140">Dodaj certyfikaty tooKey magazynu</span><span class="sxs-lookup"><span data-stu-id="dda6d-140">Add certificates tooKey Vault</span></span>
<span data-ttu-id="dda6d-141">Certyfikaty są używane w sieci szkieletowej usług tooprovide uwierzytelnianie i szyfrowanie toosecure różnych aspektów klastra i jego zastosowań.</span><span class="sxs-lookup"><span data-stu-id="dda6d-141">Certificates are used in Service Fabric tooprovide authentication and encryption toosecure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="dda6d-142">Aby uzyskać więcej informacji dotyczących używania certyfikatów w sieci szkieletowej usług, zobacz [scenariusze zabezpieczeń klastra sieci szkieletowej usług][service-fabric-cluster-security].</span><span class="sxs-lookup"><span data-stu-id="dda6d-142">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios][service-fabric-cluster-security].</span></span>

### <a name="cluster-and-server-certificate-required"></a><span data-ttu-id="dda6d-143">Klaster a serwera certyfikatów (wymagane)</span><span class="sxs-lookup"><span data-stu-id="dda6d-143">Cluster and server certificate (required)</span></span>
<span data-ttu-id="dda6d-144">Ten certyfikat jest wymagany toosecure klastra i zapobiec tooit nieautoryzowanego dostępu.</span><span class="sxs-lookup"><span data-stu-id="dda6d-144">This certificate is required toosecure a cluster and prevent unauthorized access tooit.</span></span> <span data-ttu-id="dda6d-145">Udostępnia ona zabezpieczeń klastra na kilka sposobów:</span><span class="sxs-lookup"><span data-stu-id="dda6d-145">It provides cluster security in a couple ways:</span></span>

* <span data-ttu-id="dda6d-146">**Uwierzytelnianie klastra:** uwierzytelnia komunikacji między węzłami w Federacji klastra.</span><span class="sxs-lookup"><span data-stu-id="dda6d-146">**Cluster authentication:** Authenticates node-to-node communication for cluster federation.</span></span> <span data-ttu-id="dda6d-147">Tylko węzły, które można potwierdzić swoją tożsamość, z tym certyfikatem może dołączać hello klastra.</span><span class="sxs-lookup"><span data-stu-id="dda6d-147">Only nodes that can prove their identity with this certificate can join hello cluster.</span></span>
* <span data-ttu-id="dda6d-148">**Uwierzytelnianie serwera:** uwierzytelnia hello klastra zarządzania punkty końcowe tooa zarządzania klienta, tak, aby hello klienta zarządzania zna jest mówić toohello rzeczywistych klastra.</span><span class="sxs-lookup"><span data-stu-id="dda6d-148">**Server authentication:** Authenticates hello cluster management endpoints tooa management client, so that hello management client knows it is talking toohello real cluster.</span></span> <span data-ttu-id="dda6d-149">Ten certyfikat zapewnia również SSL hello interfejsu API zarządzania HTTPS oraz Service Fabric Explorer, za pośrednictwem protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="dda6d-149">This certificate also provides SSL for hello HTTPS management API and for Service Fabric Explorer over HTTPS.</span></span>

<span data-ttu-id="dda6d-150">tooserve tych celów hello certyfikatu musi spełniać następujące wymagania hello:</span><span class="sxs-lookup"><span data-stu-id="dda6d-150">tooserve these purposes, hello certificate must meet hello following requirements:</span></span>

* <span data-ttu-id="dda6d-151">Witaj, certyfikat musi zawierać klucz prywatny.</span><span class="sxs-lookup"><span data-stu-id="dda6d-151">hello certificate must contain a private key.</span></span>
* <span data-ttu-id="dda6d-152">Witaj certyfikatu musi zostać utworzony dla wymiany kluczy, można eksportować tooa plik wymiany informacji osobistych (pfx).</span><span class="sxs-lookup"><span data-stu-id="dda6d-152">hello certificate must be created for key exchange, exportable tooa Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="dda6d-153">Hello nazwa podmiotu certyfikatu musi odpowiadać klastra hello tooaccess hello domeny używane w sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="dda6d-153">hello certificate's subject name must match hello domain used tooaccess hello Service Fabric cluster.</span></span> <span data-ttu-id="dda6d-154">Jest to wymagane tooprovide protokołu SSL dla punktów końcowych HTTPS zarządzania i Service Fabric Explorer hello klastra.</span><span class="sxs-lookup"><span data-stu-id="dda6d-154">This is required tooprovide SSL for hello cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="dda6d-155">Nie można uzyskać certyfikatu SSL z urzędu certyfikacji (CA) w celu hello `.cloudapp.azure.com` domeny.</span><span class="sxs-lookup"><span data-stu-id="dda6d-155">You cannot obtain an SSL certificate from a certificate authority (CA) for hello `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="dda6d-156">Możliwość nabycia niestandardowej nazwy domeny dla klastra.</span><span class="sxs-lookup"><span data-stu-id="dda6d-156">Acquire a custom domain name for your cluster.</span></span> <span data-ttu-id="dda6d-157">W przypadku żądania certyfikatu na podstawie nazwy podmiotu certyfikatu hello urzędu certyfikacji musi odpowiadać nazwie domeny niestandardowej hello używane dla klastra.</span><span class="sxs-lookup"><span data-stu-id="dda6d-157">When you request a certificate from a CA hello certificate's subject name must match hello custom domain name used for your cluster.</span></span>

### <a name="client-authentication-certificates"></a><span data-ttu-id="dda6d-158">Certyfikaty uwierzytelniania klienta</span><span class="sxs-lookup"><span data-stu-id="dda6d-158">Client authentication certificates</span></span>
<span data-ttu-id="dda6d-159">Certyfikaty klienta dodatkowe uwierzytelnianie Administratorzy dla zadań zarządzania w klastrze.</span><span class="sxs-lookup"><span data-stu-id="dda6d-159">Additional client certificates authenticate administrators for cluster management tasks.</span></span> <span data-ttu-id="dda6d-160">Sieć szkieletowa usług ma dwa poziomy dostępu: **admin** i **użytkownika tylko do odczytu**.</span><span class="sxs-lookup"><span data-stu-id="dda6d-160">Service Fabric has two access levels: **admin** and **read-only user**.</span></span> <span data-ttu-id="dda6d-161">Co najmniej jeden certyfikat dla dostępu administracyjnego należy używać.</span><span class="sxs-lookup"><span data-stu-id="dda6d-161">At minimum, a single certificate for administrative access should be used.</span></span> <span data-ttu-id="dda6d-162">Dodatkowe dostępu na poziomie użytkownika należy podać oddzielny certyfikat.</span><span class="sxs-lookup"><span data-stu-id="dda6d-162">For additional user-level access, a separate certificate must be provided.</span></span> <span data-ttu-id="dda6d-163">Aby uzyskać więcej informacji na dostęp do ról, zobacz [kontroli dostępu opartej na rolach dla klientów usługi sieć szkieletowa][service-fabric-cluster-security-roles].</span><span class="sxs-lookup"><span data-stu-id="dda6d-163">For more information on access roles, see [role-based access control for Service Fabric clients][service-fabric-cluster-security-roles].</span></span>

<span data-ttu-id="dda6d-164">Nie trzeba tooupload klienta uwierzytelniania certyfikatów tooKey magazynu toowork z sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="dda6d-164">You do not need tooupload Client authentication certificates tooKey Vault toowork with Service Fabric.</span></span> <span data-ttu-id="dda6d-165">Te certyfikaty muszą tylko toobe podane toousers, którzy mają uprawnienia do zarządzania klastrem.</span><span class="sxs-lookup"><span data-stu-id="dda6d-165">These certificates only need toobe provided toousers who are authorized for cluster management.</span></span> 

> [!NOTE]
> <span data-ttu-id="dda6d-166">Usługa Azure Active Directory jest hello zalecany sposób tooauthenticate klientów dla klastra operacji zarządzania.</span><span class="sxs-lookup"><span data-stu-id="dda6d-166">Azure Active Directory is hello recommended way tooauthenticate clients for cluster management operations.</span></span> <span data-ttu-id="dda6d-167">toouse usługi Azure Active Directory, należy najpierw [Tworzenie klastra przy użyciu usługi Azure Resource Manager][create-cluster-arm].</span><span class="sxs-lookup"><span data-stu-id="dda6d-167">toouse Azure Active Directory, you must [create a cluster using Azure Resource Manager][create-cluster-arm].</span></span>
> 
> 

### <a name="application-certificates-optional"></a><span data-ttu-id="dda6d-168">Certyfikaty aplikacji (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="dda6d-168">Application certificates (optional)</span></span>
<span data-ttu-id="dda6d-169">Dowolna liczba dodatkowych certyfikatów można zainstalować w klastrze dla aplikacji ze względów bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="dda6d-169">Any number of additional certificates can be installed on a cluster for application security purposes.</span></span> <span data-ttu-id="dda6d-170">Przed utworzeniem klastra, należy wziąć pod uwagę scenariusze zabezpieczeń aplikacji hello, które wymagają toobe certyfikat zainstalowany na węzłach hello, takich jak:</span><span class="sxs-lookup"><span data-stu-id="dda6d-170">Before creating your cluster, consider hello application security scenarios that require a certificate toobe installed on hello nodes, such as:</span></span>

* <span data-ttu-id="dda6d-171">Szyfrowanie i odszyfrowywanie wartości konfiguracji aplikacji</span><span class="sxs-lookup"><span data-stu-id="dda6d-171">Encryption and decryption of application configuration values</span></span>
* <span data-ttu-id="dda6d-172">Szyfrowanie danych w węzłach podczas replikacji</span><span class="sxs-lookup"><span data-stu-id="dda6d-172">Encryption of data across nodes during replication</span></span> 

<span data-ttu-id="dda6d-173">Nie można skonfigurować certyfikaty aplikacji, podczas tworzenia klastra za pośrednictwem hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="dda6d-173">Application certificates cannot be configured when creating a cluster through hello Azure portal.</span></span> <span data-ttu-id="dda6d-174">Certyfikaty aplikacji tooconfigure podczas konfiguracji klastra, należy najpierw [Tworzenie klastra przy użyciu usługi Azure Resource Manager][create-cluster-arm].</span><span class="sxs-lookup"><span data-stu-id="dda6d-174">tooconfigure application certificates at cluster setup time, you must [create a cluster using Azure Resource Manager][create-cluster-arm].</span></span> <span data-ttu-id="dda6d-175">Można również dodać klastra toohello certyfikatów aplikacji po jego utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="dda6d-175">You can also add application certificates toohello cluster after it has been created.</span></span>

### <a name="formatting-certificates-for-azure-resource-provider-use"></a><span data-ttu-id="dda6d-176">Formatowanie certyfikatów do użytku dostawcy zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="dda6d-176">Formatting certificates for Azure resource provider use</span></span>
<span data-ttu-id="dda6d-177">Pliki klucza prywatnego (pfx) można dodany i używany bezpośrednio za pomocą usługi Key Vault.</span><span class="sxs-lookup"><span data-stu-id="dda6d-177">Private key files (.pfx) can be added and used directly through Key Vault.</span></span> <span data-ttu-id="dda6d-178">Dostawcy zasobów platformy Azure hello wymaga jednak toobe klucze przechowywane w formacie JSON specjalny, który zawiera PFX hello jako base-64 zakodowany ciąg i hello hasło klucza prywatnego.</span><span class="sxs-lookup"><span data-stu-id="dda6d-178">However, hello Azure resource provider requires keys toobe stored in a special JSON format that includes hello .pfx as a base-64 encoded string and hello private key password.</span></span> <span data-ttu-id="dda6d-179">tooaccommodate tych wymagań, klucze musi być umieszczona w ciągu JSON i następnie przechowywane jako *kluczy tajnych* w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="dda6d-179">tooaccommodate these requirements, keys must be placed in a JSON string and then stored as *secrets* in Key Vault.</span></span>

<span data-ttu-id="dda6d-180">toomake to łatwiej przetwarzania, moduł programu PowerShell jest [dostępne w witrynie GitHub][service-fabric-rp-helpers].</span><span class="sxs-lookup"><span data-stu-id="dda6d-180">toomake this process easier, a PowerShell module is [available on GitHub][service-fabric-rp-helpers].</span></span> <span data-ttu-id="dda6d-181">Wykonaj te kroki toouse hello modułu:</span><span class="sxs-lookup"><span data-stu-id="dda6d-181">Follow these steps toouse hello module:</span></span>

1. <span data-ttu-id="dda6d-182">Pobierz całą zawartość repozytorium hello hello do katalogu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="dda6d-182">Download hello entire contents of hello repo into a local directory.</span></span> 
2. <span data-ttu-id="dda6d-183">Zaimportuj moduł hello w oknie programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="dda6d-183">Import hello module in your PowerShell window:</span></span>

```powershell
  PS C:\Users\vturecek> Import-Module "C:\users\vturecek\Documents\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"
```

<span data-ttu-id="dda6d-184">Witaj `Invoke-AddCertToKeyVault` polecenia w tym module środowiska PowerShell automatycznie formatuje klucz prywatny certyfikatu do ciągu JSON i przekazanie jej tooKey magazynu.</span><span class="sxs-lookup"><span data-stu-id="dda6d-184">hello `Invoke-AddCertToKeyVault` command in this PowerShell module automatically formats a certificate private key into a JSON string and uploads it tooKey Vault.</span></span> <span data-ttu-id="dda6d-185">Użyj go tooadd hello klastra certyfikat i wszelkie dodatkowe aplikacji certyfikaty tooKey magazynu.</span><span class="sxs-lookup"><span data-stu-id="dda6d-185">Use it tooadd hello cluster certificate and any additional application certificates tooKey Vault.</span></span> <span data-ttu-id="dda6d-186">Powtórz ten krok dla wszystkich dodatkowych certyfikatów, które chcesz tooinstall w klastrze.</span><span class="sxs-lookup"><span data-stu-id="dda6d-186">Repeat this step for any additional certificates you want tooinstall in your cluster.</span></span>

```powershell
PS C:\Users\vturecek> Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName mycluster-keyvault -Location "West US" -VaultName myvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

    Switching context tooSubscriptionId <guid>
    Ensuring ResourceGroup mycluster-keyvault in West US
    WARNING: hello output object type of this cmdlet will be modified in a future release.
    Using existing valut myvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret toomyvault in vault myvault


Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

<span data-ttu-id="dda6d-187">Są to wszystkie wymagania wstępne usługi Key Vault hello do konfigurowania szablonu usługi Resource Manager klastra sieci szkieletowej usług, który instaluje certyfikatów dla uwierzytelniania węzła, zarządzania punktu końcowego zabezpieczeń i uwierzytelniania oraz wszelkie dodatkowe zabezpieczenia aplikacji Funkcje, które korzystają z certyfikatów X.509.</span><span class="sxs-lookup"><span data-stu-id="dda6d-187">These are all hello Key Vault prerequisites for configuring a Service Fabric cluster Resource Manager template that installs certificates for node authentication, management endpoint security and authentication, and any additional application security features that use X.509 certificates.</span></span> <span data-ttu-id="dda6d-188">W tym momencie powinny mieć teraz powitania po zakończeniu instalacji na platformie Azure:</span><span class="sxs-lookup"><span data-stu-id="dda6d-188">At this point, you should now have hello following setup in Azure:</span></span>

* <span data-ttu-id="dda6d-189">Grupa zasobów magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="dda6d-189">Key Vault resource group</span></span>
  * <span data-ttu-id="dda6d-190">Usługa Key Vault</span><span class="sxs-lookup"><span data-stu-id="dda6d-190">Key Vault</span></span>
    * <span data-ttu-id="dda6d-191">Certyfikat uwierzytelniania serwera klastra</span><span class="sxs-lookup"><span data-stu-id="dda6d-191">Cluster server authentication certificate</span></span>

<span data-ttu-id="dda6d-192">< /a "Tworzenie klastra portal" ></a></span><span class="sxs-lookup"><span data-stu-id="dda6d-192"></a "create-cluster-portal" ></a></span></span>

## <a name="create-cluster-in-hello-azure-portal"></a><span data-ttu-id="dda6d-193">Tworzenie klastra w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="dda6d-193">Create cluster in hello Azure portal</span></span>
### <a name="search-for-hello-service-fabric-cluster-resource"></a><span data-ttu-id="dda6d-194">Wyszukaj hello zasobu klastra usługi sieć szkieletowa</span><span class="sxs-lookup"><span data-stu-id="dda6d-194">Search for hello Service Fabric cluster resource</span></span>
![Wyszukiwanie szablonu klastra sieci szkieletowej usług na powitania portalu Azure.][SearchforServiceFabricClusterTemplate]

1. <span data-ttu-id="dda6d-196">Zaloguj się toohello [portalu Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="dda6d-196">Sign in toohello [Azure portal][azure-portal].</span></span>
2. <span data-ttu-id="dda6d-197">Kliknij przycisk **nowy** tooadd nowego szablonu zasobów.</span><span class="sxs-lookup"><span data-stu-id="dda6d-197">Click **New** tooadd a new resource template.</span></span> <span data-ttu-id="dda6d-198">Wyszukaj hello szablonu klastra sieci szkieletowej usług w hello **Marketplace** w obszarze **wszystko**.</span><span class="sxs-lookup"><span data-stu-id="dda6d-198">Search for hello Service Fabric Cluster template in hello **Marketplace** under **Everything**.</span></span>
3. <span data-ttu-id="dda6d-199">Wybierz **klastra sieci szkieletowej usług** z listy hello.</span><span class="sxs-lookup"><span data-stu-id="dda6d-199">Select **Service Fabric Cluster** from hello list.</span></span>
4. <span data-ttu-id="dda6d-200">Przejdź toohello **klastra sieci szkieletowej usług** bloku, kliknij przycisk **Utwórz**,</span><span class="sxs-lookup"><span data-stu-id="dda6d-200">Navigate toohello **Service Fabric Cluster** blade, click **Create**,</span></span>
5. <span data-ttu-id="dda6d-201">Witaj **klastra tworzenia sieci szkieletowej usług** bloku ma hello następujące cztery kroki.</span><span class="sxs-lookup"><span data-stu-id="dda6d-201">hello **Create Service Fabric cluster** blade has hello following four steps.</span></span>

#### <a name="1-basics"></a><span data-ttu-id="dda6d-202">1. Podstawy</span><span class="sxs-lookup"><span data-stu-id="dda6d-202">1. Basics</span></span>
![Zrzut ekranu przedstawiający tworzenie nowej grupy zasobów.][CreateRG]

<span data-ttu-id="dda6d-204">W bloku podstawowe służące hello należy tooprovide hello podstawowe szczegóły dla klastra.</span><span class="sxs-lookup"><span data-stu-id="dda6d-204">In hello Basics blade you need tooprovide hello basic details for your cluster.</span></span>

1. <span data-ttu-id="dda6d-205">Wprowadź nazwę hello klastra.</span><span class="sxs-lookup"><span data-stu-id="dda6d-205">Enter hello name of your cluster.</span></span>
2. <span data-ttu-id="dda6d-206">Wprowadź **nazwy użytkownika** i **hasło** dla pulpitu zdalnego dla hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="dda6d-206">Enter a **user name** and **password** for Remote Desktop for hello VMs.</span></span>
3. <span data-ttu-id="dda6d-207">Upewnij się, że hello tooselect **subskrypcji** mają Twojej toobe klastra wdrożone, zwłaszcza, jeśli masz wiele subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="dda6d-207">Make sure tooselect hello **Subscription** that you want your cluster toobe deployed to, especially if you have multiple subscriptions.</span></span>
4. <span data-ttu-id="dda6d-208">Utwórz **nową grupę zasobów**.</span><span class="sxs-lookup"><span data-stu-id="dda6d-208">Create a **new resource group**.</span></span> <span data-ttu-id="dda6d-209">Jest najlepszym toogive go hello samą nazwę jak hello klastra, ponieważ pomaga w znajdowaniu je później, szczególnie w przypadku, gdy są w trakcie wdrażania tooyour zmiany toomake lub usunięciu klastra.</span><span class="sxs-lookup"><span data-stu-id="dda6d-209">It is best toogive it hello same name as hello cluster, since it helps in finding them later, especially when you are trying toomake changes tooyour deployment or delete your cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="dda6d-210">Chociaż użytkownik może określić toouse istniejącą grupę zasobów, jest dobrym rozwiązaniem toocreate nową grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="dda6d-210">Although you can decide toouse an existing resource group, it is a good practice toocreate a new resource group.</span></span> <span data-ttu-id="dda6d-211">Dzięki temu można łatwo toodelete klastrów, w których nie ma potrzeby.</span><span class="sxs-lookup"><span data-stu-id="dda6d-211">This makes it easy toodelete clusters that you do not need.</span></span>
   > 
   > 
5. <span data-ttu-id="dda6d-212">Wybierz hello **regionu** w której ma zostać toocreate hello klastra.</span><span class="sxs-lookup"><span data-stu-id="dda6d-212">Select hello **region** in which you want toocreate hello cluster.</span></span> <span data-ttu-id="dda6d-213">Witaj, znajduje się w tym samym regionie, który klucz magazynu, należy użyć.</span><span class="sxs-lookup"><span data-stu-id="dda6d-213">You must use hello same region that your Key Vault is in.</span></span>

#### <a name="2-cluster-configuration"></a><span data-ttu-id="dda6d-214">2. Konfiguracja klastra</span><span class="sxs-lookup"><span data-stu-id="dda6d-214">2. Cluster configuration</span></span>
![Tworzenie typu węzła][CreateNodeType]

<span data-ttu-id="dda6d-216">Skonfiguruj węzły klastra.</span><span class="sxs-lookup"><span data-stu-id="dda6d-216">Configure your cluster nodes.</span></span> <span data-ttu-id="dda6d-217">Typy węzłów zdefiniować rozmiary maszyn wirtualnych hello hello liczbę maszyn wirtualnych i ich właściwości.</span><span class="sxs-lookup"><span data-stu-id="dda6d-217">Node types define hello VM sizes, hello number of VMs, and their properties.</span></span> <span data-ttu-id="dda6d-218">Klaster może zawierać więcej niż jeden typ węzła, ale typ węzła podstawowego hello (hello w pierwszej kolejności należy zdefiniować w portalu hello) musi mieć co najmniej pięć maszyn wirtualnych, jak jest to typ węzła hello rozmieszczenia usługi sieć szkieletowa usług systemowych.</span><span class="sxs-lookup"><span data-stu-id="dda6d-218">Your cluster can have more than one node type, but hello primary node type (hello first one that you define on hello portal) must have at least five VMs, as this is hello node type where Service Fabric system services are placed.</span></span> <span data-ttu-id="dda6d-219">Nie należy konfigurować **właściwości umieszczania** ponieważ domyślna właściwość umieszczania "NodeTypeName" są dodawane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="dda6d-219">Do not configure **Placement Properties** because a default placement property of "NodeTypeName" is added automatically.</span></span>

> [!NOTE]
> <span data-ttu-id="dda6d-220">Typowy scenariusz dla wielu typów węzła jest aplikacja, która zawiera usługi frontonu i zaplecza.</span><span class="sxs-lookup"><span data-stu-id="dda6d-220">A common scenario for multiple node types is an application that contains a front-end service and a back-end service.</span></span> <span data-ttu-id="dda6d-221">Usługa frontonu hello tooput na mniejsze maszyn wirtualnych (na przykład D2 rozmiarów maszyn wirtualnych) z toohello otwartych portów internetowych, ale ma usługi zaplecza hello tooput na większych maszyn wirtualnych (o rozmiarów maszyn wirtualnych, takie jak D4, D6 D15 i tak dalej) z nie ma otwartych portów połączonych z Internetem.</span><span class="sxs-lookup"><span data-stu-id="dda6d-221">You want tooput hello front-end service on smaller VMs (VM sizes like D2) with ports open toohello Internet, but you want tooput hello back-end service on larger VMs (with VM sizes like D4, D6, D15, and so on) with no Internet-facing ports open.</span></span>
> 
> 

1. <span data-ttu-id="dda6d-222">Wybierz nazwę dla danego typu węzła (1 znaków too12 zawierających tylko litery i cyfry).</span><span class="sxs-lookup"><span data-stu-id="dda6d-222">Choose a name for your node type (1 too12 characters containing only letters and numbers).</span></span>
2. <span data-ttu-id="dda6d-223">Minimalna Hello **rozmiar** maszyn wirtualnych dla węzła podstawowego hello typu jest wymuszany przez hello **trwałości** warstwy wybierz hello klastra.</span><span class="sxs-lookup"><span data-stu-id="dda6d-223">hello minimum **size** of VMs for hello primary node type is driven by hello **durability** tier you choose for hello cluster.</span></span> <span data-ttu-id="dda6d-224">Witaj domyślnym warstwa trwałości hello jest brązowa.</span><span class="sxs-lookup"><span data-stu-id="dda6d-224">hello default for hello durability tier is bronze.</span></span> <span data-ttu-id="dda6d-225">Aby uzyskać więcej informacji o trwałości, zobacz [jak toochoose hello sieci szkieletowej usług klastra niezawodność i trwałość][service-fabric-cluster-capacity].</span><span class="sxs-lookup"><span data-stu-id="dda6d-225">For more information on durability, see [how toochoose hello Service Fabric cluster reliability and durability][service-fabric-cluster-capacity].</span></span>
3. <span data-ttu-id="dda6d-226">Wybierz rozmiar maszyny Wirtualnej hello i warstwę cenową.</span><span class="sxs-lookup"><span data-stu-id="dda6d-226">Select hello VM size and pricing tier.</span></span> <span data-ttu-id="dda6d-227">Maszyny wirtualne D-series mają dyski SSD i zaleca aplikacji stanowych.</span><span class="sxs-lookup"><span data-stu-id="dda6d-227">D-series VMs have SSD drives and are highly recommended for stateful applications.</span></span> <span data-ttu-id="dda6d-228">Użyj dowolnej jednostki SKU maszyny Wirtualnej z częściowa rdzeni lub nie mają mniej niż 7 GB pojemności dysku.</span><span class="sxs-lookup"><span data-stu-id="dda6d-228">Do not use any VM SKU that has partial cores or have less than 7 GB of available disk capacity.</span></span> 
4. <span data-ttu-id="dda6d-229">Minimalna Hello **numer** maszyn wirtualnych dla węzła podstawowego hello typu jest wymuszany przez hello **niezawodności** warstwy wybierzesz.</span><span class="sxs-lookup"><span data-stu-id="dda6d-229">hello minimum **number** of VMs for hello primary node type is driven by hello **reliability** tier you choose.</span></span> <span data-ttu-id="dda6d-230">domyślnym Hello warstwa niezawodności hello jest Silver.</span><span class="sxs-lookup"><span data-stu-id="dda6d-230">hello default for hello reliability tier is Silver.</span></span> <span data-ttu-id="dda6d-231">Aby uzyskać więcej informacji o niezawodności, zobacz [jak toochoose hello sieci szkieletowej usług klastra niezawodność i trwałość][service-fabric-cluster-capacity].</span><span class="sxs-lookup"><span data-stu-id="dda6d-231">For more information on reliability, see [how toochoose hello Service Fabric cluster reliability and durability][service-fabric-cluster-capacity].</span></span>
5. <span data-ttu-id="dda6d-232">Wybierz hello liczbę maszyn wirtualnych dla typu węzła hello.</span><span class="sxs-lookup"><span data-stu-id="dda6d-232">Choose hello number of VMs for hello node type.</span></span> <span data-ttu-id="dda6d-233">Możesz skalować w górę lub w dół hello liczbę maszyn wirtualnych w typ węzła później, ale dla typu węzła podstawowego hello, minimalna hello jest wymuszany przez hello poziomu niezawodności, który wybrano.</span><span class="sxs-lookup"><span data-stu-id="dda6d-233">You can scale up or down hello number of VMs in a node type later on, but on hello primary node type, hello minimum is driven by hello reliability level that you have chosen.</span></span> <span data-ttu-id="dda6d-234">Inne typy węzłów może mieć co najmniej 1 maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="dda6d-234">Other node types can have a minimum of 1 VM.</span></span>
6. <span data-ttu-id="dda6d-235">Skonfiguruj niestandardowe punkty końcowe.</span><span class="sxs-lookup"><span data-stu-id="dda6d-235">Configure custom endpoints.</span></span> <span data-ttu-id="dda6d-236">To pole umożliwia tooenter rozdzielana przecinkami lista portów, które mają tooexpose za pośrednictwem toohello modułu równoważenia obciążenia Azure hello publicznego Internetu dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="dda6d-236">This field allows you tooenter a comma-separated list of ports that you want tooexpose through hello Azure Load Balancer toohello public Internet for your applications.</span></span> <span data-ttu-id="dda6d-237">Na przykład, jeśli planujesz toodeploy klastra tooyour aplikacji sieci web, wpisz "80" tutaj tooallow ruch na porcie 80 do klastra.</span><span class="sxs-lookup"><span data-stu-id="dda6d-237">For example, if you plan toodeploy a web application tooyour cluster, enter "80" here tooallow traffic on port 80 into your cluster.</span></span> <span data-ttu-id="dda6d-238">Aby uzyskać więcej informacji dotyczących punktów końcowych, zobacz [komunikacji z aplikacjami][service-fabric-connect-and-communicate-with-services]</span><span class="sxs-lookup"><span data-stu-id="dda6d-238">For more information on endpoints, see [communicating with applications][service-fabric-connect-and-communicate-with-services]</span></span>
7. <span data-ttu-id="dda6d-239">Konfigurowanie klastra **diagnostyki**.</span><span class="sxs-lookup"><span data-stu-id="dda6d-239">Configure cluster **diagnostics**.</span></span> <span data-ttu-id="dda6d-240">Domyślnie diagnostycznych są włączone na tooassist z klastra z rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="dda6d-240">By default, diagnostics are enabled on your cluster tooassist with troubleshooting issues.</span></span> <span data-ttu-id="dda6d-241">Jeśli chcesz diagnostyki toodisable zmienić hello **stan** Przełącz zbyt**poza**.</span><span class="sxs-lookup"><span data-stu-id="dda6d-241">If you want toodisable diagnostics change hello **Status** toggle too**Off**.</span></span> <span data-ttu-id="dda6d-242">Wyłączenie diagnostyki jest **nie** zalecane.</span><span class="sxs-lookup"><span data-stu-id="dda6d-242">Turning off diagnostics is **not** recommended.</span></span>
8. <span data-ttu-id="dda6d-243">Wybierz hello uaktualnianie tryb ma ustawioną wartość klastra.</span><span class="sxs-lookup"><span data-stu-id="dda6d-243">Select hello Fabric upgrade mode you want set your cluster to.</span></span> <span data-ttu-id="dda6d-244">Wybierz **automatyczne**, jeśli chcesz hello systemu tooautomatically odbioru hello najnowszej dostępnej wersji i spróbuj tooupgrade Twojego tooit klastra.</span><span class="sxs-lookup"><span data-stu-id="dda6d-244">Select **Automatic**, if you want hello system tooautomatically pick up hello latest available version and try tooupgrade your cluster tooit.</span></span> <span data-ttu-id="dda6d-245">Ustaw tryb hello zbyt**ręcznego**, jeśli chcesz, aby toochoose obsługiwanej wersji.</span><span class="sxs-lookup"><span data-stu-id="dda6d-245">Set hello mode too**Manual**, if you want toochoose a supported version.</span></span>

> [!NOTE]
> <span data-ttu-id="dda6d-246">Firma Microsoft obsługuje tylko klastry, które są z obsługiwanymi wersjami usługi sieci szkieletowej.</span><span class="sxs-lookup"><span data-stu-id="dda6d-246">We support only clusters that are running supported versions of service Fabric.</span></span> <span data-ttu-id="dda6d-247">Po wybraniu hello **ręcznego** trybie są tworzone na powitania odpowiedzialność tooupgrade wersji tooa obsługiwane klastra.</span><span class="sxs-lookup"><span data-stu-id="dda6d-247">By selecting hello **Manual** mode, you are taking on hello responsibility tooupgrade your cluster tooa supported version.</span></span> <span data-ttu-id="dda6d-248">Witaj można znaleźć więcej szczegółów na tryb uaktualniania sieci szkieletowej hello [dokumentu usługi sieci szkieletowej klastra uaktualnienia.][service-fabric-cluster-upgrade]</span><span class="sxs-lookup"><span data-stu-id="dda6d-248">For more details on hello Fabric upgrade mode see hello [service-fabric-cluster-upgrade document.][service-fabric-cluster-upgrade]</span></span>
> 
> 

#### <a name="3-security"></a><span data-ttu-id="dda6d-249">3. Bezpieczeństwo</span><span class="sxs-lookup"><span data-stu-id="dda6d-249">3. Security</span></span>
![Zrzut ekranu przedstawiający konfiguracjach zabezpieczeń w portalu Azure.][SecurityConfigs]

<span data-ttu-id="dda6d-251">Witaj ostatnim krokiem jest tooprovide certyfikatu informacji toosecure hello klastra przy użyciu hello magazyn kluczy i certyfikatów informacji utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="dda6d-251">hello final step is tooprovide certificate information toosecure hello cluster using hello Key Vault and certificate information created earlier.</span></span>

* <span data-ttu-id="dda6d-252">Wypełniania pól podstawowego certyfikatu hello z danych wyjściowych hello uzyskane z przekazywania hello **certyfikatu klastra** tooKey magazynu przy użyciu hello `Invoke-AddCertToKeyVault` polecenia programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dda6d-252">Populate hello primary certificate fields with hello output obtained from uploading hello **cluster certificate** tooKey Vault using hello `Invoke-AddCertToKeyVault` PowerShell command.</span></span>

```powershell
Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47
```

* <span data-ttu-id="dda6d-253">Sprawdź hello **Skonfiguruj ustawienia zaawansowane** polu tooenter certyfikaty klientów dla **klienta administrator** i **klienta tylko do odczytu**.</span><span class="sxs-lookup"><span data-stu-id="dda6d-253">Check hello **Configure advanced settings** box tooenter client certificates for **admin client** and **read-only client**.</span></span> <span data-ttu-id="dda6d-254">W tych polach wprowadź hello odcisk palca certyfikatu klienta administratora i hello odcisk palca certyfikatu klienta użytkownika tylko do odczytu, jeśli ma to zastosowanie.</span><span class="sxs-lookup"><span data-stu-id="dda6d-254">In these fields, enter hello thumbprint of your admin client certificate and hello thumbprint of your read-only user client certificate, if applicable.</span></span> <span data-ttu-id="dda6d-255">Gdy administratorzy prób tooconnect toohello klastra, otrzymali dostępu tylko wtedy, gdy mają certyfikat z odciskiem palca, odpowiadającą wartości odcisku palca hello wprowadzanym w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="dda6d-255">When administrators attempt tooconnect toohello cluster, they are granted access only if they have a certificate with a thumbprint that matches hello thumbprint values entered here.</span></span>  

#### <a name="4-summary"></a><span data-ttu-id="dda6d-256">4. Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="dda6d-256">4. Summary</span></span>
![<span data-ttu-id="dda6d-257">Zrzut ekranu przedstawiający tablicy start hello wyświetlanie "Klastra sieci szkieletowej usług wdrażanie".</span><span class="sxs-lookup"><span data-stu-id="dda6d-257">Screen shot of hello start board displaying "Deploying Service Fabric Cluster."</span></span> ][Notifications]

<span data-ttu-id="dda6d-258">Utworzenie klastra hello toocomplete, kliknij przycisk **Podsumowanie** toosee hello konfiguracje, które zostały podane lub pobrać hello klastra które używane toodeploy szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="dda6d-258">toocomplete hello cluster creation, click **Summary** toosee hello configurations that you have provided, or download hello Azure Resource Manager template that that used toodeploy your cluster.</span></span> <span data-ttu-id="dda6d-259">Po dostarczeniu hello ustawienia obowiązkowe, hello **OK** przycisk staje się zielony i można uruchomić procesu tworzenia klastra hello, klikając go.</span><span class="sxs-lookup"><span data-stu-id="dda6d-259">After you have provided hello mandatory settings, hello **OK** button becomes green and you can start hello cluster creation process by clicking it.</span></span>

<span data-ttu-id="dda6d-260">Postęp tworzenia hello w powiadomieniach hello jest widoczny.</span><span class="sxs-lookup"><span data-stu-id="dda6d-260">You can see hello creation progress in hello notifications.</span></span> <span data-ttu-id="dda6d-261">(Kliknij ikonę dzwonka"hello" w pobliżu pasek stanu hello na powitania górnym rogu ekranu). Jeśli kliknięto **tooStartboard numeru Pin** podczas tworzenia klastra hello, zobaczysz **wdrażanie klastra sieci szkieletowej usług** przypięty toohello **Start** tablicy.</span><span class="sxs-lookup"><span data-stu-id="dda6d-261">(Click hello "Bell" icon near hello status bar at hello upper right of your screen.) If you clicked **Pin tooStartboard** while creating hello cluster, you will see **Deploying Service Fabric Cluster** pinned toohello **Start** board.</span></span>

### <a name="view-your-cluster-status"></a><span data-ttu-id="dda6d-262">Wyświetl stan sieci klastra</span><span class="sxs-lookup"><span data-stu-id="dda6d-262">View your cluster status</span></span>
![Zrzut ekranu przedstawiający szczegółów klastra hello w pulpicie nawigacyjnym.][ClusterDashboard]

<span data-ttu-id="dda6d-264">Po utworzeniu klastra można sprawdzić w portalu hello klastra:</span><span class="sxs-lookup"><span data-stu-id="dda6d-264">Once your cluster is created, you can inspect your cluster in hello portal:</span></span>

1. <span data-ttu-id="dda6d-265">Przejdź za**Przeglądaj** i kliknij przycisk **klastry usługi sieć szkieletowa**.</span><span class="sxs-lookup"><span data-stu-id="dda6d-265">Go too**Browse** and click **Service Fabric Clusters**.</span></span>
2. <span data-ttu-id="dda6d-266">Znajdź klastra i kliknij ją.</span><span class="sxs-lookup"><span data-stu-id="dda6d-266">Locate your cluster and click it.</span></span>
3. <span data-ttu-id="dda6d-267">Możesz teraz przeglądać szczegóły hello klastra na pulpicie nawigacyjnym hello, w tym klastrze hello publiczny punkt końcowy i tooService łącze Eksploratora sieci szkieletowej.</span><span class="sxs-lookup"><span data-stu-id="dda6d-267">You can now see hello details of your cluster in hello dashboard, including hello cluster's public endpoint and a link tooService Fabric Explorer.</span></span>

<span data-ttu-id="dda6d-268">Witaj **Monitor węzła** sekcji w bloku pulpit nawigacyjny klastra hello wskazuje hello liczbę maszyn wirtualnych, które są w dobrej kondycji i nie działa prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="dda6d-268">hello **Node Monitor** section on hello cluster's dashboard blade indicates hello number of VMs that are healthy and not healthy.</span></span> <span data-ttu-id="dda6d-269">Można znaleźć więcej szczegółów na temat kondycji hello klastra na [wprowadzenie modelu kondycji sieci szkieletowej usług][service-fabric-health-introduction].</span><span class="sxs-lookup"><span data-stu-id="dda6d-269">You can find more details about hello cluster's health at [Service Fabric health model introduction][service-fabric-health-introduction].</span></span>

> [!NOTE]
> <span data-ttu-id="dda6d-270">Klastrów sieci szkieletowej usług wymaga określonej liczby węzłów toobe zawsze toomaintain dostępności i Zachowaj stan — określonego tooas "utrzymywania kworum".</span><span class="sxs-lookup"><span data-stu-id="dda6d-270">Service Fabric clusters require a certain number of nodes toobe up always toomaintain availability and preserve state - referred tooas "maintaining quorum".</span></span> <span data-ttu-id="dda6d-271">Z tego, zwykle nie jest bezpieczne tooshut dół wszystkie komputery w klastrze hello, chyba że najpierw wykonali [pełnej kopii zapasowej według stanu][service-fabric-reliable-services-backup-restore].</span><span class="sxs-lookup"><span data-stu-id="dda6d-271">Therfore, it is typically not safe tooshut down all machines in hello cluster unless you have first performed a [full backup of your state][service-fabric-reliable-services-backup-restore].</span></span>
> 
> 

## <a name="remote-connect-tooa-virtual-machine-scale-set-instance-or-a-cluster-node"></a><span data-ttu-id="dda6d-272">Połączenie zdalne tooa wystąpienia zestawu skalowania maszyn wirtualnych lub węzła klastra</span><span class="sxs-lookup"><span data-stu-id="dda6d-272">Remote connect tooa Virtual Machine Scale Set instance or a cluster node</span></span>
<span data-ttu-id="dda6d-273">Każdy z elementów NodeType hello należy określić w wynikach klastra w zestawu skalowania maszyn wirtualnych pobieranie konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="dda6d-273">Each of hello NodeTypes you specify in your cluster results in a Virtual Machine Scale Set getting set-up.</span></span> <span data-ttu-id="dda6d-274">Zobacz [połączenie zdalne wystąpienia zestawu skalowania maszyn wirtualnych tooa] [ remote-connect-to-a-vm-scale-set] szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="dda6d-274">See [Remote connect tooa Virtual Machine Scale Set instance][remote-connect-to-a-vm-scale-set] for details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dda6d-275">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="dda6d-275">Next steps</span></span>
<span data-ttu-id="dda6d-276">W tym momencie masz bezpiecznego klastra przy użyciu certyfikatów dla uwierzytelniania zarządzania.</span><span class="sxs-lookup"><span data-stu-id="dda6d-276">At this point, you have a secure cluster using certificates for management authentication.</span></span> <span data-ttu-id="dda6d-277">Następnie [połączenia klastra tooyour](service-fabric-connect-to-secure-cluster.md) i Dowiedz się, jak za[Zarządzanie klucze tajne aplikacji](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="dda6d-277">Next, [connect tooyour cluster](service-fabric-connect-to-secure-cluster.md) and learn how too[manage application secrets](service-fabric-application-secret-management.md).</span></span>  <span data-ttu-id="dda6d-278">Zapoznaj się z [opcje pomocy technicznej usługi sieć szkieletowa](service-fabric-support.md).</span><span class="sxs-lookup"><span data-stu-id="dda6d-278">Also, learn about [Service Fabric support options](service-fabric-support.md).</span></span>

<!-- Links -->
[azure-powershell]: https://azure.microsoft.com/documentation/articles/powershell-install-configure/
[service-fabric-rp-helpers]: https://github.com/ChackDan/Service-Fabric/tree/master/Scripts/ServiceFabricRPHelpers
[azure-portal]: https://portal.azure.com/
[key-vault-get-started]: ../key-vault/key-vault-get-started.md
[create-cluster-arm]: service-fabric-cluster-creation-via-arm.md
[service-fabric-cluster-security]: service-fabric-cluster-security.md
[service-fabric-cluster-security-roles]: service-fabric-cluster-security-roles.md
[service-fabric-cluster-capacity]: service-fabric-cluster-capacity.md
[service-fabric-connect-and-communicate-with-services]: service-fabric-connect-and-communicate-with-services.md
[service-fabric-health-introduction]: service-fabric-health-introduction.md
[service-fabric-reliable-services-backup-restore]: service-fabric-reliable-services-backup-restore.md
[remote-connect-to-a-vm-scale-set]: service-fabric-cluster-nodetypes.md#remote-connect-to-a-vm-scale-set-instance-or-a-cluster-node
[service-fabric-cluster-upgrade]: service-fabric-cluster-upgrade.md

<!--Image references-->
[SearchforServiceFabricClusterTemplate]: ./media/service-fabric-cluster-creation-via-portal/SearchforServiceFabricClusterTemplate.png
[CreateRG]: ./media/service-fabric-cluster-creation-via-portal/CreateRG.png
[CreateNodeType]: ./media/service-fabric-cluster-creation-via-portal/NodeType.png
[SecurityConfigs]: ./media/service-fabric-cluster-creation-via-portal/SecurityConfigs.png
[Notifications]: ./media/service-fabric-cluster-creation-via-portal/notifications.png
[ClusterDashboard]: ./media/service-fabric-cluster-creation-via-portal/ClusterDashboard.png
[cluster-security-cert-installation]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-cert-installation.png
