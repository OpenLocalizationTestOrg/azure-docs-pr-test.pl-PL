---
title: "podmiot zabezpieczeń aaaService klastra Azure Kubernetes | Dokumentacja firmy Microsoft"
description: "Tworzenie jednostki usługi Azure Active Directory dla klastra Kubernetes w usłudze Azure Container Service i zarządzanie nią"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/08/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 7a01624c5ac3fa717dbcbd570e05ceb4d917c53a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-an-azure-ad-service-principal-for-a-kubernetes-cluster-in-container-service"></a><span data-ttu-id="da6c7-103">Konfigurowanie jednostki usługi Azure AD dla klastra Kubernetes w usłudze Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="da6c7-103">Set up an Azure AD service principal for a Kubernetes cluster in Container Service</span></span>


<span data-ttu-id="da6c7-104">W usłudze kontenera platformy Azure, wymaga klastra Kubernetes [nazwy głównej usługi Azure Active Directory](../../active-directory/develop/active-directory-application-objects.md) toointeract z interfejsami API Azure.</span><span class="sxs-lookup"><span data-stu-id="da6c7-104">In Azure Container Service, a Kubernetes cluster requires an [Azure Active Directory service principal](../../active-directory/develop/active-directory-application-objects.md) toointeract with Azure APIs.</span></span> <span data-ttu-id="da6c7-105">Witaj nazwy głównej usługi jest wymagane toodynamically zarządzanie zasobami, takich jak [trasy zdefiniowane przez użytkownika](../../virtual-network/virtual-networks-udr-overview.md) i hello [równoważenia obciążenia Azure 4 warstwy](../../load-balancer/load-balancer-overview.md).</span><span class="sxs-lookup"><span data-stu-id="da6c7-105">hello service principal is needed toodynamically manage resources such as [user-defined routes](../../virtual-network/virtual-networks-udr-overview.md) and hello [Layer 4 Azure Load Balancer](../../load-balancer/load-balancer-overview.md).</span></span> 


