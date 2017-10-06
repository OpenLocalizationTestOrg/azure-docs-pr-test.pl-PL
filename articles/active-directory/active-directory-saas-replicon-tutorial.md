---
title: 'Samouczek: Integracji Azure Active Directory z Replicon | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak toouse Replicon z usługą Azure Active Directory tooenable pojedynczy logowania jednokrotnego, automatyczne Inicjowanie obsługi i inne!"
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
ms.openlocfilehash: 4949eaf959265cfa4f732a2b73317fffe6312a17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-replicon"></a><span data-ttu-id="18bd3-103">Samouczek: Integracji Azure Active Directory z Replicon</span><span class="sxs-lookup"><span data-stu-id="18bd3-103">Tutorial: Azure Active Directory integration with Replicon</span></span>
<span data-ttu-id="18bd3-104">Celem Hello tego samouczka jest tooshow integracji hello Azure i Replicon.</span><span class="sxs-lookup"><span data-stu-id="18bd3-104">hello objective of this tutorial is tooshow hello integration of Azure and Replicon.</span></span> <span data-ttu-id="18bd3-105">Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="18bd3-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="18bd3-106">Ważnej subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="18bd3-106">A valid Azure subscription</span></span>
* <span data-ttu-id="18bd3-107">Dzierżawy Replicon</span><span class="sxs-lookup"><span data-stu-id="18bd3-107">A Replicon tenant</span></span>

