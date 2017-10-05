---
title: "Samouczek: Azure Active Directory integracji z pakietem adaptacyjną | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i adaptacyjną Suite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 13af9d00-116a-41b8-8ca0-4870b31e224c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 5d7ba2f4c7d814e3aaa1bf804ddc5030380ccb2d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adaptive-suite"></a><span data-ttu-id="cae4f-103">Samouczek: Integracji Azure Active Directory z adaptacyjną Suite</span><span class="sxs-lookup"><span data-stu-id="cae4f-103">Tutorial: Azure Active Directory integration with Adaptive Suite</span></span>

<span data-ttu-id="cae4f-104">W tym samouczku Dowiedz się integrowanie adaptacyjną pakietu z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cae4f-104">In this tutorial, you learn how to integrate Adaptive Suite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cae4f-105">Integrowanie adaptacyjną pakiet z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="cae4f-105">Integrating Adaptive Suite with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="cae4f-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do zestawu adaptacyjną</span><span class="sxs-lookup"><span data-stu-id="cae4f-106">You can control in Azure AD who has access to Adaptive Suite</span></span>
- <span data-ttu-id="cae4f-107">Umożliwia użytkownikom automatycznie pobrać zalogowane adaptacyjną pakietu (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="cae4f-107">You can enable your users to automatically get signed-on to Adaptive Suite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cae4f-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="cae4f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="cae4f-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cae4f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cae4f-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="cae4f-110">Prerequisites</span></span>

<span data-ttu-id="cae4f-111">Aby skonfigurować integrację usługi Azure AD z adaptacyjną Suite, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="cae4f-111">To configure Azure AD integration with Adaptive Suite, you need the following items:</span></span>

- <span data-ttu-id="cae4f-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="cae4f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cae4f-113">Pakiet adaptacyjną jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="cae4f-113">An Adaptive Suite single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cae4f-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="cae4f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cae4f-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="cae4f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cae4f-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="cae4f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cae4f-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cae4f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cae4f-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="cae4f-118">Scenario description</span></span>
<span data-ttu-id="cae4f-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="cae4f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cae4f-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="cae4f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cae4f-121">Dodawanie pakietu adaptacyjną z galerii</span><span class="sxs-lookup"><span data-stu-id="cae4f-121">Adding Adaptive Suite from the gallery</span></span>
2. <span data-ttu-id="cae4f-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="cae4f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adaptive-suite-from-the-gallery"></a><span data-ttu-id="cae4f-123">Dodawanie pakietu adaptacyjną z galerii</span><span class="sxs-lookup"><span data-stu-id="cae4f-123">Adding Adaptive Suite from the gallery</span></span>
<span data-ttu-id="cae4f-124">Aby skonfigurować integrację usługi Azure AD adaptacyjną pakietu, należy dodać pakiet adaptacyjną z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="cae4f-124">To configure the integration of Adaptive Suite into Azure AD, you need to add Adaptive Suite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="cae4f-125">**Aby dodać pakiet adaptacyjną z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="cae4f-125">**To add Adaptive Suite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="cae4f-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="cae4f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="cae4f-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="cae4f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="cae4f-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="cae4f-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="cae4f-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="cae4f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="cae4f-133">W polu wyszukiwania wpisz **Suite adaptacyjną**.</span><span class="sxs-lookup"><span data-stu-id="cae4f-133">In the search box, type **Adaptive Suite**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_search.png)

5. <span data-ttu-id="cae4f-135">W panelu wyników wybierz **Suite adaptacyjną**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="cae4f-135">In the results panel, select **Adaptive Suite**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cae4f-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="cae4f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cae4f-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z adaptacyjną pakietu na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="cae4f-138">In this section, you configure and test Azure AD single sign-on with Adaptive Suite based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="cae4f-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednikiem pakietu adaptacyjną jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cae4f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Adaptive Suite is to a user in Azure AD.</span></span> <span data-ttu-id="cae4f-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i danemu użytkownikowi pakietu adaptacyjną musi określone.</span><span class="sxs-lookup"><span data-stu-id="cae4f-140">In other words, a link relationship between an Azure AD user and the related user in Adaptive Suite needs to be established.</span></span>

