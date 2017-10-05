---
title: 'Samouczek: Integracji Azure Active Directory z Peoplecart | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Peoplecart."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: c83b5d9d-2638-4689-b9f0-f56a9159e7a0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: b83a1621263cac0b23bbd35a49fda213d2e4271a
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-peoplecart"></a><span data-ttu-id="87ed4-103">Samouczek: Integracji Azure Active Directory z Peoplecart</span><span class="sxs-lookup"><span data-stu-id="87ed4-103">Tutorial: Azure Active Directory integration with Peoplecart</span></span>

<span data-ttu-id="87ed4-104">Z tego samouczka dowiesz się integrowanie Peoplecart z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="87ed4-104">In this tutorial, you learn how to integrate Peoplecart with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="87ed4-105">Integracja z usługą Azure AD Peoplecart zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="87ed4-105">Integrating Peoplecart with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="87ed4-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Peoplecart</span><span class="sxs-lookup"><span data-stu-id="87ed4-106">You can control in Azure AD who has access to Peoplecart</span></span>
- <span data-ttu-id="87ed4-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Peoplecart (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="87ed4-107">You can enable your users to automatically get signed-on to Peoplecart (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="87ed4-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="87ed4-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="87ed4-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="87ed4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="87ed4-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="87ed4-110">Prerequisites</span></span>

<span data-ttu-id="87ed4-111">Aby skonfigurować integrację usługi Azure AD z Peoplecart, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="87ed4-111">To configure Azure AD integration with Peoplecart, you need the following items:</span></span>

- <span data-ttu-id="87ed4-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="87ed4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="87ed4-113">Peoplecart logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="87ed4-113">A Peoplecart single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="87ed4-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="87ed4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="87ed4-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="87ed4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="87ed4-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="87ed4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="87ed4-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="87ed4-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="87ed4-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="87ed4-118">Scenario description</span></span>
<span data-ttu-id="87ed4-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="87ed4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="87ed4-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="87ed4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="87ed4-121">Dodawanie Peoplecart z galerii</span><span class="sxs-lookup"><span data-stu-id="87ed4-121">Adding Peoplecart from the gallery</span></span>
2. <span data-ttu-id="87ed4-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="87ed4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-peoplecart-from-the-gallery"></a><span data-ttu-id="87ed4-123">Dodawanie Peoplecart z galerii</span><span class="sxs-lookup"><span data-stu-id="87ed4-123">Adding Peoplecart from the gallery</span></span>
<span data-ttu-id="87ed4-124">Aby skonfigurować integrację usługi Azure AD Peoplecart, należy dodać Peoplecart z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="87ed4-124">To configure the integration of Peoplecart into Azure AD, you need to add Peoplecart from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="87ed4-125">**Aby dodać Peoplecart z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="87ed4-125">**To add Peoplecart from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="87ed4-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="87ed4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Przycisk usługi Azure Active Directory][1]

2. <span data-ttu-id="87ed4-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="87ed4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="87ed4-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="87ed4-129">Then go to **All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa][2]
    
3. <span data-ttu-id="87ed4-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="87ed4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Nowy przycisk aplikacji][3]

