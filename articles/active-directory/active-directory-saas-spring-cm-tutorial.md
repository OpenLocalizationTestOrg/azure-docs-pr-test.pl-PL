---
title: 'Samouczek: Integracji Azure Active Directory z SpringCM | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i SpringCM."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4a42f797-ac58-4aca-a8e6-53bfe5529083
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: edfd06a06c730597fee4569ca1ce29092b45244a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-springcm"></a><span data-ttu-id="7bec6-103">Samouczek: Integracji Azure Active Directory z SpringCM</span><span class="sxs-lookup"><span data-stu-id="7bec6-103">Tutorial: Azure Active Directory integration with SpringCM</span></span>

<span data-ttu-id="7bec6-104">Z tego samouczka dowiesz się integrowanie SpringCM z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7bec6-104">In this tutorial, you learn how to integrate SpringCM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7bec6-105">Integracja z usługą Azure AD SpringCM zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="7bec6-105">Integrating SpringCM with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7bec6-106">Można kontrolować w usłudze Azure AD, który ma dostęp do SpringCM</span><span class="sxs-lookup"><span data-stu-id="7bec6-106">You can control in Azure AD who has access to SpringCM</span></span>
- <span data-ttu-id="7bec6-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do SpringCM (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7bec6-107">You can enable your users to automatically get signed-on to SpringCM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7bec6-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="7bec6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7bec6-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7bec6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7bec6-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7bec6-110">Prerequisites</span></span>

<span data-ttu-id="7bec6-111">Aby skonfigurować integrację usługi Azure AD z SpringCM, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="7bec6-111">To configure Azure AD integration with SpringCM, you need the following items:</span></span>

- <span data-ttu-id="7bec6-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7bec6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7bec6-113">SpringCM logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="7bec6-113">A SpringCM single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7bec6-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="7bec6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7bec6-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="7bec6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7bec6-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="7bec6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7bec6-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7bec6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7bec6-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="7bec6-118">Scenario description</span></span>
<span data-ttu-id="7bec6-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="7bec6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7bec6-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="7bec6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7bec6-121">Dodawanie SpringCM z galerii</span><span class="sxs-lookup"><span data-stu-id="7bec6-121">Adding SpringCM from the gallery</span></span>
2. <span data-ttu-id="7bec6-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="7bec6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-springcm-from-the-gallery"></a><span data-ttu-id="7bec6-123">Dodawanie SpringCM z galerii</span><span class="sxs-lookup"><span data-stu-id="7bec6-123">Adding SpringCM from the gallery</span></span>
<span data-ttu-id="7bec6-124">Aby skonfigurować integrację usługi Azure AD SpringCM, należy dodać SpringCM z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="7bec6-124">To configure the integration of SpringCM into Azure AD, you need to add SpringCM from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7bec6-125">**Aby dodać SpringCM z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="7bec6-125">**To add SpringCM from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7bec6-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="7bec6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="7bec6-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="7bec6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7bec6-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="7bec6-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="7bec6-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7bec6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="7bec6-133">W polu wyszukiwania wpisz **SpringCM**.</span><span class="sxs-lookup"><span data-stu-id="7bec6-133">In the search box, type **SpringCM**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_search.png)

5. <span data-ttu-id="7bec6-135">W panelu wyników wybierz **SpringCM**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="7bec6-135">In the results panel, select **SpringCM**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7bec6-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="7bec6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7bec6-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z SpringCM na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="7bec6-138">In this section, you configure and test Azure AD single sign-on with SpringCM based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7bec6-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w SpringCM jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7bec6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SpringCM is to a user in Azure AD.</span></span> <span data-ttu-id="7bec6-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w SpringCM musi się.</span><span class="sxs-lookup"><span data-stu-id="7bec6-140">In other words, a link relationship between an Azure AD user and the related user in SpringCM needs to be established.</span></span>

