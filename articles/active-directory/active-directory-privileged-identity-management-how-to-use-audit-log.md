---
title: "Jak korzystać z dziennika inspekcji w usłudze Azure AD Privileged Identity Management | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak korzystać z dziennika inspekcji w rozszerzeniu usługi Azure Privileged Identity Management."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 5d13a6dd-1fcb-4e76-82fb-cb2f4f0e4357
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 7d9a5255a64d46c1388d328a606b3f297d61262b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-audit-log-in-pim"></a><span data-ttu-id="06533-103">Korzystanie z dziennika inspekcji w PIM</span><span class="sxs-lookup"><span data-stu-id="06533-103">Using the audit log in PIM</span></span>
<span data-ttu-id="06533-104">Dziennik inspekcji zarządzania tożsamości uprzywilejowanych (PIM) umożliwia zobaczyć wszystkie przypisania użytkowników i aktywacji w danym okresie.</span><span class="sxs-lookup"><span data-stu-id="06533-104">You can use the Privileged Identity Management (PIM) audit log to see all the user assignments and activations within a given time period.</span></span> <span data-ttu-id="06533-105">Jeśli chcesz wyświetlić historię inspekcji pełnego działania w dzierżawie, w tym administratora, użytkownika i działania synchronizacji, można użyć [raportów dotyczących dostępu i użycia usługi Azure Active Directory.](active-directory-view-access-usage-reports.md)</span><span class="sxs-lookup"><span data-stu-id="06533-105">If you want to see the full audit history of activity in your tenant, including administrator, end user, and synchronization activity, you can use the [Azure Active Directory access and usage reports.](active-directory-view-access-usage-reports.md)</span></span>

