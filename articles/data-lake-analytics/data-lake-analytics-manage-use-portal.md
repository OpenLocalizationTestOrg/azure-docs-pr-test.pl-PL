---
title: "aaaManage Azure Data Lake Analytics przy użyciu hello portalu Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomanage kont usługi Data Lake Analytics, danych źródła, użytkowników i zadania."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: a0e045f1-73d6-427f-868d-7b55c10f811b
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: f63ccdfae79772c92e92462194e8cdc636a73dc6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-by-using-hello-azure-portal"></a><span data-ttu-id="2b5b4-103">Zarządzanie usługą Azure Data Lake Analytics przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="2b5b4-103">Manage Azure Data Lake Analytics by using hello Azure portal</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="2b5b4-104">Dowiedz się, jak toomanage kont usługi Azure Data Lake Analytics, źródłami danych konta użytkowników i zadań za pomocą hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-104">Learn how toomanage Azure Data Lake Analytics accounts, account data sources, users, and jobs by using hello Azure portal.</span></span> <span data-ttu-id="2b5b4-105">Tematy dotyczące zarządzania toosee o przy użyciu innych narzędzi, kliknij kartę u góry hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-105">toosee management topics about using other tools, click a tab at hello top of hello page.</span></span>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-lake-analytics-accounts"></a><span data-ttu-id="2b5b4-106">Zarządzanie kontami usługi Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="2b5b4-106">Manage Data Lake Analytics accounts</span></span>

### <a name="create-an-account"></a><span data-ttu-id="2b5b4-107">Tworzenie konta usługi</span><span class="sxs-lookup"><span data-stu-id="2b5b4-107">Create an account</span></span>

1. <span data-ttu-id="2b5b4-108">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2b5b4-108">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="2b5b4-109">Kliknij przycisk **Nowy** > **Zbieranie danych i analiza** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-109">Click **New** > **Intelligence + analytics** > **Data Lake Analytics**.</span></span>
3. <span data-ttu-id="2b5b4-110">Wybierz wartości hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="2b5b4-110">Select values for hello following items:</span></span> 
   1. <span data-ttu-id="2b5b4-111">**Nazwa**: Nazwa hello hello konta usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-111">**Name**: hello name of hello Data Lake Analytics account.</span></span>
   2. <span data-ttu-id="2b5b4-112">**Subskrypcja**: hello używane jako konto hello subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-112">**Subscription**: hello Azure subscription used for hello account.</span></span>
   3. <span data-ttu-id="2b5b4-113">**Grupa zasobów**: hello grupy zasobów platformy Azure, w które konto hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-113">**Resource Group**: hello Azure resource group in which toocreate hello account.</span></span> 
   4. <span data-ttu-id="2b5b4-114">**Lokalizacja**: hello centrum danych Azure dla konta usługi Data Lake Analytics hello.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-114">**Location**: hello Azure datacenter for hello Data Lake Analytics account.</span></span> 
   5. <span data-ttu-id="2b5b4-115">**Data Lake Store**: hello toobe magazynu domyślne używane jako konto usługi Data Lake Analytics hello.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-115">**Data Lake Store**: hello default store toobe used for hello Data Lake Analytics account.</span></span> <span data-ttu-id="2b5b4-116">Konto usługi Azure Data Lake Store Hello i hello musi należeć do konta usługi Data Lake Analytics hello tej samej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-116">hello Azure Data Lake Store account and hello Data Lake Analytics account must be in hello same location.</span></span>
4. <span data-ttu-id="2b5b4-117">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-117">Click **Create**.</span></span> 

### <a name="delete-a-data-lake-analytics-account"></a><span data-ttu-id="2b5b4-118">Usuwanie konta usługi Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="2b5b4-118">Delete a Data Lake Analytics account</span></span>

<span data-ttu-id="2b5b4-119">Aby usunąć konto usługi Data Lake Analytics, usuń jego domyślne konto usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-119">Before you delete a Data Lake Analytics account, delete its default Data Lake Store account.</span></span>

1. <span data-ttu-id="2b5b4-120">W hello portalu Azure Przejdź tooyour konta usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-120">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="2b5b4-121">Kliknij polecenie **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-121">Click **Delete**.</span></span>
3. <span data-ttu-id="2b5b4-122">Nazwa konta hello typu.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-122">Type hello account name.</span></span>
4. <span data-ttu-id="2b5b4-123">Kliknij polecenie **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-123">Click **Delete**.</span></span>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-sources"></a><span data-ttu-id="2b5b4-124">Zarządzaj źródłami danych</span><span class="sxs-lookup"><span data-stu-id="2b5b4-124">Manage data sources</span></span>

<span data-ttu-id="2b5b4-125">Data Lake Analytics obsługuje hello następujące źródła danych:</span><span class="sxs-lookup"><span data-stu-id="2b5b4-125">Data Lake Analytics supports hello following data sources:</span></span>

* <span data-ttu-id="2b5b4-126">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="2b5b4-126">Data Lake Store</span></span>
* <span data-ttu-id="2b5b4-127">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="2b5b4-127">Azure Storage</span></span>

<span data-ttu-id="2b5b4-128">Można używać źródeł danych toobrowse Eksploratora danych i wykonywać operacje zarządzania pliku podstawowego.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-128">You can use Data Explorer toobrowse data sources and perform basic file management operations.</span></span> 

