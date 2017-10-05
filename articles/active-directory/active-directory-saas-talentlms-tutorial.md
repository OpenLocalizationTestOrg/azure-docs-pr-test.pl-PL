---
title: 'Samouczek: Integracji Azure Active Directory z TalentLMS | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i TalentLMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c903d20d-18e3-42b0-b997-6349c5412dde
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: f28d6fbfad9dae578a20db7218b7e3b174ed859c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-talentlms"></a><span data-ttu-id="d831d-103">Samouczek: Integracji Azure Active Directory z TalentLMS</span><span class="sxs-lookup"><span data-stu-id="d831d-103">Tutorial: Azure Active Directory integration with TalentLMS</span></span>

<span data-ttu-id="d831d-104">Z tego samouczka dowiesz się integrowanie TalentLMS z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d831d-104">In this tutorial, you learn how to integrate TalentLMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d831d-105">Integracja z usługą Azure AD TalentLMS zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="d831d-105">Integrating TalentLMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d831d-106">Można kontrolować w usłudze Azure AD, który ma dostęp do TalentLMS</span><span class="sxs-lookup"><span data-stu-id="d831d-106">You can control in Azure AD who has access to TalentLMS</span></span>
- <span data-ttu-id="d831d-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do TalentLMS (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d831d-107">You can enable your users to automatically get signed-on to TalentLMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d831d-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="d831d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d831d-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d831d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d831d-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d831d-110">Prerequisites</span></span>

<span data-ttu-id="d831d-111">Aby skonfigurować integrację usługi Azure AD z TalentLMS, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="d831d-111">To configure Azure AD integration with TalentLMS, you need the following items:</span></span>

- <span data-ttu-id="d831d-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d831d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d831d-113">TalentLMS logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="d831d-113">A TalentLMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d831d-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="d831d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d831d-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="d831d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d831d-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="d831d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d831d-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna tutaj: [oferta wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d831d-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d831d-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="d831d-118">Scenario description</span></span>
<span data-ttu-id="d831d-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="d831d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d831d-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="d831d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d831d-121">Dodawanie TalentLMS z galerii</span><span class="sxs-lookup"><span data-stu-id="d831d-121">Adding TalentLMS from the gallery</span></span>
2. <span data-ttu-id="d831d-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="d831d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-talentlms-from-the-gallery"></a><span data-ttu-id="d831d-123">Dodawanie TalentLMS z galerii</span><span class="sxs-lookup"><span data-stu-id="d831d-123">Adding TalentLMS from the gallery</span></span>
<span data-ttu-id="d831d-124">Aby skonfigurować integrację usługi Azure AD TalentLMS, należy dodać TalentLMS z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="d831d-124">To configure the integration of TalentLMS into Azure AD, you need to add TalentLMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d831d-125">**Aby dodać TalentLMS z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="d831d-125">**To add TalentLMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d831d-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="d831d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="d831d-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="d831d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d831d-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="d831d-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="d831d-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d831d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="d831d-133">W polu wyszukiwania wpisz **TalentLMS**.</span><span class="sxs-lookup"><span data-stu-id="d831d-133">In the search box, type **TalentLMS**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_search.png)

5. <span data-ttu-id="d831d-135">W panelu wyników wybierz **TalentLMS**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="d831d-135">In the results panel, select **TalentLMS**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d831d-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="d831d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d831d-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z TalentLMS na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="d831d-138">In this section, you configure and test Azure AD single sign-on with TalentLMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d831d-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w TalentLMS jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d831d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in TalentLMS is to a user in Azure AD.</span></span> <span data-ttu-id="d831d-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w TalentLMS musi się.</span><span class="sxs-lookup"><span data-stu-id="d831d-140">In other words, a link relationship between an Azure AD user and the related user in TalentLMS needs to be established.</span></span>

