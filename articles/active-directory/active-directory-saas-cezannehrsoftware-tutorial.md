---
title: 'Samouczek: Azure Active Directory integracji z oprogramowaniem Cezanne HR | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między oprogramowaniem Cezanne HR i Azure Active Directory."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fb8f95bf-c3c1-4e1f-b2b3-3b67526be72d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 623c438edfce5f98c2d32d8bb25a97d86aa77909
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-cezanne-hr-software"></a><span data-ttu-id="a178f-103">Samouczek: Integrowanie usługi Azure Active Directory z oprogramowaniem Cezanne HR</span><span class="sxs-lookup"><span data-stu-id="a178f-103">Tutorial: Integrate Azure Active Directory with Cezanne HR software</span></span>

<span data-ttu-id="a178f-104">Z tego samouczka dowiesz się integrowanie Cezanne HR oprogramowania z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a178f-104">In this tutorial, you learn how to integrate Cezanne HR software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a178f-105">Integracja oprogramowania Cezanne HR z usługą Azure AD zapewnia następujące korzyści.</span><span class="sxs-lookup"><span data-stu-id="a178f-105">Integrating Cezanne HR software with Azure AD provides you with the following benefits.</span></span> <span data-ttu-id="a178f-106">Możesz:</span><span class="sxs-lookup"><span data-stu-id="a178f-106">You can:</span></span>

- <span data-ttu-id="a178f-107">Kontrolowanie w usłudze Azure AD, który ma dostęp do oprogramowania Cezanne HR.</span><span class="sxs-lookup"><span data-stu-id="a178f-107">Control in Azure AD who has access to Cezanne HR software.</span></span>
- <span data-ttu-id="a178f-108">Umożliwianie użytkownikom automatycznie logować się do oprogramowania Cezanne HR z logowaniem jednokrotnym (SSO) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a178f-108">Enable your users to automatically sign in to Cezanne HR software with single sign-on (SSO) with their Azure AD accounts.</span></span>
- <span data-ttu-id="a178f-109">Zarządzanie kont w jednej centralnej lokalizacji: portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="a178f-109">Manage your accounts in one central location: the Azure portal.</span></span>

