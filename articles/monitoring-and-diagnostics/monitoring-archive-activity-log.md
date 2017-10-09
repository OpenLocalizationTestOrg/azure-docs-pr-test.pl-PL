---
title: "Witaj aaaArchive dziennika aktywności platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooarchive Azure aktywności logowania w celu przechowywania długoterminowego na koncie magazynu."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/09/2016
ms.author: johnkem
ms.openlocfilehash: 58c6d3a3a31398287f66f76999d48f2942ab5109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="archive-hello-azure-activity-log"></a><span data-ttu-id="22a3f-103">Archiwum hello dziennika aktywności platformy Azure</span><span class="sxs-lookup"><span data-stu-id="22a3f-103">Archive hello Azure Activity Log</span></span>
<span data-ttu-id="22a3f-104">W tym artykule zostanie przedstawiony sposób korzystania hello portalu Azure, poleceń cmdlet programu PowerShell lub interfejsu wiersza polecenia i Platform tooarchive Twojego [ **dziennika aktywności platformy Azure** ](monitoring-overview-activity-logs.md) na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="22a3f-104">In this article, we show how you can use hello Azure portal, PowerShell Cmdlets, or Cross-Platform CLI tooarchive your [**Azure Activity Log**](monitoring-overview-activity-logs.md) in a storage account.</span></span> <span data-ttu-id="22a3f-105">Ta opcja jest przydatna, jeśli chcesz tooretain dłużej niż 90 dni (z pełną kontrolę nad zasady przechowywania hello) dla dziennika aktywności inspekcji analizy statycznej lub kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="22a3f-105">This option is useful if you would like tooretain your Activity Log longer than 90 days (with full control over hello retention policy) for audit, static analysis, or backup.</span></span> <span data-ttu-id="22a3f-106">Jeśli potrzebujesz tylko tooretain zdarzeń przez 90 dni lub mniej można nie ma potrzeby tooset archiwizacji tooa konta magazynu, ponieważ zdarzenia dziennika aktywności są przechowywane w hello platformy Azure przez 90 dni bez włączania archiwizacji.</span><span class="sxs-lookup"><span data-stu-id="22a3f-106">If you only need tooretain your events for 90 days or less you do not need tooset up archival tooa storage account, since Activity Log events are retained in hello Azure platform for 90 days without enabling archival.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="22a3f-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="22a3f-107">Prerequisites</span></span>
<span data-ttu-id="22a3f-108">Przed rozpoczęciem należy zbyt[Utwórz konto magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account) toowhich można archiwizować dziennik aktywności.</span><span class="sxs-lookup"><span data-stu-id="22a3f-108">Before you begin, you need too[create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) toowhich you can archive your Activity Log.</span></span> <span data-ttu-id="22a3f-109">Zdecydowanie zaleca się, że nie należy używać istniejącego konta magazynu z innych, niż monitorowania danych w niej przechowywane, dzięki czemu można lepiej kontrolować dostęp do danych toomonitoring.</span><span class="sxs-lookup"><span data-stu-id="22a3f-109">We highly recommend that you do not use an existing storage account that has other, non-monitoring data stored in it so that you can better control access toomonitoring data.</span></span> <span data-ttu-id="22a3f-110">Jednak jeśli są również archiwizowanie dzienników diagnostycznych i konto magazynu tooa metryki, rozsądne może toouse znaczeniu konto magazynu działanie dziennika również tookeep wszystkie dane monitorowania w centralnej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="22a3f-110">However, if you are also archiving Diagnostic Logs and metrics tooa storage account, it may make sense toouse that storage account for your Activity Log as well tookeep all monitoring data in a central location.</span></span> <span data-ttu-id="22a3f-111">Konto magazynu Hello, którego używasz, musi być konto magazynu ogólnego przeznaczenia, a nie konta magazynu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="22a3f-111">hello storage account you use must be a general purpose storage account, not a blob storage account.</span></span> <span data-ttu-id="22a3f-112">Witaj konta magazynu nie ma w hello toobe tej samej subskrypcji co subskrypcji hello emitowanie dzienniki tak długo, jak hello użytkownik, który konfiguruje ustawienia hello ma odpowiednie RBAC dostępu tooboth subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="22a3f-112">hello storage account does not have toobe in hello same subscription as hello subscription emitting logs as long as hello user who configures hello setting has appropriate RBAC access tooboth subscriptions.</span></span>

