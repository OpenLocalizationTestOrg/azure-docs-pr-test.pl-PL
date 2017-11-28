---
title: "Samouczek: Integracji Azure Active Directory z logowania jednokrotnego SAML JIRA przez firmę Microsoft | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i logowania jednokrotnego SAML JIRA przez firmę Microsoft."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0dc847b9-eec4-4c31-845e-0144ddedc4a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: b5f7813c8244d2964b6894ae49cd64e0ee71b704
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jira-saml-sso-by-microsoft"></a><span data-ttu-id="1e7a9-103">Samouczek: Integracji Azure Active Directory z logowania jednokrotnego SAML JIRA przez firmę Microsoft</span><span class="sxs-lookup"><span data-stu-id="1e7a9-103">Tutorial: Azure Active Directory integration with JIRA SAML SSO by Microsoft</span></span>

<span data-ttu-id="1e7a9-104">Z tego samouczka dowiesz się sposobu integracji z usługą Azure Active Directory (Azure AD) logowania jednokrotnego SAML JIRA przez firmę Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-104">In this tutorial, you learn how to integrate JIRA SAML SSO by Microsoft with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1e7a9-105">Integracja z usługą Azure AD logowania jednokrotnego SAML JIRA przez firmę Microsoft zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="1e7a9-105">Integrating JIRA SAML SSO by Microsoft with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1e7a9-106">Można kontrolować w usłudze Azure AD, który ma dostęp do logowania jednokrotnego SAML JIRA przez firmę Microsoft</span><span class="sxs-lookup"><span data-stu-id="1e7a9-106">You can control in Azure AD who has access to JIRA SAML SSO by Microsoft</span></span>
- <span data-ttu-id="1e7a9-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do logowania jednokrotnego SAML JIRA przez firmę Microsoft (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e7a9-107">You can enable your users to automatically get signed-on to JIRA SAML SSO by Microsoft (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1e7a9-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="1e7a9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1e7a9-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1e7a9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1e7a9-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1e7a9-110">Prerequisites</span></span>

<span data-ttu-id="1e7a9-111">Aby skonfigurować integrację usługi Azure AD z logowania jednokrotnego SAML JIRA przez firmę Microsoft, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="1e7a9-111">To configure Azure AD integration with JIRA SAML SSO by Microsoft, you need the following items:</span></span>

- <span data-ttu-id="1e7a9-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e7a9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1e7a9-113">Aplikacja serwera JIRA zainstalowany na serwerze Windows 64-bitowych (lokalnie lub w chmurze infrastruktury IaaS)</span><span class="sxs-lookup"><span data-stu-id="1e7a9-113">JIRA server application installed on a Windows 64-bit server (on premise or on the cloud IaaS infrastructure)</span></span>
- <span data-ttu-id="1e7a9-114">Serwer JIRA jest obsługujące protokół HTTPS</span><span class="sxs-lookup"><span data-stu-id="1e7a9-114">JIRA server is HTTPS enabled</span></span>
- <span data-ttu-id="1e7a9-115">Należy pamiętać, że obsługiwane wersje dla wtyczki JIRA są wymienione w poniższej sekcji.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-115">Note the supported versions for JIRA Plugin are mentioned in below section.</span></span>
- <span data-ttu-id="1e7a9-116">JIRA serwer jest dostępny w Internecie, szczególnie do strony logowania usługi AD platformy Azure do uwierzytelniania i powinien otrzymywać token z usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e7a9-116">JIRA server is reachable on internet particularly to Azure AD Login page for authentication and should able to receive the token from Azure AD</span></span>
- <span data-ttu-id="1e7a9-117">Poświadczenia administratora są konfigurowane w JIRA</span><span class="sxs-lookup"><span data-stu-id="1e7a9-117">Admin credentials are set up in JIRA</span></span>
- <span data-ttu-id="1e7a9-118">WebSudo jest wyłączona w JIRA</span><span class="sxs-lookup"><span data-stu-id="1e7a9-118">WebSudo is disabled in JIRA</span></span>
- <span data-ttu-id="1e7a9-119">Użytkownika testowego utworzone w JIRA aplikacji serwera</span><span class="sxs-lookup"><span data-stu-id="1e7a9-119">Test user created in the JIRA server application</span></span>

> [!NOTE]
> <span data-ttu-id="1e7a9-120">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego programu JIRA.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-120">To test the steps in this tutorial, we do not recommend using a production environment of JIRA.</span></span> <span data-ttu-id="1e7a9-121">Przetestowanie integracji w rozwoju lub środowisko przejściowe aplikacji, a następnie użyj środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-121">Test the integration first in development or staging environment of the application and then use the production environment.</span></span>

<span data-ttu-id="1e7a9-122">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="1e7a9-122">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1e7a9-123">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-123">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1e7a9-124">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna tutaj: [oferta wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1e7a9-124">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="supported-versions-of-jira"></a><span data-ttu-id="1e7a9-125">Obsługiwane wersje JIRA</span><span class="sxs-lookup"><span data-stu-id="1e7a9-125">Supported versions of JIRA</span></span> 

<span data-ttu-id="1e7a9-126">Od tej chwili obsługiwane są następujące wersje JIRA:</span><span class="sxs-lookup"><span data-stu-id="1e7a9-126">As of now, following versions of JIRA are supported:</span></span>

- <span data-ttu-id="1e7a9-127">Podstawowe JIRA i oprogramowania: 6.0 do 7.2.0</span><span class="sxs-lookup"><span data-stu-id="1e7a9-127">JIRA Core and Software: 6.0 to 7.2.0</span></span>
- <span data-ttu-id="1e7a9-128">JIRA działu: 3.2 do 3.0</span><span class="sxs-lookup"><span data-stu-id="1e7a9-128">JIRA Service Desk: 3.0 to 3.2</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1e7a9-129">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="1e7a9-129">Scenario description</span></span>
<span data-ttu-id="1e7a9-130">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-130">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1e7a9-131">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="1e7a9-131">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1e7a9-132">Dodawanie logowania jednokrotnego SAML JIRA przez firmę Microsoft z galerii</span><span class="sxs-lookup"><span data-stu-id="1e7a9-132">Adding JIRA SAML SSO by Microsoft from the gallery</span></span>
2. <span data-ttu-id="1e7a9-133">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="1e7a9-133">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jira-saml-sso-by-microsoft-from-the-gallery"></a><span data-ttu-id="1e7a9-134">Dodawanie logowania jednokrotnego SAML JIRA przez firmę Microsoft z galerii</span><span class="sxs-lookup"><span data-stu-id="1e7a9-134">Adding JIRA SAML SSO by Microsoft from the gallery</span></span>
<span data-ttu-id="1e7a9-135">Aby skonfigurować integrację logowania jednokrotnego SAML JIRA przez firmę Microsoft do usługi Azure AD, należy dodać logowania jednokrotnego SAML JIRA przez firmę Microsoft z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-135">To configure the integration of JIRA SAML SSO by Microsoft into Azure AD, you need to add JIRA SAML SSO by Microsoft from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1e7a9-136">**Aby dodać logowania jednokrotnego SAML JIRA przez firmę Microsoft z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="1e7a9-136">**To add JIRA SAML SSO by Microsoft from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1e7a9-137">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-137">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="1e7a9-139">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-139">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1e7a9-140">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-140">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="1e7a9-142">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-142">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="1e7a9-144">W polu wyszukiwania wpisz **logowania jednokrotnego SAML JIRA przez firmę Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-144">In the search box, type **JIRA SAML SSO by Microsoft**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_search.png)

5. <span data-ttu-id="1e7a9-146">W panelu wyników wybierz **logowania jednokrotnego SAML JIRA przez firmę Microsoft**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-146">In the results panel, select **JIRA SAML SSO by Microsoft**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1e7a9-148">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="1e7a9-148">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1e7a9-149">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego SAML JIRA przez firmę Microsoft na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="1e7a9-149">In this section, you configure and test Azure AD single sign-on with JIRA SAML SSO by Microsoft based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1e7a9-150">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w logowania jednokrotnego SAML JIRA przez firmę Microsoft jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-150">For single sign-on to work, Azure AD needs to know what the counterpart user in JIRA SAML SSO by Microsoft is to a user in Azure AD.</span></span> <span data-ttu-id="1e7a9-151">Innymi słowy musi można ustanowić łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w logowania jednokrotnego SAML JIRA przez firmę Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-151">In other words, a link relationship between an Azure AD user and the related user in JIRA SAML SSO by Microsoft needs to be established.</span></span>

<span data-ttu-id="1e7a9-152">W JIRA logowania jednokrotnego SAML przez firmę Microsoft, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-152">In JIRA SAML SSO by Microsoft, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1e7a9-153">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego SAML JIRA przez firmę Microsoft, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="1e7a9-153">To configure and test Azure AD single sign-on with JIRA SAML SSO by Microsoft, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1e7a9-154">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-154">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1e7a9-155">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-155">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1e7a9-156">**[Tworzenie logowania jednokrotnego SAML JIRA przez użytkownika testowego Microsoft](#creating-a-jira-saml-sso-by-microsoft-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta logowania jednokrotnego SAML JIRA przez firmy Microsoft, który jest połączony z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-156">**[Creating a JIRA SAML SSO by Microsoft test user](#creating-a-jira-saml-sso-by-microsoft-test-user)** - to have a counterpart of Britta Simon in JIRA SAML SSO by Microsoft that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1e7a9-157">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-157">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1e7a9-158">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-158">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1e7a9-159">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="1e7a9-159">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1e7a9-160">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i konfigurowanie rejestracji jednokrotnej w sieci logowania jednokrotnego SAML JIRA przez aplikację Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-160">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your JIRA SAML SSO by Microsoft application.</span></span>

<span data-ttu-id="1e7a9-161">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego SAML JIRA przez firmę Microsoft, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="1e7a9-161">**To configure Azure AD single sign-on with JIRA SAML SSO by Microsoft, perform the following steps:**</span></span>

1. <span data-ttu-id="1e7a9-162">W portalu Azure na **logowania jednokrotnego SAML JIRA przez firmę Microsoft** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-162">In the Azure portal, on the **JIRA SAML SSO by Microsoft** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="1e7a9-164">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-164">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_samlbase.png)

3. <span data-ttu-id="1e7a9-166">Na **logowania jednokrotnego SAML JIRA Domain firmy Microsoft i adresy URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="1e7a9-166">On the **JIRA SAML SSO by Microsoft Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_url.png)

    <span data-ttu-id="1e7a9-168">a.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-168">a.</span></span> <span data-ttu-id="1e7a9-169">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="1e7a9-169">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    <span data-ttu-id="1e7a9-170">b.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-170">b.</span></span> <span data-ttu-id="1e7a9-171">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<domain:port>/`</span><span class="sxs-lookup"><span data-stu-id="1e7a9-171">In the **Identifier** textbox, type a URL using the following pattern: `https://<domain:port>/`</span></span>

    <span data-ttu-id="1e7a9-172">c.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-172">c.</span></span> <span data-ttu-id="1e7a9-173">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="1e7a9-173">In the **Reply URL** textbox, type a URL using the following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1e7a9-174">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-174">These values are not real.</span></span> <span data-ttu-id="1e7a9-175">Rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-175">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="1e7a9-176">Port jest opcjonalny w przypadku, gdy jest nazwane adres URL.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-176">Port is optional in case it’s a named URL.</span></span> <span data-ttu-id="1e7a9-177">Te wartości są odbierane podczas konfigurowania Jira dodatek, który znajduje się w dalszej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-177">These values are received during the configuration of Jira plugin, which is explained later in the tutorial.</span></span>
 
