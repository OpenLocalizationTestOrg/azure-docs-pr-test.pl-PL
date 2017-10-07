---
title: "Dziennik inspekcji hello toouse aaaHow w usłudze Azure AD Privileged Identity Management | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak dziennika inspekcji hello toouse hello Azure Privileged Identity Management rozszerzenia."
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
ms.openlocfilehash: 36987eaab9fe02c5dd7b4f4705e487299430745d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-audit-log-in-pim"></a><span data-ttu-id="dc31a-103">Za pomocą dziennika inspekcji hello w PIM</span><span class="sxs-lookup"><span data-stu-id="dc31a-103">Using hello audit log in PIM</span></span>
<span data-ttu-id="dc31a-104">Można użyć toosee dziennik inspekcji zarządzania tożsamości uprzywilejowanych (PIM) hello wszystkich przypisań użytkownika hello i aktywacji w danym okresie.</span><span class="sxs-lookup"><span data-stu-id="dc31a-104">You can use hello Privileged Identity Management (PIM) audit log toosee all hello user assignments and activations within a given time period.</span></span> <span data-ttu-id="dc31a-105">Jeśli chcesz toosee hello inspekcji pełnej historii aktywności w dzierżawie, w tym administratora, użytkownika i działania synchronizacji, można użyć hello [raportów dotyczących dostępu i użycia usługi Azure Active Directory.](active-directory-view-access-usage-reports.md)</span><span class="sxs-lookup"><span data-stu-id="dc31a-105">If you want toosee hello full audit history of activity in your tenant, including administrator, end user, and synchronization activity, you can use hello [Azure Active Directory access and usage reports.](active-directory-view-access-usage-reports.md)</span></span>

