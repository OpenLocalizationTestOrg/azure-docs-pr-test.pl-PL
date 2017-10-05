---
title: 'Samouczek: Integracji Azure Active Directory z bezpiecznego DOSTARCZANIA | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i bezpiecznego DOSTARCZANIA."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fccd5668-fe6f-4e6d-a9ce-ba4f321c33d1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: f6e5b1e34893f6b8fe14e238e24086bb47d009a5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-secure-deliver"></a><span data-ttu-id="f7134-103">Samouczek: Integracji Azure Active Directory z bezpiecznego DOSTARCZANIA</span><span class="sxs-lookup"><span data-stu-id="f7134-103">Tutorial: Azure Active Directory integration with SECURE DELIVER</span></span>

<span data-ttu-id="f7134-104">Z tego samouczka dowiesz się integrowanie SECURE DOSTARCZANIA w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f7134-104">In this tutorial, you learn how to integrate SECURE DELIVER with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f7134-105">Integrowanie SECURE DOSTARCZANIA z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="f7134-105">Integrating SECURE DELIVER with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f7134-106">Można kontrolować w usłudze Azure AD, który ma dostęp do bezpiecznego DOSTARCZANIA</span><span class="sxs-lookup"><span data-stu-id="f7134-106">You can control in Azure AD who has access to SECURE DELIVER</span></span>
- <span data-ttu-id="f7134-107">Umożliwia użytkownikom automatycznie pobrać zalogowane SECURE dostarczać (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f7134-107">You can enable your users to automatically get signed-on to SECURE DELIVER (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f7134-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="f7134-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f7134-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f7134-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f7134-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f7134-110">Prerequisites</span></span>

<span data-ttu-id="f7134-111">Aby skonfigurować integrację usługi Azure AD z bezpiecznego DOSTARCZANIA, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="f7134-111">To configure Azure AD integration with SECURE DELIVER, you need the following items:</span></span>

- <span data-ttu-id="f7134-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f7134-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f7134-113">SECURE DOSTARCZANIA logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="f7134-113">A SECURE DELIVER single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f7134-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="f7134-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f7134-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="f7134-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f7134-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="f7134-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f7134-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f7134-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f7134-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="f7134-118">Scenario description</span></span>
<span data-ttu-id="f7134-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="f7134-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f7134-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="f7134-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f7134-121">Dodawanie SECURE DOSTARCZANIA z galerii</span><span class="sxs-lookup"><span data-stu-id="f7134-121">Adding SECURE DELIVER from the gallery</span></span>
2. <span data-ttu-id="f7134-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="f7134-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-secure-deliver-from-the-gallery"></a><span data-ttu-id="f7134-123">Dodawanie SECURE DOSTARCZANIA z galerii</span><span class="sxs-lookup"><span data-stu-id="f7134-123">Adding SECURE DELIVER from the gallery</span></span>
<span data-ttu-id="f7134-124">Aby skonfigurować integrację z bezpiecznego DOSTARCZANIA w usłudze Azure Active Directory, należy dodać SECURE DOSTARCZANIA z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="f7134-124">To configure the integration of SECURE DELIVER into Azure AD, you need to add SECURE DELIVER from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f7134-125">**Aby dodać SECURE DOSTARCZANIA z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f7134-125">**To add SECURE DELIVER from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f7134-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="f7134-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="f7134-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="f7134-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f7134-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="f7134-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="f7134-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f7134-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="f7134-133">W polu wyszukiwania wpisz **SECURE DOSTARCZANIA**.</span><span class="sxs-lookup"><span data-stu-id="f7134-133">In the search box, type **SECURE DELIVER**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-securedeliver-tutorial/tutorial_securedeliver_search.png)

5. <span data-ttu-id="f7134-135">W panelu wyników wybierz **SECURE DOSTARCZANIA**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="f7134-135">In the results panel, select **SECURE DELIVER**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-securedeliver-tutorial/tutorial_securedeliver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f7134-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="f7134-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f7134-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z bezpiecznego DOSTARCZANIA, w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="f7134-138">In this section, you configure and test Azure AD single sign-on with SECURE DELIVER based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f7134-139">Do rejestracji jednokrotnej do pracy usługi Azure AD musi ustalić użytkownika odpowiednika w bezpieczny DOSTARCZANIA do użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f7134-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SECURE DELIVER is to a user in Azure AD.</span></span> <span data-ttu-id="f7134-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i danemu użytkownikowi w bezpieczny DOSTARCZANIA musi określone.</span><span class="sxs-lookup"><span data-stu-id="f7134-140">In other words, a link relationship between an Azure AD user and the related user in SECURE DELIVER needs to be established.</span></span>

<span data-ttu-id="f7134-141">W bezpieczny DOSTARCZANIA, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="f7134-141">In SECURE DELIVER, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f7134-142">Do konfigurowania i testowania usługi Azure AD rejestracji jednokrotnej z bezpiecznego DOSTARCZANIA, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="f7134-142">To configure and test Azure AD single sign-on with SECURE DELIVER, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f7134-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="f7134-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f7134-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="f7134-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f7134-145">**[Tworzenie użytkownika testowego SECURE DOSTARCZANIA](#creating-a-secure-deliver-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta SECURE DOSTARCZANIA połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f7134-145">**[Creating a SECURE DELIVER test user](#creating-a-secure-deliver-test-user)** - to have a counterpart of Britta Simon in SECURE DELIVER that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f7134-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="f7134-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f7134-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="f7134-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f7134-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="f7134-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f7134-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji bezpiecznego DOSTARCZANIA.</span><span class="sxs-lookup"><span data-stu-id="f7134-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SECURE DELIVER application.</span></span>

<span data-ttu-id="f7134-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z bezpiecznego DOSTARCZANIA, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f7134-150">**To configure Azure AD single sign-on with SECURE DELIVER, perform the following steps:**</span></span>

1. <span data-ttu-id="f7134-151">W portalu Azure na **SECURE DOSTARCZANIA** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="f7134-151">In the Azure portal, on the **SECURE DELIVER** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="f7134-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="f7134-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-securedeliver-tutorial/tutorial_securedeliver_samlbase.png)

3. <span data-ttu-id="f7134-155">Na **SECURE DOSTARCZANIA domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f7134-155">On the **SECURE DELIVER Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-securedeliver-tutorial/tutorial_securedeliver_url.png)

    <span data-ttu-id="f7134-157">a.</span><span class="sxs-lookup"><span data-stu-id="f7134-157">a.</span></span> <span data-ttu-id="f7134-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.i-securedeliver.jp/sd/<tenantname>/jsf/login/sso`</span><span class="sxs-lookup"><span data-stu-id="f7134-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.i-securedeliver.jp/sd/<tenantname>/jsf/login/sso`</span></span>

    <span data-ttu-id="f7134-159">b.</span><span class="sxs-lookup"><span data-stu-id="f7134-159">b.</span></span> <span data-ttu-id="f7134-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.i-securedeliver.jp/sd/<tenantname>/postResponse`</span><span class="sxs-lookup"><span data-stu-id="f7134-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.i-securedeliver.jp/sd/<tenantname>/postResponse`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f7134-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="f7134-161">These values are not real.</span></span> <span data-ttu-id="f7134-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="f7134-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f7134-163">Skontaktuj się z [zespołem pomocy technicznej SECURE klienta dostarczenia](mailto:iw-sd-support@fujifilm.com) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="f7134-163">Contact [SECURE DELIVER Client support team](mailto:iw-sd-support@fujifilm.com) to get these values.</span></span> 
 
4. <span data-ttu-id="f7134-164">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="f7134-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-securedeliver-tutorial/tutorial_securedeliver_certificate.png) 

5. <span data-ttu-id="f7134-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f7134-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-securedeliver-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f7134-168">Na **SECURE konfiguracji DOSTARCZANIA** , kliknij przycisk **skonfigurować bezpiecznego DOSTARCZANIA** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="f7134-168">On the **SECURE DELIVER Configuration** section, click **Configure SECURE DELIVER** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f7134-169">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="f7134-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-securedeliver-tutorial/tutorial_securedeliver_configure.png) 

