---
title: "Stan maszyny Wirtualnej Azure tooschedule tagów w formacie JSON aaaUse | Dokumentacja firmy Microsoft"
description: "W tym artykule przedstawiono, jak ciągi toouse JSON na tagi tooautomate hello planowanie uruchamiania maszyny Wirtualnej i zamykania."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 6afed5d2-e939-4749-8b2c-9312b4c16fb2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: magoedte;paulomarquesc
ms.openlocfilehash: f6bbf1dea1c193e5d1010f12f3b1ed63562f9daf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario-using-json-formatted-tags-toocreate-a-schedule-for-azure-vm-startup-and-shutdown"></a><span data-ttu-id="6bb1d-103">Scenariusz automatyzacji Azure: przy użyciu formacie JSON tagów toocreate harmonogram uruchamiania maszyny Wirtualnej platformy Azure i zamykania</span><span class="sxs-lookup"><span data-stu-id="6bb1d-103">Azure Automation scenario: Using JSON-formatted tags toocreate a schedule for Azure VM startup and shutdown</span></span>
<span data-ttu-id="6bb1d-104">Klienci często mają tooschedule hello uruchamiania i zamykania maszyn wirtualnych toohelp obniżenie kosztów subskrypcji lub obsługuje wymagań technicznych i biznesowych.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-104">Customers often want tooschedule hello startup and shutdown of virtual machines toohelp reduce subscription costs or support business and technical requirements.</span></span>

<span data-ttu-id="6bb1d-105">Witaj następujący scenariusz umożliwia tooset się automatycznego uruchamiania i wyłączania maszyn wirtualnych przy użyciu tagu o nazwie harmonogram na poziomie grupy zasobów lub maszyny wirtualnej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-105">hello following scenario enables you tooset up automated startup and shutdown of your VMs by using a tag called Schedule at a resource group level or virtual machine level in Azure.</span></span> <span data-ttu-id="6bb1d-106">Ten harmonogram można skonfigurować w niedzielę tooSaturday czas uruchamiania i czasu zamykania.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-106">This schedule can be configured from Sunday tooSaturday with a startup time and shutdown time.</span></span>

<span data-ttu-id="6bb1d-107">Mamy niektóre opcje poza pole.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-107">We do have some out-of-the-box options.</span></span> <span data-ttu-id="6bb1d-108">Należą do nich:</span><span class="sxs-lookup"><span data-stu-id="6bb1d-108">These include:</span></span>

* <span data-ttu-id="6bb1d-109">[Zestawy skalowania maszyny wirtualnej](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) przy użyciu ustawień automatycznego skalowania, które pozwalają tooscale przychodzący lub wychodzący.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-109">[Virtual machine scale sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) with autoscale settings that enable you tooscale in or out.</span></span>
* <span data-ttu-id="6bb1d-110">[DevTest Labs](../devtest-lab/devtest-lab-overview.md) usługi, która ma wbudowaną funkcję hello planowania operacji uruchamiania i wyłączania.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-110">[DevTest Labs](../devtest-lab/devtest-lab-overview.md) service, which has hello built-in capability of scheduling startup and shutdown operations.</span></span>

<span data-ttu-id="6bb1d-111">Jednak te opcje obsługują tylko określonych scenariuszy i nie może być zastosowane tooinfrastructure jako — usługa (IaaS), maszynach wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-111">However, these options only support specific scenarios and cannot be applied tooinfrastructure-as-a-service (IaaS) VMs.</span></span>

<span data-ttu-id="6bb1d-112">Podczas hello tag harmonogramu jest stosowane tooa grupy zasobów, jest również zastosowane tooall maszyn wirtualnych w tej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-112">When hello Schedule tag is applied tooa resource group, it's also applied tooall virtual machines inside that resource group.</span></span> <span data-ttu-id="6bb1d-113">Jeśli harmonogram jest również tooa bezpośrednio zastosowane maszyny Wirtualnej, harmonogram ostatniego hello ma pierwszeństwo przed w hello w następującej kolejności:</span><span class="sxs-lookup"><span data-stu-id="6bb1d-113">If a schedule is also directly applied tooa VM, hello last schedule takes precedence in hello following order:</span></span>

