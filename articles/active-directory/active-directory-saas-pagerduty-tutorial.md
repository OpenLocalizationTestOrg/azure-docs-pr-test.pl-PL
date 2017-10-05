---
title: 'Samouczek: Integracji Azure Active Directory z PagerDuty | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i PagerDuty."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0410456a-76f7-42a7-9bb5-f767de75a0e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: bf5263ce4d8fbc231029c101f167f4b55a921e60
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pagerduty"></a><span data-ttu-id="693f1-103">Samouczek: Integracji Azure Active Directory z PagerDuty</span><span class="sxs-lookup"><span data-stu-id="693f1-103">Tutorial: Azure Active Directory integration with PagerDuty</span></span>

<span data-ttu-id="693f1-104">Z tego samouczka dowiesz się integrowanie PagerDuty z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="693f1-104">In this tutorial, you learn how to integrate PagerDuty with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="693f1-105">Integracja z usługą Azure AD PagerDuty zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="693f1-105">Integrating PagerDuty with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="693f1-106">Można kontrolować w usłudze Azure AD, który ma dostęp do PagerDuty</span><span class="sxs-lookup"><span data-stu-id="693f1-106">You can control in Azure AD who has access to PagerDuty</span></span>
- <span data-ttu-id="693f1-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do PagerDuty (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="693f1-107">You can enable your users to automatically get signed-on to PagerDuty (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="693f1-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="693f1-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="693f1-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="693f1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="693f1-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="693f1-110">Prerequisites</span></span>

<span data-ttu-id="693f1-111">Aby skonfigurować integrację usługi Azure AD z PagerDuty, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="693f1-111">To configure Azure AD integration with PagerDuty, you need the following items:</span></span>

- <span data-ttu-id="693f1-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="693f1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="693f1-113">PagerDuty logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="693f1-113">A PagerDuty single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="693f1-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="693f1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="693f1-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="693f1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="693f1-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="693f1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="693f1-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="693f1-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="693f1-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="693f1-118">Scenario description</span></span>
<span data-ttu-id="693f1-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="693f1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="693f1-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="693f1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="693f1-121">Dodawanie PagerDuty z galerii</span><span class="sxs-lookup"><span data-stu-id="693f1-121">Adding PagerDuty from the gallery</span></span>
2. <span data-ttu-id="693f1-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="693f1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pagerduty-from-the-gallery"></a><span data-ttu-id="693f1-123">Dodawanie PagerDuty z galerii</span><span class="sxs-lookup"><span data-stu-id="693f1-123">Adding PagerDuty from the gallery</span></span>
<span data-ttu-id="693f1-124">Aby skonfigurować integrację usługi Azure AD PagerDuty, należy dodać PagerDuty z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="693f1-124">To configure the integration of PagerDuty into Azure AD, you need to add PagerDuty from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="693f1-125">**Aby dodać PagerDuty z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="693f1-125">**To add PagerDuty from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="693f1-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="693f1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Przycisk usługi Azure Active Directory][1]

2. <span data-ttu-id="693f1-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="693f1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="693f1-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="693f1-129">Then go to **All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa][2]
    
3. <span data-ttu-id="693f1-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="693f1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Nowy przycisk aplikacji][3]

4. <span data-ttu-id="693f1-133">W polu wyszukiwania wpisz **PagerDuty**, wybierz pozycję **PagerDuty** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="693f1-133">In the search box, type **PagerDuty**, select  **PagerDuty**  from result panel then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="693f1-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="693f1-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="693f1-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z PagerDuty w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="693f1-136">In this section, you configure and test Azure AD single sign-on with PagerDuty based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="693f1-137">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w PagerDuty jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="693f1-137">For single sign-on to work, Azure AD needs to know what the counterpart user in PagerDuty is to a user in Azure AD.</span></span> <span data-ttu-id="693f1-138">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w PagerDuty musi się.</span><span class="sxs-lookup"><span data-stu-id="693f1-138">In other words, a link relationship between an Azure AD user and the related user in PagerDuty needs to be established.</span></span>

