---
title: 'Samouczek: Integracji Azure Active Directory z Kintone | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Kintone."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2b947dc-e1a8-4f5f-b40e-2c5180648e4f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: e5e847c12cba3611ce7ea2c3e956dbd55b1e0cac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kintone"></a><span data-ttu-id="c0f3f-103">Samouczek: Integracji Azure Active Directory z Kintone</span><span class="sxs-lookup"><span data-stu-id="c0f3f-103">Tutorial: Azure Active Directory integration with Kintone</span></span>

<span data-ttu-id="c0f3f-104">Z tego samouczka dowiesz się integrowanie Kintone z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c0f3f-104">In this tutorial, you learn how to integrate Kintone with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c0f3f-105">Integracja z usługą Azure AD Kintone zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="c0f3f-105">Integrating Kintone with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c0f3f-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Kintone</span><span class="sxs-lookup"><span data-stu-id="c0f3f-106">You can control in Azure AD who has access to Kintone</span></span>
- <span data-ttu-id="c0f3f-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Kintone (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0f3f-107">You can enable your users to automatically get signed-on to Kintone (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c0f3f-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c0f3f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c0f3f-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c0f3f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c0f3f-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c0f3f-110">Prerequisites</span></span>

<span data-ttu-id="c0f3f-111">Aby skonfigurować integrację usługi Azure AD z Kintone, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="c0f3f-111">To configure Azure AD integration with Kintone, you need the following items:</span></span>

- <span data-ttu-id="c0f3f-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0f3f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c0f3f-113">Kintone logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="c0f3f-113">A Kintone single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c0f3f-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c0f3f-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="c0f3f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c0f3f-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c0f3f-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c0f3f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c0f3f-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="c0f3f-118">Scenario description</span></span>
<span data-ttu-id="c0f3f-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c0f3f-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="c0f3f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c0f3f-121">Dodawanie Kintone z galerii</span><span class="sxs-lookup"><span data-stu-id="c0f3f-121">Adding Kintone from the gallery</span></span>
2. <span data-ttu-id="c0f3f-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="c0f3f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kintone-from-the-gallery"></a><span data-ttu-id="c0f3f-123">Dodawanie Kintone z galerii</span><span class="sxs-lookup"><span data-stu-id="c0f3f-123">Adding Kintone from the gallery</span></span>
<span data-ttu-id="c0f3f-124">Aby skonfigurować integrację usługi Azure AD Kintone, należy dodać Kintone z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-124">To configure the integration of Kintone into Azure AD, you need to add Kintone from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c0f3f-125">**Aby dodać Kintone z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c0f3f-125">**To add Kintone from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c0f3f-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="c0f3f-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c0f3f-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="c0f3f-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="c0f3f-133">W polu wyszukiwania wpisz **Kintone**.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-133">In the search box, type **Kintone**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_search.png)

5. <span data-ttu-id="c0f3f-135">W panelu wyników wybierz **Kintone**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-135">In the results panel, select **Kintone**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c0f3f-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="c0f3f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c0f3f-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Kintone w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-138">In this section, you configure and test Azure AD single sign-on with Kintone based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c0f3f-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Kintone jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kintone is to a user in Azure AD.</span></span> <span data-ttu-id="c0f3f-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Kintone musi się.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-140">In other words, a link relationship between an Azure AD user and the related user in Kintone needs to be established.</span></span>

<span data-ttu-id="c0f3f-141">W Kintone, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-141">In Kintone, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c0f3f-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Kintone, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="c0f3f-142">To configure and test Azure AD single sign-on with Kintone, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c0f3f-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c0f3f-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c0f3f-145">**[Tworzenie użytkownika testowego Kintone](#creating-a-kintone-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Kintone połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-145">**[Creating a Kintone test user](#creating-a-kintone-test-user)** - to have a counterpart of Britta Simon in Kintone that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c0f3f-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c0f3f-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c0f3f-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="c0f3f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c0f3f-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Kintone.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kintone application.</span></span>

<span data-ttu-id="c0f3f-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Kintone, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c0f3f-150">**To configure Azure AD single sign-on with Kintone, perform the following steps:**</span></span>

1. <span data-ttu-id="c0f3f-151">W portalu Azure na **Kintone** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-151">In the Azure portal, on the **Kintone** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="c0f3f-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_samlbase.png)

