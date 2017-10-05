---
title: 'Samouczek: Integracji Azure Active Directory z Certify | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Zatwierdź."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0b36e020-175a-4534-b341-85260739f889
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: bbb2357d17535de438555a0b1f8256b134c8a40e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-certify"></a><span data-ttu-id="320fa-103">Samouczek: Integracji Azure Active Directory z Certify</span><span class="sxs-lookup"><span data-stu-id="320fa-103">Tutorial: Azure Active Directory integration with Certify</span></span>

<span data-ttu-id="320fa-104">Z tego samouczka dowiesz się sposobu integracji Podpisz w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="320fa-104">In this tutorial, you learn how to integrate Certify with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="320fa-105">Integracji Podpisz z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="320fa-105">Integrating Certify with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="320fa-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Certify</span><span class="sxs-lookup"><span data-stu-id="320fa-106">You can control in Azure AD who has access to Certify</span></span>
- <span data-ttu-id="320fa-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Certify (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="320fa-107">You can enable your users to automatically get signed-on to Certify (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="320fa-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="320fa-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="320fa-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="320fa-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="320fa-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="320fa-110">Prerequisites</span></span>

<span data-ttu-id="320fa-111">Aby skonfigurować integrację usługi Azure AD z Certify, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="320fa-111">To configure Azure AD integration with Certify, you need the following items:</span></span>

- <span data-ttu-id="320fa-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="320fa-112">An Azure AD subscription</span></span>
- <span data-ttu-id="320fa-113">Podpisz logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="320fa-113">A Certify single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="320fa-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="320fa-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="320fa-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="320fa-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="320fa-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="320fa-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="320fa-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="320fa-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="320fa-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="320fa-118">Scenario description</span></span>
<span data-ttu-id="320fa-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="320fa-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="320fa-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="320fa-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="320fa-121">Dodawanie Certify z galerii</span><span class="sxs-lookup"><span data-stu-id="320fa-121">Adding Certify from the gallery</span></span>
2. <span data-ttu-id="320fa-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="320fa-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-certify-from-the-gallery"></a><span data-ttu-id="320fa-123">Dodawanie Certify z galerii</span><span class="sxs-lookup"><span data-stu-id="320fa-123">Adding Certify from the gallery</span></span>
<span data-ttu-id="320fa-124">Aby skonfigurować integracji Podpisz do usługi Azure AD, należy dodać Certify z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="320fa-124">To configure the integration of Certify into Azure AD, you need to add Certify from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="320fa-125">**Aby dodać Certify z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="320fa-125">**To add Certify from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="320fa-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="320fa-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="320fa-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="320fa-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="320fa-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="320fa-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="320fa-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="320fa-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="320fa-133">W polu wyszukiwania wpisz **Certify**.</span><span class="sxs-lookup"><span data-stu-id="320fa-133">In the search box, type **Certify**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-certify-tutorial/tutorial_certify_search.png)

5. <span data-ttu-id="320fa-135">W panelu wyników wybierz **Certify**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="320fa-135">In the results panel, select **Certify**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-certify-tutorial/tutorial_certify_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="320fa-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="320fa-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="320fa-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Certify w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="320fa-138">In this section, you configure and test Azure AD single sign-on with Certify based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="320fa-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Certify jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="320fa-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Certify is to a user in Azure AD.</span></span> <span data-ttu-id="320fa-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Certify musi się.</span><span class="sxs-lookup"><span data-stu-id="320fa-140">In other words, a link relationship between an Azure AD user and the related user in Certify needs to be established.</span></span>

<span data-ttu-id="320fa-141">W Certify, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="320fa-141">In Certify, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="320fa-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Certify, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="320fa-142">To configure and test Azure AD single sign-on with Certify, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="320fa-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="320fa-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="320fa-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="320fa-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="320fa-145">**[Tworzenie użytkownika testowego Certify](#creating-a-certify-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta potwierdzenie, że jest połączony z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="320fa-145">**[Creating a Certify test user](#creating-a-certify-test-user)** - to have a counterpart of Britta Simon in Certify that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="320fa-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="320fa-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="320fa-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="320fa-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="320fa-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="320fa-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="320fa-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Certify.</span><span class="sxs-lookup"><span data-stu-id="320fa-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Certify application.</span></span>

<span data-ttu-id="320fa-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Certify, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="320fa-150">**To configure Azure AD single sign-on with Certify, perform the following steps:**</span></span>

1. <span data-ttu-id="320fa-151">W portalu Azure na **Certify** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="320fa-151">In the Azure portal, on the **Certify** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="320fa-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="320fa-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-certify-tutorial/tutorial_certify_samlbase.png)

3. <span data-ttu-id="320fa-155">Na **certyfikować domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="320fa-155">On the **Certify Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-certify-tutorial/tutorial_certify_url.png)

    <span data-ttu-id="320fa-157">W **identyfikator** tekstowym, wpisz adres URL:`https://www.certify.com`</span><span class="sxs-lookup"><span data-stu-id="320fa-157">In the **Identifier** textbox, type the URL: `https://www.certify.com`</span></span>

4. <span data-ttu-id="320fa-158">Na **certyfikat podpisywania SAML** kliknij **Certificate(Raw)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="320fa-158">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-certify-tutorial/tutorial_certify_certificate.png) 

