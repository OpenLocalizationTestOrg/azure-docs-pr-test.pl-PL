---
title: "Używaj tagów formacie JSON można zaplanować stan maszyny Wirtualnej platformy Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule przedstawiono sposób używania ciągów JSON w tagach można zautomatyzować, harmonogram uruchamiania maszyny Wirtualnej i zamykania."
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
ms.openlocfilehash: f8d9563318c3afe299cebb7c889874392f114f84
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-scenario-using-json-formatted-tags-to-create-a-schedule-for-azure-vm-startup-and-shutdown"></a><span data-ttu-id="53385-103">Scenariusz automatyzacji Azure: przy użyciu tagów formacie JSON, aby utworzyć harmonogram uruchamiania maszyny Wirtualnej platformy Azure i zamykania</span><span class="sxs-lookup"><span data-stu-id="53385-103">Azure Automation scenario: Using JSON-formatted tags to create a schedule for Azure VM startup and shutdown</span></span>
<span data-ttu-id="53385-104">Klienci często chcą harmonogramu uruchamiania i wyłączania maszyny wirtualne lub zmniejszyć koszty subskrypcji obsługi wymagań technicznych i biznesowych.</span><span class="sxs-lookup"><span data-stu-id="53385-104">Customers often want to schedule the startup and shutdown of virtual machines to help reduce subscription costs or support business and technical requirements.</span></span>

<span data-ttu-id="53385-105">Poniższy scenariusz umożliwia konfigurowanie automatycznego uruchamiania i wyłączania maszyn wirtualnych przy użyciu tagu o nazwie harmonogram na poziomie grupy zasobów lub maszyny wirtualnej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="53385-105">The following scenario enables you to set up automated startup and shutdown of your VMs by using a tag called Schedule at a resource group level or virtual machine level in Azure.</span></span> <span data-ttu-id="53385-106">Ten harmonogram można skonfigurować od niedzieli do soboty czas uruchamiania i czasu zamykania.</span><span class="sxs-lookup"><span data-stu-id="53385-106">This schedule can be configured from Sunday to Saturday with a startup time and shutdown time.</span></span>

<span data-ttu-id="53385-107">Mamy niektóre opcje poza pole.</span><span class="sxs-lookup"><span data-stu-id="53385-107">We do have some out-of-the-box options.</span></span> <span data-ttu-id="53385-108">Należą do nich:</span><span class="sxs-lookup"><span data-stu-id="53385-108">These include:</span></span>

* <span data-ttu-id="53385-109">[Zestawy skalowania maszyny wirtualnej](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) z ustawieniami automatycznego skalowania, które umożliwiają skalowanie przychodzący lub wychodzący.</span><span class="sxs-lookup"><span data-stu-id="53385-109">[Virtual machine scale sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) with autoscale settings that enable you to scale in or out.</span></span>
* <span data-ttu-id="53385-110">[DevTest Labs](../devtest-lab/devtest-lab-overview.md) usługi, która ma wbudowaną funkcję tworzenia harmonogramu uruchamiania i wyłączania operacji.</span><span class="sxs-lookup"><span data-stu-id="53385-110">[DevTest Labs](../devtest-lab/devtest-lab-overview.md) service, which has the built-in capability of scheduling startup and shutdown operations.</span></span>

<span data-ttu-id="53385-111">Jednak te opcje obsługują tylko określonych scenariuszy i nie można zastosować do infrastruktury jako — usługa (IaaS), maszynach wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="53385-111">However, these options only support specific scenarios and cannot be applied to infrastructure-as-a-service (IaaS) VMs.</span></span>

<span data-ttu-id="53385-112">Harmonogram zostanie zastosowany do grupy zasobów, również jest stosowana do wszystkich maszyn wirtualnych w tej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="53385-112">When the Schedule tag is applied to a resource group, it's also applied to all virtual machines inside that resource group.</span></span> <span data-ttu-id="53385-113">Jeśli harmonogram jest również bezpośrednio zastosowane do maszyny Wirtualnej, harmonogram ostatniego ma pierwszeństwo przed w następującej kolejności:</span><span class="sxs-lookup"><span data-stu-id="53385-113">If a schedule is also directly applied to a VM, the last schedule takes precedence in the following order:</span></span>

