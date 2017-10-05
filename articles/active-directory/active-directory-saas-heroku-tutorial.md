---
title: 'Samouczek: Integracji Azure Active Directory z Heroku | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Heroku."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d7d72ec6-4a60-4524-8634-26d8fbbcc833
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: d30605e4757b484f327a784b73f939b62ef59373
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-heroku"></a><span data-ttu-id="332e1-103">Samouczek: Integracji Azure Active Directory z Heroku</span><span class="sxs-lookup"><span data-stu-id="332e1-103">Tutorial: Azure Active Directory integration with Heroku</span></span>

<span data-ttu-id="332e1-104">Z tego samouczka dowiesz się integrowanie Heroku z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="332e1-104">In this tutorial, you learn how to integrate Heroku with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="332e1-105">Integracja z usługą Azure AD Heroku zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="332e1-105">Integrating Heroku with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="332e1-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Heroku</span><span class="sxs-lookup"><span data-stu-id="332e1-106">You can control in Azure AD who has access to Heroku</span></span>
- <span data-ttu-id="332e1-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Heroku (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="332e1-107">You can enable your users to automatically get signed-on to Heroku (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="332e1-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="332e1-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="332e1-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="332e1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="332e1-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="332e1-110">Prerequisites</span></span>

<span data-ttu-id="332e1-111">Aby skonfigurować integrację usługi Azure AD z Heroku, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="332e1-111">To configure Azure AD integration with Heroku, you need the following items:</span></span>

- <span data-ttu-id="332e1-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="332e1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="332e1-113">Heroku logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="332e1-113">A Heroku single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="332e1-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="332e1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="332e1-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="332e1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="332e1-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="332e1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="332e1-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="332e1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="332e1-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="332e1-118">Scenario description</span></span>
<span data-ttu-id="332e1-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="332e1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="332e1-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="332e1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="332e1-121">Dodawanie Heroku z galerii</span><span class="sxs-lookup"><span data-stu-id="332e1-121">Adding Heroku from the gallery</span></span>
2. <span data-ttu-id="332e1-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="332e1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-heroku-from-the-gallery"></a><span data-ttu-id="332e1-123">Dodawanie Heroku z galerii</span><span class="sxs-lookup"><span data-stu-id="332e1-123">Adding Heroku from the gallery</span></span>
<span data-ttu-id="332e1-124">Aby skonfigurować integrację usługi Azure AD Heroku, należy dodać Heroku z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="332e1-124">To configure the integration of Heroku into Azure AD, you need to add Heroku from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="332e1-125">**Aby dodać Heroku z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="332e1-125">**To add Heroku from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="332e1-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="332e1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="332e1-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="332e1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="332e1-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="332e1-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="332e1-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="332e1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="332e1-133">W polu wyszukiwania wpisz **Heroku**.</span><span class="sxs-lookup"><span data-stu-id="332e1-133">In the search box, type **Heroku**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_search.png)

5. <span data-ttu-id="332e1-135">W panelu wyników wybierz **Heroku**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="332e1-135">In the results panel, select **Heroku**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="332e1-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="332e1-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="332e1-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Heroku na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="332e1-138">In this section, you configure and test Azure AD single sign-on with Heroku based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="332e1-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Heroku jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="332e1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Heroku is to a user in Azure AD.</span></span> <span data-ttu-id="332e1-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Heroku musi się.</span><span class="sxs-lookup"><span data-stu-id="332e1-140">In other words, a link relationship between an Azure AD user and the related user in Heroku needs to be established.</span></span>

<span data-ttu-id="332e1-141">W Heroku, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="332e1-141">In Heroku, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="332e1-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Heroku, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="332e1-142">To configure and test Azure AD single sign-on with Heroku, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="332e1-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="332e1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="332e1-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="332e1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="332e1-145">**[Tworzenie użytkownika testowego Heroku](#creating-a-heroku-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Heroku połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="332e1-145">**[Creating a Heroku test user](#creating-a-heroku-test-user)** - to have a counterpart of Britta Simon in Heroku that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="332e1-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="332e1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="332e1-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="332e1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="332e1-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="332e1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="332e1-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Heroku.</span><span class="sxs-lookup"><span data-stu-id="332e1-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Heroku application.</span></span>

<span data-ttu-id="332e1-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Heroku, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="332e1-150">**To configure Azure AD single sign-on with Heroku, perform the following steps:**</span></span>

1. <span data-ttu-id="332e1-151">W portalu Azure na **Heroku** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="332e1-151">In the Azure portal, on the **Heroku** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="332e1-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="332e1-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_samlbase.png)

