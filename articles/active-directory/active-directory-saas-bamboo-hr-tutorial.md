---
title: 'Samouczek: Integracji Azure Active Directory z BambooHR | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i BambooHR."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f826b5d2-9c64-47df-bbbf-0adf9eb0fa71
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: jeedes
ms.openlocfilehash: 06bf91b0e598fd3d8e644378efdb753611ee1ebc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bamboohr"></a><span data-ttu-id="b2c26-103">Samouczek: Integracji Azure Active Directory z BambooHR</span><span class="sxs-lookup"><span data-stu-id="b2c26-103">Tutorial: Azure Active Directory integration with BambooHR</span></span>

<span data-ttu-id="b2c26-104">Z tego samouczka dowiesz się integrowanie BambooHR z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b2c26-104">In this tutorial, you learn how to integrate BambooHR with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b2c26-105">Integracja z usługą Azure AD BambooHR zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="b2c26-105">Integrating BambooHR with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b2c26-106">Można kontrolować w usłudze Azure AD, który ma dostęp do BambooHR</span><span class="sxs-lookup"><span data-stu-id="b2c26-106">You can control in Azure AD who has access to BambooHR</span></span>
- <span data-ttu-id="b2c26-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do BambooHR (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b2c26-107">You can enable your users to automatically get signed-on to BambooHR (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b2c26-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="b2c26-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b2c26-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b2c26-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b2c26-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b2c26-110">Prerequisites</span></span>

<span data-ttu-id="b2c26-111">Aby skonfigurować integrację usługi Azure AD z BambooHR, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="b2c26-111">To configure Azure AD integration with BambooHR, you need the following items:</span></span>

- <span data-ttu-id="b2c26-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b2c26-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b2c26-113">BambooHR jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="b2c26-113">A BambooHR single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b2c26-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="b2c26-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b2c26-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="b2c26-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b2c26-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="b2c26-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b2c26-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b2c26-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b2c26-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="b2c26-118">Scenario description</span></span>
<span data-ttu-id="b2c26-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="b2c26-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b2c26-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="b2c26-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b2c26-121">Dodawanie BambooHR z galerii</span><span class="sxs-lookup"><span data-stu-id="b2c26-121">Adding BambooHR from the gallery</span></span>
2. <span data-ttu-id="b2c26-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="b2c26-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bamboohr-from-the-gallery"></a><span data-ttu-id="b2c26-123">Dodawanie BambooHR z galerii</span><span class="sxs-lookup"><span data-stu-id="b2c26-123">Adding BambooHR from the gallery</span></span>
<span data-ttu-id="b2c26-124">Aby skonfigurować integrację usługi Azure AD BambooHR, należy dodać BambooHR z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="b2c26-124">To configure the integration of BambooHR into Azure AD, you need to add BambooHR from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b2c26-125">**Aby dodać BambooHR z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="b2c26-125">**To add BambooHR from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b2c26-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="b2c26-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="b2c26-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="b2c26-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b2c26-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="b2c26-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="b2c26-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b2c26-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="b2c26-133">W polu wyszukiwania wpisz **BambooHR**.</span><span class="sxs-lookup"><span data-stu-id="b2c26-133">In the search box, type **BambooHR**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_search.png)

5. <span data-ttu-id="b2c26-135">W panelu wyników wybierz **BambooHR**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="b2c26-135">In the results panel, select **BambooHR**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b2c26-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="b2c26-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b2c26-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z BambooHR na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="b2c26-138">In this section, you configure and test Azure AD single sign-on with BambooHR based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b2c26-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w BambooHR jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b2c26-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BambooHR is to a user in Azure AD.</span></span> <span data-ttu-id="b2c26-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w BambooHR musi się.</span><span class="sxs-lookup"><span data-stu-id="b2c26-140">In other words, a link relationship between an Azure AD user and the related user in BambooHR needs to be established.</span></span>

<span data-ttu-id="b2c26-141">W BambooHR, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="b2c26-141">In BambooHR, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b2c26-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z BambooHR, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="b2c26-142">To configure and test Azure AD single sign-on with BambooHR, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b2c26-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="b2c26-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b2c26-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="b2c26-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b2c26-145">**[Tworzenie użytkownika testowego BambooHR](#creating-a-bamboohr-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta BambooHR połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b2c26-145">**[Creating a BambooHR test user](#creating-a-bamboohr-test-user)** - to have a counterpart of Britta Simon in BambooHR that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b2c26-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="b2c26-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b2c26-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="b2c26-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b2c26-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="b2c26-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b2c26-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji BambooHR.</span><span class="sxs-lookup"><span data-stu-id="b2c26-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BambooHR application.</span></span>

<span data-ttu-id="b2c26-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z BambooHR, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="b2c26-150">**To configure Azure AD single sign-on with BambooHR, perform the following steps:**</span></span>

1. <span data-ttu-id="b2c26-151">W portalu Azure na **BambooHR** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="b2c26-151">In the Azure portal, on the **BambooHR** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="b2c26-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="b2c26-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_samlbase.png)