3. <span data-ttu-id="c0f3f-155">Na **Kintone domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c0f3f-155">On the **Kintone Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_url.png)

    <span data-ttu-id="c0f3f-157">a.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-157">a.</span></span> <span data-ttu-id="c0f3f-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.kintone.com`</span><span class="sxs-lookup"><span data-stu-id="c0f3f-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.kintone.com`</span></span>

    <span data-ttu-id="c0f3f-159">b.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-159">b.</span></span> <span data-ttu-id="c0f3f-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="c0f3f-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.cybozu.com`|
    | `https://<companyname>.kintone.com`|

    > [!NOTE] 
    > <span data-ttu-id="c0f3f-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-161">These values are not real.</span></span> <span data-ttu-id="c0f3f-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c0f3f-163">Skontaktuj się z [zespołem pomocy technicznej klienta Kintone](https://www.kintone.com/contact/) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-163">Contact [Kintone Client support team](https://www.kintone.com/contact/) to get these values.</span></span> 
 
4. <span data-ttu-id="c0f3f-164">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_certificate.png) 

5. <span data-ttu-id="c0f3f-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kintone-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c0f3f-168">Na **konfiguracji Kintone** , kliknij przycisk **skonfigurować Kintone** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-168">On the **Kintone Configuration** section, click **Configure Kintone** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c0f3f-169">Kopiuj **Sign-Out adresu URL i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="c0f3f-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_configure.png) 

7. <span data-ttu-id="c0f3f-171">W oknie przeglądarki innej witryny sieci web, zaloguj się do Twojego **Kintone** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-171">In a different web browser window, log into your **Kintone** company site as an administrator.</span></span>

8. <span data-ttu-id="c0f3f-172">Kliknij przycisk **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-172">Click **Settings**.</span></span>
   
    <span data-ttu-id="c0f3f-173">![Ustawienia](./media/active-directory-saas-kintone-tutorial/ic785879.png "ustawienia")</span><span class="sxs-lookup"><span data-stu-id="c0f3f-173">![Settings](./media/active-directory-saas-kintone-tutorial/ic785879.png "Settings")</span></span>

9. <span data-ttu-id="c0f3f-174">Kliknij przycisk **użytkownicy i administrowanie systemem**.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-174">Click **Users & System Administration**.</span></span>
   
    <span data-ttu-id="c0f3f-175">![Użytkownicy i administrowanie systemem](./media/active-directory-saas-kintone-tutorial/ic785880.png "użytkowników & administracji systemu")</span><span class="sxs-lookup"><span data-stu-id="c0f3f-175">![Users & System Administration](./media/active-directory-saas-kintone-tutorial/ic785880.png "Users & System Administration")</span></span>

10. <span data-ttu-id="c0f3f-176">W obszarze **Administracja systemu \> zabezpieczeń** kliknij **logowania**.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-176">Under **System Administration \> Security** click **Login**.</span></span>
   
    <span data-ttu-id="c0f3f-177">![Logowania](./media/active-directory-saas-kintone-tutorial/ic785881.png "logowania")</span><span class="sxs-lookup"><span data-stu-id="c0f3f-177">![Login](./media/active-directory-saas-kintone-tutorial/ic785881.png "Login")</span></span>

11. <span data-ttu-id="c0f3f-178">Kliknij przycisk **uwierzytelnianie Włącz SAML**.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-178">Click **Enable SAML authentication**.</span></span>
   
    <span data-ttu-id="c0f3f-179">![Uwierzytelnianie SAML](./media/active-directory-saas-kintone-tutorial/ic785882.png "uwierzytelnianie SAML")</span><span class="sxs-lookup"><span data-stu-id="c0f3f-179">![SAML Authentication](./media/active-directory-saas-kintone-tutorial/ic785882.png "SAML Authentication")</span></span>

