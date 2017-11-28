---
title: "zalecenia wydajności aaaApply — baza danych SQL Azure | Dokumentacja firmy Microsoft"
description: "Można użyć hello toofind portalu Azure wydajności zaleceń, które można zoptymalizować wydajność bazy danych SQL Azure lub toocorrect niektórych problem wskazany w obciążenie."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: cda8a646-0584-4368-b28a-85cdd9b54fcd
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 0b2234840fc3254d235db9e7d18f5bc912851c6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="find-and-apply-performance-recommendations"></a><span data-ttu-id="c419b-103">Znajdź i stosować zalecenia wydajności</span><span class="sxs-lookup"><span data-stu-id="c419b-103">Find and apply performance recommendations</span></span>

<span data-ttu-id="c419b-104">Można użyć hello toofind portalu Azure wydajności zaleceń, które można zoptymalizować wydajność bazy danych SQL Azure lub toocorrect niektórych problem wskazany w obciążenie.</span><span class="sxs-lookup"><span data-stu-id="c419b-104">You can use hello Azure portal toofind performance recommendations that can optimize performance of your Azure SQL Database or toocorrect some issue identified in your workload.</span></span> <span data-ttu-id="c419b-105">**Zalecenie wydajności** strony w portalu Azure umożliwia toofind hello najlepsze rekomendacje na potencjalnego wpływu na ich podstawie.</span><span class="sxs-lookup"><span data-stu-id="c419b-105">**Performance recommendation** page in Azure portal enables you toofind hello top recommendations based on their potential impact.</span></span> 

## <a name="viewing-recommendations"></a><span data-ttu-id="c419b-106">Przeglądanie zaleceniami</span><span class="sxs-lookup"><span data-stu-id="c419b-106">Viewing recommendations</span></span>

<span data-ttu-id="c419b-107">tooview i stosować zalecenia dotyczące wydajności, należy hello poprawne [kontroli dostępu opartej na rolach](../active-directory/role-based-access-control-what-is.md) uprawnienia na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="c419b-107">tooview and apply performance recommendations, you need hello correct [role-based access control](../active-directory/role-based-access-control-what-is.md) permissions in Azure.</span></span> <span data-ttu-id="c419b-108">**Czytnik**, **Współautor bazy danych SQL** zalecenia tooview wymagane są uprawnienia i **właściciela**, **Współautor bazy danych SQL** uprawnienia są wymagane tooexecute wszystkie akcje; Utwórz lub Porzuć indeksy i anulowanie tworzenia indeksu.</span><span class="sxs-lookup"><span data-stu-id="c419b-108">**Reader**, **SQL DB Contributor** permissions are required tooview recommendations, and **Owner**, **SQL DB Contributor** permissions are required tooexecute any actions; create or drop indexes and cancel index creation.</span></span>

<span data-ttu-id="c419b-109">Użyj hello następujące zalecenia dotyczące wydajności toofind kroki w portalu Azure:</span><span class="sxs-lookup"><span data-stu-id="c419b-109">Use hello following steps toofind performance recommendations on Azure portal:</span></span>

1. <span data-ttu-id="c419b-110">Zaloguj się toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c419b-110">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="c419b-111">Przejdź za**więcej usług** > **baz danych**i wybierz bazę danych.</span><span class="sxs-lookup"><span data-stu-id="c419b-111">Go too**More services** > **SQL databases**, and select your database.</span></span>
3. <span data-ttu-id="c419b-112">Przejdź za**wydajności zalecenie** tooview dostępne zalecenia dotyczące hello wybranej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c419b-112">Navigate too**Performance recommendation** tooview available recommendations for hello selected database.</span></span>

<span data-ttu-id="c419b-113">Zalecenia dotyczące wydajności są shonw w hello tabeli podobne toohello przedstawionego na następującej ilustracji hello:</span><span class="sxs-lookup"><span data-stu-id="c419b-113">Performance recommendations are shonw in hello table similar toohello one shown on hello following figure:</span></span>

![Zalecenia](./media/sql-database-advisor-portal/recommendations.png)

