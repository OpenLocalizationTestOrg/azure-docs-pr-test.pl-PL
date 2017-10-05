---
title: 'Samouczek: Integracji Azure Active Directory z Optimizely | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Optimizely."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28ef03e1-9aad-4301-af97-d94e853edc74
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 4d6f6da6bace09fbd6ab105530a1162653675c99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-optimizely"></a><span data-ttu-id="6daa0-103">Samouczek: Integracji Azure Active Directory z Optimizely</span><span class="sxs-lookup"><span data-stu-id="6daa0-103">Tutorial: Azure Active Directory integration with Optimizely</span></span>

<span data-ttu-id="6daa0-104">Z tego samouczka dowiesz się integrowanie Optimizely z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6daa0-104">In this tutorial, you learn how to integrate Optimizely with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6daa0-105">Integracja z usługą Azure AD Optimizely zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="6daa0-105">Integrating Optimizely with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6daa0-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Optimizely</span><span class="sxs-lookup"><span data-stu-id="6daa0-106">You can control in Azure AD who has access to Optimizely</span></span>
- <span data-ttu-id="6daa0-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Optimizely (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6daa0-107">You can enable your users to automatically get signed-on to Optimizely (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6daa0-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="6daa0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6daa0-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6daa0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6daa0-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6daa0-110">Prerequisites</span></span>

<span data-ttu-id="6daa0-111">Aby skonfigurować integrację usługi Azure AD z Optimizely, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="6daa0-111">To configure Azure AD integration with Optimizely, you need the following items:</span></span>

- <span data-ttu-id="6daa0-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6daa0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6daa0-113">Optimizely logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="6daa0-113">An Optimizely single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6daa0-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="6daa0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6daa0-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="6daa0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6daa0-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="6daa0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6daa0-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6daa0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6daa0-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="6daa0-118">Scenario description</span></span>
<span data-ttu-id="6daa0-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="6daa0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6daa0-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="6daa0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6daa0-121">Dodawanie Optimizely z galerii</span><span class="sxs-lookup"><span data-stu-id="6daa0-121">Adding Optimizely from the gallery</span></span>
2. <span data-ttu-id="6daa0-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="6daa0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-optimizely-from-the-gallery"></a><span data-ttu-id="6daa0-123">Dodawanie Optimizely z galerii</span><span class="sxs-lookup"><span data-stu-id="6daa0-123">Adding Optimizely from the gallery</span></span>
<span data-ttu-id="6daa0-124">Aby skonfigurować integrację usługi Azure AD Optimizely, należy dodać Optimizely z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="6daa0-124">To configure the integration of Optimizely into Azure AD, you need to add Optimizely from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6daa0-125">**Aby dodać Optimizely z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="6daa0-125">**To add Optimizely from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6daa0-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="6daa0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="6daa0-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="6daa0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6daa0-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="6daa0-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="6daa0-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6daa0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="6daa0-133">W polu wyszukiwania wpisz **Optimizely**.</span><span class="sxs-lookup"><span data-stu-id="6daa0-133">In the search box, type **Optimizely**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_search.png)

5. <span data-ttu-id="6daa0-135">W panelu wyników wybierz **Optimizely**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="6daa0-135">In the results panel, select **Optimizely**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6daa0-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="6daa0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6daa0-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Optimizely na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="6daa0-138">In this section, you configure and test Azure AD single sign-on with Optimizely based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6daa0-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Optimizely jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6daa0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Optimizely is to a user in Azure AD.</span></span> <span data-ttu-id="6daa0-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Optimizely musi się.</span><span class="sxs-lookup"><span data-stu-id="6daa0-140">In other words, a link relationship between an Azure AD user and the related user in Optimizely needs to be established.</span></span>

<span data-ttu-id="6daa0-141">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w Optimizely.</span><span class="sxs-lookup"><span data-stu-id="6daa0-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Optimizely.</span></span>

<span data-ttu-id="6daa0-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Optimizely, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="6daa0-142">To configure and test Azure AD single sign-on with Optimizely, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6daa0-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="6daa0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6daa0-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="6daa0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6daa0-145">**[Tworzenie użytkownika testowego Optimizely](#creating-an-optimizely-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Optimizely połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6daa0-145">**[Creating an Optimizely test user](#creating-an-optimizely-test-user)** - to have a counterpart of Britta Simon in Optimizely that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6daa0-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="6daa0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6daa0-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="6daa0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6daa0-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="6daa0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6daa0-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Optimizely.</span><span class="sxs-lookup"><span data-stu-id="6daa0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Optimizely application.</span></span>

<span data-ttu-id="6daa0-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Optimizely, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="6daa0-150">**To configure Azure AD single sign-on with Optimizely, perform the following steps:**</span></span>

1. <span data-ttu-id="6daa0-151">W portalu Azure na **Optimizely** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="6daa0-151">In the Azure portal, on the **Optimizely** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="6daa0-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="6daa0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_samlbase.png)