## <a name="log-profile"></a><span data-ttu-id="22a3f-113">Profil dziennika</span><span class="sxs-lookup"><span data-stu-id="22a3f-113">Log Profile</span></span>
<span data-ttu-id="22a3f-114">hello tooarchive przy użyciu dowolnej z poniższych metod hello dziennik aktywności, ustaw hello **profilu dziennika** dla subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="22a3f-114">tooarchive hello Activity Log using any of hello methods below, you set hello **Log Profile** for a subscription.</span></span> <span data-ttu-id="22a3f-115">Witaj dziennika profil definiuje typ hello zdarzeń, które są zapisywane lub przesyłane strumieniowo i hello dane wyjściowe — magazynu konta i/lub zdarzenia koncentratora.</span><span class="sxs-lookup"><span data-stu-id="22a3f-115">hello Log Profile defines hello type of events that are stored or streamed and hello outputs—storage account and/or event hub.</span></span> <span data-ttu-id="22a3f-116">Definiuje również zasady przechowywania hello (liczba dni korzystania z tooretain) dla zdarzenia zapisane na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="22a3f-116">It also defines hello retention policy (number of days tooretain) for events stored in a storage account.</span></span> <span data-ttu-id="22a3f-117">Jeśli zasady przechowywania hello ustawiono toozero, zdarzenia są przechowywane w nieskończoność.</span><span class="sxs-lookup"><span data-stu-id="22a3f-117">If hello retention policy is set toozero, events are stored indefinitely.</span></span> <span data-ttu-id="22a3f-118">W przeciwnym razie można go ustawić tooany wartość z zakresu od 1 do 2147483647.</span><span class="sxs-lookup"><span data-stu-id="22a3f-118">Otherwise, this can be set tooany value between 1 and 2147483647.</span></span> <span data-ttu-id="22a3f-119">Zasady przechowywania są stosowane na dzień, więc na powitania koniec dnia (UTC), rejestruje od dnia hello, która jest teraz poza zasady przechowywania hello zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="22a3f-119">Retention policies are applied per-day, so at hello end of a day (UTC), logs from hello day that is now beyond hello retention policy will be deleted.</span></span> <span data-ttu-id="22a3f-120">Na przykład jeśli masz zasady przechowywania jeden dzień początku hello dzisiaj dzień hello hello dzienniki hello dzień przed wczoraj zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="22a3f-120">For example, if you had a retention policy of one day, at hello beginning of hello day today hello logs from hello day before yesterday would be deleted.</span></span> <span data-ttu-id="22a3f-121">[Więcej informacje dziennika tutaj profile](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile).</span><span class="sxs-lookup"><span data-stu-id="22a3f-121">[You can read more about log profiles here](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile).</span></span> 

## <a name="archive-hello-activity-log-using-hello-portal"></a><span data-ttu-id="22a3f-122">Dziennik aktywności za pomocą portalu hello hello archiwum</span><span class="sxs-lookup"><span data-stu-id="22a3f-122">Archive hello Activity Log using hello portal</span></span>
1. <span data-ttu-id="22a3f-123">W portalu powitania kliknij hello **dziennik aktywności** łącze nawigacji po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="22a3f-123">In hello portal, click hello **Activity Log** link on hello left-side navigation.</span></span> <span data-ttu-id="22a3f-124">Jeśli nie widzisz łącze hello dziennik aktywności kliknij hello **więcej usług** najpierw łącza.</span><span class="sxs-lookup"><span data-stu-id="22a3f-124">If you don’t see a link for hello Activity Log, click hello **More Services** link first.</span></span>
   
    ![Przejdź do bloku dziennika tooActivity](media/monitoring-archive-activity-log/act-log-portal-navigate.png)
