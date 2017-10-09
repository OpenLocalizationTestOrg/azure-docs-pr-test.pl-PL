---
title: "plany aaaAzure zużycia funkcje i usługi aplikacji | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak usługi Azure Functions skaluje potrzeb hello toomeet obciążeń sterowanego zdarzeniami."
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
ms.openlocfilehash: 3826915b93328635d9295efe90ecc421e6c56af2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-consumption-and-app-service-plans"></a>Azure planów zużycia funkcje i usługi aplikacji 

## <a name="introduction"></a>Wprowadzenie

Można uruchomić usługi Azure Functions w dwóch różnych trybach: plan zużycia i plan usługi aplikacji Azure. plan zużycie Hello automatycznie przydzieli moc obliczeniową po kodzie działa, skaluje się jako niezbędne toohandle obciążenia i następnie skalowany w dół, gdy kodu nie jest uruchomiona. Tak nie masz toopay bezczynnych maszyn wirtualnych i nie ma zasobów tooreserve z wyprzedzeniem. Ten artykuł skupia się na powitania zużycie planu. Aby uzyskać szczegółowe informacje dotyczące sposobu działania hello planu usługi App Service, zobacz hello [szczegółowe omówienie planów usługi aplikacji Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md). 

Jeśli nie znasz usługi Azure Functions, zobacz hello [Azure Functions — omówienie](functions-overview.md).

Podczas tworzenia aplikacji funkcji, należy skonfigurować plan hostingu dla funkcji, aplikacja hello zawiera. W trybie wystąpienia hello *hosta usługi Azure Functions* wykonuje hello funkcji. Typ Hello planu formantów:

* Jak wystąpień hosta jest skalowana w poziomie.
* Witaj zasoby, które są dostępne tooeach hosta.

Obecnie musisz wybrać typ planu hello podczas tworzenia hello hello funkcji aplikacji. Nie można zmienić go później. 

Możesz skalować między warstwami na powitania planu usługi aplikacji. W planie zużycie hello usługi Azure Functions obsługuje automatycznie alokacji zasobów.

## <a name="consumption-plan"></a>Plan Zużycie

Podczas korzystania z planu zużycia, wystąpień hosta usługi Azure Functions hello są dynamicznie dodawane i usuwane oparte na powitania liczba zdarzeń przychodzących. Ten plan skaluje automatycznie, a użytkownik naliczane są opłaty za zasoby obliczeniowe tylko wtedy, gdy są uruchomione funkcji. Na plan użycie funkcji można uruchomić maksymalnie 10 minut. 

> [!NOTE]
> Witaj domyślny limit czasu dla funkcji w planie zużycie wynosi 5 minut. wartość Hello może być zwiększona too10 minut hello funkcji aplikacji, zmieniając właściwość hello `functionTimeout` w [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).

Rozliczenia jest oparta na czas wykonywania i używanej pamięci, i jest agregowana przez wszystkie funkcje w aplikacji funkcji. Aby uzyskać więcej informacji, zobacz hello [usługi Azure Functions cennikiem].

plan zużycie Hello jest domyślnym hello i oferuje hello następujące korzyści:
- Płać tylko wtedy, gdy uruchomione są funkcji.
- Skalowanie w poziomie automatycznie, nawet w okresie wysoki obciążenia.

## <a name="app-service-plan"></a>Plan usługi App Service

W hello usługi aplikacji — plan, aplikacji funkcji Uruchom na dedykowanych maszynach wirtualnych na podstawowa, standardowa i Premium jednostki SKU, tooWeb podobne aplikacji. Dedykowanych maszyn wirtualnych są przydzielone tooyour usługi aplikacji — aplikacje, co oznacza, że host funkcji hello zawsze działa.

Należy wziąć pod uwagę plan usługi aplikacji w hello w następujących przypadkach:
- Masz istniejący, niedostatecznie maszyn wirtualnych, które zostały już uruchomione inne wystąpienia usługi aplikacji.
- Stale lub prawie stale spodziewać się toorun aplikacji z funkcji.
- Potrzebujesz więcej opcji procesora CPU lub pamięci niż jest podana w planie zużycie hello.
- Należy toorun dłużej niż hello dozwolony dla planu zużycie hello maksymalny czas wykonywania.

Maszyna wirtualna oddziela kosztów od rozmiaru zarówno środowiska uruchomieniowego, jak i pamięci. W związku z tym nie będzie płacisz więcej niż koszt hello hello wystąpienia maszyny Wirtualnej, które zostało przydzielone. Aby uzyskać szczegółowe informacje dotyczące sposobu działania hello planu usługi App Service, zobacz hello [szczegółowe omówienie planów usługi aplikacji Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md). 

