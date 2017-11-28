---
title: 'Samouczek: Integracji Azure Active Directory z CompetencyIQ | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i CompetencyIQ."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e262bf7e-cc7d-4d0e-aea7-861f00d8837d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: ad3cec3de9034ddab2161952620d31540ae51978
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-competencyiq"></a><span data-ttu-id="62254-103">Samouczek: Integracji Azure Active Directory z CompetencyIQ</span><span class="sxs-lookup"><span data-stu-id="62254-103">Tutorial: Azure Active Directory integration with CompetencyIQ</span></span>

<span data-ttu-id="62254-104">Z tego samouczka dowiesz się integrowanie CompetencyIQ z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="62254-104">In this tutorial, you learn how to integrate CompetencyIQ with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="62254-105">Integracja z usługą Azure AD CompetencyIQ zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="62254-105">Integrating CompetencyIQ with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="62254-106">Można kontrolować w usłudze Azure AD, który ma dostęp do CompetencyIQ</span><span class="sxs-lookup"><span data-stu-id="62254-106">You can control in Azure AD who has access to CompetencyIQ</span></span>
- <span data-ttu-id="62254-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do CompetencyIQ (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="62254-107">You can enable your users to automatically get signed-on to CompetencyIQ (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="62254-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="62254-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="62254-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="62254-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="62254-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="62254-110">Prerequisites</span></span>

<span data-ttu-id="62254-111">Aby skonfigurować integrację usługi Azure AD z CompetencyIQ, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="62254-111">To configure Azure AD integration with CompetencyIQ, you need the following items:</span></span>

- <span data-ttu-id="62254-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="62254-112">An Azure AD subscription</span></span>
- <span data-ttu-id="62254-113">CompetencyIQ logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="62254-113">A CompetencyIQ single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="62254-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="62254-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="62254-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="62254-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="62254-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="62254-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="62254-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="62254-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="62254-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="62254-118">Scenario description</span></span>
<span data-ttu-id="62254-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="62254-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="62254-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="62254-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="62254-121">Dodawanie CompetencyIQ z galerii</span><span class="sxs-lookup"><span data-stu-id="62254-121">Adding CompetencyIQ from the gallery</span></span>
2. <span data-ttu-id="62254-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="62254-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-competencyiq-from-the-gallery"></a><span data-ttu-id="62254-123">Dodawanie CompetencyIQ z galerii</span><span class="sxs-lookup"><span data-stu-id="62254-123">Adding CompetencyIQ from the gallery</span></span>
<span data-ttu-id="62254-124">Aby skonfigurować integrację usługi Azure AD CompetencyIQ, należy dodać CompetencyIQ z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="62254-124">To configure the integration of CompetencyIQ into Azure AD, you need to add CompetencyIQ from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="62254-125">**Aby dodać CompetencyIQ z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="62254-125">**To add CompetencyIQ from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="62254-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="62254-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="62254-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="62254-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="62254-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="62254-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="62254-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="62254-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="62254-133">W polu wyszukiwania wpisz **CompetencyIQ**.</span><span class="sxs-lookup"><span data-stu-id="62254-133">In the search box, type **CompetencyIQ**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_search.png)

5. <span data-ttu-id="62254-135">W panelu wyników wybierz **CompetencyIQ**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="62254-135">In the results panel, select **CompetencyIQ**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="62254-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="62254-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="62254-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z CompetencyIQ na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="62254-138">In this section, you configure and test Azure AD single sign-on with CompetencyIQ based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="62254-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w CompetencyIQ jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="62254-139">For single sign-on to work, Azure AD needs to know what the counterpart user in CompetencyIQ is to a user in Azure AD.</span></span> <span data-ttu-id="62254-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w CompetencyIQ musi się.</span><span class="sxs-lookup"><span data-stu-id="62254-140">In other words, a link relationship between an Azure AD user and the related user in CompetencyIQ needs to be established.</span></span>

<span data-ttu-id="62254-141">W CompetencyIQ, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="62254-141">In CompetencyIQ, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="62254-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z CompetencyIQ, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="62254-142">To configure and test Azure AD single sign-on with CompetencyIQ, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="62254-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="62254-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="62254-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="62254-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="62254-145">**[Tworzenie użytkownika testowego CompetencyIQ](#creating-a-competencyiq-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta CompetencyIQ połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="62254-145">**[Creating a CompetencyIQ test user](#creating-a-competencyiq-test-user)** - to have a counterpart of Britta Simon in CompetencyIQ that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="62254-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="62254-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="62254-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="62254-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="62254-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="62254-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="62254-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji CompetencyIQ.</span><span class="sxs-lookup"><span data-stu-id="62254-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your CompetencyIQ application.</span></span>

<span data-ttu-id="62254-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z CompetencyIQ, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="62254-150">**To configure Azure AD single sign-on with CompetencyIQ, perform the following steps:**</span></span>

1. <span data-ttu-id="62254-151">W portalu Azure na **CompetencyIQ** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="62254-151">In the Azure portal, on the **CompetencyIQ** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="62254-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="62254-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_samlbase.png)

