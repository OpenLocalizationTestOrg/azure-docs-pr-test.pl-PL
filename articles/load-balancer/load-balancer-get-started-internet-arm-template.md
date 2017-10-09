---
title: "równoważenia obciążenia aaaCreate internetowy - szablonu Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate Internetem obciążenia w Menedżerze zasobów przy użyciu szablonu usługi równoważenia"
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
ms.openlocfilehash: 2bce8cb87303838f3bc732d51228ab46d8015552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-internet-facing-load-balancer-using-a-template"></a>Tworzenie modułu równoważenia obciążenia dostępnego z Internetu za pomocą szablonu

> [!div class="op_single_selector"]
> * [Portal](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [Program PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [Interfejs wiersza polecenia platformy Azure](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [Szablon](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

W tym artykule omówiono modelu wdrażania usługi Resource Manager hello. Możesz również [Dowiedz się, jak toocreate Internetem obciążenia przy użyciu klasycznego modelu wdrażania usługi równoważenia](load-balancer-get-started-internet-classic-portal.md)

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploy-hello-template-by-using-click-toodeploy"></a>Wdrażanie szablonu hello przy użyciu kliknij toodeploy

Hello przykładowy szablon dostępne w publicznych repozytorium hello używa parametru plik zawierający hello domyślne wartości używane toogenerate hello scenariusz opisany powyżej. toodeploy przy użyciu tego szablonu kliknij toodeploy, postępuj zgodnie z [to łącze](http://go.microsoft.com/fwlink/?LinkId=544801), kliknij przycisk **wdrażanie tooAzure**, Zastąp hello domyślne wartości parametrów w razie potrzeby i wykonaj te instrukcje hello hello portalu.

## <a name="deploy-hello-template-by-using-powershell"></a>Wdrażanie szablonu hello przy użyciu programu PowerShell

toodeploy hello szablon, który został pobrany przy użyciu programu PowerShell, wykonaj poniższe kroki hello.

1. Jeśli nie znasz programu Azure PowerShell, zobacz [jak tooInstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) i wykonaj instrukcje hello wszystkich toohello sposób hello kończyć toosign na platformie Azure i wyboru subskrypcji.
2. Uruchom hello **AzureRmResourceGroupDeployment nowy** toocreate polecenia cmdlet, grupy zasobów przy użyciu hello szablonu.

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestRG -Location uswest `
        -TemplateFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' `
        -TemplateParameterFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.parameters.json'
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

3. W przeglądarce Przejdź zbyt[hello szablon szybkiego startu](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-lbrules), skopiuj zawartość pliku json hello hello i Wklej do nowy plik na swoim komputerze. W tym scenariuszu może kopiować wartości hello poniżej tooa plik o nazwie **c:\lb\azuredeploy.parameters.json**.
4. Uruchom hello **tworzenia wdrożenia grupy azure** polecenia cmdlet toodeploy hello nowego modułu równoważenia obciążenia przy użyciu szablonu hello i parametr pliki uprzednio pobranego i zmodyfikowanego. Lista Hello wyświetlana po danych wyjściowych hello wyjaśniono hello parametry używane.

    ```azurecli
    azure group create --name TestRG --location westus --template-file 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' --parameters-file 'c:\lb\azuredeploy.parameters.json'
    ```

## <a name="next-steps"></a>Następne kroki

[Get started configuring an internal load balancer](load-balancer-get-started-ilb-arm-ps.md) (Wprowadzenie do konfigurowania wewnętrznego modułu równoważenia obciążenia)

[Configure a load balancer distribution mode](load-balancer-distribution-mode.md) (Konfigurowanie trybu dystrybucji modułu równoważenia obciążenia)

[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md) (Konfigurowanie ustawień limitu czasu bezczynności protokołu TCP dla modułu równoważenia obciążenia)
