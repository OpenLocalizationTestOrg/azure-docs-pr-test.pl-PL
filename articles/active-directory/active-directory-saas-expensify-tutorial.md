---
title: 'Samouczek: Integracji Azure Active Directory z Expensify | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Expensify."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1e761484-7a2f-4321-91f4-6d5d0b69344e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: jeedes
ms.openlocfilehash: e45576fd92706881121469ccd82150b3d48059cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-expensify"></a><span data-ttu-id="314ad-103">Samouczek: Integracji Azure Active Directory z Expensify</span><span class="sxs-lookup"><span data-stu-id="314ad-103">Tutorial: Azure Active Directory integration with Expensify</span></span>

<span data-ttu-id="314ad-104">Z tego samouczka dowiesz się integrowanie Expensify z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="314ad-104">In this tutorial, you learn how to integrate Expensify with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="314ad-105">Integracja z usługą Azure AD Expensify zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="314ad-105">Integrating Expensify with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="314ad-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Expensify</span><span class="sxs-lookup"><span data-stu-id="314ad-106">You can control in Azure AD who has access to Expensify</span></span>
- <span data-ttu-id="314ad-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Expensify (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="314ad-107">You can enable your users to automatically get signed-on to Expensify (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="314ad-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="314ad-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="314ad-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="314ad-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="314ad-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="314ad-110">Prerequisites</span></span>

<span data-ttu-id="314ad-111">Aby skonfigurować integrację usługi Azure AD z Expensify, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="314ad-111">To configure Azure AD integration with Expensify, you need the following items:</span></span>

- <span data-ttu-id="314ad-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="314ad-112">An Azure AD subscription</span></span>
- <span data-ttu-id="314ad-113">Expensify jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="314ad-113">An Expensify single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="314ad-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="314ad-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="314ad-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="314ad-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="314ad-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="314ad-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="314ad-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="314ad-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="314ad-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="314ad-118">Scenario description</span></span>
<span data-ttu-id="314ad-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="314ad-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="314ad-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="314ad-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="314ad-121">Dodawanie Expensify z galerii</span><span class="sxs-lookup"><span data-stu-id="314ad-121">Adding Expensify from the gallery</span></span>
2. <span data-ttu-id="314ad-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="314ad-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-expensify-from-the-gallery"></a><span data-ttu-id="314ad-123">Dodawanie Expensify z galerii</span><span class="sxs-lookup"><span data-stu-id="314ad-123">Adding Expensify from the gallery</span></span>
<span data-ttu-id="314ad-124">Aby skonfigurować integrację usługi Azure AD Expensify, należy dodać Expensify z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="314ad-124">To configure the integration of Expensify into Azure AD, you need to add Expensify from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="314ad-125">**Aby dodać Expensify z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="314ad-125">**To add Expensify from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="314ad-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="314ad-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="314ad-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="314ad-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="314ad-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="314ad-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="314ad-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="314ad-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="314ad-133">W polu wyszukiwania wpisz **Expensify**.</span><span class="sxs-lookup"><span data-stu-id="314ad-133">In the search box, type **Expensify**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_search.png)

5. <span data-ttu-id="314ad-135">W panelu wyników wybierz **Expensify**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="314ad-135">In the results panel, select **Expensify**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="314ad-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="314ad-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="314ad-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Expensify w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="314ad-138">In this section, you configure and test Azure AD single sign-on with Expensify based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="314ad-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Expensify jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="314ad-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Expensify is to a user in Azure AD.</span></span> <span data-ttu-id="314ad-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Expensify musi się.</span><span class="sxs-lookup"><span data-stu-id="314ad-140">In other words, a link relationship between an Azure AD user and the related user in Expensify needs to be established.</span></span>

<span data-ttu-id="314ad-141">W Expensify, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="314ad-141">In Expensify, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="314ad-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Expensify, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="314ad-142">To configure and test Azure AD single sign-on with Expensify, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="314ad-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="314ad-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="314ad-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="314ad-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="314ad-145">**[Tworzenie użytkownika testowego Expensify](#creating-an-expensify-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Expensify połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="314ad-145">**[Creating an Expensify test user](#creating-an-expensify-test-user)** - to have a counterpart of Britta Simon in Expensify that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="314ad-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="314ad-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="314ad-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="314ad-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="314ad-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="314ad-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="314ad-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Expensify.</span><span class="sxs-lookup"><span data-stu-id="314ad-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Expensify application.</span></span>

