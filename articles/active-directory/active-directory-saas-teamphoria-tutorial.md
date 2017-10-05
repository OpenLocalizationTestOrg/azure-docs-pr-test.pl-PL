---
title: 'Samouczek: Integracji Azure Active Directory z Teamphoria | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Teamphoria."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d569c705-6f0f-4ec1-b485-ba82526b5d32
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: 2a35efb04d7fe22abc6894c149caf090666ce016
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamphoria"></a><span data-ttu-id="ff357-103">Samouczek: Integracji Azure Active Directory z Teamphoria</span><span class="sxs-lookup"><span data-stu-id="ff357-103">Tutorial: Azure Active Directory integration with Teamphoria</span></span>

<span data-ttu-id="ff357-104">Z tego samouczka dowiesz się integrowanie Teamphoria z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ff357-104">In this tutorial, you learn how to integrate Teamphoria with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ff357-105">Integracja z usługą Azure AD Teamphoria zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="ff357-105">Integrating Teamphoria with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ff357-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Teamphoria</span><span class="sxs-lookup"><span data-stu-id="ff357-106">You can control in Azure AD who has access to Teamphoria</span></span>
- <span data-ttu-id="ff357-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Teamphoria (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ff357-107">You can enable your users to automatically get signed-on to Teamphoria (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ff357-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu zarządzania Azure</span><span class="sxs-lookup"><span data-stu-id="ff357-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="ff357-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ff357-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

To enable single sign-on with Teamphoria, it must be configured to use Azure Active Directory as an identity provider. This guide provides information and tips on how to perform this configuration in Teamphoria.

>[!Note]: 
>This embedded guide is brand new in the new Azure portal, and we’d love to hear your thoughts. Use the Feedback ? button at the top of the portal to provide feedback. The older guide for using the [Azure classic portal](https://manage.windowsazure.com) to configure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="ff357-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ff357-110">Prerequisites</span></span>

<span data-ttu-id="ff357-111">Aby skonfigurować integrację usługi Azure AD z Teamphoria, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="ff357-111">To configure Azure AD integration with Teamphoria, you need the following items:</span></span>

- <span data-ttu-id="ff357-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ff357-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ff357-113">Teamphoria jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="ff357-113">A Teamphoria single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ff357-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="ff357-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ff357-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="ff357-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ff357-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="ff357-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="ff357-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ff357-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ff357-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="ff357-118">Scenario description</span></span>
<span data-ttu-id="ff357-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="ff357-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ff357-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="ff357-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ff357-121">Dodawanie Teamphoria z galerii</span><span class="sxs-lookup"><span data-stu-id="ff357-121">Adding Teamphoria from the gallery</span></span>
2. <span data-ttu-id="ff357-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="ff357-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-teamphoria-from-the-gallery"></a><span data-ttu-id="ff357-123">Dodawanie Teamphoria z galerii</span><span class="sxs-lookup"><span data-stu-id="ff357-123">Adding Teamphoria from the gallery</span></span>
<span data-ttu-id="ff357-124">Aby skonfigurować integrację usługi Azure AD Teamphoria, należy dodać Teamphoria z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="ff357-124">To configure the integration of Teamphoria into Azure AD, you need to add Teamphoria from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ff357-125">**Aby dodać Teamphoria z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="ff357-125">**To add Teamphoria from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ff357-126">W  **[portalu zarządzania Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ff357-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="ff357-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="ff357-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ff357-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ff357-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="ff357-131">Kliknij przycisk **Dodaj** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ff357-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="ff357-133">W polu wyszukiwania wpisz **Teamphoria**.</span><span class="sxs-lookup"><span data-stu-id="ff357-133">In the search box, type **Teamphoria**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_search.png)

5. <span data-ttu-id="ff357-135">W panelu wyników wybierz **Teamphoria**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="ff357-135">In the results panel, select **Teamphoria**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ff357-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="ff357-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ff357-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Teamphoria w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="ff357-138">In this section, you configure and test Azure AD single sign-on with Teamphoria based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ff357-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Teamphoria jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ff357-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Teamphoria is to a user in Azure AD.</span></span> <span data-ttu-id="ff357-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Teamphoria musi się.</span><span class="sxs-lookup"><span data-stu-id="ff357-140">In other words, a link relationship between an Azure AD user and the related user in Teamphoria needs to be established.</span></span>

<span data-ttu-id="ff357-141">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="ff357-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Teamphoria.</span></span>

<span data-ttu-id="ff357-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Teamphoria, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="ff357-142">To configure and test Azure AD single sign-on with Teamphoria, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ff357-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="ff357-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ff357-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="ff357-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ff357-145">**[Tworzenie użytkownika testowego Teamphoria](#creating-a-teamphoria-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Teamphoria połączonego z jej reprezentacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ff357-145">**[Creating a Teamphoria test user](#creating-a-teamphoria-test-user)** - to have a counterpart of Britta Simon in Teamphoria that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="ff357-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ff357-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ff357-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="ff357-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ff357-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ff357-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ff357-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu zarządzania Azure i skonfigurować logowanie jednokrotne w aplikacji Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="ff357-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Teamphoria application.</span></span>

<span data-ttu-id="ff357-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Teamphoria, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="ff357-150">**To configure Azure AD single sign-on with Teamphoria, perform the following steps:**</span></span>

1. <span data-ttu-id="ff357-151">W portalu zarządzania Azure na **Teamphoria** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="ff357-151">In the Azure Management portal, on the **Teamphoria** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="ff357-153">Na **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** Włącz funkcji logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="ff357-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_samlbase.png)

3. <span data-ttu-id="ff357-155">Na **Teamphoria domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ff357-155">On the **Teamphoria Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_url.png)

    <span data-ttu-id="ff357-157">a.</span><span class="sxs-lookup"><span data-stu-id="ff357-157">a.</span></span> <span data-ttu-id="ff357-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<sub-domain>.teamphoria.com/login`</span><span class="sxs-lookup"><span data-stu-id="ff357-158">In the **Sign-on URL** textbox, type the URL using the following pattern: `https://<sub-domain>.teamphoria.com/login`</span></span>    

    > [!NOTE] 
    > <span data-ttu-id="ff357-159">Należy pamiętać, że nie są one rzeczywiste wartości.</span><span class="sxs-lookup"><span data-stu-id="ff357-159">Please note that these are not the real values.</span></span> <span data-ttu-id="ff357-160">Należy zaktualizować te wartości z adresem URL logowania rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="ff357-160">You have to update these values with the actual Sign-On URL.</span></span> <span data-ttu-id="ff357-161">Skontaktuj się z [zespołem pomocy technicznej klienta Teamphoria](https://www.teamphoria.com/) Aby uzyskać adres URL logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="ff357-161">Contact [Teamphoria Client support team](https://www.teamphoria.com/) to get the Sign-on URL.</span></span> 

4. <span data-ttu-id="ff357-162">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie Zapisz certyfikat na komputerze.</span><span class="sxs-lookup"><span data-stu-id="ff357-162">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_certificate.png) 

5. <span data-ttu-id="ff357-164">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ff357-164">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-teamphoria-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ff357-166">Na **konfiguracji Teamphoria** , kliknij przycisk **skonfigurować Teamphoria** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="ff357-166">On the **Teamphoria Configuration** section, click **Configure Teamphoria** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ff357-167">Kopiuj **SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="ff357-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_configure.png) 

7. <span data-ttu-id="ff357-169">Aby skonfigurować logowanie jednokrotne w **Teamphoria** strony logowania do aplikacji Teamphoria jako administrator.</span><span class="sxs-lookup"><span data-stu-id="ff357-169">To configure single sign-on on **Teamphoria** side, Login to your Teamphoria application as an administrator.</span></span>

8. <span data-ttu-id="ff357-170">Przejdź do **ustawienia administratora** opcji na lewym pasku narzędzi i w obszarze kliknij kartę skonfigurować **POJEDYNCZEGO logowania** otworzyć okno konfiguracji logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="ff357-170">Go to **ADMIN SETTINGS** option in the left toolbar and under the the Configure Tab click on **SINGLE SIGN-ON** to open the SSO configuration window.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-teamphoria-tutorial/admin_sso_configure.png)

9. <span data-ttu-id="ff357-172">Polecenie **Dodaj nowego DOSTAWCĘ tożsamości** opcję w prawym górnym rogu, aby otworzyć formularz dodawania ustawienia logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="ff357-172">Click on **ADD NEW IDENTITY PROVIDER** option in the top right corner to open the form for adding the settings for SSO.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-teamphoria-tutorial/add_new_identity_provider.png)

