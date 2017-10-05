---
title: 'Samouczek: Integracji Azure Active Directory z Ceridian Dayforce HCM | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Ceridian Dayforce HCM."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 7adf1eb3-d063-45d6-96a8-fd53b329b3f3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: b2ea3d92f233dab5bd6814e4875f881117eac8e3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ceridian-dayforce-hcm"></a><span data-ttu-id="17ebc-103">Samouczek: Integracji Azure Active Directory z Ceridian Dayforce HCM</span><span class="sxs-lookup"><span data-stu-id="17ebc-103">Tutorial: Azure Active Directory integration with Ceridian Dayforce HCM</span></span>

<span data-ttu-id="17ebc-104">Z tego samouczka dowiesz się integrowanie Ceridian Dayforce HCM z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="17ebc-104">In this tutorial, you learn how to integrate Ceridian Dayforce HCM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="17ebc-105">Integracja z usługą Azure AD Ceridian Dayforce HCM zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="17ebc-105">Integrating Ceridian Dayforce HCM with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="17ebc-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="17ebc-106">You can control in Azure AD who has access to Ceridian Dayforce HCM.</span></span>
- <span data-ttu-id="17ebc-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do HCM Dayforce Ceridian (logowanie jednokrotne) z konta usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="17ebc-107">You can enable your users to automatically get signed-on to Ceridian Dayforce HCM (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="17ebc-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="17ebc-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="17ebc-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="17ebc-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="17ebc-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="17ebc-110">Prerequisites</span></span>

<span data-ttu-id="17ebc-111">Aby skonfigurować integrację usługi Azure AD z Ceridian Dayforce HCM, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="17ebc-111">To configure Azure AD integration with Ceridian Dayforce HCM, you need the following items:</span></span>

- <span data-ttu-id="17ebc-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="17ebc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="17ebc-113">Ceridian Dayforce HCM jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="17ebc-113">A Ceridian Dayforce HCM single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="17ebc-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="17ebc-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="17ebc-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="17ebc-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="17ebc-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="17ebc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="17ebc-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="17ebc-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="17ebc-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="17ebc-118">Scenario description</span></span>
<span data-ttu-id="17ebc-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="17ebc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="17ebc-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="17ebc-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="17ebc-121">Dodawanie Ceridian Dayforce HCM z galerii</span><span class="sxs-lookup"><span data-stu-id="17ebc-121">Adding Ceridian Dayforce HCM from the gallery</span></span>
2. <span data-ttu-id="17ebc-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="17ebc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ceridian-dayforce-hcm-from-the-gallery"></a><span data-ttu-id="17ebc-123">Dodawanie Ceridian Dayforce HCM z galerii</span><span class="sxs-lookup"><span data-stu-id="17ebc-123">Adding Ceridian Dayforce HCM from the gallery</span></span>
<span data-ttu-id="17ebc-124">Aby skonfigurować integrację usługi Azure AD Ceridian Dayforce HCM, należy dodać Ceridian Dayforce HCM z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="17ebc-124">To configure the integration of Ceridian Dayforce HCM into Azure AD, you need to add Ceridian Dayforce HCM from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="17ebc-125">**Aby dodać Ceridian Dayforce HCM z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="17ebc-125">**To add Ceridian Dayforce HCM from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="17ebc-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="17ebc-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Przycisk usługi Azure Active Directory][1]

2. <span data-ttu-id="17ebc-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="17ebc-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="17ebc-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="17ebc-129">Then go to **All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa][2]
    
3. <span data-ttu-id="17ebc-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="17ebc-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Nowy przycisk aplikacji][3]

