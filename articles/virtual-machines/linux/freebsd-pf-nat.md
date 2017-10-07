---
title: "aaaUse FreeBSD filtr pakietów toocreate zapory na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toodeploy translatorem adresów Sieciowych zapory przy użyciu jego FreeBSD PF na platformie Azure."
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/20/2017
ms.author: kyliel
ms.openlocfilehash: 3d3a5dde2ca03ba6fc384581c786f5eb746e6d92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-freebsds-packet-filter-toocreate-a-secure-firewall-in-azure"></a>Jak toouse FreeBSD filtr pakietów toocreate bezpiecznego zapory w systemie Azure
W tym artykule przedstawiono sposób toodeploy zapory NAT. przy użyciu filtru pakujący FreeBSD firmy przy użyciu szablonu usługi Azure Resource Manager dla typowego scenariusza serwera sieci web.

## <a name="what-is-pf"></a>Co to jest PF?
PF (filtr pakietów równocześnie zapisywane pf) jest filtr licencjonowane pakietów BSD, centralnej części oprogramowanie zapory. PF ponieważ powstał szybko, a teraz ma kilka zalet w porównaniu z innych dostępnych zapór. Translatora adresów sieciowych (NAT) jest PF od pierwszego dnia, a następnie Harmonogram pakietów i zarządzania active kolejki są integrowane PF, integrowanie hello ALTQ i co można skonfigurować za pomocą PF w konfiguracji. Funkcje, takie jak pfsync i protokołu CARP dla trybu failover i nadmiarowość, authpf dla sesji uwierzytelniania i ftp proxy tooease zapory hello trudne protokołu FTP, również rozszerzony PF. Krótko mówiąc PF jest wydajny i bogate zapory. 

## <a name="get-started"></a>Rozpoczęcie pracy
Jeśli planuje się skonfigurowanie bezpiecznego zapory w chmurze powitania dla serwerów sieci web, Zacznijmy od początku. Można także zastosować hello skryptom używanym w tym tooset szablonu usługi Azure Resource Manager zapasowej topologii sieci.
Skonfiguruj maszynę wirtualną FreeBSD szablonu usługi Azure Resource Manager Hello wykonuje /redirection translatora adresów Sieciowych przy użyciu PF i dwie maszyny wirtualne FreeBSD z serwera sieci web Nginx hello zainstalowana i skonfigurowana. Ponadto tooperforming translatora adresów Sieciowych dla dwóch serwerów sieci web hello wyjściowych ruchu, maszyny wirtualnej NAT/przekierowanie hello przechwytuje żądania HTTP i Przekierowanie toohello dwóch serwerów sieci web w okrężne. Witaj sieci wirtualnej używa hello prywatnej bez obsługi routingu IP adres miejsca 10.0.0.2/24 i można zmodyfikować parametry hello hello szablonu. Szablon usługi Azure Resource Manager Hello definiuje również tabelę tras dla hello całej sieci wirtualnej, która jest kolekcją indywidualnych tras używane trasy domyślne Azure toooverride na podstawie hello docelowego adresu IP. 

![pf_topology](./media/freebsd-pf-nat/pf_topology.jpg)
    
### <a name="deploy-through-azure-cli"></a>Wdrażanie za pośrednictwem interfejsu wiersza polecenia platformy Azure
Najnowsza wersja należy hello [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zarejestrowane za pomocą konta Azure tooan [logowania az](/cli/azure/#login). Utwórz grupę zasobów za pomocą polecenia [az group create](/cli/azure/group#create). Witaj poniższy przykład tworzy nazwę grupy zasobów `myResourceGroup` w hello `West US` lokalizacji.

```azurecli
az group create --name myResourceGroup --location westus
```

Następnie należy wdrożyć szablon hello [pf freebsd Konfiguracja](https://github.com/Azure/azure-quickstart-templates/tree/master/pf-freebsd-setup) z [Utwórz wdrożenie grupy az](/cli/azure/group/deployment#create). Pobierz [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/pf-freebsd-setup/azuredeploy.parameters.json) w obszarze hello tej samej ścieżce i definiować własne wartości zasobów, takich jak `adminPassword`, `networkPrefix`, i `domainNamePrefix`. 

```azurecli
az group deployment create --resource-group myResourceGroup --name myDeploymentName \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/pf-freebsd-setup/azuredeploy.json \
    --parameters '@azuredeploy.parameters.json' --verbose
```

Po około pięciu minut, uzyskasz informacje hello `"provisioningState": "Succeeded"`. Następnie możesz ssh frontonu toohello maszyny Wirtualnej (NAT) lub uzyskać dostępu do serwera sieci web Nginx w przeglądarce, za pomocą hello publicznego adresu IP lub nazwy FQDN usługi frontonu hello maszyny Wirtualnej (NAT). Witaj poniższy przykład zawiera nazwy FQDN i publicznego adresu IP przypisanego toohello frontonu maszyny Wirtualnej (NAT) w hello `myResourceGroup` grupy zasobów. 

```azurecli
az network public-ip list --resource-group myResourceGroup
```
    
## <a name="next-steps"></a>Następne kroki
Czy chcesz tooset własny protokół NAT na platformie Azure? Open Source, bezpłatne, ale wydajne? Następnie PF jest dobrym rozwiązaniem. Za pomocą szablonu hello [pf freebsd Konfiguracja](https://github.com/Azure/azure-quickstart-templates/tree/master/pf-freebsd-setup), wystarczy tooset pięć minut zapory NAT z obciążenia okrężnego równoważenia przy użyciu jego FreeBSD PF Azure typowy scenariusz serwera sieci web. 

Ofercie hello toolearn FreeBSD na platformie Azure, zapoznaj się zbyt[tooFreeBSD wprowadzenie na platformie Azure](freebsd-intro-on-azure.md).

Więcej informacji na temat PF tooknow, zapoznaj się zbyt[Podręcznik FreeBSD](https://www.freebsd.org/doc/handbook/firewalls-pf.html) lub [Podręcznik PF użytkownika](https://www.freebsd.org/doc/handbook/firewalls-pf.html).
