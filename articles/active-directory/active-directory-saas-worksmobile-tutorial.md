---
title: "Samouczek: Integracji usługi Azure Active Directory z WORKS MOBILE | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługi Azure Active Directory i działa MOBILE."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 725f32fd-d0ad-49c7-b137-1cc246bf85d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 139a1968a59424eae278de3e7fa227ad340a1eb8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-works-mobile"></a><span data-ttu-id="57cc4-103">Samouczek: Integracji Azure Active Directory z MOBILE działania</span><span class="sxs-lookup"><span data-stu-id="57cc4-103">Tutorial: Azure Active Directory integration with WORKS MOBILE</span></span>

<span data-ttu-id="57cc4-104">Z tego samouczka dowiesz się integrowanie MOBILE WSPÓŁPRACUJE z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="57cc4-104">In this tutorial, you learn how to integrate WORKS MOBILE with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="57cc4-105">Integrowanie MOBILE WSPÓŁPRACUJE z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="57cc4-105">Integrating WORKS MOBILE with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="57cc4-106">Można kontrolować w usłudze Azure AD, który ma dostęp do MOBILNEJ działa</span><span class="sxs-lookup"><span data-stu-id="57cc4-106">You can control in Azure AD who has access to WORKS MOBILE</span></span>
- <span data-ttu-id="57cc4-107">Umożliwia użytkownikom automatycznie pobrać zalogowane powyżej WORKS (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="57cc4-107">You can enable your users to automatically get signed-on to WORKS MOBILE (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="57cc4-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="57cc4-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="57cc4-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="57cc4-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="57cc4-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="57cc4-110">Prerequisites</span></span>

<span data-ttu-id="57cc4-111">Aby skonfigurować integrację usługi Azure AD z MOBILE WSPÓŁPRACUJE, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="57cc4-111">To configure Azure AD integration with WORKS MOBILE, you need the following items:</span></span>

- <span data-ttu-id="57cc4-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="57cc4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="57cc4-113">MOBILE działa logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="57cc4-113">A WORKS MOBILE single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="57cc4-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="57cc4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="57cc4-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="57cc4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="57cc4-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="57cc4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="57cc4-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="57cc4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="57cc4-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="57cc4-118">Scenario description</span></span>
<span data-ttu-id="57cc4-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="57cc4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="57cc4-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="57cc4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="57cc4-121">Dodawanie MOBILE WSPÓŁPRACUJE z galerii</span><span class="sxs-lookup"><span data-stu-id="57cc4-121">Adding WORKS MOBILE from the gallery</span></span>
2. <span data-ttu-id="57cc4-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="57cc4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-works-mobile-from-the-gallery"></a><span data-ttu-id="57cc4-123">Dodawanie MOBILE WSPÓŁPRACUJE z galerii</span><span class="sxs-lookup"><span data-stu-id="57cc4-123">Adding WORKS MOBILE from the gallery</span></span>
<span data-ttu-id="57cc4-124">Aby skonfigurować integrację MOBILE WSPÓŁPRACUJE z usługą Azure AD, należy dodać MOBILE WSPÓŁPRACUJE z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="57cc4-124">To configure the integration of WORKS MOBILE into Azure AD, you need to add WORKS MOBILE from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="57cc4-125">**Aby dodać MOBILE WSPÓŁPRACUJE z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="57cc4-125">**To add WORKS MOBILE from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="57cc4-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="57cc4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="57cc4-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="57cc4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="57cc4-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="57cc4-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="57cc4-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="57cc4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="57cc4-133">W polu wyszukiwania wpisz **MOBILE WSPÓŁPRACUJE**.</span><span class="sxs-lookup"><span data-stu-id="57cc4-133">In the search box, type **WORKS MOBILE**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_search.png)

5. <span data-ttu-id="57cc4-135">W panelu wyników wybierz **MOBILE WSPÓŁPRACUJE**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="57cc4-135">In the results panel, select **WORKS MOBILE**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="57cc4-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="57cc4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="57cc4-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z MOBILE działa na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="57cc4-138">In this section, you configure and test Azure AD single sign-on with WORKS MOBILE based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="57cc4-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w MOBILE WSPÓŁPRACUJE jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="57cc4-139">For single sign-on to work, Azure AD needs to know what the counterpart user in WORKS MOBILE is to a user in Azure AD.</span></span> <span data-ttu-id="57cc4-140">Innymi słowy łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w MOBILE WSPÓŁPRACUJE musi się.</span><span class="sxs-lookup"><span data-stu-id="57cc4-140">In other words, a link relationship between an Azure AD user and the related user in WORKS MOBILE needs to be established.</span></span>

<span data-ttu-id="57cc4-141">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w MOBILE WSPÓŁPRACUJE.</span><span class="sxs-lookup"><span data-stu-id="57cc4-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in WORKS MOBILE.</span></span>

<span data-ttu-id="57cc4-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z MOBILE WSPÓŁPRACUJE, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="57cc4-142">To configure and test Azure AD single sign-on with WORKS MOBILE, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="57cc4-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="57cc4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="57cc4-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="57cc4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="57cc4-145">**[Tworzenie użytkownika testowego MOBILE WSPÓŁPRACUJE](#creating-a-works-mobile-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta MOBILE WSPÓŁPRACUJE, połączonej z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="57cc4-145">**[Creating a WORKS MOBILE test user](#creating-a-works-mobile-test-user)** - to have a counterpart of Britta Simon in WORKS MOBILE that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="57cc4-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="57cc4-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="57cc4-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="57cc4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="57cc4-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="57cc4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="57cc4-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji MOBILNEJ działa.</span><span class="sxs-lookup"><span data-stu-id="57cc4-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your WORKS MOBILE application.</span></span>

<span data-ttu-id="57cc4-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z MOBILE działa, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="57cc4-150">**To configure Azure AD single sign-on with WORKS MOBILE, perform the following steps:**</span></span>

1. <span data-ttu-id="57cc4-151">W portalu Azure na **MOBILE WSPÓŁPRACUJE** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="57cc4-151">In the Azure portal, on the **WORKS MOBILE** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="57cc4-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="57cc4-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_samlbase.png)

