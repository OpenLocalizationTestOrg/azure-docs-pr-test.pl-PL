---
title: 'Samouczek: Integracji Azure Active Directory z xMatters OnDemand | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i xMatters na żądanie."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ca0633db-4f95-432e-b3db-0168193b5ce9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 9bfcb44ed19f167872b3cd9119e2dbdd35c82604
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-xmatters-ondemand"></a><span data-ttu-id="b70e0-103">Samouczek: Integracji Azure Active Directory z xMatters na żądanie</span><span class="sxs-lookup"><span data-stu-id="b70e0-103">Tutorial: Azure Active Directory integration with xMatters OnDemand</span></span>

<span data-ttu-id="b70e0-104">Z tego samouczka dowiesz się integrowanie xMatters OnDemand w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b70e0-104">In this tutorial, you learn how to integrate xMatters OnDemand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b70e0-105">Integrowanie xMatters na żądanie z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="b70e0-105">Integrating xMatters OnDemand with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b70e0-106">Można kontrolować w usłudze Azure AD, który ma dostęp do xMatters na żądanie</span><span class="sxs-lookup"><span data-stu-id="b70e0-106">You can control in Azure AD who has access to xMatters OnDemand</span></span>
- <span data-ttu-id="b70e0-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do xMatters OnDemand (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b70e0-107">You can enable your users to automatically get signed-on to xMatters OnDemand (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b70e0-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="b70e0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b70e0-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b70e0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b70e0-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b70e0-110">Prerequisites</span></span>

<span data-ttu-id="b70e0-111">Aby skonfigurować integrację usługi Azure AD z xMatters na żądanie, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="b70e0-111">To configure Azure AD integration with xMatters OnDemand, you need the following items:</span></span>

- <span data-ttu-id="b70e0-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b70e0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b70e0-113">XMatters OnDemand logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="b70e0-113">A xMatters OnDemand single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b70e0-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="b70e0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b70e0-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="b70e0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b70e0-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="b70e0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b70e0-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b70e0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b70e0-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="b70e0-118">Scenario description</span></span>
<span data-ttu-id="b70e0-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="b70e0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b70e0-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="b70e0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b70e0-121">Dodawanie xMatters na żądanie z galerii</span><span class="sxs-lookup"><span data-stu-id="b70e0-121">Adding xMatters OnDemand from the gallery</span></span>
2. <span data-ttu-id="b70e0-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="b70e0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-xmatters-ondemand-from-the-gallery"></a><span data-ttu-id="b70e0-123">Dodawanie xMatters na żądanie z galerii</span><span class="sxs-lookup"><span data-stu-id="b70e0-123">Adding xMatters OnDemand from the gallery</span></span>
<span data-ttu-id="b70e0-124">Aby skonfigurować integrację usługi Azure AD xMatters na żądanie, należy dodać xMatters na żądanie z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="b70e0-124">To configure the integration of xMatters OnDemand into Azure AD, you need to add xMatters OnDemand from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b70e0-125">**Aby dodać xMatters na żądanie z poziomu galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="b70e0-125">**To add xMatters OnDemand from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b70e0-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="b70e0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="b70e0-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="b70e0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b70e0-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="b70e0-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="b70e0-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b70e0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="b70e0-133">W polu wyszukiwania wpisz **xMatters OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="b70e0-133">In the search box, type **xMatters OnDemand**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_search.png)

5. <span data-ttu-id="b70e0-135">W panelu wyników wybierz **xMatters OnDemand**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="b70e0-135">In the results panel, select **xMatters OnDemand**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b70e0-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="b70e0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b70e0-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z xMatters OnDemand oparta na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="b70e0-138">In this section, you configure and test Azure AD single sign-on with xMatters OnDemand based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b70e0-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, jaki użytkownik odpowiednikiem w xMatters OnDemand jest użytkownikiem w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b70e0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in xMatters OnDemand is to a user in Azure AD.</span></span> <span data-ttu-id="b70e0-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w xMatters OnDemand musi się.</span><span class="sxs-lookup"><span data-stu-id="b70e0-140">In other words, a link relationship between an Azure AD user and the related user in xMatters OnDemand needs to be established.</span></span>

