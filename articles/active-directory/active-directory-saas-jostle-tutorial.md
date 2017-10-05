---
title: 'Samouczek: Integracji Azure Active Directory z Jostle | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Jostle."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9ca4ca1f-8f68-4225-81a6-1666b486d6a8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 0ca8aca1446a38643ce9f6751b6fe9cae1eaa5b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jostle"></a><span data-ttu-id="e7ba3-103">Samouczek: Integracji Azure Active Directory z Jostle</span><span class="sxs-lookup"><span data-stu-id="e7ba3-103">Tutorial: Azure Active Directory integration with Jostle</span></span>

<span data-ttu-id="e7ba3-104">Z tego samouczka dowiesz się integrowanie Jostle z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e7ba3-104">In this tutorial, you learn how to integrate Jostle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e7ba3-105">Integracja z usługą Azure AD Jostle zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="e7ba3-105">Integrating Jostle with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e7ba3-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Jostle</span><span class="sxs-lookup"><span data-stu-id="e7ba3-106">You can control in Azure AD who has access to Jostle</span></span>
- <span data-ttu-id="e7ba3-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Jostle (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7ba3-107">You can enable your users to automatically get signed-on to Jostle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e7ba3-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="e7ba3-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e7ba3-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e7ba3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e7ba3-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e7ba3-110">Prerequisites</span></span>

<span data-ttu-id="e7ba3-111">Aby skonfigurować integrację usługi Azure AD z Jostle, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="e7ba3-111">To configure Azure AD integration with Jostle, you need the following items:</span></span>

- <span data-ttu-id="e7ba3-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7ba3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e7ba3-113">Jostle jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="e7ba3-113">A Jostle single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e7ba3-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e7ba3-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="e7ba3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e7ba3-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e7ba3-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e7ba3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e7ba3-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="e7ba3-118">Scenario description</span></span>
<span data-ttu-id="e7ba3-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e7ba3-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="e7ba3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e7ba3-121">Dodawanie Jostle z galerii</span><span class="sxs-lookup"><span data-stu-id="e7ba3-121">Adding Jostle from the gallery</span></span>
2. <span data-ttu-id="e7ba3-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="e7ba3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jostle-from-the-gallery"></a><span data-ttu-id="e7ba3-123">Dodawanie Jostle z galerii</span><span class="sxs-lookup"><span data-stu-id="e7ba3-123">Adding Jostle from the gallery</span></span>
<span data-ttu-id="e7ba3-124">Aby skonfigurować integrację usługi Azure AD Jostle, należy dodać Jostle z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-124">To configure the integration of Jostle into Azure AD, you need to add Jostle from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e7ba3-125">**Aby dodać Jostle z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="e7ba3-125">**To add Jostle from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e7ba3-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="e7ba3-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e7ba3-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="e7ba3-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="e7ba3-133">W polu wyszukiwania wpisz **Jostle**.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-133">In the search box, type **Jostle**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jostle-tutorial/tutorial_jostle_search.png)

5. <span data-ttu-id="e7ba3-135">W panelu wyników wybierz **Jostle**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-135">In the results panel, select **Jostle**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jostle-tutorial/tutorial_jostle_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e7ba3-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="e7ba3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e7ba3-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Jostle na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="e7ba3-138">In this section, you configure and test Azure AD single sign-on with Jostle based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e7ba3-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Jostle jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Jostle is to a user in Azure AD.</span></span> <span data-ttu-id="e7ba3-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Jostle musi się.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-140">In other words, a link relationship between an Azure AD user and the related user in Jostle needs to be established.</span></span>

<span data-ttu-id="e7ba3-141">W Jostle, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-141">In Jostle, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e7ba3-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Jostle, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="e7ba3-142">To configure and test Azure AD single sign-on with Jostle, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e7ba3-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e7ba3-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e7ba3-145">**[Tworzenie użytkownika testowego Jostle](#creating-a-jostle-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Jostle połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-145">**[Creating a Jostle test user](#creating-a-jostle-test-user)** - to have a counterpart of Britta Simon in Jostle that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e7ba3-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e7ba3-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e7ba3-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e7ba3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e7ba3-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Jostle.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Jostle application.</span></span>

<span data-ttu-id="e7ba3-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Jostle, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="e7ba3-150">**To configure Azure AD single sign-on with Jostle, perform the following steps:**</span></span>

1. <span data-ttu-id="e7ba3-151">W portalu Azure na **Jostle** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-151">In the Azure portal, on the **Jostle** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="e7ba3-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jostle-tutorial/tutorial_jostle_samlbase.png)

