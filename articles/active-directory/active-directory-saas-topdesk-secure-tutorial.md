---
title: 'Samouczek: Integracji Azure Active Directory z TOPdesk - bezpiecznego | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak używać TOPdesk - zabezpieczyć za pomocą usługi Azure Active Directory, aby włączyć logowanie jednokrotne, automatyczne Inicjowanie obsługi i inne!."
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
ms.openlocfilehash: 28f0542dbe87bb34c83a7852db7c3a9fef055ce9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---secure"></a><span data-ttu-id="bcb1c-103">Samouczek: Integracji Azure Active Directory z TOPdesk - bezpieczne</span><span class="sxs-lookup"><span data-stu-id="bcb1c-103">Tutorial: Azure Active Directory integration with TOPdesk - Secure</span></span>
<span data-ttu-id="bcb1c-104">Celem tego samouczka jest pokazanie integracji Azure i TOPdesk - bezpieczny.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-104">The objective of this tutorial is to show the integration of Azure and TOPdesk - Secure.</span></span>  
<span data-ttu-id="bcb1c-105">Scenariusz opisany w tym samouczku założono, że już następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="bcb1c-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="bcb1c-106">Ważnej subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="bcb1c-106">A valid Azure subscription</span></span>
* <span data-ttu-id="bcb1c-107">A TOPdesk - bezpieczne logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="bcb1c-107">A TOPdesk - Secure single sign-on enabled subscription</span></span>

