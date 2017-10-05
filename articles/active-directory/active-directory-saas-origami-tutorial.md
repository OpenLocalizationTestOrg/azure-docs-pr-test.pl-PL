---
title: 'Samouczek: Integracji Azure Active Directory z Origami | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Origami."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a28bb0ba-b564-46ba-accc-e587699295d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 3420409b72ff032e64ac59365083dd141dfc3c1b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-origami"></a><span data-ttu-id="4a46a-103">Samouczek: Integracji Azure Active Directory z Origami</span><span class="sxs-lookup"><span data-stu-id="4a46a-103">Tutorial: Azure Active Directory integration with Origami</span></span>

<span data-ttu-id="4a46a-104">Z tego samouczka dowiesz się integrowanie Origami w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4a46a-104">In this tutorial, you learn how to integrate Origami with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4a46a-105">Integracja z usługą Azure AD Origami zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="4a46a-105">Integrating Origami with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4a46a-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Origami</span><span class="sxs-lookup"><span data-stu-id="4a46a-106">You can control in Azure AD who has access to Origami</span></span>
- <span data-ttu-id="4a46a-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Origami (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a46a-107">You can enable your users to automatically get signed-on to Origami (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4a46a-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="4a46a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4a46a-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4a46a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4a46a-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4a46a-110">Prerequisites</span></span>

<span data-ttu-id="4a46a-111">Aby skonfigurować integrację usługi Azure AD z Origami, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="4a46a-111">To configure Azure AD integration with Origami, you need the following items:</span></span>

- <span data-ttu-id="4a46a-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a46a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4a46a-113">Origami logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="4a46a-113">An Origami single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4a46a-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="4a46a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4a46a-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="4a46a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4a46a-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="4a46a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4a46a-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4a46a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4a46a-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="4a46a-118">Scenario description</span></span>
<span data-ttu-id="4a46a-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="4a46a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4a46a-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="4a46a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4a46a-121">Dodawanie Origami z galerii</span><span class="sxs-lookup"><span data-stu-id="4a46a-121">Adding Origami from the gallery</span></span>
2. <span data-ttu-id="4a46a-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="4a46a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-origami-from-the-gallery"></a><span data-ttu-id="4a46a-123">Dodawanie Origami z galerii</span><span class="sxs-lookup"><span data-stu-id="4a46a-123">Adding Origami from the gallery</span></span>
<span data-ttu-id="4a46a-124">Aby skonfigurować integrację usługi Azure AD Origami, należy dodać Origami z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="4a46a-124">To configure the integration of Origami into Azure AD, you need to add Origami from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4a46a-125">**Aby dodać Origami z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="4a46a-125">**To add Origami from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4a46a-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="4a46a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="4a46a-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="4a46a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4a46a-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="4a46a-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="4a46a-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4a46a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="4a46a-133">W polu wyszukiwania wpisz **Origami**.</span><span class="sxs-lookup"><span data-stu-id="4a46a-133">In the search box, type **Origami**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-origami-tutorial/tutorial_origami_search.png)

5. <span data-ttu-id="4a46a-135">W panelu wyników wybierz **Origami**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="4a46a-135">In the results panel, select **Origami**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-origami-tutorial/tutorial_origami_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4a46a-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="4a46a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4a46a-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Origami w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="4a46a-138">In this section, you configure and test Azure AD single sign-on with Origami based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4a46a-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Origami jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4a46a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Origami is to a user in Azure AD.</span></span> <span data-ttu-id="4a46a-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Origami musi się.</span><span class="sxs-lookup"><span data-stu-id="4a46a-140">In other words, a link relationship between an Azure AD user and the related user in Origami needs to be established.</span></span>

