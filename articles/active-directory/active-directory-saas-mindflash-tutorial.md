---
title: 'Samouczek: Integracji Azure Active Directory z Mindflash | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Mindflash."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bdf91993-aaaa-4598-89b7-77ef8ca065d5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 90de7b6a82d88f9407a35fbfebe8a652928d76cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mindflash"></a><span data-ttu-id="78ace-103">Samouczek: Integracji Azure Active Directory z Mindflash</span><span class="sxs-lookup"><span data-stu-id="78ace-103">Tutorial: Azure Active Directory integration with Mindflash</span></span>

<span data-ttu-id="78ace-104">Z tego samouczka dowiesz się integrowanie Mindflash z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="78ace-104">In this tutorial, you learn how to integrate Mindflash with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="78ace-105">Integracja z usługą Azure AD Mindflash zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="78ace-105">Integrating Mindflash with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="78ace-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Mindflash</span><span class="sxs-lookup"><span data-stu-id="78ace-106">You can control in Azure AD who has access to Mindflash</span></span>
- <span data-ttu-id="78ace-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Mindflash (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="78ace-107">You can enable your users to automatically get signed-on to Mindflash (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="78ace-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="78ace-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="78ace-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="78ace-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="78ace-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="78ace-110">Prerequisites</span></span>

<span data-ttu-id="78ace-111">Aby skonfigurować integrację usługi Azure AD z Mindflash, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="78ace-111">To configure Azure AD integration with Mindflash, you need the following items:</span></span>

- <span data-ttu-id="78ace-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="78ace-112">An Azure AD subscription</span></span>
- <span data-ttu-id="78ace-113">Mindflash logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="78ace-113">A Mindflash single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="78ace-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="78ace-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="78ace-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="78ace-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="78ace-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="78ace-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="78ace-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="78ace-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="78ace-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="78ace-118">Scenario description</span></span>
<span data-ttu-id="78ace-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="78ace-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="78ace-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="78ace-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="78ace-121">Dodawanie Mindflash z galerii</span><span class="sxs-lookup"><span data-stu-id="78ace-121">Adding Mindflash from the gallery</span></span>
2. <span data-ttu-id="78ace-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="78ace-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mindflash-from-the-gallery"></a><span data-ttu-id="78ace-123">Dodawanie Mindflash z galerii</span><span class="sxs-lookup"><span data-stu-id="78ace-123">Adding Mindflash from the gallery</span></span>
<span data-ttu-id="78ace-124">Aby skonfigurować integrację usługi Azure AD Mindflash, należy dodać Mindflash z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="78ace-124">To configure the integration of Mindflash into Azure AD, you need to add Mindflash from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="78ace-125">**Aby dodać Mindflash z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="78ace-125">**To add Mindflash from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="78ace-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="78ace-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="78ace-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="78ace-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="78ace-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="78ace-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="78ace-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="78ace-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="78ace-133">W polu wyszukiwania wpisz **Mindflash**.</span><span class="sxs-lookup"><span data-stu-id="78ace-133">In the search box, type **Mindflash**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_search.png)

5. <span data-ttu-id="78ace-135">W panelu wyników wybierz **Mindflash**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="78ace-135">In the results panel, select **Mindflash**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="78ace-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="78ace-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="78ace-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Mindflash w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="78ace-138">In this section, you configure and test Azure AD single sign-on with Mindflash based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="78ace-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Mindflash jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="78ace-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Mindflash is to a user in Azure AD.</span></span> <span data-ttu-id="78ace-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Mindflash musi się.</span><span class="sxs-lookup"><span data-stu-id="78ace-140">In other words, a link relationship between an Azure AD user and the related user in Mindflash needs to be established.</span></span>

<span data-ttu-id="78ace-141">W Mindflash, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="78ace-141">In Mindflash, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="78ace-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Mindflash, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="78ace-142">To configure and test Azure AD single sign-on with Mindflash, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="78ace-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="78ace-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="78ace-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="78ace-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="78ace-145">**[Tworzenie użytkownika testowego Mindflash](#creating-a-mindflash-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Mindflash połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="78ace-145">**[Creating a Mindflash test user](#creating-a-mindflash-test-user)** - to have a counterpart of Britta Simon in Mindflash that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="78ace-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="78ace-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="78ace-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="78ace-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="78ace-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="78ace-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="78ace-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Mindflash.</span><span class="sxs-lookup"><span data-stu-id="78ace-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mindflash application.</span></span>

