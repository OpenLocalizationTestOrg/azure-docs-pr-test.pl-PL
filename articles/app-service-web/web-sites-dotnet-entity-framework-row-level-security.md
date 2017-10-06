---
title: "Samouczek: Aplikacja sieci Web z wieloma dzierżawcami bazy danych przy użyciu programu Entity Framework i zabezpieczenia na poziomie wiersza"
description: "Dowiedz się, jak toodevelop ASP.NET MVC 5 sieci web aplikacji z wieloma dzierżawcami bazy danych SQL backent, przy użyciu programu Entity Framework i zabezpieczenia na poziomie wiersza."
metakeywords: azure asp.net mvc entity framework multi tenant row level security rls sql database
services: app-service\web
documentationcenter: .net
manager: jeffreyg
author: tmullaney
ms.assetid: 8fdc47a5-6fc3-4d29-ab6a-33e79f50699f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/25/2016
ms.author: thmullan
ms.openlocfilehash: 1b715e01807032c3f6497c374ce427dd762af141
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-web-app-with-a-multi-tenant-database-using-entity-framework-and-row-level-security"></a>Samouczek: Aplikacja sieci Web z wieloma dzierżawcami bazy danych przy użyciu programu Entity Framework i zabezpieczenia na poziomie wiersza
Ten samouczek pokazuje, jak toobuild wielodostępnej sieci web aplikacji za pomocą "[udostępnionej bazy danych, udostępnione schematu](https://msdn.microsoft.com/library/aa479086.aspx)" dzierżawy modelu, używając programu Entity Framework i [zabezpieczenia na poziomie wiersza](https://msdn.microsoft.com/library/dn765131.aspx). W tym modelu pojedynczej bazy danych zawiera dane dla wielu dzierżawców, a każdy wiersz w każdej tabeli jest skojarzony z "Dzierżawy ID." Wiersz poziom zabezpieczeń kontrola dostępu, nowej funkcji bazy danych SQL Azure jest używane tooprevent dzierżawcy dostęp do siebie nawzajem danych. Wymaga to tylko pojedynczą, aplikacje toohello niewielkie zmiany. Scentralizowaniu hello dzierżawy logika dostępu w ramach hello bazy danych zabezpieczenia na poziomie wiersza kodu aplikacji hello upraszcza i zmniejsza ryzyko hello wycieku danych przypadkowemu między dzierżawcami.

Zacznijmy od hello prostą aplikację kontaktów Menedżerze z [tworzenie aplikacji ASP.NET MVP z uwierzytelniania i bazy danych SQL i wdrażanie tooAzure usługi aplikacji](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md). Uprawnienie teraz aplikacji hello umożliwia wszystkich użytkowników (dzierżawcami) toosee wszystkich kontaktów:

![Skontaktuj się z aplikacji Menedżera przed włączeniem zabezpieczenia na poziomie wiersza](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-Before.png)

Z kilku niewielkich zmian dodamy obsługę wielu dzierżawców, tak aby użytkownicy mogli toosee tylko hello kontaktów, do których należą toothem.

## <a name="step-1-add-an-interceptor-class-in-hello-application-tooset-hello-sessioncontext"></a>Krok 1: Dodaj klasę interceptora w hello tooset aplikacji hello SESSION_CONTEXT
Brak jednej zmiany aplikacji potrzebujemy toomake. Ponieważ wszyscy użytkownicy aplikacji łączą się przy użyciu bazy danych toohello hello tych samych parametrach połączenia (tj. tego samego logowania SQL), obecnie nie istnieje sposób dla tooknow zasad Kontrola dostępu użytkownika, który go należy filtrować. Ta metoda jest bardzo często używane w aplikacji sieci web, ponieważ umożliwia ona wydajne buforowania połączeń, ale oznacza to, że potrzebujemy inny sposób tooidentify hello użytkownika bieżącej aplikacji hello bazy danych programu. Witaj rozwiązanie jest zestaw aplikacji hello toohave parę klucz wartość dla hello identyfikator bieżącego użytkownika w hello [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806) natychmiast po otwarciu połączenia, zanim wykonywania kwerendy. SESSION_CONTEXT jest magazyn kluczy i wartości o zakresie sesji, a nasze zasady zabezpieczenia na poziomie wiersza będzie używać hello UserId znajdujące się w niej tooidentify hello bieżącego użytkownika.

Teraz dodamy [interceptora](https://msdn.microsoft.com/data/dn469464.aspx) (w szczególności [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor)), nowej funkcji w ramach jednostki (EF) 6, zestaw tooautomatically hello identyfikator bieżącego użytkownika w hello SESSION_CONTEXT, wykonując Instrukcja T-SQL przy każdym EF otwarciu połączenia.

1. Otwórz projekt ContactManager hello w programie Visual Studio.
2. Kliknij prawym przyciskiem myszy na powitania folderu modeli w hello Eksploratora rozwiązań i wybierz polecenie Dodaj > klasy.
3. Nazwa nowej klasy hello "SessionContextInterceptor.cs", a następnie kliknij przycisk Dodaj.
4. Zamień zawartość hello SessionContextInterceptor.cs hello następującego kodu.

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Data.Common;
using System.Data.Entity;
using System.Data.Entity.Infrastructure.Interception;
using Microsoft.AspNet.Identity;

namespace ContactManager.Models
{
    public class SessionContextInterceptor : IDbConnectionInterceptor
    {
        public void Opened(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
            // Set SESSION_CONTEXT toocurrent UserId whenever EF opens a connection
            try
            {
                var userId = System.Web.HttpContext.Current.User.Identity.GetUserId();
                if (userId != null)
                {
                    DbCommand cmd = connection.CreateCommand();
                    cmd.CommandText = "EXEC sp_set_session_context @key=N'UserId', @value=@UserId";
                    DbParameter param = cmd.CreateParameter();
                    param.ParameterName = "@UserId";
                    param.Value = userId;
                    cmd.Parameters.Add(param);
                    cmd.ExecuteNonQuery();
                }
            }
            catch (System.NullReferenceException)
            {
                // If no user is logged in, leave SESSION_CONTEXT null (all rows will be filtered)
            }
        }

        public void Opening(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void BeganTransaction(DbConnection connection, BeginTransactionInterceptionContext interceptionContext)
        {
        }

        public void BeginningTransaction(DbConnection connection, BeginTransactionInterceptionContext interceptionContext)
        {
        }

        public void Closed(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void Closing(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void ConnectionStringGetting(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void ConnectionStringGot(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void ConnectionStringSet(DbConnection connection, DbConnectionPropertyInterceptionContext<string> interceptionContext)
        {
        }

        public void ConnectionStringSetting(DbConnection connection, DbConnectionPropertyInterceptionContext<string> interceptionContext)
        {
        }

        public void ConnectionTimeoutGetting(DbConnection connection, DbConnectionInterceptionContext<int> interceptionContext)
        {
        }

        public void ConnectionTimeoutGot(DbConnection connection, DbConnectionInterceptionContext<int> interceptionContext)
        {
        }

        public void DataSourceGetting(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void DataSourceGot(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void DatabaseGetting(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void DatabaseGot(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void Disposed(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void Disposing(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void EnlistedTransaction(DbConnection connection, EnlistTransactionInterceptionContext interceptionContext)
        {
        }

        public void EnlistingTransaction(DbConnection connection, EnlistTransactionInterceptionContext interceptionContext)
        {
        }

        public void ServerVersionGetting(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void ServerVersionGot(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void StateGetting(DbConnection connection, DbConnectionInterceptionContext<System.Data.ConnectionState> interceptionContext)
        {
        }

        public void StateGot(DbConnection connection, DbConnectionInterceptionContext<System.Data.ConnectionState> interceptionContext)
        {
        }
    }

    public class SessionContextConfiguration : DbConfiguration
    {
        public SessionContextConfiguration()
        {
            AddInterceptor(new SessionContextInterceptor());
        }
    }
}
```

To jest wymagane zmiany tylko aplikacji hello. Przejdź dalej i tworzenie i publikowanie aplikacji hello.

## <a name="step-2-add-a-userid-column-toohello-database-schema"></a>Krok 2: Dodawanie schematu bazy danych toohello kolumny identyfikatora UserId
Następnie należy tooadd tooassociate kolumny tabeli kontaktów toohello UserId każdego wiersza z użytkownikiem (dzierżawcy). Firma Microsoft zmieni schematu hello bezpośrednio w bazie danych hello, dzięki czemu nie trzeba tooinclude tego pola w modelu danych EF.

Połączenia bazy danych toohello bezpośrednio, za pomocą programu SQL Server Management Studio lub Visual Studio, a następnie wykonaj powitania po T-SQL:

```
ALTER TABLE Contacts ADD UserId nvarchar(128)
    DEFAULT CAST(SESSION_CONTEXT(N'UserId') AS nvarchar(128))
```

Spowoduje to dodanie tabeli kontaktów toohello kolumny identyfikatora użytkownika. Używamy hello nvarchar(128) danych typu toomatch powitalne UserId przechowywane w tabeli AspNetUsers hello i utworzymy ograniczenie domyślne, które automatycznie ustawi hello UserId dla nowo wstawionych wierszy toobe hello UserId przechowywanych obecnie we SESSION_CONTEXT.

Teraz tabeli hello wygląda następująco:

![Tabela kontaktów programu SSMS](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-Contacts.png)

Podczas tworzenia nowych kontaktów, automatycznie zostaną przydzieleni hello Popraw identyfikator użytkownika. Dla celów demonstracyjnych jednak teraz przypisać niektóre z tych istniejących tooan kontaktów istniejącego użytkownika.

Jeśli w aplikacji hello już zostały utworzone w przypadku kilku użytkowników (np. przy użyciu lokalnego, Google lub usługi Facebook kont), będą widoczne w tabeli AspNetUsers hello. W poniższym zrzucie ekranu hello jest tylko jeden użytkownik wykonanej do tej pory.

![Tabela SSMS AspNetUsers](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-AspNetUsers.png)

Kopiuj hello identyfikator dla user1@contoso.comi wklej go do instrukcji hello T-SQL poniżej. Wykonanie tej instrukcji tooassociate trzech hello kontaktów z tego identyfikatora użytkownika.

```
UPDATE Contacts SET UserId = '19bc9b0d-28dd-4510-bd5e-d6b6d445f511'
WHERE ContactId IN (1, 2, 5)
```

## <a name="step-3-create-a-row-level-security-policy-in-hello-database"></a>Krok 3: Tworzenie zasad zabezpieczeń na poziomie wiersza w bazie danych hello
Ostatnim krokiem Hello jest toocreate zasady zabezpieczeń, które używa hello UserId w SESSION_CONTEXT tooautomatically filtru hello wyników zwróconych w wyniku zapytania.

Podczas toohello nadal połączenia bazy danych wykonaj powitania po T-SQL:

```
CREATE SCHEMA Security
go

CREATE FUNCTION Security.userAccessPredicate(@UserId nvarchar(128))
    RETURNS TABLE
    WITH SCHEMABINDING
AS
    RETURN SELECT 1 AS accessResult
    WHERE @UserId = CAST(SESSION_CONTEXT(N'UserId') AS nvarchar(128))
go

CREATE SECURITY POLICY Security.userSecurityPolicy
    ADD FILTER PREDICATE Security.userAccessPredicate(UserId) ON dbo.Contacts,
    ADD BLOCK PREDICATE Security.userAccessPredicate(UserId) ON dbo.Contacts
go

```

Ten kod wykonuje trzy czynności. Najpierw tworzy nowego schematu, najlepszym rozwiązaniem dla scentralizowany i ograniczenie dostępu toohello zabezpieczenia na poziomie wiersza obiektów. Następnie tworzy predykatu funkcję, która zwróci "1", gdy hello UserId w SESSION_CONTEXT jest zgodna z hello UserId wiersza. Na koniec tworzy zasady zabezpieczeń, które dodaje tej funkcji jako predykatu filtru i blok w tabeli kontaktów hello. Predykat filtru Hello powoduje tooreturn zapytania tylko wiersze, które należy toohello bieżącego użytkownika, a predykat bloku hello działa jako aplikacja hello tooprevent zabezpieczenie z kiedykolwiek przypadkowo wstawiania wiersza dla użytkownika niewłaściwy hello.

Teraz uruchom aplikację hello i zaloguj się jako user1@contoso.com. Ten użytkownik widzi teraz tylko kontakty hello możemy przypisane toothis UserId wcześniej:

![Skontaktuj się z aplikacji Menedżera przed włączeniem zabezpieczenia na poziomie wiersza](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-After.png)

toovalidate to dodatkowe, spróbuj zarejestrować nowego użytkownika. Nie będzie widocznej żadne kontakty, ponieważ żaden z przypisanym toothem. Jeśli tworzenia nowego kontaktu, zostanie do niej przypisany toothem i tylko będą oni mogli toosee go.

## <a name="next-steps"></a>Następne kroki
Gotowe. Hello prostej aplikacji sieci web skontaktuj się z Menedżera został przekonwertowany na wielodostępnej jedną której każdy użytkownik ma własną listy kontaktów. Przy użyciu zabezpieczeń na poziomie wiersza, firma Microsoft już unikać złożoność hello wymuszania logika dostępu dzierżawcy w naszym kodzie aplikacji. Przezroczystość ten umożliwia toofocus aplikacji hello na problem biznesowy rzeczywistych hello wykonywanego i również zmniejsza ryzyko przypadkowego wyciekowi danych jako ścieżce bazowej kodu aplikacji hello hello rozwoju.

Ten samouczek ma tylko zadrapany hello powierzchnię możliwości odświeżania. Na przykład jest możliwe toohave dokładniejsze lub logikę szczegółowego dostępu i jego możliwych toostore więcej niż tylko hello identyfikator bieżącego użytkownika w hello SESSION_CONTEXT. Możliwe jest również zbyt[zintegrować zabezpieczenia na poziomie wiersza z bibliotek klienta narzędzi elastycznej bazy danych hello](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md) toosupport odłamków wielodostępne w warstwie danych.

Poza tych możliwości również pracujemy toomake jeszcze bardziej poprawić jakość kontrola dostępu. Jeśli masz pytania, pomysłów lub rzeczy, które chcesz toosee, prosimy o kontakt w komentarzach hello. Cenimy Twoją opinię!

