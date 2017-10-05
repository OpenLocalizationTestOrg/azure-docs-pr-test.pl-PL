---
title: 'Samouczek: Integracji Azure Active Directory z logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak skonfigurować logowanie jednokrotne między usługą Azure Active Directory i logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6b47d483-d3a3-442d-b123-171e3f0f7486
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: 9a36d686ba39b5168860a20e8c4db357888df6a7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-saml-sso-for-confluence-by-resolution-gmbh"></a><span data-ttu-id="75c15-103">Samouczek: Integracji Azure Active Directory z logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH</span><span class="sxs-lookup"><span data-stu-id="75c15-103">Tutorial: Azure Active Directory integration with SAML SSO for Confluence by resolution GmbH</span></span>

<span data-ttu-id="75c15-104">Z tego samouczka dowiesz się integrowanie logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="75c15-104">In this tutorial, you learn how to integrate SAML SSO for Confluence by resolution GmbH with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="75c15-105">Integrowanie logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="75c15-105">Integrating SAML SSO for Confluence by resolution GmbH with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="75c15-106">Można kontrolować w usłudze Azure AD, który ma dostęp do logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH</span><span class="sxs-lookup"><span data-stu-id="75c15-106">You can control in Azure AD who has access to SAML SSO for Confluence by resolution GmbH</span></span>
- <span data-ttu-id="75c15-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="75c15-107">You can enable your users to automatically get signed-on to SAML SSO for Confluence by resolution GmbH (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="75c15-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="75c15-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="75c15-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="75c15-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="75c15-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="75c15-110">Prerequisites</span></span>

<span data-ttu-id="75c15-111">Aby skonfigurować integrację usługi Azure AD z logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="75c15-111">To configure Azure AD integration with SAML SSO for Confluence by resolution GmbH, you need the following items:</span></span>

- <span data-ttu-id="75c15-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="75c15-112">An Azure AD subscription</span></span>
- <span data-ttu-id="75c15-113">Logowania jednokrotnego SAML dla zlewiska przez rozpoznawanie jednokrotnego GmbH w subskrypcji włączone</span><span class="sxs-lookup"><span data-stu-id="75c15-113">A SAML SSO for Confluence by resolution GmbH single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="75c15-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="75c15-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="75c15-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="75c15-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="75c15-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="75c15-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="75c15-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="75c15-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="75c15-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="75c15-118">Scenario description</span></span>
<span data-ttu-id="75c15-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="75c15-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="75c15-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="75c15-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="75c15-121">Dodawanie logowania jednokrotnego SAML dla zlewiska przy rozdzielczości GmbH z galerii</span><span class="sxs-lookup"><span data-stu-id="75c15-121">Adding SAML SSO for Confluence by resolution GmbH from the gallery</span></span>
2. <span data-ttu-id="75c15-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="75c15-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-saml-sso-for-confluence-by-resolution-gmbh-from-the-gallery"></a><span data-ttu-id="75c15-123">Dodawanie logowania jednokrotnego SAML dla zlewiska przy rozdzielczości GmbH z galerii</span><span class="sxs-lookup"><span data-stu-id="75c15-123">Adding SAML SSO for Confluence by resolution GmbH from the gallery</span></span>

<span data-ttu-id="75c15-124">Aby skonfigurować integrację logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH do usługi Azure AD, należy dodać logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="75c15-124">To configure the integration of SAML SSO for Confluence by resolution GmbH into Azure AD, you need to add SAML SSO for Confluence by resolution GmbH from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="75c15-125">**Aby dodać logowania jednokrotnego SAML dla zlewiska za rozdzielczość GmbH z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="75c15-125">**To add SAML SSO for Confluence by resolution GmbH from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="75c15-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="75c15-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="75c15-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="75c15-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="75c15-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="75c15-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="75c15-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="75c15-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="75c15-133">W polu wyszukiwania wpisz **logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH**.</span><span class="sxs-lookup"><span data-stu-id="75c15-133">In the search box, type **SAML SSO for Confluence by resolution GmbH**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_search.png)

