---
title: "profile Menedżera ruchu Azure aaaManage | Dokumentacja firmy Microsoft"
description: "Ten artykuł ułatwia tworzenie, wyłączanie, włączanie i usuwanie profilu usługi Azure Traffic Manager."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: f06e0365-0a20-4d08-b7e1-e56025e64f66
ms.service: traffic-manager
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/10/2017
ms.author: kumud
ms.openlocfilehash: 0c6ab0c451581d039514a9de0b525b3937e45a85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-traffic-manager-profile"></a>Zarządzanie profilem usługi Azure Traffic Manager

Profilów usługi Traffic Manager przy użyciu routingu ruchu metody toocontrol hello dystrybucji ruchu usługi w chmurze tooyour lub punktów końcowych witryny sieci Web. W tym artykule opisano sposób toocreate tych profilów i zarządzania nimi.

## <a name="create-a-traffic-manager-profile"></a>Tworzenie profilu usługi Traffic Manager

Można utworzyć profilu usługi Traffic Manager przy użyciu hello portalu Azure. Po utworzeniu profilu, można skonfigurować w portalu Azure hello punkty końcowe, monitorowanie i inne ustawienia. Obsługuje punktów końcowych too200 dla profilu Menedżera ruchu. Większość scenariuszy użycia wymaga jednak niewielkiej liczby punktów końcowych.

### <a name="toocreate-a-traffic-manager-profile"></a>toocreate profilu Menedżera ruchu

1. W przeglądarce, zaloguj się toohello [portalu Azure](http://portal.azure.com). Jeśli jeszcze nie masz konta, możesz skorzystać z [bezpłatnej miesięcznej wersji próbnej](https://azure.microsoft.com/free/). 
2. Na powitania **Centrum** menu, kliknij przycisk **nowy** > **sieci** > **zobaczyć wszystkie**, kliknij przycisk **ruchu Menedżer** hello tooopen profilu **profilu usługi Traffic Manager utwórz** bloku, następnie kliknij przycisk **Utwórz**.
3. Na powitania **profilu usługi Traffic Manager utwórz** bloku ukończenia w następujący sposób:
    1. W polu **Nazwa** podaj nazwę profilu. Ta nazwa musi toobe unikatowa w ramach strefy trafficmanager.net hello i powoduje nazwy DNS hello <name>, trafficmanager.net, która jest używana tooaccess profil Menedżera ruchu.
    2. W **metody routingu**, wybierz pozycję hello **priorytet** metody routingu.
    3. W **subskrypcji**, wybierz hello subskrypcję toocreate tego profilu, w obszarze
    4. W **grupy zasobów**, Utwórz nowy tooplace grupy zasobów tego profilu.
    5. W **lokalizacja grupy zasobów**, wybierz lokalizację hello hello grupy zasobów. To ustawienie dotyczy lokalizacji toohello hello grupy zasobów i nie ma wpływu na powitania profilu Menedżera ruchu, który będzie wdrażany globalnie.
    6. Kliknij przycisk **Utwórz**.
    7. Po zakończeniu hello globalne wdrażania profilu usługi Traffic Manager znajduje się on w grupie zasobów odpowiednich jako jeden z zasobów hello.

## <a name="disable-enable-or-delete-a-profile"></a>Wyłączanie, włączanie lub usuwanie profilu

Dzięki tym menedżera ruchu nie odwołuje się punkty końcowe skonfigurowane toohello żądań użytkownika, można wyłączyć istniejącego profilu. Po wyłączeniu profilu usługi Traffic Manager profilu hello hello informacje zawarte w profilu hello pozostaną nienaruszone i można edytować w interfejsie usługi Traffic Manager hello.  Odwołania wznowiona po ponownym włączeniu hello profilu. Po utworzeniu profilu usługi Traffic Manager w portalu Azure hello jest automatycznie włączone. Jeśli zdecydujesz, że profil nie będzie już potrzebny, możesz go usunąć.

### <a name="toodisable-a-profile"></a>toodisable profilu

1. Jeśli korzystasz z niestandardowej nazwy domeny, należy zmienić rekord CNAME hello na internetowym serwerze DNS, które nie wskazuje tooyour profilu usługi Traffic Manager.
2. Ruch przestanie być kierowany do punktów końcowych toohello za pomocą ustawień profilu usługi Traffic Manager hello.
3. W przeglądarce, zaloguj się toohello [portalu Azure](http://portal.azure.com).
2. Na pasku wyszukiwania portalu hello, wyszukaj hello **profilu usługi Traffic Manager** nazwę mają toomodify, a następnie kliknij profil Menedżera ruchu hello hello wyniki tego hello wyświetlane.
3. W hello **profilu usługi Traffic Manager** bloku, kliknij przycisk **omówienie**, w bloku omówienie powitania kliknij **wyłączyć**i Potwierdź profil Menedżera ruchu hello toodisable.

### <a name="tooenable-a-profile"></a>tooenable profilu

1. W przeglądarce, zaloguj się toohello [portalu Azure](http://portal.azure.com).
2. Na pasku wyszukiwania portalu hello, wyszukaj hello **profilu usługi Traffic Manager** nazwę mają toomodify, a następnie kliknij profil Menedżera ruchu hello hello wyniki tego hello wyświetlane.
3. W hello **profilu Menedżera ruchu** bloku, kliknij przycisk **omówienie**, a następnie w bloku omówienie powitania kliknij pozycję **włączyć**.
5. Jeśli korzystasz z niestandardowej nazwy domeny, należy utworzyć rekord zasobu CNAME na nazwę domeny DNS w Internecie serwera toopoint toohello Twojego profilu Menedżera ruchu.
6. Ruch ponownie jest bezpośrednie toohello punktów końcowych.

### <a name="toodelete-a-profile"></a>toodelete profilu

1. Upewnij się, że hello rekord zasobu DNS na internetowym serwerze DNS nie używa już rekordu zasobu CNAME, który wskazuje toohello nazwę domeny profilu usługi Traffic Manager.
2. Na pasku wyszukiwania portalu hello, wyszukaj hello **profilu usługi Traffic Manager** nazwę mają toomodify, a następnie kliknij profil Menedżera ruchu hello hello wyniki tego hello wyświetlane.
3. W hello **profilu usługi Traffic Manager** bloku, kliknij przycisk **omówienie**, w bloku omówienie powitania kliknij **usunąć**i Potwierdź profil Menedżera ruchu hello toodelete.

## <a name="next-steps"></a>Następne kroki

* [Dodawanie punktu końcowego](traffic-manager-endpoints.md)
* [Konfigurowanie metody routingu opartego na priorytecie](traffic-manager-configure-priority-routing-method.md)
* [Konfigurowanie metody routingu geograficznego](traffic-manager-configure-geographic-routing-method.md) 
* [Konfigurowanie metody routingu ważonego](traffic-manager-configure-weighted-routing-method.md)
* [Konfigurowanie metody routingu opartego na wydajności](traffic-manager-configure-performance-routing-method.md)
