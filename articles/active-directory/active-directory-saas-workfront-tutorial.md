---
title: 'Samouczek: Integracji Azure Active Directory z Workfront | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Workfront."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: aab8bd2f-f9dd-42da-a18e-d707865687d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: f7ba8d4895474de0da0e04da5f31959963ae65ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workfront"></a><span data-ttu-id="fff10-103">Samouczek: Integracji Azure Active Directory z Workfront</span><span class="sxs-lookup"><span data-stu-id="fff10-103">Tutorial: Azure Active Directory integration with Workfront</span></span>

<span data-ttu-id="fff10-104">Z tego samouczka dowiesz się integrowanie Workfront z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fff10-104">In this tutorial, you learn how to integrate Workfront with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fff10-105">Integracja z usługą Azure AD Workfront zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="fff10-105">Integrating Workfront with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="fff10-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Workfront</span><span class="sxs-lookup"><span data-stu-id="fff10-106">You can control in Azure AD who has access to Workfront</span></span>
- <span data-ttu-id="fff10-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Workfront (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="fff10-107">You can enable your users to automatically get signed-on to Workfront (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fff10-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="fff10-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="fff10-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fff10-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fff10-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="fff10-110">Prerequisites</span></span>

<span data-ttu-id="fff10-111">Aby skonfigurować integrację usługi Azure AD z Workfront, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="fff10-111">To configure Azure AD integration with Workfront, you need the following items:</span></span>

- <span data-ttu-id="fff10-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="fff10-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fff10-113">Workfront jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="fff10-113">A Workfront single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fff10-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="fff10-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fff10-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="fff10-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fff10-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="fff10-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fff10-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fff10-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fff10-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="fff10-118">Scenario description</span></span>
<span data-ttu-id="fff10-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="fff10-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fff10-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="fff10-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fff10-121">Dodawanie Workfront z galerii</span><span class="sxs-lookup"><span data-stu-id="fff10-121">Adding Workfront from the gallery</span></span>
2. <span data-ttu-id="fff10-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="fff10-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workfront-from-the-gallery"></a><span data-ttu-id="fff10-123">Dodawanie Workfront z galerii</span><span class="sxs-lookup"><span data-stu-id="fff10-123">Adding Workfront from the gallery</span></span>
<span data-ttu-id="fff10-124">Aby skonfigurować integrację usługi Azure AD Workfront, należy dodać Workfront z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="fff10-124">To configure the integration of Workfront into Azure AD, you need to add Workfront from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="fff10-125">**Aby dodać Workfront z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="fff10-125">**To add Workfront from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="fff10-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="fff10-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="fff10-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="fff10-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="fff10-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="fff10-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="fff10-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="fff10-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="fff10-133">W polu wyszukiwania wpisz **Workfront**.</span><span class="sxs-lookup"><span data-stu-id="fff10-133">In the search box, type **Workfront**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_search.png)

5. <span data-ttu-id="fff10-135">W panelu wyników wybierz **Workfront**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="fff10-135">In the results panel, select **Workfront**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fff10-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="fff10-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fff10-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Workfront na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="fff10-138">In this section, you configure and test Azure AD single sign-on with Workfront based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="fff10-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Workfront jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fff10-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Workfront is to a user in Azure AD.</span></span> <span data-ttu-id="fff10-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Workfront musi się.</span><span class="sxs-lookup"><span data-stu-id="fff10-140">In other words, a link relationship between an Azure AD user and the related user in Workfront needs to be established.</span></span>

<span data-ttu-id="fff10-141">W Workfront, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="fff10-141">In Workfront, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="fff10-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Workfront, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="fff10-142">To configure and test Azure AD single sign-on with Workfront, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="fff10-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="fff10-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="fff10-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="fff10-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fff10-145">**[Tworzenie użytkownika testowego Workfront](#creating-a-workfront-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Workfront połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fff10-145">**[Creating a Workfront test user](#creating-a-workfront-test-user)** - to have a counterpart of Britta Simon in Workfront that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="fff10-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="fff10-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fff10-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="fff10-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fff10-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="fff10-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fff10-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Workfront.</span><span class="sxs-lookup"><span data-stu-id="fff10-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workfront application.</span></span>

<span data-ttu-id="fff10-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Workfront, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="fff10-150">**To configure Azure AD single sign-on with Workfront, perform the following steps:**</span></span>

1. <span data-ttu-id="fff10-151">W portalu Azure na **Workfront** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="fff10-151">In the Azure portal, on the **Workfront** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="fff10-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="fff10-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_samlbase.png)

