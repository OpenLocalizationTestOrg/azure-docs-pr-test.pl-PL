---
title: 'Konfigurowanie bramy sieci VPN: klasyczny portal: Azure | Dokumentacja firmy Microsoft'
description: "W tym artykule przedstawiono sposób konfigurowania sieci wirtualnej bramy sieci VPN i zmianę bramy sieci VPN typu routingu. Te kroki dotyczą w klasycznym modelu wdrażania i klasycznego portalu."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: fbe59ba8-b11f-4d21-9bb1-225ec6c6d351
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/04/2017
ms.author: cherylmc
ms.openlocfilehash: 2ea4e6bb86b1ba6f7b501b193d0713d3901457af
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-vpn-gateway-in-the-classic-portal"></a>Konfigurowanie bramy sieci VPN w portalu klasycznym 
Aby utworzyć połączenie bezpieczne między lokalizacjami platformy Azure i Twojej lokalizacji lokalnej, należy utworzyć bramę sieci wirtualnej. Brama sieci VPN jest określonego typu bramy sieci wirtualnej. W klasycznym modelu wdrażania, bramy sieci VPN może być jeden z dwóch typów routingu sieci VPN: statyczny lub dynamiczny. Wybranego typu sieci VPN zależy od tego, z planem projektu sieci i lokalnego urządzenia sieci VPN, który ma być używany. Aby uzyskać więcej informacji o urządzeniach sieci VPN, zobacz [o urządzeniach sieci VPN](vpn-gateway-about-vpn-devices.md).

**Modele wdrażania Azure — informacje**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="configuration-overview"></a>Przegląd konfiguracji
W poniższych krokach objaśniono przez konfigurację bramy sieci VPN w klasycznym portalu. Te kroki dotyczą bram dla sieci wirtualnych, które zostały utworzone przy użyciu klasycznego modelu wdrażania. Obecnie nie wszystkie ustawienia konfiguracji dla bramy są dostępne w portalu Azure. Gdy są one, zostanie utworzony nowy zestaw instrukcji, które mają zastosowanie do portalu Azure.

### <a name="before-you-begin"></a>Przed rozpoczęciem
Przed skonfigurowaniem bramy, należy najpierw utworzyć sieć wirtualną. Tworzenie sieci wirtualnej dla łączności między lokalizacjami, zapoznać się [Skonfiguruj sieć wirtualną z połączenia sieci VPN typu lokacja lokacja](vpn-gateway-site-to-site-create.md), lub [Skonfiguruj sieć wirtualną z połączenia sieci VPN punkt lokacja](vpn-gateway-point-to-site-create.md). Następnie wykonaj następujące kroki, aby skonfigurować bramę sieci VPN i zbierać informacje, które należy skonfigurować urządzenie sieci VPN. 

