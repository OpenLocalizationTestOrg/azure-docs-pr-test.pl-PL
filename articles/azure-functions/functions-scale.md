---
title: "Azure planów zużycia funkcje i usługi App Service | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak usługi Azure Functions skaluje na potrzeby obciążeń sterowanego zdarzeniami."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "usługa Azure Functions, funkcje, przetwarzanie zdarzeń, elementy webhook, obliczanie dynamiczne, architektura bez serwera"
ms.assetid: 5b63649c-ec7f-4564-b168-e0a74cb7e0f3
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/12/2017
ms.author: glenga
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 70e77e09b2e2116153159167af61776398904a3c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-consumption-and-app-service-plans"></a>Azure planów zużycia funkcje i usługi aplikacji 

## <a name="introduction"></a>Wprowadzenie

Można uruchomić usługi Azure Functions w dwóch różnych trybach: plan zużycia i plan usługi aplikacji Azure. Plan zużycie automatycznie przydzieli moc obliczeniową, gdy kod działa, skaluje się wymagane do obsługi obciążenia, a następnie skalowany w dół, gdy kodu nie jest uruchomiona. Tak nie trzeba płacić za maszyny wirtualne w stanie bezczynności i nie trzeba było wydajność rezerwowa z wyprzedzeniem. Ten artykuł skupia się na plan zużycia. Aby uzyskać szczegółowe informacje dotyczące sposobu działania plan usługi aplikacji, zobacz [szczegółowe omówienie planów usługi aplikacji Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md). 

Jeśli nie znasz usługi Azure Functions, zobacz [Azure Functions — omówienie](functions-overview.md).

Podczas tworzenia aplikacji funkcji, należy skonfigurować plan hostingu dla funkcji, które zawiera aplikację. W trybie wystąpienia *hosta usługi Azure Functions* wykonuje funkcje. Typ kontrolki plan:

* Jak wystąpień hosta jest skalowana w poziomie.
* Zasoby, które są dostępne dla każdego hosta.

Obecnie musisz wybrać typ planu podczas tworzenia aplikacji funkcji. Nie można zmienić go później. 

Możesz skalować między warstwami na plan usługi aplikacji. W planie użycia usługi Azure Functions obsługuje automatycznie alokacji zasobów.

## <a name="consumption-plan"></a>Plan Zużycie

Podczas korzystania z planu zużycia, wystąpienia usługi Azure Functions hosta są dynamicznie dodawane i usuwane zależności od liczby zdarzeń przychodzących. Ten plan skaluje automatycznie, a użytkownik naliczane są opłaty za zasoby obliczeniowe tylko wtedy, gdy są uruchomione funkcji. Na plan użycie funkcji można uruchomić maksymalnie 10 minut. 

> [!NOTE]
> Domyślny limit czasu dla funkcji w planie zużycie wynosi 5 minut. Wartość można zwiększyć do 10 minut dla aplikacji funkcja, zmieniając właściwość `functionTimeout` w [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).

Rozliczenia jest oparta na czas wykonywania i używanej pamięci, i jest agregowana przez wszystkie funkcje w aplikacji funkcji. Aby uzyskać więcej informacji, zobacz [usługi Azure Functions cennikiem].

Plan zużycie jest ustawieniem domyślnym i oferuje następujące korzyści:
- Płać tylko wtedy, gdy uruchomione są funkcji.
- Skalowanie w poziomie automatycznie, nawet w okresie wysoki obciążenia.

## <a name="app-service-plan"></a>Plan usługi App Service

W planie usługi aplikacji — warstwa aplikacji funkcji Uruchom na dedykowanych maszynach wirtualnych na podstawowa, standardowa i Premium SKU, podobnie jak aplikacje sieci Web. Dedykowanych maszyn wirtualnych są przydzielone do aplikacji usługi aplikacji, co oznacza, że na hoście funkcji zawsze działa.

Należy wziąć pod uwagę plan usługi aplikacji w następujących przypadkach:
- Masz istniejący, niedostatecznie maszyn wirtualnych, które zostały już uruchomione inne wystąpienia usługi aplikacji.
- Spodziewasz się funkcji aplikacji do uruchamiania stale lub prawie w sposób ciągły.
- Potrzebujesz więcej opcji procesora CPU lub pamięci niż jest podana w planie zużycia.
- Musisz uruchomić przekracza maksymalny dozwolony dla planu zużycie czas wykonywania.

Maszyna wirtualna oddziela kosztów od rozmiaru zarówno środowiska uruchomieniowego, jak i pamięci. W związku z tym nie będzie płacisz więcej niż koszt wystąpienia maszyny Wirtualnej, które zostało przydzielone. Aby uzyskać szczegółowe informacje dotyczące sposobu działania plan usługi aplikacji, zobacz [szczegółowe omówienie planów usługi aplikacji Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md). 

