---
title: 'Samouczek: Integracji Azure Active Directory z Intralinks | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Intralinks."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 147f2bf9-166b-402e-adc4-4b19dd336883
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: ee7fd5b88ac806104002ffb41af11bab4fd1b2dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intralinks"></a><span data-ttu-id="ff3d6-103">Samouczek: Integracji Azure Active Directory z Intralinks</span><span class="sxs-lookup"><span data-stu-id="ff3d6-103">Tutorial: Azure Active Directory integration with Intralinks</span></span>

<span data-ttu-id="ff3d6-104">Z tego samouczka dowiesz się integrowanie Intralinks z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ff3d6-104">In this tutorial, you learn how to integrate Intralinks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ff3d6-105">Integracja z usługą Azure AD Intralinks zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="ff3d6-105">Integrating Intralinks with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ff3d6-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Intralinks</span><span class="sxs-lookup"><span data-stu-id="ff3d6-106">You can control in Azure AD who has access to Intralinks</span></span>
- <span data-ttu-id="ff3d6-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Intralinks (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ff3d6-107">You can enable your users to automatically get signed-on to Intralinks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ff3d6-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="ff3d6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ff3d6-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ff3d6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ff3d6-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ff3d6-110">Prerequisites</span></span>

<span data-ttu-id="ff3d6-111">Aby skonfigurować integrację usługi Azure AD z Intralinks, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="ff3d6-111">To configure Azure AD integration with Intralinks, you need the following items:</span></span>

- <span data-ttu-id="ff3d6-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ff3d6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ff3d6-113">Intralinks logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="ff3d6-113">An Intralinks single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ff3d6-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ff3d6-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="ff3d6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ff3d6-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ff3d6-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ff3d6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ff3d6-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="ff3d6-118">Scenario description</span></span>
<span data-ttu-id="ff3d6-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ff3d6-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="ff3d6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ff3d6-121">Dodawanie Intralinks z galerii</span><span class="sxs-lookup"><span data-stu-id="ff3d6-121">Adding Intralinks from the gallery</span></span>
2. <span data-ttu-id="ff3d6-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="ff3d6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intralinks-from-the-gallery"></a><span data-ttu-id="ff3d6-123">Dodawanie Intralinks z galerii</span><span class="sxs-lookup"><span data-stu-id="ff3d6-123">Adding Intralinks from the gallery</span></span>
<span data-ttu-id="ff3d6-124">Aby skonfigurować integrację usługi Azure AD Intralinks, należy dodać Intralinks z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-124">To configure the integration of Intralinks into Azure AD, you need to add Intralinks from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ff3d6-125">**Aby dodać Intralinks z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="ff3d6-125">**To add Intralinks from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ff3d6-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="ff3d6-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ff3d6-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="ff3d6-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="ff3d6-133">W polu wyszukiwania wpisz **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-133">In the search box, type **Intralinks**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_search.png)

5. <span data-ttu-id="ff3d6-135">W panelu wyników wybierz **Intralinks**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-135">In the results panel, select **Intralinks**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ff3d6-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="ff3d6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ff3d6-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Intralinks w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-138">In this section, you configure and test Azure AD single sign-on with Intralinks based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ff3d6-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Intralinks jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Intralinks is to a user in Azure AD.</span></span> <span data-ttu-id="ff3d6-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Intralinks musi się.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-140">In other words, a link relationship between an Azure AD user and the related user in Intralinks needs to be established.</span></span>

<span data-ttu-id="ff3d6-141">W Intralinks, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-141">In Intralinks, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ff3d6-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Intralinks, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="ff3d6-142">To configure and test Azure AD single sign-on with Intralinks, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ff3d6-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ff3d6-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ff3d6-145">**[Tworzenie użytkownika testowego Intralinks](#creating-an-intralinks-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Intralinks połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-145">**[Creating an Intralinks test user](#creating-an-intralinks-test-user)** - to have a counterpart of Britta Simon in Intralinks that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ff3d6-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ff3d6-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ff3d6-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ff3d6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ff3d6-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Intralinks.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Intralinks application.</span></span>

<span data-ttu-id="ff3d6-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Intralinks, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="ff3d6-150">**To configure Azure AD single sign-on with Intralinks, perform the following steps:**</span></span>

1. <span data-ttu-id="ff3d6-151">W portalu Azure na **Intralinks** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-151">In the Azure portal, on the **Intralinks** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="ff3d6-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_samlbase.png)

