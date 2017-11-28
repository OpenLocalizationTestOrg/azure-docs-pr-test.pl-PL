---
title: 'Samouczek: Integracji Azure Active Directory z InTime | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i InTime."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d4e2c6e1-ae5d-4d2c-8ffc-1b24534d376a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: jeedes
ms.openlocfilehash: 4bb22c92ad7f6963be6ca15073f7f01da99ba2bb
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intime"></a><span data-ttu-id="644fc-103">Samouczek: Integracji Azure Active Directory z InTime</span><span class="sxs-lookup"><span data-stu-id="644fc-103">Tutorial: Azure Active Directory integration with InTime</span></span>

<span data-ttu-id="644fc-104">Z tego samouczka dowiesz się integrowanie InTime z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="644fc-104">In this tutorial, you learn how to integrate InTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="644fc-105">Integracja z usługą Azure AD InTime zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="644fc-105">Integrating InTime with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="644fc-106">Można kontrolować w usłudze Azure AD, który ma dostęp do InTime.</span><span class="sxs-lookup"><span data-stu-id="644fc-106">You can control in Azure AD who has access to InTime.</span></span>
- <span data-ttu-id="644fc-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do InTime (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="644fc-107">You can enable your users to automatically get signed-on to InTime (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="644fc-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="644fc-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="644fc-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="644fc-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="644fc-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="644fc-110">Prerequisites</span></span>

<span data-ttu-id="644fc-111">Aby skonfigurować integrację usługi Azure AD z InTime, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="644fc-111">To configure Azure AD integration with InTime, you need the following items:</span></span>

- <span data-ttu-id="644fc-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="644fc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="644fc-113">InTime logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="644fc-113">A InTime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="644fc-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="644fc-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="644fc-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="644fc-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="644fc-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="644fc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="644fc-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="644fc-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="644fc-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="644fc-118">Scenario description</span></span>
<span data-ttu-id="644fc-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="644fc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="644fc-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="644fc-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="644fc-121">Dodawanie InTime z galerii</span><span class="sxs-lookup"><span data-stu-id="644fc-121">Adding InTime from the gallery</span></span>
2. <span data-ttu-id="644fc-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="644fc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intime-from-the-gallery"></a><span data-ttu-id="644fc-123">Dodawanie InTime z galerii</span><span class="sxs-lookup"><span data-stu-id="644fc-123">Adding InTime from the gallery</span></span>
<span data-ttu-id="644fc-124">Aby skonfigurować integrację usługi Azure AD InTime, należy dodać InTime z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="644fc-124">To configure the integration of InTime into Azure AD, you need to add InTime from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="644fc-125">**Aby dodać InTime z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="644fc-125">**To add InTime from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="644fc-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="644fc-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Przycisk usługi Azure Active Directory][1]

2. <span data-ttu-id="644fc-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="644fc-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="644fc-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="644fc-129">Then go to **All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa][2]
    
3. <span data-ttu-id="644fc-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="644fc-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Nowy przycisk aplikacji][3]

