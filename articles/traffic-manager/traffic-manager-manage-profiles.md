---
title: "Zarządzanie profilami usługi Azure Traffic Manager | Microsoft Docs"
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
ms.openlocfilehash: a5164282264124835692bc72a4ab61891aa7af9d
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="manage-an-azure-traffic-manager-profile"></a>Zarządzanie profilem usługi Azure Traffic Manager

Profile usługi Traffic Manager wykorzystują metody routingu ruchu do sterowania dystrybucją ruchu do usług w chmurze lub punktów końcowych witryny sieci Web. W tym artykule opisano sposób tworzenia tych profili i zarządzania nimi.

## <a name="create-a-traffic-manager-profile"></a>Tworzenie profilu usługi Traffic Manager

Profil usługi Traffic Manager można utworzyć za pomocą witryny Azure Portal. Po utworzeniu profilu w witrynie Azure Portal można skonfigurować punkty końcowe, monitorowanie i inne ustawienia. Usługa Traffic Manager obsługuje maksymalnie 200 punktów końcowych dla profilu. Większość scenariuszy użycia wymaga jednak niewielkiej liczby punktów końcowych.

### <a name="to-create-a-traffic-manager-profile"></a>Tworzenie profilu usługi Traffic Manager

1. Z poziomu przeglądarki zaloguj się do witryny [Azure Portal](http://portal.azure.com). Jeśli jeszcze nie masz konta, możesz skorzystać z [bezpłatnej miesięcznej wersji próbnej](https://azure.microsoft.com/free/). 
2. W menu **Centrum** kliknij pozycje **Nowy** > **Sieć** > **Zobacz wszystkie**, kliknij profil usługi **Traffic Manager**, aby otworzyć blok **Tworzenie profilu usługi Traffic Manager**, a następnie kliknij przycisk **Utwórz**.
3. W bloku **Tworzenie profilu usługi Traffic Manager** podaj następujące informacje:
    1. W polu **Nazwa** podaj nazwę profilu. Ta nazwa musi być unikatowa w obrębie strefy trafficmanager.net. Na jej podstawie zostanie utworzona nazwa DNS <name>, trafficmanager.net służąca do uzyskiwania dostępu do profilu usługi Traffic Manager.
    2. W obszarze **Metoda routingu** wybierz metodę routingu **Priorytet**.
    3. W obszarze **Subskrypcja** wybierz subskrypcję, w ramach której ma zostać utworzony ten profil.
    4. W obszarze **Grupy zasobów** utwórz nową grupę zasobów, w której zostanie umieszczony ten profil.
    5. W obszarze **Lokalizacja grupy zasobów** wybierz lokalizację grupy zasobów. To ustawienie dotyczy lokalizacji grupy zasobów i nie ma wpływu na profil usługi Traffic Manager, który będzie wdrażany globalnie.
    6. Kliknij przycisk **Utwórz**.
    7. Po zakończeniu globalnego wdrażania profilu usługi Traffic Manager zostanie on wyświetlony w odpowiedniej grupie zasobów jako jeden z zasobów.

## <a name="disable-enable-or-delete-a-profile"></a>Wyłączanie, włączanie lub usuwanie profilu

Istniejący profil można wyłączyć, aby w usłudze Traffic Manager żądania użytkowników nie odwoływały się do skonfigurowanych punktów końcowych. Po wyłączeniu profilu usługi Traffic Manager profil i informacje w nim zawarte pozostają nienaruszone i można je edytować w interfejsie usługi Traffic Manager.  Działanie odwołań zostaje wznowione po ponownym włączeniu profilu. Po utworzeniu w witrynie Azure Portal profil usługi Traffic Manager zostanie automatycznie włączony. Jeśli zdecydujesz, że profil nie będzie już potrzebny, możesz go usunąć.

### <a name="to-disable-a-profile"></a>Aby wyłączyć profil

1. Jeśli używasz niestandardowej nazwy domeny, zmień rekord CNAME na internetowym serwerze DNS, tak aby nie odwoływał się on już do profilu usługi Traffic Manager.
2. Ruch przestanie być kierowany do punktów końcowych za pomocą ustawień profilu usługi Traffic Manager.
3. Z poziomu przeglądarki zaloguj się do witryny [Azure Portal](http://portal.azure.com).
2. Korzystając z paska wyszukiwania portalu, wyszukaj nazwę **profilu usługi Traffic Manager**, który chcesz zmodyfikować, a następnie kliknij profil usługi Traffic Manager w wyświetlonych wynikach wyszukiwania.
3. W bloku **Profil usługi Traffic Manager** kliknij pozycję **Przegląd**. W bloku Przegląd kliknij pozycję **Wyłącz**, a następnie potwierdź wyłączenie profilu usługi Traffic Manager.

### <a name="to-enable-a-profile"></a>Aby włączyć profil

1. Z poziomu przeglądarki zaloguj się do witryny [Azure Portal](http://portal.azure.com).
2. Korzystając z paska wyszukiwania portalu, wyszukaj nazwę **profilu usługi Traffic Manager**, który chcesz zmodyfikować, a następnie kliknij profil usługi Traffic Manager w wyświetlonych wynikach wyszukiwania.
3. W bloku **Profil usługi Traffic Manager** kliknij pozycję **Przegląd**, a następnie w bloku Przegląd kliknij pozycję **Włącz**.
5. Jeśli używasz niestandardowej nazwy domeny, utwórz rekord zasobu CNAME na internetowym serwerze DNS, aby ustawić odwołanie do nazwy domeny profilu usługi Traffic Manager.
6. Ruch zostanie ponownie skierowany do punktów końcowych.

### <a name="to-delete-a-profile"></a>Aby usunąć profil

1. Upewnij się, że rekord zasobu DNS na serwerze DNS w sieci Internet nie używa już rekordu zasobu CNAME, który wskazuje nazwę domeny profilu usługi Traffic Manager.
2. Korzystając z paska wyszukiwania portalu, wyszukaj nazwę **profilu usługi Traffic Manager**, który chcesz zmodyfikować, a następnie kliknij profil usługi Traffic Manager w wyświetlonych wynikach wyszukiwania.
3. W bloku **Profil usługi Traffic Manager** kliknij pozycję **Przegląd**. W bloku Przegląd kliknij pozycję **Usuń**, a następnie potwierdź usunięcie profilu usługi Traffic Manager.

## <a name="next-steps"></a>Następne kroki

* [Dodawanie punktu końcowego](traffic-manager-endpoints.md)
* [Konfigurowanie metody routingu opartego na priorytecie](traffic-manager-configure-priority-routing-method.md)
* [Konfigurowanie metody routingu geograficznego](traffic-manager-configure-geographic-routing-method.md) 
* [Konfigurowanie metody routingu ważonego](traffic-manager-configure-weighted-routing-method.md)
* [Konfigurowanie metody routingu opartego na wydajności](traffic-manager-configure-performance-routing-method.md)
