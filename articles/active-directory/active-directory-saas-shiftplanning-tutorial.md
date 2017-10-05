---
title: "Samouczek: Integracji Azure Active Directory z ludzkości | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i ludzkości."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6aa771e9-31c6-48d1-8dde-024bebc06943
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 327cc1e3d0836e79376e0a3cd5a4422a967f5943
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-humanity"></a><span data-ttu-id="52a81-103">Samouczek: Integracji Azure Active Directory z ludzkości</span><span class="sxs-lookup"><span data-stu-id="52a81-103">Tutorial: Azure Active Directory integration with Humanity</span></span>

<span data-ttu-id="52a81-104">Z tego samouczka dowiesz się integrowanie ludzkości w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="52a81-104">In this tutorial, you learn how to integrate Humanity with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="52a81-105">Integracja z usługą Azure AD ludzkości zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="52a81-105">Integrating Humanity with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="52a81-106">Można kontrolować w usłudze Azure AD, który ma dostęp do ludzkości</span><span class="sxs-lookup"><span data-stu-id="52a81-106">You can control in Azure AD who has access to Humanity</span></span>
- <span data-ttu-id="52a81-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do ludzkości (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="52a81-107">You can enable your users to automatically get signed-on to Humanity (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="52a81-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="52a81-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="52a81-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="52a81-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="52a81-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="52a81-110">Prerequisites</span></span>

<span data-ttu-id="52a81-111">Aby skonfigurować integrację usługi Azure AD z ludzkości, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="52a81-111">To configure Azure AD integration with Humanity, you need the following items:</span></span>

- <span data-ttu-id="52a81-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="52a81-112">An Azure AD subscription</span></span>
- <span data-ttu-id="52a81-113">Ludzkości jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="52a81-113">A Humanity single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="52a81-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="52a81-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="52a81-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="52a81-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="52a81-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="52a81-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="52a81-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="52a81-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="52a81-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="52a81-118">Scenario description</span></span>
<span data-ttu-id="52a81-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="52a81-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="52a81-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="52a81-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="52a81-121">Dodawanie ludzkości z galerii</span><span class="sxs-lookup"><span data-stu-id="52a81-121">Adding Humanity from the gallery</span></span>
2. <span data-ttu-id="52a81-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="52a81-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-humanity-from-the-gallery"></a><span data-ttu-id="52a81-123">Dodawanie ludzkości z galerii</span><span class="sxs-lookup"><span data-stu-id="52a81-123">Adding Humanity from the gallery</span></span>
<span data-ttu-id="52a81-124">Aby skonfigurować integrację ludzkości do usługi Azure AD, należy dodać ludzkości z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="52a81-124">To configure the integration of Humanity into Azure AD, you need to add Humanity from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="52a81-125">**Aby dodać ludzkości z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="52a81-125">**To add Humanity from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="52a81-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="52a81-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="52a81-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="52a81-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="52a81-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="52a81-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="52a81-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="52a81-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="52a81-133">W polu wyszukiwania wpisz **ludzkości**.</span><span class="sxs-lookup"><span data-stu-id="52a81-133">In the search box, type **Humanity**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_search.png)

5. <span data-ttu-id="52a81-135">W panelu wyników wybierz **ludzkości**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="52a81-135">In the results panel, select **Humanity**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="52a81-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="52a81-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="52a81-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z ludzkości oparte na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="52a81-138">In this section, you configure and test Azure AD single sign-on with Humanity based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="52a81-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w ludzkości jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="52a81-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Humanity is to a user in Azure AD.</span></span> <span data-ttu-id="52a81-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w ludzkości musi się.</span><span class="sxs-lookup"><span data-stu-id="52a81-140">In other words, a link relationship between an Azure AD user and the related user in Humanity needs to be established.</span></span>

<span data-ttu-id="52a81-141">W ludzkości, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="52a81-141">In Humanity, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="52a81-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z ludzkości, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="52a81-142">To configure and test Azure AD single sign-on with Humanity, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="52a81-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="52a81-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="52a81-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="52a81-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="52a81-145">**[Tworzenie użytkownika testowego ludzkości](#creating-a-humanity-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta ludzkości połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="52a81-145">**[Creating a Humanity test user](#creating-a-humanity-test-user)** - to have a counterpart of Britta Simon in Humanity that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="52a81-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="52a81-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="52a81-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="52a81-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="52a81-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="52a81-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="52a81-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji ludzkości.</span><span class="sxs-lookup"><span data-stu-id="52a81-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Humanity application.</span></span>

