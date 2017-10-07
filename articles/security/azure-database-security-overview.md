---
title: "Przegląd zabezpieczeń bazy danych aaaAzure | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera omówienie funkcji zabezpieczeń hello Azure bazy danych."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: TomSh
ms.openlocfilehash: 13f14b99d15800e85e9906a9d167eb0adf2135de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-security-overview"></a>Przegląd zabezpieczeń bazy danych platformy Azure

Zabezpieczeń jest szczególnie ważne w przypadku zarządzania bazami danych i zawsze było priorytet bazy danych SQL Azure. Baza danych SQL Azure obsługuje zabezpieczenia połączeń z reguły zapory i szyfrowanie połączenia. Obsługuje on uwierzytelniania za pomocą nazwy użytkownika i hasła i Azure uwierzytelnianie usługi Active Directory, który używa tożsamości zarządzanych przez usługę Azure Active Directory. Autoryzacji używa kontroli dostępu opartej na rolach.

Baza danych SQL Azure obsługuje szyfrowanie, wykonując w czasie rzeczywistym szyfrowanie i odszyfrowywanie bazy danych, skojarzonych kopii zapasowych i plików dziennika transakcji w stanie spoczynku bez konieczności zmiany toohello aplikacji.

Firma Microsoft udostępnia dodatkowe sposoby tooencrypt danych przedsiębiorstwa:

-   Komórki poziomu szyfrowania tooencrypt określone kolumny lub komórki nawet danych z różnymi kluczami szyfrowania.
-   Jeśli potrzebujesz sprzętowego modułu zabezpieczeń lub centralne zarządzanie hierarchii klucza szyfrowania, należy rozważyć użycie usługi Azure Key Vault z programem SQL Server w maszynie Wirtualnej platformy Azure.
-   Zawsze zaszyfrowane (obecnie w wersji zapoznawczej) umożliwia tooapplications przezroczystego szyfrowania i umożliwia klientom tooencrypt poufnych danych w aplikacjach klienckich bez udostępniania kluczy szyfrowania hello z bazy danych SQL.

