---
title: 'Samouczek: Integracji Azure Active Directory z Evernote | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Evernote."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: be94152a84bbbeacb623d7dd8b540e3981931a8e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-evernote"></a><span data-ttu-id="ab374-103">Samouczek: Integracji Azure Active Directory z Evernote</span><span class="sxs-lookup"><span data-stu-id="ab374-103">Tutorial: Azure Active Directory integration with Evernote</span></span>

<span data-ttu-id="ab374-104">Z tego samouczka dowiesz się integrowanie Evernote z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ab374-104">In this tutorial, you learn how to integrate Evernote with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ab374-105">Integracja z usługą Azure AD Evernote zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="ab374-105">Integrating Evernote with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ab374-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Evernote.</span><span class="sxs-lookup"><span data-stu-id="ab374-106">You can control in Azure AD who has access to Evernote.</span></span>
- <span data-ttu-id="ab374-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Evernote (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ab374-107">You can enable your users to automatically get signed-on to Evernote (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="ab374-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ab374-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="ab374-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ab374-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ab374-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ab374-110">Prerequisites</span></span>

<span data-ttu-id="ab374-111">Aby skonfigurować integrację usługi Azure AD z Evernote, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="ab374-111">To configure Azure AD integration with Evernote, you need the following items:</span></span>

- <span data-ttu-id="ab374-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ab374-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ab374-113">Evernote logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="ab374-113">An Evernote single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ab374-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="ab374-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ab374-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="ab374-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ab374-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="ab374-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ab374-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ab374-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ab374-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="ab374-118">Scenario description</span></span>
<span data-ttu-id="ab374-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="ab374-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ab374-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="ab374-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ab374-121">Dodawanie Evernote z galerii</span><span class="sxs-lookup"><span data-stu-id="ab374-121">Adding Evernote from the gallery</span></span>
2. <span data-ttu-id="ab374-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="ab374-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-evernote-from-the-gallery"></a><span data-ttu-id="ab374-123">Dodawanie Evernote z galerii</span><span class="sxs-lookup"><span data-stu-id="ab374-123">Adding Evernote from the gallery</span></span>
<span data-ttu-id="ab374-124">Aby skonfigurować integrację usługi Azure AD Evernote, należy dodać Evernote z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="ab374-124">To configure the integration of Evernote into Azure AD, you need to add Evernote from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ab374-125">**Aby dodać Evernote z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="ab374-125">**To add Evernote from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ab374-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ab374-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Przycisk usługi Azure Active Directory][1]

2. <span data-ttu-id="ab374-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="ab374-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ab374-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ab374-129">Then go to **All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa][2]
    
3. <span data-ttu-id="ab374-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ab374-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Nowy przycisk aplikacji][3]

4. <span data-ttu-id="ab374-133">W polu wyszukiwania wpisz **Evernote**, wybierz pozycję **Evernote** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="ab374-133">In the search box, type **Evernote**, select **Evernote** from result panel then click **Add** button to add the application.</span></span>

    ![Evernote na liście wyników](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ab374-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ab374-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="ab374-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Evernote w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="ab374-136">In this section, you configure and test Azure AD single sign-on with Evernote based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ab374-137">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Evernote jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ab374-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Evernote is to a user in Azure AD.</span></span> <span data-ttu-id="ab374-138">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Evernote musi się.</span><span class="sxs-lookup"><span data-stu-id="ab374-138">In other words, a link relationship between an Azure AD user and the related user in Evernote needs to be established.</span></span>

<span data-ttu-id="ab374-139">W Evernote, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="ab374-139">In Evernote, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ab374-140">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Evernote, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="ab374-140">To configure and test Azure AD single sign-on with Evernote, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ab374-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="ab374-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ab374-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="ab374-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ab374-143">**[Tworzenie użytkownika testowego Evernote](#create-an-evernote-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Evernote połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ab374-143">**[Create an Evernote test user](#create-an-evernote-test-user)** - to have a counterpart of Britta Simon in Evernote that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ab374-144">**[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ab374-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ab374-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="ab374-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="ab374-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ab374-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="ab374-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Evernote.</span><span class="sxs-lookup"><span data-stu-id="ab374-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Evernote application.</span></span>

<span data-ttu-id="ab374-148">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Evernote, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="ab374-148">**To configure Azure AD single sign-on with Evernote, perform the following steps:**</span></span>

1. <span data-ttu-id="ab374-149">W portalu Azure na **Evernote** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="ab374-149">In the Azure portal, on the **Evernote** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="ab374-151">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="ab374-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_samlbase.png)

3. <span data-ttu-id="ab374-153">Na **Evernote domeny i adres URL** sekcji, wykonaj następujące kroki, aby skonfigurować aplikację w trybie IDP inicjowane:</span><span class="sxs-lookup"><span data-stu-id="ab374-153">On the **Evernote Domain and URLs** section, perform the following steps if you wish to configure the application in IDP initiated mode:</span></span>

    ![Adresy URL i domeny Evernote pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_url.png)

    <span data-ttu-id="ab374-155">W **identyfikator** tekstowym, wpisz adres URL:`https://www.evernote.com/saml2`</span><span class="sxs-lookup"><span data-stu-id="ab374-155">In the **Identifier** textbox, type the URL: `https://www.evernote.com/saml2`</span></span>

4. <span data-ttu-id="ab374-156">Sprawdź **Pokaż zaawansowane ustawienia adresu URL** i wykonać następujący krok, jeśli chcesz skonfigurować aplikację w **SP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="ab374-156">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Adresy URL i domeny Evernote pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_url1.png)

    <span data-ttu-id="ab374-158">W **Zaloguj się na adres URL** tekstowym, wpisz adres URL:`https://www.evernote.com/Login.action`</span><span class="sxs-lookup"><span data-stu-id="ab374-158">In the **Sign on URL** textbox, type the URL: `https://www.evernote.com/Login.action`</span></span>   

5. <span data-ttu-id="ab374-159">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="ab374-159">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Łącze pobierania certyfikatu](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_certificate.png) 

6. <span data-ttu-id="ab374-161">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ab374-161">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-evernote-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="ab374-163">Na **konfiguracji Evernote** , kliknij przycisk **skonfigurować Evernote** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="ab374-163">On the **Evernote Configuration** section, click **Configure Evernote** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ab374-164">Kopiuj **SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="ab374-164">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfiguracja Evernote](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_configure.png) 

