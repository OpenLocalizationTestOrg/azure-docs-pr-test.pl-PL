---
title: "aaaAzure Omówienie zabezpieczeń bazy danych SQL | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat zabezpieczeń usługi Azure SQL Database i programu SQL Server, w tym hello różnice między chmurą hello i lokalnej instalacji programu SQL Server po przejściu do tooauthentication, autoryzacji zabezpieczeń połączeń, szyfrowania i zgodności."
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
ms.workload: data-management
ms.date: 07/05/2017
ms.author: thmullan;jackr
ms.openlocfilehash: 7b0b0d1b59ec4018d9fb668bc8b6b56c9907e982
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="securing-your-sql-database"></a>Zabezpieczanie bazy danych SQL

W tym artykule przedstawiono podstawy hello zabezpieczanie hello warstwy danych aplikacji przy użyciu bazy danych SQL Azure. W szczególności opisano rozpoczęcie pracy z zasobami na potrzeby ochrony danych, kontrolowania dostępu i aktywnego monitorowania. 

Aby uzyskać pełny przegląd funkcji zabezpieczeń dostępnych na wszystkich odmian programu SQL Server, zobacz hello [Centrum zabezpieczeń dla aparatu bazy danych programu SQL Server i bazy danych SQL Azure](https://msdn.microsoft.com/library/bb510589). Dodatkowe informacje są także dostępne w hello [zabezpieczeń i baza danych SQL Azure techniczne oficjalny dokument](https://download.microsoft.com/download/A/C/3/AC305059-2B3F-4B08-9952-34CDCA8115A9/Security_and_Azure_SQL_Database_White_paper.pdf) (PDF).

## <a name="protect-data"></a>Ochrona danych
Usługa SQL Database zabezpiecza dane, szyfrując przesyłane dane za pomocą protokołu [Transport Layer Security](https://support.microsoft.com/kb/3135244), zapisane dane za pomocą funkcji [Transparent Data Encryption](http://go.microsoft.com/fwlink/?LinkId=526242) oraz używane dane za pomocą funkcji [Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx). 

> [!IMPORTANT]
>Wszystkie tooAzure połączenia bazy danych SQL wymagają szyfrowania (SSL/TLS) na cały czas podczas tooand "w drodze" z bazy danych hello jest danych. W parametrach połączenia aplikacji, należy określić parametry tooencrypt hello połączenia i *nie* tootrust hello certyfikatu serwera (jest to przypadku należy po skopiowaniu parametrów połączenia z hello klasycznego portalu Azure) w przeciwnym razie połączenie hello nie zweryfikuje hello tożsamości serwera hello i będzie wrażliwych ataki za "man-in--middle". Hello ADO.NET sterownika, na przykład te parametry ciągu połączenia są **Szyfruj = True** i **TrustServerCertificate = False**. 

Dla innych sposobów tooencrypt danych, należy wziąć pod uwagę:

* [Szyfrowanie na poziomie komórki](https://msdn.microsoft.com/library/ms179331.aspx) tooencrypt określone kolumny lub komórki nawet danych z różnymi kluczami szyfrowania.
* Jeśli potrzebujesz sprzętowego modułu zabezpieczeń lub centralnego zarządzania hierarchią kluczy szyfrowania, rozważ użycie [funkcji Azure Key Vault w usłudze SQL Server w maszynie wirtualnej Azure](http://blogs.technet.com/b/kv/archive/2015/01/12/using-the-key-vault-for-sql-server-encryption.aspx).

## <a name="control-access"></a>Kontrola dostępu
Baza danych SQL zabezpiecza dane poprzez ograniczenie przy użyciu reguł zapory, wymagających tooprove użytkowników, tożsamości i autoryzacji toodata za pośrednictwem członkostwa na podstawie ról i uprawnień, a także za pomocą mechanizmów uwierzytelniania tooyour dostępu do bazy danych zabezpieczenia na poziomie wiersza i maskowania danych dynamicznych. Omówienie hello użycie funkcji kontroli dostępu w bazie danych SQL, zobacz [kontroli dostępu](sql-database-control-access.md).

> [!IMPORTANT]
> Zarządzanie bazami danych i serwerami logicznymi na platformie Azure jest kontrolowane przez przypisania do ról konta użytkownika portalu. Aby uzyskać więcej informacji na ten temat, zobacz artykuł [Role-based access control in Azure Portal](../active-directory/role-based-access-control-what-is.md) (Kontrola dostępu oparta na rolach w witrynie Azure Portal).
>

### <a name="firewall-and-firewall-rules"></a>Zapora i reguły zapory
toohelp chronić dane, zapór zapobiec wszystkich serwera bazy danych tooyour dostępu do chwili określenia, które komputery mają uprawnienia za pomocą [reguły zapory](sql-database-firewall-configure.md). Zapora Hello przyznaje toodatabases dostępu oparte na powitania pochodzące z adresu IP dla każdego żądania.

### <a name="authentication"></a>Authentication
Uwierzytelnianie bazy danych SQL odwołuje się toohow potwierdzenia tożsamości, łącząc toohello bazy danych. Usługa SQL Database obsługuje dwa typy uwierzytelniania:

* **Uwierzytelnianie usługi SQL**, które używa nazwy użytkownika i hasła. Po utworzeniu powitania serwera logicznego bazy danych określonego identyfikatora logowania "administratora serwera" przy użyciu nazwy użytkownika i hasła. Przy użyciu tych poświadczeń, można uwierzytelniać tooany baza danych na tym serwerze jako właściciel bazy danych hello lub "właściciela". 
* **Uwierzytelnianie usługi Azure Active Directory**, które korzysta z tożsamości zarządzanej przez usługę Azure Active Directory i jest obsługiwane w przypadku zarządzanych i zintegrowanych domen. Używaj uwierzytelniania usługi Active Directory (zabezpieczeń zintegrowanych), [gdy tylko jest to możliwe](https://msdn.microsoft.com/library/ms144284.aspx). Jeśli chcesz toouse uwierzytelniania usługi Azure Active Directory, należy utworzyć inny administrator serwera o nazwie hello "Administratora usługi Azure AD," zezwala tooadminister usługi Azure AD użytkownicy i grupy. Ten administrator może również wykonywać wszystkie operacje, które może wykonać zwykły administrator serwera. Zobacz [łączenie tooSQL bazy danych przy użyciu usługi Azure uwierzytelnianie usługi Active Directory](sql-database-aad-authentication.md) dla przewodnik toocreate tooenable administratora usługi Azure AD uwierzytelniania usługi Azure Active Directory.

### <a name="authorization"></a>Autoryzacja
Autoryzacji odwołuje się toowhat użytkownika mogą wykonywać w bazie danych SQL Azure, a jest to kontrolowane przez członkostwo roli bazy danych konta użytkownika i na poziomie obiektu uprawnienia. Najlepszym rozwiązaniem należy udzielić hello użytkowników co najmniej niezbędne uprawnienia. konto administratora serwera Hello łączysz się z jest członek roli db_owner, którego urząd toodo żadnych elementów hello bazy danych. Zapisz to konto, aby móc wdrażać uaktualnienia schematów i wykonywać inne operacje zarządzania. Korzystać z bardziej ograniczone uprawnienia tooconnect z bazy danych toohello aplikacji za pomocą hello konta "ApplicationUser" hello najniższych uprawnień wymaganych przez aplikację.

### <a name="row-level-security"></a>Zabezpieczenia na poziomie wiersza
Zabezpieczenia na poziomie wiersza umożliwia klientom toocontrol dostępu toorows w tabeli bazy danych na podstawie charakterystyk hello użytkownika hello wykonywania zapytania (np. grupy członkostwa lub wykonywania context). Aby uzyskać więcej informacji, zobacz [Zabezpieczenia na poziomie wierszy](https://msdn.microsoft.com/library/dn765131).

### <a name="data-masking"></a>Maskowanie danych 
Maskowanie danych dynamicznych bazy danych SQL ogranicza ujawnienie danych poufnych przez maskowania go toonon uprawnieniami użytkowników. Dane dynamiczne maskowanie automatycznie wykryje potencjalnie poufnych danych w bazie danych SQL Azure i zapewnia toomask praktyczne zalecenia te pola z minimalnym wpływem na warstwie aplikacji hello. Działa on za obfuscating hello poufne dane zawarte w hello zestawu wyników zapytania za pośrednictwem pola wyznaczonych bazy danych, gdy hello danych w bazie danych hello nie ulega zmianie. Aby uzyskać więcej informacji, zobacz [Rozpoczynanie pracy z bazy danych SQL dane dynamiczne maskowanie](sql-database-dynamic-data-masking-get-started.md) mogą być używane toolimit ujawnianie danych wrażliwych.

## <a name="proactive-monitoring"></a>Aktywne monitorowanie
Usługa SQL Database zabezpiecza dane, udostępniając możliwości inspekcji i wykrywania zagrożeń. 

### <a name="auditing"></a>Inspekcja
SQL Database Auditing śledzi działania bazy danych i pomaga zgodności z przepisami toomaintain poprzez nagrywanie dziennik inspekcji tooan bazy danych na koncie magazynu Azure. Inspekcji pozwala toounderstand działania trwającą bazy danych, oraz analizowanie i badania potencjalnych zagrożeń tooidentify historyczne działanie lub podejrzane naruszenia nadużycia i zabezpieczeń. Aby uzyskać więcej informacji, zobacz artykuł z [wprowadzeniem do funkcji inspekcji usługi SQL Database](sql-database-auditing.md).  

### <a name="threat-detection"></a>Wykrywanie zagrożeń
Wykrywanie zagrożeń uzupełnia inspekcji, zapewniając dodatkową warstwę zabezpieczeń analizy wbudowane hello usługi baza danych SQL Azure, która wykrywa nietypowe i potencjalnie szkodliwe prób tooaccess lub wykorzystać baz danych. Użytkownik zostanie wygenerowany alert o podejrzanych działań, potencjalnych luk w zabezpieczeniach i ataki, a także bazy danych nietypowe wzorce dostępu. Można wyświetlić alertów wykrywania zagrożeń z [Centrum zabezpieczeń Azure](https://azure.microsoft.com/services/security-center/) zawierają szczegółowe informacje o podejrzanych działaniach i zalecane działania dotyczące tooinvestigate i uniknięcie hello zagrożenia. Wykrywanie zagrożeń koszty 15 USD/serwer/miesiąc. Będzie ona bezpłatnie do hello pierwsze 60 dni. Aby uzyskać więcej informacji, zobacz artykuł [Get started with SQL Database Threat Detection](sql-database-threat-detection.md) (Wprowadzenie do usługi SQL Database Threat Detection).
 
### <a name="data-masking"></a>Maskowanie danych 
Maskowanie danych dynamicznych bazy danych SQL ogranicza ujawnienie danych poufnych przez maskowania go toonon uprawnieniami użytkowników. Dane dynamiczne maskowanie automatycznie wykryje potencjalnie poufnych danych w bazie danych SQL Azure i zapewnia toomask praktyczne zalecenia te pola z minimalnym wpływem na warstwie aplikacji hello. Działa on za obfuscating hello poufne dane zawarte w hello zestawu wyników zapytania za pośrednictwem pola wyznaczonych bazy danych, gdy hello danych w bazie danych hello nie ulega zmianie. Aby uzyskać więcej informacji, zobacz Rozpoczynanie pracy z [maskowania danych dynamicznych bazy danych SQL](sql-database-dynamic-data-masking-get-started.md)
 
## <a name="compliance"></a>Zgodność
Ponadto toohello powyżej funkcje i możliwości, które mogą ułatwić aplikacji także spełnić różne wymagania dotyczące zabezpieczeń, baza danych SQL Azure uczestniczy w regularne inspekcje i jest certyfikowany na liczbie standardów zgodności. Aby uzyskać więcej informacji, zobacz hello [Microsoft Azure Trust Center](https://azure.microsoft.com/support/trust-center/), gdzie można znaleźć hello najbardziej aktualną listę [certyfikaty zgodności bazy danych SQL](https://azure.microsoft.com/support/trust-center/services/).

## <a name="next-steps"></a>Następne kroki

- Omówienie hello użycie funkcji kontroli dostępu w bazie danych SQL, zobacz [kontroli dostępu](sql-database-control-access.md).
- Aby uzyskać informacje dotyczące inspekcji bazy danych, zobacz [inspekcji bazy danych SQL](sql-database-auditing.md).
- Omówienie wykrywanie zagrożeń, zobacz [wykrywanie zagrożeń bazy danych SQL](sql-database-threat-detection.md).
