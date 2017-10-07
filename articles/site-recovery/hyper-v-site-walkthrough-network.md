---
title: "sieć w funkcji Hyper-V (bez programu System Center VMM) tooAzure replikacji za pomocą usługi Azure Site Recovery aaaPlan | Dokumentacja firmy Microsoft"
description: W tym artykule opisano planowanie wymagane podczas replikowania maszyn wirtualnych funkcji Hyper-V (bez VMM) tooAzure sieci
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5ca12254-975d-48e8-a84d-422825dac9b2
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: a35de72b53ca921a7b9bfca00a0edcb9416d5aa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-plan-networking-for-hyper-v-tooazure-replication"></a>Krok 4: Planowanie sieci funkcji Hyper-V tooAzure replikacji

Ten artykuł zawiera podsumowanie sieci — kwestie podczas replikowania lokalnych tooAzure maszyn wirtualnych funkcji Hyper-V (bez programu System Center VMM) przy użyciu hello [usługi Azure Site Recovery](site-recovery-overview.md) usługi.

Opublikuj wszelkie komentarze u dołu hello w tym artykule, lub zadać pytania w hello [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="connecting-tooreplica-vms-after-failover"></a>Łączenia tooreplica maszyn wirtualnych po pracy awaryjnej

Podczas planowania strategii trybu failover i replikacji, na których należy jedno z pytań klucza hello jest sposób tooconnect toohello maszyny Wirtualnej Azure po pracy awaryjnej. Istnieje kilka opcji do wyboru podczas projektowania strategii sieci dla repliki maszyny wirtualne platformy Azure:

- **Inny adres IP**: można wybrać toouse różnych zakresów adresów IP dla hello replikowane sieci maszyny Wirtualnej platformy Azure. W tym scenariuszu hello maszyny Wirtualnej pobiera nowego adresu IP po pracy awaryjnej i aktualizacji DNS jest wymagany. [Dowiedz się więcej](site-recovery-test-failover-vmm-to-vmm.md#prepare-the-infrastructure-for-test-failover)
- **Tego samego adresu IP**: może być toouse hello tego samego zakresu adresów IP, jako że w głównej lokalnej sieci, dla hello sieć platformy Azure po pracy awaryjnej.  Utrzymywanie hello upraszcza samych adresów IP odzyskiwania hello zmniejszając sieci problemy związane z po pracy awaryjnej. Jednak Jeśli replikujesz tooAzure należy tooupdate tras z nowej lokalizacji hello adresów IP hello po pracy awaryjnej.


## <a name="retain-ip-addresses"></a>Zachowaj adresów IP

Usługa Site Recovery zapewnia adresy IP tooretain stałej możliwości hello przy awarii tooAzure z trybu failover podsieci.

Tryb failover podsieci określonej podsieci jest obecny w lokacji 1 lub 2 lokacji, ale nigdy nie w obu lokacjach jednocześnie. W kolejności toomaintain hello przestrzeń adresów IP w przypadku hello trybu failover można programowo Rozmieść hello podsieci hello toomove infrastruktury router z jedną tooanother lokacji. Podczas pracy awaryjnej Przenieś podsieci hello z hello skojarzone chronionych maszyn wirtualnych. Główną wadą Hello jest w zdarzeniu hello awarii toomove hello całej podsieci.


### <a name="failover-example"></a>Przykład trybu failover

Oto przykład tooAzure trybu failover.

- Firmy ficticious, banku Woodgrove ma infrastruktury lokalnej hosting aplikacji swoich biznesowych. Ich aplikacji dla urządzeń przenośnych znajdują się na platformie Azure.
- Łączność między maszynami wirtualnymi banku Woodgrove na serwerach Azure i lokalnymi są udostępniane przez połączenie lokacja lokacja (VPN) między siecią krawędzi lokalne powitania i hello sieci wirtualnej platformy Azure.
- Oznacza to sieci VPN, że hello firmy sieci wirtualnej platformy Azure jest wyświetlany jako rozszerzenie sieci lokalnej.
- Woodgrove chce toouse usługi Site Recovery tooreplicate lokalnymi obciążeń tooAzure.
 - Woodgrove ma toodeal z aplikacje i konfiguracje, które są zależne od stałe adresy IP, a w związku z tym należy tooretain adresów IP dla swoich aplikacji po tooAzure pracy awaryjnej.
 - Woodgrove ma przypisanych adresów IP z zakresu 172.16.1.0/24, zasobów tooits 172.16.2.0/24 działające na platformie Azure.


Woodgrove toobe stanie tooreplicate adresy jego tooAzure maszyn wirtualnych podczas zachowywania hello IP w tym miejscu jest jakie firma hello wymaga toodo:

1. Tworzenie sieci wirtualnej platformy Azure. Należy go rozszerzenie hello lokalnej sieci, dzięki czemu aplikacje mogą bezproblemowo awaryjnie.
2. Azure umożliwia możesz tooadd lokacja lokacja łączność w sieci VPN, oprócz toopoint lokacja, łączność toohello sieci wirtualne utworzone na platformie Azure.
3. Podczas konfigurowania połączenia lokacja lokacja hello, w hello Azure sieci, można kierować ruchu toohello lokalnej lokalizacji (sieci lokalne) tylko wtedy, gdy zakres adresów IP hello różni się od zakresu adresów IP lokalne powitania.
    - Jest to spowodowane Azure nie obsługuje rozciągnięty podsieci. Dlatego masz podsieci 192.168.1.0/24 lokalnymi, nie można dodać 192.168.1.0/24 sieci lokalnej w hello sieć platformy Azure.
    - Oczekiwany jest Azure nie może ustalić, czy brak aktywnych maszyn wirtualnych w podsieci hello i podsieci hello jest tworzony tylko odzyskiwania po awarii.
    - Program toobe toocorrectly może kierować ruchem sieciowym poza podsieci hello sieć platformy Azure w sieci hello i sieci lokalnej hello nie może powodować konflikt.

![Przed podsieci trybu failover](./media/hyper-v-site-walkthrough-network/network-design7.png)

### <a name="before-failover"></a>Przed trybu failover

1. Utwórz dodatkowe sieci (na przykład odzyskiwania). Jest hello sieć w którego przejścia w tryb failover maszyny wirtualne są tworzone.
2. tooensure, który hello adresu IP dla maszyny Wirtualnej jest zachowywane po przejściu w tryb failover, hello właściwości maszyny Wirtualnej > **Konfiguruj**, określ hello hello, że maszyna wirtualna ma lokalnego, a następnie kliknij przycisk adres IP tego samego **zapisać**.
3. Gdy hello wirtualna przeszła w tryb failover, usługi Azure Site Recovery przypisze hello podane tooit adresów IP.

    ![Właściwości sieci](./media/hyper-v-site-walkthrough-network/network-design8.png)

4. Po wyzwoleniu wyzwalacza i hello maszyny wirtualne są tworzone na platformie Azure z adresem IP hello wymagane trybu failover można połączyć za pomocą sieci toohello [vonnection tooVnet sieci wirtualnej](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md). Ta akcja umożliwia pisanie skryptów.
5. Trasy należy zmodyfikować odpowiednio, toobe tooreflect tego 192.168.1.0/24 teraz przeniósł tooAzure.

    ![Po podsieci w tryb failover](./media/hyper-v-site-walkthrough-network/network-design9.png)

### <a name="after-failover"></a>Po pracy awaryjnej

Jeśli nie ma sieci platformy Azure, jak pokazano powyżej, można utworzyć połączenie VPN lokacja lokacja między lokacją główną a Azure, po failvoer.

## <a name="change-ip-addresses"></a>Zmiana adresów IP

To [wpis w blogu](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) wyjaśniono, jak adresy tooset się hello Azure infrastrukturę sieci, gdy tooretain IP nie jest konieczne po pracy awaryjnej. Go rozpoczyna się od opisu aplikacji wygląda w sposób tooset się sieci lokalnej i w systemie Azure i zawiera informacje o uruchamianiu przechodzenia w tryb failover.  

## <a name="next-steps"></a>Następne kroki

Przejdź do zbyt[krok 5: przygotowanie Azure](hyper-v-site-walkthrough-prepare-azure.md)
