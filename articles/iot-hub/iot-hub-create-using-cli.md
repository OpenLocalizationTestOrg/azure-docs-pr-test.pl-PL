---
title: "Tworzenie Centrum IoT przy użyciu wiersza polecenia platformy Azure (az.py) | Dokumentacja firmy Microsoft"
description: "Jak utworzyć Centrum Azure IoT przy użyciu interfejsu wiersza polecenia Azure i platform w 2.0 (az.py)."
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
ms.openlocfilehash: 161089159999a4a63a39b059e69a08b7a9297445
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-iot-hub-using-the-azure-cli-20"></a><span data-ttu-id="40ead-103">Tworzenie Centrum IoT przy użyciu 2.0 interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="40ead-103">Create an IoT hub using the Azure CLI 2.0</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="40ead-104">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="40ead-104">Introduction</span></span>

<span data-ttu-id="40ead-105">Azure CLI 2.0 (az.py) umożliwia tworzenie i zarządzanie nimi centra Azure IoT programowo.</span><span class="sxs-lookup"><span data-stu-id="40ead-105">You can use Azure CLI 2.0 (az.py) to create and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="40ead-106">W tym artykule przedstawiono sposób umożliwiają utworzenie Centrum IoT Azure CLI 2.0 (az.py).</span><span class="sxs-lookup"><span data-stu-id="40ead-106">This article shows you how to use the Azure CLI 2.0 (az.py) to create an IoT hub.</span></span>

<span data-ttu-id="40ead-107">Zadanie można wykonać przy użyciu jednej z następujących wersji interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="40ead-107">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="40ead-108">[Azure CLI (azure.js)](iot-hub-create-using-cli-nodejs.md) — interfejsu wiersza polecenia dla modeli wdrażania zarządzania classic i zasobów.</span><span class="sxs-lookup"><span data-stu-id="40ead-108">[Azure CLI (azure.js)](iot-hub-create-using-cli-nodejs.md) – the CLI for the classic and resource management deployment models.</span></span>
* <span data-ttu-id="40ead-109">Azure CLI 2.0 (az.py) - generacji interfejsu wiersza polecenia do zarządzania model wdrażania zasobów zgodnie z opisem w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="40ead-109">Azure CLI 2.0 (az.py) - the next generation CLI for the resource management deployment model as described in this article.</span></span>

<span data-ttu-id="40ead-110">Do wykonania kroków tego samouczka niezbędne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="40ead-110">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="40ead-111">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="40ead-111">An active Azure account.</span></span> <span data-ttu-id="40ead-112">Jeśli go nie masz, możesz utworzyć [bezpłatne konto][lnk-free-trial] w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="40ead-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="40ead-113">[Azure CLI 2.0][lnk-CLI-install].</span><span class="sxs-lookup"><span data-stu-id="40ead-113">[Azure CLI 2.0][lnk-CLI-install].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="40ead-114">Zaloguj się i ustawić konta platformy Azure</span><span class="sxs-lookup"><span data-stu-id="40ead-114">Sign in and set your Azure account</span></span>

<span data-ttu-id="40ead-115">Zaloguj się do konta platformy Azure i wyboru subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="40ead-115">Sign in to your Azure account and select your subscription.</span></span>

1. <span data-ttu-id="40ead-116">W wierszu polecenia Uruchom [polecenia logowania][lnk-login-command]:</span><span class="sxs-lookup"><span data-stu-id="40ead-116">At the command prompt, run the [login command][lnk-login-command]:</span></span>
    
    ```azurecli
    az login
    ```

    <span data-ttu-id="40ead-117">Postępuj zgodnie z instrukcjami w celu uwierzytelnienia przy użyciu kodu i zaloguj się do konta platformy Azure za pośrednictwem przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="40ead-117">Follow the instructions to authenticate using the code and sign in to your Azure account through a web browser.</span></span>

2. <span data-ttu-id="40ead-118">Jeśli masz wiele subskrypcji Azure, logowanie do platformy Azure przydziela dostęp do wszystkich kont platformy Azure skojarzone z poświadczeniami użytkownika.</span><span class="sxs-lookup"><span data-stu-id="40ead-118">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure accounts associated with your credentials.</span></span> <span data-ttu-id="40ead-119">Należy użyć następującego [polecenia do listy kont Azure] [ lnk-az-account-command] dostępne do użycia:</span><span class="sxs-lookup"><span data-stu-id="40ead-119">Use the following [command to list the Azure accounts][lnk-az-account-command] available for you to use:</span></span>
    
    ```azurecli
    az account list 
    ```

    <span data-ttu-id="40ead-120">Użyj następującego polecenia, aby wybrać subskrypcję, która ma być używany do uruchamiania poleceń, aby utworzyć Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="40ead-120">Use the following command to select subscription that you want to use to run the commands to create your IoT hub.</span></span> <span data-ttu-id="40ead-121">Przy użyciu subskrypcji nazwa lub identyfikator z danych wyjściowych poprzednie polecenie:</span><span class="sxs-lookup"><span data-stu-id="40ead-121">You can use either the subscription name or ID from the output of the previous command:</span></span>

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="create-an-iot-hub"></a><span data-ttu-id="40ead-122">Tworzenie Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="40ead-122">Create an IoT Hub</span></span>

