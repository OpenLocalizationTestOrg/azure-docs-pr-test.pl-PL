---
title: "Zarządzanie maszyną wirtualną platformy Azure z wykorzystaniem zbierania spisu | Microsoft Docs"
description: "Zarządzanie maszyną wirtualną z wykorzystaniem zbierania spisu"
services: automation
keywords: "spis, automatyzacja, zmiana, śledzenie"
author: jennyhunter-msft
ms.author: jehunte
ms.date: 09/13/2017
ms.topic: article
manager: carmonm
ms.openlocfilehash: 7b0e39e98a81231b68414f36ac5c1fc0897304a1
ms.sourcegitcommit: 71fa59e97b01b65f25bcae318d834358fea5224a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/11/2018
---
# <a name="manage-an-azure-virtual-machine-with-inventory-collection"></a>Zarządzanie maszyną wirtualną platformy Azure z wykorzystaniem zbierania spisu

Istnieje możliwość włączenia śledzenia z użyciem spisu dla maszyny wirtualnej platformy Azure na stronie zasobów tej maszyny wirtualnej. Ta metoda zapewnia interfejs użytkownika oparty na przeglądarce przeznaczony do instalowania i konfigurowania zbierania spisu.

## <a name="before-you-begin"></a>Przed rozpoczęciem
Jeśli nie masz subskrypcji platformy Azure, utwórz [bezpłatne konto](https://azure.microsoft.com/free/).
Jeśli nie masz maszyny wirtualnej platformy Azure, utwórz [maszynę wirtualną](https://docs.microsoft.com/azure/virtual-machines/windows/quick-create-portal).

## <a name="sign-in-to-the-azure-portal"></a>Logowanie się do witryny Azure Portal
Zaloguj się w witrynie [Azure Portal](https://portal.azure.com/).

## <a name="enable-inventory-collection-from-the-virtual-machine-resource-page"></a>Włączanie zbierania spisu na stronie zasobów maszyny wirtualnej

1. W okienku po lewej stronie witryny Azure Portal wybierz pozycję **Maszyny wirtualne**.
2. Z listy maszyn wirtualnych wybierz maszynę wirtualną.
3. W menu **Zasób** w obszarze **Operacje** Wybierz pozycję **Spis (wersja zapoznawcza)**.  
    W górnej części okna pojawi się baner informujący o tym, że rozwiązanie nie jest włączone. 
4. Aby włączyć rozwiązanie, wybierz baner.
5. Wybierz obszar roboczy usługi Log Analytics, aby zapisać w nim dzienniki danych.  
    Jeśli w tym regionie nie ma dostępnego dla Ciebie obszaru roboczego, pojawi się monit o utworzenie domyślnego obszaru roboczego i konta usługi Automation. 
6. Aby rozpocząć dołączanie swojego komputera, kliknij pozycję **Włącz**.

   ![Widok opcji dołączania](./media/automation-vm-inventory/inventory-onboarding-options.png)  
    Pojawi się pasek stanu z informacją o tym, że trwa włączanie rozwiązania. Ten proces może potrwać do 15 minut. W tym czasie możesz zamknąć okno lub zostawić je otwarte i wówczas po włączeniu rozwiązania pojawi się w nim odpowiednie powiadomienie. Stan wdrożenia możesz monitorować w okienku powiadomień.

   ![Widok rozwiązania spisu natychmiast po dołączeniu](./media/automation-vm-inventory/inventory-onboarded.png)

Po zakończeniu wdrażania pasek stanu zniknie. System nadal będzie zbierać dane spisu i dane mogą być jeszcze niewidoczne. Zebranie pełnych danych może zająć 24 godziny.

## <a name="configure-your-inventory-settings"></a>Konfigurowanie ustawień spisu

Domyślnie na potrzeby zbierania skonfigurowane są oprogramowanie, usługi systemu Windows oraz demony systemu Linux. Aby zbierać spis dla rejestru systemu Windows i plików, skonfiguruj ustawienia zbierania spisu.

1. W widoku **Spis (wersja zapoznawcza)** wybierz przycisk **Edytuj ustawienia** w górnej części okna.
2. Aby dodać nowe ustawienie zbierania, przejdź do kategorii ustawienia, które chcesz dodać, wybierając karty **Rejestr systemu Windows**, **Pliki systemu Windows** oraz **Pliki systemu Linux**. 
3. Wybierz pozycję **Przeglądaj** u góry okna.
4. Aby wyświetlić szczegóły i opisy każdej właściwości ustawienia, odwiedź [stronę dokumentacji spisu](https://aka.ms/configinventorydocs).

## <a name="disconnect-your-virtual-machine-from-management"></a>Odłączanie maszyny wirtualnej od zarządzania

Aby usunąć maszynę wirtualną z zarządzania spisem:

1. W okienku po lewej stronie w witrynie Azure Portal kliknij pozycję **Log Analytics**, a następnie wybierz kliknięciem obszar roboczy, który był używany podczas dołączania danej maszyny wirtualnej.
2. W oknie **Log Analytics** w menu **Zasób** i kategorii **Źródła danych obszaru roboczego** wybierz pozycję **Maszyny wirtualne**. 
3. Z listy wybierz maszynę wirtualną, którą chcesz odłączyć. Maszyna wirtualna ma zielony znacznik wyboru obok pozycji **Ten obszar roboczy** w kolumnie **Połączenie OMS**. 
4. U góry następnej strony wybierz pozycję **Rozłącz**.
5. W oknie potwierdzenia wybierz pozycję **Tak**.  
    Ta akcja odłączy maszynę od zarządzania.

## <a name="next-steps"></a>Kolejne kroki

* Aby dowiedzieć się więcej o zarządzaniu zmianami w plikach i ustawieniach rejestru na maszynach wirtualnych, zobacz [Track software changes in your environment with the Change Tracking solution](../log-analytics/log-analytics-change-tracking.md) (Śledzenie zmian oprogramowania w środowisku za pomocą rozwiązania do śledzenia zmian).
* Aby dowiedzieć się więcej o zarządzaniu aktualizacjami systemu Windows i aktualizacjami pakietów na maszynach wirtualnych, zobacz [Rozwiązanie do zarządzania aktualizacjami w usłudze OMS](../operations-management-suite/oms-solution-update-management.md).
