---
title: "aaaCreate Centrum IoT przy użyciu wiersza polecenia platformy Azure (az.py) | Dokumentacja firmy Microsoft"
description: "Jak toocreate Centrum Azure IoT przy użyciu hello 2.0 interfejsu wiersza polecenia platformy Azure i platform (az.py)."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-hub
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 9c9639235c2ac343e6ceb9578291dafaea26ea24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-cli-20"></a><span data-ttu-id="8ca68-103">Tworzenie Centrum IoT przy użyciu hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8ca68-103">Create an IoT hub using hello Azure CLI 2.0</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="8ca68-104">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="8ca68-104">Introduction</span></span>

<span data-ttu-id="8ca68-105">Można użyć toocreate Azure CLI 2.0 (az.py) i programowe zarządzanie centra Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="8ca68-105">You can use Azure CLI 2.0 (az.py) toocreate and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="8ca68-106">W tym artykule opisano, jak toouse hello Azure CLI 2.0 (az.py) toocreate Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="8ca68-106">This article shows you how toouse hello Azure CLI 2.0 (az.py) toocreate an IoT hub.</span></span>

<span data-ttu-id="8ca68-107">Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="8ca68-107">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="8ca68-108">[Azure CLI (azure.js)](iot-hub-create-using-cli-nodejs.md) — hello interfejsu wiersza polecenia dla hello classic i zasobów zarządzania modele wdrażania.</span><span class="sxs-lookup"><span data-stu-id="8ca68-108">[Azure CLI (azure.js)](iot-hub-create-using-cli-nodejs.md) – hello CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="8ca68-109">Azure CLI 2.0 (az.py) - hello generacji interfejsu wiersza polecenia dla hello zarządzania model wdrażania zasobów zgodnie z opisem w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="8ca68-109">Azure CLI 2.0 (az.py) - hello next generation CLI for hello resource management deployment model as described in this article.</span></span>

<span data-ttu-id="8ca68-110">toocomplete tego samouczka należy hello następujące:</span><span class="sxs-lookup"><span data-stu-id="8ca68-110">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="8ca68-111">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8ca68-111">An active Azure account.</span></span> <span data-ttu-id="8ca68-112">Jeśli go nie masz, możesz utworzyć [bezpłatne konto][lnk-free-trial] w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="8ca68-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="8ca68-113">[Azure CLI 2.0][lnk-CLI-install].</span><span class="sxs-lookup"><span data-stu-id="8ca68-113">[Azure CLI 2.0][lnk-CLI-install].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="8ca68-114">Zaloguj się i ustawić konta platformy Azure</span><span class="sxs-lookup"><span data-stu-id="8ca68-114">Sign in and set your Azure account</span></span>

<span data-ttu-id="8ca68-115">Zaloguj się tooyour konto platformy Azure i wyboru subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="8ca68-115">Sign in tooyour Azure account and select your subscription.</span></span>

1. <span data-ttu-id="8ca68-116">W wierszu polecenia hello Uruchom hello [polecenia logowania][lnk-login-command]:</span><span class="sxs-lookup"><span data-stu-id="8ca68-116">At hello command prompt, run hello [login command][lnk-login-command]:</span></span>
    
    ```azurecli
    az login
    ```

    <span data-ttu-id="8ca68-117">Postępuj zgodnie z tooauthenticate instrukcje hello przy użyciu kodu hello i zaloguj się na tooyour konto platformy Azure za pośrednictwem przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="8ca68-117">Follow hello instructions tooauthenticate using hello code and sign in tooyour Azure account through a web browser.</span></span>

2. <span data-ttu-id="8ca68-118">Jeśli masz wiele subskrypcji Azure, logowanie tooAzure umożliwiają dostęp tooall hello Azure konta skojarzone z poświadczeniami użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8ca68-118">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure accounts associated with your credentials.</span></span> <span data-ttu-id="8ca68-119">Poniższych hello [toolist polecenia hello Azure kont] [ lnk-az-account-command] dostępne dla toouse możesz:</span><span class="sxs-lookup"><span data-stu-id="8ca68-119">Use hello following [command toolist hello Azure accounts][lnk-az-account-command] available for you toouse:</span></span>
    
    ```azurecli
    az account list 
    ```

    <span data-ttu-id="8ca68-120">Użyj następującego polecenia tooselect subskrypcji ma się, że toouse toorun hello polecenia toocreate Centrum IoT hello.</span><span class="sxs-lookup"><span data-stu-id="8ca68-120">Use hello following command tooselect subscription that you want toouse toorun hello commands toocreate your IoT hub.</span></span> <span data-ttu-id="8ca68-121">Identyfikator lub Nazwa subskrypcji hello można użyć z danych wyjściowych hello hello poprzednie polecenie:</span><span class="sxs-lookup"><span data-stu-id="8ca68-121">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="create-an-iot-hub"></a><span data-ttu-id="8ca68-122">Tworzenie Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="8ca68-122">Create an IoT Hub</span></span>

<span data-ttu-id="8ca68-123">Przy użyciu hello Azure CLI toocreate grupę zasobów, a następnie dodaj Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="8ca68-123">Use hello Azure CLI toocreate a resource group and then add an IoT hub.</span></span>