5. <span data-ttu-id="75c15-135">W panelu wyników wybierz **logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="75c15-135">In the results panel, select **SAML SSO for Confluence by resolution GmbH**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="75c15-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="75c15-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="75c15-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego SAML dla zlewiska przez rozdzielczość GmbH oparte na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="75c15-138">In this section, you configure and test Azure AD single sign-on with SAML SSO for Confluence by resolution GmbH based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="75c15-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, jakiego odpowiednikiem użytkownika w logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH jest użytkownikiem w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="75c15-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SAML SSO for Confluence by resolution GmbH is to a user in Azure AD.</span></span> <span data-ttu-id="75c15-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i danemu użytkownikowi w logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH musi się.</span><span class="sxs-lookup"><span data-stu-id="75c15-140">In other words, a link relationship between an Azure AD user and the related user in SAML SSO for Confluence by resolution GmbH needs to be established.</span></span>

<span data-ttu-id="75c15-141">W logowania jednokrotnego SAML zlewiska przez rozpoznawania GmbH, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="75c15-141">In SAML SSO for Confluence by resolution GmbH, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="75c15-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="75c15-142">To configure and test Azure AD single sign-on with SAML SSO for Confluence by resolution GmbH, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="75c15-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="75c15-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="75c15-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="75c15-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="75c15-145">**[Tworzenie logowania jednokrotnego SAML dla zlewiska przez użytkownika testowego GmbH rozpoznawania](#creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="75c15-145">**[Creating a SAML SSO for Confluence by resolution GmbH test user](#creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user)** - to have a counterpart of Britta Simon in SAML SSO for Confluence by resolution GmbH that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="75c15-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="75c15-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="75c15-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="75c15-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="75c15-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="75c15-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="75c15-149">W tej sekcji możesz włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w sieci logowania jednokrotnego SAML dla zlewiska przy rozpoznawania GmbH aplikacji.</span><span class="sxs-lookup"><span data-stu-id="75c15-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAML SSO for Confluence by resolution GmbH application.</span></span>

<span data-ttu-id="75c15-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="75c15-150">**To configure Azure AD single sign-on with SAML SSO for Confluence by resolution GmbH, perform the following steps:**</span></span>

1. <span data-ttu-id="75c15-151">W portalu Azure na **logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="75c15-151">In the Azure portal, on the **SAML SSO for Confluence by resolution GmbH** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="75c15-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="75c15-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_samlbase.png)

3. <span data-ttu-id="75c15-155">Na **logowania jednokrotnego SAML zlewiska przez rozpoznawania GmbH domeny i adresów URL** sekcji, jeśli chcesz skonfigurować aplikację w **IDP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="75c15-155">On the **SAML SSO for Confluence by resolution GmbH Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_url_1.png)

    <span data-ttu-id="75c15-157">a.</span><span class="sxs-lookup"><span data-stu-id="75c15-157">a.</span></span> <span data-ttu-id="75c15-158">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="75c15-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

    <span data-ttu-id="75c15-159">b.</span><span class="sxs-lookup"><span data-stu-id="75c15-159">b.</span></span> <span data-ttu-id="75c15-160">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="75c15-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

4. <span data-ttu-id="75c15-161">Sprawdź **Pokaż zaawansowane ustawienia adresu URL**.</span><span class="sxs-lookup"><span data-stu-id="75c15-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="75c15-162">Jeśli chcesz skonfigurować aplikację w **SP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="75c15-162">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_url_2.png)

    <span data-ttu-id="75c15-164">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="75c15-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="75c15-165">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="75c15-165">These values are not real.</span></span> <span data-ttu-id="75c15-166">Rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="75c15-166">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="75c15-167">Skontaktuj się z [zespołu obsługi logowania jednokrotnego SAML dla zlewiska przez rozpoznawania klienta GmbH](https://www.resolution.de/go/support) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="75c15-167">Contact [SAML SSO for Confluence by resolution GmbH Client support team](https://www.resolution.de/go/support) to get these values.</span></span> 

5. <span data-ttu-id="75c15-168">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="75c15-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_certificate.png) 

6. <span data-ttu-id="75c15-170">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="75c15-170">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_400.png)  
    
7. <span data-ttu-id="75c15-172">W oknie przeglądarki innej witryny sieci web, zaloguj się do Twojego **logowania jednokrotnego SAML dla zlewiska przez portal administracyjny GmbH rozpoznawania** jako administrator.</span><span class="sxs-lookup"><span data-stu-id="75c15-172">In a different web browser window, log in to your **SAML SSO for Confluence by resolution GmbH admin portal** as an administrator.</span></span>

