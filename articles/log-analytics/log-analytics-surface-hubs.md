---
title: "Monitorowanie urządzenia Surface Hub z Azure Log Analytics | Dokumentacja firmy Microsoft"
description: "Rozwiązanie Surface Hub umożliwia śledzenie kondycji z urządzeń Surface Hub i zrozumieć, jak są one używane."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 8b4e56bc-2d4f-4648-a236-16e9e732ebef
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b6ecd0d09589fec85c1633f528afc1165c346b7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-surface-hubs-with-log-analytics-to-track-their-health"></a><span data-ttu-id="c9449-103">Monitorowanie urządzeń Surface Hub z analizy dzienników śledzenia ich kondycję</span><span class="sxs-lookup"><span data-stu-id="c9449-103">Monitor Surface Hubs with Log Analytics to track their health</span></span>

![Surface Hub symbol](./media/log-analytics-surface-hubs/surface-hub-symbol.png)

<span data-ttu-id="c9449-105">W tym artykule opisano, jak używasz rozwiązania Surface Hub w analizy dzienników do monitorowania urządzeń Microsoft Surface Hub z Microsoft Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="c9449-105">This article describes how you can use the Surface Hub solution in Log Analytics to monitor Microsoft Surface Hub devices with the Microsoft Operations Management Suite (OMS).</span></span> <span data-ttu-id="c9449-106">Analiza dzienników pomaga śledzić kondycji z urządzeń Surface Hub dobrze zrozumieć, jak są one używane.</span><span class="sxs-lookup"><span data-stu-id="c9449-106">Log Analytics helps you track the health of your Surface Hubs as well as understand how they are being used.</span></span>

<span data-ttu-id="c9449-107">Każdy Surface Hub został zainstalowany program Microsoft Monitoring Agent.</span><span class="sxs-lookup"><span data-stu-id="c9449-107">Each Surface Hub has the Microsoft Monitoring Agent installed.</span></span> <span data-ttu-id="c9449-108">Jego przez agenta, czy użytkownik może wysyłać dane z Twojego Surface Hub OMS.</span><span class="sxs-lookup"><span data-stu-id="c9449-108">Its through the agent that you can send data from your Surface Hub to OMS.</span></span> <span data-ttu-id="c9449-109">Pliki dziennika są odczytywane z urządzeń Surface Hub i są następnie są wysyłane z usługą OMS.</span><span class="sxs-lookup"><span data-stu-id="c9449-109">Log files are read from your Surface Hubs and are then are sent to the OMS service.</span></span> <span data-ttu-id="c9449-110">Zagadnienia, takie jak serwery w trybie offline, Kalendarz nie synchronizuje, lub jeśli nie może zalogować się do konta urządzeń Skype są przedstawione w OMS na pulpicie nawigacyjnym Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="c9449-110">Issues like servers being offline, the calendar not syncing, or if the device account is unable to log into Skype are shown in OMS in the Surface Hub dashboard.</span></span> <span data-ttu-id="c9449-111">Przy użyciu danych na pulpicie nawigacyjnym, można zidentyfikować urządzenia nie są uruchomione lub są inne problemy i potencjalnie zastosować poprawki dotyczące wykrytych problemów.</span><span class="sxs-lookup"><span data-stu-id="c9449-111">By using the data in the dashboard, you can identify devices that are not running, or that are having other problems, and potentially apply fixes for the detected issues.</span></span>

## <a name="installing-and-configuring-the-solution"></a><span data-ttu-id="c9449-112">Instalowanie i konfigurowanie rozwiązania</span><span class="sxs-lookup"><span data-stu-id="c9449-112">Installing and configuring the solution</span></span>
<span data-ttu-id="c9449-113">Skorzystaj z poniższych informacji, aby zainstalować i skonfigurować rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="c9449-113">Use the following information to install and configure the solution.</span></span> <span data-ttu-id="c9449-114">Aby zarządzać z urządzeń Surface Hub z Microsoft Operations Management Suite (OMS), będą potrzebne następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c9449-114">In order to manage your Surface Hubs from the Microsoft Operations Management Suite (OMS), you'll need the following:</span></span>