<span data-ttu-id="4a46a-141">W Origami, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="4a46a-141">In Origami, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="4a46a-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Origami, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="4a46a-142">To configure and test Azure AD single sign-on with Origami, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4a46a-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="4a46a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4a46a-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="4a46a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4a46a-145">**[Tworzenie użytkownika testowego Origami](#creating-an-origami-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Origami połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4a46a-145">**[Creating an Origami test user](#creating-an-origami-test-user)** - to have a counterpart of Britta Simon in Origami that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4a46a-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="4a46a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4a46a-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="4a46a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4a46a-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="4a46a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4a46a-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Origami.</span><span class="sxs-lookup"><span data-stu-id="4a46a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Origami application.</span></span>

<span data-ttu-id="4a46a-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Origami, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="4a46a-150">**To configure Azure AD single sign-on with Origami, perform the following steps:**</span></span>

1. <span data-ttu-id="4a46a-151">W portalu Azure na **Origami** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="4a46a-151">In the Azure portal, on the **Origami** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="4a46a-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="4a46a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-origami-tutorial/tutorial_origami_samlbase.png)

3. <span data-ttu-id="4a46a-155">Na **Origami domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="4a46a-155">On the **Origami Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-origami-tutorial/tutorial_origami_url.png)

    <span data-ttu-id="4a46a-157">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://live.origamirisk.com/origami/account/login?account=<companyname>`</span><span class="sxs-lookup"><span data-stu-id="4a46a-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://live.origamirisk.com/origami/account/login?account=<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4a46a-158">Wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="4a46a-158">The value is not real.</span></span> <span data-ttu-id="4a46a-159">Zaktualizuj tę wartość z adresem URL logowania rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="4a46a-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="4a46a-160">Skontaktuj się z [zespołem pomocy technicznej klienta Origami](https://wordpress.org/support/theme/origami) można uzyskać wartość.</span><span class="sxs-lookup"><span data-stu-id="4a46a-160">Contact [Origami Client support team](https://wordpress.org/support/theme/origami) to get the value.</span></span> 
 
4. <span data-ttu-id="4a46a-161">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="4a46a-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-origami-tutorial/tutorial_origami_certificate.png) 

5. <span data-ttu-id="4a46a-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="4a46a-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-origami-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4a46a-165">Na **konfiguracji Origami** , kliknij przycisk **skonfigurować Origami** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="4a46a-165">On the **Origami Configuration** section, click **Configure Origami** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4a46a-166">Kopiuj **Sign-Out adresu URL i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="4a46a-166">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-origami-tutorial/tutorial_origami_configure.png) 

7. <span data-ttu-id="4a46a-168">Zaloguj się do konta Origami z prawami administratora.</span><span class="sxs-lookup"><span data-stu-id="4a46a-168">Log in to the Origami account with Admin rights.</span></span>

8. <span data-ttu-id="4a46a-169">W menu u góry kliknij **Admin**.</span><span class="sxs-lookup"><span data-stu-id="4a46a-169">In the menu on the top, click **Admin**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-origami-tutorial/tutorial_origami_51.png)