3. <span data-ttu-id="57cc4-155">Na **WORKS MOBILE domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="57cc4-155">On the **WORKS MOBILE Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_url.png)

    <span data-ttu-id="57cc4-157">a.</span><span class="sxs-lookup"><span data-stu-id="57cc4-157">a.</span></span> <span data-ttu-id="57cc4-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.worksmobile.com/jp/myservice`</span><span class="sxs-lookup"><span data-stu-id="57cc4-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.worksmobile.com/jp/myservice`</span></span>

    <span data-ttu-id="57cc4-159">b.</span><span class="sxs-lookup"><span data-stu-id="57cc4-159">b.</span></span> <span data-ttu-id="57cc4-160">W **identyfikator** tekstowym, wpisz wartość jako`worksmobile.com`</span><span class="sxs-lookup"><span data-stu-id="57cc4-160">In the **Identifier** textbox, type the value as `worksmobile.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="57cc4-161">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="57cc4-161">This value is not real.</span></span> <span data-ttu-id="57cc4-162">Zaktualizuj tę wartość przy rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="57cc4-162">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="57cc4-163">Skontaktuj się z [klienta MOBILE WSPÓŁPRACUJE z pomocą techniczną](mailto:dl_ssoinfo@worksmobile.com) aby zyskać tę wartość.</span><span class="sxs-lookup"><span data-stu-id="57cc4-163">Contact [WORKS MOBILE Client support team](mailto:dl_ssoinfo@worksmobile.com) to get this value.</span></span> 
 
4. <span data-ttu-id="57cc4-164">Na **certyfikat podpisywania SAML** kliknij **Certificate(Raw)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="57cc4-164">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_certificate.png) 

5. <span data-ttu-id="57cc4-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="57cc4-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-worksmobile-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="57cc4-168">Na **konfiguracji MOBILE WSPÓŁPRACUJE** kliknij **skonfigurować MOBILE WSPÓŁPRACUJE** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="57cc4-168">On the **WORKS MOBILE Configuration** section, click **Configure WORKS MOBILE** to open **Configure sign-on** window.</span></span> <span data-ttu-id="57cc4-169">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="57cc4-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_configure.png) 

