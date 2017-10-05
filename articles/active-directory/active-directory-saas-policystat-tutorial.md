---
title: 'Samouczek: Integracji Azure Active Directory z PolicyStat | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i PolicyStat."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: af5eb0f1-1c8e-4809-b0c4-8ccfb915ca42
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 704afd5515b02ce2a4fbf35da65fad74dc506271
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-policystat"></a><span data-ttu-id="44fb0-103">Samouczek: Integracji Azure Active Directory z PolicyStat</span><span class="sxs-lookup"><span data-stu-id="44fb0-103">Tutorial: Azure Active Directory integration with PolicyStat</span></span>

<span data-ttu-id="44fb0-104">Z tego samouczka dowiesz się integrowanie PolicyStat z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="44fb0-104">In this tutorial, you learn how to integrate PolicyStat with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="44fb0-105">Integracja z usługą Azure AD PolicyStat zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="44fb0-105">Integrating PolicyStat with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="44fb0-106">Można kontrolować w usłudze Azure AD, który ma dostęp do PolicyStat</span><span class="sxs-lookup"><span data-stu-id="44fb0-106">You can control in Azure AD who has access to PolicyStat</span></span>
- <span data-ttu-id="44fb0-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do PolicyStat (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="44fb0-107">You can enable your users to automatically get signed-on to PolicyStat (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="44fb0-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="44fb0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="44fb0-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="44fb0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44fb0-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="44fb0-110">Prerequisites</span></span>

<span data-ttu-id="44fb0-111">Aby skonfigurować integrację usługi Azure AD z PolicyStat, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="44fb0-111">To configure Azure AD integration with PolicyStat, you need the following items:</span></span>

- <span data-ttu-id="44fb0-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="44fb0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="44fb0-113">PolicyStat logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="44fb0-113">A PolicyStat single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="44fb0-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="44fb0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="44fb0-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="44fb0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="44fb0-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="44fb0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="44fb0-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="44fb0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="44fb0-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="44fb0-118">Scenario description</span></span>
<span data-ttu-id="44fb0-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="44fb0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="44fb0-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="44fb0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="44fb0-121">Dodawanie PolicyStat z galerii</span><span class="sxs-lookup"><span data-stu-id="44fb0-121">Adding PolicyStat from the gallery</span></span>
2. <span data-ttu-id="44fb0-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="44fb0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-policystat-from-the-gallery"></a><span data-ttu-id="44fb0-123">Dodawanie PolicyStat z galerii</span><span class="sxs-lookup"><span data-stu-id="44fb0-123">Adding PolicyStat from the gallery</span></span>
<span data-ttu-id="44fb0-124">Aby skonfigurować integrację usługi Azure AD PolicyStat, należy dodać PolicyStat z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="44fb0-124">To configure the integration of PolicyStat into Azure AD, you need to add PolicyStat from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="44fb0-125">**Aby dodać PolicyStat z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="44fb0-125">**To add PolicyStat from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="44fb0-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="44fb0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="44fb0-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="44fb0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="44fb0-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="44fb0-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="44fb0-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="44fb0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="44fb0-133">W polu wyszukiwania wpisz **PolicyStat**.</span><span class="sxs-lookup"><span data-stu-id="44fb0-133">In the search box, type **PolicyStat**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_search.png)

5. <span data-ttu-id="44fb0-135">W panelu wyników wybierz **PolicyStat**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="44fb0-135">In the results panel, select **PolicyStat**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="44fb0-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="44fb0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="44fb0-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z PolicyStat w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="44fb0-138">In this section, you configure and test Azure AD single sign-on with PolicyStat based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="44fb0-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w PolicyStat jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="44fb0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in PolicyStat is to a user in Azure AD.</span></span> <span data-ttu-id="44fb0-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w PolicyStat musi się.</span><span class="sxs-lookup"><span data-stu-id="44fb0-140">In other words, a link relationship between an Azure AD user and the related user in PolicyStat needs to be established.</span></span>