3. <span data-ttu-id="6daa0-155">Na **Optimizely domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6daa0-155">On the **Optimizely Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_url.png)

    <span data-ttu-id="6daa0-157">a.</span><span class="sxs-lookup"><span data-stu-id="6daa0-157">a.</span></span> <span data-ttu-id="6daa0-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://app.optimizely.net/<instance name>`</span><span class="sxs-lookup"><span data-stu-id="6daa0-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://app.optimizely.net/<instance name>`</span></span>

    <span data-ttu-id="6daa0-159">b.</span><span class="sxs-lookup"><span data-stu-id="6daa0-159">b.</span></span> <span data-ttu-id="6daa0-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`urn:auth0:optimizely:contoso`</span><span class="sxs-lookup"><span data-stu-id="6daa0-160">In the **Identifier** textbox, type a URL using the following pattern:  `urn:auth0:optimizely:contoso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6daa0-161">Wartości te nie są rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="6daa0-161">These values are not the real.</span></span> <span data-ttu-id="6daa0-162">Rzeczywisty adres URL logowania i identyfikator, który znajduje się w dalszej części samouczka spowoduje zaktualizowanie wartości.</span><span class="sxs-lookup"><span data-stu-id="6daa0-162">You will update the value with the actual Sign-on URL and Identifier, which is explained later in the tutorial.</span></span> 

4. <span data-ttu-id="6daa0-163">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="6daa0-163">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_certificate.png) 

5. <span data-ttu-id="6daa0-165">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6daa0-165">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-optimizely-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6daa0-167">Na **konfiguracji Optimizely** , kliknij przycisk **skonfigurować Optimizely** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="6daa0-167">On the **Optimizely Configuration** section, click **Configure Optimizely** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6daa0-168">Kopiuj **SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="6daa0-168">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_configure.png) 

7. <span data-ttu-id="6daa0-170">Aby skonfigurować logowanie jednokrotne w **Optimizely** po stronie, skontaktuj się z menedżerem ds. klientów Optimizely i zapewnić pobrany **certyfikatu (Base64)**, i **SAML pojedynczy znak na adres URL usługi**.</span><span class="sxs-lookup"><span data-stu-id="6daa0-170">To configure single sign-on on **Optimizely** side, contact your Optimizely Account Manager and provide the downloaded **Certificate (Base64)**, and **SAML Single Sign-On Service URL**.</span></span> 

8. <span data-ttu-id="6daa0-171">W odpowiedzi na adres e-mail Optimizely pozwala na adres URL logowania (SSO zainicjował SP) i wartości Identyfikator usługi dostawcy jednostki.</span><span class="sxs-lookup"><span data-stu-id="6daa0-171">In response to your email, Optimizely provides you with the Sign On URL (SP-initiated SSO) and the Identifier (Service Provider Entity ID) values.</span></span>

    <span data-ttu-id="6daa0-172">a.</span><span class="sxs-lookup"><span data-stu-id="6daa0-172">a.</span></span> <span data-ttu-id="6daa0-173">Kopia **inicjowane SP adres URL logowania jednokrotnego** o Optimizely i Wklej do **na adres URL logowania** textbox w **Optimizely domeny i adres URL** sekcji z portalu Azure</span><span class="sxs-lookup"><span data-stu-id="6daa0-173">Copy the **SP-initiated SSO URL** provided by Optimizely, and paste into the **Sign On URL** textbox in **Optimizely Domain and URLs** section on Azure portal</span></span> 

    <span data-ttu-id="6daa0-174">b.</span><span class="sxs-lookup"><span data-stu-id="6daa0-174">b.</span></span> <span data-ttu-id="6daa0-175">Kopiuj **identyfikator jednostki dostawcy usługi** o Optimizely i Wklej do **identyfikator** textbox w **Optimizely domeny i adres URL** sekcji z portalu Azure</span><span class="sxs-lookup"><span data-stu-id="6daa0-175">Copy the **Service Provider Entity ID** provided by Optimizely, and paste into the **Identifier** textbox in **Optimizely Domain and URLs** section on Azure portal</span></span> 

9. <span data-ttu-id="6daa0-176">W oknie innej przeglądarki logowanie do aplikacji Optimizely.</span><span class="sxs-lookup"><span data-stu-id="6daa0-176">In a different browser window, sign-on to your Optimizely application.</span></span>

10. <span data-ttu-id="6daa0-177">Kliknij możesz nazwa konta w górnym prawym narożniku, a następnie **ustawienia konta**.</span><span class="sxs-lookup"><span data-stu-id="6daa0-177">Click you account name in the top right corner and then **Account Settings**.</span></span>
   
    ![Azure AD rejestracji jednokrotnej](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_09.png)

11. <span data-ttu-id="6daa0-179">Zaznacz pole wyboru na karcie konto **włączenia logowania jednokrotnego** w obszarze rejestracji jednokrotnej w **omówienie** sekcji.</span><span class="sxs-lookup"><span data-stu-id="6daa0-179">In the Account tab, check the box **Enable SSO** under Single Sign On in the **Overview** section.</span></span>
   
    ![Azure AD rejestracji jednokrotnej](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_10.png)
    
