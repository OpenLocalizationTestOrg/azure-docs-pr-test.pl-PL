---
title: 'Samouczek: Integracji Azure Active Directory z Replicon | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak używać Replicon usłudze Azure Active Directory w celu włączenia logowania jednokrotnego, automatyczne Inicjowanie obsługi i inne!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 02a62f15-917c-417c-8d80-fe685e3fd601
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 2aeeceb61191962b62892b8409218684f76c6fa8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-replicon"></a><span data-ttu-id="779b8-103">Samouczek: Integracji Azure Active Directory z Replicon</span><span class="sxs-lookup"><span data-stu-id="779b8-103">Tutorial: Azure Active Directory integration with Replicon</span></span>
<span data-ttu-id="779b8-104">Celem tego samouczka jest pokazanie integracji Azure i Replicon.</span><span class="sxs-lookup"><span data-stu-id="779b8-104">The objective of this tutorial is to show the integration of Azure and Replicon.</span></span> <span data-ttu-id="779b8-105">Scenariusz opisany w tym samouczku założono, że już następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="779b8-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="779b8-106">Ważnej subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="779b8-106">A valid Azure subscription</span></span>
* <span data-ttu-id="779b8-107">Dzierżawy Replicon</span><span class="sxs-lookup"><span data-stu-id="779b8-107">A Replicon tenant</span></span>

