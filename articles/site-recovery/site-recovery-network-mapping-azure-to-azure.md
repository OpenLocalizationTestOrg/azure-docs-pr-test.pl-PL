---
title: "Mapowanie aaaNetwork między dwóch regionach platformy Azure w usłudze Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Usługa Azure Site Recovery koordynuje hello replikacji, trybu failover i odzyskiwania maszyn wirtualnych i serwerów fizycznych. Więcej informacji na temat trybu failover tooAzure lub dodatkowego centrum danych."
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: pratshar
ms.openlocfilehash: 4f80c44e3f94eaf446bc01a7041d91fe34aa78d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="network-mapping-between-two-azure-regions"></a>Mapowanie sieci między dwóch regionach platformy Azure


W tym artykule opisano sposób toomap Azure sieci wirtualnych dwóch regionów systemu Azure wraz ze sobą. Mapowanie sieci zapewnia, że po utworzeniu maszyny wirtualnej zreplikowanej w celu hello region platformy Azure jest tworzona na powitania sieci wirtualnej jest toovirtual mapowanej sieci hello źródłowej maszyny wirtualnej.  

## <a name="prerequisites"></a>Wymagania wstępne
Przed zamapowaniem sieci upewnij się, utworzono [sieci wirtualnych platformy Azure](../virtual-network/virtual-networks-overview.md) zarówno źródłowych i docelowych regiony platformy Azure.

## <a name="map-networks"></a>Mapowanie sieci

toomap sieci wirtualnej platformy Azure w sieci wirtualnej tooanother jeden region platformy Azure w innym regionie, przejdź tooSite infrastruktura Recovery -> Mapowanie sieci (maszyn wirtualnych platformy Azure) i Utwórz mapowania sieci.

![Mapowanie sieci](./media/site-recovery-network-mapping-azure-to-azure/network-mapping1.png)


W hello w poniższym przykładzie Moja maszyna wirtualna jest uruchomiona w regionie Azja Wschodnia, a także są replikowane tooSoutheast Azja.

Wybierz sieć źródłowa i docelowa hello, a następnie kliknij przycisk OK toocreate mapowanie sieci tooSoutheast Azja Wschodnia, Azja.

![Mapowanie sieci](./media/site-recovery-network-mapping-azure-to-azure/network-mapping2.png)


Witaj sam element toocreate mapowanie sieci tooEast Azja południowo-wschodnia, Azja.  
![Mapowanie sieci](./media/site-recovery-network-mapping-azure-to-azure/network-mapping3.png)


## <a name="mapping-network-when-enabling-replication"></a>Mapowanie sieci, podczas włączania replikacji

Jeśli nie zostanie zrobione mapowanie sieci, podczas replikowania maszyny wirtualnej do hello pierwszego czasu formularza jeden region platformy Azure tooanother, możesz zdecydować, Sieć docelowa hello w ramach tego samego procesu. Usługa Site Recovery tworzy mapowania sieci z tootarget regionu źródłowego i docelowego regionu toosource na podstawie tego zaznaczenia.   

![Mapowanie sieci](./media/site-recovery-network-mapping-azure-to-azure/network-mapping4.png)

Domyślnie usługi Site Recovery tworzy sieć w regionie docelowym hello, który jest identyczne toohello źródłowej sieci i dodając "— Funkcja automatycznego odzyskiwania systemu" jako nazwę toohello sufiks hello źródła sieci. Możesz wybrać utworzone sieci, klikając przycisk Dostosuj.

![Mapowanie sieci](./media/site-recovery-network-mapping-azure-to-azure/network-mapping5.png)


Jeśli mapowanie sieci hello zostało już przeprowadzone, nie można zmienić sieci wirtualnej hello docelowego podczas włączania replikacji. toochange, zmodyfikuj istniejące mapowanie sieci.  

![Mapowanie sieci](./media/site-recovery-network-mapping-azure-to-azure/network-mapping6.png)

![Mapowanie sieci](./media/site-recovery-network-mapping-azure-to-azure/modify-network-mapping.png)

> [!IMPORTANT]
> Jeśli zmodyfikujesz mapowanie sieci z regionu 1 tooregion-2, upewnij się, że zmodyfikować mapowania sieci powitania od regionu 2 tooregion-1 również.
>
>


## <a name="subnet-selection"></a>Wybór podsieci
Podsieci hello docelowej maszyny wirtualnej jest zaznaczone, na podstawie nazwy hello podsieci hello hello źródłowej maszyny wirtualnej. Jeśli podsieć hello takie same nazwy co hello źródłowej maszyny wirtualnej dostępne w sieci docelowej hello, który jest wybrany dla hello docelowej maszyny wirtualnej, a następnie. Jeśli podsieć o hello sam nazw w sieci docelowej hello, następnie alfabetycznie pierwszej podsieci jest wybrana jako hello docelowej podsieci. Można zmodyfikować tej podsieci, przechodząc tooCompute i ustawień sieci maszyny wirtualnej hello.

![Modyfikowanie podsieci](./media/site-recovery-network-mapping-azure-to-azure/modify-subnet.png)


## <a name="ip-address"></a>Adres IP

Adres IP dla każdego interfejsu sieci hello hello docelowej maszyny wirtualnej jest wybierany w następujący sposób:

### <a name="dhcp"></a>DHCP
Jeśli interfejs sieciowy hello hello źródłowej maszyny wirtualnej jest używany serwer DHCP, interfejs sieciowy hello docelowej maszyny wirtualnej jest również ustawić jako DHCP.

### <a name="static-ip"></a>Statyczny adres IP
Interfejs sieciowy hello hello źródłowej maszyny wirtualnej używa statycznego adresu IP, następnie interfejsu sieci docelowej maszyny wirtualnej hello jest również ustawić toouse statycznego adresu IP. Statyczny adres IP jest wybierany w następujący sposób:

#### <a name="same-address-space"></a>Tą samą przestrzenią adresów

Jeśli podsieć źródła hello i hello docelowej podsieci hello sam przestrzeni adresów, docelowy adres IP jest ustawić taki sam jak hello IP interfejsu sieci hello hello źródłowej maszyny wirtualnej. Jeśli nie ma tego samego adresu IP, dostępne IP jest ustawiony jako hello docelowy adres IP.

#### <a name="different-address-space"></a>Przestrzeń adresowa różnych

Jeśli podsieć źródła hello i hello docelowej podsieci ma inny adres miejsca, docelowy adres IP jest ustawiony jako dostępny adres IP w podsieci docelowej hello.

Można zmodyfikować hello docelowy adres IP dla każdego interfejsu sieciowego, przechodząc tooCompute i ustawień sieci maszyny wirtualnej hello.

## <a name="next-steps"></a>Następne kroki

- Dowiedz się więcej o [wskazówki dotyczące replikowanie maszyn wirtualnych platformy Azure networking](site-recovery-azure-to-azure-networking-guidance.md).
