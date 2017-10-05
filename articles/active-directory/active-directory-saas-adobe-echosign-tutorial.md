---
title: "Samouczek: Integracji Azure Active Directory przy użyciu konta Adobe | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Adobe logowania."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f9385723-8fe7-4340-8afb-1508dac3e92b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: b413772de1af1fbb128d29b81e5831cfd6a39ab4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-sign"></a><span data-ttu-id="e7787-103">Samouczek: Integracji Azure Active Directory przy użyciu konta Adobe</span><span class="sxs-lookup"><span data-stu-id="e7787-103">Tutorial: Azure Active Directory integration with Adobe Sign</span></span>

<span data-ttu-id="e7787-104">Z tego samouczka dowiesz się sposobu integracji Podpisz Adobe z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e7787-104">In this tutorial, you learn how to integrate Adobe Sign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e7787-105">Integracji Podpisz Adobe z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="e7787-105">Integrating Adobe Sign with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e7787-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do programu Adobe logowania</span><span class="sxs-lookup"><span data-stu-id="e7787-106">You can control in Azure AD who has access to Adobe Sign</span></span>
- <span data-ttu-id="e7787-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do podpisania Adobe (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7787-107">You can enable your users to automatically get signed-on to Adobe Sign (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e7787-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="e7787-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e7787-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e7787-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e7787-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e7787-110">Prerequisites</span></span>

<span data-ttu-id="e7787-111">Aby skonfigurować integrację usługi Azure AD przy użyciu konta Adobe, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="e7787-111">To configure Azure AD integration with Adobe Sign, you need the following items:</span></span>

- <span data-ttu-id="e7787-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7787-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e7787-113">Adobe logowania jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="e7787-113">An Adobe Sign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e7787-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="e7787-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e7787-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="e7787-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e7787-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="e7787-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e7787-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e7787-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e7787-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="e7787-118">Scenario description</span></span>
<span data-ttu-id="e7787-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="e7787-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e7787-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="e7787-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e7787-121">Dodawanie Adobe logowania z galerii</span><span class="sxs-lookup"><span data-stu-id="e7787-121">Adding Adobe Sign from the gallery</span></span>
2. <span data-ttu-id="e7787-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="e7787-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adobe-sign-from-the-gallery"></a><span data-ttu-id="e7787-123">Dodawanie Adobe logowania z galerii</span><span class="sxs-lookup"><span data-stu-id="e7787-123">Adding Adobe Sign from the gallery</span></span>
<span data-ttu-id="e7787-124">Aby skonfigurować integrację Adobe logowania do usługi Azure AD, należy dodać Adobe logowania z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="e7787-124">To configure the integration of Adobe Sign into Azure AD, you need to add Adobe Sign from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e7787-125">**Aby dodać Adobe logowania z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="e7787-125">**To add Adobe Sign from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e7787-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="e7787-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="e7787-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="e7787-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e7787-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="e7787-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="e7787-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e7787-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="e7787-133">W polu wyszukiwania wpisz **znak Adobe**.</span><span class="sxs-lookup"><span data-stu-id="e7787-133">In the search box, type **Adobe Sign**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_search.png)

5. <span data-ttu-id="e7787-135">W panelu wyników wybierz **znak Adobe**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="e7787-135">In the results panel, select **Adobe Sign**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e7787-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="e7787-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e7787-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej znakiem Adobe oparte na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="e7787-138">In this section, you configure and test Azure AD single sign-on with Adobe Sign based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e7787-139">Do rejestracji jednokrotnej do pracy usługi Azure AD musi ustalić użytkownika odpowiednika w Adobe logowania do użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e7787-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Adobe Sign is to a user in Azure AD.</span></span> <span data-ttu-id="e7787-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i danemu użytkownikowi rejestracja Adobe musi określone.</span><span class="sxs-lookup"><span data-stu-id="e7787-140">In other words, a link relationship between an Azure AD user and the related user in Adobe Sign needs to be established.</span></span>

<span data-ttu-id="e7787-141">W Adobe logowania, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="e7787-141">In Adobe Sign, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e7787-142">Aby skonfigurować i przetestować usługi Azure AD logowania jednokrotnego przy użyciu konta Adobe, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="e7787-142">To configure and test Azure AD single sign-on with Adobe Sign, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e7787-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="e7787-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e7787-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="e7787-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e7787-145">**[Tworzenie użytkownika testowego znak Adobe](#creating-an-adobe-sign-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Adobe znaku, który jest połączony z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e7787-145">**[Creating an Adobe Sign test user](#creating-an-adobe-sign-test-user)** - to have a counterpart of Britta Simon in Adobe Sign that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e7787-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="e7787-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e7787-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="e7787-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e7787-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e7787-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e7787-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Adobe logowania.</span><span class="sxs-lookup"><span data-stu-id="e7787-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Adobe Sign application.</span></span>

<span data-ttu-id="e7787-150">**Aby skonfigurować usługi Azure AD logowania jednokrotnego przy użyciu konta Adobe, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="e7787-150">**To configure Azure AD single sign-on with Adobe Sign, perform the following steps:**</span></span>

1. <span data-ttu-id="e7787-151">W portalu Azure na **znak Adobe** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="e7787-151">In the Azure portal, on the **Adobe Sign** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="e7787-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="e7787-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_samlbase.png)

