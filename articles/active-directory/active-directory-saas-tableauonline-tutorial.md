---
title: "Samouczek: Integracja usługi Azure Active Directory z usługą Tableau Online | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Tableau Online."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d4b1149-ba3b-4f4e-8bce-9791316b730d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: 443fab1198a91a4d5749e6421f7b8603fc75a81e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-online"></a><span data-ttu-id="35cc1-103">Samouczek: Integracja usługi Azure Active Directory z usługą Tableau Online</span><span class="sxs-lookup"><span data-stu-id="35cc1-103">Tutorial: Azure Active Directory integration with Tableau Online</span></span>

<span data-ttu-id="35cc1-104">Z tego samouczka dowiesz się integrowanie Tableau Online z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="35cc1-104">In this tutorial, you learn how to integrate Tableau Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="35cc1-105">Integrowanie Tableau Online z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="35cc1-105">Integrating Tableau Online with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="35cc1-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Tableau Online</span><span class="sxs-lookup"><span data-stu-id="35cc1-106">You can control in Azure AD who has access to Tableau Online</span></span>
- <span data-ttu-id="35cc1-107">Umożliwia użytkownikom automatycznie pobrać zalogowane Tableau online (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="35cc1-107">You can enable your users to automatically get signed-on to Tableau Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="35cc1-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="35cc1-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="35cc1-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="35cc1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="35cc1-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="35cc1-110">Prerequisites</span></span>

<span data-ttu-id="35cc1-111">Aby skonfigurować integrację usługi Azure AD z Tableau Online, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="35cc1-111">To configure Azure AD integration with Tableau Online, you need the following items:</span></span>

- <span data-ttu-id="35cc1-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="35cc1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="35cc1-113">Tableau Online logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="35cc1-113">A Tableau Online single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="35cc1-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="35cc1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="35cc1-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="35cc1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="35cc1-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="35cc1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="35cc1-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="35cc1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="35cc1-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="35cc1-118">Scenario description</span></span>
<span data-ttu-id="35cc1-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="35cc1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="35cc1-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="35cc1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="35cc1-121">Dodawanie Tableau Online z poziomu galerii</span><span class="sxs-lookup"><span data-stu-id="35cc1-121">Adding Tableau Online from the gallery</span></span>
2. <span data-ttu-id="35cc1-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="35cc1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tableau-online-from-the-gallery"></a><span data-ttu-id="35cc1-123">Dodawanie Tableau Online z poziomu galerii</span><span class="sxs-lookup"><span data-stu-id="35cc1-123">Adding Tableau Online from the gallery</span></span>
<span data-ttu-id="35cc1-124">Aby skonfigurować integrację Tableau online z usługą Azure AD, należy dodać do listy zarządzanych aplikacji SaaS Tableau Online z poziomu galerii.</span><span class="sxs-lookup"><span data-stu-id="35cc1-124">To configure the integration of Tableau Online into Azure AD, you need to add Tableau Online from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="35cc1-125">**Aby dodać Tableau Online z poziomu galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="35cc1-125">**To add Tableau Online from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="35cc1-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="35cc1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="35cc1-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="35cc1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="35cc1-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="35cc1-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="35cc1-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="35cc1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="35cc1-133">W polu wyszukiwania wpisz **Tableau Online**.</span><span class="sxs-lookup"><span data-stu-id="35cc1-133">In the search box, type **Tableau Online**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_search.png)

5. <span data-ttu-id="35cc1-135">W panelu wyników wybierz **Tableau Online**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="35cc1-135">In the results panel, select **Tableau Online**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="35cc1-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="35cc1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="35cc1-138">W tej sekcji można skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Tableau Online na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="35cc1-138">In this section, you configure and test Azure AD single sign-on with Tableau Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="35cc1-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Tableau w trybie Online jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="35cc1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Tableau Online is to a user in Azure AD.</span></span> <span data-ttu-id="35cc1-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i danemu użytkownikowi w trybie Online Tableau musi określone.</span><span class="sxs-lookup"><span data-stu-id="35cc1-140">In other words, a link relationship between an Azure AD user and the related user in Tableau Online needs to be established.</span></span>

