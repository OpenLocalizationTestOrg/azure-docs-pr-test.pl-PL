---
title: "Zaawansowane skalowania automatycznego przy użyciu usługi Azure Virtual Machines | Dokumentacja firmy Microsoft"
description: "Używa usługi Resource Manager i zestawy skalowania maszyny Wirtualnej z wielu zasad i profilów, które wysyłania wiadomości e-mail i Wywołaj adresy URL elementu webhook z akcji skalowania."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 7e3576e2-4a2b-4736-b5ae-98c4689cdd2b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2016
ms.author: ancav
ms.openlocfilehash: 80955535c8d863cd3d8d1b77e2ab8bc016b6d9f3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="advanced-autoscale-configuration-using-resource-manager-templates-for-vm-scale-sets"></a><span data-ttu-id="4deea-103">Zestawy skalowania maszyny Wirtualnej za pomocą szablonów usługi Resource Manager konfiguracji zaawansowanej skalowania automatycznego</span><span class="sxs-lookup"><span data-stu-id="4deea-103">Advanced autoscale configuration using Resource Manager templates for VM Scale Sets</span></span>
<span data-ttu-id="4deea-104">Można w skali i skalowalnego w poziomie w zestawy skalowania maszyny wirtualnej w oparciu metryki progów wydajności, zgodnie z cyklicznym harmonogramem lub w określonym dniu.</span><span class="sxs-lookup"><span data-stu-id="4deea-104">You can scale-in and scale-out in Virtual Machine Scale Sets based on performance metric thresholds, by a recurring schedule, or by a particular date.</span></span> <span data-ttu-id="4deea-105">Można również skonfigurować powiadomienia e-mail i elementu webhook dla akcji skalowania.</span><span class="sxs-lookup"><span data-stu-id="4deea-105">You can also configure email and webhook notifications for scale actions.</span></span> <span data-ttu-id="4deea-106">W tym przewodniku przedstawiono przykład konfigurowania tych obiektów przy użyciu szablonu usługi Resource Manager dla zestawu skalowania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4deea-106">This walkthrough shows an example of configuring all these objects using a Resource Manager template on a VM Scale Set.</span></span>

