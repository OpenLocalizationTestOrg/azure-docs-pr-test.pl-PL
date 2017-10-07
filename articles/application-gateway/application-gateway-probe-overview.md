---
title: "Omówienie monitorowania bramy aplikacji Azure aaaHealth | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o hello funkcji monitorowania w bramy aplikacji Azure"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7eeba328-bb2d-4d3e-bdac-7552e7900b7f
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/14/2016
ms.author: gwallace
ms.openlocfilehash: 5091d80394a354ff849ce7ccee8cc9d2fd0456db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="application-gateway-health-monitoring-overview"></a>Omówienie monitorowania kondycji bramy aplikacji

Azure Application Gateway domyślnie monitoruje kondycję hello wszystkich zasobów w jego puli zaplecza i automatycznie usuwa dowolnego zasobu z puli hello określana jako zła. Brama aplikacji w nadal toomonitor hello złej kondycji wystąpień i dodaje je kopii toohello dobrej kondycji puli zaplecza po udostępnieniu i sondy toohealth odpowiedź. Brama aplikacji w wysyła hello sondy kondycji z hello tego samego portu, który jest zdefiniowany w ustawieniach protokołu HTTP zaplecza hello. Ta konfiguracja zapewnia, że tej sondy hello testuje hello sam port, że klienci będą stosowane tooconnect toohello wewnętrznej bazy danych.

![przykład sondowania bramy aplikacji][1]

W dodatku toousing domyślnej sondy monitorowanie kondycji, można również dostosować toosuit sondy kondycji hello wymagań aplikacji. W tym artykule omówiono domyślnych i sondy kondycji niestandardowych.

> [!NOTE]
> Jeśli istnieje grupa NSG podsieci bramy aplikacji, zakresy portów 65503 65534 powinien zostać otwarty w podsieci bramy aplikacji hello dla ruchu przychodzącego. Te porty są wymagane dla toowork interfejsu API kondycji hello w wewnętrznej bazie danych.

## <a name="default-health-probe"></a>Domyślnej funkcji badania kondycji

Bramy aplikacji automatycznie konfiguruje domyślnego badania kondycji, konfigurując nie żadnej konfiguracji niestandardowej sondowania. monitorowanie zachowania Hello działa przez adresy IP toohello żądania HTTP skonfigurowane dla puli zaplecza hello. Dla domyślnej sondy Jeśli ustawienia http zaplecza hello są skonfigurowane dla protokołu HTTPS, sondy hello używa jako kondycję dobrze tootest zapleczy hello HTTPS.

Na przykład: Konfigurowanie aplikacji bramy toouse serwerami zaplecza A, B i C tooreceive HTTP ruchu sieciowego na porcie 80. Monitorowanie kondycji domyślne Hello testy hello trzy serwery co 30 sekund na dobrej kondycji odpowiedź HTTP. Dobrej odpowiedzi HTTP ma [kod stanu](https://msdn.microsoft.com/library/aa287675.aspx) między 200 i 399.

Jeśli serwer A hello domyślnej sondy wyboru nie powiedzie się, bramy aplikacji hello spowoduje usunięcie jej z puli zaplecza, a ruch sieciowy zatrzymuje przepływu toothis serwera. Witaj domyślnego badania będzie nadal toocheck serwera co 30 sekund. Serwer A odpowiada pomyślnie tooone żądania z domyślnego badania kondycji, jest dodawany ponownie jako pula zaplecza toohello dobrej kondycji i ruchu nawiązaniu toohello serwer ponownie.

### <a name="default-health-probe-settings"></a>Domyślne ustawienia sondy kondycji

| Właściwość sondy | Wartość | Opis |
| --- | --- | --- |
| Sonda adresu URL |http://127.0.0.1:\<portu\>/ |Ścieżka adresu URL |
| Interwał |30 |Interwał sondowania w sekundach |
| Limit czasu |30 |Sonda limitu czasu w sekundach |
| Próg złej kondycji |3 |Badania liczby ponownych prób. serwera zaplecza Hello jest oznaczony w dół po licznik awarii kolejnych sondowania hello osiągnie hello próg złej kondycji. |

> [!NOTE]
> Witaj port jest hello sam port jako ustawienia HTTP zaplecza hello.

Witaj domyślnego badania sprawdza tylko http://127.0.0.1:\<portu\> toodetermine stan kondycji. Jeśli konieczne tooconfigure hello kondycji sondowania toogo tooa niestandardowy adres URL lub zmodyfikuj inne ustawienia, należy użyć niestandardowego sond zgodnie z opisem w hello następujące kroki:

## <a name="custom-health-probe"></a>Sondy kondycji niestandardowych

Niestandardowe sond pozwalają toohave większą kontrolę nad hello monitorowanie kondycji. Podczas korzystania z niestandardowego sond, można skonfigurować interwał sondowania powitania hello tootest adresu URL i ścieżki i ile tooaccept odpowiedzi nie powiodło się przed oznaczeniem wystąpienia puli zaplecza hello swój stan jako niezdrowy.

### <a name="custom-health-probe-settings"></a>Ustawienia sondy kondycji niestandardowych

Witaj Poniższa tabela zawiera definicje dla właściwości hello sondy kondycji niestandardowych.

| Właściwość sondy | Opis |
| --- | --- |
| Nazwa |Nazwa sondy hello. Ta nazwa jest sonda toohello toorefer używane ustawienia HTTP zaplecza. |
| Protokół |Protokół używany toosend hello sondowania. Sonda Hello używa protokołu hello zdefiniowanego w ustawieniach protokołu HTTP zaplecza hello |
| Host |Sonda hello toosend nazwy hosta. Dotyczy tylko wtedy, gdy obejmujący wiele lokacji jest skonfigurowany dla bramy aplikacji, w przeciwnym razie użyj '127.0.0.1'. Ta wartość jest inna niż nazwa hosta maszyny Wirtualnej. |
| Ścieżka |Ścieżka względna hello sondy. prawidłowa ścieżka Hello rozpoczyna się od '/'. |
| Interwał |Interwał sondy w sekundach. Ta wartość jest hello odstęp czasu między dwa kolejne sondy. |
| Limit czasu |Badania limitu czasu w sekundach. Jeśli w tym czasie limitu czasu nie odebrano prawidłowej odpowiedzi, hello sondowania jest oznaczony jako nie powiodło się.  |
| Próg złej kondycji |Badania liczby ponownych prób. serwera zaplecza Hello jest oznaczony w dół po licznik awarii kolejnych sondowania hello osiągnie hello próg złej kondycji. |

> [!IMPORTANT]
> Jeśli skonfigurowano brama aplikacji w jednej lokacji, przez domyślny hello hosta należy określać nazwy jako "127.0.0.1", chyba że w przeciwnym razie skonfigurowane w niestandardowych sondowania.
> Dla odwołania do badania niestandardowe są wysyłane za\<protokołu\>://\<hosta\>:\<portu\>\<ścieżki\>. Witaj port używany będzie hello tego samego portu, zgodnie z definicją w ustawienia HTTP zaplecza hello.

## <a name="next-steps"></a>Następne kroki
Po szkoleniowe dotyczące monitorowania kondycji aplikacji bramy, można skonfigurować [sondy kondycji niestandardowych](application-gateway-create-probe-portal.md) w portalu Azure hello lub [sondy kondycji niestandardowych](application-gateway-create-probe-ps.md) przy użyciu programu PowerShell i hello Azure Resource Manager model wdrażania.

[1]: ./media/application-gateway-probe-overview/appgatewayprobe.png
