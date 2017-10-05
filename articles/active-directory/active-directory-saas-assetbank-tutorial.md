---
title: "Samouczek: Integracji Azure Active Directory z zasobów Bank | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Bank zasobów."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3006ad6e-8831-41cd-94aa-7e7ae770ce7b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 17bc0082e3721b50269cb4b17884c0e4a4cbcb5d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-asset-bank"></a><span data-ttu-id="daf4d-103">Samouczek: Integracji Azure Active Directory z banku zasobów</span><span class="sxs-lookup"><span data-stu-id="daf4d-103">Tutorial: Azure Active Directory integration with Asset Bank</span></span>

<span data-ttu-id="daf4d-104">Z tego samouczka dowiesz się integrowanie Bank zasobów w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="daf4d-104">In this tutorial, you learn how to integrate Asset Bank with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="daf4d-105">Integrowanie Bank zasobów z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="daf4d-105">Integrating Asset Bank with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="daf4d-106">Można kontrolować w usłudze Azure AD, który ma dostęp do zasobów Bank</span><span class="sxs-lookup"><span data-stu-id="daf4d-106">You can control in Azure AD who has access to Asset Bank</span></span>
- <span data-ttu-id="daf4d-107">Umożliwia użytkownikom automatycznie pobrać zalogowane Bankowi zasobów (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="daf4d-107">You can enable your users to automatically get signed-on to Asset Bank (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="daf4d-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="daf4d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="daf4d-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="daf4d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="daf4d-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="daf4d-110">Prerequisites</span></span>

<span data-ttu-id="daf4d-111">Aby skonfigurować integrację usługi Azure AD z zasobów Bank, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="daf4d-111">To configure Azure AD integration with Asset Bank, you need the following items:</span></span>

- <span data-ttu-id="daf4d-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="daf4d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="daf4d-113">Bank zasobów jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="daf4d-113">An Asset Bank single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="daf4d-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="daf4d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="daf4d-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="daf4d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="daf4d-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="daf4d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="daf4d-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="daf4d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="daf4d-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="daf4d-118">Scenario description</span></span>
<span data-ttu-id="daf4d-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="daf4d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="daf4d-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="daf4d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="daf4d-121">Dodawanie zasobów Bank z galerii</span><span class="sxs-lookup"><span data-stu-id="daf4d-121">Adding Asset Bank from the gallery</span></span>
2. <span data-ttu-id="daf4d-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="daf4d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-asset-bank-from-the-gallery"></a><span data-ttu-id="daf4d-123">Dodawanie zasobów Bank z galerii</span><span class="sxs-lookup"><span data-stu-id="daf4d-123">Adding Asset Bank from the gallery</span></span>
<span data-ttu-id="daf4d-124">Aby skonfigurować integrację usługi Azure AD Bank zasobów, należy dodać Bank zasobów z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="daf4d-124">To configure the integration of Asset Bank into Azure AD, you need to add Asset Bank from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="daf4d-125">**Aby dodać Bank zasobów z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="daf4d-125">**To add Asset Bank from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="daf4d-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="daf4d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="daf4d-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="daf4d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="daf4d-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="daf4d-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="daf4d-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="daf4d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="daf4d-133">W polu wyszukiwania wpisz **Bank zasobów**.</span><span class="sxs-lookup"><span data-stu-id="daf4d-133">In the search box, type **Asset Bank**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_search.png)

5. <span data-ttu-id="daf4d-135">W panelu wyników wybierz **Bank zasobów**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="daf4d-135">In the results panel, select **Asset Bank**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="daf4d-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="daf4d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="daf4d-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej banku zasobów na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="daf4d-138">In this section, you configure and test Azure AD single sign-on with Asset Bank based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="daf4d-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w banku zasobów jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="daf4d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Asset Bank is to a user in Azure AD.</span></span> <span data-ttu-id="daf4d-140">Innymi słowy musi można ustanowić łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w banku zasobów.</span><span class="sxs-lookup"><span data-stu-id="daf4d-140">In other words, a link relationship between an Azure AD user and the related user in Asset Bank needs to be established.</span></span>

<span data-ttu-id="daf4d-141">W banku zasobów, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="daf4d-141">In Asset Bank, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="daf4d-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej w banku zasobów, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="daf4d-142">To configure and test Azure AD single sign-on with Asset Bank, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="daf4d-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="daf4d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="daf4d-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="daf4d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="daf4d-145">**[Tworzenie użytkownika testowego Bank zasobów](#creating-an-asset-bank-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta banku zasobów, który jest połączony z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="daf4d-145">**[Creating an Asset Bank test user](#creating-an-asset-bank-test-user)** - to have a counterpart of Britta Simon in Asset Bank that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="daf4d-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="daf4d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="daf4d-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="daf4d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="daf4d-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="daf4d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="daf4d-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w banku zasobów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="daf4d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Asset Bank application.</span></span>

<span data-ttu-id="daf4d-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z zasobów Bank, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="daf4d-150">**To configure Azure AD single sign-on with Asset Bank, perform the following steps:**</span></span>

1. <span data-ttu-id="daf4d-151">W portalu Azure na **Bank zasobów** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="daf4d-151">In the Azure portal, on the **Asset Bank** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="daf4d-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="daf4d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_samlbase.png)

