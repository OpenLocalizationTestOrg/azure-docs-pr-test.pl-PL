---
title: 'Samouczek: Integracji Azure Active Directory z 23 wideo | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i 23 wideo."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5e73dd1d-3995-4a73-b9cf-1b2318d49cb3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: jeedes
ms.openlocfilehash: ffcd665506c21e25c84367af5b6a3afb8e319af7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-23-video"></a><span data-ttu-id="a2131-103">Samouczek: Integracji Azure Active Directory z 23 wideo</span><span class="sxs-lookup"><span data-stu-id="a2131-103">Tutorial: Azure Active Directory integration with 23 Video</span></span>

<span data-ttu-id="a2131-104">Z tego samouczka dowiesz się integrowanie 23 wideo z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a2131-104">In this tutorial, you learn how to integrate 23 Video with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a2131-105">Integrowanie 23 wideo z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="a2131-105">Integrating 23 Video with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a2131-106">Można kontrolować w usłudze Azure AD, który ma dostęp do wideo 23</span><span class="sxs-lookup"><span data-stu-id="a2131-106">You can control in Azure AD who has access to 23 Video</span></span>
- <span data-ttu-id="a2131-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do 23 wideo (logowanie jednokrotne) za pomocą ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2131-107">You can enable your users to automatically get signed-on to 23 Video (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a2131-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="a2131-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a2131-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a2131-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a2131-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a2131-110">Prerequisites</span></span>

<span data-ttu-id="a2131-111">Aby skonfigurować integrację usługi Azure AD z 23 wideo, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="a2131-111">To configure Azure AD integration with 23 Video, you need the following items:</span></span>

- <span data-ttu-id="a2131-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2131-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a2131-113">23 wideo jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="a2131-113">A 23 Video single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a2131-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="a2131-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a2131-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="a2131-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a2131-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="a2131-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a2131-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a2131-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a2131-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="a2131-118">Scenario description</span></span>
<span data-ttu-id="a2131-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="a2131-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a2131-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="a2131-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a2131-121">Dodawanie 23 wideo z galerii</span><span class="sxs-lookup"><span data-stu-id="a2131-121">Adding 23 Video from the gallery</span></span>
2. <span data-ttu-id="a2131-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="a2131-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-23-video-from-the-gallery"></a><span data-ttu-id="a2131-123">Dodawanie 23 wideo z galerii</span><span class="sxs-lookup"><span data-stu-id="a2131-123">Adding 23 Video from the gallery</span></span>
<span data-ttu-id="a2131-124">Aby skonfigurować integrację 23 wideo w usłudze Azure Active Directory, należy dodać 23 wideo z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="a2131-124">To configure the integration of 23 Video into Azure AD, you need to add 23 Video from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a2131-125">**Aby dodać 23 wideo z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="a2131-125">**To add 23 Video from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a2131-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="a2131-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="a2131-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="a2131-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a2131-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="a2131-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="a2131-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a2131-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="a2131-133">W polu wyszukiwania wpisz **23 wideo**.</span><span class="sxs-lookup"><span data-stu-id="a2131-133">In the search box, type **23 Video**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-23video-tutorial/tutorial_23video_search.png)

5. <span data-ttu-id="a2131-135">W panelu wyników wybierz **23 wideo**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="a2131-135">In the results panel, select **23 Video**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-23video-tutorial/tutorial_23video_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a2131-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="a2131-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a2131-138">W tej sekcji można skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z 23 wideo na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="a2131-138">In this section, you configure and test Azure AD single sign-on with 23 Video based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a2131-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednikiem 23 wideo jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a2131-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 23 Video is to a user in Azure AD.</span></span> <span data-ttu-id="a2131-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w 23 wideo musi się.</span><span class="sxs-lookup"><span data-stu-id="a2131-140">In other words, a link relationship between an Azure AD user and the related user in 23 Video needs to be established.</span></span>

