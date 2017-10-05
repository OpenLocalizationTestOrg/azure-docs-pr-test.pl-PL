---
title: 'Samouczek: Integracji Azure Active Directory z logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak skonfigurować logowanie jednokrotne między usługą Azure Active Directory i logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 20e18819-e330-4e40-bd8d-2ff3b98e035f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: cde5983710185d1e46a5601b16bbfb1c0fcae382
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-saml-sso-for-jira-by-resolution-gmbh"></a><span data-ttu-id="3e7c0-103">Samouczek: Integracji Azure Active Directory z logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH</span><span class="sxs-lookup"><span data-stu-id="3e7c0-103">Tutorial: Azure Active Directory integration with SAML SSO for Jira by resolution GmbH</span></span>

<span data-ttu-id="3e7c0-104">Z tego samouczka dowiesz się integrowanie logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3e7c0-104">In this tutorial, you learn how to integrate SAML SSO for Jira by resolution GmbH with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3e7c0-105">Integrowanie logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="3e7c0-105">Integrating SAML SSO for Jira by resolution GmbH with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3e7c0-106">Można kontrolować w usłudze Azure AD, który ma dostęp do logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH</span><span class="sxs-lookup"><span data-stu-id="3e7c0-106">You can control in Azure AD who has access to SAML SSO for Jira by resolution GmbH</span></span>
- <span data-ttu-id="3e7c0-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e7c0-107">You can enable your users to automatically get signed-on to SAML SSO for Jira by resolution GmbH (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3e7c0-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="3e7c0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3e7c0-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3e7c0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3e7c0-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3e7c0-110">Prerequisites</span></span>

<span data-ttu-id="3e7c0-111">Aby skonfigurować integrację usługi Azure AD z logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="3e7c0-111">To configure Azure AD integration with SAML SSO for Jira by resolution GmbH, you need the following items:</span></span>

- <span data-ttu-id="3e7c0-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e7c0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3e7c0-113">Logowania jednokrotnego SAML dla Jira przez rozpoznawanie jednokrotnego GmbH w subskrypcji włączone</span><span class="sxs-lookup"><span data-stu-id="3e7c0-113">A SAML SSO for Jira by resolution GmbH single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3e7c0-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3e7c0-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="3e7c0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3e7c0-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3e7c0-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3e7c0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3e7c0-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="3e7c0-118">Scenario description</span></span>
<span data-ttu-id="3e7c0-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3e7c0-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="3e7c0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3e7c0-121">Dodawanie logowania jednokrotnego SAML dla Jira przy rozdzielczości GmbH z galerii</span><span class="sxs-lookup"><span data-stu-id="3e7c0-121">Adding SAML SSO for Jira by resolution GmbH from the gallery</span></span>
2. <span data-ttu-id="3e7c0-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="3e7c0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-saml-sso-for-jira-by-resolution-gmbh-from-the-gallery"></a><span data-ttu-id="3e7c0-123">Dodawanie logowania jednokrotnego SAML dla Jira przy rozdzielczości GmbH z galerii</span><span class="sxs-lookup"><span data-stu-id="3e7c0-123">Adding SAML SSO for Jira by resolution GmbH from the gallery</span></span>
<span data-ttu-id="3e7c0-124">Aby skonfigurować integrację logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH do usługi Azure AD, należy dodać logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-124">To configure the integration of SAML SSO for Jira by resolution GmbH into Azure AD, you need to add SAML SSO for Jira by resolution GmbH from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3e7c0-125">**Aby dodać logowania jednokrotnego SAML dla Jira za rozdzielczość GmbH z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="3e7c0-125">**To add SAML SSO for Jira by resolution GmbH from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3e7c0-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="3e7c0-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3e7c0-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="3e7c0-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="3e7c0-133">W polu wyszukiwania wpisz **logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH**.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-133">In the search box, type **SAML SSO for Jira by resolution GmbH**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_search.png)

5. <span data-ttu-id="3e7c0-135">W panelu wyników wybierz **logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-135">In the results panel, select **SAML SSO for Jira by resolution GmbH**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3e7c0-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="3e7c0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3e7c0-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego SAML dla Jira przez rozdzielczość GmbH oparte na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="3e7c0-138">In this section, you configure and test Azure AD single sign-on with SAML SSO for Jira by resolution GmbH based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3e7c0-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, jakiego odpowiednikiem użytkownika w logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH jest użytkownikiem w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SAML SSO for Jira by resolution GmbH is to a user in Azure AD.</span></span> <span data-ttu-id="3e7c0-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i danemu użytkownikowi w logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH musi się.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-140">In other words, a link relationship between an Azure AD user and the related user in SAML SSO for Jira by resolution GmbH needs to be established.</span></span>

<span data-ttu-id="3e7c0-141">W logowania jednokrotnego SAML Jira przez rozpoznawania GmbH, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-141">In SAML SSO for Jira by resolution GmbH, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3e7c0-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="3e7c0-142">To configure and test Azure AD single sign-on with SAML SSO for Jira by resolution GmbH, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3e7c0-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3e7c0-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3e7c0-145">**[Tworzenie logowania jednokrotnego SAML dla Jira przez użytkownika testowego GmbH rozpoznawania](#creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-145">**[Creating a SAML SSO for Jira by resolution GmbH test user](#creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user)** - to have a counterpart of Britta Simon in SAML SSO for Jira by resolution GmbH that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3e7c0-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3e7c0-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3e7c0-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="3e7c0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3e7c0-149">W tej sekcji możesz włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w sieci logowania jednokrotnego SAML dla Jira przy rozpoznawania GmbH aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAML SSO for Jira by resolution GmbH application.</span></span>

<span data-ttu-id="3e7c0-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="3e7c0-150">**To configure Azure AD single sign-on with SAML SSO for Jira by resolution GmbH, perform the following steps:**</span></span>

1. <span data-ttu-id="3e7c0-151">W portalu Azure na **logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-151">In the Azure portal, on the **SAML SSO for Jira by resolution GmbH** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="3e7c0-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_samlbase.png)

3. <span data-ttu-id="3e7c0-155">Na **logowania jednokrotnego SAML Jira przez rozpoznawania GmbH domeny i adresów URL** sekcji, jeśli chcesz skonfigurować aplikację w **IDP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="3e7c0-155">On the **SAML SSO for Jira by resolution GmbH Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_url_1.png)

    <span data-ttu-id="3e7c0-157">a.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-157">a.</span></span> <span data-ttu-id="3e7c0-158">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="3e7c0-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

    <span data-ttu-id="3e7c0-159">b.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-159">b.</span></span> <span data-ttu-id="3e7c0-160">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="3e7c0-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