Plan usługi aplikacji można ręcznie skalować w poziomie przez dodanie więcej wystąpień maszyny Wirtualnej, lub można włączyć automatycznego skalowania. Aby uzyskać więcej informacji, zobacz [skalowanie liczby wystąpień ręcznie lub automatycznie](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json). Można także skalowanie w górę, wybierając inny plan usługi aplikacji. Aby uzyskać więcej informacji, zobacz [skalowanie w górę aplikacji na platformie Azure](../app-service-web/web-sites-scale.md). Jeśli planujesz funkcji JavaScript toorun plan usługi aplikacji, należy wybrać plan, który ma mniejszą liczbę rdzeni. Aby uzyskać więcej informacji, zobacz hello [JavaScript — odwołanie do funkcji](functions-reference-node.md#choose-single-core-app-service-plans).  

<!-- Note: hello portal links toothis section via fwlink https://go.microsoft.com/fwlink/?linkid=830855 --> 
<a name="always-on"></a>
###Zawsze włączone

Jeśli zostanie uruchomione na plan usługi aplikacji, należy włączyć hello **zawsze na** tak, aby aplikacja funkcja działa poprawnie. Na plan usługi aplikacji hello środowisko uruchomieniowe functions przejdzie bezczynności, po upływie kilku minut braku aktywności, więc tylko wyzwalaczy HTTP "wzbudzania" funkcji. Jest to podobne toohow zadania Webjob musi mieć zawsze włączone. 

Zawsze włączone jest dostępna tylko na plan usługi aplikacji. Na plan zużycie platformy hello aktywuje automatycznie funkcji aplikacji.

## <a name="storage-account-requirements"></a>Wymagania dotyczące konta magazynu

Plan zużycia lub plan usługi aplikacji aplikacji funkcji wymaga konta usługi Azure Storage, które obsługuje magazyn obiektów Blob platformy Azure, kolejki i tabeli. Wewnętrznie usługi Azure Functions używa usługi Azure Storage dla operacji, takich jak zarządzanie wyzwalaczy i rejestrowanie wykonania funkcji. Niektóre konta magazynu nie obsługują kolejek i tabel, takich jak konta magazynu tylko do obiektów blob (w tym magazyn w warstwie premium) i kont magazynu ogólnego przeznaczenia za pomocą replikacji magazyn strefowo nadmiarowy. Te konta są filtrowane z hello **konta magazynu** bloku podczas tworzenia aplikacji funkcji.

toolearn więcej informacji na temat typów kont magazynu, zobacz [wprowadzenie do usługi Azure Storage hello](../storage/common/storage-introduction.md#introducing-the-azure-storage-services).

## <a name="how-hello-consumption-plan-works"></a>Jak działa hello zużycie planu

plan zużycie Hello jest automatycznie skalowany zasobów Procesora i pamięci przez dodanie dodatkowych wystąpień hello funkcje hosta, na podstawie liczby hello zdarzenia, które funkcje są uruchamiane na. Każde wystąpienie hosta funkcji hello jest ograniczona too1.5 GB pamięci.

Gdy używasz hello zużycie plan hostingu, funkcja kodu pliki są przechowywane w udziałach plików Azure na koncie magazynu głównego hello. Podczas usuwania konta magazynu głównego hello ta zawartość zostanie usunięta i nie może zostać odzyskany.

> [!NOTE]
> Podczas korzystania z wyzwalacza obiektu blob w planie zużycia, może istnieć się tooa 10-minutowych opóźnienia w przetwarzania nowe obiekty BLOB, jeśli aplikacja funkcji przeszedł bezczynności. Po uruchomieniu aplikacji funkcja hello obiekty BLOB są przetwarzane natychmiast. tooavoid tym początkowej opóźnienia, weź pod uwagę jedną hello następujące opcje:
> - Za pomocą plan usługi aplikacji na zawsze włączone.
> - Użyj innego mechanizmu tootrigger hello obiektu blob przetwarzania, takich jak wiadomość z kolejki hello nazwa obiektu blob. Na przykład zobacz [wyzwalacza kolejki z obiektu blob danych wejściowych powiązania](functions-bindings-storage-blob.md#input-sample).

### <a name="runtime-scaling"></a>Skalowanie środowiska wykonawczego

Środowisko Azure Functions używa składnik o nazwie hello *kontrolera skali* toomonitor hello częstość zdarzeń i określić, czy tooscale pracy lub w dół. Kontroler skali Hello korzysta z algorytmów heurystycznych dla każdego typu wyzwalacza. Na przykład podczas korzystania z wyzwalacz magazynu kolejek Azure, skalowanie na podstawie hello długość kolejki i wiek hello hello najstarsze kolejki wiadomości.

Hello jednostki skalowania jest hello funkcji aplikacji. Gdy aplikacja funkcji hello jest skalowana w poziomie, więcej zasobów są przydzielone toorun wiele wystąpień hello Azure Functions hosta. Z drugiej strony jak żądanie zostanie zmniejszona obliczeń, hello skali kontrolera usuwa wystąpienia hosta funkcji. Hello liczba wystąpień jest ostatecznie skalowany w dół toozero uruchomionej żadnych funkcji w funkcji aplikacji.

![Kontroler skali monitorowanie zdarzeń i tworzenie wystąpień](./media/functions-scale/central-listener.png)

### <a name="billing-model"></a>Model rozliczania

Rozliczeń dla planu zużycie hello opisano szczegółowo na powitania [usługi Azure Functions cennikiem]. Użycie liczby tylko czas hello jest uruchomiona funkcja kodu i jest zagregowane na poziomie aplikacji hello funkcji. Oto Hello jednostki do rozliczeń: 
* **Zużycie zasobów w ciągu sekund na gigabajtów (GB-s)**. Obliczony jako połączenie rozmiar pamięci i czasu wykonywania dla wszystkich funkcji w funkcji aplikacji. 
* **Wykonaniami**. Zliczane każdym razem, gdy funkcja jest wykonywana w przypadku tooan odpowiedzi wyzwalane przez powiązanie.

[usługi Azure Functions cennikiem]: https://azure.microsoft.com/pricing/details/functions
