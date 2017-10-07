---
title: 'Samouczek: Integracji Azure Active Directory z piaskownicy Salesforce | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak toouse piaskownicy usługi Salesforce z usługą Azure Active Directory tooenable pojedynczy logowania jednokrotnego, automatyczne Inicjowanie obsługi i inne!."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: deccd6a07b57c8ba56b7e1c3f3ab311813ca017b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a><span data-ttu-id="3852f-103">Samouczek: Integracji Azure Active Directory z piaskownicy usług Salesforce</span><span class="sxs-lookup"><span data-stu-id="3852f-103">Tutorial: Azure Active Directory integration with Salesforce Sandbox</span></span>

<span data-ttu-id="3852f-104">Celem Hello tego samouczka jest tooshow integracji hello Azure i usługi Salesforce piaskownicy.</span><span class="sxs-lookup"><span data-stu-id="3852f-104">hello objective of this tutorial is tooshow hello integration of Azure and Salesforce Sandbox.</span></span>  

>[!TIP]
><span data-ttu-id="3852f-105">Opinii, zobacz hello [stronę pomocy technicznej platformy Azure](http://go.microsoft.com/fwlink/?LinkId=521878).</span><span class="sxs-lookup"><span data-stu-id="3852f-105">For feedback, see hello [Azure support page](http://go.microsoft.com/fwlink/?LinkId=521878).</span></span> 
> 

<span data-ttu-id="3852f-106">Nadaj piaskownic możesz tekst hello toocreate możliwości wielu kopii organizacji w oddzielnych środowisk do różnych celów, takich jak projektowanie, testowanie i uczenie bez naruszenia hello danych i aplikacji w produkcji usług Salesforce organizacja.</span><span class="sxs-lookup"><span data-stu-id="3852f-106">Sandboxes give you hello ability toocreate multiple copies of your organization in separate environments for a variety of purposes, such as development, testing, and training, without compromising hello data and applications in your Salesforce production organization.</span></span>  

<span data-ttu-id="3852f-107">Aby uzyskać więcej informacji, zobacz [piaskownicy — omówienie](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US)</span><span class="sxs-lookup"><span data-stu-id="3852f-107">For more details, see [Sandbox Overview](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US)</span></span>

<span data-ttu-id="3852f-108">Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="3852f-108">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="3852f-109">Ważnej subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="3852f-109">A valid Azure subscription</span></span>
* <span data-ttu-id="3852f-110">Piaskownica w witrynie Salesforce.com</span><span class="sxs-lookup"><span data-stu-id="3852f-110">A sandbox in Salesforce.com</span></span>

<span data-ttu-id="3852f-111">Jeśli nie masz jeszcze prawidłowy piaskownicy w witrynie Salesforce.com, należy toocontact Salesforce.</span><span class="sxs-lookup"><span data-stu-id="3852f-111">If you don’t have a valid sandbox in Salesforce.com yet, you need toocontact Salesforce.</span></span>

<span data-ttu-id="3852f-112">Scenariusz Hello opisane w tym samouczku składa się z powitania po bloków konstrukcyjnych:</span><span class="sxs-lookup"><span data-stu-id="3852f-112">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="3852f-113">Włączanie integracji aplikacji hello piaskownica usług Salesforce</span><span class="sxs-lookup"><span data-stu-id="3852f-113">Enabling hello application integration for Salesforce Sandbox</span></span>
2. <span data-ttu-id="3852f-114">Konfigurowanie rejestracji jednokrotnej (SSO)</span><span class="sxs-lookup"><span data-stu-id="3852f-114">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="3852f-115">Włączanie domeny</span><span class="sxs-lookup"><span data-stu-id="3852f-115">Enabling your domain</span></span>
4. <span data-ttu-id="3852f-116">Konfigurowanie Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="3852f-116">Configuring user provisioning</span></span>
5. <span data-ttu-id="3852f-117">Przypisywanie użytkowników</span><span class="sxs-lookup"><span data-stu-id="3852f-117">Assigning users</span></span>

<span data-ttu-id="3852f-118">![Scenariusz](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "scenariusza")</span><span class="sxs-lookup"><span data-stu-id="3852f-118">![Scenario](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-salesforce-sandbox"></a><span data-ttu-id="3852f-119">Włącz integrację aplikacji hello piaskownica usług Salesforce</span><span class="sxs-lookup"><span data-stu-id="3852f-119">Enable hello application integration for Salesforce Sandbox</span></span>
<span data-ttu-id="3852f-120">Celem Hello w tej sekcji jest toooutline sposób integracji aplikacji hello tooenable piaskownica Salesforce.</span><span class="sxs-lookup"><span data-stu-id="3852f-120">hello objective of this section is toooutline how tooenable hello application integration for Salesforce sandbox.</span></span>

<span data-ttu-id="3852f-121">**Integracja aplikacji hello tooenable piaskownica Salesforce, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="3852f-121">**tooenable hello application integration for Salesforce sandbox, perform hello following steps:**</span></span>

1. <span data-ttu-id="3852f-122">W hello klasycznego portalu Azure, w okienku nawigacji po lewej stronie powitania kliknij **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3852f-122">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="3852f-123">![Usługi Active Directory](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "usługi Active Directory")</span><span class="sxs-lookup"><span data-stu-id="3852f-123">![Active Directory](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="3852f-124">Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="3852f-124">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="3852f-125">Kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.</span><span class="sxs-lookup"><span data-stu-id="3852f-125">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="3852f-126">![Aplikacje](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "aplikacji")</span><span class="sxs-lookup"><span data-stu-id="3852f-126">![Applications](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="3852f-127">Witaj tooopen **galerii aplikacji**, kliknij przycisk **Dodaj aplikację**, a następnie kliknij przycisk **Dodawanie aplikacji dla mojej organizacji toouse**.</span><span class="sxs-lookup"><span data-stu-id="3852f-127">tooopen hello **Application Gallery**, click **Add An App**, and then click **Add an application for my organization toouse**.</span></span>
   
   <span data-ttu-id="3852f-128">![Co chcesz toodo? ] (./media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "Co chcesz toodo?")</span><span class="sxs-lookup"><span data-stu-id="3852f-128">![What do you want toodo?](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "What do you want toodo?")</span></span>
5. <span data-ttu-id="3852f-129">W hello **pole wyszukiwania**, typ **piaskownicy Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="3852f-129">In hello **search box**, type **Salesforce Sandbox**.</span></span>
   
   <span data-ttu-id="3852f-130">![Galerii aplikacji](./media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "galerii aplikacji")</span><span class="sxs-lookup"><span data-stu-id="3852f-130">![Application Gallery](./media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "Application Gallery")</span></span>
6. <span data-ttu-id="3852f-131">Wybierz w okienku wyników hello **piaskownicy Salesforce**, a następnie kliknij przycisk **Complete** aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="3852f-131">In hello results pane, select **Salesforce Sandbox**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="3852f-132">![Piaskownica SalesForce](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Salesforce piaskownicy")</span><span class="sxs-lookup"><span data-stu-id="3852f-132">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Salesforce Sandbox")</span></span>
   
## <a name="configur-single-sign-on-sso"></a><span data-ttu-id="3852f-133">Configur rejestracji jednokrotnej (SSO)</span><span class="sxs-lookup"><span data-stu-id="3852f-133">Configur single sign-on (SSO)</span></span>

<span data-ttu-id="3852f-134">Celem Hello w tej sekcji jest toooutline jak tooenable użytkowników tooauthenticate tooSalesforce do swojego konta w usłudze Azure AD przy użyciu Federacji oparte na powitania protokołu SAML.</span><span class="sxs-lookup"><span data-stu-id="3852f-134">hello objective of this section is toooutline how tooenable users tooauthenticate tooSalesforce with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="3852f-135">**tooconfigure logowanie jednokrotne, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="3852f-135">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="3852f-136">W hello klasycznego portalu Azure na powitania **piaskownicy Salesforce** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** tooopen hello **skonfigurować rejestrację jednokrotną** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="3852f-136">In hello Azure classic portal, on hello **Salesforce Sandbox** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="3852f-137">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="3852f-137">![Configure single sign-on](./media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="3852f-138">Na powitania **jak ma toosign użytkowników na tooSalesforce piaskownicy** wybierz pozycję **usługi Microsoft Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="3852f-138">On hello **How would you like users toosign on tooSalesforce Sandbox** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="3852f-139">![Piaskownica SalesForce](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Salesforce piaskownicy")</span><span class="sxs-lookup"><span data-stu-id="3852f-139">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Salesforce Sandbox")</span></span>
3. <span data-ttu-id="3852f-140">Na powitania **Konfigurowanie adresu URL aplikacji** strony w hello **na adres URL logowania** pole tekstowe, wpisz adres URL przy użyciu następującego wzorca hello `http://company.my.salesforce.com`, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="3852f-140">On hello **Configure App URL** page, in hello **Sign On URL** textbox, type your URL using hello following pattern `http://company.my.salesforce.com`, and then click **Next**.</span></span>
   
   <span data-ttu-id="3852f-141">![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "skonfigurować adres URL aplikacji")</span><span class="sxs-lookup"><span data-stu-id="3852f-141">![Configure App URL](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "Configure App URL")</span></span>
4. <span data-ttu-id="3852f-142">Jeśli skonfigurowano już program rejestracji jednokrotnej dla innego wystąpienia usług Salesforce piaskownicy w katalogu, a następnie należy także skonfigurować hello **identyfikator** toohave hello tę samą wartość jak hello **Zaloguj się na adres URL**.</span><span class="sxs-lookup"><span data-stu-id="3852f-142">If you have already configured single sign-on for another Salesforce Sandbox instance in your directory, then you must also configure hello **Identifier** toohave hello same value as hello **Sign on URL**.</span></span> 
 * <span data-ttu-id="3852f-143">Witaj **identyfikator** pola można znaleźć, sprawdzając hello **Pokaż zaawansowane ustawienia** wyboru na powitania **Konfigurowanie adresu URL aplikacji** stronę hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="3852f-143">hello **Identifier** field can be found by checking hello **Show advanced settings** checkbox on hello **Configure App URL** page of hello dialog.</span></span>
5. <span data-ttu-id="3852f-144">Na powitania **skonfigurować logowanie jednokrotne w piaskownicy Salesforce** kliknij przycisk **pobierania certyfikatu**, a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="3852f-144">On hello **Configure single sign-on at Salesforce Sandbox** page, click **Download certificate**, and then save hello certificate file on your computer.</span></span>
   
   <span data-ttu-id="3852f-145">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="3852f-145">![Configure Single Sign-On](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "Configure Single Sign-On")</span></span>
6. <span data-ttu-id="3852f-146">W oknie przeglądarki innej witryny sieci web Zaloguj się do Twojego piaskownicy Salesforce jako administrator.</span><span class="sxs-lookup"><span data-stu-id="3852f-146">In a different web browser window, log into your Salesforce sandbox as an administrator.</span></span>
7. <span data-ttu-id="3852f-147">W menu hello na górze hello, kliknij przycisk **Instalatora**.</span><span class="sxs-lookup"><span data-stu-id="3852f-147">In hello menu on hello top, click **Setup**.</span></span>
   
   <span data-ttu-id="3852f-148">![Instalator](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "Instalatora")</span><span class="sxs-lookup"><span data-stu-id="3852f-148">![Setup](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "Setup")</span></span>
8. <span data-ttu-id="3852f-149">W okienku nawigacji hello po lewej stronie powitania kliknij **kontroli bezpieczeństwa**, a następnie kliknij przycisk **ustawień rejestracji jednokrotnej**.</span><span class="sxs-lookup"><span data-stu-id="3852f-149">In hello navigation pane on hello left, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>
   
   <span data-ttu-id="3852f-150">![Single Sign-On ustawienia](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "Single Sign-On ustawienia")</span><span class="sxs-lookup"><span data-stu-id="3852f-150">![Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "Single Sign-On Settings")</span></span>
9. <span data-ttu-id="3852f-151">Witaj w sekcji Ustawienia rejestracji jednokrotnej wykonywanie hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="3852f-151">On hello Single Sign-On Settings section, perform hello following steps:</span></span>
   
   <span data-ttu-id="3852f-152">![Single Sign-On ustawienia](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "Single Sign-On ustawienia")</span><span class="sxs-lookup"><span data-stu-id="3852f-152">![Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "Single Sign-On Settings")</span></span>  
 1.  <span data-ttu-id="3852f-153">Wybierz **SAML włączone**.</span><span class="sxs-lookup"><span data-stu-id="3852f-153">Select **SAML Enabled**.</span></span> 
 2.  <span data-ttu-id="3852f-154">Kliknij przycisk **Nowy**.</span><span class="sxs-lookup"><span data-stu-id="3852f-154">Click **New**.</span></span>
10. <span data-ttu-id="3852f-155">Witaj SAML pojedynczy znak w sekcji Ustawienia wykonywanie hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="3852f-155">On hello SAML Single Sign-On Settings section, perform hello following steps:</span></span>
    
    <span data-ttu-id="3852f-156">![SAML pojedynczego logowania jednokrotnego ustawienia](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "SAML jednego ustawienia rejestracji")</span><span class="sxs-lookup"><span data-stu-id="3852f-156">![SAML Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "SAML Single Sign-On Settings")</span></span>  
 1. <span data-ttu-id="3852f-157">W polu tekstowym Nazwa hello, wpisz nazwę hello hello konfiguracji (np.: *SPSSOWAAD\_testu*).</span><span class="sxs-lookup"><span data-stu-id="3852f-157">In hello Name textbox, type hello name of hello configuration (e.g.: *SPSSOWAAD\_Test*).</span></span> 
 2. <span data-ttu-id="3852f-158">W hello klasycznego portalu Azure na powitania **skonfigurować logowanie jednokrotne w piaskownicy Salesforce** dialogu strony, hello kopiowania **adres URL wystawcy** wartość, a następnie wklej go do hello **wystawcy**pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="3852f-158">In hello Azure classic portal, on hello **Configure single sign-on at Salesforce Sandbox** dialogue page, copy hello **Issuer URL** value, and then paste it into hello **Issuer** textbox.</span></span>
 3. <span data-ttu-id="3852f-159">W hello **identyfikator jednostki** pole tekstowe, typ **https://test.salesforce.com** Jeśli jest to hello pierwszego wystąpienia usług Salesforce piaskownicy dodajesz tooyour katalogu.</span><span class="sxs-lookup"><span data-stu-id="3852f-159">In hello **Entity Id** textbox, type **https://test.salesforce.com** if this is hello first Salesforce Sandbox instance that you are adding tooyour directory.</span></span> <span data-ttu-id="3852f-160">Jeśli masz już dodany wystąpienia usług Salesforce piaskownicy, a następnie dla hello **identyfikator jednostki** typu w hello **na adres URL logowania**, która powinna być w następującym formacie:`http://company.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="3852f-160">If you have already added an instance of Salesforce Sandbox, then for hello **Entity ID** type in hello **Sign On URL**, which should be in this format: `http://company.my.salesforce.com`</span></span>   
 4. <span data-ttu-id="3852f-161">Kliknij przycisk **Przeglądaj** tooupload hello pobrać certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="3852f-161">Click **Browse** tooupload hello downloaded certificate.</span></span>  
 5. <span data-ttu-id="3852f-162">Jako **typ tożsamości SAML**, wybierz pozycję **potwierdzenia zawiera hello identyfikator federacyjnej z obiektu użytkownika hello**.</span><span class="sxs-lookup"><span data-stu-id="3852f-162">As **SAML Identity Type**, select **Assertion contains hello Federation ID from hello User object**.</span></span> 
 6. <span data-ttu-id="3852f-163">Jako **lokalizacji tożsamości SAML**, wybierz pozycję **jest tożsamość w elemencie NameIdentifier hello hello instrukcji podmiotu**.</span><span class="sxs-lookup"><span data-stu-id="3852f-163">As **SAML Identity Location**, select **Identity is in hello NameIdentifier element of hello Subject statement**.</span></span>
 7. <span data-ttu-id="3852f-164">W hello klasycznego portalu Azure na powitania **skonfigurować logowanie jednokrotne w piaskownicy Salesforce** dialogu strony, hello kopiowania **zdalnego adresu URL logowania** wartość, a następnie wklej go do hello **dostawcy tożsamości Adres URL logowania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="3852f-164">In hello Azure classic portal, on hello **Configure single sign-on at Salesforce Sandbox** dialogue page, copy hello **Remote Login URL** value, and then paste it into hello **Identity Provider Login URL** textbox.</span></span> 
 8. <span data-ttu-id="3852f-165">SFDC nie obsługuje SAML wylogowania.</span><span class="sxs-lookup"><span data-stu-id="3852f-165">SFDC does not support SAML logout.</span></span>  <span data-ttu-id="3852f-166">Jako obejście, Wklej "https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0" go do hello **adres URL wylogowania dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="3852f-166">As a workaround, paste 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' it into hello **Identity Provider Logout URL** textbox.</span></span>
 9. <span data-ttu-id="3852f-167">Jako **dostawcy zainicjował żądanie powiązania usługi**, wybierz pozycję **HTTP POST**.</span><span class="sxs-lookup"><span data-stu-id="3852f-167">As **Service Provider Initiated Request Binding**, select **HTTP POST**.</span></span> 
 10. <span data-ttu-id="3852f-168">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="3852f-168">Click **Save**.</span></span>
11. <span data-ttu-id="3852f-169">Na powitania klasycznego portalu Azure, wybierz hello konfiguracji rejestracji jednokrotnej potwierdzenie, a następnie kliknij **Complete** tooclose hello **skonfigurować rejestrację jednokrotną** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="3852f-169">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="3852f-170">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="3852f-170">![Configure Single Sign-On](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "Configure Single Sign-On")</span></span>

## <a name="enable-your-domain"></a><span data-ttu-id="3852f-171">Włącz domeny</span><span class="sxs-lookup"><span data-stu-id="3852f-171">Enable your domain</span></span>
<span data-ttu-id="3852f-172">W tej sekcji założono, że już utworzono domeny.</span><span class="sxs-lookup"><span data-stu-id="3852f-172">This section assumes that you already have created a domain.</span></span>  <span data-ttu-id="3852f-173">Aby uzyskać więcej informacji, zobacz [Definiowanie Twojej nazwy domeny](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span><span class="sxs-lookup"><span data-stu-id="3852f-173">For more details, see [Defining Your Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span></span>

<span data-ttu-id="3852f-174">**tooenable domeny, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="3852f-174">**tooenable your domain, perform hello following steps:**</span></span>

1. <span data-ttu-id="3852f-175">W okienku nawigacji po lewej stronie powitania kliknij **Zarządzanie domenami**, a następnie kliknij przycisk **Moje domeny.**</span><span class="sxs-lookup"><span data-stu-id="3852f-175">In hello left navigation pane, click **Domain Management**, and then click **My Domain.**</span></span>
   
   <span data-ttu-id="3852f-176">![Mojej domeny](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "mojej domeny")</span><span class="sxs-lookup"><span data-stu-id="3852f-176">![My Domain](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "My Domain")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="3852f-177">Upewnij się, że poprawnie skonfigurowano domenę.</span><span class="sxs-lookup"><span data-stu-id="3852f-177">Please make sure that your domain has been configured correctly.</span></span> 
   > 
2. <span data-ttu-id="3852f-178">W hello **ustawienia strony logowania** , kliknij przycisk **Edytuj**, następnie jako **usługi uwierzytelniania**, wybierz nazwę hello hello SAML pojedynczego logowania jednokrotnego ustawienia z poprzednich hello sekcja, a na koniec kliknij **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="3852f-178">In hello **Login Page Settings** section, click **Edit**, then, as **Authentication Service**, select hello name of hello SAML Single Sign-On Setting from hello previous section, and finally click **Save**.</span></span>
   
   <span data-ttu-id="3852f-179">![Mojej domeny](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "mojej domeny")</span><span class="sxs-lookup"><span data-stu-id="3852f-179">![My Domain](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "My Domain")</span></span>

<span data-ttu-id="3852f-180">Jak masz domenę skonfigurowane, użytkownicy należy używać hello domeny adres URL toologin toohello Salesforce piaskownicy.</span><span class="sxs-lookup"><span data-stu-id="3852f-180">As soon as you have a domain configured, your users should use hello domain URL toologin toohello Salesforce sandbox.</span></span>  

<span data-ttu-id="3852f-181">wartość hello tooget hello adresu URL, kliknij profil rejestracji Jednokrotnej hello, utworzony w poprzedniej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="3852f-181">tooget hello value of hello URL, click hello SSO profile you have created in hello previous section.</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="3852f-182">Skonfiguruj Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="3852f-182">Configure user provisioning</span></span>
<span data-ttu-id="3852f-183">Celem Hello w tej sekcji jest toooutline jak tooenable użytkownika usługi Active Directory Inicjowanie obsługi użytkowników kont tooSalesforce piaskownicy.</span><span class="sxs-lookup"><span data-stu-id="3852f-183">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooSalesforce Sandbox.</span></span>

<span data-ttu-id="3852f-184">**tooconfigure aprowizacji użytkowników, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="3852f-184">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="3852f-185">W portalu usługi Salesforce hello hello górnym pasku nawigacyjnym wybierz tooexpand Twojej nazwy użytkownika menu użytkownika:</span><span class="sxs-lookup"><span data-stu-id="3852f-185">In hello Salesforce portal, in hello top navigation bar, select your name tooexpand your user menu:</span></span>
   
   <span data-ttu-id="3852f-186">![Ustawienia](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "Moje ustawienia")</span><span class="sxs-lookup"><span data-stu-id="3852f-186">![My Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "My Settings")</span></span>
2. <span data-ttu-id="3852f-187">Wybierz z menu programu użytkownika **Moje ustawienia** tooopen Twojego **Moje ustawienia** strony.</span><span class="sxs-lookup"><span data-stu-id="3852f-187">From your user menu, select **My Settings** tooopen your **My Settings** page.</span></span>
3. <span data-ttu-id="3852f-188">W okienku po lewej stronie powitania kliknij **osobistych** tooexpand hello sekcji osobistych, a następnie kliknij przycisk **zresetować moje tokenu zabezpieczeń**:</span><span class="sxs-lookup"><span data-stu-id="3852f-188">In hello left pane, click **Personal** tooexpand hello Personal section, and then click **Reset My Security Token**:</span></span>
   
   <span data-ttu-id="3852f-189">![Ustawienia](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "Moje ustawienia")</span><span class="sxs-lookup"><span data-stu-id="3852f-189">![My Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "My Settings")</span></span>
4. <span data-ttu-id="3852f-190">Na powitania **zresetować moje tokenu zabezpieczeń** kliknij przycisk **zresetować tokenu zabezpieczeń** toorequest wiadomości e-mail, który zawiera token zabezpieczeń witryny Salesforce.com.</span><span class="sxs-lookup"><span data-stu-id="3852f-190">On hello **Reset My Security Token** page, click **Reset Security Token** toorequest an email that contains your Salesforce.com security token.</span></span>
   
   <span data-ttu-id="3852f-191">![Nowy Token](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "nowy Token")</span><span class="sxs-lookup"><span data-stu-id="3852f-191">![New Token](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "New Token")</span></span>
5. <span data-ttu-id="3852f-192">Sprawdź skrzynki odbiorczej poczty e-mail, wiadomości e-mail z witryny Salesforce.com z "**potwierdzenia zabezpieczeń salesforce.com.com**" jako podmiotu.</span><span class="sxs-lookup"><span data-stu-id="3852f-192">Check your email inbox for an email from Salesforce.com with “**salesforce.com.com security confirmation**” as subject.</span></span>
6. <span data-ttu-id="3852f-193">Przejrzyj tej wiadomości e-mail i skopiuj hello zabezpieczeń wartość tokenu.</span><span class="sxs-lookup"><span data-stu-id="3852f-193">Review this email and copy hello security token value.</span></span>
7. <span data-ttu-id="3852f-194">W hello klasycznego portalu Azure na powitania **salesforce piaskownicy** strona integracji aplikacji, kliknij przycisk **skonfigurować Inicjowanie obsługi użytkowników** tooopen hello **skonfigurować Inicjowanie obsługi użytkowników**okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="3852f-194">In hello Azure classic portal, on hello **salesforce Sandbox** application integration page, click **Configure user provisioning** tooopen hello **Configure User Provisioning** dialog.</span></span>
   
   <span data-ttu-id="3852f-195">![Skonfiguruj Inicjowanie obsługi użytkowników](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "skonfigurować Inicjowanie obsługi użytkowników")</span><span class="sxs-lookup"><span data-stu-id="3852f-195">![Configure user provisioning](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "Configure user provisioning")</span></span>
8. <span data-ttu-id="3852f-196">Na powitania **Wprowadź użytkownika piaskownicy Salesforce poświadczenia tooenable automatyczne Inicjowanie obsługi użytkowników** Podaj hello następujące ustawienia konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="3852f-196">On hello **Enter your Salesforce Sandbox credentials tooenable automatic user provisioning** page, provide hello following configuration settings:</span></span>
   
   <span data-ttu-id="3852f-197">![Piaskownica SalesForce](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Salesforce piaskownicy")</span><span class="sxs-lookup"><span data-stu-id="3852f-197">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Salesforce Sandbox")</span></span>   
 1. <span data-ttu-id="3852f-198">W hello **nazwa użytkownika administratora piaskownicy Salesforce** tekstowym, wpisz nazwę, która ma hello konta piaskownicy Salesforce **administratorem** profilu w witrynie Salesforce.com przypisane.</span><span class="sxs-lookup"><span data-stu-id="3852f-198">In hello **Salesforce Sandbox Admin User Name** textbox, type a Salesforce sandbox account name that has hello **System Administrator** profile in Salesforce.com assigned.</span></span>
 2. <span data-ttu-id="3852f-199">W hello **hasło administratora piaskownicy Salesforce** tekstowym, wpisz hello hasło dla tego konta.</span><span class="sxs-lookup"><span data-stu-id="3852f-199">In hello **Salesforce Sandbox Admin Password** textbox, type hello password for this account.</span></span>
 3. <span data-ttu-id="3852f-200">W hello **tokenu zabezpieczeń użytkownika** pole tekstowe, wartość tokenu zabezpieczeń hello wklejania.</span><span class="sxs-lookup"><span data-stu-id="3852f-200">In hello **User Security Token** textbox, paste hello security token value.</span></span>
 4. <span data-ttu-id="3852f-201">Kliknij przycisk **weryfikacji** tooverify konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="3852f-201">Click **Validate** tooverify your configuration.</span></span>
 5. <span data-ttu-id="3852f-202">Kliknij przycisk hello **dalej** hello tooopen przycisk **potwierdzenie** strony.</span><span class="sxs-lookup"><span data-stu-id="3852f-202">Click hello **Next** button tooopen hello **Confirmation** page.</span></span>
9. <span data-ttu-id="3852f-203">Na powitania **potwierdzenie** kliknij przycisk **Complete** toosave konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="3852f-203">On hello **Confirmation** page, click **Complete** toosave your configuration.</span></span>
   
## <a name="assigning-users"></a><span data-ttu-id="3852f-204">Przypisywanie użytkowników</span><span class="sxs-lookup"><span data-stu-id="3852f-204">Assigning users</span></span>

<span data-ttu-id="3852f-205">tootest konfiguracji, należy toogrant hello Azure AD użytkownicy mają tooallow przy użyciu Twojej aplikacji tooit dostępu przez przypisywanie ich.</span><span class="sxs-lookup"><span data-stu-id="3852f-205">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="3852f-206">**tooassign użytkowników tooSalesforce piaskownicy, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="3852f-206">**tooassign users tooSalesforce Sandbox, perform hello following steps:**</span></span>

1. <span data-ttu-id="3852f-207">W hello klasycznego portalu Azure Utwórz konto testu.</span><span class="sxs-lookup"><span data-stu-id="3852f-207">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="3852f-208">Na powitania ** piaskownicy Salesforce ** strona integracji aplikacji, kliknij przycisk **przypisywać użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="3852f-208">On hello **Salesforce Sandbox **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="3852f-209">![Przypisywanie użytkowników](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "przypisywanie użytkowników")</span><span class="sxs-lookup"><span data-stu-id="3852f-209">![Assign users](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "Assign users")</span></span>
3. <span data-ttu-id="3852f-210">Wybierz użytkownika testowego, kliknij przycisk **przypisać**, a następnie kliknij przycisk **tak** tooconfirm przypisania.</span><span class="sxs-lookup"><span data-stu-id="3852f-210">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="3852f-211">![Tak](./media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "tak")</span><span class="sxs-lookup"><span data-stu-id="3852f-211">![Yes](./media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="3852f-212">Należy teraz Odczekaj 10 minut i sprawdź, czy konto hello zostało zsynchronizowane tooSalesforce piaskownicy.</span><span class="sxs-lookup"><span data-stu-id="3852f-212">You should now wait for 10 minutes and verify that hello account has been synchronized tooSalesforce Sandbox.</span></span>

<span data-ttu-id="3852f-213">Jeśli chcesz tootest ustawienia logowania jednokrotnego, otwórz hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="3852f-213">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="3852f-214">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="3852f-214">For more details about hello Access Panel, see [Introduction toohello Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