1. <span data-ttu-id="6bb1d-114">Grupa zasobów zastosowane tooa harmonogramu</span><span class="sxs-lookup"><span data-stu-id="6bb1d-114">Schedule applied tooa resource group</span></span>
2. <span data-ttu-id="6bb1d-115">Zaplanuj grupy zasobów tooa zastosowane i maszyny wirtualnej w grupie zasobów hello</span><span class="sxs-lookup"><span data-stu-id="6bb1d-115">Schedule applied tooa resource group and virtual machine in hello resource group</span></span>
3. <span data-ttu-id="6bb1d-116">Maszyna wirtualna tooa harmonogram stosowane</span><span class="sxs-lookup"><span data-stu-id="6bb1d-116">Schedule applied tooa virtual machine</span></span>

<span data-ttu-id="6bb1d-117">W tym scenariuszu zasadniczo przyjmuje ciągu JSON w określonym formacie i dodaje go jako wartość hello tagu o nazwie harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-117">This scenario essentially takes a JSON string with a specified format and adds it as hello value for a tag called Schedule.</span></span> <span data-ttu-id="6bb1d-118">Następnie element runbook zawiera listę wszystkich grup zasobów i maszyn wirtualnych i identyfikuje hello harmonogramy dla każdej maszyny Wirtualnej, oparte na scenariusze hello wymienione wcześniej.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-118">Then a runbook lists all resource groups and virtual machines and identifies hello schedules for each VM based on hello scenarios listed earlier.</span></span> <span data-ttu-id="6bb1d-119">Następnie hello maszyn wirtualnych, które mają harmonogramy dołączony w pętli i ocenia, jakie działania należy podjąć.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-119">Next it loops through hello VMs that have schedules attached and evaluates what action should be taken.</span></span> <span data-ttu-id="6bb1d-120">Na przykład określają one, które maszyny wirtualne muszą toobe zatrzymana, zamknięta lub ignorowane.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-120">For example, it determines which VMs need toobe stopped, shut down, or ignored.</span></span>

