---
title: 'Samouczek: Integracji Azure Active Directory z Hightail | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Hightail."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e15206ac-74b0-46e4-9329-892c7d242ec0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: ba55f9b62d274aa3eb91723c62b53f54de0891b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hightail"></a><span data-ttu-id="c7813-103">Samouczek: Integracji Azure Active Directory z Hightail</span><span class="sxs-lookup"><span data-stu-id="c7813-103">Tutorial: Azure Active Directory integration with Hightail</span></span>

<span data-ttu-id="c7813-104">Z tego samouczka dowiesz się integrowanie Hightail z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c7813-104">In this tutorial, you learn how to integrate Hightail with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c7813-105">Integracja z usługą Azure AD Hightail zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="c7813-105">Integrating Hightail with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c7813-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Hightail</span><span class="sxs-lookup"><span data-stu-id="c7813-106">You can control in Azure AD who has access to Hightail</span></span>
- <span data-ttu-id="c7813-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Hightail (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7813-107">You can enable your users to automatically get signed-on to Hightail (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c7813-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c7813-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c7813-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c7813-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c7813-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c7813-110">Prerequisites</span></span>

<span data-ttu-id="c7813-111">Aby skonfigurować integrację usługi Azure AD z Hightail, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="c7813-111">To configure Azure AD integration with Hightail, you need the following items:</span></span>

- <span data-ttu-id="c7813-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7813-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c7813-113">Hightail logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="c7813-113">A Hightail single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c7813-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="c7813-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c7813-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="c7813-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c7813-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="c7813-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c7813-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c7813-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c7813-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="c7813-118">Scenario description</span></span>
<span data-ttu-id="c7813-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="c7813-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c7813-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="c7813-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c7813-121">Dodawanie Hightail z galerii</span><span class="sxs-lookup"><span data-stu-id="c7813-121">Adding Hightail from the gallery</span></span>
2. <span data-ttu-id="c7813-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="c7813-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hightail-from-the-gallery"></a><span data-ttu-id="c7813-123">Dodawanie Hightail z galerii</span><span class="sxs-lookup"><span data-stu-id="c7813-123">Adding Hightail from the gallery</span></span>
<span data-ttu-id="c7813-124">Aby skonfigurować integrację usługi Azure AD Hightail, należy dodać Hightail z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="c7813-124">To configure the integration of Hightail into Azure AD, you need to add Hightail from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c7813-125">**Aby dodać Hightail z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c7813-125">**To add Hightail from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c7813-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="c7813-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="c7813-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="c7813-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c7813-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="c7813-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="c7813-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c7813-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="c7813-133">W polu wyszukiwania wpisz **Hightail**.</span><span class="sxs-lookup"><span data-stu-id="c7813-133">In the search box, type **Hightail**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_search.png)

5. <span data-ttu-id="c7813-135">W panelu wyników wybierz **Hightail**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="c7813-135">In the results panel, select **Hightail**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c7813-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="c7813-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c7813-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Hightail w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="c7813-138">In this section, you configure and test Azure AD single sign-on with Hightail based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c7813-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Hightail jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c7813-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Hightail is to a user in Azure AD.</span></span> <span data-ttu-id="c7813-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Hightail musi się.</span><span class="sxs-lookup"><span data-stu-id="c7813-140">In other words, a link relationship between an Azure AD user and the related user in Hightail needs to be established.</span></span>

<span data-ttu-id="c7813-141">W Hightail, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="c7813-141">In Hightail, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c7813-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Hightail, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="c7813-142">To configure and test Azure AD single sign-on with Hightail, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c7813-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="c7813-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c7813-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="c7813-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c7813-145">**[Tworzenie użytkownika testowego Hightail](#creating-a-hightail-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Hightail połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c7813-145">**[Creating a Hightail test user](#creating-a-hightail-test-user)** - to have a counterpart of Britta Simon in Hightail that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c7813-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="c7813-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c7813-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="c7813-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c7813-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="c7813-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c7813-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Hightail.</span><span class="sxs-lookup"><span data-stu-id="c7813-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Hightail application.</span></span>

<span data-ttu-id="c7813-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Hightail, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c7813-150">**To configure Azure AD single sign-on with Hightail, perform the following steps:**</span></span>

1. <span data-ttu-id="c7813-151">W portalu Azure na **Hightail** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="c7813-151">In the Azure portal, on the **Hightail** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="c7813-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="c7813-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_samlbase.png)

3. <span data-ttu-id="c7813-155">Na **Hightail domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c7813-155">On the **Hightail Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url.png)

     <span data-ttu-id="c7813-157">W **adres URL odpowiedzi** tekstowym, wpisz adres URL jako:`https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse`</span><span class="sxs-lookup"><span data-stu-id="c7813-157">In the **Reply URL** textbox, type the URL as: `https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c7813-158">Powyższe nie jest rzeczywistą wartość.</span><span class="sxs-lookup"><span data-stu-id="c7813-158">The preceding value is not real value.</span></span> <span data-ttu-id="c7813-159">Wartość zaktualizuje rzeczywiste odpowiedzi adres URL, który znajduje się w dalszej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="c7813-159">You will update the value with the actual Reply URL, which is explained later in the tutorial.</span></span>
 
4. <span data-ttu-id="c7813-160">Na **Hightail domeny i adres URL** sekcji, jeśli chcesz skonfigurować aplikację w **SP zainicjował tryb**, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c7813-160">On the **Hightail Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url1.png)

    <span data-ttu-id="c7813-162">a.</span><span class="sxs-lookup"><span data-stu-id="c7813-162">a.</span></span> <span data-ttu-id="c7813-163">Kliknij przycisk **Pokaż zaawansowane ustawienia adresu URL**.</span><span class="sxs-lookup"><span data-stu-id="c7813-163">Click the **Show advanced URL settings**.</span></span>

    <span data-ttu-id="c7813-164">b.</span><span class="sxs-lookup"><span data-stu-id="c7813-164">b.</span></span> <span data-ttu-id="c7813-165">W **na adres URL logowania** tekstowym, wpisz adres URL jako:`https://www.hightail.com/loginSSO`</span><span class="sxs-lookup"><span data-stu-id="c7813-165">In the **Sign On URL** textbox, type the URL as: `https://www.hightail.com/loginSSO`</span></span>

4. <span data-ttu-id="c7813-166">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="c7813-166">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_certificate.png) 

