---
title: 'Konfigurowanie bramy sieci VPN: klasyczny portal: Azure | Dokumentacja firmy Microsoft'
description: "W tym artykule przedstawiono sposób konfigurowania sieci wirtualnej bramy sieci VPN i zmianę bramy sieci VPN typu routingu. Ta procedura dotyczy toohello wdrażania klasycznego modelu i hello klasycznego portalu."
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
ms.openlocfilehash: 00d2fa18bab6eb24b33ddb18113f2a557db638d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vpn-gateway-in-hello-classic-portal"></a>Konfigurowanie bramy sieci VPN w portalu klasycznym hello 
Jeśli chcesz toocreate bezpiecznego między lokalizacjami połączenie między usługą platformy Azure i Twojej lokalizacji lokalnej, należy toocreate bramy sieci wirtualnej. Brama sieci VPN jest określonego typu bramy sieci wirtualnej. W hello klasycznego modelu wdrażania, Brama sieci VPN może być jeden z dwóch typów routingu sieci VPN: statyczny lub dynamiczny. Witaj wybranego typu sieci VPN zależy od zarówno plan projektu sieci i urządzenia sieci VPN lokalne powitania ma toouse. Aby uzyskać więcej informacji o urządzeniach sieci VPN, zobacz [o urządzeniach sieci VPN](vpn-gateway-about-vpn-devices.md).

**Modele wdrażania Azure — informacje**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="configuration-overview"></a>Przegląd konfiguracji
Witaj następujących krokach objaśniono sposób konfigurowania bramy sieci VPN w portalu klasycznym hello. Ta procedura dotyczy toogateways dla sieci wirtualnych, które zostały utworzone przy użyciu hello klasycznego modelu wdrażania. Obecnie nie wszystkie hello ustawienia konfiguracji dla bramy są dostępne w hello portalu Azure. Gdy są one, zostanie utworzony nowy zestaw instrukcji, które są stosowane toohello portalu Azure.

### <a name="before-you-begin"></a>Przed rozpoczęciem
Przed skonfigurowaniem bramy, musisz najpierw toocreate sieci wirtualnej. Kroki toocreate sieci wirtualnej dla łączności między lokalizacjami, aby zapoznać [Skonfiguruj sieć wirtualną z połączenia sieci VPN typu lokacja lokacja](vpn-gateway-site-to-site-create.md), lub [Skonfiguruj sieć wirtualną z połączenia sieci VPN punkt lokacja](vpn-gateway-point-to-site-create.md). Następnie użyj hello następujące kroki tooconfigure hello VPN bramy i zbierać informacje hello potrzebne tooconfigure urządzenie sieci VPN. 

