---
title: 'Samouczek: Integracji Azure Active Directory z gwiazdek CS | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i CS gwiazdek."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5704d151-afb8-40a4-b286-8bacd4f279ee
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: acc9160f86e58c7af4779a8bab5627dc5c5ad721
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cs-stars"></a><span data-ttu-id="9c042-103">Samouczek: Integracji Azure Active Directory z CS gwiazdek</span><span class="sxs-lookup"><span data-stu-id="9c042-103">Tutorial: Azure Active Directory integration with CS Stars</span></span>

<span data-ttu-id="9c042-104">Z tego samouczka dowiesz integrowanie CS gwiazdek w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9c042-104">In this tutorial, you learn how to integrate CS Stars with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9c042-105">Integracja z usługą Azure AD CS gwiazdek zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="9c042-105">Integrating CS Stars with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9c042-106">Można kontrolować w usłudze Azure AD, który ma dostęp do CS gwiazdek</span><span class="sxs-lookup"><span data-stu-id="9c042-106">You can control in Azure AD who has access to CS Stars</span></span>
- <span data-ttu-id="9c042-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do CS gwiazdek (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9c042-107">You can enable your users to automatically get signed-on to CS Stars (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9c042-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="9c042-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9c042-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9c042-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9c042-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9c042-110">Prerequisites</span></span>

<span data-ttu-id="9c042-111">Aby skonfigurować integrację usługi Azure AD z CS gwiazdek, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="9c042-111">To configure Azure AD integration with CS Stars, you need the following items:</span></span>

- <span data-ttu-id="9c042-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9c042-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9c042-113">CS gwiazdek jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="9c042-113">A CS Stars single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9c042-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="9c042-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9c042-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="9c042-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9c042-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="9c042-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9c042-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9c042-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9c042-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="9c042-118">Scenario description</span></span>
<span data-ttu-id="9c042-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="9c042-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9c042-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="9c042-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9c042-121">Dodawanie gwiazdek CS z galerii</span><span class="sxs-lookup"><span data-stu-id="9c042-121">Adding CS Stars from the gallery</span></span>
2. <span data-ttu-id="9c042-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="9c042-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cs-stars-from-the-gallery"></a><span data-ttu-id="9c042-123">Dodawanie gwiazdek CS z galerii</span><span class="sxs-lookup"><span data-stu-id="9c042-123">Adding CS Stars from the gallery</span></span>
<span data-ttu-id="9c042-124">Aby skonfigurować integrację usługi Azure AD CS gwiazdek, należy dodać gwiazdek CS z poziomu galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="9c042-124">To configure the integration of CS Stars into Azure AD, you need to add CS Stars from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9c042-125">**Aby dodać gwiazdek CS z poziomu galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="9c042-125">**To add CS Stars from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9c042-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="9c042-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="9c042-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="9c042-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9c042-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="9c042-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="9c042-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9c042-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="9c042-133">W polu wyszukiwania wpisz **gwiazdek CS**.</span><span class="sxs-lookup"><span data-stu-id="9c042-133">In the search box, type **CS Stars**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_search.png)

5. <span data-ttu-id="9c042-135">W panelu wyników wybierz **gwiazdek CS**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="9c042-135">In the results panel, select **CS Stars**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9c042-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="9c042-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9c042-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z gwiazdek CS na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="9c042-138">In this section, you configure and test Azure AD single sign-on with CS Stars based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9c042-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w gwiazdek CS jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9c042-139">For single sign-on to work, Azure AD needs to know what the counterpart user in CS Stars is to a user in Azure AD.</span></span> <span data-ttu-id="9c042-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i danemu użytkownikowi w gwiazdek CS musi określone.</span><span class="sxs-lookup"><span data-stu-id="9c042-140">In other words, a link relationship between an Azure AD user and the related user in CS Stars needs to be established.</span></span>

<span data-ttu-id="9c042-141">W gwiazdek CS, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="9c042-141">In CS Stars, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9c042-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z gwiazdek CS, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="9c042-142">To configure and test Azure AD single sign-on with CS Stars, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9c042-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="9c042-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9c042-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="9c042-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9c042-145">**[Tworzenie użytkownika testowego gwiazdek CS](#creating-a-cs-stars-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta CS gwiazdki, powiązaną z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9c042-145">**[Creating a CS Stars test user](#creating-a-cs-stars-test-user)** - to have a counterpart of Britta Simon in CS Stars that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9c042-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="9c042-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9c042-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="9c042-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9c042-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9c042-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9c042-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji CS gwiazdek.</span><span class="sxs-lookup"><span data-stu-id="9c042-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your CS Stars application.</span></span>

<span data-ttu-id="9c042-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z CS gwiazdek, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="9c042-150">**To configure Azure AD single sign-on with CS Stars, perform the following steps:**</span></span>

1. <span data-ttu-id="9c042-151">W portalu Azure na **gwiazdek CS** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="9c042-151">In the Azure portal, on the **CS Stars** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="9c042-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="9c042-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_samlbase.png)