3. <span data-ttu-id="b2c26-155">Na **BambooHR domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b2c26-155">On the **BambooHR Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_url.png)

    <span data-ttu-id="b2c26-157">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<company>.bamboohr.com`</span><span class="sxs-lookup"><span data-stu-id="b2c26-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company>.bamboohr.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="b2c26-158">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="b2c26-158">This value is not real.</span></span> <span data-ttu-id="b2c26-159">Zaktualizuj tę wartość przy rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="b2c26-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="b2c26-160">Skontaktuj się z [zespołem pomocy technicznej klienta BambooHR](https://www.bamboohr.com/contact.php) aby zyskać tę wartość.</span><span class="sxs-lookup"><span data-stu-id="b2c26-160">Contact [BambooHR Client support team](https://www.bamboohr.com/contact.php) to get this value.</span></span> 
 
4. <span data-ttu-id="b2c26-161">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="b2c26-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_certificate.png) 

5. <span data-ttu-id="b2c26-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b2c26-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b2c26-165">Na **konfiguracji BambooHR** , kliknij przycisk **skonfigurować BambooHR** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="b2c26-165">On the **BambooHR Configuration** section, click **Configure BambooHR** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b2c26-166">Kopiuj **SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="b2c26-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_configure.png) 

6. <span data-ttu-id="b2c26-168">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy BambooHR jako administrator.</span><span class="sxs-lookup"><span data-stu-id="b2c26-168">In a different web browser window, log into your BambooHR company site as an administrator.</span></span>

7. <span data-ttu-id="b2c26-169">Na stronie głównej wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b2c26-169">On the homepage, perform the following steps:</span></span>
   
    <span data-ttu-id="b2c26-170">![Logowanie jednokrotne](./media/active-directory-saas-bamboo-hr-tutorial/ic796691.png "logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="b2c26-170">![Single Sign-On](./media/active-directory-saas-bamboo-hr-tutorial/ic796691.png "Single Sign-On")</span></span>   

    <span data-ttu-id="b2c26-171">a.</span><span class="sxs-lookup"><span data-stu-id="b2c26-171">a.</span></span> <span data-ttu-id="b2c26-172">Kliknij przycisk **aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="b2c26-172">Click **Apps**.</span></span>
   
    <span data-ttu-id="b2c26-173">b.</span><span class="sxs-lookup"><span data-stu-id="b2c26-173">b.</span></span> <span data-ttu-id="b2c26-174">W menu aplikacji po lewej stronie kliknij **rejestracji jednokrotnej**.</span><span class="sxs-lookup"><span data-stu-id="b2c26-174">In the apps menu on the left, click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="b2c26-175">c.</span><span class="sxs-lookup"><span data-stu-id="b2c26-175">c.</span></span> <span data-ttu-id="b2c26-176">Kliknij przycisk **SAML logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="b2c26-176">Click **SAML Single Sign-On**.</span></span>

8. <span data-ttu-id="b2c26-177">W **SAML logowania jednokrotnego** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b2c26-177">In the **SAML Single Sign-On** section, perform the following steps:</span></span>
   
    <span data-ttu-id="b2c26-178">![SAML logowania jednokrotnego](./media/active-directory-saas-bamboo-hr-tutorial/ic796692.png "SAML logowania jednokrotnego")</span><span class="sxs-lookup"><span data-stu-id="b2c26-178">![SAML Single Sign-On](./media/active-directory-saas-bamboo-hr-tutorial/ic796692.png "SAML Single Sign-On")</span></span>
   
    <span data-ttu-id="b2c26-179">a.</span><span class="sxs-lookup"><span data-stu-id="b2c26-179">a.</span></span> <span data-ttu-id="b2c26-180">Wklej **SAML pojedynczy znak na adres URL usługi** wartości do **adres Url logowania jednokrotnego logowania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="b2c26-180">Paste the **SAML Single Sign-On Service URL** value into the **SSO Login Url** textbox.</span></span>
      
    <span data-ttu-id="b2c26-181">b.</span><span class="sxs-lookup"><span data-stu-id="b2c26-181">b.</span></span> <span data-ttu-id="b2c26-182">Otwórz zakodowanego certyfikatu base-64 pobrany z portalu Azure w programie Notatnik, skopiuj zawartość go do Schowka, a następnie wklej go do **certyfikatu X.509** pole tekstowe</span><span class="sxs-lookup"><span data-stu-id="b2c26-182">Open base-64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox</span></span>
   
    <span data-ttu-id="b2c26-183">c.</span><span class="sxs-lookup"><span data-stu-id="b2c26-183">c.</span></span> <span data-ttu-id="b2c26-184">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="b2c26-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="b2c26-185">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="b2c26-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b2c26-186">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="b2c26-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b2c26-187">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b2c26-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b2c26-188">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b2c26-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="b2c26-189">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="b2c26-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="b2c26-191">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="b2c26-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b2c26-192">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="b2c26-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b2c26-194">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="b2c26-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b2c26-196">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b2c26-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b2c26-198">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b2c26-198">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b2c26-200">a.</span><span class="sxs-lookup"><span data-stu-id="b2c26-200">a.</span></span> <span data-ttu-id="b2c26-201">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b2c26-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b2c26-202">b.</span><span class="sxs-lookup"><span data-stu-id="b2c26-202">b.</span></span> <span data-ttu-id="b2c26-203">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b2c26-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b2c26-204">c.</span><span class="sxs-lookup"><span data-stu-id="b2c26-204">c.</span></span> <span data-ttu-id="b2c26-205">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="b2c26-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b2c26-206">d.</span><span class="sxs-lookup"><span data-stu-id="b2c26-206">d.</span></span> <span data-ttu-id="b2c26-207">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="b2c26-207">Click **Create**.</span></span>
 
### <a name="creating-a-bamboohr-test-user"></a><span data-ttu-id="b2c26-208">Tworzenie użytkownika testowego BambooHR</span><span class="sxs-lookup"><span data-stu-id="b2c26-208">Creating a BambooHR test user</span></span>

<span data-ttu-id="b2c26-209">Aby umożliwić użytkownikom usługi Azure AD zalogować się do BambooHR, musi być przygotowana do BambooHR.</span><span class="sxs-lookup"><span data-stu-id="b2c26-209">To enable Azure AD users to log in to BambooHR, they must be provisioned into BambooHR.</span></span>  

<span data-ttu-id="b2c26-210">W przypadku BambooHR Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="b2c26-210">In the case of BambooHR, provisioning is a manual task.</span></span>

<span data-ttu-id="b2c26-211">**Aby udostępnić konta użytkownika, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="b2c26-211">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="b2c26-212">Zaloguj się do Twojego **BambooHR** lokacji jako administrator.</span><span class="sxs-lookup"><span data-stu-id="b2c26-212">Log in to your **BambooHR** site as administrator.</span></span>

2. <span data-ttu-id="b2c26-213">Na pasku narzędzi u góry kliknij **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="b2c26-213">In the toolbar on the top, click **Settings**.</span></span>
   
    <span data-ttu-id="b2c26-214">![Ustawienie](./media/active-directory-saas-bamboo-hr-tutorial/ic796694.png "ustawienie")</span><span class="sxs-lookup"><span data-stu-id="b2c26-214">![Setting](./media/active-directory-saas-bamboo-hr-tutorial/ic796694.png "Setting")</span></span>

3. <span data-ttu-id="b2c26-215">Kliknij przycisk **omówienie**.</span><span class="sxs-lookup"><span data-stu-id="b2c26-215">Click **Overview**.</span></span>

4. <span data-ttu-id="b2c26-216">W lewym okienku nawigacji, przejdź do **zabezpieczeń \> użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="b2c26-216">In the left navigation pane, go to **Security \> Users**.</span></span>

5. <span data-ttu-id="b2c26-217">Wpisz nazwę użytkownika, hasło i adres e-mail prawidłowego konta usługi AAD, który chcesz udostępnić do powiązanych pól tekstowych.</span><span class="sxs-lookup"><span data-stu-id="b2c26-217">Type the user name, password, and email address of a valid AAD account you want to provision into the related textboxes.</span></span>

6. <span data-ttu-id="b2c26-218">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="b2c26-218">Click **Save**.</span></span>
        
>[!NOTE]
><span data-ttu-id="b2c26-219">Możesz użyć innych BambooHR użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez BambooHR do kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="b2c26-219">You can use any other BambooHR user account creation tools or APIs provided by BambooHR to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b2c26-220">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b2c26-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b2c26-221">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu BambooHR.</span><span class="sxs-lookup"><span data-stu-id="b2c26-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BambooHR.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="b2c26-223">**Aby przypisać Simona Britta BambooHR, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="b2c26-223">**To assign Britta Simon to BambooHR, perform the following steps:**</span></span>

1. <span data-ttu-id="b2c26-224">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="b2c26-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="b2c26-226">Na liście aplikacji zaznacz **BambooHR**.</span><span class="sxs-lookup"><span data-stu-id="b2c26-226">In the applications list, select **BambooHR**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_app.png) 

3. <span data-ttu-id="b2c26-228">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="b2c26-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="b2c26-230">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b2c26-230">Click **Add** button.</span></span> <span data-ttu-id="b2c26-231">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b2c26-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="b2c26-233">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="b2c26-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b2c26-234">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b2c26-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b2c26-235">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b2c26-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b2c26-236">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="b2c26-236">Testing single sign-on</span></span>

<span data-ttu-id="b2c26-237">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="b2c26-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b2c26-238">Po kliknięciu kafelka BambooHR w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji BambooHR.</span><span class="sxs-lookup"><span data-stu-id="b2c26-238">When you click the BambooHR tile in the Access Panel, you should get automatically signed-on to your BambooHR application.</span></span>
<span data-ttu-id="b2c26-239">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b2c26-239">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b2c26-240">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="b2c26-240">Additional resources</span></span>

* [<span data-ttu-id="b2c26-241">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b2c26-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b2c26-242">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b2c26-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_203.png