1. <span data-ttu-id="53385-114">Harmonogram stosowane do grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="53385-114">Schedule applied to a resource group</span></span>
2. <span data-ttu-id="53385-115">Harmonogram zastosowane do maszyny wirtualnej w grupie zasobów i grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="53385-115">Schedule applied to a resource group and virtual machine in the resource group</span></span>
3. <span data-ttu-id="53385-116">Harmonogram zastosowane do maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="53385-116">Schedule applied to a virtual machine</span></span>

<span data-ttu-id="53385-117">W tym scenariuszu zasadniczo przyjmuje ciągu JSON w określonym formacie i dodaje go jako wartość tagu o nazwie harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="53385-117">This scenario essentially takes a JSON string with a specified format and adds it as the value for a tag called Schedule.</span></span> <span data-ttu-id="53385-118">Następnie element runbook zawiera listę wszystkich grup zasobów i maszyn wirtualnych i identyfikuje harmonogramy dla każdej maszyny Wirtualnej w scenariuszach wymienione wcześniej w oparciu.</span><span class="sxs-lookup"><span data-stu-id="53385-118">Then a runbook lists all resource groups and virtual machines and identifies the schedules for each VM based on the scenarios listed earlier.</span></span> <span data-ttu-id="53385-119">Następnie maszyn wirtualnych, które mają harmonogramy dołączony w pętli i ocenia, jakie działania należy podjąć.</span><span class="sxs-lookup"><span data-stu-id="53385-119">Next it loops through the VMs that have schedules attached and evaluates what action should be taken.</span></span> <span data-ttu-id="53385-120">Na przykład określają one, które maszyny wirtualne muszą zatrzymana, zamknięta lub ignorowane.</span><span class="sxs-lookup"><span data-stu-id="53385-120">For example, it determines which VMs need to be stopped, shut down, or ignored.</span></span>

