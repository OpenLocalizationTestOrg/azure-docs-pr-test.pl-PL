---
title: 'Samouczek: Integracji Azure Active Directory z TOPdesk - bezpiecznego | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak toouse TOPdesk - zabezpieczyć za pomocą usługi Azure Active Directory tooenable logowania jednokrotnego, automatyczne Inicjowanie obsługi i inne!."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 8e149d2d-7849-48ec-9993-31f4ade5fdb4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 10fe420d1691c2845b89c779486ffd6fcd736432
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---secure"></a><span data-ttu-id="62fdd-103">Samouczek: Integracji Azure Active Directory z TOPdesk - bezpieczne</span><span class="sxs-lookup"><span data-stu-id="62fdd-103">Tutorial: Azure Active Directory integration with TOPdesk - Secure</span></span>
<span data-ttu-id="62fdd-104">Celem Hello tego samouczka jest tooshow integracji hello Azure i TOPdesk — zabezpieczenia.</span><span class="sxs-lookup"><span data-stu-id="62fdd-104">hello objective of this tutorial is tooshow hello integration of Azure and TOPdesk - Secure.</span></span>  
<span data-ttu-id="62fdd-105">Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="62fdd-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="62fdd-106">Ważnej subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="62fdd-106">A valid Azure subscription</span></span>
* <span data-ttu-id="62fdd-107">A TOPdesk - bezpieczne logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="62fdd-107">A TOPdesk - Secure single sign-on enabled subscription</span></span>

