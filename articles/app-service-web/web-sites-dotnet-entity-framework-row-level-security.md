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
# <a name="tutorial-web-app-with-a-multi-tenant-database-using-entity-framework-and-row-level-security"></a><span data-ttu-id="ab2e3-103">Samouczek: Aplikacja sieci Web z wieloma dzierżawcami bazy danych przy użyciu programu Entity Framework i zabezpieczenia na poziomie wiersza</span><span class="sxs-lookup"><span data-stu-id="ab2e3-103">Tutorial: Web app with a multi-tenant database using Entity Framework and Row-Level Security</span></span>
<span data-ttu-id="ab2e3-104">Ten samouczek pokazuje, jak toobuild wielodostępnej sieci web aplikacji za pomocą "[udostępnionej bazy danych, udostępnione schematu](https://msdn.microsoft.com/library/aa479086.aspx)" dzierżawy modelu, używając programu Entity Framework i [zabezpieczenia na poziomie wiersza](https://msdn.microsoft.com/library/dn765131.aspx).</span><span class="sxs-lookup"><span data-stu-id="ab2e3-104">This tutorial shows how toobuild a multi-tenant web app with a "[shared database, shared schema](https://msdn.microsoft.com/library/aa479086.aspx)" tenancy model, using Entity Framework and [Row-Level Security](https://msdn.microsoft.com/library/dn765131.aspx).</span></span> <span data-ttu-id="ab2e3-105">W tym modelu pojedynczej bazy danych zawiera dane dla wielu dzierżawców, a każdy wiersz w każdej tabeli jest skojarzony z "Dzierżawy ID."</span><span class="sxs-lookup"><span data-stu-id="ab2e3-105">In this model, a single database contains data for many tenants, and each row in each table is associated with a "Tenant ID."</span></span> <span data-ttu-id="ab2e3-106">Wiersz poziom zabezpieczeń kontrola dostępu, nowej funkcji bazy danych SQL Azure jest używane tooprevent dzierżawcy dostęp do siebie nawzajem danych.</span><span class="sxs-lookup"><span data-stu-id="ab2e3-106">Row-Level Security (RLS), a new feature for Azure SQL Database, is used tooprevent tenants from accessing each other's data.</span></span> <span data-ttu-id="ab2e3-107">Wymaga to tylko pojedynczą, aplikacje toohello niewielkie zmiany.</span><span class="sxs-lookup"><span data-stu-id="ab2e3-107">This requires just a single, small change toohello application.</span></span> <span data-ttu-id="ab2e3-108">Scentralizowaniu hello dzierżawy logika dostępu w ramach hello bazy danych zabezpieczenia na poziomie wiersza kodu aplikacji hello upraszcza i zmniejsza ryzyko hello wycieku danych przypadkowemu między dzierżawcami.</span><span class="sxs-lookup"><span data-stu-id="ab2e3-108">By centralizing hello tenant access logic within hello database itself, RLS simplifies hello application code and reduces hello risk of accidental data leakage between tenants.</span></span>

<span data-ttu-id="ab2e3-109">Zacznijmy od hello prostą aplikację kontaktów Menedżerze z [tworzenie aplikacji ASP.NET MVP z uwierzytelniania i bazy danych SQL i wdrażanie tooAzure usługi aplikacji](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="ab2e3-109">Let's start with hello simple Contact Manager application from [Create an ASP.NET MVP app with auth and SQL DB and deploy tooAzure App Service](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span></span> <span data-ttu-id="ab2e3-110">Uprawnienie teraz aplikacji hello umożliwia wszystkich użytkowników (dzierżawcami) toosee wszystkich kontaktów:</span><span class="sxs-lookup"><span data-stu-id="ab2e3-110">Right now, hello application allows all users (tenants) toosee all contacts:</span></span>

![Skontaktuj się z aplikacji Menedżera przed włączeniem zabezpieczenia na poziomie wiersza](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-Before.png)

<span data-ttu-id="ab2e3-112">Z kilku niewielkich zmian dodamy obsługę wielu dzierżawców, tak aby użytkownicy mogli toosee tylko hello kontaktów, do których należą toothem.</span><span class="sxs-lookup"><span data-stu-id="ab2e3-112">With just a few small changes, we will add support for multi-tenancy, so that users are able toosee only hello contacts that belong toothem.</span></span>

## <a name="step-1-add-an-interceptor-class-in-hello-application-tooset-hello-sessioncontext"></a><span data-ttu-id="ab2e3-113">Krok 1: Dodaj klasę interceptora w hello tooset aplikacji hello SESSION_CONTEXT</span><span class="sxs-lookup"><span data-stu-id="ab2e3-113">Step 1: Add an Interceptor class in hello application tooset hello SESSION_CONTEXT</span></span>
<span data-ttu-id="ab2e3-114">Brak jednej zmiany aplikacji potrzebujemy toomake.</span><span class="sxs-lookup"><span data-stu-id="ab2e3-114">There is one application change we need toomake.</span></span> <span data-ttu-id="ab2e3-115">Ponieważ wszyscy użytkownicy aplikacji łączą się przy użyciu bazy danych toohello hello tych samych parametrach połączenia (tj. tego samego logowania SQL), obecnie nie istnieje sposób dla tooknow zasad Kontrola dostępu użytkownika, który go należy filtrować.</span><span class="sxs-lookup"><span data-stu-id="ab2e3-115">Because all application users connect toohello database using hello same connection string (i.e. same SQL login), there is currently no way for an RLS policy tooknow which user it should filter for.</span></span> <span data-ttu-id="ab2e3-116">Ta metoda jest bardzo często używane w aplikacji sieci web, ponieważ umożliwia ona wydajne buforowania połączeń, ale oznacza to, że potrzebujemy inny sposób tooidentify hello użytkownika bieżącej aplikacji hello bazy danych programu.</span><span class="sxs-lookup"><span data-stu-id="ab2e3-116">This approach is very common in web applications because it enables efficient connection pooling, but it means we need another way tooidentify hello current application user within hello database.</span></span> <span data-ttu-id="ab2e3-117">Witaj rozwiązanie jest zestaw aplikacji hello toohave parę klucz wartość dla hello identyfikator bieżącego użytkownika w hello [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806) natychmiast po otwarciu połączenia, zanim wykonywania kwerendy.</span><span class="sxs-lookup"><span data-stu-id="ab2e3-117">hello solution is toohave hello application set a key-value pair for hello current UserId in hello [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806) immediately after opening a connection, before it executes any queries.</span></span> <span data-ttu-id="ab2e3-118">SESSION_CONTEXT jest magazyn kluczy i wartości o zakresie sesji, a nasze zasady zabezpieczenia na poziomie wiersza będzie używać hello UserId znajdujące się w niej tooidentify hello bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ab2e3-118">SESSION_CONTEXT is a session-scoped key-value store, and our RLS policy will use hello UserId stored in it tooidentify hello current user.</span></span>

<span data-ttu-id="ab2e3-119">Teraz dodamy [interceptora](https://msdn.microsoft.com/data/dn469464.aspx) (w szczególności [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor)), nowej funkcji w ramach jednostki (EF) 6, zestaw tooautomatically hello identyfikator bieżącego użytkownika w hello SESSION_CONTEXT, wykonując Instrukcja T-SQL przy każdym EF otwarciu połączenia.</span><span class="sxs-lookup"><span data-stu-id="ab2e3-119">We will add an [interceptor](https://msdn.microsoft.com/data/dn469464.aspx) (in particular, a [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor)), a new feature in Entity Framework (EF) 6, tooautomatically set hello current UserId in hello SESSION_CONTEXT by executing a T-SQL statement whenever EF opens a connection.</span></span>

1. <span data-ttu-id="ab2e3-120">Otwórz projekt ContactManager hello w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ab2e3-120">Open hello ContactManager project in Visual Studio.</span></span>
2. <span data-ttu-id="ab2e3-121">Kliknij prawym przyciskiem myszy na powitania folderu modeli w hello Eksploratora rozwiązań i wybierz polecenie Dodaj > klasy.</span><span class="sxs-lookup"><span data-stu-id="ab2e3-121">Right-click on hello Models folder in hello Solution Explorer, and choose Add > Class.</span></span>
3. <span data-ttu-id="ab2e3-122">Nazwa nowej klasy hello "SessionContextInterceptor.cs", a następnie kliknij przycisk Dodaj.</span><span class="sxs-lookup"><span data-stu-id="ab2e3-122">Name hello new class "SessionContextInterceptor.cs" and click Add.</span></span>
4. <span data-ttu-id="ab2e3-123">Zamień zawartość hello SessionContextInterceptor.cs hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="ab2e3-123">Replace hello contents of SessionContextInterceptor.cs with hello following code.</span></span>

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

<span data-ttu-id="ab2e3-124">To jest wymagane zmiany tylko aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="ab2e3-124">That's hello only application change required.</span></span> <span data-ttu-id="ab2e3-125">Przejdź dalej i tworzenie i publikowanie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="ab2e3-125">Go ahead and build and publish hello application.</span></span>

## <a name="step-2-add-a-userid-column-toohello-database-schema"></a><span data-ttu-id="ab2e3-126">Krok 2: Dodawanie schematu bazy danych toohello kolumny identyfikatora UserId</span><span class="sxs-lookup"><span data-stu-id="ab2e3-126">Step 2: Add a UserId column toohello database schema</span></span>
<span data-ttu-id="ab2e3-127">Następnie należy tooadd tooassociate kolumny tabeli kontaktów toohello UserId każdego wiersza z użytkownikiem (dzierżawcy).</span><span class="sxs-lookup"><span data-stu-id="ab2e3-127">Next, we need tooadd a UserId column toohello Contacts table tooassociate each row with a user (tenant).</span></span> <span data-ttu-id="ab2e3-128">Firma Microsoft zmieni schematu hello bezpośrednio w bazie danych hello, dzięki czemu nie trzeba tooinclude tego pola w modelu danych EF.</span><span class="sxs-lookup"><span data-stu-id="ab2e3-128">We will alter hello schema directly in hello database, so that we don't have tooinclude this field in our EF data model.</span></span>

<span data-ttu-id="ab2e3-129">Połączenia bazy danych toohello bezpośrednio, za pomocą programu SQL Server Management Studio lub Visual Studio, a następnie wykonaj powitania po T-SQL:</span><span class="sxs-lookup"><span data-stu-id="ab2e3-129">Connect toohello database directly, using either SQL Server Management Studio or Visual Studio, and then execute hello following T-SQL:</span></span>

```
ALTER TABLE Contacts ADD UserId nvarchar(128)
    DEFAULT CAST(SESSION_CONTEXT(N'UserId') AS nvarchar(128))
```

<span data-ttu-id="ab2e3-130">Spowoduje to dodanie tabeli kontaktów toohello kolumny identyfikatora użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ab2e3-130">This adds a UserId column toohello Contacts table.</span></span> <span data-ttu-id="ab2e3-131">Używamy hello nvarchar(128) danych typu toomatch powitalne UserId przechowywane w tabeli AspNetUsers hello i utworzymy ograniczenie domyślne, które automatycznie ustawi hello UserId dla nowo wstawionych wierszy toobe hello UserId przechowywanych obecnie we SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="ab2e3-131">We use hello nvarchar(128) data type toomatch hello UserIds stored in hello AspNetUsers table, and we create a DEFAULT constraint that will automatically set hello UserId for newly inserted rows toobe hello UserId currently stored in SESSION_CONTEXT.</span></span>

<span data-ttu-id="ab2e3-132">Teraz tabeli hello wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="ab2e3-132">Now hello table looks like this:</span></span>

![Tabela kontaktów programu SSMS](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-Contacts.png)

<span data-ttu-id="ab2e3-134">Podczas tworzenia nowych kontaktów, automatycznie zostaną przydzieleni hello Popraw identyfikator użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ab2e3-134">When new contacts are created, they'll automatically be assigned hello correct UserId.</span></span> <span data-ttu-id="ab2e3-135">Dla celów demonstracyjnych jednak teraz przypisać niektóre z tych istniejących tooan kontaktów istniejącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ab2e3-135">For demo purposes, however, let's assign a few of these existing contacts tooan existing user.</span></span>

<span data-ttu-id="ab2e3-136">Jeśli w aplikacji hello już zostały utworzone w przypadku kilku użytkowników (np. przy użyciu lokalnego, Google lub usługi Facebook kont), będą widoczne w tabeli AspNetUsers hello.</span><span class="sxs-lookup"><span data-stu-id="ab2e3-136">If you've created a few users in hello application already (e.g., using local, Google, or Facebook accounts), you'll see them in hello AspNetUsers table.</span></span> <span data-ttu-id="ab2e3-137">W poniższym zrzucie ekranu hello jest tylko jeden użytkownik wykonanej do tej pory.</span><span class="sxs-lookup"><span data-stu-id="ab2e3-137">In hello screenshot below, there is only one user so far.</span></span>

![Tabela SSMS AspNetUsers](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-AspNetUsers.png)

<span data-ttu-id="ab2e3-139">Kopiuj hello identyfikator dla user1@contoso.comi wklej go do instrukcji hello T-SQL poniżej.</span><span class="sxs-lookup"><span data-stu-id="ab2e3-139">Copy hello Id for user1@contoso.com, and paste it into hello T-SQL statement below.</span></span> <span data-ttu-id="ab2e3-140">Wykonanie tej instrukcji tooassociate trzech hello kontaktów z tego identyfikatora użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ab2e3-140">Execute this statement tooassociate three of hello Contacts with this UserId.</span></span>

```
UPDATE Contacts SET UserId = '19bc9b0d-28dd-4510-bd5e-d6b6d445f511'
WHERE ContactId IN (1, 2, 5)
```

## <a name="step-3-create-a-row-level-security-policy-in-hello-database"></a><span data-ttu-id="ab2e3-141">Krok 3: Tworzenie zasad zabezpieczeń na poziomie wiersza w bazie danych hello</span><span class="sxs-lookup"><span data-stu-id="ab2e3-141">Step 3: Create a Row-Level Security policy in hello database</span></span>
<span data-ttu-id="ab2e3-142">Ostatnim krokiem Hello jest toocreate zasady zabezpieczeń, które używa hello UserId w SESSION_CONTEXT tooautomatically filtru hello wyników zwróconych w wyniku zapytania.</span><span class="sxs-lookup"><span data-stu-id="ab2e3-142">hello final step is toocreate a security policy that uses hello UserId in SESSION_CONTEXT tooautomatically filter hello results returned by queries.</span></span>

<span data-ttu-id="ab2e3-143">Podczas toohello nadal połączenia bazy danych wykonaj powitania po T-SQL:</span><span class="sxs-lookup"><span data-stu-id="ab2e3-143">While still connected toohello database, execute hello following T-SQL:</span></span>

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

<span data-ttu-id="ab2e3-144">Ten kod wykonuje trzy czynności.</span><span class="sxs-lookup"><span data-stu-id="ab2e3-144">This code does three things.</span></span> <span data-ttu-id="ab2e3-145">Najpierw tworzy nowego schematu, najlepszym rozwiązaniem dla scentralizowany i ograniczenie dostępu toohello zabezpieczenia na poziomie wiersza obiektów.</span><span class="sxs-lookup"><span data-stu-id="ab2e3-145">First, it creates a new schema as a best practice for centralizing and limiting access toohello RLS objects.</span></span> <span data-ttu-id="ab2e3-146">Następnie tworzy predykatu funkcję, która zwróci "1", gdy hello UserId w SESSION_CONTEXT jest zgodna z hello UserId wiersza.</span><span class="sxs-lookup"><span data-stu-id="ab2e3-146">Next, it creates a predicate function that will return '1' when hello UserId of a row matches hello UserId in SESSION_CONTEXT.</span></span> <span data-ttu-id="ab2e3-147">Na koniec tworzy zasady zabezpieczeń, które dodaje tej funkcji jako predykatu filtru i blok w tabeli kontaktów hello.</span><span class="sxs-lookup"><span data-stu-id="ab2e3-147">Finally, it creates a security policy that adds this function as both a filter and block predicate on hello Contacts table.</span></span> <span data-ttu-id="ab2e3-148">Predykat filtru Hello powoduje tooreturn zapytania tylko wiersze, które należy toohello bieżącego użytkownika, a predykat bloku hello działa jako aplikacja hello tooprevent zabezpieczenie z kiedykolwiek przypadkowo wstawiania wiersza dla użytkownika niewłaściwy hello.</span><span class="sxs-lookup"><span data-stu-id="ab2e3-148">hello filter predicate causes queries tooreturn only rows that belong toohello current user, and hello block predicate acts as a safeguard tooprevent hello application from ever accidentally inserting a row for hello wrong user.</span></span>

<span data-ttu-id="ab2e3-149">Teraz uruchom aplikację hello i zaloguj się jako user1@contoso.com. Ten użytkownik widzi teraz tylko kontakty hello możemy przypisane toothis UserId wcześniej:</span><span class="sxs-lookup"><span data-stu-id="ab2e3-149">Now run hello application, and sign in as user1@contoso.com. This user now sees only hello Contacts we assigned toothis UserId earlier:</span></span>

![Skontaktuj się z aplikacji Menedżera przed włączeniem zabezpieczenia na poziomie wiersza](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-After.png)

<span data-ttu-id="ab2e3-151">toovalidate to dodatkowe, spróbuj zarejestrować nowego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ab2e3-151">toovalidate this further, try registering a new user.</span></span> <span data-ttu-id="ab2e3-152">Nie będzie widocznej żadne kontakty, ponieważ żaden z przypisanym toothem.</span><span class="sxs-lookup"><span data-stu-id="ab2e3-152">They will see no contacts, because none have been assigned toothem.</span></span> <span data-ttu-id="ab2e3-153">Jeśli tworzenia nowego kontaktu, zostanie do niej przypisany toothem i tylko będą oni mogli toosee go.</span><span class="sxs-lookup"><span data-stu-id="ab2e3-153">If they create a new contact, it will be assigned toothem, and only they will be able toosee it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab2e3-154">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ab2e3-154">Next steps</span></span>
<span data-ttu-id="ab2e3-155">Gotowe.</span><span class="sxs-lookup"><span data-stu-id="ab2e3-155">That's it!</span></span> <span data-ttu-id="ab2e3-156">Hello prostej aplikacji sieci web skontaktuj się z Menedżera został przekonwertowany na wielodostępnej jedną której każdy użytkownik ma własną listy kontaktów.</span><span class="sxs-lookup"><span data-stu-id="ab2e3-156">hello simple Contact Manager web app has been converted into a multi-tenant one where each user has its own contact list.</span></span> <span data-ttu-id="ab2e3-157">Przy użyciu zabezpieczeń na poziomie wiersza, firma Microsoft już unikać złożoność hello wymuszania logika dostępu dzierżawcy w naszym kodzie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ab2e3-157">By using Row-Level Security, we've avoided hello complexity of enforcing tenant access logic in our application code.</span></span> <span data-ttu-id="ab2e3-158">Przezroczystość ten umożliwia toofocus aplikacji hello na problem biznesowy rzeczywistych hello wykonywanego i również zmniejsza ryzyko przypadkowego wyciekowi danych jako ścieżce bazowej kodu aplikacji hello hello rozwoju.</span><span class="sxs-lookup"><span data-stu-id="ab2e3-158">This transparency allows hello application toofocus on hello real business problem at hand, and it also reduces hello risk of accidentally leaking data as hello application's codebase grows.</span></span>

<span data-ttu-id="ab2e3-159">Ten samouczek ma tylko zadrapany hello powierzchnię możliwości odświeżania.</span><span class="sxs-lookup"><span data-stu-id="ab2e3-159">This tutorial has only scratched hello surface of what's possible with RLS.</span></span> <span data-ttu-id="ab2e3-160">Na przykład jest możliwe toohave dokładniejsze lub logikę szczegółowego dostępu i jego możliwych toostore więcej niż tylko hello identyfikator bieżącego użytkownika w hello SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="ab2e3-160">For instance, it's possible toohave more sophisticated or granular access logic, and it's possible toostore more than just hello current UserId in hello SESSION_CONTEXT.</span></span> <span data-ttu-id="ab2e3-161">Możliwe jest również zbyt[zintegrować zabezpieczenia na poziomie wiersza z bibliotek klienta narzędzi elastycznej bazy danych hello](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md) toosupport odłamków wielodostępne w warstwie danych.</span><span class="sxs-lookup"><span data-stu-id="ab2e3-161">It's also possible too[integrate RLS with hello elastic database tools client libraries](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md) toosupport multi-tenant shards in a scale-out data tier.</span></span>

<span data-ttu-id="ab2e3-162">Poza tych możliwości również pracujemy toomake jeszcze bardziej poprawić jakość kontrola dostępu.</span><span class="sxs-lookup"><span data-stu-id="ab2e3-162">Beyond these possibilities, we're also working toomake RLS even better.</span></span> <span data-ttu-id="ab2e3-163">Jeśli masz pytania, pomysłów lub rzeczy, które chcesz toosee, prosimy o kontakt w komentarzach hello.</span><span class="sxs-lookup"><span data-stu-id="ab2e3-163">If you have any questions, ideas, or things you'd like toosee, please let us know in hello comments.</span></span> <span data-ttu-id="ab2e3-164">Cenimy Twoją opinię!</span><span class="sxs-lookup"><span data-stu-id="ab2e3-164">We appreciate your feedback!</span></span>