<span data-ttu-id="6bb1d-121">Te elementy runbook uwierzytelniania za pomocą hello [konta Uruchom jako platformy Azure](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="6bb1d-121">These runbooks authenticate by using hello [Azure Run As account](automation-sec-configure-azure-runas-account.md).</span></span>

## <a name="download-hello-runbooks-for-hello-scenario"></a><span data-ttu-id="6bb1d-122">Pobierz elementy runbook hello hello scenariusza</span><span class="sxs-lookup"><span data-stu-id="6bb1d-122">Download hello runbooks for hello scenario</span></span>
<span data-ttu-id="6bb1d-123">Ten scenariusz obejmuje cztery elementy runbook przepływu pracy programu PowerShell, które można pobrać z hello [galerii TechNet](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) lub hello [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) repozytorium dla tego projektu.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-123">This scenario consists of four PowerShell Workflow runbooks that you can download from hello [TechNet Gallery](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) or hello [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) repository for this project.</span></span>

| <span data-ttu-id="6bb1d-124">Element Runbook</span><span class="sxs-lookup"><span data-stu-id="6bb1d-124">Runbook</span></span> | <span data-ttu-id="6bb1d-125">Opis</span><span class="sxs-lookup"><span data-stu-id="6bb1d-125">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6bb1d-126">ResourceSchedule testu</span><span class="sxs-lookup"><span data-stu-id="6bb1d-126">Test-ResourceSchedule</span></span> |<span data-ttu-id="6bb1d-127">Sprawdza harmonogram każdej maszyny wirtualnej, a następnie wykonuje zamykania lub uruchamiania w zależności od hello harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-127">Checks each virtual machine schedule and performs shutdown or startup depending on hello schedule.</span></span> |
| <span data-ttu-id="6bb1d-128">Dodaj ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="6bb1d-128">Add-ResourceSchedule</span></span> |<span data-ttu-id="6bb1d-129">Dodaje hello harmonogram tag tooa maszyny Wirtualnej lub grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-129">Adds hello Schedule tag tooa VM or resource group.</span></span> |
| <span data-ttu-id="6bb1d-130">ResourceSchedule aktualizacji</span><span class="sxs-lookup"><span data-stu-id="6bb1d-130">Update-ResourceSchedule</span></span> |<span data-ttu-id="6bb1d-131">Modyfikuje hello istniejącego harmonogramu znacznika przez zamianę nowy.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-131">Modifies hello existing Schedule tag by replacing it with a new one.</span></span> |
| <span data-ttu-id="6bb1d-132">Usuń ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="6bb1d-132">Remove-ResourceSchedule</span></span> |<span data-ttu-id="6bb1d-133">Usuwa hello harmonogram tagu z maszyny Wirtualnej lub grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-133">Removes hello Schedule tag from a VM or resource group.</span></span> |

## <a name="install-and-configure-this-scenario"></a><span data-ttu-id="6bb1d-134">Instalowanie i konfigurowanie tego scenariusza</span><span class="sxs-lookup"><span data-stu-id="6bb1d-134">Install and configure this scenario</span></span>
### <a name="install-and-publish-hello-runbooks"></a><span data-ttu-id="6bb1d-135">Instalowanie i publikować elementy runbook hello</span><span class="sxs-lookup"><span data-stu-id="6bb1d-135">Install and publish hello runbooks</span></span>
<span data-ttu-id="6bb1d-136">Po pobraniu hello elementów runbook, można je zaimportować za pomocą procedury hello w [Tworzenie lub importowanie elementu runbook automatyzacji Azure](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation).</span><span class="sxs-lookup"><span data-stu-id="6bb1d-136">After downloading hello runbooks, you can import them by using hello procedure in [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation).</span></span>  <span data-ttu-id="6bb1d-137">Każdy element runbook należy opublikować po jego został pomyślnie zaimportowany na koncie automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-137">Publish each runbook after it has been successfully imported into your Automation account.</span></span>

### <a name="add-a-schedule-toohello-test-resourceschedule-runbook"></a><span data-ttu-id="6bb1d-138">Dodaj element runbook toohello ResourceSchedule testu harmonogramu</span><span class="sxs-lookup"><span data-stu-id="6bb1d-138">Add a schedule toohello Test-ResourceSchedule runbook</span></span>
<span data-ttu-id="6bb1d-139">Wykonaj te kroki tooenable hello harmonogramu dla elementu runbook ResourceSchedule testu hello.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-139">Follow these steps tooenable hello schedule for hello Test-ResourceSchedule runbook.</span></span> <span data-ttu-id="6bb1d-140">Jest to hello elementu runbook, która sprawdza maszyn wirtualnych powinny być uruchamiane, zamknięta, lub w lewo, ponieważ jest.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-140">This is hello runbook that verifies which virtual machines should be started, shut down, or left as is.</span></span>

1. <span data-ttu-id="6bb1d-141">Z hello portalu Azure, otwórz Twoje konto usługi Automatyzacja, a następnie kliknij hello **elementów Runbook** kafelka.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-141">From hello Azure portal, open your Automation account, and then click hello **Runbooks** tile.</span></span>
2. <span data-ttu-id="6bb1d-142">Na powitania **ResourceSchedule testu** bloku, kliknij przycisk hello **harmonogramy** kafelka.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-142">On hello **Test-ResourceSchedule** blade, click hello **Schedules** tile.</span></span>
3. <span data-ttu-id="6bb1d-143">Na powitania **harmonogramy** bloku, kliknij przycisk **Dodaj harmonogram**.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-143">On hello **Schedules** blade, click **Add a schedule**.</span></span>
4. <span data-ttu-id="6bb1d-144">Na powitania **harmonogramy** bloku, wybierz opcję **powiązania elementu runbook tooyour harmonogram**.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-144">On hello **Schedules** blade, select **Link a schedule tooyour runbook**.</span></span> <span data-ttu-id="6bb1d-145">Następnie wybierz **Utwórz nowy harmonogram**.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-145">Then select **Create a new schedule**.</span></span>
5. <span data-ttu-id="6bb1d-146">Na powitania **nowy harmonogram** bloku, wpisz nazwę hello tego harmonogramu, na przykład: *HourlyExecution*.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-146">On hello **New schedule** blade, type in hello name of this schedule, for example: *HourlyExecution*.</span></span>
6. <span data-ttu-id="6bb1d-147">Dla harmonogramu hello **Start**, ustaw hello początkowy czas tooan godzina przyrostu.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-147">For hello schedule **Start**, set hello start time tooan hour increment.</span></span>
7. <span data-ttu-id="6bb1d-148">Wybierz **cyklu**, a następnie **powtarzanie co interwał**, wybierz pozycję **1 godzina**.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-148">Select **Recurrence**, and then for **Recur every interval**, select **1 hour**.</span></span>
8. <span data-ttu-id="6bb1d-149">Sprawdź, czy **ustawienia okresu ważności** ustawiono zbyt**nr**, a następnie kliknij przycisk **Utwórz** toosave nowego harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-149">Verify that **Set expiration** is set too**No**, and then click **Create** toosave your new schedule.</span></span>
9. <span data-ttu-id="6bb1d-150">Na powitania **Runbook harmonogram** bloku opcji wybierz **parametry i ustawienia uruchamiania**.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-150">On hello **Schedule Runbook** options blade, select **Parameters and run settings**.</span></span> <span data-ttu-id="6bb1d-151">W hello testu ResourceSchedule **parametry** bloku, wprowadź nazwę hello subskrypcji w hello **Nazwa subskrypcji** pola.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-151">In hello Test-ResourceSchedule **Parameters** blade, enter hello name of your subscription in hello **SubscriptionName** field.</span></span>  <span data-ttu-id="6bb1d-152">Jest to parametr tylko hello, która jest wymagana dla elementu runbook hello.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-152">This is hello only parameter that's required for hello runbook.</span></span>  <span data-ttu-id="6bb1d-153">Po zakończeniu kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-153">When you're finished, click **OK**.</span></span>

<span data-ttu-id="6bb1d-154">po jego ukończeniu harmonogram Hello powinna wyglądać hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="6bb1d-154">hello runbook schedule should look like hello following when it's completed:</span></span>

![Skonfigurowany ResourceSchedule testu elementu runbook](./media/automation-scenario-start-stop-vm-wjson-tags/automation-schedule-config.png)<br>

## <a name="format-hello-json-string"></a><span data-ttu-id="6bb1d-156">Witaj formatu ciągu JSON</span><span class="sxs-lookup"><span data-stu-id="6bb1d-156">Format hello JSON string</span></span>
<span data-ttu-id="6bb1d-157">To rozwiązanie zasadniczo ma JSON ciągu na określony format i dodaje go jako wartość hello tagu o nazwie harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-157">This solution basically takes a JSON string with a specified format and adds it as hello value for a tag called Schedule.</span></span> <span data-ttu-id="6bb1d-158">Następnie element runbook zawiera listę wszystkich grup zasobów i maszyn wirtualnych i identyfikuje hello harmonogramy dla każdej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-158">Then a runbook lists all resource groups and virtual machines and identifies hello schedules for each virtual machine.</span></span>

<span data-ttu-id="6bb1d-159">Element runbook Hello pętli hello maszyn wirtualnych, które mają harmonogramy dołączona i sprawdza, jakie działania należy podjąć.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-159">hello runbook loops over hello virtual machines that have schedules attached and checks what actions should be taken.</span></span> <span data-ttu-id="6bb1d-160">Witaj poniżej znajduje się przykład sposobu rozwiązania hello powinien być sformatowany:</span><span class="sxs-lookup"><span data-stu-id="6bb1d-160">hello following is an example of how hello solutions should be formatted:</span></span>

```json
{
    "TzId": "Eastern Standard Time",
    "0": {
        "S": "11",
        "E": "17"
    },
    "1": {
        "S": "9",
        "E": "19"
    },
    "2": {
        "S": "9",
        "E": "19"
    },
}
```

<span data-ttu-id="6bb1d-161">Oto niektóre szczegółowe informacje na temat tej struktury:</span><span class="sxs-lookup"><span data-stu-id="6bb1d-161">Here is some detailed information about this structure:</span></span>

1. <span data-ttu-id="6bb1d-162">format Hello tej struktury JSON jest zoptymalizowany toowork wokół hello 256 znaków ograniczenie wartości jeden tag na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-162">hello format of this JSON structure is optimized toowork around hello 256-character limitation of a single tag value in Azure.</span></span>
2. <span data-ttu-id="6bb1d-163">*TzId* reprezentuje hello strefy czasowej hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-163">*TzId* represents hello time zone of hello virtual machine.</span></span> <span data-ttu-id="6bb1d-164">Ten identyfikator można uzyskać za pomocą klasy TimeZoneInfo .NET hello w sesji programu PowerShell —**[System.TimeZoneInfo]:: GetSystemTimeZones()**.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-164">This ID can be obtained by using hello TimeZoneInfo .NET class in a PowerShell session--**[System.TimeZoneInfo]::GetSystemTimeZones()**.</span></span>

   ![GetSystemTimeZones w programie PowerShell](./media/automation-scenario-start-stop-vm-wjson-tags/automation-get-timzone-powershell.png)

   * <span data-ttu-id="6bb1d-166">Dni robocze są reprezentowane z wartością liczbową zero toosix.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-166">Weekdays are represented with a numeric value of zero toosix.</span></span> <span data-ttu-id="6bb1d-167">Witaj zero jest równa niedzielę.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-167">hello value zero equals Sunday.</span></span>
   * <span data-ttu-id="6bb1d-168">Witaj godzina rozpoczęcia jest reprezentowana z hello **S** atrybutu i jego wartość jest w formacie 24-godzinnym.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-168">hello start time is represented with hello **S** attribute, and its value is in a 24-hour format.</span></span>
   * <span data-ttu-id="6bb1d-169">Witaj czas zakończenia lub zamknięcie odpowiada z hello **E** atrybutu i jego wartość jest w formacie 24-godzinnym.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-169">hello end or shutdown time is represented with hello **E** attribute, and its value is in a 24-hour format.</span></span>

     <span data-ttu-id="6bb1d-170">Jeśli hello **S** i **E** atrybuty każdego mają wartość zero (0), hello maszyny wirtualnej pozostanie w jej obecnym stanie w czasie hello szacowania.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-170">If hello **S** and **E** attributes each have a value of zero (0), hello virtual machine will be left in its present state at hello time of evaluation.</span></span>
3. <span data-ttu-id="6bb1d-171">Jeśli chcesz tooskip oceny dla określonego dnia tygodnia hello, nie dodawaj sekcji za ten dzień tygodnia hello.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-171">If you want tooskip evaluation for a specific day of hello week, don’t add a section for that day of hello week.</span></span> <span data-ttu-id="6bb1d-172">Poniższy przykład, tylko poniedziałek jest oceniane hello i hello innych dni tygodnia hello są ignorowane:</span><span class="sxs-lookup"><span data-stu-id="6bb1d-172">In hello following example, only Monday is evaluated, and hello other days of hello week are ignored:</span></span>

    ```json
    {
        "TzId": "Eastern Standard Time",
        "1": {
            "S": "11",
            "E": "17"
        }
    }
    ```

## <a name="tag-resource-groups-or-vms"></a><span data-ttu-id="6bb1d-173">Tag grupy zasobów lub maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="6bb1d-173">Tag resource groups or VMs</span></span>
<span data-ttu-id="6bb1d-174">tooshut dół maszyn wirtualnych, należy tootag hello maszyn wirtualnych lub hello grup zasobów, w których są przechowywane.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-174">tooshut down VMs, you need tootag either hello VMs or hello resource groups in which they're located.</span></span> <span data-ttu-id="6bb1d-175">Maszyny wirtualne, które nie mają znacznika harmonogramu nie są uwzględniane.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-175">Virtual machines that don't have a Schedule tag are not evaluated.</span></span> <span data-ttu-id="6bb1d-176">W związku z tym nie jest uruchomiona lub zamknięta.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-176">Therefore, they aren't started or shut down.</span></span>

<span data-ttu-id="6bb1d-177">Istnieją dwa sposoby tootag zasobów grup lub maszyn wirtualnych w tym rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-177">There are two ways tootag resource groups or VMs with this solution.</span></span> <span data-ttu-id="6bb1d-178">Należy go bezpośrednio z portalu hello.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-178">You can do it directly from hello portal.</span></span> <span data-ttu-id="6bb1d-179">Lub może używać hello Dodaj ResourceSchedule, ResourceSchedule aktualizacji i Usuń ResourceSchedule elementów runbook.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-179">Or you can use hello Add-ResourceSchedule, Update-ResourceSchedule, and Remove-ResourceSchedule runbooks.</span></span>

### <a name="tag-through-hello-portal"></a><span data-ttu-id="6bb1d-180">Tag za pośrednictwem portalu hello</span><span class="sxs-lookup"><span data-stu-id="6bb1d-180">Tag through hello portal</span></span>
<span data-ttu-id="6bb1d-181">Wykonaj te kroki tootag maszyny wirtualnej lub grupy zasobów w portalu hello:</span><span class="sxs-lookup"><span data-stu-id="6bb1d-181">Follow these steps tootag a virtual machine or resource group in hello portal:</span></span>

1. <span data-ttu-id="6bb1d-182">Spłaszczanie hello ciągu JSON i sprawdź, czy nie ma żadnych spacji.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-182">Flatten hello JSON string and verify that there aren't any spaces.</span></span>  <span data-ttu-id="6bb1d-183">Ciągu JSON powinien wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="6bb1d-183">Your JSON string should look like this:</span></span>

    ```json
    {"TzId":"Eastern Standard Time","0":{"S":"11","E":"17"},"1":{"S":"9","E":"19"},"2": {"S":"9","E":"19"},"3":{"S":"9","E":"19"},"4":{"S":"9","E":"19"},"5":{"S":"9","E":"19"},"6":{"S":"11","E":"17"}}
    ```

2. <span data-ttu-id="6bb1d-184">Wybierz hello **Tag** ikony dla maszyny Wirtualnej lub zasób grupy tooapply tego harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-184">Select hello **Tag** icon for a VM or resource group tooapply this schedule.</span></span>

   ![Opcja tag maszyny Wirtualnej](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-tag-option.png)

3. <span data-ttu-id="6bb1d-186">Tagi są definiowane po parę klucz/wartość.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-186">Tags are defined following a key/value pair.</span></span> <span data-ttu-id="6bb1d-187">Typ **harmonogram** w hello **klucza** pola, a następnie wklej ciągu JSON hello na powitania **wartość** pola.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-187">Type **Schedule** in hello **Key** field, and then paste hello JSON string into hello **Value** field.</span></span> <span data-ttu-id="6bb1d-188">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-188">Click **Save**.</span></span> <span data-ttu-id="6bb1d-189">Twoje nowy znacznik powinien zostać wyświetlony na liście hello znaczników dla zasobu.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-189">Your new tag should now appear in hello list of tags for your resource.</span></span>

   ![Tag harmonogram maszyny Wirtualnej](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-schedule-tag.png)

### <a name="tag-from-powershell"></a><span data-ttu-id="6bb1d-191">Znacznik z programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="6bb1d-191">Tag from PowerShell</span></span>
<span data-ttu-id="6bb1d-192">Wszystkie zaimportowane elementy runbook zawierają informacje pomocy na początku hello hello skryptu, który opisuje, jak tooexecute hello elementy runbook bezpośrednio z programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-192">All imported runbooks contain help information at hello beginning of hello script that describes how tooexecute hello runbooks directly from PowerShell.</span></span> <span data-ttu-id="6bb1d-193">Witaj ScheduleResource Dodaj i ScheduleResource aktualizacji elementów runbook można wywołać z programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-193">You can call hello Add-ScheduleResource and Update-ScheduleResource runbooks from PowerShell.</span></span> <span data-ttu-id="6bb1d-194">Można to zrobić przez przekazanie wymaganych parametrów, które pozwalają toocreate lub aktualizacji tag harmonogram hello na maszyny Wirtualnej lub zasobów w grupie poza hello portalu.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-194">You do this by passing required parameters that enable you toocreate or update hello Schedule tag on a VM or resource group outside of hello portal.</span></span>

<span data-ttu-id="6bb1d-195">toocreate, dodawanie i usuwanie tagów za pomocą programu PowerShell, należy najpierw zbyt[konfigurowania środowiska PowerShell dla usługi Azure](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6bb1d-195">toocreate, add, and delete tags through PowerShell, you first need too[set up your PowerShell environment for Azure](/powershell/azure/overview).</span></span> <span data-ttu-id="6bb1d-196">Po zakończeniu konfiguracji hello może kontynuować hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-196">After you complete hello setup, you can proceed with hello following steps.</span></span>

### <a name="create-a-schedule-tag-with-powershell"></a><span data-ttu-id="6bb1d-197">Utwórz harmonogram tag przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="6bb1d-197">Create a schedule tag with PowerShell</span></span>
1. <span data-ttu-id="6bb1d-198">Otwórz sesję programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-198">Open a PowerShell session.</span></span> <span data-ttu-id="6bb1d-199">Następnie użyj powitania po tooauthenticate przykład przy użyciu konta Uruchom jako i toospecify subskrypcji:</span><span class="sxs-lookup"><span data-stu-id="6bb1d-199">Then use hello following example tooauthenticate with your Run As account and toospecify a subscription:</span></span>

    ```powershell
    $Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. <span data-ttu-id="6bb1d-200">Zdefiniuj harmonogram tablicy skrótów.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-200">Define a schedule hash table.</span></span> <span data-ttu-id="6bb1d-201">Poniżej przedstawiono przykładowy sposób wykonane:</span><span class="sxs-lookup"><span data-stu-id="6bb1d-201">Here is an example of how it should be constructed:</span></span>

    ```powershell
    $schedule= @{ "TzId"="Eastern Standard Time"; "0"= @{"S"="11";"E"="17"};"1"= @{"S"="9";"E"="19"};"2"= @{"S"="9";"E"="19"};"3"= @{"S"="9";"E"="19"};"4"= @{"S"="9";"E"="19"};"5"= @{"S"="9";"E"="19"};"6"= @{"S"="11";"E"="17"}}
    ```

3. <span data-ttu-id="6bb1d-202">Zdefiniuj parametry hello, które są wymagane przez element runbook hello.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-202">Define hello parameters that are required by hello runbook.</span></span> <span data-ttu-id="6bb1d-203">W hello poniższy przykład możemy przeznaczona dla maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="6bb1d-203">In hello following example, we are targeting a VM:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "VmName"="VM01";"Schedule"=$schedule}
    ```

    <span data-ttu-id="6bb1d-204">Jeśli w przypadku znakowanie grupę zasobów, Usuń hello *VMName* parametru z skrótu hello $params tabeli w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="6bb1d-204">If you’re tagging a resource group, remove hello *VMName* parameter from hello $params hash table as follows:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "Schedule"=$schedule}
    ```

4. <span data-ttu-id="6bb1d-205">Uruchom hello ResourceSchedule Dodaj element runbook z hello następujące parametry toocreate hello harmonogram tagu:</span><span class="sxs-lookup"><span data-stu-id="6bb1d-205">Run hello Add-ResourceSchedule runbook with hello following parameters toocreate hello Schedule tag:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Add-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

5. <span data-ttu-id="6bb1d-206">tooupdate tag maszyną wirtualną lub grupy zasobów, wykonywanie hello **ResourceSchedule aktualizacji** elementu runbook o hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="6bb1d-206">tooupdate a resource group or virtual machine tag, execute hello **Update-ResourceSchedule** runbook with hello following parameters:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Update-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

### <a name="remove-a-schedule-tag-with-powershell"></a><span data-ttu-id="6bb1d-207">Usuń znacznik harmonogramu przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="6bb1d-207">Remove a schedule tag with PowerShell</span></span>
1. <span data-ttu-id="6bb1d-208">Otwórz sesję programu PowerShell i uruchom następujące tooauthenticate przy użyciu konta Uruchom jako i tooselect hello i określ subskrypcję:</span><span class="sxs-lookup"><span data-stu-id="6bb1d-208">Open a PowerShell session and run hello following tooauthenticate with your Run As account and tooselect and specify a subscription:</span></span>

    ```powershell
    Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. <span data-ttu-id="6bb1d-209">Zdefiniuj parametry hello, które są wymagane przez element runbook hello.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-209">Define hello parameters that are required by hello runbook.</span></span> <span data-ttu-id="6bb1d-210">W hello poniższy przykład możemy przeznaczona dla maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="6bb1d-210">In hello following example, we are targeting a VM:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01";"VmName"="VM01"}
    ```

    <span data-ttu-id="6bb1d-211">Jeśli usuwasz tag z grupy zasobów, Usuń hello *VMName* parametru z skrótu hello $params tabeli w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="6bb1d-211">If you’re removing a tag from a resource group, remove hello *VMName* parameter from hello $params hash table as follows:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"}
    ```

