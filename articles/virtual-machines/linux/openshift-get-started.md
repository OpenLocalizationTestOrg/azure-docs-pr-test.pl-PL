---
title: aaaDeploy tooAzure pochodzenia OpenShift | Dokumentacja firmy Microsoft
description: "Dowiedz się maszyny wirtualne tooAzure pochodzenia OpenShift toodeploy."
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
ms.openlocfilehash: a67450c46da41134a5f6c669a9e54e14773ac5b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-openshift-origin-tooazure-virtual-machines"></a><span data-ttu-id="86832-103">Wdrażanie tooAzure pochodzenia OpenShift maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="86832-103">Deploy OpenShift Origin tooAzure Virtual Machines</span></span> 

<span data-ttu-id="86832-104">[Pochodzenie OpenShift](https://www.openshift.org/) to platforma kontenera typu open source oparty na [Kubernetes](https://kubernetes.io/).</span><span class="sxs-lookup"><span data-stu-id="86832-104">[OpenShift Origin](https://www.openshift.org/) is an open source container platform built on [Kubernetes](https://kubernetes.io/).</span></span> <span data-ttu-id="86832-105">Takie rozwiązanie upraszcza hello procesu wdrażania, skalowanie i działania aplikacji wielodostępnej.</span><span class="sxs-lookup"><span data-stu-id="86832-105">It simplifies hello process of deploying, scaling, and operating multi-tenant applications.</span></span> 

<span data-ttu-id="86832-106">W tym przewodniku opisano, jak toodeploy pochodzenia OpenShift na maszynach wirtualnych platformy Azure przy użyciu hello wiersza polecenia platformy Azure i szablony Menedżera zasobów Azure.</span><span class="sxs-lookup"><span data-stu-id="86832-106">This guide describes how toodeploy OpenShift Origin on Azure Virtual Machines using hello Azure CLI and Azure Resource Manager Templates.</span></span> <span data-ttu-id="86832-107">Ten samouczek zawiera informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="86832-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="86832-108">Tworzenie kluczy SSH dla klastra OpenShift hello KeyVault toomanage.</span><span class="sxs-lookup"><span data-stu-id="86832-108">Create a KeyVault toomanage SSH keys for hello OpenShift cluster.</span></span>
> * <span data-ttu-id="86832-109">Wdrażanie klastra OpenShift na maszynach wirtualnych Azure.</span><span class="sxs-lookup"><span data-stu-id="86832-109">Deploy an OpenShift cluster on Azure VMs.</span></span> 
> * <span data-ttu-id="86832-110">Instalowanie i konfigurowanie hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) toomanage hello klastra.</span><span class="sxs-lookup"><span data-stu-id="86832-110">Install and configure hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) toomanage hello cluster.</span></span>
> * <span data-ttu-id="86832-111">Dostosowywanie hello OpenShift wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="86832-111">Customize hello OpenShift deployment.</span></span>