5. <span data-ttu-id="c7813-168">Hightail aplikacji oczekuje potwierdzenia języka SAML w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="c7813-168">Hightail application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="c7813-169">Skonfiguruj następujące oświadczeń dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c7813-169">Please configure the following claims for this application.</span></span> <span data-ttu-id="c7813-170">Możesz zarządzać wartości tych atrybutów z **"Atrribute"** aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c7813-170">You can manage the values of these attributes from the **"Atrribute"** tab of the application.</span></span> <span data-ttu-id="c7813-171">Poniższy zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="c7813-171">The following screenshot shows an example for this.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_attribute.png) 

6. <span data-ttu-id="c7813-173">W **atrybuty użytkownika** sekcji na **logowanie jednokrotne** okna dialogowego, skonfiguruj atrybut tokenu SAML, jak pokazano w obrazie i wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c7813-173">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="c7813-174">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="c7813-174">Attribute Name</span></span> | <span data-ttu-id="c7813-175">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="c7813-175">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="c7813-176">Imię</span><span class="sxs-lookup"><span data-stu-id="c7813-176">FirstName</span></span> | <span data-ttu-id="c7813-177">User.givenName</span><span class="sxs-lookup"><span data-stu-id="c7813-177">user.givenname</span></span> |
    | <span data-ttu-id="c7813-178">Nazwisko</span><span class="sxs-lookup"><span data-stu-id="c7813-178">LastName</span></span> | <span data-ttu-id="c7813-179">User.surname</span><span class="sxs-lookup"><span data-stu-id="c7813-179">user.surname</span></span> |
    | <span data-ttu-id="c7813-180">Adres e-mail</span><span class="sxs-lookup"><span data-stu-id="c7813-180">Email</span></span> | <span data-ttu-id="c7813-181">User.mail</span><span class="sxs-lookup"><span data-stu-id="c7813-181">user.mail</span></span> |    
    | <span data-ttu-id="c7813-182">Tożsamości użytkownika</span><span class="sxs-lookup"><span data-stu-id="c7813-182">UserIdentity</span></span> | <span data-ttu-id="c7813-183">User.mail</span><span class="sxs-lookup"><span data-stu-id="c7813-183">user.mail</span></span> |
    
    <span data-ttu-id="c7813-184">a.</span><span class="sxs-lookup"><span data-stu-id="c7813-184">a.</span></span> <span data-ttu-id="c7813-185">Kliknij przycisk **Dodaj atrybut** otworzyć **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c7813-185">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_04.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="c7813-188">b.</span><span class="sxs-lookup"><span data-stu-id="c7813-188">b.</span></span> <span data-ttu-id="c7813-189">W **nazwa** tekstowym, wpisz nazwę atrybut wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="c7813-189">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="c7813-190">c.</span><span class="sxs-lookup"><span data-stu-id="c7813-190">c.</span></span> <span data-ttu-id="c7813-191">Z **wartość** listy, wpisz wartość atrybutu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="c7813-191">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="c7813-192">d.</span><span class="sxs-lookup"><span data-stu-id="c7813-192">d.</span></span> <span data-ttu-id="c7813-193">Pozostaw **Namespace** puste.</span><span class="sxs-lookup"><span data-stu-id="c7813-193">Leave the **Namespace** blank.</span></span>
    
    <span data-ttu-id="c7813-194">e.</span><span class="sxs-lookup"><span data-stu-id="c7813-194">e.</span></span> <span data-ttu-id="c7813-195">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="c7813-195">Click **Ok**.</span></span>

