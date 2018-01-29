---
title: "Omówienie zabezpieczeń usługi Azure SQL Database | Microsoft Docs"
description: "Więcej informacji na temat zabezpieczeń usługi Azure SQL Database i programu SQL Server, w tym różnice w chmurze i lokalnej instalacji programu SQL Server."
services: sql-database
documentationcenter: 
author: tmullaney
manager: jhubbard
editor: 
ms.assetid: a012bb85-7fb4-4fde-a2fc-cf426c0a56bb
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: On Demand
ms.date: 07/05/2017
ms.author: thmullan;jackr
ms.openlocfilehash: 14a7fdb304e90aec10bee9167817f564870cd6c1
ms.sourcegitcommit: fa28ca091317eba4e55cef17766e72475bdd4c96
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="securing-your-sql-database"></a>Zabezpieczanie bazy danych SQL

W tym artykule przedstawiono podstawowe informacje o zabezpieczeniach warstwy danych aplikacji przy użyciu usługi Azure SQL Database. W szczególności opisano rozpoczęcie pracy z zasobami na potrzeby ochrony danych, kontrolowania dostępu i aktywnego monitorowania. 

Pełne omówienie funkcji zabezpieczeń dostępnych we wszystkich wersjach bazy danych SQL znajduje się w artykule [Security Center for SQL Server Database Engine and Azure SQL Database](https://msdn.microsoft.com/library/bb510589) (Centrum zabezpieczeń dla aparatu bazy danych SQL Server Database i usługi Azure SQL Database). Dodatkowe informacje są także dostępne w artykule [Security and Azure SQL Database technical white paper](https://download.microsoft.com/download/A/C/3/AC305059-2B3F-4B08-9952-34CDCA8115A9/Security_and_Azure_SQL_Database_White_paper.pdf) (Oficjalny dokument dotyczący zabezpieczeń usługi Azure SQL Database) (w formacie PDF).

## <a name="protect-data"></a>Ochrona danych
Usługa SQL Database zabezpiecza dane, szyfrując przesyłane dane za pomocą protokołu [Transport Layer Security](https://support.microsoft.com/kb/3135244), zapisane dane za pomocą funkcji [Transparent Data Encryption](/sql/relational-databases/security/encryption/transparent-data-encryption-azure-sql) oraz używane dane za pomocą funkcji [Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx). 

> [!IMPORTANT]
>Wszystkie połączenia z usługą Azure SQL Database wymagają szyfrowania (SSL/TLS) podczas całego okresu, w którym dane są przesyłane do i z bazy danych. W parametrach połączenia aplikacji, należy określić parametry do szyfrowania połączenia oraz *nie* zaufania certyfikatu serwera (odbywa się automatycznie po skopiowaniu parametrów połączenia z portalu Azure), w przeciwnym razie połączenie nie będzie zweryfikować tożsamość serwera i będzie narażony na ataki "man-in--middle". Na przykład w przypadku sterownika ADO.NET te parametry połączenia mają wartość **Encrypt = True** i **TrustServerCertificate = False**. 

Można również rozważyć inne sposoby szyfrowania danych:

* [Szyfrowanie na poziomie komórki](https://msdn.microsoft.com/library/ms179331.aspx) służące do szyfrowania określonej kolumny lub nawet poszczególnych komórek danych przy użyciu różnych kluczy szyfrowania.
* Jeśli potrzebujesz sprzętowego modułu zabezpieczeń lub centralnego zarządzania hierarchią kluczy szyfrowania, rozważ użycie [funkcji Azure Key Vault w usłudze SQL Server w maszynie wirtualnej Azure](http://blogs.technet.com/b/kv/archive/2015/01/12/using-the-key-vault-for-sql-server-encryption.aspx).

## <a name="control-access"></a>Kontrola dostępu
Usługa SQL Database zabezpiecza dane przez ograniczenie dostępu do bazy danych przy użyciu reguł zapory, mechanizmów uwierzytelniania wymagających od użytkowników potwierdzenia tożsamości oraz funkcji autoryzacji do danych za pośrednictwem członkostw i uprawnień opartych na rolach, a także zabezpieczeń na poziomie wiersza i dynamicznego maskowania danych. Omówienie korzystania z funkcji kontroli dostępu w usłudze SQL Database zawiera artykuł dotyczący [kontroli dostępu](sql-database-control-access.md).

> [!IMPORTANT]
> Zarządzanie bazami danych i serwerami logicznymi na platformie Azure jest kontrolowane przez przypisania do ról konta użytkownika portalu. Aby uzyskać więcej informacji na ten temat, zobacz [kontroli dostępu opartej na rolach w portalu Azure](../active-directory/role-based-access-control-what-is.md).
>

### <a name="firewall-and-firewall-rules"></a>Zapora i reguły zapory
Aby ułatwić ochronę danych, zapora uniemożliwia wszelki dostęp do serwera bazy danych do momentu określenia komputerów, które mają uprawnienia, za pomocą [reguł zapory](sql-database-firewall-configure.md). Zapora udziela dostępu do bazy danych na podstawie źródłowego adresu IP każdego żądania.

### <a name="authentication"></a>Authentication
Uwierzytelnianie w usłudze SQL Database to sposób potwierdzenia tożsamości podczas nawiązywania połączenia z bazą danych. Usługa SQL Database obsługuje dwa typy uwierzytelniania:

* **Uwierzytelnianie usługi SQL**, które używa nazwy użytkownika i hasła. Po utworzeniu serwera logicznego bazy danych należy określić nazwę logowania „server admin” przy użyciu nazwy użytkownika i hasła. Przy użyciu tych poświadczeń można wybrać metodę uwierzytelniania w każdej innej bazie danych na tym serwerze jako jej właściciel, czyli „dbo”. 
* **Uwierzytelnianie usługi Azure Active Directory**, które korzysta z tożsamości zarządzanej przez usługę Azure Active Directory i jest obsługiwane w przypadku zarządzanych i zintegrowanych domen. Używaj uwierzytelniania usługi Active Directory (zabezpieczeń zintegrowanych), [gdy tylko jest to możliwe](https://msdn.microsoft.com/library/ms144284.aspx). Aby skorzystać z uwierzytelniania przy użyciu usługi Azure Active Directory, należy utworzyć innego administratora serwera o nazwie „Azure AD admin”, co umożliwi administrowanie użytkownikami i grupami usługi Azure AD. Ten administrator może również wykonywać wszystkie operacje, które może wykonać zwykły administrator serwera. Zobacz artykuł [Connecting to SQL Database By Using Azure Active Directory Authentication](sql-database-aad-authentication.md) (Łączenie z usługą SQL Database przy użyciu uwierzytelniania usługi Azure Active Directory), aby poznać krok po kroku sposób tworzenia administratora usługi Azure AD w celu włączenia uwierzytelniania usługi Azure Active Directory.

### <a name="authorization"></a>Autoryzacja
Autoryzacja określa, co użytkownik może zrobić w usłudze Azure SQL Database, i jest kontrolowana za pomocą członkostw roli bazy danych konta użytkownika i uprawnień na poziomie obiektu. Zalecanym najlepszym rozwiązaniem jest przyznanie użytkownikom minimalnych niezbędnych uprawnień. Konto administratora serwera, za pomocą którego nawiązujesz połączenie, jest członkiem roli db_owner, która ma uprawnienia do wykonywania wszystkich funkcji w bazie danych. Zapisz to konto, aby móc wdrażać uaktualnienia schematów i wykonywać inne operacje zarządzania. Używaj konta „ApplicationUser” z bardziej ograniczonymi uprawnienia do nawiązywania połączenia pomiędzy swoją aplikacją a bazą danych aplikacji, korzystając z minimalnych uprawnień wymaganych przez aplikację.

### <a name="row-level-security"></a>Zabezpieczenia na poziomie wiersza
Zabezpieczenia na poziomie wiersza umożliwiają klientom kontrolowanie dostępu do wierszy w tabeli bazy danych na podstawie właściwości użytkownika wykonującego zapytanie (np. członkostwa w grupie lub kontekstu wykonania). Aby uzyskać więcej informacji, zobacz [Zabezpieczenia na poziomie wierszy](https://msdn.microsoft.com/library/dn765131).

### <a name="data-masking"></a>Maskowanie danych 
Baza danych SQL dane dynamiczne maskowanie ogranicza ujawnienie danych poufnych przez maskowania go użytkownikom bez uprawnień. Dane dynamiczne maskowanie automatycznie wykryje potencjalnie poufnych danych w bazie danych SQL Azure i udostępnia praktyczne zalecenia do zamaskowania te pola z minimalnym wpływem na warstwie aplikacji. Jego działanie polega na zaciemnianiu poufnych danych w wyznaczonych polach bazy danych w zestawie wyników zapytania, przy czym dane w bazie danych pozostają bez zmian. Aby uzyskać więcej informacji, zobacz [Rozpoczynanie pracy z bazy danych SQL dane dynamiczne maskowanie](sql-database-dynamic-data-masking-get-started.md) można użyć w celu ograniczenia narażenia poufnych danych.

## <a name="proactive-monitoring"></a>Aktywne monitorowanie
Usługa SQL Database zabezpiecza dane, udostępniając możliwości inspekcji i wykrywania zagrożeń. 

### <a name="auditing"></a>Inspekcja
Funkcja inspekcji usługi SQL Database śledzi działania bazy danych i pozwala zachować zgodność z przepisami, rejestrując zdarzenia bazy danych w dzienniku inspekcji na koncie usługi Azure Storage. Inspekcja umożliwia zrozumienie trwających działań bazy danych, a także analizowanie i badanie działań historycznych w celu zidentyfikowania potencjalnych zagrożeń, podejrzanych nadużyć i naruszeń zabezpieczeń. Aby uzyskać więcej informacji, zobacz artykuł z [wprowadzeniem do funkcji inspekcji usługi SQL Database](sql-database-auditing.md).  

### <a name="threat-detection"></a>Wykrywanie zagrożeń
Wykrywanie zagrożeń uzupełnia inspekcji, zapewniając dodatkową warstwę zabezpieczeń analizy wbudowana w usłudze Azure SQL Database, która wykrywa nietypowe i potencjalnie szkodliwe próby dostępu lub wykorzystać baz danych. Użytkownik zostanie wygenerowany alert o podejrzanych działań, potencjalnych luk w zabezpieczeniach i ataki, a także bazy danych nietypowe wzorce dostępu. Można wyświetlić alertów wykrywania zagrożeń z [Centrum zabezpieczeń Azure](https://azure.microsoft.com/services/security-center/) zawierają szczegółowe informacje o podejrzanych działaniach i zalecane działania dotyczące sposobu badania i ograniczyć zagrożenie. Wykrywanie zagrożeń koszty 15 USD/serwer/miesiąc. Będzie ona wolnego przez pierwsze 60 dni. Aby uzyskać więcej informacji, zobacz artykuł [Get started with SQL Database Threat Detection](sql-database-threat-detection.md) (Wprowadzenie do usługi SQL Database Threat Detection).
 
### <a name="data-masking"></a>Maskowanie danych 
Baza danych SQL dane dynamiczne maskowanie ogranicza ujawnienie danych poufnych przez maskowania go użytkownikom bez uprawnień. Dane dynamiczne maskowanie automatycznie wykryje potencjalnie poufnych danych w bazie danych SQL Azure i udostępnia praktyczne zalecenia do zamaskowania te pola z minimalnym wpływem na warstwie aplikacji. Jego działanie polega na zaciemnianiu poufnych danych w wyznaczonych polach bazy danych w zestawie wyników zapytania, przy czym dane w bazie danych pozostają bez zmian. Aby uzyskać więcej informacji, zobacz Rozpoczynanie pracy z [maskowania danych dynamicznych bazy danych SQL](sql-database-dynamic-data-masking-get-started.md)
 
## <a name="compliance"></a>Zgodność
Oprócz powyższych funkcji i funkcji, które ułatwiają także spełnić różne wymagania dotyczące zabezpieczeń, baza danych SQL Azure aplikacji uczestniczy w regularne inspekcje i jest certyfikowany na liczbie standardów zgodności. Aby uzyskać więcej informacji, zobacz witrynę [Centrum zaufania Microsoft Azure](https://azure.microsoft.com/support/trust-center/), w której można znaleźć aktualną listę [certyfikatów zgodności usługi SQL Database](https://azure.microsoft.com/support/trust-center/services/).

## <a name="next-steps"></a>Następne kroki

- Omówienie korzystania z funkcji kontroli dostępu w usłudze SQL Database zawiera artykuł dotyczący [kontroli dostępu](sql-database-control-access.md).
- Aby uzyskać informacje dotyczące inspekcji bazy danych, zobacz [inspekcji bazy danych SQL](sql-database-auditing.md).
- Omówienie wykrywanie zagrożeń, zobacz [wykrywanie zagrożeń bazy danych SQL](sql-database-threat-detection.md).
