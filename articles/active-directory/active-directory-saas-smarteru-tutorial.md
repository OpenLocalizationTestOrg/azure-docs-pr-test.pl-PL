---
title: 'Samouczek: Integracji Azure Active Directory z SmarterU | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i SmarterU."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 95fe3212-d052-4ac8-87eb-ac5305227e85
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 129d08c8a7b4228d4d5f1a3b7938ab649b2747a7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-smarteru"></a><span data-ttu-id="1ef14-103">Samouczek: Integracji Azure Active Directory z SmarterU</span><span class="sxs-lookup"><span data-stu-id="1ef14-103">Tutorial: Azure Active Directory integration with SmarterU</span></span>

<span data-ttu-id="1ef14-104">Z tego samouczka dowiesz się integrowanie SmarterU z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1ef14-104">In this tutorial, you learn how to integrate SmarterU with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1ef14-105">Integracja z usługą Azure AD SmarterU zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="1ef14-105">Integrating SmarterU with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1ef14-106">Można kontrolować w usłudze Azure AD, który ma dostęp do SmarterU</span><span class="sxs-lookup"><span data-stu-id="1ef14-106">You can control in Azure AD who has access to SmarterU</span></span>
- <span data-ttu-id="1ef14-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do SmarterU (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ef14-107">You can enable your users to automatically get signed-on to SmarterU (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1ef14-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="1ef14-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1ef14-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1ef14-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1ef14-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1ef14-110">Prerequisites</span></span>

<span data-ttu-id="1ef14-111">Aby skonfigurować integrację usługi Azure AD z SmarterU, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="1ef14-111">To configure Azure AD integration with SmarterU, you need the following items:</span></span>

- <span data-ttu-id="1ef14-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ef14-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1ef14-113">SmarterU logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="1ef14-113">A SmarterU single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1ef14-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="1ef14-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1ef14-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="1ef14-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1ef14-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="1ef14-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1ef14-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1ef14-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1ef14-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="1ef14-118">Scenario description</span></span>
<span data-ttu-id="1ef14-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="1ef14-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1ef14-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="1ef14-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1ef14-121">Dodawanie SmarterU z galerii</span><span class="sxs-lookup"><span data-stu-id="1ef14-121">Adding SmarterU from the gallery</span></span>
2. <span data-ttu-id="1ef14-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="1ef14-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-smarteru-from-the-gallery"></a><span data-ttu-id="1ef14-123">Dodawanie SmarterU z galerii</span><span class="sxs-lookup"><span data-stu-id="1ef14-123">Adding SmarterU from the gallery</span></span>
<span data-ttu-id="1ef14-124">Aby skonfigurować integrację usługi Azure AD SmarterU, należy dodać SmarterU z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="1ef14-124">To configure the integration of SmarterU into Azure AD, you need to add SmarterU from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1ef14-125">**Aby dodać SmarterU z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="1ef14-125">**To add SmarterU from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1ef14-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="1ef14-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="1ef14-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="1ef14-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1ef14-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="1ef14-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="1ef14-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1ef14-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="1ef14-133">W polu wyszukiwania wpisz **SmarterU**.</span><span class="sxs-lookup"><span data-stu-id="1ef14-133">In the search box, type **SmarterU**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_search.png)

5. <span data-ttu-id="1ef14-135">W panelu wyników wybierz **SmarterU**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="1ef14-135">In the results panel, select **SmarterU**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1ef14-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="1ef14-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1ef14-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z SmarterU na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="1ef14-138">In this section, you configure and test Azure AD single sign-on with SmarterU based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1ef14-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w SmarterU jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1ef14-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SmarterU is to a user in Azure AD.</span></span> <span data-ttu-id="1ef14-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w SmarterU musi się.</span><span class="sxs-lookup"><span data-stu-id="1ef14-140">In other words, a link relationship between an Azure AD user and the related user in SmarterU needs to be established.</span></span>