<span data-ttu-id="693f1-139">W PagerDuty, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="693f1-139">In PagerDuty, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="693f1-140">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z PagerDuty, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="693f1-140">To configure and test Azure AD single sign-on with PagerDuty, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="693f1-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="693f1-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="693f1-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="693f1-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="693f1-143">**[Tworzenie użytkownika testowego PagerDuty](#create-a-pagerduty-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta PagerDuty połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="693f1-143">**[Create a PagerDuty test user](#create-a-pagerduty-test-user)** - to have a counterpart of Britta Simon in PagerDuty that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="693f1-144">**[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="693f1-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="693f1-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="693f1-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="693f1-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="693f1-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="693f1-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="693f1-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your PagerDuty application.</span></span>

<span data-ttu-id="693f1-148">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z PagerDuty, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="693f1-148">**To configure Azure AD single sign-on with PagerDuty, perform the following steps:**</span></span>

1. <span data-ttu-id="693f1-149">W portalu Azure na **PagerDuty** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="693f1-149">In the Azure portal, on the **PagerDuty** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="693f1-151">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="693f1-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_samlbase.png)

3. <span data-ttu-id="693f1-153">Na **PagerDuty domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="693f1-153">On the **PagerDuty Domain and URLs** section, perform the following steps:</span></span>

    ![Adresy URL i domeny PagerDuty pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_url.png)

    <span data-ttu-id="693f1-155">a.</span><span class="sxs-lookup"><span data-stu-id="693f1-155">a.</span></span> <span data-ttu-id="693f1-156">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<tenant-name>.pagerduty.com`</span><span class="sxs-lookup"><span data-stu-id="693f1-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.pagerduty.com`</span></span>

    <span data-ttu-id="693f1-157">b.</span><span class="sxs-lookup"><span data-stu-id="693f1-157">b.</span></span> <span data-ttu-id="693f1-158">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<tenant-name>.pagerduty.com`</span><span class="sxs-lookup"><span data-stu-id="693f1-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenant-name>.pagerduty.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="693f1-159">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="693f1-159">These values are not real.</span></span> <span data-ttu-id="693f1-160">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="693f1-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="693f1-161">Skontaktuj się z [zespołem pomocy technicznej klienta PagerDuty](https://www.pagerduty.com/support/) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="693f1-161">Contact [PagerDuty Client support team](https://www.pagerduty.com/support/) to get these values.</span></span> 

4. <span data-ttu-id="693f1-162">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="693f1-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Łącze pobierania certyfikatu](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_certificate.png) 

5. <span data-ttu-id="693f1-164">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="693f1-164">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-pagerduty-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="693f1-166">Na **konfiguracji PagerDuty** , kliknij przycisk **skonfigurować PagerDuty** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="693f1-166">On the **PagerDuty Configuration** section, click **Configure PagerDuty** to open **Configure sign-on** window.</span></span> <span data-ttu-id="693f1-167">Kopiuj **Sign-Out adresu URL i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="693f1-167">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfiguracja PagerDuty](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_configure.png) 

7. <span data-ttu-id="693f1-169">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy Pagerduty jako administrator.</span><span class="sxs-lookup"><span data-stu-id="693f1-169">In a different web browser window, log into your Pagerduty company site as an administrator.</span></span>

8. <span data-ttu-id="693f1-170">W menu u góry kliknij **ustawienia konta**.</span><span class="sxs-lookup"><span data-stu-id="693f1-170">In the menu on the top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="693f1-171">![Ustawienia konta](./media/active-directory-saas-pagerduty-tutorial/ic778535.png "ustawienia konta")</span><span class="sxs-lookup"><span data-stu-id="693f1-171">![Account Settings](./media/active-directory-saas-pagerduty-tutorial/ic778535.png "Account Settings")</span></span>

9. <span data-ttu-id="693f1-172">Kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="693f1-172">Click **Single Sign-on**.</span></span>
   
    <span data-ttu-id="693f1-173">![Logowanie jednokrotne](./media/active-directory-saas-pagerduty-tutorial/ic778536.png "logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="693f1-173">![Single sign-on](./media/active-directory-saas-pagerduty-tutorial/ic778536.png "Single sign-on")</span></span>

10. <span data-ttu-id="693f1-174">Na **włączyć logowanie jednokrotne (SSO)** wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="693f1-174">On the **Enable Single Sign-on (SSO)** page, perform the following steps:</span></span>
   
    <span data-ttu-id="693f1-175">![Włącz rejestrację jednokrotną](./media/active-directory-saas-pagerduty-tutorial/ic778537.png "Włącz rejestrację jednokrotną")</span><span class="sxs-lookup"><span data-stu-id="693f1-175">![Enable single sign-on](./media/active-directory-saas-pagerduty-tutorial/ic778537.png "Enable single sign-on")</span></span>
   
    <span data-ttu-id="693f1-176">a.</span><span class="sxs-lookup"><span data-stu-id="693f1-176">a.</span></span> <span data-ttu-id="693f1-177">Otwórz base-64 zakodowany certyfikat pobrany z portalu Azure w programie Notatnik, skopiuj zawartość go do Schowka, a następnie wklej go do **certyfikatu X.509** pole tekstowe</span><span class="sxs-lookup"><span data-stu-id="693f1-177">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox</span></span>
  
    <span data-ttu-id="693f1-178">b.</span><span class="sxs-lookup"><span data-stu-id="693f1-178">b.</span></span> <span data-ttu-id="693f1-179">W **adres URL logowania** pole tekstowe, Wklej **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="693f1-179">In the **Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="693f1-180">c.</span><span class="sxs-lookup"><span data-stu-id="693f1-180">c.</span></span> <span data-ttu-id="693f1-181">W **adresu URL wylogowania** pole tekstowe, Wklej **Sign-Out URL** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="693f1-181">In the **Logout URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="693f1-182">d.</span><span class="sxs-lookup"><span data-stu-id="693f1-182">d.</span></span> <span data-ttu-id="693f1-183">Wybierz **włączyć pojedynczego logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="693f1-183">Select **Turn on Single Sign-on**.</span></span>
 
    <span data-ttu-id="693f1-184">e.</span><span class="sxs-lookup"><span data-stu-id="693f1-184">e.</span></span> <span data-ttu-id="693f1-185">Kliknij przycisk **zapisać zmiany**.</span><span class="sxs-lookup"><span data-stu-id="693f1-185">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="693f1-186">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="693f1-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="693f1-187">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="693f1-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="693f1-188">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="693f1-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="693f1-189">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="693f1-189">Create an Azure AD test user</span></span>

<span data-ttu-id="693f1-190">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="693f1-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="693f1-192">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="693f1-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="693f1-193">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="693f1-193">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="693f1-195">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="693f1-195">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="693f1-197">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="693f1-197">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Przycisk Dodaj](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="693f1-199">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="693f1-199">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Okno dialogowe użytkownika](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="693f1-201">a.</span><span class="sxs-lookup"><span data-stu-id="693f1-201">a.</span></span> <span data-ttu-id="693f1-202">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="693f1-202">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="693f1-203">b.</span><span class="sxs-lookup"><span data-stu-id="693f1-203">b.</span></span> <span data-ttu-id="693f1-204">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="693f1-204">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="693f1-205">c.</span><span class="sxs-lookup"><span data-stu-id="693f1-205">c.</span></span> <span data-ttu-id="693f1-206">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="693f1-206">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="693f1-207">d.</span><span class="sxs-lookup"><span data-stu-id="693f1-207">d.</span></span> <span data-ttu-id="693f1-208">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="693f1-208">Click **Create**.</span></span>
 
### <a name="create-a-pagerduty-test-user"></a><span data-ttu-id="693f1-209">Tworzenie użytkownika testowego PagerDuty</span><span class="sxs-lookup"><span data-stu-id="693f1-209">Create a PagerDuty test user</span></span>

<span data-ttu-id="693f1-210">Aby umożliwić użytkownikom usługi Azure AD zalogować się do PagerDuty, musi być przygotowana do PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="693f1-210">To enable Azure AD users to log in to PagerDuty, they must be provisioned into PagerDuty.</span></span>  
<span data-ttu-id="693f1-211">W przypadku PagerDuty Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="693f1-211">In the case of PagerDuty, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="693f1-212">Możesz użyć innych Pagerduty użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Pagerduty do świadczenia usługi Azure Active Directory kont użytkowników.</span><span class="sxs-lookup"><span data-stu-id="693f1-212">You can use any other Pagerduty user account creation tools or APIs provided by Pagerduty to provision Azure Active Directory user accounts.</span></span>

<span data-ttu-id="693f1-213">**Aby udostępnić konta użytkownika, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="693f1-213">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="693f1-214">Zaloguj się do Twojego **Pagerduty** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="693f1-214">Log in to your **Pagerduty** tenant.</span></span>

2. <span data-ttu-id="693f1-215">W menu u góry kliknij **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="693f1-215">In the menu on the top, click **Users**.</span></span>

3. <span data-ttu-id="693f1-216">Kliknij przycisk **dodawania użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="693f1-216">Click **Add Users**.</span></span>
   
    <span data-ttu-id="693f1-217">![Dodawanie użytkowników](./media/active-directory-saas-pagerduty-tutorial/ic778539.png "Dodawanie użytkowników")</span><span class="sxs-lookup"><span data-stu-id="693f1-217">![Add Users](./media/active-directory-saas-pagerduty-tutorial/ic778539.png "Add Users")</span></span>

4.  <span data-ttu-id="693f1-218">Na **zaprosić zespołu** okna dialogowego, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="693f1-218">On the **Invite your team** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="693f1-219">![Zaproś zespołu](./media/active-directory-saas-pagerduty-tutorial/ic778540.png "zaprosić Twojego zespołu")</span><span class="sxs-lookup"><span data-stu-id="693f1-219">![Invite your team](./media/active-directory-saas-pagerduty-tutorial/ic778540.png "Invite your team")</span></span>

    <span data-ttu-id="693f1-220">a.</span><span class="sxs-lookup"><span data-stu-id="693f1-220">a.</span></span> <span data-ttu-id="693f1-221">Typ **pierwszy i nazwisko** użytkownika, takich jak **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="693f1-221">Type the **First and Last Name** of user like **Britta Simon**.</span></span> 
   
    <span data-ttu-id="693f1-222">b.</span><span class="sxs-lookup"><span data-stu-id="693f1-222">b.</span></span> <span data-ttu-id="693f1-223">Wprowadź **E-mail** adres użytkownika, takich jak  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="693f1-223">Enter **Email** address of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="693f1-224">c.</span><span class="sxs-lookup"><span data-stu-id="693f1-224">c.</span></span> <span data-ttu-id="693f1-225">Kliknij przycisk **Dodaj**, a następnie kliknij przycisk **wysyłania zaprasza**.</span><span class="sxs-lookup"><span data-stu-id="693f1-225">Click **Add**, and then click **Send Invites**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="693f1-226">Wszystkie dodane użytkownicy otrzymają zaproszenie, aby utworzyć konto PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="693f1-226">All added users will receive an invite to create a PagerDuty account.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="693f1-227">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="693f1-227">Assign the Azure AD test user</span></span>

<span data-ttu-id="693f1-228">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="693f1-228">In this section, you enable Britta Simon to use Azure single sign-on by granting access to PagerDuty.</span></span>

![Przypisanie roli użytkownika][200]

<span data-ttu-id="693f1-230">**Aby przypisać Simona Britta PagerDuty, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="693f1-230">**To assign Britta Simon to PagerDuty, perform the following steps:**</span></span>

1. <span data-ttu-id="693f1-231">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="693f1-231">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="693f1-233">Na liście aplikacji zaznacz **PagerDuty**.</span><span class="sxs-lookup"><span data-stu-id="693f1-233">In the applications list, select **PagerDuty**.</span></span>

    ![Łącze PagerDuty na liście aplikacji](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_app.png) 

3. <span data-ttu-id="693f1-235">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="693f1-235">In the menu on the left, click **Users and groups**.</span></span>

    ![Łącze "Użytkownicy i grupy"][202]

4. <span data-ttu-id="693f1-237">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="693f1-237">Click **Add** button.</span></span> <span data-ttu-id="693f1-238">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="693f1-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![W okienku Dodaj przydziału][203]

5. <span data-ttu-id="693f1-240">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="693f1-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="693f1-241">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="693f1-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="693f1-242">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="693f1-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="693f1-243">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="693f1-243">Test single sign-on</span></span>

<span data-ttu-id="693f1-244">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="693f1-244">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="693f1-245">Po kliknięciu kafelka PagerDuty w Panelyou dostępu należy pobrać automatycznie zalogowane PagerDuty aplikacji.</span><span class="sxs-lookup"><span data-stu-id="693f1-245">When you click the PagerDuty tile in the Access Panelyou should get automatically signed-on to your PagerDuty application.</span></span>

<span data-ttu-id="693f1-246">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="693f1-246">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="693f1-247">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="693f1-247">Additional resources</span></span>

* [<span data-ttu-id="693f1-248">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="693f1-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="693f1-249">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="693f1-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_203.png