<span data-ttu-id="b70e0-141">W xMatters na żądanie, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="b70e0-141">In xMatters OnDemand, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b70e0-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z xMatters na żądanie, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="b70e0-142">To configure and test Azure AD single sign-on with xMatters OnDemand, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b70e0-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="b70e0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b70e0-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="b70e0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b70e0-145">**[Tworzenie użytkownika testowego OnDemand xMatters](#creating-a-xmatters-ondemand-test-user)**  — mają odpowiednika Simona Britta w xMatters OnDemand połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b70e0-145">**[Creating a xMatters OnDemand test user](#creating-a-xmatters-ondemand-test-user)** - to have a counterpart of Britta Simon in xMatters OnDemand that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b70e0-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="b70e0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b70e0-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="b70e0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b70e0-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="b70e0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b70e0-149">W tej sekcji włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w sieci xMatters aplikacji na żądanie.</span><span class="sxs-lookup"><span data-stu-id="b70e0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your xMatters OnDemand application.</span></span>

<span data-ttu-id="b70e0-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z xMatters na żądanie, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="b70e0-150">**To configure Azure AD single sign-on with xMatters OnDemand, perform the following steps:**</span></span>

1. <span data-ttu-id="b70e0-151">W portalu Azure na **xMatters OnDemand** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="b70e0-151">In the Azure portal, on the **xMatters OnDemand** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="b70e0-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="b70e0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_samlbase.png)

