---
title: 'Samouczek: Integracji Azure Active Directory z BlueJeans | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i BlueJeans."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dfc634fd-1b55-4ba8-94a8-b8288429b6a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: jeedes
ms.openlocfilehash: 03bf65852b8d3cf14aebf155891a028db86e78d0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bluejeans"></a><span data-ttu-id="5bb9a-103">Samouczek: Integracji Azure Active Directory z BlueJeans</span><span class="sxs-lookup"><span data-stu-id="5bb9a-103">Tutorial: Azure Active Directory integration with BlueJeans</span></span>

<span data-ttu-id="5bb9a-104">Z tego samouczka dowiesz się integrowanie BlueJeans z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5bb9a-104">In this tutorial, you learn how to integrate BlueJeans with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5bb9a-105">Integracja z usługą Azure AD BlueJeans zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="5bb9a-105">Integrating BlueJeans with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5bb9a-106">Można kontrolować w usłudze Azure AD, który ma dostęp do BlueJeans</span><span class="sxs-lookup"><span data-stu-id="5bb9a-106">You can control in Azure AD who has access to BlueJeans</span></span>
- <span data-ttu-id="5bb9a-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do BlueJeans (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bb9a-107">You can enable your users to automatically get signed-on to BlueJeans (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5bb9a-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="5bb9a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5bb9a-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5bb9a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5bb9a-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5bb9a-110">Prerequisites</span></span>

<span data-ttu-id="5bb9a-111">Aby skonfigurować integrację usługi Azure AD z BlueJeans, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="5bb9a-111">To configure Azure AD integration with BlueJeans, you need the following items:</span></span>

- <span data-ttu-id="5bb9a-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bb9a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5bb9a-113">BlueJeans jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="5bb9a-113">A BlueJeans single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5bb9a-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5bb9a-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="5bb9a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5bb9a-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5bb9a-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5bb9a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5bb9a-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="5bb9a-118">Scenario description</span></span>
<span data-ttu-id="5bb9a-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5bb9a-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="5bb9a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5bb9a-121">Dodawanie BlueJeans z galerii</span><span class="sxs-lookup"><span data-stu-id="5bb9a-121">Adding BlueJeans from the gallery</span></span>
2. <span data-ttu-id="5bb9a-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="5bb9a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bluejeans-from-the-gallery"></a><span data-ttu-id="5bb9a-123">Dodawanie BlueJeans z galerii</span><span class="sxs-lookup"><span data-stu-id="5bb9a-123">Adding BlueJeans from the gallery</span></span>
<span data-ttu-id="5bb9a-124">Aby skonfigurować integrację usługi Azure AD BlueJeans, należy dodać BlueJeans z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-124">To configure the integration of BlueJeans into Azure AD, you need to add BlueJeans from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5bb9a-125">**Aby dodać BlueJeans z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5bb9a-125">**To add BlueJeans from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5bb9a-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="5bb9a-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5bb9a-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="5bb9a-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="5bb9a-133">W polu wyszukiwania wpisz **BlueJeans**.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-133">In the search box, type **BlueJeans**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_search.png)

5. <span data-ttu-id="5bb9a-135">W panelu wyników wybierz **BlueJeans**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-135">In the results panel, select **BlueJeans**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5bb9a-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="5bb9a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5bb9a-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z BlueJeans na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="5bb9a-138">In this section, you configure and test Azure AD single sign-on with BlueJeans based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5bb9a-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w BlueJeans jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BlueJeans is to a user in Azure AD.</span></span> <span data-ttu-id="5bb9a-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w BlueJeans musi się.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-140">In other words, a link relationship between an Azure AD user and the related user in BlueJeans needs to be established.</span></span>