8. <span data-ttu-id="ab374-166">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy Evernote jako administrator.</span><span class="sxs-lookup"><span data-stu-id="ab374-166">In a different web browser window, log into your Evernote company site as an administrator.</span></span>

9. <span data-ttu-id="ab374-167">Przejdź do **"Konsoli administracyjnej"**</span><span class="sxs-lookup"><span data-stu-id="ab374-167">Go to **'Admin Console'**</span></span>

    ![Konsola administracyjna](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_adminconsole.png)

10. <span data-ttu-id="ab374-169">Z **"Konsoli administracyjnej"**, przejdź do **"Zabezpieczenia"** i wybierz **"Logowanie jednokrotne"**</span><span class="sxs-lookup"><span data-stu-id="ab374-169">From the **'Admin Console'**, go to **‘Security’** and select **‘Single Sign-On’**</span></span>

    ![Ustawienia logowania jednokrotnego](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_sso.png)

11. <span data-ttu-id="ab374-171">Skonfiguruj następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="ab374-171">Configure the following values:</span></span>

    ![Ustawienia certyfikatów](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_certx.png)
    
    <span data-ttu-id="ab374-173">a.</span><span class="sxs-lookup"><span data-stu-id="ab374-173">a.</span></span>  <span data-ttu-id="ab374-174">**Włącz logowanie Jednokrotne:** rejestracji Jednokrotnej jest domyślnie włączona (kliknij **wyłączyć logowanie jednokrotne** Aby usunąć wymaganie logowania jednokrotnego)</span><span class="sxs-lookup"><span data-stu-id="ab374-174">**Enable SSO:** SSO is enabled by default (Click **Disable Single Sign-on** to remove the SSO requirement)</span></span>

    <span data-ttu-id="ab374-175">b.</span><span class="sxs-lookup"><span data-stu-id="ab374-175">b.</span></span> <span data-ttu-id="ab374-176">Wklej **SAML rejestracji jednokrotnej adres URL usługi** wartość, która została skopiowana z portalu Azure do **adres URL żądania HTTP SAML** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="ab374-176">Paste **SAML Single sign-on Service URL** value, which you have copied from the Azure portal into the **SAML HTTP Request URL** textbox.</span></span>

    <span data-ttu-id="ab374-177">c.</span><span class="sxs-lookup"><span data-stu-id="ab374-177">c.</span></span> <span data-ttu-id="ab374-178">Otwórz certyfikat pobrany z usługi Azure AD w programie Notatnik i skopiuj zawartość, w tym "Certyfikat BEGIN" i "END CERTIFICATE" i wklej ją do **certyfikatu X.509** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="ab374-178">Open the downloaded certificate from Azure AD in a notepad and copy the content including "BEGIN CERTIFICATE" and "END CERTIFICATE" and paste it into the **X.509 Certificate** textbox.</span></span> 

    <span data-ttu-id="ab374-179">d.Click **zapisać zmiany**</span><span class="sxs-lookup"><span data-stu-id="ab374-179">d.Click **Save Changes**</span></span>