4. <span data-ttu-id="1e7a9-178">Aby wygenerować **metadanych** adres url, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="1e7a9-178">To generate the **Metadata** url, perform the following steps:</span></span>

    <span data-ttu-id="1e7a9-179">a.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-179">a.</span></span> <span data-ttu-id="1e7a9-180">Kliknij przycisk **rejestracji aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-180">Click **App registrations**.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jiramicrosoft-tutorial/appregistrations.png)
   
    <span data-ttu-id="1e7a9-182">b.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-182">b.</span></span> <span data-ttu-id="1e7a9-183">Kliknij przycisk **punkty końcowe** otworzyć **punkty końcowe** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-183">Click **Endpoints** to open **Endpoints** dialog box.</span></span>  
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jiramicrosoft-tutorial/endpointicon.png)

    <span data-ttu-id="1e7a9-185">c.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-185">c.</span></span> <span data-ttu-id="1e7a9-186">Kliknij przycisk Kopiuj, aby skopiować **dokument METADANYCH usług FEDERACYJNYCH** adresu url i wklej go do Notatnika.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-186">Click the copy button to copy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jiramicrosoft-tutorial/endpoint.png)
     
    <span data-ttu-id="1e7a9-188">d.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-188">d.</span></span> <span data-ttu-id="1e7a9-189">Teraz przejdź do strony właściwości **logowania jednokrotnego SAML JIRA przez firmę Microsoft** i skopiuj **identyfikator aplikacji** przy użyciu **kopiowania** przycisk i wklej go do Notatnika.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-189">Now go to the property page of **JIRA SAML SSO by Microsoft** and copy the **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jiramicrosoft-tutorial/appid.png)

    <span data-ttu-id="1e7a9-191">e.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-191">e.</span></span> <span data-ttu-id="1e7a9-192">Generowanie **adres URL metadanych** przy użyciu następującego wzorca: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` i skopiuj tę wartość w programie Notatnik, ponieważ jest później używany dla konfiguracji wtyczki.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-192">Generate the **Metadata URL** using the following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` and copy this value in notepad as it is used later for the configuration of the plugin.</span></span>

5. <span data-ttu-id="1e7a9-193">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-193">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1e7a9-195">Skontaktuj się z [Microsoft](mailto:waadpartners@microsoft.com) z następującymi informacjami dla wtyczki JIRA.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-195">Contact [Microsoft](mailto:waadpartners@microsoft.com) with the following information for the JIRA plugin.</span></span>
    
    *   <span data-ttu-id="1e7a9-196">Nazwa klienta:</span><span class="sxs-lookup"><span data-stu-id="1e7a9-196">Customer Name:</span></span>
    *   <span data-ttu-id="1e7a9-197">Nazwa domeny głównej:</span><span class="sxs-lookup"><span data-stu-id="1e7a9-197">Primary domain name:</span></span>
    *   <span data-ttu-id="1e7a9-198">Azure AD Premium: Tak/nie (wtyczka będzie dostępna dla wszystkich klientów wolne, Basic i warstwy Premium)</span><span class="sxs-lookup"><span data-stu-id="1e7a9-198">Azure AD Premium: Yes/No (Plugin will be available to all     the customer Free, Basic, and Premium SKU)</span></span>
    *   <span data-ttu-id="1e7a9-199">Liczba użytkowników, którzy będą używać tej integracji:</span><span class="sxs-lookup"><span data-stu-id="1e7a9-199">Number of users who will be using this integration:</span></span>
    *   <span data-ttu-id="1e7a9-200">Wersja JIRA:</span><span class="sxs-lookup"><span data-stu-id="1e7a9-200">JIRA Version:</span></span>
    *   <span data-ttu-id="1e7a9-201">Uwagi:</span><span class="sxs-lookup"><span data-stu-id="1e7a9-201">Comments:</span></span>

7. <span data-ttu-id="1e7a9-202">W oknie przeglądarki innej witryny sieci web należy zalogować się jako administrator do Twojego wystąpienia JIRA.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-202">In a different web browser window, log in to your JIRA instance as an administrator.</span></span>

8. <span data-ttu-id="1e7a9-203">Umieść kursor na koło zębate, a następnie kliknij przycisk **dodatki**.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-203">Hover on cog and click the **Add-ons**.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jiramicrosoft-tutorial/addon1.png)

9. <span data-ttu-id="1e7a9-205">W sekcji Karta dodatki, kliknij przycisk **Zarządzanie dodatkami**.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-205">Under Add-ons tab section, click **Manage add-ons**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jiramicrosoft-tutorial/addon7.png)

10. <span data-ttu-id="1e7a9-207">Ręcznie przekazać wtyczki obsługiwane przez firmę Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-207">Manually upload the plugin provided by Microsoft.</span></span> <span data-ttu-id="1e7a9-208">Po zainstalowaniu dodatku plug-in pojawia się w **użytkownik zainstalował** sekcji dodatki **zarządzania dodatkami** sekcji.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-208">Once the plugin is installed, it appears in **User Installed** add-ons section of **Manage Add-on** section.</span></span>

11. <span data-ttu-id="1e7a9-209">Kliknij przycisk **Konfiguruj** do skonfigurowania nowej wtyczki.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-209">Click **Configure** to configure the new plugin.</span></span>

12. <span data-ttu-id="1e7a9-210">Wykonaj następujące kroki na stronie konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="1e7a9-210">Perform following steps on configuration page:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jiramicrosoft-tutorial/addon5.png)
 
    <span data-ttu-id="1e7a9-212">a.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-212">a.</span></span> <span data-ttu-id="1e7a9-213">W **adres URL metadanych** Wklej **adres URL metadanych** z usługi Azure AD i kliknij przycisk **rozwiązać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-213">In **Metadata URL** paste the **Metadata URL** generated from Azure AD and click the **Resolve** button.</span></span> <span data-ttu-id="1e7a9-214">Adres URL metadanych IdP odczytuje i wypełnienie wszystkich pól informacji.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-214">It reads the IdP metadata URL and populates all the fields information.</span></span>

    > [!Note]
    > <span data-ttu-id="1e7a9-215">Domyślna lokalizacja SAML użytkownika identyfikator to identyfikator nazwy.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-215">Default SAML User ID location is Name Identifier.</span></span> <span data-ttu-id="1e7a9-216">Można to zmienić opcję atrybutu i wprowadź odpowiednią nazwę.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-216">You can change this to an attribute option and enter the appropriate attribute name.</span></span>

    > [!TIP]
    > <span data-ttu-id="1e7a9-217">Upewnij się, że istnieje tylko jeden certyfikat mapowany aplikacji tak, aby nie było błędu rozpoznawania metadanych.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-217">Ensure that there is only one certificate mapped against the app so that there is no error in resolving the metadata.</span></span> <span data-ttu-id="1e7a9-218">Jeśli dostępnych jest wiele certyfikatów na rozpoznawanie metadanych, administrator pobiera wystąpił błąd.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-218">If there are multiple certificates, upon resolving the metadata, admin gets an error.</span></span>
    
    <span data-ttu-id="1e7a9-219">b.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-219">b.</span></span> <span data-ttu-id="1e7a9-220">Kopiuj **identyfikator, adres URL odpowiedzi i zaloguj się na adres URL** wartości i wklej je w **identyfikator, adres URL odpowiedzi i zaloguj się na adres URL** odpowiednio do pól tekstowych **logowania jednokrotnego SAML JIRA Domain firmy Microsoft i adresy URL** sekcji z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-220">Copy the **Identifier, Reply URL and Sign on URL** values and paste them in **Identifier, Reply URL and Sign on URL** textboxes respectively in **JIRA SAML SSO by Microsoft Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="1e7a9-221">c.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-221">c.</span></span> <span data-ttu-id="1e7a9-222">W **nazwa przycisku logowania** wpisz nazwę przycisku przez organizację nowych użytkowników na ekranie logowania.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-222">In **Login Button Name** type the name of button your organization wants the users to see on login screen.</span></span>

    <span data-ttu-id="1e7a9-223">d.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-223">d.</span></span> <span data-ttu-id="1e7a9-224">W **lokalizacje identyfikator użytkownika SAML** wybierz opcję **identyfikator użytkownika jest w elemencie NameIdentifier instrukcji podmiotu** lub **identyfikator użytkownika jest w elemencie atrybutu**.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-224">In **SAML User ID Locations** select either **User ID is in the NameIdentifier element of the Subject statement** or **User ID is in an Attribute element**.</span></span>  <span data-ttu-id="1e7a9-225">Ten identyfikator ma być JIRA identyfikator użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-225">This ID has to be the JIRA user id.</span></span> <span data-ttu-id="1e7a9-226">Jeśli identyfikator użytkownika nie jest zgodny, następnie system uniemożliwi użytkownikom logować się.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-226">If the user id is not matched, then system will not allow users to log in.</span></span> 
    
    <span data-ttu-id="1e7a9-227">e.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-227">e.</span></span> <span data-ttu-id="1e7a9-228">W przypadku wybrania **identyfikator użytkownika jest w elemencie atrybutu** opcji, a następnie w **nazwa atrybutu** pole tekstowe wpisz nazwę atrybutu, gdy oczekiwano identyfikatora użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-228">If you select **User ID is in an Attribute element** option, then in **Attribute name** textbox type the name of the attribute where User Id is expected.</span></span> 

    <span data-ttu-id="1e7a9-229">f.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-229">f.</span></span> <span data-ttu-id="1e7a9-230">Jeśli korzystasz z domeny federacyjnej (na przykład usług AD FS itp.) z usługą Azure AD, należy kliknąć opcję **Włączanie odnajdowania obszaru macierzystego** opcji i skonfigurować **nazwy domeny**.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-230">If you are using the federated domain (like ADFS etc.) with Azure AD, then click on the **Enable Home Realm Discovery** option and configure the **Domain Name**.</span></span>
    
    <span data-ttu-id="1e7a9-231">g.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-231">g.</span></span> <span data-ttu-id="1e7a9-232">W **nazwy domeny** wpisz nazwę domeny, w tym miejscu w przypadku logowania za pomocą usług AD FS.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-232">In **Domain Name** type the domain name here in case of the ADFS-based login.</span></span>

    <span data-ttu-id="1e7a9-233">h.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-233">h.</span></span> <span data-ttu-id="1e7a9-234">Sprawdź **włączyć pojedynczego Wyloguj** chcesz wylogować się z usługi Azure AD, gdy użytkownik zaloguje z JIRA.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-234">Check **Enable Single Sign out** if you wish to log out from Azure AD when a user logs out from JIRA.</span></span> 

    <span data-ttu-id="1e7a9-235">i.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-235">i.</span></span> <span data-ttu-id="1e7a9-236">Kliknij przycisk **zapisać** przycisk, aby zapisać ustawienia.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-236">Click **Save** button to save the settings.</span></span>

> [!TIP]
> <span data-ttu-id="1e7a9-237">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="1e7a9-237">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1e7a9-238">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-238">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1e7a9-239">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1e7a9-239">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1e7a9-240">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e7a9-240">Creating an Azure AD test user</span></span>
<span data-ttu-id="1e7a9-241">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-241">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="1e7a9-243">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="1e7a9-243">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1e7a9-244">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-244">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1e7a9-246">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-246">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1e7a9-248">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-248">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1e7a9-250">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="1e7a9-250">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1e7a9-252">a.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-252">a.</span></span> <span data-ttu-id="1e7a9-253">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-253">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1e7a9-254">b.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-254">b.</span></span> <span data-ttu-id="1e7a9-255">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-255">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1e7a9-256">c.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-256">c.</span></span> <span data-ttu-id="1e7a9-257">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-257">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1e7a9-258">d.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-258">d.</span></span> <span data-ttu-id="1e7a9-259">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-259">Click **Create**.</span></span>
 
### <a name="creating-a-jira-saml-sso-by-microsoft-test-user"></a><span data-ttu-id="1e7a9-260">Tworzenie logowania jednokrotnego SAML JIRA przez użytkownika testowego firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="1e7a9-260">Creating a JIRA SAML SSO by Microsoft test user</span></span>

<span data-ttu-id="1e7a9-261">Aby włączyć użytkowników usługi Azure AD zalogować się do serwera lokalnego JIRA, ich muszą mieć przydzielone do logowania jednokrotnego SAML JIRA przez firmę Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-261">To enable Azure AD users to log in to JIRA on-premise server, they must be provisioned into JIRA SAML SSO by Microsoft.</span></span> <span data-ttu-id="1e7a9-262">W przypadku logowania jednokrotnego SAML JIRA przez firmę Microsoft inicjowania obsługi administracyjnej jest zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-262">For JIRA SAML SSO by Microsoft, provisioning is a manual task.</span></span>

<span data-ttu-id="1e7a9-263">**Aby udostępnić konta użytkownika, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="1e7a9-263">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="1e7a9-264">Zaloguj się do serwera lokalnego JIRA jako administrator.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-264">Log in to your JIRA on-premise server as an administrator.</span></span>

2. <span data-ttu-id="1e7a9-265">Umieść kursor na koło zębate, a następnie kliknij przycisk **Zarządzanie użytkownikami**.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-265">Hover on cog and click the **User management**.</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-jiramicrosoft-tutorial/user1.png) 

3. <span data-ttu-id="1e7a9-267">Nastąpi przekierowanie do strony dostępu administratora, aby wprowadzić **hasło** i kliknij przycisk **Potwierdź** przycisku.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-267">You are redirected to Administrator Access page to enter **Password** and click **Confirm** button.</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-jiramicrosoft-tutorial/user2.png) 

4. <span data-ttu-id="1e7a9-269">W obszarze **Zarządzanie użytkownikami** sekcji, kliknij pozycję **Utwórz użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-269">Under **User management** tab section, click **create user**.</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-jiramicrosoft-tutorial/user3.png) 

5. <span data-ttu-id="1e7a9-271">Na **"Tworzenie nowego użytkownika"** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="1e7a9-271">On the **“Create new user”** dialog page, perform the following steps:</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-jiramicrosoft-tutorial/user4.png) 

    <span data-ttu-id="1e7a9-273">a.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-273">a.</span></span> <span data-ttu-id="1e7a9-274">W **adres E-mail** tekstowym, wpisz adres e-mail użytkownika, takich jak Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-274">In the **Email address** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="1e7a9-275">b.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-275">b.</span></span> <span data-ttu-id="1e7a9-276">W **imię i nazwisko** pole tekstowe, pełna nazwa typu użytkownika, takich jak Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-276">In the **Full Name** textbox, type full name of the user like Britta Simon.</span></span>

    <span data-ttu-id="1e7a9-277">c.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-277">c.</span></span> <span data-ttu-id="1e7a9-278">W **Username** tekstowym, wpisz adres e-mail użytkownika, takich jak Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-278">In the **Username** textbox, type the email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="1e7a9-279">d.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-279">d.</span></span> <span data-ttu-id="1e7a9-280">W **hasło** tekstowym, wpisz hasło użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-280">In the **Password** textbox, type the password of user.</span></span>

    <span data-ttu-id="1e7a9-281">e.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-281">e.</span></span> <span data-ttu-id="1e7a9-282">Kliknij przycisk **tworzenia użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-282">Click **Create user**.</span></span>   

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1e7a9-283">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e7a9-283">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1e7a9-284">W tej sekcji musisz włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do logowania jednokrotnego SAML JIRA przez firmę Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-284">In this section, you enable Britta Simon to use Azure single sign-on by granting access to JIRA SAML SSO by Microsoft.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="1e7a9-286">**Aby przypisać Simona Britta do logowania jednokrotnego SAML JIRA przez firmę Microsoft, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="1e7a9-286">**To assign Britta Simon to JIRA SAML SSO by Microsoft, perform the following steps:**</span></span>

1. <span data-ttu-id="1e7a9-287">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-287">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="1e7a9-289">Na liście aplikacji zaznacz **logowania jednokrotnego SAML JIRA przez firmę Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-289">In the applications list, select **JIRA SAML SSO by Microsoft**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_app.png) 

3. <span data-ttu-id="1e7a9-291">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-291">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="1e7a9-293">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-293">Click **Add** button.</span></span> <span data-ttu-id="1e7a9-294">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-294">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="1e7a9-296">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-296">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1e7a9-297">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-297">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1e7a9-298">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-298">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1e7a9-299">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="1e7a9-299">Testing single sign-on</span></span>

<span data-ttu-id="1e7a9-300">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-300">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1e7a9-301">Po kliknięciu logowania jednokrotnego SAML JIRA przez Kafelek firmy Microsoft w panelu dostępu należy powinien pobrać automatycznie zalogowane do użytkownika logowania jednokrotnego SAML JIRA przez aplikację Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1e7a9-301">When you click the JIRA SAML SSO by Microsoft tile in the Access Panel, you should get automatically signed-on to your JIRA SAML SSO by Microsoft application.</span></span>
<span data-ttu-id="1e7a9-302">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1e7a9-302">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1e7a9-303">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="1e7a9-303">Additional resources</span></span>

* [<span data-ttu-id="1e7a9-304">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1e7a9-304">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1e7a9-305">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1e7a9-305">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_203.png

