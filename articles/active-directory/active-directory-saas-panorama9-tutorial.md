---
title: 'Samouczek: Integracji Azure Active Directory z Panorama9 | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Panorama9."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5e28d7fa-03be-49f3-96c8-b567f1257d44
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 934c0743464fd32398071aa3d07f7af76fdf7e3b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-panorama9"></a><span data-ttu-id="01139-103">Samouczek: Integracji Azure Active Directory z Panorama9</span><span class="sxs-lookup"><span data-stu-id="01139-103">Tutorial: Azure Active Directory integration with Panorama9</span></span>

<span data-ttu-id="01139-104">Z tego samouczka dowiesz się integrowanie Panorama9 z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="01139-104">In this tutorial, you learn how to integrate Panorama9 with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="01139-105">Integracja z usługą Azure AD Panorama9 zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="01139-105">Integrating Panorama9 with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="01139-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Panorama9</span><span class="sxs-lookup"><span data-stu-id="01139-106">You can control in Azure AD who has access to Panorama9</span></span>
- <span data-ttu-id="01139-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Panorama9 (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="01139-107">You can enable your users to automatically get signed-on to Panorama9 (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="01139-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="01139-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="01139-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="01139-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="01139-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="01139-110">Prerequisites</span></span>

<span data-ttu-id="01139-111">Aby skonfigurować integrację usługi Azure AD z Panorama9, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="01139-111">To configure Azure AD integration with Panorama9, you need the following items:</span></span>

- <span data-ttu-id="01139-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="01139-112">An Azure AD subscription</span></span>
- <span data-ttu-id="01139-113">Panorama9 logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="01139-113">A Panorama9 single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="01139-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="01139-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="01139-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="01139-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="01139-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="01139-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="01139-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="01139-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="01139-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="01139-118">Scenario description</span></span>
<span data-ttu-id="01139-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="01139-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="01139-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="01139-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="01139-121">Dodawanie Panorama9 z galerii</span><span class="sxs-lookup"><span data-stu-id="01139-121">Adding Panorama9 from the gallery</span></span>
2. <span data-ttu-id="01139-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="01139-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-panorama9-from-the-gallery"></a><span data-ttu-id="01139-123">Dodawanie Panorama9 z galerii</span><span class="sxs-lookup"><span data-stu-id="01139-123">Adding Panorama9 from the gallery</span></span>
<span data-ttu-id="01139-124">Aby skonfigurować integrację usługi Azure AD Panorama9, należy dodać Panorama9 z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="01139-124">To configure the integration of Panorama9 into Azure AD, you need to add Panorama9 from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="01139-125">**Aby dodać Panorama9 z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="01139-125">**To add Panorama9 from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="01139-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="01139-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="01139-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="01139-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="01139-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="01139-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="01139-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="01139-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="01139-133">W polu wyszukiwania wpisz **Panorama9**.</span><span class="sxs-lookup"><span data-stu-id="01139-133">In the search box, type **Panorama9**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_search.png)

5. <span data-ttu-id="01139-135">W panelu wyników wybierz **Panorama9**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="01139-135">In the results panel, select **Panorama9**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="01139-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="01139-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="01139-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Panorama9 na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="01139-138">In this section, you configure and test Azure AD single sign-on with Panorama9 based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="01139-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Panorama9 jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="01139-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Panorama9 is to a user in Azure AD.</span></span> <span data-ttu-id="01139-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Panorama9 musi się.</span><span class="sxs-lookup"><span data-stu-id="01139-140">In other words, a link relationship between an Azure AD user and the related user in Panorama9 needs to be established.</span></span>

<span data-ttu-id="01139-141">W Panorama9, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="01139-141">In Panorama9, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="01139-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Panorama9, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="01139-142">To configure and test Azure AD single sign-on with Panorama9, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="01139-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="01139-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="01139-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="01139-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="01139-145">**[Tworzenie użytkownika testowego Panorama9](#creating-a-panorama9-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Panorama9 połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="01139-145">**[Creating a Panorama9 test user](#creating-a-panorama9-test-user)** - to have a counterpart of Britta Simon in Panorama9 that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="01139-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="01139-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="01139-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="01139-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="01139-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="01139-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="01139-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Panorama9.</span><span class="sxs-lookup"><span data-stu-id="01139-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Panorama9 application.</span></span>

<span data-ttu-id="01139-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Panorama9, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="01139-150">**To configure Azure AD single sign-on with Panorama9, perform the following steps:**</span></span>

1. <span data-ttu-id="01139-151">W portalu Azure na **Panorama9** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="01139-151">In the Azure portal, on the **Panorama9** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="01139-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="01139-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_samlbase.png)