<span data-ttu-id="bcb1c-108">Ten samouczek użytkowników usługi Azure AD, zostały przypisane do TOPdesk - bezpiecznego będzie można funkcji logowania jednokrotnego do aplikacji w TOPdesk - firmy bezpiecznej witryny (usługi zainicjował dostawcy logowania) lub przy użyciu [wprowadzenie dostępu Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bcb1c-108">After completing this tutorial, the Azure AD users you have assigned to TOPdesk - Secure will be able to single sign into the application at your TOPdesk - Secure company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="bcb1c-109">Scenariusz opisany w tym samouczku składa się z następujących bloków konstrukcyjnych:</span><span class="sxs-lookup"><span data-stu-id="bcb1c-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="bcb1c-110">Włączanie integracji aplikacji dla TOPdesk - bezpieczne</span><span class="sxs-lookup"><span data-stu-id="bcb1c-110">Enabling the application integration for TOPdesk - Secure</span></span>
2. <span data-ttu-id="bcb1c-111">Konfigurowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="bcb1c-111">Configuring single sign-on</span></span>
3. <span data-ttu-id="bcb1c-112">Konfigurowanie Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="bcb1c-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="bcb1c-113">Przypisywanie użytkowników</span><span class="sxs-lookup"><span data-stu-id="bcb1c-113">Assigning users</span></span>

<span data-ttu-id="bcb1c-114">![Scenariusz](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "scenariusza")</span><span class="sxs-lookup"><span data-stu-id="bcb1c-114">![Scenario](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-topdesk---secure"></a><span data-ttu-id="bcb1c-115">Włączanie integracji aplikacji dla TOPdesk - bezpieczne</span><span class="sxs-lookup"><span data-stu-id="bcb1c-115">Enabling the application integration for TOPdesk - Secure</span></span>
<span data-ttu-id="bcb1c-116">Celem tej sekcji jest przedstawiają sposób włączania integracji aplikacji dla TOPdesk - bezpieczny.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-116">The objective of this section is to outline how to enable the application integration for TOPdesk - Secure.</span></span>

### <a name="to-enable-the-application-integration-for-topdesk---secure-perform-the-following-steps"></a><span data-ttu-id="bcb1c-117">W celu umożliwienia integracji aplikacji programu TOPdesk - bezpieczny, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="bcb1c-117">To enable the application integration for TOPdesk - Secure, perform the following steps:</span></span>
1. <span data-ttu-id="bcb1c-118">W klasycznym portalu Azure, w okienku nawigacji po lewej stronie kliknij **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="bcb1c-119">![Usługi Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "usługi Active Directory")</span><span class="sxs-lookup"><span data-stu-id="bcb1c-119">![Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="bcb1c-120">Z **katalogu** listy, wybierz katalog, dla którego chcesz włączyć integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="bcb1c-121">Aby otworzyć widok aplikacji, w widoku katalogu, kliknij przycisk **aplikacji** w menu u góry.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="bcb1c-122">![Aplikacje](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "aplikacji")</span><span class="sxs-lookup"><span data-stu-id="bcb1c-122">![Applications](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="bcb1c-123">Kliknij przycisk **Dodaj** w dolnej części strony.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="bcb1c-124">![Dodaj aplikację](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "Dodaj aplikację")</span><span class="sxs-lookup"><span data-stu-id="bcb1c-124">![Add application](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="bcb1c-125">Na **co chcesz zrobić** okna dialogowego, kliknij przycisk **dodać aplikację z galerii**.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="bcb1c-126">![Dodawanie aplikacji z gallerry](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "dodać aplikację z gallerry")</span><span class="sxs-lookup"><span data-stu-id="bcb1c-126">![Add an application from gallerry](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="bcb1c-127">W **pole wyszukiwania**, typ **TOPdesk - bezpiecznego**.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-127">In the **search box**, type **TOPdesk - Secure**.</span></span>
   
    <span data-ttu-id="bcb1c-128">![Galerii aplikacji](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "galerii aplikacji")</span><span class="sxs-lookup"><span data-stu-id="bcb1c-128">![Application Gallery](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "Application Gallery")</span></span>

7. <span data-ttu-id="bcb1c-129">W okienku wyników wybierz **TOPdesk - bezpiecznego**, a następnie kliknij przycisk **Complete** można dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-129">In the results pane, select **TOPdesk - Secure**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="bcb1c-130">![TOPdesk - bezpiecznego](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - bezpieczne")</span><span class="sxs-lookup"><span data-stu-id="bcb1c-130">![TOPdesk - Secure](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - Secure")</span></span>

## <a name="configuring-single-sign-on"></a><span data-ttu-id="bcb1c-131">Konfigurowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="bcb1c-131">Configuring single sign-on</span></span>
<span data-ttu-id="bcb1c-132">Celem tej sekcji jest przedstawiają sposób umożliwić użytkownikom uwierzytelnianie na TOPdesk — zabezpieczyć za pomocą swojego konta w usłudze Azure AD przy użyciu federacyjnego na podstawie protokołu SAML.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-132">The objective of this section is to outline how to enable users to authenticate to TOPdesk - Secure with their account in Azure AD using federation based on the SAML protocol.</span></span>  
<span data-ttu-id="bcb1c-133">Konfigurowanie rejestracji jednokrotnej dla TOPdesk - bezpiecznego wymaga przekazać plik ikony logo.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-133">Configuring single sign-on for TOPdesk - Secure requires you to upload a logo icon file.</span></span> <span data-ttu-id="bcb1c-134">Aby uzyskać plik ikony, skontaktuj się z zespołem pomocy technicznej TOPdesk.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-134">To get the icon file, contact the TOPdesk support team.</span></span>

### <a name="to-configure-single-sign-on-perform-the-following-steps"></a><span data-ttu-id="bcb1c-135">Aby skonfigurować rejestrację jednokrotną, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="bcb1c-135">To configure single sign-on, perform the following steps:</span></span>
1. <span data-ttu-id="bcb1c-136">Zaloguj się na Twojej **TOPdesk - bezpiecznego** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-136">Sign on to your **TOPdesk - Secure** company site as an administrator.</span></span>
2. <span data-ttu-id="bcb1c-137">W **TOPdesk** menu, kliknij przycisk **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-137">In the **TOPdesk** menu, click **Settings**.</span></span>
   
    <span data-ttu-id="bcb1c-138">![Ustawienia](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "ustawienia")</span><span class="sxs-lookup"><span data-stu-id="bcb1c-138">![Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Settings")</span></span>

3. <span data-ttu-id="bcb1c-139">Kliknij przycisk **ustawienia logowania**.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-139">Click **Login Settings**.</span></span>
   
    <span data-ttu-id="bcb1c-140">![Ustawienia logowania](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "ustawienia logowania")</span><span class="sxs-lookup"><span data-stu-id="bcb1c-140">![Login Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")</span></span>

4. <span data-ttu-id="bcb1c-141">Rozwiń węzeł **ustawienia logowania** menu, a następnie kliknij przycisk **ogólne**.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-141">Expand the **Login Settings** menu, and then click **General**.</span></span>
   
    <span data-ttu-id="bcb1c-142">![Ogólne](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "ogólne")</span><span class="sxs-lookup"><span data-stu-id="bcb1c-142">![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span></span>

5. <span data-ttu-id="bcb1c-143">W **bezpiecznego** sekcji **logowania SAML** konfiguracji sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="bcb1c-143">In the **Secure** section of the **SAML login** configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="bcb1c-144">![Ustawienia techniczne](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "ustawienia techniczne")</span><span class="sxs-lookup"><span data-stu-id="bcb1c-144">![Technical Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "Technical Settings")</span></span>
   
    <span data-ttu-id="bcb1c-145">a.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-145">a.</span></span> <span data-ttu-id="bcb1c-146">Kliknij przycisk **Pobierz** można pobrać pliku metadanych publicznego, a następnie zapisz go lokalnie na komputerze.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-146">Click **Download** to download the public metadata file, and then save it locally on your computer.</span></span>
   
    <span data-ttu-id="bcb1c-147">b.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-147">b.</span></span> <span data-ttu-id="bcb1c-148">Otwórz plik metadanych, a następnie zlokalizuj **AssertionConsumerService** węzła.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-148">Open the metadata file, and then locate the **AssertionConsumerService** node.</span></span>
    
    <span data-ttu-id="bcb1c-149">![Usługa konsumenta potwierdzenia](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "potwierdzenia klienta usługi")</span><span class="sxs-lookup"><span data-stu-id="bcb1c-149">![Assertion Consumer Service](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "Assertion Consumer Service")</span></span>
   
    <span data-ttu-id="bcb1c-150">c.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-150">c.</span></span> <span data-ttu-id="bcb1c-151">Kopiuj **AssertionConsumerService** wartości.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-151">Copy the **AssertionConsumerService** value.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="bcb1c-152">Konieczne będzie wartość **Konfigurowanie adresu URL aplikacji** dalszej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-152">You will need the value in the **Configure App URL** section later in this tutorial.</span></span>
    > 
    > 

6. <span data-ttu-id="bcb1c-153">W oknie przeglądarki innej witryny sieci web, zaloguj się do Twojego **klasycznego portalu Azure** jako administrator.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-153">In a different web browser window, log into your **Azure classic portal** as an administrator.</span></span>

7. <span data-ttu-id="bcb1c-154">Na **TOPdesk - bezpiecznego** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** otworzyć ** skonfigurować rejestrację jednokrotną ** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-154">On the **TOPdesk - Secure** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On ** dialog.</span></span>
   
    <span data-ttu-id="bcb1c-155">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="bcb1c-155">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "Configure Single Sign-On")</span></span>

8. <span data-ttu-id="bcb1c-156">Na **jak chcesz użytkownikom zalogować się na TOPdesk - bezpiecznego** wybierz pozycję **usługi Microsoft Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-156">On the **How would you like users to sign on to TOPdesk - Secure** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="bcb1c-157">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="bcb1c-157">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "Configure Single Sign-On")</span></span>

9. <span data-ttu-id="bcb1c-158">Na **Konfigurowanie adresu URL aplikacji** wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="bcb1c-158">On the **Configure App URL** page, perform the following steps:</span></span>
   
    <span data-ttu-id="bcb1c-159">![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "skonfigurować adres URL aplikacji")</span><span class="sxs-lookup"><span data-stu-id="bcb1c-159">![Configure App URL](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "Configure App URL")</span></span>
   
    <span data-ttu-id="bcb1c-160">a.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-160">a.</span></span> <span data-ttu-id="bcb1c-161">W **TOPdesk - bezpiecznego logowania na adres URL** tekstowym, wpisz adres URL używany przez użytkowników do logowania się do sieci TOPdesk - zabezpieczonej aplikacji (np.: "*https://qssolutions.topdesk.net*").</span><span class="sxs-lookup"><span data-stu-id="bcb1c-161">In the **TOPdesk - Secure Sign On URL** textbox, type the URL used by your users to sign into your TOPdesk - Secure application (e.g.: "*https://qssolutions.topdesk.net*").</span></span>
   
    <span data-ttu-id="bcb1c-162">b.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-162">b.</span></span> <span data-ttu-id="bcb1c-163">W **TOPdesk — publiczny adres URL odpowiedzi** pole tekstowe, Wklej **TOPdesk - bezpiecznego adresu URL AssertionConsumerService** (np.: "*https://qssolutions.topdesk.net/tas/public/login/saml*")</span><span class="sxs-lookup"><span data-stu-id="bcb1c-163">In the **TOPdesk – Public Reply URL** textbox, paste the **TOPdesk - Secure AssertionConsumerService URL** (e.g.: "*https://qssolutions.topdesk.net/tas/public/login/saml*")</span></span>
   
    <span data-ttu-id="bcb1c-164">c.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-164">c.</span></span> <span data-ttu-id="bcb1c-165">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-165">Click **Next**.</span></span>

10. <span data-ttu-id="bcb1c-166">Na **skonfigurować logowanie jednokrotne w TOPdesk - bezpiecznego** można pobrać pliku metadanych, kliknij przycisk **pobierania metadanych**, a następnie zapisz plik lokalnie na komputerze.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-166">On the **Configure single sign-on at TOPdesk - Secure** page, to download your metadata file, click **Download metadata**, and then save the file locally on your computer.</span></span>
    
    <span data-ttu-id="bcb1c-167">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="bcb1c-167">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "Configure Single Sign-On")</span></span>

11. <span data-ttu-id="bcb1c-168">Aby utworzyć plik certyfikatu, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="bcb1c-168">To create a certificate file, perform the following steps:</span></span>
    
    <span data-ttu-id="bcb1c-169">![Certyfikat](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "certyfikatu")</span><span class="sxs-lookup"><span data-stu-id="bcb1c-169">![Certificate](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "Certificate")</span></span>
    
    <span data-ttu-id="bcb1c-170">a.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-170">a.</span></span> <span data-ttu-id="bcb1c-171">Otwórz plik pobrany metadanych.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-171">Open the downloaded metadata file.</span></span>
    <span data-ttu-id="bcb1c-172">b.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-172">b.</span></span> <span data-ttu-id="bcb1c-173">Rozwiń węzeł **RoleDescriptor** węzła, który ma **xsi: type** z **przekazywani: ApplicationServiceType**.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-173">Expand the **RoleDescriptor** node that has a **xsi:type** of **fed:ApplicationServiceType**.</span></span>
    <span data-ttu-id="bcb1c-174">c.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-174">c.</span></span> <span data-ttu-id="bcb1c-175">Skopiuj wartość **X509Certificate** węzła.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-175">Copy the value of the **X509Certificate** node.</span></span>
    <span data-ttu-id="bcb1c-176">d.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-176">d.</span></span> <span data-ttu-id="bcb1c-177">Zapisz skopiowanych **X509Certificate** wartość lokalnie na komputerze w pliku.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-177">Save the copied **X509Certificate** value locally on your computer in a file.</span></span>

12. <span data-ttu-id="bcb1c-178">W Twojej TOPdesk - zabezpieczenie witryny firmy, w **TOPdesk** menu, kliknij przycisk **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-178">On your TOPdesk - Secure company site, in the **TOPdesk** menu, click **Settings**.</span></span>
    
    <span data-ttu-id="bcb1c-179">![Ustawienia](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "ustawienia")</span><span class="sxs-lookup"><span data-stu-id="bcb1c-179">![Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Settings")</span></span>

13. <span data-ttu-id="bcb1c-180">Kliknij przycisk **ustawienia logowania**.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-180">Click **Login Settings**.</span></span>
    
    <span data-ttu-id="bcb1c-181">![Ustawienia logowania](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "ustawienia logowania")</span><span class="sxs-lookup"><span data-stu-id="bcb1c-181">![Login Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")</span></span>

14. <span data-ttu-id="bcb1c-182">Rozwiń węzeł **ustawienia logowania** menu, a następnie kliknij przycisk **ogólne**.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-182">Expand the **Login Settings** menu, and then click **General**.</span></span>
    
    <span data-ttu-id="bcb1c-183">![Ogólne](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "ogólne")</span><span class="sxs-lookup"><span data-stu-id="bcb1c-183">![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span></span>

15. <span data-ttu-id="bcb1c-184">W **publicznego** kliknij **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-184">In the **Public** section, click **Add**.</span></span>
    
    <span data-ttu-id="bcb1c-185">![Dodaj](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "Dodaj")</span><span class="sxs-lookup"><span data-stu-id="bcb1c-185">![Add](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "Add")</span></span>

16. <span data-ttu-id="bcb1c-186">Na **Asystenta konfiguracji SAML** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="bcb1c-186">On the **SAML configuration assistant** dialog page, perform the following steps:</span></span>
    
    <span data-ttu-id="bcb1c-187">![Asystent konfiguracji SAML](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "Asystenta konfiguracji SAML")</span><span class="sxs-lookup"><span data-stu-id="bcb1c-187">![SAML Configuration Assistant](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "SAML Configuration Assistant")</span></span>
    
    <span data-ttu-id="bcb1c-188">a.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-188">a.</span></span> <span data-ttu-id="bcb1c-189">Aby przesłać plik metadanych pobranych, w obszarze **metadanych Federacji**, kliknij przycisk **Przeglądaj**.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-189">To upload your downloaded metadata file, under **Federation Metadata**, click **Browse**.</span></span>

    <span data-ttu-id="bcb1c-190">b.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-190">b.</span></span> <span data-ttu-id="bcb1c-191">Aby przesłać plik certyfikatu, w obszarze **certyfikatu (RSA)**, kliknij przycisk **Przeglądaj**.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-191">To upload your certificate file, under **Certificate (RSA)**, click **Browse**.</span></span>

    <span data-ttu-id="bcb1c-192">c.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-192">c.</span></span> <span data-ttu-id="bcb1c-193">Aby przekazać plik logo uzyskano z zespołem pomocy technicznej TOPdesk, w obszarze **ikona Logo**, kliknij przycisk **Przeglądaj**.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-193">To upload the logo file you got from the TOPdesk support team, under **Logo icon**, click **Browse**.</span></span>

    <span data-ttu-id="bcb1c-194">d.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-194">d.</span></span> <span data-ttu-id="bcb1c-195">W **atrybutu nazwy użytkownika** pole tekstowe, typ **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-195">In the **User name attribute** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="bcb1c-196">e.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-196">e.</span></span> <span data-ttu-id="bcb1c-197">W **Nazwa wyświetlana** tekstowym, wpisz nazwę dla danej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-197">In the **Display name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="bcb1c-198">f.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-198">f.</span></span> <span data-ttu-id="bcb1c-199">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-199">Click **Save**.</span></span>

17. <span data-ttu-id="bcb1c-200">W klasycznym portalu Azure, wybierz Potwierdzenie konfiguracji rejestracji jednokrotnej, a następnie kliknij przycisk **Complete** zamknąć **skonfigurować rejestrację jednokrotną** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-200">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="bcb1c-201">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="bcb1c-201">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "Configure Single Sign-On")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="bcb1c-202">Konfigurowanie Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="bcb1c-202">Configuring user provisioning</span></span>
<span data-ttu-id="bcb1c-203">Aby włączyć użytkowników usługi Azure AD zalogować się do TOPdesk - bezpieczny, ich muszą mieć przydzielone do TOPdesk - bezpieczny.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-203">In order to enable Azure AD users to log into TOPdesk - Secure, they must be provisioned into TOPdesk - Secure.</span></span>  
<span data-ttu-id="bcb1c-204">W przypadku TOPdesk - bezpieczny, inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-204">In the case of TOPdesk - Secure, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="bcb1c-205">Aby skonfigurować, inicjowanie obsługi użytkowników, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="bcb1c-205">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="bcb1c-206">Zaloguj się na Twojej **TOPdesk - bezpiecznego** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-206">Sign on to your **TOPdesk - Secure** company site as administrator.</span></span>
2. <span data-ttu-id="bcb1c-207">W menu u góry kliknij **TOPdesk \> nowy \> pliki obsługi \> Operator**.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-207">In the menu on the top, click **TOPdesk \> New \> Support Files \> Operator**.</span></span>
   
    <span data-ttu-id="bcb1c-208">![Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "— Operator")</span><span class="sxs-lookup"><span data-stu-id="bcb1c-208">![Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "Operator")</span></span>

3. <span data-ttu-id="bcb1c-209">Na **operatora New** okna dialogowego, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="bcb1c-209">On the **New Operator** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="bcb1c-210">![New Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "New — Operator")</span><span class="sxs-lookup"><span data-stu-id="bcb1c-210">![New Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "New Operator")</span></span>
   
    <span data-ttu-id="bcb1c-211">a.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-211">a.</span></span> <span data-ttu-id="bcb1c-212">Kliknij kartę Ogólne.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-212">Click the General tab.</span></span>
   
    <span data-ttu-id="bcb1c-213">b.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-213">b.</span></span> <span data-ttu-id="bcb1c-214">W **nazwisko** pole tekstowe z **ogólne** wpisz nazwisko prawidłowe konto usługi Azure Active Directory, aby udostępnić.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-214">In the **Surname** textbox of the **General** section, type the last name of a valid Azure Active Directory account you want to provision.</span></span>
   
    <span data-ttu-id="bcb1c-215">c.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-215">c.</span></span> <span data-ttu-id="bcb1c-216">Wybierz **lokacji** dla konta w **lokalizacji** sekcji.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-216">Select a **Site** for the account in the **Location** section.</span></span>
   
    <span data-ttu-id="bcb1c-217">d.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-217">d.</span></span> <span data-ttu-id="bcb1c-218">W **nazwa logowania** pole tekstowe z **logowania TOPdesk** wpisz nazwę logowania dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-218">In the **Login Name** textbox of the **TOPdesk Login** section, type a login name for your user.</span></span>
   
    <span data-ttu-id="bcb1c-219">e.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-219">e.</span></span> <span data-ttu-id="bcb1c-220">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-220">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="bcb1c-221">Można użyć dowolnego innego TOPdesk — narzędzia do tworzenia konta użytkownika bezpiecznego lub interfejsów API dostarczonych przez TOPdesk - bezpieczny do udostępnienia konta użytkownika usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-221">You can use any other TOPdesk - Secure user account creation tools or APIs provided by TOPdesk - Secure to provision AAD user accounts.</span></span>
> 
> 

## <a name="assigning-users"></a><span data-ttu-id="bcb1c-222">Przypisywanie użytkowników</span><span class="sxs-lookup"><span data-stu-id="bcb1c-222">Assigning users</span></span>
<span data-ttu-id="bcb1c-223">Aby przetestować konfigurację, musisz przyznać użytkowników usługi Azure AD, czy chcesz zezwolić, używając przypisywania do nich dostęp aplikacji do niego.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-223">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

### <a name="to-assign-users-to-topdesk---secure-perform-the-following-steps"></a><span data-ttu-id="bcb1c-224">Do przypisywania użytkowników do TOPdesk - bezpieczny, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="bcb1c-224">To assign users to TOPdesk - Secure, perform the following steps:</span></span>
1. <span data-ttu-id="bcb1c-225">W klasycznym portalu Azure Utwórz konto testu.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-225">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="bcb1c-226">Na ** TOPdesk - bezpiecznego ** strona integracji aplikacji, kliknij przycisk **przypisywać użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-226">On the **TOPdesk - Secure **application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="bcb1c-227">![Przypisywanie użytkowników](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "przypisywanie użytkowników")</span><span class="sxs-lookup"><span data-stu-id="bcb1c-227">![Assign Users](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "Assign Users")</span></span>

3. <span data-ttu-id="bcb1c-228">Wybierz użytkownika testowego, kliknij przycisk **przypisać**, a następnie kliknij przycisk **tak** o potwierdzenie przypisania.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-228">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="bcb1c-229">![Tak](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "tak")</span><span class="sxs-lookup"><span data-stu-id="bcb1c-229">![Yes](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="bcb1c-230">Jeśli chcesz przetestować jednego ustawienia logowania jednokrotnego, otwórz Panel dostępu.</span><span class="sxs-lookup"><span data-stu-id="bcb1c-230">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="bcb1c-231">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bcb1c-231">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