<span data-ttu-id="53385-121">Te elementy runbook uwierzytelniania za pomocą [konta Uruchom jako platformy Azure](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="53385-121">These runbooks authenticate by using the [Azure Run As account](automation-sec-configure-azure-runas-account.md).</span></span>

## <a name="download-the-runbooks-for-the-scenario"></a><span data-ttu-id="53385-122">Pobierz elementy runbook dla tego scenariusza</span><span class="sxs-lookup"><span data-stu-id="53385-122">Download the runbooks for the scenario</span></span>
<span data-ttu-id="53385-123">Ten scenariusz obejmuje cztery elementy runbook przepływu pracy programu PowerShell, które można pobrać z [galerii TechNet](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) lub [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) repozytorium dla tego projektu.</span><span class="sxs-lookup"><span data-stu-id="53385-123">This scenario consists of four PowerShell Workflow runbooks that you can download from the [TechNet Gallery](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) or the [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) repository for this project.</span></span>

| <span data-ttu-id="53385-124">Element Runbook</span><span class="sxs-lookup"><span data-stu-id="53385-124">Runbook</span></span> | <span data-ttu-id="53385-125">Opis</span><span class="sxs-lookup"><span data-stu-id="53385-125">Description</span></span> |
| --- | --- |
| <span data-ttu-id="53385-126">ResourceSchedule testu</span><span class="sxs-lookup"><span data-stu-id="53385-126">Test-ResourceSchedule</span></span> |<span data-ttu-id="53385-127">Sprawdza harmonogram każdej maszyny wirtualnej, a następnie wykonuje zamykania lub uruchamiania w zależności od harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="53385-127">Checks each virtual machine schedule and performs shutdown or startup depending on the schedule.</span></span> |
| <span data-ttu-id="53385-128">Dodaj ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="53385-128">Add-ResourceSchedule</span></span> |<span data-ttu-id="53385-129">Dodaje tag harmonogramu do maszyny Wirtualnej lub grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="53385-129">Adds the Schedule tag to a VM or resource group.</span></span> |
| <span data-ttu-id="53385-130">ResourceSchedule aktualizacji</span><span class="sxs-lookup"><span data-stu-id="53385-130">Update-ResourceSchedule</span></span> |<span data-ttu-id="53385-131">Modyfikuje istniejące tag harmonogramu przez zamianę nowy.</span><span class="sxs-lookup"><span data-stu-id="53385-131">Modifies the existing Schedule tag by replacing it with a new one.</span></span> |
| <span data-ttu-id="53385-132">Usuń ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="53385-132">Remove-ResourceSchedule</span></span> |<span data-ttu-id="53385-133">Usuwa harmonogram tagu z maszyny Wirtualnej lub grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="53385-133">Removes the Schedule tag from a VM or resource group.</span></span> |

## <a name="install-and-configure-this-scenario"></a><span data-ttu-id="53385-134">Instalowanie i konfigurowanie tego scenariusza</span><span class="sxs-lookup"><span data-stu-id="53385-134">Install and configure this scenario</span></span>
### <a name="install-and-publish-the-runbooks"></a><span data-ttu-id="53385-135">Instalowanie i publikowanie elementów Runbook</span><span class="sxs-lookup"><span data-stu-id="53385-135">Install and publish the runbooks</span></span>
<span data-ttu-id="53385-136">Po pobraniu elementy runbook, można je zaimportować za pomocą procedury w [Tworzenie lub importowanie elementu runbook automatyzacji Azure](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation).</span><span class="sxs-lookup"><span data-stu-id="53385-136">After downloading the runbooks, you can import them by using the procedure in [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation).</span></span>  <span data-ttu-id="53385-137">Każdy element runbook należy opublikować po jego został pomyślnie zaimportowany na koncie automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="53385-137">Publish each runbook after it has been successfully imported into your Automation account.</span></span>

### <a name="add-a-schedule-to-the-test-resourceschedule-runbook"></a><span data-ttu-id="53385-138">Dodaj harmonogram do elementu runbook ResourceSchedule testu</span><span class="sxs-lookup"><span data-stu-id="53385-138">Add a schedule to the Test-ResourceSchedule runbook</span></span>
<span data-ttu-id="53385-139">Wykonaj następujące kroki, aby włączyć harmonogram ResourceSchedule testu elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="53385-139">Follow these steps to enable the schedule for the Test-ResourceSchedule runbook.</span></span> <span data-ttu-id="53385-140">Jest to element runbook, który sprawdza maszyn wirtualnych powinny być uruchomiona, zamknij lub pozostawione tak jak jest.</span><span class="sxs-lookup"><span data-stu-id="53385-140">This is the runbook that verifies which virtual machines should be started, shut down, or left as is.</span></span>

1. <span data-ttu-id="53385-141">W portalu Azure, otwórz Twoje konto usługi Automatyzacja, a następnie kliknij **elementów Runbook** kafelka.</span><span class="sxs-lookup"><span data-stu-id="53385-141">From the Azure portal, open your Automation account, and then click the **Runbooks** tile.</span></span>
2. <span data-ttu-id="53385-142">Na **ResourceSchedule testu** bloku, kliknij przycisk **harmonogramy** kafelka.</span><span class="sxs-lookup"><span data-stu-id="53385-142">On the **Test-ResourceSchedule** blade, click the **Schedules** tile.</span></span>
3. <span data-ttu-id="53385-143">Na **harmonogramy** bloku, kliknij przycisk **Dodaj harmonogram**.</span><span class="sxs-lookup"><span data-stu-id="53385-143">On the **Schedules** blade, click **Add a schedule**.</span></span>
4. <span data-ttu-id="53385-144">Na **harmonogramy** bloku, wybierz opcję **Połącz harmonogram z elementem runbook**.</span><span class="sxs-lookup"><span data-stu-id="53385-144">On the **Schedules** blade, select **Link a schedule to your runbook**.</span></span> <span data-ttu-id="53385-145">Następnie wybierz **Utwórz nowy harmonogram**.</span><span class="sxs-lookup"><span data-stu-id="53385-145">Then select **Create a new schedule**.</span></span>
5. <span data-ttu-id="53385-146">Na **nowy harmonogram** bloku, wpisz nazwę tego harmonogramu, na przykład: *HourlyExecution*.</span><span class="sxs-lookup"><span data-stu-id="53385-146">On the **New schedule** blade, type in the name of this schedule, for example: *HourlyExecution*.</span></span>
6. <span data-ttu-id="53385-147">Dla harmonogramu **Start**, ustawić czas rozpoczęcia przyrost godzinę.</span><span class="sxs-lookup"><span data-stu-id="53385-147">For the schedule **Start**, set the start time to an hour increment.</span></span>
7. <span data-ttu-id="53385-148">Wybierz **cyklu**, a następnie **powtarzanie co interwał**, wybierz pozycję **1 godzina**.</span><span class="sxs-lookup"><span data-stu-id="53385-148">Select **Recurrence**, and then for **Recur every interval**, select **1 hour**.</span></span>
8. <span data-ttu-id="53385-149">Sprawdź, czy **ustawienia okresu ważności** ustawiono **nr**, a następnie kliknij przycisk **Utwórz** można zapisać nowego harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="53385-149">Verify that **Set expiration** is set to **No**, and then click **Create** to save your new schedule.</span></span>
9. <span data-ttu-id="53385-150">Na **Runbook harmonogram** bloku opcji wybierz **parametry i ustawienia uruchamiania**.</span><span class="sxs-lookup"><span data-stu-id="53385-150">On the **Schedule Runbook** options blade, select **Parameters and run settings**.</span></span> <span data-ttu-id="53385-151">W ResourceSchedule testu **parametry** bloku, wprowadź nazwę subskrypcji w **Nazwa subskrypcji** pola.</span><span class="sxs-lookup"><span data-stu-id="53385-151">In the Test-ResourceSchedule **Parameters** blade, enter the name of your subscription in the **SubscriptionName** field.</span></span>  <span data-ttu-id="53385-152">Jest to tylko parametr, który jest wymagany dla elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="53385-152">This is the only parameter that's required for the runbook.</span></span>  <span data-ttu-id="53385-153">Po zakończeniu kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="53385-153">When you're finished, click **OK**.</span></span>

<span data-ttu-id="53385-154">Po jego ukończeniu harmonogram powinna wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="53385-154">The runbook schedule should look like the following when it's completed:</span></span>

![Skonfigurowany ResourceSchedule testu elementu runbook](./media/automation-scenario-start-stop-vm-wjson-tags/automation-schedule-config.png)<br>

## <a name="format-the-json-string"></a><span data-ttu-id="53385-156">Format ciągu JSON</span><span class="sxs-lookup"><span data-stu-id="53385-156">Format the JSON string</span></span>
<span data-ttu-id="53385-157">To rozwiązanie zasadniczo ma JSON ciąg w określonym formacie i dodaje go jako wartość tagu o nazwie harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="53385-157">This solution basically takes a JSON string with a specified format and adds it as the value for a tag called Schedule.</span></span> <span data-ttu-id="53385-158">Następnie element runbook zawiera listę wszystkich grup zasobów i maszyn wirtualnych i identyfikuje harmonogramy dla każdej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="53385-158">Then a runbook lists all resource groups and virtual machines and identifies the schedules for each virtual machine.</span></span>

<span data-ttu-id="53385-159">Element runbook pętli maszyn wirtualnych, które mają harmonogramy dołączona i sprawdza, jakie działania należy podjąć.</span><span class="sxs-lookup"><span data-stu-id="53385-159">The runbook loops over the virtual machines that have schedules attached and checks what actions should be taken.</span></span> <span data-ttu-id="53385-160">Poniżej przedstawiono przykładowy sposób formatowania rozwiązania:</span><span class="sxs-lookup"><span data-stu-id="53385-160">The following is an example of how the solutions should be formatted:</span></span>

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

<span data-ttu-id="53385-161">Oto niektóre szczegółowe informacje na temat tej struktury:</span><span class="sxs-lookup"><span data-stu-id="53385-161">Here is some detailed information about this structure:</span></span>

1. <span data-ttu-id="53385-162">Format tej struktury JSON jest zoptymalizowany do obejścia ograniczenia 256 znaków wartości jeden tag na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="53385-162">The format of this JSON structure is optimized to work around the 256-character limitation of a single tag value in Azure.</span></span>
2. <span data-ttu-id="53385-163">*TzId* reprezentuje strefę czasową dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="53385-163">*TzId* represents the time zone of the virtual machine.</span></span> <span data-ttu-id="53385-164">Ten identyfikator można uzyskać za pomocą klasy .NET informacje o strefie czasowej w sesji programu PowerShell —**[System.TimeZoneInfo]:: GetSystemTimeZones()**.</span><span class="sxs-lookup"><span data-stu-id="53385-164">This ID can be obtained by using the TimeZoneInfo .NET class in a PowerShell session--**[System.TimeZoneInfo]::GetSystemTimeZones()**.</span></span>

   ![GetSystemTimeZones w programie PowerShell](./media/automation-scenario-start-stop-vm-wjson-tags/automation-get-timzone-powershell.png)

   * <span data-ttu-id="53385-166">Dni robocze są reprezentowane z wartością liczbową 0 do 6.</span><span class="sxs-lookup"><span data-stu-id="53385-166">Weekdays are represented with a numeric value of zero to six.</span></span> <span data-ttu-id="53385-167">Wartość zero jest równa niedzielę.</span><span class="sxs-lookup"><span data-stu-id="53385-167">The value zero equals Sunday.</span></span>
   * <span data-ttu-id="53385-168">Godzina rozpoczęcia jest reprezentowana z **S** atrybutu i jego wartość jest w formacie 24-godzinnym.</span><span class="sxs-lookup"><span data-stu-id="53385-168">The start time is represented with the **S** attribute, and its value is in a 24-hour format.</span></span>
   * <span data-ttu-id="53385-169">Czas zakończenia lub zamknięcie odpowiada z **E** atrybutu i jego wartość jest w formacie 24-godzinnym.</span><span class="sxs-lookup"><span data-stu-id="53385-169">The end or shutdown time is represented with the **E** attribute, and its value is in a 24-hour format.</span></span>

     <span data-ttu-id="53385-170">Jeśli **S** i **E** atrybuty każdego mają wartość zero (0), maszyna wirtualna znajdzie się w jej obecnym stanie w chwili oceny.</span><span class="sxs-lookup"><span data-stu-id="53385-170">If the **S** and **E** attributes each have a value of zero (0), the virtual machine will be left in its present state at the time of evaluation.</span></span>
3. <span data-ttu-id="53385-171">Jeśli chcesz pominąć oceny dla określonego dnia, tygodnia, nie dodawaj sekcji za ten dzień tygodnia.</span><span class="sxs-lookup"><span data-stu-id="53385-171">If you want to skip evaluation for a specific day of the week, don’t add a section for that day of the week.</span></span> <span data-ttu-id="53385-172">W poniższym przykładzie jest oceniane tylko poniedziałek i dni tygodnia, są ignorowane:</span><span class="sxs-lookup"><span data-stu-id="53385-172">In the following example, only Monday is evaluated, and the other days of the week are ignored:</span></span>

    ```json
    {
        "TzId": "Eastern Standard Time",
        "1": {
            "S": "11",
            "E": "17"
        }
    }
    ```

## <a name="tag-resource-groups-or-vms"></a><span data-ttu-id="53385-173">Tag grupy zasobów lub maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="53385-173">Tag resource groups or VMs</span></span>
<span data-ttu-id="53385-174">Aby zamknąć maszyn wirtualnych, należy tagu maszyn wirtualnych lub grup zasobów, w których są przechowywane.</span><span class="sxs-lookup"><span data-stu-id="53385-174">To shut down VMs, you need to tag either the VMs or the resource groups in which they're located.</span></span> <span data-ttu-id="53385-175">Maszyny wirtualne, które nie mają znacznika harmonogramu nie są uwzględniane.</span><span class="sxs-lookup"><span data-stu-id="53385-175">Virtual machines that don't have a Schedule tag are not evaluated.</span></span> <span data-ttu-id="53385-176">W związku z tym nie jest uruchomiona lub zamknięta.</span><span class="sxs-lookup"><span data-stu-id="53385-176">Therefore, they aren't started or shut down.</span></span>

<span data-ttu-id="53385-177">Istnieją dwa sposoby tag grupy zasobów lub maszyn wirtualnych w tym rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="53385-177">There are two ways to tag resource groups or VMs with this solution.</span></span> <span data-ttu-id="53385-178">Należy go bezpośrednio z portalu.</span><span class="sxs-lookup"><span data-stu-id="53385-178">You can do it directly from the portal.</span></span> <span data-ttu-id="53385-179">Lub może używać ResourceSchedule Dodaj ResourceSchedule aktualizacji i Usuń ResourceSchedule elementów runbook.</span><span class="sxs-lookup"><span data-stu-id="53385-179">Or you can use the Add-ResourceSchedule, Update-ResourceSchedule, and Remove-ResourceSchedule runbooks.</span></span>

### <a name="tag-through-the-portal"></a><span data-ttu-id="53385-180">Tag za pośrednictwem portalu</span><span class="sxs-lookup"><span data-stu-id="53385-180">Tag through the portal</span></span>
<span data-ttu-id="53385-181">Wykonaj następujące kroki, aby oznaczyć maszyny wirtualnej lub grupy zasobów w portalu:</span><span class="sxs-lookup"><span data-stu-id="53385-181">Follow these steps to tag a virtual machine or resource group in the portal:</span></span>

1. <span data-ttu-id="53385-182">Spłaszczanie ciągu JSON i sprawdź, czy nie ma żadnych spacji.</span><span class="sxs-lookup"><span data-stu-id="53385-182">Flatten the JSON string and verify that there aren't any spaces.</span></span>  <span data-ttu-id="53385-183">Ciągu JSON powinien wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="53385-183">Your JSON string should look like this:</span></span>

    ```json
    {"TzId":"Eastern Standard Time","0":{"S":"11","E":"17"},"1":{"S":"9","E":"19"},"2": {"S":"9","E":"19"},"3":{"S":"9","E":"19"},"4":{"S":"9","E":"19"},"5":{"S":"9","E":"19"},"6":{"S":"11","E":"17"}}
    ```

2. <span data-ttu-id="53385-184">Wybierz **Tag** ikona maszyny Wirtualnej lub zasób grupy do zastosowania tego harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="53385-184">Select the **Tag** icon for a VM or resource group to apply this schedule.</span></span>

   ![Opcja tag maszyny Wirtualnej](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-tag-option.png)

3. <span data-ttu-id="53385-186">Tagi są definiowane po parę klucz/wartość.</span><span class="sxs-lookup"><span data-stu-id="53385-186">Tags are defined following a key/value pair.</span></span> <span data-ttu-id="53385-187">Typ **harmonogram** w **klucza** pola, a następnie wklej do ciągu JSON **wartość** pola.</span><span class="sxs-lookup"><span data-stu-id="53385-187">Type **Schedule** in the **Key** field, and then paste the JSON string into the **Value** field.</span></span> <span data-ttu-id="53385-188">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="53385-188">Click **Save**.</span></span> <span data-ttu-id="53385-189">Twoje nowy znacznik powinien zostać wyświetlony na liście tagów dla zasobu.</span><span class="sxs-lookup"><span data-stu-id="53385-189">Your new tag should now appear in the list of tags for your resource.</span></span>

   ![Tag harmonogram maszyny Wirtualnej](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-schedule-tag.png)

### <a name="tag-from-powershell"></a><span data-ttu-id="53385-191">Znacznik z programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="53385-191">Tag from PowerShell</span></span>
<span data-ttu-id="53385-192">Wszystkie zaimportowane elementy runbook zawierają informacje pomocy na początku skryptu, który opisuje sposób wykonywania elementy runbook bezpośrednio z programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="53385-192">All imported runbooks contain help information at the beginning of the script that describes how to execute the runbooks directly from PowerShell.</span></span> <span data-ttu-id="53385-193">Dodaj ScheduleResource i ScheduleResource aktualizacji elementów runbook można wywołać z programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="53385-193">You can call the Add-ScheduleResource and Update-ScheduleResource runbooks from PowerShell.</span></span> <span data-ttu-id="53385-194">W tym przez przekazanie wymaganych parametrów, które umożliwiają tworzenie lub aktualizowanie tag harmonogramu dla maszyny Wirtualnej lub zasób grupy poza portalu.</span><span class="sxs-lookup"><span data-stu-id="53385-194">You do this by passing required parameters that enable you to create or update the Schedule tag on a VM or resource group outside of the portal.</span></span>

<span data-ttu-id="53385-195">Aby utworzyć, dodawanie i usuwanie tagów za pomocą programu PowerShell, należy najpierw [konfigurowania środowiska PowerShell dla usługi Azure](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="53385-195">To create, add, and delete tags through PowerShell, you first need to [set up your PowerShell environment for Azure](/powershell/azure/overview).</span></span> <span data-ttu-id="53385-196">Po zakończeniu instalacji można kontynuować następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="53385-196">After you complete the setup, you can proceed with the following steps.</span></span>

### <a name="create-a-schedule-tag-with-powershell"></a><span data-ttu-id="53385-197">Utwórz harmonogram tag przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="53385-197">Create a schedule tag with PowerShell</span></span>
1. <span data-ttu-id="53385-198">Otwórz sesję programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="53385-198">Open a PowerShell session.</span></span> <span data-ttu-id="53385-199">Następnie skorzystaj z następującego przykładu, do uwierzytelniania przy użyciu konta Uruchom jako, a aby określić subskrypcję:</span><span class="sxs-lookup"><span data-stu-id="53385-199">Then use the following example to authenticate with your Run As account and to specify a subscription:</span></span>

    ```powershell
    $Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. <span data-ttu-id="53385-200">Zdefiniuj harmonogram tablicy skrótów.</span><span class="sxs-lookup"><span data-stu-id="53385-200">Define a schedule hash table.</span></span> <span data-ttu-id="53385-201">Poniżej przedstawiono przykładowy sposób wykonane:</span><span class="sxs-lookup"><span data-stu-id="53385-201">Here is an example of how it should be constructed:</span></span>

    ```powershell
    $schedule= @{ "TzId"="Eastern Standard Time"; "0"= @{"S"="11";"E"="17"};"1"= @{"S"="9";"E"="19"};"2"= @{"S"="9";"E"="19"};"3"= @{"S"="9";"E"="19"};"4"= @{"S"="9";"E"="19"};"5"= @{"S"="9";"E"="19"};"6"= @{"S"="11";"E"="17"}}
    ```

3. <span data-ttu-id="53385-202">Zdefiniuj parametry, które są wymagane przez element runbook.</span><span class="sxs-lookup"><span data-stu-id="53385-202">Define the parameters that are required by the runbook.</span></span> <span data-ttu-id="53385-203">W poniższym przykładzie mamy przeznaczona dla maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="53385-203">In the following example, we are targeting a VM:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "VmName"="VM01";"Schedule"=$schedule}
    ```

    <span data-ttu-id="53385-204">Jeśli w przypadku znakowanie grupę zasobów, Usuń *VMName* parametru z skrótu $params tabeli w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="53385-204">If you’re tagging a resource group, remove the *VMName* parameter from the $params hash table as follows:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "Schedule"=$schedule}
    ```

4. <span data-ttu-id="53385-205">Uruchom element runbook ResourceSchedule Dodaj z następującymi parametrami, aby utworzyć tag harmonogramu:</span><span class="sxs-lookup"><span data-stu-id="53385-205">Run the Add-ResourceSchedule runbook with the following parameters to create the Schedule tag:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Add-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

5. <span data-ttu-id="53385-206">Aby zaktualizować grupy zasobów lub tagu maszyny wirtualnej, należy wykonać **ResourceSchedule aktualizacji** elementu runbook z następującymi parametrami:</span><span class="sxs-lookup"><span data-stu-id="53385-206">To update a resource group or virtual machine tag, execute the **Update-ResourceSchedule** runbook with the following parameters:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Update-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

### <a name="remove-a-schedule-tag-with-powershell"></a><span data-ttu-id="53385-207">Usuń znacznik harmonogramu przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="53385-207">Remove a schedule tag with PowerShell</span></span>
1. <span data-ttu-id="53385-208">Otwórz sesję programu PowerShell i uruchom następujące polecenie do uwierzytelniania przy użyciu konta Uruchom jako i aby wybrać i określić subskrypcji:</span><span class="sxs-lookup"><span data-stu-id="53385-208">Open a PowerShell session and run the following to authenticate with your Run As account and to select and specify a subscription:</span></span>

    ```powershell
    Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. <span data-ttu-id="53385-209">Zdefiniuj parametry, które są wymagane przez element runbook.</span><span class="sxs-lookup"><span data-stu-id="53385-209">Define the parameters that are required by the runbook.</span></span> <span data-ttu-id="53385-210">W poniższym przykładzie mamy przeznaczona dla maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="53385-210">In the following example, we are targeting a VM:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01";"VmName"="VM01"}
    ```

    <span data-ttu-id="53385-211">Jeśli usuwasz tag z grupy zasobów, Usuń *VMName* parametru z skrótu $params tabeli w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="53385-211">If you’re removing a tag from a resource group, remove the *VMName* parameter from the $params hash table as follows:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"}
    ```

3. <span data-ttu-id="53385-212">Wykonaj runbook ResourceSchedule Usuń, aby usunąć tag harmonogramu:</span><span class="sxs-lookup"><span data-stu-id="53385-212">Execute the Remove-ResourceSchedule runbook to remove the Schedule tag:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

4. <span data-ttu-id="53385-213">Aby zaktualizować grupy zasobów lub tagu maszyny wirtualnej, wykonaj ResourceSchedule Usuń element runbook z następującymi parametrami:</span><span class="sxs-lookup"><span data-stu-id="53385-213">To update a resource group or virtual machine tag, execute the Remove-ResourceSchedule runbook with the following parameters:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

> [!NOTE]
> <span data-ttu-id="53385-214">Zaleca się, że aktywnego monitorowania tych elementów runbook (i Stany maszyny wirtualnej), aby sprawdzić, czy maszyny wirtualne są zamknięte w dół i odpowiednio uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="53385-214">We recommend that you proactively monitor these runbooks (and the virtual machine states) to verify that your virtual machines are being shut down and started accordingly.</span></span>
>

<span data-ttu-id="53385-215">Aby wyświetlić szczegóły zadania ResourceSchedule testu elementu runbook w portalu Azure, wybierz **zadania** kafelka elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="53385-215">To view the details of the Test-ResourceSchedule runbook job in the Azure portal, select the **Jobs** tile of the runbook.</span></span> <span data-ttu-id="53385-216">W obszarze podsumowania zadania są wyświetlane parametry wejściowe i dane ze strumienia wyjściowego oraz ogólne informacje o zadaniu wraz z wygenerowanymi wyjątkami.</span><span class="sxs-lookup"><span data-stu-id="53385-216">The job summary displays the input parameters and the output stream, in addition to general information about the job and any exceptions if they occurred.</span></span>

<span data-ttu-id="53385-217">W obszarze **Podsumowanie zadania** są widoczne ostrzeżenia i komunikaty o błędach oraz dane ze strumienia wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="53385-217">The **Job Summary** includes messages from the output, warning, and error streams.</span></span> <span data-ttu-id="53385-218">Wybierz kafelek **Dane wyjściowe**, aby wyświetlić szczegółowe wyniki wykonania elementu Runbook.</span><span class="sxs-lookup"><span data-stu-id="53385-218">Select the **Output** tile to view detailed results from the runbook execution.</span></span>

![Dane wyjściowe ResourceSchedule testu](./media/automation-scenario-start-stop-vm-wjson-tags/automation-job-output.png)

## <a name="next-steps"></a><span data-ttu-id="53385-220">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="53385-220">Next steps</span></span>
* <span data-ttu-id="53385-221">Aby rozpocząć pracę z elementami runbook przepływu pracy programu PowerShell, zobacz [Mój pierwszy element runbook przepływu pracy programu PowerShell](automation-first-runbook-textual.md).</span><span class="sxs-lookup"><span data-stu-id="53385-221">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md).</span></span>
* <span data-ttu-id="53385-222">Aby dowiedzieć się więcej na temat typów elementów runbook i ich zalety i ograniczenia, zobacz [typy elementu runbook usługi Automatyzacja Azure](automation-runbook-types.md).</span><span class="sxs-lookup"><span data-stu-id="53385-222">To learn more about runbook types, and their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md).</span></span>
* <span data-ttu-id="53385-223">Aby uzyskać więcej informacji o funkcji obsługi skryptów programu PowerShell, zobacz [Obsługa skryptów PowerShell natywnego automatyzacji Azure](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/).</span><span class="sxs-lookup"><span data-stu-id="53385-223">For more information about PowerShell script support features, see [Native PowerShell script support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/).</span></span>
* <span data-ttu-id="53385-224">Aby dowiedzieć się więcej na temat rejestrowania elementu runbook i dane wyjściowe, zobacz [Runbook dane wyjściowe i komunikaty w automatyzacji Azure](automation-runbook-output-and-messages.md).</span><span class="sxs-lookup"><span data-stu-id="53385-224">To learn more about runbook logging and output, see [Runbook output and messages in Azure Automation](automation-runbook-output-and-messages.md).</span></span>
* <span data-ttu-id="53385-225">Aby uzyskać więcej informacji na temat konta Uruchom jako platformy Azure i sposobu uwierzytelniania przy użyciu jego elementy runbook, zobacz [uwierzytelniania elementy runbook za pomocą konta Uruchom jako platformy Azure](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="53385-225">To learn more about an Azure Run As account and how to authenticate your runbooks by using it, see [Authenticate runbooks with Azure Run As account](automation-sec-configure-azure-runas-account.md).</span></span>
