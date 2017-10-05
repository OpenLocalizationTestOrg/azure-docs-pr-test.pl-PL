---
title: 'Samouczek: Integracji Azure Active Directory z Sciforma | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Sciforma."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: abbfb5ac-7687-4153-b263-8090102dae37
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: jeedes
ms.openlocfilehash: 4a04f5b2b5ccb33dddefc063a89118d87a11ebf5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sciforma"></a><span data-ttu-id="c2e84-103">Samouczek: Integracji Azure Active Directory z Sciforma</span><span class="sxs-lookup"><span data-stu-id="c2e84-103">Tutorial: Azure Active Directory integration with Sciforma</span></span>

<span data-ttu-id="c2e84-104">Z tego samouczka dowiesz się integrowanie Sciforma z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c2e84-104">In this tutorial, you learn how to integrate Sciforma with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c2e84-105">Integracja z usługą Azure AD Sciforma zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="c2e84-105">Integrating Sciforma with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c2e84-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Sciforma</span><span class="sxs-lookup"><span data-stu-id="c2e84-106">You can control in Azure AD who has access to Sciforma</span></span>
- <span data-ttu-id="c2e84-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Sciforma (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c2e84-107">You can enable your users to automatically get signed-on to Sciforma (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c2e84-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c2e84-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c2e84-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c2e84-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c2e84-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c2e84-110">Prerequisites</span></span>

<span data-ttu-id="c2e84-111">Aby skonfigurować integrację usługi Azure AD z Sciforma, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="c2e84-111">To configure Azure AD integration with Sciforma, you need the following items:</span></span>

- <span data-ttu-id="c2e84-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c2e84-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c2e84-113">Sciforma jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="c2e84-113">A Sciforma single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c2e84-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="c2e84-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c2e84-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="c2e84-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c2e84-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="c2e84-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c2e84-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c2e84-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c2e84-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="c2e84-118">Scenario description</span></span>
<span data-ttu-id="c2e84-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="c2e84-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c2e84-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="c2e84-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c2e84-121">Dodawanie Sciforma z galerii</span><span class="sxs-lookup"><span data-stu-id="c2e84-121">Adding Sciforma from the gallery</span></span>
2. <span data-ttu-id="c2e84-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="c2e84-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sciforma-from-the-gallery"></a><span data-ttu-id="c2e84-123">Dodawanie Sciforma z galerii</span><span class="sxs-lookup"><span data-stu-id="c2e84-123">Adding Sciforma from the gallery</span></span>
<span data-ttu-id="c2e84-124">Aby skonfigurować integrację usługi Azure AD Sciforma, należy dodać Sciforma z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="c2e84-124">To configure the integration of Sciforma into Azure AD, you need to add Sciforma from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c2e84-125">**Aby dodać Sciforma z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c2e84-125">**To add Sciforma from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c2e84-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="c2e84-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="c2e84-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="c2e84-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c2e84-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="c2e84-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="c2e84-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c2e84-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="c2e84-133">W polu wyszukiwania wpisz **Sciforma**.</span><span class="sxs-lookup"><span data-stu-id="c2e84-133">In the search box, type **Sciforma**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sciforma-tutorial/tutorial_sciforma_search.png)

5. <span data-ttu-id="c2e84-135">W panelu wyników wybierz **Sciforma**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="c2e84-135">In the results panel, select **Sciforma**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sciforma-tutorial/tutorial_sciforma_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c2e84-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="c2e84-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c2e84-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Sciforma na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="c2e84-138">In this section, you configure and test Azure AD single sign-on with Sciforma based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c2e84-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Sciforma jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c2e84-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Sciforma is to a user in Azure AD.</span></span> <span data-ttu-id="c2e84-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Sciforma musi się.</span><span class="sxs-lookup"><span data-stu-id="c2e84-140">In other words, a link relationship between an Azure AD user and the related user in Sciforma needs to be established.</span></span>

<span data-ttu-id="c2e84-141">W Sciforma, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="c2e84-141">In Sciforma, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c2e84-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Sciforma, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="c2e84-142">To configure and test Azure AD single sign-on with Sciforma, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c2e84-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="c2e84-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c2e84-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="c2e84-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c2e84-145">**[Tworzenie użytkownika testowego Sciforma](#creating-a-sciforma-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Sciforma połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c2e84-145">**[Creating a Sciforma test user](#creating-a-sciforma-test-user)** - to have a counterpart of Britta Simon in Sciforma that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c2e84-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="c2e84-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c2e84-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="c2e84-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c2e84-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="c2e84-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c2e84-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Sciforma.</span><span class="sxs-lookup"><span data-stu-id="c2e84-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Sciforma application.</span></span>

<span data-ttu-id="c2e84-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Sciforma, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c2e84-150">**To configure Azure AD single sign-on with Sciforma, perform the following steps:**</span></span>

1. <span data-ttu-id="c2e84-151">W portalu Azure na **Sciforma** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="c2e84-151">In the Azure portal, on the **Sciforma** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="c2e84-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="c2e84-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sciforma-tutorial/tutorial_sciforma_samlbase.png)

3. <span data-ttu-id="c2e84-155">Na **Sciforma domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c2e84-155">On the **Sciforma Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sciforma-tutorial/tutorial_sciforma_url.png)

    <span data-ttu-id="c2e84-157">a.</span><span class="sxs-lookup"><span data-stu-id="c2e84-157">a.</span></span> <span data-ttu-id="c2e84-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.sciforma.net/sciforma/main.html`</span><span class="sxs-lookup"><span data-stu-id="c2e84-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.sciforma.net/sciforma/main.html`</span></span>

    <span data-ttu-id="c2e84-159">b.</span><span class="sxs-lookup"><span data-stu-id="c2e84-159">b.</span></span> <span data-ttu-id="c2e84-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.sciforma.net/sciforma/saml`</span><span class="sxs-lookup"><span data-stu-id="c2e84-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.sciforma.net/sciforma/saml`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c2e84-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="c2e84-161">These values are not real.</span></span> <span data-ttu-id="c2e84-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="c2e84-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c2e84-163">Skontaktuj się z [zespołem pomocy technicznej klienta Sciforma](http://www.sciforma.com/company/contact_us) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="c2e84-163">Contact [Sciforma Client support team](http://www.sciforma.com/company/contact_us) to get these values.</span></span> 
 


4. <span data-ttu-id="c2e84-164">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="c2e84-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sciforma-tutorial/tutorial_sciforma_certificate.png) 

5. <span data-ttu-id="c2e84-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c2e84-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sciforma-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c2e84-168">Skonfigurować logowanie jednokrotne w **Sciforma** stronie, musisz wysłać pobrany **XML metadanych** do [zespołem pomocy technicznej Sciforma](http://www.sciforma.com/company/contact_us).</span><span class="sxs-lookup"><span data-stu-id="c2e84-168">To configure single sign-on on **Sciforma** side, you need to send the downloaded **Metadata XML** to [Sciforma support team](http://www.sciforma.com/company/contact_us).</span></span>

> [!TIP]
> <span data-ttu-id="c2e84-169">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="c2e84-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c2e84-170">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="c2e84-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c2e84-171">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c2e84-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c2e84-172">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c2e84-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="c2e84-173">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="c2e84-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="c2e84-175">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c2e84-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c2e84-176">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="c2e84-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sciforma-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c2e84-178">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="c2e84-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sciforma-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c2e84-180">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c2e84-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sciforma-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c2e84-182">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c2e84-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sciforma-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c2e84-184">a.</span><span class="sxs-lookup"><span data-stu-id="c2e84-184">a.</span></span> <span data-ttu-id="c2e84-185">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c2e84-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c2e84-186">b.</span><span class="sxs-lookup"><span data-stu-id="c2e84-186">b.</span></span> <span data-ttu-id="c2e84-187">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c2e84-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c2e84-188">c.</span><span class="sxs-lookup"><span data-stu-id="c2e84-188">c.</span></span> <span data-ttu-id="c2e84-189">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="c2e84-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c2e84-190">d.</span><span class="sxs-lookup"><span data-stu-id="c2e84-190">d.</span></span> <span data-ttu-id="c2e84-191">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="c2e84-191">Click **Create**.</span></span>
 
### <a name="creating-a-sciforma-test-user"></a><span data-ttu-id="c2e84-192">Tworzenie użytkownika testowego Sciforma</span><span class="sxs-lookup"><span data-stu-id="c2e84-192">Creating a Sciforma test user</span></span>

<span data-ttu-id="c2e84-193">Nie ma elementu akcji do skonfigurowania inicjowania obsługi administracyjnej Sciforma użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c2e84-193">There is no action item for you to configure user provisioning to Sciforma.</span></span> <span data-ttu-id="c2e84-194">Gdy przypisany użytkownik próbuje zalogować się do Sciforma za pomocą panelu dostępu, Sciforma sprawdza, czy użytkownik istnieje.</span><span class="sxs-lookup"><span data-stu-id="c2e84-194">When an assigned user tries to log in to Sciforma using the access panel, Sciforma checks whether the user exists.</span></span>  

* <span data-ttu-id="c2e84-195">Jeśli nie jest Brak konta użytkownika dostępny jeszcze, są tworzone przez Sciforma.</span><span class="sxs-lookup"><span data-stu-id="c2e84-195">If there is no user account available yet, it is automatically created by Sciforma.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c2e84-196">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c2e84-196">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c2e84-197">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Sciforma.</span><span class="sxs-lookup"><span data-stu-id="c2e84-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Sciforma.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="c2e84-199">**Aby przypisać Simona Britta Sciforma, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c2e84-199">**To assign Britta Simon to Sciforma, perform the following steps:**</span></span>

1. <span data-ttu-id="c2e84-200">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="c2e84-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="c2e84-202">Na liście aplikacji zaznacz **Sciforma**.</span><span class="sxs-lookup"><span data-stu-id="c2e84-202">In the applications list, select **Sciforma**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sciforma-tutorial/tutorial_sciforma_app.png) 

3. <span data-ttu-id="c2e84-204">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="c2e84-204">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="c2e84-206">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c2e84-206">Click **Add** button.</span></span> <span data-ttu-id="c2e84-207">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c2e84-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="c2e84-209">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="c2e84-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c2e84-210">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c2e84-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c2e84-211">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c2e84-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c2e84-212">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="c2e84-212">Testing single sign-on</span></span>

<span data-ttu-id="c2e84-213">Jeśli chcesz przetestować jednego ustawienia logowania jednokrotnego, otwórz Panel dostępu.</span><span class="sxs-lookup"><span data-stu-id="c2e84-213">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="c2e84-214">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c2e84-214">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c2e84-215">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="c2e84-215">Additional resources</span></span>

* [<span data-ttu-id="c2e84-216">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c2e84-216">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c2e84-217">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c2e84-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_203.png