3. <span data-ttu-id="332e1-155">Na **Heroku domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="332e1-155">On the **Heroku Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_url.png)

    <span data-ttu-id="332e1-157">a.</span><span class="sxs-lookup"><span data-stu-id="332e1-157">a.</span></span> <span data-ttu-id="332e1-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="332e1-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>    
    `https://sso.heroku.com/saml/<company-name>/init`

    <span data-ttu-id="332e1-159">b.</span><span class="sxs-lookup"><span data-stu-id="332e1-159">b.</span></span> <span data-ttu-id="332e1-160">W **adres URL identyfikatora** tekstowym, wpisz adres URL, używając następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="332e1-160">In the **Identifier URL** textbox, type a URL using the following pattern:</span></span>            
    `https://sso.heroku.com/saml/<company-name>`

    > [!NOTE]
    ><span data-ttu-id="332e1-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="332e1-161">These values are not real.</span></span> <span data-ttu-id="332e1-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="332e1-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="332e1-163">Te wartości można uzyskać od zespołu Heroku, które zostało opisane w kolejnych sekcjach niniejszego artykułu.</span><span class="sxs-lookup"><span data-stu-id="332e1-163">You get these values from Heroku team, which is described in later sections of this article.</span></span> 
        
4. <span data-ttu-id="332e1-164">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="332e1-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_certificate.png) 

5. <span data-ttu-id="332e1-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="332e1-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-heroku-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="332e1-168">Aby włączyć logowanie Jednokrotne w Heroku, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="332e1-168">To enable SSO in Heroku, perform the following steps:</span></span>
   
    <span data-ttu-id="332e1-169">a.</span><span class="sxs-lookup"><span data-stu-id="332e1-169">a.</span></span> <span data-ttu-id="332e1-170">Zaloguj się do konta Heroku jako administrator.</span><span class="sxs-lookup"><span data-stu-id="332e1-170">Log in to the Heroku account as an administrator.</span></span>

    <span data-ttu-id="332e1-171">b.</span><span class="sxs-lookup"><span data-stu-id="332e1-171">b.</span></span> <span data-ttu-id="332e1-172">Kliknij kartę **Ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="332e1-172">Click the **Settings** tab.</span></span>

    <span data-ttu-id="332e1-173">c.</span><span class="sxs-lookup"><span data-stu-id="332e1-173">c.</span></span> <span data-ttu-id="332e1-174">Na **Zaloguj się na stronie**, kliknij przycisk **przekazać metadanych**.</span><span class="sxs-lookup"><span data-stu-id="332e1-174">On the **Single Sign On Page**, click **Upload Metadata**.</span></span>

    <span data-ttu-id="332e1-175">d.</span><span class="sxs-lookup"><span data-stu-id="332e1-175">d.</span></span> <span data-ttu-id="332e1-176">Przekaż plik metadanych, który został pobrany z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="332e1-176">Upload the metadata file, which you have downloaded from the Azure portal.</span></span>

    <span data-ttu-id="332e1-177">e.</span><span class="sxs-lookup"><span data-stu-id="332e1-177">e.</span></span> <span data-ttu-id="332e1-178">Gdy Instalator zakończy się pomyślnie, Administratorzy Zobacz okno dialogowe potwierdzenia i jest wyświetlany adres URL logowania logowania jednokrotnego dla użytkowników końcowych.</span><span class="sxs-lookup"><span data-stu-id="332e1-178">When the setup is successful, administrators see a confirmation dialog and the URL of the SSO Login for end users is displayed.</span></span> 

    <span data-ttu-id="332e1-179">f.</span><span class="sxs-lookup"><span data-stu-id="332e1-179">f.</span></span> <span data-ttu-id="332e1-180">Kopia **adres URL logowania Heroku** i **Heroku identyfikator jednostki** wartości i wróć do **Heroku domeny i adres URL** sekcji w portalu Azure i Wklej te wartości do  **Adres Url logowania** i **identyfikator** pól tekstowych odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="332e1-180">Copy the **Heroku Login URL** and **Heroku Entity ID** values and go back to **Heroku Domain and URLs** section in Azure portal and paste these values into the **Sign-On Url** and **Identifier** textboxes respectively.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_52.png) 
    
8. <span data-ttu-id="332e1-182">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="332e1-182">Click **Next**.</span></span>

