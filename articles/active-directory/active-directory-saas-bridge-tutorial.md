---
title: 'Samouczek: Integracji Azure Active Directory z Mostek | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Mostek."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3dbb6499-80c1-4d00-a0b4-e0ad5522cf0f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: d2b7fd6f73f1b782cfe6337d13f9f22f9c70d389
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bridge"></a><span data-ttu-id="bd4ff-103">Samouczek: Integracji Azure Active Directory z Mostek</span><span class="sxs-lookup"><span data-stu-id="bd4ff-103">Tutorial: Azure Active Directory integration with Bridge</span></span>

<span data-ttu-id="bd4ff-104">Z tego samouczka dowiesz się integrowanie mostek z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bd4ff-104">In this tutorial, you learn how to integrate Bridge with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bd4ff-105">Integrowanie mostek z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="bd4ff-105">Integrating Bridge with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="bd4ff-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Mostek</span><span class="sxs-lookup"><span data-stu-id="bd4ff-106">You can control in Azure AD who has access to Bridge</span></span>
- <span data-ttu-id="bd4ff-107">Umożliwia użytkownikom automatycznie pobrać zalogowane Mostek (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd4ff-107">You can enable your users to automatically get signed-on to Bridge (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bd4ff-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="bd4ff-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="bd4ff-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bd4ff-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bd4ff-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="bd4ff-110">Prerequisites</span></span>

<span data-ttu-id="bd4ff-111">Aby skonfigurować integrację usługi Azure AD z mostka, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="bd4ff-111">To configure Azure AD integration with Bridge, you need the following items:</span></span>

- <span data-ttu-id="bd4ff-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd4ff-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bd4ff-113">Mostek logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="bd4ff-113">A Bridge single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bd4ff-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bd4ff-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="bd4ff-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bd4ff-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bd4ff-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bd4ff-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bd4ff-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="bd4ff-118">Scenario description</span></span>
<span data-ttu-id="bd4ff-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bd4ff-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="bd4ff-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bd4ff-121">Dodawanie mostek z galerii</span><span class="sxs-lookup"><span data-stu-id="bd4ff-121">Adding Bridge from the gallery</span></span>
2. <span data-ttu-id="bd4ff-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="bd4ff-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bridge-from-the-gallery"></a><span data-ttu-id="bd4ff-123">Dodawanie mostek z galerii</span><span class="sxs-lookup"><span data-stu-id="bd4ff-123">Adding Bridge from the gallery</span></span>
<span data-ttu-id="bd4ff-124">Aby skonfigurować integrację usługi Azure AD mostek, należy dodać mostek z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-124">To configure the integration of Bridge into Azure AD, you need to add Bridge from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="bd4ff-125">**Aby dodać mostek z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="bd4ff-125">**To add Bridge from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="bd4ff-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="bd4ff-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="bd4ff-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="bd4ff-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="bd4ff-133">W polu wyszukiwania wpisz **Mostek**.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-133">In the search box, type **Bridge**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_search.png)

5. <span data-ttu-id="bd4ff-135">W panelu wyników wybierz **Mostek**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-135">In the results panel, select **Bridge**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bd4ff-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="bd4ff-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bd4ff-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Mostek oparte na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="bd4ff-138">In this section, you configure and test Azure AD single sign-on with Bridge based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="bd4ff-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednik w programie Bridge jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Bridge is to a user in Azure AD.</span></span> <span data-ttu-id="bd4ff-140">Innymi słowy łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Mostek musi się.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-140">In other words, a link relationship between an Azure AD user and the related user in Bridge needs to be established.</span></span>

<span data-ttu-id="bd4ff-141">Mostek, przypisywanie wartości **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-141">In Bridge, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="bd4ff-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z mostka, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="bd4ff-142">To configure and test Azure AD single sign-on with Bridge, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="bd4ff-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="bd4ff-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bd4ff-145">**[Tworzenie użytkownika testowego Mostek](#creating-a-bridge-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta mostek, który jest połączony z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-145">**[Creating a Bridge test user](#creating-a-bridge-test-user)** - to have a counterpart of Britta Simon in Bridge that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="bd4ff-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bd4ff-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bd4ff-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="bd4ff-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bd4ff-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji mostek.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Bridge application.</span></span>

<span data-ttu-id="bd4ff-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z mostka, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="bd4ff-150">**To configure Azure AD single sign-on with Bridge, perform the following steps:**</span></span>

1. <span data-ttu-id="bd4ff-151">W portalu Azure na **Mostek** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-151">In the Azure portal, on the **Bridge** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="bd4ff-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_samlbase.png)

