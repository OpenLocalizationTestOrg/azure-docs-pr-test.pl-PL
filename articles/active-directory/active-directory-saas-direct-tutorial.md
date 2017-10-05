---
title: "Samouczek: Integracji Azure Active Directory bezpośrednio | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skonfigurować logowanie jednokrotne między usługą Azure Active Directory i bezpośrednie."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7c2cd1f0-d14c-42f0-94a8-9b800008b285
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 84582492592613320bd3ec2bdffe08519852d7c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-direct"></a><span data-ttu-id="c80e2-103">Samouczek: Integracji Azure Active Directory bezpośrednio</span><span class="sxs-lookup"><span data-stu-id="c80e2-103">Tutorial: Azure Active Directory integration with Direct</span></span>

<span data-ttu-id="c80e2-104">Z tego samouczka dowiesz się integrowanie bezpośrednio w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c80e2-104">In this tutorial, you learn how to integrate Direct with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c80e2-105">Integrowanie bezpośrednio z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="c80e2-105">Integrating Direct with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c80e2-106">Można kontrolować w usłudze Azure AD, który ma dostęp do bezpośredniego</span><span class="sxs-lookup"><span data-stu-id="c80e2-106">You can control in Azure AD who has access to Direct</span></span>
- <span data-ttu-id="c80e2-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do kierowania (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c80e2-107">You can enable your users to automatically get signed-on to Direct (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c80e2-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c80e2-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c80e2-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c80e2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c80e2-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c80e2-110">Prerequisites</span></span>

<span data-ttu-id="c80e2-111">Aby skonfigurować integrację usługi Azure AD bezpośrednio, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="c80e2-111">To configure Azure AD integration with Direct, you need the following items:</span></span>

- <span data-ttu-id="c80e2-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c80e2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c80e2-113">Bezpośrednie logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="c80e2-113">A Direct single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c80e2-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="c80e2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c80e2-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="c80e2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c80e2-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="c80e2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c80e2-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c80e2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c80e2-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="c80e2-118">Scenario description</span></span>
<span data-ttu-id="c80e2-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="c80e2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c80e2-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="c80e2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c80e2-121">Dodawanie bezpośrednio z galerii</span><span class="sxs-lookup"><span data-stu-id="c80e2-121">Adding Direct from the gallery</span></span>
2. <span data-ttu-id="c80e2-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="c80e2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-direct-from-the-gallery"></a><span data-ttu-id="c80e2-123">Dodawanie bezpośrednio z galerii</span><span class="sxs-lookup"><span data-stu-id="c80e2-123">Adding Direct from the gallery</span></span>
<span data-ttu-id="c80e2-124">Aby skonfigurować integrację bezpośrednio do usługi Azure AD, należy dodać bezpośrednio z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="c80e2-124">To configure the integration of Direct into Azure AD, you need to add Direct from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c80e2-125">**Aby dodać bezpośrednio z poziomu galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c80e2-125">**To add Direct from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c80e2-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="c80e2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="c80e2-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="c80e2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c80e2-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="c80e2-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="c80e2-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c80e2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="c80e2-133">W polu wyszukiwania wpisz **bezpośredniego**.</span><span class="sxs-lookup"><span data-stu-id="c80e2-133">In the search box, type **Direct**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-direct-tutorial/tutorial_direct_search.png)

5. <span data-ttu-id="c80e2-135">W panelu wyników wybierz **bezpośredniego**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="c80e2-135">In the results panel, select **Direct**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-direct-tutorial/tutorial_direct_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c80e2-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="c80e2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c80e2-138">W tej sekcji Konfigurowanie i testowanie usługi Azure AD rejestracji jednokrotnej z bezpośrednio na podstawie testu użytkownika o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="c80e2-138">In this section, you configure and test Azure AD single sign-on with Direct based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c80e2-139">Do rejestracji jednokrotnej do pracy usługi Azure AD musi ustalić użytkownika odpowiednika w bezpośrednio do użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c80e2-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Direct is to a user in Azure AD.</span></span> <span data-ttu-id="c80e2-140">Innymi słowy musi można ustanowić łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w bezpośredniej.</span><span class="sxs-lookup"><span data-stu-id="c80e2-140">In other words, a link relationship between an Azure AD user and the related user in Direct needs to be established.</span></span>

<span data-ttu-id="c80e2-141">Bezpośrednie, przypisywanie wartości **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="c80e2-141">In Direct, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c80e2-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej bezpośrednio, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="c80e2-142">To configure and test Azure AD single sign-on with Direct, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c80e2-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="c80e2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c80e2-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="c80e2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c80e2-145">**[Tworzenie użytkownika testowego bezpośredniego](#creating-a-direct-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta bezpośrednio połączony do usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c80e2-145">**[Creating a Direct test user](#creating-a-direct-test-user)** - to have a counterpart of Britta Simon in Direct that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c80e2-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="c80e2-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c80e2-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="c80e2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c80e2-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="c80e2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c80e2-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="c80e2-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Direct application.</span></span>

<span data-ttu-id="c80e2-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej bezpośrednio, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c80e2-150">**To configure Azure AD single sign-on with Direct, perform the following steps:**</span></span>

1. <span data-ttu-id="c80e2-151">W portalu Azure na **bezpośredniego** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="c80e2-151">In the Azure portal, on the **Direct** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="c80e2-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="c80e2-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-direct-tutorial/tutorial_direct_samlbase.png)

3. <span data-ttu-id="c80e2-155">Na **adresy URL i bezpośredniego domeny** sekcji, jeśli chcesz skonfigurować aplikację w **IDP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="c80e2-155">On the **Direct Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-direct-tutorial/tutorial_direct_url.png)

    <span data-ttu-id="c80e2-157">W **identyfikator** tekstowym, wpisz adres URL:`https://direct4b.com/`</span><span class="sxs-lookup"><span data-stu-id="c80e2-157">In the **Identifier** textbox, type the URL: `https://direct4b.com/`</span></span>

