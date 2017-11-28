---
title: 'Samouczek: Integracji Azure Active Directory z kanwy Lms | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i LMS kanwy."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bfed291c-a33e-410d-b919-5b965a631d45
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: jeedes
ms.openlocfilehash: 2212b7a81b66d1afd1aa78d1487b07b6d7b84129
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-canvas-lms"></a><span data-ttu-id="6b9e4-103">Samouczek: Integracji Azure Active Directory z LMS kanwy</span><span class="sxs-lookup"><span data-stu-id="6b9e4-103">Tutorial: Azure Active Directory integration with Canvas LMS</span></span>

<span data-ttu-id="6b9e4-104">Z tego samouczka dowiesz się sposobu integracji z usługą Azure Active Directory (Azure AD) kanwy.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-104">In this tutorial, you learn how to integrate Canvas with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6b9e4-105">Integracja z usługą Azure AD kanwy zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="6b9e4-105">Integrating Canvas with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6b9e4-106">Można kontrolować w usłudze Azure AD, który ma dostęp do kanwy</span><span class="sxs-lookup"><span data-stu-id="6b9e4-106">You can control in Azure AD who has access to Canvas</span></span>
- <span data-ttu-id="6b9e4-107">Umożliwia użytkownikom automatycznie pobrać zalogowane kanwy (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6b9e4-107">You can enable your users to automatically get signed-on to Canvas (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6b9e4-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="6b9e4-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6b9e4-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6b9e4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6b9e4-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6b9e4-110">Prerequisites</span></span>

<span data-ttu-id="6b9e4-111">Aby skonfigurować integrację usługi Azure AD z kanwy, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="6b9e4-111">To configure Azure AD integration with Canvas, you need the following items:</span></span>

- <span data-ttu-id="6b9e4-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6b9e4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6b9e4-113">Kanwy jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="6b9e4-113">A Canvas single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6b9e4-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6b9e4-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="6b9e4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6b9e4-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6b9e4-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6b9e4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6b9e4-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="6b9e4-118">Scenario description</span></span>
<span data-ttu-id="6b9e4-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6b9e4-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="6b9e4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6b9e4-121">Dodanie obszaru roboczego z galerii</span><span class="sxs-lookup"><span data-stu-id="6b9e4-121">Adding Canvas from the gallery</span></span>
2. <span data-ttu-id="6b9e4-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="6b9e4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-canvas-from-the-gallery"></a><span data-ttu-id="6b9e4-123">Dodanie obszaru roboczego z galerii</span><span class="sxs-lookup"><span data-stu-id="6b9e4-123">Adding Canvas from the gallery</span></span>
<span data-ttu-id="6b9e4-124">Aby skonfigurować integrację usługi Azure AD kanwy, należy dodać kanwy z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-124">To configure the integration of Canvas into Azure AD, you need to add Canvas from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6b9e4-125">**Aby dodać kanwy z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="6b9e4-125">**To add Canvas from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6b9e4-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="6b9e4-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6b9e4-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="6b9e4-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="6b9e4-133">W polu wyszukiwania wpisz **kanwy**.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-133">In the search box, type **Canvas**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_search.png)

5. <span data-ttu-id="6b9e4-135">W panelu wyników wybierz **kanwy**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-135">In the results panel, select **Canvas**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6b9e4-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="6b9e4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6b9e4-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej kanwy oparte na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="6b9e4-138">In this section, you configure and test Azure AD single sign-on with Canvas based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6b9e4-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednikiem kanwie jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Canvas is to a user in Azure AD.</span></span> <span data-ttu-id="6b9e4-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i danemu użytkownikowi kanwie musi określone.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-140">In other words, a link relationship between an Azure AD user and the related user in Canvas needs to be established.</span></span>

<span data-ttu-id="6b9e4-141">W obszarze roboczym należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-141">In Canvas, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6b9e4-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z kanwy, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="6b9e4-142">To configure and test Azure AD single sign-on with Canvas, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6b9e4-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6b9e4-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6b9e4-145">**[Tworzenie użytkownika testowego kanwy](#creating-a-canvas-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta kanwy, która jest połączona z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-145">**[Creating a Canvas test user](#creating-a-canvas-test-user)** - to have a counterpart of Britta Simon in Canvas that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6b9e4-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6b9e4-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6b9e4-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="6b9e4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6b9e4-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji kanwy.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Canvas application.</span></span>

<span data-ttu-id="6b9e4-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z kanwy, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="6b9e4-150">**To configure Azure AD single sign-on with Canvas, perform the following steps:**</span></span>

1. <span data-ttu-id="6b9e4-151">W portalu Azure na **kanwy** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-151">In the Azure portal, on the **Canvas** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="6b9e4-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_samlbase.png)

3. <span data-ttu-id="6b9e4-155">Na **kanwy domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6b9e4-155">On the **Canvas Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_url.png)

    <span data-ttu-id="6b9e4-157">a.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-157">a.</span></span> <span data-ttu-id="6b9e4-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<tenant-name>.instructure.com`</span><span class="sxs-lookup"><span data-stu-id="6b9e4-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.instructure.com`</span></span>

    <span data-ttu-id="6b9e4-159">b.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-159">b.</span></span> <span data-ttu-id="6b9e4-160">W **identyfikator** tekstowym, wpisz wartość, przy użyciu następującego wzorca:`https://<tenant-name>.instructure.com/saml2`</span><span class="sxs-lookup"><span data-stu-id="6b9e4-160">In the **Identifier** textbox, type the value using the following pattern: `https://<tenant-name>.instructure.com/saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6b9e4-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-161">These values are not real.</span></span> <span data-ttu-id="6b9e4-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="6b9e4-163">Skontaktuj się z [zespołem pomocy technicznej klienta kanwy](https://community.canvaslms.com/community/help) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-163">Contact [Canvas Client support team](https://community.canvaslms.com/community/help) to get these values.</span></span> 
 
4. <span data-ttu-id="6b9e4-164">Na **certyfikat podpisywania SAML** sekcji, skopiuj **odcisk PALCA** wartości certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_certificate.png) 

5. <span data-ttu-id="6b9e4-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6b9e4-168">Na **konfiguracji kanwy** , kliknij przycisk **skonfigurować kanwy** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-168">On the **Canvas Configuration** section, click **Configure Canvas** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6b9e4-169">Kopiuj **Zmień adres URL hasła, adres URL Sign-Out identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="6b9e4-169">Copy the **Change Password URL, Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_configure.png) 
 
