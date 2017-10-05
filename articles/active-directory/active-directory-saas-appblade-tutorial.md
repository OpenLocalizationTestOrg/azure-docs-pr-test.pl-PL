---
title: 'Samouczek: Integracji Azure Active Directory z AppBlade | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i AppBlade."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3360d7aa-6518-4f99-88bd-b7f7258183e8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 7820a70b34b6d25ba81b17c472159d08904335d1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-appblade"></a><span data-ttu-id="2d490-103">Samouczek: Integracji Azure Active Directory z AppBlade</span><span class="sxs-lookup"><span data-stu-id="2d490-103">Tutorial: Azure Active Directory integration with AppBlade</span></span>

<span data-ttu-id="2d490-104">Z tego samouczka dowiesz się integrowanie AppBlade z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2d490-104">In this tutorial, you learn how to integrate AppBlade with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2d490-105">Integracja z usługą Azure AD AppBlade zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="2d490-105">Integrating AppBlade with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2d490-106">Można kontrolować w usłudze Azure AD, który ma dostęp do AppBlade</span><span class="sxs-lookup"><span data-stu-id="2d490-106">You can control in Azure AD who has access to AppBlade</span></span>
- <span data-ttu-id="2d490-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do AppBlade (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d490-107">You can enable your users to automatically get signed-on to AppBlade (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2d490-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="2d490-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="2d490-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2d490-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2d490-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2d490-110">Prerequisites</span></span>

<span data-ttu-id="2d490-111">Aby skonfigurować integrację usługi Azure AD z AppBlade, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="2d490-111">To configure Azure AD integration with AppBlade, you need the following items:</span></span>

- <span data-ttu-id="2d490-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d490-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2d490-113">AppBlade jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="2d490-113">An AppBlade single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2d490-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="2d490-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2d490-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="2d490-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2d490-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="2d490-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2d490-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2d490-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2d490-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="2d490-118">Scenario description</span></span>
<span data-ttu-id="2d490-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="2d490-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2d490-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="2d490-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2d490-121">Dodawanie AppBlade z galerii</span><span class="sxs-lookup"><span data-stu-id="2d490-121">Adding AppBlade from the gallery</span></span>
2. <span data-ttu-id="2d490-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="2d490-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-appblade-from-the-gallery"></a><span data-ttu-id="2d490-123">Dodawanie AppBlade z galerii</span><span class="sxs-lookup"><span data-stu-id="2d490-123">Adding AppBlade from the gallery</span></span>
<span data-ttu-id="2d490-124">Aby skonfigurować integrację usługi Azure AD AppBlade, należy dodać AppBlade z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="2d490-124">To configure the integration of AppBlade into Azure AD, you need to add AppBlade from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2d490-125">**Aby dodać AppBlade z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="2d490-125">**To add AppBlade from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2d490-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="2d490-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="2d490-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="2d490-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2d490-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="2d490-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="2d490-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2d490-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="2d490-133">W polu wyszukiwania wpisz **AppBlade**.</span><span class="sxs-lookup"><span data-stu-id="2d490-133">In the search box, type **AppBlade**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_search.png)

5. <span data-ttu-id="2d490-135">W panelu wyników wybierz **AppBlade**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="2d490-135">In the results panel, select **AppBlade**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2d490-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="2d490-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2d490-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z AppBlade na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="2d490-138">In this section, you configure and test Azure AD single sign-on with AppBlade based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2d490-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w AppBlade jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2d490-139">For single sign-on to work, Azure AD needs to know what the counterpart user in AppBlade is to a user in Azure AD.</span></span> <span data-ttu-id="2d490-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w AppBlade musi się.</span><span class="sxs-lookup"><span data-stu-id="2d490-140">In other words, a link relationship between an Azure AD user and the related user in AppBlade needs to be established.</span></span>

