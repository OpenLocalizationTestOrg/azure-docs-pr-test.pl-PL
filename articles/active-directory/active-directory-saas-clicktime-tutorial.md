---
title: 'Samouczek: Integracji Azure Active Directory z ClickTime | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i ClickTime."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d437b5ab-4d71-4c13-96d0-79018cebbbd4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: jeedes
ms.openlocfilehash: 0e0123a40d52dfd7a2e29c29cb2239e979089ca9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clicktime"></a><span data-ttu-id="fab6c-103">Samouczek: Integracji Azure Active Directory z ClickTime</span><span class="sxs-lookup"><span data-stu-id="fab6c-103">Tutorial: Azure Active Directory integration with ClickTime</span></span>

<span data-ttu-id="fab6c-104">Z tego samouczka dowiesz się integrowanie ClickTime z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fab6c-104">In this tutorial, you learn how to integrate ClickTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fab6c-105">Integracja z usługą Azure AD ClickTime zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="fab6c-105">Integrating ClickTime with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="fab6c-106">Można kontrolować w usłudze Azure AD, który ma dostęp do ClickTime</span><span class="sxs-lookup"><span data-stu-id="fab6c-106">You can control in Azure AD who has access to ClickTime</span></span>
- <span data-ttu-id="fab6c-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do ClickTime (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="fab6c-107">You can enable your users to automatically get signed-on to ClickTime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fab6c-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="fab6c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="fab6c-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fab6c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fab6c-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="fab6c-110">Prerequisites</span></span>

<span data-ttu-id="fab6c-111">Aby skonfigurować integrację usługi Azure AD z ClickTime, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="fab6c-111">To configure Azure AD integration with ClickTime, you need the following items:</span></span>

- <span data-ttu-id="fab6c-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="fab6c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fab6c-113">ClickTime logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="fab6c-113">A ClickTime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fab6c-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="fab6c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fab6c-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="fab6c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fab6c-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="fab6c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fab6c-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fab6c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fab6c-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="fab6c-118">Scenario description</span></span>
<span data-ttu-id="fab6c-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="fab6c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fab6c-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="fab6c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fab6c-121">Dodawanie ClickTime z galerii</span><span class="sxs-lookup"><span data-stu-id="fab6c-121">Adding ClickTime from the gallery</span></span>
2. <span data-ttu-id="fab6c-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="fab6c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-clicktime-from-the-gallery"></a><span data-ttu-id="fab6c-123">Dodawanie ClickTime z galerii</span><span class="sxs-lookup"><span data-stu-id="fab6c-123">Adding ClickTime from the gallery</span></span>
<span data-ttu-id="fab6c-124">Aby skonfigurować integrację usługi Azure AD ClickTime, należy dodać ClickTime z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="fab6c-124">To configure the integration of ClickTime into Azure AD, you need to add ClickTime from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="fab6c-125">**Aby dodać ClickTime z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="fab6c-125">**To add ClickTime from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="fab6c-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="fab6c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Przycisk usługi Azure Active Directory][1]

2. <span data-ttu-id="fab6c-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="fab6c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="fab6c-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="fab6c-129">Then go to **All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa][2]
    
3. <span data-ttu-id="fab6c-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="fab6c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Nowy przycisk aplikacji][3]