1. <span data-ttu-id="8ca68-124">Podczas tworzenia Centrum IoT należy utworzyć ją w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="8ca68-124">When you create an IoT hub, you must create it in a resource group.</span></span> <span data-ttu-id="8ca68-125">Użyj istniejącej grupy zasobów lub uruchomić następujące hello [toocreate polecenia grupę zasobów][lnk-az-resource-command]:</span><span class="sxs-lookup"><span data-stu-id="8ca68-125">Either use an existing resource group, or run hello following [command toocreate a resource group][lnk-az-resource-command]:</span></span>
    
    ```azurecli
     az group create --name {your resource group name} --location westus
    ```

    > [!TIP]
    > <span data-ttu-id="8ca68-126">Witaj w poprzednim przykładzie tworzy hello grupy zasobów w hello lokalizacji zachodnie stany USA.</span><span class="sxs-lookup"><span data-stu-id="8ca68-126">hello previous example creates hello resource group in hello West US location.</span></span> <span data-ttu-id="8ca68-127">Można wyświetlić listę dostępnych lokalizacji, uruchamiając polecenie hello `az account list-locations -o table`.</span><span class="sxs-lookup"><span data-stu-id="8ca68-127">You can view a list of available locations by running hello command `az account list-locations -o table`.</span></span>
    >
    >

2. <span data-ttu-id="8ca68-128">Uruchom następujące hello [toocreate polecenia Centrum IoT] [ lnk-az-iot-command] w grupie zasobów, przy użyciu globalnie unikatowej nazwy Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="8ca68-128">Run hello following [command toocreate an IoT hub][lnk-az-iot-command] in your resource group, using a globally unique name for your IoT hub:</span></span>
    
    ```azurecli
    az iot hub create --name {your iot hub name} --resource-group {your resource group name} --sku S1
    ```

   [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


> [!NOTE]
> <span data-ttu-id="8ca68-129">poprzednie polecenie Hello utworzenie Centrum IoT w hello S1, dla której są rozliczane warstwy cenowej.</span><span class="sxs-lookup"><span data-stu-id="8ca68-129">hello previous command creates an IoT hub in hello S1 pricing tier for which you are billed.</span></span> <span data-ttu-id="8ca68-130">Aby uzyskać więcej informacji, zobacz [cennik Centrum IoT Azure][lnk-iot-pricing].</span><span class="sxs-lookup"><span data-stu-id="8ca68-130">For more information, see [Azure IoT Hub pricing][lnk-iot-pricing].</span></span>
>
>

## <a name="remove-an-iot-hub"></a><span data-ttu-id="8ca68-131">Usuń Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="8ca68-131">Remove an IoT Hub</span></span>

<span data-ttu-id="8ca68-132">Można użyć hello Azure CLI zbyt[usunąć pojedynczego zasobu][lnk-az-resource-command], na przykład Centrum IoT lub Usuń grupę zasobów i wszystkie jego zasoby, w tym wszystkie centra IoT.</span><span class="sxs-lookup"><span data-stu-id="8ca68-132">You can use hello Azure CLI too[delete an individual resource][lnk-az-resource-command], such as an IoT hub, or delete a resource group and all its resources, including any IoT hubs.</span></span>

<span data-ttu-id="8ca68-133">toodelete Centrum IoT, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="8ca68-133">toodelete an IoT hub, run hello following command:</span></span>

```azurecli
az iot hub delete --name {your iot hub name} --resource-group {your resource group name}
```

<span data-ttu-id="8ca68-134">toodelete grupę zasobów i wszystkie jego zasoby, hello uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="8ca68-134">toodelete a resource group and all its resources, run hello following command:</span></span>

```azurecli
az group delete --name {your resource group name}
```

## <a name="next-steps"></a><span data-ttu-id="8ca68-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8ca68-135">Next steps</span></span>
<span data-ttu-id="8ca68-136">toolearn więcej informacji na temat tworzenia Centrum IoT, zobacz następujące artykuły hello:</span><span class="sxs-lookup"><span data-stu-id="8ca68-136">toolearn more about developing for IoT Hub, see hello following articles:</span></span>

* <span data-ttu-id="8ca68-137">[Przewodnik dewelopera Centrum IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="8ca68-137">[IoT Hub developer guide][lnk-devguide]</span></span>

<span data-ttu-id="8ca68-138">toofurther Poznaj możliwości hello Centrum IoT, zobacz:</span><span class="sxs-lookup"><span data-stu-id="8ca68-138">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="8ca68-139">[Przy użyciu hello toomanage portalu Azure IoT Hub][lnk-portal]</span><span class="sxs-lookup"><span data-stu-id="8ca68-139">[Using hello Azure portal toomanage IoT Hub][lnk-portal]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-CLI-install]: https://docs.microsoft.com/cli/azure/install-az-cli2
[lnk-login-command]: https://docs.microsoft.com/cli/azure/get-started-with-az-cli2
[lnk-az-account-command]: https://docs.microsoft.com/cli/azure/account
[lnk-az-register-command]: https://docs.microsoft.com/cli/azure/provider
[lnk-az-addcomponent-command]: https://docs.microsoft.com/cli/azure/component
[lnk-az-resource-command]: https://docs.microsoft.com/cli/azure/resource
[lnk-az-iot-command]: https://docs.microsoft.com/cli/azure/iot
[lnk-iot-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-devguide]: iot-hub-devguide.md
[lnk-portal]: iot-hub-create-through-portal.md 