4. <span data-ttu-id="3e7c0-161">Sprawdź **Pokaż zaawansowane ustawienia adresu URL**.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="3e7c0-162">Jeśli chcesz skonfigurować aplikację w **SP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="3e7c0-162">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_url_2.png)

    <span data-ttu-id="3e7c0-164">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="3e7c0-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="3e7c0-165">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-165">These values are not real.</span></span> <span data-ttu-id="3e7c0-166">Rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-166">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="3e7c0-167">Skontaktuj się z [zespołu obsługi logowania jednokrotnego SAML dla Jira przez rozpoznawania klienta GmbH](https://www.resolution.de/go/support) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-167">Contact [SAML SSO for Jira by resolution GmbH Client support team](https://www.resolution.de/go/support) to get these values.</span></span> 

5. <span data-ttu-id="3e7c0-168">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_certificate.png) 

6. <span data-ttu-id="3e7c0-170">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-170">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssojira-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="3e7c0-172">W oknie przeglądarki innej witryny sieci web, zaloguj się do Twojego **logowania jednokrotnego SAML dla Jira przez portal administracyjny GmbH rozpoznawania** jako administrator.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-172">In a different web browser window, log in to your **SAML SSO for Jira by resolution GmbH admin portal** as an administrator.</span></span>

8. <span data-ttu-id="3e7c0-173">Umieść kursor na koło zębate, a następnie kliknij przycisk **dodatki**.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-173">Hover on cog and click the **Add-ons**.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssojira-tutorial/addon1.png)

9. <span data-ttu-id="3e7c0-175">Nastąpi przekierowanie do strony dostępu administratora.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-175">You are redirected to Administrator Access page.</span></span> <span data-ttu-id="3e7c0-176">Wprowadź **hasło** i kliknij przycisk **Potwierdź** przycisku.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-176">Enter the **Password** and click **Confirm** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssojira-tutorial/addon2.png)

10. <span data-ttu-id="3e7c0-178">W sekcji Karta dodatki, kliknij przycisk **znaleźć nowe dodatki**.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-178">Under Add-ons tab section, click **Find new add-ons**.</span></span> <span data-ttu-id="3e7c0-179">Wyszukiwanie **SAML pojedynczy znak na rejestracji jednokrotnej (SSO) dla JIRA** i kliknij przycisk **zainstalować** przycisk, aby zainstalować nowy wtyczki SAML.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-179">Search **SAML Single Sign On (SSO) for JIRA** and click **Install** button to install the new SAML plugin.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssojira-tutorial/addon7.png)