5. <span data-ttu-id="320fa-160">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="320fa-160">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-certify-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="320fa-162">Na **certyfikować konfiguracji** kliknij **skonfigurować certyfikować** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="320fa-162">On the **Certify Configuration** section, click **Configure Certify** to open **Configure sign-on** window.</span></span> <span data-ttu-id="320fa-163">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="320fa-163">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-certify-tutorial/tutorial_certify_configure.png) 

7. <span data-ttu-id="320fa-165">Skonfigurować logowanie jednokrotne w **Certify** stronie, musisz wysłać pobrany **Certificate(Raw)** i **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** do [zespołem pomocy technicznej Certify](mailto:support@certify.com).</span><span class="sxs-lookup"><span data-stu-id="320fa-165">To configure single sign-on on **Certify** side, you need to send the downloaded **Certificate(Raw)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Certify support team](mailto:support@certify.com).</span></span> <span data-ttu-id="320fa-166">To ustawienie, aby były prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one wartość.</span><span class="sxs-lookup"><span data-stu-id="320fa-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="320fa-167">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="320fa-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="320fa-168">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="320fa-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="320fa-169">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="320fa-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="320fa-170">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="320fa-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="320fa-171">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="320fa-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="320fa-173">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="320fa-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="320fa-174">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="320fa-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-certify-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="320fa-176">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="320fa-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-certify-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="320fa-178">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="320fa-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-certify-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="320fa-180">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="320fa-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-certify-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="320fa-182">a.</span><span class="sxs-lookup"><span data-stu-id="320fa-182">a.</span></span> <span data-ttu-id="320fa-183">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="320fa-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="320fa-184">b.</span><span class="sxs-lookup"><span data-stu-id="320fa-184">b.</span></span> <span data-ttu-id="320fa-185">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="320fa-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="320fa-186">c.</span><span class="sxs-lookup"><span data-stu-id="320fa-186">c.</span></span> <span data-ttu-id="320fa-187">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="320fa-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="320fa-188">d.</span><span class="sxs-lookup"><span data-stu-id="320fa-188">d.</span></span> <span data-ttu-id="320fa-189">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="320fa-189">Click **Create**.</span></span>
 
### <a name="creating-a-certify-test-user"></a><span data-ttu-id="320fa-190">Tworzenie użytkownika testowego Certify</span><span class="sxs-lookup"><span data-stu-id="320fa-190">Creating a Certify test user</span></span>

<span data-ttu-id="320fa-191">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w Certify.</span><span class="sxs-lookup"><span data-stu-id="320fa-191">The objective of this section is to create a user called Britta Simon in Certify.</span></span> <span data-ttu-id="320fa-192">Zatwierdź obsługuje just-in-time inicjowania obsługi, który jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="320fa-192">Certify supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="320fa-193">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="320fa-193">There is no action item for you in this section.</span></span> <span data-ttu-id="320fa-194">Nowy użytkownik zostanie utworzony podczas próby dostępu Certify, jeśli go jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="320fa-194">A new user will be created during an attempt to access Certify if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="320fa-195">Jeśli trzeba ręcznie utworzyć użytkownika, należy skontaktować się [zespołem pomocy technicznej Certify](mailto:support@certify.com).</span><span class="sxs-lookup"><span data-stu-id="320fa-195">If you need to create an user manually, you need to contact the [Certify support team](mailto:support@certify.com).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="320fa-196">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="320fa-196">Assigning the Azure AD test user</span></span>

<span data-ttu-id="320fa-197">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Certify.</span><span class="sxs-lookup"><span data-stu-id="320fa-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Certify.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="320fa-199">**Aby przypisać Simona Britta Certify, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="320fa-199">**To assign Britta Simon to Certify, perform the following steps:**</span></span>

1. <span data-ttu-id="320fa-200">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="320fa-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="320fa-202">Na liście aplikacji zaznacz **Certify**.</span><span class="sxs-lookup"><span data-stu-id="320fa-202">In the applications list, select **Certify**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-certify-tutorial/tutorial_certify_app.png) 

3. <span data-ttu-id="320fa-204">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="320fa-204">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="320fa-206">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="320fa-206">Click **Add** button.</span></span> <span data-ttu-id="320fa-207">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="320fa-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="320fa-209">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="320fa-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="320fa-210">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="320fa-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="320fa-211">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="320fa-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="320fa-212">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="320fa-212">Testing single sign-on</span></span>

<span data-ttu-id="320fa-213">Celem tej sekcji służy do testowania konfigurację usługi Azure AD z logowania jednokrotnego za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="320fa-213">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="320fa-214">Po kliknięciu kafelka Certify w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Certify.</span><span class="sxs-lookup"><span data-stu-id="320fa-214">When you click the Certify tile in the Access Panel, you should get automatically signed-on to your Certify application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="320fa-215">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="320fa-215">Additional resources</span></span>

* [<span data-ttu-id="320fa-216">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="320fa-216">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="320fa-217">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="320fa-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-certify-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-certify-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-certify-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-certify-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-certify-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-certify-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-certify-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-certify-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-certify-tutorial/tutorial_general_203.png

