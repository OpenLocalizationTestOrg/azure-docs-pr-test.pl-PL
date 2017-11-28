---
title: 'Samouczek: Integracji Azure Active Directory z HireVue | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i HireVue."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: aadfc342-14db-4d74-a83d-f0c76f0cf63c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 682d88d3010f5781948a9adde0e1351471608a5e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hirevue"></a><span data-ttu-id="dccc0-103">Samouczek: Integracji Azure Active Directory z HireVue</span><span class="sxs-lookup"><span data-stu-id="dccc0-103">Tutorial: Azure Active Directory integration with HireVue</span></span>

<span data-ttu-id="dccc0-104">Z tego samouczka dowiesz się integrowanie HireVue z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dccc0-104">In this tutorial, you learn how to integrate HireVue with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dccc0-105">Integracja z usługą Azure AD HireVue zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="dccc0-105">Integrating HireVue with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="dccc0-106">Można kontrolować w usłudze Azure AD, który ma dostęp do HireVue</span><span class="sxs-lookup"><span data-stu-id="dccc0-106">You can control in Azure AD who has access to HireVue</span></span>
- <span data-ttu-id="dccc0-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do HireVue (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="dccc0-107">You can enable your users to automatically get signed-on to HireVue (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dccc0-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="dccc0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="dccc0-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dccc0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dccc0-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="dccc0-110">Prerequisites</span></span>

<span data-ttu-id="dccc0-111">Aby skonfigurować integrację usługi Azure AD z HireVue, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="dccc0-111">To configure Azure AD integration with HireVue, you need the following items:</span></span>

- <span data-ttu-id="dccc0-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="dccc0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dccc0-113">HireVue logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="dccc0-113">A HireVue single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dccc0-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="dccc0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dccc0-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="dccc0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dccc0-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="dccc0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dccc0-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dccc0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dccc0-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="dccc0-118">Scenario description</span></span>
<span data-ttu-id="dccc0-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="dccc0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dccc0-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="dccc0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dccc0-121">Dodawanie HireVue z galerii</span><span class="sxs-lookup"><span data-stu-id="dccc0-121">Adding HireVue from the gallery</span></span>
2. <span data-ttu-id="dccc0-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="dccc0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hirevue-from-the-gallery"></a><span data-ttu-id="dccc0-123">Dodawanie HireVue z galerii</span><span class="sxs-lookup"><span data-stu-id="dccc0-123">Adding HireVue from the gallery</span></span>
<span data-ttu-id="dccc0-124">Aby skonfigurować integrację usługi Azure AD HireVue, należy dodać HireVue z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="dccc0-124">To configure the integration of HireVue into Azure AD, you need to add HireVue from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="dccc0-125">**Aby dodać HireVue z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="dccc0-125">**To add HireVue from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="dccc0-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="dccc0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="dccc0-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="dccc0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="dccc0-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="dccc0-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="dccc0-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="dccc0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="dccc0-133">W polu wyszukiwania wpisz **HireVue**.</span><span class="sxs-lookup"><span data-stu-id="dccc0-133">In the search box, type **HireVue**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_search.png)

5. <span data-ttu-id="dccc0-135">W panelu wyników wybierz **HireVue**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="dccc0-135">In the results panel, select **HireVue**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dccc0-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="dccc0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dccc0-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z HireVue w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="dccc0-138">In this section, you configure and test Azure AD single sign-on with HireVue based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="dccc0-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w HireVue jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dccc0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in HireVue is to a user in Azure AD.</span></span> <span data-ttu-id="dccc0-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w HireVue musi się.</span><span class="sxs-lookup"><span data-stu-id="dccc0-140">In other words, a link relationship between an Azure AD user and the related user in HireVue needs to be established.</span></span>

