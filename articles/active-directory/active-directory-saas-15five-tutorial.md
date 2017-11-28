---
title: 'Samouczek: Integracji Azure Active Directory z 15Five | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i 15Five."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2fb301c2-7d7a-4046-8ee1-7dc9e7684806
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: ea36774747a0fcfa4ace1aefb2d46dba815d92c4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-15five"></a><span data-ttu-id="54c9c-103">Samouczek: Integracji Azure Active Directory z 15Five</span><span class="sxs-lookup"><span data-stu-id="54c9c-103">Tutorial: Azure Active Directory integration with 15Five</span></span>

<span data-ttu-id="54c9c-104">Z tego samouczka dowiesz się integrowanie 15Five z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="54c9c-104">In this tutorial, you learn how to integrate 15Five with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="54c9c-105">Integracja z usługą Azure AD 15Five zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="54c9c-105">Integrating 15Five with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="54c9c-106">Można kontrolować w usłudze Azure AD, który ma dostęp do 15Five</span><span class="sxs-lookup"><span data-stu-id="54c9c-106">You can control in Azure AD who has access to 15Five</span></span>
- <span data-ttu-id="54c9c-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do 15Five (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="54c9c-107">You can enable your users to automatically get signed-on to 15Five (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="54c9c-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="54c9c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="54c9c-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="54c9c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="54c9c-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="54c9c-110">Prerequisites</span></span>

<span data-ttu-id="54c9c-111">Aby skonfigurować integrację usługi Azure AD z 15Five, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="54c9c-111">To configure Azure AD integration with 15Five, you need the following items:</span></span>

- <span data-ttu-id="54c9c-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="54c9c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="54c9c-113">15Five jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="54c9c-113">A 15Five single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="54c9c-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="54c9c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="54c9c-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="54c9c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="54c9c-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="54c9c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="54c9c-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="54c9c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="54c9c-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="54c9c-118">Scenario description</span></span>
<span data-ttu-id="54c9c-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="54c9c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="54c9c-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="54c9c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="54c9c-121">Dodawanie 15Five z galerii</span><span class="sxs-lookup"><span data-stu-id="54c9c-121">Adding 15Five from the gallery</span></span>
2. <span data-ttu-id="54c9c-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="54c9c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-15five-from-the-gallery"></a><span data-ttu-id="54c9c-123">Dodawanie 15Five z galerii</span><span class="sxs-lookup"><span data-stu-id="54c9c-123">Adding 15Five from the gallery</span></span>
<span data-ttu-id="54c9c-124">Aby skonfigurować integrację usługi Azure AD 15Five, należy dodać 15Five z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="54c9c-124">To configure the integration of 15Five into Azure AD, you need to add 15Five from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="54c9c-125">**Aby dodać 15Five z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="54c9c-125">**To add 15Five from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="54c9c-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="54c9c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="54c9c-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="54c9c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="54c9c-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="54c9c-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="54c9c-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="54c9c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="54c9c-133">W polu wyszukiwania wpisz **15Five**.</span><span class="sxs-lookup"><span data-stu-id="54c9c-133">In the search box, type **15Five**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-15five-tutorial/tutorial_15five_search.png)

5. <span data-ttu-id="54c9c-135">W panelu wyników wybierz **15Five**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="54c9c-135">In the results panel, select **15Five**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-15five-tutorial/tutorial_15five_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="54c9c-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="54c9c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="54c9c-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z 15Five na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="54c9c-138">In this section, you configure and test Azure AD single sign-on with 15Five based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="54c9c-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w 15Five jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="54c9c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 15Five is to a user in Azure AD.</span></span> <span data-ttu-id="54c9c-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w 15Five musi się.</span><span class="sxs-lookup"><span data-stu-id="54c9c-140">In other words, a link relationship between an Azure AD user and the related user in 15Five needs to be established.</span></span>

<span data-ttu-id="54c9c-141">W 15Five, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="54c9c-141">In 15Five, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="54c9c-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z 15Five, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="54c9c-142">To configure and test Azure AD single sign-on with 15Five, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="54c9c-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="54c9c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="54c9c-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="54c9c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="54c9c-145">**[Tworzenie użytkownika testowego 15Five](#creating-a-15five-test-user)**  — mają odpowiednika Simona Britta w 15Five połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="54c9c-145">**[Creating a 15Five test user](#creating-a-15five-test-user)** - to have a counterpart of Britta Simon in 15Five that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="54c9c-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="54c9c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="54c9c-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="54c9c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="54c9c-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="54c9c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="54c9c-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji 15Five.</span><span class="sxs-lookup"><span data-stu-id="54c9c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 15Five application.</span></span>

