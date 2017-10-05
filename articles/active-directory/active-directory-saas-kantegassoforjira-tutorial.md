---
title: 'Samouczek: Azure Active Directory integracji z logowaniem Jednokrotnym Kantega dla JIRA | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i logowania jednokrotnego Kantega dla JIRA."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e2af4891-e3c8-43b3-bdcb-0500c493e9b4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 06a1d301818f025270137f7eaa9f40e5e4503112
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-jira"></a><span data-ttu-id="3e6bb-103">Samouczek: Azure Active Directory integracji z logowaniem Jednokrotnym Kantega dla JIRA</span><span class="sxs-lookup"><span data-stu-id="3e6bb-103">Tutorial: Azure Active Directory integration with Kantega SSO for JIRA</span></span>

<span data-ttu-id="3e6bb-104">Z tego samouczka dowiesz integrowanie logowania jednokrotnego Kantega dla JIRA w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3e6bb-104">In this tutorial, you learn how to integrate Kantega SSO for JIRA with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3e6bb-105">Integracja z usługą Azure AD logowania jednokrotnego Kantega dla JIRA zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="3e6bb-105">Integrating Kantega SSO for JIRA with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3e6bb-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do logowania jednokrotnego Kantega JIRA</span><span class="sxs-lookup"><span data-stu-id="3e6bb-106">You can control in Azure AD who has access to Kantega SSO for JIRA</span></span>
- <span data-ttu-id="3e6bb-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do logowania jednokrotnego Kantega dla JIRA (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e6bb-107">You can enable your users to automatically get signed-on to Kantega SSO for JIRA (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3e6bb-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="3e6bb-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3e6bb-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3e6bb-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3e6bb-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3e6bb-110">Prerequisites</span></span>

<span data-ttu-id="3e6bb-111">Aby skonfigurować integrację usługi Azure AD z logowania jednokrotnego Kantega dla JIRA, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="3e6bb-111">To configure Azure AD integration with Kantega SSO for JIRA, you need the following items:</span></span>

- <span data-ttu-id="3e6bb-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e6bb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3e6bb-113">Kantega Usługa rejestracji Jednokrotnej dla JIRA logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="3e6bb-113">A Kantega SSO for JIRA single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3e6bb-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3e6bb-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="3e6bb-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3e6bb-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3e6bb-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3e6bb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3e6bb-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="3e6bb-118">Scenario description</span></span>
<span data-ttu-id="3e6bb-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3e6bb-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="3e6bb-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3e6bb-121">Dodawanie logowania jednokrotnego Kantega dla JIRA z galerii</span><span class="sxs-lookup"><span data-stu-id="3e6bb-121">Adding Kantega SSO for JIRA from the gallery</span></span>
2. <span data-ttu-id="3e6bb-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="3e6bb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kantega-sso-for-jira-from-the-gallery"></a><span data-ttu-id="3e6bb-123">Dodawanie logowania jednokrotnego Kantega dla JIRA z galerii</span><span class="sxs-lookup"><span data-stu-id="3e6bb-123">Adding Kantega SSO for JIRA from the gallery</span></span>
<span data-ttu-id="3e6bb-124">Aby skonfigurować integrację Kantega sesji rejestracji jednokrotnej dla JIRA do usługi Azure AD, należy dodać logowania jednokrotnego Kantega dla JIRA z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-124">To configure the integration of Kantega SSO for JIRA into Azure AD, you need to add Kantega SSO for JIRA from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3e6bb-125">**Aby dodać logowania jednokrotnego Kantega dla JIRA z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="3e6bb-125">**To add Kantega SSO for JIRA from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3e6bb-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="3e6bb-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3e6bb-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="3e6bb-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="3e6bb-133">W polu wyszukiwania wpisz **Kantega Usługa rejestracji Jednokrotnej dla JIRA**.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-133">In the search box, type **Kantega SSO for JIRA**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_search.png)

5. <span data-ttu-id="3e6bb-135">W panelu wyników wybierz **Kantega Usługa rejestracji Jednokrotnej dla JIRA**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-135">In the results panel, select **Kantega SSO for JIRA**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3e6bb-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="3e6bb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3e6bb-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego Kantega dla JIRA w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-138">In this section, you configure and test Azure AD single sign-on with Kantega SSO for JIRA based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3e6bb-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w rejestracji Jednokrotnej Kantega dla JIRA jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kantega SSO for JIRA is to a user in Azure AD.</span></span> <span data-ttu-id="3e6bb-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w rejestracji Jednokrotnej Kantega dla JIRA musi się.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-140">In other words, a link relationship between an Azure AD user and the related user in Kantega SSO for JIRA needs to be established.</span></span>

<span data-ttu-id="3e6bb-141">W Kantega logowania jednokrotnego dla JIRA, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-141">In Kantega SSO for JIRA, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3e6bb-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego Kantega dla JIRA, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="3e6bb-142">To configure and test Azure AD single sign-on with Kantega SSO for JIRA, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3e6bb-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3e6bb-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3e6bb-145">**[Tworzenie Kantega Usługa rejestracji Jednokrotnej dla użytkownika testowego JIRA](#creating-a-kantega-sso-for-jira-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Kantega Usługa rejestracji Jednokrotnej dla JIRA połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-145">**[Creating a Kantega SSO for JIRA test user](#creating-a-kantega-sso-for-jira-test-user)** - to have a counterpart of Britta Simon in Kantega SSO for JIRA that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3e6bb-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3e6bb-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3e6bb-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="3e6bb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3e6bb-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w Twojej rejestracji Jednokrotnej Kantega JIRA aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kantega SSO for JIRA application.</span></span>

<span data-ttu-id="3e6bb-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego Kantega dla JIRA, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="3e6bb-150">**To configure Azure AD single sign-on with Kantega SSO for JIRA, perform the following steps:**</span></span>

1. <span data-ttu-id="3e6bb-151">W portalu Azure na **Kantega Usługa rejestracji Jednokrotnej dla JIRA** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-151">In the Azure portal, on the **Kantega SSO for JIRA** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="3e6bb-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_samlbase.png)

3. <span data-ttu-id="3e6bb-155">W **IDP** inicjowane w trybie **logowania jednokrotnego Kantega JIRA domeny i adresów URL** sekcji wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="3e6bb-155">In **IDP** initiated mode, on the **Kantega SSO for JIRA Domain and URLs** section perform the following step:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_url1.png)

    <span data-ttu-id="3e6bb-157">a.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-157">a.</span></span> <span data-ttu-id="3e6bb-158">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="3e6bb-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    <span data-ttu-id="3e6bb-159">b.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-159">b.</span></span> <span data-ttu-id="3e6bb-160">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="3e6bb-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

