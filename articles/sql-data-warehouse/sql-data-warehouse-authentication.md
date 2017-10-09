---
title: tooAzure aaaAuthentication SQL Data Warehouse | Dokumentacja firmy Microsoft
description: Azure Active Directory (AAD) i SQL Server authentication tooAzure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
tags: 
ms.assetid: fefaaa75-2d0c-4e5d-aadb-410342d1ad73
ms.service: sql-data-warehouse
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.custom: security
ms.date: 03/21/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 66673ce1d4761243755254c8f64de1078a0ea82e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-tooazure-sql-data-warehouse"></a><span data-ttu-id="0f8be-103">TooAzure uwierzytelniania SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="0f8be-103">Authentication tooAzure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0f8be-104">Przegląd zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="0f8be-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="0f8be-105">Uwierzytelnianie</span><span class="sxs-lookup"><span data-stu-id="0f8be-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="0f8be-106">Szyfrowanie (Portal)</span><span class="sxs-lookup"><span data-stu-id="0f8be-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="0f8be-107">Szyfrowanie (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="0f8be-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

<span data-ttu-id="0f8be-108">tooSQL tooconnect hurtowni danych, należy podać poświadczenia zabezpieczeń na potrzeby uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="0f8be-108">tooconnect tooSQL Data Warehouse, you must pass in security credentials for authentication purposes.</span></span> <span data-ttu-id="0f8be-109">Po ustanowieniu połączenia, niektóre ustawienia połączenia są skonfigurowane jako część ustanawianie sesji kwerendy.</span><span class="sxs-lookup"><span data-stu-id="0f8be-109">Upon establishing a connection, certain connection settings are configured as part of establishing your query session.</span></span>  

