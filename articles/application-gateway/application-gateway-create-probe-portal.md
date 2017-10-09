---
title: "aaaCreate niestandardowego sondowania — brama aplikacji w usłudze Azure - Portal Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate niestandardowego sondowania bramy aplikacji przy użyciu portalu hello"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 33fd5564-43a7-4c54-a9ec-b1235f661f97
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: 9e9309045ef33ba1010868783949b4fde31619ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-probe-for-application-gateway-by-using-hello-portal"></a>Tworzenie niestandardowych sondowania bramy aplikacji przy użyciu portalu hello

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](application-gateway-create-probe-portal.md)
> * [Azure Resource Manager — program PowerShell](application-gateway-create-probe-ps.md)
> * [Klasyczny portal Azure — program PowerShell](application-gateway-create-probe-classic-ps.md)

W tym artykule dodaniu niestandardowych sondowania tooan istniejących aplikacji bramy za pomocą hello portalu Azure. Niestandardowe sond są przydatne dla aplikacji, które mają strona sprawdzania kondycji określonych lub aplikacji, które nie mają pomyślnej odpowiedzi na powitania domyślnej aplikacji sieci web.

## <a name="before-you-begin"></a>Przed rozpoczęciem

Jeśli nie masz już istniejącą bramę aplikacji, odwiedź stronę [Utwórz bramę aplikacji](application-gateway-create-gateway-portal.md) toocreate toowork bramy aplikacji z.

## <a name="createprobe"></a>Utworzyć hello sondy

Sondy są skonfigurowane w dwóch etapach za pośrednictwem portalu hello. pierwszym krokiem Hello jest toocreate hello sondowania. W drugim kroku hello możesz dodać hello sondowania toohello ustawienia http zaplecza bramy aplikacji hello.

1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com). Jeśli nie masz już konto, możesz zarejestrować się w celu [bezpłatna miesięczna wersja próbna](https://azure.microsoft.com/free)

1. W portalu Azure okienko Ulubione hello kliknij pozycję wszystkie zasoby. Kliknij przycisk brama aplikacji hello w hello wszystkich bloku zasobów. Jeśli subskrypcja hello, już ma kilka zasobów, można wprowadzić partners.contoso.net w hello filtru według nazwy... Brama aplikacji w polu tooeasily dostępu hello.

1. Kliknij przycisk **sondy** i kliknij przycisk hello **Dodaj** tooadd przycisk badanie.

  ![Dodaj sondowania bloku z informacjami o wypełnione][1]

1. Na powitania **sondy kondycji Dodaj** bloku wypełniania hello wymagane informacje dotyczące badania hello, a po zakończeniu kliknij przycisk **OK**.

  |**Ustawienie** | **Wartość** | **Szczegóły**|
  |---|---|---|
  |**Nazwa**|customProbe|Ta wartość jest sondowania toohello przyjazną nazwę, która jest dostępna w portalu hello.|
  |**Protokół**|HTTP lub HTTPS | używa protokołu Hello hello sondy kondycji.|
  |**Host**|tj contoso.com|Ta wartość jest nazwa hosta hello jest używany do badania hello. Dotyczy tylko wtedy, gdy obejmujący wiele lokacji jest skonfigurowany dla bramy aplikacji, w przeciwnym razie użyj '127.0.0.1'. Ta wartość jest inna niż nazwa hosta maszyny Wirtualnej hello.|
  |**Ścieżka**|/ lub inną ścieżkę|Witaj pozostałej części hello pełny adres url dla hello sondy niestandardowych. Nieprawidłowa ścieżka zaczyna się od '/'. Hello domyślną ścieżkę http://contoso.com po prostu użyj "/" |
  |**Interwał (w sekundach)**|30|Jak często hello sondy jest uruchamiany toocheck kondycji. Nie jest zalecane hello tooset mniejszą niż 30 sekund.|
  |**Limit czasu (w sekundach)**|30|Hello ilość czasu sondowania hello czeka przed przekroczeniem limitu czasu. wystarczająco wysoka, może być utworzona strona health zaplecza hello tooensure wywołanie http toobe potrzeb interwał limitu czasu Hello jest dostępna.|
  |**Próg złej kondycji**|3|Liczba nieudanych prób toobe określana jako zła. Próg 0 oznacza, że jeśli zaplecza hello niepowodzenia sprawdzania kondycji jest określany złej kondycji od razu.|

  > [!IMPORTANT]
  > Nazwa hosta Hello nie jest hello taka sama jak nazwa serwera. Ta wartość jest hello nazwę hosta wirtualnego hello uruchomionych na serwerze aplikacji hello. Sonda Hello są wysyłane toohttp: / /(host name):(port from httpsetting)/urlPath

## <a name="add-probe-toohello-gateway"></a>Dodaj bramę toohello sondy

Obecnie hello sondowania został utworzony, jest tooadd czas jego toohello bramy. Ustawienia http zaplecza hello bramy aplikacji hello są ustawienia sondy.

1. Kliknij przycisk **ustawienia HTTP** na bramie aplikacji hello, toobring się blok konfiguracji powitania kliknij hello bieżące ustawienia http zaplecza na liście w oknie hello.

  ![Okno ustawień protokołu HTTPS][2]

1. Na powitania **appGatewayBackEndHttpSettings** bloku ustawienia, hello wyboru **sondowania niestandardowych użyj** wyboru i wybierz utworzony w hello sondowania hello [sondowania hello Utwórz](#createprobe) sekcji na powitania **sondowania niestandardowe** listy rozwijanej.
Po zakończeniu kliknij przycisk **zapisać** i hello ustawienia są stosowane.

Witaj domyślnego badania sprawdza hello domyślnej aplikacji sieci web toohello dostępu. Teraz, gdy utworzono niestandardowe sondowania, bramy aplikacji hello używa hello niestandardowa ścieżka zdefiniowana toomonitor kondycji hello serwerów wewnętrznej bazy danych. Oparte na kryteriach hello, które zostało zdefiniowane, bramy aplikacji hello sprawdza hello ścieżce określonej w hello sondowania. Jeśli hello wywołać toohost:Port / ścieżki nie może zwracać HTTP 200 399 stanu odpowiedzi, powitania serwera są wykonywane poza obrotu po osiągnięciu hello próg złej kondycji. Sondowanie jest kontynuowane od hello toodetermine wystąpienia w złej kondycji, kiedy dobrej kondycji się ponownie. Po dodaniu wystąpienia hello puli serwera zapasowego toohealthy ruchu rozpoczyna się ponownie przechodzenia tooit i toohello sondowania wystąpienia jest kontynuowane od użytkownika określonego interwału normalnie.

## <a name="next-steps"></a>Następne kroki

toolearn tooconfigure odciążanie protokołu SSL z bramy aplikacji Azure, zobacz temat [skonfigurować odciążanie protokołu SSL](application-gateway-ssl-portal.md)

[1]: ./media/application-gateway-create-probe-portal/figure1.png
[2]: ./media/application-gateway-create-probe-portal/figure2.png

