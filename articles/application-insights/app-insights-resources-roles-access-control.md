---
title: "aaaResources, ról i kontroli dostępu w usłudze Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Właściciele, współautorzy i czytelnicy wgląd w organizacji."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 49f736a5-67fe-4cc6-b1ef-51b993fb39bd
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: bwren
ms.openlocfilehash: a6f6ca0443b5f60239f094606e124f856967d8ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="resources-roles-and-access-control-in-application-insights"></a><span data-ttu-id="611f5-103">Zasoby, ról i kontroli dostępu w usłudze Application Insights</span><span class="sxs-lookup"><span data-stu-id="611f5-103">Resources, roles, and access control in Application Insights</span></span>
<span data-ttu-id="611f5-104">Można kontrolować, kto ma odczytywanie i aktualizowanie danych tooyour dostępu na platformie Azure [usługi Application Insights][start], za pomocą [kontroli dostępu opartej na rolach w systemie Microsoft Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="611f5-104">You can control who has read and update access tooyour data in Azure [Application Insights][start], by using [Role-based access control in Microsoft Azure](../active-directory/role-based-access-control-configure.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="611f5-105">Przypisywanie dostępu toousers w hello **grupy zasobów lub subskrypcji** toowhich zasobu aplikacji należy - nie w zasobie hello, sama.</span><span class="sxs-lookup"><span data-stu-id="611f5-105">Assign access toousers in hello **resource group or subscription** toowhich your application resource belongs - not in hello resource itself.</span></span> <span data-ttu-id="611f5-106">Przypisz hello **współautora składników usługi Application Insights** roli.</span><span class="sxs-lookup"><span data-stu-id="611f5-106">Assign hello **Application Insights component contributor** role.</span></span> <span data-ttu-id="611f5-107">Dzięki temu uniform kontroli dostępu tooweb testy i alerty wraz z zasobu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="611f5-107">This ensures uniform control of access tooweb tests and alerts along with your application resource.</span></span> <span data-ttu-id="611f5-108">[Dowiedz się więcej](#access).</span><span class="sxs-lookup"><span data-stu-id="611f5-108">[Learn more](#access).</span></span>
> 
> 

## <a name="resources-groups-and-subscriptions"></a><span data-ttu-id="611f5-109">Zasoby, grup i subskrypcji</span><span class="sxs-lookup"><span data-stu-id="611f5-109">Resources, groups and subscriptions</span></span>
<span data-ttu-id="611f5-110">Pierwszy, definicje:</span><span class="sxs-lookup"><span data-stu-id="611f5-110">First, some definitions:</span></span>

* <span data-ttu-id="611f5-111">**Zasób** — wystąpienie usługi Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="611f5-111">**Resource** - An instance of a Microsoft Azure service.</span></span> <span data-ttu-id="611f5-112">Zasób usługi Application Insights gromadzi, analizuje i wyświetla hello danych telemetrycznych wysłanych z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="611f5-112">Your Application Insights resource collects, analyzes and displays hello telemetry data sent from your application.</span></span>  <span data-ttu-id="611f5-113">Inne typy zasobów platformy Azure obejmują aplikacje sieci web, bazy danych i maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="611f5-113">Other types of Azure resources include web apps, databases, and VMs.</span></span>
  
    <span data-ttu-id="611f5-114">Otwórz zasobów toosee hello [Azure Portal][portal], zaloguj się i kliknij pozycję wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="611f5-114">toosee your resources, open hello [Azure Portal][portal], sign in, and click All Resources.</span></span> <span data-ttu-id="611f5-115">toofind zasób typu część nazwy w polu filtru hello.</span><span class="sxs-lookup"><span data-stu-id="611f5-115">toofind a resource, type part of its name in hello filter field.</span></span>
  
    ![Lista zasobów platformy Azure](./media/app-insights-resources-roles-access-control/10-browse.png)

<a name="resource-group"></a>

* <span data-ttu-id="611f5-117">[**Grupa zasobów** ] [ group] -tooone grupy należy co zasób.</span><span class="sxs-lookup"><span data-stu-id="611f5-117">[**Resource group**][group] - Every resource belongs tooone group.</span></span> <span data-ttu-id="611f5-118">Grupa to wygodny sposób toomanage powiązanych zasobów, szczególnie w przypadku kontroli dostępu.</span><span class="sxs-lookup"><span data-stu-id="611f5-118">A group is a convenient way toomanage related resources, particularly for access control.</span></span> <span data-ttu-id="611f5-119">Na przykład do jednego zasobu grupy można umieścić w aplikacji sieci Web, aplikacji hello toomonitor zasobu usługi Application Insights i tookeep zasobów magazynu wyeksportowane dane.</span><span class="sxs-lookup"><span data-stu-id="611f5-119">For example, into one resource group you could put a Web App, an Application Insights resource toomonitor hello app, and a Storage resource tookeep exported data.</span></span>

    ![Kliknij przycisk Przeglądaj, grupy zasobów, a następnie wybierz grupę](./media/app-insights-resources-roles-access-control/11-group.png)

* <span data-ttu-id="611f5-121">[**Subskrypcja** ](https://manage.windowsazure.com) -toouse Application Insights lub innych zasobów platformy Azure, możesz zarejestrować się w tooan subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="611f5-121">[**Subscription**](https://manage.windowsazure.com) - toouse Application Insights or other Azure resources, you sign in tooan Azure subscription.</span></span> <span data-ttu-id="611f5-122">Każda grupa zasobów należy tooone subskrypcji platformy Azure, które wybierz pakiet ceny i, jeśli jest subskrypcji organizacji wybrać hello członków i uprawnień dostępu.</span><span class="sxs-lookup"><span data-stu-id="611f5-122">Every resource group belongs tooone Azure subscription, where you choose your price package and, if it's an organization subscription, choose hello members and their access permissions.</span></span>
* <span data-ttu-id="611f5-123">[**Konto Microsoft** ] [ account] — Witaj nazwy użytkownika i hasła, użyj toosign w tooMicrosoft Azure subskrypcji, XBox Live, Outlook.com i innych usług firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="611f5-123">[**Microsoft account**][account] - hello username and password that you use toosign in tooMicrosoft Azure subscriptions, XBox Live, Outlook.com, and other Microsoft services.</span></span>

## <span data-ttu-id="611f5-124"><a name="access"></a>Kontroli dostępu w grupie zasobów hello</span><span class="sxs-lookup"><span data-stu-id="611f5-124"><a name="access"></a> Control access in hello resource group</span></span>
<span data-ttu-id="611f5-125">Jest ważne toounderstand w zasobie toohello dodanie utworzone dla aplikacji, czy też oddzielić zasoby ukryte alerty i analiz sieci web.</span><span class="sxs-lookup"><span data-stu-id="611f5-125">It's important toounderstand that in addition toohello resource you created for your application, there are also separate hidden resources for alerts and web tests.</span></span> <span data-ttu-id="611f5-126">Są one dołączone toohello tego samego [grupy zasobów](#resource-group) jako aplikacji.</span><span class="sxs-lookup"><span data-stu-id="611f5-126">They are attached toohello same [resource group](#resource-group) as your application.</span></span> <span data-ttu-id="611f5-127">Może również umieszczono innymi usługami Azure w nim, takich jak magazyny lub witryn sieci Web.</span><span class="sxs-lookup"><span data-stu-id="611f5-127">You might also have put other Azure services in there, such as websites or storage.</span></span>

![Zasoby w usłudze Application Insights](./media/app-insights-resources-roles-access-control/00-resources.png)

<span data-ttu-id="611f5-129">toocontrol dostęp do toothese zasobów, dlatego zalecane jest aby:</span><span class="sxs-lookup"><span data-stu-id="611f5-129">toocontrol access toothese resources it's therefore recommended to:</span></span>

* <span data-ttu-id="611f5-130">Kontrola dostępu na powitania **grupy zasobów lub subskrypcji** poziom.</span><span class="sxs-lookup"><span data-stu-id="611f5-130">Control access at hello **resource group or subscription** level.</span></span>
* <span data-ttu-id="611f5-131">Przypisz hello **współautora Application Insights składnika** toousers roli.</span><span class="sxs-lookup"><span data-stu-id="611f5-131">Assign hello **Application Insights Component contributor** role toousers.</span></span> <span data-ttu-id="611f5-132">Umożliwia im testy sieci web tooedit, alerty i zasobów usługi Application Insights, bez konieczności podawania tooany dostępu do innych usług w grupie hello.</span><span class="sxs-lookup"><span data-stu-id="611f5-132">This allows them tooedit web tests, alerts, and Application Insights resources, without providing access tooany other services in hello group.</span></span>

## <a name="tooprovide-access-tooanother-user"></a><span data-ttu-id="611f5-133">tooprovide dostęp tooanother użytkownika</span><span class="sxs-lookup"><span data-stu-id="611f5-133">tooprovide access tooanother user</span></span>
<span data-ttu-id="611f5-134">Musisz mieć subskrypcję toohello praw właściciela lub grupy zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="611f5-134">You must have Owner rights toohello subscription or hello resource group.</span></span>

<span data-ttu-id="611f5-135">Witaj, użytkownik musi mieć [Account Microsoft][account], ani uzyskiwać dostępu do tootheir [Account Microsoft organizacji](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="611f5-135">hello user must have a [Microsoft Account][account], or access tootheir [organizational Microsoft Account](../active-directory/sign-up-organization.md).</span></span> <span data-ttu-id="611f5-136">Możesz podać tooindividuals dostępu, a także toouser grup zdefiniowanych w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="611f5-136">You can provide access tooindividuals, and also toouser groups defined in Azure Active Directory.</span></span>

#### <a name="navigate-toohello-resource-group"></a><span data-ttu-id="611f5-137">Przejdź toohello grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="611f5-137">Navigate toohello resource group</span></span>
<span data-ttu-id="611f5-138">Dodaj użytkownika hello istnieje.</span><span class="sxs-lookup"><span data-stu-id="611f5-138">Add hello user there.</span></span>

![W bloku zasobów aplikacji otwórz Essentials, otwórz hello grupy zasobów, a wybierz ustawienia/użytkowników.](./media/app-insights-resources-roles-access-control/01-add-user.png)

<span data-ttu-id="611f5-141">Lub może do góry innego poziomu i dodać toohello użytkownika hello subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="611f5-141">Or you could go up another level and add hello user toohello Subscription.</span></span>

#### <a name="select-a-role"></a><span data-ttu-id="611f5-142">Wybierz rolę</span><span class="sxs-lookup"><span data-stu-id="611f5-142">Select a role</span></span>
![Wybierz rolę do hello nowego użytkownika.](./media/app-insights-resources-roles-access-control/03-role.png)

| <span data-ttu-id="611f5-144">Rola</span><span class="sxs-lookup"><span data-stu-id="611f5-144">Role</span></span> | <span data-ttu-id="611f5-145">W grupie zasobów hello</span><span class="sxs-lookup"><span data-stu-id="611f5-145">In hello resource group</span></span> |
| --- | --- |
| <span data-ttu-id="611f5-146">Właściciel</span><span class="sxs-lookup"><span data-stu-id="611f5-146">Owner</span></span> |<span data-ttu-id="611f5-147">Można zmienić wszystko, w tym dostępu użytkownika</span><span class="sxs-lookup"><span data-stu-id="611f5-147">Can change anything, including user access</span></span> |
| <span data-ttu-id="611f5-148">Współautor</span><span class="sxs-lookup"><span data-stu-id="611f5-148">Contributor</span></span> |<span data-ttu-id="611f5-149">Można edytować wszystko, w tym wszystkie zasoby</span><span class="sxs-lookup"><span data-stu-id="611f5-149">Can edit anything, including all resources</span></span> |
| <span data-ttu-id="611f5-150">Współautor Insights składnika aplikacji</span><span class="sxs-lookup"><span data-stu-id="611f5-150">Application Insights Component contributor</span></span> |<span data-ttu-id="611f5-151">Można edytować zasobów usługi Application Insights, testy sieci web i alerty</span><span class="sxs-lookup"><span data-stu-id="611f5-151">Can edit Application Insights resources, web tests and alerts</span></span> |
| <span data-ttu-id="611f5-152">Czytelnik</span><span class="sxs-lookup"><span data-stu-id="611f5-152">Reader</span></span> |<span data-ttu-id="611f5-153">Można wyświetlać, ale nie zmienia sytuacji</span><span class="sxs-lookup"><span data-stu-id="611f5-153">Can view but not change anything</span></span> |

<span data-ttu-id="611f5-154">"Edycja" obejmuje tworzenie, usuwanie i aktualizowanie:</span><span class="sxs-lookup"><span data-stu-id="611f5-154">'Editing' includes creating, deleting and updating:</span></span>

* <span data-ttu-id="611f5-155">Zasoby</span><span class="sxs-lookup"><span data-stu-id="611f5-155">Resources</span></span>
* <span data-ttu-id="611f5-156">Testy sieci Web</span><span class="sxs-lookup"><span data-stu-id="611f5-156">Web tests</span></span>
* <span data-ttu-id="611f5-157">Alerty</span><span class="sxs-lookup"><span data-stu-id="611f5-157">Alerts</span></span>
* <span data-ttu-id="611f5-158">Eksport ciągły</span><span class="sxs-lookup"><span data-stu-id="611f5-158">Continuous export</span></span>

#### <a name="select-hello-user"></a><span data-ttu-id="611f5-159">Wybierz użytkownika hello</span><span class="sxs-lookup"><span data-stu-id="611f5-159">Select hello user</span></span>

<span data-ttu-id="611f5-160">Jeśli hello użytkownika, które mają nie znajduje się w katalogu hello, możesz poprosić każda osoba z kontem Microsoft.</span><span class="sxs-lookup"><span data-stu-id="611f5-160">If hello user you want isn't in hello directory, you can invite anyone with a Microsoft account.</span></span>
<span data-ttu-id="611f5-161">(Jeśli korzystają z usług takich jak Outlook.com, OneDrive, Windows Phone lub XBox Live, mają konta Microsoft.)</span><span class="sxs-lookup"><span data-stu-id="611f5-161">(If they use services like Outlook.com, OneDrive, Windows Phone, or XBox Live, they have a Microsoft account.)</span></span>

## <a name="related-content"></a><span data-ttu-id="611f5-162">Zawartość pokrewna</span><span class="sxs-lookup"><span data-stu-id="611f5-162">Related content</span></span>

* [<span data-ttu-id="611f5-163">Oparta na rolach kontrola dostępu na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="611f5-163">Role based access control in Azure</span></span>](../active-directory/role-based-access-control-configure.md)

<!--Link references-->

[account]: https://account.microsoft.com
[group]: ../azure-resource-manager/resource-group-overview.md
[portal]: https://portal.azure.com/
[start]: app-insights-overview.md