2. <span data-ttu-id="22a3f-126">U góry hello hello bloku, kliknij przycisk **wyeksportować**.</span><span class="sxs-lookup"><span data-stu-id="22a3f-126">At hello top of hello blade, click **Export**.</span></span>
   
    ![Kliknij przycisk Eksportuj hello](media/monitoring-archive-activity-log/act-log-portal-export-button.png)
3. <span data-ttu-id="22a3f-128">W wyświetlonym bloku hello Sprawdź pole hello **wyeksportować konta magazynu tooa** i wybierz konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="22a3f-128">In hello blade that appears, check hello box for **Export tooa storage account** and select a storage account.</span></span>
   
    ![Ustaw konto magazynu](media/monitoring-archive-activity-log/act-log-portal-export-blade.png)
4. <span data-ttu-id="22a3f-130">Za pomocą suwaka hello lub pola tekstowego, określić liczbę dni, dla których zdarzenia dziennika aktywności powinna być przechowywana w koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="22a3f-130">Using hello slider or text box, define a number of days for which Activity Log events should be kept in your storage account.</span></span> <span data-ttu-id="22a3f-131">Jeśli wolisz toohave dane utrwalone na koncie magazynu hello nieskończoność, ustaw ten numer toozero.</span><span class="sxs-lookup"><span data-stu-id="22a3f-131">If you prefer toohave your data persisted in hello storage account indefinitely, set this number toozero.</span></span>
5. <span data-ttu-id="22a3f-132">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="22a3f-132">Click **Save**.</span></span>

## <a name="archive-hello-activity-log-via-powershell"></a><span data-ttu-id="22a3f-133">Archiwum hello dziennik aktywności za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="22a3f-133">Archive hello Activity Log via PowerShell</span></span>
```
Add-AzureRmLogProfile -Name my_log_profile -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus -RetentionInDays 180 -Categories Write,Delete,Action
```

