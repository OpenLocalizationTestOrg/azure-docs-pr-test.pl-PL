---
title: "równoważenia obciążenia aaaCreate internetowy - portalu Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate internetowy modułu równoważenia obciążenia w Menedżerze zasobów przy użyciu hello portalu Azure"
services: load-balancer
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: aa9d26ca-3d8a-4a99-83b7-c410dd20b9d0
ms.service: load-balancer
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: annahar
ms.openlocfilehash: 390ba8ec1474c54cf2c0022c4a3c219d21b1a659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-internet-facing-load-balancer-using-hello-azure-portal"></a>Tworzenie usługi równoważenia obciążenia skierowane do Internetu za pomocą hello portalu Azure

> [!div class="op_single_selector"]
> * [Portal](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [Program PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [Interfejs wiersza polecenia platformy Azure](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [Szablon](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

W tym artykule omówiono modelu wdrażania usługi Resource Manager hello. Możesz również [Dowiedz się, jak usługa równoważenia przy użyciu klasycznego wdrożenia obciążenia toocreate internetowy](load-balancer-get-started-internet-classic-portal.md)

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

Obejmuje to sekwencję hello poszczególne zadania toocreate toobe gotowe modułu równoważenia obciążenia, które opisano szczegółowo, co jest wykonywana w celu hello tooaccomplish.

## <a name="what-is-required-toocreate-an-internet-facing-load-balancer"></a>Co to jest wymagane toocreate do modułu równoważenia obciążenia internetowy?

Należy toocreate i skonfigurować hello następujące obiekty toodeploy modułu równoważenia obciążenia.

* Konfiguracja IP frontonu — publiczne adresy IP dla przychodzącego ruchu sieciowego.
* Pula adresów zaplecza — zawiera interfejsów sieciowych (NIC) dla ruchu sieciowego tooreceive hello maszyn wirtualnych z hello modułu równoważenia obciążenia.
* Reguły równoważenia obciążenia — zawiera reguły mapowania port publiczny na tooport usługi równoważenia obciążenia hello hello puli adresów zaplecza.
* Reguły NAT dla ruchu przychodzącego — zawiera reguły mapowania port publiczny na porcie programu tooa usługi równoważenia obciążenia w hello dla określonej maszyny wirtualnej w puli adresów zaplecza hello.
* Sondy — zawiera dostępności toocheck badania używane kondycji wystąpień maszyn wirtualnych w puli adresów zaplecza hello.

Więcej informacji o składnikach modułu równoważenia obciążenia tworzonego za pomocą usługi Azure Resource Manager można znaleźć w artykule [Azure Resource Manager support for Load Balancer](load-balancer-arm.md) (Obsługa usługi Azure Resource Manager dla modułu równoważenia obciążenia).

## <a name="set-up-a-load-balancer-in-azure-portal"></a>Konfigurowanie modułu równoważenia obciążenia w witrynie Azure Portal

> [!IMPORTANT]
> Jednym z złożeń przyjętych na potrzeby poniższego przykładu jest utworzenie sieci wirtualnej o nazwie **myVNet**. Odwołuje się zbyt[Utwórz sieć wirtualną](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) toodo to. Zakłada się również jest podsiecią w ramach **myVNet** o nazwie **można podsieci LB** i dwie maszyny wirtualne o nazwie **web1** i **sieci Web 2** odpowiednio poziomu Witaj w tym samym zestawie o nazwie dostępności **myAvailSet** w **myVNet**. Odwołuje się zbyt[to łącze](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toocreate maszyn wirtualnych.

1. W przeglądarce Przejdź toohello portalu Azure: [http://portal.azure.com](http://portal.azure.com) i zaloguj się za pomocą konta platformy Azure.
2. Na powitania top po lewej stronie ekranu hello wybierz **nowy** > **sieci** > **usługi równoważenia obciążenia.**
3. W hello **modułu równoważenia obciążenia Utwórz** bloku, wpisz nazwę użytkownika usługi równoważenia obciążenia. W tym przykładzie ma on nazwę **myLoadBalancer**.
4. W obszarze **Typ** wybierz opcję **Publiczny**.
5. W obszarze **Publiczny adres IP** utwórz nowy publiczny adres IP o nazwie **myPublicIP**.
6. W obszarze Grupa zasobów wybierz **myRG**. Następnie wybierz odpowiednią **Lokalizację** i kliknij przycisk **OK**. Moduł równoważenia obciążenia Hello następnie zostanie uruchomiony toodeploy i dopiero po kilku minutach toosuccessfully ukończenia wdrożenia.

    ![Aktualizowanie grupy zasobów modułu równoważenia obciążenia](./media/load-balancer-get-started-internet-portal/1-load-balancer.png)

## <a name="create-a-back-end-address-pool"></a>Tworzenie puli adresów zaplecza

1. Po wdrożeniu modułu równoważenia obciążenia wybierz go z puli zasobów. W obszarze ustawień wybierz opcję Pule zaplecza. Wpisz nazwę puli zaplecza. Następnie kliknij polecenie hello **Dodaj** przycisku w kierunku hello górnej części bloku hello, które zostaną wyświetlone.
2. Polecenie **Dodaj maszynę wirtualną** w hello **Dodaj pulę zaplecza** bloku.  Wybierz opcję **Wybierz zestaw dostępności** w obszarze **Zestaw dostępności** i wybierz pozycję **myAvailSet**. Następnie wybierz pozycję **wybierz maszyny wirtualne hello** w obszarze hello sekcja maszyny wirtualne w bloku hello i wybierz polecenie **web1** i **sieci Web 2**, Witaj dwie maszyny wirtualne utworzone w programie Równoważenie obciążenia. Upewnij się, że mają pozostawione tak jak pokazano na poniższym obrazie hello toohello niebieski znaczniki wyboru. Następnie kliknij przycisk **wybierz** w tym bloku, a następnie OK w hello **maszyny wirtualnej wybierz** bloku, a następnie **OK** w hello **Dodaj pulę zaplecza** blok.

    ![Dodawanie puli adresów zaplecza toohello- ](./media/load-balancer-get-started-internet-portal/3-load-balancer-backend-02.png)

3. Sprawdź, czy na liście rozwijanej powiadomienia toomake aktualizacją dotyczące zapisywanie puli zaplecza modułu równoważenia obciążenia hello w interfejsie sieciowym hello tooupdating dodanie dla obu hello maszyn wirtualnych **web1** i **sieci Web 2**.

## <a name="create-a-probe-lb-rule-and-nat-rules"></a>Tworzenie sondy, reguły równoważenia obciążenia i reguł NAT

1. Utwórz sondę kondycji.

    W obszarze Ustawienia modułu równoważenia obciążenia wybierz pozycję Sondy. Następnie kliknij przycisk **Dodaj** znajdujący się u góry bloku hello hello.

    Istnieją dwa sposoby tooconfigure badanie: HTTP lub TCP. W tym przykładzie pokazano konfigurację HTTP, ale konfiguracja TCP przebiega bardzo podobnie.
    Zaktualizuj hello niezbędne informacje. Jak wspomniano wcześniej, moduł **myLoadBalancer** będzie równoważyć obciążenie na porcie 80. Wybrana ścieżka Hello jest HealthProbe.aspx, interwał wynosi 15 sekund i 2 jest próg złej kondycji. Po skończeniu kliknij **OK** toocreate hello sondowania.

    Umieść kursor myszy nad toolearn ikona hello "i" więcej informacji na temat tych konfiguracji poszczególnych i jak mogą być zmienione toocater tooyour wymagania.

    ![Dodawanie sondy](./media/load-balancer-get-started-internet-portal/4-load-balancer-probes.png)

2. Utwórz regułę modułu równoważenia obciążenia.

    Polecenie reguły w hello równoważenia obciążenia ustawienia sekcji przez moduł równoważenia obciążenia. W nowym bloku hello, kliknij polecenie **Dodaj**. Nadaj nazwę regule. W tym przykładzie jej nazwa to HTTP. Wybierz hello portu frontonu i wewnętrznej bazy danych. W tym przykładzie w obu przypadkach wybrano port 80. Wybierz **LB zaplecza** jako puli zaplecza i hello wcześniej utworzony **HealthProbe** jako hello sondowania. Inne konfiguracje, można skonfigurować zgodnie z wymaganiami tooyour. Następnie kliknij przycisk reguły równoważenia obciążenia hello OK toosave.

    ![Dodawanie reguły równoważenia obciążenia](./media/load-balancer-get-started-internet-portal/5-load-balancing-rules.png)

3. Tworzenie reguł NAT dla ruchu przychodzącego

    Polecenie reguły NAT ruchu przychodzącego w sekcji Ustawienia hello przez moduł równoważenia obciążenia. W hello nowy blok, który kliknij **Dodaj**. Następnie nadaj nazwę regule NAT dla ruchu przychodzącego. W tym przykładzie jej nazwa to **inboundNATrule1**. Witaj miejsce docelowe powinno być hello utworzony uprzednio publiczny adres IP. Wybierz opcję Niestandardowa, w ramach usługi i wybierz protokół hello chcesz toouse. W tym przykładzie wybrano protokół TCP. Wprowadź hello port 3441 i hello port docelowy, w tym przypadku 3389. następnie kliknij przycisk OK toosave tej reguły.

    Po utworzeniu pierwszej reguły hello, powtórz ten krok dla hello drugi przychodzącą regułę NAT z portu 3442 tooTarget portu 3389 o nazwie inboundNATrule2.

    ![Dodawanie reguły NAT dla ruchu przychodzącego](./media/load-balancer-get-started-internet-portal/6-load-balancer-inbound-nat-rules.png)

## <a name="remove-a-load-balancer"></a>Usuwanie modułu równoważenia obciążenia

toodelete modułem równoważenia obciążenia modułu równoważenia obciążenia wybierz hello ma tooremove. W hello *modułu równoważenia obciążenia* bloku, kliknij polecenie **usunąć** znajdujący się u góry bloku hello hello. Gdy pojawi się monit, kliknij przycisk **Tak**.

## <a name="next-steps"></a>Następne kroki

[Get started configuring an internal load balancer](load-balancer-get-started-ilb-arm-cli.md) (Wprowadzenie do konfigurowania wewnętrznego modułu równoważenia obciążenia)

[Configure a load balancer distribution mode](load-balancer-distribution-mode.md) (Konfigurowanie trybu dystrybucji modułu równoważenia obciążenia)

[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md) (Konfigurowanie ustawień limitu czasu bezczynności protokołu TCP dla modułu równoważenia obciążenia)