<span data-ttu-id="44fb0-141">W PolicyStat, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="44fb0-141">In PolicyStat, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="44fb0-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z PolicyStat, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="44fb0-142">To configure and test Azure AD single sign-on with PolicyStat, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="44fb0-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="44fb0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="44fb0-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="44fb0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="44fb0-145">**[Tworzenie użytkownika testowego PolicyStat](#creating-a-policystat-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta PolicyStat połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="44fb0-145">**[Creating a PolicyStat test user](#creating-a-policystat-test-user)** - to have a counterpart of Britta Simon in PolicyStat that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="44fb0-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="44fb0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="44fb0-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="44fb0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="44fb0-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="44fb0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="44fb0-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="44fb0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your PolicyStat application.</span></span>

<span data-ttu-id="44fb0-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z PolicyStat, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="44fb0-150">**To configure Azure AD single sign-on with PolicyStat, perform the following steps:**</span></span>

1. <span data-ttu-id="44fb0-151">W portalu Azure na **PolicyStat** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="44fb0-151">In the Azure portal, on the **PolicyStat** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="44fb0-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="44fb0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_samlbase.png)

3. <span data-ttu-id="44fb0-155">Na **PolicyStat domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="44fb0-155">On the **PolicyStat Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_url.png)

    <span data-ttu-id="44fb0-157">a.</span><span class="sxs-lookup"><span data-stu-id="44fb0-157">a.</span></span> <span data-ttu-id="44fb0-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.policystat.com`</span><span class="sxs-lookup"><span data-stu-id="44fb0-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.policystat.com`</span></span>

    <span data-ttu-id="44fb0-159">b.</span><span class="sxs-lookup"><span data-stu-id="44fb0-159">b.</span></span> <span data-ttu-id="44fb0-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.policystat.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="44fb0-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.policystat.com/saml2/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="44fb0-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="44fb0-161">These values are not real.</span></span> <span data-ttu-id="44fb0-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="44fb0-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="44fb0-163">Skontaktuj się z [zespołem pomocy technicznej klienta PolicyStat](http://www.policystat.com/support/) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="44fb0-163">Contact [PolicyStat Client support team](http://www.policystat.com/support/) to get these values.</span></span> 
 
4. <span data-ttu-id="44fb0-164">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="44fb0-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_certificate.png) 

5. <span data-ttu-id="44fb0-166">Celem tej sekcji jest przedstawiają sposób umożliwić użytkownikom uwierzytelnianie na PolicyStat do swojego konta w usłudze Azure AD przy użyciu federacyjnego na podstawie protokołu SAML.</span><span class="sxs-lookup"><span data-stu-id="44fb0-166">The objective of this section is to outline how to enable users to authenticate to PolicyStat with their account in Azure AD using federation based on the SAML protocol.</span></span>

    <span data-ttu-id="44fb0-167">Aplikacja PolicyStat oczekuje potwierdzenia języka SAML w określonym formacie, musisz dodać mapowania atrybutu niestandardowego do Twojej **atrybuty tokenu SAML** konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="44fb0-167">The PolicyStat application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **SAML Token Attributes** configuration.</span></span>  

     <span data-ttu-id="44fb0-168">Poniższy zrzut ekranu przedstawia przykład.</span><span class="sxs-lookup"><span data-stu-id="44fb0-168">The following screenshot shows an example of this.</span></span>

     <span data-ttu-id="44fb0-169">![Atrybuty](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_attribute.png "atrybutów")</span><span class="sxs-lookup"><span data-stu-id="44fb0-169">![Attributes](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_attribute.png "Attributes")</span></span>

6. <span data-ttu-id="44fb0-170">Aby dodać mapowania wymaganego atrybutu, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="44fb0-170">To add the required attribute mappings, perform the following steps:</span></span>

    | <span data-ttu-id="44fb0-171">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="44fb0-171">Attribute Name</span></span>    |   <span data-ttu-id="44fb0-172">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="44fb0-172">Attribute Value</span></span> |
    |------------------- | -------------------- |
    | <span data-ttu-id="44fb0-173">Identyfikator UID</span><span class="sxs-lookup"><span data-stu-id="44fb0-173">uid</span></span> | <span data-ttu-id="44fb0-174">ExtractMailPrefix([mail])</span><span class="sxs-lookup"><span data-stu-id="44fb0-174">ExtractMailPrefix([mail])</span></span> |
    
    <span data-ttu-id="44fb0-175">a.</span><span class="sxs-lookup"><span data-stu-id="44fb0-175">a.</span></span> <span data-ttu-id="44fb0-176">Kliknij przycisk **Dodaj atrybut** otworzyć **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="44fb0-176">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_04.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addatribute.png)
    
    <span data-ttu-id="44fb0-179">b.</span><span class="sxs-lookup"><span data-stu-id="44fb0-179">b.</span></span> <span data-ttu-id="44fb0-180">W **nazwa atrybutu** pole tekstowe, typ **uid**.</span><span class="sxs-lookup"><span data-stu-id="44fb0-180">In the **Attribute Name** textbox, type **uid**.</span></span>

    <span data-ttu-id="44fb0-181">c.</span><span class="sxs-lookup"><span data-stu-id="44fb0-181">c.</span></span> <span data-ttu-id="44fb0-182">W **wartość atrybutu** pole tekstowe, wybierz opcję **ExtractMailPrefix()**.</span><span class="sxs-lookup"><span data-stu-id="44fb0-182">In the **Attribute Value** textbox, select **ExtractMailPrefix()**.</span></span>    
   
    <span data-ttu-id="44fb0-183">d.</span><span class="sxs-lookup"><span data-stu-id="44fb0-183">d.</span></span> <span data-ttu-id="44fb0-184">Z **poczty** listy, wybierz **User.mail**.</span><span class="sxs-lookup"><span data-stu-id="44fb0-184">From the **Mail** list, select **User.mail**.</span></span>
    
    <span data-ttu-id="44fb0-185">e.</span><span class="sxs-lookup"><span data-stu-id="44fb0-185">e.</span></span> <span data-ttu-id="44fb0-186">Kliknij przycisk **Ok**</span><span class="sxs-lookup"><span data-stu-id="44fb0-186">Click **Ok**</span></span>

7. <span data-ttu-id="44fb0-187">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="44fb0-187">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-policystat-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="44fb0-189">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy PolicyStat jako administrator.</span><span class="sxs-lookup"><span data-stu-id="44fb0-189">In a different web browser window, log into your PolicyStat company site as an administrator.</span></span>

9. <span data-ttu-id="44fb0-190">Kliknij przycisk **Admin** , a następnie kliknij pozycję **konfiguracji rejestracji jednokrotnej** w lewym okienku nawigacji.</span><span class="sxs-lookup"><span data-stu-id="44fb0-190">Click the **Admin** tab, and then click **Single Sign-On Configuration** in left navigation pane.</span></span>
   
    <span data-ttu-id="44fb0-191">![Menu administratora](./media/active-directory-saas-policystat-tutorial/ic808633.png "Menu administratora")</span><span class="sxs-lookup"><span data-stu-id="44fb0-191">![Administrator Menu](./media/active-directory-saas-policystat-tutorial/ic808633.png "Administrator Menu")</span></span>

10. <span data-ttu-id="44fb0-192">W **Instalator** zaznacz **włączyć pojedynczego logowania jednokrotnego integracji**.</span><span class="sxs-lookup"><span data-stu-id="44fb0-192">In the **Setup** section, select **Enable Single Sign-on Integration**.</span></span>
   
    <span data-ttu-id="44fb0-193">![Pojedynczy konfiguracji logowania jednokrotnego](./media/active-directory-saas-policystat-tutorial/ic808634.png "pojedynczy konfiguracji logowania jednokrotnego")</span><span class="sxs-lookup"><span data-stu-id="44fb0-193">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808634.png "Single Sign-On Configuration")</span></span>

11. <span data-ttu-id="44fb0-194">Kliknij przycisk **Konfigurowanie atrybutów**, a następnie w **Konfigurowanie atrybutów** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="44fb0-194">Click **Configure Attributes**, and then, in the **Configure Attributes** section, perform the following steps:</span></span>
   
    <span data-ttu-id="44fb0-195">![Pojedynczy konfiguracji logowania jednokrotnego](./media/active-directory-saas-policystat-tutorial/ic808635.png "pojedynczy konfiguracji logowania jednokrotnego")</span><span class="sxs-lookup"><span data-stu-id="44fb0-195">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808635.png "Single Sign-On Configuration")</span></span>
   
    <span data-ttu-id="44fb0-196">a.</span><span class="sxs-lookup"><span data-stu-id="44fb0-196">a.</span></span> <span data-ttu-id="44fb0-197">W **atrybutu Username** pole tekstowe, typ **uid**.</span><span class="sxs-lookup"><span data-stu-id="44fb0-197">In the **Username Attribute** textbox, type **uid**.</span></span>

    <span data-ttu-id="44fb0-198">b.</span><span class="sxs-lookup"><span data-stu-id="44fb0-198">b.</span></span> <span data-ttu-id="44fb0-199">W **atrybutu imię** pole tekstowe, typ **imię** użytkownika **Britta**.</span><span class="sxs-lookup"><span data-stu-id="44fb0-199">In the **First Name Attribute** textbox, type **firstname** of user **Britta**.</span></span>

    <span data-ttu-id="44fb0-200">c.</span><span class="sxs-lookup"><span data-stu-id="44fb0-200">c.</span></span> <span data-ttu-id="44fb0-201">W **ostatniego atrybutu Name** pole tekstowe, typ **nazwisko** użytkownika **Simona**.</span><span class="sxs-lookup"><span data-stu-id="44fb0-201">In the **Last Name Attribute** textbox, type **lastname** of user **Simon**.</span></span>

    <span data-ttu-id="44fb0-202">d.</span><span class="sxs-lookup"><span data-stu-id="44fb0-202">d.</span></span> <span data-ttu-id="44fb0-203">W **atrybut poczty E-mail** pole tekstowe, typ **emailaddress** użytkownika  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="44fb0-203">In the **Email Attribute** textbox, type **emailaddress** of user **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="44fb0-204">e.</span><span class="sxs-lookup"><span data-stu-id="44fb0-204">e.</span></span> <span data-ttu-id="44fb0-205">Kliknij przycisk **zapisać zmiany**.</span><span class="sxs-lookup"><span data-stu-id="44fb0-205">Click **Save Changes**.</span></span>

12. <span data-ttu-id="44fb0-206">Kliknij przycisk **Your metadanych IDP**, a następnie w **Your metadanych IDP** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="44fb0-206">Click **Your IDP Metadata**, and then, in the **Your IDP Metadata** section, perform the following steps:</span></span>
   
    <span data-ttu-id="44fb0-207">![Pojedynczy konfiguracji logowania jednokrotnego](./media/active-directory-saas-policystat-tutorial/ic808636.png "pojedynczy konfiguracji logowania jednokrotnego")</span><span class="sxs-lookup"><span data-stu-id="44fb0-207">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808636.png "Single Sign-On Configuration")</span></span>
   
    <span data-ttu-id="44fb0-208">a.</span><span class="sxs-lookup"><span data-stu-id="44fb0-208">a.</span></span> <span data-ttu-id="44fb0-209">Otwórz plik metadanych pobranych, skopiuj zawartość, a następnie wklej go do **Your metadanych dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="44fb0-209">Open your downloaded metadata file, copy the content, and  then paste it into the **Your Identity Provider Metadata** textbox.</span></span>

    <span data-ttu-id="44fb0-210">b.</span><span class="sxs-lookup"><span data-stu-id="44fb0-210">b.</span></span> <span data-ttu-id="44fb0-211">Kliknij przycisk **zapisać zmiany**.</span><span class="sxs-lookup"><span data-stu-id="44fb0-211">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="44fb0-212">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="44fb0-212">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="44fb0-213">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="44fb0-213">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="44fb0-214">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="44fb0-214">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="44fb0-215">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="44fb0-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="44fb0-216">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="44fb0-216">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="44fb0-218">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="44fb0-218">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="44fb0-219">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="44fb0-219">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="44fb0-221">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="44fb0-221">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="44fb0-223">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="44fb0-223">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="44fb0-225">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="44fb0-225">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="44fb0-227">a.</span><span class="sxs-lookup"><span data-stu-id="44fb0-227">a.</span></span> <span data-ttu-id="44fb0-228">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="44fb0-228">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="44fb0-229">b.</span><span class="sxs-lookup"><span data-stu-id="44fb0-229">b.</span></span> <span data-ttu-id="44fb0-230">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="44fb0-230">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="44fb0-231">c.</span><span class="sxs-lookup"><span data-stu-id="44fb0-231">c.</span></span> <span data-ttu-id="44fb0-232">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="44fb0-232">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="44fb0-233">d.</span><span class="sxs-lookup"><span data-stu-id="44fb0-233">d.</span></span> <span data-ttu-id="44fb0-234">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="44fb0-234">Click **Create**.</span></span>
 
### <a name="creating-a-policystat-test-user"></a><span data-ttu-id="44fb0-235">Tworzenie użytkownika testowego PolicyStat</span><span class="sxs-lookup"><span data-stu-id="44fb0-235">Creating a PolicyStat test user</span></span>

<span data-ttu-id="44fb0-236">Aby włączyć użytkowników usługi Azure AD zalogować się do PolicyStat, musi być przygotowana do PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="44fb0-236">In order to enable Azure AD users to log into PolicyStat, they must be provisioned into PolicyStat.</span></span>  

<span data-ttu-id="44fb0-237">PolicyStat obsługuje tylko w czasie Inicjowanie obsługi użytkowników.</span><span class="sxs-lookup"><span data-stu-id="44fb0-237">PolicyStat supports just in time user provisioning.</span></span> <span data-ttu-id="44fb0-238">Oznacza to, że nie należy ręcznie dodać użytkowników do PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="44fb0-238">This means, you do not need to add the users manually to PolicyStat.</span></span> <span data-ttu-id="44fb0-239">Użytkownicy będą zostaną dodane automatycznie na ich pierwsze logowanie za pomocą logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="44fb0-239">The users will get added automatically on their first login through SSO.</span></span>

>[!NOTE]
><span data-ttu-id="44fb0-240">Możesz użyć innych PolicyStat użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez PolicyStat do udostępnienia konta użytkownika usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="44fb0-240">You can use any other PolicyStat user account creation tools or APIs provided by PolicyStat to provision Azure AD user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="44fb0-241">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="44fb0-241">Assigning the Azure AD test user</span></span>

<span data-ttu-id="44fb0-242">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="44fb0-242">In this section, you enable Britta Simon to use Azure single sign-on by granting access to PolicyStat.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="44fb0-244">**Aby przypisać Simona Britta PolicyStat, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="44fb0-244">**To assign Britta Simon to PolicyStat, perform the following steps:**</span></span>

1. <span data-ttu-id="44fb0-245">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="44fb0-245">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="44fb0-247">Na liście aplikacji zaznacz **PolicyStat**.</span><span class="sxs-lookup"><span data-stu-id="44fb0-247">In the applications list, select **PolicyStat**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_app.png) 

3. <span data-ttu-id="44fb0-249">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="44fb0-249">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="44fb0-251">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="44fb0-251">Click **Add** button.</span></span> <span data-ttu-id="44fb0-252">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="44fb0-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="44fb0-254">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="44fb0-254">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="44fb0-255">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="44fb0-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="44fb0-256">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="44fb0-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="44fb0-257">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="44fb0-257">Testing single sign-on</span></span>

<span data-ttu-id="44fb0-258">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="44fb0-258">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="44fb0-259">Po kliknięciu kafelka PolicyStat w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="44fb0-259">When you click the PolicyStat tile in the Access Panel, you should get automatically signed-on to your PolicyStat application.</span></span>
<span data-ttu-id="44fb0-260">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="44fb0-260">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="44fb0-261">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="44fb0-261">Additional resources</span></span>

* [<span data-ttu-id="44fb0-262">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="44fb0-262">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="44fb0-263">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="44fb0-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_203.png