4. <span data-ttu-id="fab6c-133">W polu wyszukiwania wpisz **ClickTime**, wybierz pozycję **ClickTime** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="fab6c-133">In the search box, type **ClickTime**, select **ClickTime** from result panel then click **Add** button to add the application.</span></span>

    ![ClickTime na liście wyników](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="fab6c-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="fab6c-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="fab6c-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z ClickTime w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="fab6c-136">In this section, you configure and test Azure AD single sign-on with ClickTime based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fab6c-137">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w ClickTime jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fab6c-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ClickTime is to a user in Azure AD.</span></span> <span data-ttu-id="fab6c-138">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w ClickTime musi się.</span><span class="sxs-lookup"><span data-stu-id="fab6c-138">In other words, a link relationship between an Azure AD user and the related user in ClickTime needs to be established.</span></span>

<span data-ttu-id="fab6c-139">W ClickTime, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="fab6c-139">In ClickTime, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="fab6c-140">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z ClickTime, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="fab6c-140">To configure and test Azure AD single sign-on with ClickTime, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="fab6c-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="fab6c-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="fab6c-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="fab6c-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fab6c-143">**[Tworzenie użytkownika testowego ClickTime](#create-a-clicktime-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta ClickTime połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fab6c-143">**[Create a ClickTime test user](#create-a-clicktime-test-user)** - to have a counterpart of Britta Simon in ClickTime that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="fab6c-144">**[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="fab6c-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fab6c-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="fab6c-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="fab6c-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="fab6c-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="fab6c-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji ClickTime.</span><span class="sxs-lookup"><span data-stu-id="fab6c-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ClickTime application.</span></span>

<span data-ttu-id="fab6c-148">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z ClickTime, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="fab6c-148">**To configure Azure AD single sign-on with ClickTime, perform the following steps:**</span></span>

1. <span data-ttu-id="fab6c-149">W portalu Azure na **ClickTime** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="fab6c-149">In the Azure portal, on the **ClickTime** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="fab6c-151">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="fab6c-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_samlbase.png)

3. <span data-ttu-id="fab6c-153">Na **ClickTime domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="fab6c-153">On the **ClickTime Domain and URLs** section, perform the following steps:</span></span>

    ![Adresy URL i domeny ClickTime pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_url.png)

    <span data-ttu-id="fab6c-155">a.</span><span class="sxs-lookup"><span data-stu-id="fab6c-155">a.</span></span> <span data-ttu-id="fab6c-156">W **identyfikator** tekstowym, wpisz adres URL jako:`https://app.clicktime.com/sp/`</span><span class="sxs-lookup"><span data-stu-id="fab6c-156">In the **Identifier** textbox, type a URL as: `https://app.clicktime.com/sp/`</span></span>
    
    <span data-ttu-id="fab6c-157">b.</span><span class="sxs-lookup"><span data-stu-id="fab6c-157">b.</span></span> <span data-ttu-id="fab6c-158">W **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą następujących wzorców:</span><span class="sxs-lookup"><span data-stu-id="fab6c-158">In the **Reply URL** textbox, type a URL using the following patterns:</span></span> 

    | |
    |--|
    | `https://app.clicktime.com/Login/` |
    | `https://app.clicktime.com/App/Login/Consume.aspx` |

4. <span data-ttu-id="fab6c-159">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="fab6c-159">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Łącze pobierania certyfikatu](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_certificate.png) 

5. <span data-ttu-id="fab6c-161">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="fab6c-161">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-clicktime-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fab6c-163">Na **konfiguracji ClickTime** , kliknij przycisk **skonfigurować ClickTime** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="fab6c-163">On the **ClickTime Configuration** section, click **Configure ClickTime** to open **Configure sign-on** window.</span></span> <span data-ttu-id="fab6c-164">Kopiuj **SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="fab6c-164">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfiguracja ClickTime](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_configure.png) 

7. <span data-ttu-id="fab6c-166">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy ClickTime jako administrator.</span><span class="sxs-lookup"><span data-stu-id="fab6c-166">In a different web browser window, log into your ClickTime company site as an administrator.</span></span>

8. <span data-ttu-id="fab6c-167">Na pasku narzędzi u góry kliknij **preferencje**, a następnie kliknij przycisk **ustawienia zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="fab6c-167">In the toolbar on the top, click **Preferences**, and then click **Security Settings**.</span></span>

9. <span data-ttu-id="fab6c-168">W **preferencje rejestracji jednokrotnej** konfiguracji sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="fab6c-168">In the **Single Sign-On Preferences** configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="fab6c-169">![Ustawienia zabezpieczeń](./media/active-directory-saas-clicktime-tutorial/tic777280.png "ustawienia zabezpieczeń")</span><span class="sxs-lookup"><span data-stu-id="fab6c-169">![Security Settings](./media/active-directory-saas-clicktime-tutorial/tic777280.png "Security Settings")</span></span>
   
    <span data-ttu-id="fab6c-170">a.</span><span class="sxs-lookup"><span data-stu-id="fab6c-170">a.</span></span>  <span data-ttu-id="fab6c-171">Wybierz **Zezwalaj** Zaloguj się przy użyciu pojedynczego logowania jednokrotnego (SSO) z **usługi Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="fab6c-171">Select **Allow** sign-in using Single Sign-On (SSO) with **Azure AD**.</span></span>
   
    <span data-ttu-id="fab6c-172">b.</span><span class="sxs-lookup"><span data-stu-id="fab6c-172">b.</span></span> <span data-ttu-id="fab6c-173">W **punktu końcowego dostawcy tożsamości** pole tekstowe, Wklej **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="fab6c-173">In the **Identity Provider Endpoint** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="fab6c-174">c.</span><span class="sxs-lookup"><span data-stu-id="fab6c-174">c.</span></span>  <span data-ttu-id="fab6c-175">Otwórz **certyfikatu algorytmem base-64** pobrany z portalu Azure w **Notatnik**, skopiuj zawartość, a następnie wklej go do **certyfikatu X.509** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="fab6c-175">Open the **base-64 encoded certificate** downloaded from Azure portal in **Notepad**, copy the content, and then paste it into the **X.509 Certificate** textbox.</span></span>
   
    <span data-ttu-id="fab6c-176">d.</span><span class="sxs-lookup"><span data-stu-id="fab6c-176">d.</span></span>  <span data-ttu-id="fab6c-177">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="fab6c-177">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="fab6c-178">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="fab6c-178">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="fab6c-179">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="fab6c-179">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="fab6c-180">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fab6c-180">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="fab6c-181">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="fab6c-181">Create an Azure AD test user</span></span>
<span data-ttu-id="fab6c-182">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="fab6c-182">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="fab6c-184">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="fab6c-184">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="fab6c-185">W portalu Azure, w okienku po lewej stronie kliknij **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="fab6c-185">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-clicktime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fab6c-187">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="fab6c-187">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>
    
    !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-clicktime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fab6c-189">Aby otworzyć **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** w górnej części **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="fab6c-189">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>
 
    ![Przycisk Dodaj](./media/active-directory-saas-clicktime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fab6c-191">W **użytkownika** okna dialogowego wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="fab6c-191">In the **User** dialog box, perform the following steps:</span></span>
 
    ![Okno dialogowe użytkownika](./media/active-directory-saas-clicktime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fab6c-193">a.</span><span class="sxs-lookup"><span data-stu-id="fab6c-193">a.</span></span> <span data-ttu-id="fab6c-194">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fab6c-194">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fab6c-195">b.</span><span class="sxs-lookup"><span data-stu-id="fab6c-195">b.</span></span> <span data-ttu-id="fab6c-196">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="fab6c-196">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fab6c-197">c.</span><span class="sxs-lookup"><span data-stu-id="fab6c-197">c.</span></span> <span data-ttu-id="fab6c-198">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="fab6c-198">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="fab6c-199">d.</span><span class="sxs-lookup"><span data-stu-id="fab6c-199">d.</span></span> <span data-ttu-id="fab6c-200">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="fab6c-200">Click **Create**.</span></span>
 
### <a name="create-a-clicktime-test-user"></a><span data-ttu-id="fab6c-201">Tworzenie użytkownika testowego ClickTime</span><span class="sxs-lookup"><span data-stu-id="fab6c-201">Create a ClickTime test user</span></span>

<span data-ttu-id="fab6c-202">Aby włączyć użytkowników usługi Azure AD zalogować się do ClickTime, musi być przygotowana do ClickTime.</span><span class="sxs-lookup"><span data-stu-id="fab6c-202">In order to enable Azure AD users to log into ClickTime, they must be provisioned into ClickTime.</span></span>  
<span data-ttu-id="fab6c-203">W przypadku ClickTime Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="fab6c-203">In the case of ClickTime, provisioning is a manual task.</span></span>

> [!NOTE]
> <span data-ttu-id="fab6c-204">Możesz użyć innych ClickTime użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez ClickTime do udostępnienia konta użytkownika usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fab6c-204">You can use any other ClickTime user account creation tools or APIs provided by ClickTime to provision Azure AD user accounts.</span></span>

<span data-ttu-id="fab6c-205">**Aby udostępnić konta użytkownika, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="fab6c-205">**To provision a user account, perform the following steps:**</span></span>
1. <span data-ttu-id="fab6c-206">Zaloguj się do Twojego **ClickTime** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="fab6c-206">Log in to your **ClickTime** tenant.</span></span>
2. <span data-ttu-id="fab6c-207">Na pasku narzędzi u góry kliknij **firmy**, a następnie kliknij przycisk **osób**.</span><span class="sxs-lookup"><span data-stu-id="fab6c-207">In the toolbar on the top, click **Company**, and then click **People**.</span></span>
   
    <span data-ttu-id="fab6c-208">![Osoby](./media/active-directory-saas-clicktime-tutorial/tic777282.png "osób")</span><span class="sxs-lookup"><span data-stu-id="fab6c-208">![People](./media/active-directory-saas-clicktime-tutorial/tic777282.png "People")</span></span>
3. <span data-ttu-id="fab6c-209">Kliknij przycisk **Dodaj osobę**.</span><span class="sxs-lookup"><span data-stu-id="fab6c-209">Click **Add Person**.</span></span>
   
    <span data-ttu-id="fab6c-210">![Dodaj osobę](./media/active-directory-saas-clicktime-tutorial/tic777283.png "Dodaj osobę")</span><span class="sxs-lookup"><span data-stu-id="fab6c-210">![Add Person](./media/active-directory-saas-clicktime-tutorial/tic777283.png "Add Person")</span></span>
4. <span data-ttu-id="fab6c-211">W sekcji nowej osoby wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="fab6c-211">In the New Person section, perform the following steps:</span></span>
   
    <span data-ttu-id="fab6c-212">![Osoby](./media/active-directory-saas-clicktime-tutorial/tic777284.png "osób")</span><span class="sxs-lookup"><span data-stu-id="fab6c-212">![People](./media/active-directory-saas-clicktime-tutorial/tic777284.png "People")</span></span>
   
    <span data-ttu-id="fab6c-213">a.</span><span class="sxs-lookup"><span data-stu-id="fab6c-213">a.</span></span>  <span data-ttu-id="fab6c-214">W **Pełna nazwa** pole tekstowe, typ Pełna nazwa użytkownika, takich jak **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="fab6c-214">In the **full name** textbox, type full name of user like **Britta Simon**.</span></span> 
  
    <span data-ttu-id="fab6c-215">b.</span><span class="sxs-lookup"><span data-stu-id="fab6c-215">b.</span></span>  <span data-ttu-id="fab6c-216">W **adres e-mail** tekstowym, wpisz adres e-mail użytkownika, takich jak  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="fab6c-216">In the **email address** textbox, type the email of user like **brittasimon@contoso.com**.</span></span>
       
    > [!NOTE]
    > <span data-ttu-id="fab6c-217">Jeśli chcesz, można ustawić dodatkowe właściwości dla nowego obiektu osoby.</span><span class="sxs-lookup"><span data-stu-id="fab6c-217">If you want to, you can set additional properties of the new person object.</span></span>
   
    <span data-ttu-id="fab6c-218">c.</span><span class="sxs-lookup"><span data-stu-id="fab6c-218">c.</span></span>  <span data-ttu-id="fab6c-219">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="fab6c-219">Click **Save**.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="fab6c-220">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="fab6c-220">Assign the Azure AD test user</span></span>

<span data-ttu-id="fab6c-221">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu ClickTime.</span><span class="sxs-lookup"><span data-stu-id="fab6c-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ClickTime.</span></span>

![Przypisanie roli użytkownika][200] 

<span data-ttu-id="fab6c-223">**Aby przypisać Simona Britta ClickTime, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="fab6c-223">**To assign Britta Simon to ClickTime, perform the following steps:**</span></span>

1. <span data-ttu-id="fab6c-224">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="fab6c-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="fab6c-226">Na liście aplikacji zaznacz **ClickTime**.</span><span class="sxs-lookup"><span data-stu-id="fab6c-226">In the applications list, select **ClickTime**.</span></span>

    ![Łącze ClickTimne na liście aplikacji](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_app.png) 

3. <span data-ttu-id="fab6c-228">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="fab6c-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Łącze "Użytkownicy i grupy"][202] 

4. <span data-ttu-id="fab6c-230">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="fab6c-230">Click **Add** button.</span></span> <span data-ttu-id="fab6c-231">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="fab6c-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![W okienku Dodaj przydziału][203]

5. <span data-ttu-id="fab6c-233">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="fab6c-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="fab6c-234">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="fab6c-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fab6c-235">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="fab6c-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="fab6c-236">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="fab6c-236">Test single sign-on</span></span>

<span data-ttu-id="fab6c-237">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="fab6c-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="fab6c-238">Po kliknięciu kafelka ClickTime w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji ClickTime.</span><span class="sxs-lookup"><span data-stu-id="fab6c-238">When you click the ClickTime tile in the Access Panel, you should get automatically signed-on to your ClickTime application.</span></span>
<span data-ttu-id="fab6c-239">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fab6c-239">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fab6c-240">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="fab6c-240">Additional resources</span></span>

* [<span data-ttu-id="fab6c-241">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fab6c-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fab6c-242">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fab6c-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_203.png