<span data-ttu-id="a178f-110">Aby dowiedzieć się więcej na temat oprogramowania jako usługa (SaaS) integracji aplikacji z usługą Azure AD, zobacz [co to jest dostęp do aplikacji i logowania jednokrotnego w usłudze Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a178f-110">To learn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and SSO with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a178f-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a178f-111">Prerequisites</span></span>

<span data-ttu-id="a178f-112">Aby skonfigurować integrację usługi Azure AD z oprogramowaniem Cezanne HR, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="a178f-112">To configure Azure AD integration with Cezanne HR software, you need the following items:</span></span>

- <span data-ttu-id="a178f-113">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a178f-113">An Azure AD subscription</span></span>
- <span data-ttu-id="a178f-114">Logowanie Jednokrotne włączone subskrypcji oprogramowania Cezanne HR</span><span class="sxs-lookup"><span data-stu-id="a178f-114">A Cezanne HR software SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a178f-115">Do testowania czynności w tym samouczku, firma Microsoft zaleca, nie używaj do środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="a178f-115">To test the steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="a178f-116">Aby przetestować kroki opisane w tym samouczku, wykonaj te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="a178f-116">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="a178f-117">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="a178f-117">Don't use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a178f-118">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a178f-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a178f-119">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="a178f-119">Scenario description</span></span>
<span data-ttu-id="a178f-120">W tym samouczku można przetestować logowania jednokrotnego programu Azure AD w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="a178f-120">In this tutorial, you test Azure AD SSO in a test environment.</span></span> 

<span data-ttu-id="a178f-121">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="a178f-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="a178f-122">Dodawanie oprogramowania Cezanne HR z galerii</span><span class="sxs-lookup"><span data-stu-id="a178f-122">Adding Cezanne HR software from the gallery</span></span>
* <span data-ttu-id="a178f-123">Konfigurowanie i testowania logowania jednokrotnego programu Azure AD</span><span class="sxs-lookup"><span data-stu-id="a178f-123">Configuring and testing Azure AD SSO</span></span>

## <a name="add-cezanne-hr-software-from-the-gallery"></a><span data-ttu-id="a178f-124">Dodawanie oprogramowania Cezanne HR z galerii</span><span class="sxs-lookup"><span data-stu-id="a178f-124">Add Cezanne HR software from the gallery</span></span>
<span data-ttu-id="a178f-125">Aby skonfigurować integrację usługi Azure AD Cezanne HR oprogramowania, należy dodać Cezanne HR oprogramowania z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="a178f-125">To configure the integration of Cezanne HR software into Azure AD, add Cezanne HR software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a178f-126">Aby dodać Cezanne HR oprogramowanie z poziomu galerii, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a178f-126">To add Cezanne HR software from the gallery, do the following:</span></span>

1. <span data-ttu-id="a178f-127">W  **[portalu Azure](https://portal.azure.com)**, w okienku po lewej stronie wybierz **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a178f-127">In the **[Azure portal](https://portal.azure.com)**, in the left pane, select the **Azure Active Directory** button.</span></span> 

    ![Przycisk "Azure Active Directory"][1]

2. <span data-ttu-id="a178f-129">Wybierz **aplikacje dla przedsiębiorstw** > **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="a178f-129">Select **Enterprise applications** > **All applications**.</span></span>

    ![Łącze "Wszystkie aplikacje"][2]
    
3. <span data-ttu-id="a178f-131">Aby dodać nową aplikację, w górnej części **wszystkie aplikacje** okno dialogowe, wybierz opcję **nowej aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="a178f-131">To add a new application, at the top of the **All applications** dialog box, select **New application**.</span></span>

    !["Nowa aplikacja" przycisku][3]

4. <span data-ttu-id="a178f-133">W polu wyszukiwania wpisz **Cezanne HR oprogramowania**.</span><span class="sxs-lookup"><span data-stu-id="a178f-133">In the search box, type **Cezanne HR Software**.</span></span>

    ![Pole wyszukiwania](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_search.png)

5. <span data-ttu-id="a178f-135">Na liście wyników wybierz **oprogramowania HR Cezanne** , a następnie wybierz **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="a178f-135">In the results list, select **Cezanne HR Software** and then select the **Add** button to add the application.</span></span>

    ![Lista wyników](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a178f-137">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="a178f-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="a178f-138">W tej sekcji możesz skonfigurować i przetestować logowania jednokrotnego programu Azure AD z oprogramowaniem Cezanne HR oparte na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="a178f-138">In this section, you configure and test Azure AD SSO with Cezanne HR software based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a178f-139">Aby logowania jednokrotnego do pracy usługi Azure AD musi znać odpowiednikiem oprogramowania Cezanne HR użytkownika usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a178f-139">For SSO to work, Azure AD needs to know the Cezanne HR software counterpart to the Azure AD user.</span></span> <span data-ttu-id="a178f-140">Innymi słowy musisz ustanowić łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w oprogramowaniu Cezanne HR.</span><span class="sxs-lookup"><span data-stu-id="a178f-140">In other words, you must establish a link relationship between an Azure AD user and the related user in the Cezanne HR software.</span></span>

<span data-ttu-id="a178f-141">Ustanowienie relacji łącze przypisywania oprogramowania Cezanne HR **nazwy użytkownika** wartość, jak usługi Azure AD **Username** wartość.</span><span class="sxs-lookup"><span data-stu-id="a178f-141">To establish the link relationship, assign the Cezanne HR software **user name** value as the Azure AD **Username** value.</span></span>

<span data-ttu-id="a178f-142">Aby skonfigurować i test rejestracji Jednokrotnej programu Azure AD przy użyciu oprogramowania Cezanne HR, wykonaj poniższe bloki konstrukcyjne.</span><span class="sxs-lookup"><span data-stu-id="a178f-142">To configure and test Azure AD SSO by using Cezanne HR software, complete the following building blocks.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="a178f-143">Konfigurowanie usługi Azure AD logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="a178f-143">Configure Azure AD SSO</span></span>

<span data-ttu-id="a178f-144">W tej sekcji możesz włączenia funkcji logowania jednokrotnego usługi Azure AD w portalu Azure i konfigurowanie logowania jednokrotnego do aplikacji oprogramowania Cezanne HR w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="a178f-144">In this section, you can enable Azure AD SSO in the Azure portal and configure SSO in your Cezanne HR software application by doing the following:</span></span>

1. <span data-ttu-id="a178f-145">W portalu Azure na **oprogramowania HR Cezanne** strona integracji aplikacji, wybierz opcję **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="a178f-145">In the Azure portal, on the **Cezanne HR Software** application integration page, select **Single sign-on**.</span></span>

    ![Polecenie "Logowanie jednokrotne"][4]

2. <span data-ttu-id="a178f-147">Aby włączyć logowanie Jednokrotne, w **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="a178f-147">To enable SSO, in the **Single sign-on** dialog box, select the **Mode** as **SAML-based Sign-on**.</span></span>
 
    ![Pole "Tryb"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_samlbase.png)

3. <span data-ttu-id="a178f-149">W obszarze **Cezanne HR oprogramowania domeny i adres URL**, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a178f-149">Under **Cezanne HR Software Domain and URLs**, do the following:</span></span>

    ![W sekcji "Cezanne HR oprogramowania domeny i adresy URL"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_url.png)

    <span data-ttu-id="a178f-151">a.</span><span class="sxs-lookup"><span data-stu-id="a178f-151">a.</span></span> <span data-ttu-id="a178f-152">W **adres URL logowania** wpisz adres URL, który ma następującą składnię:`https://w3.cezanneondemand.com/cezannehr/-/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="a178f-152">In the **Sign-on URL** box, type a URL that has the following syntax: `https://w3.cezanneondemand.com/cezannehr/-/<tenant id>`</span></span>

    <span data-ttu-id="a178f-153">b.</span><span class="sxs-lookup"><span data-stu-id="a178f-153">b.</span></span> <span data-ttu-id="a178f-154">W **adres URL odpowiedzi** wpisz adres URL, który ma następującą składnię:`https://w3.cezanneondemand.com:443/<tenantid>`</span><span class="sxs-lookup"><span data-stu-id="a178f-154">In the **Reply URL** box, type a URL that has the following syntax: `https://w3.cezanneondemand.com:443/<tenantid>`</span></span>    
     
    > [!NOTE] 
    > <span data-ttu-id="a178f-155">Poprzednie wartości nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="a178f-155">The preceding values are not real.</span></span> <span data-ttu-id="a178f-156">Zaktualizuj je z odpowiedzi rzeczywisty adres URL i adresu URL logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="a178f-156">Update them with the actual reply URL and the sign-on URL.</span></span> <span data-ttu-id="a178f-157">Aby uzyskać wartości, skontaktuj się z [Cezanne HR oprogramowanie klienta z pomocą techniczną](mailto:info@cezannehr.com).</span><span class="sxs-lookup"><span data-stu-id="a178f-157">To obtain the values, contact the [Cezanne HR software client support team](mailto:info@cezannehr.com).</span></span>

4. <span data-ttu-id="a178f-158">W obszarze **SAML certyfikat podpisywania**, wybierz pozycję **certyfikatu (Base64)**, a następnie zapisz plik certyfikatu na komputerze.</span><span class="sxs-lookup"><span data-stu-id="a178f-158">Under **SAML Signing Certificate**, select **Certificate (Base64)**, and then save the certificate file on your computer.</span></span>

    ![W sekcji "Certyfikat podpisywania SAML"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_certificate.png) 

5. <span data-ttu-id="a178f-160">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="a178f-160">Select **Save**.</span></span>

    ![Przycisk "Zapisz"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="a178f-162">W obszarze **konfiguracji oprogramowania HR Cezanne**, wybierz pozycję **Konfigurowanie oprogramowania HR Cezanne** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="a178f-162">Under **Cezanne HR Software Configuration**, select **Configure Cezanne HR Software** to open the **Configure sign-on** window.</span></span> <span data-ttu-id="a178f-163">Kopiuj **SAML identyfikator jednostki** i **SAML logowania jednokrotnego usługi pojedynczej** adresu URL z **krótki przewodnik** sekcji.</span><span class="sxs-lookup"><span data-stu-id="a178f-163">Copy the **SAML Entity ID** and **SAML Single Sign-On Service** URL from the **Quick Reference** section.</span></span>

    ![W sekcji "Konfiguracja oprogramowania HR Cezanne"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_configure.png) 

7. <span data-ttu-id="a178f-165">W oknie przeglądarki innej witryny sieci web Zaloguj się do dzierżawy oprogramowania Cezanne HR jako administrator.</span><span class="sxs-lookup"><span data-stu-id="a178f-165">In a different web browser window, sign on to your Cezanne HR software tenant as an administrator.</span></span>

8. <span data-ttu-id="a178f-166">W okienku po lewej stronie wybierz **konfiguracji systemu**.</span><span class="sxs-lookup"><span data-stu-id="a178f-166">In the left pane, select **System Setup**.</span></span> <span data-ttu-id="a178f-167">Wybierz **ustawienia zabezpieczeń** > **pojedynczy konfiguracji logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="a178f-167">Select **Security Settings** > **Single Sign-On Configuration**.</span></span>

    ![Łącze "Pojedynczego logowania jednokrotnego konfiguracji"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_000.png)

9. <span data-ttu-id="a178f-169">W **Zezwalaj użytkownikom na logowanie przy użyciu następujących usług pojedynczego logowania jednokrotnego (SSO)** okienku wybierz **SAML 2.0** pole wyboru, a następnie wybierz **Advanced Configuration** opcji.</span><span class="sxs-lookup"><span data-stu-id="a178f-169">In the **Allow users to log in using the following Single Sign-On (SSO) services** pane, select the **SAML 2.0** check box and select the **Advanced Configuration** option.</span></span>

    ![Opcje logowania jednokrotnego usług](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_001.png)

10. <span data-ttu-id="a178f-171">Wybierz **Dodawanie nowych**.</span><span class="sxs-lookup"><span data-stu-id="a178f-171">Select **Add New**.</span></span>

    ![Przycisk "Dodaj nowy"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_002.png)

11. <span data-ttu-id="a178f-173">W obszarze **dostawców tożsamości SAML 2.0**, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a178f-173">Under **SAML 2.0 Identity Providers**, do the following:</span></span>

    ![W sekcji "Dostawców tożsamości SAML 2.0"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_003.png)
    
    <span data-ttu-id="a178f-175">a.</span><span class="sxs-lookup"><span data-stu-id="a178f-175">a.</span></span> <span data-ttu-id="a178f-176">W **Nazwa wyświetlana** wprowadź nazwę dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="a178f-176">In the **Display Name** box, enter the name of your identity provider.</span></span>

    <span data-ttu-id="a178f-177">b.</span><span class="sxs-lookup"><span data-stu-id="a178f-177">b.</span></span> <span data-ttu-id="a178f-178">W **identyfikator** Wklej **identyfikator jednostki SAML** skopiowany z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="a178f-178">In the **Entity Identifier** box, paste the **SAML Entity ID** that you copied from the Azure portal.</span></span> 

    <span data-ttu-id="a178f-179">c.</span><span class="sxs-lookup"><span data-stu-id="a178f-179">c.</span></span> <span data-ttu-id="a178f-180">W **powiązanie SAML** pola listy, wybierz opcję **POST**.</span><span class="sxs-lookup"><span data-stu-id="a178f-180">In the **SAML Binding** list box, select **POST**.</span></span>

    <span data-ttu-id="a178f-181">d.</span><span class="sxs-lookup"><span data-stu-id="a178f-181">d.</span></span> <span data-ttu-id="a178f-182">W **punktu końcowego usługi tokenu zabezpieczającego** Wklej **SAML logowania jednokrotnego usługi pojedynczej** adres URL, który został skopiowany z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="a178f-182">In the **Security Token Service Endpoint** box, paste the **SAML Single Sign-On Service** URL that you copied from the Azure portal.</span></span> 
    
    <span data-ttu-id="a178f-183">e.</span><span class="sxs-lookup"><span data-stu-id="a178f-183">e.</span></span> <span data-ttu-id="a178f-184">W **nazwa atrybutu ID użytkownika** wprowadź `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="a178f-184">In the **User ID Attribute Name** box, enter `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
    
    <span data-ttu-id="a178f-185">f.</span><span class="sxs-lookup"><span data-stu-id="a178f-185">f.</span></span> <span data-ttu-id="a178f-186">Aby przekazać certyfikat pobrany z usługi Azure AD, wybierz **przekazać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a178f-186">To upload the downloaded certificate from Azure AD, select the **Upload** button.</span></span>
    
    <span data-ttu-id="a178f-187">g.</span><span class="sxs-lookup"><span data-stu-id="a178f-187">g.</span></span> <span data-ttu-id="a178f-188">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="a178f-188">Select **OK**.</span></span> 

12. <span data-ttu-id="a178f-189">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="a178f-189">Select **Save**.</span></span>

    ![Przycisk "Zapisz"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_004.png)

> [!TIP]
> <span data-ttu-id="a178f-191">Po skonfigurowaniu aplikacji może odczytywać zwięzły wersji poprzednich instrukcji w [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a178f-191">As you set up the app, you can read a concise version of the preceding instructions in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="a178f-192">Po dodaniu aplikacji z **usługi Active Directory** > **aplikacje dla przedsiębiorstw** zaznacz **logowanie jednokrotne** kartę. Dostęp do dokumentacji osadzonych z **konfiguracji** sekcji.</span><span class="sxs-lookup"><span data-stu-id="a178f-192">After you add the app from the **Active Directory** > **Enterprise applications** section, select the **Single sign-on** tab. Then access the embedded documentation from the **Configuration** section.</span></span> 

<span data-ttu-id="a178f-193">Aby dowiedzieć się więcej o funkcji osadzonych dokumentacji, zobacz [usługi Azure AD osadzonych dokumentacji]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="a178f-193">To learn more about the embedded documentation feature, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a178f-194">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a178f-194">Create an Azure AD test user</span></span>
<span data-ttu-id="a178f-195">W tej sekcji utworzysz użytkownika testowego Simona Britta w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="a178f-195">In this section, you create test user Britta Simon in the Azure portal.</span></span>

![Simona Britta użytkownika testowego][100]

<span data-ttu-id="a178f-197">Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a178f-197">To create a test user in Azure AD, do the following:</span></span>

1. <span data-ttu-id="a178f-198">W **portalu Azure**, w okienku po lewej stronie wybierz **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a178f-198">In the **Azure portal**, in the left pane, select the **Azure Active Directory** button.</span></span>

    ![Przycisk "Azure Active Directory"](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a178f-200">Aby wyświetlić listę użytkowników, wybierz **użytkowników i grup** > **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="a178f-200">To display the list of users, select **Users and groups** > **All users**.</span></span>
    
    ![Łącze "Wszyscy użytkownicy"](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_02.png) 
    
    <span data-ttu-id="a178f-202">**Wszyscy użytkownicy** zostanie otwarte okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="a178f-202">The **All users** dialog box opens.</span></span>

3. <span data-ttu-id="a178f-203">Aby otworzyć **użytkownika** okno dialogowe, wybierz opcję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="a178f-203">To open the **User** dialog box, select **Add**.</span></span>
 
    ![Przycisk "Dodaj"](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a178f-205">W **użytkownika** okno dialogowe, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a178f-205">In the **User** dialog box, do the following:</span></span>
 
    ![Okno dialogowe "Użytkownika"](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a178f-207">a.</span><span class="sxs-lookup"><span data-stu-id="a178f-207">a.</span></span> <span data-ttu-id="a178f-208">W **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a178f-208">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a178f-209">b.</span><span class="sxs-lookup"><span data-stu-id="a178f-209">b.</span></span> <span data-ttu-id="a178f-210">W **nazwy użytkownika** wpisz użytkownika Britta Simona **adres e-mail**.</span><span class="sxs-lookup"><span data-stu-id="a178f-210">In the **User name** box, type user Britta Simon's **email address**.</span></span>

    <span data-ttu-id="a178f-211">c.</span><span class="sxs-lookup"><span data-stu-id="a178f-211">c.</span></span> <span data-ttu-id="a178f-212">Wybierz **Pokaż hasło** pole wyboru, a następnie zanotuj wartości, który został wygenerowany w **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="a178f-212">Select the **Show Password** check box, and then note the value that was generated in the **Password** box.</span></span>

    <span data-ttu-id="a178f-213">d.</span><span class="sxs-lookup"><span data-stu-id="a178f-213">d.</span></span> <span data-ttu-id="a178f-214">Wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="a178f-214">Select **Create**.</span></span>
 
### <a name="create-a-cezanne-hr-software-test-user"></a><span data-ttu-id="a178f-215">Tworzenie użytkownika testowego Cezanne HR oprogramowania</span><span class="sxs-lookup"><span data-stu-id="a178f-215">Create a Cezanne HR software test user</span></span>

<span data-ttu-id="a178f-216">Aby umożliwić użytkownikom usługi Azure AD do logowania się na Cezanne HR oprogramowania, muszą mieć przydzielone do Cezanne HR oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="a178f-216">To enable Azure AD users to sign in to Cezanne HR software, they must be provisioned into Cezanne HR software.</span></span> <span data-ttu-id="a178f-217">W przypadku oprogramowania Cezanne HR Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="a178f-217">In the case of Cezanne HR software, provisioning is a manual task.</span></span>

<span data-ttu-id="a178f-218">Ustanowienie konta użytkownika, wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a178f-218">Provision a user account by doing the following:</span></span>

1.  <span data-ttu-id="a178f-219">Zaloguj się do witryny Cezanne HR oprogramowania firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="a178f-219">Sign in to your Cezanne HR software company site as an administrator.</span></span>

2.  <span data-ttu-id="a178f-220">W okienku po lewej stronie wybierz **konfiguracji systemu** > **Zarządzanie użytkownikami** > **Dodaj nowego użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="a178f-220">In the left pane, select **System Setup** > **Manage Users** > **Add New User**.</span></span>

    <span data-ttu-id="a178f-221">![Łącze "Dodaj nowego użytkownika"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "nowego użytkownika")</span><span class="sxs-lookup"><span data-stu-id="a178f-221">![The "Add New User" link](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "New User")</span></span>

3.  <span data-ttu-id="a178f-222">W obszarze **dane osobowe**, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a178f-222">Under **Person Details**, do the following:</span></span>

    <span data-ttu-id="a178f-223">![W sekcji "Dane osobowe"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "nowego użytkownika")</span><span class="sxs-lookup"><span data-stu-id="a178f-223">![The "Person Details" section](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "New User")</span></span>
    
    <span data-ttu-id="a178f-224">a.</span><span class="sxs-lookup"><span data-stu-id="a178f-224">a.</span></span> <span data-ttu-id="a178f-225">Ustaw **wewnętrznego użytkownika** jako **OFF**.</span><span class="sxs-lookup"><span data-stu-id="a178f-225">Set **Internal User** as **OFF**.</span></span>
    
    <span data-ttu-id="a178f-226">b.</span><span class="sxs-lookup"><span data-stu-id="a178f-226">b.</span></span> <span data-ttu-id="a178f-227">W **imię** wpisz imię użytkownika, na przykład **Britta**.</span><span class="sxs-lookup"><span data-stu-id="a178f-227">In the **First Name** box, type the user's first name, for example, **Britta**.</span></span>  
 
    <span data-ttu-id="a178f-228">c.</span><span class="sxs-lookup"><span data-stu-id="a178f-228">c.</span></span> <span data-ttu-id="a178f-229">W **nazwisko** wpisz nazwisko użytkownika, na przykład **Simona**.</span><span class="sxs-lookup"><span data-stu-id="a178f-229">In the **Last Name** box, type the user's last name, for example, **Simon**.</span></span>
    
    <span data-ttu-id="a178f-230">d.</span><span class="sxs-lookup"><span data-stu-id="a178f-230">d.</span></span> <span data-ttu-id="a178f-231">W **E-mail** wpisz adres e-mail użytkownika, na przykład Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="a178f-231">In the **E-mail** box, type the user's email address, for example, Brittasimon@contoso.com.</span></span>

4.  <span data-ttu-id="a178f-232">W obszarze **informacje o koncie**, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a178f-232">Under **Account Information**, do the following:</span></span>

    <span data-ttu-id="a178f-233">![Sekcja "Informacje o koncie"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "nowego użytkownika")</span><span class="sxs-lookup"><span data-stu-id="a178f-233">![The "Account Information" section](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "New User")</span></span>
    
    <span data-ttu-id="a178f-234">a.</span><span class="sxs-lookup"><span data-stu-id="a178f-234">a.</span></span> <span data-ttu-id="a178f-235">W **Username** wpisz adres e-mail użytkownika, na przykład Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="a178f-235">In the **Username** box, type the user's email address, for example, Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="a178f-236">b.</span><span class="sxs-lookup"><span data-stu-id="a178f-236">b.</span></span> <span data-ttu-id="a178f-237">W **hasło** wpisz hasło użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a178f-237">In the **Password** box, type the user's password.</span></span>
    
    <span data-ttu-id="a178f-238">c.</span><span class="sxs-lookup"><span data-stu-id="a178f-238">c.</span></span> <span data-ttu-id="a178f-239">W **roli zabezpieczeń** wybierz opcję **HR Professional**.</span><span class="sxs-lookup"><span data-stu-id="a178f-239">In the **Security Role** box, select **HR Professional**.</span></span>
    
    <span data-ttu-id="a178f-240">d.</span><span class="sxs-lookup"><span data-stu-id="a178f-240">d.</span></span> <span data-ttu-id="a178f-241">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="a178f-241">Select **OK**.</span></span>

5. <span data-ttu-id="a178f-242">Na **logowanie jednokrotne** karcie **SAML 2.0 identyfikatory** zaznacz **Dodaj nowy**.</span><span class="sxs-lookup"><span data-stu-id="a178f-242">On the **Single sign-on** tab, in the **SAML 2.0 Identifiers** section, select **Add New**.</span></span>

    <span data-ttu-id="a178f-243">![Przycisk "Dodaj nowy"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "użytkownika")</span><span class="sxs-lookup"><span data-stu-id="a178f-243">![The "Add New" button](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "User")</span></span>

6. <span data-ttu-id="a178f-244">W **dostawcy tożsamości** pola listy, wybierz dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="a178f-244">In the **Identity Provider** list box, select your identity provider.</span></span> <span data-ttu-id="a178f-245">W **identyfikator użytkownika** wprowadź adres e-mail konta Simona testu użytkownika Britta.</span><span class="sxs-lookup"><span data-stu-id="a178f-245">In the **User Identifier** box, enter the email address for test user Britta Simon's account.</span></span>

    <span data-ttu-id="a178f-246">![Pola "Dostawcy tożsamości" i "Identyfikator użytkownika"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "użytkownika")</span><span class="sxs-lookup"><span data-stu-id="a178f-246">![The "Identity Provider" and "User Identifier" boxes](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "User")</span></span>
    
7. <span data-ttu-id="a178f-247">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="a178f-247">Select **Save**.</span></span>

    <span data-ttu-id="a178f-248">![Przycisk "Zapisz"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "użytkownika")</span><span class="sxs-lookup"><span data-stu-id="a178f-248">![The "Save" button](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "User")</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="a178f-249">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a178f-249">Assign the Azure AD test user</span></span>

<span data-ttu-id="a178f-250">W tej sekcji można włączyć użytkownika testowego Simona Britta do udzielania dostępu do oprogramowania Cezanne HR za pomocą logowania jednokrotnego usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="a178f-250">In this section, you enable test user Britta Simon to use Azure SSO by granting access to Cezanne HR software.</span></span>

![Dostęp użytkownika testowego][200] 

1. <span data-ttu-id="a178f-252">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu.</span><span class="sxs-lookup"><span data-stu-id="a178f-252">In the Azure portal, open the applications view and then go to the directory view.</span></span> <span data-ttu-id="a178f-253">Wybierz **aplikacje dla przedsiębiorstw** > **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="a178f-253">Select **Enterprise applications** > **All applications**.</span></span>

    ![Łącze "Wszystkie aplikacje"][201] 

2. <span data-ttu-id="a178f-255">Na liście aplikacji zaznacz **Cezanne HR oprogramowania**.</span><span class="sxs-lookup"><span data-stu-id="a178f-255">In the applications list, select **Cezanne HR Software**.</span></span>

    ![Na liście "Aplikacji"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_app.png) 

3. <span data-ttu-id="a178f-257">W menu po lewej stronie wybierz **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="a178f-257">In the menu on the left, select **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="a178f-259">Wybierz pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="a178f-259">Select **Add**.</span></span> <span data-ttu-id="a178f-260">Następnie w **Dodaj przydziału** okno dialogowe, wybierz opcję **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="a178f-260">Then in the **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![Łącze "Użytkownicy i grupy"][203]

5. <span data-ttu-id="a178f-262">W **użytkowników i grup** okna dialogowego, **użytkowników** listy, wybierz **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="a178f-262">In the **Users and groups** dialog box, in the **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="a178f-263">W **użytkowników i grup** okno dialogowe, wybierz opcję **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="a178f-263">In the **Users and groups** dialog box, select **Select**.</span></span>

7. <span data-ttu-id="a178f-264">W **Dodaj przydziału** okno dialogowe, wybierz opcję **przypisać**.</span><span class="sxs-lookup"><span data-stu-id="a178f-264">In the **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-sso"></a><span data-ttu-id="a178f-265">Test rejestracji Jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="a178f-265">Test SSO</span></span>

<span data-ttu-id="a178f-266">W tej sekcji możesz przetestować konfigurację programu Azure AD z logowania jednokrotnego za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="a178f-266">In this section, you test your Azure AD SSO configuration by using the Access Panel.</span></span>

<span data-ttu-id="a178f-267">Po wybraniu kafelka oprogramowania Cezanne HR w panelu dostępu logowania automatycznie do aplikacji oprogramowania Cezanne HR.</span><span class="sxs-lookup"><span data-stu-id="a178f-267">When you select the Cezanne HR software tile in the Access Panel, you sign on automatically to your Cezanne HR software application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a178f-268">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a178f-268">Next steps</span></span>

* [<span data-ttu-id="a178f-269">Lista samouczków dotyczących sposobów integracji aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a178f-269">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a178f-270">Co to jest dostęp do aplikacji i logowania jednokrotnego w usłudze Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a178f-270">What is application access and SSO with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_203.png

