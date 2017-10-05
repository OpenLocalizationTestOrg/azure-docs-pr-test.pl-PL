---
title: "Operacje Menedżera usługi synchronizacji programu Azure AD Connect | Dokumentacja firmy Microsoft"
description: "Dowiedz się na karcie operacje Menedżera usługi synchronizacji programu Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 97a26565-618f-4313-8711-5925eeb47cdc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a1475e4fcd11eb008badba49665f4af6029a1697
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="using-the-sync-service-manager-operations-tab"></a><span data-ttu-id="077c2-103">Na karcie operacje Menedżera usługi synchronizacji</span><span class="sxs-lookup"><span data-stu-id="077c2-103">Using the Sync Service Manager Operations tab</span></span>

![Menedżera usługi synchronizacji](./media/active-directory-aadconnectsync-service-manager-ui/operations.png)

<span data-ttu-id="077c2-105">Na karcie operacje pokazuje wyniki od ostatniej operacji.</span><span class="sxs-lookup"><span data-stu-id="077c2-105">The operations tab shows the results from the most recent operations.</span></span> <span data-ttu-id="077c2-106">Na tej karcie jest kluczem do zrozumienia i rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="077c2-106">This tab is key to understand and troubleshoot issues.</span></span>

## <a name="understand-the-information-visible-in-the-operations-tab"></a><span data-ttu-id="077c2-107">Zrozumienie informacji widocznych na karcie operacje</span><span class="sxs-lookup"><span data-stu-id="077c2-107">Understand the information visible in the operations tab</span></span>
<span data-ttu-id="077c2-108">Górnej połowie zawiera wszystkie elementy w kolejności chronologicznej.</span><span class="sxs-lookup"><span data-stu-id="077c2-108">The top half shows all runs in chronological order.</span></span> <span data-ttu-id="077c2-109">Domyślnie operacje logowania zachowuje informacje dotyczące ostatnich siedmiu dni, ale ustawienie to można zmienić z [harmonogramu](active-directory-aadconnectsync-feature-scheduler.md).</span><span class="sxs-lookup"><span data-stu-id="077c2-109">By default, the operations log keeps information about the last seven days, but this setting can be changed with the [scheduler](active-directory-aadconnectsync-feature-scheduler.md).</span></span> <span data-ttu-id="077c2-110">Chcesz znaleźć dla dowolnego przebiegu pokazywać stanu Powodzenie.</span><span class="sxs-lookup"><span data-stu-id="077c2-110">You want to look for any run that does not show a success status.</span></span> <span data-ttu-id="077c2-111">Można zmienić sortowania, klikając nagłówki.</span><span class="sxs-lookup"><span data-stu-id="077c2-111">You can change the sorting by clicking the headers.</span></span>

<span data-ttu-id="077c2-112">**Stan** jest najważniejsze informacje i przedstawia najbardziej poważny problem dla przebiegu.</span><span class="sxs-lookup"><span data-stu-id="077c2-112">The **Status** column is the most important information and shows the most severe problem for a run.</span></span> <span data-ttu-id="077c2-113">Oto krótkie podsumowanie stanów najczęściej w kolejności priorytetu do sprawdzania, czy (gdzie * wskazać ciągi możliwy błąd kilka).</span><span class="sxs-lookup"><span data-stu-id="077c2-113">Here is a quick summary of the most common statuses in order of priority to investigate (where * indicate several possible error strings).</span></span>

