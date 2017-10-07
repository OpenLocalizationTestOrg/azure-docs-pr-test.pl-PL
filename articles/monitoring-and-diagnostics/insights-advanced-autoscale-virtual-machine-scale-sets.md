---
title: "aaaAdvanced skalowania automatycznego przy użyciu usługi Azure Virtual Machines | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: ecb01e3094f715837b75ef07a7dbecdf0f2e78f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-autoscale-configuration-using-resource-manager-templates-for-vm-scale-sets"></a><span data-ttu-id="85c1c-103">Zestawy skalowania maszyny Wirtualnej za pomocą szablonów usługi Resource Manager konfiguracji zaawansowanej skalowania automatycznego</span><span class="sxs-lookup"><span data-stu-id="85c1c-103">Advanced autoscale configuration using Resource Manager templates for VM Scale Sets</span></span>
<span data-ttu-id="85c1c-104">Można w skali i skalowalnego w poziomie w zestawy skalowania maszyny wirtualnej w oparciu metryki progów wydajności, zgodnie z cyklicznym harmonogramem lub w określonym dniu.</span><span class="sxs-lookup"><span data-stu-id="85c1c-104">You can scale-in and scale-out in Virtual Machine Scale Sets based on performance metric thresholds, by a recurring schedule, or by a particular date.</span></span> <span data-ttu-id="85c1c-105">Można również skonfigurować powiadomienia e-mail i elementu webhook dla akcji skalowania.</span><span class="sxs-lookup"><span data-stu-id="85c1c-105">You can also configure email and webhook notifications for scale actions.</span></span> <span data-ttu-id="85c1c-106">W tym przewodniku przedstawiono przykład konfigurowania tych obiektów przy użyciu szablonu usługi Resource Manager dla zestawu skalowania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="85c1c-106">This walkthrough shows an example of configuring all these objects using a Resource Manager template on a VM Scale Set.</span></span>