<span data-ttu-id="d831d-141">W TalentLMS, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="d831d-141">In TalentLMS, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d831d-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z TalentLMS, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="d831d-142">To configure and test Azure AD single sign-on with TalentLMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d831d-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="d831d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d831d-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="d831d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d831d-145">**[Tworzenie użytkownika testowego TalentLMS](#creating-a-talentlms-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta TalentLMS połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d831d-145">**[Creating a TalentLMS test user](#creating-a-talentlms-test-user)** - to have a counterpart of Britta Simon in TalentLMS that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d831d-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d831d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d831d-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="d831d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d831d-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d831d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d831d-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji TalentLMS.</span><span class="sxs-lookup"><span data-stu-id="d831d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TalentLMS application.</span></span>

<span data-ttu-id="d831d-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z TalentLMS, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="d831d-150">**To configure Azure AD single sign-on with TalentLMS, perform the following steps:**</span></span>

1. <span data-ttu-id="d831d-151">W portalu Azure na **TalentLMS** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="d831d-151">In the Azure portal, on the **TalentLMS** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="d831d-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="d831d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_samlbase.png)

3. <span data-ttu-id="d831d-155">Na **TalentLMS domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="d831d-155">On the **TalentLMS Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_url.png)

    <span data-ttu-id="d831d-157">a.</span><span class="sxs-lookup"><span data-stu-id="d831d-157">a.</span></span> <span data-ttu-id="d831d-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<tenant-name>.TalentLMSapp.com`</span><span class="sxs-lookup"><span data-stu-id="d831d-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.TalentLMSapp.com`</span></span>

    <span data-ttu-id="d831d-159">b.</span><span class="sxs-lookup"><span data-stu-id="d831d-159">b.</span></span> <span data-ttu-id="d831d-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`http://<tenant-name>.talentlms.com`</span><span class="sxs-lookup"><span data-stu-id="d831d-160">In the **Identifier** textbox, type a URL using the following pattern: `http://<tenant-name>.talentlms.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d831d-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="d831d-161">These values are not real.</span></span> <span data-ttu-id="d831d-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="d831d-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d831d-163">Skontaktuj się z [zespołem pomocy technicznej klienta TalentLMS](https://www.talentlms.com/contact) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="d831d-163">Contact [TalentLMS Client support team](https://www.talentlms.com/contact) to get these values.</span></span> 
 
4. <span data-ttu-id="d831d-164">Na **certyfikat podpisywania SAML** sekcji, skopiuj **odcisk PALCA** wartości z certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="d831d-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value from the certificate.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_certificate.png) 

5. <span data-ttu-id="d831d-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d831d-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-talentlms-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d831d-168">Na **konfiguracji TalentLMS** , kliknij przycisk **skonfigurować TalentLMS** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="d831d-168">On the **TalentLMS Configuration** section, click **Configure TalentLMS** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d831d-169">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="d831d-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_configure.png)  

7. <span data-ttu-id="d831d-171">W oknie przeglądarki innej witryny sieci web należy zalogować się jako administrator do witryny firmy TalentLMS.</span><span class="sxs-lookup"><span data-stu-id="d831d-171">In a different web browser window, log in to your TalentLMS company site as an administrator.</span></span>

8. <span data-ttu-id="d831d-172">W **& Ustawienia konta** kliknij **użytkowników** kartę.</span><span class="sxs-lookup"><span data-stu-id="d831d-172">In the **Account & Settings** section, click the **Users** tab.</span></span>
   
    <span data-ttu-id="d831d-173">![& Ustawienia konta](./media/active-directory-saas-talentlms-tutorial/IC777296.png "& Ustawienia konta")</span><span class="sxs-lookup"><span data-stu-id="d831d-173">![Account & Settings](./media/active-directory-saas-talentlms-tutorial/IC777296.png "Account & Settings")</span></span>

9. <span data-ttu-id="d831d-174">Kliknij przycisk **logowanie jednokrotne (SSO)**,</span><span class="sxs-lookup"><span data-stu-id="d831d-174">Click **Single Sign-On (SSO)**,</span></span>