3. <span data-ttu-id="daf4d-155">Na **zasobów Bank domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="daf4d-155">On the **Asset Bank Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_url.png)

    <span data-ttu-id="daf4d-157">a.</span><span class="sxs-lookup"><span data-stu-id="daf4d-157">a.</span></span> <span data-ttu-id="daf4d-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.assetbank-server.com`</span><span class="sxs-lookup"><span data-stu-id="daf4d-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.assetbank-server.com`</span></span>

    <span data-ttu-id="daf4d-159">b.</span><span class="sxs-lookup"><span data-stu-id="daf4d-159">b.</span></span> <span data-ttu-id="daf4d-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.assetbank-server.com/shibboleth`</span><span class="sxs-lookup"><span data-stu-id="daf4d-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.assetbank-server.com/shibboleth`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="daf4d-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="daf4d-161">These values are not real.</span></span> <span data-ttu-id="daf4d-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="daf4d-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="daf4d-163">Skontaktuj się z [zespołem pomocy technicznej klienta Bank zasobów](mailto:support@assetbank.co.uk) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="daf4d-163">Contact [Asset Bank Client support team](mailto:support@assetbank.co.uk) to get these values.</span></span> 
 
4. <span data-ttu-id="daf4d-164">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="daf4d-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_certificate.png) 

5. <span data-ttu-id="daf4d-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="daf4d-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-assetbank-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="daf4d-168">Skonfigurować logowanie jednokrotne w **Bank zasobów** stronie, musisz wysłać pobrany **XML metadanych** do [zespołem pomocy technicznej Bank zasobów](mailto:support@assetbank.co.uk).</span><span class="sxs-lookup"><span data-stu-id="daf4d-168">To configure single sign-on on **Asset Bank** side, you need to send the downloaded **Metadata XML** to [Asset Bank support team](mailto:support@assetbank.co.uk).</span></span> 


> [!TIP]
> <span data-ttu-id="daf4d-169">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="daf4d-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="daf4d-170">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="daf4d-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="daf4d-171">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="daf4d-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="daf4d-172">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="daf4d-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="daf4d-173">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="daf4d-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="daf4d-175">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="daf4d-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="daf4d-176">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="daf4d-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-assetbank-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="daf4d-178">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="daf4d-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-assetbank-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="daf4d-180">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="daf4d-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-assetbank-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="daf4d-182">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="daf4d-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-assetbank-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="daf4d-184">a.</span><span class="sxs-lookup"><span data-stu-id="daf4d-184">a.</span></span> <span data-ttu-id="daf4d-185">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="daf4d-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="daf4d-186">b.</span><span class="sxs-lookup"><span data-stu-id="daf4d-186">b.</span></span> <span data-ttu-id="daf4d-187">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="daf4d-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="daf4d-188">c.</span><span class="sxs-lookup"><span data-stu-id="daf4d-188">c.</span></span> <span data-ttu-id="daf4d-189">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="daf4d-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="daf4d-190">d.</span><span class="sxs-lookup"><span data-stu-id="daf4d-190">d.</span></span> <span data-ttu-id="daf4d-191">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="daf4d-191">Click **Create**.</span></span>
 
### <a name="creating-an-asset-bank-test-user"></a><span data-ttu-id="daf4d-192">Tworzenie użytkownika testowego Bank zasobów</span><span class="sxs-lookup"><span data-stu-id="daf4d-192">Creating an Asset Bank test user</span></span>

<span data-ttu-id="daf4d-193">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w banku zasobów.</span><span class="sxs-lookup"><span data-stu-id="daf4d-193">The objective of this section is to create a user called Britta Simon in Asset Bank.</span></span> <span data-ttu-id="daf4d-194">Bank zasobów obsługę w czasie, który jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="daf4d-194">Asset Bank supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="daf4d-195">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="daf4d-195">There is no action item for you in this section.</span></span> <span data-ttu-id="daf4d-196">Nowy użytkownik jest tworzony podczas próby dostępu do zasobów Bank, jeśli go jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="daf4d-196">A new user is created during an attempt to access Asset Bank if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="daf4d-197">Jeśli trzeba ręcznie utworzyć użytkownika, należy skontaktować się [zespołem pomocy technicznej Bank zasobów](mailto:support@assetbank.co.uk).</span><span class="sxs-lookup"><span data-stu-id="daf4d-197">If you need to create a user manually, you need to contact the [Asset Bank support team](mailto:support@assetbank.co.uk).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="daf4d-198">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="daf4d-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="daf4d-199">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do zasobów Bank.</span><span class="sxs-lookup"><span data-stu-id="daf4d-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Asset Bank.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="daf4d-201">**Aby przypisać Simona Britta Bank zasobów, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="daf4d-201">**To assign Britta Simon to Asset Bank, perform the following steps:**</span></span>

1. <span data-ttu-id="daf4d-202">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="daf4d-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="daf4d-204">Na liście aplikacji zaznacz **Bank zasobów**.</span><span class="sxs-lookup"><span data-stu-id="daf4d-204">In the applications list, select **Asset Bank**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_app.png) 

3. <span data-ttu-id="daf4d-206">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="daf4d-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="daf4d-208">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="daf4d-208">Click **Add** button.</span></span> <span data-ttu-id="daf4d-209">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="daf4d-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="daf4d-211">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="daf4d-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="daf4d-212">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="daf4d-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="daf4d-213">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="daf4d-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="daf4d-214">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="daf4d-214">Testing single sign-on</span></span>

<span data-ttu-id="daf4d-215">Celem tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="daf4d-215">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="daf4d-216">Po kliknięciu kafelka Bank zasobów w panelu dostępu należy należy pobrać automatycznie zalogowane do aplikacji Bank zasobów.</span><span class="sxs-lookup"><span data-stu-id="daf4d-216">When you click the Asset Bank tile in the Access Panel, you should get automatically signed-on to your Asset Bank application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="daf4d-217">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="daf4d-217">Additional resources</span></span>

* [<span data-ttu-id="daf4d-218">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="daf4d-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="daf4d-219">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="daf4d-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_203.png

