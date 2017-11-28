---
title: "Samouczek: Integracji usługi Azure Active Directory z Cisco Webex | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać Cisco Webex z usługą Azure Active Directory w celu włączenia logowania jednokrotnego, automatyczne Inicjowanie obsługi i inne!"
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
ms.openlocfilehash: b44b1a5b3e988a51db3325ec8a181651fa84e768
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-webex"></a><span data-ttu-id="4639f-103">Samouczek: Integracji usługi Azure Active Directory z Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="4639f-103">Tutorial: Azure Active Directory Integration with Cisco Webex</span></span>
<span data-ttu-id="4639f-104">Celem tego samouczka jest pokazanie integracji Azure i Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="4639f-104">The objective of this tutorial is to show the integration of Azure and Cisco Webex.</span></span>  
<span data-ttu-id="4639f-105">Scenariusz opisany w tym samouczku założono, że już następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="4639f-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="4639f-106">Ważnej subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="4639f-106">A valid Azure subscription</span></span>
* <span data-ttu-id="4639f-107">Dzierżawy Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="4639f-107">A Cisco Webex tenant</span></span>

<span data-ttu-id="4639f-108">Ten samouczek użytkowników usługi Azure AD, zostały przypisane do Cisco Webex będzie można funkcji logowania jednokrotnego do aplikacji w witrynie firmy Cisco Webex (usługa zainicjował dostawcy logowania) lub przy użyciu [wprowadzenie do panelu dostępu ](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4639f-108">After completing this tutorial, the Azure AD users you have assigned to Cisco Webex will be able to single sign into the application at your Cisco Webex company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="4639f-109">Scenariusz opisany w tym samouczku składa się z następujących bloków konstrukcyjnych:</span><span class="sxs-lookup"><span data-stu-id="4639f-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="4639f-110">Włączanie integracji aplikacji dla Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="4639f-110">Enabling the application integration for Cisco Webex</span></span>
* <span data-ttu-id="4639f-111">Konfigurowanie rejestracji jednokrotnej (SSO)</span><span class="sxs-lookup"><span data-stu-id="4639f-111">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="4639f-112">Konfigurowanie Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="4639f-112">Configuring user provisioning</span></span>
* <span data-ttu-id="4639f-113">Przypisywanie użytkowników</span><span class="sxs-lookup"><span data-stu-id="4639f-113">Assigning users</span></span>

<span data-ttu-id="4639f-114">![Scenariusz](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "scenariusza")</span><span class="sxs-lookup"><span data-stu-id="4639f-114">![Scenario](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-cisco-webex"></a><span data-ttu-id="4639f-115">Włącz integrację aplikacji dla Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="4639f-115">Enable the application integration for Cisco Webex</span></span>
<span data-ttu-id="4639f-116">Celem tej sekcji jest przedstawiają sposób włączania integracji aplikacji dla Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="4639f-116">The objective of this section is to outline how to enable the application integration for Cisco Webex.</span></span>

<span data-ttu-id="4639f-117">**Aby włączyć integrację aplikacji dla Cisco Webex, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="4639f-117">**To enable the application integration for Cisco Webex, perform the following steps:**</span></span>

1. <span data-ttu-id="4639f-118">W klasycznym portalu Azure, w okienku nawigacji po lewej stronie kliknij **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4639f-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="4639f-119">![Usługi Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "usługi Active Directory")</span><span class="sxs-lookup"><span data-stu-id="4639f-119">![Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="4639f-120">Z **katalogu** listy, wybierz katalog, dla którego chcesz włączyć integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="4639f-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="4639f-121">Aby otworzyć widok aplikacji, w widoku katalogu, kliknij przycisk **aplikacji** w menu u góry.</span><span class="sxs-lookup"><span data-stu-id="4639f-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="4639f-122">![Aplikacje](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "aplikacji")</span><span class="sxs-lookup"><span data-stu-id="4639f-122">![Applications](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="4639f-123">Kliknij przycisk **Dodaj** w dolnej części strony.</span><span class="sxs-lookup"><span data-stu-id="4639f-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="4639f-124">![Dodaj aplikację](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "Dodaj aplikację")</span><span class="sxs-lookup"><span data-stu-id="4639f-124">![Add application](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="4639f-125">Na **co chcesz zrobić** okna dialogowego, kliknij przycisk **dodać aplikację z galerii**.</span><span class="sxs-lookup"><span data-stu-id="4639f-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="4639f-126">![Dodawanie aplikacji z gallerry](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "dodać aplikację z gallerry")</span><span class="sxs-lookup"><span data-stu-id="4639f-126">![Add an application from gallerry](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="4639f-127">W **pole wyszukiwania**, typ **Cisco Webex**.</span><span class="sxs-lookup"><span data-stu-id="4639f-127">In the **search box**, type **Cisco Webex**.</span></span>
   
   <span data-ttu-id="4639f-128">![Galerii aplikacji](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "galerii aplikacji")</span><span class="sxs-lookup"><span data-stu-id="4639f-128">![Application Gallery](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "Application Gallery")</span></span>
7. <span data-ttu-id="4639f-129">W okienku wyników wybierz **Cisco Webex**, a następnie kliknij przycisk **Complete** można dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="4639f-129">In the results pane, select **Cisco Webex**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="4639f-130">![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")</span><span class="sxs-lookup"><span data-stu-id="4639f-130">![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="4639f-131">Konfigurowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="4639f-131">Configure single sign-on</span></span>

<span data-ttu-id="4639f-132">Celem tej sekcji jest przedstawiają sposób umożliwić użytkownikom uwierzytelnianie na Cisco Webex do swojego konta w usłudze Azure AD przy użyciu federacyjnego na podstawie protokołu SAML.</span><span class="sxs-lookup"><span data-stu-id="4639f-132">The objective of this section is to outline how to enable users to authenticate to Cisco Webex with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="4639f-133">W ramach tej procedury jest wymagane do utworzenia zakodowanego certyfikatu base-64.</span><span class="sxs-lookup"><span data-stu-id="4639f-133">As part of this procedure, you are required to create a base-64 encoded certificate.</span></span> <span data-ttu-id="4639f-134">Jeśli nie masz doświadczenia z tej procedury, zobacz [sposób konwertowania binarne certyfikatu do pliku tekstowego](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="4639f-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>

<span data-ttu-id="4639f-135">**Aby skonfigurować rejestrację jednokrotną, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="4639f-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="4639f-136">W klasycznym portalu Azure na **Cisco Webex** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** otworzyć **skonfigurować rejestrację jednokrotną** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4639f-136">In the Azure classic portal, on the **Cisco Webex** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="4639f-137">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="4639f-137">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="4639f-138">Na **jak chcesz użytkownikom zalogować się na Cisco Webex** wybierz pozycję **usługi Microsoft Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="4639f-138">On the **How would you like users to sign on to Cisco Webex** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="4639f-139">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="4639f-139">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="4639f-140">Na **Konfigurowanie adresu URL aplikacji** , wykonaj następujące czynności, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="4639f-140">On the **Configure App URL** page, perform the following steps, and then click **Next**.</span></span>
   
   <span data-ttu-id="4639f-141">![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "skonfigurować adres URL aplikacji")</span><span class="sxs-lookup"><span data-stu-id="4639f-141">![Configure app URL](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "Configure app URL")</span></span>   
   1. <span data-ttu-id="4639f-142">W **rejestrują na adres URL** tekstowym, wpisz adres URL dzierżawy Cisco Webex (np.: *http://contoso.webex.com*).</span><span class="sxs-lookup"><span data-stu-id="4639f-142">In the **Sing On URL** textbox, type your Cisco Webex tenant URL (e.g.: *http://contoso.webex.com*).</span></span>
   2. <span data-ttu-id="4639f-143">W **adres URL odpowiedzi Webex Cisco** pole tekstowe, typ użytkownika **adres URL AssertionConsumerService Webex Cisco** (np.: *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company* ).</span><span class="sxs-lookup"><span data-stu-id="4639f-143">In the **Cisco Webex Reply URL** textbox, type your **Cisco Webex AssertionConsumerService URL** (e.g.: *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company*).</span></span>
4. <span data-ttu-id="4639f-144">Na **skonfigurować logowanie jednokrotne w Cisco Webex** , aby pobrać certyfikat, kliknij przycisk **pobierania certyfikatu**, a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="4639f-144">On the **Configure single sign-on at Cisco Webex** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
   <span data-ttu-id="4639f-145">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="4639f-145">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="4639f-146">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy Cisco Webex jako administrator.</span><span class="sxs-lookup"><span data-stu-id="4639f-146">In a different web browser window, log into your Cisco Webex company site as an administrator.</span></span>
6. <span data-ttu-id="4639f-147">W menu u góry kliknij **administrowania lokacją**.</span><span class="sxs-lookup"><span data-stu-id="4639f-147">In the menu on the top, click **Site Administration**.</span></span>
   
   <span data-ttu-id="4639f-148">![Administrowanie lokacją](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "lokacji administracyjnej")</span><span class="sxs-lookup"><span data-stu-id="4639f-148">![Site Administration](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "Site Administration")</span></span>
7. <span data-ttu-id="4639f-149">W **zarządzania witryną** kliknij **konfiguracji logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="4639f-149">In the **Manage Site** section, click **SSO Configuration**.</span></span>
   
   <span data-ttu-id="4639f-150">![Konfiguracja rejestracji Jednokrotnej](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "konfiguracji logowania jednokrotnego")</span><span class="sxs-lookup"><span data-stu-id="4639f-150">![SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "SSO Configuration")</span></span>
8. <span data-ttu-id="4639f-151">W sekcji federacyjnych konfiguracji Usługa rejestracji Jednokrotnej w sieci Web wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="4639f-151">In the Federated Web SSO Configuration section, perform the following steps:</span></span>
   
   <span data-ttu-id="4639f-152">![Federacyjna usługa rejestracji Jednokrotnej w konfiguracji](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "Federacyjna usługa rejestracji Jednokrotnej w konfiguracji")</span><span class="sxs-lookup"><span data-stu-id="4639f-152">![Federated SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "Federated SSO Configuration")</span></span>  
   1. <span data-ttu-id="4639f-153">Z **protokołu federacyjnego** listy, wybierz **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="4639f-153">From the **Federation Protocol** list, select **SAML 2.0**.</span></span>
   2. <span data-ttu-id="4639f-154">Utwórz **algorytmem Base-64** pliku z pobranego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="4639f-154">Create a **Base-64 encoded** file from your downloaded certificate.</span></span>  
    >[!TIP]
    ><span data-ttu-id="4639f-155">Aby uzyskać więcej informacji, zobacz [sposób konwertowania binarne certyfikatu do pliku tekstowego](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="4639f-155">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>
    >  
   3. <span data-ttu-id="4639f-156">Otwórz w Notatniku certyfikatu zakodowanego base-64, a następnie skopiuj zawartość tego.</span><span class="sxs-lookup"><span data-stu-id="4639f-156">Open your base-64 encoded certificate in notepad, and then copy the content of it.</span></span>
   4. <span data-ttu-id="4639f-157">Kliknij przycisk **Importowanie metadanych SAML**, a następnie wklej certyfikatu zakodowanego base-64.</span><span class="sxs-lookup"><span data-stu-id="4639f-157">Click **Import SAML Metadata**, and then paste your base-64 encoded certificate.</span></span>
   5. <span data-ttu-id="4639f-158">W klasycznym portalu Azure na **skonfigurować logowanie jednokrotne w Cisco Webex** strony okna dialogowego, kopiowania **adres URL wystawcy** wartość, a następnie wklej ją do **wystawca SAML (identyfikator IdP)** pole tekstowe.</span><span class="sxs-lookup"><span data-stu-id="4639f-158">In the Azure classic portal, on the **Configure single sign-on at Cisco Webex** dialog page, copy the **Issuer URL** value, and then paste it into the **Issuer for SAML (IdP ID)** textbox.</span></span>
   6. <span data-ttu-id="4639f-159">W klasycznym portalu Azure na **skonfigurować logowanie jednokrotne w Cisco Webex** strony okna dialogowego, kopiowania **zdalnego adresu URL logowania** wartość, a następnie wklej ją do **adres URL logowania usługi logowania jednokrotnego klienta** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="4639f-159">In the Azure classic portal, on the **Configure single sign-on at Cisco Webex** dialog page, copy the **Remote Login URL** value, and then paste it into the **Customer SSO Service Login URL** textbox.</span></span>
   7. <span data-ttu-id="4639f-160">Z **NameID Format** listy, wybierz **adres E-mail**.</span><span class="sxs-lookup"><span data-stu-id="4639f-160">From the **NameID Format** list, select **Email address**.</span></span>
   8. <span data-ttu-id="4639f-161">W **AuthnContextClassRef** pole tekstowe, typ **urn: oasis: nazwy: tc: SAML:2.0:ac:classes:Password**.</span><span class="sxs-lookup"><span data-stu-id="4639f-161">In the **AuthnContextClassRef** textbox, type **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span></span>
   9. <span data-ttu-id="4639f-162">W klasycznym portalu Azure na **skonfigurować logowanie jednokrotne w Cisco Webex** strony okna dialogowego, kopiowania **zdalnego adresu URL wylogowania** wartość, a następnie wklej ją do **adres URL wylogowania usługi logowania jednokrotnego klienta** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="4639f-162">In the Azure classic portal, on the **Configure single sign-on at Cisco Webex** dialog page, copy the **Remote Logout URL** value, and then paste it into the **Customer SSO Service Logout URL** textbox.</span></span>
   10. <span data-ttu-id="4639f-163">Kliknij przycisk **aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="4639f-163">Click **Update**.</span></span>
9. <span data-ttu-id="4639f-164">W klasycznym portalu Azure na **skonfigurować logowanie jednokrotne w Cisco Webex** strony okna dialogowego, wybierz Potwierdzenie konfiguracji rejestracji jednokrotnej, a następnie kliknij **Complete**.</span><span class="sxs-lookup"><span data-stu-id="4639f-164">In the Azure classic portal, on the **Configure single sign-on at Cisco Webex** dialog page, select the single sign-on configuration confirmation, and then click **Complete**.</span></span>
   
   <span data-ttu-id="4639f-165">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="4639f-165">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="4639f-166">Skonfiguruj Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="4639f-166">Configure user provisioning</span></span>

<span data-ttu-id="4639f-167">Aby włączyć użytkowników usługi Azure AD zalogować się do Cisco Webex, musi być przygotowana do Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="4639f-167">In order to enable Azure AD users to log into Cisco Webex, they must be provisioned into Cisco Webex.</span></span>  

* <span data-ttu-id="4639f-168">W przypadku Cisco Webex Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="4639f-168">In the case of Cisco Webex, provisioning is a manual task.</span></span>

<span data-ttu-id="4639f-169">**Aby udostępnić konta użytkowników, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="4639f-169">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="4639f-170">Zaloguj się do Twojego **Cisco Webex** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="4639f-170">Log in to your **Cisco Webex** tenant.</span></span>
2. <span data-ttu-id="4639f-171">Przejdź do **Zarządzanie użytkownikami \> dodać użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="4639f-171">Go to **Manage Users \> Add User**.</span></span>
   
   <span data-ttu-id="4639f-172">![Dodawanie użytkowników](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "Dodawanie użytkowników")</span><span class="sxs-lookup"><span data-stu-id="4639f-172">![Add users](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "Add users")</span></span>
3. <span data-ttu-id="4639f-173">W sekcji Dodaj użytkownika wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="4639f-173">On the Add User section, perform the following steps:</span></span>
   
   <span data-ttu-id="4639f-174">![Dodaj użytkownika](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "Dodaj użytkownika")</span><span class="sxs-lookup"><span data-stu-id="4639f-174">![Add user](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "Add user")</span></span>   
   1. <span data-ttu-id="4639f-175">Jako **typ konta**, wybierz pozycję **hosta**.</span><span class="sxs-lookup"><span data-stu-id="4639f-175">As **Account Type**, select **Host**.</span></span>
   2. <span data-ttu-id="4639f-176">Wpisz informacje istniejącego użytkownika usługi Azure AD do następujących pól tekstowych: **imię, nazwisko**, **nazwy użytkownika**, **E-mail**, **hasło**, **Potwierdź hasło**.</span><span class="sxs-lookup"><span data-stu-id="4639f-176">Type the information of an existing Azure AD user into the following textboxes: **First name, Last name**, **User name**, **Email**, **Password**, **Confirm Password**.</span></span>
   3. <span data-ttu-id="4639f-177">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="4639f-177">Click **Add**.</span></span>

>[!NOTE]
><span data-ttu-id="4639f-178">Możesz użyć innych Cisco Webex użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Cisco Webex do kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="4639f-178">You can use any other Cisco Webex user account creation tools or APIs provided by Cisco Webex to provision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="4639f-179">Przypisywanie użytkowników</span><span class="sxs-lookup"><span data-stu-id="4639f-179">Assign users</span></span>
<span data-ttu-id="4639f-180">Aby przetestować konfigurację, musisz przyznać użytkowników usługi Azure AD, czy chcesz zezwolić, używając przypisywania do nich dostęp aplikacji do niego.</span><span class="sxs-lookup"><span data-stu-id="4639f-180">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="4639f-181">**Do przypisywania użytkowników do Cisco Webex, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="4639f-181">**To assign users to Cisco Webex, perform the following steps:**</span></span>

1. <span data-ttu-id="4639f-182">W klasycznym portalu Azure Utwórz konto testu.</span><span class="sxs-lookup"><span data-stu-id="4639f-182">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="4639f-183">Na **Cisco Webex** strona integracji aplikacji, kliknij przycisk **przypisywać użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="4639f-183">On the **Cisco Webex** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="4639f-184">![Przypisywanie użytkowników](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "przypisywanie użytkowników")</span><span class="sxs-lookup"><span data-stu-id="4639f-184">![Assign users](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "Assign users")</span></span>
3. <span data-ttu-id="4639f-185">Wybierz użytkownika testowego, kliknij przycisk **przypisać**, a następnie kliknij przycisk **tak** o potwierdzenie przypisania.</span><span class="sxs-lookup"><span data-stu-id="4639f-185">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="4639f-186">![Tak](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "tak")</span><span class="sxs-lookup"><span data-stu-id="4639f-186">![Yes](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="4639f-187">Jeśli chcesz przetestować jednego ustawienia logowania jednokrotnego, otwórz Panel dostępu.</span><span class="sxs-lookup"><span data-stu-id="4639f-187">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="4639f-188">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4639f-188">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

