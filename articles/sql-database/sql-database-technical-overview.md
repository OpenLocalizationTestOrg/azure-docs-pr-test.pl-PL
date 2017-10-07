---
title: "aaaWhat to jest usługa Azure SQL Database hello? | Microsoft Docs"
description: "Pobierz wprowadzenie tooSQL bazy danych: szczegóły techniczne i możliwości firmy Microsoft relacyjnej bazy danych system zarządzania (RDBMS) w chmurze hello."
keywords: wprowadzenie toosql, toosql wprowadzenie, co to jest baza danych sql
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: cgronlun
ms.assetid: c561f600-a292-4e3b-b1d4-8ab89b81db48
ms.service: sql-database
ms.custom: overview
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 06/30/2017
ms.author: carlrab
ms.openlocfilehash: 24ca383ad7e140133d19debc8899f172ee4aa424
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-azure-sql-database-service"></a>Co to jest usługa Azure SQL Database hello? 

Usługa SQL Database jest usługą relacyjnej bazy danych ogólnego przeznaczenia w systemie Microsoft Azure, obsługującą struktury takie, jak dane relacyjne, JSON, dane przestrzenne i XML. Zapewnia [dynamicznie skalowalną wydajność](sql-database-service-tiers.md) i udostępnia opcje, takie jak [indeksy magazynu kolumn](https://docs.microsoft.com/sql/relational-databases/indexes/columnstore-indexes-overview), używane w skomplikowanych analizach i raportowaniu, oraz [przetwarzanie OLTP danych w pamięci](sql-database-in-memory.md) na potrzeby ekstremalnego przetwarzania transakcyjnego. Firma Microsoft obsługuje wszystkie poprawki i uaktualniania kodu SQL hello bezproblemowo i optymalizacji abstracts całe Zarządzanie hello podstawowej infrastruktury. 

Baza danych SQL udostępnia bazy kodu hello [aparatu bazy danych programu Microsoft SQL Server](https://docs.microsoft.com/sql/sql-server/sql-server-technical-documentation). Ze strategią pierwszy chmury firmy Microsoft hello najnowsze możliwości programu SQL Server są wydanych tooSQL pierwszej bazy danych, a następnie tooSQL sam serwer. Takie podejście umożliwia hello najnowsze możliwości programu SQL Server z nie obciążenie poprawki lub uaktualnianie - i z tych nowych funkcji przetestowane przez miliony baz danych. Aby uzyskać informacje dotyczące nowych możliwości w miarę ich publikowania, zobacz:

- **[Przewodnik po bazy danych SQL Azure](https://azure.microsoft.com/roadmap/?category=databases)**: toofind miejsce nowości i wkrótce dalej. 
- **[Blog usługi Azure SQL Database](https://azure.microsoft.com/blog/topics/database)**: miejsce, w którym członkowie zespołu produktowego programu SQL Server zamieszczają informacje o nowościach i funkcjach usługi SQL Database. 

Usługa SQL Database oferuje przewidywalną wydajność na różnych poziomach usługi, która zapewnia dynamiczną skalowalność bez przestojów, wbudowany mechanizm inteligentnej optymalizacji, globalną skalowalność i dostępność oraz zaawansowane opcje zabezpieczeń — wszystko przy bliskich zeru nakładach administracyjnych. Te funkcje umożliwiają toofocus na tworzenie aplikacji szybki i przyspieszając toomarket Twojego czasu, zamiast przydzielania cenny czas i maszyn wirtualnych toomanaging zasobów i infrastruktury. Hello bazy danych SQL, usługa jest obecnie w danych 38 koncentruje się wokół Witaj świecie z więcej centrów danych regularnie, przejście w tryb online, które pozwala toorun bazy danych w centrum danych w pobliżu.

> [!NOTE]
> Aby uzyskać informacje o zabezpieczeniach platformy Azure, zobacz [Centrum zaufania Azure](https://azure.microsoft.com/support/trust-center/security/).
>

## <a name="scalable-performance-and-pools"></a>Skalowalna wydajność i pule

W usłudze SQL Database każda baza danych jest odizolowana od innych i przenośna, z własną [warstwą usług](sql-database-service-tiers.md) i z gwarantowanym poziomem wydajności. Baza danych SQL zawiera różne poziomy wydajności dla różnych potrzeb i umożliwia baz danych hello puli toomaximize toobe wykorzystania zasobów i oszczędności.

### <a name="adjust-performance-and-scale-without-downtime"></a>Dostosowanie wydajności i skalowanie bez przestojów

Baza danych SQL oferuje cztery warstwy usług obciążeń bazy danych lekkie tooheavyweight toosupport: Basic, Standard, Premium i Premium RS. Można utworzyć pierwszą aplikację w bazie danych jednego, mała przy niskich kosztach miesięcznie, a następnie zmień jego warstwy usługi ręcznie lub programowo, na potrzeby hello toomeet czasu dowolnego rozwiązania. Można dostosować wydajność bez przestojów tooyour aplikacji lub tooyour klientów. Umożliwia dynamiczne skalowalność tootransparently Twojej bazy danych odpowiada toorapidly zmiany wymagań dotyczących zasobów i umożliwia tooonly można płacić za zasoby hello należy najodpowiedniejszym czasie.

   ![skalowanie](./media/sql-database-what-is-a-dtu/single_db_dtus.png)

### <a name="elastic-pools-toomaximize-resource-utilization"></a>Wykorzystanie zasobów toomaximize pul elastycznych

Dla wielu firm i aplikacji jest możliwe toocreate pojedynczych baz danych i wybieranie wydajności w górę lub w dół na żądanie jest wystarczająca, zwłaszcza jeśli wzorce użycia są względnie przewidywalne. Ale jeśli masz nieprzewidywalnych wzorców, może być twarde toomanage kosztów i modelem biznesowym. [Pule elastyczne](sql-database-elastic-pool.md) są zaprojektowane toosolve ten problem. Witaj koncepcja jest prosta. Przydziel wydajności zasobów tooa puli, a nie poszczególnych bazy danych i zwrócić hello zasobów łączną wydajność puli hello, a nie dla pojedynczej bazy danych wydajności. 

   ![pule elastyczne](./media/sql-database-what-is-a-dtu/sqldb_elastic_pools.png)

Pule elastyczne nie wymagają toofocus na wybierania wydajność bazy danych w górę i w dół, jak zmienia się zapotrzebowania na zasoby. Witaj puli baz danych korzystanie z hello wydajności zasobów puli elastycznej hello zgodnie z potrzebami. Korzystać z puli baz danych, ale nie przekraczają limitów puli hello hello, więc koszt pozostaje przewidywalny nawet w przypadku użycia poszczególnych bazy danych nie. Ponadto można [Dodawanie i usuwanie baz danych toohello puli](sql-database-elastic-pool-manage-portal.md), skalowanie aplikacji od kilku toothousands baz danych, wszystko w ramach kontrolowanego budżetu. Możesz również minimum hello kontroli i toodatabases dostępne zasoby maksymalna w hello tooensure puli bazy danych w puli hello wykorzystuje wszystkie hello puli zasobów, a w każdej puli bazy danych ma gwarantowane minimalna ilość zasobów. toolearn więcej informacji na temat wzorców projektowych dla aplikacji SaaS wykorzystujących pule elastyczne, zobacz [wzorce projektowe dla wielodostępnych aplikacji SaaS w usłudze SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md).

### <a name="blend-single-databases-with-pooled-databases"></a>Mieszaj pojedyncze bazy danych z bazami danych w puli

W obu przypadkach — pojedyncza baza danych i pule elastyczne — nie ma ograniczenia do jednego rozwiązania. Blend pojedyncze bazy danych z puli elastycznej i zmienić hello warstwy usług pojedynczych baz danych i pul elastycznych, szybko i łatwo tooadapt tooyour sytuacji. Witaj siły i zasięgu platformy Azure można mieszanego i dopasowania Azure innych usług za pomocą aplikacji unikatowy projektowania potrzeb, dysku kosztów i wydajności zasobów toomeet bazy danych SQL i odblokować nowe możliwości biznesowe.

### <a name="extensive-monitoring-and-alerting-capabilities"></a>Możliwości rozbudowanego monitorowania i zgłaszania alertów

Jednak jak porównać względną wydajność pojedynczych baz danych i pul elastycznych hello? Skąd wiadomo, powitania kliknij prawym przyciskiem myszy, aby zatrzymać podczas wybierania w górę i w dół? Użyj hello [monitorowania wydajności wbudowanych](sql-database-performance.md) i [alerty](sql-database-insights-alerts-portal.md) narzędzi, w połączeniu z hello klasyfikacje wydajności na podstawie [jednostki transakcji bazy danych (Dtu) dla pojedynczej bazy danych i elastyczne Dtu (Edtu) dla pul elastycznych](sql-database-what-is-a-dtu.md). Za pomocą tych narzędzi, można szybko ocenić wpływ hello skalowanie w górę lub w dół na bieżącym podstawie lub projektu na potrzeby w zakresie wydajności. Zobacz artykuł [Opcje i wydajność usługi SQL Database: poznaj, co jest dostępne w poszczególnych warstwach usług](sql-database-service-tiers.md), aby uzyskać szczegółowe informacje.

Ponadto usługa SQL Database może [tworzyć metryki i dzienniki diagnostyczne](sql-database-metrics-diag-logging.md), które ułatwiają monitorowanie. Można skonfigurować użycie zasobów toostore bazy danych SQL, pracowników i sesje i łączności do jednej z tych zasobów platformy Azure:

- **Usługa Azure Storage**: w celu archiwizowania ogromnych ilości danych telemetrycznych za niewielką cenę
- **Centrum zdarzeń Azure**: w celu integracji danych telemetrycznych usługi SQL Database z niestandardowym rozwiązaniem monitorowania lub potokami danych
- **Usługa Azure Log Analytics**: w celu użycia wbudowanego rozwiązania monitorowania obejmującego funkcje raportowania, zgłaszania alertów i zmniejszenia ryzyka

    ![architektura](./media/sql-database-metrics-diag-logging/architecture.png)

## <a name="availability-capabilities"></a>Możliwości dostępności

Umowa dotycząca poziomu usług [(SLA)](http://azure.microsoft.com/support/legal/sla/) o czołowej w branży dostępności 99,99% dla platformy Azure, która jest obsługiwana przez globalną sieć centrów danych zarządzanych przez firmę Microsoft, pomaga zapewnić działanie aplikacji przez 24 godziny na dobę, 7 dni w tygodniu. Ponadto usługa SQL Database oferuje wbudowane funkcje [zapewnienia ciągłości działalności biznesowej i globalnej skalowalności](sql-database-business-continuity.md), takie jak:

- **[Automatyczne kopie zapasowe](sql-database-automated-backups.md)**: usługa SQL Database automatycznie wykonuje pełne i różnicowe kopie zapasowe oraz kopie zapasowe dziennika transakcji.
- **[W momencie przywracania](sql-database-recovery-using-backups.md)**: baza danych SQL obsługuje odzyskiwania tooany punktu w czasie w okresie przechowywania kopii zapasowych automatyczne hello.
- **[Aktywna replikacja geograficzna](sql-database-geo-replication-overview.md)**: baza danych SQL umożliwia tooconfigure się toofour pomocniczej do odczytu bazy danych w każdej hello takie same lub rozproszonych globalnie centrach danych platformy Azure.  Na przykład jeśli masz aplikacji SaaS z bazą danych katalogu, który ma dużą liczbę równoczesnych transakcji tylko do odczytu, użyj aktywna replikacja geograficzna tooenable globalne odczytu skali i Usuń powodu obciążeń tooread wąskie gardła na powitania podstawowego. 
- **[Praca awaryjna grupy](sql-database-geo-replication-overview.md)**: baza danych SQL pozwala tooenable wysokiej dostępności i równoważenia w skali globalnej, tym przezroczysty replikacja geograficzna i pracy awaryjnej dużych zestawów baz danych i pul elastycznych obciążenia. Grupy pracy awaryjnej i aktywna replikacja geograficzna umożliwia utworzenie globalnie rozproszone aplikacji SaaS przy minimalnym udziale administratora narzut pozostawienie wszystkich hello złożonych monitorowania, routing i pracy awaryjnej aranżacji tooSQL bazy danych.

## <a name="built-in-intelligence"></a>Wbudowane narzędzie analizy

Z bazy danych SQL należy pobrać wbudowanych analizy, które pomaga znacznie zmniejszyć koszty hello systemem i zarządzanie bazami danych i maksymalizację wydajności i zabezpieczeń aplikacji. Obciążeniami miliony klientów nieprzerwanemu, bazy danych SQL zbiera i przetwarza duże ilości danych telemetrii, przestrzegając całkowicie ochrona prywatności klientów w tle hello. Rozmaite algorytmy stale ocenia dane telemetryczne hello tak, aby usługa hello można dowiedzieć się i dostosowania z aplikacją. Na podstawie tej analizy, usługa hello funkcjonuje z określonego obciążenia dopasowane tooyour zalecenia dotyczące poprawy wydajności. 

### <a name="automatic-performance-tuning"></a>Automatyczne dostosowywanie wydajności

Baza danych SQL oferuje szczegółowy wgląd w hello zapytań, że należy toomonitor. SQL Database uzyskuje informacje o Twoich wzorców bazy danych i umożliwia możesz tooadapt obciążenie tooyour schematu bazy danych. Usługa SQL Database udostępnia zalecenia dotyczące dostrajania wydajności za pomocą narzędzia [SQL Database Advisor](sql-database-advisor.md), pozwalającego na przeglądanie i zastosowanie działań dostrajających. Jednak nieprzerwane monitorowanie bazy danych jest trudnym i żmudnym zadaniem, szczególnie w przypadku pracy z wieloma bazami danych. Zarządzanie olbrzymią liczbę baz danych może być niemożliwe toodo wydajnie nawet w przypadku wszystkie dostępne narzędzia i raporty zawierające bazy danych SQL i portalu Azure. Zamiast monitorowania i dostrajania bazę danych ręcznie, warto rozważyć delegowanie niektóre hello monitorowania i dostrajania tooSQL działania bazy danych przy użyciu funkcji automatycznego dostrajania. Baza danych SQL stosować zalecenia, testy i automatycznie sprawdza, czy każdego z jego dostrajania wydajności hello akcje tooensure przechowuje poprawy. Dzięki temu bazy danych SQL automatycznie dostosowuje tooyour obciążenia w sposób kontrolowanych i bezpiecznych. Automatycznego dostrajania oznacza, że dokładnie monitorowane i porównać przed i po każdej akcji dostrajania hello wydajność bazy danych, a jeśli zwiększyć wydajność hello, nie zostanie przywrócony hello dostrajanie akcji.

Dzisiaj, wielu naszych partnerów systemem [aplikacji SaaS wielodostępne](sql-database-design-patterns-multi-tenancy-saas-applications.md) na podstawie bazy danych SQL są zależne od wydajności automatycznego dostrajania toomake się, że ich aplikacji ma zawsze wydajności stabilne i przewidywalne. Dla nich ta funkcja znacznie zmniejsza hello ryzyko zdarzenia wydajności w środku hello hello nocy. Ponadto, ponieważ część podstawowej klienta używa także programu SQL Server, używają hello tego samego zalecenia indeksowania podał toohelp bazy danych SQL klientom programu SQL Server.

W usłudze SQL Database dostępne są dwa aspekty automatycznego dostrajania:

- **[Automatyczne zarządzanie indeksami](sql-database-automatic-tuning.md#automatic-index-management)**: identyfikuje indeksy, które powinny zostać dodane w bazie danych, i indeksy, które powinny zostać z niej usunięte.
- **[Automatyczna korekta planu](sql-database-automatic-tuning.md#automatic-plan-choice-correction)**: identyfikuje plany, które mogą sprawiać problemy i rozwiązuje problemy z wydajnością planów SQL (dostępne już wkrótce w programie SQL Server 2017).

### <a name="adaptive-query-processing"></a>Adaptacyjne przetwarzanie zapytań

Również dodajemy hello [przetwarzania zapytania adaptacyjną](/sql/relational-databases/performance/adaptive-query-processing) rodziny tooSQL funkcje bazy danych, wraz z przeplotem wykonywania dla funkcji zwracających wiele instrukcji partii trybu pamięci grant opinii i sprzężeń adaptacyjną trybu partii . Każda z tych funkcji przetwarzania zapytania adaptacyjną stosuje podobne techniki "Dowiedz się więcej i dostosowania" ułatwienia dalsze adres wydajności problemów powiązanych toohistorically intractable zapytanie optymalizacji problemów.

### <a name="intelligent-threat-detection"></a>Inteligentne wykrywanie zagrożeń

 [Wykrywanie zagrożeń SQL](sql-database-threat-detection.md) wykorzystuje [inspekcji bazy danych SQL](sql-database-auditing.md) toocontinuously monitor Azure SQL bazy danych programu potencjalnie szkodliwe prób tooaccess poufnych danych. Wykrywanie zagrożeń SQL zawiera nową warstwę zabezpieczeń, co umożliwia klientom toodetect i odpowiadać toopotential zagrożeń w miarę ich występowania, zapewniając alerty zabezpieczeń w nietypowych działań. Użytkownicy otrzymują alerty o podejrzanych działaniach w bazie danych, potencjalnych lukach w zabezpieczeniach, atakach polegających na wstrzyknięciu kodu SQL i anomaliach we wzorcach dostępu do bazy danych. Zagrożenia SQL alerty o wykryciu zawierają szczegółowe informacje o podejrzanych działaniach i zalecane działania dotyczące tooinvestigate i uniknięcie hello zagrożenia. Użytkownicy można eksplorować hello podejrzane zdarzenia toodetermine, jeśli wyniki zdarzenia hello tooaccess próby naruszenia lub wykorzystać danych w bazie danych hello. Wykrywanie zagrożeń umożliwia proste tooaddress potencjalne zagrożenia toohello bazy danych bez toobe potrzeby hello ekspert zabezpieczeń lub zarządzać zabezpieczeniami zaawansowanymi, monitorowanie systemów.

## <a name="advanced-security-and-compliance"></a>Zaawansowane zabezpieczenia i zgodność

Baza danych SQL oferuje szeroką gamę [wbudowane funkcje zabezpieczeń i zgodności](sql-database-security-overview.md) toohelp aplikacji spełnić różne wymagania dotyczące zabezpieczeń i zgodności. 

### <a name="auditing-for-compliance-and-security"></a>Inspekcja zgodności i zabezpieczeń

[SQL Database Auditing](sql-database-auditing.md) śledzi zdarzenia bazy danych i zapisuje je tooan dziennik inspekcji na koncie magazynu Azure. Inspekcja pomaga zachować zgodność z przepisami, analizować aktywność bazy danych oraz uzyskać wgląd w odchylenia i anomalie, które mogą oznaczać problemy biznesowe lub podejrzane naruszenia zabezpieczeń.

### <a name="data-encryption-at-rest"></a>Szyfrowanie danych w spoczynku

Baza danych SQL [przezroczystego szyfrowania danych](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database) pomaga chronić przed zagrożeniem hello złośliwych działań, wykonując w czasie rzeczywistym szyfrowania i odszyfrowywania hello bazy danych, skojarzonych kopii zapasowych, i pliki dziennika transakcji w stanie spoczynku bez konieczności zmiany toohello aplikacji. Począwszy od maja 2017 roku wszystkie nowo utworzone bazy danych SQL na platformie Azure są automatycznie chronione za pomocą funkcji przezroczystego szyfrowania danych (TDE, Transparent Data Encryption). Funkcji TDE jest SQL do sprawdzone szyfrowania na rest technologia, która jest wymagana przez wiele tooprotect standardów zgodności przed kradzieżą nośników magazynowania. Klientów można zarządzać kluczy szyfrowania funkcji TDE hello i innych informacji poufnych, w sposób bezpieczny i zgodne, za pomocą usługi Azure Key Vault.

### <a name="data-encryption-in-motion"></a>Szyfrowanie danych w ruchu

Baza danych SQL jest hello tylko bazy danych systemu toooffer ochrony danych poufnych w locie, podczas przechowywania i podczas przetwarzania z zapytań [zawsze zaszyfrowane](https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-database-engine). Zawsze zaszyfrowane jest branży — pierwszy, który oferuje bezkonkurencyjne danych zabezpieczenie przed naruszeniami obejmujące hello kradzieży danych o kluczowym znaczeniu. Na przykład w zawsze zaszyfrowane, numery kart kredytowych klientów są przechowywane zaszyfrowane w bazie danych hello zawsze, nawet podczas przetwarzania zapytania, umożliwiając odszyfrowywania w momencie hello użycia przez autoryzowanego personelu lub aplikacji wymagających tooprocess danych.

### <a name="dynamic-data-masking"></a>Dynamiczne maskowanie danych

[Baza danych SQL dane dynamiczne maskowanie](sql-database-dynamic-data-masking-get-started.md) ogranicza ujawnienie danych poufnych przez maskowania go toonon uprawnieniami użytkowników. Maskowanie danych dynamicznych zapobiega danych toosensitive nieautoryzowanego dostępu, umożliwiając klientom toodesignate ile hello tooreveal poufnych danych przy minimalnym wpływie na warstwie aplikacji hello. Jest to funkcja zabezpieczeń opartych na zasadach, która ukrywa hello poufne dane zawarte w hello zestawu wyników zapytania za pośrednictwem pola wyznaczonych bazy danych, gdy hello danych w bazie danych hello nie ulega zmianie.

### <a name="row-level-security"></a>Zabezpieczenia na poziomie wiersza

[Wiersz poziomu zabezpieczeń](https://docs.microsoft.com/sql/relational-databases/security/row-level-security) umożliwia klientom toocontrol dostępu toorows w tabeli bazy danych na podstawie charakterystyk hello użytkownika hello wykonywanie zapytania (takich jak przez kontekst grupy członkostwa lub wykonywania). Zabezpieczenia na poziomie wiersza (kontrola dostępu) upraszcza hello projektowania i kodowania zabezpieczeń w aplikacji. Kontrola dostępu umożliwia tooimplement ograniczenia dostępu do wiersza danych. Na przykład zapewnienie, że pracownicy mogą uzyskiwać dostęp do tylko te wiersze danych, które są odpowiednie tootheir działu lub ograniczanie dostępu do danych klienta tooonly firmy tootheir odpowiednich danych hello.

### <a name="azure-active-directory-integration-and-multi-factor-authentication"></a>Integracja usługi Azure Active Directory z uwierzytelnianiem wieloskładnikowym

Baza danych SQL umożliwia toocentrally można zarządzać tożsamościami bazy danych użytkownika i innych usług firmy Microsoft z [integracji Azure Active Directory](sql-database-aad-authentication.md). Ta funkcja upraszcza zarządzanie uprawnieniami i zwiększa bezpieczeństwo. Usługa Azure Active Directory obsługuje [uwierzytelnianie wieloskładnikowe](sql-database-ssms-mfa-authentication.md) (MFA) zabezpieczeń danych i aplikacji tooincrease podczas jednego procesu w tym obsługi.

### <a name="compliance-certification"></a>Certyfikacja zgodności

Usługa SQL Database jest poddawana regularnym inspekcjom i ma certyfikat kilku standardów zgodności. Aby uzyskać więcej informacji, zobacz hello [Microsoft Azure Trust Center](https://azure.microsoft.com/support/trust-center/), gdzie można znaleźć hello najbardziej aktualną listę [certyfikaty zgodności bazy danych SQL](https://azure.microsoft.com/support/trust-center/services/).

## <a name="easy-to-use-tools"></a>Łatwe w użyciu narzędzia

Dzięki usłudze SQL Database tworzenie i konserwowanie aplikacji jest łatwiejsze i bardziej produktywne. Baza danych SQL pozwala toofocus na najlepiej wykonaj: tworzenie atrakcyjnych aplikacji. W usłudze SQL Database możesz zarządzać i projektować, korzystając z narzędzi i umiejętności, które już masz.

- **[Witaj w portalu Azure](https://portal.azure.com/)**: aplikacji sieci web, do zarządzania wszystkich usług platformy Azure 
- **[SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)**: aplikacja kliencka bezpłatne, możesz pobrać zarządzania dowolnej infrastruktury SQL z programu SQL Server tooSQL bazy danych
- **[SQL Server Data Tools w programie Visual Studio](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)**: bezpłatna, udostępniona do pobrania aplikacja kliencka do projektowania relacyjnych baz danych programu SQL Server, baz danych SQL platformy Azure, pakietów usługi Integration Services, modeli danych usługi Analysis Services i raportów usługi Reporting Services.
- **[Visual Studio Code](https://code.visualstudio.com/docs)**: bezpłatne, możesz pobrać typu open source, edytora kodu dla systemu Windows, system macOS i Linux obsługujący rozszerzenia, w tym hello [rozszerzenia mssql](https://aka.ms/mssql-marketplace) do wykonywania zapytań programu Microsoft SQL Server Baza danych Azure SQL i usługi SQL Data Warehouse.

Baza danych SQL obsługuje tworzenie aplikacji z języka Python, Java, Node.js, PHP, Ruby i .NET na powitania MacOS, Linux i Windows. Baza danych SQL obsługuje hello sam [biblioteki połączeń](sql-database-libraries.md) co program SQL Server.

## <a name="engage-with-hello-sql-server-engineering-team"></a>Skontaktuj się z zespołu inżynieryjnego hello programu SQL Server

- [DBA Stack Exchange](https://dba.stackexchange.com/questions/tagged/sql-server): zadawaj pytania dotyczące administrowania bazami danych
- [Stack Overflow](http://stackoverflow.com/questions/tagged/sql-server): zadawaj pytania dotyczące opracowywania zawartości
- [Fora MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver): zadawaj pytania techniczne
- [Microsoft Connect](https://connect.microsoft.com/SQLServer/Feedback): zgłaszaj usterki i wysyłaj prośby dotyczące funkcji
- [Reddit](https://www.reddit.com/r/SQLServer/): omówienie programu SQL Server

## <a name="next-steps"></a>Następne kroki

- Zobacz hello [cennikiem](https://azure.microsoft.com/pricing/details/sql-database/) dla pojedynczej bazy danych i pul elastycznych koszt porównania i kalkulatory.

- Zobacz, czy te szybkiego uruchamiania tooget rozpoczętej:

  - [Utwórz bazę danych SQL w hello portalu Azure](sql-database-get-started-portal.md)  
  - [Utwórz bazę danych SQL z hello wiersza polecenia platformy Azure](sql-database-get-started-cli.md)
  - [Tworzenie bazy danych SQL za pomocą programu PowerShell](sql-database-get-started-powershell.md)

- Aby uzyskać zestaw przykładów interfejsu wiersza polecenia platformy Azure i programu PowerShell, zobacz:
  - [Przykłady interfejsu wiersza polecenia platformy Azure dla usługi SQL Database](sql-database-cli-samples.md)
  - [Przykłady programu Azure PowerShell dla usługi SQL Database](sql-database-powershell-samples.md)
