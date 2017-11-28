---
title: 'Samouczek: Integracji Azure Active Directory z ITRP | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i ITRP."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e09716a3-4200-4853-9414-2390e6c10d98
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: fae1c7b6b0e04c1e23123d3aee7913cb3131e645
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-itrp"></a><span data-ttu-id="c98ab-103">Samouczek: Integracji Azure Active Directory z ITRP</span><span class="sxs-lookup"><span data-stu-id="c98ab-103">Tutorial: Azure Active Directory integration with ITRP</span></span>

<span data-ttu-id="c98ab-104">Z tego samouczka dowiesz się integrowanie ITRP z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c98ab-104">In this tutorial, you learn how to integrate ITRP with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c98ab-105">Integracja z usługą Azure AD ITRP zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="c98ab-105">Integrating ITRP with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c98ab-106">Można kontrolować w usłudze Azure AD, który ma dostęp do ITRP</span><span class="sxs-lookup"><span data-stu-id="c98ab-106">You can control in Azure AD who has access to ITRP</span></span>
- <span data-ttu-id="c98ab-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do ITRP (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c98ab-107">You can enable your users to automatically get signed-on to ITRP (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c98ab-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c98ab-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c98ab-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c98ab-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c98ab-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c98ab-110">Prerequisites</span></span>

<span data-ttu-id="c98ab-111">Aby skonfigurować integrację usługi Azure AD z ITRP, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="c98ab-111">To configure Azure AD integration with ITRP, you need the following items:</span></span>

- <span data-ttu-id="c98ab-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c98ab-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c98ab-113">ITRP logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="c98ab-113">An ITRP single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c98ab-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="c98ab-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c98ab-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="c98ab-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c98ab-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="c98ab-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c98ab-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c98ab-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c98ab-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="c98ab-118">Scenario description</span></span>
<span data-ttu-id="c98ab-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="c98ab-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c98ab-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="c98ab-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c98ab-121">Dodawanie ITRP z galerii</span><span class="sxs-lookup"><span data-stu-id="c98ab-121">Adding ITRP from the gallery</span></span>
2. <span data-ttu-id="c98ab-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="c98ab-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-itrp-from-the-gallery"></a><span data-ttu-id="c98ab-123">Dodawanie ITRP z galerii</span><span class="sxs-lookup"><span data-stu-id="c98ab-123">Adding ITRP from the gallery</span></span>
<span data-ttu-id="c98ab-124">Aby skonfigurować integrację ITRP w usłudze Azure AD, należy dodać ITRP z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="c98ab-124">To configure the integration of ITRP in to Azure AD, you need to add ITRP from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c98ab-125">**Aby dodać ITRP z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c98ab-125">**To add ITRP from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c98ab-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="c98ab-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="c98ab-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="c98ab-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c98ab-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="c98ab-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="c98ab-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c98ab-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="c98ab-133">W polu wyszukiwania wpisz **ITRP**.</span><span class="sxs-lookup"><span data-stu-id="c98ab-133">In the search box, type **ITRP**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_search.png)

5. <span data-ttu-id="c98ab-135">W panelu wyników wybierz **ITRP**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="c98ab-135">In the results panel, select **ITRP**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c98ab-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="c98ab-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="c98ab-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z ITRP na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="c98ab-138">In this section, you configure and test Azure AD single sign-on with ITRP based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c98ab-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w ITRP jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c98ab-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ITRP is to a user in Azure AD.</span></span> <span data-ttu-id="c98ab-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w ITRP musi się.</span><span class="sxs-lookup"><span data-stu-id="c98ab-140">In other words, a link relationship between an Azure AD user and the related user in ITRP needs to be established.</span></span>

<span data-ttu-id="c98ab-141">W ITRP, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="c98ab-141">In ITRP, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c98ab-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z ITRP, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="c98ab-142">To configure and test Azure AD single sign-on with ITRP, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c98ab-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="c98ab-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c98ab-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="c98ab-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c98ab-145">**[Użytkownik testowy tworzenie ITRP](#creating-an-itrp-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta ITRP połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c98ab-145">**[Creating an ITRP test user](#creating-an-itrp-test-user)** - to have a counterpart of Britta Simon in ITRP that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c98ab-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="c98ab-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c98ab-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="c98ab-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c98ab-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="c98ab-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c98ab-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji ITRP.</span><span class="sxs-lookup"><span data-stu-id="c98ab-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ITRP application.</span></span>

<span data-ttu-id="c98ab-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z ITRP, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c98ab-150">**To configure Azure AD single sign-on with ITRP, perform the following steps:**</span></span>

1. <span data-ttu-id="c98ab-151">W portalu Azure na **ITRP** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="c98ab-151">In the Azure portal, on the **ITRP** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="c98ab-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="c98ab-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_samlbase.png)

3. <span data-ttu-id="c98ab-155">Na **ITRP domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c98ab-155">On the **ITRP Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_url.png)

    <span data-ttu-id="c98ab-157">a.</span><span class="sxs-lookup"><span data-stu-id="c98ab-157">a.</span></span> <span data-ttu-id="c98ab-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<tenant-name>.itrp.com`</span><span class="sxs-lookup"><span data-stu-id="c98ab-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.itrp.com`</span></span>

    <span data-ttu-id="c98ab-159">b.</span><span class="sxs-lookup"><span data-stu-id="c98ab-159">b.</span></span> <span data-ttu-id="c98ab-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<tenant-name>.itrp.com`</span><span class="sxs-lookup"><span data-stu-id="c98ab-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenant-name>.itrp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c98ab-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="c98ab-161">These values are not real.</span></span> <span data-ttu-id="c98ab-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="c98ab-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c98ab-163">Skontaktuj się z [zespołem pomocy technicznej klienta ITRP](https://www.itrp.com/support) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="c98ab-163">Contact [ITRP Client support team](https://www.itrp.com/support) to get these values.</span></span> 
 
4. <span data-ttu-id="c98ab-164">Na **certyfikat podpisywania SAML** sekcji, skopiuj **odcisk PALCA** wartości certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="c98ab-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_certificate.png) 

5. <span data-ttu-id="c98ab-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c98ab-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-itrp-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c98ab-168">Na **konfiguracji ITRP** , kliknij przycisk **skonfigurować ITRP** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="c98ab-168">On the **ITRP Configuration** section, click **Configure ITRP** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c98ab-169">Kopiuj **SAML pojedynczy znak na adres URL usługi i adres URL Sign-Out** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="c98ab-169">Copy the **SAML Single Sign-On Service URL and Sign-Out URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_configure.png) 

7. <span data-ttu-id="c98ab-171">W oknie przeglądarki innej witryny sieci web należy zalogować się jako administrator do witryny firmy ITRP.</span><span class="sxs-lookup"><span data-stu-id="c98ab-171">In a different web browser window, log in to your ITRP company site as an administrator.</span></span>

8. <span data-ttu-id="c98ab-172">Na pasku narzędzi u góry kliknij **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="c98ab-172">In the toolbar on the top, click **Settings**.</span></span>
   
    <span data-ttu-id="c98ab-173">![ITRP](./media/active-directory-saas-itrp-tutorial/ic775570.png "ITRP")</span><span class="sxs-lookup"><span data-stu-id="c98ab-173">![ITRP](./media/active-directory-saas-itrp-tutorial/ic775570.png "ITRP")</span></span>

8. <span data-ttu-id="c98ab-174">W lewym okienku nawigacji, wybierz **rejestracji jednokrotnej**.</span><span class="sxs-lookup"><span data-stu-id="c98ab-174">In the left navigation pane, select **Single Sign-On**.</span></span>
   
    <span data-ttu-id="c98ab-175">![Logowanie jednokrotne](./media/active-directory-saas-itrp-tutorial/ic775571.png "logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="c98ab-175">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775571.png "Single Sign-On")</span></span>

9. <span data-ttu-id="c98ab-176">W sekcji konfiguracji logowania jednokrotnego wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c98ab-176">In the Single Sign-On configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="c98ab-177">![Logowanie jednokrotne](./media/active-directory-saas-itrp-tutorial/ic775572.png "logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="c98ab-177">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775572.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="c98ab-178">![Logowanie jednokrotne](./media/active-directory-saas-itrp-tutorial/ic775573.png "logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="c98ab-178">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775573.png "Single Sign-On")</span></span>   

    <span data-ttu-id="c98ab-179">a.</span><span class="sxs-lookup"><span data-stu-id="c98ab-179">a.</span></span> <span data-ttu-id="c98ab-180">Kliknij przycisk **włączyć**.</span><span class="sxs-lookup"><span data-stu-id="c98ab-180">Click **Enable**.</span></span>

    <span data-ttu-id="c98ab-181">b.</span><span class="sxs-lookup"><span data-stu-id="c98ab-181">b.</span></span> <span data-ttu-id="c98ab-182">W **zdalnego adresu URL wylogowania** pole tekstowe, Wklej wartość **Sign-Out URL**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c98ab-182">In **Remote Log Out URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="c98ab-183">c.</span><span class="sxs-lookup"><span data-stu-id="c98ab-183">c.</span></span> <span data-ttu-id="c98ab-184">W **adres URL logowania jednokrotnego SAML** pole tekstowe, Wklej wartość **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c98ab-184">In **SAML SSO URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="c98ab-185">d.In **odcisk palca certyfikatu** pole tekstowe, Wklej **odcisk palca** wartość certyfikatów, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c98ab-185">d.In **Certificate Fingerprint** textbox, paste the **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span> 
      
10. <span data-ttu-id="c98ab-186">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="c98ab-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="c98ab-187">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="c98ab-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c98ab-188">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="c98ab-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c98ab-189">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c98ab-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c98ab-190">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c98ab-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="c98ab-191">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="c98ab-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="c98ab-193">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c98ab-193">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c98ab-194">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="c98ab-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-itrp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c98ab-196">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="c98ab-196">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-itrp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c98ab-198">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c98ab-198">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-itrp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c98ab-200">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c98ab-200">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-itrp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c98ab-202">a.</span><span class="sxs-lookup"><span data-stu-id="c98ab-202">a.</span></span> <span data-ttu-id="c98ab-203">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c98ab-203">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c98ab-204">b.</span><span class="sxs-lookup"><span data-stu-id="c98ab-204">b.</span></span> <span data-ttu-id="c98ab-205">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c98ab-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c98ab-206">c.</span><span class="sxs-lookup"><span data-stu-id="c98ab-206">c.</span></span> <span data-ttu-id="c98ab-207">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="c98ab-207">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c98ab-208">d.</span><span class="sxs-lookup"><span data-stu-id="c98ab-208">d.</span></span> <span data-ttu-id="c98ab-209">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="c98ab-209">Click **Create**.</span></span>
 
### <a name="creating-an-itrp-test-user"></a><span data-ttu-id="c98ab-210">Tworzenie użytkownika testowego ITRP</span><span class="sxs-lookup"><span data-stu-id="c98ab-210">Creating an ITRP test user</span></span>

<span data-ttu-id="c98ab-211">Aby umożliwić użytkownikom usługi Azure AD zalogować się do ITRP, ich należy udostępnić w celu ITRP.</span><span class="sxs-lookup"><span data-stu-id="c98ab-211">To enable Azure AD users to log in to ITRP, they must be provisioned in to ITRP.</span></span>  

<span data-ttu-id="c98ab-212">W przypadku ITRP Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="c98ab-212">In the case of ITRP, provisioning is a manual task.</span></span>

<span data-ttu-id="c98ab-213">**Aby udostępnić konta użytkownika, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c98ab-213">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="c98ab-214">Zaloguj się do Twojego **ITRP** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="c98ab-214">Log in to your **ITRP** tenant.</span></span>

2. <span data-ttu-id="c98ab-215">Na pasku narzędzi u góry kliknij **rekordów**.</span><span class="sxs-lookup"><span data-stu-id="c98ab-215">In the toolbar on the top, click **Records**.</span></span>
   
    <span data-ttu-id="c98ab-216">![Administrator](./media/active-directory-saas-itrp-tutorial/ic775575.png "administratora")</span><span class="sxs-lookup"><span data-stu-id="c98ab-216">![Admin](./media/active-directory-saas-itrp-tutorial/ic775575.png "Admin")</span></span>

3. <span data-ttu-id="c98ab-217">Wybierz z menu podręcznego **osób**.</span><span class="sxs-lookup"><span data-stu-id="c98ab-217">From the popup menu, select **People**.</span></span>
   
    <span data-ttu-id="c98ab-218">![Osoby](./media/active-directory-saas-itrp-tutorial/ic775587.png "osób")</span><span class="sxs-lookup"><span data-stu-id="c98ab-218">![People](./media/active-directory-saas-itrp-tutorial/ic775587.png "People")</span></span>

4. <span data-ttu-id="c98ab-219">Kliknij przycisk **Dodawanie nowej osoby** ("+").</span><span class="sxs-lookup"><span data-stu-id="c98ab-219">Click **Add New Person** (“+”).</span></span>
   
    <span data-ttu-id="c98ab-220">![Administrator](./media/active-directory-saas-itrp-tutorial/ic775576.png "administratora")</span><span class="sxs-lookup"><span data-stu-id="c98ab-220">![Admin](./media/active-directory-saas-itrp-tutorial/ic775576.png "Admin")</span></span>

5. <span data-ttu-id="c98ab-221">W oknie dialogowym Dodawanie nowej osoby wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c98ab-221">On the Add New Person dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="c98ab-222">![Użytkownik](./media/active-directory-saas-itrp-tutorial/ic775577.png "użytkownika")</span><span class="sxs-lookup"><span data-stu-id="c98ab-222">![User](./media/active-directory-saas-itrp-tutorial/ic775577.png "User")</span></span> 
      
    <span data-ttu-id="c98ab-223">a.</span><span class="sxs-lookup"><span data-stu-id="c98ab-223">a.</span></span> <span data-ttu-id="c98ab-224">Typ **nazwa**, **E-mail** chcesz udostępnić poprawnego konta usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="c98ab-224">Type the **Name**, **Email** of a valid AAD account you want to provision.</span></span>

    <span data-ttu-id="c98ab-225">b.</span><span class="sxs-lookup"><span data-stu-id="c98ab-225">b.</span></span> <span data-ttu-id="c98ab-226">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="c98ab-226">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="c98ab-227">Możesz użyć innych ITRP użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez ITRP do kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="c98ab-227">You can use any other ITRP user account creation tools or APIs provided by ITRP to provision AAD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c98ab-228">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c98ab-228">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c98ab-229">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu ITRP.</span><span class="sxs-lookup"><span data-stu-id="c98ab-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ITRP.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="c98ab-231">**Aby przypisać Simona Britta ITRP, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c98ab-231">**To assign Britta Simon to ITRP, perform the following steps:**</span></span>

1. <span data-ttu-id="c98ab-232">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="c98ab-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="c98ab-234">Na liście aplikacji zaznacz **ITRP**.</span><span class="sxs-lookup"><span data-stu-id="c98ab-234">In the applications list, select **ITRP**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_app.png) 

3. <span data-ttu-id="c98ab-236">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="c98ab-236">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="c98ab-238">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c98ab-238">Click **Add** button.</span></span> <span data-ttu-id="c98ab-239">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c98ab-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="c98ab-241">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="c98ab-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c98ab-242">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c98ab-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c98ab-243">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c98ab-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c98ab-244">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="c98ab-244">Testing single sign-on</span></span>

<span data-ttu-id="c98ab-245">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="c98ab-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c98ab-246">Po kliknięciu kafelka ITRP w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji ITRP.</span><span class="sxs-lookup"><span data-stu-id="c98ab-246">When you click the ITRP tile in the Access Panel, you should get automatically signed-on to your ITRP application.</span></span>
<span data-ttu-id="c98ab-247">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c98ab-247">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c98ab-248">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="c98ab-248">Additional resources</span></span>

* [<span data-ttu-id="c98ab-249">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c98ab-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c98ab-250">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c98ab-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_203.png

