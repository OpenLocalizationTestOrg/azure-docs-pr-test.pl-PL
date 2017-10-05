---
title: 'Samouczek: Integracji Azure Active Directory z & frankly | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i & frankly."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d702060-1b89-4e9d-9f01-ede4f1171c73
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: ea18a9f9bff258337a3de6d7703b4c548efa37df
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-frankly"></a><span data-ttu-id="4df47-103">Samouczek: Integracji Azure Active Directory z & frankly</span><span class="sxs-lookup"><span data-stu-id="4df47-103">Tutorial: Azure Active Directory integration with &frankly</span></span>

<span data-ttu-id="4df47-104">W tym samouczku opisano sposób integracji & frankly w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4df47-104">In this tutorial, you learn how to integrate &frankly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4df47-105">Integrowanie & frankly z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="4df47-105">Integrating &frankly with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4df47-106">Można kontrolować w usłudze Azure AD, który ma dostęp do & frankly</span><span class="sxs-lookup"><span data-stu-id="4df47-106">You can control in Azure AD who has access to &frankly</span></span>
- <span data-ttu-id="4df47-107">Można umożliwić użytkownikom automatycznie pobrać podpisane na do & frankly (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4df47-107">You can enable your users to automatically get signed-on to &frankly (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4df47-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="4df47-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4df47-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4df47-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4df47-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4df47-110">Prerequisites</span></span>

<span data-ttu-id="4df47-111">Aby skonfigurować usługi Azure AD integracji z & frankly, możesz potrzebne są następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="4df47-111">To configure Azure AD integration with &frankly, you need the following items:</span></span>

- <span data-ttu-id="4df47-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4df47-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4df47-113">A & frankly jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="4df47-113">A &frankly single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4df47-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="4df47-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4df47-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="4df47-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4df47-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="4df47-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4df47-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4df47-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4df47-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="4df47-118">Scenario description</span></span>
<span data-ttu-id="4df47-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="4df47-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4df47-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="4df47-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4df47-121">Dodawanie & frankly z galerii</span><span class="sxs-lookup"><span data-stu-id="4df47-121">Adding &frankly from the gallery</span></span>
2. <span data-ttu-id="4df47-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="4df47-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-frankly-from-the-gallery"></a><span data-ttu-id="4df47-123">Dodawanie & frankly z galerii</span><span class="sxs-lookup"><span data-stu-id="4df47-123">Adding &frankly from the gallery</span></span>
<span data-ttu-id="4df47-124">Aby skonfigurować integrację z & frankly do usługi Azure AD, należy dodać & frankly z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="4df47-124">To configure the integration of &frankly into Azure AD, you need to add &frankly from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4df47-125">**Aby dodać & frankly z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="4df47-125">**To add &frankly from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4df47-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="4df47-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="4df47-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="4df47-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4df47-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="4df47-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="4df47-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4df47-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="4df47-133">W polu wyszukiwania wpisz **& frankly**.</span><span class="sxs-lookup"><span data-stu-id="4df47-133">In the search box, type **&frankly**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_search.png)

5. <span data-ttu-id="4df47-135">W panelu wyników wybierz **& frankly**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="4df47-135">In the results panel, select **&frankly**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4df47-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="4df47-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4df47-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z & frankly oparte na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="4df47-138">In this section, you configure and test Azure AD single sign-on with &frankly based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4df47-139">Logowanie jednokrotne do pracy usługi Azure AD musi wiedzieć, jaki użytkownik odpowiednika w & frankly jest użytkownikiem w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4df47-139">For single sign-on to work, Azure AD needs to know what the counterpart user in &frankly is to a user in Azure AD.</span></span> <span data-ttu-id="4df47-140">Innymi słowy łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w & frankly musi się.</span><span class="sxs-lookup"><span data-stu-id="4df47-140">In other words, a link relationship between an Azure AD user and the related user in &frankly needs to be established.</span></span>

<span data-ttu-id="4df47-141">W & frankly, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="4df47-141">In &frankly, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="4df47-142">Aby konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej z & frankly, możesz należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="4df47-142">To configure and test Azure AD single sign-on with &frankly, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4df47-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="4df47-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4df47-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="4df47-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4df47-145">**[Tworzenie & frankly użytkownika testowego](#creating-a-frankly-test-user)**  — aby odpowiednikiem Simona Britta w & frankly jest połączone z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4df47-145">**[Creating a &frankly test user](#creating-a-frankly-test-user)** - to have a counterpart of Britta Simon in &frankly that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4df47-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="4df47-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4df47-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="4df47-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4df47-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="4df47-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4df47-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w sieci & frankly aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4df47-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your &frankly application.</span></span>

<span data-ttu-id="4df47-150">**Aby skonfigurować usługi Azure AD pojedynczy logowania z & frankly, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="4df47-150">**To configure Azure AD single sign-on with &frankly, perform the following steps:**</span></span>

1. <span data-ttu-id="4df47-151">W portalu Azure na **& frankly** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="4df47-151">In the Azure portal, on the **&frankly** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="4df47-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="4df47-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_samlbase.png)

3. <span data-ttu-id="4df47-155">Na **& frankly domeny i adres URL** sekcji, jeśli chcesz skonfigurować aplikację w **IDP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="4df47-155">On the **&frankly Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_url.png)

    <span data-ttu-id="4df47-157">a.</span><span class="sxs-lookup"><span data-stu-id="4df47-157">a.</span></span> <span data-ttu-id="4df47-158">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/metadata.php/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="4df47-158">In the **Identifier** textbox, type a URL using the following pattern: `https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/metadata.php/<tenant id>`</span></span>

    <span data-ttu-id="4df47-159">b.</span><span class="sxs-lookup"><span data-stu-id="4df47-159">b.</span></span> <span data-ttu-id="4df47-160">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/saml2-acs.php/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="4df47-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/saml2-acs.php/<tenant id>`</span></span>

