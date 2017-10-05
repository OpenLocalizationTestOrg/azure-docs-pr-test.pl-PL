---
title: "Centrum zabezpieczeń platformy migracji — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Często zadawane pytania odpowiedzi na pytania dotyczące migracji platform Centrum zabezpieczeń Azure."
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
ms.openlocfilehash: 2ffbaca614d667db565197f3c13b1658fffc2a7c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="security-center-platform-migration-faq"></a>Centrum zabezpieczeń platformy migracji — często zadawane pytania
W wczesne 2017 czerwca Centrum zabezpieczeń Azure rozpoczęło się przy użyciu programu Microsoft Monitoring Agent do gromadzenia i przechowywania danych. Aby dowiedzieć się więcej, zobacz [migracji Platform Centrum zabezpieczeń Azure](security-center-platform-migration.md). Często zadawane pytania odpowiedzi na pytania dotyczące migracji platform.

## <a name="data-collection-agents-and-workspaces"></a>Zbieranie danych, agenci i obszary robocze

### <a name="how-is-data-collected"></a>Jak zbierane są dane?
Centrum zabezpieczeń używa programu Microsoft Monitoring Agent zbierania danych zabezpieczeń z maszyn wirtualnych. Dane zabezpieczeń zawiera informacje na temat konfiguracji zabezpieczeń, które są używane do identyfikowania luk w zabezpieczeniach, a zdarzenia zabezpieczeń, które są używane do wykrywania zagrożeń. Dane zebrane przez agenta są przechowywane w istniejącym obszarem roboczym analizy dzienników podłączony do maszyny Wirtualnej lub nowy obszar roboczy utworzony przez Centrum zabezpieczeń. W Centrum zabezpieczeń tworzy nowy obszar roboczy, używanie funkcji geolokalizacji maszyny wirtualnej jest brana pod uwagę.

> [!NOTE]
> Microsoft Monitoring Agent jest tego samego agenta używane przez Operations Management Suite (OMS), usługi Analiza dzienników i System Center Operations Manager (SCOM).
>
>

Po włączeniu funkcji zbierania danych po raz pierwszy lub podczas migracji subskrypcji Centrum zabezpieczeń sprawdza, czy program Microsoft Monitoring Agent jest już zainstalowany jako rozszerzenie Azure na każdym z maszyn wirtualnych. Jeśli nie zainstalowano programu Microsoft Monitoring Agent, Centrum zabezpieczeń będą:

- Zainstaluj program Microsoft Monitoring agent w maszynie Wirtualnej
   - obszar roboczy utworzony przez Centrum zabezpieczeń już istnieje w tej samej używanie funkcji geolokalizacji jako maszyny Wirtualnej, agent jest podłączony do tego obszaru roboczego
   - obszar roboczy nie istnieje, Centrum zabezpieczeń tworzy nową grupę zasobów i domyślny obszar roboczy w tym używanie funkcji geolokalizacji oraz Połącz agenta z tego obszaru roboczego. Konwencja nazewnictwa dla grupy obszaru roboczego i zasobów są:

       Obszar roboczy: DefaultWorkspace-[identyfikator subskrypcji]-[geograficznie]

       Grupa zasobów: DefaultResouceGroup-[geograficznie]
- Instalowanie rozwiązania Centrum zabezpieczeń w obszarze roboczym

Lokalizacja obszaru roboczego jest oparta na lokalizacji maszyny wirtualnej. Aby dowiedzieć się więcej, zobacz [bezpieczeństwo danych](security-center-data-security.md).

> [!NOTE]
> Przed migracją platformy Centrum zabezpieczeń zbierane dane z maszyn wirtualnych przy użyciu agenta monitorowania Azure, a dane są przechowywane na koncie magazynu. Po zakończeniu migracji platform Centrum zabezpieczeń korzysta z programu Microsoft Monitoring Agent obszaru roboczego do gromadzenia i przechowywania tych samych danych. Po zakończeniu migracji można usunąć konta magazynu.
>
>

