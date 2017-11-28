---
title: wprowadzenie do skalowania automatycznego na platformie Azure aaaGet | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooscale zasobu na platformie Azure."
author: rajram
manager: rboucher
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: rajram
ms.openlocfilehash: 6b3c3f4529018dcaf9691c538fec63dfbb3cea06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-autoscale-in-azure"></a><span data-ttu-id="a127f-103">Wprowadzenie do skalowania automatycznego na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="a127f-103">Get started with Autoscale in Azure</span></span>
<span data-ttu-id="a127f-104">W tym artykule opisano sposób tooset zapasową ustawień automatycznego skalowania dla zasobu w portalu Microsoft Azure hello.</span><span class="sxs-lookup"><span data-stu-id="a127f-104">This article describes how tooset up your Autoscale settings for your resource in hello Microsoft Azure portal.</span></span>

<span data-ttu-id="a127f-105">Azure Monitor skalowania automatycznego ma zastosowanie tylko zestawy skalowania maszyny toovirtual, usługi w chmurze planów usługi aplikacji Azure i środowiska usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a127f-105">Azure Monitor Autoscale applies only toovirtual machine scale sets, cloud services, Azure App Service plans, and App Service environments.</span></span> 

## <a name="discover-hello-autoscale-settings-in-your-subscription"></a><span data-ttu-id="a127f-106">Wykryj ustawienia skalowania automatycznego hello w ramach subskrypcji</span><span class="sxs-lookup"><span data-stu-id="a127f-106">Discover hello Autoscale settings in your subscription</span></span>
<span data-ttu-id="a127f-107">Umożliwia odnalezienie wszystkich zasobów hello, dla których ma zastosowanie w monitorze Azure skalowania automatycznego.</span><span class="sxs-lookup"><span data-stu-id="a127f-107">You can discover all hello resources for which Autoscale is applicable in Azure Monitor.</span></span> <span data-ttu-id="a127f-108">Użyj hello następujące kroki, aby uzyskać wskazówki krok po kroku:</span><span class="sxs-lookup"><span data-stu-id="a127f-108">Use hello following steps for a step-by-step walkthrough:</span></span>

1. <span data-ttu-id="a127f-109">Otwórz hello [portalu Azure.][1]</span><span class="sxs-lookup"><span data-stu-id="a127f-109">Open hello [Azure portal.][1]</span></span>
2. <span data-ttu-id="a127f-110">Kliknij ikonę monitora Azure hello w okienku po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="a127f-110">Click hello Azure Monitor icon in hello left pane.</span></span>
  <span data-ttu-id="a127f-111">![Otwórz Monitor Azure][2]</span><span class="sxs-lookup"><span data-stu-id="a127f-111">![Open Azure Monitor][2]</span></span>
3. <span data-ttu-id="a127f-112">Kliknij przycisk **skalowania automatycznego** tooview wszystkie zasoby hello, dla których skalowania automatycznego ma zastosowanie, wraz z ich bieżący stan automatycznego skalowania.</span><span class="sxs-lookup"><span data-stu-id="a127f-112">Click **Autoscale** tooview all hello resources for which Autoscale is applicable, along with their current Autoscale status.</span></span>
  <span data-ttu-id="a127f-113">![Odnajdywanie automatycznego skalowania w Monitorze systemu Azure][3]</span><span class="sxs-lookup"><span data-stu-id="a127f-113">![Discover Autoscale in Azure Monitor][3]</span></span>

<span data-ttu-id="a127f-114">Okienko filtru hello można użyć w hello tooscope top w dół hello listy tooselect zasoby w określonej grupy zasobów, określonych typów zasobów ani konkretnego zasobu.</span><span class="sxs-lookup"><span data-stu-id="a127f-114">You can use hello filter pane at hello top tooscope down hello list tooselect resources in a specific resource group, specific resource types, or a specific resource.</span></span>

<span data-ttu-id="a127f-115">Dla każdego zasobu można znaleźć hello bieżącą liczbę wystąpień i hello skalowania automatycznego stanu.</span><span class="sxs-lookup"><span data-stu-id="a127f-115">For each resource, you will find hello current instance count and hello Autoscale status.</span></span> <span data-ttu-id="a127f-116">Witaj stanu automatycznego skalowania może być:</span><span class="sxs-lookup"><span data-stu-id="a127f-116">hello Autoscale status can be:</span></span>