<span data-ttu-id="cae4f-141">Adaptacyjną pakietu, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="cae4f-141">In Adaptive Suite, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="cae4f-142">Do konfigurowania i testowania usługi Azure AD rejestracji jednokrotnej z adaptacyjną pakietu, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="cae4f-142">To configure and test Azure AD single sign-on with Adaptive Suite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="cae4f-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="cae4f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="cae4f-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="cae4f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cae4f-145">**[Tworzenie użytkownika testowego adaptacyjną Suite](#creating-an-adaptive-suite-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta adaptacyjną pakiet, który jest połączony z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cae4f-145">**[Creating an Adaptive Suite test user](#creating-an-adaptive-suite-test-user)** - to have a counterpart of Britta Simon in Adaptive Suite that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="cae4f-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="cae4f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cae4f-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="cae4f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cae4f-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="cae4f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cae4f-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w adaptacyjną pakiet aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cae4f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Adaptive Suite application.</span></span>

<span data-ttu-id="cae4f-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z adaptacyjną pakiet, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="cae4f-150">**To configure Azure AD single sign-on with Adaptive Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="cae4f-151">W portalu Azure na **Suite adaptacyjną** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="cae4f-151">In the Azure portal, on the **Adaptive Suite** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="cae4f-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="cae4f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_samlbase.png)

3. <span data-ttu-id="cae4f-155">Na **adaptacyjną domeny Suite i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="cae4f-155">On the **Adaptive Suite Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_url.png)

    <span data-ttu-id="cae4f-157">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://login.adaptiveinsights.com:443/samlsso/<unique-id>`</span><span class="sxs-lookup"><span data-stu-id="cae4f-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://login.adaptiveinsights.com:443/samlsso/<unique-id>`</span></span>

    >[!NOTE]
    > <span data-ttu-id="cae4f-158">Tę wartość można uzyskać z adaptacyjną zestawu **ustawienia logowania jednokrotnego SAML** strony.</span><span class="sxs-lookup"><span data-stu-id="cae4f-158">You can get this value from the Adaptive Suite’s **SAML SSO Settings** page.</span></span>
    >  

4. <span data-ttu-id="cae4f-159">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="cae4f-159">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_certificate.png) 

5. <span data-ttu-id="cae4f-161">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="cae4f-161">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cae4f-163">Na **adaptacyjną konfiguracji pakietu** , kliknij przycisk **skonfigurować pakiet adaptacyjną** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="cae4f-163">On the **Adaptive Suite Configuration** section, click **Configure Adaptive Suite** to open **Configure sign-on** window.</span></span> <span data-ttu-id="cae4f-164">Kopiuj **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="cae4f-164">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_configure.png) 

7. <span data-ttu-id="cae4f-166">W oknie przeglądarki innej witryny sieci web należy zalogować się jako administrator do witryny firmy adaptacyjną Suite.</span><span class="sxs-lookup"><span data-stu-id="cae4f-166">In a different web browser window, log in to your Adaptive Suite company site as an administrator.</span></span>