10. <span data-ttu-id="ff357-174">Wprowadź dane w polach zgodnie z opisem poniżej-</span><span class="sxs-lookup"><span data-stu-id="ff357-174">Enter the details in the fields as described below-</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-teamphoria-tutorial/Teamphoria_sso_save.png)

    <span data-ttu-id="ff357-176">a.</span><span class="sxs-lookup"><span data-stu-id="ff357-176">a.</span></span> <span data-ttu-id="ff357-177">**Nazwa WYŚWIETLANA** : Wprowadź nazwę wyświetlaną wtyczki na stronie Administracja.</span><span class="sxs-lookup"><span data-stu-id="ff357-177">**DISPLAY NAME** : Enter the display name of the plugin on the admin page.</span></span>

    <span data-ttu-id="ff357-178">b.</span><span class="sxs-lookup"><span data-stu-id="ff357-178">b.</span></span> <span data-ttu-id="ff357-179">**Nazwa przycisku** : Nazwa kartę, która będzie wyświetlana na stronie logowania dla logowania za pośrednictwem rejestracji Jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ff357-179">**BUTTON NAME** : The name of the tab which will display on the login page for logging in via SSO.</span></span>

    <span data-ttu-id="ff357-180">c.</span><span class="sxs-lookup"><span data-stu-id="ff357-180">c.</span></span> <span data-ttu-id="ff357-181">**CERTYFIKAT** : Otwórz certyfikat wcześniej pobrany z portalu Azure w programie Notatnik, skopiuj zawartość tego samego i wklej go w tym miejscu w polu.</span><span class="sxs-lookup"><span data-stu-id="ff357-181">**CERTIFICATE** : Open the Certificate downloaded earlier from the Azure portal in notepad, copy the contents of the same and paste it here in the box.</span></span>

    <span data-ttu-id="ff357-182">d.</span><span class="sxs-lookup"><span data-stu-id="ff357-182">d.</span></span> <span data-ttu-id="ff357-183">**PUNKT wejścia** : Wklej **SAML pojedynczy znak na adres URL usługi** skopiowane wcześniej formularza portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ff357-183">**ENTRY POINT** : Paste the **SAML Single Sign-On Service URL** copied earlier form the Azure portal.</span></span>

    <span data-ttu-id="ff357-184">e.</span><span class="sxs-lookup"><span data-stu-id="ff357-184">e.</span></span> <span data-ttu-id="ff357-185">Przełącz opcję **ON** i wybierz polecenie **ZAPISAĆ**.</span><span class="sxs-lookup"><span data-stu-id="ff357-185">Switch the option to **ON** and click on **SAVE**.</span></span>   

