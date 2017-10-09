---
title: "Dodawanie aplikacji z systemem innym niż galerii aaaProblem | Dokumentacja firmy Microsoft"
description: "Zrozumienie hello typowych problemów osób krój podczas dodawania niestandardowych aplikacji z systemem innym niż galerii"
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
ms.openlocfilehash: cfe9b657ae18cbacaddbd85658471a2c57c9cf95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="problem-adding-a-non-gallery-application"></a><span data-ttu-id="a54cb-103">Problem podczas dodawania aplikacji z systemem innym niż galerii</span><span class="sxs-lookup"><span data-stu-id="a54cb-103">Problem adding a non-gallery application</span></span>

<span data-ttu-id="a54cb-104">W tym artykule pomóc toounderstand hello typowych problemów osób krój podczas dodawania **niestandardowych aplikacji z systemem innym niż galerii** i co można zrobić tooresolve je.</span><span class="sxs-lookup"><span data-stu-id="a54cb-104">This article help you toounderstand hello common problems people face when adding **custom non-gallery applications** and what you can do tooresolve them.</span></span> 

## <a name="i-clicked-hello-add-button-and-my-application-took-a-long-time-tooappear"></a><span data-ttu-id="a54cb-105">Po kliknięciu hello "Dodaj", że przycisk i Moja aplikacja tooappear długo trwało</span><span class="sxs-lookup"><span data-stu-id="a54cb-105">I clicked hello “add” button and my application took a long time tooappear</span></span>