8. <span data-ttu-id="75c15-173">Umieść kursor na koło zębate, a następnie kliknij przycisk **dodatki**.</span><span class="sxs-lookup"><span data-stu-id="75c15-173">Hover on cog and click the **Add-ons**.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/addon1.png)

9. <span data-ttu-id="75c15-175">Nastąpi przekierowanie do strony dostępu administratora.</span><span class="sxs-lookup"><span data-stu-id="75c15-175">You are redirected to Administrator Access page.</span></span> <span data-ttu-id="75c15-176">Wprowadź hasło i kliknij przycisk **Potwierdź** przycisku.</span><span class="sxs-lookup"><span data-stu-id="75c15-176">Enter the password and click **Confirm** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/addon2.png)

10. <span data-ttu-id="75c15-178">W obszarze **ATLASSIAN MARKETPLACE** , kliknij pozycję **znaleźć nowe dodatki**.</span><span class="sxs-lookup"><span data-stu-id="75c15-178">Under **ATLASSIAN MARKETPLACE** tab, click **Find new add-ons**.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/addon.png)

11. <span data-ttu-id="75c15-180">Wyszukiwanie **SAML pojedynczy znak na rejestracji jednokrotnej (SSO) dla zlewiska** i kliknij przycisk **zainstalować** przycisk, aby zainstalować nowy wtyczki SAML.</span><span class="sxs-lookup"><span data-stu-id="75c15-180">Search **SAML Single Sign On (SSO) for Confluence** and click **Install** button to install the new SAML plugin.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/addon7.png)

12. <span data-ttu-id="75c15-182">Uruchomi instalację dodatku.</span><span class="sxs-lookup"><span data-stu-id="75c15-182">The plugin installation will start.</span></span> <span data-ttu-id="75c15-183">Kliknij przycisk **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="75c15-183">Click **Close**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/addon8.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/addon9.png)

13. <span data-ttu-id="75c15-186">Kliknij pozycję **Zarządzaj**.</span><span class="sxs-lookup"><span data-stu-id="75c15-186">Click **Manage**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/addon10.png)
    
14. <span data-ttu-id="75c15-188">Kliknij przycisk **Konfiguruj** do skonfigurowania nowej wtyczki.</span><span class="sxs-lookup"><span data-stu-id="75c15-188">Click **Configure** to configure the new plugin.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/addon11.png)

15. <span data-ttu-id="75c15-190">Tej nowej wtyczki można także znaleźć w obszarze **użytkowników i zabezpieczenia** kartę.</span><span class="sxs-lookup"><span data-stu-id="75c15-190">This new plugin can also be found under **USERS & SECURITY** tab.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/addon3.png)
    
16. <span data-ttu-id="75c15-192">Na **konfiguracji wtyczki SingleSignOn SAML** kliknij przycisk **dodać dodatkowe dostawcy tożsamości** przycisk, aby skonfigurować ustawienia dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="75c15-192">On **SAML SingleSignOn Plugin Configuration** page, click **Add additional Identity Provider** button to configure the settings of Identity Provider.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/addon4.png)

17. <span data-ttu-id="75c15-194">Wykonaj następujące kroki na tej stronie:</span><span class="sxs-lookup"><span data-stu-id="75c15-194">Perform following steps on this page:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/addon5.png)
 
    <span data-ttu-id="75c15-196">a.</span><span class="sxs-lookup"><span data-stu-id="75c15-196">a.</span></span> <span data-ttu-id="75c15-197">Dodaj **nazwa** dostawcy tożsamości (np. usługi Azure AD).</span><span class="sxs-lookup"><span data-stu-id="75c15-197">Add **Name** of the Identity Provider (e.g Azure AD).</span></span>
    
    <span data-ttu-id="75c15-198">b.</span><span class="sxs-lookup"><span data-stu-id="75c15-198">b.</span></span> <span data-ttu-id="75c15-199">Dodaj **opis** dostawcy tożsamości (np. usługi Azure AD).</span><span class="sxs-lookup"><span data-stu-id="75c15-199">Add **Description** of the Identity Provider (e.g Azure AD).</span></span>

    <span data-ttu-id="75c15-200">c.</span><span class="sxs-lookup"><span data-stu-id="75c15-200">c.</span></span> <span data-ttu-id="75c15-201">Kliknij przycisk **XML** i wybierz **metadanych** pliku, który został pobrany z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="75c15-201">Click **XML** and select the **Metadata** file that you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="75c15-202">d.</span><span class="sxs-lookup"><span data-stu-id="75c15-202">d.</span></span> <span data-ttu-id="75c15-203">Kliknij przycisk **obciążenia** przycisku.</span><span class="sxs-lookup"><span data-stu-id="75c15-203">Click **Load** button.</span></span>

    <span data-ttu-id="75c15-204">e.</span><span class="sxs-lookup"><span data-stu-id="75c15-204">e.</span></span> <span data-ttu-id="75c15-205">Odczytuje metadanych IdP i wypełni pola jako wyróżnione na zrzucie ekranu.</span><span class="sxs-lookup"><span data-stu-id="75c15-205">It reads the IdP metadata and populates the fields as highlighted in the screenshot.</span></span> 
