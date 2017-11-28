---
title: 'Samouczek: Integracji Azure Active Directory z Merchlogix | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Merchlogix."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: a1f49bb8-6b17-433d-8f25-9d26fb390e77
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: jeedes
ms.openlocfilehash: 44fc8226480cafc130720fbe78aa85ee95caec6c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-merchlogix"></a><span data-ttu-id="b0a8f-103">Samouczek: Integracji Azure Active Directory z Merchlogix</span><span class="sxs-lookup"><span data-stu-id="b0a8f-103">Tutorial: Azure Active Directory integration with Merchlogix</span></span>

<span data-ttu-id="b0a8f-104">Z tego samouczka dowiesz się integrowanie Merchlogix z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b0a8f-104">In this tutorial, you learn how to integrate Merchlogix with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b0a8f-105">Integracja z usługą Azure AD Merchlogix zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="b0a8f-105">Integrating Merchlogix with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b0a8f-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Merchlogix.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-106">You can control in Azure AD who has access to Merchlogix.</span></span>
- <span data-ttu-id="b0a8f-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Merchlogix (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-107">You can enable your users to automatically get signed-on to Merchlogix (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="b0a8f-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="b0a8f-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b0a8f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b0a8f-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b0a8f-110">Prerequisites</span></span>

<span data-ttu-id="b0a8f-111">Aby skonfigurować integrację usługi Azure AD z Merchlogix, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="b0a8f-111">To configure Azure AD integration with Merchlogix, you need the following items:</span></span>

- <span data-ttu-id="b0a8f-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0a8f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b0a8f-113">Merchlogix logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="b0a8f-113">A Merchlogix single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b0a8f-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b0a8f-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="b0a8f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b0a8f-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b0a8f-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b0a8f-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b0a8f-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="b0a8f-118">Scenario description</span></span>
<span data-ttu-id="b0a8f-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b0a8f-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="b0a8f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b0a8f-121">Dodawanie Merchlogix z galerii</span><span class="sxs-lookup"><span data-stu-id="b0a8f-121">Adding Merchlogix from the gallery</span></span>
2. <span data-ttu-id="b0a8f-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="b0a8f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-merchlogix-from-the-gallery"></a><span data-ttu-id="b0a8f-123">Dodawanie Merchlogix z galerii</span><span class="sxs-lookup"><span data-stu-id="b0a8f-123">Adding Merchlogix from the gallery</span></span>
<span data-ttu-id="b0a8f-124">Aby skonfigurować integrację usługi Azure AD Merchlogix, należy dodać Merchlogix z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-124">To configure the integration of Merchlogix into Azure AD, you need to add Merchlogix from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b0a8f-125">**Aby dodać Merchlogix z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="b0a8f-125">**To add Merchlogix from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b0a8f-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Przycisk usługi Azure Active Directory][1]

2. <span data-ttu-id="b0a8f-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b0a8f-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-129">Then go to **All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa][2]
    
3. <span data-ttu-id="b0a8f-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Nowy przycisk aplikacji][3]

