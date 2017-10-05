---
title: 'Samouczek: Integracji Azure Active Directory z Aravo | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Aravo."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 224939d8-2c9c-4561-968d-62722f5ab5ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 2b6da25a22463619180f635954660e6efeef62ce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-aravo"></a><span data-ttu-id="e16f9-103">Samouczek: Integracji Azure Active Directory z Aravo</span><span class="sxs-lookup"><span data-stu-id="e16f9-103">Tutorial: Azure Active Directory integration with Aravo</span></span>

<span data-ttu-id="e16f9-104">Z tego samouczka dowiesz się integrowanie Aravo z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e16f9-104">In this tutorial, you learn how to integrate Aravo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e16f9-105">Integracja z usługą Azure AD Aravo zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="e16f9-105">Integrating Aravo with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e16f9-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Aravo</span><span class="sxs-lookup"><span data-stu-id="e16f9-106">You can control in Azure AD who has access to Aravo</span></span>
- <span data-ttu-id="e16f9-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Aravo (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e16f9-107">You can enable your users to automatically get signed-on to Aravo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e16f9-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="e16f9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e16f9-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e16f9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e16f9-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e16f9-110">Prerequisites</span></span>

<span data-ttu-id="e16f9-111">Aby skonfigurować integrację usługi Azure AD z Aravo, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="e16f9-111">To configure Azure AD integration with Aravo, you need the following items:</span></span>

- <span data-ttu-id="e16f9-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e16f9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e16f9-113">Aravo jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="e16f9-113">An Aravo single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e16f9-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="e16f9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e16f9-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="e16f9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e16f9-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="e16f9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e16f9-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e16f9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e16f9-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="e16f9-118">Scenario description</span></span>
<span data-ttu-id="e16f9-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="e16f9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e16f9-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="e16f9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e16f9-121">Dodawanie Aravo z galerii</span><span class="sxs-lookup"><span data-stu-id="e16f9-121">Adding Aravo from the gallery</span></span>
2. <span data-ttu-id="e16f9-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="e16f9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-aravo-from-the-gallery"></a><span data-ttu-id="e16f9-123">Dodawanie Aravo z galerii</span><span class="sxs-lookup"><span data-stu-id="e16f9-123">Adding Aravo from the gallery</span></span>
<span data-ttu-id="e16f9-124">Aby skonfigurować integrację usługi Azure AD Aravo, należy dodać Aravo z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="e16f9-124">To configure the integration of Aravo into Azure AD, you need to add Aravo from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e16f9-125">**Aby dodać Aravo z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="e16f9-125">**To add Aravo from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e16f9-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="e16f9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="e16f9-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="e16f9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e16f9-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="e16f9-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="e16f9-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e16f9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="e16f9-133">W polu wyszukiwania wpisz **Aravo**.</span><span class="sxs-lookup"><span data-stu-id="e16f9-133">In the search box, type **Aravo**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-aravo-tutorial/tutorial_aravo_search.png)

5. <span data-ttu-id="e16f9-135">W panelu wyników wybierz **Aravo**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="e16f9-135">In the results panel, select **Aravo**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-aravo-tutorial/tutorial_aravo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e16f9-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="e16f9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e16f9-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Aravo na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="e16f9-138">In this section, you configure and test Azure AD single sign-on with Aravo based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e16f9-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Aravo jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e16f9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Aravo is to a user in Azure AD.</span></span> <span data-ttu-id="e16f9-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Aravo musi się.</span><span class="sxs-lookup"><span data-stu-id="e16f9-140">In other words, a link relationship between an Azure AD user and the related user in Aravo needs to be established.</span></span>

<span data-ttu-id="e16f9-141">W Aravo, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="e16f9-141">In Aravo, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e16f9-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Aravo, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="e16f9-142">To configure and test Azure AD single sign-on with Aravo, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e16f9-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="e16f9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e16f9-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="e16f9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e16f9-145">**[Tworzenie użytkownika testowego Aravo](#creating-an-aravo-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Aravo połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e16f9-145">**[Creating an Aravo test user](#creating-an-aravo-test-user)** - to have a counterpart of Britta Simon in Aravo that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e16f9-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="e16f9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e16f9-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="e16f9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e16f9-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e16f9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e16f9-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Aravo.</span><span class="sxs-lookup"><span data-stu-id="e16f9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Aravo application.</span></span>

<span data-ttu-id="e16f9-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Aravo, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="e16f9-150">**To configure Azure AD single sign-on with Aravo, perform the following steps:**</span></span>

1. <span data-ttu-id="e16f9-151">W portalu Azure na **Aravo** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="e16f9-151">In the Azure portal, on the **Aravo** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="e16f9-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="e16f9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-aravo-tutorial/tutorial_aravo_samlbase.png)

3. <span data-ttu-id="e16f9-155">Na **Aravo domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="e16f9-155">On the **Aravo Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-aravo-tutorial/tutorial_aravo_url.png)

    <span data-ttu-id="e16f9-157">a.</span><span class="sxs-lookup"><span data-stu-id="e16f9-157">a.</span></span> <span data-ttu-id="e16f9-158">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.aravo.com`</span><span class="sxs-lookup"><span data-stu-id="e16f9-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.aravo.com`</span></span>

    <span data-ttu-id="e16f9-159">b.</span><span class="sxs-lookup"><span data-stu-id="e16f9-159">b.</span></span> <span data-ttu-id="e16f9-160">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.aravo.com/aems/login.do`</span><span class="sxs-lookup"><span data-stu-id="e16f9-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.aravo.com/aems/login.do`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e16f9-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="e16f9-161">These values are not real.</span></span> <span data-ttu-id="e16f9-162">Rzeczywisty identyfikator i adres URL odpowiedzi, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="e16f9-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="e16f9-163">Skontaktuj się z [zespołem pomocy technicznej Aravo](http://www.aravo.com/about-us/contact/) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="e16f9-163">Contact [Aravo support team](http://www.aravo.com/about-us/contact/) to get these values.</span></span>
 