3. <span data-ttu-id="e7787-155">Na **Adobe logowania domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="e7787-155">On the **Adobe Sign Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_url.png)

    <span data-ttu-id="e7787-157">a.</span><span class="sxs-lookup"><span data-stu-id="e7787-157">a.</span></span> <span data-ttu-id="e7787-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.echosign.com/`</span><span class="sxs-lookup"><span data-stu-id="e7787-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.echosign.com/`</span></span>

    <span data-ttu-id="e7787-159">b.</span><span class="sxs-lookup"><span data-stu-id="e7787-159">b.</span></span> <span data-ttu-id="e7787-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.echosign.com`</span><span class="sxs-lookup"><span data-stu-id="e7787-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.echosign.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e7787-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="e7787-161">These values are not real.</span></span> <span data-ttu-id="e7787-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="e7787-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e7787-163">Skontaktuj się z [zespołem pomocy technicznej klienta logowania Adobe](https://helpx.adobe.com/in/contact/support.html) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="e7787-163">Contact [Adobe Sign Client support team](https://helpx.adobe.com/in/contact/support.html) to get these values.</span></span> 
 
4. <span data-ttu-id="e7787-164">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="e7787-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_certificate.png) 

5. <span data-ttu-id="e7787-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e7787-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e7787-168">Na **konfiguracji logowania Adobe** , kliknij przycisk **Konfigurowanie rejestrowania programu Adobe** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="e7787-168">On the **Adobe Sign Configuration** section, click **Configure Adobe Sign** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e7787-169">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="e7787-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_configure.png) 


7. <span data-ttu-id="e7787-171">W oknie przeglądarki innej witryny sieci web należy zalogować się jako administrator do witryny firmy Adobe logowania.</span><span class="sxs-lookup"><span data-stu-id="e7787-171">In a different web browser window, log in to your Adobe Sign company site as an administrator.</span></span>

8. <span data-ttu-id="e7787-172">W menu u góry kliknij **konta**, a następnie w okienku nawigacji po lewej stronie kliknij **ustawienia SAML** w obszarze **ustawienia konta**.</span><span class="sxs-lookup"><span data-stu-id="e7787-172">In the menu on the top, click **Account**, and then, in the navigation pane on the left side, click **SAML Settings** under **Account Settings**.</span></span>
   
   <span data-ttu-id="e7787-173">![Konto](./media/active-directory-saas-adobe-echosign-tutorial/ic789520.png "konta")</span><span class="sxs-lookup"><span data-stu-id="e7787-173">![Account](./media/active-directory-saas-adobe-echosign-tutorial/ic789520.png "Account")</span></span>

9. <span data-ttu-id="e7787-174">W sekcji Ustawienia SAML wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="e7787-174">In the SAML Settings section, perform the following steps:</span></span>
   
   <span data-ttu-id="e7787-175">![Ustawienia SAML](./media/active-directory-saas-adobe-echosign-tutorial/ic789521.png "ustawienia SAML")</span><span class="sxs-lookup"><span data-stu-id="e7787-175">![SAML Settings](./media/active-directory-saas-adobe-echosign-tutorial/ic789521.png "SAML Settings")</span></span>
   
   <span data-ttu-id="e7787-176">a.</span><span class="sxs-lookup"><span data-stu-id="e7787-176">a.</span></span> <span data-ttu-id="e7787-177">Jako **tryb SAML**, wybierz pozycję **SAML obowiązkowe**.</span><span class="sxs-lookup"><span data-stu-id="e7787-177">As **SAML Mode**, select **SAML Mandatory**.</span></span>
   
   <span data-ttu-id="e7787-178">b.</span><span class="sxs-lookup"><span data-stu-id="e7787-178">b.</span></span> <span data-ttu-id="e7787-179">Wybierz **Zezwalaj Administratorzy EchoSign konta logowania przy użyciu swoich poświadczeń EchoSign**.</span><span class="sxs-lookup"><span data-stu-id="e7787-179">Select **Allow EchoSign Account Administrators to log in using their EchoSign Credentials**.</span></span>
   
   <span data-ttu-id="e7787-180">c.</span><span class="sxs-lookup"><span data-stu-id="e7787-180">c.</span></span> <span data-ttu-id="e7787-181">Jako **Tworzenie użytkownika**, wybierz pozycję **automatyczne dodawanie użytkowników uwierzytelnionych za pośrednictwem SAML**.</span><span class="sxs-lookup"><span data-stu-id="e7787-181">As **User Creation**, select **Automatically add users authenticated through SAML**.</span></span>

