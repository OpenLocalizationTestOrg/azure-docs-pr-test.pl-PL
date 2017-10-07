---
title: "najlepsze rozwiązania zabezpieczeń bazy danych aaaAzure | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera zestaw najlepsze rozwiązania dotyczące zabezpieczeń bazy danych platformy Azure."
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/21/2017
ms.author: tomsh
ms.openlocfilehash: 78984291e8f74879c7f738e2ce3176c4be18d154
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-security-best-practices"></a>Najlepsze rozwiązania Azure bazy danych

Zabezpieczeń jest szczególnie ważne w przypadku zarządzania bazami danych i zawsze było priorytet bazy danych SQL Azure. Baz danych może być ściśle zabezpieczonych toohelp spełniają najbardziej przepisami lub wymaganiami zabezpieczeń, w tym HIPAA, ISO 27001/27002 i PCI DSS poziom 1, między innymi. Bieżącą listę certyfikaty zgodności zabezpieczeń znajduje się w temacie hello [witryny Microsoft Trust Center](http://azure.microsoft.com/support/trust-center/services/). Możesz również wybrać tooplace baz danych w określonych centrach danych platformy Azure na podstawie przepisów wymagań.

W tym artykule omówiono kolekcja najlepszych rozwiązań dotyczących zabezpieczeń bazy danych platformy Azure. Następujące najlepsze rozwiązania są uzyskiwane z wiemy z doświadczenia z zabezpieczeń bazy danych platformy Azure i doświadczenia hello klientów, takich jak samodzielnie.

Dla każdego najlepszym rozwiązaniem prezentujemy zasady:

-   Jakie hello najlepszym rozwiązaniem jest
-   Dlaczego chcesz tooenable tej najlepsze praktyki
-   Co może wynikać hello tooenable hello najlepszym rozwiązaniem w przeciwnym przypadku
-   Jak można znaleźć tooenable hello najlepsze praktyki

W tym artykule najlepsze rozwiązania zabezpieczeń bazy danych Azure na podstawie opinii konsensu i funkcji platformy Azure i funkcja ustawia istniejących w chwili hello, który został zapisany w tym artykule. Opinie i technologie ulegną zmianom i będą w tym artykule zaktualizowane na tooreflect regularnie tych zmian.

Bazy danych platformy Azure najlepsze rozwiązania omówione w tym artykule obejmują:

-   Użyj dostępu bazy danych toorestrict reguły zapory
-   Włącz uwierzytelnianie bazy danych
-   Ochrona danych przy użyciu szyfrowania
-   Ochrona danych podczas przesyłania
-   Włączanie inspekcji bazy danych
-   Włączyć wykrywanie zagrożeń bazy danych


## <a name="use-firewall-rules-toorestrict-database-access"></a>Użyj dostępu bazy danych toorestrict reguły zapory

Usługa Microsoft Azure SQL Database udostępnia usługę relacyjnej bazy danych dla platformy Azure i innych aplikacji internetowych. zabezpieczenia dostępu tooprovide, baza danych SQL kontroluje dostęp przy użyciu reguł zapory ograniczenie łączności za pomocą adresu IP mechanizmów uwierzytelniania wymagające tooprove użytkowników tożsamości i ograniczanie użytkowników toospecific akcji i dane mechanizmów autoryzacji. Zapory uniemożliwiają wszystkich serwera bazy danych tooyour dostępu do chwili określenia komputery, które ma uprawnienia. Zapora Hello przyznaje toodatabases dostępu oparte na powitania pochodzące z adresu IP dla każdego żądania.

![Reguły zapory](./media/azure-database-security-best-practices/azure-database-security-best-practices-Fig1.png)

Witaj usługi baza danych SQL Azure jest dostępna tylko za pośrednictwem portu TCP 1433. tooaccess bazy danych SQL z komputera, sprawdź, czy zapory komputera klienta pozwalają wychodzących komunikacji TCP na porcie TCP 1433. Jeśli nie jest to wymagane przez inne aplikacje, należy go zablokować połączenia przychodzące na porcie TCP 1433 przy użyciu reguł zapory.

W trakcie procesu połączenia hello połączenia z maszyn wirtualnych platformy Azure są tooa przekierowane na inny adres IP i port unikatowa dla każdej roli procesu roboczego. numer portu Hello jest poza zakresem powitania od 11000 too11999. Aby uzyskać więcej informacji na temat portów TCP, zobacz [porty inne niż 1433 ADO.NET 4.5 i SQL Database2](https://docs.microsoft.com/azure/sql-database/sql-database-develop-direct-route-ports-adonet-v12).

> [!Note]
> Aby uzyskać więcej informacji na temat reguł zapory w usłudze SQL Database, zobacz [Omówienie reguł zapory usługi SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure).

## <a name="enable-database-authentication"></a>Włącz uwierzytelnianie bazy danych
Baza danych SQL obsługuje dwa typy uwierzytelniania, uwierzytelnianie SQL i Azure uwierzytelnianie usługi Active Directory (Azure AD Authentication).

**Uwierzytelnianie SQL** jest zalecane w następujących przypadkach:

-   Dzięki temu środowiskach toosupport SQL Azure przy użyciu mieszane systemy operacyjne, gdzie wszyscy użytkownicy nie są uwierzytelniane przez domeny systemu Windows.
-   Umożliwia starsze aplikacje toosupport SQL Azure i aplikacji dostarczanych przez osoby trzecie, które wymagają uwierzytelniania programu SQL Server.
-   Umożliwia użytkownikom tooconnect z nieznanej lub niezaufanej domeny. Na przykład aplikacji, których klienci ustalonych nawiązuje połączenie z przypisywany logowania do programu SQL Server tooreceive hello ich zleceń.
-   Umożliwia toosupport SQL Azure aplikacje sieci Web gdzie użytkownicy tworzyć własne tożsamości.
-   Umożliwia deweloperom toodistribute na podstawie swoich aplikacji przy użyciu uprawnień złożonych hierarchii znane, ustawienia wstępnego logowania do programu SQL Server.

> [!Note]
> Jednak uwierzytelnianie programu SQL Server nie może używać protokołu zabezpieczeń protokołu Kerberos.

Jeśli używasz **uwierzytelniania SQL** należy:

-   Zarządzanie hello silnych poświadczeń użytkownika.
-   Ochrona poświadczeń hello w parametrach połączenia hello.
-   (Potencjalnie) chronić hello poświadczenia przekazywane za pośrednictwem sieci hello z hello Web server toohello w bazie danych. Aby uzyskać więcej informacji, zobacz [porady: łączenie tooSQL serwera przy użyciu uwierzytelniania SQL w programie ASP.NET 2.0](https://msdn.microsoft.com/library/ms998300.aspx).

**Usługa Azure Active Directory authentication** mechanizm łączący tooMicrosoft bazy danych SQL Azure i [SQL Data Warehouse](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-overview-what-is) przy użyciu tożsamości w usłudze Azure Active Directory (Azure AD). Przy użyciu uwierzytelniania usługi Azure AD mogą centralnie zarządzać hello tożsamości użytkowników bazy danych i innych usług firmy Microsoft w jednej centralnej lokalizacji. Centralne zarządzanie identyfikator udostępnia jedno miejsce toomanage bazy danych użytkowników i upraszcza zarządzanie uprawnieniami. Witaj następujące korzyści:

-   Zapewnia alternatywny tooSQL uwierzytelniania serwera.
-   Pomaga zatrzymać rozprzestrzenianie hello tożsamości użytkowników na serwerach bazy danych.
-   Umożliwia obrotu hasła w jednym miejscu.
-   Klientów można zarządzać za pomocą zewnętrznego grup (AAD) uprawnień do bazy danych.
-   Można go wyeliminować zapisywania haseł przez włączenie zintegrowanego uwierzytelniania systemu Windows i innych metod uwierzytelniania obsługiwanych przez usługę Azure Active Directory.
-   Azure AD uwierzytelniania przy użyciu tożsamości tooauthenticate użytkowników zawartej bazy danych na poziomie bazy danych hello.
-   Usługi Azure AD obsługuje uwierzytelnianie na podstawie tokenu łączenie tooSQL bazy danych aplikacji.
-   Usługa Azure AD authentication obsługuje usług AD FS (Federacja domen) lub native użytkownika i hasło uwierzytelniania lokalnej usługi Azure Active Directory bez synchronizacji domeny.
-   Usługi Azure AD obsługuje połączenia z programu SQL Server Management Studio, które używają uniwersalnych uwierzytelnianie usługi Active Directory, która obejmuje usługi Multi-Factor Authentication (MFA). Silne uwierzytelnianie za pomocą różnych opcji weryfikacji łatwe obejmuje MFA — połączenie telefoniczne, wiadomość tekstowa, karty inteligentne z numeru pin lub powiadomienie aplikacji mobilnej. Aby uzyskać więcej informacji, zobacz [SSMS obsługę usługi Azure AD MFA z bazy danych SQL i usługi SQL Data Warehouse](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication).

kroki konfiguracji Hello obejmują następujące procedury tooconfigure hello i korzystać z uwierzytelniania usługi Azure Active Directory.

-   Utworzyć i wypełnić usługi Azure AD.
-   Opcjonalnie: Skojarz lub zmiany usługi active directory hello aktualnie skojarzony z subskrypcją platformy Azure.
-   Tworzenie administratora usługi Azure Active Directory dla serwera Azure SQL lub [magazyn danych SQL Azure](https://azure.microsoft.com/services/sql-data-warehouse/).
- Konfigurowanie komputerów klienckich.
-   Utwórz użytkowników zawartej bazy danych programu tooAzure zamapować bazy danych tożsamości usługi AD.
-   Łączenie tooyour bazy danych przy użyciu tożsamości usługi Azure AD.

Informacje szczegółowe informacje można znaleźć [tutaj](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).

## <a name="protect-your-data-using-encryption"></a>Ochrona danych przy użyciu szyfrowania

[Azure SQL Database przezroczystego szyfrowania danych (funkcji TDE)](https://msdn.microsoft.com/library/dn948096.aspx) pomaga chronić przed zagrożeniem hello złośliwych działań, wykonując w czasie rzeczywistym szyfrowania i odszyfrowywania hello bazy danych, skojarzonych kopii zapasowych, i pliki dziennika transakcji w stanie spoczynku bez Aplikacja toohello wymagające zmiany. Funkcji TDE szyfruje magazyn hello całej bazy danych przy użyciu klucza szyfrowania symetrycznego klucza o nazwie hello bazy danych.

Nawet wtedy, gdy cały magazyn hello jest zaszyfrowany, bardzo ważne jest tooalso szyfrowania bazy danych sam. Jest to implementacja obrony hello w głębokość podejście do ochrony danych. Jeśli używasz bazy danych SQL Azure i mają tooprotect poufnych danych, takich jak kart kredytowych lub numerów ubezpieczenia społecznego, można zaszyfrować baz danych z szyfrowania AES 256-bitową 140-2 zweryfikowane FIPS, który spełnia wymagania hello wiele standardy branżowe (np. HIPAA, PCI).

Koniecznie toounderstand, które pliki związane z zbyt[(BPE). rozszerzenie puli bufora](https://docs.microsoft.com/sql/database-engine/configure-windows/buffer-pool-extension) nie są szyfrowane, gdy baza danych jest szyfrowana przy użyciu funkcji TDE. Należy użyć narzędzia szyfrowania na poziomie systemu plików, takich jak [funkcji BitLocker](https://technet.microsoft.com/library/cc732774) lub hello [system szyfrowania plików (EFS)](https://technet.microsoft.com/library/cc700811.aspx) dla BPE powiązane pliki.

Od autoryzowanym użytkownikiem, takie jak administrator zabezpieczeń lub administrator bazy danych można uzyskiwać dostęp do danych hello nawet jeśli hello bazy danych jest szyfrowany przy funkcji TDE, należy również wykonać poniższe zalecenia hello:

-   Włącz uwierzytelnianie SQL na poziomie hello bazy danych.
-   Użyj usługi Azure AD uwierzytelnianie przy użyciu [role RBAC](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is).
-   Użytkownicy i aplikacje powinny używać tooauthenticate osobnych kont. W ten sposób można ograniczyć uprawnienia hello toousers i aplikacje i zmniejszenia ryzyka hello złośliwych działań.
-   Implementowanie zabezpieczeń na poziomie bazy danych przy użyciu ról stałej bazy danych (takich jak db_datareader lub db_datawriter), lub można utworzyć role niestandardowe dla twojej aplikacji toogrant obiektów bazy danych tooselected jawne uprawnienia.

Dla innych sposobów tooencrypt danych, należy wziąć pod uwagę:

-   [Szyfrowanie na poziomie komórki](https://msdn.microsoft.com/library/ms179331.aspx) tooencrypt określone kolumny lub komórki nawet danych z różnymi kluczami szyfrowania.
-   Szyfrowania używany przy użyciu zawsze zaszyfrowane: [zawsze zaszyfrowane](https://msdn.microsoft.com/library/mt163865.aspx) umożliwia klientom tooencrypt poufnych danych w aplikacjach klienckich i nigdy nie ujawniaj informacji o toohello klucze szyfrowania hello aparatu bazy danych (bazy danych SQL lub SQL Server). W związku z tym zawsze zaszyfrowane zapewnia oddzielenie tych, którzy własnych danych hello (i można go wyświetlić) oraz tych, którzy zarządzają danymi hello (ale powinien nie mają dostępu).
-   Przy użyciu zabezpieczeń na poziomie wiersza: zabezpieczenia na poziomie wiersza umożliwia klientom toocontrol dostępu toorows w tabeli bazy danych na podstawie charakterystyk hello użytkownika hello wykonywania zapytania (np. grupy członkostwa lub wykonywania context). Aby uzyskać więcej informacji, zobacz [Zabezpieczenia na poziomie wierszy](https://msdn.microsoft.com/library/dn765131).

## <a name="protect-data-in-transit"></a>Ochrona danych podczas przesyłania
Ochrona danych podczas przesyłania powinien być integralną część strategii ochrony danych. Ponieważ dane będą przenoszone i z powrotem w wielu lokalizacjach, ogólne zalecenie hello jest zawsze używaj danych tooexchange protokołów SSL/TLS w różnych lokalizacjach. W niektórych sytuacjach może być tooisolate hello całej komunikacji kanału między lokalnymi i w chmurze infrastruktury przy użyciu wirtualnej sieci prywatnej (VPN).

Przenoszenie między lokalną infrastrukturą i Azure danych należy rozważyć odpowiednie zabezpieczenia, takie jak HTTPS lub sieci VPN.

Dla organizacji, które wymagają dostępu toosecure z wielu stacjach roboczych znajdujących się lokalnie tooAzure, użyj [Azure VPN lokacja lokacja](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-site-to-site-create).

W przypadku organizacji, które wymagają toosecure dostęp z poszczególnych stacji roboczych lokalnymi lub tooAzure poza firmą, rozważ użycie [punkt-lokacja sieci VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-point-to-site-create).

Większych zestawów danych można przenieść za pośrednictwem dedykowanej o dużej szybkości łącza sieci WAN takich jak [ExpressRoute](https://azure.microsoft.com/services/expressroute/). Jeśli wybierzesz toouse ExpressRoute, można również szyfrowanie danych hello przy użyciu poziomu aplikacji hello [SSL/TLS](https://support.microsoft.com/kb/257591) lub innymi protokołami zapewnia dodatkową ochronę.

Jeśli użytkownik korzysta z usługi Azure Storage za pomocą portalu Azure hello, wszystkich transakcji jest realizowana za pośrednictwem protokołu HTTPS. [Interfejs API REST magazynu](https://msdn.microsoft.com/library/azure/dd179355.aspx) za pośrednictwem protokołu HTTPS może być również używane toointeract z [usługi Azure Storage](https://azure.microsoft.com/services/storage/) i [bazy danych SQL Azure](https://azure.microsoft.com/services/sql-database/).

Organizacje, które nie są przesyłane dane tooprotect są bardziej narażony na [ataków man-in--middle](https://technet.microsoft.com/library/gg195821.aspx), [podsłuchiwaniu](https://technet.microsoft.com/library/gg195641.aspx) i przejęcie kontroli sesji. Tego rodzaju ataki może być pierwszym krokiem hello w uzyskiwaniu dostępu do danych tooconfidential.

więcej informacji na temat opcji sieci VPN platformy Azure, przeczytaj artykuł hello toolearn [planowania i projektowania dla bramy sieci VPN](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-plan-design).

## <a name="enable-database-auditing"></a>Włączanie inspekcji bazy danych
Inspekcja wystąpienia hello aparatu bazy danych programu SQL Server lub jedna baza danych obejmuje śledzenie i rejestrowanie zdarzeń dotyczących hello aparatu bazy danych. SQL Server audit umożliwia tworzenie inspekcji serwera, które może zawierać specyfikacji inspekcji serwera dla zdarzenia na poziomie serwera i specyfikacji inspekcji bazy danych dla zdarzenia na poziomie bazy danych. Dzienniki zdarzeń toohello lub tooaudit plików można pisać zdarzeń inspekcji.

Istnieje kilka poziomów inspekcji dla programu SQL Server, w zależności od rząd lub standardów wymagań instalacyjnych. SQL Server Audit oferuje narzędzia hello i procesy musi mieć tooenable, magazynu i widoku inspekcji, które znajdują się na różnych obiektów serwera i bazy danych.

[Usługa Azure SQL Database Auditing](https://docs.microsoft.com/azure/sql-database/sql-database-auditing) śledzi zdarzenia bazy danych i zapisuje je tooan dziennik inspekcji na koncie magazynu Azure.

Inspekcja pomaga zachować zgodność z przepisami, analizować aktywność bazy danych oraz uzyskać wgląd w odchylenia i anomalie, które mogą oznaczać problemy biznesowe lub podejrzane naruszenia zabezpieczeń.

Inspekcja umożliwia i ułatwia standardów toocompliance zgodność, ale nie gwarantuje się zgodności.

więcej informacji na temat inspekcji bazy danych toolearn i jak tooenable, przeczytaj artykuł hello [włączyć inspekcję i wykrywania zagrożeń na serwerach SQL w Centrum zabezpieczeń Azure](https://docs.microsoft.com/azure/security-center/security-center-enable-auditing-on-sql-servers).

## <a name="enable-database-threat-detection"></a>Włączyć wykrywanie zagrożeń bazy danych
Wykrywanie zagrożeń SQL pozwala toodetect i Odpowiedz toopotential zagrożeń w miarę ich występowania, zapewniając alerty zabezpieczeń w nietypowych działań. Zostanie wyświetlony alert po bazy danych podejrzanych działań, potencjalnych luk i ataki, a także bazy danych nietypowe wzorce dostępu. Wykrywanie zagrożeń SQL alerty zawierają szczegółowe informacje o podejrzanych działaniach i zalecane działania dotyczące tooinvestigate i uniknięcie hello zagrożenia.

Na przykład iniekcja kodu SQL jest jednym z hello typowych problemów sieci Web aplikacji zabezpieczeń na powitania internetowe, aplikacje używane tooattack opartych na danych. Osoby atakujące korzystać z tooinject luk w zabezpieczeniach aplikacji złośliwego instrukcji SQL do pola wejścia aplikacji, mogą spowodować lub modyfikowanie danych w bazie danych hello.

toolearn temat tooset się wykrywanie zagrożeń dla bazy danych w hello Azure portalu, zobacz temat [wykrywanie zagrożeń bazy danych SQL](https://docs.microsoft.com/azure/sql-database/sql-database-threat-detection).

Ponadto wykrywanie zagrożeń SQL integruje alerty z [Centrum zabezpieczeń Azure](https://azure.microsoft.com/services/security-center/). Zachęcamy tootry go przez 60 dni do zwolnienia.

więcej informacji na temat wykrywania zagrożeń bazy danych toolearn i jak tooenable, przeczytaj artykuł hello [włączyć inspekcję i wykrywania zagrożeń na serwerach SQL w Centrum zabezpieczeń Azure](https://docs.microsoft.com/azure/security-center/security-center-enable-auditing-on-sql-servers).

## <a name="conclusion"></a>Podsumowanie
Bazy danych platformy Azure to platforma niezawodne bazy danych, z pełnym zakresem funkcji zabezpieczeń, które spełniają wymagania organizacyjne i przepisami zgodności wiele. Można chronić dane kontrolowanie hello dostęp fizyczny tooyour danych, a za pomocą różnych opcji zabezpieczeń danych na powitania pliku, kolumny lub poziom wiersza niewidocznego szyfrowania danych, szyfrowanie na poziomie komórki lub zabezpieczenia na poziomie wiersza. Zawsze zaszyfrowane umożliwia również operacji względem zaszyfrowane dane, co upraszcza proces aktualizacji aplikacji hello. Z kolei dostępu tooauditing Dzienniki aktywności bazy danych SQL pozwala hello potrzebne informacje, dzięki czemu tooknow, jak i kiedy jest uzyskiwany dostęp do danych.

## <a name="next-steps"></a>Następne kroki
- toolearn więcej informacji na temat reguł zapory, zobacz [reguły zapory](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure).
- toolearn o użytkownikach i logowania, zobacz [Zarządzanie logowania](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins).
- Samouczek, zobacz [zabezpieczenia bazy danych SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-security-tutorial).
