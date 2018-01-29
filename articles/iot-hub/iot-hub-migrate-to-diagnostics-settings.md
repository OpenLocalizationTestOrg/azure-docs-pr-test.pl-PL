---
title: "Centrum IoT Azure migrację do ustawień diagnostycznych | Dokumentacja firmy Microsoft"
description: "Jak zaktualizować Centrum IoT Azure, aby użyć ustawień diagnostycznych platformy Azure zamiast operacje monitorowania do monitorowania stanu operacji w Centrum IoT w czasie rzeczywistym."
services: iot-hub
documentationcenter: 
author: kgremban
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/10/2017
ms.author: kgremban
ms.openlocfilehash: 2716f397ad0e7abfdcd397340da8fa8116a172db
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="migrate-your-iot-hub-from-operations-monitoring-to-diagnostics-settings"></a>Migrowanie Centrum IoT z operacji monitorowania do ustawień diagnostycznych

Klienci korzystający z [operacje monitorowania] [ lnk-opsmon] do śledzenia stanu operacji w Centrum IoT można migrować na ten przepływ pracy do [ustawień diagnostyki Azure] [ lnk-diagnostics-settings], funkcja Azure monitora. Ustawienia diagnostyki, podaj informacje diagnostyczne poziom zasobów dla wielu usług Azure.

Operacje funkcji monitorowania w Centrum IoT jest przestarzałe i zostanie usunięte w przyszłości. Ten artykuł zawiera kroki umożliwiające przeniesienie obciążeń od działań monitorowania do ustawień diagnostycznych. Aby uzyskać więcej informacji na temat osi czasu przestarzałą zobacz [monitorować rozwiązań Azure IoT z monitorem Azure oraz kondycja zasobów Azure][lnk-blog-announcement].

## <a name="update-iot-hub"></a>Zaktualizuj Centrum IoT

Aby zaktualizować Centrum IoT w portalu Azure, najpierw należy włączyć ustawienia diagnostyki, a następnie wyłącz operacje monitorowania.  

[!INCLUDE [iot-hub-diagnostics-settings](../../includes/iot-hub-diagnostics-settings.md)]

### <a name="turn-off-operations-monitoring"></a>Wyłącz operacje monitorowania

Po przetestowaniu nowe ustawienia diagnostyki w przepływie pracy, można wyłączyć operacji funkcji monitorowania. 

1. W menu Centrum IoT, wybierz **operacje monitorowania**.
1. W każdej kategorii monitorowania, wybierz **Brak**.
1. Zapisz operacje monitorowania zmian.

## <a name="update-applications-that-use-operations-monitoring"></a>Aktualizowanie aplikacji, które używają operacje monitorowania

Schematy działań monitorowania i ustawień diagnostycznych się nieco różnić. Koniecznie zaktualizowanie aplikacje korzystające z operacji monitorowania dzisiaj do mapowania do schematu używane przez ustawienia diagnostyki. 

Ponadto diagnostyki ustawienia oferty śledzenie pięć nowych kategorii. Po zaktualizowaniu aplikacji dla istniejącego schematu, należy dodać również nowe kategorie:

- Operacje dwie chmury do urządzenia
- Operacje dwie urządzenia do chmury
- Dwie zapytań
- Operacje zadań
- Bezpośrednie metody

W strukturach schematu, zobacz [zrozumieć schematu ustawień diagnostycznych][lnk-diagnostics-schema].

## <a name="next-steps"></a>Następne kroki

- [Monitorowanie kondycji Azure IoT Hub i szybkie diagnozowanie problemów][lnk-monitor]

[lnk-opsmon]: iot-hub-operations-monitoring.md
[lnk-diagnostics-settings]: ../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md
[lnk-diagnostics-schema]: iot-hub-monitor-resource-health.md#understand-the-logs
[lnk-blog-announcement]: https://azure.microsoft.com/blog/monitor-your-azure-iot-solutions-with-azure-monitor-and-azure-resource-health
[lnk-monitor]: iot-hub-monitor-resource-health.md