7. <span data-ttu-id="c7813-196">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c7813-196">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hightail-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="c7813-198">Na **Hightail konfiguracji** kliknij **skonfigurować Hightail** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="c7813-198">On the **Hightail Configuration** section, click **Configure Hightail** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c7813-199">Kopiuj **SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="c7813-199">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_configure.png) 

    >[!NOTE] 
    ><span data-ttu-id="c7813-201">Przed rozpoczęciem konfigurowania rejestracji jednokrotnej w aplikacji Hightail, skontaktuj się z białą listę domenę poczty e-mail z Hightail zespołu, aby wszyscy użytkownicy, którzy korzystają z tej domeny można używać funkcji rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="c7813-201">Before configuring the Single Sign On at Hightail app, please white list your email domain with Hightail team so that all the users who are using this domain can use Single Sign On functionality.</span></span>


9. <span data-ttu-id="c7813-202">Aby uzyskać logowania jednokrotnego skonfigurowane dla aplikacji, należy logowania jednokrotnego dla Twojej dzierżawy Hightail jako administrator.</span><span class="sxs-lookup"><span data-stu-id="c7813-202">To get SSO configured for your application, you need to sign-on to your Hightail tenant as an administrator.</span></span>
   
    <span data-ttu-id="c7813-203">a.</span><span class="sxs-lookup"><span data-stu-id="c7813-203">a.</span></span> <span data-ttu-id="c7813-204">W menu u góry kliknij **konta** i wybierz **skonfigurować SAML**.</span><span class="sxs-lookup"><span data-stu-id="c7813-204">In the menu on the top, click the **Account** tab and select **Configure SAML**.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_001.png) 

    <span data-ttu-id="c7813-206">b.</span><span class="sxs-lookup"><span data-stu-id="c7813-206">b.</span></span> <span data-ttu-id="c7813-207">Zaznacz pole wyboru z **Włącz uwierzytelnianie SAML**.</span><span class="sxs-lookup"><span data-stu-id="c7813-207">Select the checkbox of **Enable SAML Authentication**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_002.png) 

    <span data-ttu-id="c7813-209">c.</span><span class="sxs-lookup"><span data-stu-id="c7813-209">c.</span></span> <span data-ttu-id="c7813-210">Otwórz w Notatniku pobrany z portalu Azure certyfikatu zakodowanego base-64, skopiuj zawartość go do Schowka, a następnie wklej go do **SAML certyfikat podpisywania tokenu** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="c7813-210">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **SAML Token Signing Certificate** textbox.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_003.png) 

    <span data-ttu-id="c7813-212">d.</span><span class="sxs-lookup"><span data-stu-id="c7813-212">d.</span></span> <span data-ttu-id="c7813-213">W **SAML urzędu (dostawcy tożsamości)** pole tekstowe, Wklej wartość **SAML pojedynczy znak na adres URL usługi** skopiowany z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c7813-213">In the **SAML Authority (Identity Provider)** textbox, paste the value of **SAML Single Sign-On Service URL** copied from Azure portal.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_004.png)

    <span data-ttu-id="c7813-215">e.</span><span class="sxs-lookup"><span data-stu-id="c7813-215">e.</span></span> <span data-ttu-id="c7813-216">Jeśli chcesz skonfigurować aplikację w **IDP zainicjował tryb** wybierz **"Dostawcy tożsamości (IdP) zainicjował logowania"**.</span><span class="sxs-lookup"><span data-stu-id="c7813-216">If you wish to configure the application in **IDP initiated mode** select **"Identity Provider (IdP) initiated log in"**.</span></span> <span data-ttu-id="c7813-217">Jeśli **SP zainicjował tryb** wybierz **"Dostawcy usług (SP) zainicjował logowania"**.</span><span class="sxs-lookup"><span data-stu-id="c7813-217">If **SP initiated mode** select **"Service Provider (SP) initiated log in"**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_006.png)

    <span data-ttu-id="c7813-219">f.</span><span class="sxs-lookup"><span data-stu-id="c7813-219">f.</span></span> <span data-ttu-id="c7813-220">Skopiuj adres URL klienta SAML dla swojego wystąpienia, a następnie wklej je **adres URL odpowiedzi** textbox w **Hightail domeny i adres URL** sekcji z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c7813-220">Copy the SAML consumer URL for your instance and paste it in **Reply URL** textbox in **Hightail Domain and URLs** section on Azure portal.</span></span>
    
    <span data-ttu-id="c7813-221">g.</span><span class="sxs-lookup"><span data-stu-id="c7813-221">g.</span></span> <span data-ttu-id="c7813-222">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="c7813-222">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="c7813-223">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="c7813-223">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c7813-224">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="c7813-224">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c7813-225">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c7813-225">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c7813-226">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7813-226">Creating an Azure AD test user</span></span>