### <a name="add-a-data-source"></a><span data-ttu-id="2b5b4-129">Dodawanie źródła danych</span><span class="sxs-lookup"><span data-stu-id="2b5b4-129">Add a data source</span></span>

1. <span data-ttu-id="2b5b4-130">W hello portalu Azure Przejdź tooyour konta usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-130">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="2b5b4-131">Kliknij przycisk **źródeł danych**.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-131">Click **Data Sources**.</span></span>
3. <span data-ttu-id="2b5b4-132">Kliknij przycisk **Dodaj źródło danych**.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-132">Click **Add Data Source**.</span></span>
    
   * <span data-ttu-id="2b5b4-133">tooadd konto usługi Data Lake Store, musisz mieć konto hello toohello nazwy i dostępu do konta toobe tooquery mogli go.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-133">tooadd a Data Lake Store account, you need hello account name and access toohello account toobe able tooquery it.</span></span>
   * <span data-ttu-id="2b5b4-134">tooadd magazynu obiektów Blob platformy Azure, należy hello konto magazynu i klucza konta hello.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-134">tooadd Azure Blob storage, you need hello storage account and hello account key.</span></span> <span data-ttu-id="2b5b4-135">toofind konta magazynu toohello ich, przejdź w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-135">toofind them, go toohello storage account in hello portal.</span></span>

## <a name="set-up-firewall-rules"></a><span data-ttu-id="2b5b4-136">Konfigurowanie reguł zapory</span><span class="sxs-lookup"><span data-stu-id="2b5b4-136">Set up firewall rules</span></span>

<span data-ttu-id="2b5b4-137">Data Lake Analytics toofurther blokowania tooyour dostępu do konta usługi Data Lake Analytics można użyć na poziomie sieci hello.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-137">You can use Data Lake Analytics toofurther lock down access tooyour Data Lake Analytics account at hello network level.</span></span> <span data-ttu-id="2b5b4-138">Można włączyć zapory, podaj adres IP lub zdefiniuj zakres adresów IP dla zaufanych klientów.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-138">You can enable a firewall, specify an IP address, or define an IP address range for your trusted clients.</span></span> <span data-ttu-id="2b5b4-139">Po włączeniu tych środków tylko klientów, którzy mają hello adresów IP w zakresie hello zdefiniowane można połączyć toohello magazynu.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-139">After you enable these measures, only clients that have hello IP addresses within hello defined range can connect toohello store.</span></span>

<span data-ttu-id="2b5b4-140">Jeśli innymi usługami Azure, takich jak fabryki danych Azure lub maszyn wirtualnych, połączyć konto usługi Data Lake Analytics toohello, upewnij się, że **Zezwalaj usług Azure** włączono **na**.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-140">If other Azure services, like Azure Data Factory or VMs, connect toohello Data Lake Analytics account, make sure that **Allow Azure Services** is turned **On**.</span></span> 

### <a name="set-up-a-firewall-rule"></a><span data-ttu-id="2b5b4-141">Konfigurowanie reguł zapory</span><span class="sxs-lookup"><span data-stu-id="2b5b4-141">Set up a firewall rule</span></span>

1. <span data-ttu-id="2b5b4-142">W hello portalu Azure Przejdź tooyour konta usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-142">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="2b5b4-143">Polecenie hello menu po lewej stronie powitania **zapory**.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-143">On hello menu on hello left, click **Firewall**.</span></span>

## <a name="add-a-new-user"></a><span data-ttu-id="2b5b4-144">Dodaj nowego użytkownika</span><span class="sxs-lookup"><span data-stu-id="2b5b4-144">Add a new user</span></span>

<span data-ttu-id="2b5b4-145">Można użyć hello **Kreatora dodawania użytkownika** tooeasily obsługi administracyjnej nowych użytkowników do usługi Data Lake.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-145">You can use hello **Add User Wizard** tooeasily provision new Data Lake users.</span></span>

1. <span data-ttu-id="2b5b4-146">W hello portalu Azure Przejdź tooyour konta usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-146">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="2b5b4-147">Na powitania po lewej, w obszarze **wprowadzenie**, kliknij przycisk **Kreatora dodawania użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-147">On hello left, under **Getting Started**, click **Add User Wizard**.</span></span>
3. <span data-ttu-id="2b5b4-148">Wybierz użytkownika, a następnie kliknij przycisk **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-148">Select a user, and then click **Select**.</span></span>
4. <span data-ttu-id="2b5b4-149">Wybierz rolę, a następnie kliknij przycisk **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-149">Select a role, and then click **Select**.</span></span> <span data-ttu-id="2b5b4-150">tooset się nowych toouse dewelopera usługi Azure Data Lake, wybierz hello **Data Lake Analytics Developer** roli.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-150">tooset up a new developer toouse Azure Data Lake, select hello **Data Lake Analytics Developer** role.</span></span>
5. <span data-ttu-id="2b5b4-151">Wybierz z listy kontroli dostępu hello (kontroli dostępu ACL) dla baz danych hello U-SQL.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-151">Select hello access control lists (ACLs) for hello U-SQL databases.</span></span> <span data-ttu-id="2b5b4-152">Po zakończeniu wybrane opcje, kliknij przycisk **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-152">When you're satisfied with your choices, click **Select**.</span></span>
6. <span data-ttu-id="2b5b4-153">Wybierz hello listy kontroli dostępu dla plików.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-153">Select hello ACLs for files.</span></span> <span data-ttu-id="2b5b4-154">Witaj domyślny magazyn, nie zmieniaj hello listy kontroli dostępu dla folderu głównego hello "/" i hello/system folderu.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-154">For hello default store, don't change hello ACLs for hello root folder "/" and for hello /system folder.</span></span> <span data-ttu-id="2b5b4-155">Kliknij pozycję **Wybierz**.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-155">Click **Select**.</span></span>
7. <span data-ttu-id="2b5b4-156">Przejrzyj wybrane ustawienia, a następnie kliknij przycisk **Uruchom**.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-156">Review all your selected changes, and then click **Run**.</span></span>
8. <span data-ttu-id="2b5b4-157">Po zakończeniu pracy Kreatora powitania kliknij przycisk **gotowe**.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-157">When hello wizard is finished, click **Done**.</span></span>