4. <span data-ttu-id="c80e2-158">Sprawdź **Pokaż zaawansowane ustawienia adresu URL**, jeśli chcesz skonfigurować aplikację w **SP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="c80e2-158">Check **Show advanced URL settings**, If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-direct-tutorial/tutorial_direct_url1.png)

     <span data-ttu-id="c80e2-160">W **adres URL logowania** tekstowym, wpisz adres URL:`https://direct4b.com/sso`</span><span class="sxs-lookup"><span data-stu-id="c80e2-160">In the **Sign-on URL** textbox, type the URL: `https://direct4b.com/sso`</span></span> 
    
5. <span data-ttu-id="c80e2-161">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="c80e2-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-direct-tutorial/tutorial_direct_certificate.png) 

6. <span data-ttu-id="c80e2-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c80e2-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-direct-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="c80e2-165">Do konfigurowania rejestracji jednokrotnej na **bezpośredniego** stronie, musisz wysłać pobrany **XML metadanych** do [bezpośrednio z pomocą techniczną](https://direct4b.com/ja/support.html#inquiry).</span><span class="sxs-lookup"><span data-stu-id="c80e2-165">To configure single sign-on on **Direct** side, you need to send the downloaded **Metadata XML** to [Direct support team](https://direct4b.com/ja/support.html#inquiry).</span></span> 

> [!TIP]
> <span data-ttu-id="c80e2-166">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="c80e2-166">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c80e2-167">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="c80e2-167">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c80e2-168">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c80e2-168">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c80e2-169">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c80e2-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="c80e2-170">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="c80e2-170">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="c80e2-172">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c80e2-172">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c80e2-173">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="c80e2-173">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-direct-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c80e2-175">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="c80e2-175">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-direct-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c80e2-177">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c80e2-177">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-direct-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c80e2-179">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c80e2-179">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-direct-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c80e2-181">a.</span><span class="sxs-lookup"><span data-stu-id="c80e2-181">a.</span></span> <span data-ttu-id="c80e2-182">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c80e2-182">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c80e2-183">b.</span><span class="sxs-lookup"><span data-stu-id="c80e2-183">b.</span></span> <span data-ttu-id="c80e2-184">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c80e2-184">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c80e2-185">c.</span><span class="sxs-lookup"><span data-stu-id="c80e2-185">c.</span></span> <span data-ttu-id="c80e2-186">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="c80e2-186">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c80e2-187">d.</span><span class="sxs-lookup"><span data-stu-id="c80e2-187">d.</span></span> <span data-ttu-id="c80e2-188">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="c80e2-188">Click **Create**.</span></span>
 