<span data-ttu-id="c7813-227">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="c7813-227">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="c7813-229">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c7813-229">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c7813-230">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="c7813-230">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c7813-232">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="c7813-232">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c7813-234">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c7813-234">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c7813-236">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c7813-236">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c7813-238">a.</span><span class="sxs-lookup"><span data-stu-id="c7813-238">a.</span></span> <span data-ttu-id="c7813-239">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c7813-239">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c7813-240">b.</span><span class="sxs-lookup"><span data-stu-id="c7813-240">b.</span></span> <span data-ttu-id="c7813-241">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c7813-241">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c7813-242">c.</span><span class="sxs-lookup"><span data-stu-id="c7813-242">c.</span></span> <span data-ttu-id="c7813-243">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="c7813-243">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c7813-244">d.</span><span class="sxs-lookup"><span data-stu-id="c7813-244">d.</span></span> <span data-ttu-id="c7813-245">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="c7813-245">Click **Create**.</span></span>
 
### <a name="creating-a-hightail-test-user"></a><span data-ttu-id="c7813-246">Tworzenie użytkownika testowego Hightail</span><span class="sxs-lookup"><span data-stu-id="c7813-246">Creating a Hightail test user</span></span>

<span data-ttu-id="c7813-247">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w Hightail.</span><span class="sxs-lookup"><span data-stu-id="c7813-247">The objective of this section is to create a user called Britta Simon in Hightail.</span></span> 

<span data-ttu-id="c7813-248">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="c7813-248">There is no action item for you in this section.</span></span> <span data-ttu-id="c7813-249">Hightail obsługuje użytkownika w czasie inicjowania obsługi na podstawie niestandardowych oświadczeń.</span><span class="sxs-lookup"><span data-stu-id="c7813-249">Hightail supports just-in-time user provisioning based on the custom claims.</span></span> <span data-ttu-id="c7813-250">Jeśli skonfigurowano niestandardowe oświadczenia, jak pokazano w sekcji  **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  powyżej, użytkownik zostanie automatycznie utworzone w aplikacji nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="c7813-250">If you have configured the custom claims as shown in the section **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** above, a user is automatically created in the application it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="c7813-251">Jeśli trzeba ręcznie utworzyć użytkownika, należy skontaktować się [zespołem pomocy technicznej Hightail](mailto:support@hightail.com).</span><span class="sxs-lookup"><span data-stu-id="c7813-251">If you need to create a user manually, you need to contact the [Hightail support team](mailto:support@hightail.com).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c7813-252">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7813-252">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c7813-253">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Hightail.</span><span class="sxs-lookup"><span data-stu-id="c7813-253">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Hightail.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="c7813-255">**Aby przypisać Simona Britta Hightail, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c7813-255">**To assign Britta Simon to Hightail, perform the following steps:**</span></span>

1. <span data-ttu-id="c7813-256">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="c7813-256">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="c7813-258">Na liście aplikacji zaznacz **Hightail**.</span><span class="sxs-lookup"><span data-stu-id="c7813-258">In the applications list, select **Hightail**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_app.png) 

3. <span data-ttu-id="c7813-260">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="c7813-260">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="c7813-262">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c7813-262">Click **Add** button.</span></span> <span data-ttu-id="c7813-263">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c7813-263">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="c7813-265">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="c7813-265">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c7813-266">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c7813-266">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c7813-267">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c7813-267">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c7813-268">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="c7813-268">Testing single sign-on</span></span>

<span data-ttu-id="c7813-269">Celem tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="c7813-269">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c7813-270">Po kliknięciu kafelka Hightail w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Hightail.</span><span class="sxs-lookup"><span data-stu-id="c7813-270">When you click the Hightail tile in the Access Panel, you should get automatically signed-on to your Hightail application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="c7813-271">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="c7813-271">Additional resources</span></span>

* [<span data-ttu-id="c7813-272">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c7813-272">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c7813-273">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c7813-273">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_203.png