4. <span data-ttu-id="17ebc-133">W polu wyszukiwania wpisz **Ceridian Dayforce HCM**, wybierz pozycję **Ceridian Dayforce HCM** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="17ebc-133">In the search box, type **Ceridian Dayforce HCM**, select **Ceridian Dayforce HCM** from result panel then click **Add** button to add the application.</span></span>

    ![HCM Dayforce Ceridian na liście wyników](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="17ebc-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="17ebc-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="17ebc-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z HCM Dayforce Ceridian w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="17ebc-136">In this section, you configure and test Azure AD single sign-on with Ceridian Dayforce HCM based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="17ebc-137">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Ceridian Dayforce HCM jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="17ebc-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Ceridian Dayforce HCM is to a user in Azure AD.</span></span> <span data-ttu-id="17ebc-138">Innymi słowy łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Ceridian Dayforce HCM musi się.</span><span class="sxs-lookup"><span data-stu-id="17ebc-138">In other words, a link relationship between an Azure AD user and the related user in Ceridian Dayforce HCM needs to be established.</span></span>

<span data-ttu-id="17ebc-139">W Ceridian Dayforce HCM, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="17ebc-139">In Ceridian Dayforce HCM, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="17ebc-140">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Ceridian Dayforce HCM, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="17ebc-140">To configure and test Azure AD single sign-on with Ceridian Dayforce HCM, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="17ebc-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="17ebc-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="17ebc-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="17ebc-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="17ebc-143">**[Tworzenie użytkownika testowego Ceridian Dayforce HCM](#create-a-ceridian-dayforce-hcm-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Ceridian Dayforce HCM, połączonej z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="17ebc-143">**[Create a Ceridian Dayforce HCM test user](#create-a-ceridian-dayforce-hcm-test-user)** - to have a counterpart of Britta Simon in Ceridian Dayforce HCM that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="17ebc-144">**[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="17ebc-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="17ebc-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="17ebc-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="17ebc-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="17ebc-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="17ebc-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="17ebc-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Ceridian Dayforce HCM application.</span></span>

<span data-ttu-id="17ebc-148">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Ceridian Dayforce HCM, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="17ebc-148">**To configure Azure AD single sign-on with Ceridian Dayforce HCM, perform the following steps:**</span></span>

1. <span data-ttu-id="17ebc-149">W portalu Azure na **Ceridian Dayforce HCM** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="17ebc-149">In the Azure portal, on the **Ceridian Dayforce HCM** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="17ebc-151">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="17ebc-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_samlbase.png)

3. <span data-ttu-id="17ebc-153">Na **Ceridian Dayforce HCM domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="17ebc-153">On the **Ceridian Dayforce HCM Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_url.png)
    
    <span data-ttu-id="17ebc-155">a.</span><span class="sxs-lookup"><span data-stu-id="17ebc-155">a.</span></span> <span data-ttu-id="17ebc-156">W **na adres URL logowania** tekstowym, wpisz adres URL używany przez użytkowników do logowania jednokrotnego do aplikacji Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="17ebc-156">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Ceridian Dayforce HCM application.</span></span>
    
    | <span data-ttu-id="17ebc-157">Środowisko</span><span class="sxs-lookup"><span data-stu-id="17ebc-157">Environment</span></span> | <span data-ttu-id="17ebc-158">ADRES URL</span><span class="sxs-lookup"><span data-stu-id="17ebc-158">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="17ebc-159">W środowisku produkcyjnym</span><span class="sxs-lookup"><span data-stu-id="17ebc-159">For production</span></span> | `https://sso.dayforcehcm.com/<DayforcehcmNamespace>` |
    | <span data-ttu-id="17ebc-160">Dla testu</span><span class="sxs-lookup"><span data-stu-id="17ebc-160">For test</span></span> | `https://ssotest.dayforcehcm.com/<DayforcehcmNamespace>` |
    
    <span data-ttu-id="17ebc-161">b.</span><span class="sxs-lookup"><span data-stu-id="17ebc-161">b.</span></span> <span data-ttu-id="17ebc-162">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="17ebc-162">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    
    | <span data-ttu-id="17ebc-163">Środowisko</span><span class="sxs-lookup"><span data-stu-id="17ebc-163">Environment</span></span> | <span data-ttu-id="17ebc-164">ADRES URL</span><span class="sxs-lookup"><span data-stu-id="17ebc-164">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="17ebc-165">W środowisku produkcyjnym</span><span class="sxs-lookup"><span data-stu-id="17ebc-165">For production</span></span> | `https://ncpingfederate.dayforcehcm.com/sp` |
    | <span data-ttu-id="17ebc-166">Dla testu</span><span class="sxs-lookup"><span data-stu-id="17ebc-166">For test</span></span> | `https://fs-test.dayforcehcm.com/sp` |
    
    <span data-ttu-id="17ebc-167">c.</span><span class="sxs-lookup"><span data-stu-id="17ebc-167">c.</span></span> <span data-ttu-id="17ebc-168">W **adres URL odpowiedzi** tekstowym, wpisz adres URL używany przez usługę Azure AD można opublikować odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="17ebc-168">In the **Reply URL** textbox, type the URL used by Azure AD to post the response.</span></span>
    
    | <span data-ttu-id="17ebc-169">Środowisko</span><span class="sxs-lookup"><span data-stu-id="17ebc-169">Environment</span></span> | <span data-ttu-id="17ebc-170">ADRES URL</span><span class="sxs-lookup"><span data-stu-id="17ebc-170">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="17ebc-171">W środowisku produkcyjnym</span><span class="sxs-lookup"><span data-stu-id="17ebc-171">For production</span></span> | `https://ncpingfederate.dayforcehcm.com/sp/ACS.saml2` |
    | <span data-ttu-id="17ebc-172">Dla testu</span><span class="sxs-lookup"><span data-stu-id="17ebc-172">For test</span></span> | `https://fs-test.dayforcehcm.com/sp/ACS.saml2` |
    
    > [!NOTE] 
    > <span data-ttu-id="17ebc-173">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="17ebc-173">These values are not real.</span></span> <span data-ttu-id="17ebc-174">Rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="17ebc-174">Update these values with the actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="17ebc-175">Skontaktuj się z [zespołem pomocy technicznej klienta HCM Dayforce Ceridian](https://www.ceridian.com/contact-us/index.html) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="17ebc-175">Contact [Ceridian Dayforce HCM Client support team](https://www.ceridian.com/contact-us/index.html) to get these values.</span></span>

4. <span data-ttu-id="17ebc-176">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="17ebc-176">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Łącze pobierania certyfikatu](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_certificate.png) 

5. <span data-ttu-id="17ebc-178">Aplikacja Ceridian Dayforce HCM oczekuje potwierdzenia języka SAML w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="17ebc-178">Your Ceridian Dayforce HCM application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="17ebc-179">Praca z [zespołem pomocy technicznej Ceridian Dayforce HCM](https://www.ceridian.com/contact-us/index.html) najpierw, aby zidentyfikować identyfikator użytkownika.</span><span class="sxs-lookup"><span data-stu-id="17ebc-179">Work with [Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html) first to identify the correct user identifier.</span></span> <span data-ttu-id="17ebc-180">Firma Microsoft zaleca używanie **"name"** atrybut jako identyfikator użytkownika.</span><span class="sxs-lookup"><span data-stu-id="17ebc-180">Microsoft recommends using the **"name"** attribute as user identifier.</span></span> <span data-ttu-id="17ebc-181">Możesz zarządzać wartości tych atrybutów z **atrybuty użytkownika** sekcji na stronie integracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="17ebc-181">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="17ebc-182">Poniższy zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="17ebc-182">The following screenshot shows an example for this.</span></span>  

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_07.png)

6. <span data-ttu-id="17ebc-184">W **atrybuty użytkownika** sekcji na **logowanie jednokrotne** okna dialogowego, skonfiguruj atrybut tokenu SAML, jak pokazano na ilustracji powyżej i wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="17ebc-184">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="17ebc-185">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="17ebc-185">Attribute Name</span></span>  | <span data-ttu-id="17ebc-186">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="17ebc-186">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    | <span data-ttu-id="17ebc-187">name</span><span class="sxs-lookup"><span data-stu-id="17ebc-187">name</span></span>  | <span data-ttu-id="17ebc-188">User.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="17ebc-188">user.extensionattribute2</span></span> |    

    <span data-ttu-id="17ebc-189">a.</span><span class="sxs-lookup"><span data-stu-id="17ebc-189">a.</span></span> <span data-ttu-id="17ebc-190">Kliknij przycisk **Dodaj atrybut** otworzyć **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="17ebc-190">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_attribute_04.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="17ebc-193">b.</span><span class="sxs-lookup"><span data-stu-id="17ebc-193">b.</span></span> <span data-ttu-id="17ebc-194">W **nazwa** tekstowym, wpisz nazwę atrybut wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="17ebc-194">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="17ebc-195">c.</span><span class="sxs-lookup"><span data-stu-id="17ebc-195">c.</span></span> <span data-ttu-id="17ebc-196">W **wartość** wybierz atrybut użytkownika, którego chcesz użyć implementacji.</span><span class="sxs-lookup"><span data-stu-id="17ebc-196">In the **Value** list, select the user attribute you want to use for your implementation.</span></span>
    <span data-ttu-id="17ebc-197">Na przykład, jeśli chcesz użyć identyfikatorem EmployeeID jako użytkownik Unikatowy identyfikator i przechowywanych wartości atrybutu w ExtensionAttribute2, następnie wybierz **user.extensionattribute2**.</span><span class="sxs-lookup"><span data-stu-id="17ebc-197">For example, if you want to use the EmployeeID as unique user identifier and you have stored the attribute value in the ExtensionAttribute2, then select **user.extensionattribute2**.</span></span>
    
    <span data-ttu-id="17ebc-198">d.</span><span class="sxs-lookup"><span data-stu-id="17ebc-198">d.</span></span> <span data-ttu-id="17ebc-199">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="17ebc-199">Click **Ok**.</span></span>

7. <span data-ttu-id="17ebc-200">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="17ebc-200">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="17ebc-202">Na **Ceridian Dayforce HCM konfiguracji** kliknij **skonfigurować HCM Dayforce Ceridian** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="17ebc-202">On the **Ceridian Dayforce HCM Configuration** section, click **Configure Ceridian Dayforce HCM** to open **Configure sign-on** window.</span></span> <span data-ttu-id="17ebc-203">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="17ebc-203">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Ceridian Dayforce HCM konfiguracji](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_configure.png) 

