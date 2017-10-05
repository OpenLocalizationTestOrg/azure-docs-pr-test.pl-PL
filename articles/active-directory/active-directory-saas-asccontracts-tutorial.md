---
title: 'Samouczek: Integracji Azure Active Directory z kontraktami ASC | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i kontrakty ASC."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f7f54202-1581-4e55-a97e-02633ff9382d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/21/2017
ms.author: jeedes
ms.openlocfilehash: 87ea3cc55f9683e7d5b9912a87d675575cea0347
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-asc-contracts"></a><span data-ttu-id="c0393-103">Samouczek: Integracji Azure Active Directory z kontraktami ASC</span><span class="sxs-lookup"><span data-stu-id="c0393-103">Tutorial: Azure Active Directory integration with ASC Contracts</span></span>

<span data-ttu-id="c0393-104">Z tego samouczka dowiesz integrowanie ASC umowy z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c0393-104">In this tutorial, you learn how to integrate ASC Contracts with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c0393-105">Integrowanie ASC umów z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="c0393-105">Integrating ASC Contracts with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c0393-106">Można kontrolować w usłudze Azure AD, który ma dostęp do umów ASC</span><span class="sxs-lookup"><span data-stu-id="c0393-106">You can control in Azure AD who has access to ASC Contracts</span></span>
- <span data-ttu-id="c0393-107">Umożliwia użytkownikom automatycznie pobrać zalogowane umów ASC (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0393-107">You can enable your users to automatically get signed-on to ASC Contracts (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c0393-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c0393-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c0393-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c0393-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c0393-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c0393-110">Prerequisites</span></span>

<span data-ttu-id="c0393-111">Aby skonfigurować integrację usługi Azure AD z kontraktami ASC, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="c0393-111">To configure Azure AD integration with ASC Contracts, you need the following items:</span></span>

- <span data-ttu-id="c0393-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0393-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c0393-113">Kontrakty ASC jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="c0393-113">An ASC Contracts single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c0393-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="c0393-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c0393-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="c0393-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c0393-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="c0393-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c0393-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c0393-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c0393-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="c0393-118">Scenario description</span></span>
<span data-ttu-id="c0393-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="c0393-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c0393-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="c0393-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c0393-121">Dodawanie umów ASC z galerii</span><span class="sxs-lookup"><span data-stu-id="c0393-121">Adding ASC Contracts from the gallery</span></span>
2. <span data-ttu-id="c0393-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="c0393-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-asc-contracts-from-the-gallery"></a><span data-ttu-id="c0393-123">Dodawanie umów ASC z galerii</span><span class="sxs-lookup"><span data-stu-id="c0393-123">Adding ASC Contracts from the gallery</span></span>
<span data-ttu-id="c0393-124">Aby skonfigurować integrację umów ASC do usługi Azure AD, należy dodać umów ASC z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="c0393-124">To configure the integration of ASC Contracts into Azure AD, you need to add ASC Contracts from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c0393-125">**Aby dodać umowy ASC z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c0393-125">**To add ASC Contracts from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c0393-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="c0393-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="c0393-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="c0393-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c0393-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="c0393-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="c0393-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c0393-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="c0393-133">W polu wyszukiwania wpisz **kontrakty ASC**.</span><span class="sxs-lookup"><span data-stu-id="c0393-133">In the search box, type **ASC Contracts**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_search.png)

5. <span data-ttu-id="c0393-135">W panelu wyników wybierz **kontrakty ASC**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="c0393-135">In the results panel, select **ASC Contracts**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c0393-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="c0393-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c0393-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z kontraktami ASC oparte na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="c0393-138">In this section, you configure and test Azure AD single sign-on with ASC Contracts based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c0393-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w kontraktach ASC jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c0393-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ASC Contracts is to a user in Azure AD.</span></span> <span data-ttu-id="c0393-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w kontraktach ASC musi się.</span><span class="sxs-lookup"><span data-stu-id="c0393-140">In other words, a link relationship between an Azure AD user and the related user in ASC Contracts needs to be established.</span></span>

<span data-ttu-id="c0393-141">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w kontraktach ASC.</span><span class="sxs-lookup"><span data-stu-id="c0393-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ASC Contracts.</span></span>

<span data-ttu-id="c0393-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z kontraktami ASC, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="c0393-142">To configure and test Azure AD single sign-on with ASC Contracts, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c0393-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="c0393-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c0393-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="c0393-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c0393-145">**[Tworzenie użytkownika testowego kontrakty ASC](#creating-an-asc-contracts-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta kontrakty ASC, połączonej z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c0393-145">**[Creating an ASC Contracts test user](#creating-an-asc-contracts-test-user)** - to have a counterpart of Britta Simon in ASC Contracts that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c0393-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="c0393-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c0393-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="c0393-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c0393-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="c0393-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c0393-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować rejestracji jednokrotnej w kontraktach ASC aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c0393-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ASC Contracts application.</span></span>

<span data-ttu-id="c0393-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z kontraktami ASC, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c0393-150">**To configure Azure AD single sign-on with ASC Contracts, perform the following steps:**</span></span>

1. <span data-ttu-id="c0393-151">W portalu Azure na **kontrakty ASC** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="c0393-151">In the Azure portal, on the **ASC Contracts** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="c0393-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="c0393-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_samlbase.png)

3. <span data-ttu-id="c0393-155">Na **ASC kontrakty domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c0393-155">On the **ASC Contracts Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_url.png)

    <span data-ttu-id="c0393-157">a.</span><span class="sxs-lookup"><span data-stu-id="c0393-157">a.</span></span> <span data-ttu-id="c0393-158">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.asccontracts.com/shibboleth`</span><span class="sxs-lookup"><span data-stu-id="c0393-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.asccontracts.com/shibboleth`</span></span>

    <span data-ttu-id="c0393-159">b.</span><span class="sxs-lookup"><span data-stu-id="c0393-159">b.</span></span> <span data-ttu-id="c0393-160">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.asccontracts.com/shibboleth.sso/login`</span><span class="sxs-lookup"><span data-stu-id="c0393-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.asccontracts.com/shibboleth.sso/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c0393-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="c0393-161">These values are not real.</span></span> <span data-ttu-id="c0393-162">Rzeczywisty identyfikator i adres URL odpowiedzi, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="c0393-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="c0393-163">Skontaktuj się z zespołem ASC Inc. sieci (ASC) na **613.599.6178** uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="c0393-163">Contact ASC Networks Inc. (ASC) team at **613.599.6178** to get these values.</span></span>

4. <span data-ttu-id="c0393-164">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="c0393-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_certificate.png) 

5. <span data-ttu-id="c0393-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c0393-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-asccontracts-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c0393-168">Do konfigurowania rejestracji jednokrotnej na **kontrakty ASC** po stronie, zadzwoń do pomocy technicznej ASC Inc. sieci (ASC) w **613.599.6178** i udostępnia je z pobranego **XML metadanych**.</span><span class="sxs-lookup"><span data-stu-id="c0393-168">To configure single sign-on on **ASC Contracts** side, call ASC Networks Inc. (ASC) support at **613.599.6178** and provide them with the downloaded **Metadata XML**.</span></span> <span data-ttu-id="c0393-169">Połączenia logowania jednokrotnego SAML prawidłowo po obu stronach instalacji tej aplikacji programu.</span><span class="sxs-lookup"><span data-stu-id="c0393-169">They set this application up to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="c0393-170">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="c0393-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c0393-171">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="c0393-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c0393-172">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c0393-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c0393-173">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0393-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="c0393-174">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="c0393-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="c0393-176">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c0393-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c0393-177">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="c0393-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c0393-179">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="c0393-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c0393-181">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c0393-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c0393-183">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c0393-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c0393-185">a.</span><span class="sxs-lookup"><span data-stu-id="c0393-185">a.</span></span> <span data-ttu-id="c0393-186">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c0393-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c0393-187">b.</span><span class="sxs-lookup"><span data-stu-id="c0393-187">b.</span></span> <span data-ttu-id="c0393-188">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c0393-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c0393-189">c.</span><span class="sxs-lookup"><span data-stu-id="c0393-189">c.</span></span> <span data-ttu-id="c0393-190">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="c0393-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c0393-191">d.</span><span class="sxs-lookup"><span data-stu-id="c0393-191">d.</span></span> <span data-ttu-id="c0393-192">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="c0393-192">Click **Create**.</span></span>
 
### <a name="creating-an-asc-contracts-test-user"></a><span data-ttu-id="c0393-193">Tworzenie użytkownika testowego kontrakty ASC</span><span class="sxs-lookup"><span data-stu-id="c0393-193">Creating an ASC Contracts test user</span></span>

<span data-ttu-id="c0393-194">Współpraca z zespołem pomocy technicznej ASC Inc. sieci (ASC) na **613.599.6178** uzyskać dodano platformy kontrakty ASC użytkowników.</span><span class="sxs-lookup"><span data-stu-id="c0393-194">Work with ASC Networks Inc. (ASC) support team at **613.599.6178** to get the users added in the ASC Contracts platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c0393-195">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0393-195">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c0393-196">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do ASC umów.</span><span class="sxs-lookup"><span data-stu-id="c0393-196">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ASC Contracts.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="c0393-198">**Aby przypisać Simona Britta kontrakty ASC, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c0393-198">**To assign Britta Simon to ASC Contracts, perform the following steps:**</span></span>

1. <span data-ttu-id="c0393-199">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="c0393-199">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="c0393-201">Na liście aplikacji zaznacz **kontrakty ASC**.</span><span class="sxs-lookup"><span data-stu-id="c0393-201">In the applications list, select **ASC Contracts**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_app.png) 

3. <span data-ttu-id="c0393-203">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="c0393-203">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="c0393-205">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c0393-205">Click **Add** button.</span></span> <span data-ttu-id="c0393-206">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c0393-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="c0393-208">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="c0393-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c0393-209">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c0393-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c0393-210">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c0393-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c0393-211">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="c0393-211">Testing single sign-on</span></span>

<span data-ttu-id="c0393-212">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="c0393-212">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c0393-213">Po kliknięciu kafelka ASC kontraktów w panelu dostępu należy należy pobrać automatycznie zalogowane do aplikacji ASC umów.</span><span class="sxs-lookup"><span data-stu-id="c0393-213">When you click the ASC Contracts tile in the Access Panel, you should get automatically signed-on to your ASC Contracts application.</span></span> <span data-ttu-id="c0393-214">Aby uzyskać więcej informacji na temat panelu dostępu Zobacz.</span><span class="sxs-lookup"><span data-stu-id="c0393-214">For more information about the Access Panel, see.</span></span> <span data-ttu-id="c0393-215">[Wprowadzenie do panelu dostępu](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="c0393-215">[Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c0393-216">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="c0393-216">Additional resources</span></span>

* [<span data-ttu-id="c0393-217">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c0393-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c0393-218">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c0393-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_203.png