## <a name="navigate-to-the-audit-log"></a><span data-ttu-id="06533-106">Przejdź do dziennika inspekcji</span><span class="sxs-lookup"><span data-stu-id="06533-106">Navigate to the audit log</span></span>
<span data-ttu-id="06533-107">Z [portalu Azure](https://portal.azure.com) pulpitu nawigacyjnego, wybierz opcję **Azure AD Privileged Identity Management** aplikacji.</span><span class="sxs-lookup"><span data-stu-id="06533-107">From the [Azure portal](https://portal.azure.com) dashboard, select the **Azure AD Privileged Identity Management** app.</span></span> <span data-ttu-id="06533-108">Z tego miejsca, dostępu do dziennika inspekcji, klikając **Zarządzanie ról uprzywilejowanych** > **Historia inspekcji** na pulpicie nawigacyjnym usługi PIM.</span><span class="sxs-lookup"><span data-stu-id="06533-108">From there, access the audit log by clicking **Manage privileged roles** > **Audit history** in the PIM dashboard.</span></span>

## <a name="the-audit-log-graph"></a><span data-ttu-id="06533-109">Wykres dziennika inspekcji</span><span class="sxs-lookup"><span data-stu-id="06533-109">The audit log graph</span></span>
<span data-ttu-id="06533-110">Dziennik inspekcji służy do wyświetlania łączna liczba aktywacji, max aktywacji dziennie i średnia aktywacji dziennie w wykres liniowy.</span><span class="sxs-lookup"><span data-stu-id="06533-110">You can use the audit log to view the total activations, max activations per day, and average activations per day in a line graph.</span></span>  <span data-ttu-id="06533-111">Można również filtrować dane według roli, jeśli istnieje więcej niż jednej roli w Historia inspekcji.</span><span class="sxs-lookup"><span data-stu-id="06533-111">You can also filter the data by role if there is more than one role in the audit history.</span></span>

<span data-ttu-id="06533-112">Użyj **czasu**, **akcji**, i **roli** przycisków, aby posortować dziennika.</span><span class="sxs-lookup"><span data-stu-id="06533-112">Use the **time**, **action**, and **role** buttons to sort the log.</span></span>

## <a name="the-audit-log-list"></a><span data-ttu-id="06533-113">Lista dziennika inspekcji</span><span class="sxs-lookup"><span data-stu-id="06533-113">The audit log list</span></span>
<span data-ttu-id="06533-114">Kolumny na liście dziennika inspekcji są:</span><span class="sxs-lookup"><span data-stu-id="06533-114">The columns in the audit log list are:</span></span>

* <span data-ttu-id="06533-115">**Obiekt żądający** — użytkownik, który jest wymagane uaktywnienie roli lub zmiany.</span><span class="sxs-lookup"><span data-stu-id="06533-115">**Requestor** - the user who requested the role activation or change.</span></span>  <span data-ttu-id="06533-116">Jeśli wartość to "Azure System", sprawdź dziennik inspekcji Azure, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="06533-116">If the value is "Azure System", check the Azure audit log for more information.</span></span>
* <span data-ttu-id="06533-117">**Użytkownik** — użytkownik, który jest aktywowanie lub są przypisane do roli.</span><span class="sxs-lookup"><span data-stu-id="06533-117">**User** - the user who is activating or assigned to a role.</span></span>
* <span data-ttu-id="06533-118">**Rola** -przypisane do roli, lub aktywowany przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="06533-118">**Role** - the role assigned or activated by the user.</span></span>
* <span data-ttu-id="06533-119">**Akcja** — akcje wykonywane przez obiekt żądający.</span><span class="sxs-lookup"><span data-stu-id="06533-119">**Action** - the actions taken by the requestor.</span></span> <span data-ttu-id="06533-120">Może to obejmować przypisania, anulowaniu, aktywacji lub dezaktywacji.</span><span class="sxs-lookup"><span data-stu-id="06533-120">This can include assignment, unassignment, activation, or deactivation.</span></span>
* <span data-ttu-id="06533-121">**Czas** — gdy akcja wystąpił.</span><span class="sxs-lookup"><span data-stu-id="06533-121">**Time** - when the action occurred.</span></span>
* <span data-ttu-id="06533-122">**Uzasadnienie** — Jeśli dowolny tekst został wprowadzony w polu Przyczyna podczas aktywacji, pojawi się tutaj.</span><span class="sxs-lookup"><span data-stu-id="06533-122">**Reasoning** - if any text was entered into the reason field during activation, it will show up here.</span></span>
* <span data-ttu-id="06533-123">**Wygaśnięcie** — tylko istotne dla aktywacji ról.</span><span class="sxs-lookup"><span data-stu-id="06533-123">**Expiration** - only relevant for activation of roles.</span></span>

## <a name="filter-the-audit-log"></a><span data-ttu-id="06533-124">Filtrowanie dziennika inspekcji</span><span class="sxs-lookup"><span data-stu-id="06533-124">Filter the audit log</span></span>
<span data-ttu-id="06533-125">Można filtrować dane zostaną wyświetlone w dzienniku inspekcji, klikając **filtru** przycisku.</span><span class="sxs-lookup"><span data-stu-id="06533-125">You can filter the information that shows up in the audit log by clicking the **Filter** button.</span></span>  <span data-ttu-id="06533-126">**Bloku parametry wykresu aktualizacji** będą wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="06533-126">The **Update chart parameters blade** will appear.</span></span>

<span data-ttu-id="06533-127">Po ustawieniu filtrów, kliknij przycisk **aktualizacji** do filtrowania danych w dzienniku.</span><span class="sxs-lookup"><span data-stu-id="06533-127">After you set the filters, click **Update** to filter the data in the log.</span></span>  <span data-ttu-id="06533-128">Jeśli dane nie są wyświetlane od razu, Odśwież stronę.</span><span class="sxs-lookup"><span data-stu-id="06533-128">If the data doesn't appear right away, refresh the page.</span></span>

### <a name="change-the-date-range"></a><span data-ttu-id="06533-129">Zmień zakres dat</span><span class="sxs-lookup"><span data-stu-id="06533-129">Change the date range</span></span>
<span data-ttu-id="06533-130">Użyj **dzisiaj**, **zeszłym tygodniu**, **ostatnim miesiącu**, lub **niestandardowy** przycisk, aby zmienić zakres czasu dziennika inspekcji.</span><span class="sxs-lookup"><span data-stu-id="06533-130">Use the **Today**, **Past Week**, **Past Month**, or **Custom** buttons to change the time range of the audit log.</span></span>

<span data-ttu-id="06533-131">Po wybraniu **niestandardowy** przycisku, będziesz mieć możliwość **z** Data i **do** pole daty, aby określić zakres dat dla dziennika.</span><span class="sxs-lookup"><span data-stu-id="06533-131">When you choose the **Custom** button, you will be given a **From** date field and a **To** date field to specify a range of dates for the log.</span></span>  <span data-ttu-id="06533-132">Możesz wprowadzić daty w formacie MM/DD/RRRR lub kliknięcie **kalendarza** ikonę i wybierz datę z kalendarza.</span><span class="sxs-lookup"><span data-stu-id="06533-132">You can either enter the dates in MM/DD/YYYY format or click on the **calendar** icon and choose the date from a calendar.</span></span>

### <a name="change-the-roles-included-in-the-log"></a><span data-ttu-id="06533-133">Zmień role uwzględnione w Dzienniku</span><span class="sxs-lookup"><span data-stu-id="06533-133">Change the roles included in the log</span></span>
<span data-ttu-id="06533-134">Zaznaczenie lub usunięcie zaznaczenia **roli** pole wyboru obok każdej roli, aby dołączyć lub wykluczyć go z dziennika.</span><span class="sxs-lookup"><span data-stu-id="06533-134">Check or uncheck the **Role** checkbox next to each role to include or exclude it from the log.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="06533-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="06533-135">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

