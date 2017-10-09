---
title: "aaaHow tooassign użytkowników i grup tooan aplikacji | Dokumentacja firmy Microsoft"
description: "Przypisywanie użytkowników toohello aplikacji toogrant dostępu"
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
ms.openlocfilehash: e039a26e4b8f88ad747354859f1071b8f74b6789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooassign-users-and-groups-tooan-application"></a><span data-ttu-id="65ac6-103">Jak aplikacja tooan tooassign użytkowników i grup</span><span class="sxs-lookup"><span data-stu-id="65ac6-103">How tooassign users and groups tooan application</span></span>

<span data-ttu-id="65ac6-104">Aby użytkownicy mogą wykonać żadnej z hello poniżej dla określonej aplikacji, musisz toofirst **przypisać je aplikacji toohello** toogrant im dostępu:</span><span class="sxs-lookup"><span data-stu-id="65ac6-104">Before your users can do any of hello below for a specific application, you need toofirst **assign them toohello application** toogrant them access:</span></span>

-   <span data-ttu-id="65ac6-105">Uzyskiwanie dostępu do aplikacji przez **Nawigacja bezpośrednio adres URL aplikacji toohello** (nazywany także inicjowane SP logowania jednokrotnego).</span><span class="sxs-lookup"><span data-stu-id="65ac6-105">Access an application by **navigating toohello application’s URL directly** (also known as SP-initiated sign-on).</span></span>

-   <span data-ttu-id="65ac6-106">Dostęp do aplikacji przy użyciu hello **adres URL dostępu użytkownika** w aplikacji **właściwości** strony (nazywany także inicjowane IDP logowania).</span><span class="sxs-lookup"><span data-stu-id="65ac6-106">Access an application by using hello **User Access URL** on an application’s **Properties** page (also known as IDP-initiated sign on).</span></span>