3. <span data-ttu-id="9c042-155">Na **CS gwiazdek domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9c042-155">On the **CS Stars Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_url.png)

    <span data-ttu-id="9c042-157">a.</span><span class="sxs-lookup"><span data-stu-id="9c042-157">a.</span></span> <span data-ttu-id="9c042-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.csstars.com/enterprise/default.cmdx?ssoclient=<uniqueid>`</span><span class="sxs-lookup"><span data-stu-id="9c042-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.csstars.com/enterprise/default.cmdx?ssoclient=<uniqueid>`</span></span>

    <span data-ttu-id="9c042-159">b.</span><span class="sxs-lookup"><span data-stu-id="9c042-159">b.</span></span> <span data-ttu-id="9c042-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.csstars.com/enterprise/`</span><span class="sxs-lookup"><span data-stu-id="9c042-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.csstars.com/enterprise/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9c042-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="9c042-161">These values are not real.</span></span> <span data-ttu-id="9c042-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="9c042-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="9c042-163">Skontaktuj się z [zespołem pomocy technicznej klienta gwiazdek CS](http://www.marshclearsight.com/support/) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="9c042-163">Contact [CS Stars Client support team](http://www.marshclearsight.com/support/) to get these values.</span></span> 
 
4. <span data-ttu-id="9c042-164">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="9c042-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_certificate.png) 

5. <span data-ttu-id="9c042-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9c042-166">Click **Save** button.</span></span>

    <span data-ttu-id="9c042-167">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cs-stars-tutorial/tutorial_general_400.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="9c042-167">![Configure Single Sign-On](./media/active-directory-saas-cs-stars-tutorial/tutorial_general_400.png) 
<CS></span></span>
6. <span data-ttu-id="9c042-168">Skonfigurować logowanie jednokrotne w **gwiazdek CS** stronie, musisz wysłać pobrany **XML metadanych** do [gwiazdek CS obsługuje zespołu](http://www.marshclearsight.com/support/).</span><span class="sxs-lookup"><span data-stu-id="9c042-168">To configure single sign-on on **CS Stars** side, you need to send the downloaded **Metadata XML** to [CS Stars support team](http://www.marshclearsight.com/support/).</span></span> 
<CE>

> [!TIP]
> <span data-ttu-id="9c042-169">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="9c042-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9c042-170">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="9c042-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9c042-171">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9c042-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9c042-172">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9c042-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="9c042-173">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="9c042-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="9c042-175">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="9c042-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9c042-176">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="9c042-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cs-stars-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9c042-178">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="9c042-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cs-stars-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9c042-180">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9c042-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cs-stars-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9c042-182">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9c042-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cs-stars-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9c042-184">a.</span><span class="sxs-lookup"><span data-stu-id="9c042-184">a.</span></span> <span data-ttu-id="9c042-185">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9c042-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9c042-186">b.</span><span class="sxs-lookup"><span data-stu-id="9c042-186">b.</span></span> <span data-ttu-id="9c042-187">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9c042-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9c042-188">c.</span><span class="sxs-lookup"><span data-stu-id="9c042-188">c.</span></span> <span data-ttu-id="9c042-189">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="9c042-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9c042-190">d.</span><span class="sxs-lookup"><span data-stu-id="9c042-190">d.</span></span> <span data-ttu-id="9c042-191">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="9c042-191">Click **Create**.</span></span>
 
### <a name="creating-a-cs-stars-test-user"></a><span data-ttu-id="9c042-192">Tworzenie użytkownika testowego CS gwiazdek</span><span class="sxs-lookup"><span data-stu-id="9c042-192">Creating a CS Stars test user</span></span>

<span data-ttu-id="9c042-193">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w CS gwiazdek.</span><span class="sxs-lookup"><span data-stu-id="9c042-193">The objective of this section is to create a user called Britta Simon in CS Stars.</span></span>

<span data-ttu-id="9c042-194">Aby uzyskać utworzony w gwiazdek CS przez użytkownika, należy skontaktować się z [gwiazdek CS obsługuje zespołu](http://www.marshclearsight.com/support/).</span><span class="sxs-lookup"><span data-stu-id="9c042-194">To get a user created in CS Stars, you need to contact your [CS Stars support team](http://www.marshclearsight.com/support/).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9c042-195">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9c042-195">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9c042-196">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do CS gwiazdek.</span><span class="sxs-lookup"><span data-stu-id="9c042-196">In this section, you enable Britta Simon to use Azure single sign-on by granting access to CS Stars.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="9c042-198">**Aby przypisać Simona Britta CS gwiazdek, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="9c042-198">**To assign Britta Simon to CS Stars, perform the following steps:**</span></span>

1. <span data-ttu-id="9c042-199">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="9c042-199">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="9c042-201">Na liście aplikacji zaznacz **gwiazdek CS**.</span><span class="sxs-lookup"><span data-stu-id="9c042-201">In the applications list, select **CS Stars**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_app.png) 

3. <span data-ttu-id="9c042-203">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="9c042-203">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="9c042-205">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9c042-205">Click **Add** button.</span></span> <span data-ttu-id="9c042-206">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9c042-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="9c042-208">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="9c042-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9c042-209">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9c042-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9c042-210">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9c042-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9c042-211">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9c042-211">Testing single sign-on</span></span>

<span data-ttu-id="9c042-212">Celem tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="9c042-212">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="9c042-213">Po kliknięciu kafelka CS gwiazdek w panelu dostępu należy należy pobrać automatycznie zalogowane do aplikacji CS gwiazdek.</span><span class="sxs-lookup"><span data-stu-id="9c042-213">When you click the CS Stars tile in the Access Panel, you should get automatically signed-on to your CS Stars application.</span></span>
 

## <a name="additional-resources"></a><span data-ttu-id="9c042-214">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="9c042-214">Additional resources</span></span>

* [<span data-ttu-id="9c042-215">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9c042-215">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9c042-216">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9c042-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_203.png

