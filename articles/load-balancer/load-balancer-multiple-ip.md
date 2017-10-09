---
title: "aaaLoad równoważenia na wielu konfiguracji adresów IP na platformie Azure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 8619493b8102e9d158d428fe6c59ecf3f32edc32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="load-balancing-on-multiple-ip-configurations-using-hello-azure-portal"></a>Równoważenie na wielu konfiguracji adresów IP przy użyciu portalu Azure hello obciążenia

> [!div class="op_single_selector"]
> * [Portal](load-balancer-multiple-ip.md)
> * [Program PowerShell](load-balancer-multiple-ip-powershell.md)
> * [Interfejs wiersza polecenia](load-balancer-multiple-ip-cli.md)

W tym artykule opisano, jak toouse modułu równoważenia obciążenia Azure z adresem IP wielu adresów na pomocniczym interfejsie sieciowym (NIC). W tym scenariuszu będziemy mieć dwie maszyny wirtualne z systemami Windows, każdy z podstawowym i pomocniczym karty sieciowej. Każdy z hello dodatkowej karty sieciowe mają dwie konfiguracje adresów IP. Każda maszyna wirtualna obsługuje zarówno contoso.com witryn sieci Web, jak i fabrikam.com. Każda witryna sieci Web jest powiązane tooone konfiguracji IP hello na powitania dodatkowej karty sieciowej. Używamy modułu równoważenia obciążenia Azure tooexpose dwa frontonu adresy IP, po jednej dla każdej witryny sieci Web, toodistribute ruchu toohello odpowiednich konfiguracji IP hello witryny sieci Web. W tym scenariuszu używa hello tego samego numeru portu między zarówno frontends, jak i oba adresy IP do puli wewnętrznej bazy danych.