<span data-ttu-id="35cc1-141">W Tableau w trybie Online, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="35cc1-141">In Tableau Online, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="35cc1-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Tableau Online, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="35cc1-142">To configure and test Azure AD single sign-on with Tableau Online, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="35cc1-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="35cc1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="35cc1-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="35cc1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="35cc1-145">**[Tworzenie użytkownika testowego Tableau Online](#creating-a-tableau-online-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Tableau Online, które jest połączone z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="35cc1-145">**[Creating a Tableau Online test user](#creating-a-tableau-online-test-user)** - to have a counterpart of Britta Simon in Tableau Online that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="35cc1-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="35cc1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="35cc1-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="35cc1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="35cc1-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="35cc1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="35cc1-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w trybie Online Tableau aplikacji.</span><span class="sxs-lookup"><span data-stu-id="35cc1-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Tableau Online application.</span></span>

<span data-ttu-id="35cc1-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Tableau Online, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="35cc1-150">**To configure Azure AD single sign-on with Tableau Online, perform the following steps:**</span></span>

1. <span data-ttu-id="35cc1-151">W portalu Azure na **Tableau Online** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="35cc1-151">In the Azure portal, on the **Tableau Online** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="35cc1-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="35cc1-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_samlbase.png)

3. <span data-ttu-id="35cc1-155">Na **Tableau Online domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="35cc1-155">On the **Tableau Online Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_url.png)
    
    <span data-ttu-id="35cc1-157">a.</span><span class="sxs-lookup"><span data-stu-id="35cc1-157">a.</span></span> <span data-ttu-id="35cc1-158">W **adres URL logowania** tekstowym, wpisz adres URL:`https://sso.online.tableau.com`</span><span class="sxs-lookup"><span data-stu-id="35cc1-158">In the **Sign-on URL** textbox, type the URL: `https://sso.online.tableau.com`</span></span>

    <span data-ttu-id="35cc1-159">b.</span><span class="sxs-lookup"><span data-stu-id="35cc1-159">b.</span></span> <span data-ttu-id="35cc1-160">W **identyfikator** tekstowym, wpisz adres URL:`https://sso.online.tableau.com/public/sp/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="35cc1-160">In the **Identifier** textbox, type the URL: `https://sso.online.tableau.com/public/sp/<instancename>`</span></span>

4. <span data-ttu-id="35cc1-161">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="35cc1-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_certificate.png) 

5. <span data-ttu-id="35cc1-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="35cc1-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauonline-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="35cc1-165">W oknie innej przeglądarki logowanie do aplikacji Tableau w trybie Online.</span><span class="sxs-lookup"><span data-stu-id="35cc1-165">In a different browser window, sign-on to your Tableau Online application.</span></span> <span data-ttu-id="35cc1-166">Przejdź do **ustawienia** , a następnie **uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="35cc1-166">Go to **Settings** and then **Authentication**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_09.png)
    
7. <span data-ttu-id="35cc1-168">Aby włączyć SAML, w obszarze **typy uwierzytelniania** sekcji.</span><span class="sxs-lookup"><span data-stu-id="35cc1-168">To enable SAML, Under **Authentication Types** section.</span></span> <span data-ttu-id="35cc1-169">Sprawdź **rejestracji jednokrotnej z SAML** wyboru.</span><span class="sxs-lookup"><span data-stu-id="35cc1-169">Check the **Single sign-on with SAML** checkbox.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_12.png)

8. <span data-ttu-id="35cc1-171">Przewiń w dół do **Importowanie pliku metadanych do Tableau Online** sekcji.</span><span class="sxs-lookup"><span data-stu-id="35cc1-171">Scroll down until **Import metadata file into Tableau Online** section.</span></span>  <span data-ttu-id="35cc1-172">Kliknij przycisk Przeglądaj i zaimportować plik metadanych, które zostały pobrane z usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="35cc1-172">Click Browse and import the metadata file you have downloaded from Azure AD.</span></span> <span data-ttu-id="35cc1-173">Następnie kliknij przycisk **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="35cc1-173">Then, click **Apply**.</span></span>
   
   ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_13.png)