4. <span data-ttu-id="87ed4-133">W polu wyszukiwania wpisz **Peoplecart**, wybierz pozycję **Peoplecart** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="87ed4-133">In the search box, type **Peoplecart**, select **Peoplecart** from result panel then click **Add** button to add the application.</span></span>

    ![Peoplecart na liście wyników](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="87ed4-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="87ed4-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="87ed4-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Peoplecart w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="87ed4-136">In this section, you configure and test Azure AD single sign-on with Peoplecart based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="87ed4-137">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Peoplecart jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="87ed4-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Peoplecart is to a user in Azure AD.</span></span> <span data-ttu-id="87ed4-138">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Peoplecart musi się.</span><span class="sxs-lookup"><span data-stu-id="87ed4-138">In other words, a link relationship between an Azure AD user and the related user in Peoplecart needs to be established.</span></span>

<span data-ttu-id="87ed4-139">W Peoplecart, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="87ed4-139">In Peoplecart, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="87ed4-140">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Peoplecart, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="87ed4-140">To configure and test Azure AD single sign-on with Peoplecart, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="87ed4-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="87ed4-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="87ed4-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="87ed4-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="87ed4-143">**[Tworzenie użytkownika testowego Peoplecart](#create-a-peoplecart-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Peoplecart połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="87ed4-143">**[Create a Peoplecart test user](#create-a-peoplecart-test-user)** - to have a counterpart of Britta Simon in Peoplecart that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="87ed4-144">**[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="87ed4-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="87ed4-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="87ed4-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="87ed4-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="87ed4-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="87ed4-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Peoplecart.</span><span class="sxs-lookup"><span data-stu-id="87ed4-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Peoplecart application.</span></span>

<span data-ttu-id="87ed4-148">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Peoplecart, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="87ed4-148">**To configure Azure AD single sign-on with Peoplecart, perform the following steps:**</span></span>

1. <span data-ttu-id="87ed4-149">W portalu Azure na **Peoplecart** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="87ed4-149">In the Azure portal, on the **Peoplecart** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="87ed4-151">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="87ed4-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_samlbase.png)

3. <span data-ttu-id="87ed4-153">Na **Peoplecart domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="87ed4-153">On the **Peoplecart Domain and URLs** section, perform the following steps:</span></span>

    ![Adresy URL i domeny Peoplecart pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_url.png)

    <span data-ttu-id="87ed4-155">a.</span><span class="sxs-lookup"><span data-stu-id="87ed4-155">a.</span></span> <span data-ttu-id="87ed4-156">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<tenantname>.peoplecart.com/SignIn.aspx`</span><span class="sxs-lookup"><span data-stu-id="87ed4-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.peoplecart.com/SignIn.aspx`</span></span>

    <span data-ttu-id="87ed4-157">b.</span><span class="sxs-lookup"><span data-stu-id="87ed4-157">b.</span></span> <span data-ttu-id="87ed4-158">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<tenantname>.peoplecart.com`</span><span class="sxs-lookup"><span data-stu-id="87ed4-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenantname>.peoplecart.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="87ed4-159">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="87ed4-159">These values are not real.</span></span> <span data-ttu-id="87ed4-160">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="87ed4-160">Update these values with the actual Sign-On URL, and Identifier.</span></span> <span data-ttu-id="87ed4-161">Skontaktuj się z [zespołem pomocy technicznej klienta Peoplecart](https://peoplecart.com/ContactUs.aspx) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="87ed4-161">Contact [Peoplecart Client support team](https://peoplecart.com/ContactUs.aspx) to get these values.</span></span> 
 
4. <span data-ttu-id="87ed4-162">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="87ed4-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Łącze pobierania certyfikatu](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_certificate.png) 

5. <span data-ttu-id="87ed4-164">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="87ed4-164">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-peoplecart-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="87ed4-166">Na **konfiguracji Peoplecart** , kliknij przycisk **skonfigurować Peoplecart** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="87ed4-166">On the **Peoplecart Configuration** section, click **Configure Peoplecart** to open **Configure sign-on** window.</span></span> <span data-ttu-id="87ed4-167">Kopiuj **SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="87ed4-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfiguracja Peoplecart](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_configure.png) 

7. <span data-ttu-id="87ed4-169">Skonfigurować logowanie jednokrotne w **Peoplecart** stronie, musisz wysłać pobrany **XML metadanych** i **SAML pojedynczy znak na adres URL usługi** do [zespołem pomocy technicznej Peoplecart](https://peoplecart.com/ContactUs.aspx).</span><span class="sxs-lookup"><span data-stu-id="87ed4-169">To configure single sign-on on **Peoplecart** side, you need to send the downloaded **Metadata XML** and **SAML Single Sign-On Service URL** to [Peoplecart support team](https://peoplecart.com/ContactUs.aspx).</span></span> <span data-ttu-id="87ed4-170">To ustawienie, aby były prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one wartość.</span><span class="sxs-lookup"><span data-stu-id="87ed4-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="87ed4-171">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="87ed4-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="87ed4-172">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="87ed4-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="87ed4-173">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="87ed4-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="87ed4-174">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="87ed4-174">Create an Azure AD test user</span></span>
<span data-ttu-id="87ed4-175">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="87ed4-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="87ed4-177">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="87ed4-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="87ed4-178">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="87ed4-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-peoplecart-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="87ed4-180">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="87ed4-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-peoplecart-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="87ed4-182">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="87ed4-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Przycisk Dodaj](./media/active-directory-saas-peoplecart-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="87ed4-184">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="87ed4-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Okno dialogowe użytkownika](./media/active-directory-saas-peoplecart-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="87ed4-186">a.</span><span class="sxs-lookup"><span data-stu-id="87ed4-186">a.</span></span> <span data-ttu-id="87ed4-187">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="87ed4-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="87ed4-188">b.</span><span class="sxs-lookup"><span data-stu-id="87ed4-188">b.</span></span> <span data-ttu-id="87ed4-189">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="87ed4-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="87ed4-190">c.</span><span class="sxs-lookup"><span data-stu-id="87ed4-190">c.</span></span> <span data-ttu-id="87ed4-191">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="87ed4-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="87ed4-192">d.</span><span class="sxs-lookup"><span data-stu-id="87ed4-192">d.</span></span> <span data-ttu-id="87ed4-193">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="87ed4-193">Click **Create**.</span></span>
 
### <a name="create-a-peoplecart-test-user"></a><span data-ttu-id="87ed4-194">Tworzenie użytkownika testowego Peoplecart</span><span class="sxs-lookup"><span data-stu-id="87ed4-194">Create a Peoplecart test user</span></span>

<span data-ttu-id="87ed4-195">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Peoplecart.</span><span class="sxs-lookup"><span data-stu-id="87ed4-195">In this section, you create a user called Britta Simon in Peoplecart.</span></span> <span data-ttu-id="87ed4-196">Praca z [zespołem pomocy technicznej Peoplecart](https://peoplecart.com/ContactUs.aspx) Aby dodać użytkowników do platformy Peoplecart.</span><span class="sxs-lookup"><span data-stu-id="87ed4-196">Work with [Peoplecart support team](https://peoplecart.com/ContactUs.aspx) to add the users in the Peoplecart platform.</span></span> <span data-ttu-id="87ed4-197">Użytkownicy muszą utworzyć i aktywowana, aby użyć rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="87ed4-197">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="87ed4-198">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="87ed4-198">Assign the Azure AD test user</span></span>

<span data-ttu-id="87ed4-199">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Peoplecart.</span><span class="sxs-lookup"><span data-stu-id="87ed4-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Peoplecart.</span></span>

![Przypisanie roli użytkownika][200] 

<span data-ttu-id="87ed4-201">**Aby przypisać Simona Britta Peoplecart, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="87ed4-201">**To assign Britta Simon to Peoplecart, perform the following steps:**</span></span>

1. <span data-ttu-id="87ed4-202">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="87ed4-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="87ed4-204">Na liście aplikacji zaznacz **Peoplecart**.</span><span class="sxs-lookup"><span data-stu-id="87ed4-204">In the applications list, select **Peoplecart**.</span></span>

    ![Łącze Peoplecart na liście aplikacji](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_app.png) 

3. <span data-ttu-id="87ed4-206">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="87ed4-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Łącze "Użytkownicy i grupy"][202] 

4. <span data-ttu-id="87ed4-208">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="87ed4-208">Click **Add** button.</span></span> <span data-ttu-id="87ed4-209">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="87ed4-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![W okienku Dodaj przydziału][203]

5. <span data-ttu-id="87ed4-211">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="87ed4-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="87ed4-212">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="87ed4-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="87ed4-213">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="87ed4-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="87ed4-214">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="87ed4-214">Test single sign-on</span></span>

<span data-ttu-id="87ed4-215">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="87ed4-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="87ed4-216">Po kliknięciu kafelka Peoplecart w panelu dostępu, należy pobrać strony logowania Peoplecart aplikacji.</span><span class="sxs-lookup"><span data-stu-id="87ed4-216">When you click the Peoplecart tile in the Access Panel, you should get login page of Peoplecart application.</span></span>
<span data-ttu-id="87ed4-217">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="87ed4-217">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="87ed4-218">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="87ed4-218">Additional resources</span></span>

* [<span data-ttu-id="87ed4-219">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="87ed4-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="87ed4-220">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="87ed4-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_203.png

