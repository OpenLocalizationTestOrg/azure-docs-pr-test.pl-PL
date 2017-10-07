---
title: "aaaMonitor urządzeń Surface Hub z Azure Log Analytics | Dokumentacja firmy Microsoft"
description: "Użyj hello Surface Hub rozwiązania tootrack hello kondycji z urządzeń Surface Hub i zrozumieć, jak są one używane."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 8b4e56bc-2d4f-4648-a236-16e9e732ebef
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 623d30e749cafdd4a34ba0c5b3408164f1b4a95b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-surface-hubs-with-log-analytics-tootrack-their-health"></a>Monitorowanie urządzeń Surface Hub z tootrack analizy dzienników ich kondycji

![Surface Hub symbol](./media/log-analytics-surface-hubs/surface-hub-symbol.png)

W tym artykule opisano, jak można użyć hello rozwiązania Surface Hub w analizy dzienników toomonitor Microsoft Surface Hub urządzeniom hello programu Microsoft Operations Management Suite (OMS). Zaloguj się Analytics pomaga śledzić, kondycję hello z urządzeń Surface Hub dobrze zrozumieć, jak są one używane.

Każdy Surface Hub ma hello zainstalowania programu Microsoft Monitoring Agent. Jego za pośrednictwem agenta hello wysyłania danych z programu tooOMS Surface Hub. Pliki dziennika są odczytywane z urządzeń Surface Hub i są następnie są wysyłane toohello usługę. Problemy, takie jak serwery w trybie offline, hello kalendarza nie synchronizuje lub konta urządzeń hello jest toolog do usługi Skype są wyświetlane w OMS hello Surface Hub w pulpicie nawigacyjnym. Przy użyciu danych hello hello pulpitu nawigacyjnego, można zidentyfikować urządzenia nie są uruchomione lub są inne problemy i potencjalnie zastosować poprawki hello wykryto problemów.

## <a name="installing-and-configuring-hello-solution"></a>Instalowanie i konfigurowanie hello rozwiązania
Użyj powitania po tooinstall informacji i skonfiguruj hello rozwiązania. W kolejności toomanage Twojego urządzeń Surface Hub z hello programu Microsoft Operations Management Suite (OMS) należy hello następujące:

* Ważnej subskrypcji zbyt[OMS](http://www.microsoft.com/oms).
* [Subskrypcji OMS](https://azure.microsoft.com/pricing/details/log-analytics/) poziom, który będzie obsługiwać numer hello urządzeń ma toomonitor. Cennik pakietu OMS zmienia się w zależności od liczby urządzeń zarejestrowanych i ilość danych go procesów. Należy tootake to pod uwagę podczas planowania wdrożenia Surface Hub.

Następnie spowoduje dodanie istniejącej subskrypcji Microsoft Azure OMS subskrypcji tooyour lub Utwórz nowy obszar roboczy bezpośrednio za pomocą portalu OMS hello. Szczegółowe instrukcje do przy użyciu jednej z metod jest w [wprowadzenie do analizy dzienników](log-analytics-get-started.md). Po skonfigurowaniu hello OMS subskrypcji istnieją dwa sposoby tooenroll urządzenia Surface Hub:

* Automatycznie za pomocą usługi Intune
* Ręcznie za pomocą **ustawienia** urządzenia Surface Hub.

## <a name="set-up-monitoring"></a>Konfigurowanie monitorowania
Można monitorować hello kondycji i aktywności użytkownika Surface Hub przy użyciu analizy dzienników w OMS. Witaj Surface Hub w OMS można zarejestrować za pomocą usługi Intune lub lokalnie przy użyciu **ustawienia** na powitania Surface Hub.

## <a name="connect-surface-hubs-toooms-through-intune"></a>Łączenie urządzeń Surface Hub tooOMS za pomocą usługi Intune
Konieczne będzie hello identyfikator i klucz obszaru roboczego dla obszar roboczy OMS hello, która ma zarządzać z urządzeń Surface Hub. Możesz pobrać z portalu OMS hello.

Usługa Intune jest produktem firmy Microsoft, która pozwala toocentrally Zarządzanie ustawieniami konfiguracji OMS hello, które są stosowane tooone lub więcej urządzeń. Wykonaj te kroki tooconfigure urządzenia za pomocą usługi Intune:

1. Zaloguj się tooIntune.
2. Przejdź za**ustawienia** > **połączonych źródeł**.
3. Utwórz lub Edytuj zasady na podstawie szablonu Surface Hub hello.
4. Przejdź do sekcji OMS (Azure Operational Insights) toohello hello zasad, a następnie dodaj hello *identyfikator obszaru roboczego* i *klucz obszaru roboczego* toohello zasad.
5. Zapisz zasady hello.
6. Kojarzenie zasad hello z hello odpowiednie grupy urządzeń.

   ![Zasady usługi Intune](./media/log-analytics-surface-hubs/intune.png)

Następnie usługa Intune przeprowadza synchronizację ustawień OMS hello z urządzeniami hello w grupie docelowej hello zarejestrowanie ich w obszarze roboczym pakietu OMS.

## <a name="connect-surface-hubs-toooms-using-hello-settings-app"></a>Połącz przy użyciu aplikacji ustawienia hello tooOMS urządzeń Surface Hub
Konieczne będzie hello identyfikator i klucz obszaru roboczego dla obszar roboczy OMS hello, która ma zarządzać z urządzeń Surface Hub. Możesz pobrać z portalu OMS hello.

Jeśli nie używasz usługi Intune toomanage środowiska, możesz zarejestrować ręcznie za pomocą urządzenia **ustawienia** na każdym Surface Hub:

1. Z Centrum powierzchni, otwórz **ustawienia**.
2. Wprowadź poświadczenia administratora urządzenia powitania po wyświetleniu monitu.
3. Kliknij przycisk **to urządzenie**i hello w obszarze **monitorowanie**, kliknij przycisk **Konfigurowanie ustawień OMS**.
4. Wybierz **Włącz monitorowanie**.
5. W oknie dialogowym Ustawienia OMS hello, wpisz hello **identyfikator obszaru roboczego** i typ hello **klucz obszaru roboczego**.  
   ![Ustawienia](./media/log-analytics-surface-hubs/settings.png)
6. Kliknij przycisk **OK** toocomplete hello konfiguracji.

Pojawia się potwierdzenie informujący o tym, czy powitalne OMS konfiguracja została pomyślnie zastosowana toohello urządzenia. Jeśli tak jest, pojawi się komunikat informujący, że hello agent pomyślnie nawiązano połączenie toohello usługę. urządzenie Hello następnie rozpoczyna wysyłanie tooOMS danych, w którym można wyświetlać i działa na nim.

## <a name="monitor-surface-hubs"></a>Monitor urządzenia Surface Hub.
Monitorowanie sieci urządzeń Surface Hub przy użyciu pakietu OMS jest znacznie takich jak monitorowanie innych zarejestrowanych urządzeń.

1. Zaloguj się toohello portalu OMS.
2. Przejdź toohello Surface Hub rozwiązania pakietu z pulpitu nawigacyjnego.
3. Kondycja urządzenia jest wyświetlana.

   ![Surface Hub pulpitu nawigacyjnego](./media/log-analytics-surface-hubs/surface-hub-dashboard.png)

Można utworzyć [alerty](log-analytics-alerts.md) oparte na istniejących lub niestandardowych dziennik wyszukiwania. Przy użyciu powitalne danych hello OMS zbiera dane z Twojego urządzeń Surface Hub, możesz wyszukać problemy i alert na powitania warunki, które należy zdefiniować dla urządzeń.

## <a name="next-steps"></a>Następne kroki
* Użyj [Zaloguj wyszukiwania analizy dzienników](log-analytics-log-searches.md) tooview szczegółowe dane Surface Hub.
* Utwórz [alerty](log-analytics-alerts.md) toonotify gdy występują problemy z Twojej urządzeń Surface Hub.