<span data-ttu-id="1ef14-141">W SmarterU, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="1ef14-141">In SmarterU, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1ef14-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z SmarterU, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="1ef14-142">To configure and test Azure AD single sign-on with SmarterU, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1ef14-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="1ef14-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1ef14-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="1ef14-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1ef14-145">**[Tworzenie użytkownika testowego SmarterU](#creating-a-smarteru-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta SmarterU połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1ef14-145">**[Creating a SmarterU test user](#creating-a-smarteru-test-user)** - to have a counterpart of Britta Simon in SmarterU that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1ef14-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="1ef14-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1ef14-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="1ef14-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1ef14-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="1ef14-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1ef14-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji SmarterU.</span><span class="sxs-lookup"><span data-stu-id="1ef14-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SmarterU application.</span></span>

<span data-ttu-id="1ef14-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z SmarterU, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="1ef14-150">**To configure Azure AD single sign-on with SmarterU, perform the following steps:**</span></span>

1. <span data-ttu-id="1ef14-151">W portalu Azure na **SmarterU** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="1ef14-151">In the Azure portal, on the **SmarterU** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="1ef14-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="1ef14-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_samlbase.png)

3. <span data-ttu-id="1ef14-155">Na **SmarterU domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="1ef14-155">On the **SmarterU Domain and URLs** section, perform the following steps:</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_url.png)

    <span data-ttu-id="1ef14-157">W **identyfikator** tekstowym, wpisz adres URL:`https://www.smarteru.com/`</span><span class="sxs-lookup"><span data-stu-id="1ef14-157">In the **Identifier** textbox, type the URL: `https://www.smarteru.com/`</span></span>

4. <span data-ttu-id="1ef14-158">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="1ef14-158">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_certificate.png) 

5. <span data-ttu-id="1ef14-160">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="1ef14-160">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-smarteru-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1ef14-162">W oknie przeglądarki innej witryny sieci web należy zalogować się jako administrator do witryny firmy SmarterU.</span><span class="sxs-lookup"><span data-stu-id="1ef14-162">In a different web browser window, log in to your SmarterU company site as an administrator.</span></span>

7. <span data-ttu-id="1ef14-163">Na pasku narzędzi u góry kliknij **ustawienia konta**.</span><span class="sxs-lookup"><span data-stu-id="1ef14-163">In the toolbar on the top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="1ef14-164">![Ustawienia konta](./media/active-directory-saas-smarteru-tutorial/IC777326.png "ustawienia konta")</span><span class="sxs-lookup"><span data-stu-id="1ef14-164">![Account Settings](./media/active-directory-saas-smarteru-tutorial/IC777326.png "Account Settings")</span></span>