7. <span data-ttu-id="f7134-171">Skonfigurować logowanie jednokrotne w **SECURE DOSTARCZANIA** stronie, musisz wysłać pobrany **certyfikatu (Base64)**, **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** do [SECURE DOSTARCZANIA zespołem pomocy technicznej](mailto:iw-sd-support@fujifilm.com).</span><span class="sxs-lookup"><span data-stu-id="f7134-171">To configure single sign-on on **SECURE DELIVER** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [SECURE DELIVER support team](mailto:iw-sd-support@fujifilm.com).</span></span> <span data-ttu-id="f7134-172">To ustawienie, aby były prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one wartość.</span><span class="sxs-lookup"><span data-stu-id="f7134-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="f7134-173">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="f7134-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f7134-174">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="f7134-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f7134-175">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f7134-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f7134-176">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f7134-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="f7134-177">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="f7134-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="f7134-179">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f7134-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f7134-180">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="f7134-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-securedeliver-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f7134-182">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="f7134-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-securedeliver-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f7134-184">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f7134-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-securedeliver-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f7134-186">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f7134-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-securedeliver-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f7134-188">a.</span><span class="sxs-lookup"><span data-stu-id="f7134-188">a.</span></span> <span data-ttu-id="f7134-189">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f7134-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f7134-190">b.</span><span class="sxs-lookup"><span data-stu-id="f7134-190">b.</span></span> <span data-ttu-id="f7134-191">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f7134-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f7134-192">c.</span><span class="sxs-lookup"><span data-stu-id="f7134-192">c.</span></span> <span data-ttu-id="f7134-193">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="f7134-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f7134-194">d.</span><span class="sxs-lookup"><span data-stu-id="f7134-194">d.</span></span> <span data-ttu-id="f7134-195">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="f7134-195">Click **Create**.</span></span>
 