7. <span data-ttu-id="6b9e4-171">W oknie przeglądarki innej witryny sieci web należy zalogować się jako administrator do witryny firmy kanwy.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-171">In a different web browser window, log in to your Canvas company site as an administrator.</span></span>

8. <span data-ttu-id="6b9e4-172">Przejdź do **kursów \> zarządzanych kont \> Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-172">Go to **Courses \> Managed Accounts \> Microsoft**.</span></span>
   
    <span data-ttu-id="6b9e4-173">![Kanwy](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "kanwy")</span><span class="sxs-lookup"><span data-stu-id="6b9e4-173">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span></span>

9. <span data-ttu-id="6b9e4-174">W okienku nawigacji po lewej stronie wybierz **uwierzytelniania**, a następnie kliknij przycisk **dodać nowej konfiguracji SAML**.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-174">In the navigation pane on the left, select **Authentication**, and then click **Add New SAML Config**.</span></span>
   
    <span data-ttu-id="6b9e4-175">![Uwierzytelnianie](./media/active-directory-saas-canvas-lms-tutorial/IC775991.png "uwierzytelniania")</span><span class="sxs-lookup"><span data-stu-id="6b9e4-175">![Authentication](./media/active-directory-saas-canvas-lms-tutorial/IC775991.png "Authentication")</span></span>