## <a name="manage-role-based-access-control"></a><span data-ttu-id="2b5b4-158">Zarządzanie kontrolą dostępu opartą na rolach</span><span class="sxs-lookup"><span data-stu-id="2b5b4-158">Manage Role-Based Access Control</span></span>

<span data-ttu-id="2b5b4-159">Podobnie jak innymi usługami Azure można użyć toocontrol kontroli dostępu opartej na rolach (RBAC) interakcji użytkowników z usługą hello.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-159">Like other Azure services, you can use Role-Based Access Control (RBAC) toocontrol how users interact with hello service.</span></span>

<span data-ttu-id="2b5b4-160">standardowe role RBAC Hello mają hello następujące możliwości:</span><span class="sxs-lookup"><span data-stu-id="2b5b4-160">hello standard RBAC roles have hello following capabilities:</span></span>
* <span data-ttu-id="2b5b4-161">**Właściciel**: można przesyłania zadań, monitorowania zadań anulować zadania z dowolnego użytkownika i skonfigurować konto hello.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-161">**Owner**: Can submit jobs, monitor jobs, cancel jobs from any user, and configure hello account.</span></span>
* <span data-ttu-id="2b5b4-162">**Współautor**: można przesyłania zadań, monitorowania zadań anulować zadania z dowolnego użytkownika i skonfigurować konto hello.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-162">**Contributor**: Can submit jobs, monitor jobs, cancel jobs from any user, and configure hello account.</span></span>
* <span data-ttu-id="2b5b4-163">**Czytnik**: można monitorować zadania.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-163">**Reader**: Can monitor jobs.</span></span>

<span data-ttu-id="2b5b4-164">Za pomocą hello Data Lake Analytics Developer roli tooenable U-SQL deweloperzy toouse hello usługi Data Lake Analytics usługi.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-164">Use hello Data Lake Analytics Developer role tooenable U-SQL developers toouse hello Data Lake Analytics service.</span></span> <span data-ttu-id="2b5b4-165">Program hello Data Lake Analytics Developer rolę:</span><span class="sxs-lookup"><span data-stu-id="2b5b4-165">You can use hello Data Lake Analytics Developer role to:</span></span>
* <span data-ttu-id="2b5b4-166">Przesyłanie zadań.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-166">Submit jobs.</span></span>
* <span data-ttu-id="2b5b4-167">Monitorowania stanu i hello postępu zadania zadań wysłanego przez każdego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-167">Monitor job status and hello progress of jobs submitted by any user.</span></span>
* <span data-ttu-id="2b5b4-168">Zobacz hello skryptów U-SQL z zadań wysłanego przez każdego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-168">See hello U-SQL scripts from jobs submitted by any user.</span></span>
* <span data-ttu-id="2b5b4-169">Anulowanie tylko własnych zadań.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-169">Cancel only your own jobs.</span></span>

### <a name="add-users-or-security-groups-tooa-data-lake-analytics-account"></a><span data-ttu-id="2b5b4-170">Dodaj użytkowników lub tooa grup zabezpieczeń konta usługi Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="2b5b4-170">Add users or security groups tooa Data Lake Analytics account</span></span>

1. <span data-ttu-id="2b5b4-171">W hello portalu Azure Przejdź tooyour konta usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-171">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="2b5b4-172">Kliknij przycisk **(IAM) kontroli dostępu** > **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-172">Click **Access control (IAM)** > **Add**.</span></span>
3. <span data-ttu-id="2b5b4-173">Wybierz rolę.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-173">Select a role.</span></span>
4. <span data-ttu-id="2b5b4-174">Dodawanie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-174">Add a user.</span></span>
5. <span data-ttu-id="2b5b4-175">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-175">Click **OK**.</span></span>

