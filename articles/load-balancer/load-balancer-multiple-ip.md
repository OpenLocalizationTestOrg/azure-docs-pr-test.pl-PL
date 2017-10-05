---
title: "Obciążenia równoważenia na wielu konfiguracji adresów IP na platformie Azure | Dokumentacja firmy Microsoft"
description: "Równoważenie obciążenia w konfiguracji adresu IP podstawowego i pomocniczego."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: na
ms.assetid: 244907cd-b275-4494-aaf7-dcfc4d93edfe
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2017
ms.author: kumud
ms.openlocfilehash: cf1e68c7b37b2506de007bdf24eea63a27187a33
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="load-balancing-on-multiple-ip-configurations-using-the-azure-portal"></a>Obciążenia równoważenia na wielu konfiguracji adresów IP przy użyciu portalu Azure

> [!div class="op_single_selector"]
> * [Portal](load-balancer-multiple-ip.md)
> * [Program PowerShell](load-balancer-multiple-ip-powershell.md)
> * [Interfejs wiersza polecenia](load-balancer-multiple-ip-cli.md)

W tym artykule opisano sposób korzystania z wielu adresów IP na pomocniczym interfejsie sieciowym (NIC) usługi równoważenia obciążenia Azure. W tym scenariuszu będziemy mieć dwie maszyny wirtualne z systemami Windows, każdy z podstawowym i pomocniczym karty sieciowej. Każdej dodatkowej kart sieciowych ma dwie konfiguracje adresów IP. Każda maszyna wirtualna obsługuje zarówno contoso.com witryn sieci Web, jak i fabrikam.com. Każda witryna sieci Web jest powiązana z jedną konfiguracją IP dodatkowej karty sieciowej. Możemy użyć modułu równoważenia obciążenia Azure do udostępnienia dwa adresy IP frontonu, po jednym dla każdej witryny sieci Web, aby dystrybuować ruch do odpowiednich konfigurację adresu IP dla witryny sieci Web. W tym scenariuszu używa tego samego numeru portu na zarówno frontends, jak i oba adresy IP do puli wewnętrznej bazy danych.

