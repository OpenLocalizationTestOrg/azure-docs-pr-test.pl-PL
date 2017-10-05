---
title: "Zarządzanie ról bazy danych i użytkowników w usłudze Azure Analysis Services | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zarządzać ról bazy danych i użytkowników na serwerze usług Analysis Services na platformie Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: d0bc7d7514f111b4bbde33bd60ae21264bd797fc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="manage-database-roles-and-users"></a><span data-ttu-id="07177-103">Zarządzanie ról bazy danych i użytkowników</span><span class="sxs-lookup"><span data-stu-id="07177-103">Manage database roles and users</span></span>

<span data-ttu-id="07177-104">Na poziomie bazy danych modelu wszyscy użytkownicy muszą należeć do roli.</span><span class="sxs-lookup"><span data-stu-id="07177-104">At the model database level, all users must belong to a role.</span></span> <span data-ttu-id="07177-105">Role definiują użytkowników z uprawnieniami określonego dla bazy danych modelu.</span><span class="sxs-lookup"><span data-stu-id="07177-105">Roles define users with particular permissions for the model database.</span></span> <span data-ttu-id="07177-106">Dowolnemu użytkownikowi lub grupie zabezpieczeń dodany do roli musi mieć konto w dzierżawie usługi Azure AD w tej samej subskrypcji co serwer.</span><span class="sxs-lookup"><span data-stu-id="07177-106">Any user or security group added to a role must have an account in an Azure AD tenant in the same subscription as the server.</span></span>

<span data-ttu-id="07177-107">Sposób definiowania ról różni się w zależności od używanego narzędzia, ale efekt jest taki sam.</span><span class="sxs-lookup"><span data-stu-id="07177-107">How you define roles is different depending on the tool you use, but the effect is the same.</span></span>

<span data-ttu-id="07177-108">Uprawnienia roli obejmują:</span><span class="sxs-lookup"><span data-stu-id="07177-108">Role permissions include:</span></span>
*  <span data-ttu-id="07177-109">**Administrator** — użytkownicy mają pełne uprawnienia do bazy danych.</span><span class="sxs-lookup"><span data-stu-id="07177-109">**Administrator** - Users have full permissions for the database.</span></span> <span data-ttu-id="07177-110">Role bazy danych z uprawnieniami administratora różnią się od administratorów serwera.</span><span class="sxs-lookup"><span data-stu-id="07177-110">Database roles with Administrator permissions are different from server administrators.</span></span>
*  <span data-ttu-id="07177-111">**Proces** — użytkownicy mogą połączyć się z wykonywać operacje przetwarzania w bazie danych i analizowanie danych bazy danych modelu.</span><span class="sxs-lookup"><span data-stu-id="07177-111">**Process** - Users can connect to and perform process operations on the database, and analyze model database data.</span></span>
*  <span data-ttu-id="07177-112">**Odczyt** — użytkownicy mogą używać aplikacji klienta do nawiązania połączenia i analizowania danych bazy danych modelu.</span><span class="sxs-lookup"><span data-stu-id="07177-112">**Read** -  Users can use a client application to connect to and analyze model database data.</span></span>

