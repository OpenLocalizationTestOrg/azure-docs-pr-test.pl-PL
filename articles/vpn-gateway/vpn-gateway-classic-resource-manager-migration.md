---
title: "tooResource klasycznego bramy aaaVPN Menedżera migracji | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera omówienie tooResource klasycznego bramy sieci VPN hello Menedżera migracji."
documentationcenter: na
services: vpn-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: caa8eb19-825a-4031-8b49-18fbf3ebc04e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/02/2017
ms.author: amsriva
ms.openlocfilehash: c1d84bf5315224c5c8faac53d7957b496ed205ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="vpn-gateway-classic-tooresource-manager-migration"></a>TooResource klasycznego bramy sieci VPN Menedżera migracji
Teraz można migrować z modelu wdrażania Menedżera tooResource klasycznego bramy sieci VPN. Możesz przeczytać więcej na temat usługi Azure Resource Manager [funkcje i korzyści](../azure-resource-manager/resource-group-overview.md). W tym artykule szczegółowo firma Microsoft, jak toomigrate z toonewer w przypadku wdrożeń klasycznych Menedżera zasobów na podstawie modelu. 

Bramy sieci VPN są migrowane w ramach migracji sieci wirtualnej z klasycznym tooResource Manager. Ta migracja zostanie zakończona jednej sieci wirtualnej w czasie. Nie jest wymagane dodatkowe pod względem toomigration narzędzia lub wymagania wstępne. Kroki migracji są identyczne tooexisting migracji sieci wirtualnej i są udokumentowane w [strona migracji zasobów IaaS](../virtual-machines/windows/migration-classic-resource-manager-ps.md). Podczas migracji jest bez przestojów ścieżki danych i w związku z tym istniejących obciążeń będzie nadal toofunction bez utraty połączenia lokalnego podczas migracji. Witaj publiczny adres IP skojarzone z bramą sieci VPN hello nie ulega zmianie podczas procesu migracji hello. Oznacza to, że nie będzie konieczne tooreconfigure routera lokalnego po ukończeniu migracji hello.  

model Hello w Menedżerze zasobów różni się od klasycznego modelu i składa się z bramy sieci wirtualnej, bramy sieci lokalnej i połączenia zasobów. Te reprezentują hello VPN bramy, hello reprezentujących na przestrzeń adresową lokalnych i łączność między hello dwa odpowiednio lokacji lokalnej. Po ukończeniu migracji nie jest dostępny w modelu klasycznego bramy sieci, a wszystkie operacje zarządzania dla bramy sieci wirtualnej, bramy sieci lokalnej i połączenia obiektów odbywa się przy użyciu modelu Resource Manager.

## <a name="supported-scenarios"></a>Obsługiwane scenariusze
Najbardziej typowych scenariuszy połączenia sieci VPN są objęte klasycznego tooResource Menedżera migracji. scenariusze obsługiwane Hello-

* Toosite punktu połączenia
* Lokalizacji lokalnej tooon połączone lokacji toosite łączności z bramą sieci VPN
* Sieć wirtualna tooVNet łączności między dwiema sieciami wirtualnymi przy użyciu bramy sieci VPN
* Wiele sieci wirtualnych połączone toosame w lokalizacji lokalnej
* Połączenie z wieloma lokacjami
* Wymuszanie tunelowania włączone sieci wirtualnych

Dostępne są następujące scenariusze, które nie są obsługiwane —  

* Sieć wirtualna zarówno bramę usługi ExpressRoute, jak i bramy sieci VPN nie jest obecnie obsługiwane.
* Przesyłania scenariuszy, w którym rozszerzeń maszyny Wirtualnej są połączone tooon lokalnych serwerów. Ograniczenia połączenia sieci VPN przesyłania są szczegółowo opisane poniżej.

> [!NOTE]
> Sprawdzanie poprawności CIDR w modelu usługi Resource Manager jest ściślejsze niż hello jedną w klasycznym modelu. Przed przeprowadzeniem migracji upewnij się, zakresy adresów klasycznego podane zgodność formacie CIDR toovalid przed rozpoczęciem powitalne migracji. CIDR mogą być sprawdzone za pomocą wszystkie typowe moduły CIDR. Sieć wirtualna lub lokalnych witryn na nieprawidłowe zakresy CIDR podczas migracji spowoduje awarię.
> 
> 

