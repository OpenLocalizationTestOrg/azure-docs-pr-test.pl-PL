---
title: 'Samouczek: Integracji Azure Active Directory z HappyFox | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i HappyFox."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8204ee77-f64b-4fac-b64a-25ea534feac0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jeedes
ms.openlocfilehash: 8b5ad750d7849e4037ed7ee93c48b5645c68e799
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-happyfox"></a><span data-ttu-id="c6585-103">Samouczek: Integracji Azure Active Directory z HappyFox</span><span class="sxs-lookup"><span data-stu-id="c6585-103">Tutorial: Azure Active Directory integration with HappyFox</span></span>

<span data-ttu-id="c6585-104">Z tego samouczka dowiesz się integrowanie HappyFox z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c6585-104">In this tutorial, you learn how to integrate HappyFox with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c6585-105">Integracja z usługą Azure AD HappyFox zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="c6585-105">Integrating HappyFox with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c6585-106">Można kontrolować w usłudze Azure AD, który ma dostęp do HappyFox</span><span class="sxs-lookup"><span data-stu-id="c6585-106">You can control in Azure AD who has access to HappyFox</span></span>
- <span data-ttu-id="c6585-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do HappyFox (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6585-107">You can enable your users to automatically get signed-on to HappyFox (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c6585-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c6585-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c6585-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c6585-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c6585-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c6585-110">Prerequisites</span></span>

<span data-ttu-id="c6585-111">Aby skonfigurować integrację usługi Azure AD z HappyFox, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="c6585-111">To configure Azure AD integration with HappyFox, you need the following items:</span></span>

- <span data-ttu-id="c6585-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6585-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c6585-113">HappyFox jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="c6585-113">A HappyFox single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c6585-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="c6585-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c6585-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="c6585-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c6585-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="c6585-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c6585-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c6585-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c6585-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="c6585-118">Scenario description</span></span>
<span data-ttu-id="c6585-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="c6585-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c6585-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="c6585-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c6585-121">Dodawanie HappyFox z galerii</span><span class="sxs-lookup"><span data-stu-id="c6585-121">Adding HappyFox from the gallery</span></span>
2. <span data-ttu-id="c6585-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="c6585-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-happyfox-from-the-gallery"></a><span data-ttu-id="c6585-123">Dodawanie HappyFox z galerii</span><span class="sxs-lookup"><span data-stu-id="c6585-123">Adding HappyFox from the gallery</span></span>
<span data-ttu-id="c6585-124">Aby skonfigurować integrację usługi Azure AD HappyFox, należy dodać HappyFox z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="c6585-124">To configure the integration of HappyFox into Azure AD, you need to add HappyFox from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c6585-125">**Aby dodać HappyFox z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c6585-125">**To add HappyFox from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c6585-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="c6585-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="c6585-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="c6585-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c6585-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="c6585-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="c6585-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c6585-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="c6585-133">W polu wyszukiwania wpisz **HappyFox**.</span><span class="sxs-lookup"><span data-stu-id="c6585-133">In the search box, type **HappyFox**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_search.png)

5. <span data-ttu-id="c6585-135">W panelu wyników wybierz **HappyFox**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="c6585-135">In the results panel, select **HappyFox**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c6585-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="c6585-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c6585-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z HappyFox na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="c6585-138">In this section, you configure and test Azure AD single sign-on with HappyFox based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c6585-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w HappyFox jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c6585-139">For single sign-on to work, Azure AD needs to know what the counterpart user in HappyFox is to a user in Azure AD.</span></span> <span data-ttu-id="c6585-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w HappyFox musi się.</span><span class="sxs-lookup"><span data-stu-id="c6585-140">In other words, a link relationship between an Azure AD user and the related user in HappyFox needs to be established.</span></span>

<span data-ttu-id="c6585-141">W HappyFox, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="c6585-141">In HappyFox, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c6585-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z HappyFox, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="c6585-142">To configure and test Azure AD single sign-on with HappyFox, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c6585-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="c6585-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c6585-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="c6585-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c6585-145">**[Tworzenie użytkownika testowego HappyFox](#creating-a-happyfox-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta HappyFox połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c6585-145">**[Creating a HappyFox test user](#creating-a-happyfox-test-user)** - to have a counterpart of Britta Simon in HappyFox that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c6585-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="c6585-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c6585-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="c6585-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c6585-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="c6585-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c6585-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji HappyFox.</span><span class="sxs-lookup"><span data-stu-id="c6585-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your HappyFox application.</span></span>

<span data-ttu-id="c6585-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z HappyFox, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c6585-150">**To configure Azure AD single sign-on with HappyFox, perform the following steps:**</span></span>

1. <span data-ttu-id="c6585-151">W portalu Azure na **HappyFox** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="c6585-151">In the Azure portal, on the **HappyFox** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="c6585-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="c6585-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_samlbase.png)

3. <span data-ttu-id="c6585-155">Na **HappyFox domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c6585-155">On the **HappyFox Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_url.png)

    <span data-ttu-id="c6585-157">a.</span><span class="sxs-lookup"><span data-stu-id="c6585-157">a.</span></span> <span data-ttu-id="c6585-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.happyfox.com/`</span><span class="sxs-lookup"><span data-stu-id="c6585-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.happyfox.com/`</span></span>

    <span data-ttu-id="c6585-159">b.</span><span class="sxs-lookup"><span data-stu-id="c6585-159">b.</span></span> <span data-ttu-id="c6585-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.happyfox.com/saml/metadata/`</span><span class="sxs-lookup"><span data-stu-id="c6585-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.happyfox.com/saml/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c6585-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="c6585-161">These values are not real.</span></span> <span data-ttu-id="c6585-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="c6585-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c6585-163">Skontaktuj się z [zespołem pomocy technicznej klienta HappyFox](https://support.happyfox.com/home) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="c6585-163">Contact [HappyFox Client support team](https://support.happyfox.com/home) to get these values.</span></span> 
 
4. <span data-ttu-id="c6585-164">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="c6585-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the Certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_certificate.png) 

5. <span data-ttu-id="c6585-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c6585-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-happyfox-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c6585-168">Na **konfiguracji HappyFox** , kliknij przycisk **skonfigurować HappyFox** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="c6585-168">On the **HappyFox Configuration** section, click **Configure HappyFox** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c6585-169">Kopiuj **SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami**.</span><span class="sxs-lookup"><span data-stu-id="c6585-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_configure.png) 

7. <span data-ttu-id="c6585-171">Zaloguj się do swojego portalu dla personelu HappyFox i przejdź do **Zarządzaj**, kliknij **integracji** kartę.</span><span class="sxs-lookup"><span data-stu-id="c6585-171">Sign on to your HappyFox staff portal and navigate to **Manage**, Click on **Integrations** tab.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-happyfox-tutorial/header.png) 

