---
title: 'Samouczek: Integracji Azure Active Directory osobom | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i osoby."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7c9b6202-11dd-4bb6-a679-8fb0a7a0ef4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: caa287a2ed8774965ef722685e4e950336e5e0ea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-people"></a><span data-ttu-id="77382-103">Samouczek: Integracji Azure Active Directory osobom</span><span class="sxs-lookup"><span data-stu-id="77382-103">Tutorial: Azure Active Directory integration with People</span></span>

<span data-ttu-id="77382-104">Z tego samouczka dowiesz się integrowanie osób z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="77382-104">In this tutorial, you learn how to integrate People with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="77382-105">Integrowanie osób z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="77382-105">Integrating People with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="77382-106">Można kontrolować w usłudze Azure AD, który ma dostęp do osób</span><span class="sxs-lookup"><span data-stu-id="77382-106">You can control in Azure AD who has access to People</span></span>
- <span data-ttu-id="77382-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do osób (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="77382-107">You can enable your users to automatically get signed-on to People (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="77382-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="77382-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="77382-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="77382-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="77382-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="77382-110">Prerequisites</span></span>

<span data-ttu-id="77382-111">Aby skonfigurować integrację usługi Azure AD osobom, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="77382-111">To configure Azure AD integration with People, you need the following items:</span></span>

- <span data-ttu-id="77382-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="77382-112">An Azure AD subscription</span></span>
- <span data-ttu-id="77382-113">Osoby logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="77382-113">A People single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="77382-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="77382-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="77382-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="77382-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="77382-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="77382-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="77382-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="77382-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="77382-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="77382-118">Scenario description</span></span>
<span data-ttu-id="77382-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="77382-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="77382-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="77382-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="77382-121">Dodawanie użytkowników z galerii</span><span class="sxs-lookup"><span data-stu-id="77382-121">Adding People from the gallery</span></span>
2. <span data-ttu-id="77382-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="77382-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-people-from-the-gallery"></a><span data-ttu-id="77382-123">Dodawanie użytkowników z galerii</span><span class="sxs-lookup"><span data-stu-id="77382-123">Adding People from the gallery</span></span>
<span data-ttu-id="77382-124">Aby skonfigurować integrację usługi Azure AD osób, należy dodać użytkowników z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="77382-124">To configure the integration of People into Azure AD, you need to add People from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="77382-125">**Aby dodać użytkowników z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="77382-125">**To add People from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="77382-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="77382-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="77382-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="77382-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="77382-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="77382-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="77382-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="77382-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="77382-133">W polu wyszukiwania wpisz **osób**.</span><span class="sxs-lookup"><span data-stu-id="77382-133">In the search box, type **People**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-people-tutorial/tutorial_people_search.png)

5. <span data-ttu-id="77382-135">W panelu wyników wybierz **osób**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="77382-135">In the results panel, select **People**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-people-tutorial/tutorial_people_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="77382-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="77382-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="77382-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej osobom w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="77382-138">In this section, you configure and test Azure AD single sign-on with People based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="77382-139">Do rejestracji jednokrotnej do pracy usługi Azure AD musi ustalić użytkownika odpowiednika w osób do użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="77382-139">For single sign-on to work, Azure AD needs to know what the counterpart user in People is to a user in Azure AD.</span></span> <span data-ttu-id="77382-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i danemu użytkownikowi w osób musi określone.</span><span class="sxs-lookup"><span data-stu-id="77382-140">In other words, a link relationship between an Azure AD user and the related user in People needs to be established.</span></span>

<span data-ttu-id="77382-141">Osoby, przypisywanie wartości **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="77382-141">In People, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="77382-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z osobami, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="77382-142">To configure and test Azure AD single sign-on with People, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="77382-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="77382-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="77382-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="77382-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="77382-145">**[Tworzenie użytkownika testowego osób](#creating-a-people-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta osób, którym jest połączony z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="77382-145">**[Creating a People test user](#creating-a-people-test-user)** - to have a counterpart of Britta Simon in People that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="77382-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="77382-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="77382-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="77382-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="77382-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="77382-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="77382-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji osób.</span><span class="sxs-lookup"><span data-stu-id="77382-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your People application.</span></span>

<span data-ttu-id="77382-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej osobom, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="77382-150">**To configure Azure AD single sign-on with People, perform the following steps:**</span></span>

1. <span data-ttu-id="77382-151">W portalu Azure na **osób** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="77382-151">In the Azure portal, on the **People** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="77382-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="77382-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-people-tutorial/tutorial_people_samlbase.png)

