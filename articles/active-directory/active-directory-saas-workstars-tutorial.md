---
title: 'Samouczek: Integracji Azure Active Directory z Workstars | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Workstars."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 51a4a4e4-ff60-4971-b3f8-a0367b70d220
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: e17c85689fa3aebf00ebf559185032b90103b4a5
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workstars"></a><span data-ttu-id="7454f-103">Samouczek: Integracji Azure Active Directory z Workstars</span><span class="sxs-lookup"><span data-stu-id="7454f-103">Tutorial: Azure Active Directory integration with Workstars</span></span>

<span data-ttu-id="7454f-104">Z tego samouczka dowiesz się integrowanie Workstars z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7454f-104">In this tutorial, you learn how to integrate Workstars with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7454f-105">Integracja z usługą Azure AD Workstars zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="7454f-105">Integrating Workstars with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7454f-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Workstars.</span><span class="sxs-lookup"><span data-stu-id="7454f-106">You can control in Azure AD who has access to Workstars.</span></span>
- <span data-ttu-id="7454f-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Workstars (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7454f-107">You can enable your users to automatically get signed-on to Workstars (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="7454f-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="7454f-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="7454f-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7454f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7454f-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7454f-110">Prerequisites</span></span>

<span data-ttu-id="7454f-111">Aby skonfigurować integrację usługi Azure AD z Workstars, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="7454f-111">To configure Azure AD integration with Workstars, you need the following items:</span></span>

- <span data-ttu-id="7454f-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7454f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7454f-113">Workstars logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="7454f-113">A Workstars single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7454f-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="7454f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7454f-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="7454f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7454f-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="7454f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7454f-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7454f-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7454f-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="7454f-118">Scenario description</span></span>
<span data-ttu-id="7454f-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="7454f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7454f-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="7454f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7454f-121">Dodawanie Workstars z galerii</span><span class="sxs-lookup"><span data-stu-id="7454f-121">Adding Workstars from the gallery</span></span>
2. <span data-ttu-id="7454f-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="7454f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workstars-from-the-gallery"></a><span data-ttu-id="7454f-123">Dodawanie Workstars z galerii</span><span class="sxs-lookup"><span data-stu-id="7454f-123">Adding Workstars from the gallery</span></span>
<span data-ttu-id="7454f-124">Aby skonfigurować integrację usługi Azure AD Workstars, należy dodać Workstars z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="7454f-124">To configure the integration of Workstars into Azure AD, you need to add Workstars from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7454f-125">**Aby dodać Workstars z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="7454f-125">**To add Workstars from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7454f-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="7454f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Przycisk usługi Azure Active Directory][1]

2. <span data-ttu-id="7454f-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="7454f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7454f-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="7454f-129">Then go to **All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa][2]
    
3. <span data-ttu-id="7454f-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7454f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Nowy przycisk aplikacji][3]

