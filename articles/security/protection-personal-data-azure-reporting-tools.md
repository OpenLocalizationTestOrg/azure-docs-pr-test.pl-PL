---
title: "aaaDocument ochrony danych osobowych z platformy Azure, narzędzia do raportowania | Dokumentacja firmy Microsoft"
description: "jak toouse Azure raportowania usług i technologii toohelp chronić prywatność danych osobowych."
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.openlocfilehash: 3230d26ed308a8a0e72421c001793be06334a7c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="document-protection-of-personal-data-with-azure-reporting-tools"></a>Ochrona danych osobowych dokumentu przy użyciu narzędzi do raportowania platformy Azure

W tym artykule będzie omawiać jak toouse Azure raportowania usług i technologii toohelp chronić prywatność danych osobowych.

## <a name="scenario"></a>Scenariusz

Firma rejs dużych, siedzibą w Stanach Zjednoczonych hello, rozwija trasy toooffer jego operacji w Śródziemnego hello, Adriatyku i Bałtyckiego mórz, jak również hello brytyjskich. toohelp tych działań uzyskała mniejszych rejs wiersze na podstawie we Włoszech Niemczech, Dania i hello Zjednoczone Królestwo

Witaj w firmie Microsoft Azure do przetwarzania i przechowywania danych firmowych. Dotyczy to również dane osobowe, takich jak nazwy, adresy, numery telefonów i informacje o karcie kredytowej z jej klientów globalnych. Zawiera także tradycyjnych informacje kadr, takie jak adresy, numery telefonów, numery identyfikacyjne podatku i medyczne informacje dotyczące pracowników firmy we wszystkich lokalizacjach. wiersz rejs Hello zachowuje również dużej bazy danych elementów członkowskich programu osób trzecich i lojalność zawierający dane osobowe tootrack relacje z bieżących i starszych klientów.

Pracownikom firmy dostępu hello sieci z biurach zdalnych i agentów podróży hello firmy znajdujących się wokół Witaj świecie mają dostęp do zasobów firmowych toosome.

## <a name="problem-statement"></a>Opis problemu

Witaj firmy muszą chronić prywatność hello pracowników i klientów danych osobowych za pośrednictwem strategii zabezpieczeń wielowarstwowy, która używa zarządzania platformy Azure i zabezpieczeń funkcji tooimpose ścisłą kontrolę dostępu tooand przetwarzania danych osobowych, a musi być toodemonstrate możliwe jego ochronnych środków toointernal i Audytorzy usług zewnętrznych.

## <a name="company-goal"></a>Celem firmy

W ramach jego strategii zabezpieczeń obrony zabezpieczeń jest tootrack celem firmy dostępu tooand przetwarzania danych osobowych i upewnij się, że dokumentacji odpowiedniej ochrony danych osobowych w miejscu i działa.

## <a name="solutions"></a>Rozwiązania

Microsoft Azure umożliwia kompleksowe monitorowanie, rejestrowanie i toohelp narzędzi diagnostycznych monitorowanie i rejestrowanie działań i zdarzenia związane z dostęp i przetwarzania danych osobowych, geograficzne przepływu danych, a dane toopersonal dostępu innych firm. Ponieważ bezpieczeństwo danych osobowych w chmurze hello jest udostępniony odpowiedzialność, firma Microsoft udostępnia również klientom:

- Szczegółowe informacje o jego własnej przetwarzania danych klientów

- Środki bezpieczeństwa, zarządzane przez firmę Microsoft

- Jak i gdzie wysyłania danych klientów

- Szczegółowe informacje o procesie przeglądami ochrony prywatności firmy Microsoft

### <a name="azure-active-directory"></a>Usługa Azure Active Directory