<span data-ttu-id="a54cb-106">W pewnych okolicznościach, może upłynąć 1 – 2 minuty (i czasami dłużej) dla aplikacji tooappear po dodaniu tooyour katalogu.</span><span class="sxs-lookup"><span data-stu-id="a54cb-106">Under some circumstances, it can take 1-2 minutes (and sometimes longer) for an application tooappear after adding it tooyour directory.</span></span> <span data-ttu-id="a54cb-107">Chociaż nie jest to normalne obniżenie wydajności hello widać, dodanie aplikacji hello jest w toku, klikając hello **powiadomienia** ikonę (hello dzwonka) w hello górnym rogu hello [Azure Portal](https://portal.azure.com/)i wyszukując **w toku** lub **Ukończono** powiadomień z etykietą **tworzenie aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="a54cb-107">While this is not hello normal expected performance, you can see hello application addition is in progress by clicking on hello **Notifications** icon (hello bell) in hello upper right of hello [Azure Portal](https://portal.azure.com/) and looking for an **In Progress** or **Completed** notification labeled **Create application**.</span></span>

<span data-ttu-id="a54cb-108">Jeśli aplikacja nigdy nie zostanie dodany lub w przypadku wystąpienia błędu podczas klikania hello **Dodaj** przycisku, zobaczysz **powiadomień** w **błąd** stanu.</span><span class="sxs-lookup"><span data-stu-id="a54cb-108">If your application is never added, or you encounter an error when clicking hello **Add** button, you’ll see a **Notification** in an **Error** state.</span></span> <span data-ttu-id="a54cb-109">Jeśli chcesz, aby więcej szczegółów na temat toolearn błąd hello więcej tooor udostępniać engingeer pomocy technicznej, wykonując kroki hello w hello widać więcej informacji o błędzie hello [jak toosee szczegóły hello powiadomieniu portalu](#how-to-see-the-details-of-a-portal-notification) sekcji.</span><span class="sxs-lookup"><span data-stu-id="a54cb-109">If you want more details about hello error toolearn more tooor share with a support engingeer, you can see more information about hello error by following hello steps in hello [How toosee hello details of a portal notification](#how-to-see-the-details-of-a-portal-notification) section.</span></span>

## <a name="i-clicked-hello-add-button-and-my-application-didnt-appear"></a><span data-ttu-id="a54cb-110">Po kliknięciu przycisku "Dodaj" hello, a nie pojawił się Moja aplikacja</span><span class="sxs-lookup"><span data-stu-id="a54cb-110">I clicked hello “add” button and my application didn’t appear</span></span>

<span data-ttu-id="a54cb-111">Czasami powodu tootransient problemy, problemy z siecią lub usterki, dodawanie błędów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a54cb-111">Sometimes, due tootransient issues, networking problems, or a bug, adding an application fail.</span></span> <span data-ttu-id="a54cb-112">Można ustalić dzieje się tak po kliknięciu hello **powiadomienia** ikonę (hello dzwonka) w prawym górnym rogu hello hello portalu Azure, a wyświetlony czerwony (!) ikona dalej tooyour **tworzenie aplikacji** powiadomień.</span><span class="sxs-lookup"><span data-stu-id="a54cb-112">You can tell this happens when you click hello **Notifications** icon (hello bell) in hello upper right of hello Azure Portal and you see a red (!) icon next tooyour **Create application** notification.</span></span> <span data-ttu-id="a54cb-113">Oznacza to, że wystąpił błąd podczas tworzenia aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="a54cb-113">This indicates there was an error when creating hello application.</span></span>

<span data-ttu-id="a54cb-114">Jeśli wystąpi błąd podczas klikania hello **Dodaj** przycisku, zobaczysz **powiadomień** w **błąd** stanu.</span><span class="sxs-lookup"><span data-stu-id="a54cb-114">If you encounter an error when clicking hello **Add** button, you’ll see a **Notification** in an **Error** state.</span></span> <span data-ttu-id="a54cb-115">Jeśli chcesz, aby więcej szczegółów na temat toolearn błąd hello więcej tooor udostępniać engingeer pomocy technicznej, wykonując kroki hello w hello widać więcej informacji o błędzie hello [jak toosee szczegóły hello powiadomieniu portalu](#how-to-see-the-details-of-a-portal-notification) sekcji.</span><span class="sxs-lookup"><span data-stu-id="a54cb-115">If you want more details about hello error toolearn more tooor share with a support engingeer, you can see more information about hello error by following hello steps in hello [How toosee hello details of a portal notification](#how-to-see-the-details-of-a-portal-notification) section.</span></span>

## <a name="i-dont-know-how-tooset-up-my-application-once-ive-added-it"></a><span data-ttu-id="a54cb-116">Nie wiadomo jak tooset zapasową mojej aplikacji raz zostały dodane go</span><span class="sxs-lookup"><span data-stu-id="a54cb-116">I don’t know how tooset up my application once I’ve added it</span></span>

<span data-ttu-id="a54cb-117">Jeśli potrzebujesz pomocy, informacje o niestandardowych aplikacji hello [biblioteki dokumentów aplikacji w usłudze Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-apps-index) ułatwiają toolearn więcej informacji na temat rejestracji jednokrotnej z usługą Azure AD i jej działania.</span><span class="sxs-lookup"><span data-stu-id="a54cb-117">If you need help learning about custom applications, hello [Azure AD Applications Document Library](https://docs.microsoft.com/azure/active-directory/active-directory-apps-index) help you toolearn more about single sign-on with Azure AD and how it works.</span></span>

## <a name="how-toosee-hello-details-of-a-portal-notification"></a><span data-ttu-id="a54cb-118">Jak toosee szczegóły hello powiadomieniu portalu</span><span class="sxs-lookup"><span data-stu-id="a54cb-118">How toosee hello details of a portal notification</span></span>

<span data-ttu-id="a54cb-119">Szczegóły hello powiadomienia portalu można wyświetlić, wykonując poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="a54cb-119">You can see hello details of any portal notification by following hello steps below:</span></span>

1.  <span data-ttu-id="a54cb-120">Kliknij przycisk hello **powiadomienia** ikonę (hello dzwonka) w prawym górnym rogu portalu Azure hello hello</span><span class="sxs-lookup"><span data-stu-id="a54cb-120">click hello **Notifications** icon (hello bell) in hello upper right of hello Azure Portal</span></span>

2.  <span data-ttu-id="a54cb-121">Wybierz wszystkich powiadomień w **błąd** stanu (te z toothem dalej czerwony (!)).</span><span class="sxs-lookup"><span data-stu-id="a54cb-121">Select any notification in an **Error** state (those with a red (!) next toothem).</span></span>

   >[!NOTE]
   ><span data-ttu-id="a54cb-122">Nie można kliknąć powiadomienia w **Powodzenie** lub **w toku** stanu.</span><span class="sxs-lookup"><span data-stu-id="a54cb-122">You cannot click notifications in a **Successful** or **In Progress** state.</span></span>
   >
   >

3.  <span data-ttu-id="a54cb-123">Ta Otwórz hello **szczegóły powiadomienia** bloku.</span><span class="sxs-lookup"><span data-stu-id="a54cb-123">This open hello **Notification Details** blade.</span></span>

4.  <span data-ttu-id="a54cb-124">Dzięki tym informacjom samodzielnie toounderstand więcej szczegółowych informacji o hello problem.</span><span class="sxs-lookup"><span data-stu-id="a54cb-124">Use this information yourself toounderstand more details about hello problem.</span></span>

5.  <span data-ttu-id="a54cb-125">Jeśli nadal potrzebujesz pomocy, można również udostępniać te informacje pomocy technicznej odtwarzania lub hello grupy tooget Pomoc produktu o problemie.</span><span class="sxs-lookup"><span data-stu-id="a54cb-125">If you still need help, you can also share this information with a support engineer or hello product group tooget help with your problem.</span></span>

6.  <span data-ttu-id="a54cb-126">Kliknij hello **ikonę kopiowania** toohello rogu hello **błąd kopiowania** toocopy pole tekstowe wszystkich hello tooshare szczegóły powiadomienia o z pracownikiem pomocy technicznej lub produkt grupy.</span><span class="sxs-lookup"><span data-stu-id="a54cb-126">Click hello **copy icon** toohello right of hello **Copy error** textbox toocopy all hello notification details tooshare with a support or product group engineer.</span></span>

## <a name="how-tooget-help-by-sending-notification-details-tooa-support-engineer"></a><span data-ttu-id="a54cb-127">Jak tooget pomóc, wysyłając powiadomienia szczegóły tooa specjaliście pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="a54cb-127">How tooget help by sending notification details tooa support engineer</span></span>

<span data-ttu-id="a54cb-128">Jest bardzo ważne, aby udostępniać **hello wszystkie dane przedstawione poniżej** z pracownikiem pomocy technicznej, jeśli potrzebujesz pomocy, dzięki czemu mogą one ułatwić szybkie.</span><span class="sxs-lookup"><span data-stu-id="a54cb-128">It is very important that you share **all hello details listed below** with a support engineer if you need help, so that they can help you quickly.</span></span> <span data-ttu-id="a54cb-129">Możesz to zrobić w prosty sposób przez **zrobieniem zrzutu ekranu,** lub przez kliknięcie przycisku hello **ikony błędu kopiowania**, znaleziono prawej toohello hello **błąd kopiowania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="a54cb-129">You can do this easily by **taking a screenshot,** or by clicking hello **Copy error icon**, found toohello right of hello **Copy error** textbox.</span></span>

## <a name="notification-details-explained"></a><span data-ttu-id="a54cb-130">Szczegóły powiadomienia wyjaśniono</span><span class="sxs-lookup"><span data-stu-id="a54cb-130">Notification Details Explained</span></span>

<span data-ttu-id="a54cb-131">Hello poniżej opisano bardziej jakie poszczególnych elementów powiadomień hello oznacza oraz przykłady zapewnia każdego z nich.</span><span class="sxs-lookup"><span data-stu-id="a54cb-131">hello below explains more what each of hello notification items means, and gives examples of each of them.</span></span>

### <a name="essential-notification-items"></a><span data-ttu-id="a54cb-132">Elementy podstawowych powiadomień</span><span class="sxs-lookup"><span data-stu-id="a54cb-132">Essential Notification Items</span></span>

-   <span data-ttu-id="a54cb-133">**Tytuł** — Witaj opisowy tytuł hello powiadomień</span><span class="sxs-lookup"><span data-stu-id="a54cb-133">**Title** – hello descriptive title of hello notification</span></span>
   *  <span data-ttu-id="a54cb-134">Przykład — **ustawienia serwera proxy aplikacji**</span><span class="sxs-lookup"><span data-stu-id="a54cb-134">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="a54cb-135">**Opis elementu** — Witaj opis co nastąpiło w wyniku operacji hello</span><span class="sxs-lookup"><span data-stu-id="a54cb-135">**Description** – hello description of what occurred as a result of hello operation</span></span>

   *  <span data-ttu-id="a54cb-136">Przykład — **wewnętrzny wprowadzony adres url jest już używana przez inną aplikację**</span><span class="sxs-lookup"><span data-stu-id="a54cb-136">Example – **Internal url entered is already being used by another application**</span></span>

-   <span data-ttu-id="a54cb-137">**Identyfikator powiadomień** — Unikatowy identyfikator hello hello powiadomienia</span><span class="sxs-lookup"><span data-stu-id="a54cb-137">**Notification Id** – hello unique id of hello notification</span></span>

   *  <span data-ttu-id="a54cb-138">Przykład — **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span><span class="sxs-lookup"><span data-stu-id="a54cb-138">Example – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span></span>

-   <span data-ttu-id="a54cb-139">**Identyfikator żądania klienta** — identyfikator określonego żądania hello wprowadzone przez przeglądarkę</span><span class="sxs-lookup"><span data-stu-id="a54cb-139">**Client Request Id** – hello specific request id made by your browser</span></span>

   *  <span data-ttu-id="a54cb-140">Przykład — **302fd775-3329-4670-a9f3-bea37004f0bc**</span><span class="sxs-lookup"><span data-stu-id="a54cb-140">Example – **302fd775-3329-4670-a9f3-bea37004f0bc**</span></span>

-   <span data-ttu-id="a54cb-141">**Czas UTC sygnatury** — Witaj znaczników czasu, w którym wystąpił hello powiadomień, w formacie UTC</span><span class="sxs-lookup"><span data-stu-id="a54cb-141">**Time Stamp UTC** – hello timestamp during which hello notification occurred, in UTC</span></span>

   *  <span data-ttu-id="a54cb-142">Przykład — **2017-03-23T19:50:43.7583681Z**</span><span class="sxs-lookup"><span data-stu-id="a54cb-142">Example – **2017-03-23T19:50:43.7583681Z**</span></span>

-   <span data-ttu-id="a54cb-143">**Wewnętrzny identyfikator transakcji** — Witaj wewnętrzny identyfikator możemy użyć błąd hello toolook w naszych systemów</span><span class="sxs-lookup"><span data-stu-id="a54cb-143">**Internal Transaction Id** – hello internal ID we can use toolook hello error up in our systems</span></span>

   *  <span data-ttu-id="a54cb-144">Przykład — **71a2f329-ca29-402f-aa72-bc00a7aca603**</span><span class="sxs-lookup"><span data-stu-id="a54cb-144">Example – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span></span>

-   <span data-ttu-id="a54cb-145">**Nazwa UPN** — Witaj użytkownika, który wykonał operację hello</span><span class="sxs-lookup"><span data-stu-id="a54cb-145">**UPN** – hello user who performed hello operation</span></span>

   *  <span data-ttu-id="a54cb-146">Przykład —**tperkins@f128.info**</span><span class="sxs-lookup"><span data-stu-id="a54cb-146">Example – **tperkins@f128.info**</span></span>

-   <span data-ttu-id="a54cb-147">**Identyfikator dzierżawy** — Unikatowy identyfikator dzierżawy hello, która hello użytkownika wykonującego operację hello hello był członkiem</span><span class="sxs-lookup"><span data-stu-id="a54cb-147">**Tenant Id** – hello unique ID of hello tenant that hello user who performed hello operation was a member of</span></span>

   *  <span data-ttu-id="a54cb-148">Przykład — **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span><span class="sxs-lookup"><span data-stu-id="a54cb-148">Example – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span></span>

-   <span data-ttu-id="a54cb-149">**Identyfikator obiektu użytkownika** — Witaj Unikatowy identyfikator hello użytkownika, który wykonał operację hello</span><span class="sxs-lookup"><span data-stu-id="a54cb-149">**User object Id** – hello unique ID of hello user who performed hello operation</span></span>

 *  <span data-ttu-id="a54cb-150">Przykład — **17f84be4-51f8-483a-b533-383791227a99**</span><span class="sxs-lookup"><span data-stu-id="a54cb-150">Example – **17f84be4-51f8-483a-b533-383791227a99**</span></span>

### <a name="detailed-notification-items"></a><span data-ttu-id="a54cb-151">Elementy szczegółowe powiadomienia</span><span class="sxs-lookup"><span data-stu-id="a54cb-151">Detailed Notification Items</span></span>

-   <span data-ttu-id="a54cb-152">**Nazwa wyświetlana** — **(może być pusta)** nazwę wyświetlaną bardziej szczegółowy błąd hello</span><span class="sxs-lookup"><span data-stu-id="a54cb-152">**Display Name** – **(can be empty)** a more detailed display name for hello error</span></span>

  *  <span data-ttu-id="a54cb-153">Przykład — **ustawienia serwera proxy aplikacji**</span><span class="sxs-lookup"><span data-stu-id="a54cb-153">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="a54cb-154">**Stan** — Witaj określonego stanu hello powiadomień</span><span class="sxs-lookup"><span data-stu-id="a54cb-154">**Status** – hello specific status of hello notification</span></span>

   *  <span data-ttu-id="a54cb-155">Przykład — **nie powiodło się**</span><span class="sxs-lookup"><span data-stu-id="a54cb-155">Example – **Failed**</span></span>

-   <span data-ttu-id="a54cb-156">**Obiekt o identyfikatorze** — **(może być pusta)** hello Identyfikatora obiektu, względem których hello wykonano operację</span><span class="sxs-lookup"><span data-stu-id="a54cb-156">**Object Id** – **(can be empty)** hello object ID against which hello operation was performed</span></span>

   *  <span data-ttu-id="a54cb-157">Przykład — **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span><span class="sxs-lookup"><span data-stu-id="a54cb-157">Example – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span></span>

-   <span data-ttu-id="a54cb-158">**Szczegóły** — Witaj szczegółowy opis co nastąpiło w wyniku operacji hello</span><span class="sxs-lookup"><span data-stu-id="a54cb-158">**Details** – hello detailed description of what occurred as a result of hello operation</span></span>

   *  <span data-ttu-id="a54cb-159">Przykład — **wewnętrznego adresu url "http://bing.com/" jest nieprawidłowy, ponieważ jest już używana**</span><span class="sxs-lookup"><span data-stu-id="a54cb-159">Example – **Internal url 'http://bing.com/' is invalid since it is already in use**</span></span>

-   <span data-ttu-id="a54cb-160">**Błąd kopiowania** — kliknij hello **ikonę kopiowania** toohello rogu hello **błąd kopiowania** toocopy pole tekstowe wszystkich hello tooshare szczegóły powiadomienia o inżyniera grupa pomocy technicznej lub produktu</span><span class="sxs-lookup"><span data-stu-id="a54cb-160">**Copy error** – Click hello **copy icon** toohello right of hello **Copy error** textbox toocopy all hello notification details tooshare with a support or product group engineer</span></span>

   *  <span data-ttu-id="a54cb-161">Przykład```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span><span class="sxs-lookup"><span data-stu-id="a54cb-161">Example ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span></span>

## <a name="next-steps"></a><span data-ttu-id="a54cb-162">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a54cb-162">Next steps</span></span>
[<span data-ttu-id="a54cb-163">Zarządzanie aplikacjami przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a54cb-163">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)