-   <span data-ttu-id="65ac6-107">Zobacz aplikacji są wyświetlane na ich [panelu dostępu aplikacji](https://myapps.microsoft.com/) lub aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="65ac6-107">See an application appear on their [Application Access Panel](https://myapps.microsoft.com/) or mobile application.</span></span>

-   <span data-ttu-id="65ac6-108">Zobacz aplikacji są wyświetlane na ich [uruchamiający aplikację usługi Office 365](https://support.office.com/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a).</span><span class="sxs-lookup"><span data-stu-id="65ac6-108">See an application appear on their [Office 365 Application Launcher](https://support.office.com/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a).</span></span>

## <a name="methods-tooassign-applications-with-azure-active-directory"></a><span data-ttu-id="65ac6-109">Metody tooassign aplikacji w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="65ac6-109">Methods tooassign applications with Azure Active Directory</span></span> 

<span data-ttu-id="65ac6-110">Istnieją 3 sposoby można przypisać aplikacji za pomocą usługi Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="65ac6-110">There are 3 ways you can assign applications with Azure Active Directory:</span></span>

-   [<span data-ttu-id="65ac6-111">Przypisywanie użytkownika bezpośrednio tooan aplikacji jako administrator</span><span class="sxs-lookup"><span data-stu-id="65ac6-111">Assign a user directly tooan application as an administrator</span></span>](#assign-a-user-directly-as-an-administrator)

-   [<span data-ttu-id="65ac6-112">Przypisz grupę bezpośrednio tooan aplikacji jako administrator</span><span class="sxs-lookup"><span data-stu-id="65ac6-112">Assign a group directly tooan application as an administrator</span></span>](#assign-a-group-directly-to-an-application-as-an-administrator)

-   [<span data-ttu-id="65ac6-113">Włączanie samoobsługi aplikacji dostępu tooallow użytkowników toofind własne aplikacje</span><span class="sxs-lookup"><span data-stu-id="65ac6-113">Enable self-service application access tooallow users toofind their own applications</span></span>](#enable-self-service-application-access-to-allow-users-to-find-their-own-applications)

## <a name="assign-a-user-directly-as-an-administrator"></a><span data-ttu-id="65ac6-114">Przypisywanie użytkownika bezpośrednio jako administrator</span><span class="sxs-lookup"><span data-stu-id="65ac6-114">Assign a user directly as an administrator</span></span>

<span data-ttu-id="65ac6-115">tooassign jednej lub kilku użytkowników aplikacji tooan bezpośrednio, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="65ac6-115">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="65ac6-116">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="65ac6-116">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="65ac6-117">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="65ac6-117">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="65ac6-118">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="65ac6-118">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="65ac6-119">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="65ac6-119">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="65ac6-120">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="65ac6-120">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="65ac6-121">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="65ac6-121">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="65ac6-122">Wybierz aplikację hello ma tooassign listy hello toofrom użytkownika.</span><span class="sxs-lookup"><span data-stu-id="65ac6-122">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="65ac6-123">Po załadowaniu aplikacji hello, kliknij przycisk **użytkowników i grup** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="65ac6-123">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="65ac6-124">Kliknij przycisk hello **Dodaj** przycisk na powitania **użytkowników i grup** hello tooopen listy **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="65ac6-124">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="65ac6-125">Kliknij przycisk hello **użytkowników i grup** selektora z hello **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="65ac6-125">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="65ac6-126">Typ w hello **Pełna nazwa** lub **adres e-mail** użytkownika hello planuje się przypisanie do hello **wyszukiwanie według nazwy lub adresu e-mail** pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="65ac6-126">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="65ac6-127">Umieść kursor nad hello **użytkownika** w tooreveal listy hello **wyboru**.</span><span class="sxs-lookup"><span data-stu-id="65ac6-127">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="65ac6-128">Kliknij przycisk hello wyboru dalej toohello użytkownika profilu zdjęcie lub logo tooadd Twojego toohello użytkownika **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="65ac6-128">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="65ac6-129">**Opcjonalnie:** Jeśli chcesz zbyt**dodać więcej niż jednego użytkownika**, typu w innym **Pełna nazwa** lub **adres e-mail** do hello **wyszukiwania według nazwy lub adresu e-mail** polu wyszukiwania, a następnie kliknij przycisk tooadd wyboru hello toohello tego użytkownika **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="65ac6-129">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="65ac6-130">Po wybraniu użytkowników, kliknij przycisk hello **wybierz** tooadd przycisk ich toohello listę użytkowników i grup toobe przypisane toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="65ac6-130">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="65ac6-131">**Opcjonalnie:** kliknij hello **wybierz rolę** selektora w hello **Dodaj przydziału** tooselect bloku roli użytkowników toohello tooassign wybrano.</span><span class="sxs-lookup"><span data-stu-id="65ac6-131">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="65ac6-132">Kliknij przycisk hello **przypisać** toohello aplikacji hello tooassign przycisk wybranych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="65ac6-132">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="65ac6-133">Po krótkim czasie użytkownicy hello, wybranych będą mogli toolaunch te aplikacje przy użyciu hello metod opisanych w sekcji Opis rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="65ac6-133">After a short period of time, hello users you have selected be able toolaunch these applications using hello methods described in hello solution description section.</span></span>

## <a name="assign-a-group-directly-tooan-application-as-an-administrator"></a><span data-ttu-id="65ac6-134">Przypisz grupę bezpośrednio tooan aplikacji jako administrator</span><span class="sxs-lookup"><span data-stu-id="65ac6-134">Assign a group directly tooan application as an administrator</span></span>

<span data-ttu-id="65ac6-135">tooassign jeden lub więcej grup tooan aplikacji bezpośrednio, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="65ac6-135">tooassign one or more groups tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="65ac6-136">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="65ac6-136">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="65ac6-137">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="65ac6-137">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="65ac6-138">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="65ac6-138">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="65ac6-139">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="65ac6-139">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="65ac6-140">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="65ac6-140">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="65ac6-141">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="65ac6-141">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="65ac6-142">Wybierz aplikację hello ma tooassign listy hello toofrom użytkownika.</span><span class="sxs-lookup"><span data-stu-id="65ac6-142">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="65ac6-143">Po załadowaniu aplikacji hello, kliknij przycisk **użytkowników i grup** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="65ac6-143">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="65ac6-144">Kliknij przycisk hello **Dodaj** przycisk na powitania **użytkowników i grup** hello tooopen listy **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="65ac6-144">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="65ac6-145">Kliknij przycisk hello **użytkowników i grup** selektora z hello **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="65ac6-145">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="65ac6-146">Typ w hello **grupy Pełna nazwa** grupy hello planuje się przypisanie do hello **wyszukiwanie według nazwy lub adresu e-mail** pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="65ac6-146">Type in hello **full group name** of hello group you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="65ac6-147">Umieść kursor nad hello **grupy** w tooreveal listy hello **wyboru**.</span><span class="sxs-lookup"><span data-stu-id="65ac6-147">Hover over hello **group** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="65ac6-148">Kliknij przycisk hello wyboru dalej toohello grupy profilu zdjęcie lub logo tooadd Twojego toohello użytkownika **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="65ac6-148">Click hello checkbox next toohello group’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="65ac6-149">**Opcjonalnie:** czy zbyt**dodać więcej niż jednej grupy**, typu w innym **grupy Pełna nazwa** do hello **wyszukiwanie według nazwy lub adresu e-mail** pole wyszukiwania, i kliknij przycisk tooadd wyboru hello toohello tej grupy **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="65ac6-149">**Optional:** If you would like too**add more than one group**, type in another **full group name** into hello **Search by name or email address** search box, and click hello checkbox tooadd this group toohello **Selected** list.</span></span>

13. <span data-ttu-id="65ac6-150">Po wybraniu grup kliknij hello **wybierz** tooadd przycisk ich toohello listę użytkowników i grup toobe przypisane toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="65ac6-150">When you are finished selecting groups, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="65ac6-151">**Opcjonalnie:** kliknij hello **wybierz rolę** selektora w hello **Dodaj przydziału** grupach bloku tooselect toohello tooassign roli zostały wybrane.</span><span class="sxs-lookup"><span data-stu-id="65ac6-151">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello groups you have selected.</span></span>

15. <span data-ttu-id="65ac6-152">Kliknij przycisk hello **przypisać** toohello aplikacji hello tooassign przycisk wybrane grupy.</span><span class="sxs-lookup"><span data-stu-id="65ac6-152">Click hello **Assign** button tooassign hello application toohello selected groups.</span></span>

<span data-ttu-id="65ac6-153">Po krótkim czasie hello użytkowników w grupach hello, który wybrano będzie stanie toolaunch te aplikacje przy użyciu hello metod opisanych w sekcji Opis rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="65ac6-153">After a short period of time, hello users within hello groups you have selected be able toolaunch these applications using hello methods described in hello solution description section.</span></span> <span data-ttu-id="65ac6-154">Jeśli są one grup dynamicznych, mogą występować pewne opóźnienie dodatkowego przetwarzania w tych przydziałów dla użytkowników w tych przypisanych grup.</span><span class="sxs-lookup"><span data-stu-id="65ac6-154">If these are dynamic groups, there may be some additional processing delay in these assignments appearing for users within these assigned groups.</span></span>

## <a name="enable-self-service-application-access-tooallow-users-toofind-their-own-applications"></a><span data-ttu-id="65ac6-155">Włączanie samoobsługi aplikacji dostępu tooallow użytkowników toofind własne aplikacje</span><span class="sxs-lookup"><span data-stu-id="65ac6-155">Enable self-service application access tooallow users toofind their own applications</span></span>

<span data-ttu-id="65ac6-156">Dostęp do aplikacji Sklep internetowy jest doskonałym sposobem tooallow użytkowników tooself — odnajdywanie aplikacji, opcjonalnie zezwolić na dostęp tooapprove grupy biznesowej hello toothose aplikacji.</span><span class="sxs-lookup"><span data-stu-id="65ac6-156">Self-service application access is a great way tooallow users tooself-discover applications, optionally allow hello business group tooapprove access toothose applications.</span></span> <span data-ttu-id="65ac6-157">Możesz zezwolić hello biznesowa grupy toomanage hello poświadczeń przypisanych użytkowników toothose jednokrotnego hasła w aplikacji bezpośrednio w ich panele dostępu.</span><span class="sxs-lookup"><span data-stu-id="65ac6-157">You can allow hello business group toomanage hello credentials assigned toothose users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="65ac6-158">tooenable samoobsługi aplikacji dostępu tooan aplikacji, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="65ac6-158">tooenable self-service application access tooan application, follow hello steps below:</span></span>

1.  <span data-ttu-id="65ac6-159">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="65ac6-159">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="65ac6-160">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="65ac6-160">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="65ac6-161">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="65ac6-161">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="65ac6-162">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="65ac6-162">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="65ac6-163">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="65ac6-163">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="65ac6-164">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="65ac6-164">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="65ac6-165">Wybierz aplikację hello tooenable samoobsługi dostępu toofrom hello listy.</span><span class="sxs-lookup"><span data-stu-id="65ac6-165">Select hello application you want tooenable Self-service access toofrom hello list.</span></span>

7.  <span data-ttu-id="65ac6-166">Po załadowaniu aplikacji hello, kliknij przycisk **samoobsługi** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="65ac6-166">Once hello application loads, click **Self-service** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="65ac6-167">tooenable dostęp do aplikacji Sklep internetowy dla tej aplikacji, Włącz hello **użytkownicy aplikacji toothis dostępu toorequest?** Przełącz zbyt**tak.**</span><span class="sxs-lookup"><span data-stu-id="65ac6-167">tooenable Self-service application access for this application, turn hello **Allow users toorequest access toothis application?** toggle too**Yes.**</span></span>

9.  <span data-ttu-id="65ac6-168">Następnie tooselect hello grupy toowhich użytkowników, którzy żądają dostępu do aplikacji toothis powinny zostać dodane, kliknij przycisk Dalej etykiety toohello hello selektora **toowhich grupy należy przypisać użytkownicy dodani?** i wybierz grupę.</span><span class="sxs-lookup"><span data-stu-id="65ac6-168">Next, tooselect hello group toowhich users who request access toothis application should be added, click hello selector next toohello label **toowhich group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="65ac6-169">**Opcjonalnie:** w razie potrzeby toorequire zatwierdzenia firm przed użytkownicy mogą uzyskiwać dostęp, należy ustawić hello **wymagają zatwierdzenia przed udzieleniem im dostępu do aplikacji toothis?** Przełącz zbyt**tak**.</span><span class="sxs-lookup"><span data-stu-id="65ac6-169">**Optional:** If you wish toorequire a business approval before users are allowed access, set hello **Require approval before granting access toothis application?** toggle too**Yes**.</span></span>

11. <span data-ttu-id="65ac6-170">**Opcjonalnie: dla aplikacji za pomocą hasła jednokrotnego na tylko** w razie potrzeby tooallow tych firm osób zatwierdzających toospecify hello haseł, które są wysyłane toothis aplikacji dla zatwierdzonych użytkowników ustawić hello **tooset osób zatwierdzających Zezwalaj hasła użytkownika dla tej aplikacji?**  Przełącz zbyt**tak**.</span><span class="sxs-lookup"><span data-stu-id="65ac6-170">**Optional: For applications using password single-sign on only,** if you wish tooallow those business approvers toospecify hello passwords that are sent toothis application for approved users, set hello **Allow approvers tooset user’s passwords for this application?** toggle too**Yes**.</span></span>

12. <span data-ttu-id="65ac6-171">**Opcjonalnie:** toospecify hello biznesowe osoby zatwierdzające mogą tooapprove dostępu toothis aplikacji, kliknij przycisk Dalej etykiety toohello hello selektora **użytkowników, którzy mają tooapprove dostępu toothis aplikacji?** tooselect w górę too10 biznesowe poszczególnych osób zatwierdzających.</span><span class="sxs-lookup"><span data-stu-id="65ac6-171">**Optional:** toospecify hello business approvers who are allowed tooapprove access toothis application, click hello selector next toohello label **Who is allowed tooapprove access toothis application?** tooselect up too10 individual business approvers.</span></span>

  >[!NOTE]
  ><span data-ttu-id="65ac6-172">Grupy nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="65ac6-172">Groups are not supported.</span></span>
  >
  >

13. <span data-ttu-id="65ac6-173">**Opcjonalnie:** **dla aplikacji, które ujawnia ról**, jeśli chcesz, aby tooassign roli tooa zatwierdzonych użytkowników samoobsługi, kliknij przycisk Dalej toohello selektora hello **toowhich roli należy przypisać użytkowników na tym aplikacji?**  tooselect hello roli toowhich powinien być przypisany tych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="65ac6-173">**Optional:** **For applications which expose roles**, if you wish tooassign self-service approved users tooa role, click hello selector next toohello **toowhich role should users be assigned in this application?** tooselect hello role toowhich these users should be assigned.</span></span>

14. <span data-ttu-id="65ac6-174">Kliknij przycisk hello **zapisać** przycisk u góry hello hello toofinish bloku.</span><span class="sxs-lookup"><span data-stu-id="65ac6-174">Click hello **Save** button at hello top of hello blade toofinish.</span></span>

<span data-ttu-id="65ac6-175">Po zakończeniu konfiguracji samoobsługi aplikacji, użytkownicy mogą przechodzić tootheir [panelu dostępu aplikacji](https://myapps.microsoft.com/) i kliknij przycisk hello **+ Dodaj** przycisk toofind hello aplikacji toowhich włączono Dostęp z samoobsługi.</span><span class="sxs-lookup"><span data-stu-id="65ac6-175">Once you complete Self-service application configuration, users can navigate tootheir [Application Access Panel](https://myapps.microsoft.com/) and click hello **+Add** button toofind hello apps toowhich you have enabled Self-service access.</span></span> <span data-ttu-id="65ac6-176">Osób zatwierdzających firm również wyświetlone powiadomienie w ich [panelu dostępu aplikacji](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="65ac6-176">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="65ac6-177">Można włączyć wiadomość e-mail z informacją, gdy użytkownik zażąda dostępu tooan aplikację, która wymaga zatwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="65ac6-177">You can enable an email notifying them when a user has requested access tooan application that requires their approval.</span></span> 

<span data-ttu-id="65ac6-178">Te zatwierdzenia obsługuje pojedynczy przepływów pracy, co oznacza, że jeśli określisz wiele osób zatwierdzających żadnych jedna osoba zatwierdzająca może aplikacji toohello dostęp osoby zatwierdzającej.</span><span class="sxs-lookup"><span data-stu-id="65ac6-178">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approver access toohello application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65ac6-179">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="65ac6-179">Next steps</span></span>
[<span data-ttu-id="65ac6-180">Podaj aplikacji tooyour rejestracji jednokrotnej z serwerem Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="65ac6-180">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
