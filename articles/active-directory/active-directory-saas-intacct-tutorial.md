---
title: 'Samouczek: Integracji Azure Active Directory z Intacct | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Intacct."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 92518e02-a62c-4b1b-a8e9-2803eb2b49ac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: c203b192b9da0d280cbd7f6c123219242ee4a3d1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intacct"></a><span data-ttu-id="cb509-103">Samouczek: Integracji Azure Active Directory z Intacct</span><span class="sxs-lookup"><span data-stu-id="cb509-103">Tutorial: Azure Active Directory integration with Intacct</span></span>

<span data-ttu-id="cb509-104">Z tego samouczka dowiesz się integrowanie Intacct z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cb509-104">In this tutorial, you learn how to integrate Intacct with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cb509-105">Integracja z usługą Azure AD Intacct zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="cb509-105">Integrating Intacct with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="cb509-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Intacct</span><span class="sxs-lookup"><span data-stu-id="cb509-106">You can control in Azure AD who has access to Intacct</span></span>
- <span data-ttu-id="cb509-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Intacct (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb509-107">You can enable your users to automatically get signed-on to Intacct (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cb509-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="cb509-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="cb509-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cb509-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb509-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="cb509-110">Prerequisites</span></span>

<span data-ttu-id="cb509-111">Aby skonfigurować integrację usługi Azure AD z Intacct, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="cb509-111">To configure Azure AD integration with Intacct, you need the following items:</span></span>

- <span data-ttu-id="cb509-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb509-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cb509-113">Intacct logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="cb509-113">An Intacct single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cb509-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="cb509-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cb509-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="cb509-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cb509-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="cb509-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cb509-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cb509-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cb509-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="cb509-118">Scenario description</span></span>
<span data-ttu-id="cb509-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="cb509-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cb509-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="cb509-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cb509-121">Dodawanie Intacct z galerii</span><span class="sxs-lookup"><span data-stu-id="cb509-121">Adding Intacct from the gallery</span></span>
2. <span data-ttu-id="cb509-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="cb509-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intacct-from-the-gallery"></a><span data-ttu-id="cb509-123">Dodawanie Intacct z galerii</span><span class="sxs-lookup"><span data-stu-id="cb509-123">Adding Intacct from the gallery</span></span>
<span data-ttu-id="cb509-124">Aby skonfigurować integrację usługi Azure AD Intacct, należy dodać Intacct z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="cb509-124">To configure the integration of Intacct into Azure AD, you need to add Intacct from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="cb509-125">**Aby dodać Intacct z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="cb509-125">**To add Intacct from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="cb509-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="cb509-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="cb509-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="cb509-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="cb509-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="cb509-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="cb509-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="cb509-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="cb509-133">W polu wyszukiwania wpisz **Intacct**.</span><span class="sxs-lookup"><span data-stu-id="cb509-133">In the search box, type **Intacct**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_search.png)

5. <span data-ttu-id="cb509-135">W panelu wyników wybierz **Intacct**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="cb509-135">In the results panel, select **Intacct**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cb509-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="cb509-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cb509-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Intacct w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="cb509-138">In this section, you configure and test Azure AD single sign-on with Intacct based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cb509-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Intacct jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cb509-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Intacct is to a user in Azure AD.</span></span> <span data-ttu-id="cb509-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Intacct musi się.</span><span class="sxs-lookup"><span data-stu-id="cb509-140">In other words, a link relationship between an Azure AD user and the related user in Intacct needs to be established.</span></span>

<span data-ttu-id="cb509-141">W Intacct, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="cb509-141">In Intacct, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="cb509-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Intacct, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="cb509-142">To configure and test Azure AD single sign-on with Intacct, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="cb509-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="cb509-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="cb509-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="cb509-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cb509-145">**[Tworzenie użytkownika testowego Intacct](#creating-an-intacct-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Intacct połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cb509-145">**[Creating an Intacct test user](#creating-an-intacct-test-user)** - to have a counterpart of Britta Simon in Intacct that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="cb509-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="cb509-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cb509-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="cb509-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cb509-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="cb509-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cb509-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Intacct.</span><span class="sxs-lookup"><span data-stu-id="cb509-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Intacct application.</span></span>

<span data-ttu-id="cb509-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Intacct, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="cb509-150">**To configure Azure AD single sign-on with Intacct, perform the following steps:**</span></span>

1. <span data-ttu-id="cb509-151">W portalu Azure na **Intacct** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="cb509-151">In the Azure portal, on the **Intacct** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="cb509-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="cb509-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_samlbase.png)