<span data-ttu-id="314ad-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Expensify, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="314ad-150">**To configure Azure AD single sign-on with Expensify, perform the following steps:**</span></span>

1. <span data-ttu-id="314ad-151">W portalu Azure na **Expensify** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="314ad-151">In the Azure portal, on the **Expensify** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="314ad-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="314ad-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_samlbase.png)

3. <span data-ttu-id="314ad-155">Na **Expensify domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="314ad-155">On the **Expensify Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_url.png)

    <span data-ttu-id="314ad-157">a.</span><span class="sxs-lookup"><span data-stu-id="314ad-157">a.</span></span> <span data-ttu-id="314ad-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://www.expensify.com/authentication/saml/login`</span><span class="sxs-lookup"><span data-stu-id="314ad-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.expensify.com/authentication/saml/login`</span></span>

    <span data-ttu-id="314ad-159">b.</span><span class="sxs-lookup"><span data-stu-id="314ad-159">b.</span></span> <span data-ttu-id="314ad-160">W **adres URL identyfikatora** tekstowym, wpisz adres URL, używając następującego wzorca:`https://www.<companyname>.expensify.com/`</span><span class="sxs-lookup"><span data-stu-id="314ad-160">In the **Identifier URL** textbox, type a URL using the following pattern: `https://www.<companyname>.expensify.com/`</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="314ad-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="314ad-161">These values are not real.</span></span> <span data-ttu-id="314ad-162">Rzeczywisty adres URL logowania i adres URL identyfikatora, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="314ad-162">Update these values with the actual Sign-On URL and Identifier URL.</span></span> <span data-ttu-id="314ad-163">Skontaktuj się z [zespołem pomocy technicznej klienta Expensify](mailto:help@expensify.com) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="314ad-163">Contact [Expensify Client support team](mailto:help@expensify.com) to get these values.</span></span> 
 
4. <span data-ttu-id="314ad-164">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="314ad-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_certificate.png) 