<span data-ttu-id="7bec6-141">W SpringCM, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="7bec6-141">In SpringCM, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7bec6-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z SpringCM, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="7bec6-142">To configure and test Azure AD single sign-on with SpringCM, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7bec6-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="7bec6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7bec6-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="7bec6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7bec6-145">**[Tworzenie użytkownika testowego SpringCM](#creating-a-springcm-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta SpringCM połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7bec6-145">**[Creating a SpringCM test user](#creating-a-springcm-test-user)** - to have a counterpart of Britta Simon in SpringCM that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7bec6-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="7bec6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7bec6-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="7bec6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7bec6-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="7bec6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7bec6-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji SpringCM.</span><span class="sxs-lookup"><span data-stu-id="7bec6-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SpringCM application.</span></span>

<span data-ttu-id="7bec6-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z SpringCM, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="7bec6-150">**To configure Azure AD single sign-on with SpringCM, perform the following steps:**</span></span>

1. <span data-ttu-id="7bec6-151">W portalu Azure na **SpringCM** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="7bec6-151">In the Azure portal, on the **SpringCM** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="7bec6-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="7bec6-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_samlbase.png)

3. <span data-ttu-id="7bec6-155">Na **SpringCM domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7bec6-155">On the **SpringCM Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_url.png)

    <span data-ttu-id="7bec6-157">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://na11.springcm.com/atlas/SSO/SSOEndpoint.ashx?aid=<identifier>`</span><span class="sxs-lookup"><span data-stu-id="7bec6-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://na11.springcm.com/atlas/SSO/SSOEndpoint.ashx?aid=<identifier>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7bec6-158">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="7bec6-158">This value is not real.</span></span> <span data-ttu-id="7bec6-159">Zaktualizuj tę wartość przy rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="7bec6-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="7bec6-160">Skontaktuj się z [zespołem pomocy technicznej klienta SpringCM](https://knowledge.springcm.com/support) aby zyskać tę wartość.</span><span class="sxs-lookup"><span data-stu-id="7bec6-160">Contact [SpringCM Client support team](https://knowledge.springcm.com/support) to get this value.</span></span> 
 
4. <span data-ttu-id="7bec6-161">Na **certyfikat podpisywania SAML** kliknij **Certificate(Raw)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="7bec6-161">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_certificate.png) 

5. <span data-ttu-id="7bec6-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="7bec6-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-spring-cm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7bec6-165">Na **konfiguracji SpringCM** , kliknij przycisk **skonfigurować SpringCM** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="7bec6-165">On the **SpringCM Configuration** section, click **Configure SpringCM** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7bec6-166">Kopiuj **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="7bec6-166">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_configure.png)   

7. <span data-ttu-id="7bec6-168">W oknie przeglądarki innej witryny sieci web, zaloguj się na Twojej **SpringCM** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="7bec6-168">In a different web browser window, sign on to your **SpringCM** company site as administrator.</span></span>

8. <span data-ttu-id="7bec6-169">W menu u góry kliknij **przejdź do**, kliknij przycisk **preferencje**, a następnie w **preferencje konta** , kliknij przycisk **logowania jednokrotnego SAML**.</span><span class="sxs-lookup"><span data-stu-id="7bec6-169">In the menu on the top, click **GO TO**, click **Preferences**, and then, in the **Account Preferences** section, click **SAML SSO**.</span></span>
   
    <span data-ttu-id="7bec6-170">![LOGOWANIA JEDNOKROTNEGO SAML](./media/active-directory-saas-spring-cm-tutorial/ic797051.png "LOGOWANIA JEDNOKROTNEGO SAML")</span><span class="sxs-lookup"><span data-stu-id="7bec6-170">![SAML SSO](./media/active-directory-saas-spring-cm-tutorial/ic797051.png "SAML SSO")</span></span>