8. <span data-ttu-id="cae4f-167">Przejdź do **Admin**.</span><span class="sxs-lookup"><span data-stu-id="cae4f-167">Go to **Admin**.</span></span>
   
    <span data-ttu-id="cae4f-168">![Administrator](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "administratora")</span><span class="sxs-lookup"><span data-stu-id="cae4f-168">![Admin](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")</span></span>

9. <span data-ttu-id="cae4f-169">W **użytkownikami i rolami** kliknij **Zarządzaj ustawieniami logowania jednokrotnego SAML**.</span><span class="sxs-lookup"><span data-stu-id="cae4f-169">In the **Users and Roles** section, click **Manage SAML SSO Settings**.</span></span>
   
    <span data-ttu-id="cae4f-170">![Zarządzanie ustawieniami logowania jednokrotnego SAML](./media/active-directory-saas-adaptivesuite-tutorial/IC805645.png "Zarządzanie ustawieniami logowania jednokrotnego SAML")</span><span class="sxs-lookup"><span data-stu-id="cae4f-170">![Manage SAML SSO Settings](./media/active-directory-saas-adaptivesuite-tutorial/IC805645.png "Manage SAML SSO Settings")</span></span>

10. <span data-ttu-id="cae4f-171">Na **ustawienia logowania jednokrotnego SAML** wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="cae4f-171">On the **SAML SSO Settings** page, perform the following steps:</span></span>
   
    <span data-ttu-id="cae4f-172">![Ustawienia logowania jednokrotnego SAML](./media/active-directory-saas-adaptivesuite-tutorial/IC805646.png "ustawienia logowania jednokrotnego SAML")</span><span class="sxs-lookup"><span data-stu-id="cae4f-172">![SAML SSO Settings](./media/active-directory-saas-adaptivesuite-tutorial/IC805646.png "SAML SSO Settings")</span></span>

    <span data-ttu-id="cae4f-173">a.</span><span class="sxs-lookup"><span data-stu-id="cae4f-173">a.</span></span> <span data-ttu-id="cae4f-174">W **Nazwa dostawcy tożsamości** tekstowym, wpisz nazwę dla danej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="cae4f-174">In the **Identity provider name** textbox, type a name for your configuration.</span></span>
    
    <span data-ttu-id="cae4f-175">b.</span><span class="sxs-lookup"><span data-stu-id="cae4f-175">b.</span></span> <span data-ttu-id="cae4f-176">Wklej **identyfikator jednostki SAML** wartość skopiowany z portalu Azure do **dostawcy tożsamości identyfikator jednostki** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="cae4f-176">Paste the **SAML Entity ID** value copied from Azure portal into the **Identity provider Entity ID** textbox.</span></span>
  
    <span data-ttu-id="cae4f-177">c.</span><span class="sxs-lookup"><span data-stu-id="cae4f-177">c.</span></span> <span data-ttu-id="cae4f-178">Wklej **SAML pojedynczy znak na adres URL usługi** wartość skopiowany z portalu Azure do **dostawcy tożsamości adresu URL logowania jednokrotnego** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="cae4f-178">Paste the **SAML Single Sign-On Service URL** value copied from Azure portal into the **Identity provider SSO URL** textbox.</span></span>
  
    <span data-ttu-id="cae4f-179">d.</span><span class="sxs-lookup"><span data-stu-id="cae4f-179">d.</span></span> <span data-ttu-id="cae4f-180">Wklej **SAML pojedynczy znak na adres URL usługi** wartość skopiowany z portalu Azure do **niestandardowy adres URL wylogowania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="cae4f-180">Paste the **SAML Single Sign-On Service URL** value copied from Azure portal into the **Custom logout URL** textbox.</span></span>
  
    <span data-ttu-id="cae4f-181">e.</span><span class="sxs-lookup"><span data-stu-id="cae4f-181">e.</span></span> <span data-ttu-id="cae4f-182">Aby przekazać certyfikat pobrany, kliknij przycisk **wybierz plik**.</span><span class="sxs-lookup"><span data-stu-id="cae4f-182">To upload your downloaded certificate, click **Choose file**.</span></span>
  
    <span data-ttu-id="cae4f-183">f.</span><span class="sxs-lookup"><span data-stu-id="cae4f-183">f.</span></span> <span data-ttu-id="cae4f-184">Wykonaj następujące czynności, aby uzyskać:</span><span class="sxs-lookup"><span data-stu-id="cae4f-184">Select the following, for:</span></span>
    * <span data-ttu-id="cae4f-185">**Identyfikator użytkownika SAML**, wybierz pozycję **nazwy użytkownika adaptacyjną Insights**.</span><span class="sxs-lookup"><span data-stu-id="cae4f-185">**SAML user id**, select **User’s Adaptive Insights user name**.</span></span>
    * <span data-ttu-id="cae4f-186">**Lokalizacja identyfikator użytkownika SAML**, wybierz pozycję **identyfikatora użytkownika w NameID podmiotu**.</span><span class="sxs-lookup"><span data-stu-id="cae4f-186">**SAML user id location**, select **User id in NameID of Subject**.</span></span>
    * <span data-ttu-id="cae4f-187">**Format SAML NameID**, wybierz pozycję **adres E-mail**.</span><span class="sxs-lookup"><span data-stu-id="cae4f-187">**SAML NameID format**, select **Email address**.</span></span>
    * <span data-ttu-id="cae4f-188">**Włącz SAML**, wybierz pozycję **Zezwalaj logowania jednokrotnego SAML i bezpośrednie logowanie adaptacyjną Insights**.</span><span class="sxs-lookup"><span data-stu-id="cae4f-188">**Enable SAML**, select **Allow SAML SSO and direct Adaptive Insights login**.</span></span>
    
    <span data-ttu-id="cae4f-189">g.</span><span class="sxs-lookup"><span data-stu-id="cae4f-189">g.</span></span> <span data-ttu-id="cae4f-190">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="cae4f-190">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="cae4f-191">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="cae4f-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="cae4f-192">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="cae4f-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="cae4f-193">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cae4f-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cae4f-194">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="cae4f-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="cae4f-195">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="cae4f-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="cae4f-197">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="cae4f-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="cae4f-198">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="cae4f-198">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cae4f-200">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="cae4f-200">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cae4f-202">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="cae4f-202">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cae4f-204">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="cae4f-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cae4f-206">a.</span><span class="sxs-lookup"><span data-stu-id="cae4f-206">a.</span></span> <span data-ttu-id="cae4f-207">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cae4f-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cae4f-208">b.</span><span class="sxs-lookup"><span data-stu-id="cae4f-208">b.</span></span> <span data-ttu-id="cae4f-209">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cae4f-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cae4f-210">c.</span><span class="sxs-lookup"><span data-stu-id="cae4f-210">c.</span></span> <span data-ttu-id="cae4f-211">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="cae4f-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="cae4f-212">d.</span><span class="sxs-lookup"><span data-stu-id="cae4f-212">d.</span></span> <span data-ttu-id="cae4f-213">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="cae4f-213">Click **Create**.</span></span>
 
### <a name="creating-an-adaptive-suite-test-user"></a><span data-ttu-id="cae4f-214">Tworzenie użytkownika testowego adaptacyjną Suite</span><span class="sxs-lookup"><span data-stu-id="cae4f-214">Creating an Adaptive Suite test user</span></span>

<span data-ttu-id="cae4f-215">Aby umożliwić użytkownikom usługi Azure AD zalogować się do adaptacyjnego Suite, muszą mieć przydzielone do adaptacyjnego Suite.</span><span class="sxs-lookup"><span data-stu-id="cae4f-215">To enable Azure AD users to log in to Adaptive Suite, they must be provisioned into Adaptive Suite.</span></span>  

* <span data-ttu-id="cae4f-216">W przypadku adaptacyjną Suite Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="cae4f-216">In the case of Adaptive Suite, provisioning is a manual task.</span></span>

<span data-ttu-id="cae4f-217">**Aby skonfigurować, inicjowanie obsługi użytkowników, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="cae4f-217">**To configure user provisioning, perform the following steps:**</span></span> 

1. <span data-ttu-id="cae4f-218">Zaloguj się do Twojego **Suite adaptacyjną** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="cae4f-218">Log in to your **Adaptive Suite** company site as an administrator.</span></span>
2. <span data-ttu-id="cae4f-219">Przejdź do **Admin**.</span><span class="sxs-lookup"><span data-stu-id="cae4f-219">Go to **Admin**.</span></span>
   
   <span data-ttu-id="cae4f-220">![Administrator](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "administratora")</span><span class="sxs-lookup"><span data-stu-id="cae4f-220">![Admin](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")</span></span>
3. <span data-ttu-id="cae4f-221">W **użytkownikami i rolami** kliknij **Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="cae4f-221">In the **Users and Roles** section, click **Add User**.</span></span>
   
   <span data-ttu-id="cae4f-222">![Dodaj użytkownika](./media/active-directory-saas-adaptivesuite-tutorial/IC805648.png "Dodaj użytkownika")</span><span class="sxs-lookup"><span data-stu-id="cae4f-222">![Add User](./media/active-directory-saas-adaptivesuite-tutorial/IC805648.png "Add User")</span></span>
4. <span data-ttu-id="cae4f-223">W **nowego użytkownika** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="cae4f-223">In the **New User** section, perform the following steps:</span></span>
   
   <span data-ttu-id="cae4f-224">![Przedstawia](./media/active-directory-saas-adaptivesuite-tutorial/IC805649.png "przesyłania")</span><span class="sxs-lookup"><span data-stu-id="cae4f-224">![Submit](./media/active-directory-saas-adaptivesuite-tutorial/IC805649.png "Submit")</span></span>   

   <span data-ttu-id="cae4f-225">a.</span><span class="sxs-lookup"><span data-stu-id="cae4f-225">a.</span></span> <span data-ttu-id="cae4f-226">Typ **nazwa**, **logowania**, **E-mail**, **hasło** z prawidłowym użytkownikiem usługi Azure Active Directory chcesz udostępnić w odnośnych pola tekstowe.</span><span class="sxs-lookup"><span data-stu-id="cae4f-226">Type the **Name**, **Login**, **Email**, **Password** of a valid Azure Active Directory user you want to provision into the related textboxes.</span></span>
  
   <span data-ttu-id="cae4f-227">b.</span><span class="sxs-lookup"><span data-stu-id="cae4f-227">b.</span></span> <span data-ttu-id="cae4f-228">Wybierz **roli**.</span><span class="sxs-lookup"><span data-stu-id="cae4f-228">Select a **Role**.</span></span>
  
   <span data-ttu-id="cae4f-229">c.</span><span class="sxs-lookup"><span data-stu-id="cae4f-229">c.</span></span> <span data-ttu-id="cae4f-230">Kliknij przycisk **przesłać**.</span><span class="sxs-lookup"><span data-stu-id="cae4f-230">Click **Submit**.</span></span>

>[!NOTE]
><span data-ttu-id="cae4f-231">Możesz użyć innych adaptacyjną Suite użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez pakiet adaptacyjną do kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="cae4f-231">You can use any other Adaptive Suite user account creation tools or APIs provided by Adaptive Suite to provision AAD user accounts.</span></span>
>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="cae4f-232">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="cae4f-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="cae4f-233">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do zestawu adaptacyjną.</span><span class="sxs-lookup"><span data-stu-id="cae4f-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Adaptive Suite.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="cae4f-235">**Aby przypisać Simona Britta adaptacyjną pakietu, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="cae4f-235">**To assign Britta Simon to Adaptive Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="cae4f-236">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="cae4f-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="cae4f-238">Na liście aplikacji zaznacz **Suite adaptacyjną**.</span><span class="sxs-lookup"><span data-stu-id="cae4f-238">In the applications list, select **Adaptive Suite**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_app.png) 

3. <span data-ttu-id="cae4f-240">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="cae4f-240">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="cae4f-242">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="cae4f-242">Click **Add** button.</span></span> <span data-ttu-id="cae4f-243">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="cae4f-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="cae4f-245">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="cae4f-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="cae4f-246">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="cae4f-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cae4f-247">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="cae4f-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cae4f-248">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="cae4f-248">Testing single sign-on</span></span>

<span data-ttu-id="cae4f-249">Celem tej sekcji służy do testowania usługi Microsoft Azure AD rejestracji jednokrotnej konfigurację za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="cae4f-249">The objective of this section is to test your Microsoft Azure AD Single Sign-On configuration using the Access Panel.</span></span>

<span data-ttu-id="cae4f-250">Po kliknięciu kafelka adaptacyjną Suite w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane adaptacyjną pakiet aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cae4f-250">When you click the Adaptive Suite tile in the Access Panel, you should get automatically signed-on to your Adaptive Suite application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="cae4f-251">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="cae4f-251">Additional resources</span></span>

* [<span data-ttu-id="cae4f-252">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cae4f-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cae4f-253">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cae4f-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_203.png