10. <span data-ttu-id="e7787-182">Przenieś na, wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="e7787-182">Move on, performing the following steps:</span></span>

       <span data-ttu-id="e7787-183">![Ustawienia SAML](./media/active-directory-saas-adobe-echosign-tutorial/ic789522.png "ustawienia SAML")</span><span class="sxs-lookup"><span data-stu-id="e7787-183">![SAML Settings](./media/active-directory-saas-adobe-echosign-tutorial/ic789522.png "SAML Settings")</span></span>

    <span data-ttu-id="e7787-184">a.</span><span class="sxs-lookup"><span data-stu-id="e7787-184">a.</span></span> <span data-ttu-id="e7787-185">Wklej **identyfikator jednostki SAML**, które zostały skopiowane z portalu Azure do **IdP identyfikator jednostki** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="e7787-185">Paste **SAML Entity ID**, which you have copied from Azure portal into the **IdP Entity ID** textbox.</span></span>
    
    <span data-ttu-id="e7787-186">b.</span><span class="sxs-lookup"><span data-stu-id="e7787-186">b.</span></span> <span data-ttu-id="e7787-187">Wklej **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure do **adres URL logowania IdP** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="e7787-187">Paste **SAML Single Sign-On Service URL**, which you have copied from Azure portal into the **IdP Login URL** textbox.</span></span>
   
    <span data-ttu-id="e7787-188">c.</span><span class="sxs-lookup"><span data-stu-id="e7787-188">c.</span></span> <span data-ttu-id="e7787-189">Wklej **Sign-Out URL**, które zostały skopiowane z portalu Azure do **adresu URL wylogowania IdP** pole tekstowe.</span><span class="sxs-lookup"><span data-stu-id="e7787-189">Paste **Sign-Out URL**, which you have copied from Azure portal into the **IdP Logout URL** textbox.</span></span>

    <span data-ttu-id="e7787-190">d.</span><span class="sxs-lookup"><span data-stu-id="e7787-190">d.</span></span> <span data-ttu-id="e7787-191">Otwórz z pobranego **Certificate(Base64)** plików w programie Notatnik, skopiuj zawartość go do Schowka, a następnie wklej go do **certyfikatu IdP** pole tekstowe</span><span class="sxs-lookup"><span data-stu-id="e7787-191">Open your downloaded **Certificate(Base64)** file in notepad, copy the content of it into your clipboard, and then paste it to the **IdP Certificate** textbox</span></span>

    <span data-ttu-id="e7787-192">e.</span><span class="sxs-lookup"><span data-stu-id="e7787-192">e.</span></span> <span data-ttu-id="e7787-193">Kliknij przycisk **zapisać zmiany**.</span><span class="sxs-lookup"><span data-stu-id="e7787-193">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="e7787-194">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="e7787-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e7787-195">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="e7787-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e7787-196">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e7787-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e7787-197">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7787-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="e7787-198">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="e7787-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="e7787-200">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="e7787-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e7787-201">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="e7787-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e7787-203">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="e7787-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e7787-205">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e7787-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e7787-207">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="e7787-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e7787-209">a.</span><span class="sxs-lookup"><span data-stu-id="e7787-209">a.</span></span> <span data-ttu-id="e7787-210">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e7787-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e7787-211">b.</span><span class="sxs-lookup"><span data-stu-id="e7787-211">b.</span></span> <span data-ttu-id="e7787-212">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e7787-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e7787-213">c.</span><span class="sxs-lookup"><span data-stu-id="e7787-213">c.</span></span> <span data-ttu-id="e7787-214">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="e7787-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e7787-215">d.</span><span class="sxs-lookup"><span data-stu-id="e7787-215">d.</span></span> <span data-ttu-id="e7787-216">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="e7787-216">Click **Create**.</span></span>
 
### <a name="creating-an-adobe-sign-test-user"></a><span data-ttu-id="e7787-217">Tworzenie użytkownika testowego Adobe logowania</span><span class="sxs-lookup"><span data-stu-id="e7787-217">Creating an Adobe Sign test user</span></span>