<span data-ttu-id="c419b-115">Zalecenia są sortowane według ich potencjalny wpływ na wydajność w hello następujące kategorie:</span><span class="sxs-lookup"><span data-stu-id="c419b-115">Recommendations are sorted by their potential impact on performance into hello following categories:</span></span>

| <span data-ttu-id="c419b-116">Wpływ</span><span class="sxs-lookup"><span data-stu-id="c419b-116">Impact</span></span> | <span data-ttu-id="c419b-117">Opis</span><span class="sxs-lookup"><span data-stu-id="c419b-117">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="c419b-118">Wysoka</span><span class="sxs-lookup"><span data-stu-id="c419b-118">High</span></span> |<span data-ttu-id="c419b-119">Duże znaczenie zalecenia powinien zapewnić hello najbardziej znaczący wpływ na wydajność.</span><span class="sxs-lookup"><span data-stu-id="c419b-119">High impact recommendations should provide hello most significant performance impact.</span></span> |
| <span data-ttu-id="c419b-120">Medium</span><span class="sxs-lookup"><span data-stu-id="c419b-120">Medium</span></span> |<span data-ttu-id="c419b-121">Średni wpływ zalecenia należy zwiększyć wydajność, ale nie w znacznym stopniu.</span><span class="sxs-lookup"><span data-stu-id="c419b-121">Medium impact recommendations should improve performance, but not substantially.</span></span> |
| <span data-ttu-id="c419b-122">Niska</span><span class="sxs-lookup"><span data-stu-id="c419b-122">Low</span></span> |<span data-ttu-id="c419b-123">Niski wpływ zalecenia należy zapewnić lepszą wydajność niż bez, ale ulepszenia może być niewielka.</span><span class="sxs-lookup"><span data-stu-id="c419b-123">Low impact recommendations should provide better performance than without, but improvements might not be significant.</span></span> |


> [!NOTE]
> <span data-ttu-id="c419b-124">Baza danych SQL Azure wymaga działania toomonitor co najmniej dzień w kolejności tooidentify kilka zaleceń.</span><span class="sxs-lookup"><span data-stu-id="c419b-124">Azure SQL Database needs toomonitor activities at least for a day in order tooidentify some recommendations.</span></span> <span data-ttu-id="c419b-125">Hello bazy danych SQL Azure łatwiej można zoptymalizować wzorców spójne zapytania nie może uzyskać losowe spotty seria działań.</span><span class="sxs-lookup"><span data-stu-id="c419b-125">hello Azure SQL Database can more easily optimize for consistent query patterns than it can for random spotty bursts of activity.</span></span> <span data-ttu-id="c419b-126">Jeśli zalecenia nie są dostępne corrently, hello **wydajności zalecenie** strona zawiera komunikat wyjaśniający, dlaczego.</span><span class="sxs-lookup"><span data-stu-id="c419b-126">If recommendations are not corrently available, hello **Performance recommendation** page provides a message explaining why.</span></span>
> 

<span data-ttu-id="c419b-127">Można również wyświetlić stan hello hello historyczne operacje.</span><span class="sxs-lookup"><span data-stu-id="c419b-127">You can also view hello status of hello historical operations.</span></span> <span data-ttu-id="c419b-128">Wybierz toosee zalecenia lub stan więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="c419b-128">Select a recommendation or status toosee  more details.</span></span>

<span data-ttu-id="c419b-129">Oto przykład "Create index" zalecenia w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c419b-129">Here is an example of "Create index" recommendation in hello Azure portal.</span></span>

![Tworzenie indeksu](./media/sql-database-advisor-portal/sql-database-performance-recommendation.png)

## <a name="applying-recommendations"></a><span data-ttu-id="c419b-131">Zalecenia dotyczące stosowania</span><span class="sxs-lookup"><span data-stu-id="c419b-131">Applying recommendations</span></span>
<span data-ttu-id="c419b-132">Baza danych SQL Azure umożliwia pełną kontrolę nad jak zalecenia są włączone, przy użyciu dowolnego hello następujące trzy opcje:</span><span class="sxs-lookup"><span data-stu-id="c419b-132">Azure SQL Database gives you full control over how recommendations are enabled using any of hello following three options:</span></span> 

