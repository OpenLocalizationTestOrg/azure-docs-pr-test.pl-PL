---
title: "aaaCreate wewnętrznego modułu równoważenia obciążenia - szablonu Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak usługa równoważenia przy użyciu szablonu w Menedżerze zasobów obciążenia toocreate jako wewnętrzne"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 64150862-6ced-42de-85dc-89d323257d7c
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 3ffa8178b863367cd79e2bc2b7ce4e45b23267e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-using-a-template"></a><span data-ttu-id="089ae-103">Tworzenie wewnętrznego modułu równoważenia obciążenia przy użyciu szablonu</span><span class="sxs-lookup"><span data-stu-id="089ae-103">Create an internal load balancer using a template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="089ae-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="089ae-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="089ae-105">Program PowerShell</span><span class="sxs-lookup"><span data-stu-id="089ae-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="089ae-106">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="089ae-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="089ae-107">Szablon</span><span class="sxs-lookup"><span data-stu-id="089ae-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="089ae-108">Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="089ae-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="089ae-109">W tym artykule omówiono przy użyciu modelu wdrażania Menedżera zasobów hello, który firma Microsoft zaleca dla większości nowych wdrożeń zamiast hello [klasycznego modelu wdrażania](load-balancer-get-started-ilb-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="089ae-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](load-balancer-get-started-ilb-classic-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-hello-template-by-using-click-toodeploy"></a><span data-ttu-id="089ae-110">Wdrażanie szablonu hello przy użyciu kliknij toodeploy</span><span class="sxs-lookup"><span data-stu-id="089ae-110">Deploy hello template by using click toodeploy</span></span>

<span data-ttu-id="089ae-111">Hello przykładowy szablon dostępne w publicznych repozytorium hello używa parametru plik zawierający hello domyślne wartości używane toogenerate hello scenariusz opisany powyżej.</span><span class="sxs-lookup"><span data-stu-id="089ae-111">hello sample template available in hello public repository uses a parameter file containing hello default values used toogenerate hello scenario described above.</span></span> <span data-ttu-id="089ae-112">toodeploy przy użyciu tego szablonu kliknij toodeploy, postępuj zgodnie z [to łącze](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer), kliknij przycisk **wdrażanie tooAzure**, Zastąp hello domyślne wartości parametrów w razie potrzeby i wykonaj te instrukcje hello hello portalu.</span><span class="sxs-lookup"><span data-stu-id="089ae-112">toodeploy this template using click toodeploy, follow [this link](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

## <a name="deploy-hello-template-by-using-powershell"></a><span data-ttu-id="089ae-113">Wdrażanie szablonu hello przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="089ae-113">Deploy hello template by using PowerShell</span></span>

<span data-ttu-id="089ae-114">toodeploy hello szablon, który został pobrany przy użyciu programu PowerShell, wykonaj poniższe kroki hello.</span><span class="sxs-lookup"><span data-stu-id="089ae-114">toodeploy hello template you downloaded by using PowerShell, follow hello steps below.</span></span>

1. <span data-ttu-id="089ae-115">Jeśli nie znasz programu Azure PowerShell, zobacz [jak tooInstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) i wykonaj instrukcje hello wszystkich toohello sposób hello kończyć toosign na platformie Azure i wyboru subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="089ae-115">If you have never used Azure PowerShell, see [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) and follow hello instructions all hello way toohello end toosign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="089ae-116">Pobierz hello parametry tooyour lokalnego dysku z plikiem.</span><span class="sxs-lookup"><span data-stu-id="089ae-116">Download hello parameters file tooyour local disk.</span></span>
3. <span data-ttu-id="089ae-117">Edytuj plik hello i zapisz go.</span><span class="sxs-lookup"><span data-stu-id="089ae-117">Edit hello file and save it.</span></span>
4. <span data-ttu-id="089ae-118">Uruchom hello **AzureRmResourceGroupDeployment nowy** toocreate polecenia cmdlet, grupy zasobów przy użyciu hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="089ae-118">Run hello **New-AzureRmResourceGroupDeployment** cmdlet toocreate a resource group using hello template.</span></span>

    ```azurecli
    New-AzureRmResourceGroupDeployment -Name TestRG -Location westus `
        -TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json' `
        -TemplateParameterFile 'C:\temp\azuredeploy.parameters.json'
    ```

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a><span data-ttu-id="089ae-119">Wdrażanie szablonu hello przy użyciu hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="089ae-119">Deploy hello template by using hello Azure CLI</span></span>

<span data-ttu-id="089ae-120">Szablon hello toodeploy za pomocą hello wiersza polecenia platformy Azure, wykonaj kroki hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="089ae-120">toodeploy hello template by using hello Azure CLI, follow hello steps below.</span></span>

1. <span data-ttu-id="089ae-121">Jeśli po raz pierwszy używasz interfejsu wiersza polecenia Azure, zobacz [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](../cli-install-nodejs.md) i wykonaj instrukcje hello zapasowej punktu toohello, gdzie należy wybrać konto platformy Azure i subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="089ae-121">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="089ae-122">Uruchom hello **trybie azure config** tooswitch tooResource menedżera trybu poleceń, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="089ae-122">Run hello **azure config mode** command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="089ae-123">Oto hello oczekiwane dane wyjściowe polecenia hello powyżej:</span><span class="sxs-lookup"><span data-stu-id="089ae-123">Here is hello expected output for hello command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="089ae-124">Otwórz plik parametrów hello, zaznacz zawartością i zapisz go tooa plik na swoim komputerze.</span><span class="sxs-lookup"><span data-stu-id="089ae-124">Open hello parameter file, select its contents, and save it tooa file in your computer.</span></span> <span data-ttu-id="089ae-125">Na przykład zapisaliśmy hello pliku parametrów, za*parameters.JSON następującym kodem*.</span><span class="sxs-lookup"><span data-stu-id="089ae-125">For this example, we saved hello parameters file too*parameters.json*.</span></span>
4. <span data-ttu-id="089ae-126">Uruchom hello **tworzenia wdrożenia grupy azure** polecenia toodeploy hello nowego wewnętrznego modułu równoważenia obciążenia przy użyciu szablonu hello i parametr pliki uprzednio pobranego i zmodyfikowanego.</span><span class="sxs-lookup"><span data-stu-id="089ae-126">Run hello **azure group deployment create** command toodeploy hello new internal load balancer by using hello template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="089ae-127">Lista Hello wyświetlana po danych wyjściowych hello wyjaśniono hello parametry używane.</span><span class="sxs-lookup"><span data-stu-id="089ae-127">hello list shown after hello output explains hello parameters used.</span></span>

    ```azurecli
    azure group create --name TestRG --location westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json --parameters-file parameters.json
    ```

## <a name="next-steps"></a><span data-ttu-id="089ae-128">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="089ae-128">Next steps</span></span>

<span data-ttu-id="089ae-129">[Configure a load balancer distribution mode using source IP affinity](load-balancer-distribution-mode.md) (Konfigurowanie trybu dystrybucji modułu równoważenia obciążenia przy użyciu koligacji źródłowych adresów IP)</span><span class="sxs-lookup"><span data-stu-id="089ae-129">[Configure a load balancer distribution mode using source IP affinity](load-balancer-distribution-mode.md)</span></span>

<span data-ttu-id="089ae-130">[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md) (Konfigurowanie ustawień limitu czasu bezczynności protokołu TCP dla modułu równoważenia obciążenia)</span><span class="sxs-lookup"><span data-stu-id="089ae-130">[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md)</span></span>