[Usługa Azure Active Directory](https://azure.microsoft.com/services/active-directory/) jest oparta na chmurze, wielodostępne katalogami i tożsamościami zarządzania usługi Microsoft. Witaj logowania usługi i funkcje raportowania inspekcji dostarczają szczegółowe logowania i aplikacji użycie działania informacji toohelp monitorować i upewnij się, dane osobowe toocustomers właściwy dostęp i pracowników.

Istnieją dwa typy raportów działania:

- Witaj [inspekcji dzienników raporty aktywności](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs) zapewniają szczegółowe rekord zadania działania systemu

- Witaj [dziennika raport aktywności logowania](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins) dowiesz się, kto wykonał każde działanie wymienione w raporcie inspekcji hello

Korzystanie ze hello dwa można śledzić historię hello każdego zadania wykonywane i kto wykonał każdego. Obu typów raportów można dostosowywać i mogą być filtrowane.

#### <a name="how-do-i-access-hello-audit-and-security-logs"></a>Jak dostęp hello inspekcji i zabezpieczeń dzienniki?

Witaj dzienniki inspekcji i zabezpieczeń można uzyskać dostęp z portalu usługi Active Directory hello trzy różne sposoby: poprzez hello **działania** sekcji (wybierz opcję **dzienniki inspekcji** lub **logowania**), lub z **użytkowników i grup** lub **aplikacje dla przedsiębiorstw** w obszarze **Zarządzaj** w usłudze Active Directory. Raporty można także uzyskać dostęp za pośrednictwem usługi Azure Active Directory hello raportowania interfejsu API. 

1. Hello portalu Azure, wybierz **usługi Azure Active Directory.**

2. W hello **działania** zaznacz **dzienniki inspekcji.**

    ![](media/protection-personal-data-azure-reporting-tools/image001.png)

3. Dostosowywanie hello widoku listy, klikając **kolumn** hello w pasku narzędzi.

4.  Wybierz element toosee widoku listy hello wszystkich dostępnych informacji o nim.

    ![](media/protection-personal-data-azure-reporting-tools/image003.png)

Raportowanie na platformie Azure Active Directory obejmuje również dwa typy raportów zabezpieczeń **użytkownicy oflagowani ryzyka** i **ryzykowne logowania**, który ułatwia monitorowanie potencjalnych zagrożeń w środowisku platformy Azure.

Aby uzyskać więcej informacji na temat hello Usługa raportowania patrz [raportowania usługi Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal)

Odwiedź stronę [raporty działania usługi Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal#activity-reports) Aby uzyskać więcej szczegółowych informacji o raportach hello dostępne w usłudze Azure Active Directory. Ta witryna zawiera więcej informacji o tym, jak tooaccess i użyj [dzienniki inspekcji, raporty aktywności](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs) i [raporty aktywności logowania](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins) w portalu hello. Zawiera także informacje o [użytkownicy oflagowani ryzyka](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-security-user-at-risk) i [ryzykowne logowania](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-security-risky-sign-ins) raporty dotyczące zabezpieczeń.

Odwiedź hello [inspekcji usługi Azure Active Directory dokumentacja interfejsu API](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-audit-reference) witryny, aby uzyskać więcej informacji na temat tooAzure tooconnect katalogu raportowania programowo.

### <a name="log-analytics"></a>Log Analytics

[Dziennika analizy](https://azure.microsoft.com/services/log-analytics/) można [zbierania danych z monitora Azure](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-storage) toocorrelate go z innymi danymi i udostępnia dodatkowe analizy. Azure Monitor zbiera i analizuje dane monitorowania środowiska platformy Azure. 

Narzędzia analizy w analizy dzienników takie jak dziennik wyszukiwania, widoków i rozwiązań działać względem wszystkich zebranych danych, zapewniając scentralizowane analizy całego środowiska. Analiza dzienników można agregować i analizować dzienniki zdarzeń systemu Windows, dzienniki programu IIS i audyt dzienników systemowych, co pomaga wykrywać potencjalnych naruszeń dane osobowe, które można ujawniać dane osobowe toounauthorized użytkowników.

#### <a name="how-do-i-use-log-analytics"></a>Jak używać Log Analytics?

Analiza dzienników dostępne za pośrednictwem portalu OMS hello lub hello portalu Azure, z dowolnej przeglądarki sieci web. Analiza dzienników zawiera pobrać tooquickly języka zapytań i Konsolidowanie danych w repozytorium hello. Można utworzyć i zapisać dziennik wyszukiwania toodirectly analizowanie danych w portalu hello.

toocreate obszaru roboczego analizy dzienników w hello portalu Azure, hello następujące:

1. Wybierz **analizy dzienników** z listy hello usług w hello Marketplace.

2. Wybierz **tworzenia,** należy określić nazwę hello obszar roboczy OMS, wybierz Twojej subskrypcji, grupy zasobów, lokalizacji i warstwę cenową.

3. Kliknij przycisk **OK** toodisplay listę obszarów roboczych.

4. Wybierz toosee obszaru roboczego jego szczegóły.

    ![](media/protection-personal-data-azure-reporting-tools/image004.png)

Odwiedź hello [dokumentacji analityka dziennika](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview) toolearn więcej o usłudze hello.

Odwiedź hello [Rozpoczynanie pracy z obszaru roboczego analizy dzienników](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started) samouczka toocreate obszarem roboczym oceny i Dowiedz się, jak toouse hello usługi podstawy hello.

Odwiedź powitania po sposobu logowania tooconnect toouse analizy dzienników z hello stron sieci web, aby uzyskać dokładniejsze informacje opisane powyżej:

[Źródła danych dzienników zdarzeń systemu Windows w analizy dzienników](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-windows-events)

[Rejestrowania przez usługi IIS w analizy dzienników](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-iis-logs)

[SYSLOG źródeł danych w analizy dzienników](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-syslog)

### <a name="azure-monitorazure-activity-log"></a>Dziennik aktywności platformy Azure Monitor/Azure 

[Azure Monitor](https://azure.microsoft.com/services/monitor/) zapewnia na podstawowym poziomie infrastruktury metryki i dzienniki większość usług w systemie Microsoft Azure.
Monitorowanie ułatwia toogain szczegółowych informacji o aplikacji Azure. Azure Monitor zależy od hello rozszerzenia diagnostyki Azure (Windows lub Linux) do zbierania większości dzienniki i metryki na poziomie aplikacji. [Witaj dziennika aktywności platformy Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) jest jeden z zasobów hello można wyświetlić z monitorem Azure. Śledzi każdego wywołania interfejsu API i zapewnia szereg informacji na temat działań, które występują w [usługi Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).
Możesz wyszukać hello dziennik aktywności (wcześniej nazywane Operational lub dzienniki inspekcji) informacji o zasobie widziany przez hello infrastruktury platformy Azure. 

Mimo że większość informacji hello rejestrowane w hello działania dziennika dotyczy tooperformance i usługi kondycji, jest również informacje, które są powiązane tooprotection danych. Przy użyciu hello dziennik aktywności, można określić hello ", co, kto i kiedy" dla żadnego zapisu (PUT, POST, DELETE) wykonywanych na powitania zasobów w Twojej subskrypcji platformy Azure.

Na przykład zapewnia rekordu, gdy administrator usuwa sieciową grupę zabezpieczeń, który może mieć wpływ na powitania ochrony danych osobowych. Wpisy dziennika aktywności są przechowywane w monitorze Azure przez 90 dni.

#### <a name="how-do-i-use-hello-data-collected-by-azure-monitor"></a>Jak używać hello dane zebrane przez Azure Monitor?

Istnieje wiele sposobów toouse hello danych w dzienniku aktywności hello i innych zasobów Azure monitora.

- Można przesłać strumieniowo hello lokalizacje tooother danych w wierszu prawdziwe.

- Dane można przechowywać na powitania przez czas dłuższy niż domyślne hello, za pomocą [konto magazynu Azure](https://docs.microsoft.com/azure/storage/common/storage-introduction) i ustawiania zasad przechowywania.

- Można danych visual hello w grafiki i wykresy, za pomocą hello [portalu Azure](https://azure.microsoft.com/features/azure-portal/), [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), [Microsoft PowerBI](https://powerbi.microsoft.com/), lub narzędzi innych firm wizualizacji.

- Hello danych przy użyciu hello Azure Monitor REST API, polecenia interfejsu wiersza polecenia, można zbadać [PowerShell](https://docs.microsoft.com/powershell/) poleceń cmdlet lub hello zestawu .NET SDK.

Wybierz tooget rozpoczęcia pracy z monitorem Azure **więcej usług** w hello portalu Azure.

1. Przewiń w dół za**Monitor** w hello **monitorowanie i zarządzanie** sekcji.

    ![](media/protection-personal-data-azure-reporting-tools/image005.png)

2.  Monitor zostanie otwarty w hello **dziennik aktywności** widoku.

    ![](media/protection-personal-data-azure-reporting-tools/image007.png)

Możesz utworzyć i zapisać zapytania dotyczące typowych filtrów, a następnie numeru pin hello najważniejszych zapytań tooa pulpitu nawigacyjnego portalu, aby zawsze będzie wiadomo, czy wystąpiły zdarzenia, które spełniają kryteria.

1. Można filtrować widok hello grupy zasobów, timespan i Kategoria zdarzenia.

    ![](media/protection-personal-data-azure-reporting-tools/image008.png)

2. Następnie możesz przypinać zapytania pulpitu nawigacyjnego portalu tooa klikając hello **numeru Pin** przycisku. Dzięki temu można utworzyć pojedyncze źródło informacji dla danych operacyjnych na usługi. Nazwa zapytania Hello i liczbę wyników będzie wyświetlana na powitania pulpitu nawigacyjnego.

Można również metryki hello Monitor tooview dla wszystkich zasobów platformy Azure, skonfigurować ustawienia diagnostyki i alerty i wyszukaj hello dziennika. Aby uzyskać więcej informacji na temat sposobu toouse hello Azure monitora i dziennik aktywności, zobacz [Rozpoczynanie pracy z monitorem Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-get-started).

### <a name="azure-diagnostics"></a>Diagnostyka Azure 

funkcja diagnostyki Hello na platformie Azure umożliwia zbieranie danych z wielu źródeł. dzienniki zdarzeń systemu Windows Hello, między innymi hello dziennika zabezpieczeń, może być szczególnie przydatne w śledzenia i dokumentowanie ochrony danych osobowych. Dziennik zabezpieczeń Hello śledzi zdarzenia sukcesów i niepowodzeń logowania, a także zmiany uprawnień, wykrywania wzorce wskazujące niektóre rodzaje ataków, zmiany zasad związane z zabezpieczeniami, zmian członkostwa w grupach zabezpieczeń i wiele innych.

Na przykład 4695 identyfikator zdarzenia alerty możesz toohello podjęto unprotection podlegającą inspekcji chronionych danych. Dotyczy to tylko toohello danych interfejsu API ochrony (DPAPI), co ułatwia tooprotect dane, takie jak klucze prywatne, przechowywane poświadczenia i innych informacji poufnych.

#### <a name="how-do-i-enable-hello-diagnostics-extension-for-windows-vms"></a>Jak włączyć hello diagnostyki rozszerzenia dla maszyn wirtualnych systemu Windows?

PowerShell tooenable hello diagnostyki rozszerzenie służy dla maszyny Wirtualnej systemu Windows, tak jak toocollect dane dziennika. kroki Hello w ten sposób zależeć na model wdrażania, których używasz (Resource Manager lub Classic). rozszerzenie diagnostyki hello tooenable na istniejącej maszynie Wirtualnej, który został utworzony za pośrednictwem modelu wdrażania usługi Resource Manager hello, można użyć hello [polecenia cmdlet programu PowerShell Set-AzureRMVMDiagnosticsExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension?view=azurermps-4.3.1).

   ![](media/protection-personal-data-azure-reporting-tools/image009.png)

*\$diagnosticsconfig_path* hello ścieżki toohello plik, który zawiera hello diagnostyki konfiguracji w formacie XML. Aby uzyskać szczegółowe instrukcje dotyczące włączania diagnostyki Azure na maszynie Wirtualnej, zobacz [tooenable Użyj programu PowerShell diagnostyki Azure na maszynie wirtualnej z systemem Windows.](https://docs.microsoft.com/azure/virtual-machines/windows/ps-extensions-diagnostics)

Hello rozszerzenia diagnostyki Azure można transferu hello zbieranych danych tooan konta magazynu Azure lub wysyłać je tooservices, takich jak usługi Application Insights. Następnie można hello danych inspekcji.

#### <a name="how-do-i-store-and-view-diagnostic-data"></a>Sposób przechowywania i wyświetlać dane diagnostyczne?

Jest ważne tooremember że danych diagnostycznych nie jest trwale przechowywane, chyba że transfer toohello Microsoft Azure magazynu emulatora lub tooAzure magazynu. toostore i widok danych diagnostycznych w usłudze Azure Storage, wykonaj następujące kroki:

1. Określ konto magazynu w pliku pliku ServiceConfiguration.cscfg hello. Diagnostyka Azure może używać usługi Blob hello lub hello usługi tabel, w zależności od typu hello danych. Dzienniki zdarzeń systemu Windows są przechowywane w formacie tabeli.

2. Transfer danych hello. Można zażądać danych diagnostycznych hello tootransfer za pośrednictwem hello pliku konfiguracji. 2.4 zestawu SDK oraz poprzedniej można również ustawić żądania hello programowo.

3. Wyświetlanie danych hello, przy użyciu [Eksploratora usługi Storage Azure](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer), [Eksploratora serwera](https://docs.microsoft.com/azure/vs-azure-tools-storage-resources-server-explorer-browse-manage) w programie Visual Studio lub [Menedżera diagnostyki Azure](https://www.cerebrata.com/products/azure-diagnostics-manager) w usłudze Azure Management Studio.

Aby uzyskać więcej informacji na temat tooperform tych kroków, zobacz [magazynu i widok danych diagnostycznych w usłudze Azure Storage.](https://docs.microsoft.com/azure/cloud-services/cloud-services-dotnet-diagnostics-storage)

### <a name="azure-storage-analytics"></a>Analityka usługi Azure Storage 

Analityka magazynu rejestruje szczegółowe informacje na temat usługi Magazyn tooa udane i nieudane żądania. Te informacje mogą być używane toomonitor poszczególnych żądań, które mogą pomóc w dokumentowanie dane toopersonal dostępu przechowywany w usłudze hello. Jednak rejestrowanie analityka magazynu nie jest włączone domyślnie dla konta magazynu. Możesz je włączyć w hello portalu Azure.

#### <a name="how-do-i-configure-monitoring-for-a-storage-account"></a>Jak skonfigurować monitorowanie dla konta magazynu

tooconfigure monitorowania dla konta magazynu, hello następujące:

1. Wybierz **kont magazynu** w hello portalu Azure, a następnie wybierz nazwę hello hello konta toomonitor.

    ![](media/protection-personal-data-azure-reporting-tools/image011.png)

2. W hello **monitorowanie** zaznacz **diagnostyki.**

3.  Wybierz hello **typu** danych metryki ma toomonitor dla każdej usługi (pliku Blob, tabeli,). dzienników Diagnostyka toosave tooinstruct magazynu Azure do odczytu, zapisu i usuwania żądań dla hello obiektów blob, tabel i kolejki usług, wybierz **dzienniki obiektu Blob, tabela dzienniki** i **dzienniki w kolejce.**

    ![](media/protection-personal-data-azure-reporting-tools/image013.png)

4. Za pomocą suwaka hello u dołu hello, ustaw hello **przechowywania** zasad w dniach (wartość 1 – 365). Siedem dni jest domyślnym hello.

5. Wybierz **zapisać** tooapply hello konfiguracji ustawień.

Wpisy dziennika rejestrowania magazynu zawiera następujące informacje dotyczące poszczególnych żądań hello:

- Czas informacje takie jak czas rozpoczęcia, czas oczekiwania na trasie i opóźnienie serwera.

- Szczegóły operacji magazynu hello, takie jak typ operacji hello, klucz hello hello magazynu obiektu powitania klienta jest dostęp do, Powodzenie lub błąd i zwrócony klienta toohello hello kod stanu HTTP.

- Szczegóły uwierzytelniania, takie jak typ powitania klienta hello uwierzytelniania używane.

- Współbieżność informacje takie jak hello wartość ETag i sygnatura czasowa ostatniej modyfikacji.

- rozmiary Hello hello komunikatów żądań i odpowiedzi.

Aby uzyskać szczegółowe instrukcje na temat tooenable analityka magazynu rejestrowania, zobacz [monitorować konta magazynu w hello portalu Azure.](https://docs.microsoft.com/azure/storage/common/storage-monitor-storage-account)

### <a name="azure-security-center"></a>Azure Security Center 

[Centrum zabezpieczeń Azure](https://azure.microsoft.com/services/security-center/) monitoruje stan zabezpieczeń zasobów platformy Azure w kolejności tooprevent hello wykrywać zagrożenia i podano zalecenia dotyczące odpowiada. Udostępnia kilka sposobów toohelp dokumentu z środków bezpieczeństwa, które chronić prywatność hello danych osobowych.

Monitorowanie kondycji zabezpieczeń pomaga zapewnić zgodność z zasadami zabezpieczeń. Monitorowanie zabezpieczeń jest aktywnej strategii przeprowadzania inspekcji używanych systemach tooidentify zasoby, które nie spełniają standardów organizacji lub najlepszych rozwiązań. Możesz monitorować stan zabezpieczeń hello hello następujące zasoby:

- Obliczeń (maszyny wirtualne i usługi w chmurze)

- Sieci (sieci wirtualne)

- Magazyn i dane (serwera i bazy danych inspekcji i wykrywania zagrożeń, funkcji TDE, szyfrowanie magazynu)

- Aplikacje (potencjalnych problemów z zabezpieczeniami)

Problemy z zabezpieczeniami w dowolnej z tych kategorii może stanowić zagrożenie toohello zasad ochrony prywatności danych osobowych.

#### <a name="how-do-i-view-hello-security-state-of-my-azure-resources"></a>Jak wyświetlić stan zabezpieczeń hello zasoby platformy Azure?

Centrum zabezpieczeń okresowo analizuje stan zabezpieczeń hello zasobów platformy Azure. Można wyświetlić wszystkie potencjalnych luk w zabezpieczeniach identyfikuje w hello **zapobiegania** sekcji hello pulpitu nawigacyjnego.

   ![](media/protection-personal-data-azure-reporting-tools/image014.png)

1. W hello **zapobiegania** sekcji, wybierz hello **obliczeniowe** kafelka. W tym miejscu zobaczysz **Przegląd,** wraz z hello **maszyn wirtualnych** lista wszystkich maszyn wirtualnych i ich stanów zabezpieczeń i hello **usługi w chmurze** lista ról sieci web i proces roboczy monitorowane przez Centrum zabezpieczeń.

2. Na powitania **omówienie** karcie, drugie tooview zalecenie więcej informacji.

3. Na powitania **maszyn wirtualnych** , a następnie wybierz dodatkowe szczegóły tooview maszyny Wirtualnej.

Po włączeniu funkcji zbierania danych w Centrum zabezpieczeń Azure hello Microsoft Monitoring Agent jest udostępniany automatycznie na wszystkich istniejących i nowych obsługiwanych maszyn wirtualnych, które są wdrożone. Dane zbierane z tego agenta są przechowywane w każdej istniejącej [analizy dzienników](https://azure.microsoft.com/services/log-analytics/) obszaru roboczego skojarzonego z subskrypcją lub nowego obszaru roboczego.

[Raporty analizy zagrożeń](https://docs.microsoft.com/azure/security-center/security-center-threat-report) są dostarczane przez Centrum zabezpieczeń. Ta funkcja pozwala przydatnych informacji na temat toohelp wykrycia osoby atakującej hello tożsamości, cele, bieżących i historycznych ataku kampanii i taktyk, narzędzia i procedur. Środki zaradcze i korygowania informacji jest również uwzględniony.

głównym celem tych raportów zagrożeń Hello jest toohelp toorespond można skutecznie toohello natychmiastowego zagrożeń i pomoc, środki później toomitigate hello problem. informacje Hello w raportach hello również mogą być przydatne, gdy dokument Twojej odpowiedzi na zdarzenia do raportowania i inspekcji.

Raporty analizy zagrożeń Hello są prezentowane w. Format PDF, dostępne za pośrednictwem łącza w hello **raporty** pole hello **podejrzane proces wykonywany** bloku dla każdego alertu zabezpieczeń w Centrum zabezpieczeń Azure.

Aby uzyskać więcej informacji dotyczących sposobu tooview i użyj hello raportu analizy zagrożeń, zobacz [raport analizy zagrożeń z Centrum zabezpieczeń Azure.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)

## <a name="next-steps"></a>Następne kroki:

[Wprowadzenie do korzystania z hello interfejsem API raportowania usługi Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-getting-started-azure-portal)

[Co to jest usługa Log Analytics?](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview)

[Omówienie monitorowania na platformie Microsoft Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview)

[Wprowadzenie toohello dziennika aktywności platformy Azure (klip wideo)](https://azure.microsoft.com/resources/videos/intro-activity-log/)
