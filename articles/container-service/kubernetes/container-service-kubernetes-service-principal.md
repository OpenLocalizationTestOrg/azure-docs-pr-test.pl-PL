---
title: "Nazwa główna usługi klastra Azure Kubernetes | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 37171b4e69ad7d8c41ca8e7475c33ce70379f484
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="set-up-an-azure-ad-service-principal-for-a-kubernetes-cluster-in-container-service"></a><span data-ttu-id="1b293-103">Konfigurowanie jednostki usługi Azure AD dla klastra Kubernetes w usłudze Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="1b293-103">Set up an Azure AD service principal for a Kubernetes cluster in Container Service</span></span>


<span data-ttu-id="1b293-104">W usłudze Azure Container Service klaster Kubernetes wymaga [jednostki usługi Azure Active Directory](../../active-directory/develop/active-directory-application-objects.md) do współpracy z interfejsami API platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1b293-104">In Azure Container Service, a Kubernetes cluster requires an [Azure Active Directory service principal](../../active-directory/develop/active-directory-application-objects.md) to interact with Azure APIs.</span></span> <span data-ttu-id="1b293-105">Nazwa główna usługi jest potrzebna do dynamicznego zarządzania zasobami, takimi jak [trasy zdefiniowane przez użytkownika](../../virtual-network/virtual-networks-udr-overview.md) i narzędzie [Azure Load Balancer dla warstwy 4](../../load-balancer/load-balancer-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1b293-105">The service principal is needed to dynamically manage resources such as [user-defined routes](../../virtual-network/virtual-networks-udr-overview.md) and the [Layer 4 Azure Load Balancer](../../load-balancer/load-balancer-overview.md).</span></span> 