3. <span data-ttu-id="6bb1d-212">Wykonaj hello ResourceSchedule Usuń element runbook tooremove hello harmonogram tagu:</span><span class="sxs-lookup"><span data-stu-id="6bb1d-212">Execute hello Remove-ResourceSchedule runbook tooremove hello Schedule tag:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

4. <span data-ttu-id="6bb1d-213">tooupdate tag maszyną wirtualną lub grupy zasobów, wykonywane hello ResourceSchedule Usuń element runbook za pomocą hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="6bb1d-213">tooupdate a resource group or virtual machine tag, execute hello Remove-ResourceSchedule runbook with hello following parameters:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

> [!NOTE]
> <span data-ttu-id="6bb1d-214">Zaleca się, że aktywne i można monitorować te elementy runbook (hello stany maszyny wirtualnej) zamknąć tooverify, które są maszyny wirtualne i odpowiednio uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-214">We recommend that you proactively monitor these runbooks (and hello virtual machine states) tooverify that your virtual machines are being shut down and started accordingly.</span></span>
>

<span data-ttu-id="6bb1d-215">Szczegóły hello tooview hello ResourceSchedule testu elementu runbook zadania w hello portalu Azure, wybierz hello **zadania** kafelka hello elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-215">tooview hello details of hello Test-ResourceSchedule runbook job in hello Azure portal, select hello **Jobs** tile of hello runbook.</span></span> <span data-ttu-id="6bb1d-216">Parametry wejściowe Wyświetla podsumowanie hello Hello zadania i dane wyjściowe hello strumienia, oprócz toogeneral informacje o zadaniu hello oraz wszystkie wyjątki jeśli takie były.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-216">hello job summary displays hello input parameters and hello output stream, in addition toogeneral information about hello job and any exceptions if they occurred.</span></span>

