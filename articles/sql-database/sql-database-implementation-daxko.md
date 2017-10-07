---
title: aaaAzure bazy danych SQL Azure zastosowania - Daxko/CSI | Dokumentacja firmy Microsoft
description: "Dowiedz się więcej o jak Daxko/CSI używa bazy danych SQL tooaccelerate cykl programowania i tooenhance jego działu pomocy technicznej i wydajność"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 00c8a713-f20c-4d6b-b8b7-0c1b9ba5f05b
ms.service: sql-database
ms.custom: reference
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 3e3d58a1d9c3c919fc0e4cdb2765f680719c19d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="daxkocsi-used-azure-tooaccelerate-its-development-cycle-and-tooenhance-its-customer-services-and-performance"></a>Daxko/CSI używane Azure tooaccelerate jego cykl programowania i tooenhance jego działu pomocy technicznej i wydajność
![Logo Daxko/CSI](./media/sql-database-implementation-daxko/csidaxkologo25.png)

Daxko/CSI oprogramowania, które muszą ponieść żądanie: jej klientów centrów przydatności i odtwarzania rośnie szybko, Powodzenie toohello Dziękujemy jego oprogramowania korporacyjnego kompleksowe rozwiązania, ale zatrzymując z hello infrastruktury IT wymaganych dla tego powiększania klientów zostało testowania firmy hello personel działu informatycznego. Hello firmy coraz został ograniczony przez wzrost obciążenia operacji, szczególnie w przypadku zarządzania wzrostu bazy danych. Gorsze obciążenie tej operacji została Wycinanie do zasoby projektowe dla nowych inicjatyw, takie jak nowe funkcje mobilności oprogramowania hello firmy.

Zgodnie z tooDavid Molina, dyrektor rozwoju produktów w Daxko/CSI Azure podanego oprogramowania CSI hello platforma jako usługa (PaaS) modelu, że jest ono potrzebne toosimplify Zarządzanie bazą danych, zwiększenia skalowalności i zwolnić zasoby toofocus na oprogramowanie zamiast ops. "Baza danych SQL azure to doskonałe rozwiązanie firmie Microsoft. Nie ma tooworry związane z konserwacją programu SQL Server, klastra pracy awaryjnej i hello wszystkich innych potrzeb infrastruktury to idealne dla instytucji."

Ponieważ migracji tooAzure, oprogramowania CSI musi Operatorzy tylko dwa toomanage za pośrednictwem 600 klienta baz danych. Witaj firma korzysta z bazy danych SQL Azure elastycznych pul baz danych klienta toomove na podstawie rozmiaru i wymagają.

Kontynuuje Molina "naszym klientom mieli świadomość hello zmienić natychmiast. Przed pule elastyczne czasami miało limity czasu i inne problemy w okresach serii. Używając puli elastycznej platformy Azure mogą serii zgodnie z potrzebami i używać oprogramowania hello bez problemów."

Ponadto tooimproving wydajności dla klientów, Azure pule elastyczne zwalniane zasobów oprogramowania CSI toofocus dotyczące tworzenia nowych usług i funkcji, zamiast zajmowanie operacje i zarządzania. Te zasoby IT pomogła oprogramowania CSI, zwiększyć jego oprogramowania korporacyjnego oferty, SpectrumNG, toohelp Uwzględnij elementy członkowskie siłowni, zwiększyć wydajność pracowników i nadaj pracowników i członków dostęp z urządzeń przenośnych interakcyjne zadań i powiadomień w czasie rzeczywistym.

Azure również pomogła oprogramowania CSI przyspiesza i ulepszania hello programowanie i cyklu jakości (QA), należy włączyć opcje automatyzacji. Z implementacją Azure hello firmy menedżerów kompilacji można spakować składników za hello kliknięcia przycisku. Zgodnie z opisem Molina "w ramach cyklu hello, pytań i odpowiedzi jest teraz środowisko testowe tooa stanie toodeploy na platformie Azure ściśle naśladuje naszych stosu produkcji. Natychmiast tooour deweloperów środowiska toovet zmiany, możemy wdrożyć kompilacji. To duży win firmie Microsoft, ponieważ brakuje parzystości do testowania przed nim."