<!--### Next steps

To ensure users can sign-in to Teamphoria after it has been configured to use Azure Active Directory, review the following tasks and topics:

- User accounts must be pre-provisioned into Teamphoria prior to sign-in. To set this up, see Provisioning.
 
- Users must be assigned access to Teamphoria in Azure AD to sign-in. To assign users, see Users.
 
- To configure access polices for Teamphoria users, see Access Policies.
 
- For additional information on deploying single sign-on to users, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ff357-186">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ff357-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="ff357-187">Celem tej sekcji jest tworzenie użytkownika testowego w portalu zarządzania Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="ff357-187">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="ff357-189">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="ff357-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ff357-190">W **portalu zarządzania Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ff357-190">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ff357-192">Przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** do wyświetlenia na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="ff357-192">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ff357-194">W górnej części okna dialogowego kliknij **Dodaj** otworzyć **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ff357-194">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ff357-196">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ff357-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ff357-198">a.</span><span class="sxs-lookup"><span data-stu-id="ff357-198">a.</span></span> <span data-ttu-id="ff357-199">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ff357-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ff357-200">b.</span><span class="sxs-lookup"><span data-stu-id="ff357-200">b.</span></span> <span data-ttu-id="ff357-201">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ff357-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ff357-202">c.</span><span class="sxs-lookup"><span data-stu-id="ff357-202">c.</span></span> <span data-ttu-id="ff357-203">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="ff357-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ff357-204">d.</span><span class="sxs-lookup"><span data-stu-id="ff357-204">d.</span></span> <span data-ttu-id="ff357-205">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="ff357-205">Click **Create**.</span></span>
 
### <a name="creating-a-teamphoria-test-user"></a><span data-ttu-id="ff357-206">Tworzenie użytkownika testowego Teamphoria</span><span class="sxs-lookup"><span data-stu-id="ff357-206">Creating a Teamphoria test user</span></span>

<span data-ttu-id="ff357-207">Aby włączyć użytkowników usługi Azure AD zalogować się do Teamphoria, musi być przygotowana do Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="ff357-207">In order to enable Azure AD users to log into Teamphoria, they must be provisioned into Teamphoria.</span></span> <span data-ttu-id="ff357-208">W przypadku Teamphoria Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="ff357-208">In the case of Teamphoria, provisioning is a manual task.</span></span>