<span data-ttu-id="5bb9a-141">W BlueJeans, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-141">In BlueJeans, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5bb9a-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z BlueJeans, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="5bb9a-142">To configure and test Azure AD single sign-on with BlueJeans, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5bb9a-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5bb9a-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5bb9a-145">**[Tworzenie użytkownika testowego BlueJeans](#creating-a-bluejeans-test-user)**  — aby odpowiednikiem Britta Simona w BlueJeans jest połączony z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-145">**[Creating a BlueJeans test user](#creating-a-bluejeans-test-user)** - to have a counterpart of Britta Simon in BlueJeans that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5bb9a-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5bb9a-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5bb9a-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5bb9a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5bb9a-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BlueJeans application.</span></span>

<span data-ttu-id="5bb9a-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z BlueJeans, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5bb9a-150">**To configure Azure AD single sign-on with BlueJeans, perform the following steps:**</span></span>

1. <span data-ttu-id="5bb9a-151">W portalu Azure na **BlueJeans** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-151">In the Azure portal, on the **BlueJeans** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="5bb9a-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_samlbase.png)

3. <span data-ttu-id="5bb9a-155">Na **BlueJeans domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5bb9a-155">On the **BlueJeans Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_url.png)

    <span data-ttu-id="5bb9a-157">a.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-157">a.</span></span> <span data-ttu-id="5bb9a-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.BlueJeans.com`</span><span class="sxs-lookup"><span data-stu-id="5bb9a-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.BlueJeans.com`</span></span>

    <span data-ttu-id="5bb9a-159">b.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-159">b.</span></span> <span data-ttu-id="5bb9a-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.BlueJeans.com`</span><span class="sxs-lookup"><span data-stu-id="5bb9a-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.BlueJeans.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5bb9a-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-161">These values are not real.</span></span> <span data-ttu-id="5bb9a-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="5bb9a-163">Skontaktuj się z [zespołem pomocy technicznej klienta BlueJeans](https://support.bluejeans.com/contact) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-163">Contact [BlueJeans Client support team](https://support.bluejeans.com/contact) to get these values.</span></span> 
 
4. <span data-ttu-id="5bb9a-164">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_certificate.png) 

5. <span data-ttu-id="5bb9a-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bluejeans-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5bb9a-168">Na **konfiguracji BlueJeans** , kliknij przycisk **skonfigurować BlueJeans** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-168">On the **BlueJeans Configuration** section, click **Configure BlueJeans** to open **Configure sign-on** window.</span></span> <span data-ttu-id="5bb9a-169">Kopiuj **Sign-Out adres URL, Zmień adres URL hasła i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="5bb9a-169">Copy the **Sign-Out URL, Change Password URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_configure.png) 

7. <span data-ttu-id="5bb9a-171">W oknie przeglądarki innej witryny sieci web, zaloguj się do Twojego **BlueJeans** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-171">In a different web browser window, log in to your **BlueJeans** company site as an administrator.</span></span>

8. <span data-ttu-id="5bb9a-172">Przejdź do **ADMIN \> ustawienia grupy \> zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-172">Go to **ADMIN \> Group Settings \> Security**.</span></span>
   
   <span data-ttu-id="5bb9a-173">![Administrator](./media/active-directory-saas-bluejeans-tutorial/IC785868.png "administratora")</span><span class="sxs-lookup"><span data-stu-id="5bb9a-173">![Admin](./media/active-directory-saas-bluejeans-tutorial/IC785868.png "Admin")</span></span>

9. <span data-ttu-id="5bb9a-174">W **zabezpieczeń** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5bb9a-174">In the **Security** section, perform the following steps:</span></span>
   
   <span data-ttu-id="5bb9a-175">![SAML logowania jednokrotnego](./media/active-directory-saas-bluejeans-tutorial/IC785869.png "SAML logowania jednokrotnego")</span><span class="sxs-lookup"><span data-stu-id="5bb9a-175">![SAML Single Sign On](./media/active-directory-saas-bluejeans-tutorial/IC785869.png "SAML Single Sign On")</span></span>   
   
   <span data-ttu-id="5bb9a-176">a.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-176">a.</span></span> <span data-ttu-id="5bb9a-177">Wybierz **SAML logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-177">Select **SAML Single Sign On**.</span></span>
  
   <span data-ttu-id="5bb9a-178">b.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-178">b.</span></span> <span data-ttu-id="5bb9a-179">Wybierz **Włącz automatyczne udostępnianie**.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-179">Select **Enable automatic provisioning**.</span></span>

10. <span data-ttu-id="5bb9a-180">Przenieś następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5bb9a-180">Move on with the following steps:</span></span>

    <span data-ttu-id="5bb9a-181">![Ścieżka certyfikatu](./media/active-directory-saas-bluejeans-tutorial/IC785870.png "ścieżka certyfikatu")</span><span class="sxs-lookup"><span data-stu-id="5bb9a-181">![Certificate Path](./media/active-directory-saas-bluejeans-tutorial/IC785870.png "Certificate Path")</span></span>
    
    <span data-ttu-id="5bb9a-182">a.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-182">a.</span></span> <span data-ttu-id="5bb9a-183">Kliknij przycisk **wybierz plik**, a następnie przekaż pobranego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-183">Click **Choose File**, and then upload the downloaded certificate.</span></span>
   
    <span data-ttu-id="5bb9a-184">b.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-184">b.</span></span> <span data-ttu-id="5bb9a-185">Wklej **SAML pojedynczy znak na adres URL usługi** do **adres URL logowania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-185">Paste **SAML Single Sign-On Service URL** into the **Login URL** textbox.</span></span>
   
    <span data-ttu-id="5bb9a-186">c.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-186">c.</span></span> <span data-ttu-id="5bb9a-187">Wklej **Zmień adres URL hasła** do **hasła, Zmień adres URL** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-187">Paste **Change Password URL** into the **Password Change URL** textbox.</span></span>
   
    <span data-ttu-id="5bb9a-188">d.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-188">d.</span></span> <span data-ttu-id="5bb9a-189">Wklej **Sign-Out URL** do **adresu URL wylogowania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-189">Paste **Sign-Out URL** into the **Logout URL** textbox.</span></span>

11. <span data-ttu-id="5bb9a-190">Przenieś następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5bb9a-190">Move on with the following steps:</span></span>
    
    <span data-ttu-id="5bb9a-191">![Zapisz zmiany](./media/active-directory-saas-bluejeans-tutorial/IC785874.png "zapisać zmiany")</span><span class="sxs-lookup"><span data-stu-id="5bb9a-191">![Save Changes](./media/active-directory-saas-bluejeans-tutorial/IC785874.png "Save Changes")</span></span>
    
    <span data-ttu-id="5bb9a-192">a.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-192">a.</span></span> <span data-ttu-id="5bb9a-193">W **identyfikator użytkownika** pole tekstowe, typ `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-193">In the **User id** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
   
    <span data-ttu-id="5bb9a-194">b.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-194">b.</span></span> <span data-ttu-id="5bb9a-195">W **E-mail** pole tekstowe, typ `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-195">In the **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
   
    <span data-ttu-id="5bb9a-196">c.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-196">c.</span></span> <span data-ttu-id="5bb9a-197">Kliknij przycisk **zapisać zmiany**.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-197">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="5bb9a-198">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="5bb9a-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5bb9a-199">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5bb9a-200">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5bb9a-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5bb9a-201">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bb9a-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="5bb9a-202">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="5bb9a-204">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5bb9a-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5bb9a-205">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5bb9a-207">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5bb9a-209">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5bb9a-211">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5bb9a-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5bb9a-213">a.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-213">a.</span></span> <span data-ttu-id="5bb9a-214">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5bb9a-215">b.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-215">b.</span></span> <span data-ttu-id="5bb9a-216">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5bb9a-217">c.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-217">c.</span></span> <span data-ttu-id="5bb9a-218">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5bb9a-219">d.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-219">d.</span></span> <span data-ttu-id="5bb9a-220">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-220">Click **Create**.</span></span>
 