> [!TIP]
> <span data-ttu-id="332e1-183">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="332e1-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="332e1-184">Po dodaniu tej aplikacji z **aplikacje przedsiębiorstwa w usłudze Active Directory** po prostu kliknij **rejestracji jednokrotnej** karcie i uzyskać dostęp do osadzonego dokumentacji za pośrednictwem  **Konfiguracja** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="332e1-184">After adding this app from the **Active Directory Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="332e1-185">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="332e1-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="332e1-186">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="332e1-186">Creating an Azure AD test user</span></span>

<span data-ttu-id="332e1-187">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="332e1-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="332e1-189">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="332e1-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="332e1-190">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="332e1-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-heroku-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="332e1-192">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="332e1-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-heroku-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="332e1-194">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="332e1-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-heroku-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="332e1-196">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="332e1-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-heroku-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="332e1-198">a.</span><span class="sxs-lookup"><span data-stu-id="332e1-198">a.</span></span> <span data-ttu-id="332e1-199">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="332e1-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="332e1-200">b.</span><span class="sxs-lookup"><span data-stu-id="332e1-200">b.</span></span> <span data-ttu-id="332e1-201">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="332e1-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="332e1-202">c.</span><span class="sxs-lookup"><span data-stu-id="332e1-202">c.</span></span> <span data-ttu-id="332e1-203">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="332e1-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="332e1-204">d.</span><span class="sxs-lookup"><span data-stu-id="332e1-204">d.</span></span> <span data-ttu-id="332e1-205">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="332e1-205">Click **Create**.</span></span>
 
### <a name="creating-a-heroku-test-user"></a><span data-ttu-id="332e1-206">Tworzenie użytkownika testowego Heroku</span><span class="sxs-lookup"><span data-stu-id="332e1-206">Creating a Heroku test user</span></span>

<span data-ttu-id="332e1-207">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Heroku.</span><span class="sxs-lookup"><span data-stu-id="332e1-207">In this section, you create a user called Britta Simon in Heroku.</span></span> <span data-ttu-id="332e1-208">Heroku obsługę w czasie, który jest domyślnie włączona.</span><span class="sxs-lookup"><span data-stu-id="332e1-208">Heroku supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="332e1-209">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="332e1-209">There is no action item for you in this section.</span></span> <span data-ttu-id="332e1-210">Nowy użytkownik jest tworzony podczas uzyskiwania dostępu do Heroku, jeśli użytkownik nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="332e1-210">A new user is created when accessing Heroku if the user doesn't exist yet.</span></span> <span data-ttu-id="332e1-211">Po zainicjowaniu obsługi konta, użytkownik końcowy otrzyma wiadomość e-mail weryfikacji i musi zostać kliknij łącze potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="332e1-211">After the account is provisioned, the end user receives a verification email and needs to click the acknowledgement link.</span></span>

>[!NOTE]
><span data-ttu-id="332e1-212">Jeśli trzeba ręcznie utworzyć użytkownika, należy skontaktować się [zespołem pomocy technicznej klienta Heroku](https://www.heroku.com/support).</span><span class="sxs-lookup"><span data-stu-id="332e1-212">If you need to create a user manually, you need to contact the [Heroku Client support team](https://www.heroku.com/support).</span></span>
>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="332e1-213">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="332e1-213">Assigning the Azure AD test user</span></span>

<span data-ttu-id="332e1-214">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Heroku.</span><span class="sxs-lookup"><span data-stu-id="332e1-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Heroku.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="332e1-216">**Aby przypisać Simona Britta Heroku, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="332e1-216">**To assign Britta Simon to Heroku, perform the following steps:**</span></span>

1. <span data-ttu-id="332e1-217">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="332e1-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="332e1-219">Na liście aplikacji zaznacz **Heroku**.</span><span class="sxs-lookup"><span data-stu-id="332e1-219">In the applications list, select **Heroku**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_app.png) 

3. <span data-ttu-id="332e1-221">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="332e1-221">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="332e1-223">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="332e1-223">Click **Add** button.</span></span> <span data-ttu-id="332e1-224">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="332e1-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="332e1-226">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="332e1-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="332e1-227">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="332e1-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="332e1-228">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="332e1-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="332e1-229">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="332e1-229">Testing single sign-on</span></span>

<span data-ttu-id="332e1-230">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="332e1-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="332e1-231">Po kliknięciu kafelka Heroku w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Heroku.</span><span class="sxs-lookup"><span data-stu-id="332e1-231">When you click the Heroku tile in the Access Panel, you should get automatically signed-on to your Heroku application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="332e1-232">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="332e1-232">Additional resources</span></span>

* [<span data-ttu-id="332e1-233">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="332e1-233">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="332e1-234">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="332e1-234">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_203.png
