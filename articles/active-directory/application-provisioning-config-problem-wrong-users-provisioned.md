---
title: "aaaWrong zbiór użytkowników są udostępnione tooan usługi Azure AD galerii aplikacji | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toofind się, dlaczego inny zestaw użytkowników są udostępniane tooan aplikacji niż te, które miały"
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
ms.openlocfilehash: adb90b12a53fb3160ce2b73b2559df92b283438e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="wrong-set-of-users-are-being-provisioned-tooan-azure-ad-gallery-application"></a><span data-ttu-id="7bcad-103">Nieprawidłowy zestaw użytkowników są udostępnione tooan usługi Azure AD galerii aplikacji</span><span class="sxs-lookup"><span data-stu-id="7bcad-103">Wrong set of users are being provisioned tooan Azure AD Gallery application</span></span>

<span data-ttu-id="7bcad-104">Użytkowników, którzy są udostępnione toohello aplikacji głównie wynikają z których użytkownicy i grupy zostały **przypisane** toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7bcad-104">Which users are provisioned toohello app is primarily driven by which users and groups have been **assigned** toohello application.</span></span>

<span data-ttu-id="7bcad-105">Jak korzystać z zasobów hello poniżej toolearn toocheck, którzy użytkownicy i grupy z przypisanym tooan aplikacji w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7bcad-105">Use hello resources below toolearn how toocheck which users and groups have been assigned tooan application within Azure Active Directory.</span></span>

## <a name="assign-a-user-directly-as-an-administrator"></a><span data-ttu-id="7bcad-106">Przypisywanie użytkownika bezpośrednio jako administrator</span><span class="sxs-lookup"><span data-stu-id="7bcad-106">Assign a user directly as an administrator</span></span>

<span data-ttu-id="7bcad-107">tooassign jednej lub kilku użytkowników aplikacji tooan bezpośrednio, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="7bcad-107">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="7bcad-108">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="7bcad-108">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="7bcad-109">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="7bcad-109">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7bcad-110">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="7bcad-110">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7bcad-111">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7bcad-111">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7bcad-112">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7bcad-112">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="7bcad-113">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="7bcad-113">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="7bcad-114">Wybierz aplikację hello ma tooassign listy hello toofrom użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7bcad-114">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="7bcad-115">Po załadowaniu aplikacji hello, kliknij przycisk **użytkowników i grup** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7bcad-115">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="7bcad-116">Kliknij przycisk hello **Dodaj** przycisk na powitania **użytkowników i grup** hello tooopen listy **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="7bcad-116">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="7bcad-117">Kliknij przycisk hello **użytkowników i grup** selektora z hello **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="7bcad-117">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="7bcad-118">Typ w hello **Pełna nazwa** lub **adres e-mail** użytkownika hello planuje się przypisanie do hello **wyszukiwanie według nazwy lub adresu e-mail** pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="7bcad-118">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="7bcad-119">Umieść kursor nad hello **użytkownika** w tooreveal listy hello **wyboru**.</span><span class="sxs-lookup"><span data-stu-id="7bcad-119">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="7bcad-120">Kliknij przycisk hello wyboru dalej toohello użytkownika profilu zdjęcie lub logo tooadd Twojego toohello użytkownika **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="7bcad-120">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="7bcad-121">**Opcjonalnie:** Jeśli chcesz zbyt**dodać więcej niż jednego użytkownika**, typu w innym **Pełna nazwa** lub **adres e-mail** do hello **wyszukiwania według nazwy lub adresu e-mail** polu wyszukiwania, a następnie kliknij przycisk tooadd wyboru hello toohello tego użytkownika **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="7bcad-121">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="7bcad-122">Po wybraniu użytkowników, kliknij przycisk hello **wybierz** tooadd przycisk ich toohello listę użytkowników i grup toobe przypisane toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7bcad-122">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="7bcad-123">**Opcjonalnie:** kliknij hello **wybierz rolę** selektora w hello **Dodaj przydziału** tooselect bloku roli użytkowników toohello tooassign wybrano.</span><span class="sxs-lookup"><span data-stu-id="7bcad-123">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="7bcad-124">Kliknij przycisk hello **przypisać** toohello aplikacji hello tooassign przycisk wybranych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="7bcad-124">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="7bcad-125">Jeśli Inicjowanie obsługi administracyjnej jest skonfigurowana i uruchomiona już aplikację, nowi użytkownicy powinna być elastycznie tooan aplikacji w ciągu 10 minut.</span><span class="sxs-lookup"><span data-stu-id="7bcad-125">If provisioning is configured and already running for an app, new users should be provisioned tooan application in approximately 10 minutes.</span></span> <span data-ttu-id="7bcad-126">Sprawdź hello **dzienników inspekcji** szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="7bcad-126">Check hello **Audit Logs** for details.</span></span>

## <a name="assign-a-group-directly-tooan-application-as-an-administrator"></a><span data-ttu-id="7bcad-127">Przypisz grupę bezpośrednio tooan aplikacji jako administrator</span><span class="sxs-lookup"><span data-stu-id="7bcad-127">Assign a group directly tooan application as an administrator</span></span>