3. <span data-ttu-id="e7ba3-155">Na **Jostle domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="e7ba3-155">On the **Jostle Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jostle-tutorial/tutorial_jostle_url.png)

    <span data-ttu-id="e7ba3-157">a.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-157">a.</span></span> <span data-ttu-id="e7ba3-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<tanent name>.jostle.us/jostle-prod/`</span><span class="sxs-lookup"><span data-stu-id="e7ba3-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tanent name>.jostle.us/jostle-prod/`</span></span>

    <span data-ttu-id="e7ba3-159">b.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-159">b.</span></span> <span data-ttu-id="e7ba3-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<tanent name>.jostle.us`</span><span class="sxs-lookup"><span data-stu-id="e7ba3-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<tanent name>.jostle.us`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e7ba3-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-161">These values are not real.</span></span> <span data-ttu-id="e7ba3-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e7ba3-163">Skontaktuj się z [zespołem pomocy technicznej Jostle](mailto:support@jostle.me) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-163">Contact [Jostle support team](mailto:support@jostle.me) to get these values.</span></span> 
 


4. <span data-ttu-id="e7ba3-164">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jostle-tutorial/tutorial_jostle_certificate.png) 

5. <span data-ttu-id="e7ba3-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jostle-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="e7ba3-168">Aby skonfigurować rejestrację jednokrotną Jostle strony, musisz wysłać XML metadanych pobranych do [zespołem pomocy technicznej Jostle](mailto:support@jostle.me).</span><span class="sxs-lookup"><span data-stu-id="e7ba3-168">To configure single sign-on on Jostle side, you need to send the downloaded metadata XML to [Jostle support team](mailto:support@jostle.me).</span></span> <span data-ttu-id="e7ba3-169">To ustawienie, aby były prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one wartość.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span> 

> [!TIP]
> <span data-ttu-id="e7ba3-170">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="e7ba3-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e7ba3-171">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e7ba3-172">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e7ba3-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e7ba3-173">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7ba3-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="e7ba3-174">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="e7ba3-176">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="e7ba3-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e7ba3-177">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jostle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e7ba3-179">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jostle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e7ba3-181">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jostle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e7ba3-183">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="e7ba3-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jostle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e7ba3-185">a.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-185">a.</span></span> <span data-ttu-id="e7ba3-186">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e7ba3-187">b.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-187">b.</span></span> <span data-ttu-id="e7ba3-188">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e7ba3-189">c.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-189">c.</span></span> <span data-ttu-id="e7ba3-190">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e7ba3-191">d.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-191">d.</span></span> <span data-ttu-id="e7ba3-192">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-192">Click **Create**.</span></span>
 
### <a name="creating-a-jostle-test-user"></a><span data-ttu-id="e7ba3-193">Tworzenie użytkownika testowego Jostle</span><span class="sxs-lookup"><span data-stu-id="e7ba3-193">Creating a Jostle test user</span></span>

<span data-ttu-id="e7ba3-194">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Jostle.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-194">In this section, you create a user called Britta Simon in Jostle.</span></span> <span data-ttu-id="e7ba3-195">Jeśli nie wiadomo, jak dodać Simona Britta w Jostle, skontaktuj się z [zespołem pomocy technicznej Jostle](mailto:support@jostle.me) Aby dodać użytkownika testowego i włączenia funkcji logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-195">If you don't know how to add Britta Simon in Jostle, please contact with [Jostle support team](mailto:support@jostle.me) to add the test user and enable SSO.</span></span>

> [!NOTE]
> <span data-ttu-id="e7ba3-196">Właściciel konta usługi Azure Active Directory otrzymuje wiadomość e-mail i następuje łącze, aby potwierdzić swoje konto, zanim staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-196">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e7ba3-197">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7ba3-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e7ba3-198">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Jostle.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Jostle.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="e7ba3-200">**Aby przypisać Simona Britta Jostle, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="e7ba3-200">**To assign Britta Simon to Jostle, perform the following steps:**</span></span>

1. <span data-ttu-id="e7ba3-201">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="e7ba3-203">Na liście aplikacji zaznacz **Jostle**.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-203">In the applications list, select **Jostle**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jostle-tutorial/tutorial_jostle_app.png) 

3. <span data-ttu-id="e7ba3-205">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="e7ba3-207">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-207">Click **Add** button.</span></span> <span data-ttu-id="e7ba3-208">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="e7ba3-210">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e7ba3-211">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e7ba3-212">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e7ba3-213">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e7ba3-213">Testing single sign-on</span></span>

<span data-ttu-id="e7ba3-214">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e7ba3-215">Po kliknięciu kafelka Jostle w panelu dostępu, należy uzyskać automatycznie strony logowania Jostle aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e7ba3-215">When you click the Jostle tile in the Access Panel, you should get automatically login page of Jostle application.</span></span>
<span data-ttu-id="e7ba3-216">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e7ba3-216">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e7ba3-217">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="e7ba3-217">Additional resources</span></span>

* [<span data-ttu-id="e7ba3-218">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e7ba3-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e7ba3-219">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e7ba3-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_203.png

