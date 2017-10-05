---
title: 'Samouczek: Integracji Azure Active Directory z Oneteam | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Oneteam."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2e94916c-64ae-4e1a-a8b5-bc6ef7d28c29
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: c4381ca3166bd75bda1179b9a67b2224ba58ae68
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-oneteam"></a><span data-ttu-id="5cba9-103">Samouczek: Integracji Azure Active Directory z Oneteam</span><span class="sxs-lookup"><span data-stu-id="5cba9-103">Tutorial: Azure Active Directory integration with Oneteam</span></span>

<span data-ttu-id="5cba9-104">Z tego samouczka dowiesz się integrowanie Oneteam z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5cba9-104">In this tutorial, you learn how to integrate Oneteam with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5cba9-105">Integracja z usługą Azure AD Oneteam zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="5cba9-105">Integrating Oneteam with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5cba9-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Oneteam</span><span class="sxs-lookup"><span data-stu-id="5cba9-106">You can control in Azure AD who has access to Oneteam</span></span>
- <span data-ttu-id="5cba9-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Oneteam (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5cba9-107">You can enable your users to automatically get signed-on to Oneteam (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5cba9-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="5cba9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5cba9-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5cba9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5cba9-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5cba9-110">Prerequisites</span></span>

<span data-ttu-id="5cba9-111">Aby skonfigurować integrację usługi Azure AD z Oneteam, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="5cba9-111">To configure Azure AD integration with Oneteam, you need the following items:</span></span>

- <span data-ttu-id="5cba9-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5cba9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5cba9-113">Oneteam logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="5cba9-113">A Oneteam single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5cba9-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="5cba9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5cba9-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="5cba9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5cba9-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="5cba9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5cba9-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5cba9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5cba9-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="5cba9-118">Scenario description</span></span>
<span data-ttu-id="5cba9-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="5cba9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5cba9-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="5cba9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5cba9-121">Dodawanie Oneteam z galerii</span><span class="sxs-lookup"><span data-stu-id="5cba9-121">Adding Oneteam from the gallery</span></span>
2. <span data-ttu-id="5cba9-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="5cba9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-oneteam-from-the-gallery"></a><span data-ttu-id="5cba9-123">Dodawanie Oneteam z galerii</span><span class="sxs-lookup"><span data-stu-id="5cba9-123">Adding Oneteam from the gallery</span></span>
<span data-ttu-id="5cba9-124">Aby skonfigurować integrację usługi Azure AD Oneteam, należy dodać Oneteam z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="5cba9-124">To configure the integration of Oneteam into Azure AD, you need to add Oneteam from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5cba9-125">**Aby dodać Oneteam z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5cba9-125">**To add Oneteam from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5cba9-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="5cba9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="5cba9-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="5cba9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5cba9-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="5cba9-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="5cba9-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5cba9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="5cba9-133">W polu wyszukiwania wpisz **Oneteam**.</span><span class="sxs-lookup"><span data-stu-id="5cba9-133">In the search box, type **Oneteam**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_search.png)

5. <span data-ttu-id="5cba9-135">W panelu wyników wybierz **Oneteam**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="5cba9-135">In the results panel, select **Oneteam**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5cba9-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="5cba9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5cba9-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Oneteam w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="5cba9-138">In this section, you configure and test Azure AD single sign-on with Oneteam based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5cba9-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Oneteam jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5cba9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Oneteam is to a user in Azure AD.</span></span> <span data-ttu-id="5cba9-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Oneteam musi się.</span><span class="sxs-lookup"><span data-stu-id="5cba9-140">In other words, a link relationship between an Azure AD user and the related user in Oneteam needs to be established.</span></span>

<span data-ttu-id="5cba9-141">W Oneteam, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="5cba9-141">In Oneteam, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5cba9-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Oneteam, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="5cba9-142">To configure and test Azure AD single sign-on with Oneteam, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5cba9-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="5cba9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5cba9-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="5cba9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5cba9-145">**[Tworzenie użytkownika testowego Oneteam](#creating-a-oneteam-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Oneteam połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5cba9-145">**[Creating a Oneteam test user](#creating-a-oneteam-test-user)** - to have a counterpart of Britta Simon in Oneteam that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5cba9-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="5cba9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5cba9-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="5cba9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5cba9-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5cba9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5cba9-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Oneteam.</span><span class="sxs-lookup"><span data-stu-id="5cba9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Oneteam application.</span></span>

<span data-ttu-id="5cba9-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Oneteam, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5cba9-150">**To configure Azure AD single sign-on with Oneteam, perform the following steps:**</span></span>

1. <span data-ttu-id="5cba9-151">W portalu Azure na **Oneteam** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="5cba9-151">In the Azure portal, on the **Oneteam** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="5cba9-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="5cba9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_samlbase.png)

3. <span data-ttu-id="5cba9-155">Na **Oneteam domeny i adres URL** sekcji, jeśli chcesz skonfigurować aplikację w **IDP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="5cba9-155">On the **Oneteam Domain and URLs** section, if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_url.png)

    <span data-ttu-id="5cba9-157">a.</span><span class="sxs-lookup"><span data-stu-id="5cba9-157">a.</span></span> <span data-ttu-id="5cba9-158">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://api.one-team.io/teams/<team name>`</span><span class="sxs-lookup"><span data-stu-id="5cba9-158">In the **Identifier** textbox, type a URL using the following pattern: `https://api.one-team.io/teams/<team name>`</span></span>

    <span data-ttu-id="5cba9-159">b.</span><span class="sxs-lookup"><span data-stu-id="5cba9-159">b.</span></span> <span data-ttu-id="5cba9-160">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://api.one-team.io/teams/<team name>/auth/saml/callback`</span><span class="sxs-lookup"><span data-stu-id="5cba9-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://api.one-team.io/teams/<team name>/auth/saml/callback`</span></span>