## <a name="offloading-toohello-cloud"></a>Odciążanie toohello chmury
Przed przeniesieniem toohello chmury, CSI oprogramowania pomyślnie były tworzone własnej infrastruktury wielodostępnym w lokalnym centrum danych w Houston. Rozwinięta hello firmy, które muszą ponieść zwiększa rosnący problemy z zakupu, inicjowanie obsługi i utrzymania wszystkich hello sprzętu i oprogramowania wymagane toosupport klientom. Operacji toohandle personelu IT stał się inny "wąskie gardło", która doprowadziła spowolnienie tooa inicjowania obsługi administracyjnej nowych zasobów i wprowadza nowe toocustomers usługi.

CSI oprogramowania przeanalizowaniu możliwości chmury dla eliminując tym obciążenie, dzięki czemu można skupić się na jego kod, zamiast jego operacji. firmy Hello odnalezienie wielu dostawców chmury top hello tylko oferują infrastruktura jako usługa (IaaS) rozwiązania, które nadal wymagają dużych IT personelu toomanage hello IaaS stosu. W celu hello CSI oprogramowania ustaliła, że hello Azure PaaS rozwiązanie było hello najlepiej pasujące do swoich potrzeb. Wyjaśniono Molina "Azure pobiera hello sprzętu i systemu oprogramowania poza sposób hello, więc możemy skupić się na zakupione oprogramowanie, jednocześnie zmniejszając narzut na naszych IT."

## <a name="making-hello-transition-tooazure"></a>Tworzenie hello tooAzure przejścia
Po wybraniu Azure swojego rozwiązania PaaS, oprogramowania CSI rozpoczęcia migracji jego chmury toohello wewnętrznej bazy danych, jak infrastruktury i baz danych. Wcześniejsze tooAzure SpectrumNG klientów potrzebne tooinstall aplikacji klienckiej, która przekazane za pomocą usługi Windows Communication Foundation (WCF) na powitania zaplecza. Zgodnie z tooMolina, "ale niektórzy klienci hostowana wszystko w ich własnych centrach danych, budujemy limit hello produktu toobe wielodostępnej. Firma Microsoft hostowane wszystko w centrum danych w Houston, przy użyciu programu SQL Server jako hello magazynu danych.

"Naszej ofercie produktów również uwzględnione skierowane do elementu członkowskiego portalu sieci web (napisany w języku ASP.net), która została zaprojektowana toobe etykietą biały toomatch hello odbiorcy witrynę internetową i SOAP API strony online hello toosupport i zintegrowany innych firm".

Witaj migracji toohello chmury nie zostały długi dla architektury hello. Zgodnie z tooMolina, "hello większość wysiłków hello omówione zmianę sposobu hello odczytano informacje o plikach konfiguracji, modyfikacji scentralizowane ciągu połączenia, czy automatyzacji hello pakowania, przekazywanie i wdrażanie naszych wersji."

toodevelop hello tworzenie automatyzacji, inżynierów oprogramowania CSI używać programu Azure PowerShell i interfejsów API REST toocreate pakietów i przekazać je tooa środowisko przejściowe dla wersji każdej nocy.
Witaj ogólną tooan przejścia wdrożenia oparte na chmurze usługi Azure poszło szybkie i sprawne dla zespołu IT oprogramowania CSI hello. Wyjaśniono Molina "we wszystkich, było środowisku w wersji beta w chmurze hello w ciągu trzech tygodni toofour podjęcia hello projektu. Który to zaskakująco win firmie Microsoft."

