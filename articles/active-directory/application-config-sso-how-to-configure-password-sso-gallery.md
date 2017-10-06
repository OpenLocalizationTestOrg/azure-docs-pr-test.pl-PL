---
title: "aaaHow tooconfigure hasło logowanie jednokrotne dla aplikacji w galerii Azure AD | Dokumentacja firmy Microsoft"
description: "Jak tooconfigure aplikację do zabezpieczania opartego na hasłach rejestracji jednokrotnej gdy już znajduje się w galerii aplikacji usługi Azure AD hello"
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
ms.openlocfilehash: 7a93bff119b477d946368686fc2d9006ca2722a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="8ae63-103">Jak hasło tooconfigure logowanie jednokrotne dla aplikacji w galerii Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ae63-103">How tooconfigure password single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="8ae63-104">Po dodaniu aplikacji z hello [galerii aplikacji usługi Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery), masz hello wybór sposobu toosign Twojego użytkowników w aplikacji toothat.</span><span class="sxs-lookup"><span data-stu-id="8ae63-104">When you add an application from hello [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery), you have hello choice of how you want your users toosign in toothat application.</span></span> <span data-ttu-id="8ae63-105">Ten wybór można skonfigurować w dowolnej chwili, wybierając hello **rejestracji jednokrotnej** element nawigacji w aplikacji przedsiębiorstwa w hello [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="8ae63-105">You can configure this choice at any time by selecting hello **Single Sign-on** navigation item on an Enterprise Application in hello [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="8ae63-106">Jeden z dostępnych tooyou metody rejestracji jednokrotnej hello jest hello [opartego na hasłach rejestracji jednokrotnej](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) opcji.</span><span class="sxs-lookup"><span data-stu-id="8ae63-106">One of hello single sign-on methods available tooyou is hello [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) option.</span></span> <span data-ttu-id="8ae63-107">Jest to doskonały sposób tooget uruchomiona szybko Integrowanie aplikacji z usługą Azure AD i umożliwia:</span><span class="sxs-lookup"><span data-stu-id="8ae63-107">This is a great way tooget started integrating applications into Azure AD quickly, and allows you to:</span></span>

-   <span data-ttu-id="8ae63-108">Włącz **rejestracji jednokrotnej dla użytkowników** bezpieczne przechowywanie i odtwarzanie nazwy użytkowników i hasła dla aplikacji hello zostały zintegrowane z usługą Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ae63-108">Enable **Single Sign-on for your users** by securely storing and replaying usernames and passwords for hello application you’ve integrated with Azure AD</span></span>

-   <span data-ttu-id="8ae63-109">**Obsługuje aplikacje, które wymagają wielu pól logowania** dla aplikacji, które wymagają więcej niż tylko nazwę użytkownika i hasło pola toosign w</span><span class="sxs-lookup"><span data-stu-id="8ae63-109">**Support applications that require multiple sign-in fields** for applications that require more than just username and password fields toosign in</span></span>

-   <span data-ttu-id="8ae63-110">**Dostosowywanie etykiet hello** hello nazwy użytkownika i hasła wejściowych użytkownicy zobaczą na powitania [panelu dostępu aplikacji](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) po oni wprowadzić swoje poświadczenia</span><span class="sxs-lookup"><span data-stu-id="8ae63-110">**Customize hello labels** of hello username and password input fields your users see on hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) when they enter their credentials</span></span>

