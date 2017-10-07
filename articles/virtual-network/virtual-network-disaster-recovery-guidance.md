---
title: "toodo aaaWhat w przypadku hello przerw w działaniu usługi Azure wpływających na sieciach wirtualnych platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jakie toodo w przypadku hello przerw w działaniu usługi Azure wpływających na sieciach wirtualnych platformy Azure."
services: virtual-network
documentationcenter: 
author: NarayanAnnamalai
manager: jefco
editor: 
ms.assetid: ad260ab9-d873-43b3-8896-f9a1db9858a5
ms.service: virtual-network
ms.workload: virtual-network
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2016
ms.author: narayan;aglick
ms.openlocfilehash: db022d2a042d255cf8ec6afb68cd8436aeecfe08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-network--business-continuity"></a>Sieć wirtualna — ciągłość prowadzenia działalności biznesowej
## <a name="overview"></a>Omówienie
Sieć wirtualną (VNet) jest logiczną reprezentacja sieci w chmurze hello. Pozwala ona toodefine własne prywatnego adresu IP adres miejsca i segmentów hello sieci na podsieci. Sieci wirtualne służy jako toohost granicy zaufania zasoby obliczeniowe, takich jak maszyny wirtualne platformy Azure i usługi w chmurze (role sieć web/proces roboczy). Sieć wirtualną umożliwia bezpośrednie prywatnej komunikacji IP między zasobami hello znajdujące się w nim. Sieć wirtualną można też tooan połączone sieci lokalnej za pomocą jednego z hello hybrydowego opcje, takie jak brama sieci VPN lub usługi ExpressRoute.

Sieci wirtualnej jest tworzony w zakresie hello regionu. Sieci wirtualne można tworzyć z tą samą przestrzenią adresów w dwóch różnych regionach (tj. nam wschodnie i zachód nam, ale nie można połączyć je tooone innego bezpośrednio). 

## <a name="business-continuity"></a>Ciągłość działania
Może istnieć kilka różnych sposobów, aplikacja może zostać zerwane. Danego regionu można całkowicie odcięte tooa klęski żywiołowej lub częściowe po awarii, ze względu na błąd tooa wiele urządzeń/usług. wpływ Hello na powitania usługi sieci wirtualnej różni się w każdej z tych sytuacji.

**Pytanie: co chcesz zrobić w przypadku awarii tooan całego regionu hello oznacza, że jeśli region jest całkowicie odcięcia powodu klęski żywiołowej tooa? Co się stanie toohello sieci wirtualnych hostowana w regionie hello?**

A: hello wirtualnej sieci i hello zasobów w hello wpływ pozostaje region niedostępne podczas hello hello przerw w działaniu usługi.

![Diagram prostego sieci wirtualnej](./media/virtual-network-disaster-recovery-guidance/vnet.png)

**Pytanie: jakie służy toodo ponownie utworzyć hello tej samej sieci wirtualnej w innym regionie?**

A: sieć wirtualna (VNet) jest stosunkowo lekkie zasobów. Można wywoływać interfejsy API Azure toocreate sieci wirtualnej z hello sam przestrzeni adresów w innym regionie. toore — tworzenie hello region wpływ na tym samym środowisku, które były obecne w hello, masz toore wywołania interfejsu API toomake — wdrażanie usługi w chmurze (role sieć web/proces roboczy) i maszyn wirtualnych, które były. Konieczne będzie również toospin Konfigurowanie bramy sieci VPN i połączyć sieć lokalną tooyour gdyby łączności lokalnie (np. hybrydowej).

znajdują się instrukcje tworzenia sieci wirtualnej Hello [tutaj](virtual-networks-create-vnet-arm-pportal.md). 

**Pytanie: czy replika sieci wirtualnej w danym regionie zostać ponownie utworzone w innym regionie wcześniejsze?**

A. tak, można utworzyć dwie sieci wirtualnych za pomocą hello przestrzeni adresów tego samego prywatnego adresu IP i zasobów w dwóch różnych regionach wyprzedzenia godziny. Jeśli klient został hosting internetowy usług w hello sieci wirtualnej, można mieć — Konfiguracja trasy toogeo Menedżera ruchu ruchu toohello region, który jest aktywny. Jednak klient nie może połączyć dwie sieci wirtualne z hello sam adres sieci lokalnej tootheir miejsca w postaci spowodowałoby routingu problemy. Z hello czasie awarii i utratę sieci wirtualnej w jednym regionie odbiorcy mogą się łączyć hello innych sieci wirtualnej w regionie dostępne hello z sieci lokalnej tootheir miejsca dopasowywania adresów.

znajdują się instrukcje tworzenia sieci wirtualnej Hello [tutaj](virtual-networks-create-vnet-arm-pportal.md).

