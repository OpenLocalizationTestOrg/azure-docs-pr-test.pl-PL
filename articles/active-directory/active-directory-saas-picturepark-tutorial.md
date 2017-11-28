---
title: 'Samouczek: Integracji Azure Active Directory z Picturepark | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Picturepark."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 31c21cd4-9c00-4cad-9538-a13996dc872f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: jeedes
ms.openlocfilehash: 1c009aa1fdd3140a4466cf762b6c9687e74ce4c7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-picturepark"></a><span data-ttu-id="c4428-103">Samouczek: Integracji Azure Active Directory z Picturepark</span><span class="sxs-lookup"><span data-stu-id="c4428-103">Tutorial: Azure Active Directory integration with Picturepark</span></span>

<span data-ttu-id="c4428-104">Z tego samouczka dowiesz się integrowanie Picturepark z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c4428-104">In this tutorial, you learn how to integrate Picturepark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c4428-105">Integracja z usługą Azure AD Picturepark zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="c4428-105">Integrating Picturepark with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c4428-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Picturepark</span><span class="sxs-lookup"><span data-stu-id="c4428-106">You can control in Azure AD who has access to Picturepark</span></span>
- <span data-ttu-id="c4428-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Picturepark (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4428-107">You can enable your users to automatically get signed-on to Picturepark (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c4428-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c4428-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c4428-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c4428-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c4428-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c4428-110">Prerequisites</span></span>

<span data-ttu-id="c4428-111">Aby skonfigurować integrację usługi Azure AD z Picturepark, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="c4428-111">To configure Azure AD integration with Picturepark, you need the following items:</span></span>

- <span data-ttu-id="c4428-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4428-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c4428-113">Picturepark logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="c4428-113">A Picturepark single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c4428-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="c4428-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c4428-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="c4428-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c4428-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="c4428-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c4428-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c4428-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c4428-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="c4428-118">Scenario description</span></span>
<span data-ttu-id="c4428-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="c4428-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c4428-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="c4428-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c4428-121">Dodawanie Picturepark z galerii</span><span class="sxs-lookup"><span data-stu-id="c4428-121">Adding Picturepark from the gallery</span></span>
2. <span data-ttu-id="c4428-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="c4428-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-picturepark-from-the-gallery"></a><span data-ttu-id="c4428-123">Dodawanie Picturepark z galerii</span><span class="sxs-lookup"><span data-stu-id="c4428-123">Adding Picturepark from the gallery</span></span>
<span data-ttu-id="c4428-124">Aby skonfigurować integrację usługi Azure AD Picturepark, należy dodać Picturepark z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="c4428-124">To configure the integration of Picturepark into Azure AD, you need to add Picturepark from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c4428-125">**Aby dodać Picturepark z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c4428-125">**To add Picturepark from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c4428-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="c4428-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="c4428-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="c4428-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c4428-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="c4428-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="c4428-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c4428-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="c4428-133">W polu wyszukiwania wpisz **Picturepark**.</span><span class="sxs-lookup"><span data-stu-id="c4428-133">In the search box, type **Picturepark**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_search.png)

5. <span data-ttu-id="c4428-135">W panelu wyników wybierz **Picturepark**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="c4428-135">In the results panel, select **Picturepark**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c4428-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="c4428-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c4428-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Picturepark w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="c4428-138">In this section, you configure and test Azure AD single sign-on with Picturepark based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c4428-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Picturepark jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c4428-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Picturepark is to a user in Azure AD.</span></span> <span data-ttu-id="c4428-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Picturepark musi się.</span><span class="sxs-lookup"><span data-stu-id="c4428-140">In other words, a link relationship between an Azure AD user and the related user in Picturepark needs to be established.</span></span>

<span data-ttu-id="c4428-141">W Picturepark, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="c4428-141">In Picturepark, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c4428-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Picturepark, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="c4428-142">To configure and test Azure AD single sign-on with Picturepark, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c4428-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="c4428-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c4428-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="c4428-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c4428-145">**[Tworzenie użytkownika testowego Picturepark](#creating-a-picturepark-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Picturepark połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c4428-145">**[Creating a Picturepark test user](#creating-a-picturepark-test-user)** - to have a counterpart of Britta Simon in Picturepark that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c4428-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="c4428-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c4428-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="c4428-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c4428-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="c4428-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c4428-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Picturepark.</span><span class="sxs-lookup"><span data-stu-id="c4428-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Picturepark application.</span></span>

<span data-ttu-id="c4428-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Picturepark, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c4428-150">**To configure Azure AD single sign-on with Picturepark, perform the following steps:**</span></span>

1. <span data-ttu-id="c4428-151">W portalu Azure na **Picturepark** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="c4428-151">In the Azure portal, on the **Picturepark** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="c4428-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="c4428-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_samlbase.png)

3. <span data-ttu-id="c4428-155">Na **Picturepark domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c4428-155">On the **Picturepark Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_url.png)

    <span data-ttu-id="c4428-157">a.</span><span class="sxs-lookup"><span data-stu-id="c4428-157">a.</span></span> <span data-ttu-id="c4428-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.picturepark.com`</span><span class="sxs-lookup"><span data-stu-id="c4428-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.picturepark.com`</span></span>

    <span data-ttu-id="c4428-159">b.</span><span class="sxs-lookup"><span data-stu-id="c4428-159">b.</span></span> <span data-ttu-id="c4428-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="c4428-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span> 
    
    |  |
    |--|
    | `https://<companyname>.current-picturepark.com`|
    | `https://<companyname>.picturepark.com`|
    | `https://<companyname>.next-picturepark.com`|
    | |

    > [!NOTE] 
    > <span data-ttu-id="c4428-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="c4428-161">These values are not real.</span></span> <span data-ttu-id="c4428-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="c4428-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c4428-163">Skontaktuj się z [zespołem pomocy technicznej klienta Picturepark](https://picturepark.com/about/contact/) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="c4428-163">Contact [Picturepark Client support team](https://picturepark.com/about/contact/) to get these values.</span></span> 
 
4. <span data-ttu-id="c4428-164">Na **certyfikat podpisywania SAML** sekcji, skopiuj **odcisk PALCA** wartości certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="c4428-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_certificate.png) 

5. <span data-ttu-id="c4428-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c4428-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-picturepark-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c4428-168">Na **konfiguracji Picturepark** , kliknij przycisk **skonfigurować Picturepark** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="c4428-168">On the **Picturepark Configuration** section, click **Configure Picturepark** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c4428-169">Kopiuj **SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="c4428-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_configure.png) 

7. <span data-ttu-id="c4428-171">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy Picturepark jako administrator.</span><span class="sxs-lookup"><span data-stu-id="c4428-171">In a different web browser window, log into your Picturepark company site as an administrator.</span></span>

8. <span data-ttu-id="c4428-172">Na pasku narzędzi u góry kliknij **narzędzia administracyjne**, a następnie kliknij przycisk **konsoli zarządzania**.</span><span class="sxs-lookup"><span data-stu-id="c4428-172">In the toolbar on the top, click **Administrative tools**, and then click **Management Console**.</span></span>
   
    <span data-ttu-id="c4428-173">![Konsola zarządzania](./media/active-directory-saas-picturepark-tutorial/ic795062.png "Konsola zarządzania")</span><span class="sxs-lookup"><span data-stu-id="c4428-173">![Management Console](./media/active-directory-saas-picturepark-tutorial/ic795062.png "Management Console")</span></span>

9. <span data-ttu-id="c4428-174">Kliknij przycisk **uwierzytelniania**, a następnie kliknij przycisk **dostawców tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="c4428-174">Click **Authentication**, and then click **Identity providers**.</span></span>
   
    <span data-ttu-id="c4428-175">![Uwierzytelnianie](./media/active-directory-saas-picturepark-tutorial/ic795063.png "uwierzytelniania")</span><span class="sxs-lookup"><span data-stu-id="c4428-175">![Authentication](./media/active-directory-saas-picturepark-tutorial/ic795063.png "Authentication")</span></span>

10. <span data-ttu-id="c4428-176">W **konfiguracji dostawcy tożsamości** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c4428-176">In the **Identity provider configuration** section, perform the following steps:</span></span>
   
    <span data-ttu-id="c4428-177">![Konfiguracja dostawcy tożsamości](./media/active-directory-saas-picturepark-tutorial/ic795064.png "konfiguracji dostawcy tożsamości")</span><span class="sxs-lookup"><span data-stu-id="c4428-177">![Identity provider configuration](./media/active-directory-saas-picturepark-tutorial/ic795064.png "Identity provider configuration")</span></span>
   
    <span data-ttu-id="c4428-178">a.</span><span class="sxs-lookup"><span data-stu-id="c4428-178">a.</span></span> <span data-ttu-id="c4428-179">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="c4428-179">Click **Add**.</span></span>
  
    <span data-ttu-id="c4428-180">b.</span><span class="sxs-lookup"><span data-stu-id="c4428-180">b.</span></span> <span data-ttu-id="c4428-181">Wpisz nazwę dla danej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="c4428-181">Type a name for your configuration.</span></span>
   
    <span data-ttu-id="c4428-182">c.</span><span class="sxs-lookup"><span data-stu-id="c4428-182">c.</span></span> <span data-ttu-id="c4428-183">Wybierz **Ustaw jako domyślny**.</span><span class="sxs-lookup"><span data-stu-id="c4428-183">Select **Set as default**.</span></span>
   
    <span data-ttu-id="c4428-184">d.</span><span class="sxs-lookup"><span data-stu-id="c4428-184">d.</span></span> <span data-ttu-id="c4428-185">W **URI wystawcy** pole tekstowe, Wklej wartość **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c4428-185">In **Issuer URI** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="c4428-186">e.</span><span class="sxs-lookup"><span data-stu-id="c4428-186">e.</span></span> <span data-ttu-id="c4428-187">W **zaufanego wystawcy miniatury** pole tekstowe, Wklej wartość **odcisk palca** , które zostały skopiowane z **certyfikat podpisywania SAML** sekcji.</span><span class="sxs-lookup"><span data-stu-id="c4428-187">In **Trusted Issuer Thumb Print** textbox, paste the value of **Thumbprint** which you have copied from **SAML Signing Certificate** section.</span></span> 

11. <span data-ttu-id="c4428-188">Kliknij przycisk **JoinDefaultUsersGroup**.</span><span class="sxs-lookup"><span data-stu-id="c4428-188">Click **JoinDefaultUsersGroup**.</span></span>

12. <span data-ttu-id="c4428-189">Aby ustawić **Emailaddress** atrybutu w **oświadczeń** pole tekstowe, typ `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` i kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="c4428-189">To set the **Emailaddress** attribute in the **Claim** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` and click **Save**.</span></span>

      <span data-ttu-id="c4428-190">![Konfiguracja](./media/active-directory-saas-picturepark-tutorial/ic795065.png "konfiguracji")</span><span class="sxs-lookup"><span data-stu-id="c4428-190">![Configuration](./media/active-directory-saas-picturepark-tutorial/ic795065.png "Configuration")</span></span>

> [!TIP]
> <span data-ttu-id="c4428-191">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="c4428-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c4428-192">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="c4428-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c4428-193">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c4428-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c4428-194">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4428-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="c4428-195">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="c4428-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="c4428-197">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c4428-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c4428-198">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="c4428-198">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c4428-200">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="c4428-200">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c4428-202">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c4428-202">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c4428-204">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c4428-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c4428-206">a.</span><span class="sxs-lookup"><span data-stu-id="c4428-206">a.</span></span> <span data-ttu-id="c4428-207">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c4428-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c4428-208">b.</span><span class="sxs-lookup"><span data-stu-id="c4428-208">b.</span></span> <span data-ttu-id="c4428-209">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c4428-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c4428-210">c.</span><span class="sxs-lookup"><span data-stu-id="c4428-210">c.</span></span> <span data-ttu-id="c4428-211">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="c4428-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c4428-212">d.</span><span class="sxs-lookup"><span data-stu-id="c4428-212">d.</span></span> <span data-ttu-id="c4428-213">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="c4428-213">Click **Create**.</span></span>
 
### <a name="creating-a-picturepark-test-user"></a><span data-ttu-id="c4428-214">Tworzenie użytkownika testowego Picturepark</span><span class="sxs-lookup"><span data-stu-id="c4428-214">Creating a Picturepark test user</span></span>

<span data-ttu-id="c4428-215">Aby włączyć użytkowników usługi Azure AD zalogować się do Picturepark, musi być przygotowana do Picturepark.</span><span class="sxs-lookup"><span data-stu-id="c4428-215">In order to enable Azure AD users to log into Picturepark, they must be provisioned into Picturepark.</span></span> <span data-ttu-id="c4428-216">W przypadku Picturepark Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="c4428-216">In the case of Picturepark, provisioning is a manual task.</span></span>

<span data-ttu-id="c4428-217">**Aby udostępnić konta użytkownika, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c4428-217">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="c4428-218">Zaloguj się do Twojego **Picturepark** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="c4428-218">Log in to your **Picturepark** tenant.</span></span>

2. <span data-ttu-id="c4428-219">Na pasku narzędzi u góry kliknij **narzędzia administracyjne**, a następnie kliknij przycisk **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="c4428-219">In the toolbar on the top, click **Administrative tools**, and then click **Users**.</span></span>
   
    <span data-ttu-id="c4428-220">![Użytkownicy](./media/active-directory-saas-picturepark-tutorial/ic795067.png "użytkowników")</span><span class="sxs-lookup"><span data-stu-id="c4428-220">![Users](./media/active-directory-saas-picturepark-tutorial/ic795067.png "Users")</span></span>

3. <span data-ttu-id="c4428-221">W **Przegląd użytkowników** , kliknij pozycję **nowy**.</span><span class="sxs-lookup"><span data-stu-id="c4428-221">In the **Users overview** tab, click **New**.</span></span>
   
    <span data-ttu-id="c4428-222">![Zarządzanie użytkownikami](./media/active-directory-saas-picturepark-tutorial/ic795068.png "Zarządzanie użytkownikami")</span><span class="sxs-lookup"><span data-stu-id="c4428-222">![User management](./media/active-directory-saas-picturepark-tutorial/ic795068.png "User management")</span></span>

4. <span data-ttu-id="c4428-223">Na **Tworzenie użytkownika** okna dialogowego, wykonaj następujące kroki prawidłowego Azure Active Directory użytkownika mają do przepisu:</span><span class="sxs-lookup"><span data-stu-id="c4428-223">On the **Create User** dialog, perform the following steps of a valid Azure Active Directory User you want to provision:</span></span>
   
    <span data-ttu-id="c4428-224">![Utwórz użytkownika](./media/active-directory-saas-picturepark-tutorial/ic795069.png "Tworzenie użytkownika")</span><span class="sxs-lookup"><span data-stu-id="c4428-224">![Create User](./media/active-directory-saas-picturepark-tutorial/ic795069.png "Create User")</span></span>
   
    <span data-ttu-id="c4428-225">a.</span><span class="sxs-lookup"><span data-stu-id="c4428-225">a.</span></span> <span data-ttu-id="c4428-226">W **adres E-mail** pole tekstowe, typ **adres e-mail** użytkownika  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="c4428-226">In the **Email Address** textbox, type the **email address** of the user **BrittaSimon@contoso.com**.</span></span>  
   
    <span data-ttu-id="c4428-227">b.</span><span class="sxs-lookup"><span data-stu-id="c4428-227">b.</span></span> <span data-ttu-id="c4428-228">W **hasło** i **Potwierdź hasło** pól tekstowych, typ **hasło** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c4428-228">In the **Password** and **Confirm Password** textboxes, type the **password** of BrittaSimon.</span></span> 
   
    <span data-ttu-id="c4428-229">c.</span><span class="sxs-lookup"><span data-stu-id="c4428-229">c.</span></span> <span data-ttu-id="c4428-230">W **imię** pole tekstowe, typ **imię** użytkownika **Britta**.</span><span class="sxs-lookup"><span data-stu-id="c4428-230">In the **First Name** textbox, type the **First Name** of the user **Britta**.</span></span> 
   
    <span data-ttu-id="c4428-231">d.</span><span class="sxs-lookup"><span data-stu-id="c4428-231">d.</span></span> <span data-ttu-id="c4428-232">W **nazwisko** pole tekstowe, typ **nazwisko** użytkownika **Simona**.</span><span class="sxs-lookup"><span data-stu-id="c4428-232">In the **Last Name** textbox, type the **Last Name** of the user **Simon**.</span></span>
   
    <span data-ttu-id="c4428-233">e.</span><span class="sxs-lookup"><span data-stu-id="c4428-233">e.</span></span> <span data-ttu-id="c4428-234">W **firmy** pole tekstowe, typ **nazwa firmy** użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c4428-234">In the **Company** textbox, type the **Company name** of the user.</span></span> 
   
    <span data-ttu-id="c4428-235">f.</span><span class="sxs-lookup"><span data-stu-id="c4428-235">f.</span></span> <span data-ttu-id="c4428-236">W **kraju** pole tekstowe, wybierz opcję **kraju** użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c4428-236">In the **Country** textbox, select the **Country** of the user.</span></span>
  
    <span data-ttu-id="c4428-237">g.</span><span class="sxs-lookup"><span data-stu-id="c4428-237">g.</span></span> <span data-ttu-id="c4428-238">W **ZIP** pole tekstowe, typ **kod POCZTOWY** miasta.</span><span class="sxs-lookup"><span data-stu-id="c4428-238">In the **ZIP** textbox, type the **ZIP code** of the city.</span></span>
   
    <span data-ttu-id="c4428-239">h.</span><span class="sxs-lookup"><span data-stu-id="c4428-239">h.</span></span> <span data-ttu-id="c4428-240">W **miasta** pole tekstowe, typ **nazwę miejscowości** użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c4428-240">In the **City** textbox, type the **City name** of the user.</span></span>

    <span data-ttu-id="c4428-241">i.</span><span class="sxs-lookup"><span data-stu-id="c4428-241">i.</span></span> <span data-ttu-id="c4428-242">Wybierz **języka**.</span><span class="sxs-lookup"><span data-stu-id="c4428-242">Select a **Language**.</span></span>
   
    <span data-ttu-id="c4428-243">j.</span><span class="sxs-lookup"><span data-stu-id="c4428-243">j.</span></span> <span data-ttu-id="c4428-244">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="c4428-244">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="c4428-245">Możesz użyć innych Picturepark użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Picturepark do udostępnienia konta użytkownika usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c4428-245">You can use any other Picturepark user account creation tools or APIs provided by Picturepark to provision Azure AD user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c4428-246">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4428-246">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c4428-247">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Picturepark.</span><span class="sxs-lookup"><span data-stu-id="c4428-247">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Picturepark.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="c4428-249">**Aby przypisać Simona Britta Picturepark, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c4428-249">**To assign Britta Simon to Picturepark, perform the following steps:**</span></span>

1. <span data-ttu-id="c4428-250">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="c4428-250">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="c4428-252">Na liście aplikacji zaznacz **Picturepark**.</span><span class="sxs-lookup"><span data-stu-id="c4428-252">In the applications list, select **Picturepark**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_app.png) 

3. <span data-ttu-id="c4428-254">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="c4428-254">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="c4428-256">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c4428-256">Click **Add** button.</span></span> <span data-ttu-id="c4428-257">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c4428-257">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="c4428-259">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="c4428-259">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c4428-260">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c4428-260">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c4428-261">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c4428-261">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c4428-262">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="c4428-262">Testing single sign-on</span></span>

<span data-ttu-id="c4428-263">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="c4428-263">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c4428-264">Po kliknięciu kafelka Picturepark w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Picturepark.</span><span class="sxs-lookup"><span data-stu-id="c4428-264">When you click the Picturepark tile in the Access Panel, you should get automatically signed-on to your Picturepark application.</span></span> <span data-ttu-id="c4428-265">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c4428-265">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c4428-266">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="c4428-266">Additional resources</span></span>

* [<span data-ttu-id="c4428-267">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c4428-267">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c4428-268">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c4428-268">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_203.png

