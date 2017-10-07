---
title: "aaaMonitor aplikacji w usłudze Azure App Service | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomonitor aplikacji w usłudze Azure App Service przy użyciu hello portalu Azure."
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: d273da4e-07de-48e0-b99d-4020d84a425e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/07/2016
ms.author: byvinyal
ms.openlocfilehash: 80d5a466102a894a49d04ae35aa54cc1d05a58df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-monitor-apps-in-azure-app-service"></a>Porady: monitorować aplikacje w usłudze aplikacji Azure
[Usługi aplikacji](http://go.microsoft.com/fwlink/?LinkId=529714) oferuje wbudowane funkcje monitorowania w hello [Azure Portal](https://portal.azure.com).
Dotyczy to również hello możliwości tooreview **przydziały** i **metryki** dla aplikacji, a także hello planu usługi aplikacji, ustawianie **alerty** i nawet **skalowanie** automatycznie w oparciu o te metryki.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="understanding-quotas-and-metrics"></a>Opis przydziałów i metryki
### <a name="quotas"></a>Przydziały
Aplikacje hostowane w usłudze App Service są podmiotu toocertain *limity* z użyciem zasobów. Witaj limity są definiowane przez hello **planu usługi aplikacji** skojarzone z aplikacją hello.

Jeśli aplikacja hello jest obsługiwana w **wolne** lub **Shared** planowanie, a następnie wynika z limitów hello hello zasobów można używać aplikacji hello **przydziały**.

Jeśli aplikacja hello jest obsługiwana w **podstawowe**, **standardowe** lub **Premium** planowanie, a następnie limity hello mogą używać zasobów hello są ustawiane przez hello **rozmiar** (Mały, Średni, duża) i **wystąpienia licznika** (1, 2, 3,...) z hello **planu usługi aplikacji**.

**Przydziały** dla **wolne** lub **Shared** aplikacje są:

* **CPU(Short)**
  * Ilość Procesora dozwolone dla tej aplikacji w 5 minut. Ten limit przydziału ustawia ponownie co 5 minut.
* **CPU(Day)**
  * Całkowita ilość Procesora dozwolone dla tej aplikacji w ciągu jednego dnia. Ten limit przydziału ustawia ponownie co 24 godziny, o północy czasu UTC.
* **Pamięci**
  * Całkowita ilość pamięci dozwolone dla tej aplikacji.
* **Przepustowość**
  * Całkowita ilość przepustowości wychodzącej dozwolone dla tej aplikacji w ciągu jednego dnia.
    Ten limit przydziału ustawia ponownie co 24 godziny, o północy czasu UTC.
* **System plików**
  * Całkowita liczba dozwoloną ilość pamięci masowej.

Witaj tylko przydział dotyczy tooapps hostowanych na **podstawowe**, **standardowe** i **Premium** jest planów **systemu plików**.

Więcej informacji na temat określonych przydziały hello, ograniczenia i funkcje dostępne dla hello różne jednostki magazynowe usługi aplikacji można znaleźć tutaj: [ograniczenia usługi subskrypcji platformy Azure](../azure-subscription-service-limits.md#app-service-limits)

#### <a name="quota-enforcement"></a>Wymuszanie przydziałów
Jeśli aplikacja w jej użycie przekracza hello **procesora CPU (short)**, **procesora CPU (dzień)**, lub **przepustowości** przydziału, a następnie hello aplikacji zostanie zatrzymana, aż do ponownego ustawia limit przydziału hello. W tym czasie wszystkie żądania przychodzące spowoduje **HTTP 403**.
![][http403]

Jeśli aplikacja hello **pamięci** przekroczony przydział, a następnie aplikacja hello zostanie ponownie uruchomiony.

Jeśli hello **Filesystem** przekroczony przydział, a następnie żadnego zapisu, operacja zakończy się niepowodzeniem, w tym zapisywania toologs.

Przydziały można zwiększyć lub usunięte z aplikacji, uaktualniając plan usługi aplikacji.

### <a name="metrics"></a>Metryki
**Metryki** zawierają informacje o aplikacji hello lub zachowanie planu usługi aplikacji.

Aby uzyskać **aplikacji**, są dostępne metryki hello:

* **Średni czas odpowiedzi**
  * Witaj Średni czas żądania tooserve aplikacji hello w ms.
* **Pamięć średni zestaw roboczy**
  * Hello średnia ilość pamięci w bazach MIB używany przez aplikację hello.
* **Czas procesora CPU**
  * Witaj ilość Procesora w sekundach wykorzystanych w ramach aplikacji hello. Aby uzyskać więcej informacji o tym, zobacz metryki: [procent vs Procesora czas procesora CPU](#cpu-time-vs-cpu-percentage)
* **Dane w**
  * Witaj ilość przychodzącego przepustowości aplikacji hello w bazach MIB.
* **Dla danych wychodzących**
  * Witaj ilość przepustowości wychodzącej dla aplikacji hello w bazach MIB.
* **Http 2xx**
  * Liczba żądań, co powoduje kod stanu http > = 200, ale < 300.
* **Http 3xx**
  * Liczba żądań, co powoduje kod stanu http > = 300, ale < 400.
* **HTTP 401**
  * Liczba żądań, co powoduje kod stanu HTTP 401.
* **HTTP 403**
  * Liczba żądań, co powoduje kod stanu HTTP 403.
* **HTTP 404**
  * Liczba żądań, co powoduje kod stanu HTTP 404.
* **HTTP 406**
  * Liczba żądań, co powoduje kod stanu HTTP 406.
* **Http 4xx**
  * Liczba żądań, co powoduje kod stanu http > = 400, ale < 500.
* **Błędy HTTP serwera**
  * Liczba żądań, co powoduje kod stanu http > = 500, ale < 600.
* **Zestaw roboczy pamięci**
  * Bieżąca ilość pamięci użytej przez aplikację hello w bazach MIB.
* **Żądania**
  * Całkowita liczba żądań, niezależnie od ich wynikowy kod stanu HTTP.

Aby uzyskać **planu usługi aplikacji**, są dostępne metryki hello:

> [!NOTE]
> Metryki planu usługi aplikacji są dostępne tylko dla planów w **podstawowe**, **standardowe** i **Premium** jednostki SKU.
> 
> 

* **Procent użycia procesora CPU**
  * Witaj średnie użycie procesora CPU we wszystkich wystąpieniach planu hello.
* **Procent pamięci**
  * Witaj średni pamięć używana we wszystkich wystąpieniach planu hello.
* **Dane w**
  * Witaj Średnia przepustowość przychodzące używane we wszystkich wystąpieniach planu hello.
* **Dla danych wychodzących**
  * Średnia Hello przepustowość we wszystkich wystąpieniach planu hello wychodzące.
* **Długość kolejki dysku**
  * Witaj średnią liczbę zarówno żądania odczytu i zapisu umieszczonych w kolejce w magazynie. Długość kolejki dysku będzie wskazywać aplikacji, która może zmniejszają należne we/wy dysku tooexcessive.
* **Długość kolejki http**
  * Witaj średnia liczba żądań HTTP, które ma toosit w kolejce hello przed są spełnione. Wysoki lub zwiększa długość kolejki HTTP jest symptomem planu obciążona.

### <a name="cpu-time-vs-cpu-percentage"></a>Wartość procentowa vs Procesora czas Procesora
<!-- toodo: Fix Anchor (#CPU-time-vs.-CPU-percentage) -->

Istnieją 2 metryk, które odzwierciedlają użycie procesora CPU. **Czas procesora CPU** i **procent użycia procesora CPU**

**Czas procesora CPU** jest przydatne dla aplikacji hostowanej w **wolne** lub **Shared** plany, ponieważ jeden z ich przydziały jest określana w minutach procesora CPU, używany przez aplikację hello.

**Procent użycia procesora CPU** na powitania drugiej jest przydatne dla aplikacji hostowanej w **podstawowe**, **standardowe** i **premium** plany, ponieważ mogą one być skalowana w poziomie i ta metryka jest dobrym wskaźnikiem hello ogólne wykorzystanie we wszystkich wystąpieniach.

## <a name="metrics-granularity-and-retention-policy"></a>Poziom szczegółowości metryki i zasady przechowywania
Metryki planu usługi aplikacji i aplikacji są rejestrowane i agregowane przez usługę hello z hello następujące zasady przechowywania i szczegółowości:

* **Minuta** metryki szczegółowości są zachowywane dla **48 godzin**
* **Godzina** metryki szczegółowości są zachowywane dla **30 dni**
* **Dzień** metryki szczegółowości są zachowywane dla **90 dni**

## <a name="monitoring-quotas-and-metrics-in-hello-azure-portal"></a>Monitorowanie przydziałów i metryki hello portalu Azure.
Możesz przejrzeć stan hello hello różnych **przydziały** i **metryki** mające wpływ na aplikację w hello [Azure Portal](https://portal.azure.com).

![][quotas]
**Przydziały** znajduje się w obszarze Ustawienia >**przydziały**. Witaj UX umożliwia zapoznanie się z: Nazwa przydziały hello (1), (2) jego interwał resetowania, (3) jego bieżący limit i (4) bieżącą wartość.

![][metrics]
**Metryki** może być dostępu bezpośrednio z bloku zasobów hello. Można również dostosować wykres hello przez: (1) **kliknij** i wybierz (2) **Edytuj wykres**.
W tym miejscu można zmienić hello (3) **zakres czasu**4 **typ wykresu**i 5 **metryki** toodisplay.  

Dowiedz się więcej o metryki tutaj: [monitorować metryki usługi](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).

## <a name="alerts-and-autoscale"></a>Alerty i skalowania automatycznego
Metryki planu aplikacji lub usługi aplikacji może podłączonymi tooalerts, toolearn więcej na ten temat, zobacz [otrzymywać powiadomienia o alertach](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

Aplikacje usługi aplikacji hostowanej w basic, standard lub premium plany usługi App Service obsługuje **skalowania automatycznego**. Dzięki temu można tooconfigure reguł, które monitorować metryki planu usługi aplikacji i można zwiększyć lub zmniejszyć liczbę wystąpień hello, zapewniając dodatkowe zasoby, zgodnie z potrzebami lub zapisywanie oszczędność pieniędzy w przypadku aplikacji hello nadmiernego udostępniania. Dowiedz się więcej o automatyczne skalowanie: [jak tooScale](../monitoring-and-diagnostics/insights-how-to-scale.md) i tutaj [najlepszych rozwiązań dotyczących skalowania automatycznego Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-best-practices.md)

> [!NOTE]
> Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service. Bez kart kredytowych i bez zobowiązań.
> 
> 

## <a name="whats-changed"></a>Co zostało zmienione
* Toohello przewodnik zmiany z tooApp witryn sieci Web usługi dla: [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

[fzilla]:http://go.microsoft.com/fwlink/?LinkId=247914
[vmsizes]:http://go.microsoft.com/fwlink/?LinkID=309169



<!-- Images. -->
[http403]: ./media/web-sites-monitor/http403.png
[quotas]: ./media/web-sites-monitor/quotas.png
[metrics]: ./media/web-sites-monitor/metrics.png