4. <span data-ttu-id="3e6bb-161">W **SP** inicjowane trybie wyboru **Pokaż zaawansowane ustawienia adresu URL** i wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="3e6bb-161">In **SP** initiated mode, check **Show advanced URL settings** and  perform the following step:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_url2.png)

    <span data-ttu-id="3e6bb-163">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="3e6bb-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3e6bb-164">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-164">These values are not real.</span></span> <span data-ttu-id="3e6bb-165">Rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-165">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="3e6bb-166">Te wartości są odbierane podczas konfigurowania Jira dodatek, który znajduje się w dalszej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-166">These values are received during the configuration of Jira plugin, which is explained later in the tutorial.</span></span>

5. <span data-ttu-id="3e6bb-167">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_certificate.png) 

6. <span data-ttu-id="3e6bb-169">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-169">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="3e6bb-171">W oknie przeglądarki innej witryny sieci web należy zalogować się jako administrator do Twojej JIRA na serwerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-171">In a different web browser window, log in to your JIRA on premise server as an administrator.</span></span>

8. <span data-ttu-id="3e6bb-172">Umieść kursor na koło zębate, a następnie kliknij przycisk **dodatki**.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-172">Hover on cog and click the **Add-ons**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforjira-tutorial/addon1.png)

9. <span data-ttu-id="3e6bb-174">W sekcji Karta dodatki, kliknij przycisk **znaleźć nowe dodatki**.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-174">Under Add-ons tab section, click **Find new add-ons**.</span></span> <span data-ttu-id="3e6bb-175">Wyszukiwanie **Kantega Usługa rejestracji Jednokrotnej dla JIRA (SAML i protokołu Kerberos)** i kliknij przycisk **zainstalować** przycisk, aby zainstalować nowy wtyczki SAML.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-175">Search **Kantega SSO for JIRA (SAML & Kerberos)** and click **Install** button to install the new SAML plugin.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforjira-tutorial/addon2.png)