<span data-ttu-id="1b293-106">W tym artykule przedstawiono różne sposoby konfigurowania jednostki usługi dla klastra Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="1b293-106">This article shows different options to set up a service principal for your Kubernetes cluster.</span></span> <span data-ttu-id="1b293-107">Na przykład jeśli zainstalowano i skonfigurowano [interfejs wiersza polecenia platformy Azure w wersji 2.0](/cli/azure/install-az-cli2), można uruchomić polecenie [`az acs create`](/cli/azure/acs#create), aby jednocześnie utworzyć klaster Kubernetes i nazwę główną usługi.</span><span class="sxs-lookup"><span data-stu-id="1b293-107">For example, if you installed and set up the [Azure CLI 2.0](/cli/azure/install-az-cli2), you can run the [`az acs create`](/cli/azure/acs#create) command to create the Kubernetes cluster and the service principal at the same time.</span></span>


## <a name="requirements-for-the-service-principal"></a><span data-ttu-id="1b293-108">Wymagania dotyczące nazwy głównej usługi</span><span class="sxs-lookup"><span data-stu-id="1b293-108">Requirements for the service principal</span></span>

<span data-ttu-id="1b293-109">Możesz użyć istniejącej jednostki usługi Azure AD, która spełnia następujące wymagania, albo utworzyć nową.</span><span class="sxs-lookup"><span data-stu-id="1b293-109">You can use an existing Azure AD service principal that meets the following requirements, or create a new one.</span></span>

* <span data-ttu-id="1b293-110">**Zakres**: grupa zasobów w subskrypcji użytej do wdrożenia klastra Kubernetes lub (mniej rygorystycznie) subskrypcja użyta do wdrożenia klastra.</span><span class="sxs-lookup"><span data-stu-id="1b293-110">**Scope**: the resource group in the subscription used to deploy the Kubernetes cluster, or (less restrictively) the subscription used to deploy the cluster.</span></span>

* <span data-ttu-id="1b293-111">**Rola**: **Współautor**</span><span class="sxs-lookup"><span data-stu-id="1b293-111">**Role**: **Contributor**</span></span>

* <span data-ttu-id="1b293-112">**Wpis tajny klienta**: musi to być hasło.</span><span class="sxs-lookup"><span data-stu-id="1b293-112">**Client secret**: must be a password.</span></span> <span data-ttu-id="1b293-113">Obecnie nie można używać nazwy głównej usługi do uwierzytelniania certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="1b293-113">Currently, you can't use a service principal set up for certificate authentication.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="1b293-114">Aby utworzyć jednostkę usługi, musisz mieć uprawnienia do zarejestrowania aplikacji w swojej dzierżawie usługi Azure AD i przypisania aplikacji do roli w swojej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="1b293-114">To create a service principal, you must have permissions to register an application with your Azure AD tenant, and to assign the application to a role in your subscription.</span></span> <span data-ttu-id="1b293-115">Aby sprawdzić, czy masz wymagane uprawnienia, [zajrzyj do portalu](../../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions).</span><span class="sxs-lookup"><span data-stu-id="1b293-115">To see if you have the required permissions, [check in the Portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions).</span></span> 
>

## <a name="option-1-create-a-service-principal-in-azure-ad"></a><span data-ttu-id="1b293-116">Opcja 1. Tworzenie jednostki usługi w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="1b293-116">Option 1: Create a service principal in Azure AD</span></span>

<span data-ttu-id="1b293-117">Jeśli chcesz utworzyć jednostkę usługi Azure AD przed wdrożeniem klastra Kubernetes, platforma Azure udostępnia kilka metod.</span><span class="sxs-lookup"><span data-stu-id="1b293-117">If you want to create an Azure AD service principal before you deploy your Kubernetes cluster, Azure provides several methods.</span></span> 

<span data-ttu-id="1b293-118">Następujące przykładowe polecenia pokazują, jak wykonać to za pomocą interfejsu [wiersza polecenia platformy Azure w wersji 2.0](../../azure-resource-manager/resource-group-authenticate-service-principal-cli.md).</span><span class="sxs-lookup"><span data-stu-id="1b293-118">The following example commands show you how to do this with the [Azure CLI 2.0](../../azure-resource-manager/resource-group-authenticate-service-principal-cli.md).</span></span> <span data-ttu-id="1b293-119">Można też utworzyć jednostkę usługi za pomocą programu [Azure PowerShell](../../azure-resource-manager/resource-group-authenticate-service-principal.md), [portalu](../../azure-resource-manager/resource-group-create-service-principal-portal.md) lub innej metody.</span><span class="sxs-lookup"><span data-stu-id="1b293-119">You can alternatively create a service principal using [Azure PowerShell](../../azure-resource-manager/resource-group-authenticate-service-principal.md), the [portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md), or other methods.</span></span>

```azurecli
az login

az account set --subscription "mySubscriptionID"

az group create -n "myResourceGroupName" -l "westus"

az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/mySubscriptionID/resourceGroups/myResourceGroupName"
```

<span data-ttu-id="1b293-120">Dane wyjściowe są zbliżone do następujących (pokazane tutaj zostały zredagowane):</span><span class="sxs-lookup"><span data-stu-id="1b293-120">Output is similar to the following (shown here redacted):</span></span>

![Tworzenie nazwy głównej usługi](./media/container-service-kubernetes-service-principal/service-principal-creds.png)

<span data-ttu-id="1b293-122">Wyróżniono **identyfikator klienta** (`appId`) i **klucz tajny klienta** (`password`), używane jako parametry nazwy głównej usługi przy wdrażaniu klastra.</span><span class="sxs-lookup"><span data-stu-id="1b293-122">Highlighted are the **client ID** (`appId`) and the **client secret** (`password`) that you use as service principal parameters for cluster deployment.</span></span>


### <a name="specify-service-principal-when-creating-the-kubernetes-cluster"></a><span data-ttu-id="1b293-123">Określanie jednostki usługi podczas tworzenia klastra Kubernetes</span><span class="sxs-lookup"><span data-stu-id="1b293-123">Specify service principal when creating the Kubernetes cluster</span></span>

<span data-ttu-id="1b293-124">Podaj **identyfikator klienta** (nazywany również `appId`, identyfikator aplikacji) i **wpis tajny klienta** (`password`) istniejącej nazwy głównej usługi jako parametry podczas tworzenia klastra Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="1b293-124">Provide the **client ID** (also called the `appId`, for Application ID) and **client secret** (`password`) of an existing service principal as parameters when you create the Kubernetes cluster.</span></span> <span data-ttu-id="1b293-125">Upewnij się, że jednostka usługi spełnia wymagania przedstawione na początku tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="1b293-125">Make sure the service principal meets the requirements at the beginning this article.</span></span>

<span data-ttu-id="1b293-126">Te parametry można określić podczas wdrażania klastra Kubernetes za pomocą [interfejsu wiersza polecenia platformy Azure w wersji 2.0](container-service-kubernetes-walkthrough.md), witryny [Azure Portal](../dcos-swarm/container-service-deployment.md) lub innymi metodami.</span><span class="sxs-lookup"><span data-stu-id="1b293-126">You can specify these parameters when deploying the Kubernetes cluster using the [Azure Command-Line Interface (CLI) 2.0](container-service-kubernetes-walkthrough.md), [Azure portal](../dcos-swarm/container-service-deployment.md), or other methods.</span></span>

>[!TIP] 
><span data-ttu-id="1b293-127">Podczas określania **identyfikatora klienta** należy użyć identyfikatora `appId`, a nie `ObjectId` nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="1b293-127">When specifying the **client ID**, be sure to use the `appId`, not the `ObjectId`, of the service principal.</span></span>
>

<span data-ttu-id="1b293-128">Poniższy przykład przedstawia sposób przekazania parametrów poprzez interfejs wiersza polecenia Azure w wersji 2.0.</span><span class="sxs-lookup"><span data-stu-id="1b293-128">The following example shows one way to pass the parameters with the Azure CLI 2.0.</span></span> <span data-ttu-id="1b293-129">W tym przykładzie użyto [szablonu Kubernetes quickstart](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes).</span><span class="sxs-lookup"><span data-stu-id="1b293-129">This example uses the [Kubernetes quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes).</span></span>

1. <span data-ttu-id="1b293-130">[Pobierz](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.parameters.json) plik parametrów szablonu `azuredeploy.parameters.json` z usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="1b293-130">[Download](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.parameters.json) the template parameters file `azuredeploy.parameters.json` from GitHub.</span></span>

2. <span data-ttu-id="1b293-131">Aby określić nazwę główną usługi, wprowadź wartości dla `servicePrincipalClientId` i `servicePrincipalClientSecret` w pliku.</span><span class="sxs-lookup"><span data-stu-id="1b293-131">To specify the service principal, enter values for `servicePrincipalClientId` and `servicePrincipalClientSecret` in the file.</span></span> <span data-ttu-id="1b293-132">(Należy również podać własne wartości dla `dnsNamePrefix` i `sshRSAPublicKey`.</span><span class="sxs-lookup"><span data-stu-id="1b293-132">(You also need to provide your own values for `dnsNamePrefix` and `sshRSAPublicKey`.</span></span> <span data-ttu-id="1b293-133">Ta ostatnia jest kluczem publicznym SSH umożliwiającym dostęp do klastra). Zapisz plik.</span><span class="sxs-lookup"><span data-stu-id="1b293-133">The latter is the SSH public key to access the cluster.) Save the file.</span></span>

    ![Przekazywanie parametrów nazwy głównej usługi](./media/container-service-kubernetes-service-principal/service-principal-params.png)

3. <span data-ttu-id="1b293-135">Przy użyciu opcji `--parameters` uruchom następujące polecenie, aby ustawić ścieżkę do pliku azuredeploy.parameters.json.</span><span class="sxs-lookup"><span data-stu-id="1b293-135">Run the following command, using `--parameters` to set the path to the azuredeploy.parameters.json file.</span></span> <span data-ttu-id="1b293-136">To polecenie wdraża klaster w utworzonej grupie zasobów o nazwie `myResourceGroup` w regionie Zachodnie stany USA.</span><span class="sxs-lookup"><span data-stu-id="1b293-136">This command deploys the cluster in a resource group you create called `myResourceGroup` in the West US region.</span></span>

    ```azurecli
    az login

    az account set --subscription "mySubscriptionID"

    az group create --name "myResourceGroup" --location "westus" 
    
    az group deployment create -g "myResourceGroup" --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.json" --parameters @azuredeploy.parameters.json
    ```


## <a name="option-2-generate-a-service-principal-when-creating-the-cluster-with-az-acs-create"></a><span data-ttu-id="1b293-137">Opcja 2. Wygenerowanie jednostki usługi podczas tworzenia klastra przy użyciu polecenia `az acs create`</span><span class="sxs-lookup"><span data-stu-id="1b293-137">Option 2: Generate a service principal when creating the cluster with `az acs create`</span></span>

<span data-ttu-id="1b293-138">Jeśli uruchamiasz polecenie [`az acs create`](/cli/azure/acs#create) w celu utworzenia klastra Kubernetes, masz możliwość automatycznego wygenerowania jednostki usługi.</span><span class="sxs-lookup"><span data-stu-id="1b293-138">If you run the [`az acs create`](/cli/azure/acs#create) command to create the Kubernetes cluster, you have the option to generate a service principal automatically.</span></span>

<span data-ttu-id="1b293-139">Tak jak w przypadku innych opcji tworzenia klastra Kubernetes, parametry istniejącej nazwy głównej usługi można określić po uruchomieniu polecenia `az acs create`.</span><span class="sxs-lookup"><span data-stu-id="1b293-139">As with other Kubernetes cluster creation options, you can specify parameters for an existing service principal when you run `az acs create`.</span></span> <span data-ttu-id="1b293-140">Jednak w przypadku pominięcia tych parametrów interfejs wiersza polecenia platformy Azure automatycznie tworzy jednostkę usługi do użycia z usługą Container Service.</span><span class="sxs-lookup"><span data-stu-id="1b293-140">However, when you omit these parameters, the Azure CLI creates one automatically for use with Container Service.</span></span> <span data-ttu-id="1b293-141">Podczas wdrażania dzieje się to w sposób niewidoczny dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1b293-141">This takes place transparently during the deployment.</span></span> 

<span data-ttu-id="1b293-142">Następujące polecenie tworzy klaster Kubernetes i generuje zarówno klucze SSH, jak i poświadczenia nazwy głównej usługi:</span><span class="sxs-lookup"><span data-stu-id="1b293-142">The following command creates a Kubernetes cluster and generates both SSH keys and service principal credentials:</span></span>

```console
az acs create -n myClusterName -d myDNSPrefix -g myResourceGroup --generate-ssh-keys --orchestrator-type kubernetes
```

> [!IMPORTANT]
> <span data-ttu-id="1b293-143">Jeśli konto nie ma uprawnień usługi Azure AD i subskrypcji do utworzenia jednostki usługi, polecenie generuje błąd podobny do: `Insufficient privileges to complete the operation.`</span><span class="sxs-lookup"><span data-stu-id="1b293-143">If your account doesn't have the Azure AD and subscription permissions to create a service principal, the command generates an error similar to `Insufficient privileges to complete the operation.`</span></span>
> 

## <a name="additional-considerations"></a><span data-ttu-id="1b293-144">Dodatkowe zagadnienia</span><span class="sxs-lookup"><span data-stu-id="1b293-144">Additional considerations</span></span>

* <span data-ttu-id="1b293-145">Jeśli nie masz uprawnień do utworzenia jednostki usługi w swojej subskrypcji, konieczne może być poproszenie administratora usługi Azure AD lub subskrypcji o przypisanie niezbędnych uprawnień albo o jednostkę usługi do użycia z usługą Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="1b293-145">If you don't have permissions to create a service principal in your subscription, you might need to ask your Azure AD or subscription administrator to assign the necessary permissions, or ask them for a service principal to use with Azure Container Service.</span></span> 

* <span data-ttu-id="1b293-146">Jednostka usługi dla rozwiązania Kubernetes jest częścią konfiguracji klastra.</span><span class="sxs-lookup"><span data-stu-id="1b293-146">The service principal for Kubernetes is a part of the cluster configuration.</span></span> <span data-ttu-id="1b293-147">Nie należy jednak używać tożsamości do wdrażania klastra.</span><span class="sxs-lookup"><span data-stu-id="1b293-147">However, don't use the identity to deploy the cluster.</span></span>

* <span data-ttu-id="1b293-148">Każda jednostka usługi jest skojarzona z aplikacją usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1b293-148">Every service principal is associated with an Azure AD application.</span></span> <span data-ttu-id="1b293-149">Jednostka usługi dla klastra Kubernetes może zostać skojarzona z dowolną prawidłową nazwą aplikacji usługi Azure AD (np. `https://www.contoso.org/example`).</span><span class="sxs-lookup"><span data-stu-id="1b293-149">The service principal for a Kubernetes cluster can be associated with any valid Azure AD application name (for example: `https://www.contoso.org/example`).</span></span> <span data-ttu-id="1b293-150">Adres URL dla aplikacji nie musi być rzeczywistym punktem końcowym.</span><span class="sxs-lookup"><span data-stu-id="1b293-150">The URL for the application doesn't have to be a real endpoint.</span></span>

* <span data-ttu-id="1b293-151">Podczas określania **identyfikatora klienta** jednostki usługi można użyć wartości `appId` (jak pokazano w tym artykule) lub odpowiedniej jednostki usługi `name` (na przykład `https://www.contoso.org/example`).</span><span class="sxs-lookup"><span data-stu-id="1b293-151">When specifying the service principal **Client ID**, you can use the value of the `appId` (as shown in this article) or the corresponding service principal `name` (for example,`https://www.contoso.org/example`).</span></span>

* <span data-ttu-id="1b293-152">Na głównej maszynie wirtualnej i maszynach wirtualnych agentów w klastrze Kubernetes poświadczenia jednostki usługi są przechowywane w pliku /etc/kubernetes/azure.json.</span><span class="sxs-lookup"><span data-stu-id="1b293-152">On the master and agent VMs in the Kubernetes cluster, the service principal credentials are stored in the file /etc/kubernetes/azure.json.</span></span>

* <span data-ttu-id="1b293-153">Gdy używasz polecenia `az acs create`, aby automatycznie wygenerować jednostkę usługi, poświadczenia jednostki usługi są zapisywane w pliku ~/.azure/acsServicePrincipal.json na maszynie użytej do uruchomienia polecenia.</span><span class="sxs-lookup"><span data-stu-id="1b293-153">When you use the `az acs create` command to generate the service principal automatically, the service principal credentials are written to the file ~/.azure/acsServicePrincipal.json on the machine used to run the command.</span></span> 

* <span data-ttu-id="1b293-154">Kiedy używasz polecenia `az acs create` do automatycznego wygenerowania jednostki usługi, jednostka usługi może także uwierzytelnić się za pomocą [rejestru kontenera platformy Azure](../../container-registry/container-registry-intro.md) utworzonego w tej samej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="1b293-154">When you use the `az acs create` command to generate the service principal automatically, the service principal can also authenticate with an [Azure container registry](../../container-registry/container-registry-intro.md) created in the same subscription.</span></span>




## <a name="next-steps"></a><span data-ttu-id="1b293-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1b293-155">Next steps</span></span>

* <span data-ttu-id="1b293-156">[Rozpocznij pracę z klastrem Kubernetes](container-service-kubernetes-walkthrough.md) w klastrze usług kontenera.</span><span class="sxs-lookup"><span data-stu-id="1b293-156">[Get started with Kubernetes](container-service-kubernetes-walkthrough.md) in your container service cluster.</span></span>

* <span data-ttu-id="1b293-157">Aby rozwiązać problemy z jednostką usługi dla rozwiązania Kubernetes, zobacz [dokumentację aparatu ACS](https://github.com/Azure/acs-engine/blob/master/docs/kubernetes.md#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="1b293-157">To troubleshoot the service principal for Kubernetes, see the [ACS Engine documentation](https://github.com/Azure/acs-engine/blob/master/docs/kubernetes.md#troubleshooting).</span></span>


