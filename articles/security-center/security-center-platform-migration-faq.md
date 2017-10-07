---
title: "Centrum aaaSecurity platformy migracji — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Często zadawane pytania odpowiedzi na pytania dotyczące hello migracji platform Centrum zabezpieczeń Azure."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 4d1364cd-7847-425a-bb3a-722cb0779f78
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: terrylan
ms.openlocfilehash: fcb14ae83167ef79a60371e4fcb625cf99bee6c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="security-center-platform-migration-faq"></a>Centrum zabezpieczeń platformy migracji — często zadawane pytania
W wczesne 2017 czerwca Centrum zabezpieczeń Azure rozpoczęło się przy użyciu programu Microsoft Monitoring Agent hello toocollect i magazynu danych. toolearn więcej, zobacz [migracji Platform Centrum zabezpieczeń Azure](security-center-platform-migration.md). Często zadawane pytania odpowiedzi na pytania dotyczące hello platformy migracji.

## <a name="data-collection-agents-and-workspaces"></a>Zbieranie danych, agenci i obszary robocze

### <a name="how-is-data-collected"></a>Jak zbierane są dane?
Centrum zabezpieczeń używa hello Microsoft Monitoring Agent toocollect zabezpieczeń danych z maszyn wirtualnych. dane zabezpieczeń Hello zawiera informacje na temat konfiguracji zabezpieczeń, które są używane tooidentify luk w zabezpieczeniach, a zdarzenia zabezpieczeń, które są używane toodetect zagrożeń. Dane zebrane przez agenta hello są przechowywane w istniejących toohello połączone obszaru roboczego analizy dzienników maszyny Wirtualnej lub nowy obszar roboczy utworzony przez Centrum zabezpieczeń. W Centrum zabezpieczeń tworzy nowy obszar roboczy, geolokalizacja hello z hello maszyny Wirtualnej jest brana pod uwagę.

> [!NOTE]
> Witaj Microsoft Monitoring Agent jest hello używać tego samego agenta hello Operations Management Suite (OMS), usługi Analiza dzienników i System Center Operations Manager (SCOM).
>
>

Włączenie zbierania danych dla powitania po raz pierwszy lub podczas migracji subskrypcji Centrum zabezpieczeń sprawdza toosee, hello Microsoft Monitoring Agent jest już zainstalowana jako rozszerzenie Azure na każdym z maszyn wirtualnych. Jeśli nie zainstalowano programu Microsoft Monitoring Agent hello, Centrum zabezpieczeń będą:

- Zainstaluj agenta Microsoft Monitoring hello na powitania maszyny Wirtualnej
   - Jeśli obszar roboczy utworzony przez Centrum zabezpieczeń już istnieje w hello tego samego używanie funkcji geolokalizacji jako hello maszyny Wirtualnej, hello agenta jest połączonych toothis obszaru roboczego
   - obszar roboczy nie istnieje, Centrum zabezpieczeń tworzy nową grupę zasobów i domyślny obszar roboczy w tym używanie funkcji geolokalizacji, a połączenie hello agenta toothat roboczym. Witaj konwencję nazewnictwa hello obszaru roboczego i grupie zasobów są:

       Obszar roboczy: DefaultWorkspace-[identyfikator subskrypcji]-[geograficznie]

       Grupa zasobów: DefaultResouceGroup-[geograficznie]
- Zainstaluj w obszarze roboczym hello rozwiązania Centrum zabezpieczeń

Lokalizacja Hello hello obszaru roboczego jest oparta na lokalizację hello hello maszyny Wirtualnej. toolearn więcej, zobacz [bezpieczeństwo danych](security-center-data-security.md).

> [!NOTE]
> Wcześniejsze tooplatform migracji, Centrum zabezpieczeń zbierane dane z maszyn wirtualnych przy użyciu hello agenta monitorowania Azure i dane są przechowywane na koncie magazynu. Po przeprowadzeniu migracji platform hello Centrum zabezpieczeń używa hello Microsoft Monitoring Agent i toocollect obszaru roboczego, a także przechowywać hello tych samych danych. Po zakończeniu migracji hello można usunąć konta magazynu Hello.
>
>

