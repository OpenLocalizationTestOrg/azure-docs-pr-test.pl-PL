---
title: "aaaDeploy tooAzure wystąpień kontenera z hello rejestru kontenera platformy Azure | Dokumentacja platformy Azure"
description: "Wdrażanie wystąpień kontenera tooAzure z hello rejestru kontenera platformy Azure"
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
ms.openlocfilehash: 2667f91db8ed92a9ccc9ba722a2b1f5c5ea93886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-container-instances-from-hello-azure-container-registry"></a><span data-ttu-id="67c18-103">Wdrażanie wystąpień kontenera tooAzure z hello rejestru kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="67c18-103">Deploy tooAzure Container Instances from hello Azure Container Registry</span></span>

<span data-ttu-id="67c18-104">Witaj rejestru kontenera Azure jest rejestru Azure, prywatnego obrazów kontenera Docker.</span><span class="sxs-lookup"><span data-stu-id="67c18-104">hello Azure Container Registry is an Azure-based, private registry, for Docker container images.</span></span> <span data-ttu-id="67c18-105">W tym artykule opisano, jak toodeploy kontenera obrazy przechowywane w hello Azure kontenera rejestru tooAzure wystąpień kontenera.</span><span class="sxs-lookup"><span data-stu-id="67c18-105">This article covers how toodeploy container images stored in hello Azure Container Registry tooAzure Container Instances.</span></span>

## <a name="using-hello-azure-cli"></a><span data-ttu-id="67c18-106">Przy użyciu hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="67c18-106">Using hello Azure CLI</span></span>

<span data-ttu-id="67c18-107">Witaj interfejsu wiersza polecenia Azure zawiera polecenia do tworzenia i zarządzania kontenerami w wystąpień kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="67c18-107">hello Azure CLI includes commands for creating and managing containers in Azure Container Instances.</span></span> <span data-ttu-id="67c18-108">Jeśli określisz prywatnej obraz powitania `create` polecenia, można również określić hello obrazu rejestru wymagane jest hasło tooauthenticate z rejestru kontenera hello.</span><span class="sxs-lookup"><span data-stu-id="67c18-108">If you specify a private image in hello `create` command, you can also specify hello image registry password required tooauthenticate with hello container registry.</span></span>

```azurecli-interactive
az container create --name myprivatecontainer --image mycontainerregistry.azurecr.io/mycontainerimage:v1 --registry-password myRegistryPassword --resource-group myresourcegroup
```

<span data-ttu-id="67c18-109">Witaj `create` polecenia również obsługuje określanie hello `registry-login-server` i `registry-username`.</span><span class="sxs-lookup"><span data-stu-id="67c18-109">hello `create` command also supports specifying hello `registry-login-server` and `registry-username`.</span></span> <span data-ttu-id="67c18-110">Jednak serwer logowania hello hello rejestru kontenera Azure jest zawsze *registryname*. azurecr.io i hello domyślna nazwa użytkownika to *registryname*, więc te wartości są wywnioskować na podstawie nazwy obraz powitania, jeśli nie zostało podane.</span><span class="sxs-lookup"><span data-stu-id="67c18-110">However, hello login server for hello Azure Container Registry is always *registryname*.azurecr.io and hello default username is *registryname*, so these values are inferred from hello image name if not explicitly provided.</span></span>

## <a name="using-an-azure-resource-manager-template"></a><span data-ttu-id="67c18-111">Przy użyciu szablonu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="67c18-111">Using an Azure Resource Manager template</span></span>

<span data-ttu-id="67c18-112">Możesz określić właściwości hello rejestracji kontenera Azure w szablonie usługi Azure Resource Manager, umieszczając w niej hello `imageRegistryCredentials` właściwości w definicji grupy kontenera hello:</span><span class="sxs-lookup"><span data-stu-id="67c18-112">You can specify hello properties of your Azure Container Registry in an Azure Resource Manager template by including hello `imageRegistryCredentials` property in hello container group definition:</span></span>

```json
"imageRegistryCredentials": [
  {
    "server": "imageRegistryLoginServer",
    "username": "imageRegistryUsername",
    "password": "imageRegistryPassword"
  }
]
```