10. <span data-ttu-id="3e6bb-177">Uruchamia instalację dodatku.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-177">The plugin installation starts.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforjira-tutorial/addon3.png)

11. <span data-ttu-id="3e6bb-179">Po zakończeniu instalacji.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-179">Once the installation is complete.</span></span> <span data-ttu-id="3e6bb-180">Kliknij przycisk **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-180">Click **Close**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforjira-tutorial/addon33.png)

12. <span data-ttu-id="3e6bb-182">Kliknij pozycję **Zarządzaj**.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-182">Click **Manage**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforjira-tutorial/addon34.png)
    
13. <span data-ttu-id="3e6bb-184">Nowej wtyczki znajduje się w obszarze **integracji**.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-184">New plugin is listed under **INTEGRATIONS**.</span></span> <span data-ttu-id="3e6bb-185">Kliknij przycisk **Konfiguruj** do skonfigurowania nowej wtyczki.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-185">Click **Configure** to configure the new plugin.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforjira-tutorial/addon35.png)

14. <span data-ttu-id="3e6bb-187">W **SAML** sekcji.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-187">In the **SAML** section.</span></span> <span data-ttu-id="3e6bb-188">Wybierz **usługi Azure Active Directory (Azure AD)** z **dostawcy tożsamości Dodaj** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-188">Select **Azure Active Directory (Azure AD)** from the **Add identity provider** dropdown.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforjira-tutorial/addon4.png)

15. <span data-ttu-id="3e6bb-190">Wybierz poziom subskrypcji jako **podstawowe**.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-190">Select subscription level as **Basic**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforjira-tutorial/addon5.png)     

16. <span data-ttu-id="3e6bb-192">Na **właściwości aplikacji** sekcji, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="3e6bb-192">On the **App properties** section, perform following steps:</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforjira-tutorial/addon6.png)

    <span data-ttu-id="3e6bb-194">a.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-194">a.</span></span> <span data-ttu-id="3e6bb-195">Kopiuj **identyfikator URI aplikacji** wartości i używać go jako **identyfikator, adres URL odpowiedzi i adres URL logowania** na **logowania jednokrotnego Kantega JIRA domeny i adresów URL** sekcji w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-195">Copy the **App ID URI** value and use it as **Identifier, Reply URL, and Sign-On URL** on the **Kantega SSO for JIRA Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="3e6bb-196">b.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-196">b.</span></span> <span data-ttu-id="3e6bb-197">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-197">Click **Next**.</span></span>

17. <span data-ttu-id="3e6bb-198">Na **importu metadanych** sekcji, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="3e6bb-198">On the **Metadata import** section, perform following steps:</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforjira-tutorial/addon7.png)

    <span data-ttu-id="3e6bb-200">a.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-200">a.</span></span> <span data-ttu-id="3e6bb-201">Wybierz **pliku metadanych na tym komputerze**i przekazywanie pliku metadanych, który został pobrany z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-201">Select **Metadata file on my computer**, and upload metadata file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="3e6bb-202">b.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-202">b.</span></span> <span data-ttu-id="3e6bb-203">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-203">Click **Next**.</span></span>

18. <span data-ttu-id="3e6bb-204">Na **nazwę i logowania jednokrotnego lokalizację** sekcji, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="3e6bb-204">On the **Name and SSO location** section, perform following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforjira-tutorial/addon8.png)
    
    <span data-ttu-id="3e6bb-206">a.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-206">a.</span></span> <span data-ttu-id="3e6bb-207">Dodaj nazwę dostawcy tożsamości w **Nazwa dostawcy tożsamości** pola tekstowego (np. usługi Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3e6bb-207">Add Name of the Identity Provider in **Identity provider name** textbox (e.g Azure AD).</span></span>

    <span data-ttu-id="3e6bb-208">b.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-208">b.</span></span> <span data-ttu-id="3e6bb-209">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-209">Click **Next**.</span></span>