>[!NOTE]
><span data-ttu-id="2b5b4-176">Jeśli użytkownik lub grupa zabezpieczeń wymaga toosubmit zadań, muszą uprawnienie hello konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-176">If a user or a security group needs toosubmit jobs, they also need permission on hello store account.</span></span> <span data-ttu-id="2b5b4-177">Aby uzyskać więcej informacji, zobacz [zabezpieczyć dane przechowywane w usłudze Data Lake Store](../data-lake-store/data-lake-store-secure-data.md).</span><span class="sxs-lookup"><span data-stu-id="2b5b4-177">For more information, see [Secure data stored in Data Lake Store](../data-lake-store/data-lake-store-secure-data.md).</span></span>
>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-jobs"></a><span data-ttu-id="2b5b4-178">Zarządzanie zadaniami</span><span class="sxs-lookup"><span data-stu-id="2b5b4-178">Manage jobs</span></span>

### <a name="submit-a-job"></a><span data-ttu-id="2b5b4-179">Prześlij zadanie</span><span class="sxs-lookup"><span data-stu-id="2b5b4-179">Submit a job</span></span>

1. <span data-ttu-id="2b5b4-180">W hello portalu Azure Przejdź tooyour konta usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-180">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>

2. <span data-ttu-id="2b5b4-181">Kliknij przycisk **nowe zadanie**.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-181">Click **New Job**.</span></span> <span data-ttu-id="2b5b4-182">Dla każdego zadania należy skonfigurować:</span><span class="sxs-lookup"><span data-stu-id="2b5b4-182">For each job,  configure:</span></span>

    1. <span data-ttu-id="2b5b4-183">**Nazwa zadania**: Nazwa hello hello zadania.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-183">**Job Name**: hello name of hello job.</span></span>
    2. <span data-ttu-id="2b5b4-184">**Priorytet**: niższych numerach mają wyższy priorytet.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-184">**Priority**: Lower numbers have higher priority.</span></span> <span data-ttu-id="2b5b4-185">Dwa zadania są umieszczane w kolejce, pierwszy uruchamia hello jedną z niższą wartość priorytetu.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-185">If two jobs are queued, hello one with lower priority value runs first.</span></span>
    3. <span data-ttu-id="2b5b4-186">**Równoległość**: Maksymalna liczba obliczeń hello procesów tooreserve dla tego zadania.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-186">**Parallelism**: hello maximum number of compute processes tooreserve for this job.</span></span>

3. <span data-ttu-id="2b5b4-187">Kliknij przycisk **Prześlij zadanie**.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-187">Click **Submit Job**.</span></span>

### <a name="monitor-jobs"></a><span data-ttu-id="2b5b4-188">Monitorowanie zadań</span><span class="sxs-lookup"><span data-stu-id="2b5b4-188">Monitor jobs</span></span>

1. <span data-ttu-id="2b5b4-189">W hello portalu Azure Przejdź tooyour konta usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-189">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="2b5b4-190">Kliknij przycisk **wyświetlić wszystkie zadania**.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-190">Click **View All Jobs**.</span></span> <span data-ttu-id="2b5b4-191">Listy wszystkich hello active i ostatnio zakończonych zadań na koncie hello jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-191">A list of all hello active and recently finished jobs in hello account is shown.</span></span>
3. <span data-ttu-id="2b5b4-192">Opcjonalnie kliknij **filtru** toohelp znaleźć hello zadania według **zakres czasu**, **Nazwa zadania**, i **autora** wartości.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-192">Optionally, click **Filter** toohelp you find hello jobs by **Time Range**, **Job Name**, and **Author** values.</span></span> 

### <a name="monitoring-pipeline-jobs"></a><span data-ttu-id="2b5b4-193">Monitorowanie zadań w potoku</span><span class="sxs-lookup"><span data-stu-id="2b5b4-193">Monitoring pipeline jobs</span></span>
<span data-ttu-id="2b5b4-194">Zadania, które są częścią potoku działają razem, zwykle po kolei, tooaccomplish danego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-194">Jobs that are part of a pipeline work together, usually sequentially, tooaccomplish a specific scenario.</span></span> <span data-ttu-id="2b5b4-195">Na przykład można mieć potok, który czyści, wyodrębnianie, przekształca, agreguje użycia klienta szczegółowe informacje o.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-195">For example, you can have a pipeline that cleans, extracts, transforms, aggregates usage for customer insights.</span></span> <span data-ttu-id="2b5b4-196">Potok zadania są identyfikowane za pomocą właściwości "Potoku" hello, gdy hello zadanie zostało przesłane.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-196">Pipeline jobs are identified using hello "Pipeline" property when hello job was submitted.</span></span> <span data-ttu-id="2b5b4-197">Zadania zaplanowane przy użyciu fabryki danych AZURE w wersji 2 ma automatycznie tej właściwości wypełnione.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-197">Jobs scheduled using ADF V2 will automatically have this property populated.</span></span> 

<span data-ttu-id="2b5b4-198">tooview listę zadań U-SQL, które są częścią potoków:</span><span class="sxs-lookup"><span data-stu-id="2b5b4-198">tooview a list of U-SQL jobs that are part of pipelines:</span></span> 