Usługa Azure SQL Database Auditing umożliwia przedsiębiorstwom toorecord zdarzenia tooan inspekcji logowania usługi Azure Storage. SQL Database Auditing integruje się również z usługi Microsoft Power BI toofacilitate przechodzenia raportów i analiz.

 Baz danych SQL Azure mogą być ściśle zabezpieczonych toosatisfy najbardziej przepisami lub wymagania dotyczące zabezpieczeń, w tym HIPAA, ISO 27001/27002 i PCI DSS poziom 1, między innymi. Bieżącą listę certyfikaty zgodności zabezpieczeń znajduje się w temacie hello [witryny Microsoft Azure Trust Center](http://azure.microsoft.com/support/trust-center/services/).

W tym artykule przedstawiono podstawy hello zabezpieczanie Structured, tabelarycznych i danych relacyjnych baz danych Microsoft Azure. W szczególności opisano rozpoczęcie pracy z zasobami na potrzeby ochrony danych, kontrolowania dostępu i aktywnego monitorowania.

W tym artykule Omówienie zabezpieczeń bazy danych Azure koncentruje się na powitania w następujących obszarach:

-   Ochrona danych
-   Kontrola dostępu
-   Aktywne monitorowanie
-   Zarządzanie zabezpieczeniami scentralizowane
-   Rynek platformy Azure

## <a name="protect-data"></a>Ochrona danych

Baza danych SQL zabezpiecza dane przez zapewnienie szyfrowanie danych w ruchu przy użyciu [Transport Layer Security](https://support.microsoft.com/kb/3135244)dla rest danych przy użyciu [przezroczystego szyfrowania danych](http://go.microsoft.com/fwlink/?LinkId=526242)i danych za pomocą użyj [ Zawsze zaszyfrowane](https://msdn.microsoft.com/library/mt163865.aspx).

W tej sekcji są omawiane:

-   Szyfrowanie ruchu
-   Szyfrowanie w spoczynku
-   Szyfrowanie przy użyciu (klienta)

Dla innych sposobów tooencrypt danych, należy wziąć pod uwagę:

-   [Szyfrowanie na poziomie komórki](https://msdn.microsoft.com/library/ms179331.aspx) tooencrypt określone kolumny lub komórki nawet danych z różnymi kluczami szyfrowania.
-   Jeśli potrzebujesz sprzętowego modułu zabezpieczeń lub centralnego zarządzania hierarchią kluczy szyfrowania, rozważ użycie [funkcji Azure Key Vault w usłudze SQL Server w maszynie wirtualnej Azure](http://blogs.technet.com/b/kv/archive/2015/01/12/using-the-key-vault-for-sql-server-encryption.aspx).

### <a name="encryption-in-motion"></a>Szyfrowanie ruchu

To powszechny problem, dla wszystkich aplikacji klient/serwer jest hello potrzebę prywatności, jak dane są przenoszone w sieciach prywatnych i publicznych. Jeśli dane przenoszenie za pośrednictwem sieci nie są szyfrowane, brak hello prawdopodobieństwo, że mogą być przechwytywane i kradzieży przez nieautoryzowanych użytkowników. Podczas pracy z usługami bazy danych, należy się upewnić, że dane są szyfrowane między hello bazy danych klienta i serwera, jak również między serwerami bazy danych, które komunikują się ze sobą i z aplikacji warstwy środkowej toomake.

Jednym z problemów podczas administrowania siecią jest zabezpieczanie danych przesyłanych między aplikacjami przez niezaufaną sieć. Można użyć [protokoły TLS/SSL](https://docs.microsoft.com/windows-server/security/tls/transport-layer-security-protocol) tooauthenticate serwerów i klientów i korzystania z niej tooencrypt wiadomości między stronami hello uwierzytelniony.

W procesie uwierzytelniania hello klient TLS/SSL wysyła serwer protokołu TLS/SSL tooa, a serwer hello odpowiada informacje powitania serwera hello musi tooauthenticate się. powitania klienta i serwer dodatkowo wymieniają się kluczami sesji, a hello zakończenia okna dialogowego uwierzytelniania. Po zakończeniu uwierzytelniania między powitania serwera i klienta hello przy użyciu kluczy szyfrowania symetrycznego hello, które są ustalane w procesie uwierzytelniania hello może rozpocząć komunikacja zabezpieczona protokołem SSL.

Wszystkie tooAzure połączenia bazy danych SQL wymagają szyfrowania (SSL/TLS) na cały czas podczas tooand "w drodze" z bazy danych hello jest danych. Usługi SQL Azure używa protokołu TLS/SSL tooauthenticate serwerów i klientów, a następnie użyć jej tooencrypt wiadomości między stronami hello uwierzytelniony. W parametrach połączenia aplikacji musi określić parametry tooencrypt hello połączenia i nie tootrust hello certyfikatu serwera (odbywa się automatycznie po skopiowaniu parametrów połączenia poza hello klasycznego portalu Azure), w przeciwnym razie hello połączenia zostanie weryfikuje tożsamość hello powitania serwera i będzie narażony ataki za "man-in--middle". Witaj sterownikiem programu ADO.NET, na przykład te parametry ciągu połączenia są Szyfruj = True i TrustServerCertificate = False.

### <a name="encryption-at-rest"></a>Szyfrowanie w spoczynku
Może potrwać kilka środki ostrożności toohelp hello bezpiecznej bazie danych na przykład projektowania bezpieczny system, szyfrowania poufnych zasobów i konfigurowania zapory wokół hello serwerów baz danych. Jednak w przypadku których kradzieży hello nośnik fizyczny (takich jak dyski lub taśmy kopii zapasowych), strony złośliwego można po prostu przywrócić lub dołączyć hello bazy danych i przeglądać hello danych.

Jedno rozwiązanie jest tooencrypt hello poufnych danych w bazie danych hello i chroni hello kluczy, które są używane tooencrypt hello danych przy użyciu certyfikatu. Zapobiega to osobom niemającym hello kluczy przy użyciu danych hello, ale muszą być planowane tego rodzaju ochrony.

Ten problem, SQL Server i Azure SQL obsługuje toosolve [funkcji przezroczystego szyfrowania danych (TDE)](https://docs.microsoft.com/sql/relational-databases/securityrecryption/transparent-data-encryption-tde). Funkcji TDE szyfruje programu SQL Server i bazy danych SQL Azure plików danych, znane jako szyfrowanie danych magazynowanych.

Azure SQL Database przezroczystego szyfrowania danych chroni przed zagrożeniem hello złośliwych działań, wykonując w czasie rzeczywistym szyfrowania i odszyfrowywania hello bazy danych, skojarzonych kopii zapasowych i plików dziennika transakcji w stanie spoczynku bez konieczności wprowadzania zmian toohello aplikacji.  

Funkcji TDE szyfruje magazyn hello całej bazy danych przy użyciu klucza szyfrowania symetrycznego klucza o nazwie hello bazy danych. W bazie danych SQL klucz szyfrowania bazy danych hello jest chroniony za pomocą certyfikatu wbudowanego serwera. certyfikat serwera wbudowanych Hello jest unikatowy dla każdego serwera bazy danych SQL.

Jeśli baza danych jest w relacji replikacji geograficznej GeoDR, jest chroniony przez inny klucz na każdym serwerze. Jeśli dwie bazy danych są połączone toohello tym samym serwerze, mają hello tego samego certyfikatu wbudowanych. Microsoft automatycznie przełącza tych certyfikatów, co najmniej co 90 dni. Ogólny opis funkcji TDE, zobacz [funkcji przezroczystego szyfrowania danych (TDE)](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-tde).

### <a name="encryption-in-use-client"></a>Szyfrowanie przy użyciu (klienta)

Większość naruszeń danych obejmują hello kradzież krytyczne dane, takie jak numer karty kredytowej lub dane osobowe. Bazy danych może być troves Skarb informacji poufnych. Zawierają dane osobowe, konkurencyjnych informacji poufnych i własności intelektualnej klientów. Utraty lub kradzieży danych, szczególnie danych klienta, może spowodować uszkodzenie marki, wadą konkurencyjnych i poważne kar — nawet spraw sądowych.

![Zawsze szyfrowane](./media/azure-databse-security-overview/azure-database-fig1.png)

[Zawsze zaszyfrowane](https://msdn.microsoft.com/library/mt163865.aspx) jest funkcja zaprojektowana tooprotect poufnych danych, takich jak numery kart kredytowych lub numerów identyfikacyjnych national (na przykład USA numerów ubezpieczenia społecznego), przechowywane w bazach danych usługi Azure SQL Database lub SQL Server. Zawsze zaszyfrowane umożliwia klientom tooencrypt poufnych danych w aplikacjach klienckich i nigdy nie podawaj toohello klucze szyfrowania hello aparatu bazy danych (bazy danych SQL lub SQL Server).

Zawsze zaszyfrowane zapewnia oddzielenie tych, którzy własnych danych hello (i można go wyświetlić) oraz tych, którzy zarządzają danymi hello (ale powinien nie mają dostępu). Zapewniając lokalnych administratorów bazy danych w chmurze operatory bazy danych lub innych wysokimi uprawnieniami, ale nieautoryzowani użytkownicy nie może uzyskać dostępu hello zaszyfrowane dane,

Ponadto zawsze zaszyfrowane sprawia, że tooapplications przezroczystego szyfrowania. Zawsze zaszyfrowane włączone sterownik zainstalowany na komputerze klienckim hello, dzięki czemu można automatycznie szyfrowania i odszyfrowywania danych poufnych w powitania klienta aplikacji. Sterownik Hello szyfruje dane hello w kolumnach poufnych przed przekazaniem hello danych toohello aparatu bazy danych, a automatycznie ponownie zapisuje zapytania, tak aby hello semantyki toohello aplikacji zostały zachowane. Podobnie sterownik hello niewidocznie odszyfrowuje dane przechowywane w kolumnach bazy danych zaszyfrowanych, zawarte w wynikach zapytania.

## <a name="access-control"></a>Kontrola dostępu
tooprovide zabezpieczeń, baza danych SQL kontroluje dostęp przy użyciu reguł zapory ograniczenie łączności za pomocą adresu IP mechanizmów uwierzytelniania wymagające tooprove użytkowników, tożsamości i ograniczanie użytkowników toospecific akcji i dane mechanizmów autoryzacji.

### <a name="database-access"></a>Dostęp do bazy danych

Ochrona danych rozpoczyna się od kontrolowanie dostępu do danych tooyour. datacenter Hello hosting danych zarządza fizyczny dostęp, mimo że możesz skonfigurować zabezpieczenia toomanage zapory na powitania warstwy sieci. Umożliwia również kontrolę dostępu, konfigurując nazw logowania dla uwierzytelniania i definiowanie uprawnień dla ról serwera i bazy danych.

W tej sekcji są omawiane:

-   Zapora i reguły zapory
-   Authentication
-   Autoryzacja

#### <a name="firewall-and-firewall-rules"></a>Zapora i reguły zapory

Usługa Microsoft Azure SQL Database udostępnia usługę relacyjnej bazy danych dla platformy Azure i innych aplikacji internetowych. toohelp chronić dane, zapór zapobiec wszystkich serwera bazy danych tooyour dostępu do chwili określenia komputery, które ma uprawnienia. Zapora Hello przyznaje toodatabases dostępu oparte na powitania pochodzące z adresu IP dla każdego żądania. Aby uzyskać więcej informacji, zobacz [Omówienie reguł zapory usługi Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure).

Witaj [bazy danych SQL Azure](https://azure.microsoft.com/services/sql-database/) usługi są dostępne tylko w porcie TCP 1433. tooaccess bazy danych SQL z komputera, sprawdź, czy zapory komputera klienta pozwalają wychodzących komunikacji TCP na porcie TCP 1433. Należy zablokować połączenia przychodzące na porcie TCP 1433, jeśli nie są one wymagane przez inne aplikacje.

#### <a name="authentication"></a>Authentication

Uwierzytelnianie bazy danych SQL odwołuje się toohow potwierdzenia tożsamości, łącząc toohello bazy danych. Usługa SQL Database obsługuje dwa typy uwierzytelniania:

-   **Uwierzytelnianie SQL:** konta pojedynczego logowania jest tworzony po utworzeniu logicznej wystąpienie serwera SQL o nazwie hello konta subskrybenta bazy danych SQL. To konto łączy za pomocą [uwierzytelniania programu SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-security-overview) (nazwa użytkownika i hasło). To konto jest wystąpienie toothat dołączony administratora w wystąpieniu serwera logicznego hello i na wszystkich baz danych użytkowników. uprawnienia Hello hello konta subskrybenta nie mogą być ograniczone. Może istnieć tylko jedno z tych kont.
-   **Azure uwierzytelnianie usługi Active Directory:** [uwierzytelniania usługi Azure Active Directory](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication) mechanizm łączący tooMicrosoft bazy danych SQL Azure i SQL Data Warehouse przy użyciu tożsamości w usłudze Azure Active Directory ( Azure AD). Ta umożliwia toocentrally można zarządzać tożsamościami użytkowników bazy danych.

![Authentication](./media/azure-databse-security-overview/azure-database-fig2.png)

 Zalety uwierzytelniania usługi Azure Active Directory obejmują:
  - Zapewnia alternatywny tooSQL uwierzytelniania serwera.
  - Również pomaga zatrzymać rozprzestrzenianie hello tożsamości użytkowników na serwerach bazy danych i umożliwia obrotu hasła w jednym miejscu.
  - Możesz zarządzać uprawnieniami bazy danych przy użyciu zewnętrznego grup (Azure Active Directory).
  - Można go wyeliminować zapisywania haseł przez włączenie zintegrowanego uwierzytelniania systemu Windows i innych metod uwierzytelniania obsługiwanych przez usługę Azure Active Directory.

#### <a name="authorization"></a>Autoryzacja
[Autoryzacji](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins) odwołuje się toowhat użytkownika mogą wykonywać w bazie danych SQL Azure i jest to kontrolowane przez konto użytkownika w bazie danych [członkostwo w rolach](https://msdn.microsoft.com/library/ms189121) i [uprawnienia na poziomie obiektu](https://msdn.microsoft.com/library/ms191291.aspx). Autoryzacja jest hello proces określania zabezpieczanego podmiot zabezpieczeń mogą uzyskiwać dostęp do zasobów i jakie operacje są dozwolone dla tych zasobów.

### <a name="application-access"></a>Dostęp do aplikacji

W tej sekcji są omawiane:

-   Dynamiczne maskowanie danych
-   Zabezpieczenia na poziomie wiersza

#### <a name="dynamic-data-masking"></a>Dynamiczne maskowanie danych
Z przedstawicielem w gnieździe wywołanie może identyfikować obiekty wywołujące przez kilka cyfr numeru karty kredytowej lub numer ubezpieczenia społecznego, ale te dane, które elementy nie powinny być całkowicie widoczne toohello działu obsługi.

Czy wszystkie maski, ale hello cztery ostatnie cyfry numer ubezpieczenia społecznego lub numer karty kredytowej w zestawie wyników hello wszelkie zapytania można zdefiniować reguł maskowania.

![Dynamiczne maskowanie danych](./media/azure-databse-security-overview/azure-database-fig3.png)

Inny przykład maska odpowiednie dane można tooprotect określonych danych osobowych (dane osobowe), dzięki czemu deweloper może wysyłać zapytania środowisk produkcyjnych w celu rozwiązywania problemów bez naruszania przepisy dotyczące zgodności.

[SQL bazy danych dynamicznego maskowania danych](https://docs.microsoft.com/azure/sql-database/sql-database-dynamic-data-masking-get-started) ogranicza ujawnienie danych poufnych przez maskowania go toonon uprawnieniami użytkowników. Maskowanie danych dynamicznych jest obsługiwana dla wersji V12 hello bazy danych SQL Azure.

[Maskowanie danych dynamicznych](https://docs.microsoft.com/sql/relational-databases/security/dynamic-data-masking) pomaga zapobiec dostępowi osób nieupoważnionych toosensitive danych, umożliwiając toodesignate ile hello tooreveal poufnych danych przy minimalnym wpływie na warstwie aplikacji hello. Jest to funkcja zabezpieczeń opartych na zasadach, która ukrywa hello poufne dane zawarte w hello zestawu wyników zapytania za pośrednictwem pola wyznaczonych bazy danych, gdy hello danych w bazie danych hello nie ulega zmianie.


> [!Note]
> Witaj, Administratorze bazy danych Azure, administrator serwera lub role zabezpieczeń urzędnika można skonfigurować maskowania danych dynamicznych.

#### <a name="row-level-security"></a>Zabezpieczenia na poziomie wiersza
Innego typowe wymagania dotyczące zabezpieczeń dla wielodostępnych baz danych jest [zabezpieczenia na poziomie wiersza](https://msdn.microsoft.com/library/dn765131.aspx). Ta funkcja umożliwia toocontrol toorows dostępu w tabeli bazy danych na podstawie charakterystyk hello użytkownika hello wykonywania zapytania (np. grupy członkostwa lub wykonywania context).

![-Zabezpieczenia na poziomie wiersza](./media/azure-databse-security-overview/azure-database-fig4.png)

Logika ograniczenie dostępu Hello jest znajduje się w hello warstwy bazy danych zamiast od hello danych w innej warstwie aplikacji. Witaj bazy danych systemu stosuje ograniczenia dostępu hello za każdym razem, gdy nastąpiła by dostęp do danych z dowolnej wersji. W efekcie systemu zabezpieczeń bardziej niezawodne i niezawodne zmniejszając hello powierzchni systemu zabezpieczeń.

Zabezpieczenia na poziomie wiersza wprowadza kontrola dostępu oparta na predykatu. Elastyczne, scentralizowane, na podstawie predykatu oceny, który można wziąć pod uwagę metadanych lub innych kryteriów, określa administratora hello odpowiednio zawiera funkcje. predykat Hello jest używany jako toodetermine kryterium czy hello użytkownik ma dane toohello odpowiedni dostęp hello na podstawie atrybutów użytkownika. Kontrola dostępu oparta na etykiecie można zaimplementować przy użyciu kontroli dostępu na podstawie predykatu.

## <a name="proactive-monitoring"></a>Aktywne monitorowanie
Baza danych SQL zabezpiecza dane, zapewniając **inspekcji** i **wykrywanie zagrożeń** możliwości.

### <a name="auditing"></a>Inspekcja
SQL Database Auditing zwiększa Twoje możliwości toogain analizę zdarzeń i zmiany w bazie danych hello, w tym aktualizacje i zapytań dotyczących danych hello.

[Usługa Azure SQL Database Auditing](https://docs.microsoft.com/azure/sql-database/sql-database-auditing-get-started) śledzi zdarzenia bazy danych i zapisuje je tooan dziennik inspekcji na koncie magazynu Azure. Inspekcja pomaga zachować zgodność z przepisami, analizować aktywność bazy danych oraz uzyskać wgląd w odchylenia i anomalie, które mogą oznaczać problemy biznesowe lub podejrzane naruszenia zabezpieczeń. Inspekcja umożliwia i ułatwia standardów toocompliance zgodność, ale nie gwarantuje się zgodności.

Inspekcja bazy danych SQL umożliwia:

-   **Zachowaj** dziennik inspekcji wybranych zdarzeń. Można zdefiniować rodzaje toobe działania bazy danych inspekcji.
-   **Raport** na działanie bazy danych. Można użyć wstępnie skonfigurowane raporty i tooget pulpitu nawigacyjnego, szybkie wprowadzenie aktywności i raportowanie zdarzeń.
-   **Analizowanie** raportów. Można znaleźć podejrzane zdarzenia, nietypowe działania i trendów.

Istnieją dwie metody inspekcji:

-   **Inspekcja obiektów blob** -dziennikach tooAzure magazynu obiektów Blob. Jest to metoda inspekcji nowsza, który zapewnia większą wydajność i obsługuje wyższy poziom szczegółowości na poziomie obiektu inspekcji oraz niższy koszt.
-   **Inspekcja tabeli** -dziennikach tooAzure magazynu tabel.

### <a name="threat-detection"></a>Wykrywanie zagrożeń
[Wykrywanie zagrożeń bazy danych SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-threat-detection) wykrycia podejrzanych działań, które wskazują możliwe zagrożenia bezpieczeństwa. Wykrywanie zagrożeń umożliwia toorespond toosuspicious zdarzeń w bazie danych hello, takich jak iniekcji SQL miarę ich występowania. Zawiera alerty i umożliwia wykorzystanie hello Azure SQL Database Auditing tooexplore hello podejrzane zdarzenia.

![Wykrywanie zagrożeń](./media/azure-databse-security-overview/azure-database-fig5.jpg)

Na przykład iniekcja kodu SQL jest jednym z hello typowych problemów sieci Web aplikacji zabezpieczeń na powitania internetowe, aplikacje używane tooattack opartych na danych. Osoby atakujące korzystać z tooinject luk w zabezpieczeniach aplikacji złośliwego instrukcji SQL do pola wejścia aplikacji, mogą spowodować lub modyfikowanie danych w bazie danych hello.

Funkcjonariusze lub innych administratorów wyznaczonych można uzyskać natychmiastowego wysłania powiadomienia o bazy danych podejrzanych działaniach miarę ich występowania. Każde powiadomienie zawiera szczegółowe informacje o podejrzanych działaniach hello i zaleca się, jak toofurther zbadać i uniknięcie hello zagrożenia.        

## <a name="centralized-security-management"></a>Zarządzanie zabezpieczeniami scentralizowane

[Centrum zabezpieczeń Azure](https://azure.microsoft.com/documentation/services/security-center/) pomaga zapobiec, wykrywania i reagowania toothreats. Zapewnia zintegrowane monitorowanie zabezpieczeń i zarządzanie zasadami subskrypcji platformy Azure, pomaga wykrywać zagrożenia, które w przeciwnym razie mogłyby pozostać niezauważone, a także współpracuje z szerokim ekosystemem rozwiązań z zakresu zabezpieczeń.

[Centrum zabezpieczeń](https://docs.microsoft.com/azure/security-center/security-center-sql-database) pomaga chronić dane w bazie danych SQL, zapewniając wgląd w zabezpieczenia hello wszystkich serwerów i baz danych. Centrum zabezpieczeń można:

-   Definiowanie zasad szyfrowania bazy danych SQL i inspekcji.
-   Monitorowanie zabezpieczeń hello zasobów bazy danych SQL za pośrednictwem wszystkich subskrypcji.
-   Szybkie identyfikowanie i Korygowanie problemów z zabezpieczeniami.
-   Integracja alertów z [wykrywanie zagrożeń bazy danych SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-threat-detection).
-   Centrum zabezpieczeń obsługuje dostęp opartej na rolach.

## <a name="azure-marketplace"></a>Azure Marketplace

Hello Azure Marketplace jest online marketplace aplikacji i usług, umożliwiającą rozruchów i niezależnych oprogramowania (ISV) dostawców toooffer klientom rozwiązań tooAzure wokół hello world.
Hello Azure Marketplace łączy ekosystemami partnerów firmy Microsoft Azure w toobetter jednej, ujednoliconej platformy obsługi naszym klientom i partnerom. Kliknij przycisk [tutaj](https://azuremarketplace.microsoft.com/marketplace/apps?search=Database%20Security&page=1) tooglance produkty zabezpieczeń bazy danych dostępne w platformę handlową platformy Azure.

## <a name="next-steps"></a>Następne kroki

- Dowiedz się więcej o [zabezpieczenia bazy danych SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-security-tutorial).
- Dowiedz się więcej o [usługi Centrum zabezpieczeń Azure i usługi Azure SQL Database](https://docs.microsoft.com/azure/security-center/security-center-sql-database).
- Zobacz toolearn więcej informacji na temat wykrywania zagrożeń [wykrywanie zagrożeń bazy danych SQL](https://docs.microsoft.com/azure/sql-database/sql-database-threat-detection).
- toolearn więcej, zobacz [wydajności bazy danych SQL poprawy](https://docs.microsoft.com/azure/sql-database/sql-database-performance-tutorial). 