8. <span data-ttu-id="c6585-173">Na karcie integracji kliknij **Konfiguruj** w obszarze **integrację SAML** otworzyć pojedynczy znak na ustawienia.</span><span class="sxs-lookup"><span data-stu-id="c6585-173">In the Integrations tab, Click **Configure** under **SAML Integration** to open the Single Sign On Settings.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-happyfox-tutorial/configure.png) 

9. <span data-ttu-id="c6585-175">W sekcji konfiguracji SAML, Wklej **SAML pojedynczy znak na adres URL usługi** skopiowanego z portalu Azure do **logowania jednokrotnego, docelowy adres URL** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="c6585-175">Inside SAML configuration section, paste the **SAML Single Sign-On Service URL** that you have copied from Azure portal into **SSO Target URL** textbox.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-happyfox-tutorial/targeturl.png)

10. <span data-ttu-id="c6585-177">Otwórz certyfikat pobrany z portalu Azure w programie Notatnik i Wklej zawartość w **podpisu IdP** sekcji.</span><span class="sxs-lookup"><span data-stu-id="c6585-177">Open the certificate downloaded from Azure portal in notepad and paste its content in **IdP Signature** section.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-happyfox-tutorial/cert.png)

11. <span data-ttu-id="c6585-179">Kliknij przycisk **Zapisz ustawienia** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c6585-179">Click **Save Settings** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-happyfox-tutorial/savesettings.png)

