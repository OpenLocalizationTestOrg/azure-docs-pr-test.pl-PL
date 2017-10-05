---
title: "Samouczek: Integracji Azure Active Directory z platformą Capriza | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Capriza platformy."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 48d92247-f00a-47b9-8d4e-137028d9e200
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 668c094d5330be1c5f71d51d2e76170dc69d1bce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-capriza-platform"></a><span data-ttu-id="f9c01-103">Samouczek: Integracji Azure Active Directory z platformą Capriza</span><span class="sxs-lookup"><span data-stu-id="f9c01-103">Tutorial: Azure Active Directory integration with Capriza Platform</span></span>

<span data-ttu-id="f9c01-104">Z tego samouczka dowiesz się sposobu integracji z usługą Azure Active Directory (Azure AD) Capriza platformy.</span><span class="sxs-lookup"><span data-stu-id="f9c01-104">In this tutorial, you learn how to integrate Capriza Platform with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f9c01-105">Integracja z usługą Azure AD platformy Capriza zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="f9c01-105">Integrating Capriza Platform with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f9c01-106">Można kontrolować w usłudze Azure AD, który ma dostęp do platformy Capriza</span><span class="sxs-lookup"><span data-stu-id="f9c01-106">You can control in Azure AD who has access to Capriza Platform</span></span>
- <span data-ttu-id="f9c01-107">Umożliwia użytkownikom automatycznie pobrać zalogowane Capriza platformy (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f9c01-107">You can enable your users to automatically get signed-on to Capriza Platform (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f9c01-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="f9c01-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f9c01-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f9c01-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f9c01-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f9c01-110">Prerequisites</span></span>

<span data-ttu-id="f9c01-111">Aby skonfigurować integrację usługi Azure AD z platformą Capriza, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="f9c01-111">To configure Azure AD integration with Capriza Platform, you need the following items:</span></span>

- <span data-ttu-id="f9c01-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f9c01-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f9c01-113">Platforma Capriza logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="f9c01-113">A Capriza Platform single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f9c01-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="f9c01-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f9c01-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="f9c01-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f9c01-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="f9c01-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f9c01-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f9c01-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f9c01-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="f9c01-118">Scenario description</span></span>
<span data-ttu-id="f9c01-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="f9c01-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f9c01-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="f9c01-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f9c01-121">Dodawanie platformy Capriza z galerii</span><span class="sxs-lookup"><span data-stu-id="f9c01-121">Adding Capriza Platform from the gallery</span></span>
2. <span data-ttu-id="f9c01-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="f9c01-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-capriza-platform-from-the-gallery"></a><span data-ttu-id="f9c01-123">Dodawanie platformy Capriza z galerii</span><span class="sxs-lookup"><span data-stu-id="f9c01-123">Adding Capriza Platform from the gallery</span></span>
<span data-ttu-id="f9c01-124">Aby skonfigurować integrację usługi Azure AD Capriza platformy, należy dodać platformy Capriza z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="f9c01-124">To configure the integration of Capriza Platform into Azure AD, you need to add Capriza Platform from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f9c01-125">**Aby dodać platformy Capriza z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f9c01-125">**To add Capriza Platform from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f9c01-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="f9c01-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="f9c01-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="f9c01-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f9c01-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="f9c01-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="f9c01-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f9c01-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="f9c01-133">W polu wyszukiwania wpisz **platformy Capriza**.</span><span class="sxs-lookup"><span data-stu-id="f9c01-133">In the search box, type **Capriza Platform**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_search.png)

5. <span data-ttu-id="f9c01-135">W panelu wyników wybierz **platformy Capriza**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="f9c01-135">In the results panel, select **Capriza Platform**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f9c01-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="f9c01-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f9c01-138">W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z platformą Capriza oparte na użytkownika testowego o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="f9c01-138">In this section, you configure and test Azure AD single sign-on with Capriza Platform based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f9c01-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednikiem platformy Capriza jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f9c01-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Capriza Platform is to a user in Azure AD.</span></span> <span data-ttu-id="f9c01-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i danemu użytkownikowi na platformie Capriza musi określone.</span><span class="sxs-lookup"><span data-stu-id="f9c01-140">In other words, a link relationship between an Azure AD user and the related user in Capriza Platform needs to be established.</span></span>

<span data-ttu-id="f9c01-141">Capriza platformy, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="f9c01-141">In Capriza Platform, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f9c01-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z platformą Capriza, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="f9c01-142">To configure and test Azure AD single sign-on with Capriza Platform, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f9c01-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="f9c01-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f9c01-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="f9c01-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f9c01-145">**[Tworzenie użytkownika testowego platformy Capriza](#creating-a-capriza-platform-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Capriza platforma, która jest połączona z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f9c01-145">**[Creating a Capriza Platform test user](#creating-a-capriza-platform-test-user)** - to have a counterpart of Britta Simon in Capriza Platform that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f9c01-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="f9c01-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f9c01-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="f9c01-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f9c01-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="f9c01-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f9c01-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne do aplikacji platformy Capriza.</span><span class="sxs-lookup"><span data-stu-id="f9c01-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Capriza Platform application.</span></span>

<span data-ttu-id="f9c01-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z platformą Capriza, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f9c01-150">**To configure Azure AD single sign-on with Capriza Platform, perform the following steps:**</span></span>

1. <span data-ttu-id="f9c01-151">W portalu Azure na **platformy Capriza** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="f9c01-151">In the Azure portal, on the **Capriza Platform** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="f9c01-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="f9c01-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_samlbase.png)

3. <span data-ttu-id="f9c01-155">Na **Capriza platformy domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f9c01-155">On the **Capriza Platform Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_url.png)

    <span data-ttu-id="f9c01-157">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.capriza.com/<tenantid>`</span><span class="sxs-lookup"><span data-stu-id="f9c01-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.capriza.com/<tenantid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f9c01-158">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="f9c01-158">This value is not real.</span></span> <span data-ttu-id="f9c01-159">Zaktualizuj tę wartość przy rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="f9c01-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="f9c01-160">Skontaktuj się z [zespołem pomocy technicznej klienta platformy Capriza](mailTo:support@capriza.com) aby zyskać tę wartość.</span><span class="sxs-lookup"><span data-stu-id="f9c01-160">Contact [Capriza Platform Client support team](mailTo:support@capriza.com) to get this value.</span></span> 

4. <span data-ttu-id="f9c01-161">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="f9c01-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_certificate.png) 

5. <span data-ttu-id="f9c01-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f9c01-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-capriza-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f9c01-165">Na **konfiguracji platformy Capriza** , kliknij przycisk **Konfigurowanie platformy Capriza** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="f9c01-165">On the **Capriza Platform Configuration** section, click **Configure Capriza Platform** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f9c01-166">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="f9c01-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_configure.png) 

7. <span data-ttu-id="f9c01-168">Skonfigurować logowanie jednokrotne w **Capriza platformy** stronie, musisz wysłać pobrany **certyfikatu**, **Sign-Out adres URL**, **identyfikator jednostki SAML** i **SAML pojedynczy znak na adres URL usługi** do [zespołem pomocy technicznej platformy Capriza](mailTo:support@capriza.com).</span><span class="sxs-lookup"><span data-stu-id="f9c01-168">To configure single sign-on on **Capriza Platform** side, you need to send the downloaded **Certificate**, **Sign-Out URL**, **SAML Entity ID** and **SAML Single Sign-On Service URL** to [Capriza Platform support team](mailTo:support@capriza.com).</span></span> <span data-ttu-id="f9c01-169">To ustawienie, aby były prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one wartość.</span><span class="sxs-lookup"><span data-stu-id="f9c01-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="f9c01-170">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="f9c01-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f9c01-171">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="f9c01-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f9c01-172">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f9c01-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f9c01-173">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f9c01-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="f9c01-174">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="f9c01-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="f9c01-176">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f9c01-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f9c01-177">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="f9c01-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-capriza-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f9c01-179">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="f9c01-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-capriza-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f9c01-181">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f9c01-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-capriza-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f9c01-183">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f9c01-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-capriza-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f9c01-185">a.</span><span class="sxs-lookup"><span data-stu-id="f9c01-185">a.</span></span> <span data-ttu-id="f9c01-186">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f9c01-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f9c01-187">b.</span><span class="sxs-lookup"><span data-stu-id="f9c01-187">b.</span></span> <span data-ttu-id="f9c01-188">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f9c01-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f9c01-189">c.</span><span class="sxs-lookup"><span data-stu-id="f9c01-189">c.</span></span> <span data-ttu-id="f9c01-190">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="f9c01-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f9c01-191">d.</span><span class="sxs-lookup"><span data-stu-id="f9c01-191">d.</span></span> <span data-ttu-id="f9c01-192">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="f9c01-192">Click **Create**.</span></span>
 
### <a name="creating-a-capriza-platform-test-user"></a><span data-ttu-id="f9c01-193">Tworzenie użytkownika testowego Capriza platformy</span><span class="sxs-lookup"><span data-stu-id="f9c01-193">Creating a Capriza Platform test user</span></span>

<span data-ttu-id="f9c01-194">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w Capriza.</span><span class="sxs-lookup"><span data-stu-id="f9c01-194">The objective of this section is to create a user called Britta Simon in Capriza.</span></span> <span data-ttu-id="f9c01-195">Capriza obsługę w czasie, który jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="f9c01-195">Capriza supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="f9c01-196">**Upewnij się, że nazwa domeny jest skonfigurowany z Capriza dla Inicjowanie obsługi użytkowników. Po wykonaniu tej działa tylko w czasie Inicjowanie obsługi użytkowników.**</span><span class="sxs-lookup"><span data-stu-id="f9c01-196">**Please make sure that your domain name is configured with Capriza for user provisioning. After that only the just-in-time user provisioning will work.**</span></span>

<span data-ttu-id="f9c01-197">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="f9c01-197">There is no action item for you in this section.</span></span> <span data-ttu-id="f9c01-198">Nowy użytkownik zostanie utworzony podczas próby dostępu Capriza, jeśli go jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="f9c01-198">A new user will be created during an attempt to access Capriza if it doesn't exist yet.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f9c01-199">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f9c01-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f9c01-200">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do platformy Capriza.</span><span class="sxs-lookup"><span data-stu-id="f9c01-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Capriza Platform.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="f9c01-202">**Aby przypisać Simona Britta Capriza platformy, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f9c01-202">**To assign Britta Simon to Capriza Platform, perform the following steps:**</span></span>

1. <span data-ttu-id="f9c01-203">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="f9c01-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="f9c01-205">Na liście aplikacji zaznacz **platformy Capriza**.</span><span class="sxs-lookup"><span data-stu-id="f9c01-205">In the applications list, select **Capriza Platform**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_app.png) 

3. <span data-ttu-id="f9c01-207">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="f9c01-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="f9c01-209">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f9c01-209">Click **Add** button.</span></span> <span data-ttu-id="f9c01-210">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f9c01-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="f9c01-212">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="f9c01-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f9c01-213">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f9c01-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f9c01-214">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f9c01-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f9c01-215">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="f9c01-215">Testing single sign-on</span></span>

<span data-ttu-id="f9c01-216">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="f9c01-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f9c01-217">Po kliknięciu kafelka Capriza platformy w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Capriza.</span><span class="sxs-lookup"><span data-stu-id="f9c01-217">When you click the Capriza Platform tile in the Access Panel, you should get automatically signed-on to your Capriza application.</span></span> <span data-ttu-id="f9c01-218">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f9c01-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f9c01-219">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="f9c01-219">Additional resources</span></span>

* [<span data-ttu-id="f9c01-220">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f9c01-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f9c01-221">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f9c01-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_203.png

