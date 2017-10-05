---
title: "Samouczek: Aplikacja sieci Web z wieloma dzierżawcami bazy danych przy użyciu programu Entity Framework i zabezpieczenia na poziomie wiersza"
description: "Dowiedz się, jak wdrażać aplikacji sieci web platformy ASP.NET MVC 5 z wieloma dzierżawcami bazy danych SQL backent, przy użyciu programu Entity Framework i zabezpieczenia na poziomie wiersza."
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
ms.openlocfilehash: ba1bb3d84b462dfebbb2564569517d7336bf54fd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-web-app-with-a-multi-tenant-database-using-entity-framework-and-row-level-security"></a>Samouczek: Aplikacja sieci Web z wieloma dzierżawcami bazy danych przy użyciu programu Entity Framework i zabezpieczenia na poziomie wiersza
W tym samouczku pokazano, jak tworzenie aplikacji sieci web z wieloma dzierżawcami z "[udostępnionej bazy danych, udostępnione schematu](https://msdn.microsoft.com/library/aa479086.aspx)" dzierżawy modelu, używając programu Entity Framework i [zabezpieczenia na poziomie wiersza](https://msdn.microsoft.com/library/dn765131.aspx). W tym modelu pojedynczej bazy danych zawiera dane dla wielu dzierżawców, a każdy wiersz w każdej tabeli jest skojarzony z "Dzierżawy ID." Wiersz poziom zabezpieczeń kontrola dostępu, nowej funkcji bazy danych SQL Azure jest używana do uniemożliwić dostęp do siebie nawzajem danych dzierżawcy. Wymaga tylko jednego, niewielkie zmiany w aplikacji. Centralizując logika dostępu dzierżawcy w bazie danych sam zabezpieczenia na poziomie wiersza upraszcza kod aplikacji i zmniejsza zagrożenie wyciekiem danych przypadkowemu między dzierżawcami.

Zacznijmy od prostej aplikacji menedżera kontaktu z [tworzenie aplikacji ASP.NET MVP z uwierzytelniania i bazy danych SQL i wdrożyć w usłudze Azure App Service](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md). Prawo teraz aplikacji zezwala wszystkim użytkownikom (dzierżawcami), aby wyświetlić wszystkie kontakty:

![Skontaktuj się z aplikacji Menedżera przed włączeniem zabezpieczenia na poziomie wiersza](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-Before.png)

Z kilku niewielkich zmian dodamy obsługę wielu dzierżawców, tak aby użytkownicy mogli zobaczyć kontaktów, które należą do nich.

## <a name="step-1-add-an-interceptor-class-in-the-application-to-set-the-sessioncontext"></a>Krok 1: Dodaj klasę interceptora w aplikacji, aby ustawić SESSION_CONTEXT
Brak jednej zmiany w aplikacji, które musimy upewnić. Wszyscy użytkownicy aplikacji łączyć się z bazą danych przy użyciu tych samych parametrach połączenia (tj. tego samego logowania SQL), dlatego nie istnieje obecnie sposób zasady zabezpieczenia na poziomie wiersza wiedzieć, który użytkownik powinien Filtruj. Ta metoda jest bardzo często używane w aplikacji sieci web, ponieważ umożliwia ona wydajne buforowania połączeń, ale oznacza to, że potrzebujemy inny sposób identyfikowania użytkownika bieżącej aplikacji w bazie danych. Rozwiązanie to ma zestaw par klucz wartość dla bieżącego identyfikatora użytkownika w aplikacji [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806) natychmiast po otwarciu połączenia, zanim wykonywania kwerendy. SESSION_CONTEXT jest magazyn kluczy i wartości o zakresie sesji, a nasze zasady zabezpieczenia na poziomie wiersza będzie używać UserId znajdujące się w niej do identyfikowania bieżącego użytkownika.

Dodamy [interceptora](https://msdn.microsoft.com/data/dn469464.aspx) (w szczególności [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor)), nowej funkcji w ramach jednostki (EF) 6, do automatycznego ustalania bieżącego identyfikatora użytkownika w SESSION_CONTEXT, wykonując instrukcję T-SQL przy każdym EF otwarciu połączenia.

1. Otwórz projekt ContactManager w programie Visual Studio.
2. Kliknij prawym przyciskiem folder modeli w Eksploratorze rozwiązań i wybierz polecenie Dodaj > klasy.
3. Nazwa nowej klasy "SessionContextInterceptor.cs", a następnie kliknij przycisk Dodaj.
4. Zastąp zawartość SessionContextInterceptor.cs z następującym kodem.

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
            // Set SESSION_CONTEXT to current UserId whenever EF opens a connection
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

To jest wymagana zmiana tylko aplikacji. Przejdź dalej i tworzenie i publikowanie aplikacji.

## <a name="step-2-add-a-userid-column-to-the-database-schema"></a>Krok 2: Dodaj kolumnę UserId schematu bazy danych
Następnie należy dodać kolumnę UserId do tabeli kontaktów, aby skojarzyć z użytkownikiem (dzierżawcy) każdego wiersza. Firma Microsoft zmieni schematu bezpośrednio w bazie danych, dzięki czemu nie trzeba było Dołącz nasz model danych EF to pole.

Połączenie z bazą danych bezpośrednio, za pomocą programu SQL Server Management Studio lub Visual Studio, a następnie wykonaj T-SQL:

```
ALTER TABLE Contacts ADD UserId nvarchar(128)
    DEFAULT CAST(SESSION_CONTEXT(N'UserId') AS nvarchar(128))
```

Spowoduje to dodanie kolumny UserId do tabeli kontaktów. Możemy użyć typu danych nvarchar(128) odpowiadające UserId przechowywane w tabeli AspNetUsers i utworzymy ograniczenie domyślne, które automatycznie ustawi UserId nowo wstawionych wierszy za UserId przechowywanych obecnie we SESSION_CONTEXT.

Teraz tabeli wygląda następująco:

![Tabela kontaktów programu SSMS](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-Contacts.png)

Podczas tworzenia nowych kontaktów, automatycznie zostaną przydzieleni poprawny identyfikator użytkownika. Dla celów demonstracyjnych jednak teraz przypisać niektóre z tych istniejące kontakty do istniejącego użytkownika.

Jeśli w aplikacji już zostały utworzone w przypadku kilku użytkowników (np. przy użyciu lokalnego, Google lub usługi Facebook kont), będą widoczne w tabeli AspNetUsers. Na poniższym zrzucie ekranu jest tylko jeden użytkownik do tej pory.

![Tabela SSMS AspNetUsers](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-AspNetUsers.png)

Skopiuj identyfikator user1@contoso.comi wklej go do instrukcji T-SQL poniżej. Wykonanie tej instrukcji, aby skojarzyć trzy kontaktów z tego identyfikatora użytkownika.

```
UPDATE Contacts SET UserId = '19bc9b0d-28dd-4510-bd5e-d6b6d445f511'
WHERE ContactId IN (1, 2, 5)
```

## <a name="step-3-create-a-row-level-security-policy-in-the-database"></a>Krok 3: Tworzenie zasad zabezpieczeń na poziomie wiersza w bazie danych
Ostatnim krokiem jest utworzenie zasady zabezpieczeń, która używa identyfikatora UserId SESSION_CONTEXT automatyczne filtrowanie wyników zwróconych przez zapytania.

Gdy połączenie z bazą danych, wykonaj następujące T-SQL:

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

Ten kod wykonuje trzy czynności. Najpierw tworzy nowego schematu, najlepszym rozwiązaniem dla scentralizowany i ograniczenie dostępu do obiektów zabezpieczenia na poziomie wiersza. Następnie tworzy predykatu funkcję, która zwróci "1", gdy nazwa użytkownika w SESSION_CONTEXT jest zgodna z UserId wiersza. Na koniec tworzy zasady zabezpieczeń, które dodaje tej funkcji jako predykat filtru i blok w tabeli kontaktów. Predykat filtru powoduje zapytania do zwrócenia tylko wiersze, które należą do bieżącego użytkownika, a predykat bloku działa jako zabezpieczenie, co zapobiega kiedykolwiek przypadkowo wstawiania wiersza dla niewłaściwego użytkownika aplikacji.

Teraz uruchom aplikację i zaloguj się jako user1@contoso.com. Ten użytkownik widzi teraz kontaktów, możemy przypisane do tego identyfikatora użytkownika wcześniej:

![Skontaktuj się z aplikacji Menedżera przed włączeniem zabezpieczenia na poziomie wiersza](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-After.png)

Aby to sprawdzić dodatkowe, spróbuj zarejestrować nowego użytkownika. Nie będzie widocznej żadne kontakty, ponieważ żaden z przypisanym do nich. W przypadku tworzenia nowego kontaktu, będzie można przypisać do nich, a tylko będą oni mogli go wyświetlać.

## <a name="next-steps"></a>Następne kroki
Gotowe. Prostej aplikacji sieci web skontaktuj się z Menedżera został przekonwertowany na wielodostępnej jedną której każdy użytkownik ma własną listy kontaktów. Przy użyciu zabezpieczeń na poziomie wiersza, firma Microsoft już unikać złożoność wymuszania logika dostępu dzierżawcy w naszym kodzie aplikacji. To przezroczystość zezwala aplikacji na skupić się na wykonywanego problem biznesowy rzeczywistych, a także zmniejsza ryzyko przypadkowego wyciekowi danych jako ścieżce bazowej kodu aplikacji rozwoju.

W tym samouczku jest tylko wewnętrzna powierzchni możliwości odświeżania. Na przykład można mieć bardziej zaawansowane opcje lub logika szczegółowego dostępu, a jego można przechowywać więcej niż tylko bieżący identyfikator użytkownika w SESSION_CONTEXT. Istnieje również możliwość [zintegrować zabezpieczenia na poziomie wiersza z bibliotek klienta narzędzi elastycznej bazy danych](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md) do obsługi wielu dzierżawcy fragmentów w warstwie danych.

Poza tych możliwości pracujemy również nawet ulepszyć zabezpieczenia na poziomie wiersza. Jeśli masz pytania, pomysłów lub rzeczy, które chcesz wyświetlić, prosimy o kontakt w komentarzach. Cenimy Twoją opinię!

