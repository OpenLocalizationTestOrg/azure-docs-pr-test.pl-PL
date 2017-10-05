---
title: 'Samouczek: Integracji Azure Active Directory z ThousandEyes | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i ThousandEyes."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 790e3f1e-1591-4dd6-87df-590b7bf8b4ba
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: jeedes
ms.openlocfilehash: 392add7d5f0a55598b8b90760f5c3f2d1e67ac02
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thousandeyes"></a><span data-ttu-id="1e77e-103">Samouczek: Integracji Azure Active Directory z ThousandEyes</span><span class="sxs-lookup"><span data-stu-id="1e77e-103">Tutorial: Azure Active Directory integration with ThousandEyes</span></span>

<span data-ttu-id="1e77e-104">Z tego samouczka dowiesz się integrowanie ThousandEyes z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1e77e-104">In this tutorial, you learn how to integrate ThousandEyes with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1e77e-105">Integracja z usługą Azure AD ThousandEyes zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="1e77e-105">Integrating ThousandEyes with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1e77e-106">Można kontrolować w usłudze Azure AD, który ma dostęp do ThousandEyes</span><span class="sxs-lookup"><span data-stu-id="1e77e-106">You can control in Azure AD who has access to ThousandEyes</span></span>
- <span data-ttu-id="1e77e-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do ThousandEyes (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e77e-107">You can enable your users to automatically get signed-on to ThousandEyes (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1e77e-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="1e77e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1e77e-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1e77e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1e77e-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1e77e-110">Prerequisites</span></span>

<span data-ttu-id="1e77e-111">Aby skonfigurować integrację usługi Azure AD z ThousandEyes, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="1e77e-111">To configure Azure AD integration with ThousandEyes, you need the following items:</span></span>

- <span data-ttu-id="1e77e-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e77e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1e77e-113">ThousandEyes logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="1e77e-113">A ThousandEyes single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1e77e-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="1e77e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1e77e-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="1e77e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1e77e-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="1e77e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1e77e-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna tutaj: [oferta wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1e77e-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1e77e-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="1e77e-118">Scenario description</span></span>
<span data-ttu-id="1e77e-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="1e77e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1e77e-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="1e77e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1e77e-121">Dodawanie ThousandEyes z galerii</span><span class="sxs-lookup"><span data-stu-id="1e77e-121">Adding ThousandEyes from the gallery</span></span>
2. <span data-ttu-id="1e77e-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="1e77e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thousandeyes-from-the-gallery"></a><span data-ttu-id="1e77e-123">Dodawanie ThousandEyes z galerii</span><span class="sxs-lookup"><span data-stu-id="1e77e-123">Adding ThousandEyes from the gallery</span></span>
<span data-ttu-id="1e77e-124">Aby skonfigurować integrację usługi Azure AD ThousandEyes, należy dodać ThousandEyes z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="1e77e-124">To configure the integration of ThousandEyes into Azure AD, you need to add ThousandEyes from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1e77e-125">**Aby dodać ThousandEyes z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="1e77e-125">**To add ThousandEyes from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1e77e-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="1e77e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="1e77e-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="1e77e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1e77e-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="1e77e-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="1e77e-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1e77e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="1e77e-133">W polu wyszukiwania wpisz **ThousandEyes**.</span><span class="sxs-lookup"><span data-stu-id="1e77e-133">In the search box, type **ThousandEyes**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_search.png)

5. <span data-ttu-id="1e77e-135">W panelu wyników wybierz **ThousandEyes**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="1e77e-135">In the results panel, select **ThousandEyes**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1e77e-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="1e77e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1e77e-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z ThousandEyes w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="1e77e-138">In this section, you configure and test Azure AD single sign-on with ThousandEyes based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1e77e-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w ThousandEyes jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1e77e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ThousandEyes is to a user in Azure AD.</span></span> <span data-ttu-id="1e77e-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w ThousandEyes musi się.</span><span class="sxs-lookup"><span data-stu-id="1e77e-140">In other words, a link relationship between an Azure AD user and the related user in ThousandEyes needs to be established.</span></span>