9. <span data-ttu-id="7bec6-171">W sekcji konfiguracji dostawcy tożsamości wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7bec6-171">In the Identity Provider Configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="7bec6-172">![Konfiguracja dostawcy tożsamości](./media/active-directory-saas-spring-cm-tutorial/ic797052.png "konfiguracji dostawcy tożsamości")</span><span class="sxs-lookup"><span data-stu-id="7bec6-172">![Identity Provider Configuration](./media/active-directory-saas-spring-cm-tutorial/ic797052.png "Identity Provider Configuration")</span></span>
    
    <span data-ttu-id="7bec6-173">a.</span><span class="sxs-lookup"><span data-stu-id="7bec6-173">a.</span></span> <span data-ttu-id="7bec6-174">Aby przekazać pobrany certyfikat usługi Azure Active Directory, kliknij przycisk **wybierz wystawcy certyfikatu** lub **zmiany wystawcy certyfikatu**.</span><span class="sxs-lookup"><span data-stu-id="7bec6-174">To upload your downloaded Azure Active Directory certificate, click **Select Issuer Certificate** or **Change Issuer Certificate**.</span></span>
    
    <span data-ttu-id="7bec6-175">b.</span><span class="sxs-lookup"><span data-stu-id="7bec6-175">b.</span></span> <span data-ttu-id="7bec6-176">Wklej **identyfikator jednostki SAML** wartość, która została skopiowana z portalu Azure do **wystawcy** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="7bec6-176">Paste **SAML Entity ID** value, which you have copied from Azure portal into the **Issuer** textbox.</span></span>
    
    <span data-ttu-id="7bec6-177">c.</span><span class="sxs-lookup"><span data-stu-id="7bec6-177">c.</span></span> <span data-ttu-id="7bec6-178">Wklej **SAML pojedynczy znak na adres URL usługi** wartość, która została skopiowana z portalu Azure do **punktu końcowego usługi dostawcy (SP) zainicjował** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="7bec6-178">Paste **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **Service Provider (SP) Initiated Endpoint** textbox.</span></span>
            
    <span data-ttu-id="7bec6-179">d.</span><span class="sxs-lookup"><span data-stu-id="7bec6-179">d.</span></span> <span data-ttu-id="7bec6-180">Wybierz **SAML włączone** jako **włączyć**.</span><span class="sxs-lookup"><span data-stu-id="7bec6-180">Select **SAML Enabled** as **Enable**.</span></span>

    <span data-ttu-id="7bec6-181">e.</span><span class="sxs-lookup"><span data-stu-id="7bec6-181">e.</span></span> <span data-ttu-id="7bec6-182">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="7bec6-182">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="7bec6-183">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="7bec6-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7bec6-184">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="7bec6-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7bec6-185">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7bec6-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7bec6-186">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7bec6-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="7bec6-187">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="7bec6-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="7bec6-189">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="7bec6-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7bec6-190">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="7bec6-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7bec6-192">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="7bec6-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7bec6-194">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7bec6-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7bec6-196">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7bec6-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7bec6-198">a.</span><span class="sxs-lookup"><span data-stu-id="7bec6-198">a.</span></span> <span data-ttu-id="7bec6-199">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7bec6-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7bec6-200">b.</span><span class="sxs-lookup"><span data-stu-id="7bec6-200">b.</span></span> <span data-ttu-id="7bec6-201">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7bec6-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7bec6-202">c.</span><span class="sxs-lookup"><span data-stu-id="7bec6-202">c.</span></span> <span data-ttu-id="7bec6-203">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="7bec6-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7bec6-204">d.</span><span class="sxs-lookup"><span data-stu-id="7bec6-204">d.</span></span> <span data-ttu-id="7bec6-205">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="7bec6-205">Click **Create**.</span></span>
 
### <a name="creating-a-springcm-test-user"></a><span data-ttu-id="7bec6-206">Tworzenie użytkownika testowego SpringCM</span><span class="sxs-lookup"><span data-stu-id="7bec6-206">Creating a SpringCM test user</span></span>