Po konfigurowania i testowania hello środowiska, oprogramowania CSI rozpoczęcia migracji klientów. Klienci korzystający z już hosting CSI oprogramowania przejścia hello zostało niemal bezproblemowe. W przypadku migracji z lokalnego wdrożenia klientów, przez niektóre dodatkowe czas hello migracji toohello chmury, ale nadal głównie został słabe wolne dla klientów i CSI oprogramowania.

Dla nowych klientów, CSI oprogramowania firmy Użyj personel działu informatycznego hello następujący proces tooon tablicy je tooAzure:

1. Skrypty programu PowerShell Azure są używane toospin nowej bazy danych dla klienta hello; Wszyscy klienci Uruchom na tooensure warstwy premium za mało początkowej przepływności hello przejścia.
2. Jeśli to możliwe, CSI oprogramowania używa hello Kreator migracji SQL Azure toomove istniejących danych tooan bazy danych SQL Azure wystąpienia.
3. Na koniec Microsoft SQL Server Integration Services (SSIS) są używane tooreconcile niezgodności w danych hello lub tooperform oczyszczania danych jako wymagane.

Obecnie około 99 procent CSI oprogramowania znajdują się na platformie Azure, centrów cztery regionalne (Północna centralnej, Południowa centralnej, Wschodnia i zachód). Dzięki użyciu centrów danych w regionie geograficznym każdego klienta, czas oczekiwania jest przechowywana tooa jako minimalna.

## <a name="azure-elastic-pools-free-up-it-resources"></a>Azure pule elastyczne zwolnić zasoby IT
Kilka funkcji Azure pomogły oprogramowania CSI shift przed infrastrukturę i operacje funkcji ukierunkowanych toobeing i rozwoju fokus. Prawdopodobnie została hello największych korzyści z elastyczne pule.

Oprogramowanie CSI obecnie zapewnia około 550 bazy danych dla klientów. Przed pule elastyczne było trudne toomanage tak wielu baz danych w ramach struktury warstwy. Menedżerowie OPS miał warstwami wydajności tooassign w zależności od potrzeb serii hello klientów, które są wymagane znaczących IT zasobów obciążenie. Z pule elastyczne menedżerów można przypisać dzierżawcy, premium lub puli standardowej, zgodnie z potrzebami, przenieść klientów w oparciu o rozmiar i muszą. Klienci mieli niemal natychmiast; świadomość hello skutków hello pul elastycznych przed pule elastyczne klienci była limity czasu i inne problemy okresach obciążenia serii, ale z pul elastycznych klientów może zgłaszać seria działań, zgodnie z potrzebami i może nadal toouse SpectrumNG bez problemów.

## <a name="azure-active-geo-replication-accelerates-reporting"></a>Azure aktywna replikacja geograficzna przyspiesza raportowania
Kilka klientów CSI oprogramowania są także korzystanie z platformy Azure aktywna replikacja geograficzna. Z aktywna replikacja geograficzna, zapasowej toofour czytelny pomocniczej bazy danych można skonfigurować w hello regionach z centrami danych tego samego lub innego. Oprogramowanie CSI korzysta z aktywnej georeplikacji na dwa sposoby: najpierw hello pomocniczej bazy danych są dostępne w przypadku hello datacenter awarii lub hello brakiem tooconnect toohello głównej bazy danych; i drugie, hello pomocniczej bazy danych można odczytać i mogą być używane toooffload obciążeń tylko do odczytu, takich jak zadania raportowania. Niektórzy klienci oprogramowania CSI Użyj tego tooaccelerate korzyści raportowania przepływów pracy.

## <a name="csi-software-application-logic-and-architecture"></a>Architektura i logiki aplikacji CSI oprogramowania
SpectrumNG używa role sieci web. Ponieważ aplikacja hello jest wielodostępne, usługi WCF jest używane toohandle hello początkowe żądanie połączenia od klientów. Jak Państwa Molina "hello żądanie identyfikuje każdego klienta, które następnie umożliwia nam kompilacji ciąg połączenia limit tootheir toodo baz danych niezależnie od potrzebujemy toodo."