<span data-ttu-id="ff357-209">**Aby udostępnić konta użytkowników, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="ff357-209">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="ff357-210">Zaloguj się do witryny firmy Teamphoria jako administrator.</span><span class="sxs-lookup"><span data-stu-id="ff357-210">Log in to your Teamphoria company site as an administrator.</span></span>

2. <span data-ttu-id="ff357-211">Polecenie **ADMIN** ustawień na lewym pasku narzędzi i w obszarze **ZARZĄDZAJ** karcie kliknij na **użytkowników** aby otworzyć stronę administratora dla użytkowników.</span><span class="sxs-lookup"><span data-stu-id="ff357-211">Click on **ADMIN** settings on the left toolbar and under the **MANAGE** tab Click on **USERS** to open the admin page for users.</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-teamphoria-tutorial/admin_manage_users.png)

3. <span data-ttu-id="ff357-213">Polecenie **ZAPROSIĆ RĘCZNEGO** opcji.</span><span class="sxs-lookup"><span data-stu-id="ff357-213">Click on the **MANUAL INVITE** option.</span></span>

    ![Zaproś inne osoby](./media/active-directory-saas-teamphoria-tutorial/admin_manage_add_users.png)  

4. <span data-ttu-id="ff357-215">Na tej stronie należy wykonać następujące działania.</span><span class="sxs-lookup"><span data-stu-id="ff357-215">On this page, perform following action.</span></span> 
    
    ![Zaproś inne osoby](./media/active-directory-saas-teamphoria-tutorial/manual_user_invite.png)  

    <span data-ttu-id="ff357-217">a.</span><span class="sxs-lookup"><span data-stu-id="ff357-217">a.</span></span> <span data-ttu-id="ff357-218">W **adres E-mail** pole tekstowe, **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ff357-218">In the **EMAIL ADDRESS** textbox, the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ff357-219">b.</span><span class="sxs-lookup"><span data-stu-id="ff357-219">b.</span></span> <span data-ttu-id="ff357-220">W **imię** pole tekstowe, typ **Britta**.</span><span class="sxs-lookup"><span data-stu-id="ff357-220">In the **FIRST NAME** textbox, type **Britta**.</span></span>

    <span data-ttu-id="ff357-221">c.</span><span class="sxs-lookup"><span data-stu-id="ff357-221">c.</span></span> <span data-ttu-id="ff357-222">W **nazwisko** pole tekstowe, typ **Simona**.</span><span class="sxs-lookup"><span data-stu-id="ff357-222">In the **LAST NAME** textbox, type **Simon**.</span></span>

    <span data-ttu-id="ff357-223">d.</span><span class="sxs-lookup"><span data-stu-id="ff357-223">d.</span></span> <span data-ttu-id="ff357-224">Kliknij przycisk **użytkownika zaproszenia 1**.</span><span class="sxs-lookup"><span data-stu-id="ff357-224">Click **INVITE 1 USER**.</span></span> <span data-ttu-id="ff357-225">Użytkownik musi zaakceptować zaproszenie tworzone w systemie.</span><span class="sxs-lookup"><span data-stu-id="ff357-225">User needs to accept the invite to get created in the system.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ff357-226">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ff357-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ff357-227">W tej sekcji można włączyć Simona Britta do udostępnienia jej Teamphoria za pomocą usługi Azure rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ff357-227">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Teamphoria.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="ff357-229">**Aby przypisać Simona Britta Teamphoria, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="ff357-229">**To assign Britta Simon to Teamphoria, perform the following steps:**</span></span>

1. <span data-ttu-id="ff357-230">Otwórz widok aplikacji w portalu zarządzania Azure, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ff357-230">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="ff357-232">Na liście aplikacji zaznacz **Teamphoria**.</span><span class="sxs-lookup"><span data-stu-id="ff357-232">In the applications list, select **Teamphoria**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_app.png) 

3. <span data-ttu-id="ff357-234">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="ff357-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="ff357-236">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ff357-236">Click **Add** button.</span></span> <span data-ttu-id="ff357-237">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ff357-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="ff357-239">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="ff357-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ff357-240">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ff357-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ff357-241">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ff357-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ff357-242">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ff357-242">Testing single sign-on</span></span>

<span data-ttu-id="ff357-243">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="ff357-243">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ff357-244">Jeśli chcesz przetestować jednego ustawienia logowania jednokrotnego, otwórz Panel dostępu.</span><span class="sxs-lookup"><span data-stu-id="ff357-244">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="ff357-245">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="ff357-245">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ff357-246">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="ff357-246">Additional resources</span></span>

* [<span data-ttu-id="ff357-247">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ff357-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ff357-248">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ff357-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_203.png