> [!NOTE]
> <span data-ttu-id="85c1c-107">Gdy w tym przewodniku wyjaśniono powitania dla zestawy skalowania maszyny Wirtualnej, hello te same informacje dotyczą tooautoscaling [usługi w chmurze](https://azure.microsoft.com/services/cloud-services/), i [usługi aplikacji — aplikacje sieci Web](https://azure.microsoft.com/services/app-service/web/).</span><span class="sxs-lookup"><span data-stu-id="85c1c-107">While this walkthrough explains hello steps for VM Scale Sets, hello same information applies tooautoscaling [Cloud Services](https://azure.microsoft.com/services/cloud-services/), and [App Service - Web Apps](https://azure.microsoft.com/services/app-service/web/).</span></span>
> <span data-ttu-id="85c1c-108">Dla prostego skali we/wy ustawienie dla zestawu skalowania maszyny Wirtualnej w oparciu o metryki wydajności prosty przykład procesora CPU, zobacz toohello [Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) i [Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) dokumentów</span><span class="sxs-lookup"><span data-stu-id="85c1c-108">For a simple scale in/out setting on a VM Scale Set based on a simple performance metric such as CPU, refer toohello [Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) and [Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) documents</span></span>
>
>

## <a name="walkthrough"></a><span data-ttu-id="85c1c-109">Przewodnik</span><span class="sxs-lookup"><span data-stu-id="85c1c-109">Walkthrough</span></span>
<span data-ttu-id="85c1c-110">W tym przewodniku używamy [Eksploratora zasobów Azure](https://resources.azure.com/) tooconfigure i zaktualizuj ustawienia skalowania automatycznego powitania dla zestawu skalowania.</span><span class="sxs-lookup"><span data-stu-id="85c1c-110">In this walkthrough, we use [Azure Resource Explorer](https://resources.azure.com/) tooconfigure and update hello autoscale setting for a scale set.</span></span> <span data-ttu-id="85c1c-111">Eksplorator zasobów platformy Azure jest łatwy sposób toomanage zasobów platformy Azure za pomocą szablonów Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="85c1c-111">Azure Resource Explorer is an easy way toomanage Azure resources via Resource Manager templates.</span></span> <span data-ttu-id="85c1c-112">W przypadku nowego narzędzia Eksplorator zasobów tooAzure odczytu [to wprowadzenie](https://azure.microsoft.com/blog/azure-resource-explorer-a-new-tool-to-discover-the-azure-api/).</span><span class="sxs-lookup"><span data-stu-id="85c1c-112">If you are new tooAzure Resource Explorer tool, read [this introduction](https://azure.microsoft.com/blog/azure-resource-explorer-a-new-tool-to-discover-the-azure-api/).</span></span>

1. <span data-ttu-id="85c1c-113">Wdrożenie nowej skali ustawić przy użyciu ustawienia skalowania automatycznego podstawowe.</span><span class="sxs-lookup"><span data-stu-id="85c1c-113">Deploy a new scale set with a basic autoscale setting.</span></span> <span data-ttu-id="85c1c-114">W tym artykule wykorzystano hello jedną z galerii Szybki Start Azure, który ma systemu Windows hello zestawu przy użyciu szablonu podstawowego skalowania automatycznego skalowania.</span><span class="sxs-lookup"><span data-stu-id="85c1c-114">This article uses hello one from hello Azure QuickStart Gallery, which has a Windows scale set with a basic autoscale template.</span></span> <span data-ttu-id="85c1c-115">Skala Linux ustawia hello pracy tak samo.</span><span class="sxs-lookup"><span data-stu-id="85c1c-115">Linux scale sets work hello same way.</span></span>
2. <span data-ttu-id="85c1c-116">Po utworzeniu zestawu skalowania hello Przejdź zasób zestawu skali toohello z Eksploratora zasobów Azure.</span><span class="sxs-lookup"><span data-stu-id="85c1c-116">After hello scale set is created, navigate toohello scale set resource from Azure Resource Explorer.</span></span> <span data-ttu-id="85c1c-117">Zostanie wyświetlony następujący hello w elemencie Microsoft.Insights węźle.</span><span class="sxs-lookup"><span data-stu-id="85c1c-117">You see hello following under Microsoft.Insights node.</span></span>

    ![Eksplorator systemu Azure](./media/insights-advanced-autoscale-vmss/azure_explorer_navigate.png)

    <span data-ttu-id="85c1c-119">wykonanie szablonu Hello utworzył domyślnego ustawienia skalowania automatycznego o nazwie hello **"autoscalewad"**.</span><span class="sxs-lookup"><span data-stu-id="85c1c-119">hello template execution has created a default autoscale setting with hello name **'autoscalewad'**.</span></span> <span data-ttu-id="85c1c-120">Na prawej stronie powitania można wyświetlić hello pełnej definicji tego ustawienia skalowania automatycznego.</span><span class="sxs-lookup"><span data-stu-id="85c1c-120">On hello right-hand side, you can view hello full definition of this autoscale setting.</span></span> <span data-ttu-id="85c1c-121">W takim przypadku hello domyślne ustawienie skalowania automatycznego zawiera reguły Procesora % na podstawie skalowalnego w poziomie i w skali.</span><span class="sxs-lookup"><span data-stu-id="85c1c-121">In this case, hello default autoscale setting comes with a CPU% based scale-out and scale-in rule.</span></span>  

3. <span data-ttu-id="85c1c-122">Teraz można dodać więcej profilów i reguły na podstawie harmonogramu hello lub określone wymagania.</span><span class="sxs-lookup"><span data-stu-id="85c1c-122">You can now add more profiles and rules based on hello schedule or specific requirements.</span></span> <span data-ttu-id="85c1c-123">Utworzymy ustawieniu skalowania automatycznego przy użyciu trzech profilów.</span><span class="sxs-lookup"><span data-stu-id="85c1c-123">We create an autoscale setting with three profiles.</span></span> <span data-ttu-id="85c1c-124">Profile toounderstand i zasady automatycznego skalowania, przejrzyj [najlepsze rozwiązania w zakresie skalowania automatycznego](insights-autoscale-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="85c1c-124">toounderstand profiles and rules in autoscale, review [Autoscale Best Practices](insights-autoscale-best-practices.md).</span></span>  

    | <span data-ttu-id="85c1c-125">Profile & reguły</span><span class="sxs-lookup"><span data-stu-id="85c1c-125">Profiles & Rules</span></span> | <span data-ttu-id="85c1c-126">Opis</span><span class="sxs-lookup"><span data-stu-id="85c1c-126">Description</span></span> |
    |--- | --- |
    | <span data-ttu-id="85c1c-127">**Profil**</span><span class="sxs-lookup"><span data-stu-id="85c1c-127">**Profile**</span></span> |<span data-ttu-id="85c1c-128">**Na podstawie wydajności/metryki**</span><span class="sxs-lookup"><span data-stu-id="85c1c-128">**Performance/metric based**</span></span> |
    | <span data-ttu-id="85c1c-129">Reguła</span><span class="sxs-lookup"><span data-stu-id="85c1c-129">Rule</span></span> |<span data-ttu-id="85c1c-130">Liczba wiadomości w kolejce magistrali usługi > x</span><span class="sxs-lookup"><span data-stu-id="85c1c-130">Service Bus Queue Message Count > x</span></span> |
    | <span data-ttu-id="85c1c-131">Reguła</span><span class="sxs-lookup"><span data-stu-id="85c1c-131">Rule</span></span> |<span data-ttu-id="85c1c-132">Liczba wiadomości w kolejce magistrali usługi < y</span><span class="sxs-lookup"><span data-stu-id="85c1c-132">Service Bus Queue Message Count < y</span></span> |
    | <span data-ttu-id="85c1c-133">Reguła</span><span class="sxs-lookup"><span data-stu-id="85c1c-133">Rule</span></span> |<span data-ttu-id="85c1c-134">Procent użycia procesora CPU > n</span><span class="sxs-lookup"><span data-stu-id="85c1c-134">CPU% > n</span></span> |
    | <span data-ttu-id="85c1c-135">Reguła</span><span class="sxs-lookup"><span data-stu-id="85c1c-135">Rule</span></span> |<span data-ttu-id="85c1c-136">Procent użycia procesora CPU < p</span><span class="sxs-lookup"><span data-stu-id="85c1c-136">CPU% < p</span></span> |
    | <span data-ttu-id="85c1c-137">**Profil**</span><span class="sxs-lookup"><span data-stu-id="85c1c-137">**Profile**</span></span> |<span data-ttu-id="85c1c-138">**Dzień tygodnia godziny rano (Brak reguł)**</span><span class="sxs-lookup"><span data-stu-id="85c1c-138">**Weekday morning hours (no rules)**</span></span> |
    | <span data-ttu-id="85c1c-139">**Profil**</span><span class="sxs-lookup"><span data-stu-id="85c1c-139">**Profile**</span></span> |<span data-ttu-id="85c1c-140">**Dzień uruchamiania produktu (Brak reguł)**</span><span class="sxs-lookup"><span data-stu-id="85c1c-140">**Product Launch day (no rules)**</span></span> |

4. <span data-ttu-id="85c1c-141">Oto scenariusza skalowania hipotetycznego używamy na potrzeby tego przewodnika.</span><span class="sxs-lookup"><span data-stu-id="85c1c-141">Here is a hypothetical scaling scenario that we use for this walk-through.</span></span>

    * <span data-ttu-id="85c1c-142">**Na podstawie obciążenia** — Chcę się tooscale out lub w oparte na powitania obciążenie mojej aplikacji hostowanych na mój set.* skali</span><span class="sxs-lookup"><span data-stu-id="85c1c-142">**Load based** - I'd like tooscale out or in based on hello load on my application hosted on my scale set.*</span></span>
    * <span data-ttu-id="85c1c-143">**Rozmiar kolejki wiadomości** -kolejką usługi Service Bus można używać do hello przychodzących komunikatów toomy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="85c1c-143">**Message Queue size** - I use a Service Bus Queue for hello incoming messages toomy application.</span></span> <span data-ttu-id="85c1c-144">Liczba wiadomości w kolejce hello i procent użycia procesora CPU i skonfiguruj tootrigger profil domyślny akcji skalowania, jeśli liczba komunikatów lub Procesora trafień hello threshold.*</span><span class="sxs-lookup"><span data-stu-id="85c1c-144">I use hello queue's message count and CPU% and configure a default profile tootrigger a scale action if either of message count or CPU hits hello threshold.*</span></span>
    * <span data-ttu-id="85c1c-145">**Czas tydzień i dzień** — Chcę co tydzień cyklicznego profilu "czasu dnia hello", na podstawie o nazwie "Godzin dnia tygodnia rano".</span><span class="sxs-lookup"><span data-stu-id="85c1c-145">**Time of week and day** - I want a weekly recurring 'time of hello day' based profile called 'Weekday Morning Hours'.</span></span> <span data-ttu-id="85c1c-146">Na podstawie danych historycznych, wiadomo, że jest lepsze toohave pewność, że liczba maszyn wirtualnych wystąpień toohandle Moja aplikacja obciążenia podczas tego time.*</span><span class="sxs-lookup"><span data-stu-id="85c1c-146">Based on historical data, I know it is better toohave certain number of VM instances toohandle my application's load during this time.*</span></span>
    * <span data-ttu-id="85c1c-147">**Wybranych dat** — po dodaniu profilu produktu uruchamianie dnia.</span><span class="sxs-lookup"><span data-stu-id="85c1c-147">**Special Dates** - I added a 'Product Launch Day' profile.</span></span> <span data-ttu-id="85c1c-148">I planowanie określonymi datami tak Moja aplikacja jest gotowy toohandle hello obciążenia powodu anonsów marketing i gdy testujemy nowego produktu hello application.*</span><span class="sxs-lookup"><span data-stu-id="85c1c-148">I plan ahead for specific dates so my application is ready toohandle hello load due marketing announcements and when we put a new product in hello application.*</span></span>
    * <span data-ttu-id="85c1c-149">*ostatnie dwa profile Hello ma także inne metryki na podstawie zasad wydajności w nich. W takim przypadku I uzgodnionych nie toohave, jeden i zamiast tego toorely na powitania metrykę wydajności na podstawie reguł. Reguły są opcjonalne dla profilów hello cyklicznego i oparty na dacie.*</span><span class="sxs-lookup"><span data-stu-id="85c1c-149">*hello last two profiles can also have other performance metric based rules within them. In this case, I decided not toohave one and instead toorely on hello default performance metric based rules. Rules are optional for hello recurring and date-based profiles.*</span></span>

    <span data-ttu-id="85c1c-150">Aparat skalowania automatycznego priorytetyzacji hello profile i reguł, również zostanie zarejestrowane w hello [najlepsze rozwiązania w zakresie Skalowanie automatyczne](insights-autoscale-best-practices.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="85c1c-150">Autoscale engine's prioritization of hello profiles and rules is also captured in hello [autoscaling best practices](insights-autoscale-best-practices.md) article.</span></span>
    <span data-ttu-id="85c1c-151">Listę typowych metryki skalowania automatycznego zawiera [wspólnej metryki automatycznego skalowania](insights-autoscale-common-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="85c1c-151">For a list of common metrics for autoscale, refer [Common metrics for Autoscale](insights-autoscale-common-metrics.md)</span></span>

5. <span data-ttu-id="85c1c-152">Upewnij się, że znajdują się na powitania **odczytu/zapisu** trybu w Eksploratorze zasobów</span><span class="sxs-lookup"><span data-stu-id="85c1c-152">Make sure you are on hello **Read/Write** mode in Resource Explorer</span></span>

    ![Autoscalewad, ustawienie skalowania automatycznego domyślne](./media/insights-advanced-autoscale-vmss/autoscalewad.png)

6. <span data-ttu-id="85c1c-154">Kliknij przycisk Edytuj.</span><span class="sxs-lookup"><span data-stu-id="85c1c-154">Click Edit.</span></span> <span data-ttu-id="85c1c-155">**Zastąp** element profile"hello" w ustawieniu skalowania automatycznego z hello następującej konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="85c1c-155">**Replace** hello 'profiles' element in autoscale setting with hello following configuration:</span></span>

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
    <span data-ttu-id="85c1c-157">Obsługiwane pól i ich wartości, zobacz [dokumentacja interfejsu API REST skalowania automatycznego](https://msdn.microsoft.com/en-us/library/azure/dn931928.aspx).</span><span class="sxs-lookup"><span data-stu-id="85c1c-157">For supported fields and their values, see [Autoscale REST API documentation](https://msdn.microsoft.com/en-us/library/azure/dn931928.aspx).</span></span> <span data-ttu-id="85c1c-158">Teraz ustawienia skalowania automatycznego zawiera trzy profile hello wyjaśniono wcześniej.</span><span class="sxs-lookup"><span data-stu-id="85c1c-158">Now your autoscale setting contains hello three profiles explained previously.</span></span>

7. <span data-ttu-id="85c1c-159">Na koniec przyjrzeć się hello skalowania automatycznego **powiadomień** sekcji.</span><span class="sxs-lookup"><span data-stu-id="85c1c-159">Finally, look at hello Autoscale **notification** section.</span></span> <span data-ttu-id="85c1c-160">Powiadomienia skalowania automatycznego pozwalają toodo trzy czynności podczas skalowania w poziomie lub w akcji pomyślnie zostanie wywołany.</span><span class="sxs-lookup"><span data-stu-id="85c1c-160">Autoscale notifications allow you toodo three things when a scale-out or in action is successfully triggered.</span></span>
   - <span data-ttu-id="85c1c-161">Powiadom Witaj, Administratorze i współadministratorzy subskrypcji</span><span class="sxs-lookup"><span data-stu-id="85c1c-161">Notify hello admin and co-admins of your subscription</span></span>
   - <span data-ttu-id="85c1c-162">Wyślij wiadomość e-mail zbioru użytkowników</span><span class="sxs-lookup"><span data-stu-id="85c1c-162">Email a set of users</span></span>
   - <span data-ttu-id="85c1c-163">Wyzwala wywołanie elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="85c1c-163">Trigger a webhook call.</span></span> <span data-ttu-id="85c1c-164">Po, ten element webhook wysyła metadane dotyczące hello Skalowanie automatyczne warunku i zestawu skalowania hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="85c1c-164">When fired, this webhook sends metadata about hello autoscaling condition and hello scale set resource.</span></span> <span data-ttu-id="85c1c-165">toolearn więcej informacji o ładunku hello webhook skalowania automatycznego, zobacz [skonfigurować elementu Webhook & powiadomienia E-mail dotyczące skalowania automatycznego](insights-autoscale-to-webhook-email.md).</span><span class="sxs-lookup"><span data-stu-id="85c1c-165">toolearn more about hello payload of autoscale webhook, see [Configure Webhook & Email Notifications for Autoscale](insights-autoscale-to-webhook-email.md).</span></span>

   <span data-ttu-id="85c1c-166">Dodaj powitania po zastępuje ustawienie skalowania automatycznego toohello Twojego **powiadomień** elementu, którego wartość ma wartość null</span><span class="sxs-lookup"><span data-stu-id="85c1c-166">Add hello following toohello Autoscale setting replacing your **notification** element whose value is null</span></span>

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

   <span data-ttu-id="85c1c-167">Trafienia **Put** przycisk w ustawieniu skalowania automatycznego hello tooupdate Eksploratora zasobów.</span><span class="sxs-lookup"><span data-stu-id="85c1c-167">Hit **Put** button in Resource Explorer tooupdate hello autoscale setting.</span></span>

<span data-ttu-id="85c1c-168">Zaktualizowano skalowania automatycznego ustawienie wiele profilów skalowania tooinclude zestaw skalowania maszyny Wirtualnej i skalować powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="85c1c-168">You have updated an autoscale setting on a VM Scale set tooinclude multiple scale profiles and scale notifications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="85c1c-169">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="85c1c-169">Next Steps</span></span>
<span data-ttu-id="85c1c-170">Użyj tych toolearn łącza więcej informacji na temat Skalowanie automatyczne.</span><span class="sxs-lookup"><span data-stu-id="85c1c-170">Use these links toolearn more about autoscaling.</span></span>

[<span data-ttu-id="85c1c-171">Rozwiązywanie problemów z automatycznie skalowana za pomocą zestawów skali maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="85c1c-171">TroubleShoot Autoscale with Virtual Machine Scale Sets</span></span>](../virtual-machine-scale-sets/virtual-machine-scale-sets-troubleshoot.md)

[<span data-ttu-id="85c1c-172">Typowe metryki automatycznego skalowania</span><span class="sxs-lookup"><span data-stu-id="85c1c-172">Common Metrics for Autoscale</span></span>](insights-autoscale-common-metrics.md)

[<span data-ttu-id="85c1c-173">Najlepsze rozwiązania dotyczące usługi Azure skalowania automatycznego</span><span class="sxs-lookup"><span data-stu-id="85c1c-173">Best Practices for Azure Autoscale</span></span>](insights-autoscale-best-practices.md)

[<span data-ttu-id="85c1c-174">Zarządzaj skalowania automatycznego przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="85c1c-174">Manage Autoscale using PowerShell</span></span>](insights-powershell-samples.md#create-and-manage-autoscale-settings)

[<span data-ttu-id="85c1c-175">Zarządzaj skalowania automatycznego przy użyciu interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="85c1c-175">Manage Autoscale using CLI</span></span>](insights-cli-samples.md#autoscale)

[<span data-ttu-id="85c1c-176">Konfigurowanie elementu Webhook & powiadomienia E-mail dotyczące skalowania automatycznego</span><span class="sxs-lookup"><span data-stu-id="85c1c-176">Configure Webhook & Email Notifications for Autoscale</span></span>](insights-autoscale-to-webhook-email.md)