1. <span data-ttu-id="2b5b4-199">W hello portalu Azure Przejdź tooyour kont usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-199">In hello Azure portal, go tooyour Data Lake Analytics accounts.</span></span>
2. <span data-ttu-id="2b5b4-200">Kliknij przycisk **zadania Insights**.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-200">Click **Job Insights**.</span></span> <span data-ttu-id="2b5b4-201">powitalne kartę "Wszystkie zadania" zostanie przywrócona domyślna, przedstawiający listę uruchomiona, w kolejce i zakończenia zadania.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-201">hello "All Jobs" tab will be defaulted, showing a list of running, queued, and ended jobs.</span></span>
3. <span data-ttu-id="2b5b4-202">Kliknij przycisk hello **zadania potoku** kartę. Lista zadań potoku pojawi się wraz z zagregowanych danych statystycznych dla każdego potoku.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-202">Click hello **Pipeline Jobs** tab. A list of pipeline jobs will be shown along with aggregated statistics for each pipeline.</span></span>

### <a name="monitoring-recurring-jobs"></a><span data-ttu-id="2b5b4-203">Monitorowanie zadań cyklicznych</span><span class="sxs-lookup"><span data-stu-id="2b5b4-203">Monitoring recurring jobs</span></span>
<span data-ttu-id="2b5b4-204">Cyklicznych zadań to taki, który ma hello tej samej logiki biznesowej, ale używa innego danych wejściowych każdym uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-204">A recurring job is one that has hello same business logic but uses different input data every time it runs.</span></span> <span data-ttu-id="2b5b4-205">W idealnym przypadku cyklicznych zadań należy zawsze powiodło się i mają względnie stały czas wykonania; monitorowanie zachowania te pomogą upewnij się, że zadanie hello jest w dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-205">Ideally, recurring jobs should always succeed, and have relatively stable execution time; monitoring these behaviors will help ensure hello job is healthy.</span></span> <span data-ttu-id="2b5b4-206">Cykliczne zadania są identyfikowane za pomocą właściwości "Cyklu" hello.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-206">Recurring jobs are identified using hello "Recurrence" property.</span></span> <span data-ttu-id="2b5b4-207">Zadania zaplanowane przy użyciu fabryki danych AZURE w wersji 2 ma automatycznie tej właściwości wypełnione.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-207">Jobs scheduled using ADF V2 will automatically have this property populated.</span></span>

<span data-ttu-id="2b5b4-208">tooview listę zadań U-SQL, które są cykliczne:</span><span class="sxs-lookup"><span data-stu-id="2b5b4-208">tooview a list of U-SQL jobs that are recurring:</span></span> 

1. <span data-ttu-id="2b5b4-209">W hello portalu Azure Przejdź tooyour kont usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-209">In hello Azure portal, go tooyour Data Lake Analytics accounts.</span></span>
2. <span data-ttu-id="2b5b4-210">Kliknij przycisk **zadania Insights**.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-210">Click **Job Insights**.</span></span> <span data-ttu-id="2b5b4-211">powitalne kartę "Wszystkie zadania" zostanie przywrócona domyślna, przedstawiający listę uruchomiona, w kolejce i zakończenia zadania.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-211">hello "All Jobs" tab will be defaulted, showing a list of running, queued, and ended jobs.</span></span>
3. <span data-ttu-id="2b5b4-212">Kliknij przycisk hello **cyklicznych zadań** kartę. Lista zadań cyklicznych pojawi się wraz z zagregowanych danych statystycznych dla każdego zadania cyklicznego.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-212">Click hello **Recurring Jobs** tab. A list of recurring jobs will be shown along with aggregated statistics for each recurring job.</span></span>

## <a name="manage-policies"></a><span data-ttu-id="2b5b4-213">Zarządzanie zasadami</span><span class="sxs-lookup"><span data-stu-id="2b5b4-213">Manage policies</span></span>

### <a name="account-level-policies"></a><span data-ttu-id="2b5b4-214">Zasady na poziomie konta</span><span class="sxs-lookup"><span data-stu-id="2b5b4-214">Account-level policies</span></span>

<span data-ttu-id="2b5b4-215">Te zasady są stosowane tooall zadań w ramach konta usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-215">These policies apply tooall jobs in a Data Lake Analytics account.</span></span>

#### <a name="maximum-number-of-aus-in-a-data-lake-analytics-account"></a><span data-ttu-id="2b5b4-216">Maksymalna liczba AUs w ramach konta usługi Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="2b5b4-216">Maximum number of AUs in a Data Lake Analytics account</span></span>
<span data-ttu-id="2b5b4-217">Zasady regulują hello łączną liczbę jednostek Analytics (AUs), można użyć konta usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-217">A policy controls hello total number of Analytics Units (AUs) your Data Lake Analytics account can use.</span></span> <span data-ttu-id="2b5b4-218">Domyślnie wartość hello jest ustawiana too250.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-218">By default, hello value is set too250.</span></span> <span data-ttu-id="2b5b4-219">Na przykład, jeśli ta wartość jest ustawiana too250 AUs, program może jedno zadanie uruchomione z 250 tooit AUs przypisane lub 10 zadań uruchamianych z 25 AUs każdego.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-219">For example, if this value is set too250 AUs, you can have one job running with 250 AUs assigned tooit, or 10 jobs running with 25 AUs each.</span></span> <span data-ttu-id="2b5b4-220">Dodatkowe zadania, które są przesyłane są umieszczane w kolejce zakończenie hello uruchomionych zadań.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-220">Additional jobs that are submitted are queued until hello running jobs are finished.</span></span> <span data-ttu-id="2b5b4-221">Po zakończeniu są wykonywane zadania dla hello są zwalniane AUs toorun zadań w kolejce.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-221">When running jobs are finished, AUs are freed up for hello queued jobs toorun.</span></span>