9. <span data-ttu-id="35cc1-175">W **odpowiada potwierdzenia** sekcję należy wstawić z odpowiednią nazwą potwierdzenia dostawcy tożsamości dla **adres e-mail**, **imię**, i **nazwisko**.</span><span class="sxs-lookup"><span data-stu-id="35cc1-175">In the **Match assertions** section, insert the corresponding Identity Provider assertion name for **email address**, **first name**, and **last name**.</span></span> <span data-ttu-id="35cc1-176">Aby wyświetlić te informacje z usługi Azure AD:</span><span class="sxs-lookup"><span data-stu-id="35cc1-176">To get this information from Azure AD:</span></span> 
  
    <span data-ttu-id="35cc1-177">a.</span><span class="sxs-lookup"><span data-stu-id="35cc1-177">a.</span></span> <span data-ttu-id="35cc1-178">W portalu Azure, przejdź **Tableau Online** strony integracja aplikacji.</span><span class="sxs-lookup"><span data-stu-id="35cc1-178">In the Azure portal, go on the **Tableau Online** application integration page.</span></span>
    
    <span data-ttu-id="35cc1-179">b.</span><span class="sxs-lookup"><span data-stu-id="35cc1-179">b.</span></span> <span data-ttu-id="35cc1-180">W obszarze atrybuty wybierz **"wyświetlić i edytować wszystkie atrybuty użytkowników"** pola wyboru.</span><span class="sxs-lookup"><span data-stu-id="35cc1-180">In the attributes section, Select the **"view and edit all other user attributes"** checkbox.</span></span> 
    
   ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauonline-tutorial/attributesection.png)
      
    <span data-ttu-id="35cc1-182">c.</span><span class="sxs-lookup"><span data-stu-id="35cc1-182">c.</span></span> <span data-ttu-id="35cc1-183">Skopiuj wartość przestrzeni nazw dla tych atrybutów: givenname, poczty e-mail i nazwisko, korzystając z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="35cc1-183">Copy the namespace value for these attributes: givenname, email and surname by using the following steps:</span></span>

   ![Azure AD rejestracji jednokrotnej](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_10.png)
    
    <span data-ttu-id="35cc1-185">d.</span><span class="sxs-lookup"><span data-stu-id="35cc1-185">d.</span></span> <span data-ttu-id="35cc1-186">Kliknij przycisk **user.givenname** wartości</span><span class="sxs-lookup"><span data-stu-id="35cc1-186">Click **user.givenname** value</span></span> 
    
    <span data-ttu-id="35cc1-187">e.</span><span class="sxs-lookup"><span data-stu-id="35cc1-187">e.</span></span> <span data-ttu-id="35cc1-188">Skopiuj wartości z **przestrzeni nazw** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="35cc1-188">Copy the value from the **namespace** textbox.</span></span>

   ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauonline-tutorial/attributesection2.png)

    <span data-ttu-id="35cc1-190">f.</span><span class="sxs-lookup"><span data-stu-id="35cc1-190">f.</span></span> <span data-ttu-id="35cc1-191">Aby skopiować namesapce wartości poczty e-mail i nazwisko wykonaj te czynności.</span><span class="sxs-lookup"><span data-stu-id="35cc1-191">To copy the namesapce values for the email and surname follow the preceding steps.</span></span>

    <span data-ttu-id="35cc1-192">g.</span><span class="sxs-lookup"><span data-stu-id="35cc1-192">g.</span></span> <span data-ttu-id="35cc1-193">Przełącz się do aplikacji Tableau Online, a następnie ustaw **Tableau Online atrybuty** sekcji w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="35cc1-193">Switch to the Tableau Online application, then set the **Tableau Online Attributes** section as follows:</span></span>
     * <span data-ttu-id="35cc1-194">Adres e-mail: **poczty** lub **userprincipalname**</span><span class="sxs-lookup"><span data-stu-id="35cc1-194">Email: **mail** or **userprincipalname**</span></span>
     * <span data-ttu-id="35cc1-195">Imię: **givenname**</span><span class="sxs-lookup"><span data-stu-id="35cc1-195">First name: **givenname**</span></span>
     * <span data-ttu-id="35cc1-196">Nazwisko: **nazwisko**</span><span class="sxs-lookup"><span data-stu-id="35cc1-196">Last name: **surname**</span></span>
   
   ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_14.png)