* <span data-ttu-id="c419b-133">Zastosuj poszczególne zalecenia co naraz.</span><span class="sxs-lookup"><span data-stu-id="c419b-133">Apply individual recommendations one at a time.</span></span>
* <span data-ttu-id="c419b-134">Włącz hello automatycznego dostrajania tooautomatically stosować zalecenia.</span><span class="sxs-lookup"><span data-stu-id="c419b-134">Enable hello Automatic tuning tooautomatically apply recommendations.</span></span>
* <span data-ttu-id="c419b-135">tooimplement zalecenie uruchomić ręcznie, hello zalecane skryptu T-SQL bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c419b-135">tooimplement a recommendation manually, run hello recommended T-SQL script against your database.</span></span>

<span data-ttu-id="c419b-136">Wybierz wszystkie zalecenia tooview jego szczegóły, a następnie kliknij przycisk **wyświetlić skryptu** tooreview hello szczegółowe dane dotyczące sposobu tworzenia hello zalecenia.</span><span class="sxs-lookup"><span data-stu-id="c419b-136">Select any recommendation tooview its details and then click **View script** tooreview hello exact details of how hello recommendation is created.</span></span>

<span data-ttu-id="c419b-137">Witaj bazy danych pozostaje w trybie online, gdy zastosowano zalecenie hello — przy użyciu zalecenie wydajności lub automatycznego dostrajania nigdy nie ma bazy danych w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="c419b-137">hello database remains online while hello recommendation is applied -- using performance recommendation or automatic tuning never takes a database offline.</span></span>

### <a name="apply-an-individual-recommendation"></a><span data-ttu-id="c419b-138">Zastosuj poszczególne zalecenia.</span><span class="sxs-lookup"><span data-stu-id="c419b-138">Apply an individual recommendation</span></span>
<span data-ttu-id="c419b-139">Można przeczytaj i zaakceptuj zalecenia jednym naraz.</span><span class="sxs-lookup"><span data-stu-id="c419b-139">You can review and accept recommendations one at a time.</span></span>

1. <span data-ttu-id="c419b-140">Na powitania **zalecenia** bloku, wybierz zalecenia.</span><span class="sxs-lookup"><span data-stu-id="c419b-140">On hello **Recommendations** blade, select a recommendation.</span></span>
2. <span data-ttu-id="c419b-141">Na powitania **szczegóły** kliknij bloku **Zastosuj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c419b-141">On hello **Details** blade click **Apply** button.</span></span>
   
    ![Zastosuj zalecenia](./media/sql-database-advisor-portal/apply.png)

<span data-ttu-id="c419b-143">Zalecenie wybrane zostaną zastosowane na powitania bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c419b-143">Selected recommendation will be applied on hello database.</span></span>

### <a name="removing-recommendations-from-hello-list"></a><span data-ttu-id="c419b-144">Usuwanie z listy hello zalecenia</span><span class="sxs-lookup"><span data-stu-id="c419b-144">Removing recommendations from hello list</span></span>
<span data-ttu-id="c419b-145">Jeśli lista zaleceń zawiera elementy, które mają tooremove z listy hello, można odrzucić hello zalecenia:</span><span class="sxs-lookup"><span data-stu-id="c419b-145">If your list of recommendations contains items that you want tooremove from hello list, you can discard hello recommendation:</span></span>

1. <span data-ttu-id="c419b-146">Wybierz zalecenie liście hello **zalecenia** tooopen hello szczegóły.</span><span class="sxs-lookup"><span data-stu-id="c419b-146">Select a recommendation in hello list of **Recommendations** tooopen hello details.</span></span>
2. <span data-ttu-id="c419b-147">Kliknij przycisk **odrzucić** na powitania **szczegóły** bloku.</span><span class="sxs-lookup"><span data-stu-id="c419b-147">Click **Discard** on hello **Details** blade.</span></span>

<span data-ttu-id="c419b-148">W razie potrzeby można dodać odrzucone elementy kopii toohello **zalecenia** listy:</span><span class="sxs-lookup"><span data-stu-id="c419b-148">If desired, you can add discarded items back toohello **Recommendations** list:</span></span>