![Obraz scenariusz równoważeniem obciążenia](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

##<a name="prerequisites"></a>Wymagania wstępne
W tym przykładzie przyjęto założenie, że masz grupy zasobów o nazwie *contosofabrikam* przy użyciu następującej konfiguracji:
 -  zawiera sieć wirtualną o nazwie *myVNet*, dwie maszyny wirtualne o nazwie *VM1* i *maszyny VM2* odpowiednio w tym samym zestawie nazwanego dostępności *myAvailset*. 
 - Każda maszyna wirtualna ma NIC głównej i dodatkowej karty sieciowej. Podstawowy kart interfejsu sieciowego są nazywane *VM1NIC1* i *VM2NIC1* i pomocniczej karty interfejsu sieciowego są nazywane *VM1NIC2* i *VM2NIC2*. Aby uzyskać więcej informacji na temat tworzenia maszyn wirtualnych z wieloma kartami sieciowymi, zobacz [tworzenia maszyn wirtualnych z wieloma kartami sieciowymi przy użyciu programu PowerShell](../virtual-network/virtual-network-deploy-multinic-arm-ps.md).

## <a name="steps-to-load-balance-on-multiple-ip-configurations"></a>Kroki, aby załadować saldo wielu konfiguracji adresów IP

Wykonaj te kroki, aby osiągnąć scenariusz opisany w tym artykule:

### <a name="step-1-configure-the-secondary-nics-for-each-vm"></a>Krok 1: Konfigurowanie dodatkowej karty sieciowe dla każdej maszyny Wirtualnej

Dla każdej maszyny Wirtualnej w sieci wirtualnej dodać zestaw konfigurację adresu IP dla dodatkowej karty interfejsu Sieciowego w następujący sposób:  

1. W przeglądarce przejdź do portalu Azure: http://portal.azure.com i zaloguj się za pomocą konta platformy Azure.
2. Po lewej stronie górnej części ekranu, kliknij ikonę grupy zasobów, a następnie kliknij przycisk maszyn wirtualnych znajdują się w grupie zasobów (na przykład *contosofabrikam*). **Grup zasobów** bloku, który zawiera listę wszystkich zasobów oraz interfejsy sieci dla maszyn wirtualnych jest teraz wyświetlany.
3. Do dodatkowej karty Sieciowej każdej maszyny Wirtualnej Dodaj konfigurację protokołu IP w następujący sposób:
    1. Wybierz interfejs sieciowy ma zostać dodany do konfiguracji adresu IP.
    2. W wyświetlonym karty sieciowej, które wybrano bloku, kliknij przycisk **konfiguracje adresów IP**. Następnie kliknij przycisk **Dodaj** góry bloku, który jest wyświetlany.
    3. W **konfiguracje dodawanie adresów IP** bloku, Dodaj drugi konfiguracji IP do karty Sieciowej w następujący sposób: 
        1. Wpisz nazwę dodatkowej konfiguracji adresu IP (na przykład dla konfiguracji adresów IP jako nazw VM1 i maszyny VM2 *VM1NIC2 ipconfig2* i *VM2NIC2 ipconfig2* odpowiednio).
        2. Aby uzyskać **prywatny adres IP**, dla **alokacji**, wybierz pozycję **statycznych**.
        3. Kliknij przycisk **OK**.
        4. Po zakończeniu drugiego konfiguracji IP do dodatkowej karty Sieciowej jest wyświetlany w **konfiguracje adresów IP** blok ustawień dla danej karty sieciowej.

### <a name="step-2-create-a-load-balancer"></a>Krok 2: Tworzenie usługi równoważenia obciążenia

Utwórz usługę równoważenia obciążenia w następujący sposób:

1. W przeglądarce przejdź do portalu Azure: http://portal.azure.com i zaloguj się za pomocą konta platformy Azure.
2. W lewej górnej części ekranu, kliknij polecenie **nowy** > **sieci** > **modułu równoważenia obciążenia**. Następnie kliknij przycisk **Utwórz**.
3. W bloku **Tworzenie modułu równoważenia obciążenia** wpisz nazwę modułu równoważenia obciążenia. W tym miejscu jest nazywany *mylb*.
4. Publiczny adres IP, Utwórz nowy publiczny adres IP o nazwie **PublicIP1**.
5. W grupie zasobów, wybierz istniejącą grupę zasobów w sieci maszyn wirtualnych (na przykład *contosofabrikam*). Następnie wybierz odpowiednią lokalizację, a następnie kliknij przycisk **OK**. Rozpocznie się wdrażanie modułu równoważenia obciążenia. Potrwa to kilka minut.
6. Po wdrożeniu usługi równoważenia obciążenia jest wyświetlana jako zasób w grupie zasobów.

### <a name="step-3-configure-the-frontend-ip-pool"></a>KROK 3: Konfigurowanie puli adresów IP frontonu

Skonfiguruj pulę IP frontonu dla każdej witryny sieci Web (Contoso i Fabrikam) w następujący sposób:

1. W portalu kliknij **więcej usług** > typ **publicznego adresu IP** w polu filtru, a następnie kliknij przycisk **publicznego adresu IP, adresy**. Kliknij przycisk **Dodaj** góry bloku, który jest wyświetlany.
2. Skonfiguruj dwa publiczne adresy IP (*PublicIP1* i *PublicIP2*) dla obu witryn sieci Web (contoso i fabrikam) w następujący sposób:
    1. Wpisz nazwę dla adresu IP frontonu.
    2. Aby uzyskać **grupy zasobów**, wybierz istniejącą grupę zasobów maszyn wirtualnych (na przykład *contosofabrikam*).
    3. Aby uzyskać **lokalizacji**, wybierz lokalizację, w tym samym jako maszyn wirtualnych.
    4. Kliknij przycisk **OK**.
    5. Po utworzeniu dwa publiczne adresy IP są oba wyświetlane w **publicznego adresu IP** bloku adresów.
3. W portalu kliknij **więcej usług** > typ **modułu równoważenia obciążenia** w polu filtru, a następnie kliknij przycisk **moduł równoważenia obciążenia**.  
4. Wybierz usługę równoważenia obciążenia (*mylb*) chcesz dodać puli adresów IP frontonu, aby.
5. W obszarze **ustawienia**, wybierz pozycję **pule frontonu**. Następnie kliknij przycisk **Dodaj** góry bloku, który jest wyświetlany.
6. Wpisz nazwę dla adresu IP frontonu (*farbikamfe* lub **contosofe*).
7. Kliknij przycisk **adres IP** i na **wybierz publiczny adres IP** bloku, wybierz adresy IP z serwera sieci Web (*PublicIP1* lub *PublicIP2*).
8. Powtórz kroki od 3 do 7 w tej sekcji, aby utworzyć drugiego adresu IP frontonu.
9. Po zakończeniu konfiguracji puli adresu IP frontonu, oba adresy IP frontonu są wyświetlane w **puli adresów IP frontonu** bloku przez moduł równoważenia obciążenia. 
    
### <a name="step-4-configure-the-backend-pool"></a>KROK 4: Konfigurowanie puli wewnętrznej bazy danych   
Skonfiguruj pule adresów zaplecza na moduł równoważenia obciążenia dla każdej witryny sieci Web (Contoso i Fabrikam) w następujący sposób:
        
1. W portalu kliknij **więcej usług** > typu usługi równoważenia obciążenia w polu filtru, a następnie kliknij przycisk **moduł równoważenia obciążenia**.  
2. Wybierz usługę równoważenia obciążenia (*mylb*) chcesz dodać pul zaplecza do.
3. W obszarze **ustawienia**, wybierz pozycję **pul zaplecza**. Wpisz nazwę użytkownika puli wewnętrznej bazy danych (na przykład *contosopool* lub *fabrikampool*). Następnie kliknij przycisk **Dodaj** przycisk w kierunku do góry bloku, który jest wyświetlany. 
4. Aby uzyskać **skojarzonego z**, wybierz pozycję **zestawu dostępności**.
5. Aby uzyskać **zestawu dostępności**, wybierz pozycję **myAvailset**.
6. Dodaj konfiguracje adresów IP sieci docelowej, dla obu maszyn wirtualnych w następujący sposób (patrz rysunek 2):  
    1. Aby uzyskać **maszynę wirtualną w docelowej**, wybierz maszynę Wirtualną, która ma zostać dodany do puli wewnętrznej bazy danych (na przykład VM1 lub maszyny VM2).
    2. Dla **konfiguracji sieci IP**, wybierz dodatkowej konfiguracji IP kart sieciowych dla tej maszyny Wirtualnej (na przykład VM1NIC2 ipconfig2 lub VM2NIC2 ipconfig2).
    ![Obraz scenariusz równoważeniem obciążenia](./media/load-balancer-multiple-ip/lb-backendpool.PNG)
            
        **Rysunek 2**: Konfigurowanie usługi równoważenia obciążenia z pul zaplecza  
7. Kliknij przycisk **OK**.
8. Po zakończeniu konfiguracji puli wewnętrznej bazy danych, zarówno pul adresów zaplecza są wyświetlane w **bloku puli zaplecza** Twojego modułu równoważenia obciążenia.

### <a name="step-5-configure-a-health-probe-for-your-load-balancer"></a>KROK 5: Konfigurowanie badanie kondycji dla Twojej usługi równoważenia obciążenia
Skonfiguruj badanie kondycji dla Twojej usługi równoważenia obciążenia w następujący sposób:
    1. W portalu, kliknij przycisk więcej usług > typu usługi równoważenia obciążenia w polu filtru, a następnie kliknij przycisk **moduł równoważenia obciążenia**.  
    2. Wybierz usługę równoważenia obciążenia, które chcesz dodać pul zaplecza do.
    3. W obszarze **ustawienia**, wybierz pozycję **sondy kondycji**. Następnie kliknij przycisk **Dodaj** góry bloku, który jest wyświetlany.
    4. Wpisz nazwę dla sondy kondycji (na przykład HTTP), a następnie kliknij przycisk **OK**.

### <a name="step-6-configure-load-balancing-rules"></a>KROK 6: Skonfigurowanie reguł równoważenia obciążenia
Skonfiguruj reguły równoważenia obciążenia (*HTTPc* i *HTTPf*) dla poszczególnych witryn internetowych w następujący sposób:
    
1. W obszarze **ustawienia**, wybierz pozycję **sondy kondycji**. Następnie kliknij przycisk **Dodaj** góry bloku, który jest wyświetlany.
2. Aby uzyskać **nazwa**, wpisz nazwę reguły równoważenia obciążenia (na przykład *HTTPc* "contoso", lub *HTTPf* dla firmy Fabrikam)
3. Dla adresu IP frontonu, wybierz adres IP serwera sieci Web (na przykład *Contosofe* lub *Fabrikamfe*)
4. Aby uzyskać **portu** i **portu zaplecza**, należy zachować wartość domyślną **80**.
5. Aby uzyskać **pływającego adresu IP (bezpośredni zwrot serwera)**, kliknij przycisk **włączone**.
6. Kliknij przycisk **OK**.
7. Powtórz kroki od 1 do 6 w tej sekcji, aby utworzyć drugą regułę modułu równoważenia obciążenia.
8. Gdy równoważenia obciążenia zasady, konfiguracja została ukończona, obie reguły ((*HTTPc* i *HTTPf*) są wyświetlane w **reguły równoważenia obciążenia** bloku przez moduł równoważenia obciążenia.

### <a name="step-7-configure-dns-records"></a>KROK 7: Konfigurowanie rekordów DNS
Na koniec należy skonfigurować rekordy zasobów DNS, aby wskazywał adres IP frontonu odpowiedniej usługi równoważenia obciążenia. Może hostować domen w usłudze Azure DNS. Aby uzyskać więcej informacji o korzystaniu z usługi Azure DNS z usługi równoważenia obciążenia, zobacz [przy użyciu usługi Azure DNS z innymi usługami Azure](../dns/dns-for-azure-services.md).

## <a name="next-steps"></a>Następne kroki
- Dowiedz się więcej o sposobie łączenia usługi na platformie Azure w równoważenia obciążenia [przy użyciu usługi równoważenia obciążenia w Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).
- Dowiedz się, jak używasz różne typy dzienników na platformie Azure do zarządzania i rozwiązywania problemów z usługi równoważenia obciążenia w [dziennika analizy dla usługi równoważenia obciążenia Azure](../load-balancer/load-balancer-monitor-log.md).
