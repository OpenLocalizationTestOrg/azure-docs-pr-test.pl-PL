---
title: 'Samouczek: Integracji Azure Active Directory z Kontiki | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Kontiki."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8d5e5413-da4c-40d8-b1d0-f03ecfef030b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 8c441656a1a52d1e1e75b7d0f7025f4331bf9dc1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kontiki"></a><span data-ttu-id="193e2-103">Samouczek: Integracji Azure Active Directory z Kontiki</span><span class="sxs-lookup"><span data-stu-id="193e2-103">Tutorial: Azure Active Directory integration with Kontiki</span></span>

<span data-ttu-id="193e2-104">Z tego samouczka dowiesz się integrowanie Kontiki z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="193e2-104">In this tutorial, you learn how to integrate Kontiki with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="193e2-105">Integracja z usługą Azure AD Kontiki zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="193e2-105">Integrating Kontiki with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="193e2-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Kontiki</span><span class="sxs-lookup"><span data-stu-id="193e2-106">You can control in Azure AD who has access to Kontiki</span></span>
- <span data-ttu-id="193e2-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Kontiki (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="193e2-107">You can enable your users to automatically get signed-on to Kontiki (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="193e2-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="193e2-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="193e2-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="193e2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="193e2-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="193e2-110">Prerequisites</span></span>

<span data-ttu-id="193e2-111">Aby skonfigurować integrację usługi Azure AD z Kontiki, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="193e2-111">To configure Azure AD integration with Kontiki, you need the following items:</span></span>

- <span data-ttu-id="193e2-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="193e2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="193e2-113">Kontiki logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="193e2-113">A Kontiki single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="193e2-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="193e2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="193e2-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="193e2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="193e2-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="193e2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="193e2-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="193e2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="193e2-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="193e2-118">Scenario description</span></span>
<span data-ttu-id="193e2-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="193e2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="193e2-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="193e2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="193e2-121">Dodawanie Kontiki z galerii</span><span class="sxs-lookup"><span data-stu-id="193e2-121">Adding Kontiki from the gallery</span></span>
2. <span data-ttu-id="193e2-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="193e2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kontiki-from-the-gallery"></a><span data-ttu-id="193e2-123">Dodawanie Kontiki z galerii</span><span class="sxs-lookup"><span data-stu-id="193e2-123">Adding Kontiki from the gallery</span></span>
<span data-ttu-id="193e2-124">Aby skonfigurować integrację usługi Azure AD Kontiki, należy dodać Kontiki z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="193e2-124">To configure the integration of Kontiki into Azure AD, you need to add Kontiki from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="193e2-125">**Aby dodać Kontiki z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="193e2-125">**To add Kontiki from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="193e2-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="193e2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="193e2-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="193e2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="193e2-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="193e2-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="193e2-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="193e2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="193e2-133">W polu wyszukiwania wpisz **Kontiki**.</span><span class="sxs-lookup"><span data-stu-id="193e2-133">In the search box, type **Kontiki**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kontiki-tutorial/tutorial_kontiki_search.png)

5. <span data-ttu-id="193e2-135">W panelu wyników wybierz **Kontiki**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="193e2-135">In the results panel, select **Kontiki**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kontiki-tutorial/tutorial_kontiki_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="193e2-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="193e2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="193e2-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Kontiki w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="193e2-138">In this section, you configure and test Azure AD single sign-on with Kontiki based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="193e2-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Kontiki jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="193e2-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kontiki is to a user in Azure AD.</span></span> <span data-ttu-id="193e2-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Kontiki musi się.</span><span class="sxs-lookup"><span data-stu-id="193e2-140">In other words, a link relationship between an Azure AD user and the related user in Kontiki needs to be established.</span></span>

<span data-ttu-id="193e2-141">W Kontiki, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="193e2-141">In Kontiki, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="193e2-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Kontiki, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="193e2-142">To configure and test Azure AD single sign-on with Kontiki, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="193e2-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="193e2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="193e2-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="193e2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="193e2-145">**[Tworzenie użytkownika testowego Kontiki](#creating-a-kontiki-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Kontiki połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="193e2-145">**[Creating a Kontiki test user](#creating-a-kontiki-test-user)** - to have a counterpart of Britta Simon in Kontiki that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="193e2-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="193e2-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="193e2-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="193e2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="193e2-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="193e2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="193e2-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Kontiki.</span><span class="sxs-lookup"><span data-stu-id="193e2-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kontiki application.</span></span>

<span data-ttu-id="193e2-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Kontiki, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="193e2-150">**To configure Azure AD single sign-on with Kontiki, perform the following steps:**</span></span>

1. <span data-ttu-id="193e2-151">W portalu Azure na **Kontiki** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="193e2-151">In the Azure portal, on the **Kontiki** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="193e2-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="193e2-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kontiki-tutorial/tutorial_kontiki_samlbase.png)

