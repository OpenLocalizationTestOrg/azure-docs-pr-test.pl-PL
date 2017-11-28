---
title: "Uwierzytelnianie usługi Azure SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Azure Active Directory (AAD) i SQL Server uwierzytelniania usługi Azure SQL Data Warehouse."
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
ms.openlocfilehash: 92f48027051bc4aff4d6b8d66fdd6de81bba3657
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="authentication-to-azure-sql-data-warehouse"></a><span data-ttu-id="b2386-103">Authentication to Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="b2386-103">Authentication to Azure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b2386-104">Przegląd zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="b2386-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="b2386-105">Uwierzytelnianie</span><span class="sxs-lookup"><span data-stu-id="b2386-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="b2386-106">Szyfrowanie (Portal)</span><span class="sxs-lookup"><span data-stu-id="b2386-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="b2386-107">Szyfrowanie (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="b2386-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

<span data-ttu-id="b2386-108">Aby połączyć magazyn danych SQL, należy podać poświadczenia zabezpieczeń na potrzeby uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="b2386-108">To connect to SQL Data Warehouse, you must pass in security credentials for authentication purposes.</span></span> <span data-ttu-id="b2386-109">Po ustanowieniu połączenia, niektóre ustawienia połączenia są skonfigurowane jako część ustanawianie sesji kwerendy.</span><span class="sxs-lookup"><span data-stu-id="b2386-109">Upon establishing a connection, certain connection settings are configured as part of establishing your query session.</span></span>  

<span data-ttu-id="b2386-110">Aby uzyskać więcej informacji dotyczących zabezpieczeń i sposobie włączania połączeń do magazynu danych, zobacz [Zabezpieczanie bazy danych w usłudze SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="b2386-110">For more information on security and how to enable connections to your data warehouse, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span>

## <a name="sql-authentication"></a><span data-ttu-id="b2386-111">Uwierzytelnianie SQL</span><span class="sxs-lookup"><span data-stu-id="b2386-111">SQL authentication</span></span>
<span data-ttu-id="b2386-112">Aby nawiązać połączenie SQL Data Warehouse, należy podać następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="b2386-112">To connect to SQL Data Warehouse, you must provide the following information:</span></span>

* <span data-ttu-id="b2386-113">Servername FQDN</span><span class="sxs-lookup"><span data-stu-id="b2386-113">Fully qualified servername</span></span>
* <span data-ttu-id="b2386-114">Określ uwierzytelnianie SQL</span><span class="sxs-lookup"><span data-stu-id="b2386-114">Specify SQL authentication</span></span>
* <span data-ttu-id="b2386-115">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="b2386-115">Username</span></span>
* <span data-ttu-id="b2386-116">Hasło</span><span class="sxs-lookup"><span data-stu-id="b2386-116">Password</span></span>
* <span data-ttu-id="b2386-117">Domyślna baza danych (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="b2386-117">Default database (optional)</span></span>

<span data-ttu-id="b2386-118">Domyślnie połączenie łączy się z *wzorca* bazy danych, a nie bazy danych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="b2386-118">By default your connection connects to the *master* database and not your user database.</span></span> <span data-ttu-id="b2386-119">Aby połączyć się z bazą danych użytkownika, można wykonać jedną z następujących:</span><span class="sxs-lookup"><span data-stu-id="b2386-119">To connect to your user database, you can choose to do one of two things:</span></span>

* <span data-ttu-id="b2386-120">Określ domyślną bazę danych podczas rejestrowania serwera w Eksploratorze obiektów SQL Server programu SSDT, SSMS, lub w ciągu połączenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b2386-120">Specify the default database when registering your server with the SQL Server Object Explorer in SSDT, SSMS, or in your application connection string.</span></span> <span data-ttu-id="b2386-121">Na przykład dodać parametr InitialCatalog dla połączenia ODBC.</span><span class="sxs-lookup"><span data-stu-id="b2386-121">For example, include the InitialCatalog parameter for an ODBC connection.</span></span>
* <span data-ttu-id="b2386-122">Przed utworzeniem sesji programu SSDT, zaznacz bazy danych użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b2386-122">Highlight the user database before creating a session in SSDT.</span></span>

> [!NOTE]
> <span data-ttu-id="b2386-123">Wykonywanie instrukcji języka Transact-SQL **mojabazadanych UŻYJ;** nie jest obsługiwana dla Zmiana bazy danych dla połączenia.</span><span class="sxs-lookup"><span data-stu-id="b2386-123">The Transact-SQL statement **USE MyDatabase;** is not supported for changing the database for a connection.</span></span> <span data-ttu-id="b2386-124">Wskazówki dotyczące nawiązywania połączenia z usługi SQL Data Warehouse z narzędziami SSDT można odwoływać się do [zapytania z programem Visual Studio] [ Query with Visual Studio] artykułu.</span><span class="sxs-lookup"><span data-stu-id="b2386-124">For guidance connecting to SQL Data Warehouse with SSDT, refer to the [Query with Visual Studio][Query with Visual Studio] article.</span></span>
> 
> 

## <a name="azure-active-directory-aad-authentication"></a><span data-ttu-id="b2386-125">Uwierzytelnianie usługi Azure Active Directory (AAD)</span><span class="sxs-lookup"><span data-stu-id="b2386-125">Azure Active Directory (AAD) authentication</span></span>
<span data-ttu-id="b2386-126">[Usługa Azure Active Directory] [ What is Azure Active Directory] uwierzytelnianie jest mechanizmu nawiązywania połączenia z programu Microsoft Azure SQL Data Warehouse przy użyciu tożsamości w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b2386-126">[Azure Active Directory][What is Azure Active Directory] authentication is a mechanism of connecting to Microsoft Azure SQL Data Warehouse by using identities in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="b2386-127">Przy użyciu uwierzytelniania usługi Azure Active Directory mogą centralnie zarządzać tożsamości użytkowników bazy danych i innych usług firmy Microsoft w jednej centralnej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="b2386-127">With Azure Active Directory authentication, you can centrally manage the identities of database users and other Microsoft services in one central location.</span></span> <span data-ttu-id="b2386-128">Centralne zarządzanie identyfikator udostępnia jedno miejsce do zarządzania użytkownikami usługi SQL Data Warehouse i upraszcza zarządzanie uprawnieniami.</span><span class="sxs-lookup"><span data-stu-id="b2386-128">Central ID management provides a single place to manage SQL Data Warehouse users and simplifies permission management.</span></span> 

### <a name="benefits"></a><span data-ttu-id="b2386-129">Korzyści</span><span class="sxs-lookup"><span data-stu-id="b2386-129">Benefits</span></span>
<span data-ttu-id="b2386-130">Azure Active Directory korzyści:</span><span class="sxs-lookup"><span data-stu-id="b2386-130">Azure Active Directory benefits include:</span></span>

* <span data-ttu-id="b2386-131">Stanowi alternatywę dla uwierzytelniania programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b2386-131">Provides an alternative to SQL Server authentication.</span></span>
* <span data-ttu-id="b2386-132">Pomaga zatrzymać rozprzestrzenianie tożsamości użytkowników na serwerach bazy danych.</span><span class="sxs-lookup"><span data-stu-id="b2386-132">Helps stop the proliferation of user identities across database servers.</span></span>
* <span data-ttu-id="b2386-133">Umożliwia obrotu hasła w jednym miejscu</span><span class="sxs-lookup"><span data-stu-id="b2386-133">Allows password rotation in a single place</span></span>
* <span data-ttu-id="b2386-134">Zarządzaj uprawnieniami bazy danych przy użyciu zewnętrznego grup (AAD).</span><span class="sxs-lookup"><span data-stu-id="b2386-134">Manage database permissions using external (AAD) groups.</span></span>
* <span data-ttu-id="b2386-135">Eliminuje zapisywania haseł przez włączenie zintegrowanego uwierzytelniania systemu Windows i innych metod uwierzytelniania obsługiwanych przez usługę Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b2386-135">Eliminates storing passwords by enabling integrated Windows authentication and other forms of authentication supported by Azure Active Directory.</span></span>
* <span data-ttu-id="b2386-136">Używa zawarte bazy danych użytkowników do uwierzytelniania tożsamości na poziomie bazy danych.</span><span class="sxs-lookup"><span data-stu-id="b2386-136">Uses contained database users to authenticate identities at the database level.</span></span>
* <span data-ttu-id="b2386-137">Obsługuje uwierzytelnianie na podstawie tokenu dla aplikacji nawiązywania połączenia z usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="b2386-137">Supports token-based authentication for applications connecting to SQL Data Warehouse.</span></span>
* <span data-ttu-id="b2386-138">Obsługuje uwierzytelnianie wieloskładnikowe za pomocą uwierzytelniania uniwersalnego usługi Active Directory dla programu SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="b2386-138">Supports Multi-Factor authentication through Active Directory Universal Authentication for SQL Server Management Studio.</span></span> <span data-ttu-id="b2386-139">Opis usługi Multi-Factor Authentication, zobacz [SSMS obsługę usługi Azure AD MFA z bazy danych SQL i usługi SQL Data Warehouse](../sql-database/sql-database-ssms-mfa-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b2386-139">For a description of Multi-Factor Authentication, see [SSMS support for Azure AD MFA with SQL Database and SQL Data Warehouse](../sql-database/sql-database-ssms-mfa-authentication.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b2386-140">Azure Active Directory jest nadal stosunkowo nowe i ma pewne ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="b2386-140">Azure Active Directory is still relatively new and has some limitations.</span></span> <span data-ttu-id="b2386-141">Aby upewnić się, że usługi Azure Active Directory jest odpowiedni dla danego środowiska, zobacz [funkcje usługi Azure AD i ograniczenia][Azure AD features and limitations], w szczególności dodatkowe zagadnienia.</span><span class="sxs-lookup"><span data-stu-id="b2386-141">To ensure that Azure Active Directory is a good fit for your environment, see [Azure AD features and limitations][Azure AD features and limitations], specifically the Additional considerations.</span></span>
> 
> 

### <a name="configuration-steps"></a><span data-ttu-id="b2386-142">Kroki konfiguracji</span><span class="sxs-lookup"><span data-stu-id="b2386-142">Configuration steps</span></span>
<span data-ttu-id="b2386-143">Wykonaj następujące kroki, aby skonfigurować uwierzytelnianie w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b2386-143">Follow these steps to configure Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="b2386-144">Utworzyć i wypełnić usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b2386-144">Create and populate an Azure Active Directory</span></span>
2. <span data-ttu-id="b2386-145">Opcjonalnie: Skojarz lub zmienić usługi active directory, który jest aktualnie powiązany z subskrypcją platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b2386-145">Optional: Associate or change the active directory that is currently associated with your Azure Subscription</span></span>
3. <span data-ttu-id="b2386-146">Utwórz administrator usługi Azure Active Directory dla usługi Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="b2386-146">Create an Azure Active Directory administrator for Azure SQL Data Warehouse.</span></span>
4. <span data-ttu-id="b2386-147">Konfigurowanie komputerów klienckich</span><span class="sxs-lookup"><span data-stu-id="b2386-147">Configure your client computers</span></span>
5. <span data-ttu-id="b2386-148">Utwórz użytkowników zawartej bazy danych w bazie danych mapowany na tożsamość usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b2386-148">Create contained database users in your database mapped to Azure AD identities</span></span>
6. <span data-ttu-id="b2386-149">Połącz do magazynu danych przy użyciu tożsamości usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b2386-149">Connect to your data warehouse by using Azure AD identities</span></span>

<span data-ttu-id="b2386-150">Obecnie użytkownicy usługi Azure Active Directory nie są wyświetlane w Eksploratorze obiektów program SSDT.</span><span class="sxs-lookup"><span data-stu-id="b2386-150">Currently Azure Active Directory users are not shown in SSDT Object Explorer.</span></span> <span data-ttu-id="b2386-151">Jako obejście, wyświetlania informacji o użytkownikach w [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).</span><span class="sxs-lookup"><span data-stu-id="b2386-151">As a workaround, view the users in [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).</span></span>

### <a name="find-the-details"></a><span data-ttu-id="b2386-152">Znajdź szczegóły</span><span class="sxs-lookup"><span data-stu-id="b2386-152">Find the details</span></span>
* <span data-ttu-id="b2386-153">Kroki konfigurowania i korzystania z uwierzytelniania usługi Azure Active Directory są niemal identyczne dla usługi Azure SQL Database i Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="b2386-153">The steps to configure and use Azure Active Directory authentication are nearly identical for Azure SQL Database and Azure SQL Data Warehouse.</span></span> <span data-ttu-id="b2386-154">Wykonaj szczegółowe kroki opisane w temacie [połączenie z bazą danych SQL lub SQL danych magazynu przy użyciu Azure uwierzytelnianie usługi Active Directory](../sql-database/sql-database-aad-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b2386-154">Follow the detailed steps in the topic [Connecting to SQL Database or SQL Data Warehouse By Using Azure Active Directory Authentication](../sql-database/sql-database-aad-authentication.md).</span></span>
* <span data-ttu-id="b2386-155">Tworzenie ról w niestandardowej bazie danych i dodawanie użytkowników do ról.</span><span class="sxs-lookup"><span data-stu-id="b2386-155">Create custom database roles and add users to the roles.</span></span> <span data-ttu-id="b2386-156">Następnie przydziel szczegółowe uprawnienia do ról.</span><span class="sxs-lookup"><span data-stu-id="b2386-156">Then grant granular permissions to the roles.</span></span> <span data-ttu-id="b2386-157">Aby uzyskać więcej informacji, zobacz [wprowadzenie do korzystania z bazy danych aparatu uprawnień](https://msdn.microsoft.com/library/mt667986.aspx).</span><span class="sxs-lookup"><span data-stu-id="b2386-157">For more information, see [Getting Started with Database Engine Permissions](https://msdn.microsoft.com/library/mt667986.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b2386-158">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b2386-158">Next steps</span></span>
<span data-ttu-id="b2386-159">Aby uruchomić zapytanie magazynu danych z programu Visual Studio i innymi aplikacjami, zobacz [zapytania z programem Visual Studio][Query with Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="b2386-159">To start querying your data warehouse with Visual Studio and other applications, see [Query with Visual Studio][Query with Visual Studio].</span></span>

<!-- Article references -->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md
[What is Azure Active Directory]: ../active-directory/active-directory-whatis.md
[Azure AD features and limitations]: ../sql-database/sql-database-aad-authentication.md#azure-ad-features-and-limitations