7. <span data-ttu-id="57cc4-171">Aby uzyskać logowania jednokrotnego skonfigurowane dla aplikacji, skontaktuj się z [MOBILE WSPÓŁPRACUJE z pomocą techniczną](mailto:dl_ssoinfo@worksmobile.com) i podaj następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="57cc4-171">To get SSO configured for your application, contact [WORKS MOBILE support team](mailto:dl_ssoinfo@worksmobile.com) and provide them with the following information:</span></span> 

    <span data-ttu-id="57cc4-172">• Pobrany **plik certyfikatu**</span><span class="sxs-lookup"><span data-stu-id="57cc4-172">• The downloaded **Certificate file**</span></span>

    <span data-ttu-id="57cc4-173">• **Adres URL usługi rejestracji jednokrotnej SAML**</span><span class="sxs-lookup"><span data-stu-id="57cc4-173">• The **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="57cc4-174">• **Identyfikator jednostki SAML**</span><span class="sxs-lookup"><span data-stu-id="57cc4-174">• The **SAML Entity ID**</span></span>

    <span data-ttu-id="57cc4-175">• **Adresu URL wylogowania**</span><span class="sxs-lookup"><span data-stu-id="57cc4-175">• The **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="57cc4-176">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="57cc4-176">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="57cc4-177">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="57cc4-177">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="57cc4-178">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="57cc4-178">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="57cc4-179">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="57cc4-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="57cc4-180">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="57cc4-180">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="57cc4-182">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="57cc4-182">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="57cc4-183">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="57cc4-183">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="57cc4-185">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="57cc4-185">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="57cc4-187">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="57cc4-187">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="57cc4-189">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="57cc4-189">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="57cc4-191">a.</span><span class="sxs-lookup"><span data-stu-id="57cc4-191">a.</span></span> <span data-ttu-id="57cc4-192">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="57cc4-192">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="57cc4-193">b.</span><span class="sxs-lookup"><span data-stu-id="57cc4-193">b.</span></span> <span data-ttu-id="57cc4-194">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="57cc4-194">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="57cc4-195">c.</span><span class="sxs-lookup"><span data-stu-id="57cc4-195">c.</span></span> <span data-ttu-id="57cc4-196">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="57cc4-196">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="57cc4-197">d.</span><span class="sxs-lookup"><span data-stu-id="57cc4-197">d.</span></span> <span data-ttu-id="57cc4-198">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="57cc4-198">Click **Create**.</span></span>
 
### <a name="creating-a-works-mobile-test-user"></a><span data-ttu-id="57cc4-199">Tworzenie użytkownika testowego MOBILE działania</span><span class="sxs-lookup"><span data-stu-id="57cc4-199">Creating a WORKS MOBILE test user</span></span>

 <span data-ttu-id="57cc4-200">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w przenośnych działa.</span><span class="sxs-lookup"><span data-stu-id="57cc4-200">In this section, you create a user called Britta Simon in WORKS MOBILE.</span></span> <span data-ttu-id="57cc4-201">We współpracy z [MOBILE WSPÓŁPRACUJE z pomocą techniczną](mailto:dl_ssoinfo@worksmobile.com) Aby dodać użytkowników do platformy MOBILE działa.</span><span class="sxs-lookup"><span data-stu-id="57cc4-201">Please work with [WORKS MOBILE support team](mailto:dl_ssoinfo@worksmobile.com) to add the users in the WORKS MOBILE platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="57cc4-202">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="57cc4-202">Assigning the Azure AD test user</span></span>

<span data-ttu-id="57cc4-203">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do działania MOBILE.</span><span class="sxs-lookup"><span data-stu-id="57cc4-203">In this section, you enable Britta Simon to use Azure single sign-on by granting access to WORKS MOBILE.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="57cc4-205">**Aby przypisać Simona Britta MOBILE działa, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="57cc4-205">**To assign Britta Simon to WORKS MOBILE, perform the following steps:**</span></span>

1. <span data-ttu-id="57cc4-206">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="57cc4-206">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="57cc4-208">Na liście aplikacji zaznacz **MOBILE WSPÓŁPRACUJE**.</span><span class="sxs-lookup"><span data-stu-id="57cc4-208">In the applications list, select **WORKS MOBILE**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_app.png) 

3. <span data-ttu-id="57cc4-210">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="57cc4-210">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="57cc4-212">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="57cc4-212">Click **Add** button.</span></span> <span data-ttu-id="57cc4-213">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="57cc4-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="57cc4-215">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="57cc4-215">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="57cc4-216">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="57cc4-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="57cc4-217">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="57cc4-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="57cc4-218">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="57cc4-218">Testing single sign-on</span></span>

<span data-ttu-id="57cc4-219">W tej sekcji można przetestować konfigurację usługi Azure AD z logowania jednokrotnego za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="57cc4-219">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="57cc4-220">Po kliknięciu kafelka MOBILE WSPÓŁPRACUJE w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji MOBILE WSPÓŁPRACUJE.</span><span class="sxs-lookup"><span data-stu-id="57cc4-220">When you click the WORKS MOBILE tile in the Access Panel, you should get automatically signed-on to your WORKS MOBILE application.</span></span>
<span data-ttu-id="57cc4-221">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="57cc4-221">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="57cc4-222">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="57cc4-222">Additional resources</span></span>

* [<span data-ttu-id="57cc4-223">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="57cc4-223">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="57cc4-224">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="57cc4-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_203.png