3. <span data-ttu-id="ff3d6-155">Na **Intralinks domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ff3d6-155">On the **Intralinks Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_url.png)

    <span data-ttu-id="ff3d6-157">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`</span><span class="sxs-lookup"><span data-stu-id="ff3d6-157">In the **Sign-on URL** textbox, type a URL using the following pattern:  `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ff3d6-158">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-158">This value is not real.</span></span> <span data-ttu-id="ff3d6-159">Zaktualizuj tę wartość przy rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="ff3d6-160">Skontaktuj się z [zespołem pomocy technicznej klienta Intralinks](https://www.intralinks.com/contact-1) aby zyskać tę wartość.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-160">Contact [Intralinks Client support team](https://www.intralinks.com/contact-1) to get this value.</span></span> 
 
4. <span data-ttu-id="ff3d6-161">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_certificate.png) 

5. <span data-ttu-id="ff3d6-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-intralinks-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ff3d6-165">Do konfigurowania rejestracji jednokrotnej na **Intralinks** stronie, musisz wysłać pobrany **XML metadanych** [Intralinks obsługuje zespołu](https://www.intralinks.com/contact-1).</span><span class="sxs-lookup"><span data-stu-id="ff3d6-165">To configure single sign-on on **Intralinks** side, you need to send the downloaded **Metadata XML** [Intralinks support team](https://www.intralinks.com/contact-1).</span></span> <span data-ttu-id="ff3d6-166">To ustawienie, aby były prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one wartość.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="ff3d6-167">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="ff3d6-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ff3d6-168">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ff3d6-169">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ff3d6-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ff3d6-170">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ff3d6-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="ff3d6-171">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="ff3d6-173">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="ff3d6-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ff3d6-174">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ff3d6-176">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ff3d6-178">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ff3d6-180">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ff3d6-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ff3d6-182">a.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-182">a.</span></span> <span data-ttu-id="ff3d6-183">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ff3d6-184">b.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-184">b.</span></span> <span data-ttu-id="ff3d6-185">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ff3d6-186">c.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-186">c.</span></span> <span data-ttu-id="ff3d6-187">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ff3d6-188">d.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-188">d.</span></span> <span data-ttu-id="ff3d6-189">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-189">Click **Create**.</span></span>
 
### <a name="creating-an-intralinks-test-user"></a><span data-ttu-id="ff3d6-190">Tworzenie użytkownika testowego Intralinks</span><span class="sxs-lookup"><span data-stu-id="ff3d6-190">Creating an Intralinks test user</span></span>

<span data-ttu-id="ff3d6-191">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Intralinks.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-191">In this section, you create a user called Britta Simon in Intralinks.</span></span> <span data-ttu-id="ff3d6-192">We współpracy z [Intralinks obsługuje zespołu](https://www.intralinks.com/contact-1) Aby dodać użytkowników do platformy Intralinks.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-192">Please work with [Intralinks support team](https://www.intralinks.com/contact-1) to add the users in the Intralinks platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ff3d6-193">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ff3d6-193">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ff3d6-194">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Intralinks.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Intralinks.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="ff3d6-196">**Aby przypisać Simona Britta Intralinks, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="ff3d6-196">**To assign Britta Simon to Intralinks, perform the following steps:**</span></span>

1. <span data-ttu-id="ff3d6-197">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="ff3d6-199">Na liście aplikacji zaznacz **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-199">In the applications list, select **Intralinks**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_app.png) 

3. <span data-ttu-id="ff3d6-201">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-201">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="ff3d6-203">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-203">Click **Add** button.</span></span> <span data-ttu-id="ff3d6-204">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="ff3d6-206">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ff3d6-207">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ff3d6-208">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-208">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="add-intralinks-via-or-elite-application"></a><span data-ttu-id="ff3d6-209">Dodaj aplikację Intralinks za pośrednictwem lub Elite</span><span class="sxs-lookup"><span data-stu-id="ff3d6-209">Add Intralinks VIA or Elite application</span></span>

<span data-ttu-id="ff3d6-210">Intralinks używa tej samej platformy tożsamości logowania jednokrotnego dla wszystkich innych aplikacji Intralinks z wyjątkiem aplikacji węzła transakcji.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-210">Intralinks uses the same SSO identity platform for all other Intralinks applications excluding Deal Nexus application.</span></span> <span data-ttu-id="ff3d6-211">Dlatego jeśli zamierzasz korzystać z innych aplikacji Intralinks następnie najpierw należy skonfigurować logowanie Jednokrotne dla jednej aplikacji głównej Intralinks przy użyciu procedury opisanej powyżej.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-211">So if you plan to use any other Intralinks application then first you have to configure SSO for one Primary Intralinks application using the procedure described above.</span></span>

<span data-ttu-id="ff3d6-212">Następnie można wykonać poniżej procedurą, aby dodać inną Intralinks aplikację w dzierżawie, które mogą korzystać z tej aplikacji głównej dla logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-212">After that you can follow the below procedure to add another Intralinks application in your tenant which can leverage this primary application for SSO.</span></span> 

>[!NOTE]
><span data-ttu-id="ff3d6-213">Ta funkcja jest dostępna tylko dla usługi Azure AD Premium SKU klientów i nie jest dostępna dla klientów bezpłatna lub podstawowy SKU.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-213">This feature is available only to Azure AD Premium SKU Customers and not available for Free or Basic SKU customers.</span></span>

1. <span data-ttu-id="ff3d6-214">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-214">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]


2. <span data-ttu-id="ff3d6-216">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-216">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ff3d6-217">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-217">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="ff3d6-219">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-219">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="ff3d6-221">W polu wyszukiwania wpisz **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-221">In the search box, type **Intralinks**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_search.png)

5. <span data-ttu-id="ff3d6-223">Na **Intralinks Dodaj aplikację** należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ff3d6-223">On **Intralinks Add app** perform the following steps:</span></span>

    ![Dodawanie aplikacji Intralinks za pośrednictwem lub Elite](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_addapp.png)

    <span data-ttu-id="ff3d6-225">a.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-225">a.</span></span> <span data-ttu-id="ff3d6-226">W **nazwa** pole tekstowe, wprowadź odpowiednie nazwy aplikacji, np. **Intralinks Elite**.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-226">In **Name** textbox, enter appropriate name of the application e.g. **Intralinks Elite**.</span></span>

    <span data-ttu-id="ff3d6-227">b.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-227">b.</span></span> <span data-ttu-id="ff3d6-228">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-228">Click **Add** button.</span></span>

6.  <span data-ttu-id="ff3d6-229">W portalu Azure na **Intralinks** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-229">In the Azure portal, on the **Intralinks** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

7. <span data-ttu-id="ff3d6-231">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **połączonej logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-231">On the **Single sign-on** dialog, select **Mode** as **Linked Sign-on**.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_linkedsignon.png)

8. <span data-ttu-id="ff3d6-233">Pobierz SP zainicjował rejestracji Jednokrotnej adres URL [zespołu Intralinks](https://www.intralinks.com/contact-1) stosowania Intralinks i wprowadź go w **Konfiguruj adres URL logowania** jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-233">Get the the SP Initiated SSO URL from [Intralinks team](https://www.intralinks.com/contact-1) for the other Intralinks application and enter it in **Configure Sign-on URL** as shown below.</span></span> 
    
     ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_customappurl.png)
    
     <span data-ttu-id="ff3d6-235">W polu tekstowym na adres URL logowania wpisz adres URL używany przez użytkowników do logowania jednokrotnego do aplikacji Intralinks przy użyciu następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="ff3d6-235">In the Sign On URL textbox, type the URL used by your users to sign-on to your Intralinks application using the following pattern:</span></span>
   
    `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`

9. <span data-ttu-id="ff3d6-236">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-236">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-intralinks-tutorial/tutorial_general_400.png)

10. <span data-ttu-id="ff3d6-238">Przypisz aplikację w grupach użytkowników lub, jak pokazano w sekcji  **[przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-238">Assign the application to user or groups as shown in the section **[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)**.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="ff3d6-239">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ff3d6-239">Testing single sign-on</span></span>

<span data-ttu-id="ff3d6-240">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-240">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ff3d6-241">Po kliknięciu kafelka Intralinks w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Intralinks.</span><span class="sxs-lookup"><span data-stu-id="ff3d6-241">When you click the Intralinks tile in the Access Panel, you should get automatically signed-on to your Intralinks application.</span></span>
<span data-ttu-id="ff3d6-242">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ff3d6-242">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ff3d6-243">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="ff3d6-243">Additional resources</span></span>

* [<span data-ttu-id="ff3d6-244">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ff3d6-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ff3d6-245">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ff3d6-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_203.png

