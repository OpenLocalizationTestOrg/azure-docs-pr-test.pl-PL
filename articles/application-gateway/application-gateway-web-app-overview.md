---
title: "aaaOverview wstecz wielodostępne kończy się wraz z bramy aplikacji Azure | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera omówienie obsługi bramy aplikacji hello dla wielu dzierżawców zaplecza."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: 
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: gwallace
ms.openlocfilehash: b7da8c9c68e34bd83ad2b828fab62c00caea354a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="application-gateway-support-for-multi-tenant-back-ends"></a>Obsługa wielodostępnych zapleczy w usłudze Application Gateway

Usługa Azure Application Gateway obsługuje zestawy skalowania maszyn wirtualnych, interfejsy sieciowe, publiczne/prywatne adresy IP i w pełni kwalifikowane nazwy domeny (FQDN, fully qualified domain name) w ramach swoich pul zaplecza. Domyślnie bramy aplikacji nie zmienia hello przychodzące nagłówek hosta HTTP z powitania klienta i wysyła hello nagłówka niezmienionym toohello zaplecza. Istnieje wiele usług takich jak [Azure Web Apps](../app-service-web/app-service-web-overview.md) i [zarządzanie interfejsami API](../api-management/api-management-key-concepts.md) polegać na określonym hoście nagłówek lub SNI rozszerzenia tooresolve toohello właściwego punktu końcowego, się na wielodostępną. Brama aplikacji w obsługuje teraz hello możliwości użytkowników toooverwrite hello przychodzące hosta nagłówka HTTP na podstawie ustawień zaplecza HTTP hello. Ta funkcja umożliwia obsługę wielodostępnych zapleczy usług Azure Web Apps i API Management. Ta funkcja jest dostępna zarówno hello standard, jak i SKU zapory aplikacji sieci Web. Wielodostępne zaplecza pomocy technicznej również współpracuje z SSL zakończenia i na końcu tooend SSL scenariuszy.

![Scenariusz aplikacji internetowej](./media/application-gateway-web-app-overview/scenario.png)

Ustawienia HTTP hello toospecify możliwości Hello zastąpienie hosta nie jest zdefiniowany i mogą można ponownie zastosowane tooany kończyć puli podczas tworzenia reguł. Wielodostępne wstecz kończy się następujące dwa sposoby zastępowanie nagłówka hosta i rozszerzeń SNI hello pomocy technicznej.

1. Witaj możliwości tooset hello host name tooa stałej wartości w hello ustawienia HTTP. Ta funkcja zapewnia nagłówka hosta hello jest zastępowany toothis wartość dla wszystkich puli ruchu toohello zaplecza, gdy są stosowane ustawienia hello HTTP. Podczas korzystania z końcowego tooend SSL, ta nazwa przesłoniętych hosta jest używana w hello SNI rozszerzenia. Ta funkcja umożliwia realizację scenariuszy, w którym farmy puli zaplecza oczekuje nagłówek hosta, który różni się od hello przychodzące nagłówek hosta klienta.

2. Witaj możliwości tooderive hello nazwy hosta z hello adres IP lub nazwę FQDN członków puli zaplecza hello. Ustawienia HTTP także podać nazwę hosta hello toopick opcji z członka puli zaplecza nazwy FQDN, jeśli skonfigurowana przy użyciu nazwy hosta tooderive opcji powitania od elementu członkowskiego puli zaplecza poszczególnych. Podczas korzystania z końcowego tooend SSL, tę nazwę hosta jest pochodną hello nazwy FQDN i jest używany w hello SNI rozszerzenia. Ta funkcja umożliwia obsługę scenariuszy, gdzie puli zaplecza może mieć dwóch lub więcej wielodostępne PaaS usług takich jak aplikacje sieci web platformy Azure i członek tooeach nagłówka hosta hello żądania zawiera nazwę hosta hello pochodzi od nazwy FQDN.

> [!NOTE]
> W obu hello poprzedzających przypadków hello ustawienia dotyczą tylko hello zachowanie ruchu sieciowego na żywo i nie hello zachowanie sondy kondycji. Niestandardowe już sondy Obsługa hello możliwości toospecify nagłówka hosta w konfiguracji sondowania hello. Niestandardowe sond teraz obsługują także hello możliwości tooderive hello hosta nagłówka zachowanie z hello obecnie skonfigurowane ustawienia protokołu HTTP. Tę konfigurację można określić za pomocą hello `PickHostNameFromback endAddress` parametr w konfiguracji sondowania hello. Do zakończenia tooend funkcji toowork zarówno hello sondowania i ustawienia HTTP hello muszą być zmodyfikowane tooreflect hello prawidłowej konfiguracji.

Dzięki tej możliwości klientów Określ opcje hello w ustawieniach protokołu HTTP hello i niestandardowych sondy toohello odpowiednia konfiguracja. To ustawienie jest następnie powiązane odbiornika tooa i z powrotem kończyć puli przy użyciu reguły.

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak tooset się bramę aplikacji z aplikacją sieci web jako kopii kończyć członka puli odwiedzając: [Konfigurowanie aplikacji usługi aplikacje sieci web z bramy aplikacji](application-gateway-web-app-powershell.md)