-   <span data-ttu-id="8ae63-111">Zezwalaj na Twojej **użytkowników** tooprovide własne nazwy użytkowników i hasła dla wszystkich istniejących kont aplikacji wpisywania w ręcznie na powitania [Panel dostępu do aplikacji](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span><span class="sxs-lookup"><span data-stu-id="8ae63-111">Allow your **users** tooprovide their own usernames and passwords for any existing application accounts they are typing in manually on hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span></span>

-   <span data-ttu-id="8ae63-112">Zezwalaj na **grupy biznesowej hello** toospecify hello w nazwach użytkowników i haseł przypisany użytkownik tooa przy użyciu hello [samoobsługi dostęp do aplikacji](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) funkcji</span><span class="sxs-lookup"><span data-stu-id="8ae63-112">Allow a **member of hello business group** toospecify hello usernames and passwords assigned tooa user by using hello [Self-Service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) feature</span></span>

-   <span data-ttu-id="8ae63-113">Zezwalaj na **administratora** toospecify hello w nazwach użytkowników i haseł przypisany użytkownik tooa przy użyciu poświadczeń aktualizacji hello funkcji podczas [przypisywanie aplikacji tooan użytkownika](#assign-a-user-to-an-application-directly)</span><span class="sxs-lookup"><span data-stu-id="8ae63-113">Allow an **administrator** toospecify hello usernames and passwords assigned tooa user by using hello Update Credentials feature when [assigning a user tooan application](#assign-a-user-to-an-application-directly)</span></span>

-   <span data-ttu-id="8ae63-114">Zezwalaj na **administratora** toospecify hello udostępnionych w nazwa użytkownika lub hasło używane przez grupy osób przy użyciu poświadczeń aktualizacji hello funkcji podczas [przypisanie grupy aplikacji tooan](#assign-an-application-to-a-group-directly)</span><span class="sxs-lookup"><span data-stu-id="8ae63-114">Allow an **administrator** toospecify hello shared username or password used by a group of people by using hello Update Credentials feature when [assigning a group tooan application](#assign-an-application-to-a-group-directly)</span></span>

<span data-ttu-id="8ae63-115">Poniżej opisano, jak można włączyć [opartego na hasłach rejestracji jednokrotnej](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) tooan aplikacji, która jest już hello [galerii aplikacji usługi Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span><span class="sxs-lookup"><span data-stu-id="8ae63-115">Below describes how you can enable [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) tooan application that is already in hello [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="8ae63-116">Omówienie kroków wymaganych</span><span class="sxs-lookup"><span data-stu-id="8ae63-116">Overview of steps required</span></span>
<span data-ttu-id="8ae63-117">tooconfigure aplikację z galerii Azure AD hello należy:</span><span class="sxs-lookup"><span data-stu-id="8ae63-117">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="8ae63-118">Dodawanie aplikacji hello galerii Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ae63-118">Add an application from hello Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="8ae63-119">Konfigurowanie aplikacji hello dla hasła logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="8ae63-119">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="8ae63-120">Przypisz hello aplikacji tooa użytkownika lub grupy</span><span class="sxs-lookup"><span data-stu-id="8ae63-120">Assign hello application tooa user or a group</span></span>](#assign-the-application-to-a-user-or-a-group)

    -   [<span data-ttu-id="8ae63-121">Bezpośrednio przypisać aplikację tooan użytkownika</span><span class="sxs-lookup"><span data-stu-id="8ae63-121">Assign a user tooan application directly</span></span>](#assign-a-user-to-an-application-directly)

    -   [<span data-ttu-id="8ae63-122">Przypisz grupę tooa aplikacji bezpośrednio</span><span class="sxs-lookup"><span data-stu-id="8ae63-122">Assign an application tooa group directly</span></span>](#assign-an-application-to-a-group-directly)

## <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="8ae63-123">Dodawanie aplikacji hello galerii Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ae63-123">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="8ae63-124">tooadd aplikacji hello galerii Azure AD, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="8ae63-124">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="8ae63-125">Otwórz hello [Azure Portal](https://portal.azure.com) i zaloguj się jako **administratora globalnego** lub **współadministratora**</span><span class="sxs-lookup"><span data-stu-id="8ae63-125">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="8ae63-126">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="8ae63-126">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="8ae63-127">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="8ae63-127">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="8ae63-128">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8ae63-128">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="8ae63-129">Kliknij przycisk hello **Dodaj** przycisk na powitania prawym górnym rogu na powitania **aplikacje dla przedsiębiorstw** bloku</span><span class="sxs-lookup"><span data-stu-id="8ae63-129">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="8ae63-130">W hello **wprowadź nazwę** pole tekstowe z hello **Dodaj z galerii hello** sekcji, nazwa typu hello aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="8ae63-130">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application</span></span>

7.  <span data-ttu-id="8ae63-131">Wybierz hello aplikację tooconfigure dla rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8ae63-131">Select hello application you want tooconfigure for single sign-on</span></span>

8.  <span data-ttu-id="8ae63-132">Przed dodaniem aplikacji hello, można zmienić jego nazwę z hello **nazwa** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="8ae63-132">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="8ae63-133">Kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8ae63-133">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="8ae63-134">Po krótkim czasie można blok konfiguracji aplikacji hello toosee stanie.</span><span class="sxs-lookup"><span data-stu-id="8ae63-134">After a short period, you be able toosee hello application’s configuration blade.</span></span>

## <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="8ae63-135">Konfigurowanie aplikacji hello dla hasła logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="8ae63-135">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="8ae63-136">tooconfigure logowanie jednokrotne dla aplikacji, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="8ae63-136">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="8ae63-137">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="8ae63-137">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="8ae63-138">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="8ae63-138">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="8ae63-139">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="8ae63-139">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="8ae63-140">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8ae63-140">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="8ae63-141">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8ae63-141">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="8ae63-142">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="8ae63-142">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="8ae63-143">Wybierz hello aplikację tooconfigure rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8ae63-143">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="8ae63-144">Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8ae63-144">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="8ae63-145">Tryb wybierz hello **opartego na hasłach logowania jednokrotnego.**</span><span class="sxs-lookup"><span data-stu-id="8ae63-145">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="8ae63-146">[Przypisywanie użytkowników aplikacji toohello](#assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="8ae63-146">[Assign users toohello application](#assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="8ae63-147">Ponadto można też podać poświadczenia w imieniu użytkownika hello zaznaczania wierszy hello hello użytkowników i klikając **poświadczenia aktualizacji** i wprowadzając hello nazwy użytkownika i hasła w imieniu użytkowników hello.</span><span class="sxs-lookup"><span data-stu-id="8ae63-147">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="8ae63-148">W przeciwnym razie użytkownicy będą poświadczeń hello zostanie wyświetlony monit o tooenter, się po uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="8ae63-148">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="assign-a-user-tooan-application-directly"></a><span data-ttu-id="8ae63-149">Bezpośrednio przypisać aplikację tooan użytkownika</span><span class="sxs-lookup"><span data-stu-id="8ae63-149">Assign a user tooan application directly</span></span>

<span data-ttu-id="8ae63-150">tooassign jednej lub kilku użytkowników aplikacji tooan bezpośrednio, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="8ae63-150">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="8ae63-151">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="8ae63-151">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="8ae63-152">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="8ae63-152">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="8ae63-153">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="8ae63-153">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="8ae63-154">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8ae63-154">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="8ae63-155">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8ae63-155">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="8ae63-156">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="8ae63-156">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="8ae63-157">Wybierz aplikację hello ma tooassign listy hello toofrom użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8ae63-157">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="8ae63-158">Po załadowaniu aplikacji hello, kliknij przycisk **użytkowników i grup** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8ae63-158">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="8ae63-159">Kliknij przycisk hello **Dodaj** przycisk na powitania **użytkowników i grup** hello tooopen listy **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="8ae63-159">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="8ae63-160">Kliknij przycisk hello **użytkowników i grup** selektora z hello **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="8ae63-160">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="8ae63-161">Typ w hello **Pełna nazwa** lub **adres e-mail** użytkownika hello planuje się przypisanie do hello **wyszukiwanie według nazwy lub adresu e-mail** pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="8ae63-161">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="8ae63-162">Umieść kursor nad hello **użytkownika** w tooreveal listy hello **wyboru**.</span><span class="sxs-lookup"><span data-stu-id="8ae63-162">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="8ae63-163">Kliknij przycisk hello wyboru dalej toohello użytkownika profilu zdjęcie lub logo tooadd Twojego toohello użytkownika **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="8ae63-163">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="8ae63-164">**Opcjonalnie:** Jeśli chcesz zbyt**dodać więcej niż jednego użytkownika**, typu w innym **Pełna nazwa** lub **adres e-mail** do hello **wyszukiwania według nazwy lub adresu e-mail** polu wyszukiwania, a następnie kliknij przycisk tooadd wyboru hello toohello tego użytkownika **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="8ae63-164">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="8ae63-165">Po wybraniu użytkowników, kliknij przycisk hello **wybierz** tooadd przycisk ich toohello listę użytkowników i grup toobe przypisane toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8ae63-165">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="8ae63-166">**Opcjonalnie:** kliknij hello **wybierz rolę** selektora w hello **Dodaj przydziału** tooselect bloku roli użytkowników toohello tooassign wybrano.</span><span class="sxs-lookup"><span data-stu-id="8ae63-166">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="8ae63-167">Kliknij przycisk hello **przypisać** toohello aplikacji hello tooassign przycisk wybranych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="8ae63-167">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

## <a name="assign-an-application-tooa-group-directly"></a><span data-ttu-id="8ae63-168">Przypisz grupę tooa aplikacji bezpośrednio</span><span class="sxs-lookup"><span data-stu-id="8ae63-168">Assign an application tooa group directly</span></span>

<span data-ttu-id="8ae63-169">tooassign jeden lub więcej grup tooan aplikacji bezpośrednio, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="8ae63-169">tooassign one or more groups tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="8ae63-170">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="8ae63-170">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="8ae63-171">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="8ae63-171">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="8ae63-172">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="8ae63-172">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="8ae63-173">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8ae63-173">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="8ae63-174">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8ae63-174">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="8ae63-175">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="8ae63-175">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="8ae63-176">Wybierz aplikację hello ma tooassign listy hello toofrom użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8ae63-176">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="8ae63-177">Po załadowaniu aplikacji hello, kliknij przycisk **użytkowników i grup** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8ae63-177">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="8ae63-178">Kliknij przycisk hello **Dodaj** przycisk na powitania **użytkowników i grup** hello tooopen listy **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="8ae63-178">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="8ae63-179">Kliknij przycisk hello **użytkowników i grup** selektora z hello **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="8ae63-179">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="8ae63-180">Typ w hello **grupy Pełna nazwa** grupy hello planuje się przypisanie do hello **wyszukiwanie według nazwy lub adresu e-mail** pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="8ae63-180">Type in hello **full group name** of hello group you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="8ae63-181">Umieść kursor nad hello **grupy** w tooreveal listy hello **wyboru**.</span><span class="sxs-lookup"><span data-stu-id="8ae63-181">Hover over hello **group** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="8ae63-182">Kliknij przycisk hello wyboru dalej toohello grupy profilu zdjęcie lub logo tooadd Twojego toohello użytkownika **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="8ae63-182">Click hello checkbox next toohello group’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="8ae63-183">**Opcjonalnie:** czy zbyt**dodać więcej niż jednej grupy**, typu w innym **grupy Pełna nazwa** do hello **wyszukiwanie według nazwy lub adresu e-mail** pole wyszukiwania, i kliknij przycisk tooadd wyboru hello toohello tej grupy **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="8ae63-183">**Optional:** If you would like too**add more than one group**, type in another **full group name** into hello **Search by name or email address** search box, and click hello checkbox tooadd this group toohello **Selected** list.</span></span>

13. <span data-ttu-id="8ae63-184">Po wybraniu grup kliknij hello **wybierz** tooadd przycisk ich toohello listę użytkowników i grup toobe przypisane toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8ae63-184">When you are finished selecting groups, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="8ae63-185">**Opcjonalnie:** kliknij hello **wybierz rolę** selektora w hello **Dodaj przydziału** grupach bloku tooselect toohello tooassign roli zostały wybrane.</span><span class="sxs-lookup"><span data-stu-id="8ae63-185">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello groups you have selected.</span></span>

15. <span data-ttu-id="8ae63-186">Kliknij przycisk hello **przypisać** toohello aplikacji hello tooassign przycisk wybrane grupy.</span><span class="sxs-lookup"><span data-stu-id="8ae63-186">Click hello **Assign** button tooassign hello application toohello selected groups.</span></span>

<span data-ttu-id="8ae63-187">Po krótkim hello użytkowników, dla których wybrano być stanie toolaunch tych aplikacji w hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="8ae63-187">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8ae63-188">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8ae63-188">Next steps</span></span>
[<span data-ttu-id="8ae63-189">Podaj aplikacji tooyour rejestracji jednokrotnej z serwerem Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="8ae63-189">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