<span data-ttu-id="2d490-141">W AppBlade, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="2d490-141">In AppBlade, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="2d490-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z AppBlade, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="2d490-142">To configure and test Azure AD single sign-on with AppBlade, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2d490-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="2d490-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2d490-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="2d490-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2d490-145">**[Tworzenie użytkownika testowego AppBlade](#creating-an-appblade-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta AppBlade połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2d490-145">**[Creating an AppBlade test user](#creating-an-appblade-test-user)** - to have a counterpart of Britta Simon in AppBlade that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="2d490-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="2d490-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2d490-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="2d490-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2d490-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="2d490-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2d490-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji AppBlade.</span><span class="sxs-lookup"><span data-stu-id="2d490-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your AppBlade application.</span></span>

<span data-ttu-id="2d490-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z AppBlade, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="2d490-150">**To configure Azure AD single sign-on with AppBlade, perform the following steps:**</span></span>

1. <span data-ttu-id="2d490-151">W portalu Azure na **AppBlade** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="2d490-151">In the Azure portal, on the **AppBlade** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="2d490-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="2d490-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_samlbase.png)

3. <span data-ttu-id="2d490-155">Na **AppBlade domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="2d490-155">On the **AppBlade Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_url.png)

    <span data-ttu-id="2d490-157">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.appblade.com/saml/<tenantid>`</span><span class="sxs-lookup"><span data-stu-id="2d490-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.appblade.com/saml/<tenantid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2d490-158">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="2d490-158">This value is not real.</span></span> <span data-ttu-id="2d490-159">Zaktualizuj tę wartość z adresem URL logowania rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="2d490-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="2d490-160">Skontaktuj się z [zespołem pomocy technicznej klienta AppBlade](mailto:support@appblade.com) można uzyskać wartość.</span><span class="sxs-lookup"><span data-stu-id="2d490-160">Contact [AppBlade Client support team](mailto:support@appblade.com) to get the value.</span></span> 
 
4. <span data-ttu-id="2d490-161">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="2d490-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_certificate.png) 

5. <span data-ttu-id="2d490-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="2d490-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-appblade-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2d490-165">Skonfigurować logowanie jednokrotne w **AppBlade** stronie, musisz wysłać pobrany **XML metadanych** do [zespołem pomocy technicznej AppBlade](mailto:support@appblade.com).</span><span class="sxs-lookup"><span data-stu-id="2d490-165">To configure single sign-on on **AppBlade** side, you need to send the downloaded **Metadata XML** to [AppBlade support team](mailto:support@appblade.com).</span></span> <span data-ttu-id="2d490-166">Ponadto, poproś go o skonfigurowanie **adres URL wystawcy logowania jednokrotnego** jako `https://appblade.com/saml`.</span><span class="sxs-lookup"><span data-stu-id="2d490-166">Also, please ask them to configure the **SSO Issuer URL** as `https://appblade.com/saml`.</span></span> <span data-ttu-id="2d490-167">To ustawienie jest wymagane dla rejestracji jednokrotnej do pracy.</span><span class="sxs-lookup"><span data-stu-id="2d490-167">This setting is required for single sign-on to work.</span></span>


> [!TIP]
> <span data-ttu-id="2d490-168">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="2d490-168">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2d490-169">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="2d490-169">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2d490-170">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2d490-170">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2d490-171">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d490-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="2d490-172">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="2d490-172">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="2d490-174">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="2d490-174">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2d490-175">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="2d490-175">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-appblade-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2d490-177">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="2d490-177">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-appblade-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2d490-179">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2d490-179">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-appblade-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2d490-181">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="2d490-181">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-appblade-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2d490-183">a.</span><span class="sxs-lookup"><span data-stu-id="2d490-183">a.</span></span> <span data-ttu-id="2d490-184">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2d490-184">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2d490-185">b.</span><span class="sxs-lookup"><span data-stu-id="2d490-185">b.</span></span> <span data-ttu-id="2d490-186">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2d490-186">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2d490-187">c.</span><span class="sxs-lookup"><span data-stu-id="2d490-187">c.</span></span> <span data-ttu-id="2d490-188">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="2d490-188">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2d490-189">d.</span><span class="sxs-lookup"><span data-stu-id="2d490-189">d.</span></span> <span data-ttu-id="2d490-190">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="2d490-190">Click **Create**.</span></span>
 
### <a name="creating-an-appblade-test-user"></a><span data-ttu-id="2d490-191">Tworzenie użytkownika testowego AppBlade</span><span class="sxs-lookup"><span data-stu-id="2d490-191">Creating an AppBlade test user</span></span>

