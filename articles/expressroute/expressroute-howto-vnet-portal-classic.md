---
title: "aaaConfigure sieć wirtualną i bramę usługi ExpressRoute w klasycznym portalu hello | Dokumentacja firmy Microsoft"
description: "Ten artykuł przeprowadzi Cię przez proces konfigurowania sieci wirtualnej dla usługi przy użyciu hello klasycznego modelu wdrażania i hello klasycznego portalu."
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: 688817d9-51c8-4372-9af8-33fa098c7c5a
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/20/2016
ms.author: cherylmc
ms.openlocfilehash: dd1f6c5e85dbb3ad0a53ecd81c13b4d3f5c06e66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-for-expressroute-in-hello-classic-portal"></a>Tworzenie sieci wirtualnej dla usługi ExpressRoute w portalu klasycznym hello
Witaj opisanych w tym artykule przeprowadzi Cię przez konfigurację sieci wirtualnej i Brama sieci wirtualnej do użycia z ExpressRoute przy użyciu hello klasycznego modelu wdrażania i hello klasycznego portalu.

Jeśli szukasz instrukcje dotyczące modelu wdrażania usługi Resource Manager hello, można użyć hello następujące artykuły: [utworzyć sieć wirtualną przy użyciu programu PowerShell](../virtual-network/virtual-networks-create-vnet-arm-ps.md) i [dodać tooa VPN bramy sieci wirtualnej Menedżera zasobów dla ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**Modele wdrażania Azure — informacje**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="create-a-classic-vnet-and-gateway"></a>Tworzenie klasycznej sieci wirtualnej i bramy
Hello następujące kroki tworzenia klasycznych sieci wirtualnej i Brama sieci wirtualnej. Jeśli masz już klasycznej sieci wirtualnej, zobacz hello [skonfigurować istniejącej sieci wirtualnej klasycznego](#config) w tym artykule.

1. Zaloguj się za toohello [klasycznego portalu Azure](http://manage.windowsazure.com).
2. W hello lewym dolnym rogu ekranu hello, kliknij przycisk **nowy**. W okienku nawigacji powitania kliknij **usług sieciowych**, a następnie kliknij przycisk **sieci wirtualnej**. Kliknij przycisk **Utwórz niestandardowy** toobegin hello konfiguracji kreatora.
3. Na powitania **szczegóły sieci wirtualnych** wprowadź następujące hello:
   
   * **Nazwa** — nazwa sieci wirtualnej. Podczas wdrażania swoich wystąpień maszyn wirtualnych i PaaS, dlatego nie może być nazwa hello toomake zbyt skomplikowane, będziesz używać tej nazwy sieci wirtualnej.
   * **Lokalizacja** — lokalizacja hello jest bezpośrednio powiązane toohello fizycznej lokalizacji (regionu) tooreside Twojego zasobów (maszyn wirtualnych). Na przykład jeśli chcesz, aby hello maszyn wirtualnych, wdrażanych toobe sieci wirtualnej toothis fizycznie znajduje się w wschodnie stany USA, wybierz opcję tej lokalizacji. Nie można zmienić regionu hello skojarzonego z sieci wirtualnej, po jego utworzeniu.
4. Na powitania **serwerów DNS i połączenie z siecią VPN** strony, wprowadź hello następujące informacje, a następnie kliknij strzałkę dalej hello na powitania prawym dolnym rogu. 
   
   * **Serwery DNS** — wprowadź nazwę serwera DNS hello i adres IP lub wybierz menu skrótów hello wcześniej zarejestrowanego serwera DNS. To ustawienie nie powoduje jednak utworzenia serwera DNS. Pozwala ona serwery DNS hello toospecify mają toouse do rozpoznawania nazw dla tej sieci wirtualnej.
   * **Połączenie lokacja-lokacja** — wybierz tę opcję hello wyboru **skonfigurowania sieci VPN lokacja lokacja**.
   * **ExpressRoute** — wybierz hello wyboru **ExpressRoute użyj**. Ta opcja jest dostępna tylko, jeśli wybrano **skonfigurowania sieci VPN lokacja-lokacja**.
   * **Sieci lokalnej** — są wymagane toohave lokacji sieci lokalnej w przypadku połączeń ExpressRoute. Jednak w przypadku hello połączenia ExpressRoute, prefiksy adresów hello określono hello lokalnej lokacji sieciowej zostaną zignorowane. Zamiast tego prefiksy adresów hello anonsowany tooMicrosoft za pośrednictwem hello obwodu ExpressRoute będzie służyć do celów routingu.<BR>Jeśli masz już sieć lokalną utworzone dla połączenia ExpressRoute, zostanie ona wybrana z listy rozwijanej hello. Jeśli nie, wybierz **Określ sieć lokalną**.
5. Witaj **połączenie lokacja-lokacja** strona jest wyświetlana, jeśli został wybrany w poprzednim kroku hello toospecify sieci lokalnej. tooconfigure sieci lokalnej, wprowadzić hello następujące informacje, a następnie kliknij strzałkę dalej hello. 
   
   * **Nazwa** — nazwa hello ma toocall lokalne lokacji sieciowej (lokalnego).
   * **Przestrzeń adresowa** — w tym początkowy adres IP i CIDR (liczba adresów). Można określić żadnych zakres adresów, tak długo, jak jego nie nakłada się hello zakres adresów dla sieci wirtualnej. Zazwyczaj to określić hello zakresy adresów dla sieci lokalnej, ale w przypadku hello ExpressRoute, te ustawienia nie są używane. Jednak to ustawienie jest wymagany w sieci lokalnej hello toocreate kolejności, korzystając z portalu klasycznego hello.
   * **Dodawanie przestrzeni adresów** — to ustawienie nie jest ważna w przypadku połączeń ExpressRoute.
6. Na powitania **przestrzeniami adresów sieci wirtualnej** strony, wprowadź hello następujące informacje, a następnie kliknij znacznik wyboru hello na tooconfigure prawym dolnym hello sieci. 
   
   * **Przestrzeń adresowa** — tym uruchamianie IP i adres count. Upewnij się, że przestrzenie adresowe hello, które określisz nie nakłada przestrzeni adresowych hello wyposażonych w sieci lokalnej.
   * **Dodaj podsieć** — w tym uruchamianie adresów IP i liczba adresów. Dodatkowe podsieci nie są wymagane.
   * **Dodaj podsieć bramy** -kliknij podsieć bramy hello tooadd. podsieć bramy Hello jest używany tylko dla bramy sieci wirtualnej hello i jest wymagany dla tej konfiguracji.<BR>Witaj bramy podsieci CIDR (liczba adresów) dla usługi ExpressRoute musi być /28 lub większy (/ 27, / 26 itp.). Umożliwia to za mało adresów IP w tej podsieci tooallow hello konfiguracji toowork. W portalu klasycznym hello Jeśli wybrano hello wyboru toouse ExpressRoute, hello portal określa podsieć bramy z /28.  Nie można dostosować liczba adresów CIDR hello w portalu klasycznym hello. podsieć bramy Hello będą wyświetlane jako **bramy** w portalu klasycznym hello, mimo że hello rzeczywista nazwa hello podsieć bramy, która jest tworzona jest rzeczywiście **GatewaySubnet**. Ta nazwa można wyświetlić przy użyciu programu PowerShell lub w hello portalu Azure.
7. Kliknij przycisk sieci wirtualnej zostanie rozpoczęta toocreate i hello znacznikiem wyboru w hello u dołu strony hello. Po zakończeniu wykonywania, zobaczysz **utworzony** kategorii **stan** na powitania **sieci** w portalu klasycznym hello na stronie.

## <a name="gw"></a>Utwórz bramę hello
1. Na powitania **sieci** strony, kliknij przycisk hello sieci wirtualnej, który został właśnie utworzony, a następnie kliknij przycisk **pulpitu nawigacyjnego** u góry hello hello strony.
2. Na dole hello hello **pulpitu nawigacyjnego** kliknij przycisk **Tworzenie bramy** i wybierz **routingu dynamicznego**. Kliknij przycisk **tak** tooconfirm, które mają toocreate bramy.
3. Po uruchomieniu bramy hello tworzenie zobaczysz komunikat, dzięki czemu masz pewność, że tej bramy hello została uruchomiona. Może potrwać too45 minut hello toocreate bramy.
4. Połącz obwodu tooa sieci. Wykonaj instrukcje hello w artykule hello [jak toolink sieci wirtualnych tooExpressRoute obwodów](expressroute-howto-linkvnet-classic.md).

## <a name="config"></a>Konfigurowanie klasycznego istniejącej sieci wirtualnej dla usługi ExpressRoute
Jeśli masz już klasycznej sieci wirtualnej, można skonfigurować go tooconnect tooExpressRoute w portalu klasycznym hello. Ustawienia Hello są hello sam jako sekcje hello powyżej, więc odczytu za pomocą tych sekcji toobecome zapoznać się z hello wymagane ustawienia. Jeśli toocreate coexisting połączenie ExpressRoute/lokacja-lokacja, zobacz [w tym artykule](expressroute-howto-coexist-classic.md) hello czynności. Są one różne od hello kroków w tym artykule.

1. Należy korzystać z sieci lokalnej hello toocreate przed zaktualizowaniem hello pozostałe ustawienia sieci wirtualnej. toocreate nowe sieciach lokalnych, co jest wymagane podczas konfigurowania usługi ExpressRoute za pośrednictwem portalu klasycznego hello, kliknij przycisk **nowy** ** > ** **usług sieciowych** ** > ** **Sieci wirtualnej** ** > ** **sieci lokalnej Dodaj**. Wykonaj hello kreatora kroki toocreate hello lokalnej sieci.
2. Użyj **Konfiguruj** strony tooupdate hello reszty hello ustawienia dla sieci wirtualnej i tooassociate hello sieci wirtualnej toohello sieci lokalnej.
3. Po skonfigurowaniu ustawień hello, przejdź toohello [Utwórz bramę hello](#gw) sekcji tego artykułu toocreate hello bramy.

## <a name="next-steps"></a>Następne kroki
* Sieć wirtualna tooyour tooadd maszyn wirtualnych, zobacz [ścieżki szkoleniowe dotyczące maszyn wirtualnych](https://azure.microsoft.com/documentation/learning-paths/virtual-machines/).
* Więcej informacji na temat usługi ExpressRoute toolearn, zobacz hello [omówienie ExpressRoute](expressroute-introduction.md).