- <span data-ttu-id="a127f-117">**Nieskonfigurowane**: nie włączono automatycznego skalowania jeszcze dla tego zasobu.</span><span class="sxs-lookup"><span data-stu-id="a127f-117">**Not configured**: You have not enabled Autoscale yet for this resource.</span></span>
- <span data-ttu-id="a127f-118">**Włączone**: funkcja automatycznego skalowania zostało włączone dla tego zasobu.</span><span class="sxs-lookup"><span data-stu-id="a127f-118">**Enabled**: You have enabled Autoscale for this resource.</span></span>
- <span data-ttu-id="a127f-119">**Wyłączone**: funkcja automatycznego skalowania zostało wyłączone dla tego zasobu.</span><span class="sxs-lookup"><span data-stu-id="a127f-119">**Disabled**: You have disabled Autoscale for this resource.</span></span>

## <a name="create-your-first-autoscale-setting"></a><span data-ttu-id="a127f-120">Tworzenie pierwszego Ustawienia skalowania automatycznego</span><span class="sxs-lookup"><span data-stu-id="a127f-120">Create your first Autoscale setting</span></span>

<span data-ttu-id="a127f-121">Umożliwia teraz przejść przez toocreate proste wskazówki krok po kroku pierwszego Ustawienia skalowania automatycznego.</span><span class="sxs-lookup"><span data-stu-id="a127f-121">Let's now go through a simple step-by-step walkthrough toocreate your first Autoscale setting.</span></span>

1. <span data-ttu-id="a127f-122">Otwórz hello **skalowania automatycznego** bloku Azure Monitor i wybierz zasób, które mają tooscale.</span><span class="sxs-lookup"><span data-stu-id="a127f-122">Open hello **Autoscale** blade in Azure Monitor and select a resource that you want tooscale.</span></span> <span data-ttu-id="a127f-123">(hello następujące kroki Użyj planu usługi aplikacji skojarzone z aplikacją sieci web.</span><span class="sxs-lookup"><span data-stu-id="a127f-123">(hello following steps use an App Service plan associated with a web app.</span></span> <span data-ttu-id="a127f-124">Możesz [tworzenie pierwszej aplikacji sieci web platformy ASP.NET na platformie Azure w ciągu 5 minut.] [4])</span><span class="sxs-lookup"><span data-stu-id="a127f-124">You can [create your first ASP.NET web app in Azure in 5 minutes.][4])</span></span>
2. <span data-ttu-id="a127f-125">Należy pamiętać, że bieżąca liczba wystąpień hello 1.</span><span class="sxs-lookup"><span data-stu-id="a127f-125">Note that hello current instance count is 1.</span></span> <span data-ttu-id="a127f-126">Kliknij przycisk **Włączanie automatycznego skalowania**.</span><span class="sxs-lookup"><span data-stu-id="a127f-126">Click **Enable autoscale**.</span></span>
  <span data-ttu-id="a127f-127">![Ustawienia skalowania dla nowej aplikacji sieci web][5]</span><span class="sxs-lookup"><span data-stu-id="a127f-127">![Scale setting for new web app][5]</span></span>
3. <span data-ttu-id="a127f-128">Podaj nazwę dla ustawienia skalowania hello, a następnie kliknij przycisk **dodać regułę**.</span><span class="sxs-lookup"><span data-stu-id="a127f-128">Provide a name for hello scale setting, and then click **Add a rule**.</span></span> <span data-ttu-id="a127f-129">Zwróć uwagę, opcje reguły skalowania hello Otwórz okienko kontekstu hello prawej strony.</span><span class="sxs-lookup"><span data-stu-id="a127f-129">Notice hello scale rule options that open as a context pane on hello right side.</span></span> <span data-ttu-id="a127f-130">Domyślnie to ustawienie tooscale opcji hello wystąpienia liczba 1, jeśli hello procent użycia procesora CPU zasobu hello przekracza 70 procent.</span><span class="sxs-lookup"><span data-stu-id="a127f-130">By default, this sets hello option tooscale your instance count by 1 if hello CPU percentage of hello resource exceeds 70 percent.</span></span> <span data-ttu-id="a127f-131">Pozostaw wartości domyślne, a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="a127f-131">Leave it at its default values and click **Add**.</span></span>
  <span data-ttu-id="a127f-132">![Utwórz ustawienie skali dla aplikacji sieci web][6]</span><span class="sxs-lookup"><span data-stu-id="a127f-132">![Create scale setting for a web app][6]</span></span>
