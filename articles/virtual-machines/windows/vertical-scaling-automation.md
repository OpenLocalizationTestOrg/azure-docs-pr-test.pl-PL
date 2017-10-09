---
title: "toovertically usługi Automatyzacja Azure aaaUse skalowania maszyn wirtualnych z systemem Windows | Dokumentacja firmy Microsoft"
description: "Pionowo skalowania maszyny wirtualnej systemu Windows w odpowiedzi toomonitoring alertów z usługi Automatyzacja Azure"
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4f964713-fb67-4bcc-8246-3431452ddf7d
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/29/2016
ms.author: kasing
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 24d07f3e2e217668f18676e6d6873be4f9770349
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="vertically-scale-windows-vms-with-azure-automation"></a>Skalowanie w pionie maszyn wirtualnych systemu Windows w usłudze Automatyzacja Azure

Skalowanie w pionie jest hello proces zwiększania lub zmniejszania zasobów hello maszyny w odpowiedzi toohello obciążenia. W systemie Azure można to zrobić, zmieniając rozmiar hello hello maszyny wirtualnej. Może to pomóc w hello następujące scenariusze

* Jeśli nie jest często używany hello maszyny wirtualnej, można zmienić rozmiar go w dół tooa mniejszy rozmiar tooreduce miesięcznych kosztów
* Jeśli obciążenia szczytowego ma do czynienia z hello maszyny wirtualnej, może być tooa po zmianie rozmiaru większy rozmiar tooincrease pojemności

Konspekt Hello tooaccomplish kroki hello jest jako poniżej

1. Konfiguracja usługi Automatyzacja Azure tooaccess maszyny wirtualne
2. Zaimportować elementy runbook skali pionowej automatyzacji Azure hello w ramach subskrypcji
3. Dodaj element tooyour elementu webhook
4. Dodawanie alertu tooyour maszyny wirtualnej

> [!NOTE]
> Ze względu na rozmiar hello hello pierwszej maszynie wirtualnej, rozmiarów hello mogą być skalowane, może być ograniczony powodu dostępności toohello hello innych rozmiarach w klastrze hello bieżącej maszyny wirtualnej wdrożonej w. W hello opublikowane elementy runbook automatyzacji używane w tym artykule, firma Microsoft zajmie się tym przypadku i skalować tylko w obrębie hello poniżej pary rozmiar maszyny Wirtualnej. Oznacza to, że Standard_D1v2 maszyny wirtualnej zostanie nie nagle skalowanie tooStandard_G5 lub skalowany w dół tooBasic_A0.
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

## <a name="setup-azure-automation-tooaccess-your-virtual-machines"></a>Konfiguracja usługi Automatyzacja Azure tooaccess maszyny wirtualne
najpierw Hello należy toodo jest utworzyć konto usługi Automatyzacja Azure, które będzie obsługiwać tooscale elementów runbook używane hello maszyny wirtualnej. Niedawno usługi Automatyzacja hello wprowadzone "Konto Uruchom jako" Funkcja hello, co sprawia, że skonfigurowanie hello nazwy głównej usługi dla automatycznie uruchomione hello elementy runbook w imieniu użytkownika hello bardzo proste. Możesz przeczytać dodatkowe informacje w artykule hello poniżej:

* [Uwierzytelnianie elementów Runbook przy użyciu konta Uruchom jako platformy Azure](../../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-hello-azure-automation-vertical-scale-runbooks-into-your-subscription"></a>Zaimportować elementy runbook skali pionowej automatyzacji Azure hello w ramach subskrypcji
Witaj elementów runbook, które są potrzebne w pionie skalowania maszyny wirtualnej zostały już opublikowane w hello galerię elementów Runbook automatyzacji Azure. Konieczne będzie tooimport ich do subskrypcji. Aby dowiedzieć się jak tooimport elementów runbook, odczytując hello poniższego artykułu.

* [Galeria elementów Runbook i modułów dla usługi Automatyzacja Azure](../../automation/automation-runbook-gallery.md)

w poniższym obrazie hello przedstawiono Hello elementów runbook, które należy zaimportować toobe

![Importowanie elementów runbook](./media/vertical-scaling-automation/scale-runbooks.png)

## <a name="add-a-webhook-tooyour-runbook"></a>Dodaj element tooyour elementu webhook
Po zaimportowaniu elementów runbook hello należy tooadd webhook toohello runbook, mogą być wyzwalane przez alert z maszyny wirtualnej. Szczegóły Hello tworzenia elementu webhook dla elementu Runbook, które mogą być odczytywane w tym miejscu

* [Azure automatyzacji elementów webhook](../../automation/automation-webhooks.md)

Upewnij się, że przed zamknięciem okna dialogowego elementu webhook hello ponieważ będzie on potrzebny w następnej sekcji hello kopiowania elementu webhook hello.

## <a name="add-an-alert-tooyour-virtual-machine"></a>Dodawanie alertu tooyour maszyny wirtualnej
1. Wybierz ustawienia maszyny wirtualnej
2. Wybierz opcję "Reguły alertu"
3. Wybierz opcję "Dodaj alert"
4. Wybierz alert hello toofire metryki na
5. Wybierz warunek, w przypadku których spełnione będą powodować hello toofire alertu
6. Wybierz próg dla warunku hello w kroku 5. toobe spełnione
7. Wybierz okres za pośrednictwem których hello usługi monitorowania będzie sprawdzać hello warunek i wartość progową kroki 5 i 6
8. Wklej webhook hello, które zostały skopiowane z poprzedniej sekcji hello.

![Dodaj tooVirtual alertu 1 komputera](./media/vertical-scaling-automation/add-alert-webhook-1.png)

![Dodawanie alertu tooVirtual maszyny 2](./media/vertical-scaling-automation/add-alert-webhook-2.png)