19. <span data-ttu-id="3e6bb-210">Sprawdź certyfikatu podpisywania, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-210">Verify the Signing certificate and click **Next**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforjira-tutorial/addon9.png)

20. <span data-ttu-id="3e6bb-212">Na **kont użytkowników JIRA** sekcji, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="3e6bb-212">On the **JIRA user accounts** section, perform following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforjira-tutorial/addon10.png)

    <span data-ttu-id="3e6bb-214">a.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-214">a.</span></span> <span data-ttu-id="3e6bb-215">Wybierz **tworzenie użytkowników w katalogu wewnętrzny JIRA firmy, w razie potrzeby** , a następnie wprowadź odpowiednią nazwę grupy użytkowników (może być wiele nie.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-215">Select **Create users in JIRA's internal Directory if needed** and enter the appropriate name of the group for users (can be multiple no.</span></span> <span data-ttu-id="3e6bb-216">grup rozdzielone przecinkami).</span><span class="sxs-lookup"><span data-stu-id="3e6bb-216">of groups separated by comma).</span></span>

    <span data-ttu-id="3e6bb-217">b.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-217">b.</span></span> <span data-ttu-id="3e6bb-218">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-218">Click **Next**.</span></span>

21. <span data-ttu-id="3e6bb-219">Kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-219">Click **Finish**.</span></span>   

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforjira-tutorial/addon11.png)

22. <span data-ttu-id="3e6bb-221">Na **znanych domeny dla usługi Azure AD** sekcji, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="3e6bb-221">On the **Known domains for Azure AD** section, perform following steps:</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforjira-tutorial/addon12.png)

    <span data-ttu-id="3e6bb-223">a.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-223">a.</span></span> <span data-ttu-id="3e6bb-224">Wybierz **znane domen** z lewego panelu strony.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-224">Select **Known domains** from the left panel of the page.</span></span>

    <span data-ttu-id="3e6bb-225">b.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-225">b.</span></span> <span data-ttu-id="3e6bb-226">Wprowadź nazwę domeny w **znane domen** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-226">Enter domain name in the **Known domains** textbox.</span></span>

    <span data-ttu-id="3e6bb-227">c.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-227">c.</span></span> <span data-ttu-id="3e6bb-228">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-228">Click **Save**.</span></span> 

> [!TIP]
> <span data-ttu-id="3e6bb-229">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="3e6bb-229">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3e6bb-230">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-230">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3e6bb-231">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3e6bb-231">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3e6bb-232">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e6bb-232">Creating an Azure AD test user</span></span>
<span data-ttu-id="3e6bb-233">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-233">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="3e6bb-235">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="3e6bb-235">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3e6bb-236">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-236">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kantegassoforjira-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3e6bb-238">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-238">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kantegassoforjira-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3e6bb-240">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-240">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kantegassoforjira-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3e6bb-242">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="3e6bb-242">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kantegassoforjira-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3e6bb-244">a.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-244">a.</span></span> <span data-ttu-id="3e6bb-245">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-245">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3e6bb-246">b.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-246">b.</span></span> <span data-ttu-id="3e6bb-247">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-247">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3e6bb-248">c.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-248">c.</span></span> <span data-ttu-id="3e6bb-249">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-249">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3e6bb-250">d.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-250">d.</span></span> <span data-ttu-id="3e6bb-251">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-251">Click **Create**.</span></span>
 
### <a name="creating-a-kantega-sso-for-jira-test-user"></a><span data-ttu-id="3e6bb-252">Tworzenie Kantega Usługa rejestracji Jednokrotnej dla użytkownika testowego JIRA</span><span class="sxs-lookup"><span data-stu-id="3e6bb-252">Creating a Kantega SSO for JIRA test user</span></span>

<span data-ttu-id="3e6bb-253">Aby umożliwić użytkownikom usługi Azure AD zalogować się do JIRA, musi być przygotowana do JIRA.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-253">To enable Azure AD users to log in to JIRA, they must be provisioned into JIRA.</span></span> <span data-ttu-id="3e6bb-254">W Kantega logowania jednokrotnego dla JIRA Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-254">In Kantega SSO for JIRA, provisioning is a manual task.</span></span>