<span data-ttu-id="e7787-218">Aby umożliwić użytkownikom usługi Azure AD zalogować się do logowania Adobe, muszą mieć przydzielone do programu Adobe logowania.</span><span class="sxs-lookup"><span data-stu-id="e7787-218">To enable Azure AD users to log in to Adobe Sign, they must be provisioned into Adobe Sign.</span></span> <span data-ttu-id="e7787-219">W przypadku logowania Adobe Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="e7787-219">In the case of Adobe Sign, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="e7787-220">Możesz użyć innych Adobe logowania użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Adobe logowania do kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="e7787-220">You can use any other Adobe Sign user account creation tools or APIs provided by Adobe Sign to provision AAD user accounts.</span></span> 

<span data-ttu-id="e7787-221">**Aby udostępnić konta użytkownika, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="e7787-221">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="e7787-222">Zaloguj się do Twojego **znak Adobe** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="e7787-222">Log in to your **Adobe Sign** company site as administrator.</span></span>

2. <span data-ttu-id="e7787-223">W menu u góry kliknij **konta**, a następnie w okienku nawigacji po lewej stronie kliknij **użytkownicy i grupy**, a następnie kliknij przycisk **utworzenie nowego użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="e7787-223">In the menu on the top, click **Account**, and then, in the navigation pane on the left side, click **Users & Groups**, and then, click **Create a new user**.</span></span>
   
   <span data-ttu-id="e7787-224">![Konto](./media/active-directory-saas-adobe-echosign-tutorial/ic789524.png "konta")</span><span class="sxs-lookup"><span data-stu-id="e7787-224">![Account](./media/active-directory-saas-adobe-echosign-tutorial/ic789524.png "Account")</span></span>
   
3. <span data-ttu-id="e7787-225">W **Tworzenie nowego użytkownika** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="e7787-225">In the **Create New User** section, perform the following steps:</span></span>
   
   <span data-ttu-id="e7787-226">![Utwórz użytkownika](./media/active-directory-saas-adobe-echosign-tutorial/ic789525.png "Tworzenie użytkownika")</span><span class="sxs-lookup"><span data-stu-id="e7787-226">![Create User](./media/active-directory-saas-adobe-echosign-tutorial/ic789525.png "Create User")</span></span>
   
   <span data-ttu-id="e7787-227">a.</span><span class="sxs-lookup"><span data-stu-id="e7787-227">a.</span></span> <span data-ttu-id="e7787-228">Typ **adres E-mail**, **imię**, i **nazwisko** poprawnego konta usługi AAD ustanawiane do powiązanych pól tekstowych.</span><span class="sxs-lookup"><span data-stu-id="e7787-228">Type the **Email Address**, **First Name**, and **Last Name** of a valid AAD account you want to provision into the related textboxes.</span></span>
   
   <span data-ttu-id="e7787-229">b.</span><span class="sxs-lookup"><span data-stu-id="e7787-229">b.</span></span> <span data-ttu-id="e7787-230">Kliknij przycisk **Utwórz użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="e7787-230">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="e7787-231">Właściciel konta usługi Azure Active Directory otrzymuje wiadomość e-mail zawierającą łącze do potwierdzenia konta, zanim staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="e7787-231">The Azure Active Directory account holder receives an email that includes a link to confirm the account before it becomes active.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e7787-232">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7787-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e7787-233">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do podpisania Adobe.</span><span class="sxs-lookup"><span data-stu-id="e7787-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Adobe Sign.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="e7787-235">**Aby przypisać Simona Britta Adobe logowania, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="e7787-235">**To assign Britta Simon to Adobe Sign, perform the following steps:**</span></span>

1. <span data-ttu-id="e7787-236">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="e7787-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="e7787-238">Na liście aplikacji zaznacz **znak Adobe**.</span><span class="sxs-lookup"><span data-stu-id="e7787-238">In the applications list, select **Adobe Sign**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_app.png) 

3. <span data-ttu-id="e7787-240">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="e7787-240">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="e7787-242">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e7787-242">Click **Add** button.</span></span> <span data-ttu-id="e7787-243">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e7787-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="e7787-245">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="e7787-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e7787-246">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e7787-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e7787-247">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e7787-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e7787-248">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e7787-248">Testing single sign-on</span></span>

<span data-ttu-id="e7787-249">Po kliknięciu kafelka Adobe logowania w panelu dostępu należy należy pobrać automatycznie zalogowane do aplikacji Adobe logowania.</span><span class="sxs-lookup"><span data-stu-id="e7787-249">When you click the Adobe Sign tile in the Access Panel, you should get automatically signed-on to your Adobe Sign application.</span></span>
<span data-ttu-id="e7787-250">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e7787-250">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e7787-251">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="e7787-251">Additional resources</span></span>

* [<span data-ttu-id="e7787-252">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e7787-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e7787-253">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e7787-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_203.png