12. <span data-ttu-id="c0f3f-180">W sekcji uwierzytelnianie SAML wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c0f3f-180">In the SAML Authentication section, perform the following steps:</span></span>
    
    <span data-ttu-id="c0f3f-181">![Uwierzytelnianie SAML](./media/active-directory-saas-kintone-tutorial/ic785883.png "uwierzytelnianie SAML")</span><span class="sxs-lookup"><span data-stu-id="c0f3f-181">![SAML Authentication](./media/active-directory-saas-kintone-tutorial/ic785883.png "SAML Authentication")</span></span>
    
    <span data-ttu-id="c0f3f-182">a.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-182">a.</span></span> <span data-ttu-id="c0f3f-183">W **adres URL logowania** pole tekstowe, Wklej wartość **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-183">In the **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="c0f3f-184">b.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-184">b.</span></span> <span data-ttu-id="c0f3f-185">W **adresu URL wylogowania** pole tekstowe, Wklej wartość **Sign-Out URL** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-185">In the **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="c0f3f-186">c.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-186">c.</span></span> <span data-ttu-id="c0f3f-187">Kliknij przycisk **Przeglądaj** przekazać pobranego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-187">Click **Browse** to upload your downloaded certificate.</span></span>
    
    <span data-ttu-id="c0f3f-188">d.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-188">d.</span></span> <span data-ttu-id="c0f3f-189">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-189">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="c0f3f-190">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="c0f3f-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c0f3f-191">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c0f3f-192">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c0f3f-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c0f3f-193">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0f3f-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="c0f3f-194">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="c0f3f-196">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c0f3f-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c0f3f-197">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kintone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c0f3f-199">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kintone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c0f3f-201">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kintone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c0f3f-203">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c0f3f-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kintone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c0f3f-205">a.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-205">a.</span></span> <span data-ttu-id="c0f3f-206">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c0f3f-207">b.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-207">b.</span></span> <span data-ttu-id="c0f3f-208">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c0f3f-209">c.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-209">c.</span></span> <span data-ttu-id="c0f3f-210">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c0f3f-211">d.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-211">d.</span></span> <span data-ttu-id="c0f3f-212">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-212">Click **Create**.</span></span>
 
### <a name="creating-a-kintone-test-user"></a><span data-ttu-id="c0f3f-213">Tworzenie użytkownika testowego Kintone</span><span class="sxs-lookup"><span data-stu-id="c0f3f-213">Creating a Kintone test user</span></span>

<span data-ttu-id="c0f3f-214">Aby umożliwić użytkownikom usługi Azure AD zalogować się do Kintone, musi być przygotowana do Kintone.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-214">To enable Azure AD users to log in to Kintone, they must be provisioned into Kintone.</span></span>  
<span data-ttu-id="c0f3f-215">W przypadku Kintone Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-215">In the case of Kintone, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="c0f3f-216">Aby udostępnić konta użytkownika, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c0f3f-216">To provision a user account, perform the following steps:</span></span>

1. <span data-ttu-id="c0f3f-217">Zaloguj się do Twojego **Kintone** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-217">Log in to your **Kintone** company site as an administrator.</span></span>

2. <span data-ttu-id="c0f3f-218">Kliknij przycisk **ustawienie**.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-218">Click **Setting**.</span></span>
   
    <span data-ttu-id="c0f3f-219">![Ustawienia](./media/active-directory-saas-kintone-tutorial/ic785879.png "ustawienia")</span><span class="sxs-lookup"><span data-stu-id="c0f3f-219">![Settings](./media/active-directory-saas-kintone-tutorial/ic785879.png "Settings")</span></span>