<span data-ttu-id="40ead-123">Użyj wiersza polecenia platformy Azure, Utwórz grupę zasobów, a następnie dodaj Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="40ead-123">Use the Azure CLI to create a resource group and then add an IoT hub.</span></span>

1. <span data-ttu-id="40ead-124">Podczas tworzenia Centrum IoT należy utworzyć ją w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="40ead-124">When you create an IoT hub, you must create it in a resource group.</span></span> <span data-ttu-id="40ead-125">Użyj istniejącej grupy zasobów, albo uruchom następujące polecenie [polecenie, aby utworzyć grupę zasobów][lnk-az-resource-command]:</span><span class="sxs-lookup"><span data-stu-id="40ead-125">Either use an existing resource group, or run the following [command to create a resource group][lnk-az-resource-command]:</span></span>
    
    ```azurecli
     az group create --name {your resource group name} --location westus
    ```

    > [!TIP]
    > <span data-ttu-id="40ead-126">Poprzedni przykład tworzy grupy zasobów w lokalizacji zachodnie stany USA.</span><span class="sxs-lookup"><span data-stu-id="40ead-126">The previous example creates the resource group in the West US location.</span></span> <span data-ttu-id="40ead-127">Można wyświetlić listę dostępnych lokalizacji, uruchamiając polecenie `az account list-locations -o table`.</span><span class="sxs-lookup"><span data-stu-id="40ead-127">You can view a list of available locations by running the command `az account list-locations -o table`.</span></span>
    >
    >

2. <span data-ttu-id="40ead-128">Uruchom następujące polecenie [polecenie, aby utworzyć Centrum IoT] [ lnk-az-iot-command] w grupie zasobów, przy użyciu globalnie unikatowej nazwy Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="40ead-128">Run the following [command to create an IoT hub][lnk-az-iot-command] in your resource group, using a globally unique name for your IoT hub:</span></span>
    
    ```azurecli
    az iot hub create --name {your iot hub name} --resource-group {your resource group name} --sku S1
    ```

   [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


> [!NOTE]
> <span data-ttu-id="40ead-129">Poprzednie polecenie powoduje utworzenie Centrum IoT w S1, dla której są rozliczane warstwy cenowej.</span><span class="sxs-lookup"><span data-stu-id="40ead-129">The previous command creates an IoT hub in the S1 pricing tier for which you are billed.</span></span> <span data-ttu-id="40ead-130">Aby uzyskać więcej informacji, zobacz [cennik Centrum IoT Azure][lnk-iot-pricing].</span><span class="sxs-lookup"><span data-stu-id="40ead-130">For more information, see [Azure IoT Hub pricing][lnk-iot-pricing].</span></span>
>
>

## <a name="remove-an-iot-hub"></a><span data-ttu-id="40ead-131">Usuń Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="40ead-131">Remove an IoT Hub</span></span>

<span data-ttu-id="40ead-132">Korzystając z wiersza polecenia platformy Azure do [usunąć pojedynczego zasobu][lnk-az-resource-command], na przykład Centrum IoT lub Usuń grupę zasobów i wszystkie jego zasoby, w tym wszystkie centra IoT.</span><span class="sxs-lookup"><span data-stu-id="40ead-132">You can use the Azure CLI to [delete an individual resource][lnk-az-resource-command], such as an IoT hub, or delete a resource group and all its resources, including any IoT hubs.</span></span>

<span data-ttu-id="40ead-133">Aby usunąć Centrum IoT, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="40ead-133">To delete an IoT hub, run the following command:</span></span>

```azurecli
az iot hub delete --name {your iot hub name} --resource-group {your resource group name}
```

<span data-ttu-id="40ead-134">Aby usunąć grupę zasobów i wszystkie jego zasoby, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="40ead-134">To delete a resource group and all its resources, run the following command:</span></span>

```azurecli
az group delete --name {your resource group name}
```

## <a name="next-steps"></a><span data-ttu-id="40ead-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="40ead-135">Next steps</span></span>
<span data-ttu-id="40ead-136">Aby dowiedzieć się więcej o tworzeniu aplikacji Centrum IoT, zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="40ead-136">To learn more about developing for IoT Hub, see the following articles:</span></span>

* <span data-ttu-id="40ead-137">[Przewodnik dewelopera Centrum IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="40ead-137">[IoT Hub developer guide][lnk-devguide]</span></span>

<span data-ttu-id="40ead-138">Aby dokładniej analizować możliwości Centrum IoT, zobacz:</span><span class="sxs-lookup"><span data-stu-id="40ead-138">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="40ead-139">[Przy użyciu portalu Azure do zarządzania Centrum IoT][lnk-portal]</span><span class="sxs-lookup"><span data-stu-id="40ead-139">[Using the Azure portal to manage IoT Hub][lnk-portal]</span></span>

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