4. <span data-ttu-id="4df47-161">Sprawdź **Pokaż zaawansowane ustawienia adresu URL**.</span><span class="sxs-lookup"><span data-stu-id="4df47-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="4df47-162">Jeśli chcesz skonfigurować aplikację w **SP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="4df47-162">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_url1.png)

    <span data-ttu-id="4df47-164">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://andfrankly.com/saml/okta/?saml_sso=<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="4df47-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://andfrankly.com/saml/okta/?saml_sso=<tenant id>`</span></span>
    > [!NOTE] 
    > <span data-ttu-id="4df47-165">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="4df47-165">These values are not real.</span></span> <span data-ttu-id="4df47-166">Zaktualizować te wartości przy użyciu rzeczywistego identyfikatora logowania i adres URL odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="4df47-166">Update these values with the actual Identifier, Sign-on, and Reply URL.</span></span> <span data-ttu-id="4df47-167">Skontaktuj się z [zespołem pomocy technicznej andfrankly](mailto:help@andfrankly.com) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="4df47-167">Contact [andfrankly support team](mailto:help@andfrankly.com) to get these values.</span></span>

5. <span data-ttu-id="4df47-168">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="4df47-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_certificate.png) 

6. <span data-ttu-id="4df47-170">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="4df47-170">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-andfrankly-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="4df47-172">Skonfigurować logowanie jednokrotne w **& frankly** stronie, musisz wysłać pobrany **XML metadanych** do [zespołem pomocy technicznej andfrankly](mailto:help@andfrankly.com).</span><span class="sxs-lookup"><span data-stu-id="4df47-172">To configure single sign-on on **&frankly** side, you need to send the downloaded **Metadata XML** to [andfrankly support team](mailto:help@andfrankly.com).</span></span> 

> [!TIP]
> <span data-ttu-id="4df47-173">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="4df47-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4df47-174">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="4df47-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4df47-175">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4df47-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4df47-176">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4df47-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="4df47-177">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="4df47-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="4df47-179">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="4df47-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4df47-180">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="4df47-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4df47-182">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="4df47-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4df47-184">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4df47-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4df47-186">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="4df47-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4df47-188">a.</span><span class="sxs-lookup"><span data-stu-id="4df47-188">a.</span></span> <span data-ttu-id="4df47-189">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4df47-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4df47-190">b.</span><span class="sxs-lookup"><span data-stu-id="4df47-190">b.</span></span> <span data-ttu-id="4df47-191">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4df47-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4df47-192">c.</span><span class="sxs-lookup"><span data-stu-id="4df47-192">c.</span></span> <span data-ttu-id="4df47-193">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="4df47-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4df47-194">d.</span><span class="sxs-lookup"><span data-stu-id="4df47-194">d.</span></span> <span data-ttu-id="4df47-195">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="4df47-195">Click **Create**.</span></span>
 
### <a name="creating-a-frankly-test-user"></a><span data-ttu-id="4df47-196">Tworzenie & frankly użytkownika testowego</span><span class="sxs-lookup"><span data-stu-id="4df47-196">Creating a &frankly test user</span></span>

<span data-ttu-id="4df47-197">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w & frankly.</span><span class="sxs-lookup"><span data-stu-id="4df47-197">In this section, you create a user called Britta Simon in &frankly.</span></span> <span data-ttu-id="4df47-198">Praca z [zespołem pomocy technicznej andfrankly](mailto:help@andfrankly.com) do dodawania użytkowników w z & frankly platformy.</span><span class="sxs-lookup"><span data-stu-id="4df47-198">Work with  [andfrankly support team](mailto:help@andfrankly.com) to add the users in the &frankly platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4df47-199">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4df47-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4df47-200">W tej sekcji musisz włączyć Simona Britta do użycia usługi Azure logowania jednokrotnego za udzielanie dostępu do & frankly.</span><span class="sxs-lookup"><span data-stu-id="4df47-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to &frankly.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="4df47-202">**Aby przypisać Simona Britta do & frankly, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="4df47-202">**To assign Britta Simon to &frankly, perform the following steps:**</span></span>

1. <span data-ttu-id="4df47-203">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="4df47-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="4df47-205">Na liście aplikacji zaznacz **& frankly**.</span><span class="sxs-lookup"><span data-stu-id="4df47-205">In the applications list, select **&frankly**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_app.png) 

3. <span data-ttu-id="4df47-207">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="4df47-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="4df47-209">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="4df47-209">Click **Add** button.</span></span> <span data-ttu-id="4df47-210">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4df47-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="4df47-212">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="4df47-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4df47-213">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4df47-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4df47-214">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4df47-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4df47-215">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="4df47-215">Testing single sign-on</span></span>

<span data-ttu-id="4df47-216">Celem tej sekcji służy do testowania konfigurację usługi Azure AD z logowania jednokrotnego za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="4df47-216">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="4df47-217">Po kliknięciu przycisku & frankly kafelka w panelu dostępu, należy pobrać automatycznie podpisany w z & frankly aplikacji</span><span class="sxs-lookup"><span data-stu-id="4df47-217">When you click the &frankly tile in the Access Panel, you should get automatically signed-on to your &frankly application</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4df47-218">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="4df47-218">Additional resources</span></span>

* [<span data-ttu-id="4df47-219">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4df47-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4df47-220">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4df47-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_203.png