<span data-ttu-id="18bd3-108">Ten samouczek użytkownicy hello Azure AD przypisano tooReplicon będą mogli toosingle logowania do aplikacji hello w witrynie firmy Replicon (usługa zainicjował dostawcy logowania) lub przy użyciu hello [toohello wprowadzenie dostępu Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="18bd3-108">After completing this tutorial, hello Azure AD users you have assigned tooReplicon will be able toosingle sign into hello application at your Replicon company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="18bd3-109">Scenariusz Hello opisane w tym samouczku składa się z powitania po bloków konstrukcyjnych:</span><span class="sxs-lookup"><span data-stu-id="18bd3-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="18bd3-110">Włączanie integracji aplikacji hello dla Replicon</span><span class="sxs-lookup"><span data-stu-id="18bd3-110">Enabling hello application integration for Replicon</span></span>
2. <span data-ttu-id="18bd3-111">Konfigurowanie rejestracji jednokrotnej (SSO)</span><span class="sxs-lookup"><span data-stu-id="18bd3-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="18bd3-112">Konfigurowanie Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="18bd3-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="18bd3-113">Przypisywanie użytkowników</span><span class="sxs-lookup"><span data-stu-id="18bd3-113">Assigning users</span></span>

<span data-ttu-id="18bd3-114">![Scenariusz](./media/active-directory-saas-replicon-tutorial/IC777798.png "scenariusza")</span><span class="sxs-lookup"><span data-stu-id="18bd3-114">![Scenario](./media/active-directory-saas-replicon-tutorial/IC777798.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-replicon"></a><span data-ttu-id="18bd3-115">Włącz integrację aplikacji hello dla Replicon</span><span class="sxs-lookup"><span data-stu-id="18bd3-115">Enable hello application integration for Replicon</span></span>
<span data-ttu-id="18bd3-116">Celem Hello w tej sekcji jest toooutline sposób integracji aplikacji hello tooenable dla Replicon.</span><span class="sxs-lookup"><span data-stu-id="18bd3-116">hello objective of this section is toooutline how tooenable hello application integration for Replicon.</span></span>

<span data-ttu-id="18bd3-117">**integracji aplikacji hello tooenable dla Replicon, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="18bd3-117">**tooenable hello application integration for Replicon, perform hello following steps:**</span></span>

1. <span data-ttu-id="18bd3-118">W hello klasycznego portalu Azure, w okienku nawigacji po lewej stronie powitania kliknij **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="18bd3-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="18bd3-119">![Usługi Active Directory](./media/active-directory-saas-replicon-tutorial/IC700993.png "usługi Active Directory")</span><span class="sxs-lookup"><span data-stu-id="18bd3-119">![Active Directory](./media/active-directory-saas-replicon-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="18bd3-120">Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="18bd3-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="18bd3-121">Kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.</span><span class="sxs-lookup"><span data-stu-id="18bd3-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    <span data-ttu-id="18bd3-122">![Aplikacje](./media/active-directory-saas-replicon-tutorial/IC700994.png "aplikacji")</span><span class="sxs-lookup"><span data-stu-id="18bd3-122">![Applications](./media/active-directory-saas-replicon-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="18bd3-123">Kliknij przycisk **Dodaj** u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="18bd3-123">Click **Add** at hello bottom of hello page.</span></span>
   
    <span data-ttu-id="18bd3-124">![Dodaj aplikację](./media/active-directory-saas-replicon-tutorial/IC749321.png "Dodaj aplikację")</span><span class="sxs-lookup"><span data-stu-id="18bd3-124">![Add application](./media/active-directory-saas-replicon-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="18bd3-125">Na powitania **co chcesz toodo** okna dialogowego, kliknij przycisk **dodać aplikację z galerii hello**.</span><span class="sxs-lookup"><span data-stu-id="18bd3-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    <span data-ttu-id="18bd3-126">![Dodawanie aplikacji z gallerry](./media/active-directory-saas-replicon-tutorial/IC749322.png "dodać aplikację z gallerry")</span><span class="sxs-lookup"><span data-stu-id="18bd3-126">![Add an application from gallerry](./media/active-directory-saas-replicon-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="18bd3-127">W hello **pole wyszukiwania**, typ **Replicon**.</span><span class="sxs-lookup"><span data-stu-id="18bd3-127">In hello **search box**, type **Replicon**.</span></span>
   
    <span data-ttu-id="18bd3-128">![Galerii aplikacji](./media/active-directory-saas-replicon-tutorial/IC777799.png "galerii aplikacji")</span><span class="sxs-lookup"><span data-stu-id="18bd3-128">![Application gallery](./media/active-directory-saas-replicon-tutorial/IC777799.png "Application gallery")</span></span>
7. <span data-ttu-id="18bd3-129">Wybierz w okienku wyników hello **Replicon**, a następnie kliknij przycisk **Complete** aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="18bd3-129">In hello results pane, select **Replicon**, and then click **Complete** tooadd hello application.</span></span>
   
    <span data-ttu-id="18bd3-130">![Replicon](./media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")</span><span class="sxs-lookup"><span data-stu-id="18bd3-130">![Replicon](./media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="18bd3-131">Konfigurowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="18bd3-131">Configure single sign-on</span></span>

<span data-ttu-id="18bd3-132">Celem Hello w tej sekcji jest toooutline jak tooenable użytkowników tooauthenticate tooReplicon do swojego konta w usłudze Azure AD przy użyciu Federacji oparte na powitania protokołu SAML.</span><span class="sxs-lookup"><span data-stu-id="18bd3-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooReplicon with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="18bd3-133">**tooconfigure logowanie jednokrotne, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="18bd3-133">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="18bd3-134">W hello klasycznego portalu Azure na powitania **Replicon** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** tooopen hello **skonfigurować rejestrację jednokrotną** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="18bd3-134">In hello Azure classic portal, on hello **Replicon** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="18bd3-135">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-replicon-tutorial/IC777801.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="18bd3-135">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777801.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="18bd3-136">Na powitania **jak ma toosign użytkowników na tooReplicon** wybierz pozycję **usługi Microsoft Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="18bd3-136">On hello **How would you like users toosign on tooReplicon** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="18bd3-137">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-replicon-tutorial/IC777802.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="18bd3-137">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777802.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="18bd3-138">Na powitania **Konfigurowanie adresu URL aplikacji** wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="18bd3-138">On hello **Configure App URL** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="18bd3-139">![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-replicon-tutorial/IC777803.png "skonfigurować adres URL aplikacji")</span><span class="sxs-lookup"><span data-stu-id="18bd3-139">![Configure app URL](./media/active-directory-saas-replicon-tutorial/IC777803.png "Configure app URL")</span></span>
  1. <span data-ttu-id="18bd3-140">W hello **Replicon na adres URL logowania** tekstowym, wpisz adres URL dzierżawy Replicon (np.: *https://na2.replicon.com/company/saml2/sp-sso/post*).</span><span class="sxs-lookup"><span data-stu-id="18bd3-140">In hello **Replicon Sign On URL** textbox, type your Replicon tenant URL (e.g.: *https://na2.replicon.com/company/saml2/sp-sso/post*).</span></span>
  2. <span data-ttu-id="18bd3-141">W hello **adres URL odpowiedzi Replicon** tekstowym, wpisz Replicon Twojego **AssertionConsumerService** adres URL (np.: *https://global.replicon.com/! / saml2/firmy/logowania jednokrotnego/post*).</span><span class="sxs-lookup"><span data-stu-id="18bd3-141">In hello **Replicon Reply URL** textbox, type your Replicon **AssertionConsumerService** URL(e.g.: *https://global.replicon.com/!/saml2/company/sso/post*).</span></span>  
      
     >[!NOTE]
     ><span data-ttu-id="18bd3-142">Można uzyskać adres URL hello hello Replicon metadanych w: **https://global.replicon.com/! /saml2/\<YourCompanyKey\>**.</span><span class="sxs-lookup"><span data-stu-id="18bd3-142">You can get hello URL from hello Replicon metadata at: **https://global.replicon.com/!/saml2/\<YourCompanyKey\>**.</span></span>
     > 
     > 
 
  3. <span data-ttu-id="18bd3-143">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="18bd3-143">Click **Next**.</span></span>

4. <span data-ttu-id="18bd3-144">Na powitania **skonfigurować logowanie jednokrotne w Replicon** strony, toodownload metadanych programu kliknij przycisk **pobierania metadanych**, a następnie zapisz metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="18bd3-144">On hello **Configure single sign-on at Replicon** page, toodownload your metadata, click **Download metadata**, and then save hello metadata on your computer.</span></span>
   
    <span data-ttu-id="18bd3-145">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-replicon-tutorial/IC777804.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="18bd3-145">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777804.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="18bd3-146">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy Replicon jako administrator.</span><span class="sxs-lookup"><span data-stu-id="18bd3-146">In a different web browser window, log into your Replicon company site as an administrator.</span></span>

6. <span data-ttu-id="18bd3-147">tooconfigure SAML 2.0, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="18bd3-147">tooconfigure SAML 2.0, perform hello following steps:</span></span>
   
    <span data-ttu-id="18bd3-148">![Włącz uwierzytelnianie SAML](./media/active-directory-saas-replicon-tutorial/IC777805.png "uwierzytelnianie Włącz SAML")</span><span class="sxs-lookup"><span data-stu-id="18bd3-148">![Enable SAML authentication](./media/active-directory-saas-replicon-tutorial/IC777805.png "Enable SAML authentication")</span></span>
  
  1. <span data-ttu-id="18bd3-149">Witaj toodisplay **EnableSAML Authentication2** okna dialogowego, Dołącz hello następującego adresu URL tooyour, po klucz firmy: **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span><span class="sxs-lookup"><span data-stu-id="18bd3-149">toodisplay hello **EnableSAML Authentication2** dialog, append hello following tooyour URL, after your company key: **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span></span>  
    * <span data-ttu-id="18bd3-150">Oto Hello hello schemat hello pełny adres URL:</span><span class="sxs-lookup"><span data-stu-id="18bd3-150">hello following shows hello schema of hello complete URL:</span></span>  
   <span data-ttu-id="18bd3-151">**https://Na2.replicon.com/\<YourCompanyKey\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span><span class="sxs-lookup"><span data-stu-id="18bd3-151">**https://na2.replicon.com/\<YourCompanyKey\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span></span>
   2. <span data-ttu-id="18bd3-152">Kliknij przycisk hello  **+**  tooexpand hello **v20Configuration** sekcji.</span><span class="sxs-lookup"><span data-stu-id="18bd3-152">Click hello **+** tooexpand hello **v20Configuration** section.</span></span>
   3. <span data-ttu-id="18bd3-153">Kliknij przycisk hello  **+**  tooexpand hello **metaDataConfiguration** sekcji.</span><span class="sxs-lookup"><span data-stu-id="18bd3-153">Click hello **+** tooexpand hello **metaDataConfiguration** section.</span></span>
   4. <span data-ttu-id="18bd3-154">Kliknij przycisk **wybierz plik**, tooselect Twojego pliku XML metadanych dostawcy tożsamości, a następnie kliknij przycisk **przesyłania**.</span><span class="sxs-lookup"><span data-stu-id="18bd3-154">Click **Choose File**, tooselect your identity provider metadata XML file, and click **Submit**.</span></span>

7. <span data-ttu-id="18bd3-155">Na powitania klasycznego portalu Azure, wybierz hello konfiguracji rejestracji jednokrotnej potwierdzenie, a następnie kliknij **Complete** tooclose hello **skonfigurować rejestrację jednokrotną** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="18bd3-155">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="18bd3-156">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-replicon-tutorial/IC778418.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="18bd3-156">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC778418.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="18bd3-157">Skonfiguruj Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="18bd3-157">Configure user provisioning</span></span>

<span data-ttu-id="18bd3-158">W przypadku użytkowników usługi Azure AD toolog kolejności tooenable do Replicon muszą mieć przydzielone do Replicon.</span><span class="sxs-lookup"><span data-stu-id="18bd3-158">In order tooenable Azure AD users toolog into Replicon, they must be provisioned into Replicon.</span></span>  

<span data-ttu-id="18bd3-159">W przypadku hello Replicon Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="18bd3-159">In hello case of Replicon, provisioning is a manual task.</span></span>

<span data-ttu-id="18bd3-160">**tooconfigure aprowizacji użytkowników, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="18bd3-160">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="18bd3-161">W oknie przeglądarki sieci web Zaloguj się do witryny firmy Replicon jako administrator.</span><span class="sxs-lookup"><span data-stu-id="18bd3-161">In a web browser window, log into your Replicon company site as an administrator.</span></span>
2. <span data-ttu-id="18bd3-162">Przejdź za**administracji \> użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="18bd3-162">Go too**Administration \> Users**.</span></span>
   
    <span data-ttu-id="18bd3-163">![Użytkownicy](./media/active-directory-saas-replicon-tutorial/IC777806.png "użytkowników")</span><span class="sxs-lookup"><span data-stu-id="18bd3-163">![Users](./media/active-directory-saas-replicon-tutorial/IC777806.png "Users")</span></span>
3. <span data-ttu-id="18bd3-164">Kliknij przycisk **+ Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="18bd3-164">Click **+Add User**.</span></span>
   
    <span data-ttu-id="18bd3-165">![Dodaj użytkownika](./media/active-directory-saas-replicon-tutorial/IC777807.png "Dodaj użytkownika")</span><span class="sxs-lookup"><span data-stu-id="18bd3-165">![Add User](./media/active-directory-saas-replicon-tutorial/IC777807.png "Add User")</span></span>
4. <span data-ttu-id="18bd3-166">W hello **profilu użytkownika** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="18bd3-166">In hello **User Profile** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="18bd3-167">![Profil użytkownika](./media/active-directory-saas-replicon-tutorial/IC777808.png "profilu użytkownika")</span><span class="sxs-lookup"><span data-stu-id="18bd3-167">![User profile](./media/active-directory-saas-replicon-tutorial/IC777808.png "User profile")</span></span>
   
  1. <span data-ttu-id="18bd3-168">W hello **nazwa logowania** pole tekstowe, typ hello Azure AD adres e-mail użytkownika hello Azure AD ma tooprovision.</span><span class="sxs-lookup"><span data-stu-id="18bd3-168">In hello **Login Name** textbox, type hello Azure AD email address of hello Azure AD user you want tooprovision.</span></span>
  2. <span data-ttu-id="18bd3-169">Jako **typ uwierzytelniania**, wybierz pozycję **logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="18bd3-169">As **Authentication Type**, select **SSO**.</span></span>
  3. <span data-ttu-id="18bd3-170">W hello **działu** tekstowym, wpisz dział hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="18bd3-170">In hello **Department** textbox, type hello user’s department.</span></span>
  4. <span data-ttu-id="18bd3-171">Jako **typu pracownika**, wybierz pozycję **administratora**.</span><span class="sxs-lookup"><span data-stu-id="18bd3-171">As **Employee Type**, select **Administrator**.</span></span>
  5. <span data-ttu-id="18bd3-172">Kliknij przycisk **Zapisz profil użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="18bd3-172">Click **Save User Profile**.</span></span>

>[!NOTE]
><span data-ttu-id="18bd3-173">Możesz użyć innych Replicon użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Replicon tooprovision kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="18bd3-173">You can use any other Replicon user account creation tools or APIs provided by Replicon tooprovision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="18bd3-174">Przypisywanie użytkowników</span><span class="sxs-lookup"><span data-stu-id="18bd3-174">Assign users</span></span>
<span data-ttu-id="18bd3-175">tootest konfiguracji, należy toogrant hello Azure AD użytkownicy mają tooallow przy użyciu Twojej aplikacji tooit dostępu przez przypisywanie ich.</span><span class="sxs-lookup"><span data-stu-id="18bd3-175">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="18bd3-176">**tooassign tooReplicon użytkowników, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="18bd3-176">**tooassign users tooReplicon, perform hello following steps:**</span></span>

1. <span data-ttu-id="18bd3-177">W hello klasycznego portalu Azure Utwórz konto testu.</span><span class="sxs-lookup"><span data-stu-id="18bd3-177">In hello Azure classic portal, create a test account.</span></span>

2. <span data-ttu-id="18bd3-178">Na powitania **Replicon** strona integracji aplikacji, kliknij przycisk **przypisywać użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="18bd3-178">On hello **Replicon** application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="18bd3-179">![Przypisywanie użytkowników](./media/active-directory-saas-replicon-tutorial/IC777809.png "przypisywanie użytkowników")</span><span class="sxs-lookup"><span data-stu-id="18bd3-179">![Assign users](./media/active-directory-saas-replicon-tutorial/IC777809.png "Assign users")</span></span>

3. <span data-ttu-id="18bd3-180">Wybierz użytkownika testowego, kliknij przycisk **przypisać**, a następnie kliknij przycisk **tak** tooconfirm przypisania.</span><span class="sxs-lookup"><span data-stu-id="18bd3-180">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
    <span data-ttu-id="18bd3-181">![Tak](./media/active-directory-saas-replicon-tutorial/IC767830.png "tak")</span><span class="sxs-lookup"><span data-stu-id="18bd3-181">![Yes](./media/active-directory-saas-replicon-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="18bd3-182">Jeśli chcesz tootest jednego ustawienia logowania jednokrotnego, otwórz hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="18bd3-182">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="18bd3-183">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="18bd3-183">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