## <a name="navigate-toohello-audit-log"></a><span data-ttu-id="dc31a-106">Przejdź toohello dziennik inspekcji</span><span class="sxs-lookup"><span data-stu-id="dc31a-106">Navigate toohello audit log</span></span>
<span data-ttu-id="dc31a-107">Z hello [portalu Azure](https://portal.azure.com) pulpitu nawigacyjnego, wybierz hello **Azure AD Privileged Identity Management** aplikacji.</span><span class="sxs-lookup"><span data-stu-id="dc31a-107">From hello [Azure portal](https://portal.azure.com) dashboard, select hello **Azure AD Privileged Identity Management** app.</span></span> <span data-ttu-id="dc31a-108">Z tego miejsca, uzyskać dostęp do dziennika inspekcji hello klikając **Zarządzanie ról uprzywilejowanych** > **Historia inspekcji** hello PIM w pulpicie nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="dc31a-108">From there, access hello audit log by clicking **Manage privileged roles** > **Audit history** in hello PIM dashboard.</span></span>

## <a name="hello-audit-log-graph"></a><span data-ttu-id="dc31a-109">Wykres dziennika inspekcji Hello</span><span class="sxs-lookup"><span data-stu-id="dc31a-109">hello audit log graph</span></span>
<span data-ttu-id="dc31a-110">W wykres liniowy służy hello inspekcji dziennika tooview hello łączna liczba aktywacji, max aktywacji dziennie i średnie aktywacji na dzień.</span><span class="sxs-lookup"><span data-stu-id="dc31a-110">You can use hello audit log tooview hello total activations, max activations per day, and average activations per day in a line graph.</span></span>  <span data-ttu-id="dc31a-111">Można także filtrować dane hello przez rolę, jeśli istnieje więcej niż jednej roli w hello Historia inspekcji.</span><span class="sxs-lookup"><span data-stu-id="dc31a-111">You can also filter hello data by role if there is more than one role in hello audit history.</span></span>

<span data-ttu-id="dc31a-112">Użyj hello **czasu**, **akcji**, i **roli** przyciski toosort hello dziennika.</span><span class="sxs-lookup"><span data-stu-id="dc31a-112">Use hello **time**, **action**, and **role** buttons toosort hello log.</span></span>

## <a name="hello-audit-log-list"></a><span data-ttu-id="dc31a-113">Lista dzienników inspekcji Hello</span><span class="sxs-lookup"><span data-stu-id="dc31a-113">hello audit log list</span></span>
<span data-ttu-id="dc31a-114">kolumny Hello hello na liście dziennika inspekcji są:</span><span class="sxs-lookup"><span data-stu-id="dc31a-114">hello columns in hello audit log list are:</span></span>

* <span data-ttu-id="dc31a-115">**Obiekt żądający** — użytkownik hello wymagane uaktywnienie roli hello lub zmiany.</span><span class="sxs-lookup"><span data-stu-id="dc31a-115">**Requestor** - hello user who requested hello role activation or change.</span></span>  <span data-ttu-id="dc31a-116">Jeśli jest "Systemu Azure" hello, sprawdź dziennik inspekcji Azure hello, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="dc31a-116">If hello value is "Azure System", check hello Azure audit log for more information.</span></span>
* <span data-ttu-id="dc31a-117">**Użytkownik** -hello użytkownika, który jest uaktywnianie lub przypisaną rolę tooa.</span><span class="sxs-lookup"><span data-stu-id="dc31a-117">**User** - hello user who is activating or assigned tooa role.</span></span>
* <span data-ttu-id="dc31a-118">**Rola** -roli hello przypisane lub aktywowany przez użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="dc31a-118">**Role** - hello role assigned or activated by hello user.</span></span>
* <span data-ttu-id="dc31a-119">**Akcja** — Witaj akcje wykonywane przez obiekt żądający hello.</span><span class="sxs-lookup"><span data-stu-id="dc31a-119">**Action** - hello actions taken by hello requestor.</span></span> <span data-ttu-id="dc31a-120">Może to obejmować przypisania, anulowaniu, aktywacji lub dezaktywacji.</span><span class="sxs-lookup"><span data-stu-id="dc31a-120">This can include assignment, unassignment, activation, or deactivation.</span></span>
* <span data-ttu-id="dc31a-121">**Czas** — gdy akcja hello wystąpił.</span><span class="sxs-lookup"><span data-stu-id="dc31a-121">**Time** - when hello action occurred.</span></span>
* <span data-ttu-id="dc31a-122">**Uzasadnienie** — Jeśli dowolny tekst została wprowadzona w polu Przyczyna hello podczas aktywacji, pojawi się tutaj.</span><span class="sxs-lookup"><span data-stu-id="dc31a-122">**Reasoning** - if any text was entered into hello reason field during activation, it will show up here.</span></span>
* <span data-ttu-id="dc31a-123">**Wygaśnięcie** — tylko istotne dla aktywacji ról.</span><span class="sxs-lookup"><span data-stu-id="dc31a-123">**Expiration** - only relevant for activation of roles.</span></span>

## <a name="filter-hello-audit-log"></a><span data-ttu-id="dc31a-124">Dziennik inspekcji hello filtru</span><span class="sxs-lookup"><span data-stu-id="dc31a-124">Filter hello audit log</span></span>
<span data-ttu-id="dc31a-125">Można filtrować hello informacje, które zostaną wyświetlone w dzienniku inspekcji hello klikając hello **filtru** przycisku.</span><span class="sxs-lookup"><span data-stu-id="dc31a-125">You can filter hello information that shows up in hello audit log by clicking hello **Filter** button.</span></span>  <span data-ttu-id="dc31a-126">Witaj **bloku parametry wykresu aktualizacji** będą wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="dc31a-126">hello **Update chart parameters blade** will appear.</span></span>

<span data-ttu-id="dc31a-127">Po ustawieniu filtrów powitania kliknij **aktualizacji** toofilter hello danych w dzienniku hello.</span><span class="sxs-lookup"><span data-stu-id="dc31a-127">After you set hello filters, click **Update** toofilter hello data in hello log.</span></span>  <span data-ttu-id="dc31a-128">Jeśli dane hello nie występuje od razu, Odśwież stronę hello.</span><span class="sxs-lookup"><span data-stu-id="dc31a-128">If hello data doesn't appear right away, refresh hello page.</span></span>

### <a name="change-hello-date-range"></a><span data-ttu-id="dc31a-129">Zmień zakres dat hello</span><span class="sxs-lookup"><span data-stu-id="dc31a-129">Change hello date range</span></span>
<span data-ttu-id="dc31a-130">Użyj hello **dzisiaj**, **zeszłym tygodniu**, **ostatnim miesiącu**, lub **niestandardowy** przyciski przedział czasu hello toochange hello dziennika inspekcji.</span><span class="sxs-lookup"><span data-stu-id="dc31a-130">Use hello **Today**, **Past Week**, **Past Month**, or **Custom** buttons toochange hello time range of hello audit log.</span></span>

<span data-ttu-id="dc31a-131">Po wybraniu hello **niestandardowy** przycisku, będziesz mieć możliwość **z** Data i **do** Data toospecify pola zakres dat dla hello dziennika.</span><span class="sxs-lookup"><span data-stu-id="dc31a-131">When you choose hello **Custom** button, you will be given a **From** date field and a **To** date field toospecify a range of dates for hello log.</span></span>  <span data-ttu-id="dc31a-132">Możesz wprowadzić hello daty w formacie MM/DD/RRRR lub kliknięcie hello **kalendarza** ikonę i wybierz hello datę z kalendarza.</span><span class="sxs-lookup"><span data-stu-id="dc31a-132">You can either enter hello dates in MM/DD/YYYY format or click on hello **calendar** icon and choose hello date from a calendar.</span></span>

### <a name="change-hello-roles-included-in-hello-log"></a><span data-ttu-id="dc31a-133">Zmiany zawarte w dzienniku hello ról hello</span><span class="sxs-lookup"><span data-stu-id="dc31a-133">Change hello roles included in hello log</span></span>
<span data-ttu-id="dc31a-134">Zaznaczenie lub usunięcie zaznaczenia hello **roli** wyboru dalej tooeach roli tooinclude lub wyklucz go z hello logowania.</span><span class="sxs-lookup"><span data-stu-id="dc31a-134">Check or uncheck hello **Role** checkbox next tooeach role tooinclude or exclude it from hello log.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="dc31a-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="dc31a-135">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

