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
# <a name="tutorial-web-app-with-a-multi-tenant-database-using-entity-framework-and-row-level-security"></a><span data-ttu-id="d2a1a-103">Samouczek: Aplikacja sieci Web z wieloma dzierżawcami bazy danych przy użyciu programu Entity Framework i zabezpieczenia na poziomie wiersza</span><span class="sxs-lookup"><span data-stu-id="d2a1a-103">Tutorial: Web app with a multi-tenant database using Entity Framework and Row-Level Security</span></span>
<span data-ttu-id="d2a1a-104">W tym samouczku pokazano, jak tworzenie aplikacji sieci web z wieloma dzierżawcami z "[udostępnionej bazy danych, udostępnione schematu](https://msdn.microsoft.com/library/aa479086.aspx)" dzierżawy modelu, używając programu Entity Framework i [zabezpieczenia na poziomie wiersza](https://msdn.microsoft.com/library/dn765131.aspx).</span><span class="sxs-lookup"><span data-stu-id="d2a1a-104">This tutorial shows how to build a multi-tenant web app with a "[shared database, shared schema](https://msdn.microsoft.com/library/aa479086.aspx)" tenancy model, using Entity Framework and [Row-Level Security](https://msdn.microsoft.com/library/dn765131.aspx).</span></span> <span data-ttu-id="d2a1a-105">W tym modelu pojedynczej bazy danych zawiera dane dla wielu dzierżawców, a każdy wiersz w każdej tabeli jest skojarzony z "Dzierżawy ID."</span><span class="sxs-lookup"><span data-stu-id="d2a1a-105">In this model, a single database contains data for many tenants, and each row in each table is associated with a "Tenant ID."</span></span> <span data-ttu-id="d2a1a-106">Wiersz poziom zabezpieczeń kontrola dostępu, nowej funkcji bazy danych SQL Azure jest używana do uniemożliwić dostęp do siebie nawzajem danych dzierżawcy.</span><span class="sxs-lookup"><span data-stu-id="d2a1a-106">Row-Level Security (RLS), a new feature for Azure SQL Database, is used to prevent tenants from accessing each other's data.</span></span> <span data-ttu-id="d2a1a-107">Wymaga tylko jednego, niewielkie zmiany w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d2a1a-107">This requires just a single, small change to the application.</span></span> <span data-ttu-id="d2a1a-108">Centralizując logika dostępu dzierżawcy w bazie danych sam zabezpieczenia na poziomie wiersza upraszcza kod aplikacji i zmniejsza zagrożenie wyciekiem danych przypadkowemu między dzierżawcami.</span><span class="sxs-lookup"><span data-stu-id="d2a1a-108">By centralizing the tenant access logic within the database itself, RLS simplifies the application code and reduces the risk of accidental data leakage between tenants.</span></span>

<span data-ttu-id="d2a1a-109">Zacznijmy od prostej aplikacji menedżera kontaktu z [tworzenie aplikacji ASP.NET MVP z uwierzytelniania i bazy danych SQL i wdrożyć w usłudze Azure App Service](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="d2a1a-109">Let's start with the simple Contact Manager application from [Create an ASP.NET MVP app with auth and SQL DB and deploy to Azure App Service](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span></span> <span data-ttu-id="d2a1a-110">Prawo teraz aplikacji zezwala wszystkim użytkownikom (dzierżawcami), aby wyświetlić wszystkie kontakty:</span><span class="sxs-lookup"><span data-stu-id="d2a1a-110">Right now, the application allows all users (tenants) to see all contacts:</span></span>

![Skontaktuj się z aplikacji Menedżera przed włączeniem zabezpieczenia na poziomie wiersza](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-Before.png)

<span data-ttu-id="d2a1a-112">Z kilku niewielkich zmian dodamy obsługę wielu dzierżawców, tak aby użytkownicy mogli zobaczyć kontaktów, które należą do nich.</span><span class="sxs-lookup"><span data-stu-id="d2a1a-112">With just a few small changes, we will add support for multi-tenancy, so that users are able to see only the contacts that belong to them.</span></span>

## <a name="step-1-add-an-interceptor-class-in-the-application-to-set-the-sessioncontext"></a><span data-ttu-id="d2a1a-113">Krok 1: Dodaj klasę interceptora w aplikacji, aby ustawić SESSION_CONTEXT</span><span class="sxs-lookup"><span data-stu-id="d2a1a-113">Step 1: Add an Interceptor class in the application to set the SESSION_CONTEXT</span></span>
<span data-ttu-id="d2a1a-114">Brak jednej zmiany w aplikacji, które musimy upewnić.</span><span class="sxs-lookup"><span data-stu-id="d2a1a-114">There is one application change we need to make.</span></span> <span data-ttu-id="d2a1a-115">Wszyscy użytkownicy aplikacji łączyć się z bazą danych przy użyciu tych samych parametrach połączenia (tj. tego samego logowania SQL), dlatego nie istnieje obecnie sposób zasady zabezpieczenia na poziomie wiersza wiedzieć, który użytkownik powinien Filtruj.</span><span class="sxs-lookup"><span data-stu-id="d2a1a-115">Because all application users connect to the database using the same connection string (i.e. same SQL login), there is currently no way for an RLS policy to know which user it should filter for.</span></span> <span data-ttu-id="d2a1a-116">Ta metoda jest bardzo często używane w aplikacji sieci web, ponieważ umożliwia ona wydajne buforowania połączeń, ale oznacza to, że potrzebujemy inny sposób identyfikowania użytkownika bieżącej aplikacji w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="d2a1a-116">This approach is very common in web applications because it enables efficient connection pooling, but it means we need another way to identify the current application user within the database.</span></span> <span data-ttu-id="d2a1a-117">Rozwiązanie to ma zestaw par klucz wartość dla bieżącego identyfikatora użytkownika w aplikacji [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806) natychmiast po otwarciu połączenia, zanim wykonywania kwerendy.</span><span class="sxs-lookup"><span data-stu-id="d2a1a-117">The solution is to have the application set a key-value pair for the current UserId in the [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806) immediately after opening a connection, before it executes any queries.</span></span> <span data-ttu-id="d2a1a-118">SESSION_CONTEXT jest magazyn kluczy i wartości o zakresie sesji, a nasze zasady zabezpieczenia na poziomie wiersza będzie używać UserId znajdujące się w niej do identyfikowania bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d2a1a-118">SESSION_CONTEXT is a session-scoped key-value store, and our RLS policy will use the UserId stored in it to identify the current user.</span></span>

<span data-ttu-id="d2a1a-119">Dodamy [interceptora](https://msdn.microsoft.com/data/dn469464.aspx) (w szczególności [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor)), nowej funkcji w ramach jednostki (EF) 6, do automatycznego ustalania bieżącego identyfikatora użytkownika w SESSION_CONTEXT, wykonując instrukcję T-SQL przy każdym EF otwarciu połączenia.</span><span class="sxs-lookup"><span data-stu-id="d2a1a-119">We will add an [interceptor](https://msdn.microsoft.com/data/dn469464.aspx) (in particular, a [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor)), a new feature in Entity Framework (EF) 6, to automatically set the current UserId in the SESSION_CONTEXT by executing a T-SQL statement whenever EF opens a connection.</span></span>

1. <span data-ttu-id="d2a1a-120">Otwórz projekt ContactManager w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d2a1a-120">Open the ContactManager project in Visual Studio.</span></span>
2. <span data-ttu-id="d2a1a-121">Kliknij prawym przyciskiem folder modeli w Eksploratorze rozwiązań i wybierz polecenie Dodaj > klasy.</span><span class="sxs-lookup"><span data-stu-id="d2a1a-121">Right-click on the Models folder in the Solution Explorer, and choose Add > Class.</span></span>
3. <span data-ttu-id="d2a1a-122">Nazwa nowej klasy "SessionContextInterceptor.cs", a następnie kliknij przycisk Dodaj.</span><span class="sxs-lookup"><span data-stu-id="d2a1a-122">Name the new class "SessionContextInterceptor.cs" and click Add.</span></span>
4. <span data-ttu-id="d2a1a-123">Zastąp zawartość SessionContextInterceptor.cs z następującym kodem.</span><span class="sxs-lookup"><span data-stu-id="d2a1a-123">Replace the contents of SessionContextInterceptor.cs with the following code.</span></span>

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

<span data-ttu-id="d2a1a-124">To jest wymagana zmiana tylko aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d2a1a-124">That's the only application change required.</span></span> <span data-ttu-id="d2a1a-125">Przejdź dalej i tworzenie i publikowanie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d2a1a-125">Go ahead and build and publish the application.</span></span>

## <a name="step-2-add-a-userid-column-to-the-database-schema"></a><span data-ttu-id="d2a1a-126">Krok 2: Dodaj kolumnę UserId schematu bazy danych</span><span class="sxs-lookup"><span data-stu-id="d2a1a-126">Step 2: Add a UserId column to the database schema</span></span>
<span data-ttu-id="d2a1a-127">Następnie należy dodać kolumnę UserId do tabeli kontaktów, aby skojarzyć z użytkownikiem (dzierżawcy) każdego wiersza.</span><span class="sxs-lookup"><span data-stu-id="d2a1a-127">Next, we need to add a UserId column to the Contacts table to associate each row with a user (tenant).</span></span> <span data-ttu-id="d2a1a-128">Firma Microsoft zmieni schematu bezpośrednio w bazie danych, dzięki czemu nie trzeba było Dołącz nasz model danych EF to pole.</span><span class="sxs-lookup"><span data-stu-id="d2a1a-128">We will alter the schema directly in the database, so that we don't have to include this field in our EF data model.</span></span>

<span data-ttu-id="d2a1a-129">Połączenie z bazą danych bezpośrednio, za pomocą programu SQL Server Management Studio lub Visual Studio, a następnie wykonaj T-SQL:</span><span class="sxs-lookup"><span data-stu-id="d2a1a-129">Connect to the database directly, using either SQL Server Management Studio or Visual Studio, and then execute the following T-SQL:</span></span>

```
ALTER TABLE Contacts ADD UserId nvarchar(128)
    DEFAULT CAST(SESSION_CONTEXT(N'UserId') AS nvarchar(128))
```

<span data-ttu-id="d2a1a-130">Spowoduje to dodanie kolumny UserId do tabeli kontaktów.</span><span class="sxs-lookup"><span data-stu-id="d2a1a-130">This adds a UserId column to the Contacts table.</span></span> <span data-ttu-id="d2a1a-131">Możemy użyć typu danych nvarchar(128) odpowiadające UserId przechowywane w tabeli AspNetUsers i utworzymy ograniczenie domyślne, które automatycznie ustawi UserId nowo wstawionych wierszy za UserId przechowywanych obecnie we SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="d2a1a-131">We use the nvarchar(128) data type to match the UserIds stored in the AspNetUsers table, and we create a DEFAULT constraint that will automatically set the UserId for newly inserted rows to be the UserId currently stored in SESSION_CONTEXT.</span></span>

<span data-ttu-id="d2a1a-132">Teraz tabeli wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="d2a1a-132">Now the table looks like this:</span></span>

![Tabela kontaktów programu SSMS](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-Contacts.png)

<span data-ttu-id="d2a1a-134">Podczas tworzenia nowych kontaktów, automatycznie zostaną przydzieleni poprawny identyfikator użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d2a1a-134">When new contacts are created, they'll automatically be assigned the correct UserId.</span></span> <span data-ttu-id="d2a1a-135">Dla celów demonstracyjnych jednak teraz przypisać niektóre z tych istniejące kontakty do istniejącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d2a1a-135">For demo purposes, however, let's assign a few of these existing contacts to an existing user.</span></span>

<span data-ttu-id="d2a1a-136">Jeśli w aplikacji już zostały utworzone w przypadku kilku użytkowników (np. przy użyciu lokalnego, Google lub usługi Facebook kont), będą widoczne w tabeli AspNetUsers.</span><span class="sxs-lookup"><span data-stu-id="d2a1a-136">If you've created a few users in the application already (e.g., using local, Google, or Facebook accounts), you'll see them in the AspNetUsers table.</span></span> <span data-ttu-id="d2a1a-137">Na poniższym zrzucie ekranu jest tylko jeden użytkownik do tej pory.</span><span class="sxs-lookup"><span data-stu-id="d2a1a-137">In the screenshot below, there is only one user so far.</span></span>

![Tabela SSMS AspNetUsers](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-AspNetUsers.png)

<span data-ttu-id="d2a1a-139">Skopiuj identyfikator user1@contoso.comi wklej go do instrukcji T-SQL poniżej.</span><span class="sxs-lookup"><span data-stu-id="d2a1a-139">Copy the Id for user1@contoso.com, and paste it into the T-SQL statement below.</span></span> <span data-ttu-id="d2a1a-140">Wykonanie tej instrukcji, aby skojarzyć trzy kontaktów z tego identyfikatora użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d2a1a-140">Execute this statement to associate three of the Contacts with this UserId.</span></span>

```
UPDATE Contacts SET UserId = '19bc9b0d-28dd-4510-bd5e-d6b6d445f511'
WHERE ContactId IN (1, 2, 5)
```

## <a name="step-3-create-a-row-level-security-policy-in-the-database"></a><span data-ttu-id="d2a1a-141">Krok 3: Tworzenie zasad zabezpieczeń na poziomie wiersza w bazie danych</span><span class="sxs-lookup"><span data-stu-id="d2a1a-141">Step 3: Create a Row-Level Security policy in the database</span></span>
<span data-ttu-id="d2a1a-142">Ostatnim krokiem jest utworzenie zasady zabezpieczeń, która używa identyfikatora UserId SESSION_CONTEXT automatyczne filtrowanie wyników zwróconych przez zapytania.</span><span class="sxs-lookup"><span data-stu-id="d2a1a-142">The final step is to create a security policy that uses the UserId in SESSION_CONTEXT to automatically filter the results returned by queries.</span></span>

<span data-ttu-id="d2a1a-143">Gdy połączenie z bazą danych, wykonaj następujące T-SQL:</span><span class="sxs-lookup"><span data-stu-id="d2a1a-143">While still connected to the database, execute the following T-SQL:</span></span>

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

<span data-ttu-id="d2a1a-144">Ten kod wykonuje trzy czynności.</span><span class="sxs-lookup"><span data-stu-id="d2a1a-144">This code does three things.</span></span> <span data-ttu-id="d2a1a-145">Najpierw tworzy nowego schematu, najlepszym rozwiązaniem dla scentralizowany i ograniczenie dostępu do obiektów zabezpieczenia na poziomie wiersza.</span><span class="sxs-lookup"><span data-stu-id="d2a1a-145">First, it creates a new schema as a best practice for centralizing and limiting access to the RLS objects.</span></span> <span data-ttu-id="d2a1a-146">Następnie tworzy predykatu funkcję, która zwróci "1", gdy nazwa użytkownika w SESSION_CONTEXT jest zgodna z UserId wiersza.</span><span class="sxs-lookup"><span data-stu-id="d2a1a-146">Next, it creates a predicate function that will return '1' when the UserId of a row matches the UserId in SESSION_CONTEXT.</span></span> <span data-ttu-id="d2a1a-147">Na koniec tworzy zasady zabezpieczeń, które dodaje tej funkcji jako predykat filtru i blok w tabeli kontaktów.</span><span class="sxs-lookup"><span data-stu-id="d2a1a-147">Finally, it creates a security policy that adds this function as both a filter and block predicate on the Contacts table.</span></span> <span data-ttu-id="d2a1a-148">Predykat filtru powoduje zapytania do zwrócenia tylko wiersze, które należą do bieżącego użytkownika, a predykat bloku działa jako zabezpieczenie, co zapobiega kiedykolwiek przypadkowo wstawiania wiersza dla niewłaściwego użytkownika aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d2a1a-148">The filter predicate causes queries to return only rows that belong to the current user, and the block predicate acts as a safeguard to prevent the application from ever accidentally inserting a row for the wrong user.</span></span>

<span data-ttu-id="d2a1a-149">Teraz uruchom aplikację i zaloguj się jako user1@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="d2a1a-149">Now run the application, and sign in as user1@contoso.com.</span></span> <span data-ttu-id="d2a1a-150">Ten użytkownik widzi teraz kontaktów, możemy przypisane do tego identyfikatora użytkownika wcześniej:</span><span class="sxs-lookup"><span data-stu-id="d2a1a-150">This user now sees only the Contacts we assigned to this UserId earlier:</span></span>

![Skontaktuj się z aplikacji Menedżera przed włączeniem zabezpieczenia na poziomie wiersza](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-After.png)

<span data-ttu-id="d2a1a-152">Aby to sprawdzić dodatkowe, spróbuj zarejestrować nowego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d2a1a-152">To validate this further, try registering a new user.</span></span> <span data-ttu-id="d2a1a-153">Nie będzie widocznej żadne kontakty, ponieważ żaden z przypisanym do nich.</span><span class="sxs-lookup"><span data-stu-id="d2a1a-153">They will see no contacts, because none have been assigned to them.</span></span> <span data-ttu-id="d2a1a-154">W przypadku tworzenia nowego kontaktu, będzie można przypisać do nich, a tylko będą oni mogli go wyświetlać.</span><span class="sxs-lookup"><span data-stu-id="d2a1a-154">If they create a new contact, it will be assigned to them, and only they will be able to see it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d2a1a-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d2a1a-155">Next steps</span></span>
<span data-ttu-id="d2a1a-156">Gotowe.</span><span class="sxs-lookup"><span data-stu-id="d2a1a-156">That's it!</span></span> <span data-ttu-id="d2a1a-157">Prostej aplikacji sieci web skontaktuj się z Menedżera został przekonwertowany na wielodostępnej jedną której każdy użytkownik ma własną listy kontaktów.</span><span class="sxs-lookup"><span data-stu-id="d2a1a-157">The simple Contact Manager web app has been converted into a multi-tenant one where each user has its own contact list.</span></span> <span data-ttu-id="d2a1a-158">Przy użyciu zabezpieczeń na poziomie wiersza, firma Microsoft już unikać złożoność wymuszania logika dostępu dzierżawcy w naszym kodzie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d2a1a-158">By using Row-Level Security, we've avoided the complexity of enforcing tenant access logic in our application code.</span></span> <span data-ttu-id="d2a1a-159">To przezroczystość zezwala aplikacji na skupić się na wykonywanego problem biznesowy rzeczywistych, a także zmniejsza ryzyko przypadkowego wyciekowi danych jako ścieżce bazowej kodu aplikacji rozwoju.</span><span class="sxs-lookup"><span data-stu-id="d2a1a-159">This transparency allows the application to focus on the real business problem at hand, and it also reduces the risk of accidentally leaking data as the application's codebase grows.</span></span>

<span data-ttu-id="d2a1a-160">W tym samouczku jest tylko wewnętrzna powierzchni możliwości odświeżania.</span><span class="sxs-lookup"><span data-stu-id="d2a1a-160">This tutorial has only scratched the surface of what's possible with RLS.</span></span> <span data-ttu-id="d2a1a-161">Na przykład można mieć bardziej zaawansowane opcje lub logika szczegółowego dostępu, a jego można przechowywać więcej niż tylko bieżący identyfikator użytkownika w SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="d2a1a-161">For instance, it's possible to have more sophisticated or granular access logic, and it's possible to store more than just the current UserId in the SESSION_CONTEXT.</span></span> <span data-ttu-id="d2a1a-162">Istnieje również możliwość [zintegrować zabezpieczenia na poziomie wiersza z bibliotek klienta narzędzi elastycznej bazy danych](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md) do obsługi wielu dzierżawcy fragmentów w warstwie danych.</span><span class="sxs-lookup"><span data-stu-id="d2a1a-162">It's also possible to [integrate RLS with the elastic database tools client libraries](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md) to support multi-tenant shards in a scale-out data tier.</span></span>

<span data-ttu-id="d2a1a-163">Poza tych możliwości pracujemy również nawet ulepszyć zabezpieczenia na poziomie wiersza.</span><span class="sxs-lookup"><span data-stu-id="d2a1a-163">Beyond these possibilities, we're also working to make RLS even better.</span></span> <span data-ttu-id="d2a1a-164">Jeśli masz pytania, pomysłów lub rzeczy, które chcesz wyświetlić, prosimy o kontakt w komentarzach.</span><span class="sxs-lookup"><span data-stu-id="d2a1a-164">If you have any questions, ideas, or things you'd like to see, please let us know in the comments.</span></span> <span data-ttu-id="d2a1a-165">Cenimy Twoją opinię!</span><span class="sxs-lookup"><span data-stu-id="d2a1a-165">We appreciate your feedback!</span></span>