Plan usługi aplikacji można ręcznie skalować w poziomie przez dodanie więcej wystąpień maszyny Wirtualnej, lub można włączyć automatycznego skalowania. Aby uzyskać więcej informacji, zobacz [skalowanie liczby wystąpień ręcznie lub automatycznie](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json). Można także skalowanie w górę, wybierając inny plan usługi aplikacji. Aby uzyskać więcej informacji, zobacz [skalowanie w górę aplikacji na platformie Azure](../app-service-web/web-sites-scale.md). Jeśli planujesz uruchamianie funkcji JavaScript na plan usługi aplikacji, należy wybrać plan, który ma mniejszą liczbę rdzeni. Aby uzyskać więcej informacji, zobacz [JavaScript — odwołanie do funkcji](functions-reference-node.md#choose-single-core-app-service-plans).  

<!-- Note: the portal links to this section via fwlink https://go.microsoft.com/fwlink/?linkid=830855 --> 
<a name="always-on"></a>
###Zawsze włączone

Jeśli zostanie uruchomione na plan usługi aplikacji, należy włączyć **zawsze na** tak, aby aplikacja funkcja działa poprawnie. W planie usługi aplikacji — środowisko uruchomieniowe functions przejdzie bezczynności, po upływie kilku minut braku aktywności, tak tylko wyzwalaczy HTTP "wzbudzania" funkcji. Efekt jest podobny do sposobu zadania Webjob musi mieć zawsze włączone. 

Zawsze włączone jest dostępna tylko na plan usługi aplikacji. Na plan zużycie platformy aktywuje automatycznie funkcji aplikacji.

## <a name="storage-account-requirements"></a>Wymagania dotyczące konta magazynu

Plan zużycia lub plan usługi aplikacji aplikacji funkcji wymaga konta usługi Azure Storage, które obsługuje magazyn obiektów Blob platformy Azure, kolejki i tabeli. Wewnętrznie usługi Azure Functions używa usługi Azure Storage dla operacji, takich jak zarządzanie wyzwalaczy i rejestrowanie wykonania funkcji. Niektóre konta magazynu nie obsługują kolejek i tabel, takich jak konta magazynu tylko do obiektów blob (w tym magazyn w warstwie premium) i kont magazynu ogólnego przeznaczenia za pomocą replikacji magazyn strefowo nadmiarowy. Te konta są filtrowane z **konta magazynu** bloku podczas tworzenia aplikacji funkcji.

Aby dowiedzieć się więcej na temat typów kont magazynu, zobacz [wprowadzenie do usługi Azure Storage](../storage/common/storage-introduction.md#introducing-the-azure-storage-services).

## <a name="how-the-consumption-plan-works"></a>Jak działa planu zużycie

Plan zużycie jest automatycznie skalowany zasobów Procesora i pamięci przez dodanie dodatkowych wystąpień funkcje hosta, na podstawie liczby zdarzeń, które funkcje są uruchamiane na. Każde wystąpienie hosta funkcji jest ograniczona do 1,5 GB pamięci.

Użycie zużycie plan hostingu, funkcja kodu pliki są przechowywane w udziałach plików Azure na koncie magazynu głównego. Podczas usuwania konta magazynu głównego ta zawartość zostanie usunięta i nie może zostać odzyskany.

> [!NOTE]
> Podczas korzystania z wyzwalacza obiektu blob w planie zużycia, może istnieć maksymalnie 10-minutowych opóźnienia w przetwarzaniu nowe obiekty BLOB, jeśli aplikacja funkcji przeszedł bezczynności. Po uruchomieniu aplikacji funkcja obiekty BLOB są przetwarzane natychmiast. Aby uniknąć tego opóźnienia początkowej, weź pod uwagę jedną z następujących opcji:
> - Za pomocą plan usługi aplikacji na zawsze włączone.
> - Użyj innego mechanizmu wyzwalanie obiektów blob, przetwarzanie, takie jak wiadomość z kolejki nazwa obiektu blob. Na przykład zobacz [wyzwalacza kolejki z obiektu blob danych wejściowych powiązania](functions-bindings-storage-blob.md#input-sample).

### <a name="runtime-scaling"></a>Skalowanie środowiska wykonawczego

Środowisko Azure Functions używa składnik o nazwie *kontrolera skali* do monitorowania częstość zdarzeń i określanie, czy do skalowania w poziomie lub w dół. Kontroler skali korzysta z algorytmów heurystycznych dla każdego typu wyzwalacza. Na przykład gdy używasz wyzwalacz magazynu kolejek Azure skaluje na podstawie długość kolejki i wiek najstarsze komunikatu w kolejce.

Jednostka skalowania jest aplikacja funkcji. Kiedy funkcja aplikacji jest skalowana w poziomie, więcej zasobów są przydzielane do uruchomienia wielu wystąpień hosta usługi Azure Functions. Z drugiej strony jak żądanie zostanie zmniejszona obliczeń, kontrolera skali usuwa wystąpienia hosta funkcji. Liczba wystąpień jest ostatecznie skalowany w dół od zera uruchomionej żadnych funkcji w funkcji aplikacji.

![Kontroler skali monitorowanie zdarzeń i tworzenie wystąpień](./media/functions-scale/central-listener.png)

### <a name="billing-model"></a>Model rozliczania

Rozliczeń dla planu zużycie opisano szczegółowo w [usługi Azure Functions cennikiem]. Użycie liczby tylko czasu wykonywania kodu funkcji i jest agregowana na poziomie aplikacji funkcji. Jednostki do rozliczeń są następujące: 
* **Zużycie zasobów w ciągu sekund na gigabajtów (GB-s)**. Obliczony jako połączenie rozmiar pamięci i czasu wykonywania dla wszystkich funkcji w funkcji aplikacji. 
* **Wykonaniami**. Zliczane każdym razem, gdy funkcja jest wykonywana w odpowiedzi na zdarzenia wyzwolone przez powiązanie.

[usługi Azure Functions cennikiem]: https://azure.microsoft.com/pricing/details/functions