8. <span data-ttu-id="1ef14-165">Na stronie konfiguracji konta wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="1ef14-165">On the account configuration page, perform the following steps:</span></span>
   
    <span data-ttu-id="1ef14-166">![Autoryzację zewnętrzne](./media/active-directory-saas-smarteru-tutorial/IC777327.png "autoryzację zewnętrzne")</span><span class="sxs-lookup"><span data-stu-id="1ef14-166">![External Authorization](./media/active-directory-saas-smarteru-tutorial/IC777327.png "External Authorization")</span></span> 
 
      <span data-ttu-id="1ef14-167">a.</span><span class="sxs-lookup"><span data-stu-id="1ef14-167">a.</span></span> <span data-ttu-id="1ef14-168">Wybierz **Włącz autoryzację zewnętrzne**.</span><span class="sxs-lookup"><span data-stu-id="1ef14-168">Select **Enable External Authorization**.</span></span>
  
      <span data-ttu-id="1ef14-169">b.</span><span class="sxs-lookup"><span data-stu-id="1ef14-169">b.</span></span> <span data-ttu-id="1ef14-170">W **formantu logowania wzorca** zaznacz **SmarterU** kartę.</span><span class="sxs-lookup"><span data-stu-id="1ef14-170">In the **Master Login Control** section, select the **SmarterU** tab.</span></span>
  
      <span data-ttu-id="1ef14-171">c.</span><span class="sxs-lookup"><span data-stu-id="1ef14-171">c.</span></span> <span data-ttu-id="1ef14-172">W **dane logowania użytkownika domyślne** zaznacz **SmarterU** kartę.</span><span class="sxs-lookup"><span data-stu-id="1ef14-172">In the **User Default Login** section, select the **SmarterU** tab.</span></span>
  
      <span data-ttu-id="1ef14-173">d.</span><span class="sxs-lookup"><span data-stu-id="1ef14-173">d.</span></span> <span data-ttu-id="1ef14-174">Wybierz **włączyć usługi Okta**.</span><span class="sxs-lookup"><span data-stu-id="1ef14-174">Select **Enable Okta**.</span></span>
  
      <span data-ttu-id="1ef14-175">e.</span><span class="sxs-lookup"><span data-stu-id="1ef14-175">e.</span></span> <span data-ttu-id="1ef14-176">Skopiuj zawartość pliku metadanych pobranych, a następnie wklej go do **metadanych usługi Okta** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="1ef14-176">Copy the content of the downloaded metadata file, and then paste it into the **Okta Metadata** textbox.</span></span>
  
      <span data-ttu-id="1ef14-177">f.</span><span class="sxs-lookup"><span data-stu-id="1ef14-177">f.</span></span> <span data-ttu-id="1ef14-178">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="1ef14-178">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="1ef14-179">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="1ef14-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1ef14-180">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="1ef14-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1ef14-181">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1ef14-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1ef14-182">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ef14-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="1ef14-183">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="1ef14-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="1ef14-185">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="1ef14-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1ef14-186">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="1ef14-186">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-smarteru-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1ef14-188">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="1ef14-188">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-smarteru-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1ef14-190">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1ef14-190">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-smarteru-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1ef14-192">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="1ef14-192">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-smarteru-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1ef14-194">a.</span><span class="sxs-lookup"><span data-stu-id="1ef14-194">a.</span></span> <span data-ttu-id="1ef14-195">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1ef14-195">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1ef14-196">b.</span><span class="sxs-lookup"><span data-stu-id="1ef14-196">b.</span></span> <span data-ttu-id="1ef14-197">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1ef14-197">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1ef14-198">c.</span><span class="sxs-lookup"><span data-stu-id="1ef14-198">c.</span></span> <span data-ttu-id="1ef14-199">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="1ef14-199">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1ef14-200">d.</span><span class="sxs-lookup"><span data-stu-id="1ef14-200">d.</span></span> <span data-ttu-id="1ef14-201">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="1ef14-201">Click **Create**.</span></span>
 
### <a name="creating-a-smarteru-test-user"></a><span data-ttu-id="1ef14-202">Tworzenie użytkownika testowego SmarterU</span><span class="sxs-lookup"><span data-stu-id="1ef14-202">Creating a SmarterU test user</span></span>

<span data-ttu-id="1ef14-203">Aby umożliwić użytkownikom usługi Azure AD zalogować się do SmarterU, musi być przygotowana do SmarterU.</span><span class="sxs-lookup"><span data-stu-id="1ef14-203">To enable Azure AD users to log in to SmarterU, they must be provisioned into SmarterU.</span></span>

<span data-ttu-id="1ef14-204">Gdy SmarterU, inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="1ef14-204">When SmarterU, provisioning is a manual task.</span></span>

<span data-ttu-id="1ef14-205">**Aby udostępnić konta użytkownika, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="1ef14-205">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="1ef14-206">Zaloguj się do Twojego **SmarterU** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="1ef14-206">Log in to your **SmarterU** tenant.</span></span>

2. <span data-ttu-id="1ef14-207">Przejdź do **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="1ef14-207">Go to **Users**.</span></span>

