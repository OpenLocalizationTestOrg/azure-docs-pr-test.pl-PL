---
title: "aaaAn aplikacji serwera Proxy aplikacji trwa zbyt długo tooload | Dokumentacja firmy Microsoft"
description: "Strona obciążenia Rozwiązywanie problemów z wydajnością z powitania serwera Proxy aplikacji usługi Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 4c7a51f96840966a1d88933fa4e30f39479d8a5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="an-application-proxy-application-takes-too-long-tooload"></a>Aplikacja serwera Proxy aplikacji trwa zbyt długo tooload

W tym artykule pomocy toounderstand, dlaczego aplikacja serwera Proxy aplikacji usługi Azure AD może potrwać tooload dużo czasu i co można zrobić tooresolve ten problem.

## <a name="overview"></a>Omówienie
Pracy aplikacji, ale Zobacz długi czas oczekiwania, może mieć kilka ulepszeń pomocniczych w topologii sieci, rozważ tooimprove hello szybkości. W wersji ewaluacyjnej topologii, zobacz hello [dokumentu zagadnienia dotyczące sieci](https://docs.microsoft.com/azure/active-directory/application-proxy-network-topology-considerations).

Jeśli te zagadnienia nie pomogły, Niestety nie ma obecnie mamy dodatkowe zalecenia dotyczące dostrajania wydajności. Jako powitania serwera Proxy aplikacji usługi rozszerza toomore centrów danych, które mogą być bliżej tooyou, toosee poprawia czas oczekiwania może uruchomić bezpośrednio. w centrach toosee hello pełny wykaz danych Azure, zostanie wyświetlony hello [stronę testową opóźnienia](http://www.azurespeed.com/Azure/Latency). 

Witaj centrach danych o powitania serwera Proxy aplikacji usługi można znaleźć z hello [narzędzia Test porty łącznika](https://aadap-portcheck.connectorporttest.msappproxy.net/). 

## <a name="feedback-on-application-proxy-data-center-locations"></a>Opinię na lokalizacje centrum danych serwer Proxy aplikacji 
Może to być centra danych platformy Azure, które jeszcze nie zawierają serwera Proxy aplikacji, ale może spowodować tooa poprawy opóźnienia doskonały dla Ciebie. Lokalizacja w centrum danych Hello < aadapfeedback@microsoft.com > , możemy użyć tooplan Twojej opinii, jak firma Microsoft Rozwiń.

Firma Microsoft pracuje nad pewne dodatkowe możliwości, które zwiększyć czas oczekiwania hello dzierżawcami, które są aktualnie długie opóźnienia i można się dokumentacji tooshare po dostępne.

## <a name="next-steps"></a>Następne kroki
[Praca z istniejącym lokalnych serwerów proxy](application-proxy-working-with-proxy-servers.md)