![Obraz scenariusz równoważeniem obciążenia](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

##<a name="prerequisites"></a>Wymagania wstępne
W tym przykładzie przyjęto założenie, że masz grupy zasobów o nazwie *contosofabrikam* z hello następującej konfiguracji:
 -  zawiera sieć wirtualną o nazwie *myVNet*, dwie maszyny wirtualne o nazwie *VM1* i *maszyny VM2* odpowiednio poziomu hello sam zestaw o nazwie dostępności *myAvailset*. 
 - Każda maszyna wirtualna ma NIC głównej i dodatkowej karty sieciowej. podstawowy Hello kart interfejsu sieciowego są nazywane *VM1NIC1* i *VM2NIC1* i pomocniczy hello kart interfejsu sieciowego są nazywane *VM1NIC2* i *VM2NIC2*. Aby uzyskać więcej informacji na temat tworzenia maszyn wirtualnych z wieloma kartami sieciowymi, zobacz [tworzenia maszyn wirtualnych z wieloma kartami sieciowymi przy użyciu programu PowerShell](../virtual-network/virtual-network-deploy-multinic-arm-ps.md).

## <a name="steps-tooload-balance-on-multiple-ip-configurations"></a>Saldo tooload czynności na wielu konfiguracji adresów IP

Wykonaj następujące kroki poniżej scenariuszu hello tooachieve opisane w tym artykule:

### <a name="step-1-configure-hello-secondary-nics-for-each-vm"></a>Krok 1: Konfigurowanie hello dodatkowej karty sieciowe dla każdej maszyny Wirtualnej

Dla każdej maszyny Wirtualnej w sieci wirtualnej, dodać zestaw konfigurację adresu IP dla hello dodatkowej kart interfejsu Sieciowego w następujący sposób:  

1. W przeglądarce Przejdź toohello portalu Azure: http://portal.azure.com i zaloguj się za pomocą konta platformy Azure.
2. Na hello lewej górnej części ekranu hello, kliknij ikonę grupy zasobów hello, a następnie kliknij hello grupy zasobów hello maszyn wirtualnych znajdują się w (na przykład *contosofabrikam*). Witaj **grup zasobów** bloku, który wyświetla listę wszystkich zasobów hello wraz z interfejsów sieciowych hello hello maszyny wirtualne są wyświetlane.
3. pomocniczy toohello kart każdej maszyny Wirtualnej, Dodaj konfigurację protokołu IP, w następujący sposób:
    1. Wybierz interfejs sieciowy hello interesujące konfiguracji IP hello tooadd do.
    2. W hello wyświetlonym bloku dla hello kart, które wybrano kliknij **konfiguracje adresów IP**. Następnie kliknij przycisk **Dodaj** kierunku hello górnej części bloku hello, które zostaną wyświetlone.
    3. W hello **konfiguracje dodawanie adresów IP** bloku, Dodaj drugi toohello konfiguracji adresu IP karty Sieciowej w następujący sposób: 
        1. Wpisz nazwę dodatkowej konfiguracji adresu IP (na przykład dla nazw VM1 i maszyny VM2 hello konfiguracje adresów IP jako *VM1NIC2 ipconfig2* i *VM2NIC2 ipconfig2* odpowiednio).
        2. Aby uzyskać **prywatny adres IP**, dla **alokacji**, wybierz pozycję **statycznych**.
        3. Kliknij przycisk **OK**.
        4. Po hello drugi konfigurację adresu IP dla hello dodatkowej karty Sieciowej jest wyświetlany w hello **konfiguracje adresów IP** bloku ustawień hello podanych kart sieciowych.

### <a name="step-2-create-a-load-balancer"></a>Krok 2: Tworzenie usługi równoważenia obciążenia

Utwórz usługę równoważenia obciążenia w następujący sposób:

1. W przeglądarce Przejdź toohello portalu Azure: http://portal.azure.com i zaloguj się za pomocą konta platformy Azure.
2. Polecenie hello lewej górnej części ekranu hello, **nowy** > **sieci** > **modułu równoważenia obciążenia**. Następnie kliknij przycisk **Utwórz**.
3. W hello **modułu równoważenia obciążenia Utwórz** bloku, wpisz nazwę użytkownika usługi równoważenia obciążenia. W tym miejscu jest nazywany *mylb*.
4. Publiczny adres IP, Utwórz nowy publiczny adres IP o nazwie **PublicIP1**.
5. W grupie zasobów, wybierz hello istniejącej grupy zasobów w sieci maszyn wirtualnych (na przykład *contosofabrikam*). Następnie wybierz odpowiednią lokalizację, a następnie kliknij przycisk **OK**. Moduł równoważenia obciążenia Hello następnie zostanie uruchomiony toodeploy i dopiero po kilku minutach toosuccessfully ukończenia wdrożenia.
6. Po wdrożeniu usługi równoważenia obciążenia hello jest wyświetlana jako zasób w grupie zasobów.

### <a name="step-3-configure-hello-frontend-ip-pool"></a>KROK 3: Konfigurowanie puli adresów IP frontonu hello

Skonfiguruj pulę IP frontonu dla każdej witryny sieci Web (Contoso i Fabrikam) w następujący sposób:

1. W portalu powitania kliknij **więcej usług** > typ **publicznego adresu IP** w hello pola filtru, a następnie kliknij przycisk **publicznego adresu IP, adresy**. Kliknij przycisk **Dodaj** kierunku hello górnej części bloku hello, które zostaną wyświetlone.
2. Skonfiguruj dwa publiczne adresy IP (*PublicIP1* i *PublicIP2*) dla obu witryn sieci Web (contoso i fabrikam) w następujący sposób:
    1. Wpisz nazwę dla adresu IP frontonu.
    2. Dla **grupy zasobów**, wybierz hello istniejącej grupy zasobów z hello maszyn wirtualnych (na przykład *contosofabrikam*).
    3. Aby uzyskać **lokalizacji**, wybierz hello tej samej lokalizacji, ponieważ hello maszyn wirtualnych.
    4. Kliknij przycisk **OK**.
    5. Po utworzeniu Witaj dwie publiczne adresy IP są oba wyświetlane w hello **publicznego adresu IP** bloku adresów.
3. W portalu powitania kliknij **więcej usług** > typ **modułu równoważenia obciążenia** w hello pola filtru, a następnie kliknij przycisk **moduł równoważenia obciążenia**.  
4. Wybierz moduł równoważenia obciążenia hello (*mylb*), które mają puli adresów IP frontonu hello tooadd do.
5. W obszarze **ustawienia**, wybierz pozycję **pule frontonu**. Następnie kliknij przycisk **Dodaj** kierunku hello górnej części bloku hello, które zostaną wyświetlone.
6. Wpisz nazwę dla adresu IP frontonu (*farbikamfe* lub **contosofe*).
7. Kliknij przycisk **adres IP** i na powitania **wybierz publiczny adres IP** bloku, wybierz hello adresów IP z serwera sieci Web (*PublicIP1* lub *PublicIP2*).
8. Powtórz kroki 3 too7 w tej sekcji toocreate hello drugiego adresu IP frontonu.
9. Po zakończeniu konfiguracji puli adresu IP frontonu hello oba adresy IP frontonu są wyświetlane w hello **puli adresów IP frontonu** bloku przez moduł równoważenia obciążenia. 
    
### <a name="step-4-configure-hello-backend-pool"></a>KROK 4: Konfigurowanie puli zaplecza hello   
Skonfiguruj pule adresów zaplecza hello na moduł równoważenia obciążenia dla każdej witryny sieci Web (Contoso i Fabrikam) w następujący sposób:
        
1. W portalu powitania kliknij **więcej usług** > wpisz w polu filtru hello modułu równoważenia obciążenia, a następnie kliknij przycisk **moduł równoważenia obciążenia**.  
2. Wybierz moduł równoważenia obciążenia hello (*mylb*), które mają pul zaplecza hello tooadd do.
3. W obszarze **ustawienia**, wybierz pozycję **pul zaplecza**. Wpisz nazwę użytkownika puli wewnętrznej bazy danych (na przykład *contosopool* lub *fabrikampool*). Następnie kliknij przycisk hello **Dodaj** przycisku w kierunku hello górnej części bloku hello, które zostaną wyświetlone. 
4. Aby uzyskać **skojarzonego z**, wybierz pozycję **zestawu dostępności**.
5. Aby uzyskać **zestawu dostępności**, wybierz pozycję **myAvailset**.
6. Dodaj konfiguracje adresów IP sieci docelowej, dla obu maszyn wirtualnych w następujący sposób (patrz rysunek 2):  
    1. Aby uzyskać **maszynę wirtualną w docelowej**, wybierz hello maszyn wirtualnych, które mają tooadd toohello puli zaplecza (na przykład VM1 lub maszyny VM2).
    2. Dla **konfiguracji sieci IP**, wybierz pozycję hello dodatkowej konfiguracji IP kart sieciowych dla tej maszyny Wirtualnej (na przykład VM1NIC2 ipconfig2 lub VM2NIC2 ipconfig2).
    ![Obraz scenariusz równoważeniem obciążenia](./media/load-balancer-multiple-ip/lb-backendpool.PNG)
            
        **Rysunek 2**: Konfigurowanie usługi równoważenia obciążenia hello z pul zaplecza  
7. Kliknij przycisk **OK**.
8. Po zakończeniu konfiguracji puli zaplecza hello zarówno pul adresów zaplecza są wyświetlane w hello **bloku puli zaplecza** Twojego modułu równoważenia obciążenia.

### <a name="step-5-configure-a-health-probe-for-your-load-balancer"></a>KROK 5: Konfigurowanie badanie kondycji dla Twojej usługi równoważenia obciążenia
Skonfiguruj badanie kondycji dla Twojej usługi równoważenia obciążenia w następujący sposób:
    1. W portalu powitania kliknij więcej usług > wpisz w polu filtru hello modułu równoważenia obciążenia, a następnie kliknij przycisk **moduł równoważenia obciążenia**.  
    2. Wybierz hello równoważenia obciążenia, który ma pul zaplecza hello tooadd do.
    3. W obszarze **ustawienia**, wybierz pozycję **sondy kondycji**. Następnie kliknij przycisk **Dodaj** kierunku hello górnej części bloku hello, które zostaną wyświetlone.
    4. Wpisz nazwę dla sondy kondycji hello (na przykład HTTP), a następnie kliknij przycisk **OK**.

### <a name="step-6-configure-load-balancing-rules"></a>KROK 6: Skonfigurowanie reguł równoważenia obciążenia
Skonfiguruj reguły równoważenia obciążenia (*HTTPc* i *HTTPf*) dla poszczególnych witryn internetowych w następujący sposób:
    
1. W obszarze **ustawienia**, wybierz pozycję **sondy kondycji**. Następnie kliknij przycisk **Dodaj** kierunku hello górnej części bloku hello, które zostaną wyświetlone.
2. Dla **nazwa**, wpisz nazwę reguły równoważenia obciążenia hello (na przykład *HTTPc* "contoso", lub *HTTPf* dla firmy Fabrikam)
3. Dla adresu IP frontonu, wybierz adres IP frontonu hello hello (na przykład *Contosofe* lub *Fabrikamfe*)
4. Aby uzyskać **portu** i **portu zaplecza**, należy zachować wartość domyślną hello **80**.
5. Aby uzyskać **pływającego adresu IP (bezpośredni zwrot serwera)**, kliknij przycisk **włączone**.
6. Kliknij przycisk **OK**.
7. Powtórz kroki od 1 too6 w tej drugiej reguły modułu równoważenia obciążenia sekcji toocreate hello.
8. Gdy równoważenia obciążenia hello zasady, konfiguracja została ukończona, obie reguły ((*HTTPc* i *HTTPf*) są wyświetlane w hello **reguły równoważenia obciążenia** bloku przez moduł równoważenia obciążenia.

### <a name="step-7-configure-dns-records"></a>KROK 7: Konfigurowanie rekordów DNS
Na koniec należy skonfigurować DNS zasobów rekordów toopoint toohello odpowiedniego adresu IP frontonu modułu równoważenia obciążenia hello. Może hostować domen w usłudze Azure DNS. Aby uzyskać więcej informacji o korzystaniu z usługi Azure DNS z usługi równoważenia obciążenia, zobacz [przy użyciu usługi Azure DNS z innymi usługami Azure](../dns/dns-for-azure-services.md).

## <a name="next-steps"></a>Następne kroki
- Dowiedz się więcej na temat sposobu równoważenia obciążenia toocombine usługi na platformie Azure w [przy użyciu usługi równoważenia obciążenia w Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).
- Dowiedz się, jak można używać różnych typów dzienników w Azure toomanage i rozwiązywanie problemów z usługą równoważenia obciążenia w [dziennika analizy dla usługi równoważenia obciążenia Azure](../load-balancer/load-balancer-monitor-log.md).
