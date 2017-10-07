---
title: 'Samouczek: Integracji Azure Active Directory z Qualtrics | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak toouse Qualtrics z usługą Azure Active Directory tooenable pojedynczy logowania jednokrotnego, automatyczne Inicjowanie obsługi i inne!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 4df889ab-2685-4d15-a163-1ba26567eeda
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 941642e74b90bb13a5ce37ce6665cfa32cd86016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qualtrics"></a><span data-ttu-id="5e702-103">Samouczek: Integracji Azure Active Directory z Qualtrics</span><span class="sxs-lookup"><span data-stu-id="5e702-103">Tutorial: Azure Active Directory integration with Qualtrics</span></span>
<span data-ttu-id="5e702-104">Celem Hello tego samouczka jest tooshow integracji hello Azure i Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="5e702-104">hello objective of this tutorial is tooshow hello integration of Azure and Qualtrics.</span></span>  

<span data-ttu-id="5e702-105">Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="5e702-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="5e702-106">Ważnej subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="5e702-106">A valid Azure subscription</span></span>
* <span data-ttu-id="5e702-107">Qualtrics rejestracji jednokrotnej (SSO) włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="5e702-107">A Qualtrics single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="5e702-108">Ten samouczek użytkownicy hello Azure AD przypisano tooQualtrics będą mogli toosingle logowania do aplikacji hello w witrynie firmy Qualtrics (usługa zainicjował dostawcy logowania) lub przy użyciu hello [toohello wprowadzenie Dostęp do panelu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5e702-108">After completing this tutorial, hello Azure AD users you have assigned tooQualtrics will be able toosingle sign into hello application at your Qualtrics company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="5e702-109">Scenariusz Hello opisane w tym samouczku składa się z powitania po bloków konstrukcyjnych:</span><span class="sxs-lookup"><span data-stu-id="5e702-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="5e702-110">Włączanie integracji aplikacji hello dla Qualtrics</span><span class="sxs-lookup"><span data-stu-id="5e702-110">Enabling hello application integration for Qualtrics</span></span>
2. <span data-ttu-id="5e702-111">Konfigurowanie rejestracji jednokrotnej (SSO)</span><span class="sxs-lookup"><span data-stu-id="5e702-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="5e702-112">Konfigurowanie Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="5e702-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="5e702-113">Przypisywanie użytkowników</span><span class="sxs-lookup"><span data-stu-id="5e702-113">Assigning users</span></span>

<span data-ttu-id="5e702-114">![Scenariusz](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "scenariusza")</span><span class="sxs-lookup"><span data-stu-id="5e702-114">![Scenario](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "Scenario")</span></span>

## <a name="enabling-hello-application-integration-for-qualtrics"></a><span data-ttu-id="5e702-115">Włączanie integracji aplikacji hello dla Qualtrics</span><span class="sxs-lookup"><span data-stu-id="5e702-115">Enabling hello application integration for Qualtrics</span></span>
<span data-ttu-id="5e702-116">Celem Hello w tej sekcji jest toooutline sposób integracji aplikacji hello tooenable dla Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="5e702-116">hello objective of this section is toooutline how tooenable hello application integration for Qualtrics.</span></span>

<span data-ttu-id="5e702-117">**integracji aplikacji hello tooenable dla Qualtrics, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="5e702-117">**tooenable hello application integration for Qualtrics, perform hello following steps:**</span></span>

1. <span data-ttu-id="5e702-118">W hello klasycznego portalu Azure, w okienku nawigacji po lewej stronie powitania kliknij **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5e702-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="5e702-119">![Usługi Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "usługi Active Directory")</span><span class="sxs-lookup"><span data-stu-id="5e702-119">![Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="5e702-120">Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="5e702-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="5e702-121">Kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.</span><span class="sxs-lookup"><span data-stu-id="5e702-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="5e702-122">![Aplikacje](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "aplikacji")</span><span class="sxs-lookup"><span data-stu-id="5e702-122">![Applications](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="5e702-123">Kliknij przycisk **Dodaj** u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="5e702-123">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="5e702-124">![Dodaj aplikację](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "Dodaj aplikację")</span><span class="sxs-lookup"><span data-stu-id="5e702-124">![Add application](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="5e702-125">Na powitania **co chcesz toodo** okna dialogowego, kliknij przycisk **dodać aplikację z galerii hello**.</span><span class="sxs-lookup"><span data-stu-id="5e702-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="5e702-126">![Dodawanie aplikacji z gallerry](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "dodać aplikację z gallerry")</span><span class="sxs-lookup"><span data-stu-id="5e702-126">![Add an application from gallerry](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="5e702-127">W hello **pole wyszukiwania**, typ **Qualtrics**.</span><span class="sxs-lookup"><span data-stu-id="5e702-127">In hello **search box**, type **Qualtrics**.</span></span>
   
   <span data-ttu-id="5e702-128">![Galerii aplikacji](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "galerii aplikacji")</span><span class="sxs-lookup"><span data-stu-id="5e702-128">![Application Gallery](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "Application Gallery")</span></span>
7. <span data-ttu-id="5e702-129">Wybierz w okienku wyników hello **Qualtrics**, a następnie kliknij przycisk **Complete** aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="5e702-129">In hello results pane, select **Qualtrics**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="5e702-130">![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")</span><span class="sxs-lookup"><span data-stu-id="5e702-130">![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="5e702-131">Konfigurowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5e702-131">Configure single sign-on</span></span>

<span data-ttu-id="5e702-132">Celem Hello w tej sekcji jest toooutline jak tooenable użytkowników tooauthenticate tooQualtrics do swojego konta w usłudze Azure AD przy użyciu Federacji oparte na powitania protokołu SAML.</span><span class="sxs-lookup"><span data-stu-id="5e702-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooQualtrics with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="5e702-133">**tooconfigure logowanie jednokrotne, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="5e702-133">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="5e702-134">W hello klasycznego portalu Azure na powitania **Qualtrics** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** tooopen hello **skonfigurować rejestrację jednokrotną** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5e702-134">In hello Azure classic portal, on hello **Qualtrics** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="5e702-135">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="5e702-135">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="5e702-136">Na powitania **jak ma toosign użytkowników na tooQualtrics** wybierz pozycję **usługi Microsoft Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="5e702-136">On hello **How would you like users toosign on tooQualtrics** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="5e702-137">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="5e702-137">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="5e702-138">Na powitania **Konfigurowanie adresu URL aplikacji** strony w hello **Qualtrics na adres URL logowania** pole tekstowe, wpisz adres URL (np.: "*https://ssotest2ut1.qualtrics.com*"), a następnie kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="5e702-138">On hello **Configure App URL** page, in hello **Qualtrics Sign On URL** textbox, type your URL (e.g.: “*https://ssotest2ut1.qualtrics.com*"), and then click **Next**.</span></span>
   
   <span data-ttu-id="5e702-139">![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "skonfigurować adres URL aplikacji")</span><span class="sxs-lookup"><span data-stu-id="5e702-139">![Configure App URL](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "Configure App URL")</span></span>
4. <span data-ttu-id="5e702-140">Na powitania **skonfigurować logowanie jednokrotne w Qualtrics** kliknij przycisk **pobierania metadanych**, a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="5e702-140">On hello **Configure single sign-on at Qualtrics** page, click **Download metadata**, and then save hello metadata file on your computer.</span></span>
   
   <span data-ttu-id="5e702-141">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="5e702-141">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="5e702-142">Wyślij hello metadanych pliku toohello Qualtrics zespołem pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="5e702-142">Send hello metadata file toohello Qualtrics support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="5e702-143">Konfiguracja rejestracji Jednokrotnej Hello ma toobe wykonywane przez hello Qualtrics zespołem pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="5e702-143">hello SSO configuration has toobe performed by hello Qualtrics support team.</span></span> <span data-ttu-id="5e702-144">Otrzymasz powiadomienie, jak hello konfiguracji została ukończona.</span><span class="sxs-lookup"><span data-stu-id="5e702-144">You will get a notification as soon as hello configuration has been completed.</span></span>
   > 
   > 
6. <span data-ttu-id="5e702-145">Na powitania klasycznego portalu Azure, wybierz hello konfiguracji rejestracji jednokrotnej potwierdzenie, a następnie kliknij **Complete** tooclose hello **skonfigurować rejestrację jednokrotną** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5e702-145">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="5e702-146">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="5e702-146">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="5e702-147">Skonfiguruj Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="5e702-147">Configure user provisioning</span></span>

<span data-ttu-id="5e702-148">Nie ma elementu akcji można tooconfigure użytkownika inicjowania obsługi administracyjnej tooQualtrics.</span><span class="sxs-lookup"><span data-stu-id="5e702-148">There is no action item for you tooconfigure user provisioning tooQualtrics.</span></span> <span data-ttu-id="5e702-149">Gdy przypisany użytkownik podejmie próbę toolog do Qualtrics za pomocą panelu dostępu hello, Qualtrics sprawdza, czy istnieje hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5e702-149">When an assigned user tries toolog into Qualtrics using hello access panel, Qualtrics checks whether hello user exists.</span></span>  

<span data-ttu-id="5e702-150">Jeśli nie jest Brak konta użytkownika dostępny jeszcze, są tworzone przez Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="5e702-150">If there is no user account available yet, it is automatically created by Qualtrics.</span></span>

## <a name="assign-users"></a><span data-ttu-id="5e702-151">Przypisywanie użytkowników</span><span class="sxs-lookup"><span data-stu-id="5e702-151">Assign users</span></span>
<span data-ttu-id="5e702-152">tootest konfiguracji, należy toogrant hello Azure AD użytkownicy mają tooallow przy użyciu Twojej aplikacji tooit dostępu przez przypisywanie ich.</span><span class="sxs-lookup"><span data-stu-id="5e702-152">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="5e702-153">**tooassign tooQualtrics użytkowników, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="5e702-153">**tooassign users tooQualtrics, perform hello following steps:**</span></span>

1. <span data-ttu-id="5e702-154">W hello klasycznego portalu Azure Utwórz konto testu.</span><span class="sxs-lookup"><span data-stu-id="5e702-154">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="5e702-155">Na powitania **Qualtrics** strona integracji aplikacji, kliknij przycisk **przypisywać użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="5e702-155">On hello **Qualtrics** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="5e702-156">![Przypisywanie użytkowników](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "przypisywanie użytkowników")</span><span class="sxs-lookup"><span data-stu-id="5e702-156">![Assign Users](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "Assign Users")</span></span>
3. <span data-ttu-id="5e702-157">Wybierz użytkownika testowego, kliknij przycisk **przypisać**, a następnie kliknij przycisk **tak** tooconfirm przypisania.</span><span class="sxs-lookup"><span data-stu-id="5e702-157">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="5e702-158">![Tak](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "tak")</span><span class="sxs-lookup"><span data-stu-id="5e702-158">![Yes](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="5e702-159">Jeśli chcesz tootest ustawienia logowania jednokrotnego, otwórz hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="5e702-159">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="5e702-160">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5e702-160">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

