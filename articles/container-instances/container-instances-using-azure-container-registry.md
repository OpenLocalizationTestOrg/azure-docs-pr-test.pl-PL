---
title: "Wdrażanie do wystąpień kontenera platformy Azure z rejestru kontenera platformy Azure | Dokumentacja platformy Azure"
description: "Wdrażanie do wystąpień kontenera platformy Azure z rejestru kontenera platformy Azure"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/02/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: aa1c4ea379c10dff246e2f924a345f9fa444aa64
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-to-azure-container-instances-from-the-azure-container-registry"></a><span data-ttu-id="b2c1c-103">Wdrażanie do wystąpień kontenera platformy Azure z rejestru kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b2c1c-103">Deploy to Azure Container Instances from the Azure Container Registry</span></span>

<span data-ttu-id="b2c1c-104">Rejestr kontenera Azure jest rejestru Azure, prywatnego obrazów kontenera Docker.</span><span class="sxs-lookup"><span data-stu-id="b2c1c-104">The Azure Container Registry is an Azure-based, private registry, for Docker container images.</span></span> <span data-ttu-id="b2c1c-105">W tym artykule opisano sposób wdrażania obrazów kontenera przechowywane w rejestrze kontenera Azure do wystąpień kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b2c1c-105">This article covers how to deploy container images stored in the Azure Container Registry to Azure Container Instances.</span></span>

## <a name="using-the-azure-cli"></a><span data-ttu-id="b2c1c-106">Korzystanie z interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b2c1c-106">Using the Azure CLI</span></span>

<span data-ttu-id="b2c1c-107">Interfejsu wiersza polecenia Azure zawiera polecenia do tworzenia i zarządzania kontenerami w wystąpień kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b2c1c-107">The Azure CLI includes commands for creating and managing containers in Azure Container Instances.</span></span> <span data-ttu-id="b2c1c-108">Jeśli określisz prywatnej obrazu w `create` polecenia, można również określić hasło rejestru obrazu, które są wymagane do uwierzytelniania za pomocą rejestru kontenera.</span><span class="sxs-lookup"><span data-stu-id="b2c1c-108">If you specify a private image in the `create` command, you can also specify the image registry password required to authenticate with the container registry.</span></span>

```azurecli-interactive
az container create --name myprivatecontainer --image mycontainerregistry.azurecr.io/mycontainerimage:v1 --registry-password myRegistryPassword --resource-group myresourcegroup
```

<span data-ttu-id="b2c1c-109">`create` Polecenia obsługuje również określenie `registry-login-server` i `registry-username`.</span><span class="sxs-lookup"><span data-stu-id="b2c1c-109">The `create` command also supports specifying the `registry-login-server` and `registry-username`.</span></span> <span data-ttu-id="b2c1c-110">Jednak serwery logowania rejestru kontenera platformy Azure są zawsze *registryname*. azurecr.io i domyślna nazwa użytkownika jest *registryname*, więc te wartości są wywnioskować na podstawie nazwy obrazu, jeśli nie udostępniony.</span><span class="sxs-lookup"><span data-stu-id="b2c1c-110">However, the login server for the Azure Container Registry is always *registryname*.azurecr.io and the default username is *registryname*, so these values are inferred from the image name if not explicitly provided.</span></span>

## <a name="using-an-azure-resource-manager-template"></a><span data-ttu-id="b2c1c-111">Przy użyciu szablonu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b2c1c-111">Using an Azure Resource Manager template</span></span>

<span data-ttu-id="b2c1c-112">Można określić właściwości rejestru kontenera platformy Azure w szablonie usługi Azure Resource Manager przez dołączenie `imageRegistryCredentials` właściwości w definicji kontenera grupy:</span><span class="sxs-lookup"><span data-stu-id="b2c1c-112">You can specify the properties of your Azure Container Registry in an Azure Resource Manager template by including the `imageRegistryCredentials` property in the container group definition:</span></span>

```json
"imageRegistryCredentials": [
  {
    "server": "imageRegistryLoginServer",
    "username": "imageRegistryUsername",
    "password": "imageRegistryPassword"
  }
]
```