<span data-ttu-id="6bb1d-217">Witaj **Podsumowanie zadania** obejmuje wiadomości powitania strumienie danych wyjściowych, ostrzeżeń i błędów.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-217">hello **Job Summary** includes messages from hello output, warning, and error streams.</span></span> <span data-ttu-id="6bb1d-218">Wybierz hello **dane wyjściowe** kafelka tooview szczegółowe wyniki z hello wykonanie elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="6bb1d-218">Select hello **Output** tile tooview detailed results from hello runbook execution.</span></span>

![Dane wyjściowe ResourceSchedule testu](./media/automation-scenario-start-stop-vm-wjson-tags/automation-job-output.png)

## <a name="next-steps"></a><span data-ttu-id="6bb1d-220">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6bb1d-220">Next steps</span></span>
* <span data-ttu-id="6bb1d-221">tooget pracy z elementami runbook przepływu pracy programu PowerShell, zobacz [Mój pierwszy element runbook przepływu pracy programu PowerShell](automation-first-runbook-textual.md).</span><span class="sxs-lookup"><span data-stu-id="6bb1d-221">tooget started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md).</span></span>
* <span data-ttu-id="6bb1d-222">toolearn więcej informacji na temat typów elementów runbook i ich zalety i ograniczenia, zobacz [typy elementu runbook usługi Automatyzacja Azure](automation-runbook-types.md).</span><span class="sxs-lookup"><span data-stu-id="6bb1d-222">toolearn more about runbook types, and their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md).</span></span>
* <span data-ttu-id="6bb1d-223">Aby uzyskać więcej informacji o funkcji obsługi skryptów programu PowerShell, zobacz [Obsługa skryptów PowerShell natywnego automatyzacji Azure](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/).</span><span class="sxs-lookup"><span data-stu-id="6bb1d-223">For more information about PowerShell script support features, see [Native PowerShell script support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/).</span></span>
* <span data-ttu-id="6bb1d-224">toolearn więcej informacji na temat rejestrowania elementu runbook i wychodzących, zobacz [Runbook dane wyjściowe i komunikaty w automatyzacji Azure](automation-runbook-output-and-messages.md).</span><span class="sxs-lookup"><span data-stu-id="6bb1d-224">toolearn more about runbook logging and output, see [Runbook output and messages in Azure Automation](automation-runbook-output-and-messages.md).</span></span>
* <span data-ttu-id="6bb1d-225">więcej informacji na temat konta Uruchom jako platformy Azure i tooauthenticate elementy runbook za pomocą, zobacz temat toolearn [uwierzytelniania elementy runbook za pomocą konta Uruchom jako platformy Azure](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="6bb1d-225">toolearn more about an Azure Run As account and how tooauthenticate your runbooks by using it, see [Authenticate runbooks with Azure Run As account](automation-sec-configure-azure-runas-account.md).</span></span>