10. <span data-ttu-id="d831d-175">W sekcji rejestracji jednokrotnej wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="d831d-175">In the Single Sign-On section, perform the following steps:</span></span>
   
    <span data-ttu-id="d831d-176">![Logowanie jednokrotne](./media/active-directory-saas-talentlms-tutorial/IC777297.png "logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="d831d-176">![Single Sign-On](./media/active-directory-saas-talentlms-tutorial/IC777297.png "Single Sign-On")</span></span>   

    <span data-ttu-id="d831d-177">a.</span><span class="sxs-lookup"><span data-stu-id="d831d-177">a.</span></span> <span data-ttu-id="d831d-178">Z **Typ integracji logowania jednokrotnego** listy, wybierz **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="d831d-178">From the **SSO integration type** list, select **SAML 2.0**.</span></span>

    <span data-ttu-id="d831d-179">b.</span><span class="sxs-lookup"><span data-stu-id="d831d-179">b.</span></span> <span data-ttu-id="d831d-180">W **dostawcy tożsamości (IDP)** pole tekstowe, Wklej wartość **identyfikator jednostki SAML**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d831d-180">In the **Identity provider (IDP)** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="d831d-181">c.</span><span class="sxs-lookup"><span data-stu-id="d831d-181">c.</span></span> <span data-ttu-id="d831d-182">Wklej **odcisk palca** wartość z portalu Azure do **odcisk palca certyfikatu** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="d831d-182">Paste the **Thumbprint** value from Azure portal into the **Certificate fingerprint** textbox.</span></span>    

    <span data-ttu-id="d831d-183">d.</span><span class="sxs-lookup"><span data-stu-id="d831d-183">d.</span></span>  <span data-ttu-id="d831d-184">W **zdalnego logowania adresu URL** pole tekstowe, Wklej wartość **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d831d-184">In the **Remote sign-in URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="d831d-185">e.</span><span class="sxs-lookup"><span data-stu-id="d831d-185">e.</span></span> <span data-ttu-id="d831d-186">W **zdalnego adresu URL wylogowania** pole tekstowe, Wklej wartość **Sign-Out URL**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d831d-186">In the **Remote sign-out URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="d831d-187">f.</span><span class="sxs-lookup"><span data-stu-id="d831d-187">f.</span></span> <span data-ttu-id="d831d-188">Wypełnij następujące pozycje:</span><span class="sxs-lookup"><span data-stu-id="d831d-188">Fill in the following:</span></span> 

    * <span data-ttu-id="d831d-189">W **TargetedID** pole tekstowe, typ`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`</span><span class="sxs-lookup"><span data-stu-id="d831d-189">In the **TargetedID** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`</span></span>
     
    * <span data-ttu-id="d831d-190">W **imię** pole tekstowe, typ`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`</span><span class="sxs-lookup"><span data-stu-id="d831d-190">In the **First name** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`</span></span>
    
    * <span data-ttu-id="d831d-191">W **nazwisko** pole tekstowe, typ`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`</span><span class="sxs-lookup"><span data-stu-id="d831d-191">In the **Last name** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`</span></span>
    
    * <span data-ttu-id="d831d-192">W **E-mail** pole tekstowe, typ`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span><span class="sxs-lookup"><span data-stu-id="d831d-192">In the **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span></span>
    
11. <span data-ttu-id="d831d-193">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="d831d-193">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="d831d-194">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="d831d-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d831d-195">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="d831d-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d831d-196">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d831d-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d831d-197">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d831d-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="d831d-198">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="d831d-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="d831d-200">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="d831d-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d831d-201">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="d831d-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-talentlms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d831d-203">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="d831d-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-talentlms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d831d-205">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d831d-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-talentlms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d831d-207">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="d831d-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-talentlms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d831d-209">a.</span><span class="sxs-lookup"><span data-stu-id="d831d-209">a.</span></span> <span data-ttu-id="d831d-210">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d831d-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d831d-211">b.</span><span class="sxs-lookup"><span data-stu-id="d831d-211">b.</span></span> <span data-ttu-id="d831d-212">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d831d-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d831d-213">c.</span><span class="sxs-lookup"><span data-stu-id="d831d-213">c.</span></span> <span data-ttu-id="d831d-214">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="d831d-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d831d-215">d.</span><span class="sxs-lookup"><span data-stu-id="d831d-215">d.</span></span> <span data-ttu-id="d831d-216">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d831d-216">Click **Create**.</span></span>
 
### <a name="creating-a-talentlms-test-user"></a><span data-ttu-id="d831d-217">Tworzenie użytkownika testowego TalentLMS</span><span class="sxs-lookup"><span data-stu-id="d831d-217">Creating a TalentLMS test user</span></span>

<span data-ttu-id="d831d-218">Aby umożliwić użytkownikom usługi Azure AD zalogować się do TalentLMS, musi być przygotowana do TalentLMS.</span><span class="sxs-lookup"><span data-stu-id="d831d-218">To enable Azure AD users to log in to TalentLMS, they must be provisioned into TalentLMS.</span></span> <span data-ttu-id="d831d-219">W przypadku TalentLMS Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="d831d-219">In the case of TalentLMS, provisioning is a manual task.</span></span>

<span data-ttu-id="d831d-220">**Aby udostępnić konta użytkownika, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="d831d-220">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="d831d-221">Zaloguj się do Twojego **TalentLMS** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="d831d-221">Log in to your **TalentLMS** tenant.</span></span>

2. <span data-ttu-id="d831d-222">Kliknij przycisk **użytkowników**, a następnie kliknij przycisk **Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="d831d-222">Click **Users**, and then click **Add User**.</span></span>

3. <span data-ttu-id="d831d-223">Na **Dodaj użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="d831d-223">On the **Add user** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="d831d-224">![Dodaj użytkownika](./media/active-directory-saas-talentlms-tutorial/IC777299.png "Dodaj użytkownika")</span><span class="sxs-lookup"><span data-stu-id="d831d-224">![Add User](./media/active-directory-saas-talentlms-tutorial/IC777299.png "Add User")</span></span>  

    <span data-ttu-id="d831d-225">a.</span><span class="sxs-lookup"><span data-stu-id="d831d-225">a.</span></span> <span data-ttu-id="d831d-226">W **imię** pole tekstowe, wprowadź imię użytkownika, takich jak **Britta**.</span><span class="sxs-lookup"><span data-stu-id="d831d-226">In the **First name** textbox, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="d831d-227">b.</span><span class="sxs-lookup"><span data-stu-id="d831d-227">b.</span></span> <span data-ttu-id="d831d-228">W **nazwisko** pole tekstowe, wprowadź nazwisko użytkownika, takich jak **Simona**.</span><span class="sxs-lookup"><span data-stu-id="d831d-228">In the **Last name** textbox, enter the last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="d831d-229">c.</span><span class="sxs-lookup"><span data-stu-id="d831d-229">c.</span></span> <span data-ttu-id="d831d-230">W **adres E-mail** pole tekstowe, wprowadź adres e-mail użytkownika, takich jak  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="d831d-230">In the **Email address** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="d831d-231">d.</span><span class="sxs-lookup"><span data-stu-id="d831d-231">d.</span></span> <span data-ttu-id="d831d-232">Kliknij przycisk **dodać użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="d831d-232">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="d831d-233">Możesz użyć innych TalentLMS użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez TalentLMS do kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="d831d-233">You can use any other TalentLMS user account creation tools or APIs provided by TalentLMS to provision AAD user accounts.</span></span>
 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d831d-234">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d831d-234">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d831d-235">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu TalentLMS.</span><span class="sxs-lookup"><span data-stu-id="d831d-235">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TalentLMS.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="d831d-237">**Aby przypisać Simona Britta TalentLMS, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="d831d-237">**To assign Britta Simon to TalentLMS, perform the following steps:**</span></span>

1. <span data-ttu-id="d831d-238">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="d831d-238">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="d831d-240">Na liście aplikacji zaznacz **TalentLMS**.</span><span class="sxs-lookup"><span data-stu-id="d831d-240">In the applications list, select **TalentLMS**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_app.png) 

3. <span data-ttu-id="d831d-242">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="d831d-242">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="d831d-244">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d831d-244">Click **Add** button.</span></span> <span data-ttu-id="d831d-245">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d831d-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="d831d-247">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="d831d-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d831d-248">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d831d-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d831d-249">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d831d-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d831d-250">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d831d-250">Testing single sign-on</span></span>

<span data-ttu-id="d831d-251">Celem tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="d831d-251">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d831d-252">Po kliknięciu kafelka TalentLMS w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji TalentLMS</span><span class="sxs-lookup"><span data-stu-id="d831d-252">When you click the TalentLMS tile in the Access Panel, you should get automatically signed-on to your TalentLMS application</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d831d-253">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="d831d-253">Additional resources</span></span>

* [<span data-ttu-id="d831d-254">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d831d-254">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d831d-255">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d831d-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_203.png