<span data-ttu-id="52a81-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z ludzkości, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="52a81-150">**To configure Azure AD single sign-on with Humanity, perform the following steps:**</span></span>

1. <span data-ttu-id="52a81-151">W portalu Azure na **ludzkości** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="52a81-151">In the Azure portal, on the **Humanity** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="52a81-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="52a81-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_samlbase.png)

3. <span data-ttu-id="52a81-155">Na **ludzkości domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="52a81-155">On the **Humanity Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_url.png)

    <span data-ttu-id="52a81-157">a.</span><span class="sxs-lookup"><span data-stu-id="52a81-157">a.</span></span> <span data-ttu-id="52a81-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://company.humanity.com/includes/saml/`</span><span class="sxs-lookup"><span data-stu-id="52a81-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://company.humanity.com/includes/saml/`</span></span>

    <span data-ttu-id="52a81-159">b.</span><span class="sxs-lookup"><span data-stu-id="52a81-159">b.</span></span> <span data-ttu-id="52a81-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://company.humanity.com/app/`</span><span class="sxs-lookup"><span data-stu-id="52a81-160">In the **Identifier** textbox, type a URL using the following pattern: `https://company.humanity.com/app/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="52a81-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="52a81-161">These values are not real.</span></span> <span data-ttu-id="52a81-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="52a81-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="52a81-163">Skontaktuj się z [zespołem pomocy technicznej klienta ludzkości](https://www.humanity.com/support/) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="52a81-163">Contact [Humanity Client support team](https://www.humanity.com/support/) to get these values.</span></span> 
 
4. <span data-ttu-id="52a81-164">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="52a81-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_certificate.png) 

5. <span data-ttu-id="52a81-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="52a81-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="52a81-168">Na **konfiguracji ludzkości** , kliknij przycisk **skonfigurować ludzkości** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="52a81-168">On the **Humanity Configuration** section, click **Configure Humanity** to open **Configure sign-on** window.</span></span> <span data-ttu-id="52a81-169">Kopiuj **SAML pojedynczy znak na adres URL usługi i adres URL Sign-Out** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="52a81-169">Copy the **SAML Single Sign-On Service URL, and Sign-Out URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_configure.png) 

7. <span data-ttu-id="52a81-171">W oknie przeglądarki innej witryny sieci web, zaloguj się do Twojego **ludzkości** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="52a81-171">In a different web browser window, log in to your **Humanity** company site as an administrator.</span></span>