4. <span data-ttu-id="e16f9-164">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="e16f9-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-aravo-tutorial/tutorial_aravo_certificate.png) 

5. <span data-ttu-id="e16f9-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e16f9-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-aravo-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e16f9-168">Na **konfiguracji Aravo** , kliknij przycisk **skonfigurować Aravo** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="e16f9-168">On the **Aravo Configuration** section, click **Configure Aravo** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e16f9-169">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="e16f9-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-aravo-tutorial/tutorial_aravo_configure.png) 

7. <span data-ttu-id="e16f9-171">Do konfigurowania rejestracji jednokrotnej na **Aravo** stronie, musisz wysłać pobrany **certyfikatu (Base64)**, **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** Aby [zespołem pomocy technicznej Aravo](http://www.aravo.com/about-us/contact/).</span><span class="sxs-lookup"><span data-stu-id="e16f9-171">To configure single sign-on on **Aravo** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Aravo support team](http://www.aravo.com/about-us/contact/).</span></span> 


> [!TIP]
> <span data-ttu-id="e16f9-172">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="e16f9-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e16f9-173">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="e16f9-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e16f9-174">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e16f9-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e16f9-175">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e16f9-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="e16f9-176">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="e16f9-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="e16f9-178">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="e16f9-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e16f9-179">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="e16f9-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-aravo-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e16f9-181">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="e16f9-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-aravo-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e16f9-183">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e16f9-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-aravo-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e16f9-185">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="e16f9-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-aravo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e16f9-187">a.</span><span class="sxs-lookup"><span data-stu-id="e16f9-187">a.</span></span> <span data-ttu-id="e16f9-188">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e16f9-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e16f9-189">b.</span><span class="sxs-lookup"><span data-stu-id="e16f9-189">b.</span></span> <span data-ttu-id="e16f9-190">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e16f9-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e16f9-191">c.</span><span class="sxs-lookup"><span data-stu-id="e16f9-191">c.</span></span> <span data-ttu-id="e16f9-192">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="e16f9-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e16f9-193">d.</span><span class="sxs-lookup"><span data-stu-id="e16f9-193">d.</span></span> <span data-ttu-id="e16f9-194">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="e16f9-194">Click **Create**.</span></span>
 
### <a name="creating-an-aravo-test-user"></a><span data-ttu-id="e16f9-195">Tworzenie użytkownika testowego Aravo</span><span class="sxs-lookup"><span data-stu-id="e16f9-195">Creating an Aravo test user</span></span>

<span data-ttu-id="e16f9-196">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w Aravo.</span><span class="sxs-lookup"><span data-stu-id="e16f9-196">The objective of this section is to create a user called Britta Simon in Aravo.</span></span> <span data-ttu-id="e16f9-197">Praca z [zespołem pomocy technicznej Aravo](http://www.aravo.com/about-us/contact/) Aby dodać użytkowników w ramach konta Aravo.</span><span class="sxs-lookup"><span data-stu-id="e16f9-197">Work with [Aravo support team](http://www.aravo.com/about-us/contact/) to add the users in the Aravo account.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e16f9-198">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e16f9-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e16f9-199">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Aravo.</span><span class="sxs-lookup"><span data-stu-id="e16f9-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Aravo.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="e16f9-201">**Aby przypisać Simona Britta Aravo, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="e16f9-201">**To assign Britta Simon to Aravo, perform the following steps:**</span></span>

1. <span data-ttu-id="e16f9-202">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="e16f9-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="e16f9-204">Na liście aplikacji zaznacz **Aravo**.</span><span class="sxs-lookup"><span data-stu-id="e16f9-204">In the applications list, select **Aravo**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-aravo-tutorial/tutorial_aravo_app.png) 

3. <span data-ttu-id="e16f9-206">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="e16f9-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="e16f9-208">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e16f9-208">Click **Add** button.</span></span> <span data-ttu-id="e16f9-209">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e16f9-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="e16f9-211">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="e16f9-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e16f9-212">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e16f9-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e16f9-213">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e16f9-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e16f9-214">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e16f9-214">Testing single sign-on</span></span>

<span data-ttu-id="e16f9-215">Celem tej sekcji służy do testowania usługi Microsoft Azure AD rejestracji jednokrotnej konfigurację za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="e16f9-215">The objective of this section is to test your Microsoft Azure AD Single Sign-On configuration using the Access Panel.</span></span>

<span data-ttu-id="e16f9-216">Po kliknięciu kafelka Aravo w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Aravo.</span><span class="sxs-lookup"><span data-stu-id="e16f9-216">When you click the Aravo tile in the Access Panel, you should get automatically signed-on to your Aravo application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e16f9-217">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="e16f9-217">Additional resources</span></span>

* [<span data-ttu-id="e16f9-218">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e16f9-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e16f9-219">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e16f9-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_203.png