3. <span data-ttu-id="193e2-155">Na **Kontiki domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="193e2-155">On the **Kontiki Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kontiki-tutorial/tutorial_kontiki_url.png)

     <span data-ttu-id="193e2-157">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.mc.eval.kontiki.com`</span><span class="sxs-lookup"><span data-stu-id="193e2-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.mc.eval.kontiki.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="193e2-158">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="193e2-158">This value is not real.</span></span> <span data-ttu-id="193e2-159">Zaktualizuj tę wartość z adresem URL logowania rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="193e2-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="193e2-160">Skontaktuj się z [zespołem pomocy technicznej klienta Kontiki](http://customersupport.kontiki.com/enterprise/contactsupport.html) można uzyskać wartość.</span><span class="sxs-lookup"><span data-stu-id="193e2-160">Contact [Kontiki Client support team](http://customersupport.kontiki.com/enterprise/contactsupport.html) to get the value.</span></span> 
 
4. <span data-ttu-id="193e2-161">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="193e2-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kontiki-tutorial/tutorial_kontiki_certificate.png) 

5. <span data-ttu-id="193e2-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="193e2-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kontiki-tutorial/tutorial_general_400.png) 

6. <span data-ttu-id="193e2-165">Skonfigurować logowanie jednokrotne w **Kontiki** stronie, musisz wysłać pobrany **XML metadanych** do [zespołem pomocy technicznej Kontiki](http://customersupport.kontiki.com/enterprise/contactsupport.html).</span><span class="sxs-lookup"><span data-stu-id="193e2-165">To configure single sign-on on **Kontiki** side, you need to send the downloaded **Metadata XML** to [Kontiki support team](http://customersupport.kontiki.com/enterprise/contactsupport.html).</span></span> <span data-ttu-id="193e2-166">To ustawienie, aby były prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one wartość.</span><span class="sxs-lookup"><span data-stu-id="193e2-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="193e2-167">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="193e2-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="193e2-168">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="193e2-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="193e2-169">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="193e2-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="193e2-170">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="193e2-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="193e2-171">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="193e2-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="193e2-173">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="193e2-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="193e2-174">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="193e2-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kontiki-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="193e2-176">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="193e2-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kontiki-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="193e2-178">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="193e2-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kontiki-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="193e2-180">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="193e2-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kontiki-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="193e2-182">a.</span><span class="sxs-lookup"><span data-stu-id="193e2-182">a.</span></span> <span data-ttu-id="193e2-183">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="193e2-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="193e2-184">b.</span><span class="sxs-lookup"><span data-stu-id="193e2-184">b.</span></span> <span data-ttu-id="193e2-185">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="193e2-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="193e2-186">c.</span><span class="sxs-lookup"><span data-stu-id="193e2-186">c.</span></span> <span data-ttu-id="193e2-187">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="193e2-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="193e2-188">d.</span><span class="sxs-lookup"><span data-stu-id="193e2-188">d.</span></span> <span data-ttu-id="193e2-189">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="193e2-189">Click **Create**.</span></span>
 
### <a name="creating-a-kontiki-test-user"></a><span data-ttu-id="193e2-190">Tworzenie użytkownika testowego Kontiki</span><span class="sxs-lookup"><span data-stu-id="193e2-190">Creating a Kontiki test user</span></span>

<span data-ttu-id="193e2-191">Nie ma elementu akcji do skonfigurowania inicjowania obsługi administracyjnej Kontiki użytkownika.</span><span class="sxs-lookup"><span data-stu-id="193e2-191">There is no action item for you to configure user provisioning to Kontiki.</span></span> <span data-ttu-id="193e2-192">Gdy przypisany użytkownik próbuje zalogować się do Kontiki za pomocą panelu dostępu, Kontiki sprawdza, czy użytkownik istnieje.</span><span class="sxs-lookup"><span data-stu-id="193e2-192">When an assigned user tries to log in to Kontiki using the access panel, Kontiki checks whether the user exists.</span></span>  

>[!NOTE]
><span data-ttu-id="193e2-193">Jeśli nie jest Brak konta użytkownika dostępny jeszcze, są tworzone przez Kontiki.</span><span class="sxs-lookup"><span data-stu-id="193e2-193">If there is no user account available yet, it is automatically created by Kontiki.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="193e2-194">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="193e2-194">Assigning the Azure AD test user</span></span>

<span data-ttu-id="193e2-195">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Kontiki.</span><span class="sxs-lookup"><span data-stu-id="193e2-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kontiki.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="193e2-197">**Aby przypisać Simona Britta Kontiki, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="193e2-197">**To assign Britta Simon to Kontiki, perform the following steps:**</span></span>

1. <span data-ttu-id="193e2-198">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="193e2-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="193e2-200">Na liście aplikacji zaznacz **Kontiki**.</span><span class="sxs-lookup"><span data-stu-id="193e2-200">In the applications list, select **Kontiki**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kontiki-tutorial/tutorial_kontiki_app.png) 

3. <span data-ttu-id="193e2-202">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="193e2-202">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="193e2-204">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="193e2-204">Click **Add** button.</span></span> <span data-ttu-id="193e2-205">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="193e2-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="193e2-207">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="193e2-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="193e2-208">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="193e2-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="193e2-209">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="193e2-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="193e2-210">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="193e2-210">Testing single sign-on</span></span>

<span data-ttu-id="193e2-211">Celem tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="193e2-211">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="193e2-212">Po kliknięciu kafelka Kontiki w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Kontiki.</span><span class="sxs-lookup"><span data-stu-id="193e2-212">When you click the Kontiki tile in the Access Panel, you should get automatically signed-on to your Kontiki application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="193e2-213">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="193e2-213">Additional resources</span></span>

* [<span data-ttu-id="193e2-214">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="193e2-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="193e2-215">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="193e2-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kontiki-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kontiki-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kontiki-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kontiki-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kontiki-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kontiki-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kontiki-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kontiki-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kontiki-tutorial/tutorial_general_203.png