4. <span data-ttu-id="a127f-133">Został już utworzony pierwszej reguły skalowania.</span><span class="sxs-lookup"><span data-stu-id="a127f-133">You've now created your first scale rule.</span></span> <span data-ttu-id="a127f-134">Należy pamiętać, że hello UX zaleca najlepszych rozwiązań i stanów "zalecane jest toohave co najmniej jeden skali w regule."</span><span class="sxs-lookup"><span data-stu-id="a127f-134">Note that hello UX recommends best practices and states that "It is recommended toohave at least one scale in rule."</span></span> <span data-ttu-id="a127f-135">toodo tak:</span><span class="sxs-lookup"><span data-stu-id="a127f-135">toodo so:</span></span>
  
    <span data-ttu-id="a127f-136">a.</span><span class="sxs-lookup"><span data-stu-id="a127f-136">a.</span></span> <span data-ttu-id="a127f-137">Kliknij przycisk **dodać regułę**.</span><span class="sxs-lookup"><span data-stu-id="a127f-137">Click **Add a rule**.</span></span> 

    <span data-ttu-id="a127f-138">b.</span><span class="sxs-lookup"><span data-stu-id="a127f-138">b.</span></span> <span data-ttu-id="a127f-139">Ustaw **Operator** za**mniej niż**.</span><span class="sxs-lookup"><span data-stu-id="a127f-139">Set **Operator** too**Less than**.</span></span>

    <span data-ttu-id="a127f-140">c.</span><span class="sxs-lookup"><span data-stu-id="a127f-140">c.</span></span> <span data-ttu-id="a127f-141">Ustaw **próg** za**20**.</span><span class="sxs-lookup"><span data-stu-id="a127f-141">Set **Threshold** too**20**.</span></span>

    <span data-ttu-id="a127f-142">d.</span><span class="sxs-lookup"><span data-stu-id="a127f-142">d.</span></span> <span data-ttu-id="a127f-143">Ustaw **operacji** za**zmniejszyć liczbę przez**.</span><span class="sxs-lookup"><span data-stu-id="a127f-143">Set **Operation** too**Decrease count by**.</span></span>

   <span data-ttu-id="a127f-144">Teraz powinna mieć ustawienia skalowania czy skale poza/możliwość skalowania w oparciu o użycie procesora CPU.</span><span class="sxs-lookup"><span data-stu-id="a127f-144">You should now have a scale setting that scales out/scales in based on CPU usage.</span></span>
   <span data-ttu-id="a127f-145">![Oparte na Procesorze skali][8]</span><span class="sxs-lookup"><span data-stu-id="a127f-145">![Scale based on CPU][8]</span></span>
5. <span data-ttu-id="a127f-146">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="a127f-146">Click **Save**.</span></span>

<span data-ttu-id="a127f-147">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="a127f-147">Congratulations!</span></span> <span data-ttu-id="a127f-148">Pierwszy tooautoscale w Ustawienia skalowania aplikacji sieci web oparta na użycie procesora CPU teraz została pomyślnie utworzona.</span><span class="sxs-lookup"><span data-stu-id="a127f-148">You've now successfully created your first scale setting tooautoscale your web app based on CPU usage.</span></span>

> [!NOTE] 
> <span data-ttu-id="a127f-149">Witaj te same kroki są stosowane tooget wprowadzenie do skalowania maszyny wirtualnej zestawu lub w chmurze usługi roli.</span><span class="sxs-lookup"><span data-stu-id="a127f-149">hello same steps are applicable tooget started with a virtual machine scale set or cloud service role.</span></span>

## <a name="other-considerations"></a><span data-ttu-id="a127f-150">Inne zagadnienia</span><span class="sxs-lookup"><span data-stu-id="a127f-150">Other considerations</span></span>
### <a name="scale-based-on-a-schedule"></a><span data-ttu-id="a127f-151">Skala zgodnie z harmonogramem</span><span class="sxs-lookup"><span data-stu-id="a127f-151">Scale based on a schedule</span></span>
<span data-ttu-id="a127f-152">Ponadto tooscale oparte na Procesorze, można ustawić na skalę inaczej określone dni tygodnia hello.</span><span class="sxs-lookup"><span data-stu-id="a127f-152">In addition tooscale based on CPU, you can set your scale differently for specific days of hello week.</span></span>

