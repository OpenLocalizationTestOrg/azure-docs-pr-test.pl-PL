---
title: "aaaAzure migracji Platform Centrum zabezpieczeń | Dokumentacja firmy Microsoft"
description: "W tym dokumencie opisano sposób toohello niektóre zmiany danych w Centrum zabezpieczeń Azure są zbierane."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 80246b00-bdb8-4bbc-af54-06b7d12acf58
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: yurid
ms.openlocfilehash: 28cb8d85912a3f62941cf113da51070081b5eda2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-platform-migration"></a>Migracja platformy usługi Azure Security Center

Począwszy od początku czerwca 2017, Centrum zabezpieczeń Azure wprowadza ważne zmiany toohello sposób dane są zbierane i przechowywane.  Te zmiany odblokowania nowe funkcje, takie jak hello możliwości tooeasily wyszukiwania zabezpieczeń danych i lepiej wyrównana z monitorowanie usług i innych zarządzania platformy Azure.

> [!NOTE]
> Migracja platformy Hello nie powinny mieć wpływ na zasoby produkcji, a nie jest konieczne z Twojej strony żadna akcja.


## <a name="whats-happening-during-this-platform-migration"></a>Co się stanie podczas tej migracji platformy?

Centrum zabezpieczeń używane wcześniej hello agenta monitorowania Azure toocollect zabezpieczeń danych z maszyn wirtualnych. W tym informacje o konfiguracjach zabezpieczeń, które są używane tooidentify luk w zabezpieczeniach, a zdarzenia zabezpieczeń, które są używane toodetect zagrożeń. Te dane były przechowywane na kontach magazynu na platformie Azure.

Teraz, Centrum zabezpieczeń używa hello Microsoft Monitoring Agent — jest to hello używać tego samego agenta hello Operations Management Suite i analizy dzienników usługi. Dane zbierane z tego agenta są przechowywane w każdej istniejącej *analizy dzienników* [obszaru roboczego](../log-analytics/log-analytics-manage-access.md) skojarzone z subskrypcją platformy Azure lub nowych obszarów roboczych, uwzględniając używanie funkcji geolokalizacji hello maszyny Wirtualnej na powitania konta .

## <a name="agent"></a>Agent

W ramach przejścia hello, hello Microsoft Monitoring Agent (dla [Windows](../log-analytics/log-analytics-windows-agents.md) lub [Linux](../log-analytics/log-analytics-linux-agents.md)) jest zainstalowany na wszystkich maszynach wirtualnych platformy Azure, z których obecnie są zbierane dane.  Jeśli hello maszyna wirtualna ma już hello Microsoft Monitoring Agent został zainstalowany, Centrum zabezpieczeń wykorzystuje hello bieżącego zainstalowany agent.

W danym okresie czasu (zazwyczaj za kilka dni) zarówno agentów uruchomi tooensure siebie płynne przejście bez utraty danych. Umożliwi to Microsoft działa toovalidate, który hello nowy potok danych przed zaprzestanie stosowania hello bieżącego procesu. Raz zweryfikowano hello agenta monitorowania Azure zostaną usunięte z maszyn wirtualnych. Nie jest wymagane żadne działanie ze strony użytkownika. Po przeprowadzeniu migracji wszystkich klientów otrzymasz wiadomość e-mail z powiadomieniem.
 
Nie zaleca się ręczne odinstalowanie hello agenta monitorowania Azure podczas migracji hello jako luk w danych zabezpieczeń może spowodować. Jeśli potrzebujesz dodatkowej pomocy, skonsultuj się z [działem obsługi klienta i pomocą techniczną firmy Microsoft](https://support.microsoft.com/contactus/). 

Microsoft Monitoring Agent dla systemu Windows Hello wymaga użycia portu TCP 443, przeczytaj [Azure Security Center Troubleshooting Guide](security-center-troubleshooting-guide.md) Aby uzyskać więcej informacji.


> [!NOTE] 
> Ponieważ hello Microsoft Monitoring Agent może być używany przez inne zarządzania platformy Azure i monitorowanie usług, hello agent nie zostanie usunięta automatycznie po wyłączeniu zbierania danych w Centrum zabezpieczeń. Jednak można ręcznie odinstalować agenta hello w razie potrzeby.

## <a name="workspace"></a>Obszar roboczy

Jak opisano wcześniej, danych zbieranych z programu Microsoft Monitoring Agent (imieniu Centrum zabezpieczeń) są przechowywane w istniejących analizy dzienników hello obszarów roboczych skojarzone z subskrypcją platformy Azure lub nowych obszarów roboczych, biorąc pod uwagę hello Używanie funkcji geolokalizacji hello maszyny Wirtualnej.

W hello portalu Azure możesz wyszukać toosee listę obszarów roboczych usługi Analiza dzienników, wraz ze wszystkimi utworzone przez Centrum zabezpieczeń. W przypadku nowych obszarów roboczych zostanie utworzona powiązana grupa zasobów. Stosowana jest następująca konwencja nazewnictwa:

- Obszar roboczy: *DefaultWorkspace-[identyfikator-subskrypcji]-[lokalizacja-geograficzna]*
- Grupa zasobów: *DefaultResouceGroup-[lokalizacja-geograficzna]* 
 
W przypadku obszarów roboczych utworzonych przez usługę Security Center dane są przechowywane przez 30 dni. Dla istniejących obszarów roboczych przechowywania jest oparta na roboczym hello warstwy cenowej.

> [!NOTE]
> Dane wcześniej zebrane przez usługę Security Center pozostają na kontach magazynu. Po zakończeniu migracji hello należy usunąć te konta magazynu.

### <a name="oms-security-solution"></a>Rozwiązanie OMS Security 

W przypadku istniejących klientów, którzy nie mają zainstalowanego rozwiązania OMS Security, firma Microsoft zainstaluje je w ich obszarze roboczym, ale tylko dla maszyn wirtualnych platformy Azure. Nie należy odinstalowywać tego rozwiązania, ponieważ nie ma żadnego automatycznego korygowania, jeśli zostanie to zrobione za pomocą konsoli zarządzania usługą OMS.


## <a name="other-updates"></a>Inne aktualizacje

W połączeniu z funkcją migracji platform hello możemy są wprowadza pewne dodatkowe niewielkie aktualizacje:

- Będą obsługiwane dodatkowe wersje systemów operacyjnych. Lista hello [tutaj](security-center-faq.md#virtual-machines).
- Lista Hello luk w zabezpieczeniach systemu operacyjnego zostanie rozszerzona. Lista hello [tutaj](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).
- [Ceny](https://azure.microsoft.com/pricing/details/security-center/) będą ustalane proporcjonalnie do liczby godzin (wcześniej do liczby dni), co przyniesie oszczędności niektórym klientom.
- Zbieranie danych będzie wymagane i automatycznie włączona dla klientów w warstwie cenowej standardowa hello.
- Usługa Azure Security Center rozpocznie odnajdywanie rozwiązań chroniących przed złośliwym kodem, które nie zostały wdrożone za pomocą rozszerzeń platformy Azure. Najpierw dostępne będzie odnajdywanie programów Endpoint Protection i Defender firmy Symantec dla systemu Windows 2016.
- Zasady zapobiegania i powiadomienia tylko są konfigurowane na powitania *subskrypcji* poziomu, ale cennik nadal można ustawić na powitania *grupy zasobów* poziom