| <span data-ttu-id="077c2-114">Stan</span><span class="sxs-lookup"><span data-stu-id="077c2-114">Status</span></span> | <span data-ttu-id="077c2-115">Komentarz</span><span class="sxs-lookup"><span data-stu-id="077c2-115">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="077c2-116">Zatrzymano-*</span><span class="sxs-lookup"><span data-stu-id="077c2-116">stopped-*</span></span> |<span data-ttu-id="077c2-117">Nie można wykonać przebiegu.</span><span class="sxs-lookup"><span data-stu-id="077c2-117">The run could not complete.</span></span> <span data-ttu-id="077c2-118">Na przykład, jeśli nie działa i nie można skontaktować się z systemu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="077c2-118">For example, if the remote system is down and cannot be contacted.</span></span> |
| <span data-ttu-id="077c2-119">Zatrzymano-— limit błędów</span><span class="sxs-lookup"><span data-stu-id="077c2-119">stopped-error-limit</span></span> |<span data-ttu-id="077c2-120">Wystąpiły błędy więcej niż 5000.</span><span class="sxs-lookup"><span data-stu-id="077c2-120">There are more than 5,000 errors.</span></span> <span data-ttu-id="077c2-121">Uruchom automatycznie zostało zatrzymane z powodu dużej liczby błędów.</span><span class="sxs-lookup"><span data-stu-id="077c2-121">The run was automatically stopped due to the large number of errors.</span></span> |
| <span data-ttu-id="077c2-122">Ukończono -\*— błędy</span><span class="sxs-lookup"><span data-stu-id="077c2-122">completed-\*-errors</span></span> |<span data-ttu-id="077c2-123">Przy uruchomieniu ukończone, ale wystąpiły błędy (mniej niż 5000), które należy zbadać.</span><span class="sxs-lookup"><span data-stu-id="077c2-123">The run completed, but there are errors (fewer than 5,000) that should be investigated.</span></span> |
| <span data-ttu-id="077c2-124">Ukończono -\*— ostrzeżenia</span><span class="sxs-lookup"><span data-stu-id="077c2-124">completed-\*-warnings</span></span> |<span data-ttu-id="077c2-125">Przy uruchomieniu ukończone, ale niektóre dane nie jest w oczekiwanym stanem.</span><span class="sxs-lookup"><span data-stu-id="077c2-125">The run completed, but some data is not in the expected state.</span></span> <span data-ttu-id="077c2-126">Jeśli masz błędy, następnie ten komunikat jest zwykle tylko objawem.</span><span class="sxs-lookup"><span data-stu-id="077c2-126">If you have errors, then this message is usually only a symptom.</span></span> <span data-ttu-id="077c2-127">Dopóki usunąć błędy, nie powinien być sprawdzony ostrzeżenia.</span><span class="sxs-lookup"><span data-stu-id="077c2-127">Until you have addressed errors, you should not investigate warnings.</span></span> |
| <span data-ttu-id="077c2-128">powodzenie</span><span class="sxs-lookup"><span data-stu-id="077c2-128">success</span></span> |<span data-ttu-id="077c2-129">Brak problemów.</span><span class="sxs-lookup"><span data-stu-id="077c2-129">No issues.</span></span> |

<span data-ttu-id="077c2-130">Po zaznaczeniu wiersza dolnej aktualizuje Pokaż szczegóły uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="077c2-130">When you select a row, the bottom updates to show the details of that run.</span></span> <span data-ttu-id="077c2-131">Na lewo od dołu, może mieć listy informacją o tym **krok nr**.</span><span class="sxs-lookup"><span data-stu-id="077c2-131">To the far left of the bottom, you might have a list saying **Step #**.</span></span> <span data-ttu-id="077c2-132">Ta lista jest wyświetlana tylko, jeśli masz wiele domen w lesie gdzie każdej domeny jest reprezentowany przez krok.</span><span class="sxs-lookup"><span data-stu-id="077c2-132">This list only appears if you have multiple domains in your forest where each domain is represented by a step.</span></span> <span data-ttu-id="077c2-133">Nazwa domeny znajduje się w pozycji **partycji**.</span><span class="sxs-lookup"><span data-stu-id="077c2-133">The domain name can be found under the heading **Partition**.</span></span> <span data-ttu-id="077c2-134">W obszarze **statystyki synchronizacji**, można znaleźć więcej informacji na temat liczby zmian, które zostały przetworzone.</span><span class="sxs-lookup"><span data-stu-id="077c2-134">Under **Synchronization Statistics**, you can find more information about the number of changes that were processed.</span></span> <span data-ttu-id="077c2-135">Kliknięcie łącza spowoduje wyświetlenie listy zmienionych obiektów.</span><span class="sxs-lookup"><span data-stu-id="077c2-135">You can click the links to get a list of the changed objects.</span></span> <span data-ttu-id="077c2-136">Jeśli masz obiektów z błędami, te błędy są wyświetlane w oknie **błędy synchronizacji**.</span><span class="sxs-lookup"><span data-stu-id="077c2-136">If you have objects with errors, those errors show up under **Synchronization Errors**.</span></span>

<span data-ttu-id="077c2-137">Aby uzyskać więcej informacji, zobacz [Rozwiązywanie problemów z obiektu, który nie jest synchronizowanie](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md)</span><span class="sxs-lookup"><span data-stu-id="077c2-137">For more information, see [troubleshoot an object that is not synchronizing](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="077c2-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="077c2-138">Next steps</span></span>
<span data-ttu-id="077c2-139">Dowiedz się więcej o [synchronizacja programu Azure AD Connect](active-directory-aadconnectsync-whatis.md) konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="077c2-139">Learn more about the [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="077c2-140">Dowiedz się więcej na temat [integrowania tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="077c2-140">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