<span data-ttu-id="779b8-108">Ten samouczek użytkowników usługi Azure AD, zostały przypisane do Replicon będzie można funkcji logowania jednokrotnego do aplikacji w witrynie firmy Replicon (usługa zainicjował dostawcy logowania) lub przy użyciu [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="779b8-108">After completing this tutorial, the Azure AD users you have assigned to Replicon will be able to single sign into the application at your Replicon company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="779b8-109">Scenariusz opisany w tym samouczku składa się z następujących bloków konstrukcyjnych:</span><span class="sxs-lookup"><span data-stu-id="779b8-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="779b8-110">Włączanie integracji aplikacji dla Replicon</span><span class="sxs-lookup"><span data-stu-id="779b8-110">Enabling the application integration for Replicon</span></span>
2. <span data-ttu-id="779b8-111">Konfigurowanie rejestracji jednokrotnej (SSO)</span><span class="sxs-lookup"><span data-stu-id="779b8-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="779b8-112">Konfigurowanie Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="779b8-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="779b8-113">Przypisywanie użytkowników</span><span class="sxs-lookup"><span data-stu-id="779b8-113">Assigning users</span></span>

<span data-ttu-id="779b8-114">![Scenariusz](./media/active-directory-saas-replicon-tutorial/IC777798.png "scenariusza")</span><span class="sxs-lookup"><span data-stu-id="779b8-114">![Scenario](./media/active-directory-saas-replicon-tutorial/IC777798.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-replicon"></a><span data-ttu-id="779b8-115">Włącz integrację aplikacji dla Replicon</span><span class="sxs-lookup"><span data-stu-id="779b8-115">Enable the application integration for Replicon</span></span>
<span data-ttu-id="779b8-116">Celem tej sekcji jest przedstawiają sposób włączania integracji aplikacji dla Replicon.</span><span class="sxs-lookup"><span data-stu-id="779b8-116">The objective of this section is to outline how to enable the application integration for Replicon.</span></span>

<span data-ttu-id="779b8-117">**Aby włączyć integrację aplikacji dla Replicon, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="779b8-117">**To enable the application integration for Replicon, perform the following steps:**</span></span>

1. <span data-ttu-id="779b8-118">W klasycznym portalu Azure, w okienku nawigacji po lewej stronie kliknij **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="779b8-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="779b8-119">![Usługi Active Directory](./media/active-directory-saas-replicon-tutorial/IC700993.png "usługi Active Directory")</span><span class="sxs-lookup"><span data-stu-id="779b8-119">![Active Directory](./media/active-directory-saas-replicon-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="779b8-120">Z **katalogu** listy, wybierz katalog, dla którego chcesz włączyć integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="779b8-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="779b8-121">Aby otworzyć widok aplikacji, w widoku katalogu, kliknij przycisk **aplikacji** w menu u góry.</span><span class="sxs-lookup"><span data-stu-id="779b8-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="779b8-122">![Aplikacje](./media/active-directory-saas-replicon-tutorial/IC700994.png "aplikacji")</span><span class="sxs-lookup"><span data-stu-id="779b8-122">![Applications](./media/active-directory-saas-replicon-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="779b8-123">Kliknij przycisk **Dodaj** w dolnej części strony.</span><span class="sxs-lookup"><span data-stu-id="779b8-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="779b8-124">![Dodaj aplikację](./media/active-directory-saas-replicon-tutorial/IC749321.png "Dodaj aplikację")</span><span class="sxs-lookup"><span data-stu-id="779b8-124">![Add application](./media/active-directory-saas-replicon-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="779b8-125">Na **co chcesz zrobić** okna dialogowego, kliknij przycisk **dodać aplikację z galerii**.</span><span class="sxs-lookup"><span data-stu-id="779b8-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="779b8-126">![Dodawanie aplikacji z gallerry](./media/active-directory-saas-replicon-tutorial/IC749322.png "dodać aplikację z gallerry")</span><span class="sxs-lookup"><span data-stu-id="779b8-126">![Add an application from gallerry](./media/active-directory-saas-replicon-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="779b8-127">W **pole wyszukiwania**, typ **Replicon**.</span><span class="sxs-lookup"><span data-stu-id="779b8-127">In the **search box**, type **Replicon**.</span></span>
   
    <span data-ttu-id="779b8-128">![Galerii aplikacji](./media/active-directory-saas-replicon-tutorial/IC777799.png "galerii aplikacji")</span><span class="sxs-lookup"><span data-stu-id="779b8-128">![Application gallery](./media/active-directory-saas-replicon-tutorial/IC777799.png "Application gallery")</span></span>
7. <span data-ttu-id="779b8-129">W okienku wyników wybierz **Replicon**, a następnie kliknij przycisk **Complete** można dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="779b8-129">In the results pane, select **Replicon**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="779b8-130">![Replicon](./media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")</span><span class="sxs-lookup"><span data-stu-id="779b8-130">![Replicon](./media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="779b8-131">Konfigurowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="779b8-131">Configure single sign-on</span></span>

<span data-ttu-id="779b8-132">Celem tej sekcji jest przedstawiają sposób umożliwić użytkownikom uwierzytelnianie na Replicon do swojego konta w usłudze Azure AD przy użyciu federacyjnego na podstawie protokołu SAML.</span><span class="sxs-lookup"><span data-stu-id="779b8-132">The objective of this section is to outline how to enable users to authenticate to Replicon with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="779b8-133">**Aby skonfigurować rejestrację jednokrotną, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="779b8-133">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="779b8-134">W klasycznym portalu Azure na **Replicon** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** otworzyć **skonfigurować rejestrację jednokrotną** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="779b8-134">In the Azure classic portal, on the **Replicon** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="779b8-135">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-replicon-tutorial/IC777801.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="779b8-135">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777801.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="779b8-136">Na **jak chcesz użytkownikom zalogować się na Replicon** wybierz pozycję **usługi Microsoft Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="779b8-136">On the **How would you like users to sign on to Replicon** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="779b8-137">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-replicon-tutorial/IC777802.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="779b8-137">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777802.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="779b8-138">Na **Konfigurowanie adresu URL aplikacji** wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="779b8-138">On the **Configure App URL** page, perform the following steps:</span></span>
   
    <span data-ttu-id="779b8-139">![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-replicon-tutorial/IC777803.png "skonfigurować adres URL aplikacji")</span><span class="sxs-lookup"><span data-stu-id="779b8-139">![Configure app URL](./media/active-directory-saas-replicon-tutorial/IC777803.png "Configure app URL")</span></span>
  1. <span data-ttu-id="779b8-140">W **Replicon na adres URL logowania** tekstowym, wpisz adres URL dzierżawy Replicon (np.: *https://na2.replicon.com/company/saml2/sp-sso/post*).</span><span class="sxs-lookup"><span data-stu-id="779b8-140">In the **Replicon Sign On URL** textbox, type your Replicon tenant URL (e.g.: *https://na2.replicon.com/company/saml2/sp-sso/post*).</span></span>
  2. <span data-ttu-id="779b8-141">W **adres URL odpowiedzi Replicon** tekstowym, wpisz Replicon Twojego **AssertionConsumerService** adres URL (np.: *https://global.replicon.com/! / saml2/firmy/logowania jednokrotnego/post*).</span><span class="sxs-lookup"><span data-stu-id="779b8-141">In the **Replicon Reply URL** textbox, type your Replicon **AssertionConsumerService** URL(e.g.: *https://global.replicon.com/!/saml2/company/sso/post*).</span></span>  
      
     >[!NOTE]
     ><span data-ttu-id="779b8-142">Należy uzyskać adres URL z metadanych Replicon w: **https://global.replicon.com/! /saml2/\<YourCompanyKey\>**.</span><span class="sxs-lookup"><span data-stu-id="779b8-142">You can get the URL from the Replicon metadata at: **https://global.replicon.com/!/saml2/\<YourCompanyKey\>**.</span></span>
     > 
     > 
 
  3. <span data-ttu-id="779b8-143">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="779b8-143">Click **Next**.</span></span>

4. <span data-ttu-id="779b8-144">Na **skonfigurować logowanie jednokrotne w Replicon** , aby pobrać metadane, kliknij przycisk **pobierania metadanych**, a następnie Zapisz metadane na komputerze.</span><span class="sxs-lookup"><span data-stu-id="779b8-144">On the **Configure single sign-on at Replicon** page, to download your metadata, click **Download metadata**, and then save the metadata on your computer.</span></span>
   
    <span data-ttu-id="779b8-145">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-replicon-tutorial/IC777804.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="779b8-145">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777804.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="779b8-146">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy Replicon jako administrator.</span><span class="sxs-lookup"><span data-stu-id="779b8-146">In a different web browser window, log into your Replicon company site as an administrator.</span></span>

6. <span data-ttu-id="779b8-147">Aby skonfigurować SAML 2.0, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="779b8-147">To configure SAML 2.0, perform the following steps:</span></span>
   
    <span data-ttu-id="779b8-148">![Włącz uwierzytelnianie SAML](./media/active-directory-saas-replicon-tutorial/IC777805.png "uwierzytelnianie Włącz SAML")</span><span class="sxs-lookup"><span data-stu-id="779b8-148">![Enable SAML authentication](./media/active-directory-saas-replicon-tutorial/IC777805.png "Enable SAML authentication")</span></span>
  
  1. <span data-ttu-id="779b8-149">Aby wyświetlić **EnableSAML Authentication2** okna dialogowego, dołącz następujące na adres URL po klucz firmy: **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span><span class="sxs-lookup"><span data-stu-id="779b8-149">To display the **EnableSAML Authentication2** dialog, append the following to your URL, after your company key: **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span></span>  
    * <span data-ttu-id="779b8-150">Poniżej przedstawiono schematu pełny adres URL:</span><span class="sxs-lookup"><span data-stu-id="779b8-150">The following shows the schema of the complete URL:</span></span>  
   <span data-ttu-id="779b8-151">**https://Na2.replicon.com/\<YourCompanyKey\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span><span class="sxs-lookup"><span data-stu-id="779b8-151">**https://na2.replicon.com/\<YourCompanyKey\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span></span>
   2. <span data-ttu-id="779b8-152">Kliknij przycisk  **+**  rozszerzenia **v20Configuration** sekcji.</span><span class="sxs-lookup"><span data-stu-id="779b8-152">Click the **+** to expand the **v20Configuration** section.</span></span>
   3. <span data-ttu-id="779b8-153">Kliknij przycisk  **+**  rozszerzenia **metaDataConfiguration** sekcji.</span><span class="sxs-lookup"><span data-stu-id="779b8-153">Click the **+** to expand the **metaDataConfiguration** section.</span></span>
   4. <span data-ttu-id="779b8-154">Kliknij przycisk **wybierz plik**, aby wybrać plik XML metadanych dostawcy tożsamości, a następnie kliknij przycisk **przesyłania**.</span><span class="sxs-lookup"><span data-stu-id="779b8-154">Click **Choose File**, to select your identity provider metadata XML file, and click **Submit**.</span></span>

7. <span data-ttu-id="779b8-155">W klasycznym portalu Azure, wybierz Potwierdzenie konfiguracji rejestracji jednokrotnej, a następnie kliknij przycisk **Complete** zamknąć **skonfigurować rejestrację jednokrotną** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="779b8-155">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="779b8-156">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-replicon-tutorial/IC778418.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="779b8-156">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC778418.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="779b8-157">Skonfiguruj Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="779b8-157">Configure user provisioning</span></span>

<span data-ttu-id="779b8-158">Aby włączyć użytkowników usługi Azure AD zalogować się do Replicon, musi być przygotowana do Replicon.</span><span class="sxs-lookup"><span data-stu-id="779b8-158">In order to enable Azure AD users to log into Replicon, they must be provisioned into Replicon.</span></span>  

<span data-ttu-id="779b8-159">W przypadku Replicon Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="779b8-159">In the case of Replicon, provisioning is a manual task.</span></span>

<span data-ttu-id="779b8-160">**Aby skonfigurować, inicjowanie obsługi użytkowników, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="779b8-160">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="779b8-161">W oknie przeglądarki sieci web Zaloguj się do witryny firmy Replicon jako administrator.</span><span class="sxs-lookup"><span data-stu-id="779b8-161">In a web browser window, log into your Replicon company site as an administrator.</span></span>
2. <span data-ttu-id="779b8-162">Przejdź do **administracji \> użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="779b8-162">Go to **Administration \> Users**.</span></span>
   
    <span data-ttu-id="779b8-163">![Użytkownicy](./media/active-directory-saas-replicon-tutorial/IC777806.png "użytkowników")</span><span class="sxs-lookup"><span data-stu-id="779b8-163">![Users](./media/active-directory-saas-replicon-tutorial/IC777806.png "Users")</span></span>
3. <span data-ttu-id="779b8-164">Kliknij przycisk **+ Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="779b8-164">Click **+Add User**.</span></span>
   
    <span data-ttu-id="779b8-165">![Dodaj użytkownika](./media/active-directory-saas-replicon-tutorial/IC777807.png "Dodaj użytkownika")</span><span class="sxs-lookup"><span data-stu-id="779b8-165">![Add User](./media/active-directory-saas-replicon-tutorial/IC777807.png "Add User")</span></span>
4. <span data-ttu-id="779b8-166">W **profilu użytkownika** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="779b8-166">In the **User Profile** section, perform the following steps:</span></span>
   
    <span data-ttu-id="779b8-167">![Profil użytkownika](./media/active-directory-saas-replicon-tutorial/IC777808.png "profilu użytkownika")</span><span class="sxs-lookup"><span data-stu-id="779b8-167">![User profile](./media/active-directory-saas-replicon-tutorial/IC777808.png "User profile")</span></span>
   
  1. <span data-ttu-id="779b8-168">W **nazwa logowania** pole tekstowe, adres e-mail użytkownika usługi Azure AD, aby udostępnić typu usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="779b8-168">In the **Login Name** textbox, type the Azure AD email address of the Azure AD user you want to provision.</span></span>
  2. <span data-ttu-id="779b8-169">Jako **typ uwierzytelniania**, wybierz pozycję **logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="779b8-169">As **Authentication Type**, select **SSO**.</span></span>
  3. <span data-ttu-id="779b8-170">W **działu** tekstowym, wpisz dział tego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="779b8-170">In the **Department** textbox, type the user’s department.</span></span>
  4. <span data-ttu-id="779b8-171">Jako **typu pracownika**, wybierz pozycję **administratora**.</span><span class="sxs-lookup"><span data-stu-id="779b8-171">As **Employee Type**, select **Administrator**.</span></span>
  5. <span data-ttu-id="779b8-172">Kliknij przycisk **Zapisz profil użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="779b8-172">Click **Save User Profile**.</span></span>

>[!NOTE]
><span data-ttu-id="779b8-173">Możesz użyć innych Replicon użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Replicon do kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="779b8-173">You can use any other Replicon user account creation tools or APIs provided by Replicon to provision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="779b8-174">Przypisywanie użytkowników</span><span class="sxs-lookup"><span data-stu-id="779b8-174">Assign users</span></span>
<span data-ttu-id="779b8-175">Aby przetestować konfigurację, musisz przyznać użytkowników usługi Azure AD, czy chcesz zezwolić, używając przypisywania do nich dostęp aplikacji do niego.</span><span class="sxs-lookup"><span data-stu-id="779b8-175">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="779b8-176">**Do przypisywania użytkowników do Replicon, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="779b8-176">**To assign users to Replicon, perform the following steps:**</span></span>

1. <span data-ttu-id="779b8-177">W klasycznym portalu Azure Utwórz konto testu.</span><span class="sxs-lookup"><span data-stu-id="779b8-177">In the Azure classic portal, create a test account.</span></span>

2. <span data-ttu-id="779b8-178">Na **Replicon** strona integracji aplikacji, kliknij przycisk **przypisywać użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="779b8-178">On the **Replicon** application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="779b8-179">![Przypisywanie użytkowników](./media/active-directory-saas-replicon-tutorial/IC777809.png "przypisywanie użytkowników")</span><span class="sxs-lookup"><span data-stu-id="779b8-179">![Assign users](./media/active-directory-saas-replicon-tutorial/IC777809.png "Assign users")</span></span>

3. <span data-ttu-id="779b8-180">Wybierz użytkownika testowego, kliknij przycisk **przypisać**, a następnie kliknij przycisk **tak** o potwierdzenie przypisania.</span><span class="sxs-lookup"><span data-stu-id="779b8-180">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="779b8-181">![Tak](./media/active-directory-saas-replicon-tutorial/IC767830.png "tak")</span><span class="sxs-lookup"><span data-stu-id="779b8-181">![Yes](./media/active-directory-saas-replicon-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="779b8-182">Jeśli chcesz przetestować jednego ustawienia logowania jednokrotnego, otwórz Panel dostępu.</span><span class="sxs-lookup"><span data-stu-id="779b8-182">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="779b8-183">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="779b8-183">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