3. <span data-ttu-id="01139-155">Na **Panorama9 domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="01139-155">On the **Panorama9 Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_url.png)

    <span data-ttu-id="01139-157">a.</span><span class="sxs-lookup"><span data-stu-id="01139-157">a.</span></span> <span data-ttu-id="01139-158">W **adres URL logowania** tekstowym, wpisz adres URL jako:`https://dashboard.panorama9.com/saml/access/3262`</span><span class="sxs-lookup"><span data-stu-id="01139-158">In the **Sign-on URL** textbox, type a URL as: `https://dashboard.panorama9.com/saml/access/3262`</span></span>

    <span data-ttu-id="01139-159">b.</span><span class="sxs-lookup"><span data-stu-id="01139-159">b.</span></span> <span data-ttu-id="01139-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`http://www.panorama9.com/saml20/<tenant-name>`</span><span class="sxs-lookup"><span data-stu-id="01139-160">In the **Identifier** textbox, type a URL using the following pattern: `http://www.panorama9.com/saml20/<tenant-name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="01139-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="01139-161">These values are not real.</span></span> <span data-ttu-id="01139-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="01139-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="01139-163">Skontaktuj się z [zespołem pomocy technicznej klienta Panorama9](https://support.panorama9.com) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="01139-163">Contact [Panorama9 Client support team](https://support.panorama9.com) to get these values.</span></span> 
 
4. <span data-ttu-id="01139-164">Na **certyfikat podpisywania SAML** sekcji, skopiuj **odcisk PALCA** wartości certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="01139-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_certificate.png) 

5. <span data-ttu-id="01139-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="01139-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-panorama9-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="01139-168">Na **konfiguracji Panorama9** , kliknij przycisk **skonfigurować Panorama9** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="01139-168">On the **Panorama9 Configuration** section, click **Configure Panorama9** to open **Configure sign-on** window.</span></span> <span data-ttu-id="01139-169">Kopiuj **SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="01139-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_configure.png) 

5. <span data-ttu-id="01139-171">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy Panorama9 jako administrator.</span><span class="sxs-lookup"><span data-stu-id="01139-171">In a different web browser window, log into your Panorama9 company site as an administrator.</span></span>

6. <span data-ttu-id="01139-172">Na pasku narzędzi u góry kliknij **Zarządzaj**, a następnie kliknij przycisk **rozszerzenia**.</span><span class="sxs-lookup"><span data-stu-id="01139-172">In the toolbar on the top, click **Manage**, and then click **Extensions**.</span></span>
   
   <span data-ttu-id="01139-173">![Rozszerzenia](./media/active-directory-saas-panorama9-tutorial/ic790023.png "rozszerzeń")</span><span class="sxs-lookup"><span data-stu-id="01139-173">![Extensions](./media/active-directory-saas-panorama9-tutorial/ic790023.png "Extensions")</span></span>
7. <span data-ttu-id="01139-174">Na **rozszerzenia** okna dialogowego, kliknij przycisk **rejestracji jednokrotnej**.</span><span class="sxs-lookup"><span data-stu-id="01139-174">On the **Extensions** dialog, click **Single Sign-On**.</span></span>
   
   <span data-ttu-id="01139-175">![Logowanie jednokrotne](./media/active-directory-saas-panorama9-tutorial/ic790024.png "logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="01139-175">![Single Sign-On](./media/active-directory-saas-panorama9-tutorial/ic790024.png "Single Sign-On")</span></span>
8. <span data-ttu-id="01139-176">W **ustawienia** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="01139-176">In the **Settings** section, perform the following steps:</span></span>
   
   <span data-ttu-id="01139-177">![Ustawienia](./media/active-directory-saas-panorama9-tutorial/ic790025.png "ustawienia")</span><span class="sxs-lookup"><span data-stu-id="01139-177">![Settings](./media/active-directory-saas-panorama9-tutorial/ic790025.png "Settings")</span></span>
   
    <span data-ttu-id="01139-178">a.</span><span class="sxs-lookup"><span data-stu-id="01139-178">a.</span></span> <span data-ttu-id="01139-179">W **adres URL dostawcy tożsamości** pole tekstowe, Wklej wartość **pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="01139-179">In **Identity provider URL** textbox, paste the value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="01139-180">b.</span><span class="sxs-lookup"><span data-stu-id="01139-180">b.</span></span> <span data-ttu-id="01139-181">W **odcisk palca certyfikatu** pole tekstowe, Wklej **odcisk palca** wartość certyfikatów, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="01139-181">In **Certificate fingerprint** textbox, paste the **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>    
         
9. <span data-ttu-id="01139-182">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="01139-182">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="01139-183">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="01139-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="01139-184">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="01139-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="01139-185">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="01139-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="01139-186">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="01139-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="01139-187">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="01139-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="01139-189">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="01139-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="01139-190">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="01139-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-panorama9-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="01139-192">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="01139-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-panorama9-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="01139-194">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="01139-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-panorama9-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="01139-196">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="01139-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-panorama9-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="01139-198">a.</span><span class="sxs-lookup"><span data-stu-id="01139-198">a.</span></span> <span data-ttu-id="01139-199">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="01139-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="01139-200">b.</span><span class="sxs-lookup"><span data-stu-id="01139-200">b.</span></span> <span data-ttu-id="01139-201">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="01139-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="01139-202">c.</span><span class="sxs-lookup"><span data-stu-id="01139-202">c.</span></span> <span data-ttu-id="01139-203">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="01139-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="01139-204">d.</span><span class="sxs-lookup"><span data-stu-id="01139-204">d.</span></span> <span data-ttu-id="01139-205">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="01139-205">Click **Create**.</span></span>
 
### <a name="creating-a-panorama9-test-user"></a><span data-ttu-id="01139-206">Tworzenie użytkownika testowego Panorama9</span><span class="sxs-lookup"><span data-stu-id="01139-206">Creating a Panorama9 test user</span></span>

<span data-ttu-id="01139-207">Aby włączyć użytkowników usługi Azure AD zalogować się do Panorama9, musi być przygotowana do Panorama9.</span><span class="sxs-lookup"><span data-stu-id="01139-207">In order to enable Azure AD users to log into Panorama9, they must be provisioned into Panorama9.</span></span>  

<span data-ttu-id="01139-208">W przypadku Panorama9 Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="01139-208">In the case of Panorama9, provisioning is a manual task.</span></span>

<span data-ttu-id="01139-209">**Aby skonfigurować, inicjowanie obsługi użytkowników, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="01139-209">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="01139-210">Zaloguj się do Twojego **Panorama9** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="01139-210">Log in to your **Panorama9** company site as an administrator.</span></span>

2. <span data-ttu-id="01139-211">W menu u góry kliknij **Zarządzaj**, a następnie kliknij przycisk **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="01139-211">In the menu on the top, click **Manage**, and then click **Users**.</span></span>
   
  <span data-ttu-id="01139-212">![Użytkownicy](./media/active-directory-saas-panorama9-tutorial/ic790027.png "użytkowników")</span><span class="sxs-lookup"><span data-stu-id="01139-212">![Users](./media/active-directory-saas-panorama9-tutorial/ic790027.png "Users")</span></span>

3. <span data-ttu-id="01139-213">W sekcji Użytkownicy kliknij  **+**  można dodać nowego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="01139-213">In the Users section, Click **+** to add new user.</span></span>

 <span data-ttu-id="01139-214">![Użytkownicy](./media/active-directory-saas-panorama9-tutorial/ic790028.png "użytkowników")</span><span class="sxs-lookup"><span data-stu-id="01139-214">![Users](./media/active-directory-saas-panorama9-tutorial/ic790028.png "Users")</span></span>

4. <span data-ttu-id="01139-215">Przejdź do sekcji danych użytkownika, wpisz adres e-mail chcesz udostępnić w prawidłowym użytkownikiem usługi Azure Active Directory **E-mail** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="01139-215">Go to the User data section, type the email address of a valid Azure Active Directory user you want to provision into the **Email** textbox.</span></span>

5. <span data-ttu-id="01139-216">Się w sekcji Użytkownicy kliknij **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="01139-216">Come to the Users section, Click **Save**.</span></span>
   
> [!NOTE]
    > <span data-ttu-id="01139-217">Właściciel konta usługi Azure Active Directory otrzymuje wiadomość e-mail i następuje łącze, aby potwierdzić swoje konto, zanim staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="01139-217">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="01139-218">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="01139-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="01139-219">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Panorama9.</span><span class="sxs-lookup"><span data-stu-id="01139-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Panorama9.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="01139-221">**Aby przypisać Simona Britta Panorama9, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="01139-221">**To assign Britta Simon to Panorama9, perform the following steps:**</span></span>

1. <span data-ttu-id="01139-222">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="01139-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="01139-224">Na liście aplikacji zaznacz **Panorama9**.</span><span class="sxs-lookup"><span data-stu-id="01139-224">In the applications list, select **Panorama9**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_app.png) 

3. <span data-ttu-id="01139-226">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="01139-226">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="01139-228">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="01139-228">Click **Add** button.</span></span> <span data-ttu-id="01139-229">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="01139-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="01139-231">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="01139-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="01139-232">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="01139-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="01139-233">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="01139-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="01139-234">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="01139-234">Testing single sign-on</span></span>

<span data-ttu-id="01139-235">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="01139-235">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="01139-236">Po kliknięciu kafelka Panorama9 w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane Panorama9 aplikacji.</span><span class="sxs-lookup"><span data-stu-id="01139-236">When you click the Panorama9 tile in the Access Panel, you should get automatically signed-on to Panorama9 application.</span></span>
<span data-ttu-id="01139-237">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="01139-237">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="01139-238">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="01139-238">Additional resources</span></span>

* [<span data-ttu-id="01139-239">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="01139-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="01139-240">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="01139-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_203.png