1. <span data-ttu-id="c419b-149">Na powitania **zalecenia** kliknij bloku **widoku odrzucone**.</span><span class="sxs-lookup"><span data-stu-id="c419b-149">On hello **Recommendations** blade click **View discarded**.</span></span>
2. <span data-ttu-id="c419b-150">Zaznacz element odrzuconych tooview listy hello jego szczegóły.</span><span class="sxs-lookup"><span data-stu-id="c419b-150">Select a discarded item from hello list tooview its details.</span></span>
3. <span data-ttu-id="c419b-151">Opcjonalnie kliknij **Cofnij odrzucić** tooadd hello indeksu wstecz toohello główną listę **zalecenia**.</span><span class="sxs-lookup"><span data-stu-id="c419b-151">Optionally, click **Undo Discard** tooadd hello index back toohello main list of **Recommendations**.</span></span>


### <a name="enable-automatic-tuning"></a><span data-ttu-id="c419b-152">Włączanie automatycznego dostrajania</span><span class="sxs-lookup"><span data-stu-id="c419b-152">Enable automatic tuning</span></span>
<span data-ttu-id="c419b-153">Można ustawić hello bazy danych SQL Azure tooimplement zalecenia automatycznie.</span><span class="sxs-lookup"><span data-stu-id="c419b-153">You can set hello Azure SQL Database tooimplement recommendations automatically.</span></span> <span data-ttu-id="c419b-154">Zgodnie z zaleceniami staną się dostępne automatycznie zostaną one zastosowane.</span><span class="sxs-lookup"><span data-stu-id="c419b-154">As recommendations become available they will automatically be applied.</span></span> <span data-ttu-id="c419b-155">Jako wszystkie zalecenia zarządza hello usługi, jeśli hello wpływ na wydajność jest ujemny hello zalecenie zostaną cofnięte.</span><span class="sxs-lookup"><span data-stu-id="c419b-155">As with all recommendations managed by hello service if hello performance impact is negative hello recommendation will be reverted.</span></span>

1. <span data-ttu-id="c419b-156">Na powitania **zalecenia** bloku, kliknij przycisk **automatyzacja**:</span><span class="sxs-lookup"><span data-stu-id="c419b-156">On hello **Recommendations** blade, click **Automate**:</span></span>
   
    ![Ustawienia usługi Advisor](./media/sql-database-advisor-portal/settings.png)
2. <span data-ttu-id="c419b-158">Wybierz akcje tooautomate:</span><span class="sxs-lookup"><span data-stu-id="c419b-158">Select actions tooautomate:</span></span>
   
    ![Zalecane indeksy](./media/sql-database-advisor-portal/automation.png)

### <a name="manually-run-hello-recommended-t-sql-script"></a><span data-ttu-id="c419b-160">Ręcznie uruchom hello zalecane skryptu T-SQL</span><span class="sxs-lookup"><span data-stu-id="c419b-160">Manually run hello recommended T-SQL script</span></span>
<span data-ttu-id="c419b-161">Wybierz każde zalecenie, a następnie kliknij przycisk **Wyświetl skrypt**.</span><span class="sxs-lookup"><span data-stu-id="c419b-161">Select any recommendation and then click **View script**.</span></span> <span data-ttu-id="c419b-162">Uruchom ten skrypt bazy danych toomanually zastosować zalecenie hello.</span><span class="sxs-lookup"><span data-stu-id="c419b-162">Run this script against your database toomanually apply hello recommendation.</span></span>