3. <span data-ttu-id="bd4ff-155">Na **Mostek domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="bd4ff-155">On the **Bridge Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_url.png)

    <span data-ttu-id="bd4ff-157">a.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-157">a.</span></span> <span data-ttu-id="bd4ff-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<company name>.bridgeapp.com`</span><span class="sxs-lookup"><span data-stu-id="bd4ff-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.bridgeapp.com`</span></span>

    <span data-ttu-id="bd4ff-159">b.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-159">b.</span></span> <span data-ttu-id="bd4ff-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<company name>.bridgeapp.com`</span><span class="sxs-lookup"><span data-stu-id="bd4ff-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.bridgeapp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bd4ff-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-161">These values are not real.</span></span> <span data-ttu-id="bd4ff-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="bd4ff-163">Skontaktuj się z [zespołem pomocy technicznej klienta Mostek](https://community.bridgeapp.com/community/help) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-163">Contact [Bridge Client support team](https://community.bridgeapp.com/community/help) to get these values.</span></span> 
 
4. <span data-ttu-id="bd4ff-164">Na **certyfikat podpisywania SAML** kliknij **Certificate(Raw)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-164">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_certificate.png) 

5. <span data-ttu-id="bd4ff-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bridge-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bd4ff-168">Na **konfiguracji mostu** , kliknij przycisk **Mostek Konfiguruj** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-168">On the **Bridge Configuration** section, click **Configure Bridge** to open **Configure sign-on** window.</span></span> <span data-ttu-id="bd4ff-169">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="bd4ff-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_configure.png) 

7. <span data-ttu-id="bd4ff-171">Skonfigurować logowanie jednokrotne w **Mostek** stronie, musisz wysłać pobrany **Certificate(Raw)** i **identyfikator jednostki SAML, SAML pojedynczy znak na adres URL usługi i adres URL Sign-Out** do [zespołem pomocy technicznej Mostek](https://community.bridgeapp.com/community/help).</span><span class="sxs-lookup"><span data-stu-id="bd4ff-171">To configure single sign-on on **Bridge** side, you need to send the downloaded **Certificate(Raw)** and **SAML Entity ID, SAML Single Sign-On Service URL, and Sign-Out URL** to [Bridge support team](https://community.bridgeapp.com/community/help).</span></span> 

> [!TIP]
> <span data-ttu-id="bd4ff-172">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="bd4ff-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="bd4ff-173">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="bd4ff-174">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bd4ff-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bd4ff-175">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd4ff-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="bd4ff-176">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="bd4ff-178">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="bd4ff-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="bd4ff-179">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bridge-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bd4ff-181">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bridge-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bd4ff-183">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bridge-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bd4ff-185">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="bd4ff-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bridge-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bd4ff-187">a.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-187">a.</span></span> <span data-ttu-id="bd4ff-188">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bd4ff-189">b.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-189">b.</span></span> <span data-ttu-id="bd4ff-190">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bd4ff-191">c.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-191">c.</span></span> <span data-ttu-id="bd4ff-192">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="bd4ff-193">d.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-193">d.</span></span> <span data-ttu-id="bd4ff-194">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-194">Click **Create**.</span></span>
 
### <a name="creating-a-bridge-test-user"></a><span data-ttu-id="bd4ff-195">Tworzenie użytkownika testowego Mostek</span><span class="sxs-lookup"><span data-stu-id="bd4ff-195">Creating a Bridge test user</span></span>

<span data-ttu-id="bd4ff-196">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w mostek.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-196">In this section, you create a user called Britta Simon in Bridge.</span></span> <span data-ttu-id="bd4ff-197">Praca z [zespołem pomocy technicznej klienta Mostek](https://community.bridgeapp.com/community/help) do utworzenia użytkownika w platformie.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-197">Work with [Bridge Client support team](https://community.bridgeapp.com/community/help) to create a user in the platform.</span></span> <span data-ttu-id="bd4ff-198">Można zwiększyć biletu pomocy technicznej z mostu <a href="https://community.bridgeapp.com/community/help">tutaj</a> Aby dodać użytkowników do platformy mostek.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-198">You can raise the support ticket with Bridge from <a href="https://community.bridgeapp.com/community/help">here</a> to add the users in the Bridge platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="bd4ff-199">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd4ff-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="bd4ff-200">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do mostka.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Bridge.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="bd4ff-202">**Aby przypisać Simona Britta mostek, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="bd4ff-202">**To assign Britta Simon to Bridge, perform the following steps:**</span></span>

1. <span data-ttu-id="bd4ff-203">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="bd4ff-205">Na liście aplikacji zaznacz **Mostek**.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-205">In the applications list, select **Bridge**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_app.png) 

3. <span data-ttu-id="bd4ff-207">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="bd4ff-209">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-209">Click **Add** button.</span></span> <span data-ttu-id="bd4ff-210">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="bd4ff-212">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="bd4ff-213">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bd4ff-214">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bd4ff-215">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="bd4ff-215">Testing single sign-on</span></span>

<span data-ttu-id="bd4ff-216">W tej sekcji można przetestować konfigurację usługi Azure AD z logowania jednokrotnego za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-216">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="bd4ff-217">Po kliknięciu kafelka mostek w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji mostek.</span><span class="sxs-lookup"><span data-stu-id="bd4ff-217">When you click the Bridge tile in the Access Panel, you should get automatically signed-on to your Bridge application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bd4ff-218">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="bd4ff-218">Additional resources</span></span>

* [<span data-ttu-id="bd4ff-219">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bd4ff-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bd4ff-220">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bd4ff-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_203.png