<span data-ttu-id="3e6bb-255">**Aby udostępnić konta użytkownika, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="3e6bb-255">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="3e6bb-256">Zaloguj się do sieci JIRA na lokalnym serwerze jako administrator.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-256">Log in to your JIRA on premise server as an administrator.</span></span>

2. <span data-ttu-id="3e6bb-257">Umieść kursor na koło zębate, a następnie kliknij przycisk **Zarządzanie użytkownikami**.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-257">Hover on cog and click the **User management**.</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-kantegassoforjira-tutorial/user1.png) 

3. <span data-ttu-id="3e6bb-259">W obszarze **Zarządzanie użytkownikami** sekcji, kliknij pozycję **tworzenia użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-259">Under **User management** tab section, click **Create user**.</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-kantegassoforjira-tutorial/user2.png) 

4. <span data-ttu-id="3e6bb-261">Na **"Tworzenie nowego użytkownika"** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="3e6bb-261">On the **“Create new user”** dialog page, perform the following steps:</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-kantegassoforjira-tutorial/user3.png) 

    <span data-ttu-id="3e6bb-263">a.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-263">a.</span></span> <span data-ttu-id="3e6bb-264">W **adres E-mail** tekstowym, wpisz adres e-mail użytkownika, takich jak Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-264">In the **Email address** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="3e6bb-265">b.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-265">b.</span></span> <span data-ttu-id="3e6bb-266">W **imię i nazwisko** pole tekstowe, pełna nazwa typu użytkownika, takich jak Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-266">In the **Full Name** textbox, type full name of the user like Britta Simon.</span></span>

    <span data-ttu-id="3e6bb-267">c.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-267">c.</span></span> <span data-ttu-id="3e6bb-268">W **Username** tekstowym, wpisz adres e-mail użytkownika, takich jak Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-268">In the **Username** textbox, type the email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="3e6bb-269">d.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-269">d.</span></span> <span data-ttu-id="3e6bb-270">W **hasło** tekstowym, wpisz hasło użytkownika.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-270">In the **Password** textbox, type the password of user.</span></span>

    <span data-ttu-id="3e6bb-271">e.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-271">e.</span></span> <span data-ttu-id="3e6bb-272">Kliknij przycisk **tworzenia użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-272">Click **Create user**.</span></span>   

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3e6bb-273">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e6bb-273">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3e6bb-274">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do logowania jednokrotnego Kantega dla JIRA.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-274">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kantega SSO for JIRA.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="3e6bb-276">**Aby przypisać Simona Britta do logowania jednokrotnego Kantega dla JIRA, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="3e6bb-276">**To assign Britta Simon to Kantega SSO for JIRA, perform the following steps:**</span></span>

1. <span data-ttu-id="3e6bb-277">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-277">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="3e6bb-279">Na liście aplikacji zaznacz **Kantega Usługa rejestracji Jednokrotnej dla JIRA**.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-279">In the applications list, select **Kantega SSO for JIRA**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_app.png) 

3. <span data-ttu-id="3e6bb-281">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-281">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="3e6bb-283">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-283">Click **Add** button.</span></span> <span data-ttu-id="3e6bb-284">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-284">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="3e6bb-286">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-286">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3e6bb-287">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-287">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3e6bb-288">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-288">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3e6bb-289">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="3e6bb-289">Testing single sign-on</span></span>

<span data-ttu-id="3e6bb-290">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-290">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3e6bb-291">Po kliknięciu logowania jednokrotnego Kantega JIRA kafelka w panelu dostępu należy należy pobrać automatycznie zalogowane do rejestracji Jednokrotnej z Kantega JIRA aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3e6bb-291">When you click the Kantega SSO for JIRA tile in the Access Panel, you should get automatically signed-on to your Kantega SSO for JIRA application.</span></span>
<span data-ttu-id="3e6bb-292">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3e6bb-292">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3e6bb-293">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="3e6bb-293">Additional resources</span></span>

* [<span data-ttu-id="3e6bb-294">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3e6bb-294">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3e6bb-295">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3e6bb-295">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_203.png