### <a name="creating-a-bluejeans-test-user"></a><span data-ttu-id="5bb9a-221">Tworzenie użytkownika testowego BlueJeans</span><span class="sxs-lookup"><span data-stu-id="5bb9a-221">Creating a BlueJeans test user</span></span>

<span data-ttu-id="5bb9a-222">Aby umożliwić użytkownikom usługi Azure AD zalogować się do BlueJeans, musi być przygotowana do BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-222">To enable Azure AD users to log in to BlueJeans, they must be provisioned into BlueJeans.</span></span>  

<span data-ttu-id="5bb9a-223">W przypadku BlueJeans Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-223">In case of BlueJeans, provisioning is a manual task.</span></span>

<span data-ttu-id="5bb9a-224">**Aby udostępnić konta użytkowników, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5bb9a-224">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="5bb9a-225">Zaloguj się do Twojego **BlueJeans** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-225">Log in to your **BlueJeans** company site as an administrator.</span></span>

2. <span data-ttu-id="5bb9a-226">Przejdź do **ADMIN \> Zarządzanie użytkownikami \> dodać użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-226">Go to **ADMIN \> Manage Users \> Add User**.</span></span>
   
   <span data-ttu-id="5bb9a-227">![Administrator](./media/active-directory-saas-bluejeans-tutorial/IC785877.png "administratora")</span><span class="sxs-lookup"><span data-stu-id="5bb9a-227">![Admin](./media/active-directory-saas-bluejeans-tutorial/IC785877.png "Admin")</span></span>
   
   >[!IMPORTANT]
   ><span data-ttu-id="5bb9a-228">**Dodaj użytkownika** karta jest dostępna tylko, jeśli w **kartę Zabezpieczenia**, **Włącz automatyczne udostępnianie** nie jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-228">The **Add User** tab is only available if, in the **Security tab**, **Enable automatic provisioning** is unchecked.</span></span> 
   