> [!TIP]
> <span data-ttu-id="35cc1-198">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="35cc1-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="35cc1-199">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="35cc1-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="35cc1-200">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="35cc1-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="35cc1-201">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="35cc1-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="35cc1-202">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="35cc1-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="35cc1-204">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="35cc1-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="35cc1-205">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="35cc1-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="35cc1-207">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="35cc1-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="35cc1-209">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="35cc1-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="35cc1-211">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="35cc1-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="35cc1-213">a.</span><span class="sxs-lookup"><span data-stu-id="35cc1-213">a.</span></span> <span data-ttu-id="35cc1-214">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="35cc1-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="35cc1-215">b.</span><span class="sxs-lookup"><span data-stu-id="35cc1-215">b.</span></span> <span data-ttu-id="35cc1-216">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="35cc1-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="35cc1-217">c.</span><span class="sxs-lookup"><span data-stu-id="35cc1-217">c.</span></span> <span data-ttu-id="35cc1-218">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="35cc1-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="35cc1-219">d.</span><span class="sxs-lookup"><span data-stu-id="35cc1-219">d.</span></span> <span data-ttu-id="35cc1-220">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="35cc1-220">Click **Create**.</span></span>
 
### <a name="creating-a-tableau-online-test-user"></a><span data-ttu-id="35cc1-221">Tworzenie użytkownika testowego Tableau Online</span><span class="sxs-lookup"><span data-stu-id="35cc1-221">Creating a Tableau Online test user</span></span>

<span data-ttu-id="35cc1-222">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta Tableau online.</span><span class="sxs-lookup"><span data-stu-id="35cc1-222">In this section, you create a user called Britta Simon in Tableau Online.</span></span>

1. <span data-ttu-id="35cc1-223">Na **Tableau Online**, kliknij przycisk **ustawienia** , a następnie **uwierzytelniania** sekcji.</span><span class="sxs-lookup"><span data-stu-id="35cc1-223">On **Tableau Online**, click **Settings** and then **Authentication** section.</span></span> <span data-ttu-id="35cc1-224">Przewiń w dół do **Wybieranie: Użytkownicy** sekcji.</span><span class="sxs-lookup"><span data-stu-id="35cc1-224">Scroll down to **Select Users** section.</span></span> <span data-ttu-id="35cc1-225">Kliknij przycisk **dodawania użytkowników** , a następnie **wprowadź adresy E-mail**.</span><span class="sxs-lookup"><span data-stu-id="35cc1-225">Click **Add Users** and then **Enter Email Addresses**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_15.png)
2. <span data-ttu-id="35cc1-227">Wybierz **Dodawanie użytkowników do uwierzytelniania rejestracji jednokrotnej (SSO)**.</span><span class="sxs-lookup"><span data-stu-id="35cc1-227">Select **Add users for single sign-on (SSO) authentication**.</span></span> <span data-ttu-id="35cc1-228">W **wprowadź adresy E-mail** Dodaj pole tekstowebritta.simon@contoso.com</span><span class="sxs-lookup"><span data-stu-id="35cc1-228">In the **Enter Email Addresses** textbox add britta.simon@contoso.com</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_11.png)
3. <span data-ttu-id="35cc1-230">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="35cc1-230">Click **Create**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="35cc1-231">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="35cc1-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="35cc1-232">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do Tableau Online.</span><span class="sxs-lookup"><span data-stu-id="35cc1-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Tableau Online.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="35cc1-234">**Aby przypisać Simona Britta Tableau Online, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="35cc1-234">**To assign Britta Simon to Tableau Online, perform the following steps:**</span></span>

1. <span data-ttu-id="35cc1-235">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="35cc1-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="35cc1-237">Na liście aplikacji zaznacz **Tableau Online**.</span><span class="sxs-lookup"><span data-stu-id="35cc1-237">In the applications list, select **Tableau Online**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_app.png) 

3. <span data-ttu-id="35cc1-239">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="35cc1-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="35cc1-241">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="35cc1-241">Click **Add** button.</span></span> <span data-ttu-id="35cc1-242">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="35cc1-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="35cc1-244">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="35cc1-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="35cc1-245">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="35cc1-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="35cc1-246">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="35cc1-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="35cc1-247">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="35cc1-247">Testing single sign-on</span></span>

<span data-ttu-id="35cc1-248">Celem tej sekcji służy do testowania konfigurację usługi Azure AD z logowania jednokrotnego za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="35cc1-248">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="35cc1-249">Po kliknięciu kafelka Tableau Online w panelu dostępu użytkownik powinien uzyskać automatycznie zalogowane do aplikacji Tableau Online.</span><span class="sxs-lookup"><span data-stu-id="35cc1-249">When you click the Tableau Online tile in the Access Panel, you should get automatically signed-on to your Tableau Online application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="35cc1-250">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="35cc1-250">Additional resources</span></span>

* [<span data-ttu-id="35cc1-251">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="35cc1-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="35cc1-252">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="35cc1-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_203.png