4. <span data-ttu-id="644fc-133">W polu wyszukiwania wpisz **InTime**, wybierz pozycję **InTime** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="644fc-133">In the search box, type **InTime**, select **InTime** from result panel then click **Add** button to add the application.</span></span>

    ![InTime na liście wyników](./media/active-directory-saas-intime-tutorial/tutorial_intime_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="644fc-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="644fc-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="644fc-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z InTime w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="644fc-136">In this section, you configure and test Azure AD single sign-on with InTime based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="644fc-137">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w InTime jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="644fc-137">For single sign-on to work, Azure AD needs to know what the counterpart user in InTime is to a user in Azure AD.</span></span> <span data-ttu-id="644fc-138">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w InTime musi się.</span><span class="sxs-lookup"><span data-stu-id="644fc-138">In other words, a link relationship between an Azure AD user and the related user in InTime needs to be established.</span></span>

<span data-ttu-id="644fc-139">W InTime, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="644fc-139">In InTime, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="644fc-140">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z InTime, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="644fc-140">To configure and test Azure AD single sign-on with InTime, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="644fc-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="644fc-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="644fc-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="644fc-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="644fc-143">**[Tworzenie użytkownika testowego InTime](#create-a-intime-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta InTime połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="644fc-143">**[Create a InTime test user](#create-a-intime-test-user)** - to have a counterpart of Britta Simon in InTime that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="644fc-144">**[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="644fc-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="644fc-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="644fc-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="644fc-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="644fc-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="644fc-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w InTime aplikacji.</span><span class="sxs-lookup"><span data-stu-id="644fc-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your InTime application.</span></span>

<span data-ttu-id="644fc-148">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z InTime, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="644fc-148">**To configure Azure AD single sign-on with InTime, perform the following steps:**</span></span>

1. <span data-ttu-id="644fc-149">W portalu Azure na **InTime** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="644fc-149">In the Azure portal, on the **InTime** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="644fc-151">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="644fc-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-intime-tutorial/tutorial_intime_samlbase.png)

3. <span data-ttu-id="644fc-153">Na **InTime domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="644fc-153">On the **InTime Domain and URLs** section, perform the following steps:</span></span>

    ![Adresy URL i domeny inTime pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-intime-tutorial/tutorial_intime_url.png)

    <span data-ttu-id="644fc-155">a.</span><span class="sxs-lookup"><span data-stu-id="644fc-155">a.</span></span> <span data-ttu-id="644fc-156">W **adres URL logowania** tekstowym, wpisz adres URL:`https://intime6.intimesoft.com/mytime/login/login.xhtml`</span><span class="sxs-lookup"><span data-stu-id="644fc-156">In the **Sign-on URL** textbox, type the URL: `https://intime6.intimesoft.com/mytime/login/login.xhtml`</span></span>

    <span data-ttu-id="644fc-157">b.</span><span class="sxs-lookup"><span data-stu-id="644fc-157">b.</span></span> <span data-ttu-id="644fc-158">W **identyfikator** tekstowym, wpisz adres URL:`https://auth.intimesoft.com/auth/realms/master`</span><span class="sxs-lookup"><span data-stu-id="644fc-158">In the **Identifier** textbox, type the URL: `https://auth.intimesoft.com/auth/realms/master`</span></span>

4. <span data-ttu-id="644fc-159">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="644fc-159">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Łącze pobierania certyfikatu](./media/active-directory-saas-intime-tutorial/tutorial_intime_certificate.png) 

5. <span data-ttu-id="644fc-161">Aplikacja InTime oczekuje potwierdzenia języka SAML w określonym formacie, musisz dodać mapowania atrybutu niestandardowego do konfiguracji atrybuty tokenu SAML.</span><span class="sxs-lookup"><span data-stu-id="644fc-161">Your InTime application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="644fc-162">Poniższy zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="644fc-162">The following screenshot shows an example for this.</span></span> <span data-ttu-id="644fc-163">Wartość domyślna **identyfikator użytkownika** jest **user.userprincipalname** , ale InTime oczekuje to być mapowane z adresu e-mail użytkownika.</span><span class="sxs-lookup"><span data-stu-id="644fc-163">The default value of **User Identifier** is **user.userprincipalname** but InTime expects this to be mapped with the user's email address.</span></span> <span data-ttu-id="644fc-164">W przypadku którego można użyć **user.mail** atrybutu z listy lub użyj wartości atrybutu odpowiednie na podstawie konfiguracji organizacji</span><span class="sxs-lookup"><span data-stu-id="644fc-164">For that you can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration</span></span> 

    ![Konfigurowanie atrybutów](./media/active-directory-saas-intime-tutorial/tutorial_intime_attribute.png)

6. <span data-ttu-id="644fc-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="644fc-166">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-intime-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="644fc-168">Na **InTime konfiguracji** kliknij **skonfigurować InTime** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="644fc-168">On the **InTime Configuration** section, click **Configure InTime** to open **Configure sign-on** window.</span></span> <span data-ttu-id="644fc-169">Kopiuj **Sign-Out adresu URL i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="644fc-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![InTime konfiguracji](./media/active-directory-saas-intime-tutorial/tutorial_intime_configure.png) 

8. <span data-ttu-id="644fc-171">Skonfigurować logowanie jednokrotne w **InTime** stronie, musisz wysłać pobrany **XML metadanych**, **Sign-Out adresu URL i SAML pojedynczy znak na adres URL usługi** do [zespołem pomocy technicznej InTime](mailto:hdollard@intimesoft.com).</span><span class="sxs-lookup"><span data-stu-id="644fc-171">To configure single sign-on on **InTime** side, you need to send the downloaded **Metadata XML**, **Sign-Out URL, and SAML Single Sign-On Service URL** to [InTime support team](mailto:hdollard@intimesoft.com).</span></span> <span data-ttu-id="644fc-172">To ustawienie, aby były prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one wartość.</span><span class="sxs-lookup"><span data-stu-id="644fc-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="644fc-173">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="644fc-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="644fc-174">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="644fc-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="644fc-175">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="644fc-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="644fc-176">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="644fc-176">Create an Azure AD test user</span></span>

<span data-ttu-id="644fc-177">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="644fc-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="644fc-179">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="644fc-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="644fc-180">W portalu Azure, w okienku po lewej stronie kliknij **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="644fc-180">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-intime-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="644fc-182">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="644fc-182">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-intime-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="644fc-184">Aby otworzyć **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** w górnej części **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="644fc-184">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Przycisk Dodaj](./media/active-directory-saas-intime-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="644fc-186">W **użytkownika** okna dialogowego wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="644fc-186">In the **User** dialog box, perform the following steps:</span></span>

    ![Okno dialogowe użytkownika](./media/active-directory-saas-intime-tutorial/create_aaduser_04.png)

    <span data-ttu-id="644fc-188">a.</span><span class="sxs-lookup"><span data-stu-id="644fc-188">a.</span></span> <span data-ttu-id="644fc-189">W **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="644fc-189">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="644fc-190">b.</span><span class="sxs-lookup"><span data-stu-id="644fc-190">b.</span></span> <span data-ttu-id="644fc-191">W **nazwy użytkownika** wpisz adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="644fc-191">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="644fc-192">c.</span><span class="sxs-lookup"><span data-stu-id="644fc-192">c.</span></span> <span data-ttu-id="644fc-193">Wybierz **Pokaż hasło** pole wyboru, a następnie zanotuj wartość, która jest wyświetlana w **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="644fc-193">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="644fc-194">d.</span><span class="sxs-lookup"><span data-stu-id="644fc-194">d.</span></span> <span data-ttu-id="644fc-195">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="644fc-195">Click **Create**.</span></span>
 
### <a name="create-a-intime-test-user"></a><span data-ttu-id="644fc-196">Tworzenie użytkownika testowego InTime</span><span class="sxs-lookup"><span data-stu-id="644fc-196">Create a InTime test user</span></span>

<span data-ttu-id="644fc-197">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w InTime.</span><span class="sxs-lookup"><span data-stu-id="644fc-197">In this section, you create a user called Britta Simon in InTime.</span></span> <span data-ttu-id="644fc-198">Praca z [zespołem pomocy technicznej InTime](mailto:hdollard@intimesoft.com) Aby dodać użytkowników do InTime platformy.</span><span class="sxs-lookup"><span data-stu-id="644fc-198">Work with [InTime support team](mailto:hdollard@intimesoft.com) to add the users in the InTime platform.</span></span> <span data-ttu-id="644fc-199">Użytkownicy muszą utworzyć i aktywowana, aby użyć rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="644fc-199">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="644fc-200">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="644fc-200">Assign the Azure AD test user</span></span>

<span data-ttu-id="644fc-201">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu InTime.</span><span class="sxs-lookup"><span data-stu-id="644fc-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to InTime.</span></span>

![Przypisanie roli użytkownika][200] 

<span data-ttu-id="644fc-203">**Aby przypisać Simona Britta InTime, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="644fc-203">**To assign Britta Simon to InTime, perform the following steps:**</span></span>

1. <span data-ttu-id="644fc-204">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="644fc-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="644fc-206">Na liście aplikacji zaznacz **InTime**.</span><span class="sxs-lookup"><span data-stu-id="644fc-206">In the applications list, select **InTime**.</span></span>

    ![InTime łącza na liście aplikacji](./media/active-directory-saas-intime-tutorial/tutorial_intime_app.png)  

3. <span data-ttu-id="644fc-208">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="644fc-208">In the menu on the left, click **Users and groups**.</span></span>

    ![Łącze "Użytkownicy i grupy"][202]

4. <span data-ttu-id="644fc-210">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="644fc-210">Click **Add** button.</span></span> <span data-ttu-id="644fc-211">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="644fc-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![W okienku Dodaj przydziału][203]

5. <span data-ttu-id="644fc-213">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="644fc-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="644fc-214">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="644fc-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="644fc-215">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="644fc-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="644fc-216">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="644fc-216">Test single sign-on</span></span>

<span data-ttu-id="644fc-217">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="644fc-217">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="644fc-218">Po kliknięciu kafelka InTime w panelu dostępu, należy pobrać na stronie logowania InTime aplikacji.</span><span class="sxs-lookup"><span data-stu-id="644fc-218">When you click the InTime tile in the Access Panel, you should get the login page of your InTime application.</span></span> <span data-ttu-id="644fc-219">Kliknij przycisk **logowania** przycisk, a następnie szereg IdPs będzie wyświetlana na liście przycisków.</span><span class="sxs-lookup"><span data-stu-id="644fc-219">Click the **Login** button, then a series of IdPs will be displayed on a list of buttons.</span></span> <span data-ttu-id="644fc-220">Kliknij przycisk **nazwa IDP** podana przez [zespołem pomocy technicznej InTime](mailto:hdollard@intimesoft.com) do logowania do aplikacji InTime.</span><span class="sxs-lookup"><span data-stu-id="644fc-220">click **IDP name** given by [InTime support team](mailto:hdollard@intimesoft.com) to login into your InTime application.</span></span> <span data-ttu-id="644fc-221">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="644fc-221">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="644fc-222">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="644fc-222">Additional resources</span></span>

* [<span data-ttu-id="644fc-223">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="644fc-223">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="644fc-224">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="644fc-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-intime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intime-tutorial/tutorial_general_203.png

