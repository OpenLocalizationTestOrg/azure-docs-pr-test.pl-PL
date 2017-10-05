---
title: "Oferty aplikacji sieci Web usługi aplikacji Azure dla przedsiębiorstwa"
description: "Przedstawia sposób użycia aplikacji sieci Web usługi aplikacji Azure do utworzenia witryny sieci Web rozwiązania dla biznesu enterprise"
services: app-service\web
documentationcenter: 
author: apwestgarth
manager: erikre
editor: 
ms.assetid: cf9ac3b2-0493-4461-8b64-251d3a5cd5b5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: anwestg
ms.openlocfilehash: 4d46654f42a3fd5c9b491f1b565c2acfa0dc52c4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-web-apps-offerings-for-enterprise-whitepaper"></a>Oferty aplikacji sieci Web usługi aplikacji Azure — oficjalny dokument Enterprise
Konieczność pozwalają ograniczyć koszty i dostarczanie rozwiązań IT szybsze w środowisku szybkiego rozwoju tworzy wyzwania dla deweloperów, specjalistów IT i menedżerów. Użytkownicy są coraz bardziej wyszukiwanie Linia biznesowych (LOB) aplikacje sieci web były szybki, dynamiczne i dostępna z dowolnego urządzenia. W tym samym czasie firmach próbujesz na wielką na zwiększenie produktywności i efektywności pochodzące z integrację z usługami mobilnymi i chmury, co może być coś najprostszą rejestracji jednokrotnej na urządzeniach przy użyciu usługi Active Directory w celu współpracy w usługi Office 365 przy użyciu danych pobieranych z wewnętrznych aplikacji LOB, które z kolei pobiera danych z wdrożenia firmy Salesforce. [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) to usługa w chmurze klasy korporacyjnej do tworzenia, testowania i sieci web i aplikacji dla urządzeń przenośnych, interfejsów API sieci Web i rodzajowy witryn sieci Web. Może służyć do uruchamiania firmowych witryn sieci Web, witryn intranetowych, aplikacji biznesowych i cyfrowe kampanii marketingowych w globalnej sieci centrów danych zoptymalizowanych pod kątem zapewnienia skalowalności i dostępności mechanizmy ciągłej integracji i DevOps nowoczesnych rozwiązań.  

Ten dokument zawiera opis możliwości [aplikacje sieci Web](/services/app-service/web/) usługi koncentruje się w szczególności na aplikacje LOB sieci Web, obejmujące migracji istniejących aplikacji sieci web i wdrażania nowej biznesowych aplikacji sieci web na platformie.

## <a name="audience"></a>Grupy odbiorców
Specjaliści IT, architektów i personel zarządzający systemami informatycznymi chcący migracji obciążeń sieci web chmury, które są aktualnie uruchomione lokalnie. Obciążenia sieci Web może obejmować biznesowych do pracownika albo biznesowych do aplikacji sieci web partnerów.

## <a name="introduction"></a>Wprowadzenie
Aplikacje sieci Web usługi aplikacji jest idealną platformą, na którym udostępniającej zarówno aplikacji sieci web zewnętrznych i wewnętrznych, jak i usługi zapewnia ekonomiczne, skalowalnej, zarządzane rozwiązanie pozwala skoncentrować się na dostarczanie wartość biznesową dla użytkowników, a nie spędzać dużo czasu i utrzymywanie oszczędność pieniędzy i obsługi oddzielnych środowisk. Aplikacje sieci Web oferuje elastyczne platformy, na którym chcesz wdrożyć aplikacje sieci web przedsiębiorstwa oferuje możliwość dalszego uwierzytelniania względem lokalnej usługi Active Directory za pomocą integracji z Microsoft Azure Active Directory obsługują wdrożeń bardzo proste i szybkie tworzenie użycie sieci wewnętrznej ciągłej integracji i wdrażania rozwiązań, podczas automatycznego skalowania w miarę wzrostu potrzeb biznesowych — na zarządzana platforma, która pozwala skoncentrować się na aplikacji i nie infrastruktury.