11. <span data-ttu-id="3e7c0-181">Uruchomi instalację dodatku.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-181">The plugin installation will start.</span></span> <span data-ttu-id="3e7c0-182">Kliknij przycisk **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-182">Click **Close**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssojira-tutorial/addon8.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssojira-tutorial/addon9.png)

12. <span data-ttu-id="3e7c0-185">Kliknij pozycję **Zarządzaj**.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-185">Click **Manage**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssojira-tutorial/addon10.png)
    
13. <span data-ttu-id="3e7c0-187">Kliknij przycisk **Konfiguruj** do skonfigurowania nowej wtyczki.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-187">Click **Configure** to configure the new plugin.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssojira-tutorial/addon11.png)

14. <span data-ttu-id="3e7c0-189">Na **konfiguracji wtyczki SingleSignOn SAML** kliknij przycisk **dodać dodatkowe dostawcy tożsamości** przycisk, aby skonfigurować ustawienia dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-189">On **SAML SingleSignOn Plugin Configuration** page, click **Add additional Identity Provider** button to configure the settings of Identity Provider.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssojira-tutorial/addon4.png)

15. <span data-ttu-id="3e7c0-191">Wykonaj następujące kroki na tej stronie:</span><span class="sxs-lookup"><span data-stu-id="3e7c0-191">Perform following steps on this page:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssojira-tutorial/addon5.png)
 
    <span data-ttu-id="3e7c0-193">a.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-193">a.</span></span> <span data-ttu-id="3e7c0-194">Dodaj **nazwa** dostawcy tożsamości (np. usługi Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3e7c0-194">Add **Name** of the Identity Provider (e.g Azure AD).</span></span>
    
    <span data-ttu-id="3e7c0-195">b.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-195">b.</span></span> <span data-ttu-id="3e7c0-196">Dodaj **opis** dostawcy tożsamości (np. usługi Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3e7c0-196">Add **Description** of the Identity Provider (e.g Azure AD).</span></span>

    <span data-ttu-id="3e7c0-197">c.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-197">c.</span></span> <span data-ttu-id="3e7c0-198">Kliknij przycisk **XML** i wybierz **metadanych** pliku, który został pobrany z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-198">Click **XML** and select the **Metadata** file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="3e7c0-199">d.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-199">d.</span></span> <span data-ttu-id="3e7c0-200">Kliknij przycisk **obciążenia** przycisku.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-200">Click **Load** button.</span></span>

    <span data-ttu-id="3e7c0-201">e.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-201">e.</span></span> <span data-ttu-id="3e7c0-202">Odczytuje metadanych IdP i wypełni pola jako wyróżnione na zrzucie ekranu.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-202">It reads the IdP metadata and populates the fields as highlighted in the screenshot.</span></span> 

16. <span data-ttu-id="3e7c0-203">Kliknij przycisk **Zapisz ustawienia** przycisk, aby zapisać ustawienia.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-203">Click **Save settings** button to save the settings.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssojira-tutorial/addon6.png)

> [!TIP]
> <span data-ttu-id="3e7c0-205">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="3e7c0-205">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3e7c0-206">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-206">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3e7c0-207">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3e7c0-207">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3e7c0-208">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e7c0-208">Creating an Azure AD test user</span></span>
<span data-ttu-id="3e7c0-209">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-209">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="3e7c0-211">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="3e7c0-211">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3e7c0-212">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-212">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3e7c0-214">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-214">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3e7c0-216">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-216">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3e7c0-218">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="3e7c0-218">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3e7c0-220">a.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-220">a.</span></span> <span data-ttu-id="3e7c0-221">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-221">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3e7c0-222">b.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-222">b.</span></span> <span data-ttu-id="3e7c0-223">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-223">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3e7c0-224">c.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-224">c.</span></span> <span data-ttu-id="3e7c0-225">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-225">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3e7c0-226">d.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-226">d.</span></span> <span data-ttu-id="3e7c0-227">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-227">Click **Create**.</span></span>
 
### <a name="creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user"></a><span data-ttu-id="3e7c0-228">Tworzenie logowania jednokrotnego SAML dla Jira przez użytkownika testowego GmbH rozwiązania</span><span class="sxs-lookup"><span data-stu-id="3e7c0-228">Creating a SAML SSO for Jira by resolution GmbH test user</span></span>

<span data-ttu-id="3e7c0-229">Aby umożliwić użytkownikom usługi Azure AD zalogowanie się do logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH, ich muszą mieć przydzielone do logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-229">To enable Azure AD users to log in to SAML SSO for Jira by resolution GmbH, they must be provisioned into SAML SSO for Jira by resolution GmbH.</span></span>  
<span data-ttu-id="3e7c0-230">W logowania jednokrotnego SAML Jira przez rozpoznawania GmbH Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-230">In SAML SSO for Jira by resolution GmbH, provisioning is a manual task.</span></span>

