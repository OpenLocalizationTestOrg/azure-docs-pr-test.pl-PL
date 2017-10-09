---
title: "aaaAzure przewodnik rozwiązywania problemów z Centrum zabezpieczeń | Dokumentacja firmy Microsoft"
description: "Ten dokument ułatwia tootroubleshoot problemów w Centrum zabezpieczeń Azure."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 44462de6-2cc5-4672-b1d3-dbb4749a28cd
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: yurid
ms.openlocfilehash: 78b3c49eb66fe3a4f80efbba3a47a87b039c07ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-troubleshooting-guide"></a>Przewodnik rozwiązywania problemów z usługą Azure Security Center
Ten przewodnik jest dla specjalistów technologii informatycznych (IT), analityków zabezpieczeń informacji i administratorów chmury, których organizacje korzystają z Centrum zabezpieczeń Azure i wymagają problemy związane z Centrum zabezpieczeń tootroubleshoot.

>[!NOTE] 
>Począwszy od początku czerwca 2017, Centrum zabezpieczeń używa programu Microsoft Monitoring Agent hello toocollect i magazynu danych. Zobacz [migracji Platform Centrum zabezpieczeń Azure](security-center-platform-migration.md) toolearn więcej. Witaj informacje w tym artykule reprezentuje funkcji Centrum zabezpieczeń po toohello przejścia programu Microsoft Monitoring Agent.
>

