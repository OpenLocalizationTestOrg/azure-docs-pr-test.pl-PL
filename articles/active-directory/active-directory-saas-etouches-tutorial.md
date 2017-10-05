---
title: 'Samouczek: Integracji Azure Active Directory z etouches | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i etouches."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 76cccaa8-859c-4c16-9d1d-8a6496fc7520
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 3cd9e9d6aae924369065ca492b1f6380c0ddc5fe
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-etouches"></a><span data-ttu-id="59730-103">Samouczek: Integracji Azure Active Directory z etouches</span><span class="sxs-lookup"><span data-stu-id="59730-103">Tutorial: Azure Active Directory integration with etouches</span></span>

<span data-ttu-id="59730-104">Z tego samouczka dowiesz się integrowanie etouches z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="59730-104">In this tutorial, you learn how to integrate etouches with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="59730-105">Integracja z usługą Azure AD etouches zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="59730-105">Integrating etouches with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="59730-106">Można kontrolować w usłudze Azure AD, który ma dostęp do etouches</span><span class="sxs-lookup"><span data-stu-id="59730-106">You can control in Azure AD who has access to etouches</span></span>
- <span data-ttu-id="59730-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do etouches (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="59730-107">You can enable your users to automatically get signed-on to etouches (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="59730-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="59730-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="59730-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="59730-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="59730-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="59730-110">Prerequisites</span></span>

<span data-ttu-id="59730-111">Aby skonfigurować integrację usługi Azure AD z etouches, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="59730-111">To configure Azure AD integration with etouches, you need the following items:</span></span>

- <span data-ttu-id="59730-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="59730-112">An Azure AD subscription</span></span>
- <span data-ttu-id="59730-113">Etouches logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="59730-113">An etouches single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="59730-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="59730-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="59730-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="59730-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="59730-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="59730-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="59730-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="59730-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="59730-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="59730-118">Scenario description</span></span>
<span data-ttu-id="59730-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="59730-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="59730-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="59730-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="59730-121">Dodawanie etouches z galerii</span><span class="sxs-lookup"><span data-stu-id="59730-121">Adding etouches from the gallery</span></span>
2. <span data-ttu-id="59730-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="59730-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-etouches-from-the-gallery"></a><span data-ttu-id="59730-123">Dodawanie etouches z galerii</span><span class="sxs-lookup"><span data-stu-id="59730-123">Adding etouches from the gallery</span></span>
<span data-ttu-id="59730-124">Aby skonfigurować integrację usługi Azure AD etouches, należy dodać etouches z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="59730-124">To configure the integration of etouches into Azure AD, you need to add etouches from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="59730-125">**Aby dodać etouches z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="59730-125">**To add etouches from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="59730-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="59730-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Przycisk usługi Azure Active Directory][1]

2. <span data-ttu-id="59730-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="59730-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="59730-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="59730-129">Then go to **All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa][2]
    
3. <span data-ttu-id="59730-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="59730-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Nowy przycisk aplikacji][3]