<span data-ttu-id="7bcad-128">tooassign jeden lub więcej grup tooan aplikacji bezpośrednio, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="7bcad-128">tooassign one or more groups tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="7bcad-129">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="7bcad-129">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="7bcad-130">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="7bcad-130">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7bcad-131">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="7bcad-131">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7bcad-132">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7bcad-132">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7bcad-133">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7bcad-133">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="7bcad-134">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="7bcad-134">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="7bcad-135">Wybierz aplikację hello ma tooassign listy hello toofrom użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7bcad-135">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="7bcad-136">Po załadowaniu aplikacji hello, kliknij przycisk **użytkowników i grup** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7bcad-136">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="7bcad-137">Kliknij przycisk hello **Dodaj** przycisk na powitania **użytkowników i grup** hello tooopen listy **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="7bcad-137">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="7bcad-138">Kliknij przycisk hello **użytkowników i grup** selektora z hello **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="7bcad-138">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="7bcad-139">Typ w hello **grupy Pełna nazwa** grupy hello planuje się przypisanie do hello **wyszukiwanie według nazwy lub adresu e-mail** pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="7bcad-139">Type in hello **full group name** of hello group you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="7bcad-140">Umieść kursor nad hello **grupy** w tooreveal listy hello **wyboru**.</span><span class="sxs-lookup"><span data-stu-id="7bcad-140">Hover over hello **group** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="7bcad-141">Kliknij przycisk hello wyboru dalej toohello grupy profilu zdjęcie lub logo tooadd Twojego toohello użytkownika **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="7bcad-141">Click hello checkbox next toohello group’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="7bcad-142">**Opcjonalnie:** czy zbyt**dodać więcej niż jednej grupy**, typu w innym **grupy Pełna nazwa** do hello **wyszukiwanie według nazwy lub adresu e-mail** pole wyszukiwania, i kliknij przycisk tooadd wyboru hello toohello tej grupy **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="7bcad-142">**Optional:** If you would like too**add more than one group**, type in another **full group name** into hello **Search by name or email address** search box, and click hello checkbox tooadd this group toohello **Selected** list.</span></span>

13. <span data-ttu-id="7bcad-143">Po wybraniu grup kliknij hello **wybierz** tooadd przycisk ich toohello listę użytkowników i grup toobe przypisane toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7bcad-143">When you are finished selecting groups, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="7bcad-144">**Opcjonalnie:** kliknij hello **wybierz rolę** selektora w hello **Dodaj przydziału** grupach bloku tooselect toohello tooassign roli zostały wybrane.</span><span class="sxs-lookup"><span data-stu-id="7bcad-144">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello groups you have selected.</span></span>

15. <span data-ttu-id="7bcad-145">Kliknij przycisk hello **przypisać** toohello aplikacji hello tooassign przycisk wybrane grupy.</span><span class="sxs-lookup"><span data-stu-id="7bcad-145">Click hello **Assign** button tooassign hello application toohello selected groups.</span></span>

<span data-ttu-id="7bcad-146">Jeśli Inicjowanie obsługi administracyjnej jest skonfigurowana i uruchomiona już aplikację, nowi użytkownicy, zawarte w grupie hello powinny być elastycznie tooan aplikacji w ciągu 10 minut.</span><span class="sxs-lookup"><span data-stu-id="7bcad-146">If provisioning is configured and already running for an app, new users contained within hello group should be provisioned tooan application in approximately 10 minutes.</span></span> <span data-ttu-id="7bcad-147">Sprawdź hello **dzienników inspekcji** szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="7bcad-147">Check hello **Audit Logs** for details.</span></span>

>[!IMPORTANT]
><span data-ttu-id="7bcad-148">Inicjowanie obsługi administracyjnej hello Nazwa grupy i grupowania szczegółów w elementach członkowskich toohello dodanie, jeśli obsługiwane w przypadku niektórych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7bcad-148">Provisioning of hello group name and group details, in addition toohello members, if supported for some applications.</span></span> <span data-ttu-id="7bcad-149">Można włączyć lub wyłączyć tę funkcję przez włączenie lub wyłączenie hello **mapowania** dla obiektów grupy pokazano hello **inicjowania obsługi administracyjnej** kartę.</span><span class="sxs-lookup"><span data-stu-id="7bcad-149">You can enable or disable this functionality by enabling or disabling hello **Mapping** for group objects shown in hello **Provisioning** tab.</span></span> 
>
>

<span data-ttu-id="7bcad-150">Jeśli inicjowania obsługi grup jest włączona, upewnij się, że tooreview hello atrybutu mapowania tooensure odpowiednie pole jest używany przez hello "zgodnym z Identyfikatorem".</span><span class="sxs-lookup"><span data-stu-id="7bcad-150">If provisioning groups is enabled, be sure tooreview hello attribute mappings tooensure an appropriate field is being used for hello “matching ID”.</span></span> <span data-ttu-id="7bcad-151">Może to być nazwa wyświetlana hello lub e-mail aliasu, jak hello grupy i jej elementów członkowskich nie można zainicjować obsługi administracyjnej Jeśli hello zgodnej właściwości jest pusta lub nie wypełnione grupy w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7bcad-151">This can be hello display name or email alias, as hello group and its members not be provisioned if hello matching property is empty or not populated for a group in Azure AD.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7bcad-152">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7bcad-152">Next steps</span></span>
[<span data-ttu-id="7bcad-153">Automatyzowanie Inicjowanie obsługi użytkowników i anulowania zastrzeżenia tooSaaS aplikacji za pomocą usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7bcad-153">Automate User Provisioning and Deprovisioning tooSaaS Applications with Azure Active Directory</span></span>](active-directory-saas-app-provisioning.md)