## <a name="problem-definition"></a>Definicja problemów
Poziomo IT zmienia się szybko, Przenieś poza hostingu na serwerach tradycyjnych z ich wysokie koszty inwestycyjne na czas realizacji długa na taki, który używa na żądanie za pomocą usług, które automatycznie skalować do obsługi obciążenia. Działy informatyczne trwa wąskie obniżenie kosztów oraz zużycie infrastruktury i konserwacji wydatków nacisk na zmniejsza koszty inwestycyjne, a także zwiększyć elastyczność. Koniec cyklu życia starszych platform infrastruktury, takich jak Windows Server 2003, prowadzi działy IT, aby przejrzeć migracja do chmury jako potencjalne sposobem uniknięcia koszty inwestycyjne nowe długoterminowej. W przeszłości dyrektorzy działu informatyki będą podejmować decyzje zakupów dla innych działów; jednak coraz CMOs i innych firm jednostki głowic trwa aktywnych roli w sposób ich budżetu jest zużywany i jest zwrot z inwestycji. Coraz firma potrzebuje swoim pracownikom, można znacznie bardziej przenośnymi niż kiedykolwiek przedtem pracownikom pracy zdalnej, wydatków z klientami, na potrzeby uzyskiwania dostępu do systemów proste wolnego więcej czasu.

Zmieniających się potrzeb biznesowych co miesiąc, co tydzień, codziennie. Firmy szukają błyskawicznych globalne skalowanie regularnej zaktualizowanej pełnej nowych funkcji innych firm lub wewnętrznie.  W niektórych przypadkach firmy również szukają możliwości do izolowania aplikacji oraz dostęp do zasobów, podczas gdy umożliwiając korzystanie z urządzeń chmury publicznej. Użytkownicy mają wyższe oczekiwań, z wielu korzystające z usług w ich własnych życie prywatnych, takich jak usługi Office 365. Oczekiwane mają dostęp do usług zaawansowanych funkcji podobne, na bieżąco, ich życia pracy. Aby poradzić sobie z tym żądanie IT musi wyglądu, aby pomóc firmie, aby je włączyć za pomocą wybór i integracja z innej usługi, dokładne wyboru platform, które można dostosować do potrzeb biznesowych, podczas gdy będące również niezawodnej z zmniejszenie całkowitego kosztu posiadania.

Zespoły deweloperów szukasz dostarczać natychmiastowe korzyści, dostarczania nowych funkcji na częste. Wyszukaj ekonomiczne, niezawodne platforma, która integruje się z ich istniejącego testu narzędzia i rozwiązań — programowanie, wersji; i pracy wraz z działów IT automatyzuje wdrażania, zarządzania i alerty, wszystko w celu przestojów.

<a name="highlevel"></a>
## <a name="high-level-solution"></a>Wysokiego poziomu rozwiązania
Aby tworzyć, testować i obsługiwać aplikacje biznesowe coraz używanych platformy sieci Web i platform.  Linią typowych aplikacji biznesowej, takich jak system wydatków pracowników wewnętrznych często składające się wyłącznie z aplikacji sieci web z tworzenia kopii bazy danych do przechowywania danych związane ze stosowaniem.

Usługi aplikacji sieci Web aplikacji jest dobre rozwiązanie do obsługi takich aplikacji oferty skalowalne i niezawodne infrastruktury, który jest zarządzany i poprawkami z niemal zero ręcznej interwencji i przestoje. Platforma Microsoft Azure udostępnia wiele opcji dotyczących magazynów danych na potrzeby obsługi aplikacji sieci web hostowanych w aplikacji sieci Web z programu Microsoft Azure SQL Database, zarządzane skalowalne relacyjnej bazy danych jako usługi, do popularnych usług przez naszych partnerów, takich jak baza danych ClearDB MySQL i bazy danych MongoDB.

Informacje o innym podejściu jest zapewnienie korzystać z istniejących inwestycji lokalnie. W przykładowym scenariuszu system wydatków pracownika, warto Obsługa magazynie danych w ramach infrastruktury wewnętrznej. Może to być integracji z wewnętrznych systemach (raportowania, Lista płac i rozliczeń itp.) lub na spełniają wymagania ładu IT.  Aplikacje sieci Web udostępnia kilka metod umożliwiających można nawiązać połączenia z infrastruktury lokalnej na:

* [Środowiska usługi App Service](app-service-app-service-environment-intro.md) -środowiska usługi aplikacji (ASE) są nową funkcją Premium, który został ostatnio Dodaj do oferty Microsoft Azure App Service.  ASEs zapewniają środowisko pełni izolowanym środowisku, aby bezpiecznie pracować aplikacji w usłudze Azure App Service na dużą skalę, a doświadczonym izolacji i bezpiecznego dostępu do sieci   
* [Połączenia hybrydowe](../biztalk-services/integration-hybrid-connection-overview.md) — połączeń hybrydowych są funkcją usługi BizTalk platformy Microsoft Azure i Włącz aplikacje sieci Web do łączenia się z lokalnych zasobów bezpieczne, na przykład programu SQL Server, MySQL, interfejsów API sieci Web i usług sieci web niestandardowego.
* [Integracja sieci wirtualnych](https://azure.microsoft.com/blog/2014/09/15/azure-websites-virtual-network-integration/) — integracja aplikacji sieci Web z siecią wirtualną Azure umożliwia nawiązanie połączenia aplikacji sieci web do sieci wirtualnej Azure, który z kolei może być połączony z infrastruktury lokalnej na za pośrednictwem sieci VPN lokacja lokacja.

Poniższych diagramach przedstawiać przykład rozwiązania wysokiego poziomu przy użyciu opcji łączności dla zasobów lokalnych.  W pierwszym przykładzie pokazano, jak można to osiągnąć przy użyciu standardowych funkcji Azure App Service i drugi przedstawia, jak to osiągnąć za pomocą premium oferty środowiska usługi App Service.

Korzystanie z usługi aplikacji — warstwa standardowa funkcji:![](./media/web-sites-enterprise-offerings/on-premise-connectivity-solutions.png "Using Standard App Service Features")

Przy użyciu środowiska usługi aplikacji:![](./media/web-sites-enterprise-offerings/on-premise-connectivity-solutions-ASE.png "Using an App Service Environment")

## <a name="business-benefits"></a>Korzyści biznesowe
Usługi aplikacji Web Apps zapewnia szereg korzyści biznesowe, umożliwiające funkcja ma być bardziej ekonomiczne i elastyczne w dostarczaniu dla potrzeb biznesowych.

### <a name="paas-model"></a>PaaS Model
Usługi aplikacji sieci Web aplikacji jest oparty na platformie jako model usługi, która udostępnia wiele oszczędności kosztów i wydajności.  Nie należy poświęcić godziny Zarządzanie maszynami wirtualnymi, stosowanie poprawek systemów operacyjnych i platform. Aplikacje sieci Web jest automatycznie poprawioną środowiska, dzięki czemu można skupić się na zarządzaniu aplikacji sieci web i nie maszyn wirtualnych, pozostawiając zespoły swobodę stanowią wartość biznesową dodatkowe.

PaaS Model wspieranie aplikacji sieci Web umożliwia lekarze metodologii DevOps do zrealizowania założonych. Jako firma oznacza pełnego zarządzania i integracji w całej aplikacji cały cykl, w tym projektowanie, testowanie, wersji, monitorowania i zarządzania i pomocy technicznej.

Dla zespołów deweloperów można skonfigurować ciągłej integracji i wdrażania przepływy pracy w Visual Studio Team Services, GitHub, TeamCity, Hudson lub BitBucket, włączenie automatycznego kompilacji, testu i wdrożenia umożliwiające szybsze wersji cykle, podczas gdy zmniejszenie tarcie wykonywane podczas zwalniania w istniejącej infrastruktury. Aplikacje sieci Web obsługuje również tworzenie wielu testowania i przejściowych środowiskach wersji przepływu pracy, nie należy do zarezerwowania lub przydzielić sprzętu dla tych celów, można utworzyć dowolną liczbę środowiska mają i definiować własne podwyższanie poziomu do zwolnienia przepływu pracy. Jako biznesowe, które można wersji do gniazda testu z kontroli źródła, wykonaj serii testów i po pomyślnym zakończeniu wyznaczyć na gniazdo etap, a ostatecznie przechodź do środowiska produkcyjnego bez przestojów, tę zaletę, aplikacji sieci web obsługiwanych aplikacji sieci Web są wstępnie załadowane i dynamicznego, aby zapewnić najwyższy poziom zadowolenia.  Ponadto firm można wykorzystać testowanie w produkcji możliwości aplikacji usługi sieci Web aplikacji do bezpośrednio części ruchu do innego gniazda, zweryfikuj zmian przed przełączanie cały ruch do nowego wdrożenia lub przywrócenie cały ruch do poprzedniego wdrożenia.

Zespoły operacje można uznać pewność, że są one najlepsze pozycji do reagowania na problemy ze wszystkimi swoimi aplikacjami sieci web hostowanych aplikacji sieci Web z wbudowanych funkcji monitorowania i alertów. Należy zespołów operacyjnych poczynionych inwestycji w analizy i rozwiązań monitorowania takich z Microsoft Visual Studio Application Insights, New Relic i AppDynamics. Są także w pełni obsługiwane aplikacji sieci Web, zapewniając ciągłość obsługi i znanych środowiskach, z którym mają być monitorowane aplikacje sieci web.

Ponadto aplikacje sieci Web udostępnia funkcję automatycznego wykonywania kopii zapasowej Twoje aplikacje i hostowanej baz danych bezpośrednio do kontenera magazynu obiektów Blob Azure. Zapewnia to łatwa metoda sposób i bardzo ekonomiczne, z którą ma zostać odzyskiwania danych po awarii, zmniejszając potrzebę złożonej na lokalnym sprzętu i oprogramowania.

### <a name="ease-of-migration"></a>Łatwość migracji
Konserwacji sprzętu i obrotu jest problem z kluczem dla firm, ponieważ przyspieszyć cykle sprzętu i systemów operacyjnych. Może mieć wiele serwerów z systemem Windows Server 2003 R2, które są dostępne w celu wsparcia w 2015, ale są one nadal hosting aplikacji sieci web klucza dla Twojej firmy? Usługi aplikacji sieci Web aplikacji jest doskonałym kandydatem na którym obsługi tych aplikacji sieci web i racjonalizacja biznesowa nieruchomości sprzętu. Aplikacje sieci Web umożliwia dostęp do zakresu specyfikacje sprzętowe, które są zarządzane i przechowywane w ramach usługi, co eliminuje konieczność współczynnik zastąpienia i kosztów zarządzania jako część budżetu infrastruktury.  Migracji może być proste jako kopię i Wklej operację z istniejącego wdrożenia aplikacji sieci Web lub bardziej złożonych migracji, gdzie korzystania z Asystenta migracji aplikacji sieci Web spowoduje dodanie wartości. Aplikacje sieci web migrowanych kredyty pełne spektrum usług platformy Azure, integrację dodatkowych usług do aplikacji sieci web. Na przykład można rozważyć dodanie usługi Azure Active Directory do kontrolowania dostępu do aplikacji oparte na skojarzenie użytkowników do grup zabezpieczeń. Innym przykładem może być dodanie usługi pamięć podręczna w celu zwiększenia wydajności i zmniejszenia opóźnień, jeśli całkowity lepsze środowisko użytkownika.

### <a name="enterprise-class-hosting"></a>Hosting klasy Enterprise
Usługi aplikacji Web Apps zapewnia stabilny, niezawodne platforma, która ma zostały sprawdzone, aby można było obsługiwać wiele różnych firm musi z wewnętrznego projektowania i testowania obciążeń małymi, wysoko skalowane dużego natężenia ruchu sieciowego witryn sieci Web. Za pomocą aplikacji sieci Web, tworzysz, użyj tej samej platformy hostingu klasy enterprise używanej przez firmę Microsoft jako firmę do śledzenia obciążenia sieci web wysokiej wartości. Aplikacje sieci Web oraz wszystkie usługi na platformie Azure, są tworzone za zabezpieczeń i zgodności z przepisami dotyczącymi działalności, takich jak ISO (ISO/IEC 27001:2005); SOC1 i SOC2 SSAE 16/ISAE 3402 poświadczenia, HIPAA BAA i PCI oraz Fedramp istotą bardzo każdego elementu i funkcji, aby uzyskać więcej informacji można znaleźć pod adresem [http://aka.ms/azurecompliance](/support/trust-center/compliance/).

Platforma Microsoft Azure umożliwia roli na podstawie autoryzacji formanty Włączanie poziomów enterprise sterowania do zasobów w aplikacji sieci Web. RBAC daje przedsiębiorstw zasilania do zaimplementowania własnych zasad zarządzania aplikacjami dla wszystkich ich zasobów w środowisku Azure przypisywania użytkowników do grup i z kolei przypisując wymaganych uprawnień do tych grup względem zasobów, takich jak aplikacji sieci web. Aby uzyskać więcej informacji o RBAC na platformie Azure, zobacz [http://aka.ms/azurerbac](../active-directory/role-based-access-control-configure.md). Korzystając z aplikacji sieci Web, możesz mieć pewność, aplikacji sieci web są wdrażane w środowisku bezpieczne i ma pełną kontrolę, na których terytorium wdrożonych zasobów.

Środowiska usługi aplikacji Azure [http://aka.ms/aseintro](http://aka.ms/aseintro) mają nową opcję planu usług premium klienci chcą korzystać z usługi aplikacji Azure i te zapewniają pełni izolowanym środowisku, środowisko.  Dzięki temu klienci korporacyjni do wdrażania aplikacji, które można wykorzystać bardzo dużej skali przy jednoczesnym również posiadanie pełną kontrolę nad przychodzący i wychodzący ruch sieciowy i ASEs Włącz aplikacje mają mieć szybkich bezpiecznych połączeń za pośrednictwem sieci wirtualnych do zasobów lokalnych.

Aplikacje sieci Web usługi aplikacji mogą również wykorzystać inwestycji w lokalnym oferując możliwość łączenia z powrotem do wewnętrznych zasobów, takie jak magazyn danych lub środowisko programu SharePoint. Zgodnie z opisem w [rozwiązania wysokiego poziomu](#high-level-solution) umożliwia użycie połączeń hybrydowych i łączność sieciową wirtualnych może nawiązywać połączenia w lokalnej infrastrukturze do obsługi i usług.

### <a name="global-scale"></a>Skala globalna
Usługi aplikacji sieci Web aplikacji jest platformy globalnej i skalowalne, włączanie aplikacji sieci web do powiększania i dostosowania do potrzeb rozwoju firmy szybko i z minimalnym długoterminowej planowania i kosztów. Typowe scenariusze infrastruktury lokalnej, rozszerzenia i wzrostu popytu zarówno lokalnie, jak i geograficznie może wymagać dużej ilości zarządzania, planowania i wydatków, aby udostępnić i zarządzania nimi dodatkowej infrastruktury. Aplikacje sieci Web umożliwia skalowanie aplikacji sieci web z i przypływ wymagania. Na przykład przy użyciu aplikacji wydatków na przykład dla większości miesiąca są użytkownicy światła użytkowników aplikacji, ale jako termin każdego miesiąca dla przesyłania wydatków, które zostaną wprowadzone i zwiększa obciążenie dla aplikacji, aplikacje sieci Web ma możliwość automatycznie udostępniać więcej infrastruktury aplikacji i następnie po użycia ma subsided ponownie go można skalować do należy zdefiniować infrastrukturę linii bazowej.

Aplikacje sieci Web jest dostępna globalnie w 24 centrów danych na całym świecie i rosnącym. Najnowsze listy regiony i lokalizacji, zobacz [http://aka.ms/azlocations](http://aka.ms/azlocations). Firmy z aplikacji sieci Web, łatwo można osiągnąć, globalne i skali. Miarę rozwoju firmy do nowych regionów, pulpitów nawigacyjnych aplikacji, których używasz raportowania i hosta aplikacji sieci Web można łatwo wdrożyć do dodatkowe centra danych i obsługiwać lokalnych użytkowników szybciej za pomocą kombinacji aplikacji sieci Web i usługi Azure Traffic Manager, wszystkie tę zaletę skalowalnej infrastruktury poniżej kontraktu i rozwiń potrzeb zmień biur regionalnych.

## <a name="solution-details"></a>Szczegóły rozwiązania
Oto przykład scenariusza migracji aplikacji. Przedstawiono to szczegóły dotyczące sposobu funkcje aplikacji usługi sieci Web aplikacji grupuje aby zapewnić doskonałe rozwiązanie i wartość biznesowa.

W tym przykładzie linia aplikacji biznesowej, które firma Microsoft będzie w niniejszym dokumencie jest raportowanie aplikacji, która umożliwia pracownikom przesłać koszty zwrotu kosztów. Hostowania aplikacji systemu Windows Server 2003 R2 uruchamiania usług IIS 6 i bazy danych jest bazą danych programu SQL Server 2005. Przyczyna wybieramy opcję starszym serwerze znajduje się o nadchodzących końcowy elementu usługi dla Windows Server 2003 R2 i SQL Server 2005 i mamy [narzędzia](http://aka.ms/websitesmigration) i [wskazówki](http://aka.ms/websitesmigrationresources) automatycznie migrację obciążeń na platformie Azure. Z tym pamiętać wzorca w tym przykładzie dotyczą szeroki AGA scenariuszy migracji.

### <a name="migrate-existing-application"></a>Migrowanie istniejących aplikacji
Pierwszym kroku ogólnego rozwiązania przenoszenie aplikacji — biznesowych do aplikacji sieci Web jest aby zidentyfikować istniejące zasoby aplikacji i architektury. Przykładem w tym dokumencie jest hostowany na serwerze usług IIS z bazą danych hostowany na osobnym serwerze SQL, jak pokazano na poniższej ilustracji aplikację sieci web platformy ASP.NET. Pracownicy logowania do systemu za pomocą kombinacji nazwy użytkownika i hasła, wprowadź szczegóły kosztów i przekazać zeskanowane kopie potwierdzeń, do bazy danych dla każdego elementu wydatków.

![](./media/web-sites-enterprise-offerings/on-premise-app-example.png)

#### <a name="items-to-consider"></a>Elementów do uwzględnienia
Gdy aplikacja migracji ze środowiska lokalnego, może być pamiętać kilka ograniczeń aplikacji sieci Web. Oto niektóre kluczowe tematy pod uwagę podczas migrowania aplikacji sieci web do aplikacji sieci Web ([http://aka.ms/websitesmigrationresources](http://aka.ms/websitesmigrationresources)):

* Port powiązania — aplikacji sieci Web obsługuje tylko port 80 dla protokołu HTTP i portu 443 dla ruchu HTTPS. Jeśli aplikacja używa innego portu, a następnie po migracji aplikacja będzie używać portu 80 dla protokołu HTTP i portu 443 dla ruchu HTTPS. Jest to często nieszkodliwe problem, ponieważ jest typowe w przypadku wdrożeń lokalnych, aby korzystanie z różnych portów, aby rozwiązać nazwy domeny, szczególnie w środowiskach programistycznych i testowych
* Uwierzytelnianie — aplikacji sieci Web obsługuje uwierzytelnianie anonimowe domyślnie i uwierzytelnianie oparte na formularzach określonych przez aplikację. Aplikacje sieci Web można zapewniają uwierzytelnianie systemu Windows, gdy aplikacja jest zintegrowany z usługą Azure Active Directory i usług AD FS tylko. Jest to funkcja, która została omówiona szczegółowo w [tutaj](http://aka.ms/azurebizapp)
* Zestawy na podstawie GAC — aplikacji sieci Web nie zezwala na wdrożenie zestawów do globalnej pamięci podręcznej zestawów (GAC). W związku z tym Jeśli migrowane aplikacja wykorzystuje to funkcja lokalnymi, rozważ migrację zestawy, aby otworzyć folder bin aplikacji.
* Wersją IIS5 Tryb zgodności — aplikacji sieci Web nie obsługuje trybu zgodności z wersją IIS5, a jako takie każdego wystąpienia aplikacji sieci Web i wszystkich aplikacji sieci web w ramach nadrzędnej wystąpienia aplikacji sieci Web uruchom ten sam proces roboczy w ramach jednej puli aplikacji.
* Używanie bibliotek COM — aplikacji sieci Web nie zezwala na rejestracji składników COM na platformie. Dlatego jeśli aplikacja jest użycie wszystkich składników modelu COM, te potrzebny do ponownego napisania w kodzie zarządzanym i wdrażane w aplikacji.
* Filtry ISAPI — filtry ISAPI są obsługiwane w aplikacjach sieci Web. Musi być wdrożony jako część aplikacji, a zarejestrowanego w pliku web.config aplikacji sieci web. Aby uzyskać więcej informacji, zobacz [http://aka.ms/azurewebsitesxdt](web-sites-transform-extend.md).

Gdy te tematy zostały uwzględnione, aplikacji sieci web jest gotowa do chmury. Nie martw się, a jeśli niektóre tematy pełni nie są spełnione, narzędzie do migracji zapewni najlepszą do migracji.

Następne kroki w procesie migracji są do tworzenia aplikacji sieci web usługi aplikacji i bazy danych SQL Azure. Istnieją różne rozmiary wystąpienia aplikacji sieci Web z różną liczbę rdzeni Procesora i ilości pamięci RAM dostępnych do wyboru oparte na wymagań aplikacji sieci web. Aby uzyskać więcej informacji i cenach, zobacz [https://azure.microsoft.com/pricing/details/app-service/](https://azure.microsoft.com/pricing/details/app-service/). Podobnie Microsoft Azure SQL Database może wszystkich potrzeb biznesowych z różnych warstw usług i poziomy wydajności do spełnienia wymagań. Więcej informacji można znaleźć w folderze [https://azure.microsoft.com/pricing/details/sql-database/](https://azure.microsoft.com/pricing/details/sql-database/). Po utworzeniu aplikacji jest przekazywany do aplikacji usługi sieci Web aplikacji, za pośrednictwem FTP lub WebDeploy, a następnie przenieść w bazie danych.

W tej migracji rozwiązania używana baza danych SQL Azure, ale oznacza to nie tylko bazy danych, która jest obsługiwana na platformie Azure. Firmy mogą również wykorzystać MySQL, bazy danych MongoDB, bazy danych Azure rozwiązania Cosmos i wiele innych za pomocą dodatków, które można kupić w [magazynu Azure](/marketplace/partner-program/).

Podczas tworzenia bazy danych SQL Azure wiele opcji są dostępne do importowania istniejącą bazę danych z lokalnego serwera z wygenerowaniem skryptu istniejącej bazy danych przy użyciu [eksportowania aplikacji warstwy danych, a następnie zaimportuj](http://aka.ms/dacpac).

Bazy danych aplikacji wydatków został utworzony przez utworzenie nowej bazy danych SQL Azure, łączenie z bazą danych przy użyciu programu SQL Server Management Studio i ponownie uruchomić skrypt w celu tworzenia schematu bazy danych i wypełnić je danymi z lokalną bazą danych.

Ostatnim krokiem w pierwszym etapie migracji wymaga zaktualizowania parametry połączenia z bazą danych dla aplikacji. Można to osiągnąć za pomocą portalu Azure. Dla każdej aplikacji sieci web można zmodyfikować ustawienia dotyczące aplikacji, w tym wszelkie parametry połączenia używane do łączenia z bazą używany przez aplikację.

### <a name="alternatives-to-using-azure-sql-database"></a>Alternatywy dla przy użyciu bazy danych SQL Azure
Platformy Azure oferuje wiele rozwiązań alternatywnych, do korzystania z bazy danych SQL Azure jako bazy danych podstawowego aplikacji sieci web, jest umożliwienie różnych obciążeń, tj. za pomocą rozwiązania NoSQL lub Włącz platformę do potrzeb danych biznesowych. Na przykład firma może utrzymywać dane, które nie mogą być przechowywane w innej lokalizacji lub w środowisku chmury publicznej i w związku z tym będzie wyglądać Obsługa ich lokalnej bazy danych.

#### <a name="connectivity-to-on-premises-resources"></a>Łączność z lokalnych zasobów
Usługi aplikacji Web Apps oferuje wiele opcji w celu nawiązania zasobów lokalnych, takich jak bazy danych, włączanie ponownego użycia istniejącej infrastruktury wysokiej wartości. Dostępne opcje to wymienione poniżej:

* Środowiska usługi App Service są izolowane i tworzone w podsieci sieci wirtualnej, w związku z tym włączenie środowiska do komunikowania się z punktami końcowymi prywatne, znajduje się w tej samej sieci wirtualnej - [http://aka.ms/appserviceasenetworking](http://aka.ms/appserviceasenetworking)
* Integracja sieci wirtualnych aplikacji sieci Web obsługuje integrację między aplikacjami sieci Web i sieci wirtualnej platformy Azure, umożliwiając dostęp do zasobów w sieci wirtualnej, umożliwiający, jeśli połączone z siecią lokalną z siecią VPN lokacja lokacja, łączność bezpośrednio do użytkownika w przypadku systemów lokalnych.
* Połączenia hybrydowe są funkcją usługi BizTalk Azure i podaj łatwy sposób łączenia się poszczególnych lokalnych zasobów, takich jak SQL Server, MySQL, interfejsów API sieci Web HTTP i najbardziej niestandardowych usług sieci Web.

#### <a name="scale-and-resiliency"></a>Skalowanie i odporność
W miarę rozwoju jej pracowników, za pośrednictwem nabycia lub przyrost organicznym naturalny firmy tak zbyt musi sieci web skalowania aplikacji do spełnienia tych wymagań nowe. W rzeczywistości dzisiaj częściej można zobaczyć lepsze rozpowszechniania wspólnie zespołów i pracowników zdalnych, na przykład wymusić firm z oddziałów w Stanach Zjednoczonych, Europie i Azji, przenośne sprzedaży w wielu terytoriów więcej. Aplikacje sieci Web ma możliwość obsługi elastycznej zmiany w skali wygodnie i automatycznie.

Usługi aplikacji Web Apps umożliwia aplikacji sieci web można skonfigurować do skalowania automatycznie za pośrednictwem portalu Azure, w zależności od dwóch wektorów — zaplanowany czas lub przez użycie procesora CPU. Skalowania automatycznego aplikacji sieci Web oferuje ekonomiczne i bardzo elastyczny sposób umożliwiający obsługę większej zmiany w użycia dla wszystkich aplikacji biznesowych, z aplikacji sieci web, takich jak naszym wydatków systemu raportowania do witryny sieci Web, środowisko wysoką odporność ruchu krótki czas trwania promocji marketingowych. Aby uzyskać więcej informacji i wskazówek dotyczących skalowania aplikacji sieci web za pomocą aplikacji sieci Web, zobacz [sposobu skalowania witryn sieci Web](web-sites-scale.md).

Oprócz elastyczność skalowania aplikacji sieci Web ogólną platformy umożliwia ciągłość prowadzenia działalności biznesowej i odporność dzięki możliwości dystrybucji aplikacji sieci web i ich zasobów w wielu centrach danych i regionów geograficznych.

## <a name="summary"></a>Podsumowanie
Usługi aplikacji Web Apps oferuje elastyczny, ekonomiczne, reakcji rozwiązań na potrzeby dynamicznej w środowisku szybkiego rozwoju firmy. Web Apps pomaga firmom zwiększenie produktywności i efektywności przez użycie zarządzana platforma z nowoczesnych możliwości DevOps i zmniejszenie ręce zarządzanie, zapewniając możliwości przedsiębiorstwa w skalowalności, odporności, zabezpieczeń i integracja z lokalnymi zasoby.

## <a name="call-to-action"></a>Wywołanie akcji
Aby uzyskać więcej informacji w usłudze Azure App Service Web Apps, odwiedź stronę [http://aka.ms/enterprisewebsites](/services/websites/enterprise/) gdzie więcej informacji można ustalić źródło, a następnie zaloguj do korzystania z wersji próbnej pod [https://azure.microsoft.com/pricing/free-trial/](https://azure.microsoft.com/pricing/free-trial/) do oceny usługi i odnajdywanie korzyści dla Twojej firmy.

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]