3. <span data-ttu-id="fff10-155">Na **Workfront domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="fff10-155">On the **Workfront Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_url.png)

    <span data-ttu-id="fff10-157">a.</span><span class="sxs-lookup"><span data-stu-id="fff10-157">a.</span></span> <span data-ttu-id="fff10-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.attask-ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="fff10-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.attask-ondemand.com`</span></span>

    <span data-ttu-id="fff10-159">b.</span><span class="sxs-lookup"><span data-stu-id="fff10-159">b.</span></span> <span data-ttu-id="fff10-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.attasksandbox.com/SAML2`</span><span class="sxs-lookup"><span data-stu-id="fff10-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.attasksandbox.com/SAML2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fff10-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="fff10-161">These values are not real.</span></span> <span data-ttu-id="fff10-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="fff10-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="fff10-163">Skontaktuj się z [zespołem pomocy technicznej klienta Workfront](https://www.workfront.com/contact-us/) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="fff10-163">Contact [Workfront Client support team](https://www.workfront.com/contact-us/) to get these values.</span></span> 
 
4. <span data-ttu-id="fff10-164">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="fff10-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the Certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_certificate.png) 

5. <span data-ttu-id="fff10-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="fff10-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workfront-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fff10-168">Na **konfiguracji Workfront** , kliknij przycisk **skonfigurować Workfront** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="fff10-168">On the **Workfront Configuration** section, click **Configure Workfront** to open **Configure sign-on** window.</span></span> <span data-ttu-id="fff10-169">Kopiuj **Sign-Out adresu URL i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="fff10-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_configure.png) 

7. <span data-ttu-id="fff10-171">Logowanie do witryny firmy Workfront jako administrator.</span><span class="sxs-lookup"><span data-stu-id="fff10-171">Sign-on to your Workfront company site as administrator.</span></span>

8. <span data-ttu-id="fff10-172">Przejdź do **Rejestracja jednokrotna w konfiguracji**.</span><span class="sxs-lookup"><span data-stu-id="fff10-172">Go to **Single Sign On Configuration**.</span></span>

9. <span data-ttu-id="fff10-173">Na **rejestracji jednokrotnej** okna dialogowego, wykonaj następujące czynności</span><span class="sxs-lookup"><span data-stu-id="fff10-173">On the **Single Sign-On** dialog, perform the following steps</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej][23]
   
    <span data-ttu-id="fff10-175">a.</span><span class="sxs-lookup"><span data-stu-id="fff10-175">a.</span></span> <span data-ttu-id="fff10-176">Jako **typu**, wybierz pozycję **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="fff10-176">As **Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="fff10-177">b.</span><span class="sxs-lookup"><span data-stu-id="fff10-177">b.</span></span> <span data-ttu-id="fff10-178">Wybierz **usługi identyfikator dostawcy**.</span><span class="sxs-lookup"><span data-stu-id="fff10-178">Select **Service Provider ID**.</span></span>
   
    <span data-ttu-id="fff10-179">c.</span><span class="sxs-lookup"><span data-stu-id="fff10-179">c.</span></span> <span data-ttu-id="fff10-180">Wklej **SAML pojedynczy znak na adres URL usługi** do **adresu URL logowania do portalu** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="fff10-180">Paste the **SAML Single Sign-On Service URL** into the **Login Portal URL** textbox.</span></span>
   
    <span data-ttu-id="fff10-181">d.</span><span class="sxs-lookup"><span data-stu-id="fff10-181">d.</span></span> <span data-ttu-id="fff10-182">Wklej **pojedynczy adres URL usługi Sign-Out** do **Sign-Out URL** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="fff10-182">Paste **Single Sign-Out Service URL** into the **Sign-Out URL** textbox.</span></span>
   
    <span data-ttu-id="fff10-183">e.</span><span class="sxs-lookup"><span data-stu-id="fff10-183">e.</span></span> <span data-ttu-id="fff10-184">Wklej **Zmień adres URL hasła** do **Zmień adres URL hasła** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="fff10-184">Paste **Change Password URL** into the **Change Password URL** textbox.</span></span>
   
    <span data-ttu-id="fff10-185">f.</span><span class="sxs-lookup"><span data-stu-id="fff10-185">f.</span></span> <span data-ttu-id="fff10-186">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="fff10-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="fff10-187">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="fff10-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="fff10-188">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="fff10-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="fff10-189">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fff10-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fff10-190">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="fff10-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="fff10-191">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="fff10-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="fff10-193">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="fff10-193">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="fff10-194">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="fff10-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-workfront-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fff10-196">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="fff10-196">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-workfront-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fff10-198">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="fff10-198">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-workfront-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fff10-200">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="fff10-200">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-workfront-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fff10-202">a.</span><span class="sxs-lookup"><span data-stu-id="fff10-202">a.</span></span> <span data-ttu-id="fff10-203">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fff10-203">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fff10-204">b.</span><span class="sxs-lookup"><span data-stu-id="fff10-204">b.</span></span> <span data-ttu-id="fff10-205">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="fff10-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fff10-206">c.</span><span class="sxs-lookup"><span data-stu-id="fff10-206">c.</span></span> <span data-ttu-id="fff10-207">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="fff10-207">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="fff10-208">d.</span><span class="sxs-lookup"><span data-stu-id="fff10-208">d.</span></span> <span data-ttu-id="fff10-209">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="fff10-209">Click **Create**.</span></span>
 