<span data-ttu-id="3e7c0-231">**Aby udostępnić konta użytkownika, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="3e7c0-231">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="3e7c0-232">Zaloguj się do użytkownika logowania jednokrotnego SAML dla Jira przez witrynę firmy GmbH rozpoznawania jako administrator.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-232">Log in to your SAML SSO for Jira by resolution GmbH company site as an administrator.</span></span>

2. <span data-ttu-id="3e7c0-233">Umieść kursor na koło zębate, a następnie kliknij przycisk **Zarządzanie użytkownikami**.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-233">Hover on cog and click the **User management**.</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-samlssojira-tutorial/user1.png) 

3. <span data-ttu-id="3e7c0-235">Nastąpi przekierowanie do strony dostępu administratora, aby wprowadzić **hasło** i kliknij przycisk **Potwierdź** przycisku.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-235">You are redirected to Administrator Access page to enter **Password** and click **Confirm** button.</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-samlssojira-tutorial/user2.png) 

4. <span data-ttu-id="3e7c0-237">W obszarze **Zarządzanie użytkownikami** sekcji, kliknij pozycję **Utwórz użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-237">Under **User management** tab section, click **create user**.</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-samlssojira-tutorial/user3.png) 

5. <span data-ttu-id="3e7c0-239">Na **"Tworzenie nowego użytkownika"** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="3e7c0-239">On the **“Create new user”** dialog page, perform the following steps:</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-samlssojira-tutorial/user4.png) 

    <span data-ttu-id="3e7c0-241">a.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-241">a.</span></span> <span data-ttu-id="3e7c0-242">W **adres E-mail** tekstowym, wpisz adres e-mail użytkownika, takich jak Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-242">In the **Email address** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="3e7c0-243">b.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-243">b.</span></span> <span data-ttu-id="3e7c0-244">W **imię i nazwisko** pole tekstowe, pełna nazwa typu użytkownika, takich jak Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-244">In the **Full Name** textbox, type full name of the user like Britta Simon.</span></span>

    <span data-ttu-id="3e7c0-245">c.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-245">c.</span></span> <span data-ttu-id="3e7c0-246">W **Username** tekstowym, wpisz adres e-mail użytkownika, takich jak Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-246">In the **Username** textbox, type the email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="3e7c0-247">d.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-247">d.</span></span> <span data-ttu-id="3e7c0-248">W **hasło** tekstowym, wpisz hasło użytkownika.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-248">In the **Password** textbox, type the password of user.</span></span>

    <span data-ttu-id="3e7c0-249">e.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-249">e.</span></span> <span data-ttu-id="3e7c0-250">Kliknij przycisk **tworzenia użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-250">Click **Create user**.</span></span>   

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3e7c0-251">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e7c0-251">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3e7c0-252">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-252">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAML SSO for Jira by resolution GmbH.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="3e7c0-254">**Aby przypisać Simona Britta logowania jednokrotnego SAML dla Jira rozpoznawania GmbH, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="3e7c0-254">**To assign Britta Simon to SAML SSO for Jira by resolution GmbH, perform the following steps:**</span></span>

1. <span data-ttu-id="3e7c0-255">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-255">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="3e7c0-257">Na liście aplikacji zaznacz **logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH**.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-257">In the applications list, select **SAML SSO for Jira by resolution GmbH**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_app.png) 

3. <span data-ttu-id="3e7c0-259">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-259">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="3e7c0-261">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-261">Click **Add** button.</span></span> <span data-ttu-id="3e7c0-262">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-262">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="3e7c0-264">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-264">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3e7c0-265">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-265">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3e7c0-266">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-266">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3e7c0-267">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="3e7c0-267">Testing single sign-on</span></span>

<span data-ttu-id="3e7c0-268">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-268">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3e7c0-269">Kliknięcie logowania jednokrotnego SAML dla Jira rozpoznawania GmbH kafelka w panelu dostępu, możesz powinien pobrać automatycznie zalogowane do użytkownika logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3e7c0-269">When you click the SAML SSO for Jira by resolution GmbH tile in the Access Panel, you should get automatically signed-on to your SAML SSO for Jira by resolution GmbH application.</span></span>
<span data-ttu-id="3e7c0-270">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3e7c0-270">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3e7c0-271">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="3e7c0-271">Additional resources</span></span>

* [<span data-ttu-id="3e7c0-272">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3e7c0-272">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3e7c0-273">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3e7c0-273">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_203.png