<span data-ttu-id="67c18-113">tooavoid przechowywania hasła rejestru kontenera bezpośrednio w szablonie hello, firma Microsoft zaleca, zapisz go jako klucza tajnego w [usługi Azure Key Vault](../key-vault/key-vault-manage-with-cli2.md) i odwołaj się w szablonie hello przy użyciu hello [natywna integracja pomiędzy usługą Witaj usługi Azure Resource Manager i usługi Key Vault](../azure-resource-manager/resource-manager-keyvault-parameter.md).</span><span class="sxs-lookup"><span data-stu-id="67c18-113">tooavoid storing your container registry password directly in hello template, we recommend that you store it as a secret in [Azure Key Vault](../key-vault/key-vault-manage-with-cli2.md) and reference it in hello template using hello [native integration between hello Azure Resource Manager and Key Vault](../azure-resource-manager/resource-manager-keyvault-parameter.md).</span></span>

## <a name="using-hello-azure-portal"></a><span data-ttu-id="67c18-114">Przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="67c18-114">Using hello Azure portal</span></span>

<span data-ttu-id="67c18-115">Jeśli obsługa obrazów kontenera w hello rejestru kontenera platformy Azure, można łatwo utworzyć kontener w wystąpień kontenera Azure za pomocą hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="67c18-115">If you maintain container images in hello Azure Container Registry, you can easily create a container in Azure Container Instances using hello Azure portal.</span></span>

1. <span data-ttu-id="67c18-116">W hello portalu Azure Przejdź tooyour kontenera rejestru.</span><span class="sxs-lookup"><span data-stu-id="67c18-116">In hello Azure portal, navigate tooyour container registry.</span></span>

2. <span data-ttu-id="67c18-117">Wybierz repozytoriów.</span><span class="sxs-lookup"><span data-stu-id="67c18-117">Choose Repositories.</span></span>

    ![menu rejestru kontenera Azure Hello hello portalu Azure][acr-menu]

3. <span data-ttu-id="67c18-119">Wybierz hello repozytorium, który ma toodeploy z.</span><span class="sxs-lookup"><span data-stu-id="67c18-119">Choose hello repository that you want toodeploy from.</span></span>

4. <span data-ttu-id="67c18-120">Kliknij prawym przyciskiem myszy hello tag obrazu kontenera hello ma toodeploy.</span><span class="sxs-lookup"><span data-stu-id="67c18-120">Right-click hello tag for hello container image you want toodeploy.</span></span>

    ![Menu kontekstowe dla uruchamiania kontener z wystąpień kontenera platformy Azure][acr-runinstance-contextmenu]

5. <span data-ttu-id="67c18-122">Wprowadź nazwę kontenera hello i nazwę grupy zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="67c18-122">Enter a name for hello container and a name for hello resource group.</span></span> <span data-ttu-id="67c18-123">W razie potrzeby można również zmienić hello wartości domyślne.</span><span class="sxs-lookup"><span data-stu-id="67c18-123">You can also change hello default values if you wish.</span></span>

    ![Tworzenie menu dla wystąpień kontenera platformy Azure][acr-create-deeplink]

6. <span data-ttu-id="67c18-125">Po zakończeniu wdrażania hello można przechodzić toohello kontenera grupy z toofind okienko powiadomień hello adresu IP i inne właściwości.</span><span class="sxs-lookup"><span data-stu-id="67c18-125">Once hello deployment completes, you can navigate toohello container group from hello notifications pane toofind its IP address and other properties.</span></span>

    ![Widok szczegółów grupy kontener wystąpień kontenera platformy Azure][aci-detailsview]

## <a name="next-steps"></a><span data-ttu-id="67c18-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="67c18-127">Next steps</span></span>

<span data-ttu-id="67c18-128">Dowiedz się, jak kontenery toobuild wypchniesz tooa Kontener prywatny rejestru i wdrażać je wystąpień kontenera tooAzure przez [Ukończenie samouczka hello](container-instances-tutorial-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="67c18-128">Learn how toobuild containers, push them tooa private container registry, and deploy them tooAzure Container Instances by [completing hello tutorial](container-instances-tutorial-prepare-app.md).</span></span>

<!-- IMAGES -->
[acr-menu]: ./media/container-instances-using-azure-container-registry/acr-menu.png

[acr-runinstance-contextmenu]: ./media/container-instances-using-azure-container-registry/acr-runinstance-contextmenu.png

[acr-create-deeplink]: ./media/container-instances-using-azure-container-registry/acr-create-deeplink.png

[aci-detailsview]: ./media/container-instances-using-azure-container-registry/aci-detailsview.png