3. <span data-ttu-id="cb509-155">Na **Intacct domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="cb509-155">On the **Intacct Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_url.png)

    <span data-ttu-id="cb509-157">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="cb509-157">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.intacct.com/ia/acct/sso_response.phtml`|
    | `https://www.intacct.com/ia/acct/sso_response.phtml` |

    > [!NOTE] 
    > <span data-ttu-id="cb509-158">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="cb509-158">This value is not real.</span></span> <span data-ttu-id="cb509-159">Zaktualizuj tę wartość przy rzeczywisty adres URL odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="cb509-159">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="cb509-160">Skontaktuj się z [zespołem pomocy technicznej Intacct](https://us.intacct.com/support) aby zyskać tę wartość.</span><span class="sxs-lookup"><span data-stu-id="cb509-160">Contact [Intacct support team](https://us.intacct.com/support) to get this value.</span></span>

4. <span data-ttu-id="cb509-161">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="cb509-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_certificate.png) 

5. <span data-ttu-id="cb509-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="cb509-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-intacct-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cb509-165">Na **konfiguracji Intacct** , kliknij przycisk **skonfigurować Intacct** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="cb509-165">On the **Intacct Configuration** section, click **Configure Intacct** to open **Configure sign-on** window.</span></span> <span data-ttu-id="cb509-166">Kopiuj **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="cb509-166">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_configure.png) 

7. <span data-ttu-id="cb509-168">W oknie przeglądarki innej witryny sieci web należy zalogować się jako administrator do witryny firmy Intacct.</span><span class="sxs-lookup"><span data-stu-id="cb509-168">In a different web browser window, sign in to your Intacct company site as an administrator.</span></span>

8. <span data-ttu-id="cb509-169">Kliknij przycisk **firmy** , a następnie kliknij pozycję **informacje o firmie**.</span><span class="sxs-lookup"><span data-stu-id="cb509-169">Click the **Company** tab, and then click **Company Info**.</span></span>

    <span data-ttu-id="cb509-170">![Firmy](./media/active-directory-saas-intacct-tutorial/ic790037.png "firmy")</span><span class="sxs-lookup"><span data-stu-id="cb509-170">![Company](./media/active-directory-saas-intacct-tutorial/ic790037.png "Company")</span></span>

9. <span data-ttu-id="cb509-171">Kliknij przycisk **zabezpieczeń** , a następnie kliknij pozycję **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="cb509-171">Click the **Security** tab, and then click **Edit**.</span></span>

    <span data-ttu-id="cb509-172">![Zabezpieczenia](./media/active-directory-saas-intacct-tutorial/ic790038.png "zabezpieczeń")</span><span class="sxs-lookup"><span data-stu-id="cb509-172">![Security](./media/active-directory-saas-intacct-tutorial/ic790038.png "Security")</span></span>

10. <span data-ttu-id="cb509-173">W **logowania (SSO) z jednym** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="cb509-173">In the **Single sign on (SSO)** section, perform the following steps:</span></span>

    <span data-ttu-id="cb509-174">![Jednokrotne](./media/active-directory-saas-intacct-tutorial/ic790039.png "jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="cb509-174">![Single sign on](./media/active-directory-saas-intacct-tutorial/ic790039.png "single sign on")</span></span>

    <span data-ttu-id="cb509-175">a.</span><span class="sxs-lookup"><span data-stu-id="cb509-175">a.</span></span> <span data-ttu-id="cb509-176">Wybierz **włączenia funkcji logowania jednokrotnego w**.</span><span class="sxs-lookup"><span data-stu-id="cb509-176">Select **Enable single sign on**.</span></span>

    <span data-ttu-id="cb509-177">b.</span><span class="sxs-lookup"><span data-stu-id="cb509-177">b.</span></span> <span data-ttu-id="cb509-178">Jako **typ dostawcy tożsamości**, wybierz pozycję **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="cb509-178">As **Identity provider type**, select **SAML 2.0**.</span></span>

    <span data-ttu-id="cb509-179">c.</span><span class="sxs-lookup"><span data-stu-id="cb509-179">c.</span></span> <span data-ttu-id="cb509-180">W **adres URL wystawcy** pole tekstowe, Wklej wartość **identyfikator jednostki SAML** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="cb509-180">In **Issuer URL** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="cb509-181">d.</span><span class="sxs-lookup"><span data-stu-id="cb509-181">d.</span></span> <span data-ttu-id="cb509-182">W **adres URL logowania** pole tekstowe, Wklej wartość **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="cb509-182">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="cb509-183">e.</span><span class="sxs-lookup"><span data-stu-id="cb509-183">e.</span></span> <span data-ttu-id="cb509-184">Otwórz z **base-64** zakodowane certyfikatów w programie Notatnik, skopiuj zawartość go do Schowka, a następnie wklej go do **certyfikatu** pole.</span><span class="sxs-lookup"><span data-stu-id="cb509-184">Open your **base-64** encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Certificate** box.</span></span>
   
    <span data-ttu-id="cb509-185">f.</span><span class="sxs-lookup"><span data-stu-id="cb509-185">f.</span></span> <span data-ttu-id="cb509-186">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="cb509-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="cb509-187">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="cb509-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="cb509-188">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="cb509-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="cb509-189">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cb509-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cb509-190">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb509-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="cb509-191">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="cb509-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="cb509-193">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="cb509-193">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="cb509-194">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="cb509-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cb509-196">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="cb509-196">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cb509-198">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="cb509-198">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cb509-200">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="cb509-200">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cb509-202">a.</span><span class="sxs-lookup"><span data-stu-id="cb509-202">a.</span></span> <span data-ttu-id="cb509-203">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cb509-203">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cb509-204">b.</span><span class="sxs-lookup"><span data-stu-id="cb509-204">b.</span></span> <span data-ttu-id="cb509-205">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cb509-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cb509-206">c.</span><span class="sxs-lookup"><span data-stu-id="cb509-206">c.</span></span> <span data-ttu-id="cb509-207">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="cb509-207">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="cb509-208">d.</span><span class="sxs-lookup"><span data-stu-id="cb509-208">d.</span></span> <span data-ttu-id="cb509-209">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="cb509-209">Click **Create**.</span></span>
 
### <a name="creating-an-intacct-test-user"></a><span data-ttu-id="cb509-210">Tworzenie użytkownika testowego Intacct</span><span class="sxs-lookup"><span data-stu-id="cb509-210">Creating an Intacct test user</span></span>

<span data-ttu-id="cb509-211">Aby skonfigurować użytkowników usługi Azure AD, aby móc zalogować się do Intacct, muszą mieć przydzielone do Intacct.</span><span class="sxs-lookup"><span data-stu-id="cb509-211">To set up Azure AD users so they can sign in to Intacct, they must be provisioned into Intacct.</span></span> <span data-ttu-id="cb509-212">Dla Intacct Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="cb509-212">For Intacct, provisioning is a manual task.</span></span>

<span data-ttu-id="cb509-213">**Aby udostępnić konta użytkowników, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="cb509-213">**To provision user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="cb509-214">Zaloguj się do Twojego **Intacct** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="cb509-214">Sign in to your **Intacct** tenant.</span></span>

2. <span data-ttu-id="cb509-215">Kliknij przycisk **firmy** , a następnie kliknij pozycję **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="cb509-215">Click the **Company** tab, and then click **Users**.</span></span>

    <span data-ttu-id="cb509-216">![Użytkownicy](./media/active-directory-saas-intacct-tutorial/ic790041.png "użytkowników")</span><span class="sxs-lookup"><span data-stu-id="cb509-216">![Users](./media/active-directory-saas-intacct-tutorial/ic790041.png "Users")</span></span>
3. <span data-ttu-id="cb509-217">Kliknij przycisk **Dodaj** kartę.</span><span class="sxs-lookup"><span data-stu-id="cb509-217">Click the **Add** tab.</span></span>

    <span data-ttu-id="cb509-218">![Dodaj](./media/active-directory-saas-intacct-tutorial/ic790042.png "Dodaj")</span><span class="sxs-lookup"><span data-stu-id="cb509-218">![Add](./media/active-directory-saas-intacct-tutorial/ic790042.png "Add")</span></span>
4. <span data-ttu-id="cb509-219">W **informacje o użytkowniku** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="cb509-219">In the **User Information** section, perform the following steps:</span></span>

    <span data-ttu-id="cb509-220">![Informacje o użytkowniku](./media/active-directory-saas-intacct-tutorial/ic790043.png "informacje o użytkowniku")</span><span class="sxs-lookup"><span data-stu-id="cb509-220">![User Information](./media/active-directory-saas-intacct-tutorial/ic790043.png "User Information")</span></span>

    <span data-ttu-id="cb509-221">a.</span><span class="sxs-lookup"><span data-stu-id="cb509-221">a.</span></span> <span data-ttu-id="cb509-222">Wprowadź **identyfikator użytkownika**, **nazwisko**, **imię**, **adres E-mail**, **tytuł**i **Phone** konta usługi Azure AD, które chcesz udostępnić w **informacje o użytkowniku** sekcji.</span><span class="sxs-lookup"><span data-stu-id="cb509-222">Enter the **User ID**, the **Last name**, **First name**, the **Email address**, the **Title**, and the **Phone** of an Azure AD account that you want to provision into the **User Information** section.</span></span>

    <span data-ttu-id="cb509-223">b.</span><span class="sxs-lookup"><span data-stu-id="cb509-223">b.</span></span> <span data-ttu-id="cb509-224">Wybierz **uprawnień administratora** konta usługi Azure AD, które chcesz udostępnić.</span><span class="sxs-lookup"><span data-stu-id="cb509-224">Select the **Admin privileges** of an Azure AD account that you want to provision.</span></span>
   
    <span data-ttu-id="cb509-225">c.</span><span class="sxs-lookup"><span data-stu-id="cb509-225">c.</span></span> <span data-ttu-id="cb509-226">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="cb509-226">Click **Save**.</span></span> <span data-ttu-id="cb509-227">Właścicielem konta usługi Azure AD odbiera wiadomości e-mail i następuje łącze, aby potwierdzić swoje konto, zanim staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="cb509-227">The Azure AD account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

>[!NOTE]
><span data-ttu-id="cb509-228">Aby udostępnić konta użytkownika usługi Azure AD, można użyć innych Intacct narzędzia do tworzenia konta użytkownika lub interfejsów API, które są dostarczane przez Intacct.</span><span class="sxs-lookup"><span data-stu-id="cb509-228">To provision Azure AD user accounts, you can use other Intacct user account creation tools or APIs that are provided by Intacct.</span></span>
        
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="cb509-229">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb509-229">Assigning the Azure AD test user</span></span>

<span data-ttu-id="cb509-230">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Intacct.</span><span class="sxs-lookup"><span data-stu-id="cb509-230">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Intacct.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="cb509-232">**Aby przypisać Simona Britta Intacct, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="cb509-232">**To assign Britta Simon to Intacct, perform the following steps:**</span></span>

1. <span data-ttu-id="cb509-233">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="cb509-233">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="cb509-235">Na liście aplikacji zaznacz **Intacct**.</span><span class="sxs-lookup"><span data-stu-id="cb509-235">In the applications list, select **Intacct**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_app.png) 

3. <span data-ttu-id="cb509-237">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="cb509-237">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="cb509-239">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="cb509-239">Click **Add** button.</span></span> <span data-ttu-id="cb509-240">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="cb509-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="cb509-242">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="cb509-242">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="cb509-243">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="cb509-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cb509-244">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="cb509-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cb509-245">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="cb509-245">Testing single sign-on</span></span>

<span data-ttu-id="cb509-246">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="cb509-246">In this section, you test your Azure AD single sign-on configuration by using the Access Panel.</span></span>

<span data-ttu-id="cb509-247">Po kliknięciu kafelka Intacct w panelu dostępu należy powinny być automatycznie zalogowany do aplikacji Intacct.</span><span class="sxs-lookup"><span data-stu-id="cb509-247">When you click the Intacct tile in the Access Panel, you should be automatically signed in to your Intacct application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cb509-248">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="cb509-248">Additional resources</span></span>

* [<span data-ttu-id="cb509-249">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cb509-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cb509-250">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cb509-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_203.png

