---
title: 'Samouczek: Integracji Azure Active Directory z piaskownicy Salesforce | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak użyć piaskownicy Salesforce z usługą Azure Active Directory w celu włączenia logowania jednokrotnego, automatyczne Inicjowanie obsługi i inne!."
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
ms.openlocfilehash: 32835e79188806bb2ff319eea23b1b52ab585ab1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a><span data-ttu-id="45564-103">Samouczek: Integracji Azure Active Directory z piaskownicy usług Salesforce</span><span class="sxs-lookup"><span data-stu-id="45564-103">Tutorial: Azure Active Directory integration with Salesforce Sandbox</span></span>

<span data-ttu-id="45564-104">Celem tego samouczka jest pokazanie integracji Azure i usługi Salesforce piaskownicy.</span><span class="sxs-lookup"><span data-stu-id="45564-104">The objective of this tutorial is to show the integration of Azure and Salesforce Sandbox.</span></span>  

>[!TIP]
><span data-ttu-id="45564-105">Opinii, zobacz [stronę pomocy technicznej platformy Azure](http://go.microsoft.com/fwlink/?LinkId=521878).</span><span class="sxs-lookup"><span data-stu-id="45564-105">For feedback, see the [Azure support page](http://go.microsoft.com/fwlink/?LinkId=521878).</span></span> 
> 

<span data-ttu-id="45564-106">Piaskownic zapewniają możliwość tworzenia wielu kopii organizacji w oddzielnych środowisk do różnych celów, takich jak projektowanie, testowanie i uczenie bez naruszania danych i aplikacji w organizacji produkcji Salesforce.</span><span class="sxs-lookup"><span data-stu-id="45564-106">Sandboxes give you the ability to create multiple copies of your organization in separate environments for a variety of purposes, such as development, testing, and training, without compromising the data and applications in your Salesforce production organization.</span></span>  

<span data-ttu-id="45564-107">Aby uzyskać więcej informacji, zobacz [piaskownicy — omówienie](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US)</span><span class="sxs-lookup"><span data-stu-id="45564-107">For more details, see [Sandbox Overview](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US)</span></span>

<span data-ttu-id="45564-108">Scenariusz opisany w tym samouczku założono, że już następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="45564-108">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="45564-109">Ważnej subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="45564-109">A valid Azure subscription</span></span>
* <span data-ttu-id="45564-110">Piaskownica w witrynie Salesforce.com</span><span class="sxs-lookup"><span data-stu-id="45564-110">A sandbox in Salesforce.com</span></span>

<span data-ttu-id="45564-111">Jeśli nie masz prawidłowe piaskownicy w witrynie Salesforce.com jeszcze, musisz skontaktować się z usług Salesforce.</span><span class="sxs-lookup"><span data-stu-id="45564-111">If you don’t have a valid sandbox in Salesforce.com yet, you need to contact Salesforce.</span></span>

<span data-ttu-id="45564-112">Scenariusz opisany w tym samouczku składa się z następujących bloków konstrukcyjnych:</span><span class="sxs-lookup"><span data-stu-id="45564-112">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="45564-113">Włączanie integracji aplikacji Salesforce piaskownica</span><span class="sxs-lookup"><span data-stu-id="45564-113">Enabling the application integration for Salesforce Sandbox</span></span>
2. <span data-ttu-id="45564-114">Konfigurowanie rejestracji jednokrotnej (SSO)</span><span class="sxs-lookup"><span data-stu-id="45564-114">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="45564-115">Włączanie domeny</span><span class="sxs-lookup"><span data-stu-id="45564-115">Enabling your domain</span></span>
4. <span data-ttu-id="45564-116">Konfigurowanie Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="45564-116">Configuring user provisioning</span></span>
5. <span data-ttu-id="45564-117">Przypisywanie użytkowników</span><span class="sxs-lookup"><span data-stu-id="45564-117">Assigning users</span></span>

<span data-ttu-id="45564-118">![Scenariusz](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "scenariusza")</span><span class="sxs-lookup"><span data-stu-id="45564-118">![Scenario](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-salesforce-sandbox"></a><span data-ttu-id="45564-119">Włącz integrację aplikacji Salesforce piaskownica</span><span class="sxs-lookup"><span data-stu-id="45564-119">Enable the application integration for Salesforce Sandbox</span></span>
<span data-ttu-id="45564-120">Celem tej sekcji jest przedstawiają sposób włączania integracji aplikacji Salesforce piaskownica.</span><span class="sxs-lookup"><span data-stu-id="45564-120">The objective of this section is to outline how to enable the application integration for Salesforce sandbox.</span></span>

<span data-ttu-id="45564-121">**Aby włączyć integrację aplikacji Salesforce piaskownica, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="45564-121">**To enable the application integration for Salesforce sandbox, perform the following steps:**</span></span>

1. <span data-ttu-id="45564-122">W klasycznym portalu Azure, w okienku nawigacji po lewej stronie kliknij **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="45564-122">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="45564-123">![Usługi Active Directory](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "usługi Active Directory")</span><span class="sxs-lookup"><span data-stu-id="45564-123">![Active Directory](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="45564-124">Z **katalogu** listy, wybierz katalog, dla którego chcesz włączyć integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="45564-124">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="45564-125">Aby otworzyć widok aplikacji, w widoku katalogu, kliknij przycisk **aplikacji** w menu u góry.</span><span class="sxs-lookup"><span data-stu-id="45564-125">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="45564-126">![Aplikacje](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "aplikacji")</span><span class="sxs-lookup"><span data-stu-id="45564-126">![Applications](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="45564-127">Aby otworzyć **galerii aplikacji**, kliknij przycisk **Dodaj aplikację**, a następnie kliknij przycisk **Dodawanie aplikacji dla mojej organizacji do używania**.</span><span class="sxs-lookup"><span data-stu-id="45564-127">To open the **Application Gallery**, click **Add An App**, and then click **Add an application for my organization to use**.</span></span>
   
   <span data-ttu-id="45564-128">![Co chcesz zrobić? ] (./media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "Co chcesz zrobić?")</span><span class="sxs-lookup"><span data-stu-id="45564-128">![What do you want to do?](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "What do you want to do?")</span></span>
5. <span data-ttu-id="45564-129">W **pole wyszukiwania**, typ **piaskownicy Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="45564-129">In the **search box**, type **Salesforce Sandbox**.</span></span>
   
   <span data-ttu-id="45564-130">![Galerii aplikacji](./media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "galerii aplikacji")</span><span class="sxs-lookup"><span data-stu-id="45564-130">![Application Gallery](./media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "Application Gallery")</span></span>
6. <span data-ttu-id="45564-131">W okienku wyników wybierz **piaskownicy Salesforce**, a następnie kliknij przycisk **Complete** można dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="45564-131">In the results pane, select **Salesforce Sandbox**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="45564-132">![Piaskownica SalesForce](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Salesforce piaskownicy")</span><span class="sxs-lookup"><span data-stu-id="45564-132">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Salesforce Sandbox")</span></span>
   
## <a name="configur-single-sign-on-sso"></a><span data-ttu-id="45564-133">Configur rejestracji jednokrotnej (SSO)</span><span class="sxs-lookup"><span data-stu-id="45564-133">Configur single sign-on (SSO)</span></span>

<span data-ttu-id="45564-134">Celem tej sekcji jest przedstawiają sposób użytkownicy mogli uwierzytelniania do usług Salesforce za pomocą swojego konta w usłudze Azure AD przy użyciu federacyjnego na podstawie protokołu SAML.</span><span class="sxs-lookup"><span data-stu-id="45564-134">The objective of this section is to outline how to enable users to authenticate to Salesforce with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="45564-135">**Aby skonfigurować rejestrację jednokrotną, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="45564-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="45564-136">W klasycznym portalu Azure na **piaskownicy Salesforce** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** otworzyć **skonfigurować rejestrację jednokrotną** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="45564-136">In the Azure classic portal, on the **Salesforce Sandbox** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="45564-137">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="45564-137">![Configure single sign-on](./media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="45564-138">Na **jak chcesz użytkownikom zalogować się na piaskownicy Salesforce** wybierz pozycję **usługi Microsoft Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="45564-138">On the **How would you like users to sign on to Salesforce Sandbox** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="45564-139">![Piaskownica SalesForce](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Salesforce piaskownicy")</span><span class="sxs-lookup"><span data-stu-id="45564-139">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Salesforce Sandbox")</span></span>
3. <span data-ttu-id="45564-140">Na **Konfigurowanie adresu URL aplikacji** strony w **na adres URL logowania** pole tekstowe, wpisz adres URL przy użyciu następującego wzorca `http://company.my.salesforce.com`, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="45564-140">On the **Configure App URL** page, in the **Sign On URL** textbox, type your URL using the following pattern `http://company.my.salesforce.com`, and then click **Next**.</span></span>
   
   <span data-ttu-id="45564-141">![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "skonfigurować adres URL aplikacji")</span><span class="sxs-lookup"><span data-stu-id="45564-141">![Configure App URL](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "Configure App URL")</span></span>
4. <span data-ttu-id="45564-142">Jeśli skonfigurowano już program rejestracji jednokrotnej dla innego wystąpienia usług Salesforce piaskownicy w katalogu, a następnie należy także skonfigurować **identyfikator** mają taką samą wartość jak **Zaloguj się na adres URL**.</span><span class="sxs-lookup"><span data-stu-id="45564-142">If you have already configured single sign-on for another Salesforce Sandbox instance in your directory, then you must also configure the **Identifier** to have the same value as the **Sign on URL**.</span></span> 
 * <span data-ttu-id="45564-143">**Identyfikator** można znaleźć pola sprawdzając **Pokaż zaawansowane ustawienia** wyboru na **Konfigurowanie adresu URL aplikacji** strony okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="45564-143">The **Identifier** field can be found by checking the **Show advanced settings** checkbox on the **Configure App URL** page of the dialog.</span></span>
5. <span data-ttu-id="45564-144">Na **skonfigurować logowanie jednokrotne w piaskownicy Salesforce** kliknij przycisk **pobierania certyfikatu**, a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="45564-144">On the **Configure single sign-on at Salesforce Sandbox** page, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
   <span data-ttu-id="45564-145">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="45564-145">![Configure Single Sign-On](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "Configure Single Sign-On")</span></span>
6. <span data-ttu-id="45564-146">W oknie przeglądarki innej witryny sieci web Zaloguj się do Twojego piaskownicy Salesforce jako administrator.</span><span class="sxs-lookup"><span data-stu-id="45564-146">In a different web browser window, log into your Salesforce sandbox as an administrator.</span></span>
7. <span data-ttu-id="45564-147">W menu u góry kliknij **Instalatora**.</span><span class="sxs-lookup"><span data-stu-id="45564-147">In the menu on the top, click **Setup**.</span></span>
   
   <span data-ttu-id="45564-148">![Instalator](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "Instalatora")</span><span class="sxs-lookup"><span data-stu-id="45564-148">![Setup](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "Setup")</span></span>
8. <span data-ttu-id="45564-149">W okienku nawigacji po lewej stronie kliknij **kontroli bezpieczeństwa**, a następnie kliknij przycisk **ustawień rejestracji jednokrotnej**.</span><span class="sxs-lookup"><span data-stu-id="45564-149">In the navigation pane on the left, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>
   
   <span data-ttu-id="45564-150">![Single Sign-On ustawienia](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "Single Sign-On ustawienia")</span><span class="sxs-lookup"><span data-stu-id="45564-150">![Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "Single Sign-On Settings")</span></span>
9. <span data-ttu-id="45564-151">W sekcji Ustawienia rejestracji jednokrotnej wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="45564-151">On the Single Sign-On Settings section, perform the following steps:</span></span>
   
   <span data-ttu-id="45564-152">![Single Sign-On ustawienia](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "Single Sign-On ustawienia")</span><span class="sxs-lookup"><span data-stu-id="45564-152">![Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "Single Sign-On Settings")</span></span>  
 1.  <span data-ttu-id="45564-153">Wybierz **SAML włączone**.</span><span class="sxs-lookup"><span data-stu-id="45564-153">Select **SAML Enabled**.</span></span> 
 2.  <span data-ttu-id="45564-154">Kliknij przycisk **Nowy**.</span><span class="sxs-lookup"><span data-stu-id="45564-154">Click **New**.</span></span>
10. <span data-ttu-id="45564-155">W sekcji SAML jednego ustawienia rejestracji wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="45564-155">On the SAML Single Sign-On Settings section, perform the following steps:</span></span>
    
    <span data-ttu-id="45564-156">![SAML pojedynczego logowania jednokrotnego ustawienia](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "SAML jednego ustawienia rejestracji")</span><span class="sxs-lookup"><span data-stu-id="45564-156">![SAML Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "SAML Single Sign-On Settings")</span></span>  
 1. <span data-ttu-id="45564-157">W polu tekstowym Nazwa wpisz nazwę konfiguracji (np.: *SPSSOWAAD\_testu*).</span><span class="sxs-lookup"><span data-stu-id="45564-157">In the Name textbox, type the name of the configuration (e.g.: *SPSSOWAAD\_Test*).</span></span> 
 2. <span data-ttu-id="45564-158">W klasycznym portalu Azure na **skonfigurować logowanie jednokrotne w piaskownicy Salesforce** dialogu strony, kopiowania **adres URL wystawcy** wartość, a następnie wklej ją do **wystawcy** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="45564-158">In the Azure classic portal, on the **Configure single sign-on at Salesforce Sandbox** dialogue page, copy the **Issuer URL** value, and then paste it into the **Issuer** textbox.</span></span>
 3. <span data-ttu-id="45564-159">W **identyfikator jednostki** pole tekstowe, typ **https://test.salesforce.com** Jeśli jest to pierwsze wystąpienie piaskownicy Salesforce, które ma zostać dodane do katalogu.</span><span class="sxs-lookup"><span data-stu-id="45564-159">In the **Entity Id** textbox, type **https://test.salesforce.com** if this is the first Salesforce Sandbox instance that you are adding to your directory.</span></span> <span data-ttu-id="45564-160">Jeśli masz już dodany wystąpienia usług Salesforce piaskownicy, następnie dla **identyfikator jednostki** wpisz **na adres URL logowania**, która powinna być w następującym formacie:`http://company.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="45564-160">If you have already added an instance of Salesforce Sandbox, then for the **Entity ID** type in the **Sign On URL**, which should be in this format: `http://company.my.salesforce.com`</span></span>   
 4. <span data-ttu-id="45564-161">Kliknij przycisk **Przeglądaj** przekazywania pobranego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="45564-161">Click **Browse** to upload the downloaded certificate.</span></span>  
 5. <span data-ttu-id="45564-162">Jako **typ tożsamości SAML**, wybierz pozycję **potwierdzenia zawiera identyfikator federacji z obiektu użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="45564-162">As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.</span></span> 
 6. <span data-ttu-id="45564-163">Jako **lokalizacji tożsamości SAML**, wybierz pozycję **jest tożsamość w elemencie NameIdentifier instrukcji podmiotu**.</span><span class="sxs-lookup"><span data-stu-id="45564-163">As **SAML Identity Location**, select **Identity is in the NameIdentifier element of the Subject statement**.</span></span>
 7. <span data-ttu-id="45564-164">W klasycznym portalu Azure na **skonfigurować logowanie jednokrotne w piaskownicy Salesforce** dialogu strony, kopiowania **zdalnego adresu URL logowania** wartość, a następnie wklej ją do **adresu URL logowania do dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="45564-164">In the Azure classic portal, on the **Configure single sign-on at Salesforce Sandbox** dialogue page, copy the **Remote Login URL** value, and then paste it into the **Identity Provider Login URL** textbox.</span></span> 
 8. <span data-ttu-id="45564-165">SFDC nie obsługuje SAML wylogowania.</span><span class="sxs-lookup"><span data-stu-id="45564-165">SFDC does not support SAML logout.</span></span>  <span data-ttu-id="45564-166">Jako obejście, Wklej "https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0" go do **adres URL wylogowania dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="45564-166">As a workaround, paste 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' it into the **Identity Provider Logout URL** textbox.</span></span>
 9. <span data-ttu-id="45564-167">Jako **dostawcy zainicjował żądanie powiązania usługi**, wybierz pozycję **HTTP POST**.</span><span class="sxs-lookup"><span data-stu-id="45564-167">As **Service Provider Initiated Request Binding**, select **HTTP POST**.</span></span> 
 10. <span data-ttu-id="45564-168">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="45564-168">Click **Save**.</span></span>
11. <span data-ttu-id="45564-169">W klasycznym portalu Azure, wybierz Potwierdzenie konfiguracji rejestracji jednokrotnej, a następnie kliknij przycisk **Complete** zamknąć **skonfigurować rejestrację jednokrotną** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="45564-169">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="45564-170">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="45564-170">![Configure Single Sign-On](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "Configure Single Sign-On")</span></span>

## <a name="enable-your-domain"></a><span data-ttu-id="45564-171">Włącz domeny</span><span class="sxs-lookup"><span data-stu-id="45564-171">Enable your domain</span></span>
<span data-ttu-id="45564-172">W tej sekcji założono, że już utworzono domeny.</span><span class="sxs-lookup"><span data-stu-id="45564-172">This section assumes that you already have created a domain.</span></span>  <span data-ttu-id="45564-173">Aby uzyskać więcej informacji, zobacz [Definiowanie Twojej nazwy domeny](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span><span class="sxs-lookup"><span data-stu-id="45564-173">For more details, see [Defining Your Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span></span>

<span data-ttu-id="45564-174">**Aby włączyć domeny, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="45564-174">**To enable your domain, perform the following steps:**</span></span>

1. <span data-ttu-id="45564-175">W okienku nawigacji po lewej stronie kliknij **Zarządzanie domenami**, a następnie kliknij przycisk **Moje domeny.**</span><span class="sxs-lookup"><span data-stu-id="45564-175">In the left navigation pane, click **Domain Management**, and then click **My Domain.**</span></span>
   
   <span data-ttu-id="45564-176">![Mojej domeny](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "mojej domeny")</span><span class="sxs-lookup"><span data-stu-id="45564-176">![My Domain](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "My Domain")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="45564-177">Upewnij się, że poprawnie skonfigurowano domenę.</span><span class="sxs-lookup"><span data-stu-id="45564-177">Please make sure that your domain has been configured correctly.</span></span> 
   > 
2. <span data-ttu-id="45564-178">W **ustawienia strony logowania** kliknij **Edytuj**, następnie jako **usługi uwierzytelniania**, wybierz nazwę SAML pojedynczy znak na ustawienie z poprzedniej sekcji, a na koniec kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="45564-178">In the **Login Page Settings** section, click **Edit**, then, as **Authentication Service**, select the name of the SAML Single Sign-On Setting from the previous section, and finally click **Save**.</span></span>
   
   <span data-ttu-id="45564-179">![Mojej domeny](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "mojej domeny")</span><span class="sxs-lookup"><span data-stu-id="45564-179">![My Domain](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "My Domain")</span></span>

<span data-ttu-id="45564-180">Jak masz domenę skonfigurowane, użytkownicy należy używać URL domeny na potrzeby logowania do usługi Salesforce piaskownicy.</span><span class="sxs-lookup"><span data-stu-id="45564-180">As soon as you have a domain configured, your users should use the domain URL to login to the Salesforce sandbox.</span></span>  

<span data-ttu-id="45564-181">Aby uzyskać wartość adresu URL, kliknij profil rejestracji Jednokrotnej, utworzony w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="45564-181">To get the value of the URL, click the SSO profile you have created in the previous section.</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="45564-182">Skonfiguruj Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="45564-182">Configure user provisioning</span></span>
<span data-ttu-id="45564-183">Celem tej sekcji jest przedstawiają sposób włączania kont użytkowników usługi Active Directory do usługi Salesforce piaskownicy Inicjowanie obsługi użytkowników.</span><span class="sxs-lookup"><span data-stu-id="45564-183">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Salesforce Sandbox.</span></span>

<span data-ttu-id="45564-184">**Aby skonfigurować, inicjowanie obsługi użytkowników, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="45564-184">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="45564-185">W portalu usług Salesforce w górnym pasku nawigacyjnym wybierz nazwę, aby rozwinąć menu programu użytkownika:</span><span class="sxs-lookup"><span data-stu-id="45564-185">In the Salesforce portal, in the top navigation bar, select your name to expand your user menu:</span></span>
   
   <span data-ttu-id="45564-186">![Ustawienia](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "Moje ustawienia")</span><span class="sxs-lookup"><span data-stu-id="45564-186">![My Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "My Settings")</span></span>
2. <span data-ttu-id="45564-187">Menu użytkownika wybierz **Moje ustawienia** otworzyć Twojego **Moje ustawienia** strony.</span><span class="sxs-lookup"><span data-stu-id="45564-187">From your user menu, select **My Settings** to open your **My Settings** page.</span></span>
3. <span data-ttu-id="45564-188">W okienku po lewej stronie kliknij **osobistych** rozwiń sekcję osobistych, a następnie kliknij przycisk **zresetować moje tokenu zabezpieczeń**:</span><span class="sxs-lookup"><span data-stu-id="45564-188">In the left pane, click **Personal** to expand the Personal section, and then click **Reset My Security Token**:</span></span>
   
   <span data-ttu-id="45564-189">![Ustawienia](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "Moje ustawienia")</span><span class="sxs-lookup"><span data-stu-id="45564-189">![My Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "My Settings")</span></span>
4. <span data-ttu-id="45564-190">Na **zresetować moje tokenu zabezpieczeń** kliknij przycisk **zresetować tokenu zabezpieczeń** Aby zażądać wiadomości e-mail, który zawiera token zabezpieczeń witryny Salesforce.com.</span><span class="sxs-lookup"><span data-stu-id="45564-190">On the **Reset My Security Token** page, click **Reset Security Token** to request an email that contains your Salesforce.com security token.</span></span>
   
   <span data-ttu-id="45564-191">![Nowy Token](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "nowy Token")</span><span class="sxs-lookup"><span data-stu-id="45564-191">![New Token](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "New Token")</span></span>
5. <span data-ttu-id="45564-192">Sprawdź skrzynki odbiorczej poczty e-mail, wiadomości e-mail z witryny Salesforce.com z "**potwierdzenia zabezpieczeń salesforce.com.com**" jako podmiotu.</span><span class="sxs-lookup"><span data-stu-id="45564-192">Check your email inbox for an email from Salesforce.com with “**salesforce.com.com security confirmation**” as subject.</span></span>
6. <span data-ttu-id="45564-193">Przejrzyj tę wiadomość e-mail, a następnie skopiuj wartość tokenu zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="45564-193">Review this email and copy the security token value.</span></span>
7. <span data-ttu-id="45564-194">W klasycznym portalu Azure na **salesforce piaskownicy** strona integracji aplikacji, kliknij przycisk **skonfigurować Inicjowanie obsługi użytkowników** otworzyć **skonfigurować Inicjowanie obsługi użytkowników** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="45564-194">In the Azure classic portal, on the **salesforce Sandbox** application integration page, click **Configure user provisioning** to open the **Configure User Provisioning** dialog.</span></span>
   
   <span data-ttu-id="45564-195">![Skonfiguruj Inicjowanie obsługi użytkowników](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "skonfigurować Inicjowanie obsługi użytkowników")</span><span class="sxs-lookup"><span data-stu-id="45564-195">![Configure user provisioning](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "Configure user provisioning")</span></span>
8. <span data-ttu-id="45564-196">Na **wprowadź swoje poświadczenia piaskownicy Salesforce umożliwia inicjowanie obsługi użytkowników automatyczne** Podaj następujące ustawienia konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="45564-196">On the **Enter your Salesforce Sandbox credentials to enable automatic user provisioning** page, provide the following configuration settings:</span></span>
   
   <span data-ttu-id="45564-197">![Piaskownica SalesForce](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Salesforce piaskownicy")</span><span class="sxs-lookup"><span data-stu-id="45564-197">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Salesforce Sandbox")</span></span>   
 1. <span data-ttu-id="45564-198">W **nazwa użytkownika administratora piaskownicy Salesforce** tekstowym, wpisz nazwę, która ma konto Salesforce piaskownicy **administratorem** profilu w witrynie Salesforce.com przypisane.</span><span class="sxs-lookup"><span data-stu-id="45564-198">In the **Salesforce Sandbox Admin User Name** textbox, type a Salesforce sandbox account name that has the **System Administrator** profile in Salesforce.com assigned.</span></span>
 2. <span data-ttu-id="45564-199">W **hasło administratora piaskownicy Salesforce** tekstowym, wpisz hasło dla tego konta.</span><span class="sxs-lookup"><span data-stu-id="45564-199">In the **Salesforce Sandbox Admin Password** textbox, type the password for this account.</span></span>
 3. <span data-ttu-id="45564-200">W **tokenu zabezpieczeń użytkownika** pole tekstowe, Wklej wartość tokenu zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="45564-200">In the **User Security Token** textbox, paste the security token value.</span></span>
 4. <span data-ttu-id="45564-201">Kliknij przycisk **weryfikacji** Aby zweryfikować konfigurację.</span><span class="sxs-lookup"><span data-stu-id="45564-201">Click **Validate** to verify your configuration.</span></span>
 5. <span data-ttu-id="45564-202">Kliknij przycisk **dalej** przycisk, aby otworzyć **potwierdzenie** strony.</span><span class="sxs-lookup"><span data-stu-id="45564-202">Click the **Next** button to open the **Confirmation** page.</span></span>
9. <span data-ttu-id="45564-203">Na **potwierdzenie** kliknij przycisk **Complete** Aby zapisać konfigurację.</span><span class="sxs-lookup"><span data-stu-id="45564-203">On the **Confirmation** page, click **Complete** to save your configuration.</span></span>
   
## <a name="assigning-users"></a><span data-ttu-id="45564-204">Przypisywanie użytkowników</span><span class="sxs-lookup"><span data-stu-id="45564-204">Assigning users</span></span>

<span data-ttu-id="45564-205">Aby przetestować konfigurację, musisz przyznać użytkowników usługi Azure AD, czy chcesz zezwolić, używając przypisywania do nich dostęp aplikacji do niego.</span><span class="sxs-lookup"><span data-stu-id="45564-205">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="45564-206">**Do przypisywania użytkowników do usługi Salesforce piaskownicy, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="45564-206">**To assign users to Salesforce Sandbox, perform the following steps:**</span></span>

1. <span data-ttu-id="45564-207">W klasycznym portalu Azure Utwórz konto testu.</span><span class="sxs-lookup"><span data-stu-id="45564-207">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="45564-208">Na ** piaskownicy Salesforce ** strona integracji aplikacji, kliknij przycisk **przypisywać użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="45564-208">On the **Salesforce Sandbox **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="45564-209">![Przypisywanie użytkowników](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "przypisywanie użytkowników")</span><span class="sxs-lookup"><span data-stu-id="45564-209">![Assign users](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "Assign users")</span></span>
3. <span data-ttu-id="45564-210">Wybierz użytkownika testowego, kliknij przycisk **przypisać**, a następnie kliknij przycisk **tak** o potwierdzenie przypisania.</span><span class="sxs-lookup"><span data-stu-id="45564-210">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="45564-211">![Tak](./media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "tak")</span><span class="sxs-lookup"><span data-stu-id="45564-211">![Yes](./media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="45564-212">Należy teraz Odczekaj 10 minut i sprawdź, czy konto zostało zsynchronizowane z Salesforce piaskownicy.</span><span class="sxs-lookup"><span data-stu-id="45564-212">You should now wait for 10 minutes and verify that the account has been synchronized to Salesforce Sandbox.</span></span>

<span data-ttu-id="45564-213">Jeśli chcesz przetestować ustawienia logowania jednokrotnego, otwórz Panel dostępu.</span><span class="sxs-lookup"><span data-stu-id="45564-213">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="45564-214">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="45564-214">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