4. <span data-ttu-id="b0a8f-133">W polu wyszukiwania wpisz **Merchlogix**, wybierz pozycję **Merchlogix** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-133">In the search box, type **Merchlogix**, select **Merchlogix** from result panel then click **Add** button to add the application.</span></span>

    ![Merchlogix na liście wyników](./media/active-directory-saas-merchlogix-tutorial/tutorial_merchlogix_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b0a8f-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="b0a8f-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="b0a8f-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Merchlogix w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-136">In this section, you configure and test Azure AD single sign-on with Merchlogix based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b0a8f-137">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Merchlogix jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Merchlogix is to a user in Azure AD.</span></span> <span data-ttu-id="b0a8f-138">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Merchlogix musi się.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-138">In other words, a link relationship between an Azure AD user and the related user in Merchlogix needs to be established.</span></span>

<span data-ttu-id="b0a8f-139">W Merchlogix, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-139">In Merchlogix, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b0a8f-140">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Merchlogix, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="b0a8f-140">To configure and test Azure AD single sign-on with Merchlogix, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b0a8f-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b0a8f-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b0a8f-143">**[Tworzenie użytkownika testowego Merchlogix](#create-a-merchlogix-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Merchlogix połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-143">**[Create a Merchlogix test user](#create-a-merchlogix-test-user)** - to have a counterpart of Britta Simon in Merchlogix that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b0a8f-144">**[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b0a8f-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b0a8f-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="b0a8f-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b0a8f-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Merchlogix.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Merchlogix application.</span></span>

<span data-ttu-id="b0a8f-148">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Merchlogix, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="b0a8f-148">**To configure Azure AD single sign-on with Merchlogix, perform the following steps:**</span></span>

1. <span data-ttu-id="b0a8f-149">W portalu Azure na **Merchlogix** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-149">In the Azure portal, on the **Merchlogix** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="b0a8f-151">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-merchlogix-tutorial/tutorial_merchlogix_samlbase.png)

3. <span data-ttu-id="b0a8f-153">Na **Merchlogix domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b0a8f-153">On the **Merchlogix Domain and URLs** section, perform the following steps:</span></span>

    ![Adresy URL i domeny Merchlogix pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-merchlogix-tutorial/tutorial_merchlogix_url.png)

    <span data-ttu-id="b0a8f-155">a.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-155">a.</span></span> <span data-ttu-id="b0a8f-156">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<DOMAIN>/login.php?saml=true`</span><span class="sxs-lookup"><span data-stu-id="b0a8f-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<DOMAIN>/login.php?saml=true`</span></span>

    <span data-ttu-id="b0a8f-157">b.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-157">b.</span></span> <span data-ttu-id="b0a8f-158">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<DOMAIN>/simplesaml/module.php/saml/sp/metadata.php/<SAML_NAME>`</span><span class="sxs-lookup"><span data-stu-id="b0a8f-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<DOMAIN>/simplesaml/module.php/saml/sp/metadata.php/<SAML_NAME>`</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="b0a8f-159">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-159">These values are not real.</span></span> <span data-ttu-id="b0a8f-160">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="b0a8f-161">Skontaktuj się z [zespołem pomocy technicznej Merchlogix](http://www.merchlogix.com/contact/) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-161">Contact [Merchlogix support team](http://www.merchlogix.com/contact/) to get these values.</span></span>

4. <span data-ttu-id="b0a8f-162">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-162">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Łącze pobierania certyfikatu](./media/active-directory-saas-merchlogix-tutorial/tutorial_merchlogix_certificate.png) 

5. <span data-ttu-id="b0a8f-164">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-164">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-merchlogix-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b0a8f-166">Na **konfiguracji Merchlogix** , kliknij przycisk **skonfigurować Merchlogix** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-166">On the **Merchlogix Configuration** section, click **Configure Merchlogix** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b0a8f-167">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML,** i **SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="b0a8f-167">Copy the **Sign-Out URL, SAML Entity ID,** and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfiguracja Merchlogix](./media/active-directory-saas-merchlogix-tutorial/tutorial_merchlogix_configure.png) 

7. <span data-ttu-id="b0a8f-169">Skonfigurować logowanie jednokrotne w **Merchlogix** stronie, musisz wysłać pobrany **certyfikatu (Base64)**, **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** do [zespołem pomocy technicznej Merchlogix](http://www.merchlogix.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="b0a8f-169">To configure single sign-on on **Merchlogix** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Merchlogix support team](http://www.merchlogix.com/contact/).</span></span> <span data-ttu-id="b0a8f-170">To ustawienie, aby były prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one wartość.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="b0a8f-171">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="b0a8f-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b0a8f-172">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b0a8f-173">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b0a8f-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b0a8f-174">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0a8f-174">Create an Azure AD test user</span></span>

<span data-ttu-id="b0a8f-175">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="b0a8f-177">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="b0a8f-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b0a8f-178">W portalu Azure, w okienku po lewej stronie kliknij **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-merchlogix-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="b0a8f-180">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-merchlogix-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="b0a8f-182">Aby otworzyć **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** w górnej części **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Przycisk Dodaj](./media/active-directory-saas-merchlogix-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="b0a8f-184">W **użytkownika** okna dialogowego wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b0a8f-184">In the **User** dialog box, perform the following steps:</span></span>

    ![Okno dialogowe użytkownika](./media/active-directory-saas-merchlogix-tutorial/create_aaduser_04.png)

    <span data-ttu-id="b0a8f-186">a.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-186">a.</span></span> <span data-ttu-id="b0a8f-187">W **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-187">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b0a8f-188">b.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-188">b.</span></span> <span data-ttu-id="b0a8f-189">W **nazwy użytkownika** wpisz adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-189">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="b0a8f-190">c.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-190">c.</span></span> <span data-ttu-id="b0a8f-191">Wybierz **Pokaż hasło** pole wyboru, a następnie zanotuj wartość, która jest wyświetlana w **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="b0a8f-192">d.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-192">d.</span></span> <span data-ttu-id="b0a8f-193">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-193">Click **Create**.</span></span>
 
### <a name="create-a-merchlogix-test-user"></a><span data-ttu-id="b0a8f-194">Tworzenie użytkownika testowego Merchlogix</span><span class="sxs-lookup"><span data-stu-id="b0a8f-194">Create a Merchlogix test user</span></span>

<span data-ttu-id="b0a8f-195">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Merchlogix.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-195">In this section, you create a user called Britta Simon in Merchlogix.</span></span> <span data-ttu-id="b0a8f-196">Praca z [zespołem pomocy technicznej Merchlogix](http://www.merchlogix.com/contact/) Aby dodać użytkowników do platformy Merchlogix.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-196">Work with [Merchlogix support team](http://www.merchlogix.com/contact/) to add the users in the Merchlogix platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="b0a8f-197">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0a8f-197">Assign the Azure AD test user</span></span>

<span data-ttu-id="b0a8f-198">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Merchlogix.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Merchlogix.</span></span>

![Przypisanie roli użytkownika][200] 

<span data-ttu-id="b0a8f-200">**Aby przypisać Simona Britta Merchlogix, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="b0a8f-200">**To assign Britta Simon to Merchlogix, perform the following steps:**</span></span>

1. <span data-ttu-id="b0a8f-201">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="b0a8f-203">Na liście aplikacji zaznacz **Merchlogix**.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-203">In the applications list, select **Merchlogix**.</span></span>

    ![Łącze Merchlogix na liście aplikacji](./media/active-directory-saas-merchlogix-tutorial/tutorial_merchlogix_app.png)  

3. <span data-ttu-id="b0a8f-205">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Łącze "Użytkownicy i grupy"][202]

4. <span data-ttu-id="b0a8f-207">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-207">Click **Add** button.</span></span> <span data-ttu-id="b0a8f-208">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![W okienku Dodaj przydziału][203]

5. <span data-ttu-id="b0a8f-210">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b0a8f-211">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b0a8f-212">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b0a8f-213">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="b0a8f-213">Test single sign-on</span></span>

<span data-ttu-id="b0a8f-214">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b0a8f-215">Po kliknięciu kafelka Merchlogix w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Merchlogix.</span><span class="sxs-lookup"><span data-stu-id="b0a8f-215">When you click the Merchlogix tile in the Access Panel, you should get automatically signed-on to your Merchlogix application.</span></span>
<span data-ttu-id="b0a8f-216">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b0a8f-216">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b0a8f-217">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="b0a8f-217">Additional resources</span></span>

* [<span data-ttu-id="b0a8f-218">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b0a8f-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b0a8f-219">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b0a8f-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-merchlogix-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-merchlogix-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-merchlogix-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-merchlogix-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-merchlogix-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-merchlogix-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-merchlogix-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-merchlogix-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-merchlogix-tutorial/tutorial_general_203.png

