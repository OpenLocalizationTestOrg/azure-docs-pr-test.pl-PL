---
title: "Moduł równoważenia - obciążenia aaaCreate internetowy, klasycznym Azure PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak usługa równoważenia w trybie klasycznym przy użyciu programu PowerShell obciążenia toocreate umożliwiających dostęp z Internetu"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 73e8bfa4-8086-4ef0-9e35-9e00b24be319
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 76d9a712a0acda223fc86b80be9c35c0ed9f3a50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-powershell"></a>Wprowadzenie do tworzenia dostępnego z Internetu modułu równoważenia obciążenia (klasycznego) przy użyciu programu PowerShell

> [!div class="op_single_selector"]
> * [Klasyczna witryna Azure Portal](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [Program PowerShell](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [Interfejs wiersza polecenia platformy Azure](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [Azure Cloud Services](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> Przed rozpoczęciem pracy z zasobów platformy Azure, jest ważne toounderstand, że Azure ma obecnie dwa modele wdrażania: usługi Azure Resource Manager i model klasyczny. Przed rozpoczęciem pracy z dowolnym zasobem Azure należy zapoznać się z [modelami i narzędziami wdrażania](../azure-classic-rm.md). Hello dokumentację dotyczącą różnych narzędzi można wyświetlić, klikając karty hello u góry hello tego artykułu. W tym artykule omówiono hello klasycznego modelu wdrażania. Możesz również [Dowiedz się, jak usługa równoważenia przy użyciu usługi Azure Resource Manager obciążenia toocreate Internetem](load-balancer-get-started-internet-arm-ps.md).

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-load-balancer-using-powershell"></a>Konfiguracja modułu równoważenia obciążenia za pomocą programu PowerShell

tooset się moduł równoważenia obciążenia przy użyciu programu powershell, wykonaj poniższe kroki hello:

1. Jeśli nie znasz programu Azure PowerShell, zobacz [jak tooInstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) i wykonaj instrukcje hello wszystkich toohello sposób hello kończyć toosign na platformie Azure i wyboru subskrypcji.
2. Po utworzeniu maszyny wirtualnej, można użyć tooadd poleceń cmdlet programu PowerShell maszyny wirtualnej tooa usługi równoważenia obciążenia w ramach hello sama usługa w chmurze.

W hello następujące przykładowe, należy dodać zestaw usługi równoważenia obciążenia o nazwie "farma sieci Web" toocloud maszyny "mytestcloud" (lub myctestcloud.cloudapp.net), dodając toovirtual usługi równoważenia obciążenia hello hello punktów końcowych usługi o nazwie "web1" i "Web 2". Witaj modułu równoważenia obciążenia odbiera ruch sieciowy na porcie 80 i równoważy obciążenia między maszynami wirtualnymi hello zdefiniowane przez hello lokalnego punktu końcowego (w tym przypadku port 80) za pomocą protokołu TCP.

### <a name="step-1"></a>Krok 1

Tworzenie punktu końcowego ze zrównoważonym obciążeniem na serwerze web1"hello pierwszej maszyny Wirtualnej"

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

### <a name="step-2"></a>Krok 2

Utwórz inny punkt końcowy dla hello drugi maszyny Wirtualnej "sieci Web 2" przy użyciu hello sama nazwa zestawu równoważenia

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web2" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

## <a name="remove-a-virtual-machine-from-a-load-balancer"></a>Usuwanie maszyny wirtualnej z modułu równoważenia obciążenia

Można użyć tooremove AzureEndpoint Usuń punkt końcowy maszyny wirtualnej z hello modułu równoważenia obciążenia

```powershell
Get-azureVM -ServiceName mytestcloud  -Name web1 |Remove-AzureEndpoint -Name httpin | Update-AzureVM
```

## <a name="next-steps"></a>Następne kroki

Możesz też zapoznać się z artykułem na temat [wprowadzenia do tworzenia wewnętrznego modułu równoważenia obciążenia](load-balancer-get-started-ilb-classic-ps.md) i określić typ [trybu dystrybucji](load-balancer-distribution-mode.md) dotyczącego danego ruchu sieciowego modułu równoważenia obciążenia.

Jeśli aplikacja wymaga połączenia tookeep aktywności dla serwerów za modułem równoważenia obciążenia, użytkownik może dowiedzieć się więcej o [ustawienia limitu czasu protokołu TCP dla usługi równoważenia obciążenia w stanie bezczynności](load-balancer-tcp-idle-timeout.md). Aby ułatwić toolearn dotyczących zachowania bezczynności połączenia podczas korzystania z usługi równoważenia obciążenia Azure.
