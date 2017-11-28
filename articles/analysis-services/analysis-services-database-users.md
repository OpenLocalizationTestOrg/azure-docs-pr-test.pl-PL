---
title: "aaaManage bazy danych, ról i użytkowników w usłudze Azure Analysis Services | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomanage bazy danych, ról i użytkowników na serwerze usług Analysis Services na platformie Azure."
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
ms.openlocfilehash: 2ad069a6bcce11bc43347625cb32ec400d48af18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-database-roles-and-users"></a><span data-ttu-id="c6ed4-103">Zarządzanie ról bazy danych i użytkowników</span><span class="sxs-lookup"><span data-stu-id="c6ed4-103">Manage database roles and users</span></span>

<span data-ttu-id="c6ed4-104">Na poziomie bazy danych modelu hello wszyscy użytkownicy muszą należeć tooa roli.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-104">At hello model database level, all users must belong tooa role.</span></span> <span data-ttu-id="c6ed4-105">Role definiują użytkowników z uprawnieniami określonego dla hello bazy danych modelu.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-105">Roles define users with particular permissions for hello model database.</span></span> <span data-ttu-id="c6ed4-106">Dowolnego użytkownika lub grupy zabezpieczeń dodaje tooa roli musi mieć konto w dzierżawie usługi Azure AD w hello tej samej subskrypcji co powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-106">Any user or security group added tooa role must have an account in an Azure AD tenant in hello same subscription as hello server.</span></span>

<span data-ttu-id="c6ed4-107">Sposób definiowania ról jest różne w zależności od używanego narzędzia hello, ale wpływ hello jest hello takie same.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-107">How you define roles is different depending on hello tool you use, but hello effect is hello same.</span></span>

<span data-ttu-id="c6ed4-108">Uprawnienia roli obejmują:</span><span class="sxs-lookup"><span data-stu-id="c6ed4-108">Role permissions include:</span></span>
*  <span data-ttu-id="c6ed4-109">**Administrator** — użytkownicy mają pełne uprawnienia do hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-109">**Administrator** - Users have full permissions for hello database.</span></span> <span data-ttu-id="c6ed4-110">Role bazy danych z uprawnieniami administratora różnią się od administratorów serwera.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-110">Database roles with Administrator permissions are different from server administrators.</span></span>
*  <span data-ttu-id="c6ed4-111">**Proces** — użytkownicy mogą nawiązywać połączenie tooand wykonanie procesu na powitania bazy danych i analizowanie danych bazy danych modelu.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-111">**Process** - Users can connect tooand perform process operations on hello database, and analyze model database data.</span></span>
*  <span data-ttu-id="c6ed4-112">**Odczyt** — użytkownicy mogą używać klienta aplikacji tooconnect tooand analizowanie danych bazy danych modelu.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-112">**Read** -  Users can use a client application tooconnect tooand analyze model database data.</span></span>