18. <span data-ttu-id="75c15-206">Kliknij przycisk **Zapisz ustawienia** przycisk, aby zapisać ustawienia.</span><span class="sxs-lookup"><span data-stu-id="75c15-206">Click **Save settings** button to save the settings.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/addon6.png)

> [!TIP]
> <span data-ttu-id="75c15-208">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="75c15-208">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="75c15-209">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="75c15-209">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="75c15-210">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="75c15-210">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="75c15-211">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="75c15-211">Creating an Azure AD test user</span></span>
<span data-ttu-id="75c15-212">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="75c15-212">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="75c15-214">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="75c15-214">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="75c15-215">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="75c15-215">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="75c15-217">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="75c15-217">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="75c15-219">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="75c15-219">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="75c15-221">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="75c15-221">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="75c15-223">a.</span><span class="sxs-lookup"><span data-stu-id="75c15-223">a.</span></span> <span data-ttu-id="75c15-224">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="75c15-224">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="75c15-225">b.</span><span class="sxs-lookup"><span data-stu-id="75c15-225">b.</span></span> <span data-ttu-id="75c15-226">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="75c15-226">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="75c15-227">c.</span><span class="sxs-lookup"><span data-stu-id="75c15-227">c.</span></span> <span data-ttu-id="75c15-228">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="75c15-228">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="75c15-229">d.</span><span class="sxs-lookup"><span data-stu-id="75c15-229">d.</span></span> <span data-ttu-id="75c15-230">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="75c15-230">Click **Create**.</span></span>
 
### <a name="creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user"></a><span data-ttu-id="75c15-231">Tworzenie logowania jednokrotnego SAML dla zlewiska przez użytkownika testowego GmbH rozwiązania</span><span class="sxs-lookup"><span data-stu-id="75c15-231">Creating a SAML SSO for Confluence by resolution GmbH test user</span></span>

<span data-ttu-id="75c15-232">Aby umożliwić użytkownikom usługi Azure AD zalogowanie się do logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH, ich muszą mieć przydzielone do logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH.</span><span class="sxs-lookup"><span data-stu-id="75c15-232">To enable Azure AD users to log in to SAML SSO for Confluence by resolution GmbH, they must be provisioned into SAML SSO for Confluence by resolution GmbH.</span></span>  
<span data-ttu-id="75c15-233">W logowania jednokrotnego SAML zlewiska przez rozpoznawania GmbH Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="75c15-233">In SAML SSO for Confluence by resolution GmbH, provisioning is a manual task.</span></span>

<span data-ttu-id="75c15-234">**Aby udostępnić konta użytkownika, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="75c15-234">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="75c15-235">Zaloguj się do użytkownika logowania jednokrotnego SAML dla zlewiska przez witrynę firmy GmbH rozpoznawania jako administrator.</span><span class="sxs-lookup"><span data-stu-id="75c15-235">Log in to your SAML SSO for Confluence by resolution GmbH company site as an administrator.</span></span>

2. <span data-ttu-id="75c15-236">Umieść kursor na koło zębate, a następnie kliknij przycisk **Zarządzanie użytkownikami**.</span><span class="sxs-lookup"><span data-stu-id="75c15-236">Hover on cog and click the **User management**.</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-samlssoconfluence-tutorial/user1.png) 