<span data-ttu-id="a2131-141">23 wideo, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="a2131-141">In 23 Video, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a2131-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z 23 wideo, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="a2131-142">To configure and test Azure AD single sign-on with 23 Video, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a2131-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="a2131-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a2131-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="a2131-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a2131-145">**[Tworzenie użytkownika testowego 23 wideo](#creating-a-23-video-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta 23 wideo, która jest połączona z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a2131-145">**[Creating a 23 Video test user](#creating-a-23-video-test-user)** - to have a counterpart of Britta Simon in 23 Video that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a2131-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="a2131-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a2131-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="a2131-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a2131-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="a2131-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a2131-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w 23 aplikacji wideo.</span><span class="sxs-lookup"><span data-stu-id="a2131-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 23 Video application.</span></span>

<span data-ttu-id="a2131-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z 23 wideo, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="a2131-150">**To configure Azure AD single sign-on with 23 Video, perform the following steps:**</span></span>

1. <span data-ttu-id="a2131-151">W portalu Azure na **23 wideo** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="a2131-151">In the Azure portal, on the **23 Video** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="a2131-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="a2131-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-23video-tutorial/tutorial_23video_samlbase.png)

3. <span data-ttu-id="a2131-155">Na **23 Video domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a2131-155">On the **23 Video Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-23video-tutorial/tutorial_23video_url.png)

    <span data-ttu-id="a2131-157">a.</span><span class="sxs-lookup"><span data-stu-id="a2131-157">a.</span></span> <span data-ttu-id="a2131-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.23video.com`</span><span class="sxs-lookup"><span data-stu-id="a2131-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.23video.com`</span></span>

    <span data-ttu-id="a2131-159">b.</span><span class="sxs-lookup"><span data-stu-id="a2131-159">b.</span></span> <span data-ttu-id="a2131-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://www.23video.com/saml/trust/<uniqueid>`</span><span class="sxs-lookup"><span data-stu-id="a2131-160">In the **Identifier** textbox, type a URL using the following pattern: `https://www.23video.com/saml/trust/<uniqueid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a2131-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="a2131-161">These values are not real.</span></span> <span data-ttu-id="a2131-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="a2131-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a2131-163">Skontaktuj się z [23 zespołem pomocy technicznej klienta wideo](mailto:support@23company.com) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="a2131-163">Contact [23 Video Client support team](mailto:support@23company.com) to get these values.</span></span> 
 
4. <span data-ttu-id="a2131-164">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="a2131-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-23video-tutorial/tutorial_23video_certificate.png) 

5. <span data-ttu-id="a2131-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a2131-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-23video-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a2131-168">Na **23 konfiguracji wideo** kliknij **skonfigurować wideo 23** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="a2131-168">On the **23 Video Configuration** section, click **Configure 23 Video** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a2131-169">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="a2131-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-23video-tutorial/tutorial_23video_configure.png) 

7. <span data-ttu-id="a2131-171">Skonfigurować logowanie jednokrotne w **23 wideo** stronie, musisz wysłać pobrany **certyfikatu (Base64)**, **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** do [23 zespołem pomocy technicznej wideo](mailto:support@23company.com).</span><span class="sxs-lookup"><span data-stu-id="a2131-171">To configure single sign-on on **23 Video** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [23 Video support team](mailto:support@23company.com).</span></span> 


> [!TIP]
> <span data-ttu-id="a2131-172">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="a2131-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a2131-173">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="a2131-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a2131-174">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a2131-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a2131-175">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2131-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="a2131-176">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="a2131-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="a2131-178">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="a2131-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a2131-179">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="a2131-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-23video-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a2131-181">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="a2131-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-23video-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a2131-183">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a2131-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-23video-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a2131-185">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a2131-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-23video-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a2131-187">a.</span><span class="sxs-lookup"><span data-stu-id="a2131-187">a.</span></span> <span data-ttu-id="a2131-188">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a2131-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a2131-189">b.</span><span class="sxs-lookup"><span data-stu-id="a2131-189">b.</span></span> <span data-ttu-id="a2131-190">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a2131-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a2131-191">c.</span><span class="sxs-lookup"><span data-stu-id="a2131-191">c.</span></span> <span data-ttu-id="a2131-192">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="a2131-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a2131-193">d.</span><span class="sxs-lookup"><span data-stu-id="a2131-193">d.</span></span> <span data-ttu-id="a2131-194">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="a2131-194">Click **Create**.</span></span>
 
### <a name="creating-a-23-video-test-user"></a><span data-ttu-id="a2131-195">Tworzenie użytkownika testowego 23 wideo</span><span class="sxs-lookup"><span data-stu-id="a2131-195">Creating a 23 Video test user</span></span>

<span data-ttu-id="a2131-196">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta 23 wideo.</span><span class="sxs-lookup"><span data-stu-id="a2131-196">The objective of this section is to create a user called Britta Simon in 23 Video.</span></span>

<span data-ttu-id="a2131-197">**Aby utworzyć użytkownika o nazwie Simona Britta 23 wideo, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="a2131-197">**To create a user called Britta Simon in 23 Video, perform the following steps:**</span></span>

1. <span data-ttu-id="a2131-198">Logowanie się do witryny firmy 23 wideo jako administrator.</span><span class="sxs-lookup"><span data-stu-id="a2131-198">Sign on to your 23 Video company site as administrator.</span></span>

2. <span data-ttu-id="a2131-199">Przejdź do **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="a2131-199">Go to **Settings**.</span></span>
 
3. <span data-ttu-id="a2131-200">W **użytkowników** kliknij **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="a2131-200">In **Users** section, click **Configure**.</span></span>
   
    ![Przypisz użytkownika][400]

4. <span data-ttu-id="a2131-202">Kliknij przycisk **dodać nowego użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="a2131-202">Click **Add a new user**.</span></span> 
   
    ![Przypisz użytkownika][401]

5. <span data-ttu-id="a2131-204">W **Poproś kogoś dołączenie do tej lokacji** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a2131-204">In the **Invite someone to join this site** section, perform the following steps:</span></span>
   
    ![Przypisz użytkownika][402]

    <span data-ttu-id="a2131-206">a.</span><span class="sxs-lookup"><span data-stu-id="a2131-206">a.</span></span> <span data-ttu-id="a2131-207">W **adresy E-mail** tekstowym, wpisz adres e-mail Simona Britta w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a2131-207">In the **E-mail addresses** textbox, type Britta Simon's email address in Azure AD.</span></span>  
 
    <span data-ttu-id="a2131-208">b.</span><span class="sxs-lookup"><span data-stu-id="a2131-208">b.</span></span> <span data-ttu-id="a2131-209">Kliknij przycisk **Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="a2131-209">Click **Add the user**.</span></span>   

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a2131-210">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2131-210">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a2131-211">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do 23 wideo.</span><span class="sxs-lookup"><span data-stu-id="a2131-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 23 Video.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="a2131-213">**Aby przypisać Simona Britta 23 wideo, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="a2131-213">**To assign Britta Simon to 23 Video, perform the following steps:**</span></span>

1. <span data-ttu-id="a2131-214">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="a2131-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="a2131-216">Na liście aplikacji zaznacz **23 wideo**.</span><span class="sxs-lookup"><span data-stu-id="a2131-216">In the applications list, select **23 Video**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-23video-tutorial/tutorial_23video_app.png) 

3. <span data-ttu-id="a2131-218">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="a2131-218">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="a2131-220">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a2131-220">Click **Add** button.</span></span> <span data-ttu-id="a2131-221">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a2131-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="a2131-223">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="a2131-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a2131-224">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a2131-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a2131-225">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a2131-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a2131-226">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="a2131-226">Testing single sign-on</span></span>

<span data-ttu-id="a2131-227">Celem tej sekcji służy do testowania konfigurację usługi Azure AD z logowania jednokrotnego za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="a2131-227">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="a2131-228">Po kliknięciu kafelka 23 wideo w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do 23 aplikacji wideo.</span><span class="sxs-lookup"><span data-stu-id="a2131-228">When you click the 23 Video tile in the Access Panel, you should get automatically signed-on to your 23 Video application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a2131-229">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="a2131-229">Additional resources</span></span>

* [<span data-ttu-id="a2131-230">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a2131-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a2131-231">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a2131-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-23video-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-23video-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-23video-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-23video-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-23video-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-23video-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-23video-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-23video-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-23video-tutorial/tutorial_general_203.png

[400]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_10.png
[401]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_11.png
[402]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_12.png