<span data-ttu-id="86832-112">Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="86832-112">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="86832-113">To szybki start wymaga hello Azure CLI w wersji 2.0.8 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="86832-113">This quick start requires hello Azure CLI version 2.0.8 or later.</span></span> <span data-ttu-id="86832-114">Wersja hello toofind, uruchom `az --version`.</span><span class="sxs-lookup"><span data-stu-id="86832-114">toofind hello version, run `az --version`.</span></span> <span data-ttu-id="86832-115">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="86832-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="log-in-tooazure"></a><span data-ttu-id="86832-116">Zaloguj się za tooAzure</span><span class="sxs-lookup"><span data-stu-id="86832-116">Log in tooAzure</span></span> 
<span data-ttu-id="86832-117">Zaloguj się za tooyour subskrypcji platformy Azure z hello [logowania az](/cli/azure/#login) polecenia i wykonaj hello na ekranie instrukcjami lub kliknij przycisk **wypróbuj** toouse powłoki chmury.</span><span class="sxs-lookup"><span data-stu-id="86832-117">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions or click **Try it** toouse Cloud Shell.</span></span>

```azurecli 
az login
```
## <a name="create-a-resource-group"></a><span data-ttu-id="86832-118">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="86832-118">Create a resource group</span></span>

<span data-ttu-id="86832-119">Utwórz grupę zasobów o hello [Tworzenie grupy az](/cli/azure/group#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="86832-119">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="86832-120">Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="86832-120">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="86832-121">Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *eastus* lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="86832-121">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-key-vault"></a><span data-ttu-id="86832-122">Tworzenie magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="86832-122">Create a Key Vault</span></span>
<span data-ttu-id="86832-123">Tworzenie kluczy SSH dla klastra hello KeyVault toostore hello z hello [az keyvault utworzyć](/cli/azure/keyvault#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="86832-123">Create a KeyVault toostore hello SSH keys for hello cluster with hello [az keyvault create](/cli/azure/keyvault#create) command.</span></span>  

```azurecli 
az keyvault create --resource-group myResourceGroup --name myKeyVault \
       --enabled-for-template-deployment true \
       --location eastus
```

## <a name="create-an-ssh-key"></a><span data-ttu-id="86832-124">Tworzenie klucza SSH</span><span class="sxs-lookup"><span data-stu-id="86832-124">Create an SSH key</span></span> 
<span data-ttu-id="86832-125">Klucz SSH jest wymagane toosecure dostępu toohello pochodzenia OpenShift klastra.</span><span class="sxs-lookup"><span data-stu-id="86832-125">An SSH key is needed toosecure access toohello OpenShift Origin cluster.</span></span> <span data-ttu-id="86832-126">Utwórz parę kluczy SSH za pomocą hello `ssh-keygen` polecenia.</span><span class="sxs-lookup"><span data-stu-id="86832-126">Create an SSH key-pair using hello `ssh-keygen` command.</span></span> 
 
 ```bash
ssh-keygen -f ~/.ssh/openshift_rsa -t rsa -N ''
```

> [!NOTE]
> <span data-ttu-id="86832-127">Witaj pary kluczy SSH, którą utworzysz nie może zawierać hasło.</span><span class="sxs-lookup"><span data-stu-id="86832-127">hello SSH key pair you create must not have a passphrase.</span></span>

<span data-ttu-id="86832-128">Aby uzyskać więcej informacji na temat kluczy SSH w systemie Windows [jak klucze toocreate SSH w systemie Windows](/azure/virtual-machines/linux/ssh-from-windows).</span><span class="sxs-lookup"><span data-stu-id="86832-128">For more information on SSH keys on Windows, [How toocreate SSH keys on Windows](/azure/virtual-machines/linux/ssh-from-windows).</span></span>

## <a name="store-ssh-private-key-in-key-vault"></a><span data-ttu-id="86832-129">Przechowywanie klucza prywatnego SSH w magazynie kluczy</span><span class="sxs-lookup"><span data-stu-id="86832-129">Store SSH private key in Key Vault</span></span>
<span data-ttu-id="86832-130">Hello wdrożenia OpenShift używa klucza SSH hello utworzone dostępu toosecure toohello OpenShift wzorca.</span><span class="sxs-lookup"><span data-stu-id="86832-130">hello OpenShift deployment uses hello SSH key you created toosecure access toohello OpenShift master.</span></span> <span data-ttu-id="86832-131">tooenable hello wdrożenia toosecurely pobrać hello klucz SSH, przechowywać klucz hello w Key Vault za pomocą następującego polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="86832-131">tooenable hello deployment toosecurely retrieve hello SSH key, store hello key in Key Vault using hello following command.</span></span>

# <a name="enabled-for-template-deployment"></a><span data-ttu-id="86832-132">Włączony do wdrożenia szablonu</span><span class="sxs-lookup"><span data-stu-id="86832-132">Enabled for template deployment</span></span>
```azurecli
az keyvault secret set --vault-name KeyVaultName --name OpenShiftKey --file ~/.ssh/openshift.rsa
```

## <a name="create-a-service-principal"></a><span data-ttu-id="86832-133">Tworzenie nazwy głównej usługi</span><span class="sxs-lookup"><span data-stu-id="86832-133">Create a service principal</span></span> 
<span data-ttu-id="86832-134">OpenShift komunikuje się z platformy Azure przy użyciu nazwy użytkownika i hasła lub nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="86832-134">OpenShift communicates with Azure using a username and password or a service principal.</span></span> <span data-ttu-id="86832-135">Podmiot zabezpieczeń usługi Azure jest tożsamość zabezpieczeń korzystających z aplikacji, usługami i automatyzacja takich narzędzi jak OpenShift.</span><span class="sxs-lookup"><span data-stu-id="86832-135">An Azure service principal is a security identity that you can use with apps, services, and automation tools like OpenShift.</span></span> <span data-ttu-id="86832-136">Kontrolowanie i definiowanie uprawnień hello toowhat operacji hello service principal można wykonywać na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="86832-136">You control and define hello permissions as toowhat operations hello service principal can perform in Azure.</span></span> <span data-ttu-id="86832-137">tooimprove zabezpieczeń za pośrednictwem tylko podanie nazwy użytkownika i hasła, w tym przykładzie tworzy podstawowe usługę podmiotu zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="86832-137">tooimprove security over just providing a username and password, this example creates a basic service principal.</span></span>

<span data-ttu-id="86832-138">Utwórz usługę podmiotu zabezpieczeń z [az ad sp utworzyć do rbac](/cli/azure/ad/sp#create-for-rbac) i dane wyjściowe hello poświadczenia, które wymaga OpenShift:</span><span class="sxs-lookup"><span data-stu-id="86832-138">Create a service principal with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) and output hello credentials that OpenShift needs:</span></span>

```azurecli
az ad sp create-for-rbac --name openshiftsp \
          --role Contributor --password {strong password} \
          --scopes $(az group show --name myResourceGroup --query id)
```
<span data-ttu-id="86832-139">Zwróć uwagę na powitania appId właściwości zwróconej z hello polecenia.</span><span class="sxs-lookup"><span data-stu-id="86832-139">Take note of hello appId property returned from hello command.</span></span>
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
 > <span data-ttu-id="86832-140">Nie twórz niezabezpieczonego hasła.</span><span class="sxs-lookup"><span data-stu-id="86832-140">Don't create an insecure password.</span></span>  <span data-ttu-id="86832-141">Postępuj zgodnie ze wskazówkami zawartymi w [ograniczeniach i regułach dotyczących hasła usługi Azure AD](/azure/active-directory/active-directory-passwords-policy).</span><span class="sxs-lookup"><span data-stu-id="86832-141">Follow the [Azure AD password rules and restrictions](/azure/active-directory/active-directory-passwords-policy) guidance.</span></span>

<span data-ttu-id="86832-142">Aby uzyskać więcej informacji dotyczących nazwy główne usług, zobacz [Tworzenie nazwy głównej usługi platformy Azure z 2.0 interfejsu wiersza polecenia platformy Azure](/cli/azure/create-an-azure-service-principal-azure-cli)</span><span class="sxs-lookup"><span data-stu-id="86832-142">For more information on service principals, see [Create an Azure service principal with Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)</span></span>

## <a name="deploy-hello-openshift-origin-template"></a><span data-ttu-id="86832-143">Wdrażanie hello pochodzenia OpenShift szablonu</span><span class="sxs-lookup"><span data-stu-id="86832-143">Deploy hello OpenShift Origin template</span></span>
<span data-ttu-id="86832-144">Następnie wdrożyć pochodzenia OpenShift przy użyciu szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="86832-144">Next deploy OpenShift Origin using an Azure Resource Manager template.</span></span> 

> [!NOTE] 
> <span data-ttu-id="86832-145">Witaj następujące polecenie wymaga az CLI 2.0.8 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="86832-145">hello following command requires az CLI 2.0.8 or later.</span></span> <span data-ttu-id="86832-146">Możesz sprawdzić hello az CLI wersji z hello `az --version` polecenia.</span><span class="sxs-lookup"><span data-stu-id="86832-146">You can verify hello az CLI version with hello `az --version` command.</span></span> <span data-ttu-id="86832-147">tooupdate hello wersji interfejsu wiersza polecenia, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="86832-147">tooupdate hello CLI version, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="86832-148">Użyj hello `appId` wartości z nazwy głównej usługi hello utworzony wcześniej dla hello `aadClientId` parametru.</span><span class="sxs-lookup"><span data-stu-id="86832-148">Use hello `appId` value from hello service principal you created earlier for hello `aadClientId` parameter.</span></span>

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
<span data-ttu-id="86832-149">Witaj wdrażania może potrwać too20 toocomplete minut.</span><span class="sxs-lookup"><span data-stu-id="86832-149">hello deployment may take up too20 minutes toocomplete.</span></span> <span data-ttu-id="86832-150">Witaj adres URL konsoli OpenShift hello i nazwa DNS hello OpenShift wzorzec jest drukowane toohello terminal po zakończeniu wdrażania hello.</span><span class="sxs-lookup"><span data-stu-id="86832-150">hello URL of hello OpenShift console and DNS name of hello OpenShift master is printed toohello terminal when hello deployment completes.</span></span>

```json
{
  "OpenShift Console Uri": "http://openshiftlb.cloudapp.azure.com:8443/console",
  "OpenShift Master SSH": "ocpadmin@myopenshiftmaster.cloudapp.azure.com"
}
```
## <a name="connect-toohello-openshift-cluster"></a><span data-ttu-id="86832-151">Połącz toohello OpenShift klastra</span><span class="sxs-lookup"><span data-stu-id="86832-151">Connect toohello OpenShift cluster</span></span>
<span data-ttu-id="86832-152">Po zakończeniu wdrażania hello, Połącz konsolę OpenShift toohello za pomocą przeglądarki hello przy użyciu hello `OpenShift Console Uri`.</span><span class="sxs-lookup"><span data-stu-id="86832-152">When hello deployment completes, connect toohello OpenShift console using hello browser using hello `OpenShift Console Uri`.</span></span> <span data-ttu-id="86832-153">Alternatywnie możesz połączyć za pomocą następującego polecenia hello wzorca OpenShift toohello.</span><span class="sxs-lookup"><span data-stu-id="86832-153">Alternatively, you can connect toohello OpenShift master using hello following command.</span></span>

```bash
$ ssh ocpadmin@myopenshiftmaster.cloudapp.azure.com
```

## <a name="clean-up-resources"></a><span data-ttu-id="86832-154">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="86832-154">Clean up resources</span></span>
<span data-ttu-id="86832-155">Gdy nie są już potrzebne, można użyć hello [usunięcie grupy az](/cli/azure/group#delete) polecenia grupy zasobów hello tooremove, OpenShift klastra i wszystkich powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="86832-155">When no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, OpenShift cluster, and all related resources.</span></span>

```azurecli 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="86832-156">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="86832-156">Next steps</span></span>

<span data-ttu-id="86832-157">W przypadku tego samouczka, zapamiętanych jak:</span><span class="sxs-lookup"><span data-stu-id="86832-157">In this tutorial, learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="86832-158">Tworzenie kluczy SSH dla klastra OpenShift hello KeyVault toomanage.</span><span class="sxs-lookup"><span data-stu-id="86832-158">Create a KeyVault toomanage SSH keys for hello OpenShift cluster.</span></span>
> * <span data-ttu-id="86832-159">Wdrażanie klastra OpenShift na maszynach wirtualnych Azure.</span><span class="sxs-lookup"><span data-stu-id="86832-159">Deploy an OpenShift cluster on Azure VMs.</span></span> 
> * <span data-ttu-id="86832-160">Instalowanie i konfigurowanie hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) toomanage hello klastra.</span><span class="sxs-lookup"><span data-stu-id="86832-160">Install and configure hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) toomanage hello cluster.</span></span>

<span data-ttu-id="86832-161">Po wdrożeniu klastra OpenShift pochodzenia.</span><span class="sxs-lookup"><span data-stu-id="86832-161">Now that OpenShift Origin cluster is deployed.</span></span> <span data-ttu-id="86832-162">Jak wykonać toolearn samouczki OpenShift toodeploy pierwszą aplikację i użyj narzędzia OpenShift hello.</span><span class="sxs-lookup"><span data-stu-id="86832-162">You can follow OpenShift tutorials toolearn how toodeploy your first application and use hello OpenShift tools.</span></span> <span data-ttu-id="86832-163">Zobacz [wprowadzenie pochodzenia OpenShift](https://docs.openshift.org/latest/getting_started/index.html) tooget uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="86832-163">See [Getting Started with OpenShift Origin](https://docs.openshift.org/latest/getting_started/index.html) tooget started.</span></span> 