9. <span data-ttu-id="4a46a-171">Na stronie okna dialogowego konfiguracji na znak pojedynczego wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="4a46a-171">On the Single Sign On Setup dialog page, perform the following steps:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-origami-tutorial/tutorial_origami_531.png)

    <span data-ttu-id="4a46a-173">a.</span><span class="sxs-lookup"><span data-stu-id="4a46a-173">a.</span></span> <span data-ttu-id="4a46a-174">Wybierz **włączenia funkcji logowania jednokrotnego w**.</span><span class="sxs-lookup"><span data-stu-id="4a46a-174">Select **Enable Single Sign On**.</span></span>

    <span data-ttu-id="4a46a-175">b.</span><span class="sxs-lookup"><span data-stu-id="4a46a-175">b.</span></span> <span data-ttu-id="4a46a-176">W **dostawcy tożsamości logowania URL strony** pole tekstowe, Wklej wartość **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="4a46a-176">In the **Identity Provider's Sign-in Page URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="4a46a-177">c.</span><span class="sxs-lookup"><span data-stu-id="4a46a-177">c.</span></span> <span data-ttu-id="4a46a-178">W **adres URL strony Sign-out dostawcy tożsamości** pole tekstowe, Wklej wartość **Sign-Out URL**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="4a46a-178">In the **Identity Provider's Sign-out Page URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="4a46a-179">d.</span><span class="sxs-lookup"><span data-stu-id="4a46a-179">d.</span></span> <span data-ttu-id="4a46a-180">Kliknij przycisk **Przeglądaj** można przekazać certyfikatu został pobrany z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="4a46a-180">Click **Browse** to upload the certificate you have downloaded from the Azure portal.</span></span>

    <span data-ttu-id="4a46a-181">e.</span><span class="sxs-lookup"><span data-stu-id="4a46a-181">e.</span></span> <span data-ttu-id="4a46a-182">Kliknij przycisk **zapisać zmiany**.</span><span class="sxs-lookup"><span data-stu-id="4a46a-182">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="4a46a-183">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="4a46a-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4a46a-184">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="4a46a-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4a46a-185">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4a46a-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4a46a-186">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a46a-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="4a46a-187">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="4a46a-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="4a46a-189">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="4a46a-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4a46a-190">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="4a46a-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-origami-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4a46a-192">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="4a46a-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-origami-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4a46a-194">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4a46a-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-origami-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4a46a-196">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="4a46a-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-origami-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4a46a-198">a.</span><span class="sxs-lookup"><span data-stu-id="4a46a-198">a.</span></span> <span data-ttu-id="4a46a-199">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4a46a-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4a46a-200">b.</span><span class="sxs-lookup"><span data-stu-id="4a46a-200">b.</span></span> <span data-ttu-id="4a46a-201">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4a46a-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4a46a-202">c.</span><span class="sxs-lookup"><span data-stu-id="4a46a-202">c.</span></span> <span data-ttu-id="4a46a-203">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="4a46a-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4a46a-204">d.</span><span class="sxs-lookup"><span data-stu-id="4a46a-204">d.</span></span> <span data-ttu-id="4a46a-205">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="4a46a-205">Click **Create**.</span></span>
 
### <a name="creating-an-origami-test-user"></a><span data-ttu-id="4a46a-206">Tworzenie użytkownika testowego Origami</span><span class="sxs-lookup"><span data-stu-id="4a46a-206">Creating an Origami test user</span></span>

<span data-ttu-id="4a46a-207">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Origami.</span><span class="sxs-lookup"><span data-stu-id="4a46a-207">In this section, you create a user called Britta Simon in Origami.</span></span> 

1. <span data-ttu-id="4a46a-208">Zaloguj się do konta Origami z prawami administratora.</span><span class="sxs-lookup"><span data-stu-id="4a46a-208">Log in to the Origami account with Admin rights.</span></span>

2. <span data-ttu-id="4a46a-209">W menu u góry kliknij **Admin**.</span><span class="sxs-lookup"><span data-stu-id="4a46a-209">In the menu on the top, click **Admin**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-origami-tutorial/tutorial_origami_51.png)

3. <span data-ttu-id="4a46a-211">Na **użytkowników i zabezpieczeń** okna dialogowego, kliknij przycisk **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="4a46a-211">On the **Users and Security** dialog, click **Users**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-origami-tutorial/tutorial_origami_54.png)

4. <span data-ttu-id="4a46a-213">Kliknij przycisk **Dodaj nowego użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="4a46a-213">Click **Add New User**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-origami-tutorial/tutorial_origami_55.png)