> [!TIP]
> <span data-ttu-id="c6585-181">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="c6585-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c6585-182">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="c6585-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c6585-183">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c6585-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c6585-184">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6585-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="c6585-185">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="c6585-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="c6585-187">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c6585-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c6585-188">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="c6585-188">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-happyfox-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c6585-190">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="c6585-190">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-happyfox-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c6585-192">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c6585-192">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-happyfox-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c6585-194">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c6585-194">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-happyfox-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c6585-196">a.</span><span class="sxs-lookup"><span data-stu-id="c6585-196">a.</span></span> <span data-ttu-id="c6585-197">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c6585-197">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c6585-198">b.</span><span class="sxs-lookup"><span data-stu-id="c6585-198">b.</span></span> <span data-ttu-id="c6585-199">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c6585-199">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c6585-200">c.</span><span class="sxs-lookup"><span data-stu-id="c6585-200">c.</span></span> <span data-ttu-id="c6585-201">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="c6585-201">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c6585-202">d.</span><span class="sxs-lookup"><span data-stu-id="c6585-202">d.</span></span> <span data-ttu-id="c6585-203">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="c6585-203">Click **Create**.</span></span>
 
### <a name="creating-a-happyfox-test-user"></a><span data-ttu-id="c6585-204">Tworzenie użytkownika testowego HappyFox</span><span class="sxs-lookup"><span data-stu-id="c6585-204">Creating a HappyFox test user</span></span>

<span data-ttu-id="c6585-205">Aplikacja obsługuje tylko w czasie Inicjowanie obsługi użytkowników i uwierzytelnianie użytkowników są tworzone automatycznie w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c6585-205">Application supports Just in time user provisioning and after authentication users are created in the application automatically.</span></span>
        
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c6585-206">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6585-206">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c6585-207">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu HappyFox.</span><span class="sxs-lookup"><span data-stu-id="c6585-207">In this section, you enable Britta Simon to use Azure single sign-on by granting access to HappyFox.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="c6585-209">**Aby przypisać Simona Britta HappyFox, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c6585-209">**To assign Britta Simon to HappyFox, perform the following steps:**</span></span>

1. <span data-ttu-id="c6585-210">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="c6585-210">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="c6585-212">Na liście aplikacji zaznacz **HappyFox**.</span><span class="sxs-lookup"><span data-stu-id="c6585-212">In the applications list, select **HappyFox**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_app.png) 

3. <span data-ttu-id="c6585-214">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="c6585-214">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="c6585-216">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c6585-216">Click **Add** button.</span></span> <span data-ttu-id="c6585-217">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c6585-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="c6585-219">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="c6585-219">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c6585-220">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c6585-220">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c6585-221">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c6585-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c6585-222">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="c6585-222">Testing single sign-on</span></span>

<span data-ttu-id="c6585-223">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="c6585-223">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

1. <span data-ttu-id="c6585-224">Po kliknięciu kafelka HappyFox w panelu dostępu, należy pobrać strony logowania HappyFox aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c6585-224">When you click the HappyFox tile in the Access Panel, you should get login page of HappyFox application.</span></span> <span data-ttu-id="c6585-225">Powinny pojawić się **"SAML"** przycisk na stronie logowania.</span><span class="sxs-lookup"><span data-stu-id="c6585-225">You should see the **‘SAML’** button on the sign-in page.</span></span>

    ![Wtyczki](./media/active-directory-saas-happyfox-tutorial/saml.png) 

2. <span data-ttu-id="c6585-227">Kliknij przycisk **"SAML"** przycisk, aby zalogować się do HappyFox przy użyciu konta usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c6585-227">Click the **‘SAML’** button to log in to HappyFox using your Azure AD account.</span></span>

<span data-ttu-id="c6585-228">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c6585-228">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c6585-229">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="c6585-229">Additional resources</span></span>

* [<span data-ttu-id="c6585-230">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c6585-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c6585-231">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c6585-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_203.png

