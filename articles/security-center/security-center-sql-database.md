---
title: "aaaAzure usługi Centrum zabezpieczeń i baza danych SQL Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak Centrum zabezpieczeń można zabezpieczyć baz danych w bazie danych SQL Azure."
services: sql-database
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: f109adfd-daed-4257-9692-2042a1399480
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 173590500f0ce64140f214ada24b9692e01dbd4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-and-azure-sql-database-service"></a>Usługa Centrum zabezpieczeń Azure i bazy danych SQL Azure
[Centrum zabezpieczeń Azure](https://azure.microsoft.com/documentation/services/security-center/) pomaga zapobiec, wykrywania i reagowania toothreats. Zapewnia zintegrowane monitorowanie zabezpieczeń i zarządzanie zasadami subskrypcji platformy Azure, pomaga wykrywać zagrożenia, które w przeciwnym razie mogłyby pozostać niezauważone, a także współpracuje z szerokim ekosystemem rozwiązań z zakresu zabezpieczeń.

W tym artykule opisano, jak Centrum zabezpieczeń można zabezpieczyć baz danych w bazie danych SQL Azure.

## <a name="why-use-security-center"></a>Dlaczego warto korzystać z usługi Security Center?
Centrum zabezpieczeń pomaga chronić dane w bazie danych SQL, zapewniając wgląd w zabezpieczenia hello wszystkich serwerów i baz danych. Centrum zabezpieczeń można:

* Definiowanie zasad szyfrowania bazy danych SQL i inspekcji.
* Monitorowanie zabezpieczeń hello zasobów bazy danych SQL za pośrednictwem wszystkich subskrypcji.
* Szybkie identyfikowanie i Korygowanie problemów z zabezpieczeniami.
* Integracja alertów z [wykrywanie zagrożeń bazy danych SQL Azure](../sql-database/sql-database-threat-detection.md).

Ponadto toohelping ochrony zasobów bazy danych SQL, Centrum zabezpieczeń zawiera także monitorowanie zabezpieczeń i zarządzanie nim dla maszyn wirtualnych platformy Azure, usługi w chmurze, aplikacji, usług i sieci wirtualnych. Dowiedz się więcej na temat Centrum zabezpieczeń [tutaj](security-center-intro.md).

## <a name="prerequisites"></a>Wymagania wstępne
wprowadzenie do Centrum zabezpieczeń tooget, musi mieć tooMicrosoft subskrypcji Azure. Warstwa bezpłatna Hello Centrum zabezpieczeń jest włączone w ramach subskrypcji. Aby uzyskać więcej informacji na wolne Centrum zabezpieczeń i warstwy standardowa, zobacz [cennik Centrum zabezpieczeń](https://azure.microsoft.com/pricing/details/security-center/).

Centrum zabezpieczeń obsługuje dostęp opartej na rolach. toolearn więcej informacji na temat kontroli dostępu opartej na rolach (RBAC) na platformie Azure, zobacz [kontroli dostępu opartej na roli Azure Active Directory](../active-directory/role-based-access-control-configure.md). Witaj często zadawane pytania na temat Centrum zabezpieczeń zawiera informacje na temat [obsługi uprawnienia w Centrum zabezpieczeń](security-center-faq.md#permissions).

## <a name="access-security-center"></a>Dostęp do usługi Security Center
Dostęp do Centrum zabezpieczeń hello [portalu Azure](https://azure.microsoft.com/features/azure-portal/). [Zaloguj się w portalu toohello](https://portal.azure.com/) i wybierz hello **opcji Centrum zabezpieczeń**.

![Opcja Centrum zabezpieczeń][1]

Witaj **Centrum zabezpieczeń** zostanie otwarty blok.
![Blok Centrum zabezpieczeń][2]

## <a name="set-security-policy"></a>Ustawianie zasad zabezpieczeń
Zasady zabezpieczeń definiuje zestaw hello formantów, które są zalecane dla zasobów w ramach hello określonej subskrypcji lub grupy zasobów. W Centrum zabezpieczeń można zdefiniować zasady dla subskrypcji lub grupy zasobów zgodnie z związanych z zabezpieczeniami tooyour firmy i typem aplikacji hello lub czułości hello danych w każdej subskrypcji.

Tooshow zasady można ustawić zalecenia dotyczące inspekcji SQL i niewidoczne szyfrowanie danych SQL (funkcji TDE).

* Po ponownym włączeniu **inspekcję SQL i wykrywania zagrożeń**, Centrum zabezpieczeń zaleca się, że włączyć przeprowadzanie inspekcji tooAzure dostępu do bazy danych dla zapewnienia zgodności, zaawansowanego wykrywania i badań do celów.
* Po ponownym włączeniu **niewidoczne szyfrowanie danych SQL**, że szyfrowanie magazynowane zaleca Centrum zabezpieczeń jest włączone dla bazy danych SQL Azure, skojarzonych kopii zapasowych i plików dziennika transakcji.

tooset zasady zabezpieczeń, wybierz hello **zasad** kafelka w bloku Centrum zabezpieczeń hello. Na powitania **zasady zabezpieczeń** bloku, na którym ma zostać zasady zabezpieczeń hello tooenable subskrypcji wybierz hello. Wybierz **zasady zapobiegania** i włączyć **na** hello zalecenia dotyczące zabezpieczeń, które mają toouse w tej subskrypcji.
![Zasady zabezpieczeń][3]

toolearn więcej, zobacz [ustawiania zasad zabezpieczeń](security-center-policies.md).

## <a name="manage-security-recommendation"></a>Zarządzanie zalecana ze względów bezpieczeństwa
Centrum zabezpieczeń okresowo analizuje stan zabezpieczeń hello zasobów platformy Azure. Po znalezieniu potencjalnych luk w zabezpieczeniach usługa Security Center tworzy odpowiednie zalecenia. zalecenia Hello pomocne hello proces konfigurowania kontrolek hello potrzebne.

Po ustawieniu zasad zabezpieczeń Centrum zabezpieczeń analizuje stan zabezpieczeń hello z zasobów tooidentify potencjalnych luk w zabezpieczeniach. zalecenia Hello są wyświetlane w formacie tabeli, w którym każdy wiersz zawiera jeden zaleceń. Użyj hello jako toohelp odwołania, zrozumieć hello dostępne zalecenia dotyczące bazy danych SQL Azure i jakie każde zalecenie jest w przypadku zastosowania w poniższej tabeli. Wybieranie zalecenie ma tooan artykułu, w którym wyjaśniono, jak tooimplement hello zalecenia w Centrum zabezpieczeń.

| Zalecenie | Opis |
| --- | --- |
| [Włączanie inspekcji i wykrywania zagrożeń na serwerach SQL](security-center-enable-auditing-on-sql-servers.md) |Zaleca się włączenie inspekcji i wykrywania zagrożeń dla serwerów baz danych SQL. (Tylko w przypadku usługi baza danych SQL. Nie obejmuje programu Microsoft SQL Server uruchomiony na maszynach wirtualnych). |
| [Włączanie inspekcji i wykrywania zagrożeń baz danych SQL](security-center-enable-auditing-on-sql-databases.md) |Zaleca się włączenie inspekcji i wykrywania zagrożeń dla baz danych SQL Database. (Tylko w przypadku usługi baza danych SQL. Nie obejmuje programu Microsoft SQL Server uruchomiony na maszynach wirtualnych). |
| [Włączanie technologii Transparent Data Encryption](security-center-enable-transparent-data-encryption.md) |Zaleca się, aby włączyć szyfrowanie dla bazy danych SQL. (Tylko usługa SQL Database). |

toosee zalecenia dotyczące zasobów platformy Azure, wybierz hello **zalecenia** kafelka w bloku Centrum zabezpieczeń hello. Na powitania **zalecenia** bloku, wybierz Szczegóły toosee zalecenia. W tym przykładzie załóżmy wybierz **Włączanie inspekcji i wykrywanie zagrożeń na serwerach SQL**.

![Zalecenia][4]

Jak pokazano poniżej przedstawiono Centrum zabezpieczeń hello serwerów SQL, których nie włączono inspekcji i wykrywania zagrożeń. Po włączeniu inspekcji można skonfigurować ustawienia wykrywanie zagrożeń i alerty w wiadomościach e-mail tooreceive ustawień zabezpieczeń. Wykrywanie zagrożeń alerty po wykryciu nietypowe działania bazy danych, które wskazują potencjalne bazy danych toohello zagrożenia zabezpieczeń. Witaj alerty są wyświetlane na pulpicie nawigacyjnym Centrum zabezpieczeń hello.
![Inspekcja i wykrywania zagrożeń][5]

Wykonaj kroki hello w [wykrywanie zagrożeń bazy danych SQL w portalu Azure hello](../sql-database/sql-database-threat-detection-portal.md) tooturn na i skonfiguruj wykrywanie zagrożeń i listę hello tooconfigure wiadomości e-mail, które będą wysyłane alerty zabezpieczeń po wykryciu nietypowych działań.

toolearn więcej informacji na temat zalecenia, zobacz [Zarządzanie zaleceniami dotyczącymi zabezpieczeń](security-center-recommendations.md).

## <a name="monitor-security-health"></a>Monitoruj kondycję zabezpieczeń
Po włączeniu [zasady zabezpieczeń](security-center-policies.md) dla zasobów subskrypcji Centrum zabezpieczeń będzie analizować zabezpieczenia hello z zasobów tooidentify potencjalnych luk w zabezpieczeniach.  Witaj stan zabezpieczeń zasobów można wyświetlić w hello **kondycja zabezpieczeń zasobów** kafelka. Po kliknięciu **danych** w hello **kondycja zabezpieczeń zasobów** kafelku hello **zasobów danych** zostanie otwarty blok zawierający SQL zalecenia dotyczące problemów, takich jak przeprowadzanie inspekcji i przejrzysty szyfrowanie danych nie jest włączone. Ma ona również zalecenia dotyczące ogólnej kondycji stanu hello hello bazy danych.
![Kondycja zabezpieczeń zasobów][6]

toolearn więcej, zobacz [monitorowanie kondycji zabezpieczeń](security-center-monitoring.md).

## <a name="manage-and-respond-toosecurity-alerts"></a>Zarządzanie i reagowanie na alerty toosecurity
Centrum zabezpieczeń automatycznie gromadzi, analizuje i integruje dane dzienników z [wykrywanie zagrożeń SQL Azure](../sql-database/sql-database-threat-detection.md), jak i innych zasobów platformy Azure, toodetect prawdziwe zagrożenia i redukować liczbę fałszywych alarmów. Lista alertów zabezpieczeń uporządkowanych według priorytetu jest wyświetlany w Centrum zabezpieczeń oraz hello informacje potrzebne tooquickly Zbadaj hello problem i zalecenia dotyczące tooremediate atak.

toosee alerty, wybierz hello **alerty zabezpieczeń** kafelka w bloku Centrum zabezpieczeń hello. Na powitania **alerty zabezpieczeń** bloku, wybierz alert toolearn więcej informacji o zdarzeniach hello wyzwalane hello oraz, jeśli kroki, możesz muszą tooremediate tootake atak. W tym przykładzie załóżmy wybierz **iniekcja kodu SQL potencjalne**.
![Alerty zabezpieczeń][7]

Jak pokazano poniżej, Centrum zabezpieczeń zapewnia dodatkowe informacje, które oferuje wgląd w jakie alertów wyzwalanych hello hello docelowych zasobów, gdy stosowane hello źródłowy adres IP i zaleceń dotyczących tooremediate.
![Potencjalne iniekcja kodu SQL][8]

toolearn więcej, zobacz [zarządzanie i odpowiada alerty toosecurity](security-center-managing-and-responding-alerts.md).

## <a name="next-steps"></a>Następne kroki
* [Często zadawane pytania dotyczące Centrum zabezpieczeń](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi hello Znajdź.
* [Przewodnik dotyczący planowania i operacji Centrum zabezpieczeń](security-center-planning-and-operations-guide.md) — Wykonaj zestaw kroków i zadań toooptimize korzystanie z Centrum zabezpieczeń, w oparciu o wymagania dotyczące zabezpieczeń oraz modelu zarządzania chmurą w organizacji.
* [Bezpieczeństwo danych Centrum zabezpieczeń](security-center-data-security.md) — Dowiedz się, jak Centrum zabezpieczeń zbiera i przetwarza dane dotyczące zasobów platformy Azure, w tym informacje o konfiguracji, metadane, dzienniki zdarzeń i pliki zrzutu awaryjnego.
* [Obsługi zdarzeń zabezpieczeń](security-center-incident.md) — Dowiedz się, jak zabezpieczenia hello toouse alertów możliwości w Centrum zabezpieczeń tooassist w obsługi zdarzeń zabezpieczeń.

<!--Image references-->
[1]: ./media/security-center-sql-database/security-center.png
[2]: ./media/security-center-sql-database/security-center-blade.png
[3]: ./media/security-center-sql-database/security-policy.png
[4]: ./media/security-center-sql-database/recommendation.png
[5]: ./media/security-center-sql-database/turn-on-auditing.png
[6]: ./media/security-center-sql-database/monitor-health.png
[7]: ./media/security-center-sql-database/alert.png
[8]: ./media/security-center-sql-database/sql-injection.png