3. <span data-ttu-id="c0f3f-220">Kliknij przycisk **użytkownicy i administrowanie systemem**.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-220">Click **Users & System Administration**.</span></span>
   
    <span data-ttu-id="c0f3f-221">![Administracja systemu & użytkownika](./media/active-directory-saas-kintone-tutorial/ic785880.png "Administracja systemu & użytkownika")</span><span class="sxs-lookup"><span data-stu-id="c0f3f-221">![User & System Administration](./media/active-directory-saas-kintone-tutorial/ic785880.png "User & System Administration")</span></span>

4. <span data-ttu-id="c0f3f-222">W obszarze **Administracja użytkownikami**, kliknij przycisk **działów i użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-222">Under **User Administration**, click **Departments & Users**.</span></span>
   
    <span data-ttu-id="c0f3f-223">![Dział & użytkowników](./media/active-directory-saas-kintone-tutorial/ic785888.png "działu & użytkowników")</span><span class="sxs-lookup"><span data-stu-id="c0f3f-223">![Department & Users](./media/active-directory-saas-kintone-tutorial/ic785888.png "Department & Users")</span></span>

5. <span data-ttu-id="c0f3f-224">Kliknij przycisk **nowego użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-224">Click **New User**.</span></span>
   
    <span data-ttu-id="c0f3f-225">![Nowi użytkownicy](./media/active-directory-saas-kintone-tutorial/ic785889.png "nowych użytkowników")</span><span class="sxs-lookup"><span data-stu-id="c0f3f-225">![New Users](./media/active-directory-saas-kintone-tutorial/ic785889.png "New Users")</span></span>

6. <span data-ttu-id="c0f3f-226">W **nowego użytkownika** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c0f3f-226">In the **New User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="c0f3f-227">![Nowi użytkownicy](./media/active-directory-saas-kintone-tutorial/ic785890.png "nowych użytkowników")</span><span class="sxs-lookup"><span data-stu-id="c0f3f-227">![New Users](./media/active-directory-saas-kintone-tutorial/ic785890.png "New Users")</span></span>
   
    <span data-ttu-id="c0f3f-228">a.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-228">a.</span></span> <span data-ttu-id="c0f3f-229">Wpisz **Nazwa wyświetlana**, **nazwa logowania**, **nowe hasło**, **Potwierdź hasło**, **adres E-mail**oraz innych szczegółów prawidłowego konta usługi AAD ustanawiane do powiązanych pól tekstowych.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-229">Type a **Display Name**, **Login Name**, **New Password**, **Confirm Password**, **E-mail Address**, and other details of a valid AAD account you want to provision into the related textboxes.</span></span>
 
    <span data-ttu-id="c0f3f-230">b.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-230">b.</span></span> <span data-ttu-id="c0f3f-231">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-231">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="c0f3f-232">Możesz użyć innych Kintone użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Kintone do kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-232">You can use any other Kintone user account creation tools or APIs provided by Kintone to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c0f3f-233">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0f3f-233">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c0f3f-234">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Kintone.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-234">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kintone.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="c0f3f-236">**Aby przypisać Simona Britta Kintone, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c0f3f-236">**To assign Britta Simon to Kintone, perform the following steps:**</span></span>

1. <span data-ttu-id="c0f3f-237">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-237">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="c0f3f-239">Na liście aplikacji zaznacz **Kintone**.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-239">In the applications list, select **Kintone**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_app.png) 

3. <span data-ttu-id="c0f3f-241">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-241">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="c0f3f-243">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-243">Click **Add** button.</span></span> <span data-ttu-id="c0f3f-244">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="c0f3f-246">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c0f3f-247">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c0f3f-248">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c0f3f-249">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="c0f3f-249">Testing single sign-on</span></span>

<span data-ttu-id="c0f3f-250">Celem tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-250">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c0f3f-251">Po kliknięciu kafelka Kintone w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Kintone.</span><span class="sxs-lookup"><span data-stu-id="c0f3f-251">When you click the Kintone tile in the Access Panel, you should get automatically signed-on to your Kintone application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c0f3f-252">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="c0f3f-252">Additional resources</span></span>

* [<span data-ttu-id="c0f3f-253">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c0f3f-253">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c0f3f-254">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c0f3f-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_203.png