### <a name="creating-a-direct-test-user"></a><span data-ttu-id="c80e2-189">Tworzenie użytkownika Direct — test</span><span class="sxs-lookup"><span data-stu-id="c80e2-189">Creating a Direct test user</span></span>

<span data-ttu-id="c80e2-190">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w bezpośredniej.</span><span class="sxs-lookup"><span data-stu-id="c80e2-190">In this section, you create a user called Britta Simon in Direct.</span></span> <span data-ttu-id="c80e2-191">Praca z [bezpośrednio z pomocą techniczną](https://direct4b.com/ja/support.html#inquiry) Aby dodać użytkowników do bezpośredniego platformy.</span><span class="sxs-lookup"><span data-stu-id="c80e2-191">Work with [Direct support team](https://direct4b.com/ja/support.html#inquiry) to add the users in the Direct platform.</span></span> <span data-ttu-id="c80e2-192">Użytkownicy muszą utworzyć i aktywowana, aby użyć rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="c80e2-192">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c80e2-193">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c80e2-193">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c80e2-194">W tej sekcji musisz włączyć Simona Britta do użycia usługi Azure logowania jednokrotnego za udzielanie dostępu do bezpośredniego.</span><span class="sxs-lookup"><span data-stu-id="c80e2-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Direct.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="c80e2-196">**Aby przypisać Simona Britta Direct, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c80e2-196">**To assign Britta Simon to Direct, perform the following steps:**</span></span>

1. <span data-ttu-id="c80e2-197">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="c80e2-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="c80e2-199">Na liście aplikacji zaznacz **bezpośredniego**.</span><span class="sxs-lookup"><span data-stu-id="c80e2-199">In the applications list, select **Direct**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-direct-tutorial/tutorial_direct_app.png) 

3. <span data-ttu-id="c80e2-201">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="c80e2-201">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="c80e2-203">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c80e2-203">Click **Add** button.</span></span> <span data-ttu-id="c80e2-204">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c80e2-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="c80e2-206">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="c80e2-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c80e2-207">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c80e2-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c80e2-208">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c80e2-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c80e2-209">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="c80e2-209">Testing single sign-on</span></span>

<span data-ttu-id="c80e2-210">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="c80e2-210">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

1. <span data-ttu-id="c80e2-211">Jeśli chcesz przeprowadzić test w **tryb zainicjował IDP**:</span><span class="sxs-lookup"><span data-stu-id="c80e2-211">If you wish to test in **IDP Initiated Mode**:</span></span>

    <span data-ttu-id="c80e2-212">Po kliknięciu **bezpośredniego** kafelka w panelu dostępu, należy pobrać automatycznie zalogowane do Twojej **bezpośredniego** aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c80e2-212">When you click the **Direct** tile in the Access Panel, you should get automatically signed-on to your **Direct** application.</span></span>

2. <span data-ttu-id="c80e2-213">Jeśli chcesz przeprowadzić test w **SP zainicjował tryb**:</span><span class="sxs-lookup"><span data-stu-id="c80e2-213">If you wish to test in **SP Initiated Mode**:</span></span>
    
    <span data-ttu-id="c80e2-214">a.</span><span class="sxs-lookup"><span data-stu-id="c80e2-214">a.</span></span> <span data-ttu-id="c80e2-215">Polecenie **bezpośredniego** kafelka w panelu dostępu i nastąpi przekierowanie do strony logowania w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c80e2-215">Click on the **Direct** tile in the Access Panel and you will be redirected to the application sign-on page.</span></span>

    <span data-ttu-id="c80e2-216">b.</span><span class="sxs-lookup"><span data-stu-id="c80e2-216">b.</span></span> <span data-ttu-id="c80e2-217">Danych wejściowych użytkownika `subdomain` wyświetlane pole tekstowe i naciśnij przycisk "次へ (dalej)", a należy uzyskać automatycznie zalogowane do Twojej **bezpośredniego** aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c80e2-217">Input your `subdomain` in the textbox displayed and press '次へ (Next)' and you should get automatically signed-on to your **Direct** application .</span></span>
    
<span data-ttu-id="c80e2-218">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c80e2-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c80e2-219">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="c80e2-219">Additional resources</span></span>

* [<span data-ttu-id="c80e2-220">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c80e2-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c80e2-221">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c80e2-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-direct-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-direct-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-direct-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-direct-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-direct-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-direct-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-direct-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-direct-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-direct-tutorial/tutorial_general_203.png

