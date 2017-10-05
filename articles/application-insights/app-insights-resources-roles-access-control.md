---
title: "Kontrolę zasobów, ról i dostępu w usłudze Azure Application Insights | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: c979a8bfbeecacc7c0bbc112e02a4b68e874c219
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="resources-roles-and-access-control-in-application-insights"></a><span data-ttu-id="94abb-103">Zasoby, ról i kontroli dostępu w usłudze Application Insights</span><span class="sxs-lookup"><span data-stu-id="94abb-103">Resources, roles, and access control in Application Insights</span></span>
<span data-ttu-id="94abb-104">Można kontrolować, kto ma odczytywanie i aktualizowanie dostępu do danych na platformie Azure [usługi Application Insights][start], za pomocą [kontroli dostępu opartej na rolach w systemie Microsoft Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="94abb-104">You can control who has read and update access to your data in Azure [Application Insights][start], by using [Role-based access control in Microsoft Azure](../active-directory/role-based-access-control-configure.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94abb-105">Przypisywanie dostępu dla użytkowników w **grupy zasobów lub subskrypcji** do której należy zasób aplikacji — nie w zasobie samej siebie.</span><span class="sxs-lookup"><span data-stu-id="94abb-105">Assign access to users in the **resource group or subscription** to which your application resource belongs - not in the resource itself.</span></span> <span data-ttu-id="94abb-106">Przypisz **współautora składników usługi Application Insights** roli.</span><span class="sxs-lookup"><span data-stu-id="94abb-106">Assign the **Application Insights component contributor** role.</span></span> <span data-ttu-id="94abb-107">Dzięki temu uniform kontroli dostępu do testów sieci web i alerty wraz z zasobu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="94abb-107">This ensures uniform control of access to web tests and alerts along with your application resource.</span></span> <span data-ttu-id="94abb-108">[Dowiedz się więcej](#access).</span><span class="sxs-lookup"><span data-stu-id="94abb-108">[Learn more](#access).</span></span>
> 
> 

## <a name="resources-groups-and-subscriptions"></a><span data-ttu-id="94abb-109">Zasoby, grup i subskrypcji</span><span class="sxs-lookup"><span data-stu-id="94abb-109">Resources, groups and subscriptions</span></span>
<span data-ttu-id="94abb-110">Pierwszy, definicje:</span><span class="sxs-lookup"><span data-stu-id="94abb-110">First, some definitions:</span></span>

* <span data-ttu-id="94abb-111">**Zasób** — wystąpienie usługi Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="94abb-111">**Resource** - An instance of a Microsoft Azure service.</span></span> <span data-ttu-id="94abb-112">Zasób usługi Application Insights gromadzi, analizuje i wyświetla danych telemetrycznych wysłanych z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="94abb-112">Your Application Insights resource collects, analyzes and displays the telemetry data sent from your application.</span></span>  <span data-ttu-id="94abb-113">Inne typy zasobów platformy Azure obejmują aplikacje sieci web, bazy danych i maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="94abb-113">Other types of Azure resources include web apps, databases, and VMs.</span></span>
  
    <span data-ttu-id="94abb-114">Aby wyświetlić zasoby, otwórz [Azure Portal][portal], zaloguj się i kliknij pozycję wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="94abb-114">To see your resources, open the [Azure Portal][portal], sign in, and click All Resources.</span></span> <span data-ttu-id="94abb-115">Aby znaleźć zasobu, wpisz część nazwy w polu filtru.</span><span class="sxs-lookup"><span data-stu-id="94abb-115">To find a resource, type part of its name in the filter field.</span></span>
  
    ![Lista zasobów platformy Azure](./media/app-insights-resources-roles-access-control/10-browse.png)

<a name="resource-group"></a>

* <span data-ttu-id="94abb-117">[**Grupa zasobów** ] [ group] — każdy zasób należy do jednej grupy.</span><span class="sxs-lookup"><span data-stu-id="94abb-117">[**Resource group**][group] - Every resource belongs to one group.</span></span> <span data-ttu-id="94abb-118">Grupa jest wygodnym sposobem zarządzania powiązane zasoby, szczególnie dla kontroli dostępu.</span><span class="sxs-lookup"><span data-stu-id="94abb-118">A group is a convenient way to manage related resources, particularly for access control.</span></span> <span data-ttu-id="94abb-119">Na przykład w jednej grupy zasobów można umieścić w aplikacji sieci Web, zasobu usługi Application Insights do monitorowania aplikacji i zasobów magazynu, należy wyeksportowane dane.</span><span class="sxs-lookup"><span data-stu-id="94abb-119">For example, into one resource group you could put a Web App, an Application Insights resource to monitor the app, and a Storage resource to keep exported data.</span></span>

    ![Kliknij przycisk Przeglądaj, grupy zasobów, a następnie wybierz grupę](./media/app-insights-resources-roles-access-control/11-group.png)

* <span data-ttu-id="94abb-121">[**Subskrypcja** ](https://manage.windowsazure.com) — Aby używać usługi Application Insights lub innych zasobów platformy Azure, zaloguj się do subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="94abb-121">[**Subscription**](https://manage.windowsazure.com) - To use Application Insights or other Azure resources, you sign in to an Azure subscription.</span></span> <span data-ttu-id="94abb-122">Każda grupa zasobów należy do jednej subskrypcji platformy Azure, które wybierz pakiet ceny i, jeśli jest subskrypcji organizacji wybrać członków i uprawnień dostępu.</span><span class="sxs-lookup"><span data-stu-id="94abb-122">Every resource group belongs to one Azure subscription, where you choose your price package and, if it's an organization subscription, choose the members and their access permissions.</span></span>
* <span data-ttu-id="94abb-123">[**Konto Microsoft** ] [ account] — nazwa użytkownika i hasło, którego używasz do logowania się na Microsoft Azure subskrypcji, XBox Live, Outlook.com i innych usług firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="94abb-123">[**Microsoft account**][account] - The username and password that you use to sign in to Microsoft Azure subscriptions, XBox Live, Outlook.com, and other Microsoft services.</span></span>

## <span data-ttu-id="94abb-124"><a name="access"></a>Kontroli dostępu w grupie zasobów</span><span class="sxs-lookup"><span data-stu-id="94abb-124"><a name="access"></a> Control access in the resource group</span></span>
<span data-ttu-id="94abb-125">Należy zrozumieć, oprócz zasobów utworzonej dla aplikacji, czy też oddzielne zasoby ukryte alertów i testy sieci web.</span><span class="sxs-lookup"><span data-stu-id="94abb-125">It's important to understand that in addition to the resource you created for your application, there are also separate hidden resources for alerts and web tests.</span></span> <span data-ttu-id="94abb-126">Są one dołączone do tej samej [grupy zasobów](#resource-group) jako aplikacji.</span><span class="sxs-lookup"><span data-stu-id="94abb-126">They are attached to the same [resource group](#resource-group) as your application.</span></span> <span data-ttu-id="94abb-127">Może również umieszczono innymi usługami Azure w nim, takich jak magazyny lub witryn sieci Web.</span><span class="sxs-lookup"><span data-stu-id="94abb-127">You might also have put other Azure services in there, such as websites or storage.</span></span>

![Zasoby w usłudze Application Insights](./media/app-insights-resources-roles-access-control/00-resources.png)

<span data-ttu-id="94abb-129">Aby kontrolować dostęp do tych zasobów w związku z tym zaleca się:</span><span class="sxs-lookup"><span data-stu-id="94abb-129">To control access to these resources it's therefore recommended to:</span></span>

* <span data-ttu-id="94abb-130">Kontrola dostępu w **grupy zasobów lub subskrypcji** poziom.</span><span class="sxs-lookup"><span data-stu-id="94abb-130">Control access at the **resource group or subscription** level.</span></span>
* <span data-ttu-id="94abb-131">Przypisz **współautora Application Insights składnika** roli do użytkowników.</span><span class="sxs-lookup"><span data-stu-id="94abb-131">Assign the **Application Insights Component contributor** role to users.</span></span> <span data-ttu-id="94abb-132">Umożliwia im to edytować testy sieci web, alerty i zasobów usługi Application Insights, bez konieczności podawania dostępu do innych usług w grupie.</span><span class="sxs-lookup"><span data-stu-id="94abb-132">This allows them to edit web tests, alerts, and Application Insights resources, without providing access to any other services in the group.</span></span>

## <a name="to-provide-access-to-another-user"></a><span data-ttu-id="94abb-133">Aby zapewnić dostęp do innego użytkownika</span><span class="sxs-lookup"><span data-stu-id="94abb-133">To provide access to another user</span></span>
<span data-ttu-id="94abb-134">Musi mieć prawa właściciela subskrypcji lub grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="94abb-134">You must have Owner rights to the subscription or the resource group.</span></span>

<span data-ttu-id="94abb-135">Użytkownik musi mieć [Account Microsoft][account], lub dostęp do ich [Account Microsoft organizacji](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="94abb-135">The user must have a [Microsoft Account][account], or access to their [organizational Microsoft Account](../active-directory/sign-up-organization.md).</span></span> <span data-ttu-id="94abb-136">Można zapewnić dostęp do osób, a także do grup użytkowników zdefiniowanych w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="94abb-136">You can provide access to individuals, and also to user groups defined in Azure Active Directory.</span></span>

#### <a name="navigate-to-the-resource-group"></a><span data-ttu-id="94abb-137">Przejdź do grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="94abb-137">Navigate to the resource group</span></span>
<span data-ttu-id="94abb-138">Dodaj użytkownika istnieje.</span><span class="sxs-lookup"><span data-stu-id="94abb-138">Add the user there.</span></span>

![W bloku zasobów aplikacji otwórz Essentials, otwórz grupę zasobów, a wybierz ustawienia/użytkowników.](./media/app-insights-resources-roles-access-control/01-add-user.png)

<span data-ttu-id="94abb-141">Lub może do góry innego poziomu i dodać użytkownika do subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="94abb-141">Or you could go up another level and add the user to the Subscription.</span></span>

#### <a name="select-a-role"></a><span data-ttu-id="94abb-142">Wybierz rolę</span><span class="sxs-lookup"><span data-stu-id="94abb-142">Select a role</span></span>
![Wybierz rolę dla nowego użytkownika](./media/app-insights-resources-roles-access-control/03-role.png)

| <span data-ttu-id="94abb-144">Rola</span><span class="sxs-lookup"><span data-stu-id="94abb-144">Role</span></span> | <span data-ttu-id="94abb-145">W grupie zasobów</span><span class="sxs-lookup"><span data-stu-id="94abb-145">In the resource group</span></span> |
| --- | --- |
| <span data-ttu-id="94abb-146">Właściciel</span><span class="sxs-lookup"><span data-stu-id="94abb-146">Owner</span></span> |<span data-ttu-id="94abb-147">Można zmienić wszystko, w tym dostępu użytkownika</span><span class="sxs-lookup"><span data-stu-id="94abb-147">Can change anything, including user access</span></span> |
| <span data-ttu-id="94abb-148">Współautor</span><span class="sxs-lookup"><span data-stu-id="94abb-148">Contributor</span></span> |<span data-ttu-id="94abb-149">Można edytować wszystko, w tym wszystkie zasoby</span><span class="sxs-lookup"><span data-stu-id="94abb-149">Can edit anything, including all resources</span></span> |
| <span data-ttu-id="94abb-150">Współautor Insights składnika aplikacji</span><span class="sxs-lookup"><span data-stu-id="94abb-150">Application Insights Component contributor</span></span> |<span data-ttu-id="94abb-151">Można edytować zasobów usługi Application Insights, testy sieci web i alerty</span><span class="sxs-lookup"><span data-stu-id="94abb-151">Can edit Application Insights resources, web tests and alerts</span></span> |
| <span data-ttu-id="94abb-152">Czytelnik</span><span class="sxs-lookup"><span data-stu-id="94abb-152">Reader</span></span> |<span data-ttu-id="94abb-153">Można wyświetlać, ale nie zmienia sytuacji</span><span class="sxs-lookup"><span data-stu-id="94abb-153">Can view but not change anything</span></span> |

<span data-ttu-id="94abb-154">"Edycja" obejmuje tworzenie, usuwanie i aktualizowanie:</span><span class="sxs-lookup"><span data-stu-id="94abb-154">'Editing' includes creating, deleting and updating:</span></span>

* <span data-ttu-id="94abb-155">Zasoby</span><span class="sxs-lookup"><span data-stu-id="94abb-155">Resources</span></span>
* <span data-ttu-id="94abb-156">Testy sieci Web</span><span class="sxs-lookup"><span data-stu-id="94abb-156">Web tests</span></span>
* <span data-ttu-id="94abb-157">Alerty</span><span class="sxs-lookup"><span data-stu-id="94abb-157">Alerts</span></span>
* <span data-ttu-id="94abb-158">Eksport ciągły</span><span class="sxs-lookup"><span data-stu-id="94abb-158">Continuous export</span></span>

#### <a name="select-the-user"></a><span data-ttu-id="94abb-159">Wybierz użytkownika</span><span class="sxs-lookup"><span data-stu-id="94abb-159">Select the user</span></span>

<span data-ttu-id="94abb-160">Jeśli użytkownik, który ma nie znajduje się w katalogu, możesz poprosić każda osoba z kontem Microsoft.</span><span class="sxs-lookup"><span data-stu-id="94abb-160">If the user you want isn't in the directory, you can invite anyone with a Microsoft account.</span></span>
<span data-ttu-id="94abb-161">(Jeśli korzystają z usług takich jak Outlook.com, OneDrive, Windows Phone lub XBox Live, mają konta Microsoft.)</span><span class="sxs-lookup"><span data-stu-id="94abb-161">(If they use services like Outlook.com, OneDrive, Windows Phone, or XBox Live, they have a Microsoft account.)</span></span>

## <a name="related-content"></a><span data-ttu-id="94abb-162">Zawartość pokrewna</span><span class="sxs-lookup"><span data-stu-id="94abb-162">Related content</span></span>

* [<span data-ttu-id="94abb-163">Oparta na rolach kontrola dostępu na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="94abb-163">Role based access control in Azure</span></span>](../active-directory/role-based-access-control-configure.md)

<!--Link references-->

[account]: https://account.microsoft.com
[group]: ../azure-resource-manager/resource-group-overview.md
[portal]: https://portal.azure.com/
[start]: app-insights-overview.md