<span data-ttu-id="07177-113">Podczas tworzenia projektu modelu tabelarycznego, tworzyć role i dodać użytkowników lub grupy do tych ról za pomocą menedżera ról programu SSDT.</span><span class="sxs-lookup"><span data-stu-id="07177-113">When creating a tabular model project, you create roles and add users or groups to those roles by using Role Manager in SSDT.</span></span> <span data-ttu-id="07177-114">Po wdrożeniu na serwerze, użyj narzędzia SSMS, [poleceń cmdlet programu PowerShell usługi analizy](https://msdn.microsoft.com/library/hh758425.aspx), lub [język skryptów modelu tabelarycznego](https://msdn.microsoft.com/library/mt614797.aspx) (TMSL), aby dodać lub usunąć role i członkowie.</span><span class="sxs-lookup"><span data-stu-id="07177-114">When deployed to a server, you use SSMS, [Analysis Services PowerShell cmdlets](https://msdn.microsoft.com/library/hh758425.aspx), or [Tabular Model Scripting Language](https://msdn.microsoft.com/library/mt614797.aspx) (TMSL) to add or remove roles and user members.</span></span>

## <a name="to-add-or-manage-roles-and-users-in-ssdt"></a><span data-ttu-id="07177-115">Aby dodać lub zarządzania rolami i użytkownicy programu SSDT</span><span class="sxs-lookup"><span data-stu-id="07177-115">To add or manage roles and users in SSDT</span></span>  
  
1.  <span data-ttu-id="07177-116">Programu SSDT > **Eksplorator modelu tabelarycznego**, kliknij prawym przyciskiem myszy **ról**.</span><span class="sxs-lookup"><span data-stu-id="07177-116">In SSDT > **Tabular Model Explorer**, right-click **Roles**.</span></span>  
  
2.  <span data-ttu-id="07177-117">W **Menedżerze ról** kliknij przycisk **Nowa**.</span><span class="sxs-lookup"><span data-stu-id="07177-117">In **Role Manager**, click **New**.</span></span>  
  
3.  <span data-ttu-id="07177-118">Wpisz nazwę roli.</span><span class="sxs-lookup"><span data-stu-id="07177-118">Type a name for the role.</span></span>  
  
     <span data-ttu-id="07177-119">Domyślnie nazwa domyślna rola jest przyrostowo numerowane dla każdej nowej roli.</span><span class="sxs-lookup"><span data-stu-id="07177-119">By default, the name of the default role is incrementally numbered for each new role.</span></span> <span data-ttu-id="07177-120">Zaleca się, że wpisz nazwę, która jasno identyfikuje typ elementu członkowskiego, na przykład menedżerów finansowych lub specjalistami w zasoby ludzkie.</span><span class="sxs-lookup"><span data-stu-id="07177-120">It's recommended you type a name that clearly identifies the member type, for example, Finance Managers or Human Resources Specialists.</span></span>  
  
4.  <span data-ttu-id="07177-121">Wybierz jedną z następujących uprawnień:</span><span class="sxs-lookup"><span data-stu-id="07177-121">Select one of the following permissions:</span></span>  
  
    |<span data-ttu-id="07177-122">Uprawnienie</span><span class="sxs-lookup"><span data-stu-id="07177-122">Permission</span></span>|<span data-ttu-id="07177-123">Opis</span><span class="sxs-lookup"><span data-stu-id="07177-123">Description</span></span>|  
    |----------------|-----------------|  
    |<span data-ttu-id="07177-124">**Brak**</span><span class="sxs-lookup"><span data-stu-id="07177-124">**None**</span></span>|<span data-ttu-id="07177-125">Elementy członkowskie nie można zmodyfikować schematu modelu i nie można wykonać zapytania na danych.</span><span class="sxs-lookup"><span data-stu-id="07177-125">Members cannot modify the model schema and cannot query data.</span></span>|  
    |<span data-ttu-id="07177-126">**Odczyt**</span><span class="sxs-lookup"><span data-stu-id="07177-126">**Read**</span></span>|<span data-ttu-id="07177-127">Członkowie mogą zapytania na danych (w oparciu filtrów wierszy), ale nie można zmodyfikować schematu modelu.</span><span class="sxs-lookup"><span data-stu-id="07177-127">Members can query data (based on row filters) but cannot modify the model schema.</span></span>|  
    |<span data-ttu-id="07177-128">**Odczyt i procesu**</span><span class="sxs-lookup"><span data-stu-id="07177-128">**Read and Process**</span></span>|<span data-ttu-id="07177-129">Elementy członkowskie danych (oparte na poziomie wiersza filtry) oraz wykonywania operacji procesu i przetwórz wszystko można zapytania, ale nie można zmodyfikować schematu modelu.</span><span class="sxs-lookup"><span data-stu-id="07177-129">Members can query data (based on row-level filters) and run Process and Process All operations, but cannot modify the model schema.</span></span>|  
    |<span data-ttu-id="07177-130">**Proces**</span><span class="sxs-lookup"><span data-stu-id="07177-130">**Process**</span></span>|<span data-ttu-id="07177-131">Elementy członkowskie można uruchomić proces i procesu wszystkie operacje.</span><span class="sxs-lookup"><span data-stu-id="07177-131">Members can run Process and Process All operations.</span></span> <span data-ttu-id="07177-132">Nie można zmodyfikować schematu modelu i nie można wykonać zapytania na danych.</span><span class="sxs-lookup"><span data-stu-id="07177-132">Cannot modify the model schema and cannot query data.</span></span>|  
    |<span data-ttu-id="07177-133">**Administrator**</span><span class="sxs-lookup"><span data-stu-id="07177-133">**Administrator**</span></span>|<span data-ttu-id="07177-134">Elementy członkowskie można zmodyfikować schematu modelu i wyszukiwać wszystkie dane.</span><span class="sxs-lookup"><span data-stu-id="07177-134">Members can modify the model schema and query all data.</span></span>|   
  
5.  <span data-ttu-id="07177-135">W przypadku roli tworzenie ma odczytu lub uprawnienia odczytu i procesu, można dodać filtrów wierszy przy użyciu formuły języka DAX.</span><span class="sxs-lookup"><span data-stu-id="07177-135">If the role you are creating has Read or Read and Process permission, you can add row filters by using a DAX formula.</span></span> <span data-ttu-id="07177-136">Kliknij przycisk **filtrów wierszy** , a następnie wybierz tabelę, a następnie kliknij **filtru DAX** pola, a następnie wpisz formułę języka DAX.</span><span class="sxs-lookup"><span data-stu-id="07177-136">Click the **Row Filters** tab, then select a table, then click the **DAX Filter** field, and then type a DAX formula.</span></span>
  
6.  <span data-ttu-id="07177-137">Kliknij przycisk **członków** > **Dodaj zewnętrzne**.</span><span class="sxs-lookup"><span data-stu-id="07177-137">Click **Members** > **Add External**.</span></span>  
  
8.  <span data-ttu-id="07177-138">W **dodawania zewnętrznego członka**, wprowadź użytkowników lub grup w dzierżawie usługi Azure AD za pomocą adresu e-mail.</span><span class="sxs-lookup"><span data-stu-id="07177-138">In **Add External Member**, enter users or groups in your tenant Azure AD by email address.</span></span> <span data-ttu-id="07177-139">Po kliknij przycisk OK i zamknąć Menedżera ról, ról i członkowie roli są widoczne w Eksploratorze modelu tabelarycznego.</span><span class="sxs-lookup"><span data-stu-id="07177-139">After you click OK and close Role Manager, roles and role members appear in Tabular Model Explorer.</span></span> 
 
     ![Role i użytkownicy w Eksploratorze modelu tabelarycznego](./media/analysis-services-database-users/aas-roles-tmexplorer.png)

9. <span data-ttu-id="07177-141">Wdrażanie z serwerem usług Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="07177-141">Deploy to your Azure Analysis Services server.</span></span>


## <a name="to-add-or-manage-roles-and-users-in-ssms"></a><span data-ttu-id="07177-142">Aby dodać lub zarządzania rolami i użytkowników w programie SSMS</span><span class="sxs-lookup"><span data-stu-id="07177-142">To add or manage roles and users in SSMS</span></span>
<span data-ttu-id="07177-143">Dodawanie ról i użytkowników do bazy danych modelu wdrożone, można musi być połączone z serwerem administrator serwera lub jest już w roli bazy danych z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="07177-143">To add roles and users to a deployed model database, you must be connected to the server as a Server administrator or already in a database role with administrator permissions.</span></span>

1. <span data-ttu-id="07177-144">W obiekcie Exporer, kliknij prawym przyciskiem myszy **ról** > **nową rolę**.</span><span class="sxs-lookup"><span data-stu-id="07177-144">In Object Exporer, right-click **Roles** > **New Role**.</span></span>

2. <span data-ttu-id="07177-145">W **Utwórz rolę**, wprowadź nazwę roli i opis.</span><span class="sxs-lookup"><span data-stu-id="07177-145">In **Create Role**, enter a role name and description.</span></span>

3. <span data-ttu-id="07177-146">Wybierz uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="07177-146">Select a permission.</span></span>
   |<span data-ttu-id="07177-147">Uprawnienie</span><span class="sxs-lookup"><span data-stu-id="07177-147">Permission</span></span>|<span data-ttu-id="07177-148">Opis</span><span class="sxs-lookup"><span data-stu-id="07177-148">Description</span></span>|  
   |----------------|-----------------|  
   |<span data-ttu-id="07177-149">**Pełna kontrola (Administrator)**</span><span class="sxs-lookup"><span data-stu-id="07177-149">**Full control (Administrator)**</span></span>|<span data-ttu-id="07177-150">Członkowie mogą modyfikować schematu modelu przetwarzania i można zbadać wszystkie dane.</span><span class="sxs-lookup"><span data-stu-id="07177-150">Members can modify the model schema, process, and can query all data.</span></span>| 
   |<span data-ttu-id="07177-151">**Proces bazy danych**</span><span class="sxs-lookup"><span data-stu-id="07177-151">**Process database**</span></span>|<span data-ttu-id="07177-152">Elementy członkowskie można uruchomić proces i procesu wszystkie operacje.</span><span class="sxs-lookup"><span data-stu-id="07177-152">Members can run Process and Process All operations.</span></span> <span data-ttu-id="07177-153">Nie można zmodyfikować schematu modelu i nie można wykonać zapytania na danych.</span><span class="sxs-lookup"><span data-stu-id="07177-153">Cannot modify the model schema and cannot query data.</span></span>|  
   |<span data-ttu-id="07177-154">**Odczyt**</span><span class="sxs-lookup"><span data-stu-id="07177-154">**Read**</span></span>|<span data-ttu-id="07177-155">Członkowie mogą zapytania na danych (w oparciu filtrów wierszy), ale nie można zmodyfikować schematu modelu.</span><span class="sxs-lookup"><span data-stu-id="07177-155">Members can query data (based on row filters) but cannot modify the model schema.</span></span>|  
  
4. <span data-ttu-id="07177-156">Kliknij przycisk **członkostwa**, wprowadź użytkownika lub grupy w dzierżawie usługi Azure AD za pomocą adresu e-mail.</span><span class="sxs-lookup"><span data-stu-id="07177-156">Click **Membership**, then enter a user or group in your tenant Azure AD by email address.</span></span>

     ![Dodawanie użytkownika](./media/analysis-services-database-users/aas-roles-adduser-ssms.png)

5. <span data-ttu-id="07177-158">Jeśli rola tworzonego ma uprawnień do odczytu, możesz dodać filtrów wierszy przy użyciu formuły języka DAX.</span><span class="sxs-lookup"><span data-stu-id="07177-158">If the role you are creating has Read permission, you can add row filters by using a DAX formula.</span></span> <span data-ttu-id="07177-159">Kliknij przycisk **filtrów wierszy**, wybierz tabelę, a następnie wpisz formułę języka DAX w **filtru DAX** pola.</span><span class="sxs-lookup"><span data-stu-id="07177-159">Click **Row Filters**, select a table, and then type a DAX formula in the **DAX Filter** field.</span></span> 

## <a name="to-add-roles-and-users-by-using-a-tmsl-script"></a><span data-ttu-id="07177-160">Dodawanie ról i użytkowników przy użyciu skryptu TMSL</span><span class="sxs-lookup"><span data-stu-id="07177-160">To add roles and users by using a TMSL script</span></span>
<span data-ttu-id="07177-161">W oknie XMLA w programie SSMS lub przy użyciu programu PowerShell, należy uruchomić skrypt TMSL.</span><span class="sxs-lookup"><span data-stu-id="07177-161">You can run a TMSL script in the XMLA window in SSMS or by using PowerShell.</span></span> <span data-ttu-id="07177-162">Użyj [CreateOrReplace](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl) polecenia i [ról](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl) obiektu.</span><span class="sxs-lookup"><span data-stu-id="07177-162">Use the [CreateOrReplace](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl) command and the [Roles](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl) object.</span></span>

<span data-ttu-id="07177-163">**Przykładowy skrypt TMSL**</span><span class="sxs-lookup"><span data-stu-id="07177-163">**Sample TMSL script**</span></span>

<span data-ttu-id="07177-164">W tym przykładzie użytkownik zewnętrzny B2B i grupy są dodawane do roli analityk z uprawnieniami odczytu SalesBI bazy danych.</span><span class="sxs-lookup"><span data-stu-id="07177-164">In this sample, a B2B external user and a group are added to the Analyst role with Read permissions for the SalesBI database.</span></span> <span data-ttu-id="07177-165">Zarówno użytkownika zewnętrznego, jak i grupa musi być w tej samej dzierżawy usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07177-165">Both the external user and group must be in same tenant Azure AD.</span></span>

```
{
  "createOrReplace": {
    "object": {
      "database": "SalesBI",
      "role": "Analyst"
    },
    "role": {
      "name": "Users",
      "description": "All allowed users to query the model",
      "modelPermission": "read",
      "members": [
        {
          "memberName": "user1@contoso.com",
          "identityProvider": "AzureAD"
        },
        {
          "memberName": "group1@adventureworks.com",
          "identityProvider": "AzureAD"
        }
      ]
    }
  }
}
```

## <a name="to-add-roles-and-users-by-using-powershell"></a><span data-ttu-id="07177-166">Dodawanie ról i użytkowników przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="07177-166">To add roles and users by using PowerShell</span></span>
<span data-ttu-id="07177-167">[SqlServer](https://msdn.microsoft.com/library/hh758425.aspx) modułu udostępnia polecenia cmdlet do bazy danych specyficznych dla zadań zarządzania i cmdlet Invoke-ASCmd ogólnego przeznaczenia akceptuje zapytań tabelarycznych modelu skryptów języka (TMSL) lub skryptu.</span><span class="sxs-lookup"><span data-stu-id="07177-167">The [SqlServer](https://msdn.microsoft.com/library/hh758425.aspx) module provides task-specific database management cmdlets and the general-purpose Invoke-ASCmd cmdlet that accepts a Tabular Model Scripting Language (TMSL) query or script.</span></span> <span data-ttu-id="07177-168">Następujące polecenia cmdlet są używane do zarządzania rolami bazy danych i użytkowników.</span><span class="sxs-lookup"><span data-stu-id="07177-168">The following cmdlets are used for managing database roles and users.</span></span>
  
|<span data-ttu-id="07177-169">Polecenie cmdlet</span><span class="sxs-lookup"><span data-stu-id="07177-169">Cmdlet</span></span>|<span data-ttu-id="07177-170">Opis</span><span class="sxs-lookup"><span data-stu-id="07177-170">Description</span></span>|
|------------|-----------------| 
|[<span data-ttu-id="07177-171">Dodaj RoleMember</span><span class="sxs-lookup"><span data-stu-id="07177-171">Add-RoleMember</span></span>](https://msdn.microsoft.com/library/hh510167.aspx)|<span data-ttu-id="07177-172">Dodaj członka do roli bazy danych.</span><span class="sxs-lookup"><span data-stu-id="07177-172">Add a member to a database role.</span></span>| 
|[<span data-ttu-id="07177-173">Usuń RoleMember</span><span class="sxs-lookup"><span data-stu-id="07177-173">Remove-RoleMember</span></span>](https://msdn.microsoft.com/library/hh510173.aspx)|<span data-ttu-id="07177-174">Usuwanie członka z roli bazy danych.</span><span class="sxs-lookup"><span data-stu-id="07177-174">Remove a member from a database role.</span></span>|   
|[<span data-ttu-id="07177-175">Wywołanie ASCmd</span><span class="sxs-lookup"><span data-stu-id="07177-175">Invoke-ASCmd</span></span>](https://msdn.microsoft.com/library/hh479579.aspx)|<span data-ttu-id="07177-176">Wykonanie skryptu TMSL.</span><span class="sxs-lookup"><span data-stu-id="07177-176">Execute a TMSL script.</span></span>|

## <a name="row-filters"></a><span data-ttu-id="07177-177">Filtrów wierszy</span><span class="sxs-lookup"><span data-stu-id="07177-177">Row filters</span></span>  
<span data-ttu-id="07177-178">Filtry wiersza definiują, które wiersze w tabeli mogą być przeszukiwane przez członków określonej roli.</span><span class="sxs-lookup"><span data-stu-id="07177-178">Row filters define which rows in a table can be queried by members of a particular role.</span></span> <span data-ttu-id="07177-179">Filtrów wierszy są definiowane dla każdej tabeli w modelu przy użyciu formuły języka DAX.</span><span class="sxs-lookup"><span data-stu-id="07177-179">Row filters are defined for each table in a model by using DAX formulas.</span></span>  
  
<span data-ttu-id="07177-180">Filtrów wierszy można zdefiniować tylko do odczytu i odczytu ról i uprawnień procesu.</span><span class="sxs-lookup"><span data-stu-id="07177-180">Row filters can be defined only for roles with Read and Read and Process permissions.</span></span> <span data-ttu-id="07177-181">Domyślnie jeśli filtr wiersza nie jest zdefiniowany dla danej tabeli, elementy Członkowskie mogą wysyłać zapytania wszystkie wiersze w tabeli, chyba że filtrowania krzyżowego stosuje z innej tabeli.</span><span class="sxs-lookup"><span data-stu-id="07177-181">By default, if a row filter is not defined for a particular table, members  can query all rows in the table unless cross-filtering applies from another table.</span></span>
  
 <span data-ttu-id="07177-182">Filtry wiersza wymagają formuły języka DAX musi zwrócić wartość TRUE/FALSE, aby określić wiersze, które mogą być przeszukiwane przez członków tej konkretnej roli.</span><span class="sxs-lookup"><span data-stu-id="07177-182">Row filters require a DAX formula, which must evaluate to a TRUE/FALSE value, to define the rows that can be queried by members of that particular role.</span></span> <span data-ttu-id="07177-183">Nie można zbadać wierszy, które nie są uwzględnione w formule języka DAX.</span><span class="sxs-lookup"><span data-stu-id="07177-183">Rows not included in the DAX formula cannot be queried.</span></span> <span data-ttu-id="07177-184">Na przykład tabela klientów o następujący wiersz filtruje wyrażenia *= klientów [Kraj] = "USA"*, członkowie roli sprzedaży może zobaczyć tylko klientów w USA.</span><span class="sxs-lookup"><span data-stu-id="07177-184">For example, the Customers table with the following row filters expression, *=Customers [Country] = “USA”*, members of the Sales role can only see customers in the USA.</span></span>  
  
<span data-ttu-id="07177-185">Filtrów wierszy są stosowane do określonych wierszy i powiązane wiersze.</span><span class="sxs-lookup"><span data-stu-id="07177-185">Row filters apply to the specified rows and related rows.</span></span> <span data-ttu-id="07177-186">Tabela ma wiele relacji, filtry stosowane zabezpieczeń dla relacji, który jest aktywny.</span><span class="sxs-lookup"><span data-stu-id="07177-186">When a table has multiple relationships, filters apply security for the relationship that is active.</span></span> <span data-ttu-id="07177-187">Filtrów wierszy są zakończone z innych filtrach wiersza zdefiniowane dla powiązane tabele, na przykład:</span><span class="sxs-lookup"><span data-stu-id="07177-187">Row filters are intersected with other row filers defined for related tables, for example:</span></span>  
  
|<span data-ttu-id="07177-188">Tabela</span><span class="sxs-lookup"><span data-stu-id="07177-188">Table</span></span>|<span data-ttu-id="07177-189">Wyrażenie DAX</span><span class="sxs-lookup"><span data-stu-id="07177-189">DAX expression</span></span>|  
|-----------|--------------------|  
|<span data-ttu-id="07177-190">Region</span><span class="sxs-lookup"><span data-stu-id="07177-190">Region</span></span>|<span data-ttu-id="07177-191">= Region [Kraj] = "USA"</span><span class="sxs-lookup"><span data-stu-id="07177-191">=Region[Country]=”USA”</span></span>|  
|<span data-ttu-id="07177-192">ProductCategory</span><span class="sxs-lookup"><span data-stu-id="07177-192">ProductCategory</span></span>|<span data-ttu-id="07177-193">= ProductCategory [nazwa] = "Rowerów"</span><span class="sxs-lookup"><span data-stu-id="07177-193">=ProductCategory[Name]=”Bicycles”</span></span>|  
|<span data-ttu-id="07177-194">Transakcje</span><span class="sxs-lookup"><span data-stu-id="07177-194">Transactions</span></span>|<span data-ttu-id="07177-195">= Transakcje [rok] = 2016</span><span class="sxs-lookup"><span data-stu-id="07177-195">=Transactions[Year]=2016</span></span>|  
  
 <span data-ttu-id="07177-196">Net powoduje, że członkowie można zbadać wiersze danych, gdy klient jest w USA, Kategoria produktu jest rowerów i rok jest 2016.</span><span class="sxs-lookup"><span data-stu-id="07177-196">The net effect is members can query rows of data where the customer is in the USA, the product category is bicycles, and the year is 2016.</span></span> <span data-ttu-id="07177-197">Użytkownicy nie mogą badać transakcji poza USA, transakcje, które nie znajdują się nie rowerów lub transakcji w 2016, chyba że są one członkiem innej roli, która udziela te uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="07177-197">Users cannot query transactions outside of the USA, transactions that are not bicycles, or transactions not in 2016 unless they are a member of another role that grants these permissions.</span></span>
  
 <span data-ttu-id="07177-198">Możesz użyć opcji Filtruj *=FALSE()*, aby odmówić dostępu do wszystkich wierszy dla całej tabeli.</span><span class="sxs-lookup"><span data-stu-id="07177-198">You can use the filter, *=FALSE()*, to deny access to all rows for an entire table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="07177-199">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="07177-199">Next steps</span></span>
  <span data-ttu-id="07177-200">[Administratorzy serwerów zarządzania](analysis-services-server-admins.md) </span><span class="sxs-lookup"><span data-stu-id="07177-200">[Manage server administrators](analysis-services-server-admins.md) </span></span>  
  [<span data-ttu-id="07177-201">Zarządzanie usług Azure Analysis Services przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="07177-201">Manage Azure Analysis Services with PowerShell</span></span>](analysis-services-powershell.md)  
  [<span data-ttu-id="07177-202">Model tabelaryczny skryptów materiały referencyjne dotyczące języka (TMSL)</span><span class="sxs-lookup"><span data-stu-id="07177-202">Tabular Model Scripting Language (TMSL) Reference</span></span>](https://docs.microsoft.com/sql/analysis-services/tabular-model-scripting-language-tmsl-reference)