<span data-ttu-id="2b5b4-222">toochange hello liczba AUs dla Twojego konta usługi Data Lake Analytics:</span><span class="sxs-lookup"><span data-stu-id="2b5b4-222">toochange hello number of AUs for your Data Lake Analytics account:</span></span>

1. <span data-ttu-id="2b5b4-223">W hello portalu Azure Przejdź tooyour konta usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-223">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="2b5b4-224">Kliknij pozycję **Właściwości**.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-224">Click **Properties**.</span></span>
3. <span data-ttu-id="2b5b4-225">W obszarze **maksymalna AUs**, Przenieś hello suwaka tooselect wartości lub wprowadź hello wartość w polu tekstowym hello.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-225">Under **Maximum AUs**, move hello slider tooselect a value, or enter hello value in hello text box.</span></span> 
4. <span data-ttu-id="2b5b4-226">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-226">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="2b5b4-227">Jeśli użytkownik należy większej hello domyślne (250) AUs, w portalu powitania kliknij **pomoc + Obsługa** toosubmit żądania pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-227">If you need more than hello default (250) AUs, in hello portal, click **Help+Support** toosubmit a support request.</span></span> <span data-ttu-id="2b5b4-228">można zwiększyć liczbę Hello AUs dostępne w ramach konta usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-228">hello number of AUs available in your Data Lake Analytics account can be increased.</span></span>
>

#### <a name="maximum-number-of-jobs-that-can-run-simultaneously"></a><span data-ttu-id="2b5b4-229">Maksymalna liczba zadań, które można uruchomić jednocześnie</span><span class="sxs-lookup"><span data-stu-id="2b5b4-229">Maximum number of jobs that can run simultaneously</span></span>
<span data-ttu-id="2b5b4-230">Zasady regulują, jak wiele zadań można uruchomić na powitania tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-230">A policy controls how many jobs can run at hello same time.</span></span> <span data-ttu-id="2b5b4-231">Domyślnie ta wartość jest ustawiana too20.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-231">By default, this value is set too20.</span></span> <span data-ttu-id="2b5b4-232">Jeśli usługi Data Lake Analytics ma AUs dostępne, nowe zadania są zaplanowane toorun do momentu hello całkowita liczba uruchomionych zadań osiągnie wartość hello niniejszych zasad.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-232">If your Data Lake Analytics has AUs available, new jobs are scheduled toorun immediately until hello total number of running jobs reaches hello value of this policy.</span></span> <span data-ttu-id="2b5b4-233">Po osiągnięciu hello maksymalna liczba zadań, które można uruchomić jednocześnie, kolejne zadania są umieszczane w kolejce w kolejności priorytetu do momentu ukończenia co najmniej jedno zadanie uruchomione (w zależności od dostępności Australia).</span><span class="sxs-lookup"><span data-stu-id="2b5b4-233">When you reach hello maximum number of jobs that can run simultaneously, subsequent jobs are queued in priority order until one or more running jobs complete (depending on AU availability).</span></span>

<span data-ttu-id="2b5b4-234">toochange hello liczba zadań, które można uruchomić jednocześnie:</span><span class="sxs-lookup"><span data-stu-id="2b5b4-234">toochange hello number of jobs that can run simultaneously:</span></span>

1. <span data-ttu-id="2b5b4-235">W hello portalu Azure Przejdź tooyour konta usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-235">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="2b5b4-236">Kliknij pozycję **Właściwości**.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-236">Click **Properties**.</span></span>
3. <span data-ttu-id="2b5b4-237">W obszarze **maksymalny numer z uruchomione zadania**, Przenieś hello suwaka tooselect wartości lub wprowadź hello wartość w polu tekstowym hello.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-237">Under **Maximum Number of Running Jobs**, move hello slider tooselect a value, or enter hello value in hello text box.</span></span> 
4. <span data-ttu-id="2b5b4-238">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-238">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="2b5b4-239">Jeśli potrzebujesz więcej niż hello domyślne (20) liczba zadań, w portalu powitania kliknij toorun **pomoc + Obsługa** toosubmit żądania pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-239">If you need toorun more than hello default (20) number of jobs, in hello portal, click **Help+Support** toosubmit a support request.</span></span> <span data-ttu-id="2b5b4-240">można zwiększyć Hello liczba zadań, które można uruchomić jednocześnie w ramach konta usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-240">hello number of jobs that can run simultaneously in your Data Lake Analytics account can be increased.</span></span>
>