<span data-ttu-id="2d490-192">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w AppBlade.</span><span class="sxs-lookup"><span data-stu-id="2d490-192">The objective of this section is to create a user called Britta Simon in AppBlade.</span></span> <span data-ttu-id="2d490-193">AppBlade obsługę w czasie, który jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="2d490-193">AppBlade supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="2d490-194">**Upewnij się, że nazwa domeny jest skonfigurowany z AppBlade dla Inicjowanie obsługi użytkowników. Po wykonaniu tylko przez użytkownika w czasie inicjowania obsługi administracyjnej działa.**</span><span class="sxs-lookup"><span data-stu-id="2d490-194">**Make sure that your domain name is configured with AppBlade for user provisioning. After that only the just-in-time user provisioning works.**</span></span>

<span data-ttu-id="2d490-195">Jeśli użytkownik ma adres e-mail, kończąc domeny skonfigurowanych przez AppBlade dla tego konta, a następnie użytkownika zostaną automatycznie dołączone jako element członkowski z poziomem uprawnień, które można określić konto, które jest jednym z "Basic" (podstawowe użytkownika, który można zainstalować tylko aplikacje) , "Członek zespołu" (użytkownik, który można przesłać nowe wersje aplikacji i zarządzanie projektami), lub "Administrator" (Administrator o pełnych uprawnieniach uprawnienia do konta).</span><span class="sxs-lookup"><span data-stu-id="2d490-195">If the user has an email address ending with the domain configured by AppBlade for your account, then the user will automatically join the account as a member with the permission level you specify, which is one of "Basic" (a basic user who can only install applications), "Team Member" (a user who can upload new app versions and manage projects), or "Administrator" (full admin privileges to the account).</span></span> <span data-ttu-id="2d490-196">Zwykle będzie jedna wybierz Basic i promować użytkowników ręcznie za pośrednictwem identyfikator logowania administratora (AppBlade musi wcześniej skonfigurowane logowania administratora pocztą e-mail lub podwyższyć poziom użytkownika w imieniu klienta po logowania).</span><span class="sxs-lookup"><span data-stu-id="2d490-196">Normally one would choose Basic and then promote users manually via an Admin login (AppBlade needs to configure either an email-based admin login in advance or promote a user on behalf of the customer after login).</span></span>

<span data-ttu-id="2d490-197">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="2d490-197">There is no action item for you in this section.</span></span> <span data-ttu-id="2d490-198">Nowy użytkownik został utworzony podczas próby dostępu AppBlade, jeśli go jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="2d490-198">A new user is created during an attempt to access AppBlade if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="2d490-199">Jeśli trzeba ręcznie utworzyć użytkownika, należy skontaktować się [zespołem pomocy technicznej AppBlade](mailto:support@appblade.com).</span><span class="sxs-lookup"><span data-stu-id="2d490-199">If you need to create a user manually, you need to contact the [AppBlade support team](mailto:support@appblade.com).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2d490-200">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d490-200">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2d490-201">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu AppBlade.</span><span class="sxs-lookup"><span data-stu-id="2d490-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to AppBlade.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="2d490-203">**Aby przypisać Simona Britta AppBlade, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="2d490-203">**To assign Britta Simon to AppBlade, perform the following steps:**</span></span>

1. <span data-ttu-id="2d490-204">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="2d490-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="2d490-206">Na liście aplikacji zaznacz **AppBlade**.</span><span class="sxs-lookup"><span data-stu-id="2d490-206">In the applications list, select **AppBlade**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_app.png) 

3. <span data-ttu-id="2d490-208">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="2d490-208">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="2d490-210">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="2d490-210">Click **Add** button.</span></span> <span data-ttu-id="2d490-211">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2d490-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="2d490-213">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="2d490-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2d490-214">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2d490-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2d490-215">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2d490-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2d490-216">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="2d490-216">Testing single sign-on</span></span>

<span data-ttu-id="2d490-217">Celem tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="2d490-217">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="2d490-218">Po kliknięciu kafelka AppBlade w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji AppBlade.</span><span class="sxs-lookup"><span data-stu-id="2d490-218">When you click the AppBlade tile in the Access Panel, you should get automatically signed-on to your AppBlade application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="2d490-219">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="2d490-219">Additional resources</span></span>

* [<span data-ttu-id="2d490-220">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2d490-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2d490-221">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2d490-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_203.png

