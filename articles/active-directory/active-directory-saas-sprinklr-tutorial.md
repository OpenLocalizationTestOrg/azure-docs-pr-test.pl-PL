---
title: 'Samouczek: Integracji Azure Active Directory z Sprinklr | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Sprinklr."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b33938a1-25a5-484c-8e75-7dc6de2d534d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 6e1622cd55e3b0e8063604ac9dc0cb0673fa9753
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sprinklr"></a><span data-ttu-id="a5144-103">Samouczek: Integracji Azure Active Directory z Sprinklr</span><span class="sxs-lookup"><span data-stu-id="a5144-103">Tutorial: Azure Active Directory integration with Sprinklr</span></span>

<span data-ttu-id="a5144-104">Z tego samouczka dowiesz się integrowanie Sprinklr z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a5144-104">In this tutorial, you learn how to integrate Sprinklr with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a5144-105">Integracja z usługą Azure AD Sprinklr zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="a5144-105">Integrating Sprinklr with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a5144-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Sprinklr</span><span class="sxs-lookup"><span data-stu-id="a5144-106">You can control in Azure AD who has access to Sprinklr</span></span>
- <span data-ttu-id="a5144-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Sprinklr (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a5144-107">You can enable your users to automatically get signed-on to Sprinklr (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a5144-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="a5144-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a5144-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a5144-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a5144-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a5144-110">Prerequisites</span></span>

<span data-ttu-id="a5144-111">Aby skonfigurować integrację usługi Azure AD z Sprinklr, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="a5144-111">To configure Azure AD integration with Sprinklr, you need the following items:</span></span>

- <span data-ttu-id="a5144-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a5144-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a5144-113">Sprinklr jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="a5144-113">A Sprinklr single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a5144-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="a5144-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a5144-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="a5144-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a5144-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="a5144-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a5144-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a5144-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a5144-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="a5144-118">Scenario description</span></span>
<span data-ttu-id="a5144-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="a5144-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a5144-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="a5144-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a5144-121">Dodawanie Sprinklr z galerii</span><span class="sxs-lookup"><span data-stu-id="a5144-121">Adding Sprinklr from the gallery</span></span>
2. <span data-ttu-id="a5144-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="a5144-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sprinklr-from-the-gallery"></a><span data-ttu-id="a5144-123">Dodawanie Sprinklr z galerii</span><span class="sxs-lookup"><span data-stu-id="a5144-123">Adding Sprinklr from the gallery</span></span>
<span data-ttu-id="a5144-124">Aby skonfigurować integrację usługi Azure AD Sprinklr, należy dodać Sprinklr z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="a5144-124">To configure the integration of Sprinklr into Azure AD, you need to add Sprinklr from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a5144-125">**Aby dodać Sprinklr z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="a5144-125">**To add Sprinklr from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a5144-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="a5144-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="a5144-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="a5144-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a5144-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="a5144-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="a5144-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a5144-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="a5144-133">W polu wyszukiwania wpisz **Sprinklr**.</span><span class="sxs-lookup"><span data-stu-id="a5144-133">In the search box, type **Sprinklr**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_search.png)

5. <span data-ttu-id="a5144-135">W panelu wyników wybierz **Sprinklr**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="a5144-135">In the results panel, select **Sprinklr**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a5144-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="a5144-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a5144-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Sprinklr na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="a5144-138">In this section, you configure and test Azure AD single sign-on with Sprinklr based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a5144-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Sprinklr jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a5144-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Sprinklr is to a user in Azure AD.</span></span> <span data-ttu-id="a5144-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Sprinklr musi się.</span><span class="sxs-lookup"><span data-stu-id="a5144-140">In other words, a link relationship between an Azure AD user and the related user in Sprinklr needs to be established.</span></span>

<span data-ttu-id="a5144-141">W Sprinklr, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="a5144-141">In Sprinklr, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a5144-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Sprinklr, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="a5144-142">To configure and test Azure AD single sign-on with Sprinklr, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a5144-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="a5144-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a5144-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="a5144-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a5144-145">**[Tworzenie użytkownika testowego Sprinklr](#creating-a-sprinklr-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Sprinklr połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a5144-145">**[Creating a Sprinklr test user](#creating-a-sprinklr-test-user)** - to have a counterpart of Britta Simon in Sprinklr that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a5144-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="a5144-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a5144-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="a5144-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a5144-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="a5144-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a5144-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Sprinklr.</span><span class="sxs-lookup"><span data-stu-id="a5144-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Sprinklr application.</span></span>

<span data-ttu-id="a5144-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Sprinklr, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="a5144-150">**To configure Azure AD single sign-on with Sprinklr, perform the following steps:**</span></span>

1. <span data-ttu-id="a5144-151">W portalu Azure na **Sprinklr** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="a5144-151">In the Azure portal, on the **Sprinklr** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="a5144-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="a5144-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_samlbase.png)