#### <a name="how-long-tookeep-job-metadata-and-resources"></a><span data-ttu-id="2b5b4-241">Jak długo tookeep zadania metadanych i zasoby</span><span class="sxs-lookup"><span data-stu-id="2b5b4-241">How long tookeep job metadata and resources</span></span> 
<span data-ttu-id="2b5b4-242">Po wykonaniu zadań U-SQL hello usługi Data Lake Analytics zachowuje wszystkie powiązane pliki.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-242">When your users run U-SQL jobs, hello Data Lake Analytics service retains all related files.</span></span> <span data-ttu-id="2b5b4-243">Powiązane pliki obejmują skrypt hello U-SQL, pliki DLL hello w skryptu U-SQL hello, skompilowanych zasobów i statystyki.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-243">Related files include hello U-SQL script, hello DLL files referenced in hello U-SQL script, compiled resources, and statistics.</span></span> <span data-ttu-id="2b5b4-244">pliki Hello znajdują się w folderze /system/ hello hello domyślnego konta usługi Azure Data Lake Storage.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-244">hello files are in hello /system/ folder of hello default Azure Data Lake Storage account.</span></span> <span data-ttu-id="2b5b4-245">Ta zasada kontroluje, jak długo są przechowywane tych zasobów, zanim zostaną automatycznie usunięte (hello domyślny to 30 dni).</span><span class="sxs-lookup"><span data-stu-id="2b5b4-245">This policy controls how long these resources are stored before they are automatically deleted (hello default is 30 days).</span></span> <span data-ttu-id="2b5b4-246">Debugowanie i dostrajania wydajności zadań, które będzie ponownie w przyszłości hello można używać tych plików.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-246">You can use these files for debugging, and for performance-tuning of jobs that you'll rerun in hello future.</span></span>

<span data-ttu-id="2b5b4-247">toochange jak długo tookeep zadania metadanych i zasoby:</span><span class="sxs-lookup"><span data-stu-id="2b5b4-247">toochange how long tookeep job metadata and resources:</span></span>

1. <span data-ttu-id="2b5b4-248">W hello portalu Azure Przejdź tooyour konta usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-248">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="2b5b4-249">Kliknij pozycję **Właściwości**.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-249">Click **Properties**.</span></span>
3. <span data-ttu-id="2b5b4-250">W obszarze **tooRetain dni zadanie odpytuje**, Przenieś hello suwaka tooselect wartości lub wprowadź hello wartość w polu tekstowym hello.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-250">Under **Days tooRetain Job Queries**, move hello slider tooselect a value, or enter hello value in hello text box.</span></span>  
4. <span data-ttu-id="2b5b4-251">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-251">Click **Save**.</span></span>

### <a name="job-level-policies"></a><span data-ttu-id="2b5b4-252">Zasady na poziomie zadania</span><span class="sxs-lookup"><span data-stu-id="2b5b4-252">Job-level policies</span></span>
<span data-ttu-id="2b5b4-253">Z zasady na poziomie zadania, można kontrolować hello AUs maksymalna i maksymalny priorytet poszczególnych użytkowników (lub członków określonych grup zabezpieczeń), które można ustawić dla zadania, które przesyłają hello.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-253">With job-level policies, you can control hello maximum AUs and hello maximum priority that individual users (or members of specific security groups) can set on jobs that they submit.</span></span> <span data-ttu-id="2b5b4-254">To pozwala na kontrolowanie hello kosztów ponoszonych przez użytkowników.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-254">This lets you control hello costs incurred by users.</span></span> <span data-ttu-id="2b5b4-255">Umożliwia również kontroli hello wpływ, jaki zaplanowane zadania może być na wysoki priorytet zadania produkcji, które działają w hello tego samego konta usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-255">It also lets you control hello effect that scheduled jobs might have on high-priority production jobs that are running in hello same Data Lake Analytics account.</span></span>

<span data-ttu-id="2b5b4-256">Data Lake Analytics ma dwie zasady, które można ustawić na poziomie zadania hello:</span><span class="sxs-lookup"><span data-stu-id="2b5b4-256">Data Lake Analytics has two policies that you can set at hello job level:</span></span>

* <span data-ttu-id="2b5b4-257">**Australia limit dla zadania**: użytkownicy, można kierować tylko zadania, które mają toothis liczby AUs.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-257">**AU limit per job**: Users can only submit jobs that have up toothis number of AUs.</span></span> <span data-ttu-id="2b5b4-258">Domyślnie ten limit jest hello taki sam jak hello maksymalny limit Australia hello konta.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-258">By default, this limit is hello same as hello maximum AU limit for hello account.</span></span>
* <span data-ttu-id="2b5b4-259">**Priorytet**: użytkownicy, można kierować tylko zadania, które mają wartość priorytetu toothis mniejsze niż lub równe.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-259">**Priority**: Users can only submit jobs that have a priority lower than or equal toothis value.</span></span> <span data-ttu-id="2b5b4-260">Należy pamiętać, że większa liczba oznacza o niższym priorytecie.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-260">Note that a higher number means a lower priority.</span></span> <span data-ttu-id="2b5b4-261">To jest domyślnie too1, która jest hello najwyższy możliwy priorytet.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-261">By default, this is set too1, which is hello highest possible priority.</span></span>

<span data-ttu-id="2b5b4-262">Brak domyślnych zasad ustawić dla każdego konta.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-262">There is a default policy set on every account.</span></span> <span data-ttu-id="2b5b4-263">zasady domyślne Hello stosuje użytkowników tooall hello konta.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-263">hello default policy applies tooall users of hello account.</span></span> <span data-ttu-id="2b5b4-264">Dodatkowe zasady można ustawić dla poszczególnych użytkowników i grup.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-264">You can set additional policies for specific users and groups.</span></span> 

> [!NOTE]
> <span data-ttu-id="2b5b4-265">Zasady na poziomie konta i zasad na poziomie zadania się jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-265">Account-level policies and job-level policies apply simultaneously.</span></span>
>