| <span data-ttu-id="22a3f-134">Właściwość</span><span class="sxs-lookup"><span data-stu-id="22a3f-134">Property</span></span> | <span data-ttu-id="22a3f-135">Wymagane</span><span class="sxs-lookup"><span data-stu-id="22a3f-135">Required</span></span> | <span data-ttu-id="22a3f-136">Opis</span><span class="sxs-lookup"><span data-stu-id="22a3f-136">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="22a3f-137">StorageAccountId</span><span class="sxs-lookup"><span data-stu-id="22a3f-137">StorageAccountId</span></span> |<span data-ttu-id="22a3f-138">Nie</span><span class="sxs-lookup"><span data-stu-id="22a3f-138">No</span></span> |<span data-ttu-id="22a3f-139">Identyfikator zasobu hello konta magazynu toowhich Dzienniki aktywności ma zostać zapisany.</span><span class="sxs-lookup"><span data-stu-id="22a3f-139">Resource ID of hello Storage Account toowhich Activity Logs should be saved.</span></span> |
| <span data-ttu-id="22a3f-140">Lokalizacje</span><span class="sxs-lookup"><span data-stu-id="22a3f-140">Locations</span></span> |<span data-ttu-id="22a3f-141">Tak</span><span class="sxs-lookup"><span data-stu-id="22a3f-141">Yes</span></span> |<span data-ttu-id="22a3f-142">Rozdzielana przecinkami lista regionów, dla których chcesz toocollect dziennik zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="22a3f-142">Comma-separated list of regions for which you would like toocollect Activity Log events.</span></span> <span data-ttu-id="22a3f-143">Można wyświetlić listę wszystkich regionach [, przechodząc na stronę tej strony](https://azure.microsoft.com/en-us/regions) lub za pomocą [hello interfejsu API REST zarządzania Azure](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span><span class="sxs-lookup"><span data-stu-id="22a3f-143">You can view a list of all regions [by visiting this page](https://azure.microsoft.com/en-us/regions) or by using [hello Azure Management REST API](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span></span> |
| <span data-ttu-id="22a3f-144">retentionInDays</span><span class="sxs-lookup"><span data-stu-id="22a3f-144">RetentionInDays</span></span> |<span data-ttu-id="22a3f-145">Tak</span><span class="sxs-lookup"><span data-stu-id="22a3f-145">Yes</span></span> |<span data-ttu-id="22a3f-146">Liczba dni dla zdarzenia, które mają być przechowywane, od 1 do 2147483647.</span><span class="sxs-lookup"><span data-stu-id="22a3f-146">Number of days for which events should be retained, between 1 and 2147483647.</span></span> <span data-ttu-id="22a3f-147">Wartość zero przechowuje dzienniki hello nieskończoność (zawsze).</span><span class="sxs-lookup"><span data-stu-id="22a3f-147">A value of zero stores hello logs indefinitely (forever).</span></span> |
| <span data-ttu-id="22a3f-148">Kategorie</span><span class="sxs-lookup"><span data-stu-id="22a3f-148">Categories</span></span> |<span data-ttu-id="22a3f-149">Tak</span><span class="sxs-lookup"><span data-stu-id="22a3f-149">Yes</span></span> |<span data-ttu-id="22a3f-150">Rozdzielana przecinkami lista kategorii zdarzeń, które powinny być zbierane.</span><span class="sxs-lookup"><span data-stu-id="22a3f-150">Comma-separated list of event categories that should be collected.</span></span> <span data-ttu-id="22a3f-151">Możliwe wartości to zapisu, usuwania i akcji.</span><span class="sxs-lookup"><span data-stu-id="22a3f-151">Possible values are Write, Delete, and Action.</span></span> |

## <a name="archive-hello-activity-log-via-cli"></a><span data-ttu-id="22a3f-152">Archiwum hello dziennik aktywności za pomocą interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="22a3f-152">Archive hello Activity Log via CLI</span></span>
```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --locations global,westus,eastus,northeurope --retentionInDays 180 –categories Write,Delete,Action
```

| <span data-ttu-id="22a3f-153">Właściwość</span><span class="sxs-lookup"><span data-stu-id="22a3f-153">Property</span></span> | <span data-ttu-id="22a3f-154">Wymagane</span><span class="sxs-lookup"><span data-stu-id="22a3f-154">Required</span></span> | <span data-ttu-id="22a3f-155">Opis</span><span class="sxs-lookup"><span data-stu-id="22a3f-155">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="22a3f-156">name</span><span class="sxs-lookup"><span data-stu-id="22a3f-156">name</span></span> |<span data-ttu-id="22a3f-157">Tak</span><span class="sxs-lookup"><span data-stu-id="22a3f-157">Yes</span></span> |<span data-ttu-id="22a3f-158">Nazwa profilu dziennika.</span><span class="sxs-lookup"><span data-stu-id="22a3f-158">Name of your log profile.</span></span> |
| <span data-ttu-id="22a3f-159">storageId</span><span class="sxs-lookup"><span data-stu-id="22a3f-159">storageId</span></span> |<span data-ttu-id="22a3f-160">Nie</span><span class="sxs-lookup"><span data-stu-id="22a3f-160">No</span></span> |<span data-ttu-id="22a3f-161">Identyfikator zasobu hello konta magazynu toowhich Dzienniki aktywności ma zostać zapisany.</span><span class="sxs-lookup"><span data-stu-id="22a3f-161">Resource ID of hello Storage Account toowhich Activity Logs should be saved.</span></span> |
| <span data-ttu-id="22a3f-162">Lokalizacje</span><span class="sxs-lookup"><span data-stu-id="22a3f-162">locations</span></span> |<span data-ttu-id="22a3f-163">Tak</span><span class="sxs-lookup"><span data-stu-id="22a3f-163">Yes</span></span> |<span data-ttu-id="22a3f-164">Rozdzielana przecinkami lista regionów, dla których chcesz toocollect dziennik zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="22a3f-164">Comma-separated list of regions for which you would like toocollect Activity Log events.</span></span> <span data-ttu-id="22a3f-165">Można wyświetlić listę wszystkich regionach [, przechodząc na stronę tej strony](https://azure.microsoft.com/en-us/regions) lub za pomocą [hello interfejsu API REST zarządzania Azure](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span><span class="sxs-lookup"><span data-stu-id="22a3f-165">You can view a list of all regions [by visiting this page](https://azure.microsoft.com/en-us/regions) or by using [hello Azure Management REST API](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span></span> |
| <span data-ttu-id="22a3f-166">retentionInDays</span><span class="sxs-lookup"><span data-stu-id="22a3f-166">retentionInDays</span></span> |<span data-ttu-id="22a3f-167">Tak</span><span class="sxs-lookup"><span data-stu-id="22a3f-167">Yes</span></span> |<span data-ttu-id="22a3f-168">Liczba dni dla zdarzenia, które mają być przechowywane, od 1 do 2147483647.</span><span class="sxs-lookup"><span data-stu-id="22a3f-168">Number of days for which events should be retained, between 1 and 2147483647.</span></span> <span data-ttu-id="22a3f-169">Wartość zero będą przechowywane dzienniki hello nieskończoność (zawsze).</span><span class="sxs-lookup"><span data-stu-id="22a3f-169">A value of zero will store hello logs indefinitely (forever).</span></span> |
| <span data-ttu-id="22a3f-170">Kategorie</span><span class="sxs-lookup"><span data-stu-id="22a3f-170">categories</span></span> |<span data-ttu-id="22a3f-171">Tak</span><span class="sxs-lookup"><span data-stu-id="22a3f-171">Yes</span></span> |<span data-ttu-id="22a3f-172">Rozdzielana przecinkami lista kategorii zdarzeń, które powinny być zbierane.</span><span class="sxs-lookup"><span data-stu-id="22a3f-172">Comma-separated list of event categories that should be collected.</span></span> <span data-ttu-id="22a3f-173">Możliwe wartości to zapisu, usuwania i akcji.</span><span class="sxs-lookup"><span data-stu-id="22a3f-173">Possible values are Write, Delete, and Action.</span></span> |

## <a name="storage-schema-of-hello-activity-log"></a><span data-ttu-id="22a3f-174">Schemat magazynu hello dziennik aktywności</span><span class="sxs-lookup"><span data-stu-id="22a3f-174">Storage schema of hello Activity Log</span></span>
<span data-ttu-id="22a3f-175">Po skonfigurowaniu archiwizacji, kontenera magazynu zostanie utworzony na koncie magazynu hello zaraz po wystąpieniu zdarzenia dziennika aktywności.</span><span class="sxs-lookup"><span data-stu-id="22a3f-175">Once you have set up archival, a storage container will be created in hello storage account as soon as an Activity Log event occurs.</span></span> <span data-ttu-id="22a3f-176">obiekty BLOB Hello w kontenerze hello wykonaj hello takiego samego formatu między hello dziennika aktywności i dzienników diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="22a3f-176">hello blobs within hello container follow hello same format across hello Activity Log and Diagnostic Logs.</span></span> <span data-ttu-id="22a3f-177">Struktura Hello tych obiektów blob jest:</span><span class="sxs-lookup"><span data-stu-id="22a3f-177">hello structure of these blobs is:</span></span>

> <span data-ttu-id="22a3f-178">szczegółowe informacje operacyjne dzienniki/nazwa-= domyślne/resourceId = / SUBSKRYPCJI / {identyfikator subskrypcji} / y = {czterocyfrowy rok liczbowych} / m = {dwucyfrowe liczbowych month} / d = {dwucyfrowe liczbą dzień} / h = {dwucyfrowe 24-godzinnym hour}/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="22a3f-178">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/{subscription ID}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="22a3f-179">Na przykład może być nazwa obiektu blob:</span><span class="sxs-lookup"><span data-stu-id="22a3f-179">For example, a blob name might be:</span></span>

> <span data-ttu-id="22a3f-180">insights-Operational-Logs/name=default/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/y=2016/m=08/d=22/h=18/m=00/PT1H.JSON</span><span class="sxs-lookup"><span data-stu-id="22a3f-180">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="22a3f-181">Każdy obiekt blob PT1H.json zawiera obiektu blob JSON zdarzeń, które wystąpiły w ciągu godziny hello określona w adresie URL obiektu blob hello (np. h = 12).</span><span class="sxs-lookup"><span data-stu-id="22a3f-181">Each PT1H.json blob contains a JSON blob of events that occurred within hello hour specified in hello blob URL (e.g. h=12).</span></span> <span data-ttu-id="22a3f-182">Podczas hello obecny godzinę zdarzenia są toohello dołączany plik PT1H.json miarę ich występowania.</span><span class="sxs-lookup"><span data-stu-id="22a3f-182">During hello present hour, events are appended toohello PT1H.json file as they occur.</span></span> <span data-ttu-id="22a3f-183">Witaj wartość minuty (m = 00) jest zawsze 00, ponieważ dziennik zdarzeń są podzielone na poszczególne obiekty BLOB na godzinę.</span><span class="sxs-lookup"><span data-stu-id="22a3f-183">hello minute value (m=00) is always 00, since Activity Log events are broken into individual blobs per hour.</span></span>

<span data-ttu-id="22a3f-184">W pliku PT1H.json hello każde zdarzenie jest przechowywane w tablicy rekordy"hello", po tym formacie:</span><span class="sxs-lookup"><span data-stu-id="22a3f-184">Within hello PT1H.json file, each event is stored in hello “records” array, following this format:</span></span>

```
{
    "records": [
        {
            "time": "2015-01-21T22:14:26.9792776Z",
            "resourceId": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
            "operationName": "microsoft.support/supporttickets/write",
            "category": "Write",
            "resultType": "Success",
            "resultSignature": "Succeeded.Created",
            "durationMs": 2826,
            "callerIpAddress": "111.111.111.11",
            "correlationId": "c776f9f4-36e5-4e0e-809b-c9b3c3fb62a8",
            "identity": {
                "authorization": {
                    "scope": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
                    "action": "microsoft.support/supporttickets/write",
                    "evidence": {
                        "role": "Subscription Admin"
                    }
                },
                "claims": {
                    "aud": "https://management.core.windows.net/",
                    "iss": "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",
                    "iat": "1421876371",
                    "nbf": "1421876371",
                    "exp": "1421880271",
                    "ver": "1.0",
                    "http://schemas.microsoft.com/identity/claims/tenantid": "1e8d8218-c5e7-4578-9acc-9abbd5d23315 ",
                    "http://schemas.microsoft.com/claims/authnmethodsreferences": "pwd",
                    "http://schemas.microsoft.com/identity/claims/objectidentifier": "2468adf0-8211-44e3-95xq-85137af64708",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "admin@contoso.com",
                    "puid": "20030000801A118C",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": "9vckmEGF7zDKk1YzIY8k0t1_EAPaXoeHyPRn6f413zM",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname": "John",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname": "Smith",
                    "name": "John Smith",
                    "groups": "cacfe77c-e058-4712-83qw-f9b08849fd60,7f71d11d-4c41-4b23-99d2-d32ce7aa621c,31522864-0578-4ea0-9gdc-e66cc564d18c",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name": " admin@contoso.com",
                    "appid": "c44b4083-3bq0-49c1-b47d-974e53cbdf3c",
                    "appidacr": "2",
                    "http://schemas.microsoft.com/identity/claims/scope": "user_impersonation",
                    "http://schemas.microsoft.com/claims/authnclassreference": "1"
                }
            },
            "level": "Information",
            "location": "global",
            "properties": {
                "statusCode": "Created",
                "serviceRequestId": "50d5cddb-8ca0-47ad-9b80-6cde2207f97c"
            }
        }
    ]
}
```


| <span data-ttu-id="22a3f-185">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="22a3f-185">Element name</span></span> | <span data-ttu-id="22a3f-186">Opis</span><span class="sxs-lookup"><span data-stu-id="22a3f-186">Description</span></span> |
| --- | --- |
| <span data-ttu-id="22a3f-187">time</span><span class="sxs-lookup"><span data-stu-id="22a3f-187">time</span></span> |<span data-ttu-id="22a3f-188">Znacznik czasu w momencie hello zdarzeń został wygenerowany przez hello przetwarzania usługi Azure hello żądanie odpowiednie zdarzenie hello.</span><span class="sxs-lookup"><span data-stu-id="22a3f-188">Timestamp when hello event was generated by hello Azure service processing hello request corresponding hello event.</span></span> |
| <span data-ttu-id="22a3f-189">resourceId</span><span class="sxs-lookup"><span data-stu-id="22a3f-189">resourceId</span></span> |<span data-ttu-id="22a3f-190">Identyfikator zasobu hello wpływ na zasobów.</span><span class="sxs-lookup"><span data-stu-id="22a3f-190">Resource ID of hello impacted resource.</span></span> |
| <span data-ttu-id="22a3f-191">operationName</span><span class="sxs-lookup"><span data-stu-id="22a3f-191">operationName</span></span> |<span data-ttu-id="22a3f-192">Nazwa operacji hello.</span><span class="sxs-lookup"><span data-stu-id="22a3f-192">Name of hello operation.</span></span> |
| <span data-ttu-id="22a3f-193">category</span><span class="sxs-lookup"><span data-stu-id="22a3f-193">category</span></span> |<span data-ttu-id="22a3f-194">Kategoria hello akcji, np.</span><span class="sxs-lookup"><span data-stu-id="22a3f-194">Category of hello action, eg.</span></span> <span data-ttu-id="22a3f-195">Zapis, Odczyt, akcji.</span><span class="sxs-lookup"><span data-stu-id="22a3f-195">Write, Read, Action.</span></span> |
| <span data-ttu-id="22a3f-196">resultType</span><span class="sxs-lookup"><span data-stu-id="22a3f-196">resultType</span></span> |<span data-ttu-id="22a3f-197">Witaj typu wyniku hello, np.</span><span class="sxs-lookup"><span data-stu-id="22a3f-197">hello type of hello result, eg.</span></span> <span data-ttu-id="22a3f-198">Sukces, Niepowodzenie, Start</span><span class="sxs-lookup"><span data-stu-id="22a3f-198">Success, Failure, Start</span></span> |
| <span data-ttu-id="22a3f-199">resultSignature</span><span class="sxs-lookup"><span data-stu-id="22a3f-199">resultSignature</span></span> |<span data-ttu-id="22a3f-200">Zależy od typu zasobu hello.</span><span class="sxs-lookup"><span data-stu-id="22a3f-200">Depends on hello resource type.</span></span> |
| <span data-ttu-id="22a3f-201">durationMs</span><span class="sxs-lookup"><span data-stu-id="22a3f-201">durationMs</span></span> |<span data-ttu-id="22a3f-202">Czas trwania operacji hello w milisekundach</span><span class="sxs-lookup"><span data-stu-id="22a3f-202">Duration of hello operation in milliseconds</span></span> |
| <span data-ttu-id="22a3f-203">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="22a3f-203">callerIpAddress</span></span> |<span data-ttu-id="22a3f-204">Adres IP hello użytkownik wykonał operację hello, oświadczenia UPN lub nazwy SPN oświadczenia na podstawie dostępności.</span><span class="sxs-lookup"><span data-stu-id="22a3f-204">IP address of hello user who has performed hello operation, UPN claim, or SPN claim based on availability.</span></span> |
| <span data-ttu-id="22a3f-205">correlationId</span><span class="sxs-lookup"><span data-stu-id="22a3f-205">correlationId</span></span> |<span data-ttu-id="22a3f-206">Zazwyczaj identyfikator GUID w formacie ciągu hello.</span><span class="sxs-lookup"><span data-stu-id="22a3f-206">Usually a GUID in hello string format.</span></span> <span data-ttu-id="22a3f-207">Zdarzenia, które mają correlationId należą toohello tę samą akcję pełny.</span><span class="sxs-lookup"><span data-stu-id="22a3f-207">Events that share a correlationId belong toohello same uber action.</span></span> |
| <span data-ttu-id="22a3f-208">identity</span><span class="sxs-lookup"><span data-stu-id="22a3f-208">identity</span></span> |<span data-ttu-id="22a3f-209">Obiekt blob JSON opisujące hello autoryzacji i oświadczenia.</span><span class="sxs-lookup"><span data-stu-id="22a3f-209">JSON blob describing hello authorization and claims.</span></span> |
| <span data-ttu-id="22a3f-210">Autoryzacji</span><span class="sxs-lookup"><span data-stu-id="22a3f-210">authorization</span></span> |<span data-ttu-id="22a3f-211">Obiekt typu blob właściwości RBAC hello zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="22a3f-211">Blob of RBAC properties of hello event.</span></span> <span data-ttu-id="22a3f-212">Obejmuje zazwyczaj hello właściwości "Akcja", "rola" i "zakresu".</span><span class="sxs-lookup"><span data-stu-id="22a3f-212">Usually includes hello “action”, “role” and “scope” properties.</span></span> |
| <span data-ttu-id="22a3f-213">poziom</span><span class="sxs-lookup"><span data-stu-id="22a3f-213">level</span></span> |<span data-ttu-id="22a3f-214">Poziom hello zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="22a3f-214">Level of hello event.</span></span> <span data-ttu-id="22a3f-215">Jeden z hello następujące wartości: "Krytyczne", "Błąd", "Ostrzeżenie", "Informacyjny" i "Pełne"</span><span class="sxs-lookup"><span data-stu-id="22a3f-215">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="22a3f-216">location</span><span class="sxs-lookup"><span data-stu-id="22a3f-216">location</span></span> |<span data-ttu-id="22a3f-217">Region, w którym miejscu hello wystąpił (lub globalne).</span><span class="sxs-lookup"><span data-stu-id="22a3f-217">Region in which hello location occurred (or global).</span></span> |
| <span data-ttu-id="22a3f-218">properties</span><span class="sxs-lookup"><span data-stu-id="22a3f-218">properties</span></span> |<span data-ttu-id="22a3f-219">Zestaw `<Key, Value>` pary (tj. Słownik) opisujący szczegóły hello hello zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="22a3f-219">Set of `<Key, Value>` pairs (i.e. Dictionary) describing hello details of hello event.</span></span> |

> [!NOTE]
> <span data-ttu-id="22a3f-220">właściwości Hello i użycia tych właściwości zależy od zasobu hello.</span><span class="sxs-lookup"><span data-stu-id="22a3f-220">hello properties and usage of those properties can vary depending on hello resource.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="22a3f-221">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="22a3f-221">Next steps</span></span>
* [<span data-ttu-id="22a3f-222">Pobierać obiekty BLOB do analizy</span><span class="sxs-lookup"><span data-stu-id="22a3f-222">Download blobs for analysis</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)
* [<span data-ttu-id="22a3f-223">Strumienia hello dziennik aktywności tooEvent koncentratory</span><span class="sxs-lookup"><span data-stu-id="22a3f-223">Stream hello Activity Log tooEvent Hubs</span></span>](monitoring-stream-activity-logs-event-hubs.md)
* [<span data-ttu-id="22a3f-224">Więcej informacji na temat hello dziennik aktywności</span><span class="sxs-lookup"><span data-stu-id="22a3f-224">Read more about hello Activity Log</span></span>](monitoring-overview-activity-logs.md)