Jeśli masz już bramy sieci VPN i ma typ routingu toochange hello sieci VPN, zobacz [jak toochange hello routingu typ sieci VPN dla bramy](#how-to-change-the-vpn-routing-type-for-your-gateway).

## <a name="create-a-vpn-gateway"></a>Utwórz bramę VPN
1. W hello [klasycznego portalu Azure](https://manage.windowsazure.com), na powitania **sieci** upewnij się, że w kolumnie Stan hello dla sieci wirtualnej jest **utworzony**.
2. W hello **nazwa** kolumny, kliknij nazwę hello sieci wirtualnej.
3. Na powitania **pulpitu nawigacyjnego** strony, zwróć uwagę, że ta sieć wirtualna nie jest jeszcze skonfigurowana brama. Ten stan zostanie wyświetlone podczas wykonywania kroków tooconfigure kroki hello bramy.

![Nie utworzono bramy](./media/vpn-gateway-configure-vpn-gateway-mp/IC717025.png)

Następnie u dołu hello hello strony, kliknij przycisk **Tworzenie bramy**. Można wybrać dowolną *Routing statyczny* lub *routingu dynamicznego*. Witaj wybranego typu sieci VPN routingu zależy od kilku czynników. Na przykład obsługuje urządzenia sieci VPN i tego, czy należy toosupport połączenia punkt lokacja. Sprawdź [o urządzeniach sieci VPN do łączności sieciowej wirtualnego](vpn-gateway-about-vpn-devices.md) tooverify hello typu routingu sieci VPN, które są potrzebne. Po utworzeniu bramy hello, nie można zmienić między typami bramy sieci VPN routingu bez usunięcia i ponownego utworzenia hello bramy. Gdy hello system monit tooconfirm interesujące hello utworzone bramy, kliknij przycisk **tak**.

![Typ routingu bramy sieci VPN](./media/vpn-gateway-configure-vpn-gateway-mp/IC717026.png)

Tworząc bramy, zwróć uwagę hello bramy grafiki na stronie powitania zmiany tooyellow i mówi *Tworzenie bramy*. Może potrwać too45 minut hello toocreate bramy. Poczekaj, aż zakończy się hello bramy, zanim będzie możliwe przeniesienie do przodu z innymi ustawieniami konfiguracji.

![Tworzenie bramy](./media/vpn-gateway-configure-vpn-gateway-mp/IC717027.png)

Gdy zbyt hello zmian bramy*łączenie*, można zbierać informacje hello będą potrzebne dla urządzenia sieci VPN.

![Połączenie bramy](./media/vpn-gateway-configure-vpn-gateway-mp/IC717028.png)

## <a name="site-to-site-connections"></a>Połączenia typu lokacja-lokacja

### <a name="step-1-gather-information-for-your-vpn-device-configuration"></a>Krok 1. Zbierz informacje dotyczące konfiguracji urządzenia sieci VPN
Jeśli tworzysz połączenie lokacja-lokacja, po utworzeniu bramy hello zebrania informacji o konfiguracji urządzenia sieci VPN. Tych informacji znajduje się na powitania **pulpitu nawigacyjnego** strony dla sieci wirtualnej:

1. **Adres IP bramy -** hello adres IP znajduje się na powitania **pulpitu nawigacyjnego** strony. Nie będzie możliwe toosee dopiero po bramy zakończenia tworzenia.
2. **Klucz współużytkowany —** kliknij **Zarządzanie klucza** u dołu ekranu hello hello. Kliknij hello ikona dalej toohello klucza toocopy on tooyour Schowka, a następnie wklej i zapisać klucz hello. Ten przycisk działa tylko w przypadku, gdy istnieje jeden tunel S2S VPN. Jeśli masz wiele tuneli S2S VPN, użyj hello *uzyskać wirtualnych sieci bramy klucz wstępny* interfejsu API lub program PowerShell polecenia cmdlet.

![Zarządzanie kluczem](./media/vpn-gateway-configure-vpn-gateway-mp/IC717029.png)

### <a name="step-2--configure-your-vpn-device"></a>Krok 2.  Konfiguracja urządzenia sieci VPN
Sieć lokalną tooan połączeń lokacja-lokacja wymagają urządzenia sieci VPN. Gdy firma Microsoft nie zawierają opis etapów konfiguracji wszystkich urządzeń sieci VPN, można sprawdzić w hello następującego łącza przydatne informacje hello:

- Aby uzyskać informacje o zgodnych urządzeniach sieci VPN, zobacz [Urządzenia sieci VPN](vpn-gateway-about-vpn-devices.md). 
- Ustawienia konfiguracji toodevice łączy, zobacz [zweryfikowane urządzenia sieci VPN](vpn-gateway-about-vpn-devices.md#devicetable). Te linki zostały podane na zasadzie największej staranności. Zawsze jest najlepszym toocheck od producenta urządzenia hello najnowsze informacje dotyczące konfiguracji.
- Aby uzyskać informacje na temat edytowania przykładów konfiguracji urządzeń, zobacz [Edytowanie przykładów](vpn-gateway-about-vpn-devices.md#editing).
- Aby zapoznać się z parametrami protokołów IPsec/IKE, zobacz [Parametry](vpn-gateway-about-vpn-devices.md#ipsec).
- Przed skonfigurowaniem urządzenia sieci VPN, sprawdzić [znane problemy ze zgodnością urządzenia](vpn-gateway-about-vpn-devices.md#known) hello urządzenia sieci VPN, które mają toouse.

Podczas konfigurowania urządzenia sieci VPN, należy hello następujące elementy:

- Witaj publiczny adres IP bramy sieci wirtualnej. Możesz znaleźć to przejście toohello **omówienie** bloku dla sieci wirtualnej.
- Klucz współużytkowany. Jest to hello sam udostępniony klucz, który należy określić podczas tworzenia połączenia sieci VPN typu lokacja-lokacja. W naszych przykładach używamy bardzo prostego klucza wspólnego. Powinna generować bardziej złożone toouse klucza.

Po skonfigurowaniu urządzenia sieci VPN hello można wyświetlić informacje o połączeniu zaktualizowane na powitania strony pulpitu nawigacyjnego sieci wirtualnej.

### <a name="step-3-verify-your-local-network-ranges-and-vpn-gateway-ip-address"></a>Krok 3. Sprawdź zakresy sieci lokalnej i adres IP bramy sieci VPN
#### <a name="verify-your-vpn-gateway-ip-address"></a>Zweryfikuj swój adres IP bramy sieci VPN
Dla bramy tooconnect poprawnie, hello adres IP urządzenia sieci VPN musi być poprawnie skonfigurowany dla hello sieci lokalnej określony dla danej konfiguracji między lokalizacjami. Zazwyczaj jest to skonfigurowany podczas procesu konfiguracji lokacja lokacja hello. Jednak jeśli wcześniej używana tej sieci lokalnej z innego urządzenia lub adres IP hello została zmieniona dla tej sieci lokalnej, należy edytować hello ustawienia toospecify hello poprawne adresu IP bramy.

1. tooverify swój adres IP bramy, kliknij przycisk **sieci** na hello w okienku po lewej stronie portalu, a następnie wybierz **sieci lokalne** u góry strony hello hello. Zostanie wyświetlone powitalne adres bramy sieci VPN dla każdej sieci lokalnej, które zostały utworzone. adres IP hello tooedit, wybierz hello sieci wirtualnej i kliknij przycisk **Edytuj** u dołu hello hello strony.
2. Na powitania **Określ szczegóły sieci lokalnej** strony, Edytuj adres IP hello, a następnie kliknij strzałkę dalej hello u dołu hello hello strony.
3. Na powitania **określić przestrzeń adresową hello** kliknij znacznik wyboru hello na toosave prawym dolnym hello ustawień.

#### <a name="verify-hello-address-ranges-for-your-local-networks"></a>Sprawdź hello zakresy adresów dla sieci lokalnej
Hello tooflow poprawne ruchu za pośrednictwem hello bramy tooyour lokalnej lokalizacji należy tooverify określenia wszystkich zakresów adresów IP. Każdego zakresu musi być wymienione w Azure **sieci lokalne** konfiguracji. W zależności od konfiguracji sieci hello lokalizacji lokalnej może to być nieco dużych zadań. Ruch, który jest przeznaczony dla adres IP, który znajduje się w zakresie hello wymienione zostaną wysłane za pośrednictwem bramy VPN hello sieci wirtualnej. Witaj zakresy, że liście nie ma toobe zakresów prywatnych, mimo że można tooverify, który może odbierać konfigurację lokalnej hello ruchu przychodzącego.

zakresy hello tooadd lub edycji dla sieci lokalnej, należy użyć hello następujące kroki:

1. zakresy adresów IP hello tooedit dla sieci lokalnej, kliknij przycisk **sieci** na hello w okienku po lewej stronie portalu, a następnie wybierz **sieci lokalne** u góry hello hello strony. W portalu hello hello Najprostszym sposobem tooview hello zakresy, które zostały umieszczone znajduje się na powitania **Edytuj** strony. toosee zakresy, wybierz hello sieci wirtualnej i kliknij przycisk **Edytuj** u dołu hello hello strony.
2. Na powitania **Określ szczegóły sieci lokalnej** strony, nie wprowadzono żadnych zmian. Kliknij strzałkę dalej hello u dołu hello hello strony.
3. Na powitania **określić przestrzeń adresową hello** upewnij Twoje zmiany przestrzeni adresowej sieci. Następnie kliknij przycisk toosave znacznikiem wyboru hello konfiguracji.

## <a name="how-tooview-gateway-traffic"></a>Jak tooview bramy ruchu
Można wyświetlić bramy i bramy ruch z sieci wirtualnej **pulpitu nawigacyjnego** strony.

Na powitania **pulpitu nawigacyjnego** strony można wyświetlić następujące hello:

* Witaj ilość danych, które jest przepływających przez bramy, zarówno dane, jak i dla danych wychodzących.
* nazwy Hello hello serwerów DNS, które są określone dla sieci wirtualnej.
* Witaj połączenie między bramą i urządzenie sieci VPN.
* Hello udostępniony klucz, który jest używany tooconfigure urządzenie sieci VPN tooyour połączenia bramy.

## <a name="how-toochange-hello-vpn-routing-type-for-your-gateway"></a>Jak toochange hello routingu typ sieci VPN dla bramy
Ponieważ w niektórych konfiguracjach łączności są dostępne tylko dla niektórych typów routingu bramy, może się okazać, że należy toochange hello bramy sieci VPN routingu typ istniejącej bramy sieci VPN. Na przykład można tooadd połączenie punkt lokacja tooan już istniejącą lokacja lokacja połączenie bramy statyczne. Połączenia punkt lokacja wymagają bramy dynamiczne. Oznacza to, że tooconfigure połączeń P2S, masz toochange bramy sieci VPN typu routingu z toodynamic statycznych.

Toochange bramy sieci VPN typu routingu, należy będzie usunąć hello istniejącą bramę, a następnie utwórz nową bramę z hello nowy typ routingu. Nie trzeba toodelete hello cały toochange hello typu bramy sieci wirtualnej routingu.

Przed zmianą bramy sieci VPN typu routingu, można tooverify się, że urządzenie sieci VPN obsługuje hello typ routingu, które mają toouse. Przykłady nowej konfiguracji routingu toodownload i sprawdź wymagania dotyczące urządzeń sieci VPN, zobacz [o urządzeniach sieci VPN do łączności sieciowej wirtualnego](vpn-gateway-about-vpn-devices.md).

> [!IMPORTANT]
> Po usunięciu bramy sieci wirtualnej sieci VPN jest zwalniany hello wirtualne adresy IP przypisane toohello bramy. Podczas ponownego tworzenia bramy hello nowego adresu VIP jest przypisany tooit.
> 
> 

1. **Usuń hello istniejącą bramę sieci VPN.**
   
    Na powitania **pulpitu nawigacyjnego** dla sieci wirtualnej, przejdź toohello u dołu strony hello i kliknij przycisk **usunąć bramę**. Oczekiwanie na powiadomienie hello hello bramy został usunięty. Po otrzymaniu powiadomienia hello na ekranie powitania bramy został usunięty, można utworzyć nowej bramy.
2. **Utwórz nową bramę sieci VPN.**
   
    Procedura hello u góry hello hello strony toocreate nową bramę: [Utwórz bramę sieci VPN](#create-a-vpn-gateway).

## <a name="next-steps"></a>Następne kroki
Można dodać sieci wirtualnej tooyour maszyn wirtualnych. Zobacz [jak toocreate niestandardowych maszyny wirtualnej](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Jeśli chcesz, aby połączenia sieci VPN tooconfigure punkt do lokacji, zobacz [Skonfiguruj połączenie VPN punkt lokacja](vpn-gateway-point-to-site-create.md).