5. <span data-ttu-id="314ad-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="314ad-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-expensify-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="314ad-168">Aby włączyć logowanie Jednokrotne w Expensify, należy najpierw włączyć **kontroli domeny** w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="314ad-168">To enable SSO in Expensify, you first need to enable **Domain Control** in the application.</span></span> <span data-ttu-id="314ad-169">Formant domeny można włączyć w aplikacji za pomocą kroków opisanych [tutaj](http://help.expensify.com/domain-control).</span><span class="sxs-lookup"><span data-stu-id="314ad-169">You can enable Domain Control in the application through the steps listed [here](http://help.expensify.com/domain-control).</span></span> <span data-ttu-id="314ad-170">Aby uzyskać dodatkową pomoc, Praca z [zespołem pomocy technicznej klienta Expensify](mailto:help@expensify.com).</span><span class="sxs-lookup"><span data-stu-id="314ad-170">For additional support, work with [Expensify Client support team](mailto:help@expensify.com).</span></span> <span data-ttu-id="314ad-171">Po utworzeniu włączona funkcja Kontrola domeny, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="314ad-171">Once you have Domain Control enabled, follow these steps:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_51.png)
    
    <span data-ttu-id="314ad-173">a.</span><span class="sxs-lookup"><span data-stu-id="314ad-173">a.</span></span> <span data-ttu-id="314ad-174">Zaloguj się do aplikacji Expensify.</span><span class="sxs-lookup"><span data-stu-id="314ad-174">Sign on to your Expensify application.</span></span>
    
    <span data-ttu-id="314ad-175">b.</span><span class="sxs-lookup"><span data-stu-id="314ad-175">b.</span></span> <span data-ttu-id="314ad-176">Na pasku narzędzi u góry kliknij **Admin**.</span><span class="sxs-lookup"><span data-stu-id="314ad-176">In the toolbar on the top, click **Admin**.</span></span>
    
    <span data-ttu-id="314ad-177">c.</span><span class="sxs-lookup"><span data-stu-id="314ad-177">c.</span></span> <span data-ttu-id="314ad-178">W lewym panelu kliknij **domeny**.</span><span class="sxs-lookup"><span data-stu-id="314ad-178">In the left panel, click **Domain**.</span></span>
    
    <span data-ttu-id="314ad-179">d.</span><span class="sxs-lookup"><span data-stu-id="314ad-179">d.</span></span> <span data-ttu-id="314ad-180">Kliknij nazwę zweryfikowanej domeny.</span><span class="sxs-lookup"><span data-stu-id="314ad-180">Click your verified domain name.</span></span>
    
    <span data-ttu-id="314ad-181">e.</span><span class="sxs-lookup"><span data-stu-id="314ad-181">e.</span></span> <span data-ttu-id="314ad-182">W lewym panelu kliknij **SAML**, a następnie wybierz **włączone**.</span><span class="sxs-lookup"><span data-stu-id="314ad-182">In the left panel, click **SAML**, and then select **Enabled**.</span></span>
    
    <span data-ttu-id="314ad-183">f.</span><span class="sxs-lookup"><span data-stu-id="314ad-183">f.</span></span> <span data-ttu-id="314ad-184">Otwórz pobrany metadanych federacji z usługi Azure AD w programie Notatnik, skopiuj zawartość, a następnie wklej go do **metadanych dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="314ad-184">Open the downloaded Federation Metadata from Azure AD in notepad, copy the content, and then paste it into the **Identity Provider Metadata** textbox.</span></span>

> [!TIP]
> <span data-ttu-id="314ad-185">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="314ad-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="314ad-186">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="314ad-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="314ad-187">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="314ad-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="314ad-188">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="314ad-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="314ad-189">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="314ad-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="314ad-191">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="314ad-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="314ad-192">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="314ad-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-expensify-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="314ad-194">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="314ad-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-expensify-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="314ad-196">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="314ad-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-expensify-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="314ad-198">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="314ad-198">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-expensify-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="314ad-200">a.</span><span class="sxs-lookup"><span data-stu-id="314ad-200">a.</span></span> <span data-ttu-id="314ad-201">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="314ad-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="314ad-202">b.</span><span class="sxs-lookup"><span data-stu-id="314ad-202">b.</span></span> <span data-ttu-id="314ad-203">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="314ad-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="314ad-204">c.</span><span class="sxs-lookup"><span data-stu-id="314ad-204">c.</span></span> <span data-ttu-id="314ad-205">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="314ad-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="314ad-206">d.</span><span class="sxs-lookup"><span data-stu-id="314ad-206">d.</span></span> <span data-ttu-id="314ad-207">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="314ad-207">Click **Create**.</span></span>
 
### <a name="creating-an-expensify-test-user"></a><span data-ttu-id="314ad-208">Tworzenie użytkownika testowego Expensify</span><span class="sxs-lookup"><span data-stu-id="314ad-208">Creating an Expensify test user</span></span>

<span data-ttu-id="314ad-209">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Expensify.</span><span class="sxs-lookup"><span data-stu-id="314ad-209">In this section, you create a user called Britta Simon in Expensify.</span></span> <span data-ttu-id="314ad-210">Praca z [zespołem pomocy technicznej klienta Expensify](mailto:help@expensify.com) Aby dodać użytkowników do platformy Expensify.</span><span class="sxs-lookup"><span data-stu-id="314ad-210">Work with [Expensify Client support team](mailto:help@expensify.com) to add the users in the Expensify platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="314ad-211">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="314ad-211">Assigning the Azure AD test user</span></span>

<span data-ttu-id="314ad-212">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Expensify.</span><span class="sxs-lookup"><span data-stu-id="314ad-212">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Expensify.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="314ad-214">**Aby przypisać Simona Britta Expensify, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="314ad-214">**To assign Britta Simon to Expensify, perform the following steps:**</span></span>

1. <span data-ttu-id="314ad-215">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="314ad-215">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="314ad-217">Na liście aplikacji zaznacz **Expensify**.</span><span class="sxs-lookup"><span data-stu-id="314ad-217">In the applications list, select **Expensify**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_app.png) 

3. <span data-ttu-id="314ad-219">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="314ad-219">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="314ad-221">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="314ad-221">Click **Add** button.</span></span> <span data-ttu-id="314ad-222">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="314ad-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="314ad-224">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="314ad-224">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="314ad-225">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="314ad-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="314ad-226">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="314ad-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="314ad-227">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="314ad-227">Testing single sign-on</span></span>

<span data-ttu-id="314ad-228">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="314ad-228">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>  

<span data-ttu-id="314ad-229">Po kliknięciu kafelka Expensify w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Expensify.</span><span class="sxs-lookup"><span data-stu-id="314ad-229">When you click the Expensify tile in the Access Panel, you should get automatically signed-on to your Expensify application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="314ad-230">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="314ad-230">Additional resources</span></span>

* [<span data-ttu-id="314ad-231">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="314ad-231">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="314ad-232">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="314ad-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_203.png

