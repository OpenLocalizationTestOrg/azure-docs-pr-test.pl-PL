---
title: "aaaCreate regułę modułu równoważenia obciążenia Azure dla klastra"
description: "Skonfiguruj porty tooopen modułu równoważenia obciążenia Azure dla klastra usługi sieć szkieletowa usług Azure."
services: service-fabric
documentationcenter: na
author: thraka
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/22/2017
ms.author: adegeo
ms.openlocfilehash: 4a40f62422bd895d782be8cbaace5f4e1af81db3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="open-ports-for-a-service-fabric-cluster"></a>Otwieranie portów dla klastra sieci szkieletowej usług

usługi równoważenia obciążenia Hello wdrożone z klastrem usługi sieć szkieletowa usług Azure kieruje ruch tooyour aplikacji uruchomionej na węźle. Jeśli zmienisz toouse Twojej aplikacji innego portu, musi ujawniać tego portu (lub trasy innego portu) w hello modułu równoważenia obciążenia Azure.

Po wdrożeniu sieci tooAzure klastra sieci szkieletowej usług równoważenia obciążenia został utworzony automatycznie. Jeśli nie masz usługi równoważenia obciążenia, zobacz [skonfigurowania funkcji równoważenia obciążenia internetowy](..\load-balancer\load-balancer-get-started-internet-portal.md).

## <a name="configure-service-fabric"></a>Konfigurowanie sieci szkieletowej usług

Aplikacja usługi Service Fabric **ServiceManifest.xml** hello punkty końcowe aplikacji oczekuje toouse definiuje pliku konfiguracji. Po hello config plik został zaktualizowany toodefine punktu końcowego, hello modułu równoważenia obciążenia musi być zaktualizowany tooexpose tego (lub innej) portu. Aby uzyskać więcej informacji dotyczących sposobu toocreate hello punkt końcowy usługi sieci szkieletowej, zobacz [Konfiguracja punktu końcowego](service-fabric-service-manifest-resources.md).

## <a name="create-a-load-balancer-rule"></a>Tworzenie reguły modułu równoważenia obciążenia

Reguły modułu równoważenia obciążenia otwiera port połączonych z Internetem i przekazuje ruch toohello wewnętrznego węzła port używany przez aplikację. Jeśli nie masz usługi równoważenia obciążenia, zobacz [skonfigurowania funkcji równoważenia obciążenia internetowy](..\load-balancer\load-balancer-get-started-internet-portal.md).

toocreate reguły modułu równoważenia obciążenia, należy hello toocollect następujących informacji:

- Nazwa modułu równoważenia obciążenia.
- Grupa zasobów hello obciążenia równoważenia i klastra sieci szkieletowej usług.
- Portu zewnętrznego.
- Port wewnętrzny.

## <a name="azure-cli"></a>Interfejs wiersza polecenia platformy Azure
>[!NOTE]
>Nazwa hello toodetermine hello usługi równoważenia obciążenia, należy użyć tego polecenia get tooquickly listę wszystkich usług równoważenia obciążenia i hello skojarzonych grup zasobów.
>
>`az network lb list --query "[].{ResourceGroup: resourceGroup, Name: name}"`
>

Potrwa to tylko toocreate jednego polecenia reguły modułu równoważenia obciążenia z hello **interfejsu wiersza polecenia Azure**. Wystarczy tooknow zarówno nazwę hello hello obciążenia równoważenia i zasobów grupy toocreate nową regułę.

```azurecli
az network lb rule create --backend-port 40000 --frontend-port 39999 --protocol Tcp --lb-name LB-svcfab3 -g svcfab_cli -n my-app-rule
```

Witaj polecenia interfejsu wiersza polecenia Azure ma kilka parametrów, które zostały opisane w poniższej tabeli hello:

| Parametr | Opis |
| --------- | ----------- |
| `--backend-port`  | nasłuchuje aplikacja Hello portu hello usługi sieci szkieletowej. |
| `--frontend-port` | Witaj Witaj portu załadować ujawnia równoważenia dla połączeń zewnętrznych. |
| `-lb-name` | Nazwa Hello hello załadować toochange równoważenia. |
| `-g`       | Grupa zasobów Hello ma hello modułu równoważenia obciążenia oraz klastra sieci szkieletowej usług. |
| `-n`       | Wybrana nazwa reguły hello Hello. |


>[!NOTE]
>Aby uzyskać więcej informacji na temat toocreate modułu równoważenia obciążenia z hello wiersza polecenia platformy Azure, zobacz temat [Utwórz usługę równoważenia obciążenia z hello Azure CLI](..\load-balancer\load-balancer-get-started-internet-arm-cli.md).

## <a name="powershell"></a>PowerShell

>[!NOTE]
>Nazwa hello toodetermine hello usługi równoważenia obciążenia, należy użyć tego polecenia get tooquickly listę wszystkich usług równoważenia obciążenia i grup zasobów.
>
>`Get-AzureRmLoadBalancer | Select Name, ResourceGroupName`

PowerShell jest nieco bardziej skomplikowane niż hello wiersza polecenia platformy Azure. Koncepcyjnie wykonaj następujące kroki toocreate hello reguły.

1. Pobierz hello modułu równoważenia obciążenia z platformy Azure.
2. Utwórz regułę.
3. Dodaj hello reguły toohello — moduł równoważenia obciążenia.
4. Zaktualizuj hello modułu równoważenia obciążenia.

```powershell
# Get hello load balancer
$lb = Get-AzureRmLoadBalancer -Name LB-svcfab3 -ResourceGroupName svcfab_cli

# Create hello rule based on information from hello load balancer.
$lbrule = New-AzureRmLoadBalancerRuleConfig -Name my-app-rule7 -Protocol Tcp -FrontendPort 39990 -BackendPort 40009 `
                                            -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
                                            -BackendAddressPool  $lb.BackendAddressPools[0] `
                                            -Probe $lb.Probes[0]

# Add hello rule toohello load balancer
$lb.LoadBalancingRules.Add($lbrule)

# Update hello load balancer on Azure
$lb | Set-AzureRmLoadBalancer
```

Dotyczące hello `New-AzureRmLoadBalancerRuleConfig` polecenia hello `-FrontendPort` udostępnia usługi równoważenia obciążenia hello reprezentuje hello port dla połączeń zewnętrznych i hello `-BackendPort` nasłuchuje reprezentuje hello portu hello usługi sieć szkieletowa aplikacji.

>[!NOTE]
>Aby uzyskać więcej informacji na toocreate modułu równoważenia obciążenia przy użyciu programu PowerShell, zobacz temat [tworzenia modułu równoważenia obciążenia przy użyciu programu PowerShell](..\load-balancer\load-balancer-get-started-internet-arm-ps.md).