<span data-ttu-id="1e77e-141">W ThousandEyes, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="1e77e-141">In ThousandEyes, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1e77e-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z ThousandEyes, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="1e77e-142">To configure and test Azure AD single sign-on with ThousandEyes, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1e77e-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="1e77e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1e77e-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="1e77e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1e77e-145">**[Tworzenie użytkownika testowego ThousandEyes](#creating-a-thousandeyes-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta ThousandEyes połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1e77e-145">**[Creating a ThousandEyes test user](#creating-a-thousandeyes-test-user)** - to have a counterpart of Britta Simon in ThousandEyes that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1e77e-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="1e77e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1e77e-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="1e77e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1e77e-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="1e77e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1e77e-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="1e77e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ThousandEyes application.</span></span>

<span data-ttu-id="1e77e-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z ThousandEyes, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="1e77e-150">**To configure Azure AD single sign-on with ThousandEyes, perform the following steps:**</span></span>

1. <span data-ttu-id="1e77e-151">W portalu Azure na **ThousandEyes** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="1e77e-151">In the Azure portal, on the **ThousandEyes** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="1e77e-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="1e77e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_samlbase.png)

3. <span data-ttu-id="1e77e-155">Na **ThousandEyes domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="1e77e-155">On the **ThousandEyes Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_url.png)

    <span data-ttu-id="1e77e-157">W **adres URL logowania** tekstowym, wpisz adres URL jako:`https://app.thousandeyes.com/login/sso`</span><span class="sxs-lookup"><span data-stu-id="1e77e-157">In the **Sign-on URL** textbox, type a URL as: `https://app.thousandeyes.com/login/sso`</span></span>

4. <span data-ttu-id="1e77e-158">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="1e77e-158">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_certificate.png) 

5. <span data-ttu-id="1e77e-160">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="1e77e-160">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1e77e-162">Na **konfiguracji ThousandEyes** , kliknij przycisk **skonfigurować ThousandEyes** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="1e77e-162">On the **ThousandEyes Configuration** section, click **Configure ThousandEyes** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1e77e-163">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="1e77e-163">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_configure.png) 

7. <span data-ttu-id="1e77e-165">W oknie przeglądarki innej witryny sieci web, zaloguj się na Twojej **ThousandEyes** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="1e77e-165">In a different web browser window, sign on to your **ThousandEyes** company site as an administrator.</span></span>

8. <span data-ttu-id="1e77e-166">W menu u góry kliknij **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="1e77e-166">In the menu on the top, click **Settings**.</span></span>
   
    <span data-ttu-id="1e77e-167">![Ustawienia](./media/active-directory-saas-thousandeyes-tutorial/ic790066.png "ustawienia")</span><span class="sxs-lookup"><span data-stu-id="1e77e-167">![Settings](./media/active-directory-saas-thousandeyes-tutorial/ic790066.png "Settings")</span></span>

9. <span data-ttu-id="1e77e-168">Kliknij przycisk **konta**</span><span class="sxs-lookup"><span data-stu-id="1e77e-168">Click **Account**</span></span>
   
    <span data-ttu-id="1e77e-169">![Konto](./media/active-directory-saas-thousandeyes-tutorial/ic790067.png "konta")</span><span class="sxs-lookup"><span data-stu-id="1e77e-169">![Account](./media/active-directory-saas-thousandeyes-tutorial/ic790067.png "Account")</span></span>

10. <span data-ttu-id="1e77e-170">Kliknij przycisk **zabezpieczeń i uwierzytelniania** kartę.</span><span class="sxs-lookup"><span data-stu-id="1e77e-170">Click the **Security & Authentication** tab.</span></span>
   
    <span data-ttu-id="1e77e-171">![Bezpieczeństwo i uwierzytelniania](./media/active-directory-saas-thousandeyes-tutorial/ic790068.png "zabezpieczeń i uwierzytelniania")</span><span class="sxs-lookup"><span data-stu-id="1e77e-171">![Security & Authentication](./media/active-directory-saas-thousandeyes-tutorial/ic790068.png "Security & Authentication")</span></span>