### <a name="creating-a-secure-deliver-test-user"></a><span data-ttu-id="f7134-196">Tworzenie użytkownika testowego SECURE DOSTARCZANIA</span><span class="sxs-lookup"><span data-stu-id="f7134-196">Creating a SECURE DELIVER test user</span></span>

<span data-ttu-id="f7134-197">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w bezpieczny DOSTARCZANIA.</span><span class="sxs-lookup"><span data-stu-id="f7134-197">The objective of this section is to create a user called Britta Simon in SECURE DELIVER.</span></span> <span data-ttu-id="f7134-198">Praca z [SECURE DOSTARCZANIA zespołem pomocy technicznej](mailto:iw-sd-support@fujifilm.com) Aby dodać użytkowników w ramach konta SECURE DOSTARCZANIA.</span><span class="sxs-lookup"><span data-stu-id="f7134-198">Work with [SECURE DELIVER support team](mailto:iw-sd-support@fujifilm.com) to add the users in the SECURE DELIVER account.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f7134-199">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f7134-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f7134-200">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do bezpiecznego DOSTARCZANIA.</span><span class="sxs-lookup"><span data-stu-id="f7134-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SECURE DELIVER.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="f7134-202">**Aby przypisać Simona Britta do bezpiecznego DOSTARCZANIA, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f7134-202">**To assign Britta Simon to SECURE DELIVER, perform the following steps:**</span></span>

1. <span data-ttu-id="f7134-203">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="f7134-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="f7134-205">Na liście aplikacji zaznacz **SECURE DOSTARCZANIA**.</span><span class="sxs-lookup"><span data-stu-id="f7134-205">In the applications list, select **SECURE DELIVER**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-securedeliver-tutorial/tutorial_securedeliver_app.png) 

3. <span data-ttu-id="f7134-207">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="f7134-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="f7134-209">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f7134-209">Click **Add** button.</span></span> <span data-ttu-id="f7134-210">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f7134-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="f7134-212">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="f7134-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f7134-213">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f7134-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f7134-214">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f7134-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f7134-215">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="f7134-215">Testing single sign-on</span></span>

<span data-ttu-id="f7134-216">Celem tej sekcji służy do testowania konfigurację usługi Azure AD z logowania jednokrotnego za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="f7134-216">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="f7134-217">Po kliknięciu kafelka SECURE DOSTARCZANIA w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do bezpiecznego DOSTARCZANIA aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f7134-217">When you click the SECURE DELIVER tile in the Access Panel, you should get automatically signed-on to your SECURE DELIVER application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f7134-218">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="f7134-218">Additional resources</span></span>

* [<span data-ttu-id="f7134-219">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f7134-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f7134-220">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f7134-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_203.png

