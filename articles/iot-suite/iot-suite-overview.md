---
title: "Omówienie pakiet IoT Azure aaaMicrosoft | Dokumentacja firmy Microsoft"
description: "Omówienie sposobu pakiet IoT Azure oferuje internet rzeczy toocollect wstępnie skonfigurowanych rozwiązań, analizować i przechowywania danych, podaj wizualizacje i integracji z innymi systemami."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 2d38d08a-4133-4e5c-8b28-f93cadb5df05
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 385025c5ec0d37c74689a928bc09e85b33439634
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-iot-suite"></a>Przegląd Pakietu IoT Azure

Hello Azure Internetu rzeczy (IoT) usług oferuje szeroką gamę możliwości. Są to usługi klasy korporacyjnej, które pozwalają wykonywać następujące operacje:

* Zbieranie danych z urządzeń
* Analizowanie strumieni danych w ruchu
* Przechowywanie dużych zestawów danych i tworzenie dotyczących ich zapytań
* Wizualizowanie danych w czasie rzeczywistym i danych historycznych
* Integrowanie z systemami zaplecza biura
* Zarządzanie urządzeniami

toodeliver te możliwości pakiet IoT Azure razem pakietów wiele usług platformy Azure z rozszerzeniami niestandardowymi jako *wstępnie rozwiązań*. Te wstępnie skonfigurowanych rozwiązań jest podstawowych implementacji typowe wzorce rozwiązania IoT pomagających w czasie hello tooreduce zająć toodeliver Twojego rozwiązania IoT. Przy użyciu hello [IoT software development kit][lnk-sdks], można dostosować i rozszerzyć toomeet tych rozwiązań do własnych wymagań. Można ich także użyć jako przykładów lub szablonów podczas tworzenia nowych rozwiązań IoT.

Witaj poniższego klipu wideo zapewnia tooAzure wprowadzenie pakiet IoT:

> [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON309/player]
> 
> 

## <a name="azure-iot-services-in-azure-iot-suite"></a>Usługi Azure IoT w Pakiecie IoT Azure
Witaj wstępnie rozwiązaniach jest zwykle używany hello następujące usługi:

* Podstawowe tooAzure pakiet IoT jest hello [Centrum IoT Azure] [ lnk-iot-hub] usługi. Ta usługa udostępnia hello urządzenia do chmury i możliwości obsługi komunikatów chmury do urządzenia i działania jako brama toohello hello chmury hello inne klucza usługi pakiet IoT. usługi Hello pozwala tooreceive wiadomości z urządzeń na dużą skalę i wysyłać polecenia tooyour urządzeń. Usługa Hello pozwala również zbyt[zarządzania urządzeniami][lnk-device-management]. Na przykład można skonfigurować, ponownie uruchomić system lub wykonaj resetowania co najmniej jednego koncentratora toohello podłączonego urządzenia do ustawień fabrycznych.
* Usługa [Azure Stream Analytics][lnk-asa] umożliwia analizowanie danych w ruchu. Pakiet IoT używa telemetrii przychodzące tooprocess usługi, wykonywanie agregacji i wykrywa zdarzenia. rozwiązania Hello wstępnie również używają stream analytics tooprocess komunikaty informacyjne, które zawierają dane, takie jak metadanych lub polecenia odpowiedzi z urządzeń. rozwiązania Hello Użyj wiadomości powitania tooprocess Stream Analytics z urządzeń i świadczenia usług pod tooother tych wiadomości.
* [Usługa Azure Storage] [ lnk-azure-storage] i [bazy danych Azure rozwiązania Cosmos] [ lnk-document-db] zapewniają funkcji magazynowania danych hello. Witaj wstępnie skonfigurowanych rozwiązań Użyj telemetrii toostore magazynu obiektów blob i toomake je do analizy. rozwiązania Hello używać rozwiązania Cosmos DB toostore urządzenia metadanych i umożliwiają możliwości zarządzania urządzeniami hello hello rozwiązań.
* [Aplikacje sieci Web platformy Azure] [ lnk-web-apps] i [Microsoft Power BI] [ lnk-power-bi] zapewniają możliwości wizualizacji danych hello. elastyczność Hello usługi Power BI pozwala tooquickly tworzenie własnych interaktywnych pulpitów nawigacyjnych, korzystających z danych pakiet IoT.

Omówienie architektury hello typowe rozwiązania IoT, zobacz [Microsoft Azure i hello Internetu rzeczy (IoT)][iot-suite-what-is-azure-iot].

## <a name="preconfigured-solutions"></a>Wstępnie skonfigurowane rozwiązania

Pakiet IoT zawiera wstępnie skonfigurowanego rozwiązania tego wprowadzenie tooquickly można włączyć i tooexplore hello typowych scenariuszy IoT, takich jak:

* Zdalne monitorowanie
* Konserwacja zapobiegawcza
* Połączona fabryka

Można wdrożyć te rozwiązania tooyour subskrypcji platformy Azure, a następnie uruchom scenariusz IoT pełną, end-to-end.

## <a name="next-steps"></a>Następne kroki

Teraz, gdy masz omówienie czynności pakiet IoT i jakie są jej główne składniki można Dowiedz się więcej o rozwiązaniach hello wstępnie skonfigurowane w pakiet IoT. Aby uzyskać więcej informacji, zobacz [co hello Azure IoT wstępnie rozwiązania?][lnk-what-are-preconfig]

[lnk-sdks]: https://azure.microsoft.com/documentation/articles/iot-hub-sdks-summary/
[lnk-iot-hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-azure-storage]: https://azure.microsoft.com/documentation/services/storage/
[lnk-document-db]: https://azure.microsoft.com/documentation/services/documentdb/
[lnk-power-bi]: https://powerbi.microsoft.com/
[lnk-web-apps]: https://azure.microsoft.com/documentation/services/app-service/web/
[iot-suite-what-is-azure-iot]: iot-suite-what-is-azure-iot.md
[lnk-what-are-preconfig]: iot-suite-what-are-preconfigured-solutions.md
[lnk-device-management]: ../iot-hub/iot-hub-device-management-overview.md
