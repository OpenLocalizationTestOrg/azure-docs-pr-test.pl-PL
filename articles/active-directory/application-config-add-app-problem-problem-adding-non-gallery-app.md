---
title: "Problem podczas dodawania aplikacji z systemem innym niż galerii | Dokumentacja firmy Microsoft"
description: "Zrozumienie kroju osób typowe problemy podczas dodawania niestandardowych aplikacji z systemem innym niż galerii"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: bb3fc7877f4e7cafc3904fc67abd87b897874d8a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="problem-adding-a-non-gallery-application"></a><span data-ttu-id="ae52b-103">Problem podczas dodawania aplikacji z systemem innym niż galerii</span><span class="sxs-lookup"><span data-stu-id="ae52b-103">Problem adding a non-gallery application</span></span>

<span data-ttu-id="ae52b-104">Ten artykuł ułatwia zrozumienie kroju osób typowe problemy przy dodawaniu **niestandardowych aplikacji z systemem innym niż galerii** i sposoby ich rozwiązywania.</span><span class="sxs-lookup"><span data-stu-id="ae52b-104">This article help you to understand the common problems people face when adding **custom non-gallery applications** and what you can do to resolve them.</span></span> 

## <a name="i-clicked-the-add-button-and-my-application-took-a-long-time-to-appear"></a><span data-ttu-id="ae52b-105">Po kliknięciu przycisku "Dodaj" i Moja aplikacja przez długi czas i pojawienie się</span><span class="sxs-lookup"><span data-stu-id="ae52b-105">I clicked the “add” button and my application took a long time to appear</span></span>

<span data-ttu-id="ae52b-106">W pewnych okolicznościach, może upłynąć 1 – 2 minuty (i czasami dłużej) do pojawiają się po dodaniu go do katalogu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ae52b-106">Under some circumstances, it can take 1-2 minutes (and sometimes longer) for an application to appear after adding it to your directory.</span></span> <span data-ttu-id="ae52b-107">Chociaż nie jest to normalne obniżenie wydajności widać dodawania aplikacji jest w toku, klikając **powiadomienia** ikonę (dzwonka) w prawym górnym rogu [Azure Portal](https://portal.azure.com/) i wyszukując **w toku** lub **Ukończono** powiadomień z etykietą **tworzenie aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="ae52b-107">While this is not the normal expected performance, you can see the application addition is in progress by clicking on the **Notifications** icon (the bell) in the upper right of the [Azure Portal](https://portal.azure.com/) and looking for an **In Progress** or **Completed** notification labeled **Create application**.</span></span>