Jeśli masz już bramy sieci VPN i chcesz zmienić typ routingu w sieci VPN, zobacz [jak zmienić typ routingu sieci VPN dla bramy](#how-to-change-the-vpn-routing-type-for-your-gateway).

## <a name="create-a-vpn-gateway"></a>Utwórz bramę VPN
1. W [klasycznego portalu Azure](https://manage.windowsazure.com)na **sieci** upewnij się, że w kolumnie Stan dla sieci wirtualnej jest **utworzony**.
2. W **nazwa** kolumny, kliknij nazwę sieci wirtualnej.
3. Na **pulpitu nawigacyjnego** strony, zwróć uwagę, że ta sieć wirtualna nie jest jeszcze skonfigurowana brama. Ten stan zostanie wyświetlone jako przejść przez kolejne kroki konfigurowania bramy.

![Nie utworzono bramy](./media/vpn-gateway-configure-vpn-gateway-mp/IC717025.png)

Następnie w dolnej części strony, kliknij przycisk **Tworzenie bramy**. Można wybrać dowolną *Routing statyczny* lub *routingu dynamicznego*. Wybrany typ routingu sieci VPN zależy od kilku czynników. Na przykład obsługuje urządzenia sieci VPN i tego, czy należy do obsługi połączeń punkt lokacja. Sprawdź [o urządzeniach sieci VPN do łączności sieciowej wirtualnego](vpn-gateway-about-vpn-devices.md) można zweryfikować typu routingu sieci VPN, które są potrzebne. Po utworzeniu bramy nie można zmienić typu bramy sieci VPN routingu bez usunięcia i ponownego utworzenia bramy. Gdy pojawi się monit o upewnij się, że chcesz utworzyć bramę, kliknij system **tak**.

![Typ routingu bramy sieci VPN](./media/vpn-gateway-configure-vpn-gateway-mp/IC717026.png)

Tworząc bramy zauważyć grafiki bramy na stronie zmienia się na żółty oraz mówi *Tworzenie bramy*. Może potrwać do 45 minut bramy do utworzenia. Poczekaj, aż zakończy się bramy, zanim będzie możliwe przeniesienie do przodu z innymi ustawieniami konfiguracji.

![Tworzenie bramy](./media/vpn-gateway-configure-vpn-gateway-mp/IC717027.png)

Zmiany bramy na *łączenie*, można zbierać informacje, należy dla urządzenia sieci VPN.

![Połączenie bramy](./media/vpn-gateway-configure-vpn-gateway-mp/IC717028.png)

## <a name="site-to-site-connections"></a>Połączenia typu lokacja-lokacja

### <a name="step-1-gather-information-for-your-vpn-device-configuration"></a>Krok 1. Zbierz informacje dotyczące konfiguracji urządzenia sieci VPN
Jeśli tworzysz połączenie lokacja-lokacja, po utworzeniu bramy zebrania informacji o konfiguracji urządzenia sieci VPN. Tych informacji znajduje się na **pulpitu nawigacyjnego** strony dla sieci wirtualnej:

1. **Adres IP bramy -** adresów IP można znaleźć w **pulpitu nawigacyjnego** strony. Nie można jest widoczny dopiero po zakończeniu bramy tworzenia.
2. **Klucz współużytkowany —** kliknij **Zarządzanie klucza** w dolnej części ekranu. Kliknij ikonę obok klawisz, aby skopiować go do Schowka, a następnie wklej i zapisać klucz. Ten przycisk działa tylko w przypadku, gdy istnieje jeden tunel S2S VPN. Jeśli masz wiele tuneli S2S VPN, użyj *uzyskać wirtualnych sieci bramy klucz wstępny* interfejsu API lub program PowerShell polecenia cmdlet.

![Zarządzanie kluczem](./media/vpn-gateway-configure-vpn-gateway-mp/IC717029.png)

### <a name="step-2--configure-your-vpn-device"></a>Krok 2.  Konfiguracja urządzenia sieci VPN
Połączenia typu lokacja-lokacja z siecią lokalną wymagają urządzenia sieci VPN. Nie podajemy kroków konfiguracji dla wszystkich urządzeń sieci VPN, jednak następujące linki mogą zawierać przydatne informacje:

- Aby uzyskać informacje o zgodnych urządzeniach sieci VPN, zobacz [Urządzenia sieci VPN](vpn-gateway-about-vpn-devices.md). 
- Aby uzyskać linki do ustawień konfiguracji urządzeń, zobacz [Zweryfikowane urządzenia sieci VPN](vpn-gateway-about-vpn-devices.md#devicetable). Te linki zostały podane na zasadzie największej staranności. Zawsze najlepiej jest skontaktować się z producentem urządzenia, aby uzyskać najnowsze informacje o konfiguracji.
- Aby uzyskać informacje na temat edytowania przykładów konfiguracji urządzeń, zobacz [Edytowanie przykładów](vpn-gateway-about-vpn-devices.md#editing).
- Aby zapoznać się z parametrami protokołów IPsec/IKE, zobacz [Parametry](vpn-gateway-about-vpn-devices.md#ipsec).
- Przed skonfigurowaniem urządzenia sieci VPN, którego zamierzasz użyć, sprawdź, czy istnieją dla niego [znane problemy dotyczące zgodności urządzeń](vpn-gateway-about-vpn-devices.md#known).

Podczas konfigurowania urządzenia sieci VPN potrzebne będą:

- Publiczny adres IP bramy sieci wirtualnej. Aby go sprawdzić, przejdź do bloku **Przegląd** sieci wirtualnej.
- Klucz wspólny. To ten sam klucz wspólny, który jest określany podczas tworzenia połączenia sieci VPN typu lokacja-lokacja. W naszych przykładach używamy bardzo prostego klucza wspólnego. Do użycia należy wygenerować bardziej złożony klucz.

Po skonfigurowaniu urządzenia sieci VPN można wyświetlić informacje o połączeniu zaktualizowane na stronie pulpitu nawigacyjnego sieci wirtualnej.

### <a name="step-3-verify-your-local-network-ranges-and-vpn-gateway-ip-address"></a>Krok 3. Sprawdź zakresy sieci lokalnej i adres IP bramy sieci VPN
#### <a name="verify-your-vpn-gateway-ip-address"></a>Zweryfikuj swój adres IP bramy sieci VPN
Dla bramy można się połączyć adres IP urządzenia sieci VPN musi być poprawnie skonfigurowany dla sieci lokalnej określony dla danej konfiguracji między lokalizacjami. Zazwyczaj jest to skonfigurowana w procesie konfiguracji lokacja lokacja. Jednak jeśli wcześniej używana tej sieci lokalnej z innego urządzenia lub adres IP została zmieniona dla tej sieci lokalnej, należy edytować ustawienia, aby określić poprawny adres IP bramy.

1. Aby zweryfikować swój adres IP bramy, kliknij przycisk **sieci** w okienku po lewej stronie portalu, a następnie wybierz **sieci lokalne** w górnej części strony. Zostanie wyświetlony adres bramy sieci VPN dla każdej sieci lokalnej, które zostały utworzone. Aby edytować adres IP, wybierz sieć wirtualną, a następnie kliknij przycisk **Edytuj** w dolnej części strony.
2. Na **Określ szczegóły sieci lokalnej** strony, Edytuj adres IP, a następnie kliknij strzałkę dalej w dolnej części strony.
3. Na **określić przestrzeń adresowa** kliknij znacznik wyboru w prawej dolnej, aby zapisać ustawienia.

#### <a name="verify-the-address-ranges-for-your-local-networks"></a>Sprawdź zakresy adresów dla sieci lokalnej
Poprawne przepływ ruchu za pośrednictwem bramy do lokalizacji lokalnej należy sprawdź, czy wszystkie zakresy adresów IP jest określony. Każdego zakresu musi być wymienione w Azure **sieci lokalne** konfiguracji. W zależności od konfiguracji sieci lokalnej lokalizacji może to być nieco dużych zadań. Ruch, który jest powiązany dla zawartej w wymienionych zakresów adresów IP zostaną wysłane za pośrednictwem bramy sieci VPN w sieci wirtualnej. Zakresy, które możesz listy nie muszą być zakresów prywatnych, mimo że można sprawdzić, czy konfigurację lokalnej mogą odbierać ruch przychodzący.

Aby dodać lub edytować zakresy dla sieci lokalnej, wykonaj następujące kroki:

1. Aby edytować zakresy adresów IP dla sieci lokalnej, kliknij przycisk **sieci** w okienku po lewej stronie portalu, a następnie wybierz **sieci lokalne** w górnej części strony. W portalu, najprostszym sposobem na wyświetlenie zakresów, które zostały umieszczone znajduje się na **Edytuj** strony. Aby wyświetlić zakresy, wybierz sieć wirtualną, a następnie kliknij przycisk **Edytuj** w dolnej części strony.
2. Na **Określ szczegóły sieci lokalnej** strony, nie wprowadzono żadnych zmian. Kliknij strzałkę dalej w dolnej części strony.
3. Na **określić przestrzeń adresowa** upewnij Twoje zmiany przestrzeni adresowej sieci. Następnie kliknij znacznik wyboru, aby zapisać konfigurację.

## <a name="how-to-view-gateway-traffic"></a>Jak wyświetlić ruch z bramy
Można wyświetlić bramy i bramy ruch z sieci wirtualnej **pulpitu nawigacyjnego** strony.

Na **pulpitu nawigacyjnego** strony można wyświetlić następujące:

* Ilość danych, które jest przepływających przez bramy, zarówno dane, jak i dla danych wychodzących.
* Nazwy serwerów DNS, które są określone dla sieci wirtualnej.
* Połączenie między bramą i urządzenie sieci VPN.
* Udostępniony klucz, który służy do skonfigurowania połączenia bramy do Twojego urządzenia sieci VPN.

## <a name="how-to-change-the-vpn-routing-type-for-your-gateway"></a>Sposób zmiany typu routingu VPN dla bramy
Ponieważ w niektórych konfiguracjach łączności są dostępne tylko dla niektórych typów routingu bramy, może się okazać, że trzeba będzie zmienić bramy sieci VPN typu routingu istniejącej bramy sieci VPN. Na przykład może chcesz dodać połączenie punkt lokacja do już istniejącego połączenia lokacja lokacja z bramy statyczne. Połączenia punkt lokacja wymagają bramy dynamiczne. Oznacza to skonfigurować połączenie P2S, trzeba zmienić bramy sieci VPN typu routingu ze statycznego na dynamiczny.

Jeśli musisz zmienić bramy sieci VPN typu routingu, będzie Usuń istniejącą bramę, a następnie utwórz nową bramę z nowym typem routingu. Nie trzeba usunąć całą sieć wirtualną, aby zmienić typ routingu bramy.

Przed zmianą bramy sieci VPN typu routingu, należy upewnić się, że urządzenie sieci VPN obsługuje typ routingu, który ma być używany. Aby pobrać nowe próbki konfiguracji routingu i sprawdzić wymagania dotyczące urządzeń sieci VPN, zobacz [o urządzeniach sieci VPN do łączności sieciowej wirtualnego](vpn-gateway-about-vpn-devices.md).

> [!IMPORTANT]
> Po usunięciu bramy sieci wirtualnej sieci VPN jest zwalniany wirtualne adresy IP przypisane do bramy. Podczas ponownego tworzenia bramy nowego adresu VIP jest do niego przypisany.
> 
> 

1. **Usuń istniejącą bramę sieci VPN.**
   
    Na **pulpitu nawigacyjnego** dla sieci wirtualnej, przejdź do dolnej części strony i kliknij przycisk **usunąć bramę**. Poczekaj na powiadomienie, że brama została usunięta. Po otrzymaniu powiadomienia na ekranie, że brama została usunięta, można utworzyć nowej bramy.
2. **Utwórz nową bramę sieci VPN.**
   
    Użyj procedury w górnej części strony, aby utworzyć nową bramę: [Utwórz bramę sieci VPN](#create-a-vpn-gateway).

## <a name="next-steps"></a>Następne kroki
Do sieci wirtualnej można dodać maszyny wirtualne. Zobacz artykuł [How to create a custom virtual machine](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (Tworzenie niestandardowej maszyny wirtualnej).

Jeśli chcesz skonfigurować połączenie VPN punkt lokacja, zobacz [Skonfiguruj połączenie VPN punkt lokacja](vpn-gateway-point-to-site-create.md).