<span data-ttu-id="da6c7-106">W tym artykule przedstawiono różne opcje tooset usługi głównej dla klastra Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="da6c7-106">This article shows different options tooset up a service principal for your Kubernetes cluster.</span></span> <span data-ttu-id="da6c7-107">Na przykład, jeśli zostanie zainstalowany i skonfigurowany hello [Azure CLI 2.0](/cli/azure/install-az-cli2), możesz uruchomić hello [ `az acs create` ](/cli/azure/acs#create) polecenia toocreate hello Kubernetes głównej na powitania usługi klastrowania i hello tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="da6c7-107">For example, if you installed and set up hello [Azure CLI 2.0](/cli/azure/install-az-cli2), you can run hello [`az acs create`](/cli/azure/acs#create) command toocreate hello Kubernetes cluster and hello service principal at hello same time.</span></span>


## <a name="requirements-for-hello-service-principal"></a><span data-ttu-id="da6c7-108">Wymagania dotyczące hello nazwy głównej usługi</span><span class="sxs-lookup"><span data-stu-id="da6c7-108">Requirements for hello service principal</span></span>

<span data-ttu-id="da6c7-109">Można użyć istniejącej usługi Azure AD nazwy głównej usługi spełnia hello wymogów lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="da6c7-109">You can use an existing Azure AD service principal that meets hello following requirements, or create a new one.</span></span>

* <span data-ttu-id="da6c7-110">**Zakres**: hello grupy zasobów w subskrypcji hello używane toodeploy hello Kubernetes klastra lub (mniej twierdzi) hello subskrypcji używane toodeploy hello klastra.</span><span class="sxs-lookup"><span data-stu-id="da6c7-110">**Scope**: hello resource group in hello subscription used toodeploy hello Kubernetes cluster, or (less restrictively) hello subscription used toodeploy hello cluster.</span></span>

* <span data-ttu-id="da6c7-111">**Rola**: **Współautor**</span><span class="sxs-lookup"><span data-stu-id="da6c7-111">**Role**: **Contributor**</span></span>

* <span data-ttu-id="da6c7-112">**Wpis tajny klienta**: musi to być hasło.</span><span class="sxs-lookup"><span data-stu-id="da6c7-112">**Client secret**: must be a password.</span></span> <span data-ttu-id="da6c7-113">Obecnie nie można używać nazwy głównej usługi do uwierzytelniania certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="da6c7-113">Currently, you can't use a service principal set up for certificate authentication.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="da6c7-114">toocreate nazwy głównej usługi musisz mieć uprawnienia tooregister aplikację z dzierżawą usługi Azure AD i rolę tooa aplikacji hello tooassign w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="da6c7-114">toocreate a service principal, you must have permissions tooregister an application with your Azure AD tenant, and tooassign hello application tooa role in your subscription.</span></span> <span data-ttu-id="da6c7-115">toosee, jeśli masz uprawnienia wymagane hello [zaewidencjonować hello Portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions).</span><span class="sxs-lookup"><span data-stu-id="da6c7-115">toosee if you have hello required permissions, [check in hello Portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions).</span></span> 
>

## <a name="option-1-create-a-service-principal-in-azure-ad"></a><span data-ttu-id="da6c7-116">Opcja 1. Tworzenie jednostki usługi w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="da6c7-116">Option 1: Create a service principal in Azure AD</span></span>

<span data-ttu-id="da6c7-117">Jeśli chcesz toocreate nazwy głównej usługi Azure AD, przed wdrożeniem klastra Kubernetes, platforma Azure udostępnia kilka metod.</span><span class="sxs-lookup"><span data-stu-id="da6c7-117">If you want toocreate an Azure AD service principal before you deploy your Kubernetes cluster, Azure provides several methods.</span></span> 

<span data-ttu-id="da6c7-118">następujące przykładowe polecenia Hello przedstawia sposób toodo pomocą hello [Azure CLI 2.0](../../azure-resource-manager/resource-group-authenticate-service-principal-cli.md).</span><span class="sxs-lookup"><span data-stu-id="da6c7-118">hello following example commands show you how toodo this with hello [Azure CLI 2.0](../../azure-resource-manager/resource-group-authenticate-service-principal-cli.md).</span></span> <span data-ttu-id="da6c7-119">Można też utworzyć główną usługi za pomocą [programu Azure PowerShell](../../azure-resource-manager/resource-group-authenticate-service-principal.md), hello [portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md), lub innych metod.</span><span class="sxs-lookup"><span data-stu-id="da6c7-119">You can alternatively create a service principal using [Azure PowerShell](../../azure-resource-manager/resource-group-authenticate-service-principal.md), hello [portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md), or other methods.</span></span>

```azurecli
az login

az account set --subscription "mySubscriptionID"

az group create -n "myResourceGroupName" -l "westus"

az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/mySubscriptionID/resourceGroups/myResourceGroupName"
```

<span data-ttu-id="da6c7-120">Dane wyjściowe są podobne następujące toohello (w tym miejscu pokazano zredagowanym):</span><span class="sxs-lookup"><span data-stu-id="da6c7-120">Output is similar toohello following (shown here redacted):</span></span>

![Tworzenie nazwy głównej usługi](./media/container-service-kubernetes-service-principal/service-principal-creds.png)

<span data-ttu-id="da6c7-122">Wyróżnione są hello **identyfikator klienta** (`appId`) i hello **klucz tajny klienta** (`password`) używanej jako parametry główną usługi dla wdrożenia klastra.</span><span class="sxs-lookup"><span data-stu-id="da6c7-122">Highlighted are hello **client ID** (`appId`) and hello **client secret** (`password`) that you use as service principal parameters for cluster deployment.</span></span>


### <a name="specify-service-principal-when-creating-hello-kubernetes-cluster"></a><span data-ttu-id="da6c7-123">Podczas tworzenia klastra Kubernetes hello należy podać nazwę główną usługi</span><span class="sxs-lookup"><span data-stu-id="da6c7-123">Specify service principal when creating hello Kubernetes cluster</span></span>

<span data-ttu-id="da6c7-124">Podaj hello **identyfikator klienta** (nazywane również hello `appId`, dla Identyfikatora aplikacji) i **klucz tajny klienta** (`password`) z istniejącą usługę podmiotu zabezpieczeń jako parametry podczas tworzenia hello Kubernetes klastra.</span><span class="sxs-lookup"><span data-stu-id="da6c7-124">Provide hello **client ID** (also called hello `appId`, for Application ID) and **client secret** (`password`) of an existing service principal as parameters when you create hello Kubernetes cluster.</span></span> <span data-ttu-id="da6c7-125">Upewnij się, że nazwy głównej usługi hello spełnia wymagania hello na powitania rozpoczynający się w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="da6c7-125">Make sure hello service principal meets hello requirements at hello beginning this article.</span></span>

<span data-ttu-id="da6c7-126">Te parametry można określić podczas wdrażania klastra Kubernetes hello przy użyciu hello [Azure interfejsu wiersza polecenia (CLI) 2.0](container-service-kubernetes-walkthrough.md), [portalu Azure](../dcos-swarm/container-service-deployment.md), lub innych metod.</span><span class="sxs-lookup"><span data-stu-id="da6c7-126">You can specify these parameters when deploying hello Kubernetes cluster using hello [Azure Command-Line Interface (CLI) 2.0](container-service-kubernetes-walkthrough.md), [Azure portal](../dcos-swarm/container-service-deployment.md), or other methods.</span></span>

>[!TIP] 
><span data-ttu-id="da6c7-127">Podczas określania hello **identyfikator klienta**, należy się hello toouse `appId`, nie hello `ObjectId`, hello głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="da6c7-127">When specifying hello **client ID**, be sure toouse hello `appId`, not hello `ObjectId`, of hello service principal.</span></span>
>

<span data-ttu-id="da6c7-128">Witaj poniższy przykład przedstawia toopass jednokierunkowej hello parametrów z hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="da6c7-128">hello following example shows one way toopass hello parameters with hello Azure CLI 2.0.</span></span> <span data-ttu-id="da6c7-129">W tym przykładzie użyto hello [szablon szybkiego startu Kubernetes](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes).</span><span class="sxs-lookup"><span data-stu-id="da6c7-129">This example uses hello [Kubernetes quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes).</span></span>

1. <span data-ttu-id="da6c7-130">[Pobierz](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.parameters.json) pliku parametrów szablonu hello `azuredeploy.parameters.json` z usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="da6c7-130">[Download](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.parameters.json) hello template parameters file `azuredeploy.parameters.json` from GitHub.</span></span>

2. <span data-ttu-id="da6c7-131">Usługa hello toospecify główna, wprowadź wartości w polach `servicePrincipalClientId` i `servicePrincipalClientSecret` w pliku hello.</span><span class="sxs-lookup"><span data-stu-id="da6c7-131">toospecify hello service principal, enter values for `servicePrincipalClientId` and `servicePrincipalClientSecret` in hello file.</span></span> <span data-ttu-id="da6c7-132">(Należy też tooprovide własne wartości `dnsNamePrefix` i `sshRSAPublicKey`.</span><span class="sxs-lookup"><span data-stu-id="da6c7-132">(You also need tooprovide your own values for `dnsNamePrefix` and `sshRSAPublicKey`.</span></span> <span data-ttu-id="da6c7-133">ostatnie Hello jest klastra hello tooaccess klucza publicznego SSH hello). Zapisz plik hello.</span><span class="sxs-lookup"><span data-stu-id="da6c7-133">hello latter is hello SSH public key tooaccess hello cluster.) Save hello file.</span></span>

    ![Przekazywanie parametrów nazwy głównej usługi](./media/container-service-kubernetes-service-principal/service-principal-params.png)

3. <span data-ttu-id="da6c7-135">Witaj uruchom następujące polecenie, używając `--parameters` tooset hello ścieżki toohello azuredeploy.parameters.json pliku.</span><span class="sxs-lookup"><span data-stu-id="da6c7-135">Run hello following command, using `--parameters` tooset hello path toohello azuredeploy.parameters.json file.</span></span> <span data-ttu-id="da6c7-136">To polecenie wdraża hello klastra w grupie zasobów o nazwie tworzenia `myResourceGroup` hello regionu zachodnie stany USA.</span><span class="sxs-lookup"><span data-stu-id="da6c7-136">This command deploys hello cluster in a resource group you create called `myResourceGroup` in hello West US region.</span></span>

    ```azurecli
    az login

    az account set --subscription "mySubscriptionID"

    az group create --name "myResourceGroup" --location "westus" 
    
    az group deployment create -g "myResourceGroup" --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.json" --parameters @azuredeploy.parameters.json
    ```


## <a name="option-2-generate-a-service-principal-when-creating-hello-cluster-with-az-acs-create"></a><span data-ttu-id="da6c7-137">Opcja 2: Generowanie nazwy głównej usługi podczas tworzenia klastra hello z`az acs create`</span><span class="sxs-lookup"><span data-stu-id="da6c7-137">Option 2: Generate a service principal when creating hello cluster with `az acs create`</span></span>

<span data-ttu-id="da6c7-138">Po uruchomieniu hello [ `az acs create` ](/cli/azure/acs#create) toocreate polecenia hello Kubernetes klastra, masz toogenerate opcji hello nazwy głównej usługi automatycznie.</span><span class="sxs-lookup"><span data-stu-id="da6c7-138">If you run hello [`az acs create`](/cli/azure/acs#create) command toocreate hello Kubernetes cluster, you have hello option toogenerate a service principal automatically.</span></span>

<span data-ttu-id="da6c7-139">Tak jak w przypadku innych opcji tworzenia klastra Kubernetes, parametry istniejącej nazwy głównej usługi można określić po uruchomieniu polecenia `az acs create`.</span><span class="sxs-lookup"><span data-stu-id="da6c7-139">As with other Kubernetes cluster creation options, you can specify parameters for an existing service principal when you run `az acs create`.</span></span> <span data-ttu-id="da6c7-140">Jednak jeśli pominięto tych parametrów, hello Azure CLI tworzy jeden automatycznie do użycia z usługą kontenera.</span><span class="sxs-lookup"><span data-stu-id="da6c7-140">However, when you omit these parameters, hello Azure CLI creates one automatically for use with Container Service.</span></span> <span data-ttu-id="da6c7-141">Podczas wdrażania hello to ma miejsce przezroczysty.</span><span class="sxs-lookup"><span data-stu-id="da6c7-141">This takes place transparently during hello deployment.</span></span> 

<span data-ttu-id="da6c7-142">Witaj następujące polecenie tworzy klaster Kubernetes i generuje zarówno kluczy SSH i poświadczenia główne usługi:</span><span class="sxs-lookup"><span data-stu-id="da6c7-142">hello following command creates a Kubernetes cluster and generates both SSH keys and service principal credentials:</span></span>

```console
az acs create -n myClusterName -d myDNSPrefix -g myResourceGroup --generate-ssh-keys --orchestrator-type kubernetes
```

> [!IMPORTANT]
> <span data-ttu-id="da6c7-143">Jeśli konto nie ma hello Azure AD i toocreate uprawnienia subskrypcji nazwy głównej usługi, polecenie hello zbyt generuje błąd podobny`Insufficient privileges toocomplete hello operation.`</span><span class="sxs-lookup"><span data-stu-id="da6c7-143">If your account doesn't have hello Azure AD and subscription permissions toocreate a service principal, hello command generates an error similar too`Insufficient privileges toocomplete hello operation.`</span></span>
> 

## <a name="additional-considerations"></a><span data-ttu-id="da6c7-144">Dodatkowe zagadnienia</span><span class="sxs-lookup"><span data-stu-id="da6c7-144">Additional considerations</span></span>

* <span data-ttu-id="da6c7-145">Jeśli nie masz uprawnień toocreate nazwy głównej usługi w ramach subskrypcji, może być konieczne tooask usługi Azure AD lub tooassign administratora subskrypcji hello niezbędne uprawnienia lub uzyskać toouse głównej usługi, z usługi kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="da6c7-145">If you don't have permissions toocreate a service principal in your subscription, you might need tooask your Azure AD or subscription administrator tooassign hello necessary permissions, or ask them for a service principal toouse with Azure Container Service.</span></span> 

* <span data-ttu-id="da6c7-146">nazwy głównej usługi powitania dla Kubernetes jest częścią hello konfiguracji klastra.</span><span class="sxs-lookup"><span data-stu-id="da6c7-146">hello service principal for Kubernetes is a part of hello cluster configuration.</span></span> <span data-ttu-id="da6c7-147">Jednak nie należy używać hello tożsamości toodeploy hello klastra.</span><span class="sxs-lookup"><span data-stu-id="da6c7-147">However, don't use hello identity toodeploy hello cluster.</span></span>

* <span data-ttu-id="da6c7-148">Każda jednostka usługi jest skojarzona z aplikacją usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="da6c7-148">Every service principal is associated with an Azure AD application.</span></span> <span data-ttu-id="da6c7-149">Hello nazwy głównej usługi dla klastra Kubernetes może być skojarzony z żadnych Azure prawidłową nazwę aplikacji usługi AD (na przykład: `https://www.contoso.org/example`).</span><span class="sxs-lookup"><span data-stu-id="da6c7-149">hello service principal for a Kubernetes cluster can be associated with any valid Azure AD application name (for example: `https://www.contoso.org/example`).</span></span> <span data-ttu-id="da6c7-150">adres URL aplikacji hello Hello nie ma toobe rzeczywistych punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="da6c7-150">hello URL for hello application doesn't have toobe a real endpoint.</span></span>

* <span data-ttu-id="da6c7-151">Podczas określania nazwy głównej usługi hello **identyfikator klienta**, można użyć wartości hello hello `appId` (jak pokazano w tym artykule) lub nazwy głównej usługi odpowiedniego hello `name` (na przykład`https://www.contoso.org/example`).</span><span class="sxs-lookup"><span data-stu-id="da6c7-151">When specifying hello service principal **Client ID**, you can use hello value of hello `appId` (as shown in this article) or hello corresponding service principal `name` (for example,`https://www.contoso.org/example`).</span></span>

* <span data-ttu-id="da6c7-152">Na wzorcu hello i agenta maszyny wirtualne w klastrze Kubernetes hello hello poświadczenia główne są przechowywane w hello /etc/kubernetes/azure.json pliku.</span><span class="sxs-lookup"><span data-stu-id="da6c7-152">On hello master and agent VMs in hello Kubernetes cluster, hello service principal credentials are stored in hello file /etc/kubernetes/azure.json.</span></span>

* <span data-ttu-id="da6c7-153">Jeśli używasz hello `az acs create` polecenia nazwy głównej usługi hello toogenerate automatycznie, hello poświadczenia główne są zapisywane toohello ~/.azure/acsServicePrincipal.json pliku na maszynie hello używane toorun hello polecenia.</span><span class="sxs-lookup"><span data-stu-id="da6c7-153">When you use hello `az acs create` command toogenerate hello service principal automatically, hello service principal credentials are written toohello file ~/.azure/acsServicePrincipal.json on hello machine used toorun hello command.</span></span> 

* <span data-ttu-id="da6c7-154">Jeśli używasz hello `az acs create` polecenia nazwy głównej usługi hello toogenerate automatycznie, nazwy głównej usługi hello mogą również uwierzytelniać za pomocą [rejestru kontenera platformy Azure](../../container-registry/container-registry-intro.md) utworzone w hello sam subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="da6c7-154">When you use hello `az acs create` command toogenerate hello service principal automatically, hello service principal can also authenticate with an [Azure container registry](../../container-registry/container-registry-intro.md) created in hello same subscription.</span></span>




## <a name="next-steps"></a><span data-ttu-id="da6c7-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="da6c7-155">Next steps</span></span>

* <span data-ttu-id="da6c7-156">[Rozpocznij pracę z klastrem Kubernetes](container-service-kubernetes-walkthrough.md) w klastrze usług kontenera.</span><span class="sxs-lookup"><span data-stu-id="da6c7-156">[Get started with Kubernetes](container-service-kubernetes-walkthrough.md) in your container service cluster.</span></span>

* <span data-ttu-id="da6c7-157">tootroubleshoot hello nazwy głównej usługi dla Kubernetes, zobacz hello [dokumentacji aparatu ACS](https://github.com/Azure/acs-engine/blob/master/docs/kubernetes.md#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="da6c7-157">tootroubleshoot hello service principal for Kubernetes, see hello [ACS Engine documentation](https://github.com/Azure/acs-engine/blob/master/docs/kubernetes.md#troubleshooting).</span></span>