<span data-ttu-id="c419b-163">*Indeksy, które są wykonywane ręcznie nie są monitorowane i weryfikowane pod kątem wpływu na wydajność przez usługę hello* , zaleca się monitorowanie tych indeksów po utworzeniu tooverify one zapewniają większą wydajność i dostosować lub usuń je, jeśli niezbędne.</span><span class="sxs-lookup"><span data-stu-id="c419b-163">*Indexes that are manually executed are not monitored and validated for performance impact by hello service* so it is suggested that you monitor these indexes after creation tooverify they provide performance gains and adjust or delete them if necessary.</span></span> <span data-ttu-id="c419b-164">Aby uzyskać więcej informacji o tworzeniu indeksów, zobacz [CREATE INDEX (Transact-SQL)](https://msdn.microsoft.com/library/ms188783.aspx).</span><span class="sxs-lookup"><span data-stu-id="c419b-164">For details about creating indexes, see [CREATE INDEX (Transact-SQL)](https://msdn.microsoft.com/library/ms188783.aspx).</span></span>

### <a name="canceling-recommendations"></a><span data-ttu-id="c419b-165">Anulowanie zalecenia</span><span class="sxs-lookup"><span data-stu-id="c419b-165">Canceling recommendations</span></span>
<span data-ttu-id="c419b-166">Zalecenia, które znajdują się w **oczekujące**, **weryfikacji**, lub **Powodzenie** stanu mogą zostać anulowane.</span><span class="sxs-lookup"><span data-stu-id="c419b-166">Recommendations that are in a **Pending**, **Verifying**, or **Success** status can be canceled.</span></span> <span data-ttu-id="c419b-167">Zalecenia dotyczące ze stanem **Executing** nie można anulować.</span><span class="sxs-lookup"><span data-stu-id="c419b-167">Recommendations with a status of **Executing** cannot be canceled.</span></span>

1. <span data-ttu-id="c419b-168">Wybierz zalecenie hello **dostrajanie historii** hello tooopen obszaru **szczegóły zalecenia** bloku.</span><span class="sxs-lookup"><span data-stu-id="c419b-168">Select a recommendation in hello **Tuning History** area tooopen hello **recommendations details** blade.</span></span>
2. <span data-ttu-id="c419b-169">Kliknij przycisk **anulować** tooabort hello proces stosowania hello zalecenia.</span><span class="sxs-lookup"><span data-stu-id="c419b-169">Click **Cancel** tooabort hello process of applying hello recommendation.</span></span>

## <a name="monitoring-operations"></a><span data-ttu-id="c419b-170">Operacje monitorowania</span><span class="sxs-lookup"><span data-stu-id="c419b-170">Monitoring operations</span></span>
<span data-ttu-id="c419b-171">Zalecamy stosowanie może odbywa się natychmiast.</span><span class="sxs-lookup"><span data-stu-id="c419b-171">Applying a recommendation might not happen instantaneously.</span></span> <span data-ttu-id="c419b-172">Hello portal zawiera szczegółowe informacje dotyczące stanu hello zalecenia.</span><span class="sxs-lookup"><span data-stu-id="c419b-172">hello portal provides details regarding hello status of recommendation.</span></span> <span data-ttu-id="c419b-173">Witaj poniżej przedstawiono możliwe stany, które można indeksu w:</span><span class="sxs-lookup"><span data-stu-id="c419b-173">hello following are possible states that an index can be in:</span></span>

| <span data-ttu-id="c419b-174">Stan</span><span class="sxs-lookup"><span data-stu-id="c419b-174">Status</span></span> | <span data-ttu-id="c419b-175">Opis</span><span class="sxs-lookup"><span data-stu-id="c419b-175">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="c419b-176">Oczekujące</span><span class="sxs-lookup"><span data-stu-id="c419b-176">Pending</span></span> |<span data-ttu-id="c419b-177">Zastosuj zalecenie polecenie zostało odebrane i jest zaplanowane do uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="c419b-177">Apply recommendation command has been received and is scheduled for execution.</span></span> |
| <span data-ttu-id="c419b-178">Wykonywanie</span><span class="sxs-lookup"><span data-stu-id="c419b-178">Executing</span></span> |<span data-ttu-id="c419b-179">zalecenie Hello jest stosowany.</span><span class="sxs-lookup"><span data-stu-id="c419b-179">hello recommendation is being applied.</span></span> |
| <span data-ttu-id="c419b-180">Weryfikowanie</span><span class="sxs-lookup"><span data-stu-id="c419b-180">Verifying</span></span> |<span data-ttu-id="c419b-181">Zalecenie zostało pomyślnie zastosowane i usługi hello jest pomiaru hello korzyści.</span><span class="sxs-lookup"><span data-stu-id="c419b-181">Recommendation was successfully applied and hello service is measuring hello benefits.</span></span> |
| <span data-ttu-id="c419b-182">Powodzenie</span><span class="sxs-lookup"><span data-stu-id="c419b-182">Success</span></span> |<span data-ttu-id="c419b-183">Zalecenie zostało pomyślnie zastosowane i zostały zmierzone korzyści.</span><span class="sxs-lookup"><span data-stu-id="c419b-183">Recommendation was successfully applied and benefits have been measured.</span></span> |
| <span data-ttu-id="c419b-184">Błąd</span><span class="sxs-lookup"><span data-stu-id="c419b-184">Error</span></span> |<span data-ttu-id="c419b-185">Wystąpił błąd podczas procesu hello stosowania hello zalecenia.</span><span class="sxs-lookup"><span data-stu-id="c419b-185">An error occurred during hello process of applying hello recommendation.</span></span> <span data-ttu-id="c419b-186">Może to być przejściowy problem lub toohello zmiany schematu tabeli i hello skryptu nie jest już prawidłowy.</span><span class="sxs-lookup"><span data-stu-id="c419b-186">This can be a transient issue, or possibly a schema change toohello table and hello script is no longer valid.</span></span> |
| <span data-ttu-id="c419b-187">Przywracanie</span><span class="sxs-lookup"><span data-stu-id="c419b-187">Reverting</span></span> |<span data-ttu-id="c419b-188">zalecenie Hello została zastosowana, ale został uznany za z systemem innym niż wydajność i zostanie automatycznie przywrócony.</span><span class="sxs-lookup"><span data-stu-id="c419b-188">hello recommendation was applied, but has been deemed non-performant and is being automatically reverted.</span></span> |
| <span data-ttu-id="c419b-189">Przywrócono</span><span class="sxs-lookup"><span data-stu-id="c419b-189">Reverted</span></span> |<span data-ttu-id="c419b-190">zalecenie Hello została przywrócona.</span><span class="sxs-lookup"><span data-stu-id="c419b-190">hello recommendation was reverted.</span></span> |

<span data-ttu-id="c419b-191">Kliknij w trakcie zalecenie toosee listy hello więcej szczegółów:</span><span class="sxs-lookup"><span data-stu-id="c419b-191">Click an in-process recommendation from hello list toosee more details:</span></span>

![Zalecane indeksy](./media/sql-database-advisor-portal/operations.png)

### <a name="reverting-a-recommendation"></a><span data-ttu-id="c419b-193">Przywrócenie zalecenia</span><span class="sxs-lookup"><span data-stu-id="c419b-193">Reverting a recommendation</span></span>
<span data-ttu-id="c419b-194">Jeśli użyto hello wydajności zalecenia tooapply hello zalecenie (co oznacza, że nie został ręcznie uruchomiony skryptu hello T-SQL) automatycznie zostanie przywrócona jego przypadku ich znalezienia hello wydajności wpływ toobe ujemna.</span><span class="sxs-lookup"><span data-stu-id="c419b-194">If you used hello performance recommendations tooapply hello recommendation (meaning you did not manually run hello T-SQL script) it will automatically revert it if it finds hello performance impact toobe negative.</span></span> <span data-ttu-id="c419b-195">Przyczyny po prostu chcesz toorevert zalecenia należy hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c419b-195">If for any reason you simply want toorevert a recommendation you can do hello following:</span></span>

1. <span data-ttu-id="c419b-196">Wybierz zalecenie pomyślnie zastosowane w hello **dostrajanie historii** obszaru.</span><span class="sxs-lookup"><span data-stu-id="c419b-196">Select a successfully applied recommendation in hello **Tuning history** area.</span></span>
2. <span data-ttu-id="c419b-197">Kliknij przycisk **Przywróć** na powitania **szczegóły zalecenia** bloku.</span><span class="sxs-lookup"><span data-stu-id="c419b-197">Click **Revert** on hello **recommendation details** blade.</span></span>

![Zalecane indeksy](./media/sql-database-advisor-portal/details.png)

## <a name="monitoring-performance-impact-of-index-recommendations"></a><span data-ttu-id="c419b-199">Wpływ na wydajność monitorowania zalecenia dotyczące indeksu</span><span class="sxs-lookup"><span data-stu-id="c419b-199">Monitoring performance impact of index recommendations</span></span>
<span data-ttu-id="c419b-200">Po pomyślnie zostały zaimplementowane zalecenia (obecnie indeksu operacji i parametryzacja zapytań zalecenia tylko) możesz kliknąć **szczegółowe informacje o zapytań** na powitania zalecenie szczegóły blok tooopen [zapytania Szczegółowe informacje o wydajności](sql-database-query-performance.md) zobaczyć wpływ na wydajność hello top zapytań.</span><span class="sxs-lookup"><span data-stu-id="c419b-200">After recommendations are successfully implemented (currently, index operations and parameterize queries recommendations only) you can click **Query Insights** on hello recommendation details blade tooopen [Query Performance Insights](sql-database-query-performance.md) and see hello performance impact of your top queries.</span></span>

![Wpływ na wydajność monitora](./media/sql-database-advisor-portal/query-insights.png)

## <a name="summary"></a><span data-ttu-id="c419b-202">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="c419b-202">Summary</span></span>
<span data-ttu-id="c419b-203">Baza danych SQL Azure zawiera zalecenia dotyczące poprawy wydajności bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="c419b-203">Azure SQL Database provides recommendations for improving SQL database performance.</span></span> <span data-ttu-id="c419b-204">Zapewniając skryptów T-SQL, a także osoby i pełni — automatyczne, otrzymasz przydatne pomocy w optymalizacji bazy danych i ostatecznie poprawę wydajności zapytań.</span><span class="sxs-lookup"><span data-stu-id="c419b-204">By providing T-SQL scripts, as well as individual and fully-automatic, you get a helpful assistance in optimizing your database and ultimately improving query performance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c419b-205">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c419b-205">Next steps</span></span>
<span data-ttu-id="c419b-206">Monitorowanie zalecenia i kontynuować tooapply ich toorefine wydajności.</span><span class="sxs-lookup"><span data-stu-id="c419b-206">Monitor your recommendations and continue tooapply them toorefine performance.</span></span> <span data-ttu-id="c419b-207">Obciążeń bazy danych są dynamiczne i zmienianie w sposób ciągły.</span><span class="sxs-lookup"><span data-stu-id="c419b-207">Database workloads are dynamic and change continuously.</span></span> <span data-ttu-id="c419b-208">Baza danych SQL Azure będzie kontynuować toomonitor i podano zalecenia, które może potencjalnie podnieść wydajność bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c419b-208">Azure SQL Database will continue toomonitor and provide recommendations that can potentially improve your database's performance.</span></span> 

* <span data-ttu-id="c419b-209">Zobacz [automatycznego dostrajania](sql-database-automatic-tuning.md) hello toolearn więcej na temat automatycznego dostrajania w bazie danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c419b-209">See [Automatic tuning](sql-database-automatic-tuning.md) toolearn more about hello automatic tuning in Azure SQL Database.</span></span>
* <span data-ttu-id="c419b-210">Zobacz [zaleceń](sql-database-advisor.md) omówienie zaleceń wydajności bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c419b-210">See [Performance recommendations](sql-database-advisor.md) for an overview of Azure SQL Database performance recommendations.</span></span>
* <span data-ttu-id="c419b-211">Zobacz [szczegółowe informacje o wydajności zapytań](sql-database-query-performance.md) toolearn o wyświetlaniu hello wpływ na wydajność kwerend top.</span><span class="sxs-lookup"><span data-stu-id="c419b-211">See [Query Performance Insights](sql-database-query-performance.md) toolearn about viewing hello performance impact of your top queries.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c419b-212">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="c419b-212">Additional resources</span></span>
* [<span data-ttu-id="c419b-213">Magazyn zapytań</span><span class="sxs-lookup"><span data-stu-id="c419b-213">Query Store</span></span>](https://msdn.microsoft.com/library/dn817826.aspx)
* [<span data-ttu-id="c419b-214">TWORZENIE INDEKSU</span><span class="sxs-lookup"><span data-stu-id="c419b-214">CREATE INDEX</span></span>](https://msdn.microsoft.com/library/ms188783.aspx)
* [<span data-ttu-id="c419b-215">Kontrola dostępu oparta na rolach</span><span class="sxs-lookup"><span data-stu-id="c419b-215">Role-based access control</span></span>](../active-directory/role-based-access-control-what-is.md)