1. <span data-ttu-id="a127f-153">Kliknij przycisk **Dodaj warunek skali**.</span><span class="sxs-lookup"><span data-stu-id="a127f-153">Click **Add a scale condition**.</span></span>
2. <span data-ttu-id="a127f-154">Skala hello reguły trybu i hello jest sama hello jako hello domyślnego warunku.</span><span class="sxs-lookup"><span data-stu-id="a127f-154">Setting hello scale mode and hello rules is hello same as hello default condition.</span></span>
3. <span data-ttu-id="a127f-155">Wybierz **Powtórz określone dni** hello harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="a127f-155">Select **Repeat specific days** for hello schedule.</span></span>
4. <span data-ttu-id="a127f-156">Wybierz hello dni i godziny rozpoczęcia i zakończenia hello stosowania hello Skala warunkiem.</span><span class="sxs-lookup"><span data-stu-id="a127f-156">Select hello days and hello start/end time for when hello scale condition should be applied.</span></span>

![Skala warunkiem na podstawie harmonogramu][9]
### <a name="scale-differently-on-specific-dates"></a><span data-ttu-id="a127f-158">Skalowanie inaczej w określonym dniu</span><span class="sxs-lookup"><span data-stu-id="a127f-158">Scale differently on specific dates</span></span>
<span data-ttu-id="a127f-159">Ponadto tooscale oparte na Procesorze, można ustawić na skalę inaczej dla określonej daty.</span><span class="sxs-lookup"><span data-stu-id="a127f-159">In addition tooscale based on CPU, you can set your scale differently for specific dates.</span></span>

1. <span data-ttu-id="a127f-160">Kliknij przycisk **Dodaj warunek skali**.</span><span class="sxs-lookup"><span data-stu-id="a127f-160">Click **Add a scale condition**.</span></span>
2. <span data-ttu-id="a127f-161">Skala hello reguły trybu i hello jest sama hello jako hello domyślnego warunku.</span><span class="sxs-lookup"><span data-stu-id="a127f-161">Setting hello scale mode and hello rules is hello same as hello default condition.</span></span>
3. <span data-ttu-id="a127f-162">Wybierz **określ daty rozpoczęcia i zakończenia** hello harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="a127f-162">Select **Specify start/end dates** for hello schedule.</span></span>
4. <span data-ttu-id="a127f-163">Wybierz hello rozpoczęcia i zakończenia daty i godziny rozpoczęcia i zakończenia hello stosowania hello Skala warunkiem.</span><span class="sxs-lookup"><span data-stu-id="a127f-163">Select hello start/end dates and hello start/end time for when hello scale condition should be applied.</span></span>

![Warunek skali na podstawie dat][10]

### <a name="view-hello-scale-history-of-your-resource"></a><span data-ttu-id="a127f-165">Wyświetl historię skali hello zasobu</span><span class="sxs-lookup"><span data-stu-id="a127f-165">View hello scale history of your resource</span></span>
<span data-ttu-id="a127f-166">Zawsze, gdy zasób jest skalowana w górę lub w dół, zdarzenie jest rejestrowane w dzienniku aktywności hello.</span><span class="sxs-lookup"><span data-stu-id="a127f-166">Whenever your resource is scaled up or down, an event is logged in hello activity log.</span></span> <span data-ttu-id="a127f-167">Można wyświetlić historię skali hello zasobu dla hello ostatnich 24 godzin przełączając toohello **Historia uruchomień** kartę.</span><span class="sxs-lookup"><span data-stu-id="a127f-167">You can view hello scale history of your resource for hello past 24 hours by switching toohello **Run history** tab.</span></span>

![Historia uruchomień][11]

<span data-ttu-id="a127f-169">Jeśli chcesz, aby tooview hello skali pełną historię (dla too90 dni w górę), wybierz pozycję **kliknij tutaj toosee szczegółowe**.</span><span class="sxs-lookup"><span data-stu-id="a127f-169">If you want tooview hello complete scale history (for up too90 days), select **Click here toosee more details**.</span></span> <span data-ttu-id="a127f-170">Umożliwia otwarcie dziennika aktywności Hello z automatycznego skalowania jest wstępnie zaznaczona dla zasobu i kategorii.</span><span class="sxs-lookup"><span data-stu-id="a127f-170">hello activity log opens, with Autoscale pre-selected for your resource and category.</span></span>

### <a name="view-hello-scale-definition-of-your-resource"></a><span data-ttu-id="a127f-171">Witaj skali definicji zasobu</span><span class="sxs-lookup"><span data-stu-id="a127f-171">View hello scale definition of your resource</span></span>
<span data-ttu-id="a127f-172">Skalowania automatycznego jest zasobem usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a127f-172">Autoscale is an Azure Resource Manager resource.</span></span> <span data-ttu-id="a127f-173">Hello definicji skali można wyświetlić w formacie JSON, przełączając toohello **JSON** kartę.</span><span class="sxs-lookup"><span data-stu-id="a127f-173">You can view hello scale definition in JSON by switching toohello **JSON** tab.</span></span>