<span data-ttu-id="0f8be-110">Aby uzyskać więcej informacji na temat zabezpieczeń i w jaki sposób tooenable połączeń tooyour hurtowni danych, zobacz [Zabezpieczanie bazy danych w usłudze SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="0f8be-110">For more information on security and how tooenable connections tooyour data warehouse, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span>

## <a name="sql-authentication"></a><span data-ttu-id="0f8be-111">Uwierzytelnianie SQL</span><span class="sxs-lookup"><span data-stu-id="0f8be-111">SQL authentication</span></span>
<span data-ttu-id="0f8be-112">tooSQL tooconnect hurtowni danych, należy podać hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="0f8be-112">tooconnect tooSQL Data Warehouse, you must provide hello following information:</span></span>

* <span data-ttu-id="0f8be-113">Servername FQDN</span><span class="sxs-lookup"><span data-stu-id="0f8be-113">Fully qualified servername</span></span>
* <span data-ttu-id="0f8be-114">Określ uwierzytelnianie SQL</span><span class="sxs-lookup"><span data-stu-id="0f8be-114">Specify SQL authentication</span></span>
* <span data-ttu-id="0f8be-115">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="0f8be-115">Username</span></span>
* <span data-ttu-id="0f8be-116">Hasło</span><span class="sxs-lookup"><span data-stu-id="0f8be-116">Password</span></span>
* <span data-ttu-id="0f8be-117">Domyślna baza danych (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="0f8be-117">Default database (optional)</span></span>

<span data-ttu-id="0f8be-118">Domyślnie nawiązaniu połączenia toohello *wzorca* bazy danych, a nie bazy danych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="0f8be-118">By default your connection connects toohello *master* database and not your user database.</span></span> <span data-ttu-id="0f8be-119">tooconnect tooyour użytkownika bazy danych, można wybrać toodo jedną z następujących operacji:</span><span class="sxs-lookup"><span data-stu-id="0f8be-119">tooconnect tooyour user database, you can choose toodo one of two things:</span></span>

* <span data-ttu-id="0f8be-120">Określ hello domyślnej bazy danych podczas rejestrowania serwera w Eksploratorze obiektów SQL Server programu SSDT, SSMS, lub w ciągu połączenia aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="0f8be-120">Specify hello default database when registering your server with hello SQL Server Object Explorer in SSDT, SSMS, or in your application connection string.</span></span> <span data-ttu-id="0f8be-121">Na przykład obejmować hello parametru InitialCatalog dla połączenia ODBC.</span><span class="sxs-lookup"><span data-stu-id="0f8be-121">For example, include hello InitialCatalog parameter for an ODBC connection.</span></span>
* <span data-ttu-id="0f8be-122">Przed utworzeniem sesji programu SSDT, zaznacz hello bazy danych użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0f8be-122">Highlight hello user database before creating a session in SSDT.</span></span>

> [!NOTE]
> <span data-ttu-id="0f8be-123">Witaj instrukcji języka Transact-SQL **mojabazadanych UŻYJ;** nie jest obsługiwana dla Zmiana bazy danych hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="0f8be-123">hello Transact-SQL statement **USE MyDatabase;** is not supported for changing hello database for a connection.</span></span> <span data-ttu-id="0f8be-124">Wskazówki dotyczące łączenia tooSQL magazynu danych z narzędziami SSDT można odwoływać się toohello [zapytania z programem Visual Studio] [ Query with Visual Studio] artykułu.</span><span class="sxs-lookup"><span data-stu-id="0f8be-124">For guidance connecting tooSQL Data Warehouse with SSDT, refer toohello [Query with Visual Studio][Query with Visual Studio] article.</span></span>
> 
> 

## <a name="azure-active-directory-aad-authentication"></a><span data-ttu-id="0f8be-125">Uwierzytelnianie usługi Azure Active Directory (AAD)</span><span class="sxs-lookup"><span data-stu-id="0f8be-125">Azure Active Directory (AAD) authentication</span></span>
<span data-ttu-id="0f8be-126">[Usługa Azure Active Directory] [ What is Azure Active Directory] uwierzytelnianie jest mechanizm łączący tooMicrosoft Azure SQL Data Warehouse przy użyciu tożsamości w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0f8be-126">[Azure Active Directory][What is Azure Active Directory] authentication is a mechanism of connecting tooMicrosoft Azure SQL Data Warehouse by using identities in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="0f8be-127">Przy użyciu uwierzytelniania usługi Azure Active Directory mogą centralnie zarządzać hello tożsamości użytkowników bazy danych i innych usług firmy Microsoft w jednej centralnej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="0f8be-127">With Azure Active Directory authentication, you can centrally manage hello identities of database users and other Microsoft services in one central location.</span></span> <span data-ttu-id="0f8be-128">Centralne zarządzanie identyfikator udostępnia jedno miejsce toomanage SQL Data Warehouse użytkowników i upraszcza zarządzanie uprawnieniami.</span><span class="sxs-lookup"><span data-stu-id="0f8be-128">Central ID management provides a single place toomanage SQL Data Warehouse users and simplifies permission management.</span></span> 

### <a name="benefits"></a><span data-ttu-id="0f8be-129">Korzyści</span><span class="sxs-lookup"><span data-stu-id="0f8be-129">Benefits</span></span>
<span data-ttu-id="0f8be-130">Azure Active Directory korzyści:</span><span class="sxs-lookup"><span data-stu-id="0f8be-130">Azure Active Directory benefits include:</span></span>

* <span data-ttu-id="0f8be-131">Zapewnia alternatywny tooSQL uwierzytelniania serwera.</span><span class="sxs-lookup"><span data-stu-id="0f8be-131">Provides an alternative tooSQL Server authentication.</span></span>
* <span data-ttu-id="0f8be-132">Pomaga zatrzymać rozprzestrzenianie hello tożsamości użytkowników na serwerach bazy danych.</span><span class="sxs-lookup"><span data-stu-id="0f8be-132">Helps stop hello proliferation of user identities across database servers.</span></span>
* <span data-ttu-id="0f8be-133">Umożliwia obrotu hasła w jednym miejscu</span><span class="sxs-lookup"><span data-stu-id="0f8be-133">Allows password rotation in a single place</span></span>
* <span data-ttu-id="0f8be-134">Zarządzaj uprawnieniami bazy danych przy użyciu zewnętrznego grup (AAD).</span><span class="sxs-lookup"><span data-stu-id="0f8be-134">Manage database permissions using external (AAD) groups.</span></span>
* <span data-ttu-id="0f8be-135">Eliminuje zapisywania haseł przez włączenie zintegrowanego uwierzytelniania systemu Windows i innych metod uwierzytelniania obsługiwanych przez usługę Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0f8be-135">Eliminates storing passwords by enabling integrated Windows authentication and other forms of authentication supported by Azure Active Directory.</span></span>
* <span data-ttu-id="0f8be-136">Używa zawarte bazy danych użytkowników tooauthenticate tożsamości na poziomie hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="0f8be-136">Uses contained database users tooauthenticate identities at hello database level.</span></span>
* <span data-ttu-id="0f8be-137">Obsługuje uwierzytelnianie na podstawie tokenu dla aplikacji łączenie tooSQL hurtowni danych.</span><span class="sxs-lookup"><span data-stu-id="0f8be-137">Supports token-based authentication for applications connecting tooSQL Data Warehouse.</span></span>
* <span data-ttu-id="0f8be-138">Obsługuje uwierzytelnianie wieloskładnikowe za pomocą uwierzytelniania uniwersalnego usługi Active Directory dla programu SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="0f8be-138">Supports Multi-Factor authentication through Active Directory Universal Authentication for SQL Server Management Studio.</span></span> <span data-ttu-id="0f8be-139">Opis usługi Multi-Factor Authentication, zobacz [SSMS obsługę usługi Azure AD MFA z bazy danych SQL i usługi SQL Data Warehouse](../sql-database/sql-database-ssms-mfa-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="0f8be-139">For a description of Multi-Factor Authentication, see [SSMS support for Azure AD MFA with SQL Database and SQL Data Warehouse](../sql-database/sql-database-ssms-mfa-authentication.md).</span></span>

> [!NOTE]
> <span data-ttu-id="0f8be-140">Azure Active Directory jest nadal stosunkowo nowe i ma pewne ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="0f8be-140">Azure Active Directory is still relatively new and has some limitations.</span></span> <span data-ttu-id="0f8be-141">tooensure, że usługi Azure Active Directory jest odpowiedni dla danego środowiska, zobacz [funkcje usługi Azure AD i ograniczenia][Azure AD features and limitations], w szczególności hello dodatkowe zagadnienia.</span><span class="sxs-lookup"><span data-stu-id="0f8be-141">tooensure that Azure Active Directory is a good fit for your environment, see [Azure AD features and limitations][Azure AD features and limitations], specifically hello Additional considerations.</span></span>
> 
> 

### <a name="configuration-steps"></a><span data-ttu-id="0f8be-142">Kroki konfiguracji</span><span class="sxs-lookup"><span data-stu-id="0f8be-142">Configuration steps</span></span>
<span data-ttu-id="0f8be-143">Wykonaj te kroki tooconfigure usługi Azure Active Directory uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="0f8be-143">Follow these steps tooconfigure Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="0f8be-144">Utworzyć i wypełnić usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0f8be-144">Create and populate an Azure Active Directory</span></span>
2. <span data-ttu-id="0f8be-145">Opcjonalnie: Skojarz lub zmienić usługi active directory hello aktualnie skojarzony z subskrypcją platformy Azure</span><span class="sxs-lookup"><span data-stu-id="0f8be-145">Optional: Associate or change hello active directory that is currently associated with your Azure Subscription</span></span>
3. <span data-ttu-id="0f8be-146">Utwórz administrator usługi Azure Active Directory dla usługi Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="0f8be-146">Create an Azure Active Directory administrator for Azure SQL Data Warehouse.</span></span>
4. <span data-ttu-id="0f8be-147">Konfigurowanie komputerów klienckich</span><span class="sxs-lookup"><span data-stu-id="0f8be-147">Configure your client computers</span></span>
5. <span data-ttu-id="0f8be-148">Utwórz użytkowników zawartej bazy danych w sieci tooAzure zamapować bazy danych tożsamości usługi AD</span><span class="sxs-lookup"><span data-stu-id="0f8be-148">Create contained database users in your database mapped tooAzure AD identities</span></span>
6. <span data-ttu-id="0f8be-149">Połącz tooyour hurtowni danych przy użyciu tożsamości usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0f8be-149">Connect tooyour data warehouse by using Azure AD identities</span></span>

<span data-ttu-id="0f8be-150">Obecnie użytkownicy usługi Azure Active Directory nie są wyświetlane w Eksploratorze obiektów program SSDT.</span><span class="sxs-lookup"><span data-stu-id="0f8be-150">Currently Azure Active Directory users are not shown in SSDT Object Explorer.</span></span> <span data-ttu-id="0f8be-151">Jako obejście, Wyświetl użytkowników hello w [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).</span><span class="sxs-lookup"><span data-stu-id="0f8be-151">As a workaround, view hello users in [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).</span></span>

### <a name="find-hello-details"></a><span data-ttu-id="0f8be-152">Znajduje szczegóły hello</span><span class="sxs-lookup"><span data-stu-id="0f8be-152">Find hello details</span></span>
* <span data-ttu-id="0f8be-153">Hello kroki tooconfigure i używanie usługi Azure Active Directory uwierzytelniania są niemal identyczne dla usługi Azure SQL Database i Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="0f8be-153">hello steps tooconfigure and use Azure Active Directory authentication are nearly identical for Azure SQL Database and Azure SQL Data Warehouse.</span></span> <span data-ttu-id="0f8be-154">Wykonaj czynności opisane w temacie hello szczegółowe hello [tooSQL łączenie bazy danych lub danych magazynu przez przy użyciu Azure Active Directory uwierzytelniania SQL](../sql-database/sql-database-aad-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="0f8be-154">Follow hello detailed steps in hello topic [Connecting tooSQL Database or SQL Data Warehouse By Using Azure Active Directory Authentication](../sql-database/sql-database-aad-authentication.md).</span></span>
* <span data-ttu-id="0f8be-155">Tworzenie ról w niestandardowej bazie danych i Dodawanie ról toohello użytkowników.</span><span class="sxs-lookup"><span data-stu-id="0f8be-155">Create custom database roles and add users toohello roles.</span></span> <span data-ttu-id="0f8be-156">Następnie przydziel uprawnienia szczegółowego toohello ról.</span><span class="sxs-lookup"><span data-stu-id="0f8be-156">Then grant granular permissions toohello roles.</span></span> <span data-ttu-id="0f8be-157">Aby uzyskać więcej informacji, zobacz [wprowadzenie do korzystania z bazy danych aparatu uprawnień](https://msdn.microsoft.com/library/mt667986.aspx).</span><span class="sxs-lookup"><span data-stu-id="0f8be-157">For more information, see [Getting Started with Database Engine Permissions](https://msdn.microsoft.com/library/mt667986.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f8be-158">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0f8be-158">Next steps</span></span>
<span data-ttu-id="0f8be-159">toostart badania magazynu danych z programu Visual Studio i innych aplikacji, zobacz [zapytania z programem Visual Studio][Query with Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="0f8be-159">toostart querying your data warehouse with Visual Studio and other applications, see [Query with Visual Studio][Query with Visual Studio].</span></span>

<!-- Article references -->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md
[What is Azure Active Directory]: ../active-directory/active-directory-whatis.md
[Azure AD features and limitations]: ../sql-database/sql-database-aad-authentication.md#azure-ad-features-and-limitations
