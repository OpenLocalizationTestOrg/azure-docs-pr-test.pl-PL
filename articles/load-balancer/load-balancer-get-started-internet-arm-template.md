---
title: "Tworzenie modułu równoważenia obciążenia dostępnego z Internetu — szablon platformy Azure | Microsoft Docs"
description: "Dowiedz się, jak utworzyć dostępny z Internetu moduł równoważenia obciążenia w usłudze Resource Manager za pomocą szablonu"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: b24f4729-4559-4458-8527-71009d242647
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: d829000e63515814b192f3f8256e3b8637bb3a34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="creating-an-internet-facing-load-balancer-using-a-template"></a><span data-ttu-id="30fb1-103">Tworzenie modułu równoważenia obciążenia dostępnego z Internetu za pomocą szablonu</span><span class="sxs-lookup"><span data-stu-id="30fb1-103">Creating an Internet facing load balancer using a template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="30fb1-104">Portal</span><span class="sxs-lookup"><span data-stu-id="30fb1-104">Portal</span></span>](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [<span data-ttu-id="30fb1-105">Program PowerShell</span><span class="sxs-lookup"><span data-stu-id="30fb1-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [<span data-ttu-id="30fb1-106">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="30fb1-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [<span data-ttu-id="30fb1-107">Szablon</span><span class="sxs-lookup"><span data-stu-id="30fb1-107">Template</span></span>](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="30fb1-108">W tym artykule opisano model wdrażania usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="30fb1-108">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="30fb1-109">Możesz też zapoznać się z artykułem na temat [tworzenia modułu równoważenia obciążenia dostępnego z Internetu w klasycznym modelu wdrażania](load-balancer-get-started-internet-classic-portal.md).</span><span class="sxs-lookup"><span data-stu-id="30fb1-109">You can also [Learn how to create an Internet facing load balancer using classic deployment model](load-balancer-get-started-internet-classic-portal.md)</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploy-the-template-by-using-click-to-deploy"></a><span data-ttu-id="30fb1-110">Wdrażanie szablonu przy użyciu metody „kliknij, aby wdrożyć”</span><span class="sxs-lookup"><span data-stu-id="30fb1-110">Deploy the template by using click to deploy</span></span>

<span data-ttu-id="30fb1-111">Przykładowy szablon dostępny w repozytorium publicznym korzysta z pliku parametrów zawierającego wartości domyślne używane do generowania scenariusza opisanego powyżej.</span><span class="sxs-lookup"><span data-stu-id="30fb1-111">The sample template available in the public repository uses a parameter file containing the default values used to generate the scenario described above.</span></span> <span data-ttu-id="30fb1-112">Aby wdrożyć ten szablon przy użyciu metody „kliknij, aby wdrożyć”, kliknij [ten link](http://go.microsoft.com/fwlink/?LinkId=544801), kliknij przycisk **Deploy to Azure** (Wdróż na platformie Azure), w razie potrzeby zastąp wartości domyślne parametrów i postępuj zgodnie z instrukcjami podanymi w portalu.</span><span class="sxs-lookup"><span data-stu-id="30fb1-112">To deploy this template using click to deploy, follow [this link](http://go.microsoft.com/fwlink/?LinkId=544801), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>

## <a name="deploy-the-template-by-using-powershell"></a><span data-ttu-id="30fb1-113">Wdrażanie szablonu przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="30fb1-113">Deploy the template by using PowerShell</span></span>

<span data-ttu-id="30fb1-114">Aby wdrożyć pobrany szablon przy użyciu programu PowerShell, wykonaj poniższe kroki.</span><span class="sxs-lookup"><span data-stu-id="30fb1-114">To deploy the template you downloaded by using PowerShell, follow the steps below.</span></span>

1. <span data-ttu-id="30fb1-115">Jeśli nie znasz programu Azure PowerShell, zapoznaj się z artykułem [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) i postępuj zgodnie z instrukcjami aż do momentu logowania się w programie Azure i wyboru subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="30fb1-115">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azure/overview) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="30fb1-116">Uruchom polecenie cmdlet **New AzureRmResourceGroupDeployment**, aby utworzyć grupę zasobów za pomocą szablonu.</span><span class="sxs-lookup"><span data-stu-id="30fb1-116">Run the **New-AzureRmResourceGroupDeployment** cmdlet to create a resource group using the template.</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestRG -Location uswest `
        -TemplateFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' `
        -TemplateParameterFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.parameters.json'
    ```

## <a name="deploy-the-template-by-using-the-azure-cli"></a><span data-ttu-id="30fb1-117">Wdrażanie szablonu przy użyciu interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="30fb1-117">Deploy the template by using the Azure CLI</span></span>

<span data-ttu-id="30fb1-118">Aby wdrożyć szablon przy użyciu interfejsu wiersza polecenia platformy Azure, wykonaj poniższe kroki.</span><span class="sxs-lookup"><span data-stu-id="30fb1-118">To deploy the template by using the Azure CLI, follow the steps below.</span></span>

1. <span data-ttu-id="30fb1-119">Jeśli po raz pierwszy używasz interfejsu wiersza polecenia Azure, zobacz artykuł [Instalowanie i konfigurowania interfejsu wiersza polecenia Azure](../cli-install-nodejs.md) i postępuj zgodnie z instrukcjami aż do punktu, w którym należy wybrać konto platformy Azure i subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="30fb1-119">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="30fb1-120">Uruchom polecenie **azure config mode**, aby włączyć tryb Resource Manager, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="30fb1-120">Run the **azure config mode** command to switch to Resource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="30fb1-121">Oto oczekiwane dane wyjściowe po wprowadzeniu powyższego polecenia:</span><span class="sxs-lookup"><span data-stu-id="30fb1-121">Here is the expected output for the command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="30fb1-122">Przejdź w przeglądarce do [szablonów szybkiego startu](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-lbrules), skopiuj zawartość pliku json i wklej ją do nowego pliku na komputerze.</span><span class="sxs-lookup"><span data-stu-id="30fb1-122">From your browser, navigate to [the Quickstart Template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-lbrules), copy the contents of the json file and paste into a new file in your computer.</span></span> <span data-ttu-id="30fb1-123">Na potrzeby tego scenariusza należy skopiować poniższe wartości do pliku **c:\lb\azuredeploy.parameters.json**.</span><span class="sxs-lookup"><span data-stu-id="30fb1-123">For this scenario, you would be copying the values below to a file named **c:\lb\azuredeploy.parameters.json**.</span></span>
4. <span data-ttu-id="30fb1-124">Uruchom polecenie cmdlet **azure group deployment create**, aby wdrożyć nowy moduł równoważenia obciążenia przy użyciu uprzednio pobranych i zmodyfikowanych plików szablonu oraz parametrów.</span><span class="sxs-lookup"><span data-stu-id="30fb1-124">Run the **azure group deployment create** cmdlet to deploy the new load balancer by using the template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="30fb1-125">Lista wyświetlana po danych wyjściowych zawiera opis używanych parametrów.</span><span class="sxs-lookup"><span data-stu-id="30fb1-125">The list shown after the output explains the parameters used.</span></span>

    ```azurecli
    azure group create --name TestRG --location westus --template-file 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' --parameters-file 'c:\lb\azuredeploy.parameters.json'
    ```

## <a name="next-steps"></a><span data-ttu-id="30fb1-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="30fb1-126">Next steps</span></span>

<span data-ttu-id="30fb1-127">[Get started configuring an internal load balancer](load-balancer-get-started-ilb-arm-ps.md) (Wprowadzenie do konfigurowania wewnętrznego modułu równoważenia obciążenia)</span><span class="sxs-lookup"><span data-stu-id="30fb1-127">[Get started configuring an internal load balancer](load-balancer-get-started-ilb-arm-ps.md)</span></span>

<span data-ttu-id="30fb1-128">[Configure a load balancer distribution mode](load-balancer-distribution-mode.md) (Konfigurowanie trybu dystrybucji modułu równoważenia obciążenia)</span><span class="sxs-lookup"><span data-stu-id="30fb1-128">[Configure a load balancer distribution mode](load-balancer-distribution-mode.md)</span></span>

<span data-ttu-id="30fb1-129">[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md) (Konfigurowanie ustawień limitu czasu bezczynności protokołu TCP dla modułu równoważenia obciążenia)</span><span class="sxs-lookup"><span data-stu-id="30fb1-129">[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md)</span></span>