11. <span data-ttu-id="1e77e-172">W **ustawienia logowania jednokrotnego** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="1e77e-172">In the **Setup Single Sign-On** section, perform the following steps:</span></span>
   
    <span data-ttu-id="1e77e-173">![Konfiguracja rejestracji jednokrotnej](./media/active-directory-saas-thousandeyes-tutorial/ic790069.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="1e77e-173">![Setup Single Sign-On](./media/active-directory-saas-thousandeyes-tutorial/ic790069.png "Setup Single Sign-On")</span></span>
  
    <span data-ttu-id="1e77e-174">a.</span><span class="sxs-lookup"><span data-stu-id="1e77e-174">a.</span></span> <span data-ttu-id="1e77e-175">Wybierz **Włącz rejestrację jednokrotną**.</span><span class="sxs-lookup"><span data-stu-id="1e77e-175">Select **Enable Single Sign-On**.</span></span>
  
    <span data-ttu-id="1e77e-176">b.</span><span class="sxs-lookup"><span data-stu-id="1e77e-176">b.</span></span> <span data-ttu-id="1e77e-177">W **adres URL strony logowania** pole tekstowe, Wklej **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="1e77e-177">In **Login Page URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="1e77e-178">c.</span><span class="sxs-lookup"><span data-stu-id="1e77e-178">c.</span></span> <span data-ttu-id="1e77e-179">W **adres URL strony wylogowania** pole tekstowe, Wklej **Sign-Out URL** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="1e77e-179">In **Logout Page URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="1e77e-180">d.</span><span class="sxs-lookup"><span data-stu-id="1e77e-180">d.</span></span> <span data-ttu-id="1e77e-181">**Wystawca dostawcy tożsamości** pole tekstowe, Wklej **identyfikator jednostki SAML** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="1e77e-181">**Identity Provider Issuer** textbox, paste **SAML Entity ID** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="1e77e-182">e.</span><span class="sxs-lookup"><span data-stu-id="1e77e-182">e.</span></span> <span data-ttu-id="1e77e-183">W **certyfikatu weryfikacji**, kliknij przycisk **wybierz plik**, a następnie przekaż certyfikat został pobrany z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="1e77e-183">In **Verification Certificate**, click **Choose file**, and then upload the certificate you have downloaded from Azure portal.</span></span>
  
    <span data-ttu-id="1e77e-184">f.</span><span class="sxs-lookup"><span data-stu-id="1e77e-184">f.</span></span> <span data-ttu-id="1e77e-185">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="1e77e-185">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="1e77e-186">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="1e77e-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1e77e-187">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="1e77e-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1e77e-188">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1e77e-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1e77e-189">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e77e-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="1e77e-190">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="1e77e-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="1e77e-192">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="1e77e-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1e77e-193">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="1e77e-193">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1e77e-195">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="1e77e-195">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1e77e-197">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1e77e-197">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1e77e-199">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="1e77e-199">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1e77e-201">a.</span><span class="sxs-lookup"><span data-stu-id="1e77e-201">a.</span></span> <span data-ttu-id="1e77e-202">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1e77e-202">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1e77e-203">b.</span><span class="sxs-lookup"><span data-stu-id="1e77e-203">b.</span></span> <span data-ttu-id="1e77e-204">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1e77e-204">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1e77e-205">c.</span><span class="sxs-lookup"><span data-stu-id="1e77e-205">c.</span></span> <span data-ttu-id="1e77e-206">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="1e77e-206">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1e77e-207">d.</span><span class="sxs-lookup"><span data-stu-id="1e77e-207">d.</span></span> <span data-ttu-id="1e77e-208">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="1e77e-208">Click **Create**.</span></span>
 
### <a name="creating-a-thousandeyes-test-user"></a><span data-ttu-id="1e77e-209">Tworzenie użytkownika testowego ThousandEyes</span><span class="sxs-lookup"><span data-stu-id="1e77e-209">Creating a ThousandEyes test user</span></span>

<span data-ttu-id="1e77e-210">Aby włączyć użytkowników usługi Azure AD zalogować się do ThousandEyes, musi być przygotowana do ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="1e77e-210">In order to enable Azure AD users to log into ThousandEyes, they must be provisioned into ThousandEyes.</span></span>  
<span data-ttu-id="1e77e-211">W przypadku ThousandEyes Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="1e77e-211">In the case of ThousandEyes, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="1e77e-212">Możesz użyć innych ThousandEyes użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez ThousandEyes do świadczenia usługi Azure Active Directory kont użytkowników.</span><span class="sxs-lookup"><span data-stu-id="1e77e-212">You can use any other ThousandEyes user account creation tools or APIs provided by ThousandEyes to provision Azure Active Directory user accounts.</span></span>

<span data-ttu-id="1e77e-213">**Aby udostępnić konta użytkownika do ThousandEyes, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="1e77e-213">**To provision a user account to ThousandEyes, perform the following steps:**</span></span>

1. <span data-ttu-id="1e77e-214">Zaloguj się do witryny firmy ThousandEyes jako administrator.</span><span class="sxs-lookup"><span data-stu-id="1e77e-214">Log into your ThousandEyes company site as an administrator.</span></span>

2. <span data-ttu-id="1e77e-215">Kliknij przycisk **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="1e77e-215">Click **Settings**.</span></span>
   
    <span data-ttu-id="1e77e-216">![Ustawienia](./media/active-directory-saas-thousandeyes-tutorial/IC790066.png "ustawienia")</span><span class="sxs-lookup"><span data-stu-id="1e77e-216">![Settings](./media/active-directory-saas-thousandeyes-tutorial/IC790066.png "Settings")</span></span>

3. <span data-ttu-id="1e77e-217">Kliknij przycisk **konta**.</span><span class="sxs-lookup"><span data-stu-id="1e77e-217">Click **Account**.</span></span>
   
    <span data-ttu-id="1e77e-218">![Konto](./media/active-directory-saas-thousandeyes-tutorial/IC790067.png "konta")</span><span class="sxs-lookup"><span data-stu-id="1e77e-218">![Account](./media/active-directory-saas-thousandeyes-tutorial/IC790067.png "Account")</span></span>

4. <span data-ttu-id="1e77e-219">Kliknij przycisk **konta & użytkowników** kartę.</span><span class="sxs-lookup"><span data-stu-id="1e77e-219">Click the **Accounts & Users** tab.</span></span>
   
    <span data-ttu-id="1e77e-220">![Konta & użytkowników](./media/active-directory-saas-thousandeyes-tutorial/IC790073.png "konta & użytkowników")</span><span class="sxs-lookup"><span data-stu-id="1e77e-220">![Accounts & Users](./media/active-directory-saas-thousandeyes-tutorial/IC790073.png "Accounts & Users")</span></span>

5. <span data-ttu-id="1e77e-221">W **Dodawanie użytkowników i kont** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="1e77e-221">In the **Add Users & Accounts** section, perform the following steps:</span></span>
   
    <span data-ttu-id="1e77e-222">![Dodaj konta użytkowników](./media/active-directory-saas-thousandeyes-tutorial/IC790074.png "dodawania kont użytkowników")</span><span class="sxs-lookup"><span data-stu-id="1e77e-222">![Add User Accounts](./media/active-directory-saas-thousandeyes-tutorial/IC790074.png "Add User Accounts")</span></span>   
  
    <span data-ttu-id="1e77e-223">a.</span><span class="sxs-lookup"><span data-stu-id="1e77e-223">a.</span></span> <span data-ttu-id="1e77e-224">W **nazwa** tekstowym, wpisz nazwę użytkownika, takich jak **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="1e77e-224">In **Name** textbox, type the name of user like **Britta Simon**.</span></span>

    <span data-ttu-id="1e77e-225">b.</span><span class="sxs-lookup"><span data-stu-id="1e77e-225">b.</span></span> <span data-ttu-id="1e77e-226">W **E-mail** tekstowym, wpisz adres e-mail użytkownika, takich jak  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="1e77e-226">In **Email** textbox, type the email of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="1e77e-227">b.</span><span class="sxs-lookup"><span data-stu-id="1e77e-227">b.</span></span> <span data-ttu-id="1e77e-228">Kliknij przycisk **Dodaj nowego użytkownika do konta**.</span><span class="sxs-lookup"><span data-stu-id="1e77e-228">Click **Add New User to Account**.</span></span>
      
     >[!NOTE]
     ><span data-ttu-id="1e77e-229">Właściciel konta usługi Azure Active Directory otrzyma wiadomość e-mail, łącznie z łączem do potwierdzenia i Aktywuj konta.</span><span class="sxs-lookup"><span data-stu-id="1e77e-229">The Azure Active Directory account holder will get an email including a link to confirm and activate the account.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1e77e-230">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e77e-230">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1e77e-231">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="1e77e-231">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ThousandEyes.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="1e77e-233">**Aby przypisać Simona Britta ThousandEyes, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="1e77e-233">**To assign Britta Simon to ThousandEyes, perform the following steps:**</span></span>

1. <span data-ttu-id="1e77e-234">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="1e77e-234">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="1e77e-236">Na liście aplikacji zaznacz **ThousandEyes**.</span><span class="sxs-lookup"><span data-stu-id="1e77e-236">In the applications list, select **ThousandEyes**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_app.png) 

3. <span data-ttu-id="1e77e-238">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="1e77e-238">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="1e77e-240">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="1e77e-240">Click **Add** button.</span></span> <span data-ttu-id="1e77e-241">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1e77e-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="1e77e-243">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="1e77e-243">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1e77e-244">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1e77e-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1e77e-245">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1e77e-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1e77e-246">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="1e77e-246">Testing single sign-on</span></span>

<span data-ttu-id="1e77e-247">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="1e77e-247">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1e77e-248">Po kliknięciu kafelka ThousandEyes w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="1e77e-248">When you click the ThousandEyes tile in the Access Panel, you should get automatically signed-on to your ThousandEyes application.</span></span>

<span data-ttu-id="1e77e-249">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1e77e-249">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1e77e-250">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="1e77e-250">Additional resources</span></span>

* [<span data-ttu-id="1e77e-251">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1e77e-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1e77e-252">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1e77e-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_203.png

