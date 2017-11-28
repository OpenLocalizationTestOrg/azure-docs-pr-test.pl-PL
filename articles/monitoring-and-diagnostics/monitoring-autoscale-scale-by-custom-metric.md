---
title: "aaaGet pracę z Skalowanie automatyczne według metryki niestandardowe na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooscale zasobu według metryki niestandardowe na platformie Azure."
author: anirudhcavale
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
ms.date: 05/07/2017
ms.author: ancav
ms.openlocfilehash: d3e268ec322698d0d367361cd9c156b21e0fb6e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-auto-scale-by-custom-metric-in-azure"></a><span data-ttu-id="d10bc-103">Rozpoczynanie pracy z Skalowanie automatyczne według metryki niestandardowe na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="d10bc-103">Get started with auto scale by custom metric in Azure</span></span>
<span data-ttu-id="d10bc-104">W tym artykule opisano sposób tooscale zasobu przez niestandardowa Metryka w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d10bc-104">This article describes how tooscale your resource by a custom metric in Azure portal.</span></span>

<span data-ttu-id="d10bc-105">Azure automatyczne skalowanie monitora dotyczy tylko tooVirtual zestawy skalowania maszyny (VMSS), usługi w chmurze, planów usługi aplikacji i środowiska usługi app service.</span><span class="sxs-lookup"><span data-stu-id="d10bc-105">Azure Monitor auto scale applies only tooVirtual Machine Scale Sets (VMSS), cloud services, app service plans and app service environments.</span></span> 

# <a name="lets-get-started"></a><span data-ttu-id="d10bc-106">Umożliwia wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="d10bc-106">Lets get started</span></span>
<span data-ttu-id="d10bc-107">W tym artykule założono, że aplikacja sieci web z usługą application insights skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="d10bc-107">This article assumes that you have a web app with application insights configured.</span></span> <span data-ttu-id="d10bc-108">Jeśli nie masz już, możesz [skonfiguruj usługę Application Insights dla witryny sieci Web ASP.NET][1]</span><span class="sxs-lookup"><span data-stu-id="d10bc-108">If you don't have one already, you can [set up Application Insights for your ASP.NET website][1]</span></span>

- <span data-ttu-id="d10bc-109">Otwórz [portalu Azure][2]</span><span class="sxs-lookup"><span data-stu-id="d10bc-109">Open [Azure portal][2]</span></span>
- <span data-ttu-id="d10bc-110">Kliknij ikonę monitora Azure w okienku nawigacji po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="d10bc-110">Click on Azure Monitor icon in hello left navigation pane.</span></span>
  <span data-ttu-id="d10bc-111">![Uruchom Azure Monitor][3]</span><span class="sxs-lookup"><span data-stu-id="d10bc-111">![Launch Azure Monitor][3]</span></span>
- <span data-ttu-id="d10bc-112">Ustawienie tooview wszystkie zasoby hello, dla których automatycznego skalowania ma zastosowanie, wraz z jego bieżącym stanie skalowania automatycznego skalowania automatycznego, kliknij polecenie ![odnajdywanie automatyczne skalowanie w Monitorze systemu Azure][4]</span><span class="sxs-lookup"><span data-stu-id="d10bc-112">Click on Autoscale setting tooview all hello resources for which auto scale is applicable, along with its current autoscale status ![Discover auto scale in Azure monitor][4]</span></span>
- <span data-ttu-id="d10bc-113">Otwarcie bloku "Skalowania automatycznego" w monitorze Azure i wybierz zasób ma tooscale</span><span class="sxs-lookup"><span data-stu-id="d10bc-113">Open 'Autoscale' blade in Azure Monitor and select a resource you want tooscale</span></span>
> <span data-ttu-id="d10bc-114">Uwaga: hello czynności użyć plan usługi aplikacji skojarzonych z aplikacji sieci web, który ma skonfigurowane insights aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d10bc-114">Note: hello steps below use an app service plan associated with a web app that has app insights configured.</span></span>
- <span data-ttu-id="d10bc-115">W bloku Ustawienia skalowania hello hello zasobu należy zauważyć, że bieżąca liczba wystąpień hello jest 1.</span><span class="sxs-lookup"><span data-stu-id="d10bc-115">In hello scale setting blade for hello resource, notice that hello current instance count is 1.</span></span> <span data-ttu-id="d10bc-116">Kliknij pozycję "Włącz skalowania automatycznego".</span><span class="sxs-lookup"><span data-stu-id="d10bc-116">Click on 'Enable autoscale'.</span></span>
  <span data-ttu-id="d10bc-117">![Ustawienia skalowania dla nowej aplikacji sieci web][5]</span><span class="sxs-lookup"><span data-stu-id="d10bc-117">![Scale setting for new web app][5]</span></span>