12. <span data-ttu-id="6daa0-181">Kliknij przycisk **Zapisz**</span><span class="sxs-lookup"><span data-stu-id="6daa0-181">Click **Save**</span></span>

> [!TIP]
> <span data-ttu-id="6daa0-182">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="6daa0-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6daa0-183">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="6daa0-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6daa0-184">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6daa0-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6daa0-185">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6daa0-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="6daa0-186">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="6daa0-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="6daa0-188">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="6daa0-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6daa0-189">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="6daa0-189">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6daa0-191">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="6daa0-191">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6daa0-193">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6daa0-193">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6daa0-195">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6daa0-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6daa0-197">a.</span><span class="sxs-lookup"><span data-stu-id="6daa0-197">a.</span></span> <span data-ttu-id="6daa0-198">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6daa0-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6daa0-199">b.</span><span class="sxs-lookup"><span data-stu-id="6daa0-199">b.</span></span> <span data-ttu-id="6daa0-200">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="6daa0-200">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="6daa0-201">c.</span><span class="sxs-lookup"><span data-stu-id="6daa0-201">c.</span></span> <span data-ttu-id="6daa0-202">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="6daa0-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6daa0-203">d.</span><span class="sxs-lookup"><span data-stu-id="6daa0-203">d.</span></span> <span data-ttu-id="6daa0-204">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="6daa0-204">Click **Create**.</span></span>
 
### <a name="creating-an-optimizely-test-user"></a><span data-ttu-id="6daa0-205">Tworzenie użytkownika testowego Optimizely</span><span class="sxs-lookup"><span data-stu-id="6daa0-205">Creating an Optimizely test user</span></span>

<span data-ttu-id="6daa0-206">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Optimizely.</span><span class="sxs-lookup"><span data-stu-id="6daa0-206">In this section, you create a user called Britta Simon in Optimizely.</span></span>

1. <span data-ttu-id="6daa0-207">Na stronie głównej wybierz **współpracownicy** kartę.</span><span class="sxs-lookup"><span data-stu-id="6daa0-207">On the home page, select **Collaborators** tab.</span></span>

2. <span data-ttu-id="6daa0-208">Aby dodać nowy współpracownika do projektu, kliknij przycisk **nowego współpracownika**.</span><span class="sxs-lookup"><span data-stu-id="6daa0-208">To add new collaborator to the project, click **New Collaborator**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_10.png)

3. <span data-ttu-id="6daa0-210">Wprowadź adres e-mail i przydzielić mu rolę.</span><span class="sxs-lookup"><span data-stu-id="6daa0-210">Fill in the email address and assign them a role.</span></span> <span data-ttu-id="6daa0-211">Kliknij przycisk **zaprosić**.</span><span class="sxs-lookup"><span data-stu-id="6daa0-211">Click **Invite**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_11.png)

4. <span data-ttu-id="6daa0-213">Te otrzymają zaproszenie poczty e-mail.</span><span class="sxs-lookup"><span data-stu-id="6daa0-213">They receive an email invite.</span></span> <span data-ttu-id="6daa0-214">Przy użyciu adresu e-mail, muszą oni zalogować się do Optimizely.</span><span class="sxs-lookup"><span data-stu-id="6daa0-214">Using the email address, they have to log in to Optimizely.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6daa0-215">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6daa0-215">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6daa0-216">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Optimizely.</span><span class="sxs-lookup"><span data-stu-id="6daa0-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Optimizely.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="6daa0-218">**Aby przypisać Simona Britta Optimizely, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="6daa0-218">**To assign Britta Simon to Optimizely, perform the following steps:**</span></span>

1. <span data-ttu-id="6daa0-219">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="6daa0-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="6daa0-221">Na liście aplikacji zaznacz **Optimizely**.</span><span class="sxs-lookup"><span data-stu-id="6daa0-221">In the applications list, select **Optimizely**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_app.png) 

3. <span data-ttu-id="6daa0-223">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="6daa0-223">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="6daa0-225">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6daa0-225">Click **Add** button.</span></span> <span data-ttu-id="6daa0-226">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6daa0-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="6daa0-228">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="6daa0-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6daa0-229">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6daa0-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6daa0-230">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6daa0-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6daa0-231">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="6daa0-231">Testing single sign-on</span></span>

<span data-ttu-id="6daa0-232">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="6daa0-232">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6daa0-233">Po kliknięciu kafelka Optimizely w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Optimizely.</span><span class="sxs-lookup"><span data-stu-id="6daa0-233">When you click the Optimizely tile in the Access Panel, you should get automatically signed-on to your Optimizely application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6daa0-234">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="6daa0-234">Additional resources</span></span>

* [<span data-ttu-id="6daa0-235">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6daa0-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6daa0-236">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6daa0-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_203.png

