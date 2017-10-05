---
title: 'Samouczek: Integracji Azure Active Directory z AppDynamics | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i AppDynamics."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 25fd1df0-411c-4f55-8be3-4273b543100f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 634e68bdb937eba68b27b824dc62fe2677e24ffe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-appdynamics"></a><span data-ttu-id="f835e-103">Samouczek: Integracji Azure Active Directory z AppDynamics</span><span class="sxs-lookup"><span data-stu-id="f835e-103">Tutorial: Azure Active Directory integration with AppDynamics</span></span>

<span data-ttu-id="f835e-104">Z tego samouczka dowiesz się integrowanie AppDynamics z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f835e-104">In this tutorial, you learn how to integrate AppDynamics with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f835e-105">Integracja z usługą Azure AD AppDynamics zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="f835e-105">Integrating AppDynamics with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f835e-106">Można kontrolować w usłudze Azure AD, który ma dostęp do AppDynamics</span><span class="sxs-lookup"><span data-stu-id="f835e-106">You can control in Azure AD who has access to AppDynamics</span></span>
- <span data-ttu-id="f835e-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do AppDynamics (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f835e-107">You can enable your users to automatically get signed-on to AppDynamics (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f835e-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="f835e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f835e-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f835e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f835e-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f835e-110">Prerequisites</span></span>

<span data-ttu-id="f835e-111">Aby skonfigurować integrację usługi Azure AD z AppDynamics, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="f835e-111">To configure Azure AD integration with AppDynamics, you need the following items:</span></span>

- <span data-ttu-id="f835e-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f835e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f835e-113">AppDynamics logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="f835e-113">An AppDynamics single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f835e-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="f835e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f835e-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="f835e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f835e-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="f835e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f835e-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f835e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f835e-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="f835e-118">Scenario description</span></span>
<span data-ttu-id="f835e-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="f835e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f835e-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="f835e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f835e-121">Dodawanie AppDynamics z galerii</span><span class="sxs-lookup"><span data-stu-id="f835e-121">Adding AppDynamics from the gallery</span></span>
2. <span data-ttu-id="f835e-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="f835e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-appdynamics-from-the-gallery"></a><span data-ttu-id="f835e-123">Dodawanie AppDynamics z galerii</span><span class="sxs-lookup"><span data-stu-id="f835e-123">Adding AppDynamics from the gallery</span></span>
<span data-ttu-id="f835e-124">Aby skonfigurować integrację usługi Azure AD AppDynamics, należy dodać AppDynamics z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="f835e-124">To configure the integration of AppDynamics into Azure AD, you need to add AppDynamics from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f835e-125">**Aby dodać AppDynamics z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f835e-125">**To add AppDynamics from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f835e-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="f835e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="f835e-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="f835e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f835e-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="f835e-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="f835e-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f835e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="f835e-133">W polu wyszukiwania wpisz **AppDynamics**.</span><span class="sxs-lookup"><span data-stu-id="f835e-133">In the search box, type **AppDynamics**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_search.png)

5. <span data-ttu-id="f835e-135">W panelu wyników wybierz **AppDynamics**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="f835e-135">In the results panel, select **AppDynamics**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f835e-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="f835e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f835e-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z AppDynamics na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="f835e-138">In this section, you configure and test Azure AD single sign-on with AppDynamics based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f835e-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w AppDynamics jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f835e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in AppDynamics is to a user in Azure AD.</span></span> <span data-ttu-id="f835e-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w AppDynamics musi się.</span><span class="sxs-lookup"><span data-stu-id="f835e-140">In other words, a link relationship between an Azure AD user and the related user in AppDynamics needs to be established.</span></span>

<span data-ttu-id="f835e-141">W AppDynamics, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="f835e-141">In AppDynamics, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f835e-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z AppDynamics, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="f835e-142">To configure and test Azure AD single sign-on with AppDynamics, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f835e-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="f835e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f835e-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="f835e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f835e-145">**[Tworzenie użytkownika testowego AppDynamics](#creating-an-appdynamics-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta AppDynamics połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f835e-145">**[Creating an AppDynamics test user](#creating-an-appdynamics-test-user)** - to have a counterpart of Britta Simon in AppDynamics that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f835e-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="f835e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f835e-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="f835e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f835e-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="f835e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f835e-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji AppDynamics.</span><span class="sxs-lookup"><span data-stu-id="f835e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your AppDynamics application.</span></span>

<span data-ttu-id="f835e-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z AppDynamics, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f835e-150">**To configure Azure AD single sign-on with AppDynamics, perform the following steps:**</span></span>

1. <span data-ttu-id="f835e-151">W portalu Azure na **AppDynamics** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="f835e-151">In the Azure portal, on the **AppDynamics** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="f835e-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="f835e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_samlbase.png)

3. <span data-ttu-id="f835e-155">Na **AppDynamics domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f835e-155">On the **AppDynamics Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_url.png)

    <span data-ttu-id="f835e-157">a.</span><span class="sxs-lookup"><span data-stu-id="f835e-157">a.</span></span> <span data-ttu-id="f835e-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.saas.appdynamics.com`</span><span class="sxs-lookup"><span data-stu-id="f835e-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.saas.appdynamics.com`</span></span>

    <span data-ttu-id="f835e-159">b.</span><span class="sxs-lookup"><span data-stu-id="f835e-159">b.</span></span> <span data-ttu-id="f835e-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.saas.appdynamics.com/controller`</span><span class="sxs-lookup"><span data-stu-id="f835e-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.saas.appdynamics.com/controller`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f835e-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="f835e-161">These values are not real.</span></span> <span data-ttu-id="f835e-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="f835e-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f835e-163">Skontaktuj się z [zespołem pomocy technicznej klienta AppDynamics](https://www.appdynamics.com/support/) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="f835e-163">Contact [AppDynamics Client support team](https://www.appdynamics.com/support/) to get these values.</span></span> 
 
4. <span data-ttu-id="f835e-164">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="f835e-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_certificate.png) 

5. <span data-ttu-id="f835e-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f835e-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-appdynamics-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f835e-168">Na **konfiguracji AppDynamics** , kliknij przycisk **skonfigurować AppDynamics** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="f835e-168">On the **AppDynamics Configuration** section, click **Configure AppDynamics** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f835e-169">Kopiuj **Sign-Out adresu URL i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="f835e-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_configure.png) 

7. <span data-ttu-id="f835e-171">W oknie przeglądarki innej witryny sieci web należy zalogować się jako administrator do witryny firmy AppDynamics.</span><span class="sxs-lookup"><span data-stu-id="f835e-171">In a different web browser window, log in to your AppDynamics company site as an administrator.</span></span>

8. <span data-ttu-id="f835e-172">Na pasku narzędzi u góry kliknij **ustawienia**, a następnie kliknij przycisk **administracji**.</span><span class="sxs-lookup"><span data-stu-id="f835e-172">In the toolbar on the top, click **Settings**, and then click **Administration**.</span></span>
   
    <span data-ttu-id="f835e-173">![Administracja](./media/active-directory-saas-appdynamics-tutorial/ic790216.png "administracji")</span><span class="sxs-lookup"><span data-stu-id="f835e-173">![Administration](./media/active-directory-saas-appdynamics-tutorial/ic790216.png "Administration")</span></span>

9. <span data-ttu-id="f835e-174">Kliknij przycisk **dostawcy uwierzytelniania** kartę.</span><span class="sxs-lookup"><span data-stu-id="f835e-174">Click the **Authentication Provider** tab.</span></span>
   
    <span data-ttu-id="f835e-175">![Dostawca uwierzytelniania](./media/active-directory-saas-appdynamics-tutorial/ic790224.png "dostawcy uwierzytelniania")</span><span class="sxs-lookup"><span data-stu-id="f835e-175">![Authentication Provider](./media/active-directory-saas-appdynamics-tutorial/ic790224.png "Authentication Provider")</span></span>

10. <span data-ttu-id="f835e-176">W **dostawcy uwierzytelniania** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f835e-176">In the **Authentication Provider** section, perform the following steps:</span></span>
   
    <span data-ttu-id="f835e-177">![Konfiguracja SAML](./media/active-directory-saas-appdynamics-tutorial/ic790225.png "Konfiguracja SAML")</span><span class="sxs-lookup"><span data-stu-id="f835e-177">![SAML Configuration](./media/active-directory-saas-appdynamics-tutorial/ic790225.png "SAML Configuration")</span></span>   

    <span data-ttu-id="f835e-178">a.</span><span class="sxs-lookup"><span data-stu-id="f835e-178">a.</span></span> <span data-ttu-id="f835e-179">Jako **dostawcy uwierzytelniania**, wybierz pozycję **SAML**.</span><span class="sxs-lookup"><span data-stu-id="f835e-179">As **Authentication Provider**, select **SAML**.</span></span>

    <span data-ttu-id="f835e-180">b.</span><span class="sxs-lookup"><span data-stu-id="f835e-180">b.</span></span> <span data-ttu-id="f835e-181">W **adres URL logowania** pole tekstowe, Wklej wartość **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f835e-181">In the **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="f835e-182">c.</span><span class="sxs-lookup"><span data-stu-id="f835e-182">c.</span></span> <span data-ttu-id="f835e-183">W **adresu URL wylogowania** pole tekstowe, Wklej wartość **Sign-Out URL** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f835e-183">In the **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
       
    <span data-ttu-id="f835e-184">d.</span><span class="sxs-lookup"><span data-stu-id="f835e-184">d.</span></span> <span data-ttu-id="f835e-185">Otwórz w Notatniku certyfikatu zakodowanego base-64, skopiuj zawartość go do Schowka, a następnie wklej go do **certyfikatu** pole tekstowe</span><span class="sxs-lookup"><span data-stu-id="f835e-185">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Certificate** textbox</span></span>

    <span data-ttu-id="f835e-186">e.</span><span class="sxs-lookup"><span data-stu-id="f835e-186">e.</span></span> <span data-ttu-id="f835e-187">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="f835e-187">Click **Save**.</span></span>

     <span data-ttu-id="f835e-188">![Zapisz](./media/active-directory-saas-appdynamics-tutorial/ic777673.png "Zapisz")</span><span class="sxs-lookup"><span data-stu-id="f835e-188">![Save](./media/active-directory-saas-appdynamics-tutorial/ic777673.png "Save")</span></span>

> [!TIP]
> <span data-ttu-id="f835e-189">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="f835e-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f835e-190">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="f835e-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f835e-191">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f835e-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f835e-192">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f835e-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="f835e-193">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="f835e-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="f835e-195">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f835e-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f835e-196">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="f835e-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f835e-198">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="f835e-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f835e-200">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f835e-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f835e-202">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f835e-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f835e-204">a.</span><span class="sxs-lookup"><span data-stu-id="f835e-204">a.</span></span> <span data-ttu-id="f835e-205">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f835e-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f835e-206">b.</span><span class="sxs-lookup"><span data-stu-id="f835e-206">b.</span></span> <span data-ttu-id="f835e-207">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f835e-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f835e-208">c.</span><span class="sxs-lookup"><span data-stu-id="f835e-208">c.</span></span> <span data-ttu-id="f835e-209">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="f835e-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f835e-210">d.</span><span class="sxs-lookup"><span data-stu-id="f835e-210">d.</span></span> <span data-ttu-id="f835e-211">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="f835e-211">Click **Create**.</span></span>
 
### <a name="creating-an-appdynamics-test-user"></a><span data-ttu-id="f835e-212">Tworzenie użytkownika testowego AppDynamics</span><span class="sxs-lookup"><span data-stu-id="f835e-212">Creating an AppDynamics test user</span></span>

<span data-ttu-id="f835e-213">Aby umożliwić użytkownikom usługi Azure AD zalogować się do AppDynamics, musi być przygotowana do AppDynamics.</span><span class="sxs-lookup"><span data-stu-id="f835e-213">To enable Azure AD users to log in to AppDynamics, they must be provisioned into AppDynamics.</span></span> <span data-ttu-id="f835e-214">W przypadku AppDynamics Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="f835e-214">In the case of AppDynamics, provisioning is a manual task.</span></span>

<span data-ttu-id="f835e-215">**Aby skonfigurować, inicjowanie obsługi użytkowników, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f835e-215">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="f835e-216">Zaloguj się do witryny firmy AppDynamics jako administrator.</span><span class="sxs-lookup"><span data-stu-id="f835e-216">Log in to your AppDynamics company site as an administrator.</span></span>

2. <span data-ttu-id="f835e-217">Przejdź do **użytkowników**, a następnie kliknij przycisk  **+**  otworzyć **Tworzenie użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f835e-217">Go to **Users**, and then click **+** to open the **Create User** dialog.</span></span>
   
    <span data-ttu-id="f835e-218">![Użytkownicy](./media/active-directory-saas-appdynamics-tutorial/ic790229.png "użytkowników")</span><span class="sxs-lookup"><span data-stu-id="f835e-218">![Users](./media/active-directory-saas-appdynamics-tutorial/ic790229.png "Users")</span></span>

3. <span data-ttu-id="f835e-219">W **Tworzenie użytkownika** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f835e-219">In the **Create User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="f835e-220">![Utwórz użytkownika](./media/active-directory-saas-appdynamics-tutorial/ic790230.png "Tworzenie użytkownika")</span><span class="sxs-lookup"><span data-stu-id="f835e-220">![Create User](./media/active-directory-saas-appdynamics-tutorial/ic790230.png "Create User")</span></span>
   
    <span data-ttu-id="f835e-221">a.</span><span class="sxs-lookup"><span data-stu-id="f835e-221">a.</span></span> <span data-ttu-id="f835e-222">Typ **Username**, **nazwa**, **poczty E-mail**, **nowe hasło**, **powtórz nowe hasło** poprawnego konta usługi AAD ustanawiane do powiązanych pól tekstowych.</span><span class="sxs-lookup"><span data-stu-id="f835e-222">Type the **Username**, **Name**, **Email**, **New Password**, **Repeat New Password** of a valid AAD account you want to provision into the related textboxes.</span></span>

    <span data-ttu-id="f835e-223">b.</span><span class="sxs-lookup"><span data-stu-id="f835e-223">b.</span></span> <span data-ttu-id="f835e-224">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="f835e-224">Click **Save**.</span></span>

    >[!NOTE]
    ><span data-ttu-id="f835e-225">Możesz użyć innych AppDynamics użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez AppDynamics do udostępnienia konta użytkownika usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f835e-225">You can use any other AppDynamics user account creation tools or APIs provided by AppDynamics to provision Azure AD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f835e-226">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f835e-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f835e-227">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu AppDynamics.</span><span class="sxs-lookup"><span data-stu-id="f835e-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to AppDynamics.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="f835e-229">**Aby przypisać Simona Britta AppDynamics, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f835e-229">**To assign Britta Simon to AppDynamics, perform the following steps:**</span></span>

1. <span data-ttu-id="f835e-230">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="f835e-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="f835e-232">Na liście aplikacji zaznacz **AppDynamics**.</span><span class="sxs-lookup"><span data-stu-id="f835e-232">In the applications list, select **AppDynamics**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_app.png) 

3. <span data-ttu-id="f835e-234">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="f835e-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="f835e-236">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f835e-236">Click **Add** button.</span></span> <span data-ttu-id="f835e-237">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f835e-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="f835e-239">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="f835e-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f835e-240">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f835e-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f835e-241">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f835e-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f835e-242">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="f835e-242">Testing single sign-on</span></span>

<span data-ttu-id="f835e-243">Celem tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="f835e-243">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f835e-244">Po kliknięciu kafelka AppDynamics w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji AppDynamics.</span><span class="sxs-lookup"><span data-stu-id="f835e-244">When you click the AppDynamics tile in the Access Panel, you should get automatically signed-on to your AppDynamics application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f835e-245">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="f835e-245">Additional resources</span></span>

* [<span data-ttu-id="f835e-246">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f835e-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f835e-247">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f835e-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_203.png

