---
title: aaaSecuring PaaS baz danych Azure | Dokumentacja firmy Microsoft
description: " Więcej informacji na temat zabezpieczeń bazy danych SQL Azure i SQL Data Warehouse najlepsze rozwiązania dotyczące zabezpieczania PaaS w sieci web i aplikacji dla urządzeń przenośnych. "
services: security
documentationcenter: na
author: techlake
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: terrylan
ms.openlocfilehash: a7f9a2846b59dcb05e82f2ad88b41c5213295603
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="securing-paas-databases-in-azure"></a>Zabezpieczanie PaaS baz danych na platformie Azure

W tym artykule omówiono Kolekcja [bazy danych SQL Azure](https://azure.microsoft.com/services/sql-database/) i [SQL Data Warehouse](https://azure.microsoft.com/services/sql-data-warehouse/) najlepsze rozwiązania dotyczące zabezpieczania PaaS w sieci web i aplikacji dla urządzeń przenośnych. Następujące najlepsze rozwiązania są uzyskiwane z wiemy z doświadczenia z platformy Azure i doświadczenia hello klientów, takich jak samodzielnie.

## <a name="azure-sql-database-and-sql-data-warehouse"></a>Baza danych Azure SQL i SQL Data Warehouse
[Baza danych SQL Azure](../sql-database/sql-database-technical-overview.md) i [SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) świadczenia usługi relacyjnej bazy danych dla aplikacji internetowych. Oto usługi pomagające w ochronie danych i aplikacji, podczas korzystania z bazy danych SQL Azure i SQL Data Warehouse w ramach wdrożenia PaaS:

- Uwierzytelnianie usługi Active Directory platformy Azure (zamiast uwierzytelniania programu SQL Server)
- Zapory SQL Azure
- Przezroczystego szyfrowania danych (funkcji TDE)

## <a name="best-practices"></a>Najlepsze praktyki

### <a name="use-a-centralized-identity-repository-for-authentication-and-authorization"></a>Korzystania z repozytorium scentralizowane tożsamości do uwierzytelniania i autoryzacji

Bazy danych SQL Azure może być skonfigurowany toouse, jeden z dwóch typów uwierzytelniania:

- **Uwierzytelnianie SQL** używa nazwy użytkownika i hasła. Po utworzeniu powitania serwera logicznego bazy danych określonego identyfikatora logowania "administratora serwera" przy użyciu nazwy użytkownika i hasła. Przy użyciu tych poświadczeń, można uwierzytelniać tooany baza danych na tym serwerze jako hello właściciela bazy danych.

- **Uwierzytelniania usługi Azure Active Directory** używa tożsamości zarządzanych przez usługę Azure Active Directory i jest obsługiwana w przypadku domen zarządzanych i zintegrowanego. toouse uwierzytelniania usługi Azure Active Directory, należy utworzyć inny administrator serwera o nazwie hello "Administratora usługi Azure AD," zezwala tooadminister usługi Azure AD użytkownicy i grupy. Ten administrator może również wykonywać wszystkie operacje, które może wykonać zwykły administrator serwera.

[Usługa Azure Active Directory authentication](../active-directory/develop/active-directory-authentication-scenarios.md) mechanizm łączący tooAzure bazy danych SQL i usługi SQL Data Warehouse przy użyciu tożsamości w usłudze Azure Active Directory (AD). Usługa Azure AD zapewnia alternatywny tooSQL uwierzytelniania serwera, można zatrzymać rozprzestrzenianie hello tożsamości użytkowników na serwerach bazy danych. Umożliwia uwierzytelniania usługi Azure AD toocentrally można zarządzać tożsamościami hello bazy danych użytkowników i innych usług firmy Microsoft w jednej centralnej lokalizacji. Centralne zarządzanie identyfikator udostępnia jedno miejsce toomanage bazy danych użytkowników i upraszcza zarządzanie uprawnieniami.  

Za pomocą usługi Azure AD authentication zamiast uwierzytelniania SQL zalety:

- Umożliwia obrotu hasła w jednym miejscu.
- Zarządza uprawnień do bazy danych za pomocą zewnętrznej usługi Azure AD grup.
- Eliminuje zapisywania haseł przez włączenie zintegrowanego uwierzytelniania systemu Windows i innych metod uwierzytelniania obsługiwanych przez usługę Azure AD.
- Używa zawarte bazy danych użytkowników tooauthenticate tożsamości na poziomie hello bazy danych.
- Obsługuje uwierzytelnianie na podstawie tokenu dla aplikacji łączenie tooSQL bazy danych.
- Obsługuje uwierzytelnianie macierzysty użytkownika/hasło lub usług AD FS (Federacja domen) dla lokalnej usługi Azure AD bez synchronizacji domeny.
- Obsługuje połączenia z programu SQL Server Management Studio, które używają uniwersalnych uwierzytelnianie usługi Active Directory, która obejmuje [Multi-Factor Authentication (MFA)](../multi-factor-authentication/multi-factor-authentication.md). Silne uwierzytelnianie za pomocą różnych opcji weryfikacji łatwe obejmuje MFA — połączenie telefoniczne, wiadomość tekstowa, karty inteligentne z numeru pin lub powiadomienie aplikacji mobilnej. Aby uzyskać więcej informacji, zobacz [SSMS obsługę usługi Azure AD MFA z bazy danych SQL i usługi SQL Data Warehouse](../sql-database/sql-database-ssms-mfa-authentication.md).

toolearn więcej informacji na temat uwierzytelniania usługi Azure AD, zobacz:

- [Łączenie tooSQL bazy danych lub danych magazynu przez przy użyciu Azure Active Directory uwierzytelniania SQL](../sql-database/sql-database-aad-authentication.md)
- [TooAzure uwierzytelniania SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-authentication.md)
- [Obsługę uwierzytelniania opartego na tokenie dla bazy danych SQL Azure przy użyciu uwierzytelniania usługi Azure AD](https://blogs.msdn.microsoft.com/sqlsecurity/2016/02/09/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth/)

> [!NOTE]
> tooensure, że usługi Azure Active Directory jest odpowiedni dla danego środowiska, zobacz [funkcje usługi Azure AD i ograniczenia](../sql-database/sql-database-aad-authentication.md#azure-ad-features-and-limitations), w szczególności hello dodatkowe zagadnienia.
>
>

### <a name="restrict-access-based-on-ip-address"></a>Ograniczanie dostępu na podstawie adresu IP
Można utworzyć reguły zapory, które określ zakresy adresów IP akceptowane. Reguły te mogą być wskazywane na zarówno hello poziomach serwera i bazy danych. Firma Microsoft zaleca korzystanie z reguł zapory na poziomie bazy danych przy każdym możliwe tooenhance zabezpieczeń i toomake przenośną bazy danych. Reguły zapory poziomu serwera najlepiej nadaje się do administratorów, a jeśli masz wiele baz danych, które mają hello te same wymagania dostępu, ale nie ma czasu toospend indywidualnie skonfigurowanie każdej bazy danych.

Ograniczenia adresu IP źródłowego domyślne SQL Database zezwolić na dostęp z dowolnego adresu Azure (w tym inne subskrypcje i dzierżawców). Można ograniczyć ten tooonly Zezwalaj wystąpienia hello tooaccess adresów IP. Nawet w przypadku zapory SQL i ograniczenia adresu IP są nadal potrzebne silnego uwierzytelniania. Zobacz hello zalecenia w tym artykule.

toolearn więcej informacji na temat zapory SQL Azure i ograniczenia adresów IP, zobacz:

- [Kontrola dostępu do bazy danych SQL Azure](../sql-database/sql-database-control-access.md)
- [Konfigurowanie reguł zapory bazy danych SQL Azure — omówienie](../sql-database/sql-database-firewall-configure.md)
- [Skonfiguruj regułę zapory poziomu serwera bazy danych SQL Azure przy użyciu hello portalu Azure](../sql-database/sql-database-configure-firewall-settings.md)

### <a name="encryption-of-data-at-rest"></a>Szyfrowanie nieużywanych danych
[Funkcji przezroczystego szyfrowania danych (TDE)](https://msdn.microsoft.com/library/azure/bb934049) jest domyślnie włączona. Funkcji TDE szyfruje niewidocznie plików danych i dziennika programu SQL Server, bazy danych SQL Azure i usługi Azure SQL Data Warehouse. Funkcji TDE chroni przed naruszeniem bezpośredni dostęp do plików toohello lub ich kopii zapasowej. Dzięki temu możesz tooencrypt przechowywanych danych bez zmieniania istniejących aplikacji. Funkcji TDE powinien zawsze włączone; jednak nie spowoduje to zatrzymanie atakujący, przy użyciu hello dostęp do ścieżki. Funkcji TDE zapewnia toocomply możliwości hello z wielu ustawowych, wykonawczych i wskazówkami w różnych branżach.

Azure SQL zarządza klucza problemy związane z funkcji TDE. Z funkcji TDE, lokalnie specjalne należy zachować ostrożność tooensure odzyskiwania, gdy przenoszenia baz danych. W bardziej zaawansowanych scenariuszy klucze hello jawnie odbywa się w usłudze Azure Key Vault za pośrednictwem rozszerzonego zarządzania kluczami (zobacz [włączenia funkcji TDE na SQL Server przy użyciu EKM](/security/encryption/enable-tde-on-sql-server-using-ekm)). Umożliwia to także dla Przenieś swój własny klucza (BYOK) za pośrednictwem funkcji BYOK magazynów kluczy Azure.

Azure SQL zapewnia szyfrowanie kolumn za pomocą [zawsze zaszyfrowane](/sql/relational-databases/security/encryption/always-encrypted-database-engine). Dzięki temu dostęp wyłącznie autoryzowanych aplikacji toosensitive kolumn. Za pomocą tego rodzaju szyfrowania ogranicza kwerendy SQL dla zaszyfrowanych kolumn na podstawie tooequality wartości.

Szyfrowanie na poziomie aplikacji, powinien także służyć do wybranych danych. Czasami można zminimalizować problemy suwerenności danych przez szyfrowania danych przy użyciu klucza, który jest przechowywany w hello prawidłowy kraj. Transfer danych nawet przypadkowemu zapobiega przyczyną problemu, ponieważ jest niemożliwe toodecrypt powitalne dane bez klucza hello, zakładając, że algorytm silne są używane (np. AES 256).

Można użyć bazy danych bezpiecznego hello toohelp dodatkowe środki ostrożności, takich jak projektowania bezpieczny system, szyfrowania poufnych zasobów i konfigurowania zapory wokół hello serwerów baz danych.

## <a name="next-steps"></a>Następne kroki
W tym artykule wprowadzono możesz tooa kolekcji bazy danych SQL i usługi SQL Data Warehouse zabezpieczeń najlepsze rozwiązania dotyczące zabezpieczania PaaS w sieci web i aplikacji dla urządzeń przenośnych. toolearn więcej informacji na temat zabezpieczania wdrożeń typu PaaS, zobacz:

- [Zabezpieczanie wdrożeń typu PaaS](security-paas-deployments.md)
- [Zabezpieczanie PaaS w sieci web i aplikacji dla urządzeń przenośnych za pomocą usługi aplikacji Azure](security-paas-applications-using-app-services.md)