3. <span data-ttu-id="b70e0-155">Na **xMatters OnDemand domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b70e0-155">On the **xMatters OnDemand Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_url.png)
    
    <span data-ttu-id="b70e0-157">a.</span><span class="sxs-lookup"><span data-stu-id="b70e0-157">a.</span></span> <span data-ttu-id="b70e0-158">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="b70e0-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>   
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au/`|
    | `https://<companyname>.cs1.xmatters.com/`|
    | `https://<companyname>.xmatters.com/`|
    | `https://www.xmatters.com`|
    | `https://<companyname>.xmatters.com.au/`|

    <span data-ttu-id="b70e0-159">b.</span><span class="sxs-lookup"><span data-stu-id="b70e0-159">b.</span></span> <span data-ttu-id="b70e0-160">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="b70e0-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au`|
    | `https://<companyname>.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.cs1.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.au1.xmatters.com.au/<instancename>`|

    > [!NOTE] 
    > <span data-ttu-id="b70e0-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="b70e0-161">These values are not real.</span></span> <span data-ttu-id="b70e0-162">Rzeczywisty identyfikator i adres URL odpowiedzi, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="b70e0-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="b70e0-163">Skontaktuj się z [xMatters OnDemand obsługuje zespołu](https://www.xmatters.com/company/contact-us/) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="b70e0-163">Contact [xMatters OnDemand support team](https://www.xmatters.com/company/contact-us/) to get these values.</span></span>

4. <span data-ttu-id="b70e0-164">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu lokalnie jako **c:\\XMatters OnDemand.cer**.</span><span class="sxs-lookup"><span data-stu-id="b70e0-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file locally as **c:\\XMatters OnDemand.cer**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_certificate.png)
    
    > [!IMPORTANT]
    > <span data-ttu-id="b70e0-166">Konieczne przekazywanie certyfikatu [xMatters OnDemand obsługuje zespołu](https://www.xmatters.com/company/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="b70e0-166">You need to forward the certificate to the [xMatters OnDemand support team](https://www.xmatters.com/company/contact-us/).</span></span> <span data-ttu-id="b70e0-167">Ten certyfikat musi się do przekazania przez zespół pomocy technicznej xMatters przed może zakończyć pojedynczego konfigurację logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="b70e0-167">The certificate needs to be uploaded by the xMatters support team before you can finalize the single sign-on configuration.</span></span> 

5. <span data-ttu-id="b70e0-168">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b70e0-168">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b70e0-170">Na **xMatters konfiguracji OnDemand** , kliknij przycisk **skonfigurować xMatters OnDemand** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="b70e0-170">On the **xMatters OnDemand Configuration** section, click **Configure xMatters OnDemand** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b70e0-171">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="b70e0-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_configure.png) 

7. <span data-ttu-id="b70e0-173">W oknie przeglądarki innej witryny sieci web należy zalogować się jako administrator do witryny firmy XMatters OnDemand.</span><span class="sxs-lookup"><span data-stu-id="b70e0-173">In a different web browser window, log in to your XMatters OnDemand company site as an administrator.</span></span>

8. <span data-ttu-id="b70e0-174">Na pasku narzędzi u góry kliknij **Admin**, a następnie kliknij przycisk **szczegóły firmy** na pasku nawigacyjnym po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="b70e0-174">In the toolbar on the top, click **Admin**, and then click **Company Details** in the navigation bar on the left side.</span></span>
   
    <span data-ttu-id="b70e0-175">![Administrator](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776795.png "administratora")</span><span class="sxs-lookup"><span data-stu-id="b70e0-175">![Admin](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776795.png "Admin")</span></span>

9. <span data-ttu-id="b70e0-176">Na **Konfiguracja SAML** wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b70e0-176">On the **SAML Configuration** page, perform the following steps:</span></span>
   
    <span data-ttu-id="b70e0-177">![Konfiguracja SAML](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776796.png "Konfiguracja SAML")</span><span class="sxs-lookup"><span data-stu-id="b70e0-177">![SAML configuration](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776796.png "SAML configuration")</span></span>
   
    <span data-ttu-id="b70e0-178">a.</span><span class="sxs-lookup"><span data-stu-id="b70e0-178">a.</span></span> <span data-ttu-id="b70e0-179">Wybierz **Włącz SAML**.</span><span class="sxs-lookup"><span data-stu-id="b70e0-179">Select **Enable SAML**.</span></span>
   
    <span data-ttu-id="b70e0-180">b.</span><span class="sxs-lookup"><span data-stu-id="b70e0-180">b.</span></span> <span data-ttu-id="b70e0-181">Wklej **identyfikator jednostki SAML**, które zostały skopiowane z portalu Azure do **identyfikator dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="b70e0-181">Paste **SAML Entity ID**, which you have copied from the Azure portal into the **Identity Provider ID** textbox.</span></span>
   
    <span data-ttu-id="b70e0-182">c.</span><span class="sxs-lookup"><span data-stu-id="b70e0-182">c.</span></span> <span data-ttu-id="b70e0-183">Wklej **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure do **jeden znak na adres URL** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="b70e0-183">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **Single Sign On URL** textbox.</span></span>
   
    <span data-ttu-id="b70e0-184">d.</span><span class="sxs-lookup"><span data-stu-id="b70e0-184">d.</span></span> <span data-ttu-id="b70e0-185">Wklej **Sign-Out URL**, które zostały skopiowane z portalu Azure do **pojedynczego adresu URL wylogowania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="b70e0-185">Paste **Sign-Out URL**, which you have copied from the Azure portal into the **Single Logout URL** textbox.</span></span>
   
    <span data-ttu-id="b70e0-186">e.</span><span class="sxs-lookup"><span data-stu-id="b70e0-186">e.</span></span> <span data-ttu-id="b70e0-187">Na stronie Szczegóły firmy u góry, kliknij przycisk **Zapisz zmiany**.</span><span class="sxs-lookup"><span data-stu-id="b70e0-187">On the Company Details page, at the top, click **Save Changes**.</span></span>
    
    <span data-ttu-id="b70e0-188">![Szczegóły firmy](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776797.png "firmy szczegóły")</span><span class="sxs-lookup"><span data-stu-id="b70e0-188">![Company details](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776797.png "Company details")</span></span>

> [!TIP]
> <span data-ttu-id="b70e0-189">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="b70e0-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b70e0-190">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="b70e0-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b70e0-191">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b70e0-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b70e0-192">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b70e0-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="b70e0-193">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="b70e0-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="b70e0-195">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="b70e0-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b70e0-196">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="b70e0-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b70e0-198">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="b70e0-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b70e0-200">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b70e0-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b70e0-202">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b70e0-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b70e0-204">a.</span><span class="sxs-lookup"><span data-stu-id="b70e0-204">a.</span></span> <span data-ttu-id="b70e0-205">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b70e0-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b70e0-206">b.</span><span class="sxs-lookup"><span data-stu-id="b70e0-206">b.</span></span> <span data-ttu-id="b70e0-207">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b70e0-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b70e0-208">c.</span><span class="sxs-lookup"><span data-stu-id="b70e0-208">c.</span></span> <span data-ttu-id="b70e0-209">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="b70e0-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b70e0-210">d.</span><span class="sxs-lookup"><span data-stu-id="b70e0-210">d.</span></span> <span data-ttu-id="b70e0-211">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="b70e0-211">Click **Create**.</span></span>
 
### <a name="creating-a-xmatters-ondemand-test-user"></a><span data-ttu-id="b70e0-212">Tworzenie użytkownika testowego OnDemand xMatters</span><span class="sxs-lookup"><span data-stu-id="b70e0-212">Creating a xMatters OnDemand test user</span></span>

<span data-ttu-id="b70e0-213">Aby umożliwić użytkownikom zalogować się do atrybutu XMatters usługi Azure AD, muszą mieć przydzielone do XMatters OnDemand.</span><span class="sxs-lookup"><span data-stu-id="b70e0-213">In order to enable Azure AD users to log in to XMatters OnDemand, they must be provisioned into XMatters OnDemand.</span></span> <span data-ttu-id="b70e0-214">W przypadku XMatters OnDemand Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="b70e0-214">In the case of XMatters OnDemand, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-accounts-perform-the-following-steps"></a><span data-ttu-id="b70e0-215">Aby udostępnić konta użytkowników, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b70e0-215">To provision a user accounts, perform the following steps:</span></span>
1. <span data-ttu-id="b70e0-216">Zaloguj się do Twojego **XMatters OnDemand** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="b70e0-216">Log in to your **XMatters OnDemand** tenant.</span></span>

2.  <span data-ttu-id="b70e0-217">Kliknij przycisk **użytkowników** kartę.</span><span class="sxs-lookup"><span data-stu-id="b70e0-217">Click **Users** tab.</span></span> <span data-ttu-id="b70e0-218">a następnie kliknij przycisk **Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="b70e0-218">and then click **Add User**.</span></span>
  
    <span data-ttu-id="b70e0-219">![Użytkownicy](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781048.png "użytkowników")</span><span class="sxs-lookup"><span data-stu-id="b70e0-219">![Users](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781048.png "Users")</span></span>

3. <span data-ttu-id="b70e0-220">W **dodać użytkownika** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b70e0-220">In the **Add a User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="b70e0-221">![Dodawanie użytkownika](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781049.png "Dodawanie użytkownika")</span><span class="sxs-lookup"><span data-stu-id="b70e0-221">![Add a User](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781049.png "Add a User")</span></span>

    <span data-ttu-id="b70e0-222">a.</span><span class="sxs-lookup"><span data-stu-id="b70e0-222">a.</span></span> <span data-ttu-id="b70e0-223">Wybierz **Active**.</span><span class="sxs-lookup"><span data-stu-id="b70e0-223">Select **Active**.</span></span>

    <span data-ttu-id="b70e0-224">b.</span><span class="sxs-lookup"><span data-stu-id="b70e0-224">b.</span></span> <span data-ttu-id="b70e0-225">W **identyfikator użytkownika** pole tekstowe, typ identyfikatora użytkownika użytkownika, takich jak Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="b70e0-225">In the **User ID** textbox, type the user id of user like Brittasimon@contoso.com.</span></span>
   
    <span data-ttu-id="b70e0-226">c.</span><span class="sxs-lookup"><span data-stu-id="b70e0-226">c.</span></span> <span data-ttu-id="b70e0-227">W **imię** tekstowym, wpisz imię użytkownika, takich jak Britta.</span><span class="sxs-lookup"><span data-stu-id="b70e0-227">In the **First Name** textbox, type first name of the user like Britta.</span></span>

    <span data-ttu-id="b70e0-228">d.</span><span class="sxs-lookup"><span data-stu-id="b70e0-228">d.</span></span> <span data-ttu-id="b70e0-229">W **nazwisko** tekstowym, wpisz nazwisko użytkownika, takich jak Simona.</span><span class="sxs-lookup"><span data-stu-id="b70e0-229">In the **Last Name** textbox, type last name of the user like Simon.</span></span>
    
    <span data-ttu-id="b70e0-230">e.</span><span class="sxs-lookup"><span data-stu-id="b70e0-230">e.</span></span> <span data-ttu-id="b70e0-231">W **lokacji** pole tekstowe, wprowadź prawidłową witryną Azure prawidłowe konto AD, które chcesz udostępnić.</span><span class="sxs-lookup"><span data-stu-id="b70e0-231">In the **Site** textbox, Enter the valid site of a valid Azure AD account you want to provision.</span></span>
    
    <span data-ttu-id="b70e0-232">f.</span><span class="sxs-lookup"><span data-stu-id="b70e0-232">f.</span></span> <span data-ttu-id="b70e0-233">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="b70e0-233">Click **Save**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b70e0-234">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b70e0-234">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b70e0-235">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do xMatters OnDemand.</span><span class="sxs-lookup"><span data-stu-id="b70e0-235">In this section, you enable Britta Simon to use Azure single sign-on by granting access to xMatters OnDemand.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="b70e0-237">**Aby przypisać Simona Britta xMatters na żądanie, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="b70e0-237">**To assign Britta Simon to xMatters OnDemand, perform the following steps:**</span></span>

1. <span data-ttu-id="b70e0-238">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="b70e0-238">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="b70e0-240">Na liście aplikacji zaznacz **xMatters OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="b70e0-240">In the applications list, select **xMatters OnDemand**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_app.png) 

3. <span data-ttu-id="b70e0-242">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="b70e0-242">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="b70e0-244">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b70e0-244">Click **Add** button.</span></span> <span data-ttu-id="b70e0-245">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b70e0-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="b70e0-247">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="b70e0-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b70e0-248">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b70e0-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b70e0-249">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b70e0-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b70e0-250">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="b70e0-250">Testing single sign-on</span></span>

<span data-ttu-id="b70e0-251">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="b70e0-251">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b70e0-252">Po kliknięciu xMatters kafelka na żądanie w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do Twojej aplikacji OnDemand xMatters.</span><span class="sxs-lookup"><span data-stu-id="b70e0-252">When you click the xMatters OnDemand tile in the Access Panel, you should get automatically signed-on to your xMatters OnDemand application.</span></span>
<span data-ttu-id="b70e0-253">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b70e0-253">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b70e0-254">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="b70e0-254">Additional resources</span></span>

* [<span data-ttu-id="b70e0-255">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b70e0-255">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b70e0-256">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b70e0-256">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_203.png