8. <span data-ttu-id="52a81-172">W menu u góry kliknij **Admin**.</span><span class="sxs-lookup"><span data-stu-id="52a81-172">In the menu on the top, click **Admin**.</span></span>
   
    <span data-ttu-id="52a81-173">![Administrator](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "administratora")</span><span class="sxs-lookup"><span data-stu-id="52a81-173">![Admin](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")</span></span>

9. <span data-ttu-id="52a81-174">W obszarze **integracji**, kliknij przycisk **rejestracji jednokrotnej**.</span><span class="sxs-lookup"><span data-stu-id="52a81-174">Under **Integration**, click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="52a81-175">![Logowanie jednokrotne](./media/active-directory-saas-shiftplanning-tutorial/iC786620.png "logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="52a81-175">![Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/iC786620.png "Single Sign-On")</span></span>

10. <span data-ttu-id="52a81-176">W **rejestracji jednokrotnej** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="52a81-176">In the **Single Sign-On** section, perform the following steps:</span></span>
   
    <span data-ttu-id="52a81-177">![Logowanie jednokrotne](./media/active-directory-saas-shiftplanning-tutorial/iC786905.png "logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="52a81-177">![Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/iC786905.png "Single Sign-On")</span></span>
   
    <span data-ttu-id="52a81-178">a.</span><span class="sxs-lookup"><span data-stu-id="52a81-178">a.</span></span> <span data-ttu-id="52a81-179">Wybierz **SAML włączone**.</span><span class="sxs-lookup"><span data-stu-id="52a81-179">Select **SAML Enabled**.</span></span>

    <span data-ttu-id="52a81-180">b.</span><span class="sxs-lookup"><span data-stu-id="52a81-180">b.</span></span> <span data-ttu-id="52a81-181">Wybierz **Zezwalaj na hasło logowania**.</span><span class="sxs-lookup"><span data-stu-id="52a81-181">Select **Allow Password Login**.</span></span>

    <span data-ttu-id="52a81-182">c.</span><span class="sxs-lookup"><span data-stu-id="52a81-182">c.</span></span> <span data-ttu-id="52a81-183">Wklej **SAML pojedynczy znak na adres URL usługi** wartości do **adres URL wystawcy SAML** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="52a81-183">Paste the **SAML Single Sign-On Service URL** value into the **SAML Issuer URL** textbox.</span></span>

    <span data-ttu-id="52a81-184">d.</span><span class="sxs-lookup"><span data-stu-id="52a81-184">d.</span></span> <span data-ttu-id="52a81-185">Wklej **Sign-Out URL** wartości do **zdalnego adresu URL wylogowania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="52a81-185">Paste the **Sign-Out URL** value into the **Remote Logout URL** textbox.</span></span>
   
    <span data-ttu-id="52a81-186">e.</span><span class="sxs-lookup"><span data-stu-id="52a81-186">e.</span></span> <span data-ttu-id="52a81-187">Otwórz w Notatniku certyfikatu zakodowanego base-64, skopiuj zawartość go do Schowka, a następnie wklej go do **certyfikatu X.509** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="52a81-187">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox.</span></span>

11. <span data-ttu-id="52a81-188">Kliknij przycisk **Zapisz ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="52a81-188">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="52a81-189">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="52a81-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="52a81-190">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="52a81-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="52a81-191">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="52a81-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="52a81-192">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="52a81-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="52a81-193">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="52a81-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="52a81-195">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="52a81-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="52a81-196">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="52a81-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="52a81-198">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="52a81-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="52a81-200">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="52a81-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="52a81-202">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="52a81-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="52a81-204">a.</span><span class="sxs-lookup"><span data-stu-id="52a81-204">a.</span></span> <span data-ttu-id="52a81-205">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="52a81-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="52a81-206">b.</span><span class="sxs-lookup"><span data-stu-id="52a81-206">b.</span></span> <span data-ttu-id="52a81-207">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="52a81-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="52a81-208">c.</span><span class="sxs-lookup"><span data-stu-id="52a81-208">c.</span></span> <span data-ttu-id="52a81-209">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="52a81-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="52a81-210">d.</span><span class="sxs-lookup"><span data-stu-id="52a81-210">d.</span></span> <span data-ttu-id="52a81-211">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="52a81-211">Click **Create**.</span></span>
 
### <a name="creating-a-humanity-test-user"></a><span data-ttu-id="52a81-212">Tworzenie użytkownika testowego ludzkości</span><span class="sxs-lookup"><span data-stu-id="52a81-212">Creating a Humanity test user</span></span>

<span data-ttu-id="52a81-213">Aby umożliwić użytkownikom zalogować się do ludzkości usługi Azure AD, musi być przygotowana do ludzkości.</span><span class="sxs-lookup"><span data-stu-id="52a81-213">In order to enable Azure AD users to log in to Humanity, they must be provisioned into Humanity.</span></span> <span data-ttu-id="52a81-214">W przypadku ludzkości Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="52a81-214">In the case of Humanity, provisioning is a manual task.</span></span>

<span data-ttu-id="52a81-215">**Aby udostępnić konta użytkownika, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="52a81-215">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="52a81-216">Zaloguj się do Twojego **ludzkości** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="52a81-216">Log in to your **Humanity** company site as an administrator.</span></span>

2. <span data-ttu-id="52a81-217">Kliknij przycisk **Admin**.</span><span class="sxs-lookup"><span data-stu-id="52a81-217">Click **Admin**.</span></span>
   
    <span data-ttu-id="52a81-218">![Administrator](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "administratora")</span><span class="sxs-lookup"><span data-stu-id="52a81-218">![Admin](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")</span></span>

3. <span data-ttu-id="52a81-219">Kliknij przycisk **personelu**.</span><span class="sxs-lookup"><span data-stu-id="52a81-219">Click **Staff**.</span></span>
   
    <span data-ttu-id="52a81-220">![Personel](./media/active-directory-saas-shiftplanning-tutorial/ic786623.png "personelu")</span><span class="sxs-lookup"><span data-stu-id="52a81-220">![Staff](./media/active-directory-saas-shiftplanning-tutorial/ic786623.png "Staff")</span></span>

4. <span data-ttu-id="52a81-221">W obszarze **akcje**, kliknij przycisk **dodać pracowników**.</span><span class="sxs-lookup"><span data-stu-id="52a81-221">Under **Actions**, click **Add Employees**.</span></span>
   
    <span data-ttu-id="52a81-222">![Dodaj pracowników](./media/active-directory-saas-shiftplanning-tutorial/iC786624.png "dodać pracowników")</span><span class="sxs-lookup"><span data-stu-id="52a81-222">![Add Employees](./media/active-directory-saas-shiftplanning-tutorial/iC786624.png "Add Employees")</span></span>

5. <span data-ttu-id="52a81-223">W **dodać pracowników** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="52a81-223">In the **Add Employees** section, perform the following steps:</span></span>
   
    <span data-ttu-id="52a81-224">![Zapisz pracowników](./media/active-directory-saas-shiftplanning-tutorial/iC786625.png "zapisać pracowników")</span><span class="sxs-lookup"><span data-stu-id="52a81-224">![Save Employees](./media/active-directory-saas-shiftplanning-tutorial/iC786625.png "Save Employees")</span></span>
   
    <span data-ttu-id="52a81-225">a.</span><span class="sxs-lookup"><span data-stu-id="52a81-225">a.</span></span> <span data-ttu-id="52a81-226">Typ **imię**, **nazwisko**, i **E-mail** poprawnego konta usługi AAD ustanawiane do powiązanych pól tekstowych.</span><span class="sxs-lookup"><span data-stu-id="52a81-226">Type the **First Name**, **Last Name**, and **Email** of a valid AAD account you want to provision into the related textboxes.</span></span>

    <span data-ttu-id="52a81-227">b.</span><span class="sxs-lookup"><span data-stu-id="52a81-227">b.</span></span> <span data-ttu-id="52a81-228">Kliknij przycisk **zapisać pracowników**.</span><span class="sxs-lookup"><span data-stu-id="52a81-228">Click **Save Employees**.</span></span>

>[!NOTE]
><span data-ttu-id="52a81-229">Możesz użyć innych ludzkości użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez ludzkości do kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="52a81-229">You can use any other Humanity user account creation tools or APIs provided by Humanity to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="52a81-230">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="52a81-230">Assigning the Azure AD test user</span></span>

<span data-ttu-id="52a81-231">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu ludzkości.</span><span class="sxs-lookup"><span data-stu-id="52a81-231">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Humanity.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="52a81-233">**Aby przypisać Simona Britta ludzkości, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="52a81-233">**To assign Britta Simon to Humanity, perform the following steps:**</span></span>

1. <span data-ttu-id="52a81-234">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="52a81-234">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="52a81-236">Na liście aplikacji zaznacz **ludzkości**.</span><span class="sxs-lookup"><span data-stu-id="52a81-236">In the applications list, select **Humanity**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_app.png) 

3. <span data-ttu-id="52a81-238">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="52a81-238">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="52a81-240">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="52a81-240">Click **Add** button.</span></span> <span data-ttu-id="52a81-241">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="52a81-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="52a81-243">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="52a81-243">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="52a81-244">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="52a81-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="52a81-245">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="52a81-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="52a81-246">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="52a81-246">Testing single sign-on</span></span>

<span data-ttu-id="52a81-247">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="52a81-247">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="52a81-248">Po kliknięciu kafelka ludzkości w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji ludzkości.</span><span class="sxs-lookup"><span data-stu-id="52a81-248">When you click the Humanity tile in the Access Panel, you should get automatically signed-on to your Humanity application.</span></span>
<span data-ttu-id="52a81-249">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="52a81-249">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="52a81-250">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="52a81-250">Additional resources</span></span>

* [<span data-ttu-id="52a81-251">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="52a81-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="52a81-252">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="52a81-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_203.png