3. <span data-ttu-id="77382-155">Na **domeny osoby i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="77382-155">On the **People Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-people-tutorial/tutorial_people_url.png)

    <span data-ttu-id="77382-157">a.</span><span class="sxs-lookup"><span data-stu-id="77382-157">a.</span></span> <span data-ttu-id="77382-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<company name>.peoplehr.com/`</span><span class="sxs-lookup"><span data-stu-id="77382-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.peoplehr.com/`</span></span>

    <span data-ttu-id="77382-159">b.</span><span class="sxs-lookup"><span data-stu-id="77382-159">b.</span></span> <span data-ttu-id="77382-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://www.peoplehr.com`</span><span class="sxs-lookup"><span data-stu-id="77382-160">In the **Identifier** textbox, type a URL using the following pattern: `https://www.peoplehr.com`</span></span>

    <span data-ttu-id="77382-161">c.</span><span class="sxs-lookup"><span data-stu-id="77382-161">c.</span></span> <span data-ttu-id="77382-162">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<company name>.peoplehr.net/Pages/Saml/ConsumeAzureAD.aspx`</span><span class="sxs-lookup"><span data-stu-id="77382-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.peoplehr.net/Pages/Saml/ConsumeAzureAD.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="77382-163">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="77382-163">These values are not real.</span></span> <span data-ttu-id="77382-164">Rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="77382-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="77382-165">Skontaktuj się z [zespołem pomocy technicznej klienta osób](mailto:customerservices@peoplehr.com) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="77382-165">Contact [People Client support team](mailto:customerservices@peoplehr.com) to get these values.</span></span>

5. <span data-ttu-id="77382-166">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="77382-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-people-tutorial/tutorial_people_certificate.png) 

6. <span data-ttu-id="77382-168">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="77382-168">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-people-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="77382-170">Aby uzyskać logowania jednokrotnego skonfigurowane dla aplikacji, należy logowanie do osób dzierżawy z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="77382-170">To get SSO configured for your application, you need to sign-on to your People tenant as an administrator.</span></span>
   
8. <span data-ttu-id="77382-171">W menu po lewej stronie kliknij **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="77382-171">In the menu on the left side, click **Settings**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-people-tutorial/tutorial_people_001.png)

9. <span data-ttu-id="77382-173">Kliknij przycisk **firmy**.</span><span class="sxs-lookup"><span data-stu-id="77382-173">Click **Company**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-people-tutorial/tutorial_people_002.png)

10. <span data-ttu-id="77382-175">Na **przekazywania "Rejestracji jednokrotnej" SAML metadane pliku**, kliknij przycisk **Przeglądaj** można przekazać pliku pobranego metadanych.</span><span class="sxs-lookup"><span data-stu-id="77382-175">On the **Upload 'Single Sign On' SAML meta-data file**, click **Browse** to upload the downloaded metadata file.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-people-tutorial/tutorial_people_003.png)

> [!TIP]
> <span data-ttu-id="77382-177">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="77382-177">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="77382-178">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="77382-178">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="77382-179">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="77382-179">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="77382-180">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="77382-180">Creating an Azure AD test user</span></span>
<span data-ttu-id="77382-181">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="77382-181">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="77382-183">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="77382-183">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="77382-184">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="77382-184">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-people-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="77382-186">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="77382-186">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-people-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="77382-188">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="77382-188">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-people-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="77382-190">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="77382-190">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-people-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="77382-192">a.</span><span class="sxs-lookup"><span data-stu-id="77382-192">a.</span></span> <span data-ttu-id="77382-193">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="77382-193">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="77382-194">b.</span><span class="sxs-lookup"><span data-stu-id="77382-194">b.</span></span> <span data-ttu-id="77382-195">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="77382-195">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="77382-196">c.</span><span class="sxs-lookup"><span data-stu-id="77382-196">c.</span></span> <span data-ttu-id="77382-197">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="77382-197">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="77382-198">d.</span><span class="sxs-lookup"><span data-stu-id="77382-198">d.</span></span> <span data-ttu-id="77382-199">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="77382-199">Click **Create**.</span></span>
 
### <a name="creating-a-people-test-user"></a><span data-ttu-id="77382-200">Tworzenie użytkownika testowego osób</span><span class="sxs-lookup"><span data-stu-id="77382-200">Creating a People test user</span></span>

<span data-ttu-id="77382-201">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w osób.</span><span class="sxs-lookup"><span data-stu-id="77382-201">In this section, you create a user called Britta Simon in People.</span></span> <span data-ttu-id="77382-202">Praca z [zespołem pomocy technicznej klienta osób](mailto:customerservices@peoplehr.com) Aby dodać użytkowników do platformy osób.</span><span class="sxs-lookup"><span data-stu-id="77382-202">Work with [People Client support team](mailto:customerservices@peoplehr.com) to add the users in the People platform.</span></span> <span data-ttu-id="77382-203">Użytkownicy muszą utworzyć i aktywowana, aby użyć rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="77382-203">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="77382-204">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="77382-204">Assigning the Azure AD test user</span></span>

<span data-ttu-id="77382-205">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do osób.</span><span class="sxs-lookup"><span data-stu-id="77382-205">In this section, you enable Britta Simon to use Azure single sign-on by granting access to People.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="77382-207">**Aby przypisać Simona Britta do osoby, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="77382-207">**To assign Britta Simon to People, perform the following steps:**</span></span>

1. <span data-ttu-id="77382-208">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="77382-208">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="77382-210">Na liście aplikacji zaznacz **osób**.</span><span class="sxs-lookup"><span data-stu-id="77382-210">In the applications list, select **People**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-people-tutorial/tutorial_people_app.png) 

3. <span data-ttu-id="77382-212">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="77382-212">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="77382-214">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="77382-214">Click **Add** button.</span></span> <span data-ttu-id="77382-215">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="77382-215">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="77382-217">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="77382-217">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="77382-218">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="77382-218">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="77382-219">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="77382-219">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="77382-220">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="77382-220">Testing single sign-on</span></span>

<span data-ttu-id="77382-221">Celem tej sekcji służy do testowania konfigurację usługi Azure AD z logowania jednokrotnego za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="77382-221">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="77382-222">Po kliknięciu kafelka osób w panelu dostępu należy należy pobrać automatycznie zalogowane do aplikacji osób.</span><span class="sxs-lookup"><span data-stu-id="77382-222">When you click the People tile in the Access Panel, you should get automatically signed-on to your People application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="77382-223">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="77382-223">Additional resources</span></span>

* [<span data-ttu-id="77382-224">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="77382-224">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="77382-225">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="77382-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-people-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-people-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-people-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-people-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-people-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-people-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-people-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-people-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-people-tutorial/tutorial_general_203.png