Dla warstwy sieci web hello jej usług oprogramowania CSI korzysta z platformy Azure automatyczne skalowanie, oparte na datę i godzinę. Dostępne zasoby są automatycznie zwiększona tooaccommodate większego użycia w godzinach pracy, zgodnie z toohello strefą czasową każdego regionalne centrum danych. Zasoby są również określać tooscale w weekendy, gdy są niższe potrzeb klientów.

![Architektura Daxko/CSI](./media/sql-database-implementation-daxko/figure1.png)

Rysunek 1. Rola proces roboczy usługi w chmurze pobiera dane strukturalne z bazy danych SQL Azure i częściowo ustrukturyzowanych danych z magazynu tabel. SpectrumNG użytkownicy korzystają z, że danych za pośrednictwem chmury usług roli sieci web.

## <a name="using-web-apps-and-a-web-plan-tier-for-mobile-apps"></a>Za pomocą aplikacji sieci web i warstwą plan sieci web dla aplikacji mobilnych
Za pomocą usługi Azure SQL Database zwalniane zasobów dla oprogramowania CSI tooenable nowych inicjatyw, łącznie z pełną platform przenośnych oparte na niestandardowego interfejsu API hostowanych w aplikacjach sieci web platformy Azure. Platforma Hello umożliwia członkom siłowni i personelu toouse urządzeń przenośnych toocheck harmonogramy zarezerwować klas i odbierania wiadomości.

Witaj platformy używa tootake zorientowane na usługę architektura (SOA) pojedynczego składnika —, takich jak system punktach sprzedaży (POS) lub system sprzedaży — Przenieś go na powitania Przylot tooanother web planu, a następnie pokrętła się toosupport usługi tego składnika, pozostawiając wszystkich elementów na Witaj oryginalnego planu sieci web. Ta możliwość zapewnia elastyczność ogromne CSI oprogramowania, co zapewnia utrzymywanie niskich kosztów.

## <a name="azure-lets-csi-software-developers-focus-on-apps-and-services"></a>Azure umożliwia oprogramowania CSI deweloperzy fokus na aplikacje i usługi
Baza danych SQL Azure nie jest po prostu boon tooSpectrumNG klientom, którzy korzystają usługi hello szybkie i niezawodne, również jest duży win oprogramowania CSI personelu IT i deweloperów. Przenosząc tooAzure ops w chmurze hello oprogramowania CSI zmniejszyć obciążenie zasobów i infrastruktury, znacznie skrócić czas jego programistycznych i nie będzie już potrzebował toomicromanage baz danych toooptimize wydajności dla swoich dzierżaw.

## <a name="more-information"></a>Więcej informacji
* toolearn więcej informacji na temat usługi Azure pule elastyczne, zobacz [pule elastyczne](sql-database-elastic-pool.md).
* Zobacz toolearn więcej informacji na temat narzędzia bazy danych i elastyczne skalowanie [narzędzi elastycznej bazy danych i elastyczne skalowanie](sql-database-elastic-scale-get-started.md).
* Zobacz toolearn więcej informacji na temat migracji bazy danych programu SQL Server, zobacz [migracji tooAzure bazy danych programu SQL Server](sql-database-cloud-migrate.md).
* toolearn więcej informacji na temat aktywna replikacja geograficzna, zobacz [aktywna replikacja geograficzna](sql-database-geo-replication-overview.md).
* Zobacz toolearn więcej informacji na temat ról sieć Web i roli proces roboczy [roli proces roboczy](../fundamentals-introduction-to-azure.md#compute).    
* toolearn więcej informacji na temat usługi Azure Service Bus, zobacz [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).
* Zobacz toolearn więcej informacji na temat automatycznego skalowania [skalowania usługi w chmurze](../cloud-services/cloud-services-how-to-scale.md).

