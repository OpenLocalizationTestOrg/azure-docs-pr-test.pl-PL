---
title: aaaGet wprowadzenie Harmonogram systemu Azure w portalu Azure | Dokumentacja firmy Microsoft
description: "Rozpoczynanie pracy z usługą Azure Scheduler w portalu Azure"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: e69542ec-d10f-4f17-9b7a-2ee441ee7d68
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/10/2016
ms.author: deli
ms.openlocfilehash: 58255c0ad19da65932f8b1d36cb8fef1ff6e651b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-scheduler-in-azure-portal"></a>Rozpoczynanie pracy z usługą Azure Scheduler w portalu Azure
Jest łatwy toocreate zaplanowane zadania w harmonogramie Azure. W przypadku tego samouczka, dowiesz się, jak toocreate zadania. Są w nim zawarte także informacje na temat możliwości monitorowania oraz zarządzania, jakie oferuje usługa Scheduler.

## <a name="create-a-job"></a>Tworzenie zadania
1. Zaloguj się za[portalu Azure](https://portal.azure.com/).  
2. Kliknij przycisk **+ nowy** > typ *harmonogramu* w polu wyszukiwania hello > Wybierz **harmonogramu** w wynikach > kliknij **Utwórz**.
   
    ![][marketplace-create]
3. Utwórzmy zadanie, które spowoduje przesłanie żądania GET do witryny http://www.microsoft.com/. W hello **zadania harmonogramu** ekranu, wprowadź hello następujących informacji:
   
   1. **Nazwa:** `getmicrosoft`  
   2. **Subskrypcja:** subskrypcja usługi Azure użytkownika   
   3. **Kolekcja zadań:** wybierz istniejącą kolekcję zadań lub kliknij przycisk **Utwórz nową** > wprowadź nazwę.
4. Następnie w **ustawienia akcji**, zdefiniuj hello następujące wartości:
   
   1. **Typ akcji:** ` HTTP`  
   2. **Metoda:** `GET`  
   3. **Adres URL:** ` http://www.microsoft.com`  
      
      ![][action-settings]
5. Ostatnią czynnością jest zdefiniowanie harmonogramu. Witaj zadania można określić jako zadanie wykonywane, ale umożliwia pobranie harmonogram cyklu:
   
   1. **Cykl**: `Recurring`
   2. **Uruchom**: dzisiejsza data
   3. **Powtarzaj co**: `12 Hours`
   4. **Zakończ**: dwa dni od dnia dzisiejszego  
      
      ![][recurrence-schedule]
6. Kliknij przycisk **Utwórz**

## <a name="manage-and-monitor-jobs"></a>Zarządzanie i monitorowanie zadań
Po utworzeniu zadania zostanie wyświetlona hello pulpitu nawigacyjnego Azure głównego. Kliknij zadanie hello i nowy zostanie otwarte okno z hello następujące karty:

1. Właściwości  
2. Ustawienia akcji  
3. Harmonogram  
4. Historia
5. Użytkownicy
   
   ![][job-overview]

### <a name="properties"></a>Właściwości
Te właściwości tylko do odczytu opisują metadanych zarządzania hello hello harmonogram zadania.

   ![][job-properties]

### <a name="action-settings"></a>Ustawienia akcji
Kliknięcie zadania w hello **zadania** ekran umożliwia tooconfigure zadania. Dzięki temu można skonfigurować ustawienia zaawansowane, jeśli nie możesz skonfigurować je w hello szybkie — tworzenie kreatora.

Dla wszystkich typów akcji może zmienić zasady ponawiania hello i hello akcji błędu.

Dla typów akcji zadania HTTP i HTTPS mogą ulec zmianie tooany metody hello dozwolone zlecenie HTTP. Mogą również dodać, usunąć lub zmienić informacje uwierzytelniania podstawowego lub hello nagłówków.

Dla typów akcji kolejki magazynu możesz zmienić hello konta magazynu, nazwę kolejki tokenu sygnatury dostępu Współdzielonego i treść.

Dla typów akcji magistrali usług możesz zmienić hello przestrzeni nazw, ścieżki tematu/kolejki, ustawienia uwierzytelniania, typem transportu, właściwości wiadomości i treści wiadomości.

   ![][job-action-settings]

### <a name="schedule"></a>Harmonogram
Dzięki temu można skonfigurować harmonogram hello, jeśli chcesz toochange hello harmonogram, który został utworzony w hello szybkie — tworzenie kreatora.

Jest to toobuild możliwości [harmonogramy złożone i zaawansowane cyklu w zadanie](scheduler-advanced-complexity.md)

Możesz zmienić hello Data rozpoczęcia i czas, w przypadku harmonogramu powtarzającego i hello Data zakończenia i czasu (Jeśli zadanie hello jest cykliczny.)

   ![][job-schedule]

### <a name="history"></a>Historia
Witaj **historii** karcie są wyświetlane wybrane metryki dla każdego wykonania zadania w systemie hello hello wybranego zadania. Te metryki Podaj wartości w czasie rzeczywistym dotyczące kondycji hello użytkownika harmonogramu:

1. Stan  
2. Szczegóły  
3. Liczba ponownych prób
4. Wystąpienie: 1., 2., 3. itp.
5. Godzina rozpoczęcia wykonywania  
6. Godzina zakończenia wykonywania
   
   ![][job-history]

Możesz kliknąć opcję wykonywania tooview jego **szczegóły historii**, tym hello całej odpowiedzi dla każdego wykonania. To okno dialogowe umożliwia również toocopy hello odpowiedzi toohello Schowka.

   ![][job-history-details]

### <a name="users"></a>Użytkownicy
Kontrola dostępu oparta na rolach (Role-Based Access Control, RBAC) na platformie Azure umożliwia precyzyjne zarządzanie dostępem dla usługi Azure Scheduler. toolearn jak hello toouse kartę Użytkownicy, można znaleźć zbyt[kontroli dostępu](../active-directory/role-based-access-control-configure.md)

## <a name="see-also"></a>Zobacz też
 [Co to jest usługa Scheduler?](scheduler-intro.md)

 [Pojęcia i terminologia dotyczące usługi Scheduler oraz hierarchia jednostek](scheduler-concepts-terms.md)

 [Plany i rozliczenia w usłudze Azure Scheduler](scheduler-plans-billing.md)

 [Jak planuje toobuild złożone i zaawansowane cyklu z Harmonogram systemu Azure](scheduler-advanced-complexity.md)

 [Dokumentacja interfejsu API REST usługi Scheduler](https://msdn.microsoft.com/library/mt629143)

 [Dokumentacja poleceń cmdlet programu PowerShell dla usługi Scheduler](scheduler-powershell-reference.md)

 [Wysoka dostępność i niezawodność usługi Scheduler](scheduler-high-availability-reliability.md)

 [Limity, wartości domyślne i kody błędów usługi Scheduler](scheduler-limits-defaults-errors.md)

 [Uwierzytelnianie połączeń wychodzących usługi Scheduler](scheduler-outbound-authentication.md)

[marketplace-create]: ./media/scheduler-get-started-portal/scheduler-v2-portal-marketplace-create.png
[action-settings]: ./media/scheduler-get-started-portal/scheduler-v2-portal-action-settings.png
[recurrence-schedule]: ./media/scheduler-get-started-portal/scheduler-v2-portal-recurrence-schedule.png
[job-properties]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-properties.png
[job-overview]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-overview-1.png
[job-action-settings]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-action-settings.png
[job-schedule]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-schedule.png
[job-history]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-history.png
[job-history-details]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-history-details.png


[1]: ./media/scheduler-get-started-portal/scheduler-get-started-portal001.png
[2]: ./media/scheduler-get-started-portal/scheduler-get-started-portal002.png
[3]: ./media/scheduler-get-started-portal/scheduler-get-started-portal003.png
[4]: ./media/scheduler-get-started-portal/scheduler-get-started-portal004.png
[5]: ./media/scheduler-get-started-portal/scheduler-get-started-portal005.png
[6]: ./media/scheduler-get-started-portal/scheduler-get-started-portal006.png
[7]: ./media/scheduler-get-started-portal/scheduler-get-started-portal007.png
[8]: ./media/scheduler-get-started-portal/scheduler-get-started-portal008.png
[9]: ./media/scheduler-get-started-portal/scheduler-get-started-portal009.png
[10]: ./media/scheduler-get-started-portal/scheduler-get-started-portal010.png
[11]: ./media/scheduler-get-started-portal/scheduler-get-started-portal011.png
[12]: ./media/scheduler-get-started-portal/scheduler-get-started-portal012.png
[13]: ./media/scheduler-get-started-portal/scheduler-get-started-portal013.png
[14]: ./media/scheduler-get-started-portal/scheduler-get-started-portal014.png
[15]: ./media/scheduler-get-started-portal/scheduler-get-started-portal015.png
