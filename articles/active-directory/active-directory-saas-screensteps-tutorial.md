---
title: 'Samouczek: Integracji Azure Active Directory z ScreenSteps | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i ScreenSteps."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4563fe94-a88f-4895-a07f-79df44889cf9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: b6ded8ba1adf03fdccbdb7573c09fae1857c8b16
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-screensteps"></a><span data-ttu-id="9e584-103">Samouczek: Integracji Azure Active Directory z ScreenSteps</span><span class="sxs-lookup"><span data-stu-id="9e584-103">Tutorial: Azure Active Directory integration with ScreenSteps</span></span>

<span data-ttu-id="9e584-104">Z tego samouczka dowiesz się integrowanie ScreenSteps z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9e584-104">In this tutorial, you learn how to integrate ScreenSteps with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9e584-105">Integracja z usługą Azure AD ScreenSteps zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="9e584-105">Integrating ScreenSteps with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9e584-106">Można kontrolować w usłudze Azure AD, który ma dostęp do ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="9e584-106">You can control in Azure AD who has access to ScreenSteps.</span></span>
- <span data-ttu-id="9e584-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do ScreenSteps (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9e584-107">You can enable your users to automatically get signed-on to ScreenSteps (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="9e584-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="9e584-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="9e584-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9e584-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9e584-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9e584-110">Prerequisites</span></span>

<span data-ttu-id="9e584-111">Aby skonfigurować integrację usługi Azure AD z ScreenSteps, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="9e584-111">To configure Azure AD integration with ScreenSteps, you need the following items:</span></span>

- <span data-ttu-id="9e584-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e584-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9e584-113">ScreenSteps logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="9e584-113">A ScreenSteps single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9e584-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="9e584-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9e584-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="9e584-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9e584-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="9e584-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9e584-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9e584-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9e584-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="9e584-118">Scenario description</span></span>
<span data-ttu-id="9e584-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="9e584-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9e584-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="9e584-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9e584-121">Dodawanie ScreenSteps z galerii</span><span class="sxs-lookup"><span data-stu-id="9e584-121">Adding ScreenSteps from the gallery</span></span>
2. <span data-ttu-id="9e584-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="9e584-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-screensteps-from-the-gallery"></a><span data-ttu-id="9e584-123">Dodawanie ScreenSteps z galerii</span><span class="sxs-lookup"><span data-stu-id="9e584-123">Adding ScreenSteps from the gallery</span></span>
<span data-ttu-id="9e584-124">Aby skonfigurować integrację usługi Azure AD ScreenSteps, należy dodać ScreenSteps z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="9e584-124">To configure the integration of ScreenSteps into Azure AD, you need to add ScreenSteps from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9e584-125">**Aby dodać ScreenSteps z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="9e584-125">**To add ScreenSteps from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9e584-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="9e584-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Przycisk usługi Azure Active Directory][1]

2. <span data-ttu-id="9e584-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="9e584-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9e584-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="9e584-129">Then go to **All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa][2]
    
3. <span data-ttu-id="9e584-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9e584-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Nowy przycisk aplikacji][3]

