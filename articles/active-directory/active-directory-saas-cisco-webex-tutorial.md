---
title: "Samouczek: Integracji usługi Azure Active Directory z Cisco Webex | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse Cisco Webex z usługą Azure Active Directory tooenable pojedynczy logowania jednokrotnego, automatyczne Inicjowanie obsługi i inne!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 26704ca7-13ed-4261-bf24-fd6252e2072b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 9fc11e58a7acaa6fbfb32eeccbfbf85984950e67
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-webex"></a><span data-ttu-id="38830-103">Samouczek: Integracji usługi Azure Active Directory z Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="38830-103">Tutorial: Azure Active Directory Integration with Cisco Webex</span></span>
<span data-ttu-id="38830-104">Celem Hello tego samouczka jest tooshow integracji hello Azure i Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="38830-104">hello objective of this tutorial is tooshow hello integration of Azure and Cisco Webex.</span></span>  
<span data-ttu-id="38830-105">Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="38830-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="38830-106">Ważnej subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="38830-106">A valid Azure subscription</span></span>
* <span data-ttu-id="38830-107">Dzierżawy Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="38830-107">A Cisco Webex tenant</span></span>

<span data-ttu-id="38830-108">Ten samouczek hello użytkowników usługi Azure AD przypisano tooCisco Webex będą mogli toosingle logowania do aplikacji hello w witrynie firmy Cisco Webex (usługa zainicjował dostawcy logowania) lub przy użyciu hello [toohello wprowadzenie Dostęp do panelu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="38830-108">After completing this tutorial, hello Azure AD users you have assigned tooCisco Webex will be able toosingle sign into hello application at your Cisco Webex company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="38830-109">Scenariusz Hello opisane w tym samouczku składa się z powitania po bloków konstrukcyjnych:</span><span class="sxs-lookup"><span data-stu-id="38830-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

* <span data-ttu-id="38830-110">Włączanie integracji aplikacji hello dla Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="38830-110">Enabling hello application integration for Cisco Webex</span></span>
* <span data-ttu-id="38830-111">Konfigurowanie rejestracji jednokrotnej (SSO)</span><span class="sxs-lookup"><span data-stu-id="38830-111">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="38830-112">Konfigurowanie Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="38830-112">Configuring user provisioning</span></span>
* <span data-ttu-id="38830-113">Przypisywanie użytkowników</span><span class="sxs-lookup"><span data-stu-id="38830-113">Assigning users</span></span>

<span data-ttu-id="38830-114">![Scenariusz](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "scenariusza")</span><span class="sxs-lookup"><span data-stu-id="38830-114">![Scenario](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-cisco-webex"></a><span data-ttu-id="38830-115">Włącz integrację aplikacji hello dla Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="38830-115">Enable hello application integration for Cisco Webex</span></span>
<span data-ttu-id="38830-116">Celem Hello w tej sekcji jest toooutline sposób integracji aplikacji hello tooenable dla Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="38830-116">hello objective of this section is toooutline how tooenable hello application integration for Cisco Webex.</span></span>

<span data-ttu-id="38830-117">**Integracja aplikacji hello tooenable dla Cisco Webex wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="38830-117">**tooenable hello application integration for Cisco Webex, perform hello following steps:**</span></span>

1. <span data-ttu-id="38830-118">W hello klasycznego portalu Azure, w okienku nawigacji po lewej stronie powitania kliknij **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="38830-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="38830-119">![Usługi Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "usługi Active Directory")</span><span class="sxs-lookup"><span data-stu-id="38830-119">![Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="38830-120">Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="38830-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="38830-121">Kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.</span><span class="sxs-lookup"><span data-stu-id="38830-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="38830-122">![Aplikacje](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "aplikacji")</span><span class="sxs-lookup"><span data-stu-id="38830-122">![Applications](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="38830-123">Kliknij przycisk **Dodaj** u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="38830-123">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="38830-124">![Dodaj aplikację](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "Dodaj aplikację")</span><span class="sxs-lookup"><span data-stu-id="38830-124">![Add application](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="38830-125">Na powitania **co chcesz toodo** okna dialogowego, kliknij przycisk **dodać aplikację z galerii hello**.</span><span class="sxs-lookup"><span data-stu-id="38830-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="38830-126">![Dodawanie aplikacji z gallerry](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "dodać aplikację z gallerry")</span><span class="sxs-lookup"><span data-stu-id="38830-126">![Add an application from gallerry](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="38830-127">W hello **pole wyszukiwania**, typ **Cisco Webex**.</span><span class="sxs-lookup"><span data-stu-id="38830-127">In hello **search box**, type **Cisco Webex**.</span></span>
   
   <span data-ttu-id="38830-128">![Galerii aplikacji](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "galerii aplikacji")</span><span class="sxs-lookup"><span data-stu-id="38830-128">![Application Gallery](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "Application Gallery")</span></span>
7. <span data-ttu-id="38830-129">Wybierz w okienku wyników hello **Cisco Webex**, a następnie kliknij przycisk **Complete** aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="38830-129">In hello results pane, select **Cisco Webex**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="38830-130">![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")</span><span class="sxs-lookup"><span data-stu-id="38830-130">![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="38830-131">Konfigurowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="38830-131">Configure single sign-on</span></span>

<span data-ttu-id="38830-132">Celem Hello w tej sekcji jest toooutline jak tooenable użytkowników tooauthenticate tooCisco Webex do swojego konta w usłudze Azure AD przy użyciu Federacji oparte na powitania protokołu SAML.</span><span class="sxs-lookup"><span data-stu-id="38830-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooCisco Webex with their account in Azure AD using federation based on hello SAML protocol.</span></span>  

<span data-ttu-id="38830-133">W ramach tej procedury jest wymagana toocreate zakodowanego certyfikatu base-64.</span><span class="sxs-lookup"><span data-stu-id="38830-133">As part of this procedure, you are required toocreate a base-64 encoded certificate.</span></span> <span data-ttu-id="38830-134">Jeśli nie masz doświadczenia z tej procedury, zobacz [jak tooconvert pliku binarnego certyfikatu do pliku tekstowego](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="38830-134">If you are not familiar with this procedure, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>

<span data-ttu-id="38830-135">**tooconfigure logowanie jednokrotne, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="38830-135">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="38830-136">W hello klasycznego portalu Azure na powitania **Cisco Webex** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** tooopen hello **skonfigurować rejestrację jednokrotną** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="38830-136">In hello Azure classic portal, on hello **Cisco Webex** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="38830-137">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="38830-137">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="38830-138">Na powitania **jak ma toosign użytkowników na tooCisco Webex** wybierz pozycję **usługi Microsoft Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="38830-138">On hello **How would you like users toosign on tooCisco Webex** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="38830-139">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="38830-139">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="38830-140">Na powitania **Konfigurowanie adresu URL aplikacji** , wykonaj następujące kroki hello, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="38830-140">On hello **Configure App URL** page, perform hello following steps, and then click **Next**.</span></span>
   
   <span data-ttu-id="38830-141">![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "skonfigurować adres URL aplikacji")</span><span class="sxs-lookup"><span data-stu-id="38830-141">![Configure app URL](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "Configure app URL")</span></span>   
   1. <span data-ttu-id="38830-142">W hello **rejestrują na adres URL** tekstowym, wpisz adres URL dzierżawy Cisco Webex (np.: *http://contoso.webex.com*).</span><span class="sxs-lookup"><span data-stu-id="38830-142">In hello **Sing On URL** textbox, type your Cisco Webex tenant URL (e.g.: *http://contoso.webex.com*).</span></span>
   2. <span data-ttu-id="38830-143">W hello **adres URL odpowiedzi Webex Cisco** pole tekstowe, typ użytkownika **adres URL AssertionConsumerService Webex Cisco** (np.: *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company* ).</span><span class="sxs-lookup"><span data-stu-id="38830-143">In hello **Cisco Webex Reply URL** textbox, type your **Cisco Webex AssertionConsumerService URL** (e.g.: *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company*).</span></span>
4. <span data-ttu-id="38830-144">Na powitania **skonfigurować logowanie jednokrotne w Cisco Webex** strony, toodownload certyfikat, kliknij przycisk **pobierania certyfikatu**, a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="38830-144">On hello **Configure single sign-on at Cisco Webex** page, toodownload your certificate, click **Download certificate**, and then save hello certificate file on your computer.</span></span>
   
   <span data-ttu-id="38830-145">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="38830-145">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="38830-146">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy Cisco Webex jako administrator.</span><span class="sxs-lookup"><span data-stu-id="38830-146">In a different web browser window, log into your Cisco Webex company site as an administrator.</span></span>
6. <span data-ttu-id="38830-147">W menu hello na górze hello, kliknij przycisk **administrowania lokacją**.</span><span class="sxs-lookup"><span data-stu-id="38830-147">In hello menu on hello top, click **Site Administration**.</span></span>
   
   <span data-ttu-id="38830-148">![Administrowanie lokacją](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "lokacji administracyjnej")</span><span class="sxs-lookup"><span data-stu-id="38830-148">![Site Administration](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "Site Administration")</span></span>
7. <span data-ttu-id="38830-149">W hello **zarządzania witryną** kliknij **konfiguracji logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="38830-149">In hello **Manage Site** section, click **SSO Configuration**.</span></span>
   
   <span data-ttu-id="38830-150">![Konfiguracja rejestracji Jednokrotnej](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "konfiguracji logowania jednokrotnego")</span><span class="sxs-lookup"><span data-stu-id="38830-150">![SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "SSO Configuration")</span></span>
8. <span data-ttu-id="38830-151">W hello sekcji federacyjnych konfiguracji Usługa rejestracji Jednokrotnej w sieci Web wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="38830-151">In hello Federated Web SSO Configuration section, perform hello following steps:</span></span>
   
   <span data-ttu-id="38830-152">![Federacyjna usługa rejestracji Jednokrotnej w konfiguracji](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "Federacyjna usługa rejestracji Jednokrotnej w konfiguracji")</span><span class="sxs-lookup"><span data-stu-id="38830-152">![Federated SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "Federated SSO Configuration")</span></span>  
   1. <span data-ttu-id="38830-153">Z hello **protokołu federacyjnego** listy, wybierz **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="38830-153">From hello **Federation Protocol** list, select **SAML 2.0**.</span></span>
   2. <span data-ttu-id="38830-154">Utwórz **algorytmem Base-64** pliku z pobranego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="38830-154">Create a **Base-64 encoded** file from your downloaded certificate.</span></span>  
    >[!TIP]
    ><span data-ttu-id="38830-155">Aby uzyskać więcej informacji, zobacz [jak tooconvert pliku binarnego certyfikatu do pliku tekstowego](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="38830-155">For more details, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>
    >  
   3. <span data-ttu-id="38830-156">Otwórz certyfikatu zakodowanego base-64 w Notatniku i hello kopiowania zawartości z niego.</span><span class="sxs-lookup"><span data-stu-id="38830-156">Open your base-64 encoded certificate in notepad, and then copy hello content of it.</span></span>
   4. <span data-ttu-id="38830-157">Kliknij przycisk **Importowanie metadanych SAML**, a następnie wklej certyfikatu zakodowanego base-64.</span><span class="sxs-lookup"><span data-stu-id="38830-157">Click **Import SAML Metadata**, and then paste your base-64 encoded certificate.</span></span>
   5. <span data-ttu-id="38830-158">W hello klasycznego portalu Azure na powitania **skonfigurować logowanie jednokrotne w Cisco Webex** strony okna dialogowego, hello kopiowania **adres URL wystawcy** wartość, a następnie wklej go do hello **wystawca SAML (identyfikator IdP)** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="38830-158">In hello Azure classic portal, on hello **Configure single sign-on at Cisco Webex** dialog page, copy hello **Issuer URL** value, and then paste it into hello **Issuer for SAML (IdP ID)** textbox.</span></span>
   6. <span data-ttu-id="38830-159">W hello klasycznego portalu Azure na powitania **skonfigurować logowanie jednokrotne w Cisco Webex** strony okna dialogowego, hello kopiowania **zdalnego adresu URL logowania** wartość, a następnie wklej go do hello **klienta logowania jednokrotnego usługi logowania Adres URL** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="38830-159">In hello Azure classic portal, on hello **Configure single sign-on at Cisco Webex** dialog page, copy hello **Remote Login URL** value, and then paste it into hello **Customer SSO Service Login URL** textbox.</span></span>
   7. <span data-ttu-id="38830-160">Z hello **NameID Format** listy, wybierz **adres E-mail**.</span><span class="sxs-lookup"><span data-stu-id="38830-160">From hello **NameID Format** list, select **Email address**.</span></span>
   8. <span data-ttu-id="38830-161">W hello **AuthnContextClassRef** pole tekstowe, typ **urn: oasis: nazwy: tc: SAML:2.0:ac:classes:Password**.</span><span class="sxs-lookup"><span data-stu-id="38830-161">In hello **AuthnContextClassRef** textbox, type **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span></span>
   9. <span data-ttu-id="38830-162">W hello klasycznego portalu Azure na powitania **skonfigurować logowanie jednokrotne w Cisco Webex** strony okna dialogowego, hello kopiowania **zdalnego adresu URL wylogowania** wartość, a następnie wklej go do hello **wylogowania usługi logowania jednokrotnego klienta Adres URL** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="38830-162">In hello Azure classic portal, on hello **Configure single sign-on at Cisco Webex** dialog page, copy hello **Remote Logout URL** value, and then paste it into hello **Customer SSO Service Logout URL** textbox.</span></span>
   10. <span data-ttu-id="38830-163">Kliknij przycisk **aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="38830-163">Click **Update**.</span></span>
9. <span data-ttu-id="38830-164">W hello klasycznego portalu Azure na powitania **skonfigurować logowanie jednokrotne w Cisco Webex** strony okna dialogowego, wybierz hello konfiguracji rejestracji jednokrotnej potwierdzenie, a następnie kliknij **Complete**.</span><span class="sxs-lookup"><span data-stu-id="38830-164">In hello Azure classic portal, on hello **Configure single sign-on at Cisco Webex** dialog page, select hello single sign-on configuration confirmation, and then click **Complete**.</span></span>
   
   <span data-ttu-id="38830-165">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="38830-165">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="38830-166">Skonfiguruj Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="38830-166">Configure user provisioning</span></span>

<span data-ttu-id="38830-167">W przypadku użytkowników usługi Azure AD toolog kolejności tooenable do Cisco Webex muszą mieć przydzielone do Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="38830-167">In order tooenable Azure AD users toolog into Cisco Webex, they must be provisioned into Cisco Webex.</span></span>  

* <span data-ttu-id="38830-168">W przypadku hello Cisco Webex Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="38830-168">In hello case of Cisco Webex, provisioning is a manual task.</span></span>

<span data-ttu-id="38830-169">**tooprovision kont użytkowników, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="38830-169">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="38830-170">Zaloguj się za tooyour **Cisco Webex** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="38830-170">Log in tooyour **Cisco Webex** tenant.</span></span>
2. <span data-ttu-id="38830-171">Przejdź za**Zarządzanie użytkownikami \> Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="38830-171">Go too**Manage Users \> Add User**.</span></span>
   
   <span data-ttu-id="38830-172">![Dodawanie użytkowników](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "Dodawanie użytkowników")</span><span class="sxs-lookup"><span data-stu-id="38830-172">![Add users](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "Add users")</span></span>
3. <span data-ttu-id="38830-173">W sekcji Dodaj użytkownika hello wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="38830-173">On hello Add User section, perform hello following steps:</span></span>
   
   <span data-ttu-id="38830-174">![Dodaj użytkownika](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "Dodaj użytkownika")</span><span class="sxs-lookup"><span data-stu-id="38830-174">![Add user](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "Add user")</span></span>   
   1. <span data-ttu-id="38830-175">Jako **typ konta**, wybierz pozycję **hosta**.</span><span class="sxs-lookup"><span data-stu-id="38830-175">As **Account Type**, select **Host**.</span></span>
   2. <span data-ttu-id="38830-176">Wpisz informacje hello istniejącego użytkownika usługi Azure AD do hello następujące pola tekstowe: **imię, nazwisko**, **nazwy użytkownika**, **E-mail**, **hasło**, **Potwierdź hasło**.</span><span class="sxs-lookup"><span data-stu-id="38830-176">Type hello information of an existing Azure AD user into hello following textboxes: **First name, Last name**, **User name**, **Email**, **Password**, **Confirm Password**.</span></span>
   3. <span data-ttu-id="38830-177">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="38830-177">Click **Add**.</span></span>

>[!NOTE]
><span data-ttu-id="38830-178">Możesz użyć innych Cisco Webex użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez tooprovision Cisco Webex kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="38830-178">You can use any other Cisco Webex user account creation tools or APIs provided by Cisco Webex tooprovision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="38830-179">Przypisywanie użytkowników</span><span class="sxs-lookup"><span data-stu-id="38830-179">Assign users</span></span>
<span data-ttu-id="38830-180">tootest konfiguracji, należy toogrant hello Azure AD użytkownicy mają tooallow przy użyciu Twojej aplikacji tooit dostępu przez przypisywanie ich.</span><span class="sxs-lookup"><span data-stu-id="38830-180">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="38830-181">**tooassign użytkowników tooCisco Webex, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="38830-181">**tooassign users tooCisco Webex, perform hello following steps:**</span></span>

1. <span data-ttu-id="38830-182">W hello klasycznego portalu Azure Utwórz konto testu.</span><span class="sxs-lookup"><span data-stu-id="38830-182">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="38830-183">Na powitania **Cisco Webex** strona integracji aplikacji, kliknij przycisk **przypisywać użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="38830-183">On hello **Cisco Webex** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="38830-184">![Przypisywanie użytkowników](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "przypisywanie użytkowników")</span><span class="sxs-lookup"><span data-stu-id="38830-184">![Assign users](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "Assign users")</span></span>
3. <span data-ttu-id="38830-185">Wybierz użytkownika testowego, kliknij przycisk **przypisać**, a następnie kliknij przycisk **tak** tooconfirm przypisania.</span><span class="sxs-lookup"><span data-stu-id="38830-185">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="38830-186">![Tak](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "tak")</span><span class="sxs-lookup"><span data-stu-id="38830-186">![Yes](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="38830-187">Jeśli chcesz tootest jednego ustawienia logowania jednokrotnego, otwórz hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="38830-187">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="38830-188">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="38830-188">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