> [!NOTE]
> <span data-ttu-id="4deea-107">Gdy w tym przewodniku opisano kroki dla zestawy skalowania maszyny Wirtualnej, te same informacje dotyczą Skalowanie automatyczne [usługi w chmurze](https://azure.microsoft.com/services/cloud-services/), i [usługi aplikacji — aplikacje sieci Web](https://azure.microsoft.com/services/app-service/web/).</span><span class="sxs-lookup"><span data-stu-id="4deea-107">While this walkthrough explains the steps for VM Scale Sets, the same information applies to autoscaling [Cloud Services](https://azure.microsoft.com/services/cloud-services/), and [App Service - Web Apps](https://azure.microsoft.com/services/app-service/web/).</span></span>
> <span data-ttu-id="4deea-108">Dla prostego skali we/wy ustawienie dla zestawu skalowania maszyny Wirtualnej w oparciu o metryki wydajności prosty przykład procesora CPU, zapoznaj się [Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) i [Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) dokumentów</span><span class="sxs-lookup"><span data-stu-id="4deea-108">For a simple scale in/out setting on a VM Scale Set based on a simple performance metric such as CPU, refer to the [Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) and [Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) documents</span></span>
>
>

## <a name="walkthrough"></a><span data-ttu-id="4deea-109">Przewodnik</span><span class="sxs-lookup"><span data-stu-id="4deea-109">Walkthrough</span></span>
<span data-ttu-id="4deea-110">W tym przewodniku używamy [Eksploratora zasobów Azure](https://resources.azure.com/) do konfigurowania i aktualizowania w ustawieniu skalowania automatycznego dla zestawu skalowania.</span><span class="sxs-lookup"><span data-stu-id="4deea-110">In this walkthrough, we use [Azure Resource Explorer](https://resources.azure.com/) to configure and update the autoscale setting for a scale set.</span></span> <span data-ttu-id="4deea-111">Eksploratora zasobów Azure to prosty sposób zarządzania zasobami Azure za pomocą szablonów Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4deea-111">Azure Resource Explorer is an easy way to manage Azure resources via Resource Manager templates.</span></span> <span data-ttu-id="4deea-112">Jeśli jesteś nowym użytkownikiem narzędzia Eksploratora zasobów Azure, przeczytaj [to wprowadzenie](https://azure.microsoft.com/blog/azure-resource-explorer-a-new-tool-to-discover-the-azure-api/).</span><span class="sxs-lookup"><span data-stu-id="4deea-112">If you are new to Azure Resource Explorer tool, read [this introduction](https://azure.microsoft.com/blog/azure-resource-explorer-a-new-tool-to-discover-the-azure-api/).</span></span>

1. <span data-ttu-id="4deea-113">Wdrożenie nowej skali ustawić przy użyciu ustawienia skalowania automatycznego podstawowe.</span><span class="sxs-lookup"><span data-stu-id="4deea-113">Deploy a new scale set with a basic autoscale setting.</span></span> <span data-ttu-id="4deea-114">W tym artykule wykorzystano z galerii Szybki Start Azure, z systemu Windows zestawu przy użyciu szablonu podstawowego skalowania automatycznego skalowania.</span><span class="sxs-lookup"><span data-stu-id="4deea-114">This article uses the one from the Azure QuickStart Gallery, which has a Windows scale set with a basic autoscale template.</span></span> <span data-ttu-id="4deea-115">Zestawy skalowania Linux działają tak samo.</span><span class="sxs-lookup"><span data-stu-id="4deea-115">Linux scale sets work the same way.</span></span>
2. <span data-ttu-id="4deea-116">Po utworzeniu zestawu skalowania, przejdź do zasobu zestaw skali z Eksploratora zasobów Azure.</span><span class="sxs-lookup"><span data-stu-id="4deea-116">After the scale set is created, navigate to the scale set resource from Azure Resource Explorer.</span></span> <span data-ttu-id="4deea-117">Można znaleźć w następujących tematach w węźle elemencie Microsoft.Insights.</span><span class="sxs-lookup"><span data-stu-id="4deea-117">You see the following under Microsoft.Insights node.</span></span>

    ![Eksplorator systemu Azure](./media/insights-advanced-autoscale-vmss/azure_explorer_navigate.png)

    <span data-ttu-id="4deea-119">Wykonanie szablon został utworzony domyślnego ustawienia skalowania automatycznego o nazwie **"autoscalewad"**.</span><span class="sxs-lookup"><span data-stu-id="4deea-119">The template execution has created a default autoscale setting with the name **'autoscalewad'**.</span></span> <span data-ttu-id="4deea-120">Po prawej stronie można wyświetlić pełnej definicji tego ustawienia skalowania automatycznego.</span><span class="sxs-lookup"><span data-stu-id="4deea-120">On the right-hand side, you can view the full definition of this autoscale setting.</span></span> <span data-ttu-id="4deea-121">W takim przypadku domyślne ustawienie skalowania automatycznego zawiera reguły Procesora % na podstawie skalowalnego w poziomie i w skali.</span><span class="sxs-lookup"><span data-stu-id="4deea-121">In this case, the default autoscale setting comes with a CPU% based scale-out and scale-in rule.</span></span>  

3. <span data-ttu-id="4deea-122">Teraz można dodać więcej profilów i reguły na podstawie harmonogramu lub określone wymagania.</span><span class="sxs-lookup"><span data-stu-id="4deea-122">You can now add more profiles and rules based on the schedule or specific requirements.</span></span> <span data-ttu-id="4deea-123">Utworzymy ustawieniu skalowania automatycznego przy użyciu trzech profilów.</span><span class="sxs-lookup"><span data-stu-id="4deea-123">We create an autoscale setting with three profiles.</span></span> <span data-ttu-id="4deea-124">Aby zrozumieć, profile i zasady automatycznego skalowania, przejrzyj [najlepsze rozwiązania w zakresie skalowania automatycznego](insights-autoscale-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="4deea-124">To understand profiles and rules in autoscale, review [Autoscale Best Practices](insights-autoscale-best-practices.md).</span></span>  

    | <span data-ttu-id="4deea-125">Profile & reguły</span><span class="sxs-lookup"><span data-stu-id="4deea-125">Profiles & Rules</span></span> | <span data-ttu-id="4deea-126">Opis</span><span class="sxs-lookup"><span data-stu-id="4deea-126">Description</span></span> |
    |--- | --- |
    | <span data-ttu-id="4deea-127">**Profil**</span><span class="sxs-lookup"><span data-stu-id="4deea-127">**Profile**</span></span> |<span data-ttu-id="4deea-128">**Na podstawie wydajności/metryki**</span><span class="sxs-lookup"><span data-stu-id="4deea-128">**Performance/metric based**</span></span> |
    | <span data-ttu-id="4deea-129">Reguła</span><span class="sxs-lookup"><span data-stu-id="4deea-129">Rule</span></span> |<span data-ttu-id="4deea-130">Liczba wiadomości w kolejce magistrali usługi > x</span><span class="sxs-lookup"><span data-stu-id="4deea-130">Service Bus Queue Message Count > x</span></span> |
    | <span data-ttu-id="4deea-131">Reguła</span><span class="sxs-lookup"><span data-stu-id="4deea-131">Rule</span></span> |<span data-ttu-id="4deea-132">Liczba wiadomości w kolejce magistrali usługi < y</span><span class="sxs-lookup"><span data-stu-id="4deea-132">Service Bus Queue Message Count < y</span></span> |
    | <span data-ttu-id="4deea-133">Reguła</span><span class="sxs-lookup"><span data-stu-id="4deea-133">Rule</span></span> |<span data-ttu-id="4deea-134">Procent użycia procesora CPU > n</span><span class="sxs-lookup"><span data-stu-id="4deea-134">CPU% > n</span></span> |
    | <span data-ttu-id="4deea-135">Reguła</span><span class="sxs-lookup"><span data-stu-id="4deea-135">Rule</span></span> |<span data-ttu-id="4deea-136">Procent użycia procesora CPU < p</span><span class="sxs-lookup"><span data-stu-id="4deea-136">CPU% < p</span></span> |
    | <span data-ttu-id="4deea-137">**Profil**</span><span class="sxs-lookup"><span data-stu-id="4deea-137">**Profile**</span></span> |<span data-ttu-id="4deea-138">**Dzień tygodnia godziny rano (Brak reguł)**</span><span class="sxs-lookup"><span data-stu-id="4deea-138">**Weekday morning hours (no rules)**</span></span> |
    | <span data-ttu-id="4deea-139">**Profil**</span><span class="sxs-lookup"><span data-stu-id="4deea-139">**Profile**</span></span> |<span data-ttu-id="4deea-140">**Dzień uruchamiania produktu (Brak reguł)**</span><span class="sxs-lookup"><span data-stu-id="4deea-140">**Product Launch day (no rules)**</span></span> |

4. <span data-ttu-id="4deea-141">Oto scenariusza skalowania hipotetycznego używamy na potrzeby tego przewodnika.</span><span class="sxs-lookup"><span data-stu-id="4deea-141">Here is a hypothetical scaling scenario that we use for this walk-through.</span></span>

    * <span data-ttu-id="4deea-142">**Na podstawie obciążenia** — Chcę skalowania w poziomie lub w oparciu o obciążenie mojej aplikacji hostowanych na mój set.* skali</span><span class="sxs-lookup"><span data-stu-id="4deea-142">**Load based** - I'd like to scale out or in based on the load on my application hosted on my scale set.*</span></span>
    * <span data-ttu-id="4deea-143">**Rozmiar kolejki wiadomości** -używam kolejką usługi Service Bus dla komunikatów przychodzących do mojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4deea-143">**Message Queue size** - I use a Service Bus Queue for the incoming messages to my application.</span></span> <span data-ttu-id="4deea-144">Użyj kolejki wiadomości i procent użycia procesora CPU i skonfigurować profil domyślny, aby wyzwolić akcji skalowania, jeśli liczba komunikatów lub Procesora trafienia threshold.*</span><span class="sxs-lookup"><span data-stu-id="4deea-144">I use the queue's message count and CPU% and configure a default profile to trigger a scale action if either of message count or CPU hits the threshold.*</span></span>
    * <span data-ttu-id="4deea-145">**Czas tydzień i dzień** — Chcę co tydzień cyklicznego profilu "czasu dnia", na podstawie o nazwie "Godzin dnia tygodnia rano".</span><span class="sxs-lookup"><span data-stu-id="4deea-145">**Time of week and day** - I want a weekly recurring 'time of the day' based profile called 'Weekday Morning Hours'.</span></span> <span data-ttu-id="4deea-146">Na podstawie danych historycznych, wiadomo, że warto mieć określoną liczbę wystąpień maszyn wirtualnych do obsługi obciążenia mojej aplikacji podczas tego time.*</span><span class="sxs-lookup"><span data-stu-id="4deea-146">Based on historical data, I know it is better to have certain number of VM instances to handle my application's load during this time.*</span></span>
    * <span data-ttu-id="4deea-147">**Wybranych dat** — po dodaniu profilu produktu uruchamianie dnia.</span><span class="sxs-lookup"><span data-stu-id="4deea-147">**Special Dates** - I added a 'Product Launch Day' profile.</span></span> <span data-ttu-id="4deea-148">I planowanie określonymi datami tak Moja aplikacja jest gotowa do obsługi obciążenia powodu anonsów marketing i testujemy nowego produktu w application.*</span><span class="sxs-lookup"><span data-stu-id="4deea-148">I plan ahead for specific dates so my application is ready to handle the load due marketing announcements and when we put a new product in the application.*</span></span>
    * <span data-ttu-id="4deea-149">*Ostatnie dwa profile ma także inne metryki na podstawie zasad wydajności w nich. W takim przypadku I postanowiła nie istnieje, a zamiast tego polegać na domyślne metryki wydajności na podstawie reguł. Reguły są opcjonalne dla profilów cyklicznego i oparty na dacie.*</span><span class="sxs-lookup"><span data-stu-id="4deea-149">*The last two profiles can also have other performance metric based rules within them. In this case, I decided not to have one and instead to rely on the default performance metric based rules. Rules are optional for the recurring and date-based profiles.*</span></span>

    <span data-ttu-id="4deea-150">Aparat skalowania automatycznego priorytetyzacji profilów i zasad jest również przechwycone w [najlepsze rozwiązania w zakresie Skalowanie automatyczne](insights-autoscale-best-practices.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="4deea-150">Autoscale engine's prioritization of the profiles and rules is also captured in the [autoscaling best practices](insights-autoscale-best-practices.md) article.</span></span>
    <span data-ttu-id="4deea-151">Listę typowych metryki skalowania automatycznego zawiera [wspólnej metryki automatycznego skalowania](insights-autoscale-common-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="4deea-151">For a list of common metrics for autoscale, refer [Common metrics for Autoscale](insights-autoscale-common-metrics.md)</span></span>

5. <span data-ttu-id="4deea-152">Upewnij się, że jesteś na **odczytu/zapisu** trybu w Eksploratorze zasobów</span><span class="sxs-lookup"><span data-stu-id="4deea-152">Make sure you are on the **Read/Write** mode in Resource Explorer</span></span>

    ![Autoscalewad, ustawienie skalowania automatycznego domyślne](./media/insights-advanced-autoscale-vmss/autoscalewad.png)

6. <span data-ttu-id="4deea-154">Kliknij przycisk Edytuj.</span><span class="sxs-lookup"><span data-stu-id="4deea-154">Click Edit.</span></span> <span data-ttu-id="4deea-155">**Zastąp** element "profilów" w ustawieniu skalowania automatycznego przy użyciu następującej konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="4deea-155">**Replace** the 'profiles' element in autoscale setting with the following configuration:</span></span>

    ![Profile](./media/insights-advanced-autoscale-vmss/profiles.png)

    ```
    {
            "name": "Perf_Based_Scale",
            "capacity": {
              "minimum": "2",
              "maximum": "12",
              "default": "2"
            },
            "rules": [
              {
                "metricTrigger": {
                  "metricName": "MessageCount",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 10
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "MessageCount",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "LessThan",
                  "threshold": 3
                },
                "scaleAction": {
                  "direction": "Decrease",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "Percentage CPU",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.Compute/virtualMachineScaleSets/<this_vmss_name>",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT30M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 85
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "Percentage CPU",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.Compute/virtualMachineScaleSets/<this_vmss_name>",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT30M",
                  "timeAggregation": "Average",
                  "operator": "LessThan",
                  "threshold": 60
                },
                "scaleAction": {
                  "direction": "Decrease",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              }
            ]
          },
          {
            "name": "Weekday_Morning_Hours_Scale",
            "capacity": {
              "minimum": "4",
              "maximum": "12",
              "default": "4"
            },
            "rules": [],
            "recurrence": {
              "frequency": "Week",
              "schedule": {
                "timeZone": "Pacific Standard Time",
                "days": [
                  "Monday",
                  "Tuesday",
                  "Wednesday",
                  "Thursday",
                  "Friday"
                ],
                "hours": [
                  6
                ],
                "minutes": [
                  0
                ]
              }
            }
          },
          {
            "name": "Product_Launch_Day",
            "capacity": {
              "minimum": "6",
              "maximum": "20",
              "default": "6"
            },
            "rules": [],
            "fixedDate": {
              "timeZone": "Pacific Standard Time",
              "start": "2016-06-20T00:06:00Z",
              "end": "2016-06-21T23:59:00Z"
            }
          }
    ```
    <span data-ttu-id="4deea-157">Obsługiwane pól i ich wartości, zobacz [dokumentacja interfejsu API REST skalowania automatycznego](https://msdn.microsoft.com/en-us/library/azure/dn931928.aspx).</span><span class="sxs-lookup"><span data-stu-id="4deea-157">For supported fields and their values, see [Autoscale REST API documentation](https://msdn.microsoft.com/en-us/library/azure/dn931928.aspx).</span></span> <span data-ttu-id="4deea-158">Teraz ustawienia skalowania automatycznego zawiera trzy profile wyjaśniono wcześniej.</span><span class="sxs-lookup"><span data-stu-id="4deea-158">Now your autoscale setting contains the three profiles explained previously.</span></span>

7. <span data-ttu-id="4deea-159">Na koniec przyjrzeć się skalowania automatycznego **powiadomień** sekcji.</span><span class="sxs-lookup"><span data-stu-id="4deea-159">Finally, look at the Autoscale **notification** section.</span></span> <span data-ttu-id="4deea-160">Powiadomienia skalowania automatycznego umożliwiają wykonać trzy czynności podczas skalowania w poziomie lub w akcji pomyślnie zostanie wywołany.</span><span class="sxs-lookup"><span data-stu-id="4deea-160">Autoscale notifications allow you to do three things when a scale-out or in action is successfully triggered.</span></span>
   - <span data-ttu-id="4deea-161">Powiadom administratora i współadministratorzy subskrypcji</span><span class="sxs-lookup"><span data-stu-id="4deea-161">Notify the admin and co-admins of your subscription</span></span>
   - <span data-ttu-id="4deea-162">Wyślij wiadomość e-mail zbioru użytkowników</span><span class="sxs-lookup"><span data-stu-id="4deea-162">Email a set of users</span></span>
   - <span data-ttu-id="4deea-163">Wyzwala wywołanie elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="4deea-163">Trigger a webhook call.</span></span> <span data-ttu-id="4deea-164">Po, ten element webhook wysyła metadane dotyczące warunku Skalowanie automatyczne i zestawu skalowania zasobu.</span><span class="sxs-lookup"><span data-stu-id="4deea-164">When fired, this webhook sends metadata about the autoscaling condition and the scale set resource.</span></span> <span data-ttu-id="4deea-165">Aby dowiedzieć się więcej na temat ładunku webhook skalowania automatycznego, zobacz [skonfigurować elementu Webhook & powiadomienia E-mail dotyczące skalowania automatycznego](insights-autoscale-to-webhook-email.md).</span><span class="sxs-lookup"><span data-stu-id="4deea-165">To learn more about the payload of autoscale webhook, see [Configure Webhook & Email Notifications for Autoscale](insights-autoscale-to-webhook-email.md).</span></span>

   <span data-ttu-id="4deea-166">Dodaj następującą wartość do ustawienia skalowania automatycznego zastąpienia z **powiadomień** elementu, którego wartość ma wartość null</span><span class="sxs-lookup"><span data-stu-id="4deea-166">Add the following to the Autoscale setting replacing your **notification** element whose value is null</span></span>

   ```
   "notifications": [
      {
        "operation": "Scale",
        "email": {
          "sendToSubscriptionAdministrator": true,
          "sendToSubscriptionCoAdministrators": false,
          "customEmails": [
              "user1@mycompany.com",
              "user2@mycompany.com"
              ]
        },
        "webhooks": [
          {
            "serviceUri": "https://foo.webhook.example.com?token=abcd1234",
            "properties": {
              "optional_key1": "optional_value1",
              "optional_key2": "optional_value2"
            }
          }
        ]
      }
    ]

   ```

   <span data-ttu-id="4deea-167">Trafienia **Put** przycisk w Eksploratorze zasobów, aby zaktualizować ustawienia skalowania automatycznego.</span><span class="sxs-lookup"><span data-stu-id="4deea-167">Hit **Put** button in Resource Explorer to update the autoscale setting.</span></span>

<span data-ttu-id="4deea-168">Zaktualizowano Ustawienia skalowania automatycznego skali maszyny Wirtualnej obejmują wiele profilów skalowania i skalować powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="4deea-168">You have updated an autoscale setting on a VM Scale set to include multiple scale profiles and scale notifications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4deea-169">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4deea-169">Next Steps</span></span>
<span data-ttu-id="4deea-170">Użyj poniższych linków, aby dowiedzieć się więcej na temat skalowania automatycznego.</span><span class="sxs-lookup"><span data-stu-id="4deea-170">Use these links to learn more about autoscaling.</span></span>

[<span data-ttu-id="4deea-171">Rozwiązywanie problemów z automatycznie skalowana za pomocą zestawów skali maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="4deea-171">TroubleShoot Autoscale with Virtual Machine Scale Sets</span></span>](../virtual-machine-scale-sets/virtual-machine-scale-sets-troubleshoot.md)

[<span data-ttu-id="4deea-172">Typowe metryki automatycznego skalowania</span><span class="sxs-lookup"><span data-stu-id="4deea-172">Common Metrics for Autoscale</span></span>](insights-autoscale-common-metrics.md)

[<span data-ttu-id="4deea-173">Najlepsze rozwiązania dotyczące usługi Azure skalowania automatycznego</span><span class="sxs-lookup"><span data-stu-id="4deea-173">Best Practices for Azure Autoscale</span></span>](insights-autoscale-best-practices.md)

[<span data-ttu-id="4deea-174">Zarządzaj skalowania automatycznego przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="4deea-174">Manage Autoscale using PowerShell</span></span>](insights-powershell-samples.md#create-and-manage-autoscale-settings)

[<span data-ttu-id="4deea-175">Zarządzaj skalowania automatycznego przy użyciu interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="4deea-175">Manage Autoscale using CLI</span></span>](insights-cli-samples.md#autoscale)

[<span data-ttu-id="4deea-176">Konfigurowanie elementu Webhook & powiadomienia E-mail dotyczące skalowania automatycznego</span><span class="sxs-lookup"><span data-stu-id="4deea-176">Configure Webhook & Email Notifications for Autoscale</span></span>](insights-autoscale-to-webhook-email.md)