> [!TIP]
> <span data-ttu-id="ab374-180">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="ab374-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ab374-181">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="ab374-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ab374-182">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ab374-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ab374-183">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ab374-183">Create an Azure AD test user</span></span>

<span data-ttu-id="ab374-184">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="ab374-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="ab374-186">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="ab374-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ab374-187">W portalu Azure, w okienku po lewej stronie kliknij **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ab374-187">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-evernote-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="ab374-189">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="ab374-189">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-evernote-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="ab374-191">Aby otworzyć **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** w górnej części **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="ab374-191">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Przycisk Dodaj](./media/active-directory-saas-evernote-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="ab374-193">W **użytkownika** okna dialogowego wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ab374-193">In the **User** dialog box, perform the following steps:</span></span>

    ![Okno dialogowe użytkownika](./media/active-directory-saas-evernote-tutorial/create_aaduser_04.png)

    <span data-ttu-id="ab374-195">a.</span><span class="sxs-lookup"><span data-stu-id="ab374-195">a.</span></span> <span data-ttu-id="ab374-196">W **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ab374-196">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ab374-197">b.</span><span class="sxs-lookup"><span data-stu-id="ab374-197">b.</span></span> <span data-ttu-id="ab374-198">W **nazwy użytkownika** wpisz adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="ab374-198">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="ab374-199">c.</span><span class="sxs-lookup"><span data-stu-id="ab374-199">c.</span></span> <span data-ttu-id="ab374-200">Wybierz **Pokaż hasło** pole wyboru, a następnie zanotuj wartość, która jest wyświetlana w **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="ab374-200">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="ab374-201">d.</span><span class="sxs-lookup"><span data-stu-id="ab374-201">d.</span></span> <span data-ttu-id="ab374-202">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="ab374-202">Click **Create**.</span></span>
 
### <a name="create-an-evernote-test-user"></a><span data-ttu-id="ab374-203">Tworzenie użytkownika testowego Evernote</span><span class="sxs-lookup"><span data-stu-id="ab374-203">Create an Evernote test user</span></span>

<span data-ttu-id="ab374-204">Aby włączyć użytkowników usługi Azure AD zalogować się do Evernote, musi być przygotowana do Evernote.</span><span class="sxs-lookup"><span data-stu-id="ab374-204">In order to enable Azure AD users to log into Evernote, they must be provisioned into Evernote.</span></span>  
<span data-ttu-id="ab374-205">W przypadku Evernote Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="ab374-205">In the case of Evernote, provisioning is a manual task.</span></span>

<span data-ttu-id="ab374-206">**Aby udostępnić konta użytkowników, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="ab374-206">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="ab374-207">Zaloguj się do witryny firmy Evernote jako administrator.</span><span class="sxs-lookup"><span data-stu-id="ab374-207">Log in to your Evernote company site as an administrator.</span></span>

2. <span data-ttu-id="ab374-208">Kliknij przycisk **"Konsoli administracyjnej"**.</span><span class="sxs-lookup"><span data-stu-id="ab374-208">Click the **'Admin Console'**.</span></span>

    ![Konsola administracyjna](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_adminconsole.png)

3. <span data-ttu-id="ab374-210">Z **"Konsoli administracyjnej"**, przejdź do **"Dodawanie użytkowników"**.</span><span class="sxs-lookup"><span data-stu-id="ab374-210">From the **'Admin Console'**, go to **‘Add users’**.</span></span>

    ![Dodaj testUser](./media/active-directory-saas-evernote-tutorial/create_aaduser_0001.png)

4. <span data-ttu-id="ab374-212">**Dodawanie członków zespołu** w **E-mail** tekstowym, wpisz adres e-mail konta użytkownika i kliknij przycisk **zaprosić.**</span><span class="sxs-lookup"><span data-stu-id="ab374-212">**Add team members** in the **Email** textbox, type the email address of user account and click **Invite.**</span></span>

    ![Dodaj testUser](./media/active-directory-saas-evernote-tutorial/create_aaduser_0002.png)
    
5. <span data-ttu-id="ab374-214">Po wysłaniu zaproszenia, właścicielem konta usługi Azure Active Directory zostanie wysłana wiadomość e-mail o zaakceptowanie zaproszenia.</span><span class="sxs-lookup"><span data-stu-id="ab374-214">After invitation is sent, the Azure Active Directory account holder will receive an email to accept the invitation.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="ab374-215">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ab374-215">Assign the Azure AD test user</span></span>

<span data-ttu-id="ab374-216">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Evernote.</span><span class="sxs-lookup"><span data-stu-id="ab374-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Evernote.</span></span>

![Przypisanie roli użytkownika][200] 

<span data-ttu-id="ab374-218">**Aby przypisać Simona Britta Evernote, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="ab374-218">**To assign Britta Simon to Evernote, perform the following steps:**</span></span>

1. <span data-ttu-id="ab374-219">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ab374-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="ab374-221">Na liście aplikacji zaznacz **Evernote**.</span><span class="sxs-lookup"><span data-stu-id="ab374-221">In the applications list, select **Evernote**.</span></span>

    ![Łącze Evernote na liście aplikacji](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_app.png)  

3. <span data-ttu-id="ab374-223">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="ab374-223">In the menu on the left, click **Users and groups**.</span></span>

    ![Łącze "Użytkownicy i grupy"][202]

4. <span data-ttu-id="ab374-225">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ab374-225">Click **Add** button.</span></span> <span data-ttu-id="ab374-226">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ab374-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![W okienku Dodaj przydziału][203]

5. <span data-ttu-id="ab374-228">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="ab374-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ab374-229">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ab374-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ab374-230">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ab374-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="ab374-231">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ab374-231">Test single sign-on</span></span>

<span data-ttu-id="ab374-232">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="ab374-232">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ab374-233">Po kliknięciu kafelka Evernote w panelu dostępu użytkownik powinien pobrać zalogowane do aplikacji Evernote.</span><span class="sxs-lookup"><span data-stu-id="ab374-233">When you click the Evernote tile in the Access Panel, you should get signed-on to your Evernote application.</span></span> <span data-ttu-id="ab374-234">Można będzie można logować się jako organizacji konta muszą jednak następnie zaloguj się przy użyciu konta osobistego.</span><span class="sxs-lookup"><span data-stu-id="ab374-234">You'll be logging in as an Organization account but then need to log in with your personal account.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ab374-235">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="ab374-235">Additional resources</span></span>

* [<span data-ttu-id="ab374-236">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ab374-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ab374-237">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ab374-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_203.png

