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
# <a name="create-an-internal-load-balancer-using-a-template"></a>Tworzenie wewnętrznego modułu równoważenia obciążenia przy użyciu szablonu

> [!div class="op_single_selector"]
> * [Azure Portal](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [Program PowerShell](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [Interfejs wiersza polecenia platformy Azure](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [Szablon](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../azure-resource-manager/resource-manager-deployment-model.md).  W tym artykule omówiono przy użyciu modelu wdrażania Menedżera zasobów hello, który firma Microsoft zaleca dla większości nowych wdrożeń zamiast hello [klasycznego modelu wdrażania](load-balancer-get-started-ilb-classic-ps.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-hello-template-by-using-click-toodeploy"></a>Wdrażanie szablonu hello przy użyciu kliknij toodeploy

Hello przykładowy szablon dostępne w publicznych repozytorium hello używa parametru plik zawierający hello domyślne wartości używane toogenerate hello scenariusz opisany powyżej. toodeploy przy użyciu tego szablonu kliknij toodeploy, postępuj zgodnie z [to łącze](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer), kliknij przycisk **wdrażanie tooAzure**, Zastąp hello domyślne wartości parametrów w razie potrzeby i wykonaj te instrukcje hello hello portalu.

## <a name="deploy-hello-template-by-using-powershell"></a>Wdrażanie szablonu hello przy użyciu programu PowerShell

toodeploy hello szablon, który został pobrany przy użyciu programu PowerShell, wykonaj poniższe kroki hello.

1. Jeśli nie znasz programu Azure PowerShell, zobacz [jak tooInstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) i wykonaj instrukcje hello wszystkich toohello sposób hello kończyć toosign na platformie Azure i wyboru subskrypcji.
2. Pobierz hello parametry tooyour lokalnego dysku z plikiem.
3. Edytuj plik hello i zapisz go.
4. Uruchom hello **AzureRmResourceGroupDeployment nowy** toocreate polecenia cmdlet, grupy zasobów przy użyciu hello szablonu.

    ```azurecli
    New-AzureRmResourceGroupDeployment -Name TestRG -Location westus `
        -TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json' `
        -TemplateParameterFile 'C:\temp\azuredeploy.parameters.json'
    ```

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a>Wdrażanie szablonu hello przy użyciu hello wiersza polecenia platformy Azure

Szablon hello toodeploy za pomocą hello wiersza polecenia platformy Azure, wykonaj kroki hello poniżej.

1. Jeśli po raz pierwszy używasz interfejsu wiersza polecenia Azure, zobacz [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](../cli-install-nodejs.md) i wykonaj instrukcje hello zapasowej punktu toohello, gdzie należy wybrać konto platformy Azure i subskrypcji.
2. Uruchom hello **trybie azure config** tooswitch tooResource menedżera trybu poleceń, jak pokazano poniżej.

    ```azurecli
    azure config mode arm
    ```

    Oto hello oczekiwane dane wyjściowe polecenia hello powyżej:

        info:    New mode is arm

3. Otwórz plik parametrów hello, zaznacz zawartością i zapisz go tooa plik na swoim komputerze. Na przykład zapisaliśmy hello pliku parametrów, za*parameters.JSON następującym kodem*.
4. Uruchom hello **tworzenia wdrożenia grupy azure** polecenia toodeploy hello nowego wewnętrznego modułu równoważenia obciążenia przy użyciu szablonu hello i parametr pliki uprzednio pobranego i zmodyfikowanego. Lista Hello wyświetlana po danych wyjściowych hello wyjaśniono hello parametry używane.

    ```azurecli
    azure group create --name TestRG --location westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json --parameters-file parameters.json
    ```

## <a name="next-steps"></a>Następne kroki

[Configure a load balancer distribution mode using source IP affinity](load-balancer-distribution-mode.md) (Konfigurowanie trybu dystrybucji modułu równoważenia obciążenia przy użyciu koligacji źródłowych adresów IP)

[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md) (Konfigurowanie ustawień limitu czasu bezczynności protokołu TCP dla modułu równoważenia obciążenia)