## <a name="vnet-toovnet-connectivity-migration"></a>Migracja łączności tooVNet sieci wirtualnej
Osiągnięto łączności tooVNet sieć wirtualną w klasycznym przez utworzenie lokacji lokalnej reprezentację hello połączone sieci wirtualnej. Klienci byli toocreate wymagane dwie lokacje lokalne reprezentujących Witaj dwie sieci wirtualne, które potrzebne toobe połączonych ze sobą. Zostały one następnie połączonych toohello odpowiadającego przy użyciu połączenia tooestablish tunelu IPsec między sieciami wirtualnymi Witaj dwie sieci wirtualne. Ten model ma wyzwania możliwości zarządzania, ponieważ zmiany zakresu adresów w jednej sieci wirtualnej również muszą zostać zachowane w odpowiedniej reprezentacji lokacji lokalnej hello. W modelu usługi Resource Manager to rozwiązanie nie jest już potrzebne. Witaj połączenie między powitalne dwie sieci wirtualne bezpośrednio uzyskuje się za pomocą typu połączenia 'Vnet2Vnet' w zasobie połączenia. 

![Zrzut ekranu sieci wirtualnej tooVNet migracji.](./media/vpn-gateway-migration/migration1.png)

Podczas migracji sieci wirtualnej, które firma Microsoft wykrywać który hello połączonych jednostki toocurrent sieci wirtualnej bramy sieci VPN jest innej sieci wirtualnej i upewnij się, że po zakończeniu migracji sieci zarówno wirtualnych, nie zobaczysz dwie lokacje lokalne powitania reprezentujący innych sieci wirtualnej. Witaj modelu klasycznego bramy sieci VPN, dwie lokacje lokalne i dwa połączenia między nimi jest przekształcone tooResource modelu Manager za pomocą dwóch bram sieci VPN i dwa połączenia typu Vnet2Vnet.

## <a name="transit-vpn-connectivity"></a>Połączenie z siecią VPN przesyłania
Tak, aby łączność z lokalnymi dla sieci wirtualnej jest to osiągane przez połączenie sieci wirtualnej, która jest bezpośrednio połączone lokalne tooon tooanother, można skonfigurować bramy sieci VPN w topologii. To jest przesyłania łączność w sieci VPN, w których wystąpień w pierwszej sieci wirtualnej są połączone lokalne tooon zasobów za pośrednictwem bramy sieci VPN toohello przesyłania w połączonych sieci wirtualnej, która jest bezpośrednio połączone lokalne tooon. tooachieve tej konfiguracji w klasycznym modelu wdrażania będzie potrzebny toocreate lokalnej lokacji, który ma zagregowane prefiksy reprezentujący zarówno hello połączone sieci wirtualnej i lokalnej przestrzenią adresów. Ta representational lokacji lokalnej jest toohello połączonych sieci wirtualnej tooachieve przesyłania łączności. Klasycznego modelu ma również podobne wyzwania możliwości zarządzania, ponieważ każda zmiana zakresu adresów lokalnych również muszą zostać zachowane w witrynie lokalne powitania reprezentujący agregacji hello sieci wirtualnej i lokalnej. Wprowadzenie obsługi protokołu BGP w bram Resource Manager obsługiwane upraszcza możliwości zarządzania, ponieważ hello połączonych bram można znaleźć trasy z lokalnie bez tooprefixes ręcznej modyfikacji.

![Zrzut ekranu przedstawiający Scenariusz routingu tranzytowego.](./media/vpn-gateway-migration/migration2.png)

Ponieważ firma Microsoft przekształcić łączności tooVNet sieci wirtualnej bez konieczności lokalnych witryn, scenariusz przesyłania hello utraci łączność lokalnej dla sieci wirtualnej jest pośrednio połączenia lokalnego tooon. Witaj utraty połączenia można zminimalizować w hello następujące dwa sposoby, po zakończeniu migracji - 

* Należy włączyć protokół BGP dla bramy sieci VPN, które są połączone ze sobą i tooon lokalnego. Włączanie protokołu BGP przywraca łączności bez zmiany konfiguracji, ponieważ trasy są rozpoznawane i anonsowane między bramy sieci wirtualnej. Należy pamiętać, że BGP opcja jest dostępna tylko na standardowych i nowsze wersje produktu.
* Ustanowić połączenie jawne z odpowiednim bramy sieci wirtualnej toohello sieci lokalnej, reprezentujący lokalizacji lokalnej. Spowoduje to również wymagają zmiany konfiguracji na powitania lokalnego routera toocreate i skonfiguruj hello tunelu IPsec.

## <a name="next-steps"></a>Następne kroki
Po szkoleniowe dotyczące obsługi migracji bramy sieci VPN, przejdź zbyt[obsługiwane platformy migracji zasobów IaaS z klasycznym tooResource Menedżera](../virtual-machines/windows/migration-classic-resource-manager-ps.md) tooget uruchomiona.

