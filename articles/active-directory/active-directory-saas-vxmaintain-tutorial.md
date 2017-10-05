---
title: "Samouczek: Integrowanie usługi Azure Active Directory z vxMaintain | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i vxMaintain."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 841a1066-593c-4603-9abe-f48496d73d10
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: ad87534af448356b8cc80d8ddd278bfb8a9165e7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-vxmaintain"></a><span data-ttu-id="2f092-103">Samouczek: Integrowanie usługi Azure Active Directory z vxMaintain</span><span class="sxs-lookup"><span data-stu-id="2f092-103">Tutorial: Integrate Azure Active Directory with vxMaintain</span></span>

<span data-ttu-id="2f092-104">Z tego samouczka dowiesz się integrowanie vxMaintain z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2f092-104">In this tutorial, you learn how to integrate vxMaintain with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2f092-105">Integracja ta zapewnia kilka istotnych korzyści.</span><span class="sxs-lookup"><span data-stu-id="2f092-105">This integration provides several important benefits.</span></span> <span data-ttu-id="2f092-106">Możesz:</span><span class="sxs-lookup"><span data-stu-id="2f092-106">You can:</span></span>

- <span data-ttu-id="2f092-107">Kontrolowanie w usłudze Azure AD, który ma dostęp do vxMaintain.</span><span class="sxs-lookup"><span data-stu-id="2f092-107">Control in Azure AD who has access to vxMaintain.</span></span>
- <span data-ttu-id="2f092-108">Umożliwianie użytkownikom automatycznie logować się do vxMaintain z logowaniem jednokrotnym (SSO) za pomocą ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f092-108">Enable your users to automatically sign in to vxMaintain with single sign-on (SSO) by using their Azure AD accounts.</span></span>
- <span data-ttu-id="2f092-109">Zarządzanie kont w jednej centralnej lokalizacji: portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="2f092-109">Manage your accounts in one central location: the Azure portal.</span></span>

<span data-ttu-id="2f092-110">Aby dowiedzieć się więcej na temat integracji aplikacji SaaS z usługą Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2f092-110">To learn more about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f092-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2f092-111">Prerequisites</span></span>

<span data-ttu-id="2f092-112">Aby skonfigurować integrację usługi Azure AD z vxMaintain, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="2f092-112">To configure Azure AD integration with vxMaintain, you need the following items:</span></span>

- <span data-ttu-id="2f092-113">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f092-113">An Azure AD subscription</span></span>
- <span data-ttu-id="2f092-114">VxMaintain logowanie Jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="2f092-114">A vxMaintain SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2f092-115">Podczas testowania czynności w tym samouczku, firma Microsoft zaleca, nie używaj do środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="2f092-115">When you test the steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="2f092-116">Aby przetestować kroki opisane w tym samouczku, wykonaj te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="2f092-116">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="2f092-117">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="2f092-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2f092-118">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2f092-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2f092-119">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="2f092-119">Scenario description</span></span>
<span data-ttu-id="2f092-120">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="2f092-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="2f092-121">Scenariusz, w tym samouczku przedstawiono składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="2f092-121">The scenario that this tutorial outlines consists of two main building blocks:</span></span>

* <span data-ttu-id="2f092-122">Dodawanie vxMaintain z galerii</span><span class="sxs-lookup"><span data-stu-id="2f092-122">Adding vxMaintain from the gallery</span></span>
* <span data-ttu-id="2f092-123">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="2f092-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="add-vxmaintain-from-the-gallery"></a><span data-ttu-id="2f092-124">Dodaj vxMaintain z galerii</span><span class="sxs-lookup"><span data-stu-id="2f092-124">Add vxMaintain from the gallery</span></span>
<span data-ttu-id="2f092-125">Aby skonfigurować integrację vxMaintain z usługą Azure AD, należy dodać vxMaintain z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="2f092-125">To configure the integration of vxMaintain with Azure AD, you need to add vxMaintain from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2f092-126">Aby dodać vxMaintain z galerii, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="2f092-126">To add vxMaintain from the gallery, do the following:</span></span>