3. <span data-ttu-id="a5144-155">Na **Sprinklr domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a5144-155">On the **Sprinklr Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_url.png)

    <span data-ttu-id="a5144-157">a.</span><span class="sxs-lookup"><span data-stu-id="a5144-157">a.</span></span> <span data-ttu-id="a5144-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.sprinklr.com`</span><span class="sxs-lookup"><span data-stu-id="a5144-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.sprinklr.com`</span></span>

    <span data-ttu-id="a5144-159">b.</span><span class="sxs-lookup"><span data-stu-id="a5144-159">b.</span></span> <span data-ttu-id="a5144-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.sprinklr.com`</span><span class="sxs-lookup"><span data-stu-id="a5144-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.sprinklr.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a5144-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="a5144-161">These values are not real.</span></span> <span data-ttu-id="a5144-162">Zaktualizuj tę wartość przy użyciu rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="a5144-162">Update the value with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a5144-163">Skontaktuj się z [zespołem pomocy technicznej klienta Sprinklr](https://www.sprinklr.com/contact-us/) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="a5144-163">Contact [Sprinklr Client support team](https://www.sprinklr.com/contact-us/) to get these values.</span></span> 
 
4. <span data-ttu-id="a5144-164">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="a5144-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_certificate.png) 

5. <span data-ttu-id="a5144-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a5144-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sprinklr-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a5144-168">Na **konfiguracji Sprinklr** , kliknij przycisk **skonfigurować Sprinklr** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="a5144-168">On the **Sprinklr Configuration** section, click **Configure Sprinklr** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a5144-169">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="a5144-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

7. <span data-ttu-id="a5144-170">W oknie przeglądarki innej witryny sieci web należy zalogować się jako administrator do witryny firmy Sprinklr.</span><span class="sxs-lookup"><span data-stu-id="a5144-170">In a different web browser window, log in to your Sprinklr company site as an administrator.</span></span>

8. <span data-ttu-id="a5144-171">Przejdź do **administracji \> ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="a5144-171">Go to **Administration \> Settings**.</span></span>
   
    <span data-ttu-id="a5144-172">![Administracja](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "administracji")</span><span class="sxs-lookup"><span data-stu-id="a5144-172">![Administration](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administration")</span></span>

9. <span data-ttu-id="a5144-173">Przejdź do **Zarządzanie partnera \> jednokrotnego** na w lewym okienku.</span><span class="sxs-lookup"><span data-stu-id="a5144-173">Go to **Manage Partner \> Single Sign** on from the left pane.</span></span>
   
    <span data-ttu-id="a5144-174">![Zarządzanie partnerem](./media/active-directory-saas-sprinklr-tutorial/ic782908.png "Zarządzanie partnera")</span><span class="sxs-lookup"><span data-stu-id="a5144-174">![Manage Partner](./media/active-directory-saas-sprinklr-tutorial/ic782908.png "Manage Partner")</span></span>

10. <span data-ttu-id="a5144-175">Kliknij przycisk **+ dodatki jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="a5144-175">Click **+Add Single Sign Ons**.</span></span>
   
    <span data-ttu-id="a5144-176">![Pojedynczy prób logowania](./media/active-directory-saas-sprinklr-tutorial/ic782909.png "pojedynczy prób logowania")</span><span class="sxs-lookup"><span data-stu-id="a5144-176">![Single Sign-Ons](./media/active-directory-saas-sprinklr-tutorial/ic782909.png "Single Sign-Ons")</span></span>

11. <span data-ttu-id="a5144-177">Na **logowania jednokrotnego** wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a5144-177">On the **Single Sign on** page, perform the following steps:</span></span>
   
    <span data-ttu-id="a5144-178">![Pojedynczy prób logowania](./media/active-directory-saas-sprinklr-tutorial/ic782910.png "pojedynczy prób logowania")</span><span class="sxs-lookup"><span data-stu-id="a5144-178">![Single Sign-Ons](./media/active-directory-saas-sprinklr-tutorial/ic782910.png "Single Sign-Ons")</span></span>

    <span data-ttu-id="a5144-179">a.</span><span class="sxs-lookup"><span data-stu-id="a5144-179">a.</span></span> <span data-ttu-id="a5144-180">W **nazwa** tekstowym, wpisz nazwę konfiguracji (na przykład: *WAADSSOTest*).</span><span class="sxs-lookup"><span data-stu-id="a5144-180">In the **Name** textbox, type a name for your configuration (for example: *WAADSSOTest*).</span></span>

    <span data-ttu-id="a5144-181">b.</span><span class="sxs-lookup"><span data-stu-id="a5144-181">b.</span></span> <span data-ttu-id="a5144-182">Wybierz **włączone**.</span><span class="sxs-lookup"><span data-stu-id="a5144-182">Select **Enabled**.</span></span>

    <span data-ttu-id="a5144-183">c.</span><span class="sxs-lookup"><span data-stu-id="a5144-183">c.</span></span> <span data-ttu-id="a5144-184">Wybierz **korzystania z nowego certyfikatu logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="a5144-184">Select **Use new SSO Certificate**.</span></span>
             
    <span data-ttu-id="a5144-185">e.</span><span class="sxs-lookup"><span data-stu-id="a5144-185">e.</span></span> <span data-ttu-id="a5144-186">Otwórz w Notatniku certyfikatu zakodowanego base-64, skopiuj zawartość go do Schowka, a następnie wklej go do **certyfikat dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="a5144-186">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Identity Provider Certificate** textbox.</span></span>

    <span data-ttu-id="a5144-187">f.</span><span class="sxs-lookup"><span data-stu-id="a5144-187">f.</span></span> <span data-ttu-id="a5144-188">Wklej **identyfikator jednostki SAML** wartość, która została skopiowana z portalu Azure do **identyfikator jednostki** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="a5144-188">Paste the **SAML Entity ID** value which you have copied from Azure Portal into the **Entity Id** textbox.</span></span>

    <span data-ttu-id="a5144-189">g.</span><span class="sxs-lookup"><span data-stu-id="a5144-189">g.</span></span> <span data-ttu-id="a5144-190">Wklej **SAML pojedynczy znak na adres URL usługi** wartość, która została skopiowana z portalu Azure do **adresu URL logowania do dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="a5144-190">Paste the **SAML Single Sign-On Service URL** value which you have copied from Azure Portal into the **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="a5144-191">h.</span><span class="sxs-lookup"><span data-stu-id="a5144-191">h.</span></span> <span data-ttu-id="a5144-192">Wklej **Sign-Out URL** wartość, która została skopiowana z portalu Azure do **adres URL wylogowania dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="a5144-192">Paste the **Sign-Out URL** value which you have copied from Azure Portal into the **Identity Provider Logout URL** textbox.</span></span>
     
    <span data-ttu-id="a5144-193">i.</span><span class="sxs-lookup"><span data-stu-id="a5144-193">i.</span></span> <span data-ttu-id="a5144-194">Jako **typ Identyfikatora użytkownika SAML**, wybierz pozycję **potwierdzenia zawiera użytkownika "s sprinklr.com username**.</span><span class="sxs-lookup"><span data-stu-id="a5144-194">As **SAML User ID Type**, select **Assertion contains User”s sprinklr.com username**.</span></span>

    <span data-ttu-id="a5144-195">j.</span><span class="sxs-lookup"><span data-stu-id="a5144-195">j.</span></span> <span data-ttu-id="a5144-196">Jako **lokalizacji identyfikator użytkownika SAML**, wybierz pozycję **identyfikator użytkownika jest w elemencie identyfikator nazwy podmiotu instrukcji**.</span><span class="sxs-lookup"><span data-stu-id="a5144-196">As **SAML User ID Location**, select **User ID is in the Name Identifier element of the Subject statement**.</span></span>

    <span data-ttu-id="a5144-197">k.</span><span class="sxs-lookup"><span data-stu-id="a5144-197">k.</span></span> <span data-ttu-id="a5144-198">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="a5144-198">Click **Save**.</span></span>
       
    <span data-ttu-id="a5144-199">![SAML](./media/active-directory-saas-sprinklr-tutorial/ic782911.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="a5144-199">![SAML](./media/active-directory-saas-sprinklr-tutorial/ic782911.png "SAML")</span></span>

> [!TIP]
> <span data-ttu-id="a5144-200">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="a5144-200">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a5144-201">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="a5144-201">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a5144-202">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a5144-202">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a5144-203">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a5144-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="a5144-204">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="a5144-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="a5144-206">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="a5144-206">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a5144-207">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="a5144-207">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a5144-209">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="a5144-209">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a5144-211">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a5144-211">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a5144-213">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a5144-213">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a5144-215">a.</span><span class="sxs-lookup"><span data-stu-id="a5144-215">a.</span></span> <span data-ttu-id="a5144-216">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a5144-216">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a5144-217">b.</span><span class="sxs-lookup"><span data-stu-id="a5144-217">b.</span></span> <span data-ttu-id="a5144-218">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a5144-218">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a5144-219">c.</span><span class="sxs-lookup"><span data-stu-id="a5144-219">c.</span></span> <span data-ttu-id="a5144-220">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="a5144-220">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a5144-221">d.</span><span class="sxs-lookup"><span data-stu-id="a5144-221">d.</span></span> <span data-ttu-id="a5144-222">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="a5144-222">Click **Create**.</span></span>
 
### <a name="creating-a-sprinklr-test-user"></a><span data-ttu-id="a5144-223">Tworzenie użytkownika testowego Sprinklr</span><span class="sxs-lookup"><span data-stu-id="a5144-223">Creating a Sprinklr test user</span></span>

1. <span data-ttu-id="a5144-224">Zaloguj się do witryny firmy Sprinklr jako administrator.</span><span class="sxs-lookup"><span data-stu-id="a5144-224">Log in to your Sprinklr company site as an administrator.</span></span>

2. <span data-ttu-id="a5144-225">Przejdź do **administracji \> ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="a5144-225">Go to **Administration \> Settings**.</span></span>
   
    <span data-ttu-id="a5144-226">![Administracja](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "administracji")</span><span class="sxs-lookup"><span data-stu-id="a5144-226">![Administration](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administration")</span></span>

3. <span data-ttu-id="a5144-227">Przejdź do **klienta zarządzania \> użytkowników** w lewym okienku.</span><span class="sxs-lookup"><span data-stu-id="a5144-227">Go to **Manage Client \> Users** from the left pane.</span></span>
   
    <span data-ttu-id="a5144-228">![Ustawienia](./media/active-directory-saas-sprinklr-tutorial/ic782914.png "ustawienia")</span><span class="sxs-lookup"><span data-stu-id="a5144-228">![Settings](./media/active-directory-saas-sprinklr-tutorial/ic782914.png "Settings")</span></span>

4. <span data-ttu-id="a5144-229">Kliknij przycisk **dodać użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="a5144-229">Click **Add User**.</span></span>
   
    <span data-ttu-id="a5144-230">![Ustawienia](./media/active-directory-saas-sprinklr-tutorial/ic782915.png "ustawienia")</span><span class="sxs-lookup"><span data-stu-id="a5144-230">![Settings](./media/active-directory-saas-sprinklr-tutorial/ic782915.png "Settings")</span></span>

5. <span data-ttu-id="a5144-231">Na **Edycja użytkownika** okna dialogowego, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a5144-231">On the **Edit user** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="a5144-232">![Edytowanie użytkownika](./media/active-directory-saas-sprinklr-tutorial/ic782916.png "Edycja użytkownika")</span><span class="sxs-lookup"><span data-stu-id="a5144-232">![Edit user](./media/active-directory-saas-sprinklr-tutorial/ic782916.png "Edit user")</span></span> 

    <span data-ttu-id="a5144-233">a.</span><span class="sxs-lookup"><span data-stu-id="a5144-233">a.</span></span> <span data-ttu-id="a5144-234">W **E-mail**, **imię** i **nazwisko** pól tekstowych, wpisz informacje, które chcesz udostępnić konta użytkownika usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a5144-234">In the **Email**, **First Name** and **Last Name** textboxes, type the information of an Azure AD user account you want to provision.</span></span>

    <span data-ttu-id="a5144-235">b.</span><span class="sxs-lookup"><span data-stu-id="a5144-235">b.</span></span> <span data-ttu-id="a5144-236">Wybierz **wyłączone hasło**.</span><span class="sxs-lookup"><span data-stu-id="a5144-236">Select **Password Disabled**.</span></span>

    <span data-ttu-id="a5144-237">c.</span><span class="sxs-lookup"><span data-stu-id="a5144-237">c.</span></span> <span data-ttu-id="a5144-238">Wybierz **języka**.</span><span class="sxs-lookup"><span data-stu-id="a5144-238">Select **Language**.</span></span>

    <span data-ttu-id="a5144-239">d.</span><span class="sxs-lookup"><span data-stu-id="a5144-239">d.</span></span> <span data-ttu-id="a5144-240">Wybierz **typ użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="a5144-240">Select **User Type**.</span></span>

    <span data-ttu-id="a5144-241">e.</span><span class="sxs-lookup"><span data-stu-id="a5144-241">e.</span></span> <span data-ttu-id="a5144-242">Kliknij przycisk **aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="a5144-242">Click **Update**.</span></span>
   
     >[!IMPORTANT]
     ><span data-ttu-id="a5144-243">**Wyłączone hasło** należy wybrać, aby użytkownik mógł zalogować się za pośrednictwem dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="a5144-243">**Password Disabled** must be selected to enable a user to log in via an Identity provider.</span></span> 
     
6. <span data-ttu-id="a5144-244">Przejdź do **roli**, a następnie wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a5144-244">Go to **Role**, and then perform the following steps:</span></span>
   
    <span data-ttu-id="a5144-245">![Partnera ról](./media/active-directory-saas-sprinklr-tutorial/ic782917.png "partnera ról")</span><span class="sxs-lookup"><span data-stu-id="a5144-245">![Partner Roles](./media/active-directory-saas-sprinklr-tutorial/ic782917.png "Partner Roles")</span></span>

    <span data-ttu-id="a5144-246">a.</span><span class="sxs-lookup"><span data-stu-id="a5144-246">a.</span></span> <span data-ttu-id="a5144-247">Z **Global** listy, wybierz **wszystkie\_uprawnienia**.</span><span class="sxs-lookup"><span data-stu-id="a5144-247">From the **Global** list, select **ALL\_Permissions**.</span></span>  

    <span data-ttu-id="a5144-248">b.</span><span class="sxs-lookup"><span data-stu-id="a5144-248">b.</span></span> <span data-ttu-id="a5144-249">Kliknij przycisk **aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="a5144-249">Click **Update**.</span></span>

>[!NOTE]
><span data-ttu-id="a5144-250">Możesz użyć innych Sprinklr użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Sprinklr do udostępnienia konta użytkownika usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a5144-250">You can use any other Sprinklr user account creation tools or APIs provided by Sprinklr to provision Azure AD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a5144-251">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a5144-251">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a5144-252">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Sprinklr.</span><span class="sxs-lookup"><span data-stu-id="a5144-252">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Sprinklr.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="a5144-254">**Aby przypisać Simona Britta Sprinklr, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="a5144-254">**To assign Britta Simon to Sprinklr, perform the following steps:**</span></span>

1. <span data-ttu-id="a5144-255">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="a5144-255">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="a5144-257">Na liście aplikacji zaznacz **Sprinklr**.</span><span class="sxs-lookup"><span data-stu-id="a5144-257">In the applications list, select **Sprinklr**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_app.png) 

3. <span data-ttu-id="a5144-259">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="a5144-259">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="a5144-261">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a5144-261">Click **Add** button.</span></span> <span data-ttu-id="a5144-262">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a5144-262">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="a5144-264">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="a5144-264">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a5144-265">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a5144-265">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a5144-266">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a5144-266">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a5144-267">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="a5144-267">Testing single sign-on</span></span>

<span data-ttu-id="a5144-268">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="a5144-268">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a5144-269">Po kliknięciu kafelka Sprinklr w panelu dostępu, należy pobrać automatycznie zalogowane Sprinklr aplikacji można znaleźć więcej informacji na temat panelu dostępu [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a5144-269">When you click the Sprinklr tile in the Access Panel, you should get automatically signed-on to your Sprinklr application For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a5144-270">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="a5144-270">Additional resources</span></span>

* [<span data-ttu-id="a5144-271">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a5144-271">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a5144-272">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a5144-272">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_203.png