<span data-ttu-id="7bec6-207">Aby umożliwić użytkownikom usługi Azure Active Directory zalogować się do SpringCM, musi być przygotowana do SpringCM.</span><span class="sxs-lookup"><span data-stu-id="7bec6-207">To enable Azure Active Directory users to log in to SpringCM, they must be provisioned into SpringCM.</span></span> <span data-ttu-id="7bec6-208">W przypadku SpringCM Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="7bec6-208">In the case of SpringCM, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="7bec6-209">Aby uzyskać więcej informacji, zobacz [tworzenie i edytowanie użytkownika SpringCM](http://knowledge.springcm.com/create-and-edit-a-springcm-user).</span><span class="sxs-lookup"><span data-stu-id="7bec6-209">For more information, see [Create and Edit a SpringCM User](http://knowledge.springcm.com/create-and-edit-a-springcm-user).</span></span> 

<span data-ttu-id="7bec6-210">**Aby udostępnić konta użytkownika do SpringCM, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="7bec6-210">**To provision a user account to SpringCM, perform the following steps:**</span></span>

1. <span data-ttu-id="7bec6-211">Zaloguj się do Twojego **SpringCM** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="7bec6-211">Log in to your **SpringCM** company site as administrator.</span></span>

2. <span data-ttu-id="7bec6-212">Kliknij przycisk **GOTO**, a następnie kliknij przycisk **KSIĄŻKI ADRESOWEJ**.</span><span class="sxs-lookup"><span data-stu-id="7bec6-212">Click **GOTO**, and then click **ADDRESS BOOK**.</span></span>
   
    <span data-ttu-id="7bec6-213">![Utwórz użytkownika](./media/active-directory-saas-spring-cm-tutorial/ic797054.png "Tworzenie użytkownika")</span><span class="sxs-lookup"><span data-stu-id="7bec6-213">![Create User](./media/active-directory-saas-spring-cm-tutorial/ic797054.png "Create User")</span></span>

3. <span data-ttu-id="7bec6-214">Kliknij przycisk **Utwórz użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="7bec6-214">Click **Create User**.</span></span>

4. <span data-ttu-id="7bec6-215">Wybierz **roli użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="7bec6-215">Select a **User Role**.</span></span>

5. <span data-ttu-id="7bec6-216">Wybierz **wysyłania wiadomości E-mail o aktywacji**.</span><span class="sxs-lookup"><span data-stu-id="7bec6-216">Select **Send Activation Email**.</span></span>

6. <span data-ttu-id="7bec6-217">Wpisz imię, nazwisko i adres e-mail prawidłowe konto użytkownika usługi Azure Active Directory, które chcesz udostępnić do powiązanych pól tekstowych.</span><span class="sxs-lookup"><span data-stu-id="7bec6-217">Type the first name, last name, and email address of a valid Azure Active Directory user account you want to provision into the related textboxes.</span></span>

7. <span data-ttu-id="7bec6-218">Dodaj użytkownika do **grupy zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="7bec6-218">Add the user to a **Security group**.</span></span>

8. <span data-ttu-id="7bec6-219">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="7bec6-219">Click **Save**.</span></span>

  >[!NOTE]
  ><span data-ttu-id="7bec6-220">Możesz użyć innych SpringCM użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez SpringCM do kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="7bec6-220">You can use any other SpringCM user account creation tools or APIs provided by SpringCM to provision AAD user accounts.</span></span>  
  > 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7bec6-221">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7bec6-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7bec6-222">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu SpringCM.</span><span class="sxs-lookup"><span data-stu-id="7bec6-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SpringCM.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="7bec6-224">**Aby przypisać Simona Britta SpringCM, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="7bec6-224">**To assign Britta Simon to SpringCM, perform the following steps:**</span></span>

1. <span data-ttu-id="7bec6-225">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="7bec6-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="7bec6-227">Na liście aplikacji zaznacz **SpringCM**.</span><span class="sxs-lookup"><span data-stu-id="7bec6-227">In the applications list, select **SpringCM**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_app.png) 

3. <span data-ttu-id="7bec6-229">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="7bec6-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="7bec6-231">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="7bec6-231">Click **Add** button.</span></span> <span data-ttu-id="7bec6-232">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7bec6-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="7bec6-234">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="7bec6-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7bec6-235">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7bec6-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7bec6-236">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7bec6-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7bec6-237">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="7bec6-237">Testing single sign-on</span></span>

<span data-ttu-id="7bec6-238">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="7bec6-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
 
<span data-ttu-id="7bec6-239">Po kliknięciu kafelka SpringCM w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji SpringCM.</span><span class="sxs-lookup"><span data-stu-id="7bec6-239">When you click the SpringCM tile in the Access Panel, you should get automatically signed-on to your SpringCM application.</span></span>

<span data-ttu-id="7bec6-240">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7bec6-240">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7bec6-241">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="7bec6-241">Additional resources</span></span>

* [<span data-ttu-id="7bec6-242">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7bec6-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7bec6-243">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7bec6-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_203.png