#### <a name="add-a-policy-for-a-specific-user-or-group"></a><span data-ttu-id="2b5b4-266">Dodaj zasady dla określonego użytkownika lub grupy</span><span class="sxs-lookup"><span data-stu-id="2b5b4-266">Add a policy for a specific user or group</span></span>

1. <span data-ttu-id="2b5b4-267">W hello portalu Azure Przejdź tooyour konta usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-267">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="2b5b4-268">Kliknij pozycję **Właściwości**.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-268">Click **Properties**.</span></span>
3. <span data-ttu-id="2b5b4-269">W obszarze **limitów przesyłanie zadań**, kliknij przycisk hello **Dodaj zasady** przycisku.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-269">Under **Job Submission Limits**, click hello **Add Policy** button.</span></span> <span data-ttu-id="2b5b4-270">Następnie wybierz lub wprowadź hello następujące ustawienia:</span><span class="sxs-lookup"><span data-stu-id="2b5b4-270">Then, select or enter hello following settings:</span></span>
    1. <span data-ttu-id="2b5b4-271">**Obliczeniowe Nazwa zasady**: Wprowadź nazwę zasad, tooremind o celu hello hello zasad.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-271">**Compute Policy Name**: Enter a policy name, tooremind you of hello purpose of hello policy.</span></span>
    2. <span data-ttu-id="2b5b4-272">**Wybierz użytkownika lub grupy**: Wybierz hello użytkownika lub grupy, które dotyczą te zasady.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-272">**Select User or Group**: Select hello user or group this policy applies to.</span></span>
    3. <span data-ttu-id="2b5b4-273">**Ustaw Limit Australia zadania hello**: hello Australia wyznaczonym stosowanym toohello wybrany użytkownik lub grupa.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-273">**Set hello Job AU Limit**: Set hello AU limit that applies toohello selected user or group.</span></span>
    4. <span data-ttu-id="2b5b4-274">**Ustaw Limit priorytet hello**: Ustaw hello priorytet limit ma zastosowanie toohello wybrany użytkownik lub grupa.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-274">**Set hello Priority Limit**: Set hello priority limit that applies toohello selected user or group.</span></span>

4. <span data-ttu-id="2b5b4-275">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-275">Click **Ok**.</span></span>

5. <span data-ttu-id="2b5b4-276">nowe zasady Hello ma na liście hello **domyślne** w sekcji tabela zasad **limitów przesyłanie zadań**.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-276">hello new policy is listed in hello **Default** policy table, under **Job Submission Limits**.</span></span> 

#### <a name="delete-or-edit-an-existing-policy"></a><span data-ttu-id="2b5b4-277">Usuń lub Edytuj istniejące zasady</span><span class="sxs-lookup"><span data-stu-id="2b5b4-277">Delete or edit an existing policy</span></span>

1. <span data-ttu-id="2b5b4-278">W hello portalu Azure Przejdź tooyour konta usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-278">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="2b5b4-279">Kliknij pozycję **Właściwości**.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-279">Click **Properties**.</span></span>
3. <span data-ttu-id="2b5b4-280">W obszarze **limitów przesyłanie zadań**, Znajdź hello zasady tooedit.</span><span class="sxs-lookup"><span data-stu-id="2b5b4-280">Under **Job Submission Limits**, find hello policy you want tooedit.</span></span>
4.  <span data-ttu-id="2b5b4-281">Witaj toosee **usunąć** i **Edytuj** kliknij przycisk Opcje w prawej kolumnie tabeli hello, hello **...** .</span><span class="sxs-lookup"><span data-stu-id="2b5b4-281">toosee hello **Delete** and **Edit** options, in hello rightmost column of hello table, click **...**.</span></span>

### <a name="additional-resources-for-job-policies"></a><span data-ttu-id="2b5b4-282">Dodatkowe zasoby dotyczące zasad zadania</span><span class="sxs-lookup"><span data-stu-id="2b5b4-282">Additional resources for job policies</span></span>
* [<span data-ttu-id="2b5b4-283">Omówienie zasad wpis w blogu</span><span class="sxs-lookup"><span data-stu-id="2b5b4-283">Policy overview blog post</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-overview/)
* [<span data-ttu-id="2b5b4-284">Wpis w blogu zasad na poziomie konta</span><span class="sxs-lookup"><span data-stu-id="2b5b4-284">Account-level policies blog post</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-account-level-policy/)
* [<span data-ttu-id="2b5b4-285">Zasady na poziomie zadania wpis w blogu</span><span class="sxs-lookup"><span data-stu-id="2b5b4-285">Job-level policies blog post</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-job-level-policy/)

## <a name="next-steps"></a><span data-ttu-id="2b5b4-286">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2b5b4-286">Next steps</span></span>

* [<span data-ttu-id="2b5b4-287">Omówienie usługi Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="2b5b4-287">Overview of Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="2b5b4-288">Rozpoczynanie pracy z usługą Data Lake Analytics przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="2b5b4-288">Get started with Data Lake Analytics by using hello Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="2b5b4-289">Zarządzanie usługą Azure Data Lake Analytics przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="2b5b4-289">Manage Azure Data Lake Analytics by using Azure PowerShell</span></span>](data-lake-analytics-manage-use-powershell.md)