1. <span data-ttu-id="2f092-127">W [portalu Azure](https://portal.azure.com), w okienku po lewej stronie wybierz **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="2f092-127">In the [Azure portal](https://portal.azure.com), in the left pane, select the **Azure Active Directory** button.</span></span> 

    ![Przycisk usługi Azure Active Directory][1]

2. <span data-ttu-id="2f092-129">Wybierz **aplikacje dla przedsiębiorstw** > **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="2f092-129">Select **Enterprise applications** > **All applications**.</span></span>

    ![W okienku "Aplikacje przedsiębiorstwa"][2]
    
3. <span data-ttu-id="2f092-131">Aby dodać aplikację, w **wszystkie aplikacje** okno dialogowe, wybierz opcję **nowej aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="2f092-131">To add an application, in the **All applications** dialog box, select **New application**.</span></span>

    !["Nowa aplikacja" przycisku][3]

4. <span data-ttu-id="2f092-133">W polu wyszukiwania wpisz **vxMaintain**.</span><span class="sxs-lookup"><span data-stu-id="2f092-133">In the search box, type **vxMaintain**.</span></span>

    ![Na liście rozwijanej "Pojedynczy znak na tryb"](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_search.png)

5. <span data-ttu-id="2f092-135">Na liście wyników wybierz **vxMaintain**, a następnie wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="2f092-135">In the results list, select **vxMaintain**, and then select **Add**.</span></span>

    ![Łącze vxMaintain](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="2f092-137">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="2f092-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="2f092-138">W tej sekcji można skonfigurować i przetestować logowania jednokrotnego programu Azure AD przy użyciu vxMaintain, na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="2f092-138">In this section, you configure and test Azure AD SSO by using vxMaintain, based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2f092-139">Aby logowanie Jednokrotne do pracy usługi Azure AD musi znać vxMaintain odpowiednikiem użytkownika usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f092-139">For SSO to work, Azure AD needs to know the vxMaintain counterpart to the Azure AD user.</span></span> <span data-ttu-id="2f092-140">Oznacza to należy ustanowić relację łącza między użytkownikiem usługi Azure AD i odpowiedniego użytkownika vxMaintain.</span><span class="sxs-lookup"><span data-stu-id="2f092-140">That is, you must establish a link relationship between the Azure AD user and the corresponding vxMaintain user.</span></span>

<span data-ttu-id="2f092-141">Do ustanawiania relacji łącza, przypisz vxMaintain **nazwy użytkownika** wartość, jak usługi Azure AD **Username** wartość.</span><span class="sxs-lookup"><span data-stu-id="2f092-141">To establish the link relationship, assign the vxMaintain **user name** value as the Azure AD **Username** value.</span></span>

<span data-ttu-id="2f092-142">Aby skonfigurować i przetestować logowania jednokrotnego programu Azure AD przy użyciu vxMaintain, wykonaj poniższe bloki konstrukcyjne.</span><span class="sxs-lookup"><span data-stu-id="2f092-142">To configure and test Azure AD SSO by using vxMaintain, complete the following building blocks.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="2f092-143">Konfigurowanie usługi Azure AD logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="2f092-143">Configure Azure AD SSO</span></span>

<span data-ttu-id="2f092-144">W tej sekcji można zarówno włączenia funkcji logowania jednokrotnego usługi Azure AD w portalu Azure i skonfigurować logowanie Jednokrotne w aplikacji vxMaintain w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="2f092-144">In this section, you can both enable Azure AD SSO in the Azure portal and configure SSO in your vxMaintain application by doing the following:</span></span>

1. <span data-ttu-id="2f092-145">W portalu Azure na **vxMaintain** strona integracji aplikacji, wybierz opcję **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="2f092-145">In the Azure portal, on the **vxMaintain** application integration page, select **Single sign-on**.</span></span>

    ![Polecenie "Logowanie jednokrotne"][4]

2. <span data-ttu-id="2f092-147">Aby włączyć logowanie Jednokrotne, w **tryb rejestracji jednokrotnej** listy rozwijanej wybierz **na języku SAML logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="2f092-147">To enable SSO, in the **Single Sign-on Mode** drop-down list, select **SAML-based Sign-on**.</span></span>
 
    ![Polecenie "na podstawie SAML logowania"](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_samlbase.png)

3. <span data-ttu-id="2f092-149">W obszarze **vxMaintain domeny i adres URL**, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="2f092-149">Under **vxMaintain Domain and URLs**, do the following:</span></span>

    ![VxMaintain sekcji domeny i adresy URL](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_url.png)

    <span data-ttu-id="2f092-151">a.</span><span class="sxs-lookup"><span data-stu-id="2f092-151">a.</span></span> <span data-ttu-id="2f092-152">W **identyfikator** wpisz adres URL, który ma następującą składnię:`https://<company name>.verisae.com`</span><span class="sxs-lookup"><span data-stu-id="2f092-152">In the **Identifier** box, type a URL that has the following syntax: `https://<company name>.verisae.com`</span></span>

    <span data-ttu-id="2f092-153">b.</span><span class="sxs-lookup"><span data-stu-id="2f092-153">b.</span></span> <span data-ttu-id="2f092-154">W **adres URL odpowiedzi** wpisz adres URL, który ma następującą składnię:`https://<company name>.verisae.com/DataNett/action/ssoConsume/mobile?_log=true`</span><span class="sxs-lookup"><span data-stu-id="2f092-154">In the **Reply URL** box, type a URL that has the following syntax: `https://<company name>.verisae.com/DataNett/action/ssoConsume/mobile?_log=true`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2f092-155">Poprzednie wartości nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="2f092-155">The preceding values are not real.</span></span> <span data-ttu-id="2f092-156">Zaktualizuj je z rzeczywistego identyfikatora i adres URL odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="2f092-156">Update them with the actual identifier and reply URL.</span></span> <span data-ttu-id="2f092-157">Aby uzyskać wartości, skontaktuj się z [zespołem pomocy technicznej vxMaintain](http://www.verisae.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="2f092-157">To obtain the values, contact the [vxMaintain support team](http://www.verisae.com/contact-us).</span></span>
 
4. <span data-ttu-id="2f092-158">W obszarze **certyfikat podpisywania SAML**, wybierz pozycję **XML metadanych**, a następnie zapisz plik metadanych do komputera.</span><span class="sxs-lookup"><span data-stu-id="2f092-158">Under **SAML Signing Certificate**, select **Metadata XML**, and then save the metadata file to your computer.</span></span>

    ![W sekcji "Certyfikat podpisywania SAML"](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_certificate.png) 

5. <span data-ttu-id="2f092-160">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="2f092-160">Select **Save**.</span></span>

    ![Przycisk Zapisz](./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2f092-162">Aby skonfigurować **vxMaintain** logowania jednokrotnego, Wyślij pobrany **XML metadanych** pliku na [vxMaintain zespołem pomocy technicznej](http://www.verisae.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="2f092-162">To configure **vxMaintain** SSO, send the downloaded **Metadata XML** file to the [vxMaintain support team](http://www.verisae.com/contact-us).</span></span>

> [!TIP]
> <span data-ttu-id="2f092-163">Po skonfigurowaniu aplikacji może odczytywać zwięzły wersji poprzednich instrukcji w [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2f092-163">As you set up the app, you can read a concise version of the preceding instructions in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="2f092-164">Po dodaniu aplikacji z **usługi Active Directory** > **aplikacje dla przedsiębiorstw** zaznacz **rejestracji jednokrotnej** karcie i uzyskuje dostęp do osadzonego Dokumentacja z **konfiguracji** sekcji.</span><span class="sxs-lookup"><span data-stu-id="2f092-164">After you add the app from the **Active Directory** > **Enterprise Applications** section, select the **Single Sign-On** tab, and then access the embedded documentation from the **Configuration** section.</span></span> 
>
><span data-ttu-id="2f092-165">Aby dowiedzieć się więcej o funkcji osadzonych dokumentacji, zobacz [Zarządzanie logowanie jednokrotne dla aplikacji przedsiębiorstwa](https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="2f092-165">To learn more about the embedded documentation feature, see [Managing single sign-on for enterprise apps](https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="2f092-166">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f092-166">Create an Azure AD test user</span></span>
<span data-ttu-id="2f092-167">W tej sekcji możesz tworzyć użytkownika testowego Simona Britta w portalu Azure w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="2f092-167">In this section, you create test user Britta Simon in the Azure portal by doing the following:</span></span>

![Dane użytkownika usługi Azure AD][100]

1. <span data-ttu-id="2f092-169">W **portalu Azure**, w okienku po lewej stronie wybierz **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="2f092-169">In the **Azure portal**, in the left pane, select the **Azure Active Directory** button.</span></span>

    ![Przycisk "Azure Active Directory"](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2f092-171">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** > **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="2f092-171">To display a list of users, go to **Users and groups** > **All users**.</span></span>
    
    <span data-ttu-id="2f092-172">![Łącze "Wszyscy użytkownicy"](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_02.png)</span><span class="sxs-lookup"><span data-stu-id="2f092-172">![The "All users" link](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_02.png)</span></span>  
    <span data-ttu-id="2f092-173">**Wszyscy użytkownicy** zostanie otwarte okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="2f092-173">The **All users** dialog box opens.</span></span> 

3. <span data-ttu-id="2f092-174">Aby otworzyć **użytkownika** okno dialogowe, wybierz opcję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="2f092-174">To open the **User** dialog box, select **Add**.</span></span>
 
    ![Przycisk Dodaj](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2f092-176">W **użytkownika** okno dialogowe, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="2f092-176">In the **User** dialog box, do the following:</span></span>
 
    ![Okno dialogowe użytkownika](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2f092-178">a.</span><span class="sxs-lookup"><span data-stu-id="2f092-178">a.</span></span> <span data-ttu-id="2f092-179">W **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2f092-179">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2f092-180">b.</span><span class="sxs-lookup"><span data-stu-id="2f092-180">b.</span></span> <span data-ttu-id="2f092-181">W **nazwy użytkownika** wpisz adres e-mail użytkownika testowego Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="2f092-181">In the **User name** box, type the email address of test user Britta Simon.</span></span>

    <span data-ttu-id="2f092-182">c.</span><span class="sxs-lookup"><span data-stu-id="2f092-182">c.</span></span> <span data-ttu-id="2f092-183">Wybierz **Pokaż hasło** pole wyboru, a następnie zanotuj wartości, który został wygenerowany w **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="2f092-183">Select the **Show Password** check box, and then note the value that was generated in the **Password** box.</span></span>

    <span data-ttu-id="2f092-184">d.</span><span class="sxs-lookup"><span data-stu-id="2f092-184">d.</span></span> <span data-ttu-id="2f092-185">Wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="2f092-185">Select **Create**.</span></span>
 
### <a name="create-a-vxmaintain-test-user"></a><span data-ttu-id="2f092-186">Tworzenie użytkownika testowego vxMaintain</span><span class="sxs-lookup"><span data-stu-id="2f092-186">Create a vxMaintain test user</span></span>

<span data-ttu-id="2f092-187">W tej sekcji utworzysz użytkownika testowego Simona Britta w vxMaintain.</span><span class="sxs-lookup"><span data-stu-id="2f092-187">In this section, you create test user Britta Simon in vxMaintain.</span></span> <span data-ttu-id="2f092-188">Aby dodać użytkowników do platformy vxMaintain, pracy z [zespołem pomocy technicznej vxMaintain](http://www.verisae.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="2f092-188">To add users in the vxMaintain platform, work with the [vxMaintain support team](http://www.verisae.com/contact-us).</span></span> <span data-ttu-id="2f092-189">Przed użyciem logowania jednokrotnego, Utwórz i Aktywuj użytkowników.</span><span class="sxs-lookup"><span data-stu-id="2f092-189">Before you use SSO, create and activate the users.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="2f092-190">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f092-190">Assign the Azure AD test user</span></span>

<span data-ttu-id="2f092-191">W tej sekcji można włączyć użytkownika testowego Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do vxMaintain.</span><span class="sxs-lookup"><span data-stu-id="2f092-191">In this section, you enable test user Britta Simon to use Azure SSO by granting access to vxMaintain.</span></span> <span data-ttu-id="2f092-192">Aby to zrobić, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="2f092-192">To do so, do the following:</span></span>

![Użytkownik testowy na liście Nazwa wyświetlana][200] 

1. <span data-ttu-id="2f092-194">W portalu Azure **aplikacji** widok, przejdź do **katalogu** Widok > **aplikacje dla przedsiębiorstw** > **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="2f092-194">In the Azure portal **Applications** view, go to **Directory** view > **Enterprise applications** > **All applications**.</span></span>

    ![Łącze "Wszystkie aplikacje"][201] 

2. <span data-ttu-id="2f092-196">W **aplikacji** listy, wybierz **vxMaintain**.</span><span class="sxs-lookup"><span data-stu-id="2f092-196">In the **Applications** list, select **vxMaintain**.</span></span>

    ![Łącze vxMaintain](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_app.png) 

3. <span data-ttu-id="2f092-198">W okienku po lewej stronie wybierz **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="2f092-198">In the left pane, select **Users and groups**.</span></span>

    ![Łącze "Użytkownicy i grupy"][202] 

4. <span data-ttu-id="2f092-200">Wybierz **Dodaj** , a następnie w **Dodaj przydziału** okienku wybierz **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="2f092-200">Select **Add** and then, in the **Add Assignment** pane, select **Users and groups**.</span></span>

    ![Łącze "Użytkownicy i grupy"][203]

5. <span data-ttu-id="2f092-202">W **użytkowników i grup** okna dialogowego, **użytkowników** listy, wybierz **Simona Britta**, a następnie wybierz **wybierz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="2f092-202">In the **Users and groups** dialog box, in the **Users** list, select **Britta Simon**, and then select the **Select** button.</span></span>

7. <span data-ttu-id="2f092-203">W **Dodaj przydziału** okno dialogowe, wybierz opcję **przypisać**.</span><span class="sxs-lookup"><span data-stu-id="2f092-203">In the **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-your-azure-ad-single-sign-on"></a><span data-ttu-id="2f092-204">Test z usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="2f092-204">Test your Azure AD single sign-on</span></span>

<span data-ttu-id="2f092-205">W tej sekcji możesz przetestować konfigurację programu Azure AD z logowania jednokrotnego za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="2f092-205">In this section, you test your Azure AD SSO configuration by using the Access Panel.</span></span>

<span data-ttu-id="2f092-206">Wybieranie **vxMaintain** kafelka w panelu dostępu należy logować Cię w aplikacji vxMaintain automatycznie.</span><span class="sxs-lookup"><span data-stu-id="2f092-206">Selecting the **vxMaintain** tile in the Access Panel should sign you in to your vxMaintain application automatically.</span></span>

<span data-ttu-id="2f092-207">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2f092-207">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f092-208">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2f092-208">Next steps</span></span>

* [<span data-ttu-id="2f092-209">Lista samouczków dotyczących integracji aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2f092-209">List of tutorials on integrating SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2f092-210">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2f092-210">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_203.png