<span data-ttu-id="78ace-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Mindflash, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="78ace-150">**To configure Azure AD single sign-on with Mindflash, perform the following steps:**</span></span>

1. <span data-ttu-id="78ace-151">W portalu Azure na **Mindflash** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="78ace-151">In the Azure portal, on the **Mindflash** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="78ace-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="78ace-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_samlbase.png)

3. <span data-ttu-id="78ace-155">Na **Mindflash domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="78ace-155">On the **Mindflash Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_url.png)

    <span data-ttu-id="78ace-157">a.</span><span class="sxs-lookup"><span data-stu-id="78ace-157">a.</span></span> <span data-ttu-id="78ace-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.mindflash.com`</span><span class="sxs-lookup"><span data-stu-id="78ace-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.mindflash.com`</span></span>

    <span data-ttu-id="78ace-159">b.</span><span class="sxs-lookup"><span data-stu-id="78ace-159">b.</span></span> <span data-ttu-id="78ace-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.mindflash.com`</span><span class="sxs-lookup"><span data-stu-id="78ace-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.mindflash.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="78ace-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="78ace-161">These values are not real.</span></span> <span data-ttu-id="78ace-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="78ace-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="78ace-163">Skontaktuj się z [zespołem pomocy technicznej klienta Mindflash](https://www.mindflash.com/contact/) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="78ace-163">Contact [Mindflash Client support team](https://www.mindflash.com/contact/) to get these values.</span></span> 
 


4. <span data-ttu-id="78ace-164">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="78ace-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_certificate.png) 

5. <span data-ttu-id="78ace-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="78ace-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mindflash-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="78ace-168">Skonfigurować logowanie jednokrotne w **Mindflash** stronie, musisz wysłać pobrany **XML metadanych** do [zespołem pomocy technicznej Mindflash](https://www.mindflash.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="78ace-168">To configure single sign-on on **Mindflash** side, you need to send the downloaded **Metadata XML** to [Mindflash support team](https://www.mindflash.com/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="78ace-169">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="78ace-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="78ace-170">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="78ace-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="78ace-171">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="78ace-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="78ace-172">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="78ace-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="78ace-173">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="78ace-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="78ace-175">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="78ace-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="78ace-176">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="78ace-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mindflash-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="78ace-178">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="78ace-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mindflash-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="78ace-180">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="78ace-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mindflash-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="78ace-182">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="78ace-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mindflash-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="78ace-184">a.</span><span class="sxs-lookup"><span data-stu-id="78ace-184">a.</span></span> <span data-ttu-id="78ace-185">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="78ace-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="78ace-186">b.</span><span class="sxs-lookup"><span data-stu-id="78ace-186">b.</span></span> <span data-ttu-id="78ace-187">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="78ace-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="78ace-188">c.</span><span class="sxs-lookup"><span data-stu-id="78ace-188">c.</span></span> <span data-ttu-id="78ace-189">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="78ace-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="78ace-190">d.</span><span class="sxs-lookup"><span data-stu-id="78ace-190">d.</span></span> <span data-ttu-id="78ace-191">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="78ace-191">Click **Create**.</span></span>
 
### <a name="creating-a-mindflash-test-user"></a><span data-ttu-id="78ace-192">Tworzenie użytkownika testowego Mindflash</span><span class="sxs-lookup"><span data-stu-id="78ace-192">Creating a Mindflash test user</span></span>

<span data-ttu-id="78ace-193">Aby włączyć użytkowników usługi Azure AD zalogować się do Mindflash, musi być przygotowana do Mindflash.</span><span class="sxs-lookup"><span data-stu-id="78ace-193">In order to enable Azure AD users to log into Mindflash, they must be provisioned into Mindflash.</span></span> <span data-ttu-id="78ace-194">W przypadku Mindflash Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="78ace-194">In the case of Mindflash, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-accounts-perform-the-following-steps"></a><span data-ttu-id="78ace-195">Aby udostępnić konta użytkowników, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="78ace-195">To provision a user accounts, perform the following steps:</span></span>

1. <span data-ttu-id="78ace-196">Zaloguj się do Twojego **Mindflash** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="78ace-196">Log in to your **Mindflash** company site as an administrator.</span></span>

2. <span data-ttu-id="78ace-197">Przejdź do **Zarządzanie użytkownikami**.</span><span class="sxs-lookup"><span data-stu-id="78ace-197">Go to **Manage Users**.</span></span>
   
    <span data-ttu-id="78ace-198">![Zarządzaj użytkownikami](./media/active-directory-saas-mindflash-tutorial/ic787140.png "Zarządzanie użytkownikami")</span><span class="sxs-lookup"><span data-stu-id="78ace-198">![Manage Users](./media/active-directory-saas-mindflash-tutorial/ic787140.png "Manage Users")</span></span>

3. <span data-ttu-id="78ace-199">Kliknij przycisk **Dodaj użytkowników**, a następnie kliknij przycisk **nowy**.</span><span class="sxs-lookup"><span data-stu-id="78ace-199">Click the **Add Users**, and then click **New**.</span></span>

4. <span data-ttu-id="78ace-200">W **Dodaj nowych użytkowników** sekcji, wykonaj następujące kroki prawidłowy Azure AD konta chcesz udostępnić:</span><span class="sxs-lookup"><span data-stu-id="78ace-200">In the **Add New Users** section, perform the following steps of a valid Azure AD account you want to provision:</span></span>
   
    <span data-ttu-id="78ace-201">![Dodawanie nowych użytkowników](./media/active-directory-saas-mindflash-tutorial/ic787141.png "Dodawanie nowych użytkowników")</span><span class="sxs-lookup"><span data-stu-id="78ace-201">![Add New Users](./media/active-directory-saas-mindflash-tutorial/ic787141.png "Add New Users")</span></span>
   
    <span data-ttu-id="78ace-202">a.</span><span class="sxs-lookup"><span data-stu-id="78ace-202">a.</span></span> <span data-ttu-id="78ace-203">W **imię** pole tekstowe, typ **imię** użytkownika jako **Britta**.</span><span class="sxs-lookup"><span data-stu-id="78ace-203">In the **First name** textbox, type **First name** of the user as **Britta**.</span></span>

    <span data-ttu-id="78ace-204">b.</span><span class="sxs-lookup"><span data-stu-id="78ace-204">b.</span></span> <span data-ttu-id="78ace-205">W **nazwisko** pole tekstowe, typ **nazwisko** użytkownika jako **Simona**.</span><span class="sxs-lookup"><span data-stu-id="78ace-205">In the **Last name** textbox, type **Last name** of the user as **Simon**.</span></span>
    
    <span data-ttu-id="78ace-206">c.</span><span class="sxs-lookup"><span data-stu-id="78ace-206">c.</span></span> <span data-ttu-id="78ace-207">W **E-mail** pole tekstowe, typ **adres E-mail** użytkownika jako  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="78ace-207">In the **Email** textbox, type **Email Address** of the user as **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="78ace-208">b.</span><span class="sxs-lookup"><span data-stu-id="78ace-208">b.</span></span> <span data-ttu-id="78ace-209">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="78ace-209">Click **Add**.</span></span>

>[!NOTE]
><span data-ttu-id="78ace-210">Możesz użyć innych Mindflash użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Mindflash do kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="78ace-210">You can use any other Mindflash user account creation tools or APIs provided by Mindflash to provision AAD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="78ace-211">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="78ace-211">Assigning the Azure AD test user</span></span>

<span data-ttu-id="78ace-212">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Mindflash.</span><span class="sxs-lookup"><span data-stu-id="78ace-212">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mindflash.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="78ace-214">**Aby przypisać Simona Britta Mindflash, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="78ace-214">**To assign Britta Simon to Mindflash, perform the following steps:**</span></span>

1. <span data-ttu-id="78ace-215">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="78ace-215">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="78ace-217">Na liście aplikacji zaznacz **Mindflash**.</span><span class="sxs-lookup"><span data-stu-id="78ace-217">In the applications list, select **Mindflash**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_app.png) 

3. <span data-ttu-id="78ace-219">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="78ace-219">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="78ace-221">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="78ace-221">Click **Add** button.</span></span> <span data-ttu-id="78ace-222">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="78ace-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="78ace-224">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="78ace-224">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="78ace-225">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="78ace-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="78ace-226">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="78ace-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="78ace-227">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="78ace-227">Testing single sign-on</span></span>

<span data-ttu-id="78ace-228">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="78ace-228">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="78ace-229">Po kliknięciu kafelka Mindflash w panelu dostępu, należy pobrać strony logowania Mindflash aplikacji.</span><span class="sxs-lookup"><span data-stu-id="78ace-229">When you click the Mindflash tile in the Access Panel, you should get login page of Mindflash application.</span></span>
<span data-ttu-id="78ace-230">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="78ace-230">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="78ace-231">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="78ace-231">Additional resources</span></span>

* [<span data-ttu-id="78ace-232">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="78ace-232">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="78ace-233">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="78ace-233">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_203.png