<span data-ttu-id="54c9c-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z 15Five, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="54c9c-150">**To configure Azure AD single sign-on with 15Five, perform the following steps:**</span></span>

1. <span data-ttu-id="54c9c-151">W portalu Azure na **15Five** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="54c9c-151">In the Azure portal, on the **15Five** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="54c9c-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="54c9c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-15five-tutorial/tutorial_15five_samlbase.png)

3. <span data-ttu-id="54c9c-155">Na **15Five domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="54c9c-155">On the **15Five Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-15five-tutorial/tutorial_15five_url.png)

    <span data-ttu-id="54c9c-157">a.</span><span class="sxs-lookup"><span data-stu-id="54c9c-157">a.</span></span> <span data-ttu-id="54c9c-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.15five.com`</span><span class="sxs-lookup"><span data-stu-id="54c9c-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.15five.com`</span></span>

    <span data-ttu-id="54c9c-159">b.</span><span class="sxs-lookup"><span data-stu-id="54c9c-159">b.</span></span> <span data-ttu-id="54c9c-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.15five.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="54c9c-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.15five.com/saml2/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="54c9c-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="54c9c-161">These values are not real.</span></span> <span data-ttu-id="54c9c-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="54c9c-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="54c9c-163">Skontaktuj się z [zespołem pomocy technicznej klienta 15Five](https://www.15five.com/contact/) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="54c9c-163">Contact [15Five Client support team](https://www.15five.com/contact/) to get these values.</span></span> 
 
4. <span data-ttu-id="54c9c-164">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="54c9c-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-15five-tutorial/tutorial_15five_certificate.png) 

5. <span data-ttu-id="54c9c-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="54c9c-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-15five-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="54c9c-168">Skonfigurować logowanie jednokrotne w **15Five** stronie, musisz wysłać pobrany **XML metadanych** do [zespołem pomocy technicznej 15Five](https://www.15five.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="54c9c-168">To configure single sign-on on **15Five** side, you need to send the downloaded **Metadata XML** to [15Five support team](https://www.15five.com/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="54c9c-169">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="54c9c-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="54c9c-170">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="54c9c-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="54c9c-171">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="54c9c-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="54c9c-172">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="54c9c-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="54c9c-173">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="54c9c-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="54c9c-175">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="54c9c-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="54c9c-176">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="54c9c-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-15five-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="54c9c-178">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="54c9c-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-15five-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="54c9c-180">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="54c9c-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-15five-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="54c9c-182">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="54c9c-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-15five-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="54c9c-184">a.</span><span class="sxs-lookup"><span data-stu-id="54c9c-184">a.</span></span> <span data-ttu-id="54c9c-185">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="54c9c-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="54c9c-186">b.</span><span class="sxs-lookup"><span data-stu-id="54c9c-186">b.</span></span> <span data-ttu-id="54c9c-187">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="54c9c-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="54c9c-188">c.</span><span class="sxs-lookup"><span data-stu-id="54c9c-188">c.</span></span> <span data-ttu-id="54c9c-189">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="54c9c-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="54c9c-190">d.</span><span class="sxs-lookup"><span data-stu-id="54c9c-190">d.</span></span> <span data-ttu-id="54c9c-191">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="54c9c-191">Click **Create**.</span></span>
 
### <a name="creating-a-15five-test-user"></a><span data-ttu-id="54c9c-192">Tworzenie użytkownika testowego 15Five</span><span class="sxs-lookup"><span data-stu-id="54c9c-192">Creating a 15Five test user</span></span>

<span data-ttu-id="54c9c-193">Aby umożliwić użytkownikom usługi Azure AD zalogować się do 15Five, musi być przygotowana do 15Five.</span><span class="sxs-lookup"><span data-stu-id="54c9c-193">To enable Azure AD users to log in to 15Five, they must be provisioned into 15Five.</span></span> <span data-ttu-id="54c9c-194">Podczas inicjowania obsługi administracyjnej jest 15Five, ręcznie.</span><span class="sxs-lookup"><span data-stu-id="54c9c-194">When 15Five, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="54c9c-195">Aby skonfigurować, inicjowanie obsługi użytkowników, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="54c9c-195">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="54c9c-196">Zaloguj się do Twojego **15Five** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="54c9c-196">Log in to your **15Five** company site as administrator.</span></span>

2. <span data-ttu-id="54c9c-197">Przejdź do **Zarządzanie firmy**.</span><span class="sxs-lookup"><span data-stu-id="54c9c-197">Go to **Manage Company**.</span></span>
   
    <span data-ttu-id="54c9c-198">![Zarządzanie firmy](./media/active-directory-saas-15five-tutorial/IC784675.png "Zarządzanie firmy")</span><span class="sxs-lookup"><span data-stu-id="54c9c-198">![Manage Company](./media/active-directory-saas-15five-tutorial/IC784675.png "Manage Company")</span></span>

3. <span data-ttu-id="54c9c-199">Przejdź do **osób \> dodać osoby**.</span><span class="sxs-lookup"><span data-stu-id="54c9c-199">Go to **People \> Add People**.</span></span>
   
    <span data-ttu-id="54c9c-200">![Osoby](./media/active-directory-saas-15five-tutorial/IC784676.png "osób")</span><span class="sxs-lookup"><span data-stu-id="54c9c-200">![People](./media/active-directory-saas-15five-tutorial/IC784676.png "People")</span></span>

4. <span data-ttu-id="54c9c-201">W sekcji Dodawanie nowej osoby wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="54c9c-201">In the Add New Person section, perform the following steps:</span></span>
   
    <span data-ttu-id="54c9c-202">![Dodawanie nowej osoby](./media/active-directory-saas-15five-tutorial/IC784677.png "Dodawanie nowej osoby")</span><span class="sxs-lookup"><span data-stu-id="54c9c-202">![Add New Person](./media/active-directory-saas-15five-tutorial/IC784677.png "Add New Person")</span></span>
   
    <span data-ttu-id="54c9c-203">a.</span><span class="sxs-lookup"><span data-stu-id="54c9c-203">a.</span></span> <span data-ttu-id="54c9c-204">Typ **imię**, **nazwisko**, **tytuł**, **adres E-mail** poprawnego konta usługi Azure Active Directory ustanawiane do powiązanych pól tekstowych.</span><span class="sxs-lookup"><span data-stu-id="54c9c-204">Type the **First Name**, **Last Name**, **Title**, **Email address** of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>

    <span data-ttu-id="54c9c-205">b.</span><span class="sxs-lookup"><span data-stu-id="54c9c-205">b.</span></span> <span data-ttu-id="54c9c-206">Kliknij przycisk **Gotowe**.</span><span class="sxs-lookup"><span data-stu-id="54c9c-206">Click **Done**.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="54c9c-207">Właściciel konta usługi Azure AD odbiera wiadomości e-mail, łącznie z łączem do potwierdzenia konta, zanim staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="54c9c-207">The Azure AD account holder receives an email including a link to confirm the account before it becomes active.</span></span>
   
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="54c9c-208">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="54c9c-208">Assigning the Azure AD test user</span></span>

<span data-ttu-id="54c9c-209">W tej sekcji musisz włączyć Simona Britta do użycia usługi Azure logowania jednokrotnego za udzielanie dostępu do 15Five.</span><span class="sxs-lookup"><span data-stu-id="54c9c-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 15Five.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="54c9c-211">**Aby przypisać Simona Britta 15Five, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="54c9c-211">**To assign Britta Simon to 15Five, perform the following steps:**</span></span>

1. <span data-ttu-id="54c9c-212">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="54c9c-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="54c9c-214">Na liście aplikacji zaznacz **15Five**.</span><span class="sxs-lookup"><span data-stu-id="54c9c-214">In the applications list, select **15Five**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-15five-tutorial/tutorial_15five_app.png) 

3. <span data-ttu-id="54c9c-216">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="54c9c-216">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="54c9c-218">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="54c9c-218">Click **Add** button.</span></span> <span data-ttu-id="54c9c-219">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="54c9c-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="54c9c-221">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="54c9c-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="54c9c-222">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="54c9c-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="54c9c-223">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="54c9c-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="54c9c-224">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="54c9c-224">Testing single sign-on</span></span>

<span data-ttu-id="54c9c-225">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="54c9c-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="54c9c-226">Po kliknięciu kafelka 15Five w panelu dostępu, należy pobrać strony logowania 15Five aplikacji.</span><span class="sxs-lookup"><span data-stu-id="54c9c-226">When you click the 15Five tile in the Access Panel, you should get login page of 15Five application.</span></span>
<span data-ttu-id="54c9c-227">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="54c9c-227">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="54c9c-228">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="54c9c-228">Additional resources</span></span>

* [<span data-ttu-id="54c9c-229">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="54c9c-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="54c9c-230">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="54c9c-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-15five-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-15five-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-15five-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-15five-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-15five-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-15five-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-15five-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-15five-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-15five-tutorial/tutorial_general_203.png