### <a name="am-i-billed-for-log-analytics-or-oms-on-the-workspaces-created-by-security-center"></a>Jestem rozliczane analizy dzienników lub OMS na obszary robocze tworzone przez Centrum zabezpieczeń?
Nie. Obszary robocze tworzone przez Centrum zabezpieczeń podczas skonfigurowane dla pakietu OMS na rozliczenia węzła nie wiąże się z OMS opłatami. Rozliczeń Centrum zabezpieczeń jest zawsze na podstawie zasad zabezpieczeń Centrum zabezpieczeń i rozwiązań zainstalowanym obszaru roboczego:

- **Warstwa bezpłatna** — rozwiązanie "SecurityCenterFree" w Centrum zabezpieczeń jest instalowana na domyślny obszar roboczy. Nie są opłaty naliczane w warstwie bezpłatna.
- **Warstwy standardowa** — rozwiązania "SecurityCenterFree" i "Zabezpieczenia" w Centrum zabezpieczeń jest instalowana na domyślny obszar roboczy.

Aby uzyskać więcej informacji o cenach, zobacz [cennik Centrum zabezpieczeń](https://azure.microsoft.com/pricing/details/security-center/). Stronie cen adresów zmiany do magazynu danych zabezpieczeń i proporcjonalnie rozliczeń począwszy od czerwca 2017 r.

> [!NOTE]
> OMS cenowym obszarów roboczych utworzonych przez Centrum zabezpieczeń nie ma wpływu na rozliczenia Centrum zabezpieczeń.
>
>

### <a name="can-i-delete-the-default-workspaces-created-by-security-center"></a>Czy można usunąć domyślnego obszarów roboczych, utworzonych przez Centrum zabezpieczeń?
**Usuwanie domyślny obszar roboczy nie jest zalecane.** Centrum zabezpieczeń używa domyślne obszary robocze do przechowywania danych zabezpieczeń z maszyn wirtualnych.  W przypadku usunięcia obszaru roboczego, Centrum zabezpieczeń nie będzie mógł zbierać dane i niektóre zalecenia dotyczące zabezpieczeń i alertów są niedostępne

Aby odzyskać, Usuń program Microsoft Monitoring Agent na maszynach wirtualnych podłączone do usuniętego obszaru roboczego. Centrum zabezpieczeń ponownie instaluje agenta i tworzy nowy domyślny obszarów roboczych.

### <a name="what-if-the-microsoft-monitoring-agent-was-already-installed-as-an-extension-on-the-vm"></a>Co w przypadku programu Microsoft Monitoring Agent została już zainstalowana jako rozszerzenie na maszynie Wirtualnej?
Centrum zabezpieczeń nie zastępują istniejące połączenia do użytkownika obszarów roboczych. Centrum zabezpieczeń przechowuje dane zabezpieczeń z maszyny Wirtualnej w obszarze roboczym już połączone.

### <a name="what-if-i-had-a-microsoft-monitoring-agent-installed-on-the-machine-but-not-as-an-extension"></a>Co zrobić, jeśli użytkownik miał Microsoft Monitoring Agent zainstalowany na komputerze, ale nie jako rozszerzenie?
Po zainstalowaniu programu Microsoft Monitoring Agent bezpośrednio na maszyny Wirtualnej (nie jako rozszerzenie Azure), Centrum zabezpieczeń nie zostanie zainstalowany program Microsoft Monitoring Agent oraz monitorowanie zabezpieczeń jest ograniczona.

### <a name="what-is-the-impact-of-removing-these-extensions"></a>Jaki jest wpływ usunięcia tych rozszerzeń?
Jeśli usuniesz rozszerzenia monitorowania firmy Microsoft, Centrum zabezpieczeń nie będzie mógł zbierać dane zabezpieczeń z maszyny Wirtualnej, a niektóre zalecenia dotyczące zabezpieczeń i alertów są niedostępne. W ciągu 24 godzin Centrum zabezpieczeń określa, że maszyna wirtualna nie ma rozszerzenia i ponownie instaluje rozszerzenia.

### <a name="how-do-i-stop-the-automatic-agent-installation-and-workspace-creation"></a>Jak zatrzymać agenta automatycznego tworzenia instalacji i obszar roboczy?
Zbieranie danych można wyłączyć dla subskrypcji w zasadach zabezpieczeń, ale nie jest to zalecane. Wyłączenie limity kolekcji danych zaleceń Centrum zabezpieczeń i alertów. Zbieranie danych jest wymagane dla subskrypcji na warstwa cenowa standardowa. Aby wyłączyć zbieranie danych:

1. Jeśli subskrypcja jest skonfigurowany do warstwy standardowa, otworzyć przystawkę Zasady zabezpieczeń dla tej subskrypcji i wybierz **wolne** warstwy.

   ![Warstwa cenowa][1]

2. Następnie należy wyłączyć zbieranie danych, wybierając **poza** na **zasady zabezpieczeń — zbieranie danych** bloku.

   ![Zbieranie danych][2]

### <a name="how-do-i-remove-oms-extensions-installed-by-security-center"></a>Jak usunąć rozszerzenia OMS zainstalowane przez Centrum zabezpieczeń?
Można ręcznie usunąć agenta monitorowania firmy Microsoft. Nie jest to zalecane, ponieważ ogranicza zaleceń Centrum zabezpieczeń i alertów.

> [!NOTE]
> Po włączeniu funkcji zbierania danych Centrum zabezpieczeń będzie ponownie zainstalować agenta po jej usunięciu.  Należy wyłączyć zbieranie danych przed ręczne usunięcie agenta. Zobacz [jak Zatrzymaj agenta automatycznego tworzenia instalacji i obszar roboczy?](#how-do-i-stop-the-automatic-agent-installation-and-workspace-creation?) instrukcje dotyczące wyłączenia zbierania danych.
>
>

Aby ręcznie usunąć agenta:

1.  W portalu, otwórz **analizy dzienników**.
2.  W bloku analizy dzienników wybierz obszar roboczy:
3.  Wybierz każdej maszyny Wirtualnej, których nie chcesz, aby monitorować i wybierz **rozłączenia**.

   ![Usuń agenta][3]

> [!NOTE]
> Jeśli Maszynę wirtualną systemu Linux jest już agent pakietu OMS bez rozszerzeń, usunięcie rozszerzenia spowoduje usunięcie również agenta i klient ma zainstalować go ponownie.
>
>

## <a name="existing-oms-customers"></a>Istniejących klientów OMS

### <a name="does-security-center-override-any-existing-connections-between-vms-and-workspaces"></a>Centrum zabezpieczeń zastąpienie istniejących połączeń między maszynami wirtualnymi i obszary robocze?
Jeśli maszyna wirtualna ma już zainstalowany jako rozszerzenie Azure Microsoft Monitoring Agent, Centrum zabezpieczeń nie zastępują istniejące połączenie obszaru roboczego. Zamiast tego Centrum zabezpieczeń korzysta z istniejącym obszarem roboczym.

Rozwiązanie Centrum zabezpieczeń jest zainstalowany w obszarze roboczym Jeśli nie znajduje się już i rozwiązanie jest stosowane tylko do odpowiednich maszyn wirtualnych. Po dodaniu rozwiązania jest automatycznie wdrażane domyślnie do wszystkich agentów systemu Windows i Linux podłączone do obszaru roboczego analizy dzienników. [Rozwiązanie docelowych](../operations-management-suite/operations-management-suite-solution-targeting.md), która jest funkcją OMS umożliwia stosowanie zakresu do rozwiązań.

Po zainstalowaniu programu Microsoft Monitoring Agent bezpośrednio na Maszynie wirtualnej (nie jako rozszerzenie Azure) Centrum zabezpieczeń nie zostanie zainstalowany program Microsoft Monitoring Agent oraz monitorowanie zabezpieczeń jest ograniczony.

### <a name="what-should-i-do-if-i-suspect-that-the-data-platform-migration-broke-the-connection-between-one-of-my-vms-and-my-workspace"></a>Co należy zrobić w przypadku podejrzeń, że migracja danych platformy spowodowało przerwanie połączenia między jedną z maszyn wirtualnych i obszar Mój obszar roboczy?
To nie powinno się zdarzyć. Jeśli to się zdarzyć, następnie [utworzyć żądanie pomocy technicznej platformy Azure](../azure-supportability/how-to-create-azure-support-request.md) i podaj następujące informacje:

- Identyfikator zasobu Azure wpływ na maszynie Wirtualnej
- Identyfikator zasobów platformy Azure w obszarze roboczym skonfigurowane na rozszerzenia przed połączenie zostało przerwane
- Agent i wersji, który został wcześniej zainstalowany

### <a name="does-security-center-install-solutions-on-my-existing-oms-workspaces-what-are-the-billing-implications"></a>Centrum zabezpieczeń instaluje rozwiązań na mój istniejących obszarów roboczych OMS? Jakie są skutki rozliczeniowym?
Gdy Centrum zabezpieczeń rozpozna, że maszyna wirtualna jest już połączona z obszaru roboczego, który został utworzony, Centrum zabezpieczeń umożliwia rozwiązań na ten obszar roboczy zgodnie z warstwy cenowej. Rozwiązania są stosowane tylko do odpowiednich maszynach wirtualnych platformy Azure za pośrednictwem [przeznaczonych dla rozwiązania](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solution-targeting), więc rozliczenia jest taka sama.

- **Warstwa bezpłatna** — Centrum zabezpieczeń instaluje rozwiązanie "SecurityCenterFree" w obszarze roboczym. Nie są opłaty naliczane w warstwie bezpłatna.
- **Warstwy standardowa** — Centrum zabezpieczeń instaluje rozwiązania "SecurityCenterFree" i "Zabezpieczenia" w obszarze roboczym.

   ![Rozwiązania na domyślny obszar roboczy][4]

> [!NOTE]
> Rozwiązanie "Zabezpieczenia" w Log Analytics to rozwiązanie zabezpieczeń i inspekcji w OMS.
>
>

### <a name="i-already-have-workspaces-in-my-environment-can-i-use-them-to-collect-security-data"></a>Mam już obszarów roboczych w mojej środowisku, można z nich korzystać do zbierania danych zabezpieczeń?
Jeśli maszyna wirtualna ma już zainstalowany jako rozszerzenie Azure Microsoft Monitoring Agent, Centrum zabezpieczeń używa istniejącego połączenia obszaru roboczego. Rozwiązanie Centrum zabezpieczeń jest zainstalowany w obszarze roboczym Jeśli nie znajduje się już i rozwiązanie jest stosowane tylko do odpowiednich maszyn wirtualnych za pośrednictwem [przeznaczonych dla rozwiązania](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solution-targeting).

Podczas instalowania programu Microsoft Monitoring Agent na maszynach wirtualnych Centrum zabezpieczeń używa domyślnej obszarów roboczych, utworzonych przez Centrum zabezpieczeń. Wkrótce klienci będą mogli jej konfigurować na które obszarów roboczych są używane.

### <a name="i-already-have-security-solution-on-my-workspaces-what-are-the-billing-implications"></a>Mam już rozwiązanie z zakresu zabezpieczeń na mój obszarów roboczych. Jakie są skutki rozliczeniowym?
Aby włączyć funkcje warstwy standardowa Centrum zabezpieczeń dla maszyn wirtualnych platformy Azure jest używane rozwiązanie zabezpieczające i inspekcji. Jeśli rozwiązania zabezpieczeń i inspekcji jest już zainstalowany w obszarze roboczym, Centrum zabezpieczeń używa istniejącego rozwiązania. Nie została zmieniona w rozliczeń.

## <a name="next-steps"></a>Następne kroki
Aby dowiedzieć się więcej na temat migracji platform Centrum zabezpieczeń, zobacz

- [Centrum zabezpieczeń Azure platformy migracji](security-center-platform-migration.md)
- [Przewodnik dotyczący rozwiązywania problemów w Centrum zabezpieczeń Azure](security-center-troubleshooting-guide.md)

<!--Image references-->
[1]: ./media/security-center-platform-migration-faq/pricing-tier.png
[2]: ./media/security-center-platform-migration-faq/data-collection.png
[3]: ./media/security-center-platform-migration-faq/remove-the-agent.png
[4]: ./media/security-center-platform-migration-faq/solutions.png