### <a name="creating-a-workfront-test-user"></a><span data-ttu-id="fff10-210">Tworzenie użytkownika testowego Workfront</span><span class="sxs-lookup"><span data-stu-id="fff10-210">Creating a Workfront test user</span></span>

<span data-ttu-id="fff10-211">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w Workfront.</span><span class="sxs-lookup"><span data-stu-id="fff10-211">The objective of this section is to create a user called Britta Simon in Workfront.</span></span>

<span data-ttu-id="fff10-212">**Aby utworzyć użytkownika o nazwie Simona Britta w Workfront, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="fff10-212">**To create a user called Britta Simon in Workfront, perform the following steps:**</span></span>

1. <span data-ttu-id="fff10-213">Logowanie się do witryny firmy Workfront jako administrator.</span><span class="sxs-lookup"><span data-stu-id="fff10-213">Sign on to your Workfront company site as administrator.</span></span>
2. <span data-ttu-id="fff10-214">W menu u góry kliknij **osób**.</span><span class="sxs-lookup"><span data-stu-id="fff10-214">In the menu on the top, click **People**.</span></span>
3. <span data-ttu-id="fff10-215">Kliknij przycisk **nowej osoby**.</span><span class="sxs-lookup"><span data-stu-id="fff10-215">Click **New Person**.</span></span> 
4. <span data-ttu-id="fff10-216">W oknie dialogowym nowej osoby wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="fff10-216">On the New Person dialog, perform the following steps:</span></span>
   
    ![Tworzenie użytkownika testowego Workfront][21] 
   
    <span data-ttu-id="fff10-218">a.</span><span class="sxs-lookup"><span data-stu-id="fff10-218">a.</span></span> <span data-ttu-id="fff10-219">W **imię** tekstowym, wpisz "Britta."</span><span class="sxs-lookup"><span data-stu-id="fff10-219">In the **First Name** textbox, type "Britta."</span></span>
   
    <span data-ttu-id="fff10-220">b.</span><span class="sxs-lookup"><span data-stu-id="fff10-220">b.</span></span> <span data-ttu-id="fff10-221">W **nazwisko** tekstowym, wpisz "Simona."</span><span class="sxs-lookup"><span data-stu-id="fff10-221">In the **Last Name** textbox, type "Simon."</span></span>
   
    <span data-ttu-id="fff10-222">c.</span><span class="sxs-lookup"><span data-stu-id="fff10-222">c.</span></span> <span data-ttu-id="fff10-223">W **adres E-mail** tekstowym, wpisz adres e-mail Simona Britta w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fff10-223">In the **Email Address** textbox, type Britta Simon's email address in Azure Active Directory.</span></span>
   
    <span data-ttu-id="fff10-224">d.</span><span class="sxs-lookup"><span data-stu-id="fff10-224">d.</span></span> <span data-ttu-id="fff10-225">Kliknij przycisk **Dodaj osobę**.</span><span class="sxs-lookup"><span data-stu-id="fff10-225">Click **Add Person**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="fff10-226">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="fff10-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="fff10-227">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Workfront.</span><span class="sxs-lookup"><span data-stu-id="fff10-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workfront.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="fff10-229">**Aby przypisać Simona Britta Workfront, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="fff10-229">**To assign Britta Simon to Workfront, perform the following steps:**</span></span>

1. <span data-ttu-id="fff10-230">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="fff10-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="fff10-232">Na liście aplikacji zaznacz **Workfront**.</span><span class="sxs-lookup"><span data-stu-id="fff10-232">In the applications list, select **Workfront**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_app.png) 

3. <span data-ttu-id="fff10-234">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="fff10-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="fff10-236">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="fff10-236">Click **Add** button.</span></span> <span data-ttu-id="fff10-237">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="fff10-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="fff10-239">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="fff10-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="fff10-240">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="fff10-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fff10-241">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="fff10-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fff10-242">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="fff10-242">Testing single sign-on</span></span>

<span data-ttu-id="fff10-243">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="fff10-243">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="fff10-244">Po kliknięciu kafelka Workfront w panelu dostępu, należy pobrać strony logowania Workfront aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fff10-244">When you click the Workfront tile in the Access Panel, you should get login page of Workfront application.</span></span>
<span data-ttu-id="fff10-245">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fff10-245">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="fff10-246">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="fff10-246">Additional resources</span></span>

* [<span data-ttu-id="fff10-247">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fff10-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fff10-248">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fff10-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_04.png
[21]:./media/active-directory-saas-workfront-tutorial/tutorial_attask_08.png
[23]:./media/active-directory-saas-workfront-tutorial/tutorial_attask_06.png
[100]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_203.png