9. <span data-ttu-id="17ebc-205">Skonfigurować logowanie jednokrotne w **Ceridian Dayforce HCM** stronie, musisz wysłać pobrany **XML metadanych** i **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** do [zespołem pomocy technicznej Ceridian Dayforce HCM](https://www.ceridian.com/contact-us/index.html).</span><span class="sxs-lookup"><span data-stu-id="17ebc-205">To configure single sign-on on **Ceridian Dayforce HCM** side, you need to send the downloaded **Metadata XML** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html).</span></span>

> [!TIP]
> <span data-ttu-id="17ebc-206">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="17ebc-206">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="17ebc-207">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="17ebc-207">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="17ebc-208">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="17ebc-208">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="17ebc-209">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="17ebc-209">Create an Azure AD test user</span></span>

<span data-ttu-id="17ebc-210">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="17ebc-210">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="17ebc-212">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="17ebc-212">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="17ebc-213">W portalu Azure, w okienku po lewej stronie kliknij **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="17ebc-213">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="17ebc-215">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="17ebc-215">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="17ebc-217">Aby otworzyć **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** w górnej części **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="17ebc-217">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Przycisk Dodaj](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="17ebc-219">W **użytkownika** okna dialogowego wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="17ebc-219">In the **User** dialog box, perform the following steps:</span></span>

    ![Okno dialogowe użytkownika](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_04.png)

    <span data-ttu-id="17ebc-221">a.</span><span class="sxs-lookup"><span data-stu-id="17ebc-221">a.</span></span> <span data-ttu-id="17ebc-222">W **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="17ebc-222">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="17ebc-223">b.</span><span class="sxs-lookup"><span data-stu-id="17ebc-223">b.</span></span> <span data-ttu-id="17ebc-224">W **nazwy użytkownika** wpisz adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="17ebc-224">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="17ebc-225">c.</span><span class="sxs-lookup"><span data-stu-id="17ebc-225">c.</span></span> <span data-ttu-id="17ebc-226">Wybierz **Pokaż hasło** pole wyboru, a następnie zanotuj wartość, która jest wyświetlana w **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="17ebc-226">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="17ebc-227">d.</span><span class="sxs-lookup"><span data-stu-id="17ebc-227">d.</span></span> <span data-ttu-id="17ebc-228">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="17ebc-228">Click **Create**.</span></span>
 
### <a name="create-a-ceridian-dayforce-hcm-test-user"></a><span data-ttu-id="17ebc-229">Tworzenie użytkownika testowego Ceridian Dayforce HCM</span><span class="sxs-lookup"><span data-stu-id="17ebc-229">Create a Ceridian Dayforce HCM test user</span></span>

<span data-ttu-id="17ebc-230">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="17ebc-230">The objective of this section is to create a user called Britta Simon in Ceridian Dayforce HCM.</span></span> <span data-ttu-id="17ebc-231">Praca z [zespołem pomocy technicznej Ceridian Dayforce HCM](https://www.ceridian.com/contact-us/index.html) można pobrać użytkowników dodanych w aplikacji Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="17ebc-231">Work with the [Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html) to get users added in the Ceridian Dayforce HCM application.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="17ebc-232">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="17ebc-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="17ebc-233">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="17ebc-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Ceridian Dayforce HCM.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="17ebc-235">**Aby przypisać Simona Britta Ceridian Dayforce HCM, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="17ebc-235">**To assign Britta Simon to Ceridian Dayforce HCM, perform the following steps:**</span></span>

1. <span data-ttu-id="17ebc-236">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="17ebc-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="17ebc-238">Na liście aplikacji zaznacz **Ceridian Dayforce HCM**.</span><span class="sxs-lookup"><span data-stu-id="17ebc-238">In the applications list, select **Ceridian Dayforce HCM**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_app.png) 

3. <span data-ttu-id="17ebc-240">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="17ebc-240">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="17ebc-242">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="17ebc-242">Click **Add** button.</span></span> <span data-ttu-id="17ebc-243">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="17ebc-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="17ebc-245">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="17ebc-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="17ebc-246">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="17ebc-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="17ebc-247">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="17ebc-247">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="17ebc-248">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="17ebc-248">Assign the Azure AD test user</span></span>

<span data-ttu-id="17ebc-249">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="17ebc-249">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Ceridian Dayforce HCM.</span></span>

![Przypisanie roli użytkownika][200] 

<span data-ttu-id="17ebc-251">**Aby przypisać Simona Britta Ceridian Dayforce HCM, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="17ebc-251">**To assign Britta Simon to Ceridian Dayforce HCM, perform the following steps:**</span></span>

1. <span data-ttu-id="17ebc-252">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="17ebc-252">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="17ebc-254">Na liście aplikacji zaznacz **Ceridian Dayforce HCM**.</span><span class="sxs-lookup"><span data-stu-id="17ebc-254">In the applications list, select **Ceridian Dayforce HCM**.</span></span>

    ![Łącze Ceridian Dayforce HCM na liście aplikacji](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_app.png)  

3. <span data-ttu-id="17ebc-256">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="17ebc-256">In the menu on the left, click **Users and groups**.</span></span>

    ![Łącze "Użytkownicy i grupy"][202]

4. <span data-ttu-id="17ebc-258">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="17ebc-258">Click **Add** button.</span></span> <span data-ttu-id="17ebc-259">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="17ebc-259">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![W okienku Dodaj przydziału][203]

5. <span data-ttu-id="17ebc-261">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="17ebc-261">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="17ebc-262">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="17ebc-262">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="17ebc-263">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="17ebc-263">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="17ebc-264">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="17ebc-264">Test single sign-on</span></span>

<span data-ttu-id="17ebc-265">Celem tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="17ebc-265">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="17ebc-266">Po kliknięciu kafelka Ceridian Dayforce HCM w panelu dostępu użytkownik powinien uzyskać automatycznie zalogowane do aplikacji Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="17ebc-266">When you click the Ceridian Dayforce HCM tile in the Access Panel, you should get automatically signed-on to your Ceridian Dayforce HCM application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="17ebc-267">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="17ebc-267">Additional resources</span></span>

* [<span data-ttu-id="17ebc-268">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="17ebc-268">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="17ebc-269">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="17ebc-269">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_203.png

