---
title: "Samouczek: Integracja usługi Azure Active Directory z usługą Ekspresyjne Online | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Ekspresyjne Online."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4fd6b29b-1b46-4fd1-9f5e-16b1c9d892cd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: d1abd3f8e2980e03fc092613183a261880fbce38
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bgs-online"></a><span data-ttu-id="f872f-103">Samouczek: Integracja usługi Azure Active Directory z usługą Ekspresyjne Online</span><span class="sxs-lookup"><span data-stu-id="f872f-103">Tutorial: Azure Active Directory integration with BGS Online</span></span>

<span data-ttu-id="f872f-104">Z tego samouczka dowiesz się integrowanie Ekspresyjne Online z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f872f-104">In this tutorial, you learn how to integrate BGS Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f872f-105">Integrowanie Ekspresyjne Online z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="f872f-105">Integrating BGS Online with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f872f-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Ekspresyjne Online</span><span class="sxs-lookup"><span data-stu-id="f872f-106">You can control in Azure AD who has access to BGS Online</span></span>
- <span data-ttu-id="f872f-107">Umożliwia użytkownikom automatycznie pobrać zalogowane Ekspresyjne online (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f872f-107">You can enable your users to automatically get signed-on to BGS Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f872f-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="f872f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f872f-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f872f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f872f-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f872f-110">Prerequisites</span></span>

<span data-ttu-id="f872f-111">Aby skonfigurować integrację usługi Azure AD z Ekspresyjne Online, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="f872f-111">To configure Azure AD integration with BGS Online, you need the following items:</span></span>

- <span data-ttu-id="f872f-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f872f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f872f-113">Ekspresyjne Online jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="f872f-113">A BGS Online single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f872f-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="f872f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f872f-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="f872f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f872f-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="f872f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f872f-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f872f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f872f-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="f872f-118">Scenario description</span></span>
<span data-ttu-id="f872f-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="f872f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f872f-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="f872f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f872f-121">Dodawanie Ekspresyjne Online z poziomu galerii</span><span class="sxs-lookup"><span data-stu-id="f872f-121">Adding BGS Online from the gallery</span></span>
2. <span data-ttu-id="f872f-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="f872f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bgs-online-from-the-gallery"></a><span data-ttu-id="f872f-123">Dodawanie Ekspresyjne Online z poziomu galerii</span><span class="sxs-lookup"><span data-stu-id="f872f-123">Adding BGS Online from the gallery</span></span>
<span data-ttu-id="f872f-124">Aby skonfigurować integrację Ekspresyjne online z usługą Azure AD, należy dodać do listy zarządzanych aplikacji SaaS Ekspresyjne Online z poziomu galerii.</span><span class="sxs-lookup"><span data-stu-id="f872f-124">To configure the integration of BGS Online into Azure AD, you need to add BGS Online from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f872f-125">**Aby dodać Ekspresyjne Online z poziomu galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f872f-125">**To add BGS Online from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f872f-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="f872f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="f872f-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="f872f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f872f-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="f872f-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="f872f-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f872f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="f872f-133">W polu wyszukiwania wpisz **Ekspresyjne Online**.</span><span class="sxs-lookup"><span data-stu-id="f872f-133">In the search box, type **BGS Online**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_search.png)

5. <span data-ttu-id="f872f-135">W panelu wyników wybierz **Ekspresyjne Online**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="f872f-135">In the results panel, select **BGS Online**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f872f-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="f872f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f872f-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej Ekspresyjne online na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="f872f-138">In this section, you configure and test Azure AD single sign-on with BGS Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f872f-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednikiem Ekspresyjne online jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f872f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BGS Online is to a user in Azure AD.</span></span> <span data-ttu-id="f872f-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i danemu użytkownikowi w trybie Online Ekspresyjne musi określone.</span><span class="sxs-lookup"><span data-stu-id="f872f-140">In other words, a link relationship between an Azure AD user and the related user in BGS Online needs to be established.</span></span>

<span data-ttu-id="f872f-141">W trybie Online Ekspresyjne przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="f872f-141">In BGS Online, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f872f-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Ekspresyjne Online, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="f872f-142">To configure and test Azure AD single sign-on with BGS Online, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f872f-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="f872f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f872f-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="f872f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f872f-145">**[Tworzenie użytkownika testowego Ekspresyjne Online](#creating-a-bgs-online-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Ekspresyjne Online, które jest połączone z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f872f-145">**[Creating a BGS Online test user](#creating-a-bgs-online-test-user)** - to have a counterpart of Britta Simon in BGS Online that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f872f-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="f872f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f872f-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="f872f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f872f-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="f872f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f872f-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w trybie Online Ekspresyjne aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f872f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BGS Online application.</span></span>

<span data-ttu-id="f872f-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Ekspresyjne Online, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f872f-150">**To configure Azure AD single sign-on with BGS Online, perform the following steps:**</span></span>

1. <span data-ttu-id="f872f-151">W portalu Azure na **Ekspresyjne Online** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="f872f-151">In the Azure portal, on the **BGS Online** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="f872f-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="f872f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_samlbase.png)

3. <span data-ttu-id="f872f-155">Na **Ekspresyjne Online domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f872f-155">On the **BGS Online Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_url.png)

    <span data-ttu-id="f872f-157">a.</span><span class="sxs-lookup"><span data-stu-id="f872f-157">a.</span></span> <span data-ttu-id="f872f-158">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="f872f-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>

    <span data-ttu-id="f872f-159">W środowisku produkcyjnym należy używać tego wzorca`https://<company name>.millwardbrown.report`</span><span class="sxs-lookup"><span data-stu-id="f872f-159">For production environment, use this pattern `https://<company name>.millwardbrown.report`</span></span> 

    <span data-ttu-id="f872f-160">Dla środowiska testowego Użyj tego wzorca`https://millwardbrown.marketingtracker.nl/mt5/`</span><span class="sxs-lookup"><span data-stu-id="f872f-160">For test environment, use this pattern `https://millwardbrown.marketingtracker.nl/mt5/`</span></span>

    <span data-ttu-id="f872f-161">b.</span><span class="sxs-lookup"><span data-stu-id="f872f-161">b.</span></span> <span data-ttu-id="f872f-162">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="f872f-162">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    
    <span data-ttu-id="f872f-163">W środowisku produkcyjnym należy używać tego wzorca`https://<company name>.millwardbrown.report/sso/saml/AssertionConsumerService.aspx`</span><span class="sxs-lookup"><span data-stu-id="f872f-163">For production environment, use this pattern `https://<company name>.millwardbrown.report/sso/saml/AssertionConsumerService.aspx`</span></span> 
      
    <span data-ttu-id="f872f-164">Dla środowiska testowego Użyj tego wzorca`https://millwardbrown.marketingtracker.nl/mt5/sso/saml/AssertionConsumerService.aspx`</span><span class="sxs-lookup"><span data-stu-id="f872f-164">For test environment, use this pattern `https://millwardbrown.marketingtracker.nl/mt5/sso/saml/AssertionConsumerService.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f872f-165">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="f872f-165">These values are not real.</span></span> <span data-ttu-id="f872f-166">Rzeczywisty identyfikator i adres URL odpowiedzi, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="f872f-166">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="f872f-167">Skontaktuj się z [zespół pomocy technicznej Online Ekspresyjne](mailTo:bgsdashboardteam@millwardbrown.com) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="f872f-167">Contact [BGS Online support team](mailTo:bgsdashboardteam@millwardbrown.com) to get these values.</span></span>
 

4. <span data-ttu-id="f872f-168">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="f872f-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_certificate.png) 

5. <span data-ttu-id="f872f-170">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f872f-170">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bgsonline-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f872f-172">Na **konfiguracji Online Ekspresyjne** , kliknij przycisk **skonfigurować Ekspresyjne Online** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="f872f-172">On the **BGS Online Configuration** section, click **Configure BGS Online** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f872f-173">Kopiuj **SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="f872f-173">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_configure.png) 

7. <span data-ttu-id="f872f-175">Do konfigurowania rejestracji jednokrotnej na **Ekspresyjne Online** stronie, musisz wysłać pobrany **XML metadanych** i **SAML pojedynczy znak na adres URL usługi** do [Ekspresyjne Online obsługuje zespołu](mailto:bgsdashboardteam@millwardbrown.com).</span><span class="sxs-lookup"><span data-stu-id="f872f-175">To configure single sign-on on **BGS Online** side, you need to send the downloaded **Metadata XML** and **SAML Single Sign-On Service URL** to [BGS Online support team](mailto:bgsdashboardteam@millwardbrown.com).</span></span> 


> [!TIP]
> <span data-ttu-id="f872f-176">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="f872f-176">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f872f-177">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="f872f-177">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f872f-178">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f872f-178">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f872f-179">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f872f-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="f872f-180">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="f872f-180">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="f872f-182">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f872f-182">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f872f-183">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="f872f-183">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bgsonline-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f872f-185">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="f872f-185">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bgsonline-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f872f-187">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f872f-187">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bgsonline-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f872f-189">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f872f-189">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bgsonline-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f872f-191">a.</span><span class="sxs-lookup"><span data-stu-id="f872f-191">a.</span></span> <span data-ttu-id="f872f-192">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f872f-192">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f872f-193">b.</span><span class="sxs-lookup"><span data-stu-id="f872f-193">b.</span></span> <span data-ttu-id="f872f-194">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f872f-194">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f872f-195">c.</span><span class="sxs-lookup"><span data-stu-id="f872f-195">c.</span></span> <span data-ttu-id="f872f-196">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="f872f-196">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f872f-197">d.</span><span class="sxs-lookup"><span data-stu-id="f872f-197">d.</span></span> <span data-ttu-id="f872f-198">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="f872f-198">Click **Create**.</span></span>
 
### <a name="creating-a-bgs-online-test-user"></a><span data-ttu-id="f872f-199">Tworzenie użytkownika testowego Ekspresyjne Online</span><span class="sxs-lookup"><span data-stu-id="f872f-199">Creating a BGS Online test user</span></span>

<span data-ttu-id="f872f-200">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta Ekspresyjne online.</span><span class="sxs-lookup"><span data-stu-id="f872f-200">In this section, you create a user called Britta Simon in BGS Online.</span></span> <span data-ttu-id="f872f-201">Praca z [zespół pomocy technicznej Online Ekspresyjne](mailto:bgsdashboardteam@millwardbrown.com) Aby dodać użytkowników do platformy Ekspresyjne Online.</span><span class="sxs-lookup"><span data-stu-id="f872f-201">Work with [BGS Online support team](mailto:bgsdashboardteam@millwardbrown.com) to add the users in the BGS Online platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f872f-202">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f872f-202">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f872f-203">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do Ekspresyjne Online.</span><span class="sxs-lookup"><span data-stu-id="f872f-203">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BGS Online.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="f872f-205">**Aby przypisać Simona Britta Ekspresyjne Online, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f872f-205">**To assign Britta Simon to BGS Online, perform the following steps:**</span></span>

1. <span data-ttu-id="f872f-206">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="f872f-206">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="f872f-208">Na liście aplikacji zaznacz **Ekspresyjne Online**.</span><span class="sxs-lookup"><span data-stu-id="f872f-208">In the applications list, select **BGS Online**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_app.png) 

3. <span data-ttu-id="f872f-210">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="f872f-210">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="f872f-212">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f872f-212">Click **Add** button.</span></span> <span data-ttu-id="f872f-213">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f872f-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="f872f-215">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="f872f-215">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f872f-216">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f872f-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f872f-217">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f872f-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f872f-218">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="f872f-218">Testing single sign-on</span></span>

<span data-ttu-id="f872f-219">W tej sekcji można przetestować konfigurację usługi Azure AD z logowania jednokrotnego za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="f872f-219">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="f872f-220">Po kliknięciu kafelka Ekspresyjne Online w panelu dostępu użytkownik powinien uzyskać automatycznie zalogowane Ekspresyjne Online aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f872f-220">When you click the BGS Online tile in the Access Panel, you should get automatically signed-on to your BGS Online application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f872f-221">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="f872f-221">Additional resources</span></span>

* [<span data-ttu-id="f872f-222">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f872f-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f872f-223">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f872f-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_203.png