- <span data-ttu-id="d10bc-118">Podaj nazwę dla ustawienia skalowania hello i hello kliknij "Dodaj regułę".</span><span class="sxs-lookup"><span data-stu-id="d10bc-118">Provide a name for hello scale setting, and hello click on "Add a rule".</span></span> <span data-ttu-id="d10bc-119">Zwróć uwagę, hello skali reguł opcje, które Otwiera okienko kontekstu w powitania po prawej stronie.</span><span class="sxs-lookup"><span data-stu-id="d10bc-119">Notice hello scale rule options that opens as a context pane in hello right hand side.</span></span> <span data-ttu-id="d10bc-120">Domyślnie ustawia tooscale opcji hello wystąpienia liczba przez 1, jeśli percetage Procesora hello zasobu hello przekracza 70%.</span><span class="sxs-lookup"><span data-stu-id="d10bc-120">By default, it sets hello option tooscale your instance count by 1 if hello CPU percetage of hello resource exceeds 70%.</span></span> <span data-ttu-id="d10bc-121">Zmień hello metryki źródło u góry hello zbyt "Usługi Application Insights", wybierz hello aplikacji zasobu wgląd w listy rozwijanej "Resource" hello i hello wybierz opcję Niestandardowa Metryka oparte na których ma być tooscale.</span><span class="sxs-lookup"><span data-stu-id="d10bc-121">Change hello metric source at hello top too"Application Insights", select hello app insights resource in hello 'Resource' dropdown and then select hello custom metric based on which you want tooscale.</span></span>
  <span data-ttu-id="d10bc-122">![Skalować według metryki niestandardowe][6]</span><span class="sxs-lookup"><span data-stu-id="d10bc-122">![Scale by custom metric][6]</span></span>
- <span data-ttu-id="d10bc-123">Podobne krok toohello powyżej, Dodaj regułę Skala będzie skalować w i zmniejszyć liczby skali hello, 1, jeśli niestandardowa Metryka hello jest poniżej wartości progowej.</span><span class="sxs-lookup"><span data-stu-id="d10bc-123">Similar toohello step above, add a scale rule that will scale in and decrease hello scale count by 1 if hello custom metric is below a threshold.</span></span>
  <span data-ttu-id="d10bc-124">![Oparte na procesorze skali][7]</span><span class="sxs-lookup"><span data-stu-id="d10bc-124">![Scale based on cpu][7]</span></span>
- <span data-ttu-id="d10bc-125">Ustaw hello wystąpienia limity.</span><span class="sxs-lookup"><span data-stu-id="d10bc-125">Set hello you instance limits.</span></span> <span data-ttu-id="d10bc-126">Na przykład, jeśli chcesz tooscale między wystąpieniami 2-5, w zależności od fluktuacji metryki niestandardowe hello, ustaw "minimalna" za "2", "maksymalna" za "5" i "default" zbyt 2</span><span class="sxs-lookup"><span data-stu-id="d10bc-126">For example, if you want tooscale between 2-5 instances depending on hello custom metric fluctuations, set 'minimum' too'2', 'maximum' too'5' and 'default' too'2'</span></span>
> <span data-ttu-id="d10bc-127">Uwaga: W przypadku, gdy istnieje problem z odczytem hello zasobu metryki i jest obecna pojemność hello poniżej pojemności domyślnej hello, następnie tooensure hello dostępność zasobów hello automatycznego skalowania zostanie skalowanie w poziomie toohello wartości domyślnej.</span><span class="sxs-lookup"><span data-stu-id="d10bc-127">Note: In case there is a problem reading hello resource metrics and hello current capacity is below hello default capacity, then tooensure hello availability of hello resource, Autoscale will scale out toohello default value.</span></span> <span data-ttu-id="d10bc-128">Jeśli obecna pojemność hello już jest wyższa niż pojemności domyślnej, skalowania automatycznego nie będzie skalować w.</span><span class="sxs-lookup"><span data-stu-id="d10bc-128">If hello current capacity is already higher than default capacity, Autoscale will not scale in.</span></span>
- <span data-ttu-id="d10bc-129">Kliknij przycisk "Zapisz"</span><span class="sxs-lookup"><span data-stu-id="d10bc-129">Click on 'Save'</span></span>

<span data-ttu-id="d10bc-130">Gratulacje.</span><span class="sxs-lookup"><span data-stu-id="d10bc-130">Congratulations.</span></span> <span data-ttu-id="d10bc-131">Możesz teraz został pomyślnie utworzony z tooauto ustawienie skali skalowanie aplikacji sieci web, w oparciu metryki niestandardowe.</span><span class="sxs-lookup"><span data-stu-id="d10bc-131">You now now succesfully created your scale setting tooauto scale your web app based on a custom metric.</span></span>

> <span data-ttu-id="d10bc-132">Uwaga: hello te same kroki są stosowane tooget uruchomiony w roli usługi VMSS lub w chmurze.</span><span class="sxs-lookup"><span data-stu-id="d10bc-132">Note: hello same steps are applicable tooget started with a VMSS or cloud service role.</span></span>

<!--Reference-->
[1]: https://docs.microsoft.com/en-us/azure/application-insights/app-insights-asp-net
[2]: https://portal.azure.com
[3]: ./media/monitoring-autoscale-scale-by-custom-metric/azure-monitor-launch.png
[4]: ./media/monitoring-autoscale-scale-by-custom-metric/discover-autoscale-azure-monitor.png
[5]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-setting-new-web-app.png
[6]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-by-custom-metric.png
[7]: ./media/monitoring-autoscale-scale-by-custom-metric/autoscale-setting-custom-metrics-ai.png