4. <span data-ttu-id="7454f-133">W polu wyszukiwania wpisz **Workstars**, wybierz pozycję **Workstars** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="7454f-133">In the search box, type **Workstars**, select **Workstars** from result panel then click **Add** button to add the application.</span></span>

    ![Workstars na liście wyników](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7454f-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="7454f-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="7454f-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Workstars w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="7454f-136">In this section, you configure and test Azure AD single sign-on with Workstars based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7454f-137">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Workstars jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7454f-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Workstars is to a user in Azure AD.</span></span> <span data-ttu-id="7454f-138">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Workstars musi się.</span><span class="sxs-lookup"><span data-stu-id="7454f-138">In other words, a link relationship between an Azure AD user and the related user in Workstars needs to be established.</span></span>

<span data-ttu-id="7454f-139">W Workstars, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="7454f-139">In Workstars, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7454f-140">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Workstars, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="7454f-140">To configure and test Azure AD single sign-on with Workstars, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7454f-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="7454f-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7454f-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="7454f-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7454f-143">**[Tworzenie użytkownika testowego Workstars](#create-a-workstars-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Workstars połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7454f-143">**[Create a Workstars test user](#create-a-workstars-test-user)** - to have a counterpart of Britta Simon in Workstars that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7454f-144">**[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="7454f-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7454f-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="7454f-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7454f-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="7454f-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7454f-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Workstars.</span><span class="sxs-lookup"><span data-stu-id="7454f-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workstars application.</span></span>

<span data-ttu-id="7454f-148">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Workstars, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="7454f-148">**To configure Azure AD single sign-on with Workstars, perform the following steps:**</span></span>

1. <span data-ttu-id="7454f-149">W portalu Azure na **Workstars** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="7454f-149">In the Azure portal, on the **Workstars** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="7454f-151">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="7454f-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_samlbase.png)

3. <span data-ttu-id="7454f-153">Na **Workstars domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7454f-153">On the **Workstars Domain and URLs** section, perform the following steps:</span></span>

    ![Adresy URL i domeny Workstars pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_url.png)

    <span data-ttu-id="7454f-155">a.</span><span class="sxs-lookup"><span data-stu-id="7454f-155">a.</span></span> <span data-ttu-id="7454f-156">W **identyfikator** tekstowym, wpisz adres URL:`https://workstars.com`</span><span class="sxs-lookup"><span data-stu-id="7454f-156">In the **Identifier** textbox, type the URL: `https://workstars.com`</span></span>

    <span data-ttu-id="7454f-157">b.</span><span class="sxs-lookup"><span data-stu-id="7454f-157">b.</span></span> <span data-ttu-id="7454f-158">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.workstars.com/saml/login_check`</span><span class="sxs-lookup"><span data-stu-id="7454f-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.workstars.com/saml/login_check`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7454f-159">Wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="7454f-159">The value is not real.</span></span> <span data-ttu-id="7454f-160">Zaktualizuj tę wartość do rzeczywistego adresu URL odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="7454f-160">Update the value with the actual Reply URL.</span></span> <span data-ttu-id="7454f-161">Skontaktuj się z [Workstars obsługuje zespołu](https://support.workstars.com) można uzyskać wartość.</span><span class="sxs-lookup"><span data-stu-id="7454f-161">Contact [Workstars support team](https://support.workstars.com) to get the value.</span></span>
 
4. <span data-ttu-id="7454f-162">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="7454f-162">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Łącze pobierania certyfikatu](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_certificate.png) 

5. <span data-ttu-id="7454f-164">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="7454f-164">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-workstars-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7454f-166">Na **konfiguracji Workstars** , kliknij przycisk **skonfigurować Workstars** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="7454f-166">On the **Workstars Configuration** section, click **Configure Workstars** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7454f-167">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="7454f-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfiguracja Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_configure.png) 

7. <span data-ttu-id="7454f-169">W innym oknie przeglądarki należy zalogować się jako administrator do witryny firmy Workstars.</span><span class="sxs-lookup"><span data-stu-id="7454f-169">In another browser window, sign on to your Workstars company site as an administrator.</span></span>

8. <span data-ttu-id="7454f-170">Na głównym pasku narzędzi, kliknij przycisk **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="7454f-170">In the main toolbar, click **Settings**.</span></span>

    ![Ustaw Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_sett.png)

9. <span data-ttu-id="7454f-172">Przejdź do **logowania** > **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="7454f-172">Go to **Sign On** > **Settings**.</span></span>

    ![Logować Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_signon.png)

    ![Ustawienia Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_settings.png)

10. <span data-ttu-id="7454f-175">Na **pojedynczy znak na (SAML) — ustawienia** wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7454f-175">On the **Single Sign On (SAML) - Settings** page, perform the following steps:</span></span>
    
    ![Workstars saml](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_saml.png)

    <span data-ttu-id="7454f-177">a.</span><span class="sxs-lookup"><span data-stu-id="7454f-177">a.</span></span> <span data-ttu-id="7454f-178">W **Nazwa dostawcy tożsamości** pole tekstowe, typ **usługi Office 365**.</span><span class="sxs-lookup"><span data-stu-id="7454f-178">In **Identity Provider Name** textbox, type **Office 365**.</span></span>

    <span data-ttu-id="7454f-179">b.</span><span class="sxs-lookup"><span data-stu-id="7454f-179">b.</span></span> <span data-ttu-id="7454f-180">W **identyfikator jednostki dostawcy tożsamości** pole tekstowe, Wklej wartość **identyfikator jednostki SAML**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="7454f-180">In the **Identity Provider Entity ID** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="7454f-181">c.</span><span class="sxs-lookup"><span data-stu-id="7454f-181">c.</span></span> <span data-ttu-id="7454f-182">Skopiuj zawartość pliku pobranego certyfikatu w programie Notatnik, a następnie wklej go do **x509 certyfikatu** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="7454f-182">Copy the content of the downloaded certificate file in notepad, and then paste it into the **x509 Certificate** textbox.</span></span> 

    <span data-ttu-id="7454f-183">d.</span><span class="sxs-lookup"><span data-stu-id="7454f-183">d.</span></span> <span data-ttu-id="7454f-184">W **adres URL logowania jednokrotnego SAML** pole tekstowe, Wklej wartość **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="7454f-184">In the **SAML SSO URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="7454f-185">e.</span><span class="sxs-lookup"><span data-stu-id="7454f-185">e.</span></span> <span data-ttu-id="7454f-186">W **zdalnego adresu URL wylogowania** pole tekstowe, Wklej wartość **Sign-Out URL**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="7454f-186">In the **Remote Logout URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="7454f-187">f.</span><span class="sxs-lookup"><span data-stu-id="7454f-187">f.</span></span> <span data-ttu-id="7454f-188">Wybierz **Identyfikatora nazwy** jako **poczty E-mail (ustawienie domyślne)**.</span><span class="sxs-lookup"><span data-stu-id="7454f-188">select **Name ID** as **Email (Default)**.</span></span>

    <span data-ttu-id="7454f-189">g.</span><span class="sxs-lookup"><span data-stu-id="7454f-189">g.</span></span> <span data-ttu-id="7454f-190">Kliknij przycisk **potwierdzić**.</span><span class="sxs-lookup"><span data-stu-id="7454f-190">Click **Confirm**.</span></span>
    
> [!TIP]
> <span data-ttu-id="7454f-191">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="7454f-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7454f-192">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="7454f-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7454f-193">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7454f-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7454f-194">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7454f-194">Create an Azure AD test user</span></span>

<span data-ttu-id="7454f-195">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="7454f-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="7454f-197">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="7454f-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7454f-198">W portalu Azure, w okienku po lewej stronie kliknij **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="7454f-198">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-workstars-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="7454f-200">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="7454f-200">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-workstars-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="7454f-202">Aby otworzyć **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** w górnej części **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="7454f-202">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Przycisk Dodaj](./media/active-directory-saas-workstars-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="7454f-204">W **użytkownika** okna dialogowego wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7454f-204">In the **User** dialog box, perform the following steps:</span></span>

    ![Okno dialogowe użytkownika](./media/active-directory-saas-workstars-tutorial/create_aaduser_04.png)

    <span data-ttu-id="7454f-206">a.</span><span class="sxs-lookup"><span data-stu-id="7454f-206">a.</span></span> <span data-ttu-id="7454f-207">W **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7454f-207">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7454f-208">b.</span><span class="sxs-lookup"><span data-stu-id="7454f-208">b.</span></span> <span data-ttu-id="7454f-209">W **nazwy użytkownika** wpisz adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="7454f-209">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="7454f-210">c.</span><span class="sxs-lookup"><span data-stu-id="7454f-210">c.</span></span> <span data-ttu-id="7454f-211">Wybierz **Pokaż hasło** pole wyboru, a następnie zanotuj wartość, która jest wyświetlana w **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="7454f-211">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="7454f-212">d.</span><span class="sxs-lookup"><span data-stu-id="7454f-212">d.</span></span> <span data-ttu-id="7454f-213">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="7454f-213">Click **Create**.</span></span>
  
### <a name="create-a-workstars-test-user"></a><span data-ttu-id="7454f-214">Tworzenie użytkownika testowego Workstars</span><span class="sxs-lookup"><span data-stu-id="7454f-214">Create a Workstars test user</span></span>

<span data-ttu-id="7454f-215">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Workstars.</span><span class="sxs-lookup"><span data-stu-id="7454f-215">In this section, you create a user called Britta Simon in Workstars.</span></span> <span data-ttu-id="7454f-216">Praca z [Workstars obsługuje zespołu](https://support.workstars.com) Aby dodać użytkowników do platformy Workstars.</span><span class="sxs-lookup"><span data-stu-id="7454f-216">Work with [Workstars support team](https://support.workstars.com) to add the users in the Workstars platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="7454f-217">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7454f-217">Assign the Azure AD test user</span></span>

<span data-ttu-id="7454f-218">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Workstars.</span><span class="sxs-lookup"><span data-stu-id="7454f-218">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workstars.</span></span>

![Przypisanie roli użytkownika][200] 

<span data-ttu-id="7454f-220">**Aby przypisać Simona Britta Workstars, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="7454f-220">**To assign Britta Simon to Workstars, perform the following steps:**</span></span>

1. <span data-ttu-id="7454f-221">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="7454f-221">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="7454f-223">Na liście aplikacji zaznacz **Workstars**.</span><span class="sxs-lookup"><span data-stu-id="7454f-223">In the applications list, select **Workstars**.</span></span>

    ![Łącze Workstars na liście aplikacji](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_app.png)  

3. <span data-ttu-id="7454f-225">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="7454f-225">In the menu on the left, click **Users and groups**.</span></span>

    ![Łącze "Użytkownicy i grupy"][202]

4. <span data-ttu-id="7454f-227">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="7454f-227">Click **Add** button.</span></span> <span data-ttu-id="7454f-228">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7454f-228">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![W okienku Dodaj przydziału][203]

5. <span data-ttu-id="7454f-230">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="7454f-230">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7454f-231">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7454f-231">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7454f-232">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7454f-232">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="7454f-233">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="7454f-233">Test single sign-on</span></span>

<span data-ttu-id="7454f-234">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="7454f-234">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7454f-235">Po kliknięciu kafelka Workstars w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Workstars.</span><span class="sxs-lookup"><span data-stu-id="7454f-235">When you click the Workstars tile in the Access Panel, you should get automatically signed-on to your Workstars application.</span></span>
<span data-ttu-id="7454f-236">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7454f-236">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7454f-237">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="7454f-237">Additional resources</span></span>

* [<span data-ttu-id="7454f-238">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7454f-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7454f-239">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7454f-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_203.png