<span data-ttu-id="dccc0-141">W HireVue, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="dccc0-141">In HireVue, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="dccc0-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z HireVue, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="dccc0-142">To configure and test Azure AD single sign-on with HireVue, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="dccc0-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="dccc0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="dccc0-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="dccc0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dccc0-145">**[Tworzenie użytkownika testowego HireVue](#creating-a-hirevue-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta HireVue połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="dccc0-145">**[Creating a HireVue test user](#creating-a-hirevue-test-user)** - to have a counterpart of Britta Simon in HireVue that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="dccc0-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="dccc0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dccc0-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="dccc0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dccc0-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="dccc0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dccc0-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji HireVue.</span><span class="sxs-lookup"><span data-stu-id="dccc0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your HireVue application.</span></span>

<span data-ttu-id="dccc0-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z HireVue, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="dccc0-150">**To configure Azure AD single sign-on with HireVue, perform the following steps:**</span></span>

1. <span data-ttu-id="dccc0-151">W portalu Azure na **HireVue** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="dccc0-151">In the Azure portal, on the **HireVue** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="dccc0-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="dccc0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_samlbase.png)

3. <span data-ttu-id="dccc0-155">Na **HireVue domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="dccc0-155">On the **HireVue Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_url.png)

    <span data-ttu-id="dccc0-157">a.</span><span class="sxs-lookup"><span data-stu-id="dccc0-157">a.</span></span> <span data-ttu-id="dccc0-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="dccc0-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>

    | <span data-ttu-id="dccc0-159">Środowisko</span><span class="sxs-lookup"><span data-stu-id="dccc0-159">Environment</span></span> | <span data-ttu-id="dccc0-160">ADRES URL</span><span class="sxs-lookup"><span data-stu-id="dccc0-160">URL</span></span> |
    |-------------|---|
    | <span data-ttu-id="dccc0-161">Produkcji</span><span class="sxs-lookup"><span data-stu-id="dccc0-161">Production</span></span> | `https://<companyname>.hirevue.com` |
    | <span data-ttu-id="dccc0-162">Przemieszczania</span><span class="sxs-lookup"><span data-stu-id="dccc0-162">Staging</span></span>    | `https://<companyname>.stghv.com` |
    
    <span data-ttu-id="dccc0-163">b.</span><span class="sxs-lookup"><span data-stu-id="dccc0-163">b.</span></span> <span data-ttu-id="dccc0-164">W **identyfikator** tekstowym, wpisz adres URL jako:</span><span class="sxs-lookup"><span data-stu-id="dccc0-164">In the **Identifier** textbox, type a URL as:</span></span>
    
    | <span data-ttu-id="dccc0-165">Środowisko</span><span class="sxs-lookup"><span data-stu-id="dccc0-165">Environment</span></span> | <span data-ttu-id="dccc0-166">URN</span><span class="sxs-lookup"><span data-stu-id="dccc0-166">URN</span></span> |
    |-------------|-----|
    | <span data-ttu-id="dccc0-167">Produkcji</span><span class="sxs-lookup"><span data-stu-id="dccc0-167">Production</span></span> |`urn:federation:hirevue.com:saml:sp:prod` |
    | <span data-ttu-id="dccc0-168">Przemieszczania</span><span class="sxs-lookup"><span data-stu-id="dccc0-168">Staging</span></span>    | `urn:federation:hirevue.com:saml:sp:staging`|
    
    > [!NOTE] 
    > <span data-ttu-id="dccc0-169">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="dccc0-169">These values are not real.</span></span> <span data-ttu-id="dccc0-170">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="dccc0-170">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="dccc0-171">Skontaktuj się z [zespołem pomocy technicznej klienta HireVue](mailto:samlsupport@hirevue.com) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="dccc0-171">Contact [HireVue Client support team](mailto:samlsupport@hirevue.com) to get these values.</span></span> 
 
4. <span data-ttu-id="dccc0-172">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="dccc0-172">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_certificate.png) 

5. <span data-ttu-id="dccc0-174">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="dccc0-174">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hirevue-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="dccc0-176">Na **konfiguracji HireVue** , kliknij przycisk **skonfigurować HireVue** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="dccc0-176">On the **HireVue Configuration** section, click **Configure HireVue** to open **Configure sign-on** window.</span></span> <span data-ttu-id="dccc0-177">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="dccc0-177">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_configure.png) 