3. <span data-ttu-id="62254-155">Na **CompetencyIQ domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="62254-155">On the **CompetencyIQ Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_url1.png)

    <span data-ttu-id="62254-157">a.</span><span class="sxs-lookup"><span data-stu-id="62254-157">a.</span></span> <span data-ttu-id="62254-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<customer>.competencyiq.com/`</span><span class="sxs-lookup"><span data-stu-id="62254-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<customer>.competencyiq.com/`</span></span>
    
    <span data-ttu-id="62254-159">b.</span><span class="sxs-lookup"><span data-stu-id="62254-159">b.</span></span> <span data-ttu-id="62254-160">W **identyfikator** tekstowym, wpisz adres URL:`https://www.competencyiq.com/`</span><span class="sxs-lookup"><span data-stu-id="62254-160">In the **Identifier** textbox, type the URL: `https://www.competencyiq.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="62254-161">Wartość adres URL logowania jest nie rzeczywistym tak zaktualizować to o rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="62254-161">The Sign-on URL value is not real so update this with actual Sign-On URL.</span></span> <span data-ttu-id="62254-162">Skontaktuj się z [zespołem pomocy technicznej klienta CompetencyIQ](https://www.competencyiq.com/) to uzyskać.</span><span class="sxs-lookup"><span data-stu-id="62254-162">Contact [CompetencyIQ Client support team](https://www.competencyiq.com/) to get this.</span></span> 
 
4. <span data-ttu-id="62254-163">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="62254-163">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_certificate.png) 

5. <span data-ttu-id="62254-165">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="62254-165">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-competencyiq-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="62254-167">Na **konfiguracji CompetencyIQ** , kliknij przycisk **skonfigurować CompetencyIQ** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="62254-167">On the **CompetencyIQ Configuration** section, click **Configure CompetencyIQ** to open **Configure sign-on** window.</span></span> <span data-ttu-id="62254-168">Kopiuj **SAML identyfikator jednostki**, i **SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="62254-168">Copy the **SAML Entity ID**, and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_configure.png) 

7. <span data-ttu-id="62254-170">Skonfigurować logowanie jednokrotne w **CompetencyIQ** stronie, musisz wysłać pobrany **XML metadanych**, **identyfikator jednostki SAML** i **SAML logowania jednokrotnego usługi pojedynczej Adres URL** do [zespołem pomocy technicznej CompetencyIQ](https://www.competencyiq.com/).</span><span class="sxs-lookup"><span data-stu-id="62254-170">To configure single sign-on on **CompetencyIQ** side, you need to send the downloaded **Metadata XML**, **SAML Entity ID** and **SAML Single Sign-On Service URL** to [CompetencyIQ support team](https://www.competencyiq.com/).</span></span> <span data-ttu-id="62254-171">To ustawienie, aby były prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one wartość.</span><span class="sxs-lookup"><span data-stu-id="62254-171">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="62254-172">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="62254-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="62254-173">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="62254-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="62254-174">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="62254-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="62254-175">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="62254-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="62254-176">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="62254-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="62254-178">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="62254-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="62254-179">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="62254-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-competencyiq-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="62254-181">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="62254-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-competencyiq-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="62254-183">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="62254-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-competencyiq-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="62254-185">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="62254-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-competencyiq-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="62254-187">a.</span><span class="sxs-lookup"><span data-stu-id="62254-187">a.</span></span> <span data-ttu-id="62254-188">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="62254-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="62254-189">b.</span><span class="sxs-lookup"><span data-stu-id="62254-189">b.</span></span> <span data-ttu-id="62254-190">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="62254-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="62254-191">c.</span><span class="sxs-lookup"><span data-stu-id="62254-191">c.</span></span> <span data-ttu-id="62254-192">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="62254-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="62254-193">d.</span><span class="sxs-lookup"><span data-stu-id="62254-193">d.</span></span> <span data-ttu-id="62254-194">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="62254-194">Click **Create**.</span></span>
 
### <a name="creating-a-competencyiq-test-user"></a><span data-ttu-id="62254-195">Tworzenie użytkownika testowego CompetencyIQ</span><span class="sxs-lookup"><span data-stu-id="62254-195">Creating a CompetencyIQ test user</span></span>

<span data-ttu-id="62254-196">Aby umożliwić użytkownikom usługi Azure AD zalogować się do CompetencyIQ, musi być przygotowana do CompetencyIQ.</span><span class="sxs-lookup"><span data-stu-id="62254-196">To enable Azure AD users to log in to CompetencyIQ, they must be provisioned into CompetencyIQ.</span></span> <span data-ttu-id="62254-197">Skontaktuj się z [zespołem pomocy technicznej CompetencyIQ](https://www.competencyiq.com/) może tworzyć użytkowników w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="62254-197">Contact [CompetencyIQ support team](https://www.competencyiq.com/) to create users in the application.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="62254-198">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="62254-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="62254-199">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu CompetencyIQ.</span><span class="sxs-lookup"><span data-stu-id="62254-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to CompetencyIQ.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="62254-201">**Aby przypisać Simona Britta CompetencyIQ, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="62254-201">**To assign Britta Simon to CompetencyIQ, perform the following steps:**</span></span>

1. <span data-ttu-id="62254-202">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="62254-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="62254-204">Na liście aplikacji zaznacz **CompetencyIQ**.</span><span class="sxs-lookup"><span data-stu-id="62254-204">In the applications list, select **CompetencyIQ**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_app.png) 

3. <span data-ttu-id="62254-206">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="62254-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="62254-208">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="62254-208">Click **Add** button.</span></span> <span data-ttu-id="62254-209">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="62254-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="62254-211">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="62254-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="62254-212">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="62254-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="62254-213">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="62254-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="62254-214">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="62254-214">Testing single sign-on</span></span>

<span data-ttu-id="62254-215">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="62254-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="62254-216">Po kliknięciu kafelka CompetencyIQ w panelu dostępu, należy pobrać automatycznie zalogowania do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="62254-216">When you click the CompetencyIQ tile in the Access Panel, you should get automatically logged into the application.</span></span>
<span data-ttu-id="62254-217">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="62254-217">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="62254-218">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="62254-218">Additional resources</span></span>

* [<span data-ttu-id="62254-219">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="62254-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="62254-220">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="62254-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_203.png