4. <span data-ttu-id="59730-133">W polu wyszukiwania wpisz **etouches**, wybierz pozycję **etouches** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="59730-133">In the search box, type **etouches**, select **etouches** from result panel then click **Add** button to add the application.</span></span>

    ![etouches na liście wyników](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="59730-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="59730-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="59730-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z etouches w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="59730-136">In this section, you configure and test Azure AD single sign-on with etouches based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="59730-137">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w etouches jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="59730-137">For single sign-on to work, Azure AD needs to know what the counterpart user in etouches is to a user in Azure AD.</span></span> <span data-ttu-id="59730-138">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w etouches musi się.</span><span class="sxs-lookup"><span data-stu-id="59730-138">In other words, a link relationship between an Azure AD user and the related user in etouches needs to be established.</span></span>

<span data-ttu-id="59730-139">W etouches, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="59730-139">In etouches, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="59730-140">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z etouches, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="59730-140">To configure and test Azure AD single sign-on with etouches, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="59730-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="59730-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="59730-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="59730-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="59730-143">**[Tworzenie użytkownika testowego etouches](#create-an-etouches-test-user)**  — mają odpowiednika Simona Britta w etouches połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="59730-143">**[Create an etouches test user](#create-an-etouches-test-user)** - to have a counterpart of Britta Simon in etouches that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="59730-144">**[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="59730-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="59730-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="59730-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="59730-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="59730-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="59730-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji etouches.</span><span class="sxs-lookup"><span data-stu-id="59730-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your etouches application.</span></span>

<span data-ttu-id="59730-148">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z etouches, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="59730-148">**To configure Azure AD single sign-on with etouches, perform the following steps:**</span></span>

1. <span data-ttu-id="59730-149">W portalu Azure na **etouches** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="59730-149">In the Azure portal, on the **etouches** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="59730-151">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="59730-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_samlbase.png)

3. <span data-ttu-id="59730-153">Na **etouches domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="59730-153">On the **etouches Domain and URLs** section, perform the following steps:</span></span>

    ![informacje logowania z jednym etouches domeny i adres URL](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_url.png)

    <span data-ttu-id="59730-155">a.</span><span class="sxs-lookup"><span data-stu-id="59730-155">a.</span></span> <span data-ttu-id="59730-156">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://www.eiseverywhere.com/saml/accounts/?sso&accountid=<ACCOUNTID>`</span><span class="sxs-lookup"><span data-stu-id="59730-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.eiseverywhere.com/saml/accounts/?sso&accountid=<ACCOUNTID>`</span></span>

    <span data-ttu-id="59730-157">b.</span><span class="sxs-lookup"><span data-stu-id="59730-157">b.</span></span> <span data-ttu-id="59730-158">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://www.eiseverywhere.com/<instance name>`</span><span class="sxs-lookup"><span data-stu-id="59730-158">In the **Identifier** textbox, type a URL using the following pattern: `https://www.eiseverywhere.com/<instance name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="59730-159">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="59730-159">These values are not real.</span></span> <span data-ttu-id="59730-160">Należy zaktualizować wartość znakiem rzeczywisty adres URL i identyfikator, który znajduje się w dalszej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="59730-160">You update the value with the actual Sign on URL and Identifier, which is explained later in the tutorial.</span></span>
    > 

4. <span data-ttu-id="59730-161">Aplikacja etouches oczekuje potwierdzenia języka SAML w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="59730-161">etouches application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="59730-162">Skonfiguruj następujące oświadczeń dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="59730-162">Configure the following claims for this application.</span></span> <span data-ttu-id="59730-163">Możesz zarządzać wartości tych atrybutów z **atrybut użytkownika** aplikacji.</span><span class="sxs-lookup"><span data-stu-id="59730-163">You can manage the values of these attributes from the **User Attribute** of the application.</span></span> <span data-ttu-id="59730-164">Poniższy zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="59730-164">The following screenshot shows an example for this.</span></span> 

    ![Atrybut użytkownika](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_attribute.png) 

5. <span data-ttu-id="59730-166">W **atrybuty użytkownika** sekcji na **logowanie jednokrotne** okna dialogowego, skonfiguruj atrybut tokenu SAML, jak pokazano w obrazie i wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="59730-166">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="59730-167">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="59730-167">Attribute Name</span></span> | <span data-ttu-id="59730-168">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="59730-168">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="59730-169">Adres e-mail</span><span class="sxs-lookup"><span data-stu-id="59730-169">Email</span></span> | <span data-ttu-id="59730-170">User.mail</span><span class="sxs-lookup"><span data-stu-id="59730-170">user.mail</span></span> |    
    
    <span data-ttu-id="59730-171">a.</span><span class="sxs-lookup"><span data-stu-id="59730-171">a.</span></span> <span data-ttu-id="59730-172">Kliknij przycisk **Dodaj atrybut** otworzyć **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="59730-172">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Dodaj atrybut](./media/active-directory-saas-etouches-tutorial/tutorial_attribute_04.png)

    ![Dodaj atrybut okna dialogowego](./media/active-directory-saas-etouches-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="59730-175">b.</span><span class="sxs-lookup"><span data-stu-id="59730-175">b.</span></span> <span data-ttu-id="59730-176">W **nazwa** tekstowym, wpisz nazwę atrybut wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="59730-176">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="59730-177">c.</span><span class="sxs-lookup"><span data-stu-id="59730-177">c.</span></span> <span data-ttu-id="59730-178">Z **wartość** listy, wpisz wartość atrybutu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="59730-178">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="59730-179">d.</span><span class="sxs-lookup"><span data-stu-id="59730-179">d.</span></span> <span data-ttu-id="59730-180">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="59730-180">Click **Ok**.</span></span> 

6. <span data-ttu-id="59730-181">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="59730-181">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Łącze pobierania certyfikatu](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_certificate.png) 

7. <span data-ttu-id="59730-183">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="59730-183">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-etouches-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="59730-185">Aby uzyskać logowania jednokrotnego skonfigurowane dla aplikacji, wykonaj następujące czynności w aplikacji etouches:</span><span class="sxs-lookup"><span data-stu-id="59730-185">To get SSO configured for your application, perform the following steps in the etouches application:</span></span> 

    ![Konfiguracja etouches](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_06.png) 

    <span data-ttu-id="59730-187">a.</span><span class="sxs-lookup"><span data-stu-id="59730-187">a.</span></span> <span data-ttu-id="59730-188">Zaloguj się do **etouches** aplikacji przy użyciu uprawnień administratora.</span><span class="sxs-lookup"><span data-stu-id="59730-188">Login to **etouches** application using the Admin rights.</span></span>
   
    <span data-ttu-id="59730-189">b.</span><span class="sxs-lookup"><span data-stu-id="59730-189">b.</span></span> <span data-ttu-id="59730-190">Przejdź do **SAML** konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="59730-190">Go to the **SAML** Configuration.</span></span>

    <span data-ttu-id="59730-191">c.</span><span class="sxs-lookup"><span data-stu-id="59730-191">c.</span></span> <span data-ttu-id="59730-192">W **ustawienia ogólne** sekcji, Otwórz swój certyfikat pobrany z portalu Azure w programie Notatnik, skopiuj zawartość i wklej go w polu tekstowym metadanych IDP.</span><span class="sxs-lookup"><span data-stu-id="59730-192">In the **General Settings** section, open your downloaded certificate from Azure portal in notepad, copy the content, and then paste it into the IDP metadata textbox.</span></span> 

    <span data-ttu-id="59730-193">d.</span><span class="sxs-lookup"><span data-stu-id="59730-193">d.</span></span> <span data-ttu-id="59730-194">Polecenie **Zapisz & pozostać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="59730-194">Click on the **Save & Stay** button.</span></span>
  
    <span data-ttu-id="59730-195">e.</span><span class="sxs-lookup"><span data-stu-id="59730-195">e.</span></span> <span data-ttu-id="59730-196">Polecenie **metadane aktualizacji** przycisk w sekcji metadanych SAML.</span><span class="sxs-lookup"><span data-stu-id="59730-196">Click on the **Update Metadata** button in the SAML Metadata section.</span></span> 

    <span data-ttu-id="59730-197">f.</span><span class="sxs-lookup"><span data-stu-id="59730-197">f.</span></span> <span data-ttu-id="59730-198">To spowoduje otwarcie strony i wykonania rejestracji Jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="59730-198">This opens the page and perform SSO.</span></span> <span data-ttu-id="59730-199">Po rejestracji Jednokrotnej jest praca następnie można skonfigurować nazwę użytkownika.</span><span class="sxs-lookup"><span data-stu-id="59730-199">Once the SSO is working then you can set up the username.</span></span>

    <span data-ttu-id="59730-200">g.</span><span class="sxs-lookup"><span data-stu-id="59730-200">g.</span></span> <span data-ttu-id="59730-201">W polu nazwy użytkownika, wybierz **emailaddress** jak pokazano na poniższej ilustracji.</span><span class="sxs-lookup"><span data-stu-id="59730-201">In the Username field, select the **emailaddress** as shown in the image below.</span></span> 

    <span data-ttu-id="59730-202">h.</span><span class="sxs-lookup"><span data-stu-id="59730-202">h.</span></span> <span data-ttu-id="59730-203">Kopiuj **SP identyfikator jednostki** i wklej go do **identyfikator** pola tekstowego, który znajduje się w **etouches domeny i adres URL** sekcji z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="59730-203">Copy the **SP entity ID** value and paste it into the **Identifier**  textbox, which is in **etouches Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="59730-204">i.</span><span class="sxs-lookup"><span data-stu-id="59730-204">i.</span></span> <span data-ttu-id="59730-205">Kopiuj **adres URL logowania jednokrotnego / ACS** i wklej go do **Zaloguj się na adres URL** pola tekstowego, który znajduje się w **etouches domeny i adres URL** sekcji z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="59730-205">Copy the **SSO URL / ACS** value and paste it into the **Sign on URL** textbox, which is in **etouches Domain and URLs** section on Azure portal.</span></span>
   
> [!TIP]
> <span data-ttu-id="59730-206">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="59730-206">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="59730-207">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="59730-207">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="59730-208">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="59730-208">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="59730-209">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="59730-209">Create an Azure AD test user</span></span>
<span data-ttu-id="59730-210">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="59730-210">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="59730-212">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="59730-212">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="59730-213">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="59730-213">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-etouches-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="59730-215">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="59730-215">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-etouches-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="59730-217">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="59730-217">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Przycisk Dodaj](./media/active-directory-saas-etouches-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="59730-219">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="59730-219">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Okno dialogowe użytkownika](./media/active-directory-saas-etouches-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="59730-221">a.</span><span class="sxs-lookup"><span data-stu-id="59730-221">a.</span></span> <span data-ttu-id="59730-222">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="59730-222">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="59730-223">b.</span><span class="sxs-lookup"><span data-stu-id="59730-223">b.</span></span> <span data-ttu-id="59730-224">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="59730-224">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="59730-225">c.</span><span class="sxs-lookup"><span data-stu-id="59730-225">c.</span></span> <span data-ttu-id="59730-226">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="59730-226">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="59730-227">d.</span><span class="sxs-lookup"><span data-stu-id="59730-227">d.</span></span> <span data-ttu-id="59730-228">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="59730-228">Click **Create**.</span></span>
 
### <a name="create-an-etouches-test-user"></a><span data-ttu-id="59730-229">Tworzenie użytkownika testowego etouches</span><span class="sxs-lookup"><span data-stu-id="59730-229">Create an etouches test user</span></span>

<span data-ttu-id="59730-230">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w etouches.</span><span class="sxs-lookup"><span data-stu-id="59730-230">In this section, you create a user called Britta Simon in etouches.</span></span> <span data-ttu-id="59730-231">Praca z [etouches klienta obsługuje zespołu](https://www.etouches.com/event-software/support/customer-support/) Aby dodać użytkowników do platformy etouches.</span><span class="sxs-lookup"><span data-stu-id="59730-231">Work with [etouches Client support team](https://www.etouches.com/event-software/support/customer-support/) to add the users in the etouches platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="59730-232">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="59730-232">Assign the Azure AD test user</span></span>

<span data-ttu-id="59730-233">W tej sekcji musisz włączyć Simona Britta do użycia usługi Azure logowania jednokrotnego za udzielanie dostępu do etouches.</span><span class="sxs-lookup"><span data-stu-id="59730-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to etouches.</span></span>

![Przypisanie roli użytkownika][200] 

<span data-ttu-id="59730-235">**Aby przypisać Simona Britta etouches, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="59730-235">**To assign Britta Simon to etouches, perform the following steps:**</span></span>

1. <span data-ttu-id="59730-236">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="59730-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="59730-238">Na liście aplikacji zaznacz **etouches**.</span><span class="sxs-lookup"><span data-stu-id="59730-238">In the applications list, select **etouches**.</span></span>

    ![Łącze etouches na liście aplikacji](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_app.png) 

3. <span data-ttu-id="59730-240">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="59730-240">In the menu on the left, click **Users and groups**.</span></span>

    ![Łącze "Użytkownicy i grupy"][202] 

4. <span data-ttu-id="59730-242">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="59730-242">Click **Add** button.</span></span> <span data-ttu-id="59730-243">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="59730-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![W okienku Dodaj przydziału][203]

5. <span data-ttu-id="59730-245">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="59730-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="59730-246">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="59730-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="59730-247">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="59730-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="59730-248">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="59730-248">Test single sign-on</span></span>


<span data-ttu-id="59730-249">Celem tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="59730-249">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="59730-250">Po kliknięciu kafelka etouches w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji etouches.</span><span class="sxs-lookup"><span data-stu-id="59730-250">When you click the etouches tile in the Access Panel, you should get automatically signed-on to your etouches application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="59730-251">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="59730-251">Additional resources</span></span>

* [<span data-ttu-id="59730-252">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="59730-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="59730-253">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="59730-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_203.png

