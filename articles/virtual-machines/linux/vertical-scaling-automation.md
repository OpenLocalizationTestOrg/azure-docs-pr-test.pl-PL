---
title: "Skalowanie w pionie maszyny wirtualnej platformy Azure w usłudze Automatyzacja Azure | Dokumentacja firmy Microsoft"
description: "Sposób pionowo skalowania maszyny wirtualnej systemu Linux w odpowiedzi na monitorowanie alertów w usłudze Automatyzacja Azure"
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: dcee199e-fa25-44d5-9b25-df564cee9b45
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/29/2016
ms.author: singhkay
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1ffcecf1e61fc0cd9ee668514fbb913dafe39bd8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="vertically-scale-azure-linux-virtual-machine-with-azure-automation"></a>Skalowanie w pionie maszyny wirtualnej systemu Linux platformy Azure w usłudze Automatyzacja Azure
Skalowanie w pionie to proces zwiększania lub zmniejszania zasobów w odpowiedzi na obciążenie pracą maszyny. W systemie Azure można to zrobić przez zmianę rozmiaru maszyny wirtualnej. Może to pomóc w następujących scenariuszach

* Jeśli maszyna wirtualna nie jest często używany, można zmienić rozmiar go do mniejszy rozmiar, aby zmniejszyć koszty miesięcznego
* Jeśli maszyna wirtualna ma do czynienia obciążenia szczytowego, można zmieniać na większy rozmiar, aby zwiększyć jego pojemność

Konspekt instrukcje w tym celu jest jako poniżej

1. Instalator usługi Automatyzacja Azure na dostęp do maszyn wirtualnych
2. Importowanie elementów runbook skali pionowej automatyzacji Azure w ramach subskrypcji
3. Dodawanie elementu webhook z elementem runbook
4. Dodawanie alertu do maszyny wirtualnej

> [!NOTE]
> Ze względu na rozmiar maszyny wirtualnej pierwszej rozmiary, do których może być skalowana, może być ograniczony z powodu dostępności bieżącej maszyny wirtualnej wdrożonej w innej wielkości w klastrze. W elementach runbook automatyzacji opublikowanych używane w tym artykule zajmie się tym przypadku firma Microsoft i skalować tylko w ramach poniżej pary rozmiar maszyny Wirtualnej. Oznacza to, czy Standard_D1v2 maszyny wirtualnej zostanie nie nagle Skalowanie z Standard_G5 lub skalowany w dół do Basic_A0.
> 
> | Rozmiary maszyn wirtualnych, skalowanie pary |  |
> | --- | --- |
> | Basic_A0 |Basic_A4 |
> | Standardowa_A0 |Standardowa_A4 |
> | Standardowa_A5 |Standardowa_A7 |
> | Standard_A8 |Standard_A9 |
> | Standardowa_A10 |Standardowa_A11 |
> | Standardowa_D1 |Standardowa_D4 |
> | Standardowa_D11 |Standardowa_D14 |
> | Standardowa_DS1 |Standardowa_DS4 |
> | Standardowa_DS11 |Standardowa_DS14 |
> | Standard_D1v2 |Standard_D5v2 |
> | Standard_D11v2 |Standard_D14v2 |
> | Standardowa_G1 |Standard_G5 |
> | Standardowa_GS1 |Standard_GS5 |
> 
> 

## <a name="setup-azure-automation-to-access-your-virtual-machines"></a>Instalator usługi Automatyzacja Azure na dostęp do maszyn wirtualnych
W pierwszej kolejności należy wykonać to utworzyć konto usługi Automatyzacja Azure, które będą obsługiwać elementów runbook, używana do skalowania wystąpienia zestawu skali maszyny Wirtualnej. Ostatnio usługi Automatyzacja wprowadzono funkcję "Konto Uruchom jako", co sprawia, że ustawienia zapasowej główną usługi dla automatycznie uruchomione elementy runbook w imieniu użytkownika bardzo proste. Możesz przeczytać więcej na temat tego artykułu poniżej:

* [Uwierzytelnianie elementów Runbook przy użyciu konta Uruchom jako platformy Azure](../../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-the-azure-automation-vertical-scale-runbooks-into-your-subscription"></a>Importowanie elementów runbook skali pionowej automatyzacji Azure w ramach subskrypcji
Elementy runbook, które są potrzebne w pionie skalowania maszyny wirtualnej zostały już opublikowane w galerii elementu Runbook automatyzacji Azure. Konieczne będzie zaimportowanie ich do subskrypcji. Można poznać sposoby zaimportować elementy runbook, odczytując w następującym artykule.

* [Galeria elementów Runbook i modułów dla usługi Automatyzacja Azure](../../automation/automation-runbook-gallery.md)

Elementy runbook, które wymagają zaimportowania przedstawiono na poniższej ilustracji

![Importowanie elementów runbook](./media/vertical-scaling-automation/scale-runbooks.png)

## <a name="add-a-webhook-to-your-runbook"></a>Dodawanie elementu webhook z elementem runbook
Po zaimportowaniu elementów runbook, które będą potrzebne, aby dodać elementu webhook do elementu runbook, mogą być wyzwalane przez alert z maszyny wirtualnej. Szczegółowe informacje o utworzeniu elementu webhook dla elementu Runbook, które mogą być odczytywane w tym miejscu

* [Azure automatyzacji elementów webhook](../../automation/automation-webhooks.md)

Upewnij się, że można skopiować elementu webhook przed zamknięciem okna dialogowego elementu webhook, ponieważ będzie on potrzebny w następnej sekcji.

## <a name="add-an-alert-to-your-virtual-machine"></a>Dodawanie alertu do maszyny wirtualnej
1. Wybierz ustawienia maszyny wirtualnej
2. Wybierz opcję "Reguły alertu"
3. Wybierz opcję "Dodaj alert"
4. Wybierz metrykę, aby wyzwalać alert na
5. Wybierz warunek, w przypadku których spełnione będą powodować wyzwalać alert
6. Wybierz próg dla warunku w kroku 5. do spełnienia
7. Wybierz okres służącym usługi monitorowania będzie sprawdzać, warunek i wartość progową kroki 5 i 6
8. Wklej skopiowane z poprzedniej sekcji elementu webhook.

![Dodawanie alertu do maszyny wirtualnej 1](./media/vertical-scaling-automation/add-alert-webhook-1.png)

![Dodawanie alertu do maszyny wirtualnej 2](./media/vertical-scaling-automation/add-alert-webhook-2.png)