4. <span data-ttu-id="9e584-133">W polu wyszukiwania wpisz **ScreenSteps**, wybierz pozycję **ScreenSteps** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="9e584-133">In the search box, type **ScreenSteps**, select **ScreenSteps** from result panel then click **Add** button to add the application.</span></span>

    ![ScreenSteps na liście wyników](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="9e584-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9e584-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="9e584-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z ScreenSteps w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="9e584-136">In this section, you configure and test Azure AD single sign-on with ScreenSteps based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9e584-137">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w ScreenSteps jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9e584-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ScreenSteps is to a user in Azure AD.</span></span> <span data-ttu-id="9e584-138">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w ScreenSteps musi się.</span><span class="sxs-lookup"><span data-stu-id="9e584-138">In other words, a link relationship between an Azure AD user and the related user in ScreenSteps needs to be established.</span></span>

<span data-ttu-id="9e584-139">W ScreenSteps, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="9e584-139">In ScreenSteps, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9e584-140">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z ScreenSteps, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="9e584-140">To configure and test Azure AD single sign-on with ScreenSteps, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9e584-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="9e584-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9e584-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="9e584-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9e584-143">**[Tworzenie użytkownika testowego ScreenSteps](#create-a-screensteps-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta ScreenSteps połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9e584-143">**[Create a ScreenSteps test user](#create-a-screensteps-test-user)** - to have a counterpart of Britta Simon in ScreenSteps that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9e584-144">**[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="9e584-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9e584-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="9e584-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="9e584-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9e584-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="9e584-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="9e584-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ScreenSteps application.</span></span>

<span data-ttu-id="9e584-148">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z ScreenSteps, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="9e584-148">**To configure Azure AD single sign-on with ScreenSteps, perform the following steps:**</span></span>

1. <span data-ttu-id="9e584-149">W portalu Azure na **ScreenSteps** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="9e584-149">In the Azure portal, on the **ScreenSteps** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="9e584-151">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="9e584-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_samlbase.png)

3. <span data-ttu-id="9e584-153">Na **ScreenSteps domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9e584-153">On the **ScreenSteps Domain and URLs** section, perform the following steps:</span></span>

    ![Adresy URL i domeny ScreenSteps pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_url.png)

    <span data-ttu-id="9e584-155">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<tenantname>.ScreenSteps.com`</span><span class="sxs-lookup"><span data-stu-id="9e584-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.ScreenSteps.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9e584-156">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="9e584-156">This value is not real.</span></span> <span data-ttu-id="9e584-157">Zaktualizuj tę wartość rzeczywista logowania jednokrotnego adres URL, który znajduje się w dalszej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="9e584-157">Update this value with the actual Sign-On URL, which is explained later in this tutorial.</span></span> 

4. <span data-ttu-id="9e584-158">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="9e584-158">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Łącze pobierania certyfikatu](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_certificate.png) 

5. <span data-ttu-id="9e584-160">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9e584-160">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-screensteps-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9e584-162">Na **konfiguracji ScreenSteps** , kliknij przycisk **skonfigurować ScreenSteps** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="9e584-162">On the **ScreenSteps Configuration** section, click **Configure ScreenSteps** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9e584-163">Kopiuj **Sign-Out adresu URL i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="9e584-163">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfiguracja ScreenSteps](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_configure.png) 

7. <span data-ttu-id="9e584-165">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy ScreenSteps jako administrator.</span><span class="sxs-lookup"><span data-stu-id="9e584-165">In a different web browser window, log into your ScreenSteps company site as an administrator.</span></span>

8. <span data-ttu-id="9e584-166">Kliknij przycisk **ustawienia konta**.</span><span class="sxs-lookup"><span data-stu-id="9e584-166">Click **Account Settings**.</span></span>

    <span data-ttu-id="9e584-167">![Zarządzanie kontami](./media/active-directory-saas-screensteps-tutorial/ic778523.png "Zarządzanie kontami")</span><span class="sxs-lookup"><span data-stu-id="9e584-167">![Account management](./media/active-directory-saas-screensteps-tutorial/ic778523.png "Account management")</span></span>

9. <span data-ttu-id="9e584-168">Kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="9e584-168">Click **Single Sign-on**.</span></span>

    <span data-ttu-id="9e584-169">![Zdalne uwierzytelnianie](./media/active-directory-saas-screensteps-tutorial/ic778524.png "uwierzytelniania zdalnego")</span><span class="sxs-lookup"><span data-stu-id="9e584-169">![Remote authentication](./media/active-directory-saas-screensteps-tutorial/ic778524.png "Remote authentication")</span></span>

10. <span data-ttu-id="9e584-170">Kliknij przycisk **Tworzenie końcowego rejestracji jednokrotnej**.</span><span class="sxs-lookup"><span data-stu-id="9e584-170">Click **Create Single Sign-on Endpoint**.</span></span>

    <span data-ttu-id="9e584-171">![Zdalne uwierzytelnianie](./media/active-directory-saas-screensteps-tutorial/ic778525.png "uwierzytelniania zdalnego")</span><span class="sxs-lookup"><span data-stu-id="9e584-171">![Remote authentication](./media/active-directory-saas-screensteps-tutorial/ic778525.png "Remote authentication")</span></span>

11. <span data-ttu-id="9e584-172">W **utworzyć jeden znak na punkt końcowy** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9e584-172">In the **Create Single Sign-on Endpoint** section, perform the following steps:</span></span>

    <span data-ttu-id="9e584-173">![Tworzenie punktu końcowego uwierzytelniania](./media/active-directory-saas-screensteps-tutorial/ic778526.png "Tworzenie punktu końcowego uwierzytelniania")</span><span class="sxs-lookup"><span data-stu-id="9e584-173">![Create an authentication endpoint](./media/active-directory-saas-screensteps-tutorial/ic778526.png "Create an authentication endpoint")</span></span>
    
    <span data-ttu-id="9e584-174">a.</span><span class="sxs-lookup"><span data-stu-id="9e584-174">a.</span></span> <span data-ttu-id="9e584-175">W **tytuł** tekstowym, wpisz tytuł.</span><span class="sxs-lookup"><span data-stu-id="9e584-175">In the **Title** textbox, type a title.</span></span>
    
    <span data-ttu-id="9e584-176">b.</span><span class="sxs-lookup"><span data-stu-id="9e584-176">b.</span></span> <span data-ttu-id="9e584-177">Z **tryb** listy, wybierz **SAML**.</span><span class="sxs-lookup"><span data-stu-id="9e584-177">From the **Mode** list, select **SAML**.</span></span>
    
    <span data-ttu-id="9e584-178">c.</span><span class="sxs-lookup"><span data-stu-id="9e584-178">c.</span></span> <span data-ttu-id="9e584-179">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="9e584-179">Click **Create**.</span></span>

12. <span data-ttu-id="9e584-180">**Edytuj** nowy punkt końcowy.</span><span class="sxs-lookup"><span data-stu-id="9e584-180">**Edit** the new endpoint.</span></span>

    <span data-ttu-id="9e584-181">![Edytuj punktu końcowego](./media/active-directory-saas-screensteps-tutorial/ic778528.png "edycji punktu końcowego")</span><span class="sxs-lookup"><span data-stu-id="9e584-181">![Edit endpoint](./media/active-directory-saas-screensteps-tutorial/ic778528.png "Edit endpoint")</span></span>

13. <span data-ttu-id="9e584-182">W **edytować jeden znak na punkt końcowy** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9e584-182">In the **Edit Single Sign-on Endpoint** section, perform the following steps:</span></span>

    <span data-ttu-id="9e584-183">![Uwierzytelniania zdalnego punktu końcowego](./media/active-directory-saas-screensteps-tutorial/ic778527.png "uwierzytelniania zdalnego punktu końcowego")</span><span class="sxs-lookup"><span data-stu-id="9e584-183">![Remote authentication endpoint](./media/active-directory-saas-screensteps-tutorial/ic778527.png "Remote authentication endpoint")</span></span>

    <span data-ttu-id="9e584-184">a.</span><span class="sxs-lookup"><span data-stu-id="9e584-184">a.</span></span> <span data-ttu-id="9e584-185">Kliknij przycisk **Przekaż nowy plik certyfikatu SAML**, a następnie przekaż certyfikat, który został pobrany z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="9e584-185">Click **Upload new SAML Certificate file**, and then upload the certificate, which you have downloaded from Azure portal.</span></span>
    
    <span data-ttu-id="9e584-186">b.</span><span class="sxs-lookup"><span data-stu-id="9e584-186">b.</span></span> <span data-ttu-id="9e584-187">Wklej **SAML pojedynczy znak na adres URL usługi** wartość, która została skopiowana z portalu Azure do **zdalnego adresu URL logowania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="9e584-187">Paste **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **Remote Login URL** textbox.</span></span>
    
    <span data-ttu-id="9e584-188">c.</span><span class="sxs-lookup"><span data-stu-id="9e584-188">c.</span></span> <span data-ttu-id="9e584-189">Wklej **Sign-Out URL** wartość, która została skopiowana z portalu Azure do **adres URL wylogowania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="9e584-189">Paste **Sign-Out URL** value, which you have copied from the Azure portal into the **Log out URL** textbox.</span></span>
    
    <span data-ttu-id="9e584-190">d.</span><span class="sxs-lookup"><span data-stu-id="9e584-190">d.</span></span> <span data-ttu-id="9e584-191">Wybierz **grupy** do przypisywania użytkowników do po ich udostępnieniu.</span><span class="sxs-lookup"><span data-stu-id="9e584-191">Select a **Group** to assign users to when they are provisioned.</span></span>
    
    <span data-ttu-id="9e584-192">e.</span><span class="sxs-lookup"><span data-stu-id="9e584-192">e.</span></span> <span data-ttu-id="9e584-193">Kliknij przycisk **aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="9e584-193">Click **Update**.</span></span>

    <span data-ttu-id="9e584-194">f.</span><span class="sxs-lookup"><span data-stu-id="9e584-194">f.</span></span> <span data-ttu-id="9e584-195">Kopiuj **adres URL klienta SAML** do Schowka i Wklej do **adres URL logowania** textbox w **ScreenSteps domeny i adres URL** sekcji.</span><span class="sxs-lookup"><span data-stu-id="9e584-195">Copy the **SAML Consumer URL** to the clipboard and paste in to the **Sign-on URL** textbox in **ScreenSteps Domain and URLs** section.</span></span>
    
    <span data-ttu-id="9e584-196">g.</span><span class="sxs-lookup"><span data-stu-id="9e584-196">g.</span></span> <span data-ttu-id="9e584-197">Wróć do **Edytuj Endpoint rejestracji jednokrotnej**.</span><span class="sxs-lookup"><span data-stu-id="9e584-197">Return to the **Edit Single Sign-on Endpoint**.</span></span>
    
    <span data-ttu-id="9e584-198">h.</span><span class="sxs-lookup"><span data-stu-id="9e584-198">h.</span></span> <span data-ttu-id="9e584-199">Kliknij przycisk **domyślnym kontem** przycisk, aby używać tego punktu końcowego dla wszystkich użytkowników, którzy logują ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="9e584-199">Click the **Make default for account** button to use this endpoint for all users who log into ScreenSteps.</span></span> <span data-ttu-id="9e584-200">Alternatywnie możesz kliknąć **dodać do lokacji** przycisk, aby używać tego punktu końcowego dla określonych witryn internetowych w **ScreenSteps**.</span><span class="sxs-lookup"><span data-stu-id="9e584-200">Alternatively you can click the **Add to Site** button to use this endpoint for specific sites in **ScreenSteps**.</span></span>

> [!TIP]
> <span data-ttu-id="9e584-201">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="9e584-201">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9e584-202">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="9e584-202">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9e584-203">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9e584-203">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="9e584-204">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e584-204">Create an Azure AD test user</span></span>

<span data-ttu-id="9e584-205">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="9e584-205">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="9e584-207">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="9e584-207">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9e584-208">W portalu Azure, w okienku po lewej stronie kliknij **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9e584-208">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-screensteps-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="9e584-210">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="9e584-210">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-screensteps-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="9e584-212">Aby otworzyć **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** w górnej części **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="9e584-212">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Przycisk Dodaj](./media/active-directory-saas-screensteps-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="9e584-214">W **użytkownika** okna dialogowego wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9e584-214">In the **User** dialog box, perform the following steps:</span></span>

    ![Okno dialogowe użytkownika](./media/active-directory-saas-screensteps-tutorial/create_aaduser_04.png)

    <span data-ttu-id="9e584-216">a.</span><span class="sxs-lookup"><span data-stu-id="9e584-216">a.</span></span> <span data-ttu-id="9e584-217">W **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9e584-217">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9e584-218">b.</span><span class="sxs-lookup"><span data-stu-id="9e584-218">b.</span></span> <span data-ttu-id="9e584-219">W **nazwy użytkownika** wpisz adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="9e584-219">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="9e584-220">c.</span><span class="sxs-lookup"><span data-stu-id="9e584-220">c.</span></span> <span data-ttu-id="9e584-221">Wybierz **Pokaż hasło** pole wyboru, a następnie zanotuj wartość, która jest wyświetlana w **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="9e584-221">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="9e584-222">d.</span><span class="sxs-lookup"><span data-stu-id="9e584-222">d.</span></span> <span data-ttu-id="9e584-223">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="9e584-223">Click **Create**.</span></span>
 
### <a name="create-a-screensteps-test-user"></a><span data-ttu-id="9e584-224">Tworzenie użytkownika testowego ScreenSteps</span><span class="sxs-lookup"><span data-stu-id="9e584-224">Create a ScreenSteps test user</span></span>

<span data-ttu-id="9e584-225">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="9e584-225">In this section, you create a user called Britta Simon in ScreenSteps.</span></span> <span data-ttu-id="9e584-226">Praca z [zespołem pomocy technicznej klienta ScreenSteps](https://www.screensteps.com/contact) Aby dodać użytkowników do platformy ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="9e584-226">Work with [ScreenSteps Client support team](https://www.screensteps.com/contact) to add the users in the ScreenSteps platform.</span></span> <span data-ttu-id="9e584-227">Użytkownicy muszą utworzyć i aktywowana, aby użyć rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="9e584-227">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="9e584-228">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e584-228">Assign the Azure AD test user</span></span>

<span data-ttu-id="9e584-229">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="9e584-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ScreenSteps.</span></span>

![Przypisanie roli użytkownika][200] 

<span data-ttu-id="9e584-231">**Aby przypisać Simona Britta ScreenSteps, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="9e584-231">**To assign Britta Simon to ScreenSteps, perform the following steps:**</span></span>

1. <span data-ttu-id="9e584-232">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="9e584-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="9e584-234">Na liście aplikacji zaznacz **ScreenSteps**.</span><span class="sxs-lookup"><span data-stu-id="9e584-234">In the applications list, select **ScreenSteps**.</span></span>

    ![Łącze ScreenSteps na liście aplikacji](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_app.png)  

3. <span data-ttu-id="9e584-236">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="9e584-236">In the menu on the left, click **Users and groups**.</span></span>

    ![Łącze "Użytkownicy i grupy"][202]

4. <span data-ttu-id="9e584-238">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9e584-238">Click **Add** button.</span></span> <span data-ttu-id="9e584-239">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9e584-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![W okienku Dodaj przydziału][203]

5. <span data-ttu-id="9e584-241">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="9e584-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9e584-242">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9e584-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9e584-243">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9e584-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="9e584-244">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9e584-244">Test single sign-on</span></span>

<span data-ttu-id="9e584-245">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="9e584-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9e584-246">Po kliknięciu kafelka ScreenSteps w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="9e584-246">When you click the ScreenSteps tile in the Access Panel, you should get automatically signed-on to your ScreenSteps application.</span></span>
<span data-ttu-id="9e584-247">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9e584-247">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="9e584-248">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="9e584-248">Additional resources</span></span>

* [<span data-ttu-id="9e584-249">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9e584-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9e584-250">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9e584-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_203.png