3. <span data-ttu-id="5bb9a-229">W **Dodaj użytkownika** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5bb9a-229">In the **Add User** section, perform the following steps:</span></span>

    <span data-ttu-id="5bb9a-230">![Dodaj użytkownika](./media/active-directory-saas-bluejeans-tutorial/IC785886.png "Dodaj użytkownika")</span><span class="sxs-lookup"><span data-stu-id="5bb9a-230">![Add User](./media/active-directory-saas-bluejeans-tutorial/IC785886.png "Add User")</span></span>
    
    <span data-ttu-id="5bb9a-231">a.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-231">a.</span></span> <span data-ttu-id="5bb9a-232">Wpisz **BlueJeans Username**, **adres E-mail**, **identyfikator spotkania BlueJeans**, **moderatora kod dostępu**, **imię i nazwisko**, **firmy** poprawnego konta usługi AAD ustanawiane do powiązanych pól tekstowych.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-232">Type a **BlueJeans Username**, an **Email address**, a **BlueJeans Meeting ID**, a **Moderator Passcode**, a **Full Name**, the **Company** of a valid AAD account you want to provision into the related textboxes.</span></span>
    
    <span data-ttu-id="5bb9a-233">b.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-233">b.</span></span> <span data-ttu-id="5bb9a-234">Kliknij przycisk **dodać użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-234">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="5bb9a-235">Możesz użyć innych BlueJeans użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez BlueJeans do kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-235">You can use any other BlueJeans user account creation tools or APIs provided by BlueJeans to provision AAD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5bb9a-236">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bb9a-236">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5bb9a-237">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-237">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BlueJeans.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="5bb9a-239">**Aby przypisać Simona Britta BlueJeans, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5bb9a-239">**To assign Britta Simon to BlueJeans, perform the following steps:**</span></span>

1. <span data-ttu-id="5bb9a-240">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-240">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="5bb9a-242">Na liście aplikacji zaznacz **BlueJeans**.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-242">In the applications list, select **BlueJeans**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_app.png) 

3. <span data-ttu-id="5bb9a-244">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-244">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="5bb9a-246">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-246">Click **Add** button.</span></span> <span data-ttu-id="5bb9a-247">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-247">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="5bb9a-249">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-249">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5bb9a-250">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-250">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5bb9a-251">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-251">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5bb9a-252">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5bb9a-252">Testing single sign-on</span></span>

<span data-ttu-id="5bb9a-253">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-253">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5bb9a-254">Po kliknięciu kafelka BlueJeans w panelu dostępu, należy pobrać strony logowania BlueJeans aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5bb9a-254">When you click the BlueJeans tile in the Access Panel, you should get login page of BlueJeans application.</span></span>
<span data-ttu-id="5bb9a-255">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5bb9a-255">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5bb9a-256">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="5bb9a-256">Additional resources</span></span>

* [<span data-ttu-id="5bb9a-257">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5bb9a-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5bb9a-258">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5bb9a-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_203.png