10. <span data-ttu-id="6b9e4-176">Na stronie bieżącego integracji wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6b9e4-176">On the Current Integration page, perform the following steps:</span></span>
   
    <span data-ttu-id="6b9e4-177">![Integracja z bieżącym](./media/active-directory-saas-canvas-lms-tutorial/IC775992.png "bieżącego integracji")</span><span class="sxs-lookup"><span data-stu-id="6b9e4-177">![Current Integration](./media/active-directory-saas-canvas-lms-tutorial/IC775992.png "Current Integration")</span></span>

    <span data-ttu-id="6b9e4-178">a.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-178">a.</span></span> <span data-ttu-id="6b9e4-179">W **identyfikator jednostki IdP** pole tekstowe, Wklej wartość **identyfikator jednostki SAML** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-179">In **IdP Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="6b9e4-180">b.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-180">b.</span></span> <span data-ttu-id="6b9e4-181">W **dziennika na adres URL** pole tekstowe, Wklej wartość **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-181">In **Log On URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal .</span></span>

    <span data-ttu-id="6b9e4-182">c.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-182">c.</span></span> <span data-ttu-id="6b9e4-183">W **adresu URL wylogowania** pole tekstowe, Wklej wartość **Sign-Out URL** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-183">In **Log Out URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="6b9e4-184">d.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-184">d.</span></span> <span data-ttu-id="6b9e4-185">W **łącze Zmień hasło** pole tekstowe, Wklej wartość **Zmień adres URL hasła** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-185">In **Change Password Link** textbox, paste the value of **Change Password URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="6b9e4-186">e.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-186">e.</span></span> <span data-ttu-id="6b9e4-187">W **odcisk palca certyfikatu** pole tekstowe, Wklej **odcisk palca** wartość certyfikatów, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-187">In **Certificate Fingerprint** textbox, paste the **Thumbprint** value of certificate which you have copied from Azure portal.</span></span>      
        
    <span data-ttu-id="6b9e4-188">f.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-188">f.</span></span> <span data-ttu-id="6b9e4-189">Z **atrybutu logowania** listy, wybierz **NameID**.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-189">From the **Login Attribute** list, select **NameID**.</span></span>

    <span data-ttu-id="6b9e4-190">g.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-190">g.</span></span> <span data-ttu-id="6b9e4-191">Z **Format identyfikatora** listy, wybierz **emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-191">From the **Identifier Format** list, select **emailAddress**.</span></span>

    <span data-ttu-id="6b9e4-192">h.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-192">h.</span></span> <span data-ttu-id="6b9e4-193">Kliknij przycisk **Zapisz ustawienia uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-193">Click **Save Authentication Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="6b9e4-194">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="6b9e4-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6b9e4-195">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6b9e4-196">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6b9e4-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6b9e4-197">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6b9e4-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="6b9e4-198">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="6b9e4-200">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="6b9e4-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6b9e4-201">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6b9e4-203">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6b9e4-205">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6b9e4-207">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6b9e4-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6b9e4-209">a.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-209">a.</span></span> <span data-ttu-id="6b9e4-210">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6b9e4-211">b.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-211">b.</span></span> <span data-ttu-id="6b9e4-212">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6b9e4-213">c.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-213">c.</span></span> <span data-ttu-id="6b9e4-214">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6b9e4-215">d.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-215">d.</span></span> <span data-ttu-id="6b9e4-216">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-216">Click **Create**.</span></span>
 
### <a name="creating-a-canvas-test-user"></a><span data-ttu-id="6b9e4-217">Tworzenie użytkownika testowego kanwy</span><span class="sxs-lookup"><span data-stu-id="6b9e4-217">Creating a Canvas test user</span></span>

<span data-ttu-id="6b9e4-218">Aby umożliwić użytkownikom usługi Azure AD zalogować się do kanwy, muszą mieć przydzielone do kanwy.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-218">To enable Azure AD users to log in to Canvas, they must be provisioned into Canvas.</span></span>

<span data-ttu-id="6b9e4-219">W przypadku kanwy Inicjowanie obsługi użytkowników jest zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-219">In case of Canvas, user provisioning is a manual task.</span></span>

<span data-ttu-id="6b9e4-220">**Aby udostępnić konta użytkownika, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="6b9e4-220">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="6b9e4-221">Zaloguj się do Twojego **kanwy** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-221">Log in to your **Canvas** tenant.</span></span>

2. <span data-ttu-id="6b9e4-222">Przejdź do **kursów \> zarządzanych kont \> Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-222">Go to **Courses \> Managed Accounts \> Microsoft**.</span></span>
   
   <span data-ttu-id="6b9e4-223">![Kanwy](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "kanwy")</span><span class="sxs-lookup"><span data-stu-id="6b9e4-223">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span></span>