5. <span data-ttu-id="4a46a-215">W oknie dialogowym Dodawanie nowego użytkownika wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="4a46a-215">On the Add New User dialog, perform the following steps:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-origami-tutorial/tutorial_origami_56.png)

    <span data-ttu-id="4a46a-217">a.</span><span class="sxs-lookup"><span data-stu-id="4a46a-217">a.</span></span> <span data-ttu-id="4a46a-218">W **nazwy użytkownika** pole tekstowe, wprowadź adres e-mail użytkownika, takich jak  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="4a46a-218">In the **User Name** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="4a46a-219">b.</span><span class="sxs-lookup"><span data-stu-id="4a46a-219">b.</span></span> <span data-ttu-id="4a46a-220">W **hasło** tekstowym, wpisz hasło.</span><span class="sxs-lookup"><span data-stu-id="4a46a-220">In the **Password** textbox, type a password.</span></span>

    <span data-ttu-id="4a46a-221">c.</span><span class="sxs-lookup"><span data-stu-id="4a46a-221">c.</span></span> <span data-ttu-id="4a46a-222">W **Potwierdź hasło** tekstowym, wpisz hasło ponownie.</span><span class="sxs-lookup"><span data-stu-id="4a46a-222">In the **Confirm Password** textbox, type the password again.</span></span>

    <span data-ttu-id="4a46a-223">d.</span><span class="sxs-lookup"><span data-stu-id="4a46a-223">d.</span></span> <span data-ttu-id="4a46a-224">W **imię** pole tekstowe, wprowadź imię użytkownika, takich jak **Britta**.</span><span class="sxs-lookup"><span data-stu-id="4a46a-224">In the **First Name** textbox, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="4a46a-225">e.</span><span class="sxs-lookup"><span data-stu-id="4a46a-225">e.</span></span> <span data-ttu-id="4a46a-226">W **nazwisko** pole tekstowe, wprowadź nazwisko użytkownika, takich jak **Simona**.</span><span class="sxs-lookup"><span data-stu-id="4a46a-226">In the **Last Name** textbox, enter the last name of user like **Simon**.</span></span>

    <span data-ttu-id="4a46a-227">f.</span><span class="sxs-lookup"><span data-stu-id="4a46a-227">f.</span></span> <span data-ttu-id="4a46a-228">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="4a46a-228">Click **Save**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-origami-tutorial/tutorial_origami_57.png)

6. <span data-ttu-id="4a46a-230">Przypisz **ról użytkownika** i **dostępu klienta** dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4a46a-230">Assign **User Roles** and **Client Access** to the user.</span></span> 
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-origami-tutorial/tutorial_origami_58.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4a46a-232">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a46a-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4a46a-233">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Origami.</span><span class="sxs-lookup"><span data-stu-id="4a46a-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Origami.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="4a46a-235">**Aby przypisać Simona Britta Origami, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="4a46a-235">**To assign Britta Simon to Origami, perform the following steps:**</span></span>

1. <span data-ttu-id="4a46a-236">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="4a46a-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="4a46a-238">Na liście aplikacji zaznacz **Origami**.</span><span class="sxs-lookup"><span data-stu-id="4a46a-238">In the applications list, select **Origami**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-origami-tutorial/tutorial_origami_app.png) 

3. <span data-ttu-id="4a46a-240">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="4a46a-240">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="4a46a-242">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="4a46a-242">Click **Add** button.</span></span> <span data-ttu-id="4a46a-243">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4a46a-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="4a46a-245">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="4a46a-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4a46a-246">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4a46a-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4a46a-247">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4a46a-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4a46a-248">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="4a46a-248">Testing single sign-on</span></span>

<span data-ttu-id="4a46a-249">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="4a46a-249">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="4a46a-250">Po kliknięciu kafelka Origami w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Origami.</span><span class="sxs-lookup"><span data-stu-id="4a46a-250">When you click the Origami tile in the Access Panel, you should get automatically signed-on to your Origami application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4a46a-251">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="4a46a-251">Additional resources</span></span>

* [<span data-ttu-id="4a46a-252">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4a46a-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4a46a-253">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4a46a-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-origami-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-origami-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-origami-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-origami-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-origami-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-origami-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-origami-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-origami-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-origami-tutorial/tutorial_general_203.png