<span data-ttu-id="ae52b-108">Aplikacja nigdy nie zostanie dodany, czy w przypadku wystąpienia błędu podczas klikania **Dodaj** przycisku, zobaczysz **powiadomień** w **błąd** stanu.</span><span class="sxs-lookup"><span data-stu-id="ae52b-108">If your application is never added, or you encounter an error when clicking the **Add** button, you’ll see a **Notification** in an **Error** state.</span></span> <span data-ttu-id="ae52b-109">Jeśli chcesz szczegółowe informacje o błędzie, aby dowiedzieć się więcej na temat lub udostępniać engingeer pomocy technicznej, wykonując kroki opisane w widać więcej informacji o błędzie [sposób wyświetlić szczegóły powiadomieniu portalu](#how-to-see-the-details-of-a-portal-notification) sekcji.</span><span class="sxs-lookup"><span data-stu-id="ae52b-109">If you want more details about the error to learn more to or share with a support engingeer, you can see more information about the error by following the steps in the [How to see the details of a portal notification](#how-to-see-the-details-of-a-portal-notification) section.</span></span>

## <a name="i-clicked-the-add-button-and-my-application-didnt-appear"></a><span data-ttu-id="ae52b-110">Po kliknięciu przycisku "Dodaj" i nie pojawił się Moja aplikacja</span><span class="sxs-lookup"><span data-stu-id="ae52b-110">I clicked the “add” button and my application didn’t appear</span></span>

<span data-ttu-id="ae52b-111">Czasami z powodu przejściowych problemów, problemy z siecią lub usterki, dodawanie błędów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ae52b-111">Sometimes, due to transient issues, networking problems, or a bug, adding an application fail.</span></span> <span data-ttu-id="ae52b-112">Można ustalić dzieje się tak po kliknięciu **powiadomienia** ikonę (dzwonka) w prawym górnym rogu portalu Azure, a ikona jest widoczna czerwony (!) obok pozycji z **tworzenie aplikacji** powiadomień.</span><span class="sxs-lookup"><span data-stu-id="ae52b-112">You can tell this happens when you click the **Notifications** icon (the bell) in the upper right of the Azure Portal and you see a red (!) icon next to your **Create application** notification.</span></span> <span data-ttu-id="ae52b-113">Oznacza to, że wystąpił błąd podczas tworzenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ae52b-113">This indicates there was an error when creating the application.</span></span>

<span data-ttu-id="ae52b-114">Jeśli wystąpi błąd, po kliknięciu przycisku **Dodaj** przycisku, zobaczysz **powiadomień** w **błąd** stanu.</span><span class="sxs-lookup"><span data-stu-id="ae52b-114">If you encounter an error when clicking the **Add** button, you’ll see a **Notification** in an **Error** state.</span></span> <span data-ttu-id="ae52b-115">Jeśli chcesz szczegółowe informacje o błędzie, aby dowiedzieć się więcej na temat lub udostępniać engingeer pomocy technicznej, wykonując kroki opisane w widać więcej informacji o błędzie [sposób wyświetlić szczegóły powiadomieniu portalu](#how-to-see-the-details-of-a-portal-notification) sekcji.</span><span class="sxs-lookup"><span data-stu-id="ae52b-115">If you want more details about the error to learn more to or share with a support engingeer, you can see more information about the error by following the steps in the [How to see the details of a portal notification](#how-to-see-the-details-of-a-portal-notification) section.</span></span>

## <a name="i-dont-know-how-to-set-up-my-application-once-ive-added-it"></a><span data-ttu-id="ae52b-116">I nie wiadomo, jak skonfigurować aplikację, gdy został dodany</span><span class="sxs-lookup"><span data-stu-id="ae52b-116">I don’t know how to set up my application once I’ve added it</span></span>

<span data-ttu-id="ae52b-117">Jeśli potrzebujesz pomocy, informacje o niestandardowych aplikacji [biblioteki dokumentów aplikacji w usłudze Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-apps-index) pomoc, aby dowiedzieć się więcej o rejestracji jednokrotnej z usługą Azure AD i jak działa.</span><span class="sxs-lookup"><span data-stu-id="ae52b-117">If you need help learning about custom applications, the [Azure AD Applications Document Library](https://docs.microsoft.com/azure/active-directory/active-directory-apps-index) help you to learn more about single sign-on with Azure AD and how it works.</span></span>

## <a name="how-to-see-the-details-of-a-portal-notification"></a><span data-ttu-id="ae52b-118">Jak wyświetlić szczegóły powiadomieniu portalu</span><span class="sxs-lookup"><span data-stu-id="ae52b-118">How to see the details of a portal notification</span></span>

<span data-ttu-id="ae52b-119">Szczegółowe informacje o każdym powiadomieniu portalu można wyświetlić, wykonując poniższe kroki:</span><span class="sxs-lookup"><span data-stu-id="ae52b-119">You can see the details of any portal notification by following the steps below:</span></span>

1.  <span data-ttu-id="ae52b-120">Kliknij przycisk **powiadomienia** ikonę (dzwonka) w prawym górnym rogu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="ae52b-120">click the **Notifications** icon (the bell) in the upper right of the Azure Portal</span></span>

2.  <span data-ttu-id="ae52b-121">Wybierz wszystkich powiadomień w **błąd** stanu (te z czerwonym znakiem (!) obok nich).</span><span class="sxs-lookup"><span data-stu-id="ae52b-121">Select any notification in an **Error** state (those with a red (!) next to them).</span></span>

   >[!NOTE]
   ><span data-ttu-id="ae52b-122">Nie można kliknąć powiadomienia w **Powodzenie** lub **w toku** stanu.</span><span class="sxs-lookup"><span data-stu-id="ae52b-122">You cannot click notifications in a **Successful** or **In Progress** state.</span></span>
   >
   >

3.  <span data-ttu-id="ae52b-123">Otwórz ten **szczegóły powiadomienia** bloku.</span><span class="sxs-lookup"><span data-stu-id="ae52b-123">This open the **Notification Details** blade.</span></span>

4.  <span data-ttu-id="ae52b-124">Dzięki tym informacjom samodzielnie, aby poznać więcej szczegółów o problemie.</span><span class="sxs-lookup"><span data-stu-id="ae52b-124">Use this information yourself to understand more details about the problem.</span></span>

5.  <span data-ttu-id="ae52b-125">Jeśli nadal potrzebujesz pomocy, te informacje mogą również współużytkować z pracownikiem pomocy technicznej lub grupa produktów, aby uzyskać pomoc dotyczącą tego problemu.</span><span class="sxs-lookup"><span data-stu-id="ae52b-125">If you still need help, you can also share this information with a support engineer or the product group to get help with your problem.</span></span>

6.  <span data-ttu-id="ae52b-126">Kliknij przycisk **ikonę kopiowania** z prawej strony **błąd kopiowania** skopiuj wszystkie szczegóły powiadomienia na udostępnianie z pracownikiem pomocy technicznej lub produkt grupy w polu tekstowym.</span><span class="sxs-lookup"><span data-stu-id="ae52b-126">Click the **copy icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer.</span></span>

## <a name="how-to-get-help-by-sending-notification-details-to-a-support-engineer"></a><span data-ttu-id="ae52b-127">Jak uzyskać pomoc, wysyłając szczegóły powiadomienia do pracownika pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="ae52b-127">How to get help by sending notification details to a support engineer</span></span>

<span data-ttu-id="ae52b-128">Jest bardzo ważne, aby udostępniać **poniższymi szczegółami** z pracownikiem pomocy technicznej, jeśli potrzebujesz pomocy, dzięki czemu mogą one ułatwić szybkie.</span><span class="sxs-lookup"><span data-stu-id="ae52b-128">It is very important that you share **all the details listed below** with a support engineer if you need help, so that they can help you quickly.</span></span> <span data-ttu-id="ae52b-129">Możesz to zrobić w prosty sposób przez **zrobieniem zrzutu ekranu,** lub przez kliknięcie przycisku **ikony błędu kopiowania**, liczba znalezionych na prawo od **błąd kopiowania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="ae52b-129">You can do this easily by **taking a screenshot,** or by clicking the **Copy error icon**, found to the right of the **Copy error** textbox.</span></span>

## <a name="notification-details-explained"></a><span data-ttu-id="ae52b-130">Szczegóły powiadomienia wyjaśniono</span><span class="sxs-lookup"><span data-stu-id="ae52b-130">Notification Details Explained</span></span>

<span data-ttu-id="ae52b-131">Poniżej przedstawiono więcej funkcji każdego, powiadomienia elementów oznacza i zawiera przykłady każdego z nich.</span><span class="sxs-lookup"><span data-stu-id="ae52b-131">The below explains more what each of the notification items means, and gives examples of each of them.</span></span>

### <a name="essential-notification-items"></a><span data-ttu-id="ae52b-132">Elementy podstawowych powiadomień</span><span class="sxs-lookup"><span data-stu-id="ae52b-132">Essential Notification Items</span></span>

-   <span data-ttu-id="ae52b-133">**Tytuł** — opisowy tytuł powiadomienia</span><span class="sxs-lookup"><span data-stu-id="ae52b-133">**Title** – the descriptive title of the notification</span></span>
   *  <span data-ttu-id="ae52b-134">Przykład — **ustawienia serwera proxy aplikacji**</span><span class="sxs-lookup"><span data-stu-id="ae52b-134">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="ae52b-135">**Opis elementu** — opis co nastąpiło w wyniku operacji</span><span class="sxs-lookup"><span data-stu-id="ae52b-135">**Description** – the description of what occurred as a result of the operation</span></span>

   *  <span data-ttu-id="ae52b-136">Przykład — **wewnętrzny wprowadzony adres url jest już używana przez inną aplikację**</span><span class="sxs-lookup"><span data-stu-id="ae52b-136">Example – **Internal url entered is already being used by another application**</span></span>

-   <span data-ttu-id="ae52b-137">**Identyfikator powiadomień** — Unikatowy identyfikator powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="ae52b-137">**Notification Id** – the unique id of the notification</span></span>

   *  <span data-ttu-id="ae52b-138">Przykład — **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span><span class="sxs-lookup"><span data-stu-id="ae52b-138">Example – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span></span>

-   <span data-ttu-id="ae52b-139">**Identyfikator żądania klienta** — identyfikator określonego żądania przez przeglądarkę</span><span class="sxs-lookup"><span data-stu-id="ae52b-139">**Client Request Id** – the specific request id made by your browser</span></span>

   *  <span data-ttu-id="ae52b-140">Przykład — **302fd775-3329-4670-a9f3-bea37004f0bc**</span><span class="sxs-lookup"><span data-stu-id="ae52b-140">Example – **302fd775-3329-4670-a9f3-bea37004f0bc**</span></span>

-   <span data-ttu-id="ae52b-141">**Czas UTC sygnatury** — znacznik czasu, w którym wystąpił powiadomienia, w formacie UTC</span><span class="sxs-lookup"><span data-stu-id="ae52b-141">**Time Stamp UTC** – the timestamp during which the notification occurred, in UTC</span></span>

   *  <span data-ttu-id="ae52b-142">Przykład — **2017-03-23T19:50:43.7583681Z**</span><span class="sxs-lookup"><span data-stu-id="ae52b-142">Example – **2017-03-23T19:50:43.7583681Z**</span></span>

-   <span data-ttu-id="ae52b-143">**Wewnętrzny identyfikator transakcji** — wewnętrzny identyfikator możemy użyć do wyszukiwania błąd w naszym systemie</span><span class="sxs-lookup"><span data-stu-id="ae52b-143">**Internal Transaction Id** – the internal ID we can use to look the error up in our systems</span></span>

   *  <span data-ttu-id="ae52b-144">Przykład — **71a2f329-ca29-402f-aa72-bc00a7aca603**</span><span class="sxs-lookup"><span data-stu-id="ae52b-144">Example – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span></span>

-   <span data-ttu-id="ae52b-145">**Nazwa UPN** — użytkownik, który wykonał działanie</span><span class="sxs-lookup"><span data-stu-id="ae52b-145">**UPN** – the user who performed the operation</span></span>

   *  <span data-ttu-id="ae52b-146">Przykład —**tperkins@f128.info**</span><span class="sxs-lookup"><span data-stu-id="ae52b-146">Example – **tperkins@f128.info**</span></span>

-   <span data-ttu-id="ae52b-147">**Identyfikator dzierżawy** — Unikatowy identyfikator dzierżawy, który użytkownik, który wykonał działanie był członkiem</span><span class="sxs-lookup"><span data-stu-id="ae52b-147">**Tenant Id** – the unique ID of the tenant that the user who performed the operation was a member of</span></span>

   *  <span data-ttu-id="ae52b-148">Przykład — **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span><span class="sxs-lookup"><span data-stu-id="ae52b-148">Example – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span></span>

-   <span data-ttu-id="ae52b-149">**Identyfikator obiektu użytkownika** — Unikatowy identyfikator użytkownika, który wykonał działanie</span><span class="sxs-lookup"><span data-stu-id="ae52b-149">**User object Id** – the unique ID of the user who performed the operation</span></span>

 *  <span data-ttu-id="ae52b-150">Przykład — **17f84be4-51f8-483a-b533-383791227a99**</span><span class="sxs-lookup"><span data-stu-id="ae52b-150">Example – **17f84be4-51f8-483a-b533-383791227a99**</span></span>

### <a name="detailed-notification-items"></a><span data-ttu-id="ae52b-151">Elementy szczegółowe powiadomienia</span><span class="sxs-lookup"><span data-stu-id="ae52b-151">Detailed Notification Items</span></span>

-   <span data-ttu-id="ae52b-152">**Nazwa wyświetlana** — **(może być pusta)** nazwę wyświetlaną bardziej szczegółowy kod błędu</span><span class="sxs-lookup"><span data-stu-id="ae52b-152">**Display Name** – **(can be empty)** a more detailed display name for the error</span></span>

  *  <span data-ttu-id="ae52b-153">Przykład — **ustawienia serwera proxy aplikacji**</span><span class="sxs-lookup"><span data-stu-id="ae52b-153">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="ae52b-154">**Stan** — stan określonego powiadomienia</span><span class="sxs-lookup"><span data-stu-id="ae52b-154">**Status** – the specific status of the notification</span></span>

   *  <span data-ttu-id="ae52b-155">Przykład — **nie powiodło się**</span><span class="sxs-lookup"><span data-stu-id="ae52b-155">Example – **Failed**</span></span>

-   <span data-ttu-id="ae52b-156">**Obiekt o identyfikatorze** — **(może być pusta)** Identyfikatora obiektu, względem którego wykonano operację</span><span class="sxs-lookup"><span data-stu-id="ae52b-156">**Object Id** – **(can be empty)** the object ID against which the operation was performed</span></span>

   *  <span data-ttu-id="ae52b-157">Przykład — **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span><span class="sxs-lookup"><span data-stu-id="ae52b-157">Example – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span></span>

-   <span data-ttu-id="ae52b-158">**Szczegóły** — szczegółowy opis co nastąpiło w wyniku operacji</span><span class="sxs-lookup"><span data-stu-id="ae52b-158">**Details** – the detailed description of what occurred as a result of the operation</span></span>

   *  <span data-ttu-id="ae52b-159">Przykład — **wewnętrznego adresu url "http://bing.com/" jest nieprawidłowy, ponieważ jest już używana**</span><span class="sxs-lookup"><span data-stu-id="ae52b-159">Example – **Internal url 'http://bing.com/' is invalid since it is already in use**</span></span>

-   <span data-ttu-id="ae52b-160">**Błąd kopiowania** — kliknij przycisk **ikonę kopiowania** z prawej strony **błąd kopiowania** pole tekstowe, aby skopiować wszystkie szczegóły powiadomienia na udostępnianie z pracownikiem pomocy technicznej lub produkt grupy</span><span class="sxs-lookup"><span data-stu-id="ae52b-160">**Copy error** – Click the **copy icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer</span></span>

   *  <span data-ttu-id="ae52b-161">Przykład```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span><span class="sxs-lookup"><span data-stu-id="ae52b-161">Example ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span></span>

## <a name="next-steps"></a><span data-ttu-id="ae52b-162">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ae52b-162">Next steps</span></span>
[<span data-ttu-id="ae52b-163">Zarządzanie aplikacjami przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ae52b-163">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)