7. <span data-ttu-id="dccc0-179">Skonfigurować logowanie jednokrotne w **HireVue** stronie, musisz wysłać pobrany **Certificate(Base64)** i **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** do [zespołem pomocy technicznej HireVue](mailto:samlsupport@hirevue.com).</span><span class="sxs-lookup"><span data-stu-id="dccc0-179">To configure single sign-on on **HireVue** side, you need to send the downloaded **Certificate(Base64)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [HireVue support team](mailto:samlsupport@hirevue.com).</span></span> <span data-ttu-id="dccc0-180">To ustawienie, aby były prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one wartość.</span><span class="sxs-lookup"><span data-stu-id="dccc0-180">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="dccc0-181">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="dccc0-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="dccc0-182">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="dccc0-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="dccc0-183">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="dccc0-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dccc0-184">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="dccc0-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="dccc0-185">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="dccc0-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="dccc0-187">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="dccc0-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="dccc0-188">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="dccc0-188">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hirevue-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dccc0-190">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="dccc0-190">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hirevue-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dccc0-192">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="dccc0-192">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hirevue-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dccc0-194">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="dccc0-194">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hirevue-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dccc0-196">a.</span><span class="sxs-lookup"><span data-stu-id="dccc0-196">a.</span></span> <span data-ttu-id="dccc0-197">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dccc0-197">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dccc0-198">b.</span><span class="sxs-lookup"><span data-stu-id="dccc0-198">b.</span></span> <span data-ttu-id="dccc0-199">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="dccc0-199">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dccc0-200">c.</span><span class="sxs-lookup"><span data-stu-id="dccc0-200">c.</span></span> <span data-ttu-id="dccc0-201">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="dccc0-201">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="dccc0-202">d.</span><span class="sxs-lookup"><span data-stu-id="dccc0-202">d.</span></span> <span data-ttu-id="dccc0-203">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="dccc0-203">Click **Create**.</span></span>
 
### <a name="creating-a-hirevue-test-user"></a><span data-ttu-id="dccc0-204">Tworzenie użytkownika testowego HireVue</span><span class="sxs-lookup"><span data-stu-id="dccc0-204">Creating a HireVue test user</span></span>

<span data-ttu-id="dccc0-205">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w HireVue.</span><span class="sxs-lookup"><span data-stu-id="dccc0-205">In this section, you create a user called Britta Simon in HireVue.</span></span> <span data-ttu-id="dccc0-206">We współpracy z [zespołem pomocy technicznej HireVue](mailto:samlsupport@hirevue.com) Aby dodać użytkowników do platformy HireVue.</span><span class="sxs-lookup"><span data-stu-id="dccc0-206">Please work with [HireVue support team](mailto:samlsupport@hirevue.com) to add the users in the HireVue platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="dccc0-207">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="dccc0-207">Assigning the Azure AD test user</span></span>

<span data-ttu-id="dccc0-208">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu HireVue.</span><span class="sxs-lookup"><span data-stu-id="dccc0-208">In this section, you enable Britta Simon to use Azure single sign-on by granting access to HireVue.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="dccc0-210">**Aby przypisać Simona Britta HireVue, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="dccc0-210">**To assign Britta Simon to HireVue, perform the following steps:**</span></span>

1. <span data-ttu-id="dccc0-211">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="dccc0-211">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="dccc0-213">Na liście aplikacji zaznacz **HireVue**.</span><span class="sxs-lookup"><span data-stu-id="dccc0-213">In the applications list, select **HireVue**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_app.png) 

3. <span data-ttu-id="dccc0-215">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="dccc0-215">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="dccc0-217">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="dccc0-217">Click **Add** button.</span></span> <span data-ttu-id="dccc0-218">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="dccc0-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="dccc0-220">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="dccc0-220">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="dccc0-221">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="dccc0-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dccc0-222">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="dccc0-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dccc0-223">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="dccc0-223">Testing single sign-on</span></span>

<span data-ttu-id="dccc0-224">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="dccc0-224">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="dccc0-225">Po kliknięciu kafelka HireVue w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji HireVue.</span><span class="sxs-lookup"><span data-stu-id="dccc0-225">When you click the HireVue tile in the Access Panel, you should get automatically signed-on to your HireVue application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dccc0-226">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="dccc0-226">Additional resources</span></span>

* [<span data-ttu-id="dccc0-227">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dccc0-227">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dccc0-228">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="dccc0-228">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_203.png

