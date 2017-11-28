---
title: "aaaAzure sieci szkieletowej usług z interfejsu API zarządzania szybki start | Dokumentacja firmy Microsoft"
description: "Ten przewodnik przedstawia, jak tooquickly wprowadzenie do usługi Azure API Management i sieci szkieletowej usług."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 96176149-69bb-4b06-a72e-ebbfea84454b
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: vturecek
ms.openlocfilehash: f76f3f39a92f89892d6a02ecaab1ec3d343fe2a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-with-azure-api-management-quick-start"></a><span data-ttu-id="15078-103">Sieć szkieletowa usług z usługi Azure API Management Szybki Start</span><span class="sxs-lookup"><span data-stu-id="15078-103">Service Fabric with Azure API Management Quick Start</span></span>

<span data-ttu-id="15078-104">W tym przewodniku przedstawiono jak tooset Konfigurowanie usługi Azure API Management z sieci szkieletowej usług i skonfigurować pierwszy interfejsu API operacji toosend ruchu tooback-end usług w sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="15078-104">This guide shows you how tooset up Azure API Management with Service Fabric and configure your first API operation toosend traffic tooback-end services in Service Fabric.</span></span> <span data-ttu-id="15078-105">toolearn więcej informacji na temat usługi Azure API Management scenariuszy z sieci szkieletowej usług, zobacz hello [omówienie](service-fabric-api-management-overview.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="15078-105">toolearn more about Azure API Management scenarios with Service Fabric, see hello [overview](service-fabric-api-management-overview.md) article.</span></span> 

## <a name="deploy-api-management-and-service-fabric-tooazure"></a><span data-ttu-id="15078-106">Wdrażanie tooAzure API Management i sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="15078-106">Deploy API Management and Service Fabric tooAzure</span></span>

<span data-ttu-id="15078-107">Witaj pierwszym krokiem jest toodeploy API Management i tooAzure klastra sieci szkieletowej usług w udostępnionym sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="15078-107">hello first step is toodeploy API Management and a Service Fabric cluster tooAzure in a shared Virtual Network.</span></span> <span data-ttu-id="15078-108">Dzięki temu zarządzanie interfejsami API toocommunicate bezpośrednio z usługi Service Fabric, który może wykonywać odnajdywania usługi, rozdzielczość partycji usługi i przekazywać ruch bezpośrednio tooany wewnętrznej bazy danych usługi w sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="15078-108">This allows API Management toocommunicate directly with Service Fabric so it can perform service discovery, service partition resolution, and forward traffic directly tooany backend service in Service Fabric.</span></span>

### <a name="topology"></a><span data-ttu-id="15078-109">Topologia</span><span class="sxs-lookup"><span data-stu-id="15078-109">Topology</span></span>

<span data-ttu-id="15078-110">Ten przewodnik wdrażania następujących hello tooAzure topologii, w którym interfejs API zarządzania i sieci szkieletowej usług znajdują się w podsieci hello tej samej sieci wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="15078-110">This guide deploys hello following topology tooAzure in which API Management and Service Fabric are in subnets of hello same Virtual Network:</span></span>

 ![Podpis obrazu][sf-apim-topology-overview]

<span data-ttu-id="15078-112">tooget szybko rozpocząć pracę, szablony usługi Resource Manager są dostępne dla każdego kroku wdrożenia:</span><span class="sxs-lookup"><span data-stu-id="15078-112">tooget started quickly, Resource Manager templates are provided for each deployment step:</span></span>

 - <span data-ttu-id="15078-113">Topologia sieci:</span><span class="sxs-lookup"><span data-stu-id="15078-113">Network topology:</span></span>
    - <span data-ttu-id="15078-114">[Network.JSON][network-arm]</span><span class="sxs-lookup"><span data-stu-id="15078-114">[network.json][network-arm]</span></span>
    - <span data-ttu-id="15078-115">[Network.parameters.JSON][network-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="15078-115">[network.parameters.json][network-parameters-arm]</span></span>
 - <span data-ttu-id="15078-116">Klaster sieci szkieletowej usług:</span><span class="sxs-lookup"><span data-stu-id="15078-116">Service Fabric cluster:</span></span>
    - <span data-ttu-id="15078-117">[cluster.JSON][cluster-arm]</span><span class="sxs-lookup"><span data-stu-id="15078-117">[cluster.json][cluster-arm]</span></span>
    - <span data-ttu-id="15078-118">[cluster.parameters.JSON][cluster-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="15078-118">[cluster.parameters.json][cluster-parameters-arm]</span></span>
 - <span data-ttu-id="15078-119">Zarządzanie interfejsami API:</span><span class="sxs-lookup"><span data-stu-id="15078-119">API Management:</span></span>
    - <span data-ttu-id="15078-120">[APIM.JSON][apim-arm]</span><span class="sxs-lookup"><span data-stu-id="15078-120">[apim.json][apim-arm]</span></span>
    - <span data-ttu-id="15078-121">[APIM.parameters.JSON][apim-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="15078-121">[apim.parameters.json][apim-parameters-arm]</span></span>

### <a name="sign-in-tooazure-and-select-your-subscription"></a><span data-ttu-id="15078-122">Zaloguj się tooAzure i wybierz subskrypcję</span><span class="sxs-lookup"><span data-stu-id="15078-122">Sign in tooAzure and select your subscription</span></span>

<span data-ttu-id="15078-123">Ten przewodnik po używa [programu Azure PowerShell][azure-powershell].</span><span class="sxs-lookup"><span data-stu-id="15078-123">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="15078-124">Po ponownym uruchomieniu nowej sesji programu PowerShell, zaloguj się tooyour konto platformy Azure i wybierz subskrypcję, przed wykonaniem polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="15078-124">When you start a new PowerShell session, sign in tooyour Azure account and select your subscription before you execute Azure commands.</span></span>
 
<span data-ttu-id="15078-125">Zaloguj się tooyour konto platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="15078-125">Sign in tooyour Azure account:</span></span>

```powershell
PS > Login-AzureRmAccount
```

<span data-ttu-id="15078-126">Wybierz subskrypcję:</span><span class="sxs-lookup"><span data-stu-id="15078-126">Select your subscription:</span></span>

```powershell
PS > Get-AzureRmSubscription
PS > Set-AzureRmContext -SubscriptionId <guid>
```

### <a name="create-a-resource-group"></a><span data-ttu-id="15078-127">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="15078-127">Create a resource group</span></span>

<span data-ttu-id="15078-128">Utwórz nową grupę zasobów dla danego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="15078-128">Create a new resource group for your deployment.</span></span> <span data-ttu-id="15078-129">Nadaj nazwę i lokalizację.</span><span class="sxs-lookup"><span data-stu-id="15078-129">Give it a name and a location.</span></span>

```powershell
PS > New-AzureRmResourceGroup -Name <my-resource-group> -Location westus
```

### <a name="deploy-hello-network-topology"></a><span data-ttu-id="15078-130">Wdrażanie hello topologii sieci</span><span class="sxs-lookup"><span data-stu-id="15078-130">Deploy hello network topology</span></span>

<span data-ttu-id="15078-131">Hello pierwszym krokiem jest tooset się toowhich topologii sieci hello interfejsu API zarządzania i zostanie wdrożony hello klastra sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="15078-131">hello first step is tooset up hello network topology toowhich API Management and hello Service Fabric cluster will be deployed.</span></span> <span data-ttu-id="15078-132">Witaj [network.json] [ network-arm] szablonu usługi Resource Manager jest skonfigurowany toocreate wirtualnych sieci (sieć Wirtualną) z dwoma podsieciami i dwie grupy zabezpieczeń sieci (NSG).</span><span class="sxs-lookup"><span data-stu-id="15078-132">hello [network.json][network-arm] Resource Manager template is configured toocreate a Virtual Network (VNET) with two subnets and two Network Security Groups (NSG).</span></span> 

<span data-ttu-id="15078-133">Witaj [network.parameters.json] [ network-parameters-arm] plik parametrów zawiera nazwy hello hello podsieci i grup NSG, które interfejs API zarządzania i sieci szkieletowej usług zostaną wdrożone do.</span><span class="sxs-lookup"><span data-stu-id="15078-133">hello [network.parameters.json][network-parameters-arm] parameters file contains hello names of hello subnets and NSGs that API Management and Service Fabric will be deployed to.</span></span> <span data-ttu-id="15078-134">Ten przewodnik wartości parametrów hello nie ma potrzeby toobe zmienione.</span><span class="sxs-lookup"><span data-stu-id="15078-134">For this guide, hello parameter values do not need toobe changed.</span></span> <span data-ttu-id="15078-135">Szablony API Management i Menedżer zasobów sieci szkieletowej usług Hello użyć tych wartości, jeśli zostaną zmodyfikowane w tym miejscu, należy zmodyfikować je w związku z tym hello innych szablonów usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="15078-135">hello API Management and Service Fabric Resource Manager templates use these values, so if they are modified here, you must modify them in hello other Resource Manager templates accordingly.</span></span> 

 1. <span data-ttu-id="15078-136">Pobierz hello następującego pliku szablonu i parametry Menedżera zasobów:</span><span class="sxs-lookup"><span data-stu-id="15078-136">Download hello following Resource Manager template and parameters file:</span></span>

    - <span data-ttu-id="15078-137">[Network.JSON][network-arm]</span><span class="sxs-lookup"><span data-stu-id="15078-137">[network.json][network-arm]</span></span>
    - <span data-ttu-id="15078-138">[Network.parameters.JSON][network-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="15078-138">[network.parameters.json][network-parameters-arm]</span></span>

 2. <span data-ttu-id="15078-139">Użyj hello następujące PowerShell polecenie toodeploy hello Menedżera zasobów szablonu i parametr pliki instalacji sieciowej hello:</span><span class="sxs-lookup"><span data-stu-id="15078-139">Use hello following PowerShell command toodeploy hello Resource Manager template and parameter files for hello network setup:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\network.json -TemplateParameterFile .\network.parameters.json -Verbose
    ```

### <a name="deploy-hello-service-fabric-cluster"></a><span data-ttu-id="15078-140">Wdrażanie klastra usługi sieć szkieletowa hello</span><span class="sxs-lookup"><span data-stu-id="15078-140">Deploy hello Service Fabric cluster</span></span>

<span data-ttu-id="15078-141">Po zasobów sieciowych hello zostało ukończone, wdrażanie, hello następnym krokiem jest toodeploy toohello klastra sieci szkieletowej usług sieci Wirtualnej w podsieci hello i NSG przeznaczone dla klastra usługi sieć szkieletowa hello.</span><span class="sxs-lookup"><span data-stu-id="15078-141">Once hello network resources have finished deploying, hello next step is toodeploy a Service Fabric cluster toohello VNET in hello subnet and NSG designated for hello Service Fabric cluster.</span></span> <span data-ttu-id="15078-142">W tym samouczku nazw hello toouse wstępnie skonfigurowane hello sieci Wirtualnej, podsieci i NSG, skonfigurowanym w poprzednim kroku hello jest hello szablon Menedżera zasobów sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="15078-142">For this tutorial, hello Service Fabric Resource Manager template is pre-configured toouse hello names of hello VNET, subnet, and NSG that you set up in hello previous step.</span></span> 

<span data-ttu-id="15078-143">Szablon usługi Resource Manager klastra usługi sieć szkieletowa Hello jest skonfigurowany toocreate bezpiecznego klastra z certyfikatu zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="15078-143">hello Service Fabric cluster Resource Manager template is configured toocreate a secure cluster with certificate security.</span></span> <span data-ttu-id="15078-144">certyfikat Hello jest komunikacji między węzłami toosecure używane dla klastra i klaster sieci szkieletowej usług tooyour toomanage użytkownika dostępu.</span><span class="sxs-lookup"><span data-stu-id="15078-144">hello certificate is used toosecure node-to-node communication for your cluster and toomanage user access tooyour Service Fabric cluster.</span></span> <span data-ttu-id="15078-145">Zarządzanie interfejsami API używa tego certyfikatu tooaccess hello Usługa nazewnictwa sieci szkieletowej dla potrzeb odnajdywania usług.</span><span class="sxs-lookup"><span data-stu-id="15078-145">API Management uses this certificate tooaccess  hello Service Fabric Naming Service for service discovery.</span></span>

<span data-ttu-id="15078-146">Ten krok wymaga mające certyfikat w magazynie kluczy dla zabezpieczeń klastra.</span><span class="sxs-lookup"><span data-stu-id="15078-146">This step requires having a certificate in Key Vault for cluster security.</span></span> <span data-ttu-id="15078-147">Aby uzyskać więcej informacji na temat konfigurowania bezpiecznej klastra z Key Vault, zobacz [ten przewodnik na temat tworzenia klastra na platformie Azure przy użyciu usługi Resource Manager](service-fabric-cluster-creation-via-arm.md)</span><span class="sxs-lookup"><span data-stu-id="15078-147">For more information on setting up a secure cluster with Key Vault, see [this guide on creating a cluster in Azure using Resource Manager](service-fabric-cluster-creation-via-arm.md)</span></span>

> [!NOTE]
> <span data-ttu-id="15078-148">Można dodać uwierzytelniania usługi Azure Active Directory w dodanie toohello certyfikatu używanego na potrzeby dostępu do klastra.</span><span class="sxs-lookup"><span data-stu-id="15078-148">You may add Azure Active Directory authentication in addition toohello certificate used for cluster access.</span></span> <span data-ttu-id="15078-149">Azure Active Directory jest hello zalecane klastra sieci szkieletowej usług tooyour dostępu sposób toomanage użytkownika, ale jest toocomplete nie jest konieczna w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="15078-149">Azure Active Directory is hello recommended way toomanage user access tooyour Service Fabric cluster, but is not necessary toocomplete this tutorial.</span></span> <span data-ttu-id="15078-150">Certyfikat jest wymagany niezależnie od sposobu zabezpieczenia węzła do węzła klastra, a do uwierzytelniania usługi Azure API Management, który obecnie nie obsługuje uwierzytelniania w usłudze Azure Active Directory dla usługi Service Fabric w wewnętrznej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="15078-150">A certificate is required either way for cluster node-to-node security and for Azure API Management authentication, which currently does not support authenticating with Azure Active Directory for a Service Fabric backend.</span></span>

 1. <span data-ttu-id="15078-151">Pobierz hello następującego pliku szablonu i parametry Menedżera zasobów:</span><span class="sxs-lookup"><span data-stu-id="15078-151">Download hello following Resource Manager template and parameters file:</span></span>
 
    - <span data-ttu-id="15078-152">[cluster.JSON][cluster-arm]</span><span class="sxs-lookup"><span data-stu-id="15078-152">[cluster.json][cluster-arm]</span></span>
    - <span data-ttu-id="15078-153">[cluster.parameters.JSON][cluster-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="15078-153">[cluster.parameters.json][cluster-parameters-arm]</span></span>

 2. <span data-ttu-id="15078-154">Wypełnij puste parametry hello w hello `cluster.parameters.json` plików dla danego wdrożenia, w tym hello [informacje magazynie klucza](service-fabric-cluster-creation-via-arm.md#set-up-a-key-vault) dla certyfikatu klastra.</span><span class="sxs-lookup"><span data-stu-id="15078-154">Fill in hello empty parameters in hello `cluster.parameters.json` file for your deployment, including hello [Key Vault information](service-fabric-cluster-creation-via-arm.md#set-up-a-key-vault) for your cluster certificate.</span></span>

 3. <span data-ttu-id="15078-155">Użyj hello następującego środowiska PowerShell polecenie toodeploy hello Menedżera zasobów szablonu i parametr pliki toocreate hello klastra sieci szkieletowej usług:</span><span class="sxs-lookup"><span data-stu-id="15078-155">Use hello following PowerShell command toodeploy hello Resource Manager template and parameter files toocreate hello Service Fabric cluster:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\cluster.json -TemplateParameterFile .\cluster.parameters.json -Verbose
    ```

### <a name="deploy-api-management"></a><span data-ttu-id="15078-156">Wdrażanie usługi API Management</span><span class="sxs-lookup"><span data-stu-id="15078-156">Deploy API Management</span></span>

<span data-ttu-id="15078-157">Ponadto należy wdrożyć toohello interfejsu API zarządzania sieciami Wirtualnymi w podsieci hello i NSG przeznaczone dla interfejsu API zarządzania.</span><span class="sxs-lookup"><span data-stu-id="15078-157">Finally, deploy API Management toohello VNET in hello subnet and NSG designated for API Management.</span></span> <span data-ttu-id="15078-158">Nie trzeba toowait dla toofinish wdrażania klastra usługi sieć szkieletowa hello przed wdrożeniem usługi API Management.</span><span class="sxs-lookup"><span data-stu-id="15078-158">You do not need toowait for hello Service Fabric cluster deployment toofinish before deploying API Management.</span></span> 

<span data-ttu-id="15078-159">W tym samouczku nazw hello toouse wstępnie skonfigurowane hello sieci Wirtualnej, podsieci i NSG, skonfigurowanym w poprzednim kroku hello jest hello szablonu interfejsu API zarządzania Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="15078-159">For this tutorial, hello API Management Resource Manager template is pre-configured toouse hello names of hello VNET, subnet, and NSG that you set up in hello previous step.</span></span> 

 1. <span data-ttu-id="15078-160">Pobierz hello następującego pliku szablonu i parametry Menedżera zasobów:</span><span class="sxs-lookup"><span data-stu-id="15078-160">Download hello following Resource Manager template and parameters file:</span></span>
 
    - <span data-ttu-id="15078-161">[APIM.JSON][apim-arm]</span><span class="sxs-lookup"><span data-stu-id="15078-161">[apim.json][apim-arm]</span></span>
    - <span data-ttu-id="15078-162">[APIM.parameters.JSON][apim-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="15078-162">[apim.parameters.json][apim-parameters-arm]</span></span>

 2. <span data-ttu-id="15078-163">Wypełnij puste parametry hello w hello `apim.parameters.json` dla danego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="15078-163">Fill in hello empty parameters in hello `apim.parameters.json` for your deployment.</span></span>

 3. <span data-ttu-id="15078-164">Użyj hello następujące PowerShell polecenie toodeploy hello Menedżera zasobów szablonu i parametr pliki dla interfejsu API zarządzania:</span><span class="sxs-lookup"><span data-stu-id="15078-164">Use hello following PowerShell command toodeploy hello Resource Manager template and parameter files for API Management:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\apim.json -TemplateParameterFile .\apim.parameters.json -Verbose
    ```

## <a name="configure-api-management"></a><span data-ttu-id="15078-165">Skonfiguruj zarządzanie interfejsami API</span><span class="sxs-lookup"><span data-stu-id="15078-165">Configure API Management</span></span>

<span data-ttu-id="15078-166">Po są wdrażane w klastrze API Management i sieci szkieletowej usług, można skonfigurować sieci szkieletowej usług w wewnętrznej bazie danych w usłudze API Management.</span><span class="sxs-lookup"><span data-stu-id="15078-166">Once your API Management and Service Fabric cluster are deployed, you can configure a Service Fabric backend in API Management.</span></span> <span data-ttu-id="15078-167">Dzięki temu toocreate zasadę usługi wewnętrznej bazy danych, która wysyła klastra sieci szkieletowej usług tooyour ruchu.</span><span class="sxs-lookup"><span data-stu-id="15078-167">This allows you toocreate a backend service policy that sends traffic tooyour Service Fabric cluster.</span></span>

### <a name="api-management-security"></a><span data-ttu-id="15078-168">Zabezpieczenia Management API</span><span class="sxs-lookup"><span data-stu-id="15078-168">API Management Security</span></span>

<span data-ttu-id="15078-169">tooconfigure hello sieci szkieletowej usług wewnętrznej bazy danych, należy najpierw ustawienia zabezpieczeń interfejsu API zarządzania tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="15078-169">tooconfigure hello Service Fabric backend, you first need tooconfigure API Management security settings.</span></span> <span data-ttu-id="15078-170">ustawienia zabezpieczeń tooconfigure, przejdź tooyour interfejsu API usługi zarządzania w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="15078-170">tooconfigure security settings, go tooyour API Management service in hello Azure portal.</span></span>

#### <a name="enable-hello-api-management-rest-api"></a><span data-ttu-id="15078-171">Włącz hello interfejsu API REST zarządzania interfejsu API</span><span class="sxs-lookup"><span data-stu-id="15078-171">Enable hello API Management REST API</span></span>

<span data-ttu-id="15078-172">Witaj interfejsu API REST zarządzania interfejsu API jest obecnie hello tylko sposób tooconfigure usługi wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="15078-172">hello API Management REST API is currently hello only way tooconfigure a backend service.</span></span> <span data-ttu-id="15078-173">pierwszym krokiem Hello jest hello tooenable interfejsu API REST zarządzania interfejsu API i zabezpieczyć.</span><span class="sxs-lookup"><span data-stu-id="15078-173">hello first step is tooenable hello API Management REST API and secure it.</span></span>

 1. <span data-ttu-id="15078-174">Hello usługi API Management, wybierz **API Management — wersja ZAPOZNAWCZA** w obszarze **zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="15078-174">In hello API Management service, select **Management API - PREVIEW** under **Security**.</span></span>
 2. <span data-ttu-id="15078-175">Sprawdź hello **Włącz interfejs API zarządzania interfejsu API REST** wyboru.</span><span class="sxs-lookup"><span data-stu-id="15078-175">Check hello **Enable API Management REST API** checkbox.</span></span>
 3. <span data-ttu-id="15078-176">Uwaga hello adres URL interfejsu API zarządzania — to jest adres URL hello użyjemy nowsze tooset się hello sieci szkieletowej usług zaplecza</span><span class="sxs-lookup"><span data-stu-id="15078-176">Note hello Management API URL - this is hello URL we'll use later tooset up hello Service Fabric backend</span></span>
 4. <span data-ttu-id="15078-177">Generuj **tokenu dostępu** wybierając datę wygaśnięcia oraz klucz, następnie kliknij przycisk hello **Generuj** przycisku w kierunku hello u dołu strony hello.</span><span class="sxs-lookup"><span data-stu-id="15078-177">Generate an **access Token** by selecting an expiry date and a key, then click hello **Generate** button toward hello bottom of hello page.</span></span>
 5. <span data-ttu-id="15078-178">Kopiuj hello **token dostępu** i zapisać go — użyjemy w hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="15078-178">Copy hello **access token** and save it - we'll use this in hello following steps.</span></span> <span data-ttu-id="15078-179">Należy zauważyć, że ta różni się od hello klucza podstawowego i pomocniczego klucza.</span><span class="sxs-lookup"><span data-stu-id="15078-179">Note this is different from hello primary key and secondary key.</span></span>

#### <a name="upload-a-service-fabric-client-certificate"></a><span data-ttu-id="15078-180">Przekaż certyfikat klienta sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="15078-180">Upload a Service Fabric client certificate</span></span>

<span data-ttu-id="15078-181">Zarządzanie interfejsami API musi uwierzytelniać się z klastrem usługi sieć szkieletowa usług dla potrzeb odnajdywania usług za pomocą certyfikatu klienta, który ma dostęp tooyour klastra.</span><span class="sxs-lookup"><span data-stu-id="15078-181">API Management must authenticate with your Service Fabric cluster for service discovery using a client certificate that has access tooyour cluster.</span></span> <span data-ttu-id="15078-182">Dla uproszczenia ten samouczek używa hello sam certyfikat określony podczas tworzenia klastra usługi sieć szkieletowa hello, które domyślnie mogą być używane tooaccess klastra.</span><span class="sxs-lookup"><span data-stu-id="15078-182">For simplicity, this tutorial uses hello same certificate specified when creating hello Service Fabric cluster, which by default can be used tooaccess your cluster.</span></span>

 1. <span data-ttu-id="15078-183">Hello usługi API Management, wybierz **certyfikatów klienta — w wersji ZAPOZNAWCZEJ** w obszarze **zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="15078-183">In hello API Management service, select **Client certificates - PREVIEW** under **Security**.</span></span>
 2. <span data-ttu-id="15078-184">Kliknij przycisk hello **+ Dodaj** przycisku</span><span class="sxs-lookup"><span data-stu-id="15078-184">Click hello **+ Add** button</span></span>
 2. <span data-ttu-id="15078-185">Wybierz hello pliku klucza prywatnego (pfx) hello klastra certyfikatu, który określone podczas tworzenia klastra usługi sieć szkieletowa, nadaj mu nazwę, a następnie podaj hasło klucza prywatnego hello.</span><span class="sxs-lookup"><span data-stu-id="15078-185">Select hello private key file (.pfx) of hello cluster certificate that you specified when creating your Service Fabric cluster, give it a name, and provide hello private key password.</span></span>

> [!NOTE]
> <span data-ttu-id="15078-186">Ten samouczek używa hello sam certyfikat bezpieczeństwa węzła do węzła klienta uwierzytelniania i klastra.</span><span class="sxs-lookup"><span data-stu-id="15078-186">This tutorial uses hello same certificate for client authentication and cluster node-to-node security.</span></span> <span data-ttu-id="15078-187">Certyfikat klienta w osobnym można używać, jeśli masz jeden tooaccess skonfigurowany klaster sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="15078-187">You may use a separate client certificate if you have one configured tooaccess your Service Fabric cluster.</span></span>

### <a name="configure-hello-backend"></a><span data-ttu-id="15078-188">Skonfiguruj hello wewnętrznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="15078-188">Configure hello backend</span></span>

<span data-ttu-id="15078-189">Teraz, gdy zabezpieczeń interfejsu API zarządzania jest skonfigurowany, można skonfigurować hello sieci szkieletowej usług zaplecza.</span><span class="sxs-lookup"><span data-stu-id="15078-189">Now that API Management security is configured, you can configure hello Service Fabric backend.</span></span> <span data-ttu-id="15078-190">W przypadku zapleczy sieci szkieletowej usług klastra sieci szkieletowej usług hello jest hello wewnętrznej bazy danych, a nie dla określonej usługi sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="15078-190">For Service Fabric backends, hello Service Fabric cluster is hello backend, rather than a specific Service Fabric service.</span></span> <span data-ttu-id="15078-191">Dzięki temu toomore tooroute w ramach jednych zasad, niż jedna usługa hello klastra.</span><span class="sxs-lookup"><span data-stu-id="15078-191">This allows a single policy tooroute toomore than one service in hello cluster.</span></span>

<span data-ttu-id="15078-192">Ten krok wymaga tokenu dostępu hello wcześniej wygenerowania i hello odcisk palca dla certyfikatu klastra się, że przekazano tooAPI zarządzania hello poprzedniego kroku.</span><span class="sxs-lookup"><span data-stu-id="15078-192">This step requires hello access token you generated earlier and hello thumbprint for your cluster certificate you uploaded tooAPI Management in hello previous step.</span></span>

> [!NOTE]
> <span data-ttu-id="15078-193">Jeśli używasz certyfikatu klienta w osobnym w poprzednim kroku powitania dla interfejsu API zarządzania należy hello odcisk palca dla certyfikatu klienta hello w dodanie toohello klastra odcisk palca certyfikatu w tym kroku.</span><span class="sxs-lookup"><span data-stu-id="15078-193">If you used a separate client certificate in hello previous step for API Management, you need hello thumbprint for hello client certificate in addition toohello cluster certificate thumbprint in this step.</span></span>

<span data-ttu-id="15078-194">Wyślij powitania po toohello żądanie HTTP PUT URL interfejsu API zarządzania interfejsu API zanotowaną wcześniej podczas włączania usługi wewnętrznej bazy danych usługi Service Fabric hello tooconfigure hello interfejsu API REST zarządzania interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="15078-194">Send hello following HTTP PUT request toohello API Management API URL you noted earlier when enabling hello API Management REST API tooconfigure hello Service Fabric backend service.</span></span> <span data-ttu-id="15078-195">Powinny pojawić się `HTTP 201 Created` odpowiedzi, gdy polecenia hello zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="15078-195">You should see an `HTTP 201 Created` response when hello command succeeds.</span></span> <span data-ttu-id="15078-196">Aby uzyskać więcej informacji na każde pole, zobacz hello zarządzanie interfejsami API [dokumentacji zaplecza interfejsu API](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend).</span><span class="sxs-lookup"><span data-stu-id="15078-196">For more information on each field, see hello API Management [backend API reference documentation](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend).</span></span>

<span data-ttu-id="15078-197">Polecenia HTTP i adres URL:</span><span class="sxs-lookup"><span data-stu-id="15078-197">HTTP command and URL:</span></span>
```http
PUT https://your-apim.management.azure-api.net/backends/servicefabric?api-version=2016-10-10
```

<span data-ttu-id="15078-198">Nagłówki żądania:</span><span class="sxs-lookup"><span data-stu-id="15078-198">Request headers:</span></span>
```http
Authorization: SharedAccessSignature <your access token>
Content-Type: application/json
```

<span data-ttu-id="15078-199">Treść żądania:</span><span class="sxs-lookup"><span data-stu-id="15078-199">Request body:</span></span>
```http
{
    "description": "<description>",
    "url": "<fallback service name>",
    "protocol": "http",
    "resourceId": "<cluster HTTP management endpoint>",
    "properties": {
        "serviceFabricCluster": {
            "managementEndpoints": [ "<cluster HTTP management endpoint>" ],
            "clientCertificateThumbprint": "<client cert thumbprint>",
            "serverCertificateThumbprints": [ "<cluster cert thumbprint>" ],
            "maxPartitionResolutionRetries" : 5
        }
    }
}
```

<span data-ttu-id="15078-200">Witaj **adres url** parametru w tym miejscu jest usługi w pełni kwalifikowaną nazwę usługi w klastrze, które są wszystkie żądania kierowane tooby domyślne, jeśli nazwa usługi, nie jest określona w zasadzie wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="15078-200">hello **url** parameter here is a fully-qualified service name of a service in your cluster that all requests are routed tooby default if no service name is specified in a backend policy.</span></span> <span data-ttu-id="15078-201">Może używać nazw fałszywych usług, takich jak "fabric: fałszywych/service" Jeśli nie chcesz, aby toohave usługę rezerwowy.</span><span class="sxs-lookup"><span data-stu-id="15078-201">You may use a fake service name, such as "fabric:/fake/service" if you do not intend toohave a fallback service.</span></span>

<span data-ttu-id="15078-202">Zobacz toohello zarządzanie interfejsami API [interfejs API zaplecza dokumentacji](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend) uzyskać więcej informacji dotyczących każdego pola.</span><span class="sxs-lookup"><span data-stu-id="15078-202">Refer toohello API Management [backend API reference documentation](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend) for more details on each field.</span></span>

#### <a name="example"></a><span data-ttu-id="15078-203">Przykład</span><span class="sxs-lookup"><span data-stu-id="15078-203">Example</span></span>

```http
PUT https://your-apim.management.azure-api.net/backends/servicefabric?api-version=2016-10-10
Authorization: SharedAccessSignature 230948023984&Ld93cRGcNU6KZ4uVz7JlfTec4eX43Q9Nu8ndatOgBzs6+f559Pkf3iHX2cSge+r42pn35qGY3TitjrIl13hwcQ==
Content-Type: application/json

{
    "description": "My Service Fabric backend",
    "url": "fabric:/myapp/myservice",
    "protocol": "http",
    "resourceId": "https://your-cluster.westus.cloudapp.azure.com:19080",
    "properties": {
        "serviceFabricCluster": {
            "managementEndpoints": ["https://your-cluster.westus.cloudapp.azure.com:19080"],
            "clientCertificateThumbprint": "57bc463aba3aea3a12a18f36f44154f819f0fe32",
            "serverCertificateThumbprints": ["57bc463aba3aea3a12a18f36f44154f819f0fe32"],
            "maxPartitionResolutionRetries" : 5
        }
    }
}
```

## <a name="deploy-a-service-fabric-back-end-service"></a><span data-ttu-id="15078-204">Wdrażanie usługi zaplecza sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="15078-204">Deploy a Service Fabric back-end service</span></span>

<span data-ttu-id="15078-205">Teraz, gdy masz powitalne sieci szkieletowej usług skonfigurowany jako tooAPI wewnętrznej bazy danych zarządzania można tworzyć zasady wewnętrznej bazy danych dla interfejsów API, które przesyłają tooyour usługi sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="15078-205">Now that you have hello Service Fabric configured as a backend tooAPI Management, you can author backend policies for your APIs that send traffic tooyour Service Fabric services.</span></span> <span data-ttu-id="15078-206">Ale najpierw należy w usłudze działającej w żądaniach tooaccept sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="15078-206">But first you need a service running in Service Fabric tooaccept requests.</span></span>

### <a name="create-a-service-fabric-service-with-an-http-endpoint"></a><span data-ttu-id="15078-207">Tworzenie usługi sieć szkieletowa usług za pomocą punktu końcowego HTTP</span><span class="sxs-lookup"><span data-stu-id="15078-207">Create a Service Fabric service with an HTTP endpoint</span></span>

<span data-ttu-id="15078-208">W tym samouczku utworzymy podstawowe bezstanowej platformy ASP.NET Core niezawodnej usługi za pomocą hello domyślny szablon projektu interfejsu API sieci Web.</span><span class="sxs-lookup"><span data-stu-id="15078-208">For this tutorial, we'll create a basic stateless ASP.NET Core Reliable Service using hello default Web API project template.</span></span> <span data-ttu-id="15078-209">Spowoduje to utworzenie punktu końcowego HTTP dla usługi, która będzie udostępnić za pośrednictwem usługi Azure API Management:</span><span class="sxs-lookup"><span data-stu-id="15078-209">This creates an HTTP endpoint for your service, which you'll expose through Azure API Management:</span></span>

```
/api/values
```

<span data-ttu-id="15078-210">Rozpocznij od [Konfigurowanie środowiska programowania do tworzenia aplikacji platformy ASP.NET Core](service-fabric-add-a-web-frontend.md#set-up-your-environment-for-aspnet-core).</span><span class="sxs-lookup"><span data-stu-id="15078-210">Start by [setting up your development environment for ASP.NET Core development](service-fabric-add-a-web-frontend.md#set-up-your-environment-for-aspnet-core).</span></span>

<span data-ttu-id="15078-211">Po skonfigurowaniu środowiska projektowego, uruchom program Visual Studio jako Administrator i Utwórz usługę platformy ASP.NET Core:</span><span class="sxs-lookup"><span data-stu-id="15078-211">Once your development environment is set up, start Visual Studio as Administrator and create an ASP.NET Core service:</span></span>

 1. <span data-ttu-id="15078-212">W programie Visual Studio wybierz Plik -> Nowy projekt.</span><span class="sxs-lookup"><span data-stu-id="15078-212">In Visual Studio, select File -> New Project.</span></span>
 2. <span data-ttu-id="15078-213">Wybierz hello szablonu aplikacji sieci szkieletowej usług w chmurze i nadaj mu nazwę **"ApiApplication"**.</span><span class="sxs-lookup"><span data-stu-id="15078-213">Select hello Service Fabric Application template under Cloud and name it **"ApiApplication"**.</span></span>
 3. <span data-ttu-id="15078-214">Wybierz hello platformy ASP.NET Core szablonu usługi i nazwę projektu hello **"WebApiService"**.</span><span class="sxs-lookup"><span data-stu-id="15078-214">Select hello ASP.NET Core service template and name hello project **"WebApiService"**.</span></span>
 4. <span data-ttu-id="15078-215">Wybierz szablon projektu hello Web API platformy ASP.NET Core 1.1.</span><span class="sxs-lookup"><span data-stu-id="15078-215">Select hello Web API ASP.NET Core 1.1 project template.</span></span>
 5. <span data-ttu-id="15078-216">Po utworzeniu projektu hello Otwórz `PackageRoot\ServiceManifest.xml` i Usuń hello `Port` atrybut z konfiguracji zasobu punktu końcowego hello:</span><span class="sxs-lookup"><span data-stu-id="15078-216">Once hello project is created, open `PackageRoot\ServiceManifest.xml` and remove hello `Port` attribute from hello endpoint resource configuration:</span></span>
 
    ```xml
    <Resources>
      <Endpoints>
        <Endpoint Protocol="http" Name="ServiceEndpoint" Type="Input" />
      </Endpoints>
    </Resources>
    ```

    <span data-ttu-id="15078-217">Dzięki temu usługi sieć szkieletowa toospecify port dynamicznie z zakresu portów aplikacji hello, którego możemy otworzyć za pomocą hello sieciowej grupy zabezpieczeń w szablonie usługi Resource Manager klastra hello, dzięki czemu ruch tooflow tooit z interfejsu API zarządzania.</span><span class="sxs-lookup"><span data-stu-id="15078-217">This allows Service Fabric toospecify a port dynamically from hello application port range, which we opened through hello Network Security Group in hello cluster Resource Manager template, allowing traffic tooflow tooit from API Management.</span></span>
 
 6. <span data-ttu-id="15078-218">Naciśnij klawisz F5 w programie Visual Studio tooverify hello interfejsu API sieci web jest dostępna lokalnie.</span><span class="sxs-lookup"><span data-stu-id="15078-218">Press F5 in Visual Studio tooverify hello web API is available locally.</span></span> 

    <span data-ttu-id="15078-219">Otwórz Eksploratora usługi sieć szkieletowa i przechodzenie do szczegółów tooa konkretne wystąpienie hello platformy ASP.NET Core toosee hello adres podstawowy hello usługa nasłuchuje.</span><span class="sxs-lookup"><span data-stu-id="15078-219">Open Service Fabric Explorer and drill down tooa specific instance of hello ASP.NET Core service toosee hello base address hello service is listening on.</span></span> <span data-ttu-id="15078-220">Dodaj `/api/values` toohello adresem podstawowym i otwórz go w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="15078-220">Add `/api/values` toohello base address and open it in a browser.</span></span> <span data-ttu-id="15078-221">Wywołuje to hello metody Get na powitania ValuesController hello szablonu interfejsu API sieci Web.</span><span class="sxs-lookup"><span data-stu-id="15078-221">This invokes hello Get method on hello ValuesController in hello Web API template.</span></span> <span data-ttu-id="15078-222">Zwraca odpowiedź domyślna hello dostarczone przez szablon hello, tablicy JSON, który zawiera dwa ciągi:</span><span class="sxs-lookup"><span data-stu-id="15078-222">It returns hello default response that is provided by hello template, a JSON array that contains two strings:</span></span>

    ```json
    ["value1", "value2"]`
    ```

    <span data-ttu-id="15078-223">To jest punkt końcowy hello, który będzie udostępnić za pośrednictwem interfejsu API zarządzania na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="15078-223">This is hello endpoint that you'll expose through API Management in Azure.</span></span>

 7. <span data-ttu-id="15078-224">Ponadto wdrożyć klaster tooyour aplikacji hello na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="15078-224">Finally, deploy hello application tooyour cluster in Azure.</span></span> <span data-ttu-id="15078-225">[Za pomocą programu Visual Studio](service-fabric-publish-app-remote-cluster.md#to-publish-an-application-using-the-publish-service-fabric-application-dialog-box), kliknij prawym przyciskiem myszy projekt aplikacji hello i wybierz **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="15078-225">[Using Visual Studio](service-fabric-publish-app-remote-cluster.md#to-publish-an-application-using-the-publish-service-fabric-application-dialog-box), right-click hello Application project and select **Publish**.</span></span> <span data-ttu-id="15078-226">Podaj punkt końcowy klastra (na przykład `mycluster.westus.cloudapp.azure.com:19000`) tooyour aplikacji hello toodeploy sieci szkieletowej usług klastra na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="15078-226">Provide your cluster endpoint (for example, `mycluster.westus.cloudapp.azure.com:19000`) toodeploy hello application tooyour Service Fabric cluster in Azure.</span></span>

<span data-ttu-id="15078-227">Usługi bezstanowej platformy ASP.NET Core o nazwie `fabric:/ApiApplication/WebApiService` teraz powinna być uruchomiona w klastrze usługi sieć szkieletowa na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="15078-227">An ASP.NET Core stateless service named `fabric:/ApiApplication/WebApiService` should now be running in your Service Fabric cluster in Azure.</span></span>

## <a name="create-an-api-operation"></a><span data-ttu-id="15078-228">Tworzenie operacji interfejsu API</span><span class="sxs-lookup"><span data-stu-id="15078-228">Create an API operation</span></span>

<span data-ttu-id="15078-229">Teraz jest gotowy toocreate operacji w usłudze API Management tego toocommunicate używany przez klientów zewnętrznych z hello uruchamiania w klastrze usługi sieć szkieletowa hello usługi bezstanowej platformy ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="15078-229">Now we're ready toocreate an operation in API Management that external clients use toocommunicate with hello ASP.NET Core stateless service running in hello Service Fabric cluster.</span></span>

 1. <span data-ttu-id="15078-230">Zaloguj się za toohello portalu Azure i przejdź do wdrożenia usługi Zarządzanie interfejsami API tooyour.</span><span class="sxs-lookup"><span data-stu-id="15078-230">Log in toohello Azure portal and navigate tooyour API Management service deployment.</span></span>
 2. <span data-ttu-id="15078-231">W bloku usługi Zarządzanie interfejsami API hello, wybierz **interfejsów API — wersja zapoznawcza**</span><span class="sxs-lookup"><span data-stu-id="15078-231">In hello API Management service blade, select **APIs - Preview**</span></span>
 3. <span data-ttu-id="15078-232">Dodaj nowy interfejs API, klikając hello **puste API** pole i wypełniania okno dialogowe hello:</span><span class="sxs-lookup"><span data-stu-id="15078-232">Add a new API by clicking hello **Blank API** box and filling out hello dialog box:</span></span>

     - <span data-ttu-id="15078-233">**Adres URL usługi sieci Web**: dla sieci szkieletowej usług zapleczy, ta wartość adresu URL nie jest używany.</span><span class="sxs-lookup"><span data-stu-id="15078-233">**Web service URL**: For Service Fabric backends, this URL value is not used.</span></span> <span data-ttu-id="15078-234">Tutaj możesz umieścić żadnej wartości.</span><span class="sxs-lookup"><span data-stu-id="15078-234">You can put any value here.</span></span> <span data-ttu-id="15078-235">W tym samouczku, użyj: `http://servicefabric`.</span><span class="sxs-lookup"><span data-stu-id="15078-235">For this tutorial, use: `http://servicefabric`.</span></span>
     - <span data-ttu-id="15078-236">**Nazwa**: Podaj dowolną nazwę interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="15078-236">**Name**: Provide any name for your API.</span></span> <span data-ttu-id="15078-237">W tym samouczku, użyj `Service Fabric App`.</span><span class="sxs-lookup"><span data-stu-id="15078-237">For this tutorial, use `Service Fabric App`.</span></span>
     - <span data-ttu-id="15078-238">**Schemat adresu URL**: Wybierz HTTP, HTTPS lub obu.</span><span class="sxs-lookup"><span data-stu-id="15078-238">**URL scheme**: Select either HTTP, HTTPS, or both.</span></span> <span data-ttu-id="15078-239">W tym samouczku, użyj `both`.</span><span class="sxs-lookup"><span data-stu-id="15078-239">For this tutorial, use `both`.</span></span>
     - <span data-ttu-id="15078-240">**Sufiks adresu URL interfejsu API**: Podaj sufiks na interfejsie API.</span><span class="sxs-lookup"><span data-stu-id="15078-240">**API URL Suffix**: Provide a suffix for our API.</span></span> <span data-ttu-id="15078-241">W tym samouczku, użyj `myapp`.</span><span class="sxs-lookup"><span data-stu-id="15078-241">For this tutorial, use `myapp`.</span></span>
 
 4. <span data-ttu-id="15078-242">Po utworzeniu hello interfejsu API, kliknij przycisk **+ Dodaj operację** operacji tooadd frontonu interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="15078-242">Once hello API is created, click **+ Add operation** tooadd a front-end API operation.</span></span> <span data-ttu-id="15078-243">Wypełnianie hello wartości:</span><span class="sxs-lookup"><span data-stu-id="15078-243">Fill out hello values:</span></span>
    
     - <span data-ttu-id="15078-244">**Adres URL**: Wybierz `GET` i podaj ścieżkę adresu URL dla hello interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="15078-244">**URL**: Select `GET` and provide a URL path for hello API.</span></span> <span data-ttu-id="15078-245">W tym samouczku, użyj `/api/values`.</span><span class="sxs-lookup"><span data-stu-id="15078-245">For this tutorial, use `/api/values`.</span></span>
     
       <span data-ttu-id="15078-246">Domyślnie program hello ścieżki adresu URL określone w tym miejscu są wysyłane hello ścieżki adresu URL usługi sieci szkieletowej usług zaplecza toohello.</span><span class="sxs-lookup"><span data-stu-id="15078-246">By default, hello URL path specified here is hello URL path sent toohello backend Service Fabric service.</span></span> <span data-ttu-id="15078-247">Jeśli używasz hello tej samej ścieżki adresu URL w tym miejscu używanego z usługą, w tym przypadku `/api/values`, następnie hello działa bez dalszej modyfikacji.</span><span class="sxs-lookup"><span data-stu-id="15078-247">If you use hello same URL path here that your service uses, in this case `/api/values`, then hello operation works without further modification.</span></span> <span data-ttu-id="15078-248">Może również określić ścieżki adresu URL w tym miejscu, który różni się od ścieżki adresu URL hello korzystali z wewnętrzną bazą danych usługi Service Fabric, w którym to przypadku będą również toospecify należy ścieżką przepisywania w zasadach operację później.</span><span class="sxs-lookup"><span data-stu-id="15078-248">You may also specify a URL path here that is different from hello URL path used by your backend Service Fabric service, in which case you will also need toospecify a path rewrite in your operation policy later.</span></span>
     - <span data-ttu-id="15078-249">**Nazwa wyświetlana**: Podaj nazwę dowolnego hello interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="15078-249">**Display name**: Provide any name for hello API.</span></span> <span data-ttu-id="15078-250">W tym samouczku, użyj `Values`.</span><span class="sxs-lookup"><span data-stu-id="15078-250">For this tutorial, use `Values`.</span></span>

## <a name="configure-a-backend-policy"></a><span data-ttu-id="15078-251">Skonfiguruj zasady wewnętrznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="15078-251">Configure a backend policy</span></span>

<span data-ttu-id="15078-252">zasady zaplecza Hello wiąże co wszystko.</span><span class="sxs-lookup"><span data-stu-id="15078-252">hello backend policy ties everything together.</span></span> <span data-ttu-id="15078-253">Jest to, gdzie skonfigurować hello wewnętrznej bazy danych są kierowane żądania toowhich usługi sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="15078-253">This is where you configure hello backend Service Fabric service toowhich requests are routed.</span></span> <span data-ttu-id="15078-254">Można zastosować operacji interfejsu API tooany tej zasady.</span><span class="sxs-lookup"><span data-stu-id="15078-254">You can apply this policy tooany API operation.</span></span> <span data-ttu-id="15078-255">Witaj [wewnętrznej bazy danych konfiguracji sieci szkieletowej usług](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService) zapewnia następujące hello żądania routingu formantów:</span><span class="sxs-lookup"><span data-stu-id="15078-255">hello [backend configuration for Service Fabric](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService) provides hello following request routing controls:</span></span> 
 - <span data-ttu-id="15078-256">Usługa Wybór wystąpienia, określając nazwę wystąpienia usługi Service Fabric, albo zapisane na stałe (na przykład `"fabric:/myapp/myservice"`) lub generowane na podstawie żądania hello HTTP (na przykład `"fabric:/myapp/users/" + context.Request.MatchedParameters["name"]`).</span><span class="sxs-lookup"><span data-stu-id="15078-256">Service instance selection by specifying a Service Fabric service instance name, either hardcoded (for example, `"fabric:/myapp/myservice"`) or generated from hello HTTP request (for example, `"fabric:/myapp/users/" + context.Request.MatchedParameters["name"]`).</span></span>
 - <span data-ttu-id="15078-257">Rozdzielczość partycji przez generowanie klucza partycji przy użyciu dowolnego schemat partycjonowania sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="15078-257">Partition resolution by generating a partition key using any Service Fabric partitioning scheme.</span></span>
 - <span data-ttu-id="15078-258">Wybór repliki dla stanowych usług.</span><span class="sxs-lookup"><span data-stu-id="15078-258">Replica selection for stateful services.</span></span>
 - <span data-ttu-id="15078-259">Rozdzielczość ponów warunki, które należy spełnić warunki hello toospecify ponowne rozpoznanie lokalizację usługi i wysłać żądanie.</span><span class="sxs-lookup"><span data-stu-id="15078-259">Resolution retry conditions that allow you toospecify hello conditions for re-resolving a service location and resending a request.</span></span>

<span data-ttu-id="15078-260">W tym samouczku Utwórz zasadę wewnętrznej bazy danych trasy żądań bezpośrednio toohello platformy ASP.NET Core usługi bezstanowej wdrożonej wcześniej:</span><span class="sxs-lookup"><span data-stu-id="15078-260">For this tutorial, create a backend policy that routes requests directly toohello ASP.NET Core stateless service deployed earlier:</span></span>

 1. <span data-ttu-id="15078-261">Wybierz i edytować hello **przychodzących zasad** dla hello `Values` operacji, klikając ikonę edycji hello, a następnie wybierając **widoku kodu**.</span><span class="sxs-lookup"><span data-stu-id="15078-261">Select and edit hello **inbound policies** for hello `Values` operation by clicking hello edit icon, and then selecting **Code View**.</span></span>
 2. <span data-ttu-id="15078-262">W edytorze kodu hello zasad, Dodaj `set-backend-service` zasad w obszarze zasady ruchu przychodzącego, jak pokazano poniżej i kliknij przycisk hello **zapisać** przycisk:</span><span class="sxs-lookup"><span data-stu-id="15078-262">In hello policy code editor, add a `set-backend-service` policy under inbound policies as shown here and click hello **Save** button:</span></span>
    
    ```xml
    <policies>
      <inbound>
        <base/>
        <set-backend-service 
           backend-id="servicefabric"
           sf-service-instance-name="fabric:/ApiApplication/WebApiService"
           sf-resolve-condition="@((int)context.Response.StatusCode != 200)" />
      </inbound>
      <backend>
        <base/>
      </backend>
      <outbound>
        <base/>
      </outbound>
    </policies>
    ```

<span data-ttu-id="15078-263">Pełny zestaw atrybutów wewnętrznych zasad sieci szkieletowej usług można znaleźć w temacie toohello [dokumentacji zaplecza interfejsu API zarządzania](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService)</span><span class="sxs-lookup"><span data-stu-id="15078-263">For a full set of Service Fabric back-end policy attributes, refer toohello [API Management back-end documentation](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService)</span></span>

### <a name="add-hello-api-tooa-product"></a><span data-ttu-id="15078-264">Dodaj hello interfejsu API tooa produktu.</span><span class="sxs-lookup"><span data-stu-id="15078-264">Add hello API tooa product.</span></span> 

<span data-ttu-id="15078-265">Przed wywołaniem interfejsu API hello, należy dodać go tooa produktu, którym udzielasz dostępu toousers.</span><span class="sxs-lookup"><span data-stu-id="15078-265">Before you can call hello API, it must be added tooa product where you can grant access toousers.</span></span> 

 1. <span data-ttu-id="15078-266">Hello usługi API Management, wybierz **produktów - PREVIEW**.</span><span class="sxs-lookup"><span data-stu-id="15078-266">In hello API Management service, select **Products - PREVIEW**.</span></span>
 2. <span data-ttu-id="15078-267">Domyślnie produkty przeznaczone do interfejsu API zarządzania dwóch dostawców: Starter i bez ograniczeń.</span><span class="sxs-lookup"><span data-stu-id="15078-267">By default, API Management providers two products: Starter and Unlimited.</span></span> <span data-ttu-id="15078-268">Wybierz hello nieograniczone produktu.</span><span class="sxs-lookup"><span data-stu-id="15078-268">Select hello Unlimited product.</span></span>
 3. <span data-ttu-id="15078-269">Wybierz interfejsy API.</span><span class="sxs-lookup"><span data-stu-id="15078-269">Select APIs.</span></span>
 4. <span data-ttu-id="15078-270">Kliknij przycisk hello **+ Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="15078-270">Click hello **+ Add** button.</span></span>
 5. <span data-ttu-id="15078-271">Wybierz hello `Service Fabric App` interfejsu API utworzone w poprzednich krokach hello i kliknij przycisk hello **wybierz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="15078-271">Select hello `Service Fabric App` API you created in hello previous steps and click hello **Select** button.</span></span>

### <a name="test-it"></a><span data-ttu-id="15078-272">należy przeprowadzić test</span><span class="sxs-lookup"><span data-stu-id="15078-272">Test it</span></span>

<span data-ttu-id="15078-273">Teraz możesz spróbować wysyła żądanie usługi zaplecza tooyour w sieci szkieletowej usług za pośrednictwem interfejsu API zarządzania bezpośrednio z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="15078-273">You can now try sending a request tooyour back-end service in Service Fabric through API Management directly from hello Azure portal.</span></span>

 1. <span data-ttu-id="15078-274">Hello usługi API Management, wybierz **interfejsu API — wersja ZAPOZNAWCZA**.</span><span class="sxs-lookup"><span data-stu-id="15078-274">In hello API Management service, select **API - PREVIEW**.</span></span>
 2. <span data-ttu-id="15078-275">W hello `Service Fabric App` interfejsu API utworzone w poprzednich krokach hello, wybierz hello **testu** kartę.</span><span class="sxs-lookup"><span data-stu-id="15078-275">In hello `Service Fabric App` API you created in hello previous steps, select hello **Test** tab.</span></span>
 3. <span data-ttu-id="15078-276">Kliknij przycisk hello **wysyłania** toosend przycisk test żądania toohello wewnętrznej bazy danych usługi.</span><span class="sxs-lookup"><span data-stu-id="15078-276">Click hello **Send** button toosend a test request toohello backend service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="15078-277">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="15078-277">Next steps</span></span>

<span data-ttu-id="15078-278">W tym momencie powinny mieć podstawowe ustawienia z interfejsu API zarządzania i sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="15078-278">At this point, you should have a basic setup with Service Fabric and API Management.</span></span>

<span data-ttu-id="15078-279">W tym samouczku korzysta z uwierzytelniania opartego na certyfikatach użytkownika podstawowego dla Twojego tooget klastra sieci szkieletowej usług, który można szybko skonfigurować.</span><span class="sxs-lookup"><span data-stu-id="15078-279">This tutorial uses basic certificate-based user authentication for your Service Fabric cluster tooget you set up quickly.</span></span> <span data-ttu-id="15078-280">Bardziej zaawansowanego uwierzytelniania użytkownika dla klastra usługi sieć szkieletowa jest preferowana w [uwierzytelniania usługi Azure Active Directory](service-fabric-cluster-creation-via-arm.md#set-up-azure-active-directory-for-client-authentication).</span><span class="sxs-lookup"><span data-stu-id="15078-280">More advanced user authentication for your Service Fabric cluster is preferable with [Azure Active Directory authentication](service-fabric-cluster-creation-via-arm.md#set-up-azure-active-directory-for-client-authentication).</span></span> 

<span data-ttu-id="15078-281">Następnie [utworzyć i skonfigurować ustawienia zaawansowane produktu w usłudze Azure API Management](https://docs.microsoft.com/azure/api-management/api-management-howto-product-with-rules) tooprepare aplikacji dla ruchu w świecie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="15078-281">Next, [create and configure advanced product settings in Azure API Management](https://docs.microsoft.com/azure/api-management/api-management-howto-product-with-rules) tooprepare your application for real world traffic.</span></span>

<!-- links -->
[azure-powershell]:https://azure.microsoft.com/documentation/articles/powershell-install-configure/

[network-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/network.json
[network-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/network.parameters.json

[apim-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/apim.json
[apim-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/apim.parameters.json

[cluster-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/cluster.json
[cluster-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/cluster.parameters.json


<!-- pics -->
[sf-apim-topology-overview]: ./media/service-fabric-api-management-quickstart/sf-apim-topology-overview.png