3. <span data-ttu-id="6b9e4-224">Kliknij przycisk **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-224">Click **Users**.</span></span>
   
   <span data-ttu-id="6b9e4-225">![Użytkownicy](./media/active-directory-saas-canvas-lms-tutorial/IC775995.png "użytkowników")</span><span class="sxs-lookup"><span data-stu-id="6b9e4-225">![Users](./media/active-directory-saas-canvas-lms-tutorial/IC775995.png "Users")</span></span>

4. <span data-ttu-id="6b9e4-226">Kliknij przycisk **Dodaj nowego użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-226">Click **Add New User**.</span></span>
   
   <span data-ttu-id="6b9e4-227">![Użytkownicy](./media/active-directory-saas-canvas-lms-tutorial/IC775996.png "użytkowników")</span><span class="sxs-lookup"><span data-stu-id="6b9e4-227">![Users](./media/active-directory-saas-canvas-lms-tutorial/IC775996.png "Users")</span></span>

5. <span data-ttu-id="6b9e4-228">Na stronie Dodawanie nowego użytkownika okna dialogowego wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6b9e4-228">On the Add a New User dialog page, perform the following steps:</span></span>
   
   <span data-ttu-id="6b9e4-229">![Dodaj użytkownika](./media/active-directory-saas-canvas-lms-tutorial/IC775997.png "Dodaj użytkownika")</span><span class="sxs-lookup"><span data-stu-id="6b9e4-229">![Add User](./media/active-directory-saas-canvas-lms-tutorial/IC775997.png "Add User")</span></span>
   
   <span data-ttu-id="6b9e4-230">a.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-230">a.</span></span> <span data-ttu-id="6b9e4-231">W **imię i nazwisko** pole tekstowe, wprowadź nazwę użytkownika, takich jak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-231">In the **Full Name** textbox, enter the name of user like **BrittaSimon**.</span></span>

   <span data-ttu-id="6b9e4-232">b.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-232">b.</span></span> <span data-ttu-id="6b9e4-233">W **E-mail** pole tekstowe, wprowadź adres e-mail użytkownika, takich jak  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="6b9e4-233">In the **Email** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

   <span data-ttu-id="6b9e4-234">c.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-234">c.</span></span> <span data-ttu-id="6b9e4-235">W **logowania** pole tekstowe, wprowadź adres e-mail użytkownika usługi Azure AD takich jak  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="6b9e4-235">In the **Login** textbox, enter the user’s Azure AD email address like **brittasimon@contoso.com**.</span></span>

   <span data-ttu-id="6b9e4-236">d.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-236">d.</span></span> <span data-ttu-id="6b9e4-237">Wybierz **użytkownika o tworzeniu tego konta E-mail**.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-237">Select **Email the user about this account creation**.</span></span>

   <span data-ttu-id="6b9e4-238">e.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-238">e.</span></span> <span data-ttu-id="6b9e4-239">Kliknij przycisk **dodać użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-239">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="6b9e4-240">Możesz użyć innych kanwy użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez kanwy do kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-240">You can use any other Canvas user account creation tools or APIs provided by Canvas to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6b9e4-241">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6b9e4-241">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6b9e4-242">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-242">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Canvas.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="6b9e4-244">**Aby przypisać Simona Britta do kanwy, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="6b9e4-244">**To assign Britta Simon to Canvas, perform the following steps:**</span></span>

1. <span data-ttu-id="6b9e4-245">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-245">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="6b9e4-247">Na liście aplikacji zaznacz **kanwy**.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-247">In the applications list, select **Canvas**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_app.png) 

3. <span data-ttu-id="6b9e4-249">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-249">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="6b9e4-251">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-251">Click **Add** button.</span></span> <span data-ttu-id="6b9e4-252">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="6b9e4-254">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-254">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6b9e4-255">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6b9e4-256">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6b9e4-257">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="6b9e4-257">Testing single sign-on</span></span>

<span data-ttu-id="6b9e4-258">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-258">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6b9e4-259">Po kliknięciu kafelka kanwy w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do obszaru roboczego aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6b9e4-259">When you click the Canvas tile in the Access Panel, you should get automatically signed-on to your Canvas application.</span></span>
<span data-ttu-id="6b9e4-260">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6b9e4-260">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6b9e4-261">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="6b9e4-261">Additional resources</span></span>

* [<span data-ttu-id="6b9e4-262">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6b9e4-262">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6b9e4-263">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6b9e4-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_203.png