<span data-ttu-id="b2c1c-113">Aby uniknąć przechowywania hasła rejestru kontenera bezpośrednio w szablonie, firma Microsoft zaleca, zapisz go jako klucza tajnego w [usługi Azure Key Vault](../key-vault/key-vault-manage-with-cli2.md) i odwołaj się za pomocą szablonu [natywna integracja pomiędzy usługą platformy Azure Resource Manager i magazynu kluczy](../azure-resource-manager/resource-manager-keyvault-parameter.md).</span><span class="sxs-lookup"><span data-stu-id="b2c1c-113">To avoid storing your container registry password directly in the template, we recommend that you store it as a secret in [Azure Key Vault](../key-vault/key-vault-manage-with-cli2.md) and reference it in the template using the [native integration between the Azure Resource Manager and Key Vault](../azure-resource-manager/resource-manager-keyvault-parameter.md).</span></span>

## <a name="using-the-azure-portal"></a><span data-ttu-id="b2c1c-114">Korzystanie z witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b2c1c-114">Using the Azure portal</span></span>

<span data-ttu-id="b2c1c-115">Jeśli obsługa obrazów kontenera w rejestrze kontenera platformy Azure, można łatwo utworzyć kontener w wystąpień kontenera Azure za pomocą portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b2c1c-115">If you maintain container images in the Azure Container Registry, you can easily create a container in Azure Container Instances using the Azure portal.</span></span>

1. <span data-ttu-id="b2c1c-116">W portalu Azure przejdź do kontenera rejestru.</span><span class="sxs-lookup"><span data-stu-id="b2c1c-116">In the Azure portal, navigate to your container registry.</span></span>

2. <span data-ttu-id="b2c1c-117">Wybierz repozytoriów.</span><span class="sxs-lookup"><span data-stu-id="b2c1c-117">Choose Repositories.</span></span>

    ![Menu rejestru kontenera platformy Azure w portalu Azure][acr-menu]

3. <span data-ttu-id="b2c1c-119">Wybierz przewidzianą do wdrożenia z repozytorium.</span><span class="sxs-lookup"><span data-stu-id="b2c1c-119">Choose the repository that you want to deploy from.</span></span>

4. <span data-ttu-id="b2c1c-120">Kliknij prawym przyciskiem myszy tag obrazu kontenera, który chcesz wdrożyć.</span><span class="sxs-lookup"><span data-stu-id="b2c1c-120">Right-click the tag for the container image you want to deploy.</span></span>

    ![Menu kontekstowe dla uruchamiania kontener z wystąpień kontenera platformy Azure][acr-runinstance-contextmenu]

5. <span data-ttu-id="b2c1c-122">Wprowadź nazwę kontenera i nazwy grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="b2c1c-122">Enter a name for the container and a name for the resource group.</span></span> <span data-ttu-id="b2c1c-123">Jeśli chcesz, możesz również zmienić wartości domyślne.</span><span class="sxs-lookup"><span data-stu-id="b2c1c-123">You can also change the default values if you wish.</span></span>

    ![Tworzenie menu dla wystąpień kontenera platformy Azure][acr-create-deeplink]

6. <span data-ttu-id="b2c1c-125">Po zakończeniu wdrożenia, można przejść do kontenera grupy z okienka powiadomienia, aby znaleźć adres IP i inne właściwości.</span><span class="sxs-lookup"><span data-stu-id="b2c1c-125">Once the deployment completes, you can navigate to the container group from the notifications pane to find its IP address and other properties.</span></span>

    ![Widok szczegółów grupy kontener wystąpień kontenera platformy Azure][aci-detailsview]

## <a name="next-steps"></a><span data-ttu-id="b2c1c-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b2c1c-127">Next steps</span></span>

<span data-ttu-id="b2c1c-128">Informacje o sposobie tworzenia kontenery, wypychanie ich rejestru Kontener prywatny i wdrożyć je do wystąpień kontenera Azure przez [wykonywania kroków samouczka](container-instances-tutorial-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="b2c1c-128">Learn how to build containers, push them to a private container registry, and deploy them to Azure Container Instances by [completing the tutorial](container-instances-tutorial-prepare-app.md).</span></span>

<!-- IMAGES -->
[acr-menu]: ./media/container-instances-using-azure-container-registry/acr-menu.png

[acr-runinstance-contextmenu]: ./media/container-instances-using-azure-container-registry/acr-runinstance-contextmenu.png

[acr-create-deeplink]: ./media/container-instances-using-azure-container-registry/acr-create-deeplink.png

[aci-detailsview]: ./media/container-instances-using-azure-container-registry/aci-detailsview.png