4. <span data-ttu-id="5cba9-161">Sprawdź **Pokaż zaawansowane ustawienia adresu URL**, jeśli chcesz skonfigurować aplikację w **SP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="5cba9-161">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_url1.png)

    <span data-ttu-id="5cba9-163">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<team name>.one-team.io/`</span><span class="sxs-lookup"><span data-stu-id="5cba9-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<team name>.one-team.io/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="5cba9-164">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="5cba9-164">These values are not real.</span></span> <span data-ttu-id="5cba9-165">Rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="5cba9-165">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="5cba9-166">Skontaktuj się z [zespołem pomocy technicznej klienta Oneteam](https://support.one-team.com/hc/requests/new) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="5cba9-166">Contact [Oneteam Client support team](https://support.one-team.com/hc/requests/new) to get these values.</span></span> 



5. <span data-ttu-id="5cba9-167">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="5cba9-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_certificate.png) 

6. <span data-ttu-id="5cba9-169">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5cba9-169">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-oneteam-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="5cba9-171">Uzyskanie logowania jednokrotnego skonfigurowane dla aplikacji, można zwiększyć biletu pomocy technicznej z [zespołem pomocy technicznej Oneteam](https://support.one-team.com/hc/requests/new) i podaj pobrany **metadanych**.</span><span class="sxs-lookup"><span data-stu-id="5cba9-171">To get SSO configured for your application, you can raise the support ticket with [Oneteam support team](https://support.one-team.com/hc/requests/new) and provide them the downloaded **Metadata**.</span></span> 

> [!TIP]
> <span data-ttu-id="5cba9-172">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="5cba9-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5cba9-173">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="5cba9-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5cba9-174">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5cba9-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5cba9-175">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5cba9-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="5cba9-176">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="5cba9-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="5cba9-178">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5cba9-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5cba9-179">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="5cba9-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-oneteam-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5cba9-181">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="5cba9-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-oneteam-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5cba9-183">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5cba9-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-oneteam-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5cba9-185">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5cba9-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-oneteam-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5cba9-187">a.</span><span class="sxs-lookup"><span data-stu-id="5cba9-187">a.</span></span> <span data-ttu-id="5cba9-188">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5cba9-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5cba9-189">b.</span><span class="sxs-lookup"><span data-stu-id="5cba9-189">b.</span></span> <span data-ttu-id="5cba9-190">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5cba9-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5cba9-191">c.</span><span class="sxs-lookup"><span data-stu-id="5cba9-191">c.</span></span> <span data-ttu-id="5cba9-192">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="5cba9-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5cba9-193">d.</span><span class="sxs-lookup"><span data-stu-id="5cba9-193">d.</span></span> <span data-ttu-id="5cba9-194">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="5cba9-194">Click **Create**.</span></span>
 
### <a name="creating-a-oneteam-test-user"></a><span data-ttu-id="5cba9-195">Tworzenie użytkownika testowego Oneteam</span><span class="sxs-lookup"><span data-stu-id="5cba9-195">Creating a Oneteam test user</span></span>

<span data-ttu-id="5cba9-196">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w Oneteam.</span><span class="sxs-lookup"><span data-stu-id="5cba9-196">The objective of this section is to create a user called Britta Simon in Oneteam.</span></span> <span data-ttu-id="5cba9-197">Oneteam obsługę w czasie, który jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="5cba9-197">Oneteam supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="5cba9-198">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="5cba9-198">There is no action item for you in this section.</span></span> <span data-ttu-id="5cba9-199">Nowy użytkownik zostanie utworzony podczas próby dostępu Oneteam, jeśli go jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="5cba9-199">A new user will be created during an attempt to access Oneteam, if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="5cba9-200">Jeśli musisz ręcznie utworzyć użytkownika może wiązać się biletu pomocy technicznej z [zespołem pomocy technicznej Oneteam](https://support.one-team.com/hc/requests/new).</span><span class="sxs-lookup"><span data-stu-id="5cba9-200">If you need to create an user manually, you can raise the support ticket with [Oneteam support team](https://support.one-team.com/hc/requests/new).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5cba9-201">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5cba9-201">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5cba9-202">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Oneteam.</span><span class="sxs-lookup"><span data-stu-id="5cba9-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Oneteam.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="5cba9-204">**Aby przypisać Simona Britta Oneteam, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5cba9-204">**To assign Britta Simon to Oneteam, perform the following steps:**</span></span>

1. <span data-ttu-id="5cba9-205">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="5cba9-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="5cba9-207">Na liście aplikacji zaznacz **Oneteam**.</span><span class="sxs-lookup"><span data-stu-id="5cba9-207">In the applications list, select **Oneteam**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_app.png) 

3. <span data-ttu-id="5cba9-209">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="5cba9-209">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="5cba9-211">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5cba9-211">Click **Add** button.</span></span> <span data-ttu-id="5cba9-212">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5cba9-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="5cba9-214">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="5cba9-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5cba9-215">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5cba9-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5cba9-216">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5cba9-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5cba9-217">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5cba9-217">Testing single sign-on</span></span>

<span data-ttu-id="5cba9-218">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="5cba9-218">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5cba9-219">Po kliknięciu kafelka Oneteam w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Oneteam.</span><span class="sxs-lookup"><span data-stu-id="5cba9-219">When you click the Oneteam tile in the Access Panel, you should get automatically signed-on to your Oneteam application.</span></span>
<span data-ttu-id="5cba9-220">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5cba9-220">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5cba9-221">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="5cba9-221">Additional resources</span></span>

* [<span data-ttu-id="5cba9-222">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5cba9-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5cba9-223">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5cba9-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_203.png