## <a name="troubleshooting-guide"></a>Przewodnik rozwiązywania problemów
W tym przewodniku wyjaśniono, jak problemy związane z Centrum zabezpieczeń tootroubleshoot. Większość hello rozwiązywania problemów w Centrum zabezpieczeń ma miejsce, sprawdzając hello [dziennik inspekcji](https://azure.microsoft.com/updates/audit-logs-in-azure-preview-portal/) rekordy hello składników nie powiodło się. Za pomocą dzienników inspekcji można określić:

* Operacje, które zostały wykonane
* Kto zainicjował operację hello
* wystąpienia hello operacji
* Stan Hello hello operacji
* Hello wartości innych właściwości, które mogą ułatwić badania hello operacji

Dziennik inspekcji Hello zawiera wszystkich operacji zapisu (PUT, POST, DELETE) na zasoby, ale nie ma operacji odczytu (GET).

## <a name="microsoft-monitoring-agent"></a>Microsoft Monitoring Agent
Centrum zabezpieczeń używa hello Microsoft Monitoring Agent — to hello używać tego samego agenta hello Operations Management Suite i usługi analizy dzienników — toocollect zabezpieczeń danych z maszyn wirtualnych platformy Azure. Po włączeniu funkcji zbierania danych i agenta hello jest poprawnie zainstalowany na maszynie docelowej hello, hello procesem opisanym niżej musi należeć do wykonania:

* HealthService.exe

Po otwarciu konsoli zarządzania usługami hello (services.msc), pojawi się także uruchomiona usługa Microsoft Monitoring Agent hello w sposób przedstawiony poniżej:

![Usługi](./media/security-center-troubleshooting-guide/security-center-troubleshooting-guide-fig5.png)

Otwórz toosee wersji agenta hello masz, **Menedżera zadań**, w hello **procesów** kartę zlokalizować hello **usługę Microsoft Monitoring Agent**, kliknij prawym przyciskiem myszy na nim i Kliknij przycisk **właściwości**. W hello **szczegóły** karcie, sprawdź wersję pliku hello, jak pokazano poniżej:

![Plik](./media/security-center-troubleshooting-guide/security-center-troubleshooting-guide-fig6.png)
   

## <a name="microsoft-monitoring-agent-installation-scenarios"></a>Scenariusze instalacji programu Microsoft Monitoring Agent
Istnieją dwa scenariusze instalacji, które można wygenerować różne wyniki, instalując hello Microsoft Monitoring Agent na tym komputerze. Witaj obsługiwane scenariusze są następujące:

* **Agent zainstalowany automatycznie przez Centrum zabezpieczeń**: w tym scenariuszu będą mogli tooview hello alertów w lokalizacjach, Centrum zabezpieczeń i wyszukiwania dziennika. Zostanie wyświetlony adres e-mail toohello powiadomienia e-mail, który zostało skonfigurowane w zasadach zabezpieczeń hello hello subskrypcji hello zasób należy do.
.
* **Agent zainstalowany ręcznie na maszynie Wirtualnej znajduje się na platformie Azure**: w tym scenariuszu, jeśli używasz agentów pobrany i zainstalowany ręcznie przed tooFebruary 2017, będzie możliwe tooview hello alerty w portalu Centrum zabezpieczeń hello tylko wtedy, gdy odfiltrować hello obszar roboczy hello subskrypcji należy. W przypadku filtru na powitania subskrypcji hello zasobów, do której należy użytkownik nie będzie możliwe toosee żadnych alertów. Zostanie wyświetlony adres e-mail toohello powiadomienia e-mail, które zostały skonfigurowane w zasadach zabezpieczeń powitania dla obszaru roboczego hello subskrypcji hello należy do.

>[!NOTE]
> zachowanie hello tooavoid wyjaśniono w hello drugie, upewnij się, że możesz pobrać najnowszą wersję agenta hello hello.
> 

## <a name="troubleshooting-monitoring-agent-network-requirements"></a>Rozwiązywanie problemów z wymaganiami dotyczącymi sieci agenta monitorowania
Aby zarejestrować tooand tooconnect agentów z Centrum zabezpieczeń muszą mieć dostęp do zasobów toonetwork, w tym adresy URL domeny i numery portów hello.

- W przypadku serwerów proxy należy tooensure, który hello serwera proxy odpowiednie, zasoby są konfigurowane w ustawieniach agenta. Przeczytaj ten artykuł, aby uzyskać więcej informacji na [jak toochange hello ustawienia serwera proxy](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-windows-agents#configure-proxy-settings).
- Dla zapory, które ograniczają toohello dostęp do Internetu należy tooconfigure Twojego tooOMS dostępu toopermit zapory. W ustawieniach agenta nie jest wymagana żadna akcja.

Witaj w poniższej tabeli przedstawiono zasoby wymagane do komunikacji.

| Zasób agenta | Porty | Obejście inspekcji HTTPS |
|---|---|---|
| *.ods.opinsights.azure.com | 443 | Tak |
| *.oms.opinsights.azure.com | 443 | Tak |
| *.blob.core.windows.net | 443 | Tak |
| *.azure-automation.net | 443 | Tak |

Jeśli wystąpią problemy dotyczące dołączania z agentem hello, upewnij się, że artykuł hello tooread [jak problemy przechodzenia do usługi Operations Management Suite tootroubleshoot](https://support.microsoft.com/en-us/help/3126513/how-to-troubleshoot-operations-management-suite-onboarding-issues).


## <a name="troubleshooting-endpoint-protection-not-working-properly"></a>Rozwiązywanie problemów z niedziałającą prawidłowo ochroną punktów końcowych

agent gościa Hello jest proces nadrzędny hello wszystkich hello [Microsoft Antimalware](../security/azure-security-antimalware.md) jest rozszerzeniem. Proces agenta gościa hello zakończy się niepowodzeniem, hello Microsoft Antimalware uruchamianego jako proces podrzędny hello agenta gościa może również zakończyć się niepowodzeniem.  W scenariuszach, takich jak, która jest zalecanym tooverify hello następujące opcje:

- Jeśli docelowy hello maszyny Wirtualnej jest obraz niestandardowy i Twórca hello hello maszyny Wirtualnej nie jest zainstalowany agent gościa.
- Jeśli maszyny Wirtualnej systemu Linux, a następnie zainstalowanie wersji systemu Windows hello hello ochrony przed złośliwym kodem rozszerzenia na maszynie Wirtualnej systemu Linux maszyny Wirtualnej systemu Windows hello docelowego zakończy się niepowodzeniem. agent gościa Linux Hello ma szczególne wymagania w zakresie wersji systemu operacyjnego i wymagane pakiety, i jeśli te wymagania nie zostaną spełnione hello agenta maszyny Wirtualnej nie będzie działać albo. 
- Jeśli hello maszyna wirtualna została utworzona z starszą wersję agenta gościa. Jeśli tak jest, należy pamiętać, że niektóre starego agentów może nie automatycznej aktualizacji samego toohello nowszej wersji i może to spowodować toothis problem. Zawsze używaj hello najnowszą wersję agenta gościa, w przypadku tworzenia własnych obrazów.
- Niektóre oprogramowanie firm administracji mogą wyłączyć agenta gościa hello, lub zablokować lokalizacje plików toocertain dostępu. Jeśli masz innych producentów zainstalowane na maszynie Wirtualnej, upewnij się, że hello agent znajduje się na liście wykluczeń hello.
- Niektórych ustawień zapory lub grupy zabezpieczeń sieci (NSG) może zablokować tooand ruchu sieciowego z agenta gościa.
- Niektóre listy kontroli dostępu (ACL) mogą uniemożliwiać dostęp do dysku.
- Brak miejsca na dysku, można zablokować hello agenta gościa z działa prawidłowo. 

Przez hello domyślny interfejs użytkownika ochrony przed złośliwym oprogramowaniem firmy Microsoft jest wyłączona, przeczytaj [włączenie Microsoft chroniące przed złośliwym kodem na interfejs użytkownika usługi Azure Resource Manager maszyn wirtualnych po wdrożeniu](https://blogs.msdn.microsoft.com/azuresecurity/2016/03/09/enabling-microsoft-antimalware-user-interface-post-deployment/) Aby uzyskać więcej informacji na temat tooenable go, jeśli potrzebujesz.

## <a name="troubleshooting-problems-loading-hello-dashboard"></a>Rozwiązywanie problemów podczas ładowania hello pulpitu nawigacyjnego

Jeśli wystąpią problemy podczas ładowania hello pulpit nawigacyjny Centrum zabezpieczeń, upewnij się, ten użytkownik hello, który rejestruje Centrum tooSecurity hello subskrypcji (tj. hello pierwszy użytkownik jedną, który otworzył Centrum zabezpieczeń z subskrypcją hello) i hello użytkownik, który chcesz tooturn na zbieranie danych powinien być *właściciela* lub *współautora* na powitania subskrypcji. Od tej chwili na również użytkownikom *czytnika* na powitania subskrypcji można zobaczyć hello pulpitu nawigacyjnego alerty/zalecenie/zasad /.

## <a name="contacting-microsoft-support"></a>Kontaktowanie się z pomocą techniczną firmy Microsoft
Niektóre problemy mogą zostać zidentyfikowane przy użyciu wskazówki hello w tym artykule, innych użytkowników można również znaleźć udokumentowany na powitania Centrum zabezpieczeń publicznego [Forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureSecurityCenter). Jeśli jednak potrzebna jest dalsza pomoc w rozwiązywaniu problemów, możesz otworzyć nowe żądanie obsługi, używając witryny **Azure Portal** w sposób pokazany poniżej: 

![Pomoc techniczna firmy Microsoft](./media/security-center-troubleshooting-guide/security-center-troubleshooting-guide-fig2.png)


## <a name="see-also"></a>Zobacz też
W tym dokumencie możesz przedstawiono sposób tooconfigure zasad zabezpieczeń w Centrum zabezpieczeń Azure. toolearn więcej informacji na temat Centrum zabezpieczeń Azure, zobacz następujące hello:

* [Przewodnik planowania Centrum zabezpieczeń Azure i obsługi](security-center-planning-and-operations-guide.md) — Dowiedz się jak tooplan i zrozumieć zagadnienia dotyczące projektowania hello tooadopt Centrum zabezpieczeń Azure.
* [Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md) — Dowiedz się, jak toomonitor hello kondycji zasobów platformy Azure
* [Zarządzanie i odpowiada toosecurity alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md) — Dowiedz się jak alerty toosecurity toomanage i odpowiedź
* [Monitorowanie rozwiązań partnerskich w Centrum zabezpieczeń Azure](security-center-partner-solutions.md) — Dowiedz się, jak toomonitor hello stanu kondycji rozwiązań partnerskich.
* [Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi hello Znajdź
* [Blog Azure Security](http://blogs.msdn.com/b/azuresecurity/) — wpisy na blogu dotyczące zabezpieczeń i zgodności platformy Azure