<span data-ttu-id="62fdd-108">Po ukończeniu tego samouczka, użytkownicy hello Azure AD przypisano tooTOPdesk - bezpiecznego będzie można stanie toosingle logowania do aplikacji hello w Twojej TOPdesk - firmy bezpiecznej witryny (usługi zainicjował dostawcy logowania) lub przy użyciu hello [wprowadzenie Panel dostępu toohello](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="62fdd-108">After completing this tutorial, hello Azure AD users you have assigned tooTOPdesk - Secure will be able toosingle sign into hello application at your TOPdesk - Secure company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="62fdd-109">Scenariusz Hello opisane w tym samouczku składa się z powitania po bloków konstrukcyjnych:</span><span class="sxs-lookup"><span data-stu-id="62fdd-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="62fdd-110">Włączanie integracji aplikacji hello dla TOPdesk - bezpieczne</span><span class="sxs-lookup"><span data-stu-id="62fdd-110">Enabling hello application integration for TOPdesk - Secure</span></span>
2. <span data-ttu-id="62fdd-111">Konfigurowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="62fdd-111">Configuring single sign-on</span></span>
3. <span data-ttu-id="62fdd-112">Konfigurowanie Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="62fdd-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="62fdd-113">Przypisywanie użytkowników</span><span class="sxs-lookup"><span data-stu-id="62fdd-113">Assigning users</span></span>

<span data-ttu-id="62fdd-114">![Scenariusz](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "scenariusza")</span><span class="sxs-lookup"><span data-stu-id="62fdd-114">![Scenario](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "Scenario")</span></span>

## <a name="enabling-hello-application-integration-for-topdesk---secure"></a><span data-ttu-id="62fdd-115">Włączanie integracji aplikacji hello dla TOPdesk - bezpieczne</span><span class="sxs-lookup"><span data-stu-id="62fdd-115">Enabling hello application integration for TOPdesk - Secure</span></span>
<span data-ttu-id="62fdd-116">Celem Hello w tej sekcji jest toooutline sposób integracji aplikacji hello tooenable dla TOPdesk - bezpieczny.</span><span class="sxs-lookup"><span data-stu-id="62fdd-116">hello objective of this section is toooutline how tooenable hello application integration for TOPdesk - Secure.</span></span>

### <a name="tooenable-hello-application-integration-for-topdesk---secure-perform-hello-following-steps"></a><span data-ttu-id="62fdd-117">Integracja aplikacji hello tooenable dla TOPdesk - bezpieczny, wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="62fdd-117">tooenable hello application integration for TOPdesk - Secure, perform hello following steps:</span></span>
1. <span data-ttu-id="62fdd-118">W hello klasycznego portalu Azure, w okienku nawigacji po lewej stronie powitania kliknij **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="62fdd-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="62fdd-119">![Usługi Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "usługi Active Directory")</span><span class="sxs-lookup"><span data-stu-id="62fdd-119">![Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="62fdd-120">Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="62fdd-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="62fdd-121">Kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.</span><span class="sxs-lookup"><span data-stu-id="62fdd-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    <span data-ttu-id="62fdd-122">![Aplikacje](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "aplikacji")</span><span class="sxs-lookup"><span data-stu-id="62fdd-122">![Applications](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="62fdd-123">Kliknij przycisk **Dodaj** u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="62fdd-123">Click **Add** at hello bottom of hello page.</span></span>
   
    <span data-ttu-id="62fdd-124">![Dodaj aplikację](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "Dodaj aplikację")</span><span class="sxs-lookup"><span data-stu-id="62fdd-124">![Add application](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="62fdd-125">Na powitania **co chcesz toodo** okna dialogowego, kliknij przycisk **dodać aplikację z galerii hello**.</span><span class="sxs-lookup"><span data-stu-id="62fdd-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    <span data-ttu-id="62fdd-126">![Dodawanie aplikacji z gallerry](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "dodać aplikację z gallerry")</span><span class="sxs-lookup"><span data-stu-id="62fdd-126">![Add an application from gallerry](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="62fdd-127">W hello **pole wyszukiwania**, typ **TOPdesk - bezpiecznego**.</span><span class="sxs-lookup"><span data-stu-id="62fdd-127">In hello **search box**, type **TOPdesk - Secure**.</span></span>
   
    <span data-ttu-id="62fdd-128">![Galerii aplikacji](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "galerii aplikacji")</span><span class="sxs-lookup"><span data-stu-id="62fdd-128">![Application Gallery](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "Application Gallery")</span></span>

7. <span data-ttu-id="62fdd-129">Wybierz w okienku wyników hello **TOPdesk - bezpiecznego**, a następnie kliknij przycisk **Complete** aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="62fdd-129">In hello results pane, select **TOPdesk - Secure**, and then click **Complete** tooadd hello application.</span></span>
   
    <span data-ttu-id="62fdd-130">![TOPdesk - bezpiecznego](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - bezpieczne")</span><span class="sxs-lookup"><span data-stu-id="62fdd-130">![TOPdesk - Secure](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - Secure")</span></span>

## <a name="configuring-single-sign-on"></a><span data-ttu-id="62fdd-131">Konfigurowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="62fdd-131">Configuring single sign-on</span></span>
<span data-ttu-id="62fdd-132">Celem Hello w tej sekcji jest toooutline jak tooTOPdesk tooauthenticate użytkowników tooenable - zabezpieczyć za pomocą swojego konta w usłudze Azure AD przy użyciu Federacji oparte na powitania protokołu SAML.</span><span class="sxs-lookup"><span data-stu-id="62fdd-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooTOPdesk - Secure with their account in Azure AD using federation based on hello SAML protocol.</span></span>  
<span data-ttu-id="62fdd-133">Konfigurowanie rejestracji jednokrotnej dla TOPdesk - bezpiecznego wymaga tooupload pliku ikony logo.</span><span class="sxs-lookup"><span data-stu-id="62fdd-133">Configuring single sign-on for TOPdesk - Secure requires you tooupload a logo icon file.</span></span> <span data-ttu-id="62fdd-134">Plik ikony hello tooget, skontaktuj się z pomocą hello TOPdesk z pomocą techniczną.</span><span class="sxs-lookup"><span data-stu-id="62fdd-134">tooget hello icon file, contact hello TOPdesk support team.</span></span>

### <a name="tooconfigure-single-sign-on-perform-hello-following-steps"></a><span data-ttu-id="62fdd-135">tooconfigure logowanie jednokrotne, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="62fdd-135">tooconfigure single sign-on, perform hello following steps:</span></span>
1. <span data-ttu-id="62fdd-136">Zaloguj się na tooyour **TOPdesk - bezpiecznego** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="62fdd-136">Sign on tooyour **TOPdesk - Secure** company site as an administrator.</span></span>
2. <span data-ttu-id="62fdd-137">W hello **TOPdesk** menu, kliknij przycisk **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="62fdd-137">In hello **TOPdesk** menu, click **Settings**.</span></span>
   
    <span data-ttu-id="62fdd-138">![Ustawienia](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "ustawienia")</span><span class="sxs-lookup"><span data-stu-id="62fdd-138">![Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Settings")</span></span>

3. <span data-ttu-id="62fdd-139">Kliknij przycisk **ustawienia logowania**.</span><span class="sxs-lookup"><span data-stu-id="62fdd-139">Click **Login Settings**.</span></span>
   
    <span data-ttu-id="62fdd-140">![Ustawienia logowania](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "ustawienia logowania")</span><span class="sxs-lookup"><span data-stu-id="62fdd-140">![Login Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")</span></span>

4. <span data-ttu-id="62fdd-141">Rozwiń węzeł hello **ustawienia logowania** menu, a następnie kliknij przycisk **ogólne**.</span><span class="sxs-lookup"><span data-stu-id="62fdd-141">Expand hello **Login Settings** menu, and then click **General**.</span></span>
   
    <span data-ttu-id="62fdd-142">![Ogólne](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "ogólne")</span><span class="sxs-lookup"><span data-stu-id="62fdd-142">![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span></span>

5. <span data-ttu-id="62fdd-143">W hello **bezpiecznego** sekcji hello **logowania SAML** konfiguracji sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="62fdd-143">In hello **Secure** section of hello **SAML login** configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="62fdd-144">![Ustawienia techniczne](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "ustawienia techniczne")</span><span class="sxs-lookup"><span data-stu-id="62fdd-144">![Technical Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "Technical Settings")</span></span>
   
    <span data-ttu-id="62fdd-145">a.</span><span class="sxs-lookup"><span data-stu-id="62fdd-145">a.</span></span> <span data-ttu-id="62fdd-146">Kliknij przycisk **Pobierz** toodownload hello pliku metadanych publicznego, a następnie zapisz go lokalnie na komputerze.</span><span class="sxs-lookup"><span data-stu-id="62fdd-146">Click **Download** toodownload hello public metadata file, and then save it locally on your computer.</span></span>
   
    <span data-ttu-id="62fdd-147">b.</span><span class="sxs-lookup"><span data-stu-id="62fdd-147">b.</span></span> <span data-ttu-id="62fdd-148">Otwórz plik metadanych hello, a następnie zlokalizuj hello **AssertionConsumerService** węzła.</span><span class="sxs-lookup"><span data-stu-id="62fdd-148">Open hello metadata file, and then locate hello **AssertionConsumerService** node.</span></span>
    
    <span data-ttu-id="62fdd-149">![Usługa konsumenta potwierdzenia](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "potwierdzenia klienta usługi")</span><span class="sxs-lookup"><span data-stu-id="62fdd-149">![Assertion Consumer Service](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "Assertion Consumer Service")</span></span>
   
    <span data-ttu-id="62fdd-150">c.</span><span class="sxs-lookup"><span data-stu-id="62fdd-150">c.</span></span> <span data-ttu-id="62fdd-151">Kopiuj hello **AssertionConsumerService** wartości.</span><span class="sxs-lookup"><span data-stu-id="62fdd-151">Copy hello **AssertionConsumerService** value.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="62fdd-152">Będzie konieczne hello wartość hello **Konfigurowanie adresu URL aplikacji** dalszej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="62fdd-152">You will need hello value in hello **Configure App URL** section later in this tutorial.</span></span>
    > 
    > 

6. <span data-ttu-id="62fdd-153">W oknie przeglądarki innej witryny sieci web, zaloguj się do Twojego **klasycznego portalu Azure** jako administrator.</span><span class="sxs-lookup"><span data-stu-id="62fdd-153">In a different web browser window, log into your **Azure classic portal** as an administrator.</span></span>

7. <span data-ttu-id="62fdd-154">Na powitania **TOPdesk - bezpiecznego** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** tooopen hello ** skonfigurować rejestrację jednokrotną ** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="62fdd-154">On hello **TOPdesk - Secure** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On ** dialog.</span></span>
   
    <span data-ttu-id="62fdd-155">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="62fdd-155">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "Configure Single Sign-On")</span></span>

8. <span data-ttu-id="62fdd-156">Na powitania **jak czy jak toosign użytkowników na tooTOPdesk - Secure** wybierz pozycję **usługi Microsoft Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="62fdd-156">On hello **How would you like users toosign on tooTOPdesk - Secure** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="62fdd-157">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="62fdd-157">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "Configure Single Sign-On")</span></span>

9. <span data-ttu-id="62fdd-158">Na powitania **Konfigurowanie adresu URL aplikacji** wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="62fdd-158">On hello **Configure App URL** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="62fdd-159">![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "skonfigurować adres URL aplikacji")</span><span class="sxs-lookup"><span data-stu-id="62fdd-159">![Configure App URL](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "Configure App URL")</span></span>
   
    <span data-ttu-id="62fdd-160">a.</span><span class="sxs-lookup"><span data-stu-id="62fdd-160">a.</span></span> <span data-ttu-id="62fdd-161">W hello **TOPdesk - bezpiecznego logowania na adres URL** pole tekstowe, wprowadź adres URL hello używany przez Twoje toosign użytkowników do Twojej TOPdesk - zabezpieczonej aplikacji (np.: "*https://qssolutions.topdesk.net*").</span><span class="sxs-lookup"><span data-stu-id="62fdd-161">In hello **TOPdesk - Secure Sign On URL** textbox, type hello URL used by your users toosign into your TOPdesk - Secure application (e.g.: "*https://qssolutions.topdesk.net*").</span></span>
   
    <span data-ttu-id="62fdd-162">b.</span><span class="sxs-lookup"><span data-stu-id="62fdd-162">b.</span></span> <span data-ttu-id="62fdd-163">W hello **TOPdesk — publiczny adres URL odpowiedzi** pole tekstowe, Wklej hello **TOPdesk - bezpiecznego adresu URL AssertionConsumerService** (np.: "*https://qssolutions.topdesk.net/tas/public/login/saml*")</span><span class="sxs-lookup"><span data-stu-id="62fdd-163">In hello **TOPdesk – Public Reply URL** textbox, paste hello **TOPdesk - Secure AssertionConsumerService URL** (e.g.: "*https://qssolutions.topdesk.net/tas/public/login/saml*")</span></span>
   
    <span data-ttu-id="62fdd-164">c.</span><span class="sxs-lookup"><span data-stu-id="62fdd-164">c.</span></span> <span data-ttu-id="62fdd-165">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="62fdd-165">Click **Next**.</span></span>

10. <span data-ttu-id="62fdd-166">Na powitania **skonfigurować logowanie jednokrotne w TOPdesk - bezpiecznego** strony, toodownload pliku metadanych, kliknij przycisk **pobierania metadanych**, a następnie zapisz plik hello lokalnie na komputerze.</span><span class="sxs-lookup"><span data-stu-id="62fdd-166">On hello **Configure single sign-on at TOPdesk - Secure** page, toodownload your metadata file, click **Download metadata**, and then save hello file locally on your computer.</span></span>
    
    <span data-ttu-id="62fdd-167">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="62fdd-167">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "Configure Single Sign-On")</span></span>

11. <span data-ttu-id="62fdd-168">toocreate plik certyfikatu, należy wykonać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="62fdd-168">toocreate a certificate file, perform hello following steps:</span></span>
    
    <span data-ttu-id="62fdd-169">![Certyfikat](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "certyfikatu")</span><span class="sxs-lookup"><span data-stu-id="62fdd-169">![Certificate](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "Certificate")</span></span>
    
    <span data-ttu-id="62fdd-170">a.</span><span class="sxs-lookup"><span data-stu-id="62fdd-170">a.</span></span> <span data-ttu-id="62fdd-171">Plik metadanych pobranych hello otwarte.</span><span class="sxs-lookup"><span data-stu-id="62fdd-171">Open hello downloaded metadata file.</span></span>
    <span data-ttu-id="62fdd-172">b.</span><span class="sxs-lookup"><span data-stu-id="62fdd-172">b.</span></span> <span data-ttu-id="62fdd-173">Rozwiń węzeł hello **RoleDescriptor** węzła, który ma **xsi: type** z **przekazywani: ApplicationServiceType**.</span><span class="sxs-lookup"><span data-stu-id="62fdd-173">Expand hello **RoleDescriptor** node that has a **xsi:type** of **fed:ApplicationServiceType**.</span></span>
    <span data-ttu-id="62fdd-174">c.</span><span class="sxs-lookup"><span data-stu-id="62fdd-174">c.</span></span> <span data-ttu-id="62fdd-175">Skopiuj wartość hello hello **X509Certificate** węzła.</span><span class="sxs-lookup"><span data-stu-id="62fdd-175">Copy hello value of hello **X509Certificate** node.</span></span>
    <span data-ttu-id="62fdd-176">d.</span><span class="sxs-lookup"><span data-stu-id="62fdd-176">d.</span></span> <span data-ttu-id="62fdd-177">Zapisz hello skopiowane **X509Certificate** wartość lokalnie na komputerze w pliku.</span><span class="sxs-lookup"><span data-stu-id="62fdd-177">Save hello copied **X509Certificate** value locally on your computer in a file.</span></span>

12. <span data-ttu-id="62fdd-178">W Twojej TOPdesk - zabezpieczenie witryny firmy, w hello **TOPdesk** menu, kliknij przycisk **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="62fdd-178">On your TOPdesk - Secure company site, in hello **TOPdesk** menu, click **Settings**.</span></span>
    
    <span data-ttu-id="62fdd-179">![Ustawienia](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "ustawienia")</span><span class="sxs-lookup"><span data-stu-id="62fdd-179">![Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Settings")</span></span>

13. <span data-ttu-id="62fdd-180">Kliknij przycisk **ustawienia logowania**.</span><span class="sxs-lookup"><span data-stu-id="62fdd-180">Click **Login Settings**.</span></span>
    
    <span data-ttu-id="62fdd-181">![Ustawienia logowania](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "ustawienia logowania")</span><span class="sxs-lookup"><span data-stu-id="62fdd-181">![Login Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")</span></span>

14. <span data-ttu-id="62fdd-182">Rozwiń węzeł hello **ustawienia logowania** menu, a następnie kliknij przycisk **ogólne**.</span><span class="sxs-lookup"><span data-stu-id="62fdd-182">Expand hello **Login Settings** menu, and then click **General**.</span></span>
    
    <span data-ttu-id="62fdd-183">![Ogólne](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "ogólne")</span><span class="sxs-lookup"><span data-stu-id="62fdd-183">![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span></span>

15. <span data-ttu-id="62fdd-184">W hello **publicznego** kliknij **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="62fdd-184">In hello **Public** section, click **Add**.</span></span>
    
    <span data-ttu-id="62fdd-185">![Dodaj](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "Dodaj")</span><span class="sxs-lookup"><span data-stu-id="62fdd-185">![Add](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "Add")</span></span>

16. <span data-ttu-id="62fdd-186">Na powitania **Asystenta konfiguracji SAML** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="62fdd-186">On hello **SAML configuration assistant** dialog page, perform hello following steps:</span></span>
    
    <span data-ttu-id="62fdd-187">![Asystent konfiguracji SAML](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "Asystenta konfiguracji SAML")</span><span class="sxs-lookup"><span data-stu-id="62fdd-187">![SAML Configuration Assistant](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "SAML Configuration Assistant")</span></span>
    
    <span data-ttu-id="62fdd-188">a.</span><span class="sxs-lookup"><span data-stu-id="62fdd-188">a.</span></span> <span data-ttu-id="62fdd-189">tooupload metadanych pobranych plików, w obszarze **metadanych Federacji**, kliknij przycisk **Przeglądaj**.</span><span class="sxs-lookup"><span data-stu-id="62fdd-189">tooupload your downloaded metadata file, under **Federation Metadata**, click **Browse**.</span></span>

    <span data-ttu-id="62fdd-190">b.</span><span class="sxs-lookup"><span data-stu-id="62fdd-190">b.</span></span> <span data-ttu-id="62fdd-191">tooupload pliku certyfikatu, w obszarze **certyfikatu (RSA)**, kliknij przycisk **Przeglądaj**.</span><span class="sxs-lookup"><span data-stu-id="62fdd-191">tooupload your certificate file, under **Certificate (RSA)**, click **Browse**.</span></span>

    <span data-ttu-id="62fdd-192">c.</span><span class="sxs-lookup"><span data-stu-id="62fdd-192">c.</span></span> <span data-ttu-id="62fdd-193">plik z logo hello tooupload uzyskano z zespołem pomocy technicznej TOPdesk hello, w obszarze **ikona Logo**, kliknij przycisk **Przeglądaj**.</span><span class="sxs-lookup"><span data-stu-id="62fdd-193">tooupload hello logo file you got from hello TOPdesk support team, under **Logo icon**, click **Browse**.</span></span>

    <span data-ttu-id="62fdd-194">d.</span><span class="sxs-lookup"><span data-stu-id="62fdd-194">d.</span></span> <span data-ttu-id="62fdd-195">W hello **atrybutu nazwy użytkownika** pole tekstowe, typ **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="62fdd-195">In hello **User name attribute** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="62fdd-196">e.</span><span class="sxs-lookup"><span data-stu-id="62fdd-196">e.</span></span> <span data-ttu-id="62fdd-197">W hello **Nazwa wyświetlana** tekstowym, wpisz nazwę dla danej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="62fdd-197">In hello **Display name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="62fdd-198">f.</span><span class="sxs-lookup"><span data-stu-id="62fdd-198">f.</span></span> <span data-ttu-id="62fdd-199">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="62fdd-199">Click **Save**.</span></span>

17. <span data-ttu-id="62fdd-200">Na powitania klasycznego portalu Azure, wybierz hello konfiguracji rejestracji jednokrotnej potwierdzenie, a następnie kliknij **Complete** tooclose hello **skonfigurować rejestrację jednokrotną** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="62fdd-200">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="62fdd-201">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="62fdd-201">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "Configure Single Sign-On")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="62fdd-202">Konfigurowanie Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="62fdd-202">Configuring user provisioning</span></span>
<span data-ttu-id="62fdd-203">W kolejności tooenable usługi Azure AD użytkownicy toolog do TOPdesk - bezpieczny, ich muszą mieć przydzielone do TOPdesk - bezpieczny.</span><span class="sxs-lookup"><span data-stu-id="62fdd-203">In order tooenable Azure AD users toolog into TOPdesk - Secure, they must be provisioned into TOPdesk - Secure.</span></span>  
<span data-ttu-id="62fdd-204">W przypadku hello TOPdesk - bezpieczny, inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="62fdd-204">In hello case of TOPdesk - Secure, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="62fdd-205">tooconfigure aprowizacji użytkowników, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="62fdd-205">tooconfigure user provisioning, perform hello following steps:</span></span>
1. <span data-ttu-id="62fdd-206">Zaloguj się na tooyour **TOPdesk - bezpiecznego** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="62fdd-206">Sign on tooyour **TOPdesk - Secure** company site as administrator.</span></span>
2. <span data-ttu-id="62fdd-207">W menu hello na górze hello, kliknij przycisk **TOPdesk \> nowy \> pliki obsługi \> Operator**.</span><span class="sxs-lookup"><span data-stu-id="62fdd-207">In hello menu on hello top, click **TOPdesk \> New \> Support Files \> Operator**.</span></span>
   
    <span data-ttu-id="62fdd-208">![Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "— Operator")</span><span class="sxs-lookup"><span data-stu-id="62fdd-208">![Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "Operator")</span></span>

3. <span data-ttu-id="62fdd-209">Na powitania **operatora New** okna dialogowego, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="62fdd-209">On hello **New Operator** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="62fdd-210">![New Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "New — Operator")</span><span class="sxs-lookup"><span data-stu-id="62fdd-210">![New Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "New Operator")</span></span>
   
    <span data-ttu-id="62fdd-211">a.</span><span class="sxs-lookup"><span data-stu-id="62fdd-211">a.</span></span> <span data-ttu-id="62fdd-212">Kliknij kartę Ogólne hello.</span><span class="sxs-lookup"><span data-stu-id="62fdd-212">Click hello General tab.</span></span>
   
    <span data-ttu-id="62fdd-213">b.</span><span class="sxs-lookup"><span data-stu-id="62fdd-213">b.</span></span> <span data-ttu-id="62fdd-214">W hello **nazwisko** textbox hello **ogólne** typu hello nazwisko prawidłowe konto usługi Azure Active Directory ma tooprovision, sekcji.</span><span class="sxs-lookup"><span data-stu-id="62fdd-214">In hello **Surname** textbox of hello **General** section, type hello last name of a valid Azure Active Directory account you want tooprovision.</span></span>
   
    <span data-ttu-id="62fdd-215">c.</span><span class="sxs-lookup"><span data-stu-id="62fdd-215">c.</span></span> <span data-ttu-id="62fdd-216">Wybierz **lokacji** konta hello w hello **lokalizacji** sekcji.</span><span class="sxs-lookup"><span data-stu-id="62fdd-216">Select a **Site** for hello account in hello **Location** section.</span></span>
   
    <span data-ttu-id="62fdd-217">d.</span><span class="sxs-lookup"><span data-stu-id="62fdd-217">d.</span></span> <span data-ttu-id="62fdd-218">W hello **nazwa logowania** textbox hello **logowania TOPdesk** wpisz nazwę logowania dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="62fdd-218">In hello **Login Name** textbox of hello **TOPdesk Login** section, type a login name for your user.</span></span>
   
    <span data-ttu-id="62fdd-219">e.</span><span class="sxs-lookup"><span data-stu-id="62fdd-219">e.</span></span> <span data-ttu-id="62fdd-220">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="62fdd-220">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="62fdd-221">Można użyć dowolnego innych TOPdesk - bezpieczne konta narzędzia do tworzenia lub interfejsów API dostarczonych przez TOPdesk - Secure tooprovision kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="62fdd-221">You can use any other TOPdesk - Secure user account creation tools or APIs provided by TOPdesk - Secure tooprovision AAD user accounts.</span></span>
> 
> 

## <a name="assigning-users"></a><span data-ttu-id="62fdd-222">Przypisywanie użytkowników</span><span class="sxs-lookup"><span data-stu-id="62fdd-222">Assigning users</span></span>
<span data-ttu-id="62fdd-223">tootest konfiguracji, należy toogrant hello Azure AD użytkownicy mają tooallow przy użyciu Twojej aplikacji tooit dostępu przez przypisywanie ich.</span><span class="sxs-lookup"><span data-stu-id="62fdd-223">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

### <a name="tooassign-users-tootopdesk---secure-perform-hello-following-steps"></a><span data-ttu-id="62fdd-224">tooTOPdesk użytkowników tooassign - bezpieczny, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="62fdd-224">tooassign users tooTOPdesk - Secure, perform hello following steps:</span></span>
1. <span data-ttu-id="62fdd-225">W hello klasycznego portalu Azure Utwórz konto testu.</span><span class="sxs-lookup"><span data-stu-id="62fdd-225">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="62fdd-226">Na powitania ** TOPdesk - bezpiecznego ** strona integracji aplikacji, kliknij przycisk **przypisywać użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="62fdd-226">On hello **TOPdesk - Secure **application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="62fdd-227">![Przypisywanie użytkowników](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "przypisywanie użytkowników")</span><span class="sxs-lookup"><span data-stu-id="62fdd-227">![Assign Users](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "Assign Users")</span></span>

3. <span data-ttu-id="62fdd-228">Wybierz użytkownika testowego, kliknij przycisk **przypisać**, a następnie kliknij przycisk **tak** tooconfirm przypisania.</span><span class="sxs-lookup"><span data-stu-id="62fdd-228">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
    <span data-ttu-id="62fdd-229">![Tak](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "tak")</span><span class="sxs-lookup"><span data-stu-id="62fdd-229">![Yes](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="62fdd-230">Jeśli chcesz tootest jednego ustawienia logowania jednokrotnego, otwórz hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="62fdd-230">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="62fdd-231">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="62fdd-231">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