* <span data-ttu-id="c9449-115">Prawidłowych subskrypcji umożliwiających [OMS](http://www.microsoft.com/oms).</span><span class="sxs-lookup"><span data-stu-id="c9449-115">A valid subscription to [OMS](http://www.microsoft.com/oms).</span></span>
* <span data-ttu-id="c9449-116">[Subskrypcji OMS](https://azure.microsoft.com/pricing/details/log-analytics/) poziomu, która będzie obsługiwać liczbę urządzeń, które chcesz monitorować.</span><span class="sxs-lookup"><span data-stu-id="c9449-116">An [OMS subscription](https://azure.microsoft.com/pricing/details/log-analytics/) level that will support the number of devices you want to monitor.</span></span> <span data-ttu-id="c9449-117">Cennik pakietu OMS zmienia się w zależności od liczby urządzeń zarejestrowanych i ilość danych go procesów.</span><span class="sxs-lookup"><span data-stu-id="c9449-117">OMS pricing varies depending on how many devices are enrolled, and how much data it processes.</span></span> <span data-ttu-id="c9449-118">Należy to uwzględnić podczas planowania wdrożenia Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="c9449-118">You'll want to take this into consideration when planning your Surface Hub rollout.</span></span>

<span data-ttu-id="c9449-119">Następnie zostanie dodać subskrypcję pakietu OMS do istniejącej subskrypcji Microsoft Azure lub Utwórz nowy obszar roboczy bezpośrednio za pomocą portalu OMS.</span><span class="sxs-lookup"><span data-stu-id="c9449-119">Next, you will either add an OMS subscription to your existing Microsoft Azure subscription or create a new workspace directly through the OMS portal.</span></span> <span data-ttu-id="c9449-120">Szczegółowe instrukcje do przy użyciu jednej z metod jest w [wprowadzenie do analizy dzienników](log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c9449-120">Detailed instructions for using either method is at [Get started with Log Analytics](log-analytics-get-started.md).</span></span> <span data-ttu-id="c9449-121">Po skonfigurowaniu subskrypcji OMS istnieją dwa sposoby zarejestrować swoje urządzenia Surface Hub:</span><span class="sxs-lookup"><span data-stu-id="c9449-121">Once the OMS subscription is set up, there are two ways to enroll your Surface Hub devices:</span></span>

* <span data-ttu-id="c9449-122">Automatycznie za pomocą usługi Intune</span><span class="sxs-lookup"><span data-stu-id="c9449-122">Automatically through Intune</span></span>
* <span data-ttu-id="c9449-123">Ręcznie za pomocą **ustawienia** urządzenia Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="c9449-123">Manually through **Settings** on your Surface Hub device.</span></span>

## <a name="set-up-monitoring"></a><span data-ttu-id="c9449-124">Konfigurowanie monitorowania</span><span class="sxs-lookup"><span data-stu-id="c9449-124">Set up monitoring</span></span>
<span data-ttu-id="c9449-125">Można monitorować kondycję i działanie Centrum powierzchni przy użyciu analizy dzienników w OMS.</span><span class="sxs-lookup"><span data-stu-id="c9449-125">You can monitor the health and activity of your Surface Hub using Log Analytics in OMS.</span></span> <span data-ttu-id="c9449-126">Surface Hub w OMS można zarejestrować za pomocą usługi Intune lub lokalnie przy użyciu **ustawienia** na Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="c9449-126">You can enroll the Surface Hub in OMS by using Intune, or locally by using **Settings** on the Surface Hub.</span></span>

## <a name="connect-surface-hubs-to-oms-through-intune"></a><span data-ttu-id="c9449-127">Urządzenia Surface Hub nawiązać połączenia z usługą OMS za pomocą usługi Intune</span><span class="sxs-lookup"><span data-stu-id="c9449-127">Connect Surface Hubs to OMS through Intune</span></span>
<span data-ttu-id="c9449-128">Wymagany identyfikator i klucz obszaru roboczego dla obszaru roboczego OMS, która ma zarządzać z urządzeń Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="c9449-128">You'll need the workspace ID and workspace key for the OMS workspace that will manage your Surface Hubs.</span></span> <span data-ttu-id="c9449-129">Możesz pobrać z portalu OMS.</span><span class="sxs-lookup"><span data-stu-id="c9449-129">You can get those from the OMS portal.</span></span>

<span data-ttu-id="c9449-130">Usługa Intune jest produktem firmy Microsoft, która umożliwia centralne zarządzanie OMS ustawienia konfiguracji, które są stosowane do co najmniej jednego z urządzeń.</span><span class="sxs-lookup"><span data-stu-id="c9449-130">Intune is a Microsoft product that allows you to centrally manage the OMS configuration settings that are applied to one or more of your devices.</span></span> <span data-ttu-id="c9449-131">Wykonaj następujące kroki, aby skonfigurować urządzenia za pomocą usługi Intune:</span><span class="sxs-lookup"><span data-stu-id="c9449-131">Follow these steps to configure your devices through Intune:</span></span>

1. <span data-ttu-id="c9449-132">Zaloguj się do usługi Intune.</span><span class="sxs-lookup"><span data-stu-id="c9449-132">Sign in to Intune.</span></span>
2. <span data-ttu-id="c9449-133">Przejdź do **ustawienia** > **połączone źródła**.</span><span class="sxs-lookup"><span data-stu-id="c9449-133">Navigate to **Settings** > **Connected Sources**.</span></span>
3. <span data-ttu-id="c9449-134">Utwórz lub Edytuj zasady na podstawie szablonu Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="c9449-134">Create or edit a policy based on the Surface Hub template.</span></span>
4. <span data-ttu-id="c9449-135">Przejdź do sekcji OMS (Azure Operational Insights), zasad, a następnie dodaj *identyfikator obszaru roboczego* i *klucz obszaru roboczego* z zasadami.</span><span class="sxs-lookup"><span data-stu-id="c9449-135">Navigate to the OMS (Azure Operational Insights) section of the policy, and add the *Workspace ID* and *Workspace Key* to the policy.</span></span>
5. <span data-ttu-id="c9449-136">Zapisać zasady.</span><span class="sxs-lookup"><span data-stu-id="c9449-136">Save the policy.</span></span>
6. <span data-ttu-id="c9449-137">Skojarzyć zasady z odpowiedniej grupy urządzeń.</span><span class="sxs-lookup"><span data-stu-id="c9449-137">Associate the policy with the appropriate group of devices.</span></span>

   ![Zasady usługi Intune](./media/log-analytics-surface-hubs/intune.png)

<span data-ttu-id="c9449-139">Następnie usługa Intune przeprowadza synchronizację ustawień OMS z urządzeniami w grupie docelowej zarejestrowanie ich w obszarze roboczym pakietu OMS.</span><span class="sxs-lookup"><span data-stu-id="c9449-139">Intune then syncs the OMS settings with the devices in the target group, enrolling them in your OMS workspace.</span></span>

## <a name="connect-surface-hubs-to-oms-using-the-settings-app"></a><span data-ttu-id="c9449-140">Nawiązać urządzeń Surface Hub OMS przy użyciu ustawień aplikacji</span><span class="sxs-lookup"><span data-stu-id="c9449-140">Connect Surface Hubs to OMS using the Settings app</span></span>
<span data-ttu-id="c9449-141">Wymagany identyfikator i klucz obszaru roboczego dla obszaru roboczego OMS, która ma zarządzać z urządzeń Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="c9449-141">You'll need the workspace ID and workspace key for the OMS workspace that will manage your Surface Hubs.</span></span> <span data-ttu-id="c9449-142">Możesz pobrać z portalu OMS.</span><span class="sxs-lookup"><span data-stu-id="c9449-142">You can get those from the OMS portal.</span></span>

<span data-ttu-id="c9449-143">Jeśli nie używasz usługi Intune do zarządzania używanym środowiskiem, można zarejestrować ręcznie za pomocą urządzenia **ustawienia** na każdym Surface Hub:</span><span class="sxs-lookup"><span data-stu-id="c9449-143">If you don't use Intune to manage your environment, you can enroll devices manually through **Settings** on each Surface Hub:</span></span>

1. <span data-ttu-id="c9449-144">Z Centrum powierzchni, otwórz **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="c9449-144">From your Surface Hub, open **Settings**.</span></span>
2. <span data-ttu-id="c9449-145">Wprowadź poświadczenia administratora urządzenia, po wyświetleniu monitu.</span><span class="sxs-lookup"><span data-stu-id="c9449-145">Enter the device admin credentials when prompted.</span></span>
3. <span data-ttu-id="c9449-146">Kliknij przycisk **to urządzenie**i w obszarze **monitorowanie**, kliknij przycisk **Konfigurowanie ustawień OMS**.</span><span class="sxs-lookup"><span data-stu-id="c9449-146">Click **This device**, and the under **Monitoring**, click **Configure OMS Settings**.</span></span>
4. <span data-ttu-id="c9449-147">Wybierz **Włącz monitorowanie**.</span><span class="sxs-lookup"><span data-stu-id="c9449-147">Select **Enable monitoring**.</span></span>
5. <span data-ttu-id="c9449-148">W oknie dialogowym Ustawienia OMS wpisz **identyfikator obszaru roboczego** i wpisz **klucz obszaru roboczego**.</span><span class="sxs-lookup"><span data-stu-id="c9449-148">In the OMS settings dialog, type the **Workspace ID** and type the **Workspace Key**.</span></span>  
   <span data-ttu-id="c9449-149">![Ustawienia](./media/log-analytics-surface-hubs/settings.png)</span><span class="sxs-lookup"><span data-stu-id="c9449-149">![settings](./media/log-analytics-surface-hubs/settings.png)</span></span>
6. <span data-ttu-id="c9449-150">Kliknij przycisk **OK** w celu ukończenia konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="c9449-150">Click **OK** to complete the configuration.</span></span>

<span data-ttu-id="c9449-151">Pojawia się potwierdzenie informujący o tym, czy konfiguracja OMS została pomyślnie zastosowana do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="c9449-151">A confirmation appears telling you whether or not the OMS configuration was successfully applied to the device.</span></span> <span data-ttu-id="c9449-152">Jeśli tak jest, pojawi się komunikat z informacją, że agent pomyślnie nawiązano połączenie z usługą OMS.</span><span class="sxs-lookup"><span data-stu-id="c9449-152">If it was, a message appears stating that the agent successfully connected to the OMS service.</span></span> <span data-ttu-id="c9449-153">Urządzenie następnie rozpoczyna wysyłanie danych do OMS, gdzie można przeglądać i działa na nim.</span><span class="sxs-lookup"><span data-stu-id="c9449-153">The device then starts sending data to OMS where you can view and act on it.</span></span>

## <a name="monitor-surface-hubs"></a><span data-ttu-id="c9449-154">Monitor urządzenia Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="c9449-154">Monitor Surface Hubs</span></span>
<span data-ttu-id="c9449-155">Monitorowanie sieci urządzeń Surface Hub przy użyciu pakietu OMS jest znacznie takich jak monitorowanie innych zarejestrowanych urządzeń.</span><span class="sxs-lookup"><span data-stu-id="c9449-155">Monitoring your Surface Hubs using OMS is much like monitoring any other enrolled devices.</span></span>

1. <span data-ttu-id="c9449-156">Zaloguj się do portalu OMS.</span><span class="sxs-lookup"><span data-stu-id="c9449-156">Sign in to the OMS portal.</span></span>
2. <span data-ttu-id="c9449-157">Przejdź do pulpitu nawigacyjnego pakietu rozwiązania Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="c9449-157">Navigate to the Surface Hub solution pack dashboard.</span></span>
3. <span data-ttu-id="c9449-158">Kondycja urządzenia jest wyświetlana.</span><span class="sxs-lookup"><span data-stu-id="c9449-158">Your device's health is displayed.</span></span>

   ![Surface Hub pulpitu nawigacyjnego](./media/log-analytics-surface-hubs/surface-hub-dashboard.png)

<span data-ttu-id="c9449-160">Można utworzyć [alerty](log-analytics-alerts.md) oparte na istniejących lub niestandardowych dziennik wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="c9449-160">You can create [alerts](log-analytics-alerts.md) based on existing or custom log searches.</span></span> <span data-ttu-id="c9449-161">Przy użyciu dane OMS zbiera dane z Twojego urządzeń Surface Hub, możesz wyszukać problemy i alert na warunki, które definiują urządzeń.</span><span class="sxs-lookup"><span data-stu-id="c9449-161">Using the data the OMS collects from your Surface Hubs, you can search for issues and alert on the conditions that you define for your devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c9449-162">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c9449-162">Next steps</span></span>
* <span data-ttu-id="c9449-163">Użyj [Zaloguj wyszukiwania analizy dzienników](log-analytics-log-searches.md) Aby wyświetlić szczegółowe dane Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="c9449-163">Use [Log searches in Log Analytics](log-analytics-log-searches.md) to view detailed Surface Hub data.</span></span>
* <span data-ttu-id="c9449-164">Utwórz [alerty](log-analytics-alerts.md) do powiadamiania, gdy występują problemy z Twojej urządzeń Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="c9449-164">Create [alerts](log-analytics-alerts.md) to notify you when issues occur with your Surface Hubs.</span></span>