![Definicja skali][12]

<span data-ttu-id="a127f-175">Należy wprowadzić zmiany w formacie JSON, jeśli jest to wymagane.</span><span class="sxs-lookup"><span data-stu-id="a127f-175">You can make changes in JSON directly, if required.</span></span> <span data-ttu-id="a127f-176">Te zmiany zostaną uwzględnione po ich zapisaniu.</span><span class="sxs-lookup"><span data-stu-id="a127f-176">These changes will be reflected after you save them.</span></span>

### <a name="disable-autoscale-and-manually-scale-your-instances"></a><span data-ttu-id="a127f-177">Wyłączanie automatycznego skalowania i ręcznie skalować swoich wystąpień</span><span class="sxs-lookup"><span data-stu-id="a127f-177">Disable Autoscale and manually scale your instances</span></span>
<span data-ttu-id="a127f-178">Może być razy podczas mają toodisable bieżące ustawienia skali i ręcznie skalować zasób.</span><span class="sxs-lookup"><span data-stu-id="a127f-178">There might be times when you want toodisable your current scale setting and manually scale your resource.</span></span>

<span data-ttu-id="a127f-179">Kliknij przycisk hello **wyłączanie automatycznego skalowania** przycisk u góry hello.</span><span class="sxs-lookup"><span data-stu-id="a127f-179">Click hello **Disable autoscale** button at hello top.</span></span>
<span data-ttu-id="a127f-180">![Wyłączanie automatycznego skalowania][13]</span><span class="sxs-lookup"><span data-stu-id="a127f-180">![Disable Autoscale][13]</span></span>

> [!NOTE] 
> <span data-ttu-id="a127f-181">Ta opcja powoduje wyłączenie konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="a127f-181">This option disables your configuration.</span></span> <span data-ttu-id="a127f-182">Jednak możesz odzyskać tooit po włączeniu skalowania automatycznego ponownie.</span><span class="sxs-lookup"><span data-stu-id="a127f-182">However, you can get back tooit after you enable Autoscale again.</span></span> 

<span data-ttu-id="a127f-183">Można teraz ustawić hello liczba wystąpień, które mają tooscale toomanually.</span><span class="sxs-lookup"><span data-stu-id="a127f-183">You can now set hello number of instances that you want tooscale toomanually.</span></span>

![Zestaw skali ręczne][14]

<span data-ttu-id="a127f-185">Możesz zawsze wrócić, klikając tooAutoscale **Włączanie automatycznego skalowania** , a następnie **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="a127f-185">You can always return tooAutoscale by clicking **Enable autoscale** and then **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a127f-186">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a127f-186">Next steps</span></span>
- [<span data-ttu-id="a127f-187">Utwórz Alert dziennika aktywności toomonitor wszystkie operacje aparat skalowania automatycznego na subskrypcję</span><span class="sxs-lookup"><span data-stu-id="a127f-187">Create an Activity Log Alert toomonitor all Autoscale engine operations on your subscription</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert)
- [<span data-ttu-id="a127f-188">Tworzenie alertów dziennika aktywności toomonitor wszystkie nieudane operacje w/skali skalowalnych w poziomie skalowania automatycznego na subskrypcję</span><span class="sxs-lookup"><span data-stu-id="a127f-188">Create an Activity Log Alert toomonitor all failed Autoscale scale-in/scale-out operations on your subscription</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert)

<!--Reference-->
[1]:https://portal.azure.com
[2]: ./media/monitoring-autoscale-get-started/azure-monitor-launch.png
[3]: ./media/monitoring-autoscale-get-started/discover-autoscale-azure-monitor.png
[4]: https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-get-started-dotnet
[5]: ./media/monitoring-autoscale-get-started/scale-setting-new-web-app.png
[6]: ./media/monitoring-autoscale-get-started/create-scale-setting-web-app.png
[7]: ./media/monitoring-autoscale-get-started/scale-in-recommendation.png
[8]: ./media/monitoring-autoscale-get-started/scale-based-on-cpu.png
[9]: ./media/monitoring-autoscale-get-started/scale-condition-schedule.png
[10]: ./media/monitoring-autoscale-get-started/scale-condition-dates.png
[11]: ./media/monitoring-autoscale-get-started/scale-history.png
[12]: ./media/monitoring-autoscale-get-started/scale-definition-json.png
[13]: ./media/monitoring-autoscale-get-started/disable-autoscale.png
[14]: ./media/monitoring-autoscale-get-started/set-manualscale.png