3. <span data-ttu-id="75c15-238">W sekcji Użytkownicy kliknij **dodawania użytkowników** kartę.</span><span class="sxs-lookup"><span data-stu-id="75c15-238">Under Users section, click **Add users** tab.</span></span> <span data-ttu-id="75c15-239">Na **"Dodaj użytkownika"** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="75c15-239">On the **“Add a User”** dialog page, perform the following steps:</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-samlssoconfluence-tutorial/user2.png) 

    <span data-ttu-id="75c15-241">a.</span><span class="sxs-lookup"><span data-stu-id="75c15-241">a.</span></span> <span data-ttu-id="75c15-242">W **Username** tekstowym, wpisz adres e-mail użytkownika, takich jak Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="75c15-242">In the **Username** textbox, type the email of user like Britta Simon.</span></span>

    <span data-ttu-id="75c15-243">b.</span><span class="sxs-lookup"><span data-stu-id="75c15-243">b.</span></span> <span data-ttu-id="75c15-244">W **imię i nazwisko** tekstowym, wpisz pełną nazwę użytkownika, takich jak Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="75c15-244">In the **Full Name** textbox, type the full name of user like Britta Simon.</span></span>

    <span data-ttu-id="75c15-245">c.</span><span class="sxs-lookup"><span data-stu-id="75c15-245">c.</span></span> <span data-ttu-id="75c15-246">W **E-mail** tekstowym, wpisz adres e-mail użytkownika, takich jak Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="75c15-246">In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="75c15-247">d.</span><span class="sxs-lookup"><span data-stu-id="75c15-247">d.</span></span> <span data-ttu-id="75c15-248">W **hasło** tekstowym, wpisz hasło dla Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="75c15-248">In the **Password** textbox, type the password for Britta Simon.</span></span>

    <span data-ttu-id="75c15-249">e.</span><span class="sxs-lookup"><span data-stu-id="75c15-249">e.</span></span> <span data-ttu-id="75c15-250">Kliknij przycisk **Potwierdź hasło** wprowadź ponownie hasło.</span><span class="sxs-lookup"><span data-stu-id="75c15-250">Click **Confirm Password** reenter the password.</span></span>
    
    <span data-ttu-id="75c15-251">f.</span><span class="sxs-lookup"><span data-stu-id="75c15-251">f.</span></span> <span data-ttu-id="75c15-252">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="75c15-252">Click **Add** button.</span></span>    

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="75c15-253">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="75c15-253">Assigning the Azure AD test user</span></span>

<span data-ttu-id="75c15-254">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH.</span><span class="sxs-lookup"><span data-stu-id="75c15-254">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAML SSO for Confluence by resolution GmbH.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="75c15-256">**Aby przypisać Simona Britta logowania jednokrotnego SAML dla zlewiska rozpoznawania GmbH, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="75c15-256">**To assign Britta Simon to SAML SSO for Confluence by resolution GmbH, perform the following steps:**</span></span>

1. <span data-ttu-id="75c15-257">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="75c15-257">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="75c15-259">Na liście aplikacji zaznacz **logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH**.</span><span class="sxs-lookup"><span data-stu-id="75c15-259">In the applications list, select **SAML SSO for Confluence by resolution GmbH**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_app.png) 

3. <span data-ttu-id="75c15-261">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="75c15-261">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="75c15-263">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="75c15-263">Click **Add** button.</span></span> <span data-ttu-id="75c15-264">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="75c15-264">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="75c15-266">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="75c15-266">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="75c15-267">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="75c15-267">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="75c15-268">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="75c15-268">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="75c15-269">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="75c15-269">Testing single sign-on</span></span>

<span data-ttu-id="75c15-270">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="75c15-270">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="75c15-271">Kliknięcie logowania jednokrotnego SAML dla zlewiska rozpoznawania GmbH kafelka w panelu dostępu, możesz powinien pobrać automatycznie zalogowane do użytkownika logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH aplikacji.</span><span class="sxs-lookup"><span data-stu-id="75c15-271">When you click the SAML SSO for Confluence by resolution GmbH tile in the Access Panel, you should get automatically signed-on to your SAML SSO for Confluence by resolution GmbH application.</span></span>
<span data-ttu-id="75c15-272">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="75c15-272">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="75c15-273">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="75c15-273">Additional resources</span></span>

* [<span data-ttu-id="75c15-274">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="75c15-274">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="75c15-275">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="75c15-275">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_203.png