<span data-ttu-id="c6ed4-113">Podczas tworzenia projektu modelu tabelarycznego, tworzyć role i Dodawanie ról toothose użytkowników lub grup za pomocą menedżera ról programu SSDT.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-113">When creating a tabular model project, you create roles and add users or groups toothose roles by using Role Manager in SSDT.</span></span> <span data-ttu-id="c6ed4-114">Wdrożone tooa serwera, korzystając SSMS, [poleceń cmdlet programu PowerShell usługi analizy](https://msdn.microsoft.com/library/hh758425.aspx), lub [język skryptów modelu tabelarycznego](https://msdn.microsoft.com/library/mt614797.aspx) tooadd (TMSL) lub usuwania ról i członkowie.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-114">When deployed tooa server, you use SSMS, [Analysis Services PowerShell cmdlets](https://msdn.microsoft.com/library/hh758425.aspx), or [Tabular Model Scripting Language](https://msdn.microsoft.com/library/mt614797.aspx) (TMSL) tooadd or remove roles and user members.</span></span>

## <a name="tooadd-or-manage-roles-and-users-in-ssdt"></a><span data-ttu-id="c6ed4-115">tooadd lub zarządzania rolami i użytkownicy programu SSDT</span><span class="sxs-lookup"><span data-stu-id="c6ed4-115">tooadd or manage roles and users in SSDT</span></span>  
  
1.  <span data-ttu-id="c6ed4-116">Programu SSDT > **Eksplorator modelu tabelarycznego**, kliknij prawym przyciskiem myszy **ról**.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-116">In SSDT > **Tabular Model Explorer**, right-click **Roles**.</span></span>  
  
2.  <span data-ttu-id="c6ed4-117">W **Menedżerze ról** kliknij przycisk **Nowa**.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-117">In **Role Manager**, click **New**.</span></span>  
  
3.  <span data-ttu-id="c6ed4-118">Wpisz nazwę roli hello.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-118">Type a name for hello role.</span></span>  
  
     <span data-ttu-id="c6ed4-119">Domyślnie nazwa hello hello domyślnej roli jest przyrostowo numerowane dla każdej nowej roli.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-119">By default, hello name of hello default role is incrementally numbered for each new role.</span></span> <span data-ttu-id="c6ed4-120">Zaleca się, że wpisz nazwę, która jasno identyfikuje typ elementu członkowskiego hello, na przykład menedżerów finansowych lub specjalistami w zasoby ludzkie.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-120">It's recommended you type a name that clearly identifies hello member type, for example, Finance Managers or Human Resources Specialists.</span></span>  
  
4.  <span data-ttu-id="c6ed4-121">Wybierz jedną z następujących uprawnień hello:</span><span class="sxs-lookup"><span data-stu-id="c6ed4-121">Select one of hello following permissions:</span></span>  
  
    |<span data-ttu-id="c6ed4-122">Uprawnienie</span><span class="sxs-lookup"><span data-stu-id="c6ed4-122">Permission</span></span>|<span data-ttu-id="c6ed4-123">Opis</span><span class="sxs-lookup"><span data-stu-id="c6ed4-123">Description</span></span>|  
    |----------------|-----------------|  
    |<span data-ttu-id="c6ed4-124">**Brak**</span><span class="sxs-lookup"><span data-stu-id="c6ed4-124">**None**</span></span>|<span data-ttu-id="c6ed4-125">Elementy członkowskie nie można zmodyfikować schematu modelu hello i nie można wykonać zapytania na danych.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-125">Members cannot modify hello model schema and cannot query data.</span></span>|  
    |<span data-ttu-id="c6ed4-126">**Odczyt**</span><span class="sxs-lookup"><span data-stu-id="c6ed4-126">**Read**</span></span>|<span data-ttu-id="c6ed4-127">Elementy członkowskie można zbadać danych (w oparciu filtrów wierszy), ale nie można zmodyfikować schematu modelu hello.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-127">Members can query data (based on row filters) but cannot modify hello model schema.</span></span>|  
    |<span data-ttu-id="c6ed4-128">**Odczyt i procesu**</span><span class="sxs-lookup"><span data-stu-id="c6ed4-128">**Read and Process**</span></span>|<span data-ttu-id="c6ed4-129">Elementy członkowskie danych (oparte na poziomie wiersza filtry) oraz wykonywania operacji procesu i przetwórz wszystko można zapytania, ale nie można zmodyfikować schematu modelu hello.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-129">Members can query data (based on row-level filters) and run Process and Process All operations, but cannot modify hello model schema.</span></span>|  
    |<span data-ttu-id="c6ed4-130">**Proces**</span><span class="sxs-lookup"><span data-stu-id="c6ed4-130">**Process**</span></span>|<span data-ttu-id="c6ed4-131">Elementy członkowskie można uruchomić proces i procesu wszystkie operacje.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-131">Members can run Process and Process All operations.</span></span> <span data-ttu-id="c6ed4-132">Nie można zmodyfikować schematu modelu hello i nie można wykonać zapytania na danych.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-132">Cannot modify hello model schema and cannot query data.</span></span>|  
    |<span data-ttu-id="c6ed4-133">**Administrator**</span><span class="sxs-lookup"><span data-stu-id="c6ed4-133">**Administrator**</span></span>|<span data-ttu-id="c6ed4-134">Elementy członkowskie można zmodyfikować schematu modelu hello i wyszukiwać wszystkie dane.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-134">Members can modify hello model schema and query all data.</span></span>|   
  
5.  <span data-ttu-id="c6ed4-135">W przypadku roli hello tworzenie ma odczytu lub uprawnienia odczytu i procesu, można dodać filtrów wierszy przy użyciu formuły języka DAX.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-135">If hello role you are creating has Read or Read and Process permission, you can add row filters by using a DAX formula.</span></span> <span data-ttu-id="c6ed4-136">Kliknij przycisk hello **filtrów wierszy** , a następnie wybierz tabelę, a następnie kliknij hello **filtru DAX** pola, a następnie wpisz formułę języka DAX.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-136">Click hello **Row Filters** tab, then select a table, then click hello **DAX Filter** field, and then type a DAX formula.</span></span>
  
6.  <span data-ttu-id="c6ed4-137">Kliknij przycisk **członków** > **Dodaj zewnętrzne**.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-137">Click **Members** > **Add External**.</span></span>  
  
8.  <span data-ttu-id="c6ed4-138">W **dodawania zewnętrznego członka**, wprowadź użytkowników lub grup w dzierżawie usługi Azure AD za pomocą adresu e-mail.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-138">In **Add External Member**, enter users or groups in your tenant Azure AD by email address.</span></span> <span data-ttu-id="c6ed4-139">Po kliknij przycisk OK i zamknąć Menedżera ról, ról i członkowie roli są widoczne w Eksploratorze modelu tabelarycznego.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-139">After you click OK and close Role Manager, roles and role members appear in Tabular Model Explorer.</span></span> 
 
     ![Role i użytkownicy w Eksploratorze modelu tabelarycznego](./media/analysis-services-database-users/aas-roles-tmexplorer.png)

9. <span data-ttu-id="c6ed4-141">Wdrażanie tooyour serwera usług Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-141">Deploy tooyour Azure Analysis Services server.</span></span>


## <a name="tooadd-or-manage-roles-and-users-in-ssms"></a><span data-ttu-id="c6ed4-142">tooadd lub zarządzania rolami i użytkowników w programie SSMS</span><span class="sxs-lookup"><span data-stu-id="c6ed4-142">tooadd or manage roles and users in SSMS</span></span>
<span data-ttu-id="c6ed4-143">tooadd ról i użytkowników tooa wdrożone bazy danych modelu, musi być toohello podłączonego serwera, administrator serwera lub jest już w roli bazy danych z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-143">tooadd roles and users tooa deployed model database, you must be connected toohello server as a Server administrator or already in a database role with administrator permissions.</span></span>

1. <span data-ttu-id="c6ed4-144">W obiekcie Exporer, kliknij prawym przyciskiem myszy **ról** > **nową rolę**.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-144">In Object Exporer, right-click **Roles** > **New Role**.</span></span>

2. <span data-ttu-id="c6ed4-145">W **Utwórz rolę**, wprowadź nazwę roli i opis.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-145">In **Create Role**, enter a role name and description.</span></span>

3. <span data-ttu-id="c6ed4-146">Wybierz uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-146">Select a permission.</span></span>
   |<span data-ttu-id="c6ed4-147">Uprawnienie</span><span class="sxs-lookup"><span data-stu-id="c6ed4-147">Permission</span></span>|<span data-ttu-id="c6ed4-148">Opis</span><span class="sxs-lookup"><span data-stu-id="c6ed4-148">Description</span></span>|  
   |----------------|-----------------|  
   |<span data-ttu-id="c6ed4-149">**Pełna kontrola (Administrator)**</span><span class="sxs-lookup"><span data-stu-id="c6ed4-149">**Full control (Administrator)**</span></span>|<span data-ttu-id="c6ed4-150">Członkowie mogą modyfikować schematu modelu hello, przetwarzania i można zbadać wszystkie dane.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-150">Members can modify hello model schema, process, and can query all data.</span></span>| 
   |<span data-ttu-id="c6ed4-151">**Proces bazy danych**</span><span class="sxs-lookup"><span data-stu-id="c6ed4-151">**Process database**</span></span>|<span data-ttu-id="c6ed4-152">Elementy członkowskie można uruchomić proces i procesu wszystkie operacje.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-152">Members can run Process and Process All operations.</span></span> <span data-ttu-id="c6ed4-153">Nie można zmodyfikować schematu modelu hello i nie można wykonać zapytania na danych.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-153">Cannot modify hello model schema and cannot query data.</span></span>|  
   |<span data-ttu-id="c6ed4-154">**Odczyt**</span><span class="sxs-lookup"><span data-stu-id="c6ed4-154">**Read**</span></span>|<span data-ttu-id="c6ed4-155">Elementy członkowskie można zbadać danych (w oparciu filtrów wierszy), ale nie można zmodyfikować schematu modelu hello.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-155">Members can query data (based on row filters) but cannot modify hello model schema.</span></span>|  
  
4. <span data-ttu-id="c6ed4-156">Kliknij przycisk **członkostwa**, wprowadź użytkownika lub grupy w dzierżawie usługi Azure AD za pomocą adresu e-mail.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-156">Click **Membership**, then enter a user or group in your tenant Azure AD by email address.</span></span>

     ![Dodawanie użytkownika](./media/analysis-services-database-users/aas-roles-adduser-ssms.png)

5. <span data-ttu-id="c6ed4-158">Jeśli rola hello, które tworzysz ma uprawnień do odczytu, możesz dodać filtrów wierszy przy użyciu formuły języka DAX.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-158">If hello role you are creating has Read permission, you can add row filters by using a DAX formula.</span></span> <span data-ttu-id="c6ed4-159">Kliknij przycisk **filtrów wierszy**, wybierz tabelę, a następnie wpisz formułę języka DAX w hello **filtru DAX** pola.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-159">Click **Row Filters**, select a table, and then type a DAX formula in hello **DAX Filter** field.</span></span> 

## <a name="tooadd-roles-and-users-by-using-a-tmsl-script"></a><span data-ttu-id="c6ed4-160">tooadd ról i użytkowników przy użyciu skryptu TMSL</span><span class="sxs-lookup"><span data-stu-id="c6ed4-160">tooadd roles and users by using a TMSL script</span></span>
<span data-ttu-id="c6ed4-161">W oknie XMLA hello w programie SSMS lub przy użyciu programu PowerShell, należy uruchomić skrypt TMSL.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-161">You can run a TMSL script in hello XMLA window in SSMS or by using PowerShell.</span></span> <span data-ttu-id="c6ed4-162">Użyj hello [CreateOrReplace](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl) polecenia i hello [ról](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl) obiektu.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-162">Use hello [CreateOrReplace](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl) command and hello [Roles](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl) object.</span></span>

<span data-ttu-id="c6ed4-163">**Przykładowy skrypt TMSL**</span><span class="sxs-lookup"><span data-stu-id="c6ed4-163">**Sample TMSL script**</span></span>

<span data-ttu-id="c6ed4-164">W tym przykładzie użytkownik zewnętrzny B2B i grupy są dodawane rola analityka toohello o uprawnienia do odczytu dla bazy danych SalesBI hello.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-164">In this sample, a B2B external user and a group are added toohello Analyst role with Read permissions for hello SalesBI database.</span></span> <span data-ttu-id="c6ed4-165">Zarówno hello użytkownika zewnętrznego i grupy musi być w tej samej dzierżawy usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-165">Both hello external user and group must be in same tenant Azure AD.</span></span>

```
{
  "createOrReplace": {
    "object": {
      "database": "SalesBI",
      "role": "Analyst"
    },
    "role": {
      "name": "Users",
      "description": "All allowed users tooquery hello model",
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

## <a name="tooadd-roles-and-users-by-using-powershell"></a><span data-ttu-id="c6ed4-166">tooadd ról i użytkowników przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="c6ed4-166">tooadd roles and users by using PowerShell</span></span>
<span data-ttu-id="c6ed4-167">Witaj [SqlServer](https://msdn.microsoft.com/library/hh758425.aspx) moduł dostarcza bazy danych specyficznych dla zadań zarządzania poleceń cmdlet i hello ogólnego przeznaczenia Invoke ASCmd polecenia cmdlet, które akceptuje zapytań tabelarycznych modelu skryptów języka (TMSL) lub skryptu.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-167">hello [SqlServer](https://msdn.microsoft.com/library/hh758425.aspx) module provides task-specific database management cmdlets and hello general-purpose Invoke-ASCmd cmdlet that accepts a Tabular Model Scripting Language (TMSL) query or script.</span></span> <span data-ttu-id="c6ed4-168">następujące polecenia cmdlet Hello są używane do zarządzania ról bazy danych i użytkowników.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-168">hello following cmdlets are used for managing database roles and users.</span></span>
  
|<span data-ttu-id="c6ed4-169">Polecenie cmdlet</span><span class="sxs-lookup"><span data-stu-id="c6ed4-169">Cmdlet</span></span>|<span data-ttu-id="c6ed4-170">Opis</span><span class="sxs-lookup"><span data-stu-id="c6ed4-170">Description</span></span>|
|------------|-----------------| 
|[<span data-ttu-id="c6ed4-171">Dodaj RoleMember</span><span class="sxs-lookup"><span data-stu-id="c6ed4-171">Add-RoleMember</span></span>](https://msdn.microsoft.com/library/hh510167.aspx)|<span data-ttu-id="c6ed4-172">Dodaj element członkowski tooa roli bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-172">Add a member tooa database role.</span></span>| 
|[<span data-ttu-id="c6ed4-173">Usuń RoleMember</span><span class="sxs-lookup"><span data-stu-id="c6ed4-173">Remove-RoleMember</span></span>](https://msdn.microsoft.com/library/hh510173.aspx)|<span data-ttu-id="c6ed4-174">Usuwanie członka z roli bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-174">Remove a member from a database role.</span></span>|   
|[<span data-ttu-id="c6ed4-175">Wywołanie ASCmd</span><span class="sxs-lookup"><span data-stu-id="c6ed4-175">Invoke-ASCmd</span></span>](https://msdn.microsoft.com/library/hh479579.aspx)|<span data-ttu-id="c6ed4-176">Wykonanie skryptu TMSL.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-176">Execute a TMSL script.</span></span>|

## <a name="row-filters"></a><span data-ttu-id="c6ed4-177">Filtrów wierszy</span><span class="sxs-lookup"><span data-stu-id="c6ed4-177">Row filters</span></span>  
<span data-ttu-id="c6ed4-178">Filtry wiersza definiują, które wiersze w tabeli mogą być przeszukiwane przez członków określonej roli.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-178">Row filters define which rows in a table can be queried by members of a particular role.</span></span> <span data-ttu-id="c6ed4-179">Filtrów wierszy są definiowane dla każdej tabeli w modelu przy użyciu formuły języka DAX.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-179">Row filters are defined for each table in a model by using DAX formulas.</span></span>  
  
<span data-ttu-id="c6ed4-180">Filtrów wierszy można zdefiniować tylko do odczytu i odczytu ról i uprawnień procesu.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-180">Row filters can be defined only for roles with Read and Read and Process permissions.</span></span> <span data-ttu-id="c6ed4-181">Domyślnie jeśli filtr wiersza nie jest zdefiniowany dla danej tabeli, elementy Członkowskie mogą wysyłać zapytania wszystkie wiersze w tabeli hello, chyba że filtrowania krzyżowego stosuje z innej tabeli.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-181">By default, if a row filter is not defined for a particular table, members  can query all rows in hello table unless cross-filtering applies from another table.</span></span>
  
 <span data-ttu-id="c6ed4-182">Filtry wiersza wymagają formuły języka DAX, musi ocenić tooa wartość PRAWDA/FAŁSZ, toodefine hello wierszy, które mogą być przeszukiwane przez członków tej konkretnej roli.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-182">Row filters require a DAX formula, which must evaluate tooa TRUE/FALSE value, toodefine hello rows that can be queried by members of that particular role.</span></span> <span data-ttu-id="c6ed4-183">Nie można zbadać wierszy, które nie są objęte hello formuły języka DAX.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-183">Rows not included in hello DAX formula cannot be queried.</span></span> <span data-ttu-id="c6ed4-184">Na przykład Witaj tabeli klientów z hello następującego wyrażenia filtrów wiersza, *= klientów [Kraj] = "USA"*, członkowie roli sprzedaży hello może zobaczyć tylko klientów z hello USA.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-184">For example, hello Customers table with hello following row filters expression, *=Customers [Country] = “USA”*, members of hello Sales role can only see customers in hello USA.</span></span>  
  
<span data-ttu-id="c6ed4-185">Stosowane filtry wiersza toohello określone wiersze i powiązane wiersze.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-185">Row filters apply toohello specified rows and related rows.</span></span> <span data-ttu-id="c6ed4-186">Tabela ma wiele relacji, filtry stosowane zabezpieczenia hello relacji, który jest aktywny.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-186">When a table has multiple relationships, filters apply security for hello relationship that is active.</span></span> <span data-ttu-id="c6ed4-187">Filtrów wierszy są zakończone z innych filtrach wiersza zdefiniowane dla powiązane tabele, na przykład:</span><span class="sxs-lookup"><span data-stu-id="c6ed4-187">Row filters are intersected with other row filers defined for related tables, for example:</span></span>  
  
|<span data-ttu-id="c6ed4-188">Tabela</span><span class="sxs-lookup"><span data-stu-id="c6ed4-188">Table</span></span>|<span data-ttu-id="c6ed4-189">Wyrażenie DAX</span><span class="sxs-lookup"><span data-stu-id="c6ed4-189">DAX expression</span></span>|  
|-----------|--------------------|  
|<span data-ttu-id="c6ed4-190">Region</span><span class="sxs-lookup"><span data-stu-id="c6ed4-190">Region</span></span>|<span data-ttu-id="c6ed4-191">= Region [Kraj] = "USA"</span><span class="sxs-lookup"><span data-stu-id="c6ed4-191">=Region[Country]=”USA”</span></span>|  
|<span data-ttu-id="c6ed4-192">ProductCategory</span><span class="sxs-lookup"><span data-stu-id="c6ed4-192">ProductCategory</span></span>|<span data-ttu-id="c6ed4-193">= ProductCategory [nazwa] = "Rowerów"</span><span class="sxs-lookup"><span data-stu-id="c6ed4-193">=ProductCategory[Name]=”Bicycles”</span></span>|  
|<span data-ttu-id="c6ed4-194">Transakcje</span><span class="sxs-lookup"><span data-stu-id="c6ed4-194">Transactions</span></span>|<span data-ttu-id="c6ed4-195">= Transakcje [rok] = 2016</span><span class="sxs-lookup"><span data-stu-id="c6ed4-195">=Transactions[Year]=2016</span></span>|  
  
 <span data-ttu-id="c6ed4-196">Efekt netto Hello jest członków można zbadać wiersze danych, gdzie powitania klienta znajduje się w hello USA, Kategoria produktu hello jest rowerów i rok hello jest 2016.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-196">hello net effect is members can query rows of data where hello customer is in hello USA, hello product category is bicycles, and hello year is 2016.</span></span> <span data-ttu-id="c6ed4-197">Użytkownicy nie mogą badać transakcji poza hello USA, transakcje, które nie znajdują się nie rowerów lub transakcji w 2016, chyba że są one członkiem innej roli, która udziela te uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-197">Users cannot query transactions outside of hello USA, transactions that are not bicycles, or transactions not in 2016 unless they are a member of another role that grants these permissions.</span></span>
  
 <span data-ttu-id="c6ed4-198">Możesz użyć opcji Filtruj hello *=FALSE()*, toodeny dostępu tooall wierszy dla całej tabeli.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-198">You can use hello filter, *=FALSE()*, toodeny access tooall rows for an entire table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6ed4-199">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c6ed4-199">Next steps</span></span>
  <span data-ttu-id="c6ed4-200">[Administratorzy serwerów zarządzania](analysis-services-server-admins.md) </span><span class="sxs-lookup"><span data-stu-id="c6ed4-200">[Manage server administrators](analysis-services-server-admins.md) </span></span>  
  [<span data-ttu-id="c6ed4-201">Zarządzanie usług Azure Analysis Services przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="c6ed4-201">Manage Azure Analysis Services with PowerShell</span></span>](analysis-services-powershell.md)  
  [<span data-ttu-id="c6ed4-202">Model tabelaryczny skryptów materiały referencyjne dotyczące języka (TMSL)</span><span class="sxs-lookup"><span data-stu-id="c6ed4-202">Tabular Model Scripting Language (TMSL) Reference</span></span>](https://docs.microsoft.com/sql/analysis-services/tabular-model-scripting-language-tmsl-reference)