3. <span data-ttu-id="1ef14-208">W sekcji użytkownika wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="1ef14-208">In the user section, perform the following steps:</span></span>
   
    <span data-ttu-id="1ef14-209">![Nowy użytkownik](./media/active-directory-saas-smarteru-tutorial/IC777329.png "nowego użytkownika")</span><span class="sxs-lookup"><span data-stu-id="1ef14-209">![New User](./media/active-directory-saas-smarteru-tutorial/IC777329.png "New User")</span></span>  

    <span data-ttu-id="1ef14-210">a.</span><span class="sxs-lookup"><span data-stu-id="1ef14-210">a.</span></span> <span data-ttu-id="1ef14-211">Kliknij przycisk **+ użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="1ef14-211">Click **+User**.</span></span>
    
    <span data-ttu-id="1ef14-212">b.</span><span class="sxs-lookup"><span data-stu-id="1ef14-212">b.</span></span> <span data-ttu-id="1ef14-213">Wpisz wartości powiązany z atrybutem konto użytkownika usługi Azure AD w następujących pól tekstowych: **podstawowemu adresowi E-mail**, **identyfikator**, **hasło**, **Sprawdź Hasło**, **imię**, **nazwisko**.</span><span class="sxs-lookup"><span data-stu-id="1ef14-213">Type the related attribute values of the Azure AD user account into the following textboxes: **Primary Email**, **Employee ID**, **Password**, **Verify Password**, **Given Name**, **Surname**.</span></span>
    
    <span data-ttu-id="1ef14-214">c.</span><span class="sxs-lookup"><span data-stu-id="1ef14-214">c.</span></span> <span data-ttu-id="1ef14-215">Kliknij przycisk **Active**.</span><span class="sxs-lookup"><span data-stu-id="1ef14-215">Click **Active**.</span></span> 
    
    <span data-ttu-id="1ef14-216">d.</span><span class="sxs-lookup"><span data-stu-id="1ef14-216">d.</span></span> <span data-ttu-id="1ef14-217">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="1ef14-217">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="1ef14-218">Możesz użyć innych SmarterU użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez SmarterU do kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="1ef14-218">You can use any other SmarterU user account creation tools or APIs provided by SmarterU to provision AAD user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1ef14-219">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ef14-219">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1ef14-220">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu SmarterU.</span><span class="sxs-lookup"><span data-stu-id="1ef14-220">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SmarterU.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="1ef14-222">**Aby przypisać Simona Britta SmarterU, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="1ef14-222">**To assign Britta Simon to SmarterU, perform the following steps:**</span></span>

1. <span data-ttu-id="1ef14-223">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="1ef14-223">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="1ef14-225">Na liście aplikacji zaznacz **SmarterU**.</span><span class="sxs-lookup"><span data-stu-id="1ef14-225">In the applications list, select **SmarterU**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_app.png) 

3. <span data-ttu-id="1ef14-227">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="1ef14-227">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="1ef14-229">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="1ef14-229">Click **Add** button.</span></span> <span data-ttu-id="1ef14-230">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1ef14-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="1ef14-232">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="1ef14-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1ef14-233">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1ef14-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1ef14-234">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1ef14-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1ef14-235">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="1ef14-235">Testing single sign-on</span></span>

<span data-ttu-id="1ef14-236">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="1ef14-236">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
 
<span data-ttu-id="1ef14-237">Po kliknięciu kafelka SmarterU w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji SmarterU.</span><span class="sxs-lookup"><span data-stu-id="1ef14-237">When you click the SmarterU tile in the Access Panel, you should get automatically signed-on to your SmarterU application.</span></span>
<span data-ttu-id="1ef14-238">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1ef14-238">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 


## <a name="additional-resources"></a><span data-ttu-id="1ef14-239">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="1ef14-239">Additional resources</span></span>

* [<span data-ttu-id="1ef14-240">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1ef14-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1ef14-241">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1ef14-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_203.png