### <a name="am-i-billed-for-log-analytics-or-oms-on-hello-workspaces-created-by-security-center"></a>Jestem rozliczane analizy dzienników lub OMS na powitania obszary robocze tworzone przez Centrum zabezpieczeń?
Nie. Obszary robocze tworzone przez Centrum zabezpieczeń podczas skonfigurowane dla pakietu OMS na rozliczenia węzła nie wiąże się z OMS opłatami. Karta Centrum zabezpieczeń jest zawsze oparty na rozwiązań zasad i hello zabezpieczeń Centrum zabezpieczeń zainstalowanym obszaru roboczego:

- **Warstwa bezpłatna** — Centrum zabezpieczeń instaluje rozwiązanie "SecurityCenterFree" hello na powitania domyślny obszar roboczy. Nie rozliczenie jest hello warstwę bezpłatna.
- **Warstwy standardowa** — Centrum zabezpieczeń instaluje hello "SecurityCenterFree" i "Zabezpieczenia" rozwiązań na hello domyślny obszar roboczy.

Aby uzyskać więcej informacji o cenach, zobacz [cennik Centrum zabezpieczeń](https://azure.microsoft.com/pricing/details/security-center/). Hello cennik adresy stron zmienia toosecurity magazynu danych i proporcjonalnie rozliczeń począwszy od czerwca 2017 r.

> [!NOTE]
> Warstwa cenowa OMS Hello obszarów roboczych utworzonych przez Centrum zabezpieczeń nie ma wpływu na rozliczenia Centrum zabezpieczeń.
>
>

### <a name="can-i-delete-hello-default-workspaces-created-by-security-center"></a>Czy można usunąć obszary robocze domyślne hello utworzone przez Centrum zabezpieczeń?
**Usuwanie hello domyślny obszar roboczy nie jest zalecane.** Centrum zabezpieczeń używa hello domyślne obszary robocze toostore zabezpieczeń danych z maszyn wirtualnych.  W przypadku usunięcia obszaru roboczego, Centrum zabezpieczeń jest toocollect tych danych i niektóre zalecenia dotyczące zabezpieczeń i alertów są niedostępne

toorecover, Usuń hello Microsoft Monitoring Agent w obszarze roboczym połączonych toohello usunięte maszyny wirtualne hello. Centrum zabezpieczeń ponownie instaluje agenta hello i tworzy nowy domyślny obszarów roboczych.

### <a name="what-if-hello-microsoft-monitoring-agent-was-already-installed-as-an-extension-on-hello-vm"></a>Co zrobić, jeśli hello Microsoft Monitoring Agent została już zainstalowana jako rozszerzenie na powitania maszyny Wirtualnej?
Centrum zabezpieczeń nie zastąpienie istniejących połączeń toouser w obszarach roboczych. Centrum zabezpieczeń magazynów zabezpieczeń danych z maszyny Wirtualnej w obszarze roboczym hello hello już połączone.

### <a name="what-if-i-had-a-microsoft-monitoring-agent-installed-on-hello-machine-but-not-as-an-extension"></a>Co zrobić, jeśli użytkownik miał Microsoft Monitoring Agent zainstalowany na komputerze hello, ale nie jako rozszerzenie?
Jeśli hello Microsoft Monitoring Agent jest zainstalowany bezpośrednio na powitania maszyny Wirtualnej (nie jako rozszerzenie Azure), Centrum zabezpieczeń nie zostanie zainstalowana hello Microsoft Monitoring Agent i monitorowanie zabezpieczeń jest ograniczona.

### <a name="what-is-hello-impact-of-removing-these-extensions"></a>Jaki jest wpływ hello usunięcie tych rozszerzeń?
Jeśli usuniesz hello rozszerzenia monitorowania firmy Microsoft, Centrum zabezpieczeń nie jest możliwe toocollect zabezpieczeń danych z hello maszyny Wirtualnej i niektórych zalecenia dotyczące zabezpieczeń i alertów są niedostępne. W ciągu 24 godzin Centrum zabezpieczeń określa, że hello maszyny Wirtualnej nie ma rozszerzenia hello i ponownie instaluje hello rozszerzenia.

### <a name="how-do-i-stop-hello-automatic-agent-installation-and-workspace-creation"></a>Jak zatrzymać instalację agenta automatyczne hello i tworzenie obszaru roboczego?
Zbieranie danych można wyłączyć dla subskrypcji w zasadach zabezpieczeń hello, ale nie jest to zalecane. Wyłączenie limity kolekcji danych zaleceń Centrum zabezpieczeń i alertów. Zbieranie danych jest wymagane dla subskrypcji na warstwę cenową standardowa hello. zbieranie danych toodisable:

1. Jeśli subskrypcja jest skonfigurowany do warstwy standardowa hello, otwórz hello zasad zabezpieczeń dla tej subskrypcji i wybierz hello **wolne** warstwy.

   ![Warstwa cenowa][1]

2. Następnie należy wyłączyć zbieranie danych, wybierając **poza** na powitania **zasady zabezpieczeń — zbieranie danych** bloku.

   ![Zbieranie danych][2]

### <a name="how-do-i-remove-oms-extensions-installed-by-security-center"></a>Jak usunąć rozszerzenia OMS zainstalowane przez Centrum zabezpieczeń?
Można ręcznie usunąć hello Microsoft Monitoring Agent. Nie jest to zalecane, ponieważ ogranicza zaleceń Centrum zabezpieczeń i alertów.

> [!NOTE]
> Po włączeniu funkcji zbierania danych Centrum zabezpieczeń będzie ponownie zainstaluj agenta powitania po jej usunięciu.  Należy toodisable zbierania danych przed usunięciem ręcznie hello agenta. Zobacz [jak zatrzymać hello agentami automatycznymi instalacji i tworzenie obszaru roboczego?](#how-do-i-stop-the-automatic-agent-installation-and-workspace-creation?) instrukcje dotyczące wyłączenia zbierania danych.
>
>

toomanually Usuń hello agenta:

1.  Otwórz w portalu hello **analizy dzienników**.
2.  W bloku analizy dzienników hello wybierz obszar roboczy:
3.  Wybierz każdej maszyny Wirtualnej nie ma toomonitor i wybierz **rozłączenia**.

   ![Usuń agenta hello][3]

> [!NOTE]
> Jeśli Maszynę wirtualną systemu Linux jest już agent pakietu OMS bez rozszerzeń, usunięcie rozszerzenia hello spowoduje usunięcie również hello agenta i powitania klienta ma tooreinstall go.
>
>

## <a name="existing-oms-customers"></a>Istniejących klientów OMS

### <a name="does-security-center-override-any-existing-connections-between-vms-and-workspaces"></a>Centrum zabezpieczeń zastąpienie istniejących połączeń między maszynami wirtualnymi i obszary robocze?
Jeśli maszyna wirtualna ma już hello Microsoft Monitoring Agent został zainstalowany jako rozszerzenie Azure, Centrum zabezpieczeń nie przesłania hello istniejące połączenie obszaru roboczego. Zamiast tego Centrum zabezpieczeń używa hello istniejący obszar roboczy.

Rozwiązanie Centrum zabezpieczeń jest zainstalowany w obszarze roboczym hello Jeśli nie znajduje się już i rozwiązanie hello jest stosowane tylko toohello odpowiednich maszyn wirtualnych. Po dodaniu rozwiązania jest automatycznie wdrażane przez domyślny tooall systemu Windows i Linux agentów połączonych tooyour obszaru roboczego analizy dzienników. [Rozwiązanie docelowych](../operations-management-suite/operations-management-suite-solution-targeting.md), która jest funkcją OMS umożliwia tooapply zakres tooyour rozwiązania.

Jeśli hello Microsoft Monitoring Agent jest zainstalowany bezpośrednio na powitania maszyny Wirtualnej (nie jako rozszerzenie Azure), Centrum zabezpieczeń nie zostanie zainstalowana hello Microsoft Monitoring Agent i monitorowanie zabezpieczeń jest ograniczony.

### <a name="what-should-i-do-if-i-suspect-that-hello-data-platform-migration-broke-hello-connection-between-one-of-my-vms-and-my-workspace"></a>Co należy zrobić w przypadku podejrzeń, że migracji platformy danych hello spowodowało przerwanie połączenia hello jednego z maszyn wirtualnych i obszar Mój obszar roboczy?
To nie powinno się zdarzyć. Jeśli to się zdarzyć, następnie [utworzyć żądanie pomocy technicznej platformy Azure](../azure-supportability/how-to-create-azure-support-request.md) i zawierają hello poniższe informacje:

- Identyfikator zasobu Azure Hello hello wpływ na maszyny Wirtualnej
- Identyfikator zasobu Azure Hello obszaru roboczego hello skonfigurowane na powitania rozszerzenia przed hello połączenie zostało przerwane
- Hello agent i wersji, który został wcześniej zainstalowany

### <a name="does-security-center-install-solutions-on-my-existing-oms-workspaces-what-are-hello-billing-implications"></a>Centrum zabezpieczeń instaluje rozwiązań na mój istniejących obszarów roboczych OMS? Jakie są skutki rozliczeń hello?
Jeśli Centrum zabezpieczeń zostanie zidentyfikowana maszyny Wirtualnej jest już połączony tooa obszar roboczy utworzony, Centrum zabezpieczeń umożliwia rozwiązań na ten obszar roboczy, zgodnie z tooyour warstwy cenowej. Witaj rozwiązania są stosowane tylko toohello odpowiednich maszyn wirtualnych platformy Azure, za pomocą [przeznaczonych dla rozwiązania](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solution-targeting), więc pozostaje rozliczeń hello hello takie same.

- **Warstwa bezpłatna** — Centrum zabezpieczeń instaluje rozwiązanie "SecurityCenterFree" hello, w obszarze roboczym hello. Nie rozliczenie jest hello warstwę bezpłatna.
- **Warstwy standardowa** — Centrum zabezpieczeń instaluje hello "SecurityCenterFree" i "Zabezpieczenia" rozwiązań na hello obszaru roboczego.

   ![Rozwiązania na domyślny obszar roboczy][4]

> [!NOTE]
> rozwiązania analizy dzienników "Zabezpieczenia" Hello jest rozwiązanie inspekcji w OMS & hello zabezpieczeń.
>
>

### <a name="i-already-have-workspaces-in-my-environment-can-i-use-them-toocollect-security-data"></a>Mam już obszarów roboczych w mojej środowisku, można z nich korzystać toocollect zabezpieczeń danych?
Jeśli maszyna wirtualna ma już hello Microsoft Monitoring Agent został zainstalowany jako rozszerzenie Azure, Centrum zabezpieczeń używa hello istniejącego połączenia obszaru roboczego. Rozwiązanie Centrum zabezpieczeń jest zainstalowany w obszarze roboczym hello Jeśli nie znajduje się już i rozwiązanie hello jest stosowane tylko toohello odpowiednich maszyn wirtualnych za pośrednictwem [przeznaczonych dla rozwiązania](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solution-targeting).

Podczas instalacji Centrum zabezpieczeń hello Microsoft Monitoring Agent na maszynach wirtualnych używa obszarów roboczych domyślne hello utworzone przez Centrum zabezpieczeń. Wkrótce klienci będą mogli tooconfigure, które obszarów roboczych są używane.

### <a name="i-already-have-security-solution-on-my-workspaces-what-are-hello-billing-implications"></a>Mam już rozwiązanie z zakresu zabezpieczeń na mój obszarów roboczych. Jakie są skutki rozliczeń hello?
Witaj rozwiązanie zabezpieczające i inspekcji jest używane tooenable Security Center Standard warstwy funkcje maszynach wirtualnych platformy Azure. Jeśli rozwiązania zabezpieczeń i inspekcji hello jest już zainstalowany w obszarze roboczym, Centrum zabezpieczeń używa hello istniejącego rozwiązania. Nie została zmieniona w rozliczeń.

## <a name="next-steps"></a>Następne kroki
Zobacz toolearn więcej informacji na temat migracji platform hello Centrum zabezpieczeń

- [Centrum zabezpieczeń Azure platformy migracji](security-center-platform-migration.md)
- [Przewodnik dotyczący rozwiązywania problemów w Centrum zabezpieczeń Azure](security-center-troubleshooting-guide.md)

<!--Image references-->
[1]: ./media/security-center-platform-migration-faq/pricing-tier.png
[2]: ./media/security-center-platform-migration-faq/data-collection.png
[3]: ./media/security-center-platform-migration-faq/remove-the-agent.png
[4]: ./media/security-center-platform-migration-faq/solutions.png
