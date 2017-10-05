---
title: "Wdrażanie pochodzenia OpenShift na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się wdrożyć pochodzenia OpenShift maszyn wirtualnych platformy Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: jbinder
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 
ms.author: jbinder
ms.openlocfilehash: e03da05625e440eab29ccc28a2343d3433fc7607
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-openshift-origin-to-azure-virtual-machines"></a><span data-ttu-id="bae2e-103">Wdrażanie pochodzenia OpenShift na maszynach wirtualnych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="bae2e-103">Deploy OpenShift Origin to Azure Virtual Machines</span></span> 

<span data-ttu-id="bae2e-104">[Pochodzenie OpenShift](https://www.openshift.org/) to platforma kontenera typu open source oparty na [Kubernetes](https://kubernetes.io/).</span><span class="sxs-lookup"><span data-stu-id="bae2e-104">[OpenShift Origin](https://www.openshift.org/) is an open source container platform built on [Kubernetes](https://kubernetes.io/).</span></span> <span data-ttu-id="bae2e-105">Takie rozwiązanie upraszcza proces wdrażania, skalowanie i działania aplikacji wielodostępnej.</span><span class="sxs-lookup"><span data-stu-id="bae2e-105">It simplifies the process of deploying, scaling, and operating multi-tenant applications.</span></span> 

<span data-ttu-id="bae2e-106">W tym przewodniku opisano sposób wdrażania pochodzenia OpenShift na maszynach wirtualnych platformy Azure przy użyciu wiersza polecenia platformy Azure i szablonów Menedżera zasobów Azure.</span><span class="sxs-lookup"><span data-stu-id="bae2e-106">This guide describes how to deploy OpenShift Origin on Azure Virtual Machines using the Azure CLI and Azure Resource Manager Templates.</span></span> <span data-ttu-id="bae2e-107">Ten samouczek zawiera informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="bae2e-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bae2e-108">Utwórz KeyVault do zarządzania kluczy SSH dla klastra OpenShift.</span><span class="sxs-lookup"><span data-stu-id="bae2e-108">Create a KeyVault to manage SSH keys for the OpenShift cluster.</span></span>
> * <span data-ttu-id="bae2e-109">Wdrażanie klastra OpenShift na maszynach wirtualnych Azure.</span><span class="sxs-lookup"><span data-stu-id="bae2e-109">Deploy an OpenShift cluster on Azure VMs.</span></span> 
> * <span data-ttu-id="bae2e-110">Instalowanie i konfigurowanie [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) do zarządzania klastrem.</span><span class="sxs-lookup"><span data-stu-id="bae2e-110">Install and configure the [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) to manage the cluster.</span></span>
> * <span data-ttu-id="bae2e-111">Dostosowywanie wdrożenia OpenShift.</span><span class="sxs-lookup"><span data-stu-id="bae2e-111">Customize the OpenShift deployment.</span></span>

<span data-ttu-id="bae2e-112">Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="bae2e-112">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="bae2e-113">To szybki start wymaga wiersza polecenia platformy Azure w wersji 2.0.8 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="bae2e-113">This quick start requires the Azure CLI version 2.0.8 or later.</span></span> <span data-ttu-id="bae2e-114">Aby dowiedzieć się, jaka wersja jest używana, uruchom polecenie `az --version`.</span><span class="sxs-lookup"><span data-stu-id="bae2e-114">To find the version, run `az --version`.</span></span> <span data-ttu-id="bae2e-115">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="bae2e-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="log-in-to-azure"></a><span data-ttu-id="bae2e-116">Zaloguj się do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bae2e-116">Log in to Azure</span></span> 
<span data-ttu-id="bae2e-117">Zaloguj się do Twojej subskrypcji platformy Azure z [az logowania](/cli/azure/#login) polecenia i wykonaj na ekranie kliknij lub kierunki **wypróbuj** użycia chmury powłoki.</span><span class="sxs-lookup"><span data-stu-id="bae2e-117">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions or click **Try it** to use Cloud Shell.</span></span>

```azurecli 
az login
```
## <a name="create-a-resource-group"></a><span data-ttu-id="bae2e-118">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="bae2e-118">Create a resource group</span></span>

<span data-ttu-id="bae2e-119">Utwórz grupę zasobów za pomocą polecenia [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="bae2e-119">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="bae2e-120">Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="bae2e-120">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="bae2e-121">Poniższy przykład obejmuje tworzenie grupy zasobów o nazwie *myResourceGroup* w lokalizacji *eastus*.</span><span class="sxs-lookup"><span data-stu-id="bae2e-121">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-key-vault"></a><span data-ttu-id="bae2e-122">Tworzenie magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="bae2e-122">Create a Key Vault</span></span>
<span data-ttu-id="bae2e-123">Utwórz KeyVault do przechowywania kluczy SSH dla klastra z [az keyvault utworzyć](/cli/azure/keyvault#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="bae2e-123">Create a KeyVault to store the SSH keys for the cluster with the [az keyvault create](/cli/azure/keyvault#create) command.</span></span>  

```azurecli 
az keyvault create --resource-group myResourceGroup --name myKeyVault \
       --enabled-for-template-deployment true \
       --location eastus
```

## <a name="create-an-ssh-key"></a><span data-ttu-id="bae2e-124">Tworzenie klucza SSH</span><span class="sxs-lookup"><span data-stu-id="bae2e-124">Create an SSH key</span></span> 
<span data-ttu-id="bae2e-125">Klucz SSH jest wymagany do bezpiecznego dostępu do klastra OpenShift pochodzenia.</span><span class="sxs-lookup"><span data-stu-id="bae2e-125">An SSH key is needed to secure access to the OpenShift Origin cluster.</span></span> <span data-ttu-id="bae2e-126">Utwórz parę kluczy SSH przy użyciu `ssh-keygen` polecenia.</span><span class="sxs-lookup"><span data-stu-id="bae2e-126">Create an SSH key-pair using the `ssh-keygen` command.</span></span> 
 
 ```bash
ssh-keygen -f ~/.ssh/openshift_rsa -t rsa -N ''
```

> [!NOTE]
> <span data-ttu-id="bae2e-127">Pary kluczy SSH, którą utworzysz nie może zawierać hasło.</span><span class="sxs-lookup"><span data-stu-id="bae2e-127">The SSH key pair you create must not have a passphrase.</span></span>

<span data-ttu-id="bae2e-128">Aby uzyskać więcej informacji na temat kluczy SSH w systemie Windows [tworzenie SSH kluczy w systemie Windows](/azure/virtual-machines/linux/ssh-from-windows).</span><span class="sxs-lookup"><span data-stu-id="bae2e-128">For more information on SSH keys on Windows, [How to create SSH keys on Windows](/azure/virtual-machines/linux/ssh-from-windows).</span></span>

## <a name="store-ssh-private-key-in-key-vault"></a><span data-ttu-id="bae2e-129">Przechowywanie klucza prywatnego SSH w magazynie kluczy</span><span class="sxs-lookup"><span data-stu-id="bae2e-129">Store SSH private key in Key Vault</span></span>
<span data-ttu-id="bae2e-130">Wdrożenie OpenShift używa klucza SSH, utworzenia bezpiecznego dostępu do głównego OpenShift.</span><span class="sxs-lookup"><span data-stu-id="bae2e-130">The OpenShift deployment uses the SSH key you created to secure access to the OpenShift master.</span></span> <span data-ttu-id="bae2e-131">Aby włączyć wdrożenie w celu bezpiecznego pobierania klucza SSH, należy przechowywać klucz w Key Vault za pomocą następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="bae2e-131">To enable the deployment to securely retrieve the SSH key, store the key in Key Vault using the following command.</span></span>

# <a name="enabled-for-template-deployment"></a><span data-ttu-id="bae2e-132">Włączony do wdrożenia szablonu</span><span class="sxs-lookup"><span data-stu-id="bae2e-132">Enabled for template deployment</span></span>
```azurecli
az keyvault secret set --vault-name KeyVaultName --name OpenShiftKey --file ~/.ssh/openshift.rsa
```

## <a name="create-a-service-principal"></a><span data-ttu-id="bae2e-133">Tworzenie nazwy głównej usługi</span><span class="sxs-lookup"><span data-stu-id="bae2e-133">Create a service principal</span></span> 
<span data-ttu-id="bae2e-134">OpenShift komunikuje się z platformy Azure przy użyciu nazwy użytkownika i hasła lub nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="bae2e-134">OpenShift communicates with Azure using a username and password or a service principal.</span></span> <span data-ttu-id="bae2e-135">Podmiot zabezpieczeń usługi Azure jest tożsamość zabezpieczeń korzystających z aplikacji, usługami i automatyzacja takich narzędzi jak OpenShift.</span><span class="sxs-lookup"><span data-stu-id="bae2e-135">An Azure service principal is a security identity that you can use with apps, services, and automation tools like OpenShift.</span></span> <span data-ttu-id="bae2e-136">Kontrolowanie i definiowanie uprawnień określające, jakie operacje nazwy głównej usługi można wykonać na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="bae2e-136">You control and define the permissions as to what operations the service principal can perform in Azure.</span></span> <span data-ttu-id="bae2e-137">Zwiększające bezpieczeństwo za pośrednictwem tylko podanie nazwy użytkownika i hasła, w tym przykładzie tworzy podstawowe usługę podmiotu zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="bae2e-137">To improve security over just providing a username and password, this example creates a basic service principal.</span></span>

<span data-ttu-id="bae2e-138">Utwórz usługę podmiotu zabezpieczeń z [az ad sp utworzyć do rbac](/cli/azure/ad/sp#create-for-rbac) i poświadczenia, które wymaga OpenShift wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="bae2e-138">Create a service principal with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) and output the credentials that OpenShift needs:</span></span>

```azurecli
az ad sp create-for-rbac --name openshiftsp \
          --role Contributor --password {strong password} \
          --scopes $(az group show --name myResourceGroup --query id)
```
<span data-ttu-id="bae2e-139">Zwróć uwagę na właściwość appId zwrócone przez polecenie.</span><span class="sxs-lookup"><span data-stu-id="bae2e-139">Take note of the appId property returned from the command.</span></span>
```json
{
  "appId": "a487e0c1-82af-47d9-9a0b-af184eb87646d",
  "displayName": "openshiftsp",
  "name": "http://openshiftsp",
  "password": {strong password},
  "tenant": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX"
}
```
 > [!WARNING] 
 > <span data-ttu-id="bae2e-140">Nie twórz niezabezpieczonego hasła.</span><span class="sxs-lookup"><span data-stu-id="bae2e-140">Don't create an insecure password.</span></span>  <span data-ttu-id="bae2e-141">Postępuj zgodnie ze wskazówkami zawartymi w [ograniczeniach i regułach dotyczących hasła usługi Azure AD](/azure/active-directory/active-directory-passwords-policy).</span><span class="sxs-lookup"><span data-stu-id="bae2e-141">Follow the [Azure AD password rules and restrictions](/azure/active-directory/active-directory-passwords-policy) guidance.</span></span>

<span data-ttu-id="bae2e-142">Aby uzyskać więcej informacji dotyczących nazwy główne usług, zobacz [Tworzenie nazwy głównej usługi platformy Azure z 2.0 interfejsu wiersza polecenia platformy Azure](/cli/azure/create-an-azure-service-principal-azure-cli)</span><span class="sxs-lookup"><span data-stu-id="bae2e-142">For more information on service principals, see [Create an Azure service principal with Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)</span></span>

## <a name="deploy-the-openshift-origin-template"></a><span data-ttu-id="bae2e-143">Wdrażanie szablonu OpenShift źródła</span><span class="sxs-lookup"><span data-stu-id="bae2e-143">Deploy the OpenShift Origin template</span></span>
<span data-ttu-id="bae2e-144">Następnie wdrożyć pochodzenia OpenShift przy użyciu szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bae2e-144">Next deploy OpenShift Origin using an Azure Resource Manager template.</span></span> 

> [!NOTE] 
> <span data-ttu-id="bae2e-145">Polecenie wymaga az CLI 2.0.8 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="bae2e-145">The following command requires az CLI 2.0.8 or later.</span></span> <span data-ttu-id="bae2e-146">Az interfejsu wiersza polecenia można sprawdzić wersji z `az --version` polecenia.</span><span class="sxs-lookup"><span data-stu-id="bae2e-146">You can verify the az CLI version with the `az --version` command.</span></span> <span data-ttu-id="bae2e-147">Aby zaktualizować wersję interfejsu wiersza polecenia, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="bae2e-147">To update the CLI version, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="bae2e-148">Użyj `appId` wartości z nazwy głównej usługi utworzony wcześniej dla `aadClientId` parametru.</span><span class="sxs-lookup"><span data-stu-id="bae2e-148">Use the `appId` value from the service principal you created earlier for the `aadClientId` parameter.</span></span>

```azurecli 
az group deployment create --name myOpenShiftCluster \
      --template-uri https://raw.githubusercontent.com/Microsoft/openshift-origin/master/azuredeploy.json \
      --params \ 
        openshiftMasterPublicIpDnsLabel=myopenshiftmaster \
        infraLbPublicIpDnsLabel=myopenshiftlb \
        openshiftPassword=Pass@word!
        sshPublicKey=~/.ssh/openshift_rsa.pub \
        keyVaultResourceGroup=myResourceGroup \
        keyVaultName=myKeyVault \
        keyVaultSecret=OpenShiftKey \
        aadClientId={appId} \
        aadClientSecret={strong password} 
```
<span data-ttu-id="bae2e-149">Wdrażanie może potrwać maksymalnie 20 minut.</span><span class="sxs-lookup"><span data-stu-id="bae2e-149">The deployment may take up to 20 minutes to complete.</span></span> <span data-ttu-id="bae2e-150">Adres URL konsoli OpenShift i nazwa DNS wzorca OpenShift drukowania na terminalu po zakończeniu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="bae2e-150">The URL of the OpenShift console and DNS name of the OpenShift master is printed to the terminal when the deployment completes.</span></span>

```json
{
  "OpenShift Console Uri": "http://openshiftlb.cloudapp.azure.com:8443/console",
  "OpenShift Master SSH": "ocpadmin@myopenshiftmaster.cloudapp.azure.com"
}
```
## <a name="connect-to-the-openshift-cluster"></a><span data-ttu-id="bae2e-151">Połącz się z klastrem OpenShift</span><span class="sxs-lookup"><span data-stu-id="bae2e-151">Connect to the OpenShift cluster</span></span>
<span data-ttu-id="bae2e-152">Po zakończeniu wdrożenia łączenie z konsolą OpenShift przy użyciu przeglądarki `OpenShift Console Uri`.</span><span class="sxs-lookup"><span data-stu-id="bae2e-152">When the deployment completes, connect to the OpenShift console using the browser using the `OpenShift Console Uri`.</span></span> <span data-ttu-id="bae2e-153">Alternatywnie można nawiązać wzorca OpenShift przy użyciu następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="bae2e-153">Alternatively, you can connect to the OpenShift master using the following command.</span></span>

```bash
$ ssh ocpadmin@myopenshiftmaster.cloudapp.azure.com
```

## <a name="clean-up-resources"></a><span data-ttu-id="bae2e-154">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="bae2e-154">Clean up resources</span></span>
<span data-ttu-id="bae2e-155">Gdy nie są już potrzebne, można użyć [usunięcie grupy az](/cli/azure/group#delete) polecenia, aby usunąć grupę zasobów, OpenShift klastra, a wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="bae2e-155">When no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, OpenShift cluster, and all related resources.</span></span>

```azurecli 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="bae2e-156">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bae2e-156">Next steps</span></span>

<span data-ttu-id="bae2e-157">W przypadku tego samouczka, zapamiętanych jak:</span><span class="sxs-lookup"><span data-stu-id="bae2e-157">In this tutorial, learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="bae2e-158">Utwórz KeyVault do zarządzania kluczy SSH dla klastra OpenShift.</span><span class="sxs-lookup"><span data-stu-id="bae2e-158">Create a KeyVault to manage SSH keys for the OpenShift cluster.</span></span>
> * <span data-ttu-id="bae2e-159">Wdrażanie klastra OpenShift na maszynach wirtualnych Azure.</span><span class="sxs-lookup"><span data-stu-id="bae2e-159">Deploy an OpenShift cluster on Azure VMs.</span></span> 
> * <span data-ttu-id="bae2e-160">Instalowanie i konfigurowanie [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) do zarządzania klastrem.</span><span class="sxs-lookup"><span data-stu-id="bae2e-160">Install and configure the [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) to manage the cluster.</span></span>

<span data-ttu-id="bae2e-161">Po wdrożeniu klastra OpenShift pochodzenia.</span><span class="sxs-lookup"><span data-stu-id="bae2e-161">Now that OpenShift Origin cluster is deployed.</span></span> <span data-ttu-id="bae2e-162">Możesz wykonać OpenShift samouczkami, aby dowiedzieć się, jak wdrażanie pierwszej aplikacji i korzystania z narzędzi OpenShift.</span><span class="sxs-lookup"><span data-stu-id="bae2e-162">You can follow OpenShift tutorials to learn how to deploy your first application and use the OpenShift tools.</span></span> <span data-ttu-id="bae2e-163">Zobacz [wprowadzenie pochodzenia OpenShift](https://docs.openshift.org/latest/getting_started/index.html) rozpocząć pracę.</span><span class="sxs-lookup"><span data-stu-id="bae2e-163">See [Getting Started with OpenShift Origin](https://docs.openshift.org/latest/getting_started/index.html) to get started.</span></span> 
