---
title: 'Samouczek: Integracji Azure Active Directory z myPolicies | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i myPolicies."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bf79e858-1dfb-4ab3-a6df-74b2d5a878d2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: jeedes
ms.openlocfilehash: fcb403041cb3a8bd20ff7b34aa5cc4b7bf0c0a16
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mypolicies"></a><span data-ttu-id="2bc78-103">Samouczek: Integracji Azure Active Directory z myPolicies</span><span class="sxs-lookup"><span data-stu-id="2bc78-103">Tutorial: Azure Active Directory integration with myPolicies</span></span>

<span data-ttu-id="2bc78-104">Z tego samouczka dowiesz się integrowanie myPolicies z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2bc78-104">In this tutorial, you learn how to integrate myPolicies with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2bc78-105">Integracja z usługą Azure AD myPolicies zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="2bc78-105">Integrating myPolicies with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2bc78-106">Można kontrolować w usłudze Azure AD, który ma dostęp do myPolicies</span><span class="sxs-lookup"><span data-stu-id="2bc78-106">You can control in Azure AD who has access to myPolicies</span></span>
- <span data-ttu-id="2bc78-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do myPolicies (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="2bc78-107">You can enable your users to automatically get signed-on to myPolicies (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2bc78-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="2bc78-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="2bc78-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2bc78-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2bc78-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2bc78-110">Prerequisites</span></span>

<span data-ttu-id="2bc78-111">Aby skonfigurować integrację usługi Azure AD z myPolicies, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="2bc78-111">To configure Azure AD integration with myPolicies, you need the following items:</span></span>

- <span data-ttu-id="2bc78-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="2bc78-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2bc78-113">MyPolicies logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="2bc78-113">A myPolicies single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2bc78-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="2bc78-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2bc78-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="2bc78-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2bc78-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="2bc78-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2bc78-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2bc78-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2bc78-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="2bc78-118">Scenario description</span></span>
<span data-ttu-id="2bc78-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="2bc78-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2bc78-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="2bc78-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2bc78-121">Dodawanie myPolicies z galerii</span><span class="sxs-lookup"><span data-stu-id="2bc78-121">Adding myPolicies from the gallery</span></span>
2. <span data-ttu-id="2bc78-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="2bc78-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mypolicies-from-the-gallery"></a><span data-ttu-id="2bc78-123">Dodawanie myPolicies z galerii</span><span class="sxs-lookup"><span data-stu-id="2bc78-123">Adding myPolicies from the gallery</span></span>
<span data-ttu-id="2bc78-124">Aby skonfigurować integrację usługi Azure AD myPolicies, należy dodać myPolicies z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="2bc78-124">To configure the integration of myPolicies into Azure AD, you need to add myPolicies from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2bc78-125">**Aby dodać myPolicies z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="2bc78-125">**To add myPolicies from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2bc78-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="2bc78-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="2bc78-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="2bc78-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2bc78-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="2bc78-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="2bc78-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2bc78-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="2bc78-133">W polu wyszukiwania wpisz **myPolicies**.</span><span class="sxs-lookup"><span data-stu-id="2bc78-133">In the search box, type **myPolicies**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_search.png)

5. <span data-ttu-id="2bc78-135">W panelu wyników wybierz **myPolicies**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="2bc78-135">In the results panel, select **myPolicies**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2bc78-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="2bc78-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2bc78-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z myPolicies w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="2bc78-138">In this section, you configure and test Azure AD single sign-on with myPolicies based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2bc78-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w myPolicies jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2bc78-139">For single sign-on to work, Azure AD needs to know what the counterpart user in myPolicies is to a user in Azure AD.</span></span> <span data-ttu-id="2bc78-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w myPolicies musi się.</span><span class="sxs-lookup"><span data-stu-id="2bc78-140">In other words, a link relationship between an Azure AD user and the related user in myPolicies needs to be established.</span></span>

<span data-ttu-id="2bc78-141">W myPolicies, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="2bc78-141">In myPolicies, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="2bc78-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z myPolicies, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="2bc78-142">To configure and test Azure AD single sign-on with myPolicies, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2bc78-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="2bc78-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2bc78-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="2bc78-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2bc78-145">**[Tworzenie użytkownika testowego myPolicies](#creating-a-mypolicies-test-user)**  — mają odpowiednika Simona Britta w myPolicies połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2bc78-145">**[Creating a myPolicies test user](#creating-a-mypolicies-test-user)** - to have a counterpart of Britta Simon in myPolicies that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="2bc78-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="2bc78-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2bc78-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="2bc78-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2bc78-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="2bc78-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2bc78-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji myPolicies.</span><span class="sxs-lookup"><span data-stu-id="2bc78-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your myPolicies application.</span></span>

<span data-ttu-id="2bc78-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z myPolicies, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="2bc78-150">**To configure Azure AD single sign-on with myPolicies, perform the following steps:**</span></span>

1. <span data-ttu-id="2bc78-151">W portalu Azure na **myPolicies** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="2bc78-151">In the Azure portal, on the **myPolicies** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="2bc78-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="2bc78-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_samlbase.png)

3. <span data-ttu-id="2bc78-155">Na **myPolicies domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="2bc78-155">On the **myPolicies Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_url.png)

    <span data-ttu-id="2bc78-157">a.</span><span class="sxs-lookup"><span data-stu-id="2bc78-157">a.</span></span> <span data-ttu-id="2bc78-158">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<tenantname>.mypolicies.com/`</span><span class="sxs-lookup"><span data-stu-id="2bc78-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenantname>.mypolicies.com/`</span></span>

    <span data-ttu-id="2bc78-159">b.</span><span class="sxs-lookup"><span data-stu-id="2bc78-159">b.</span></span> <span data-ttu-id="2bc78-160">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<tenantname>.mypolicies.com/users/auth/saml/callback`</span><span class="sxs-lookup"><span data-stu-id="2bc78-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<tenantname>.mypolicies.com/users/auth/saml/callback`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2bc78-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="2bc78-161">These values are not real.</span></span> <span data-ttu-id="2bc78-162">Rzeczywisty identyfikator i adres URL odpowiedzi, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="2bc78-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="2bc78-163">Skontaktuj się z [myPolicies obsługuje zespołu](mailto:support@mypolicies.com) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="2bc78-163">Contact [myPolicies support team](mailto:support@mypolicies.com) to get these values.</span></span>

4. <span data-ttu-id="2bc78-164">Aplikacja myPolicies oczekuje potwierdzenia języka SAML w określonym formacie, musisz dodać mapowania atrybutu niestandardowego do konfiguracji atrybuty tokenu SAML.</span><span class="sxs-lookup"><span data-stu-id="2bc78-164">The myPolicies application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="2bc78-165">Skonfiguruj następujące oświadczeń dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2bc78-165">Configure the following claims for this application.</span></span> <span data-ttu-id="2bc78-166">Możesz zarządzać wartości tych atrybutów z "**atrybuty użytkownika**" sekcji na stronie integracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2bc78-166">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="2bc78-167">Poniższy zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="2bc78-167">The following screenshot shows an example for this.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_attribute.png)

5. <span data-ttu-id="2bc78-169">Kliknij przycisk **widoku i edytować wszystkie atrybuty użytkowników** checkbox w **atrybuty użytkownika** sekcji, aby rozwinąć atrybutów.</span><span class="sxs-lookup"><span data-stu-id="2bc78-169">Click **View and edit all other user attributes** checkbox in the **User Attributes** section to expand the attributes.</span></span> <span data-ttu-id="2bc78-170">Wykonaj poniższe kroki na każdym z atrybutów wyświetlanych-</span><span class="sxs-lookup"><span data-stu-id="2bc78-170">Perform the following steps on each of the displayed attributes-</span></span>

    | <span data-ttu-id="2bc78-171">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="2bc78-171">Attribute Name</span></span> | <span data-ttu-id="2bc78-172">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="2bc78-172">Attribute Value</span></span> |
    | ------------------- | ---------- |
    | <span data-ttu-id="2bc78-173">Imię</span><span class="sxs-lookup"><span data-stu-id="2bc78-173">givenname</span></span> | <span data-ttu-id="2bc78-174">User.givenName</span><span class="sxs-lookup"><span data-stu-id="2bc78-174">user.givenname</span></span> |
    | <span data-ttu-id="2bc78-175">nazwisko</span><span class="sxs-lookup"><span data-stu-id="2bc78-175">surname</span></span> | <span data-ttu-id="2bc78-176">User.surname</span><span class="sxs-lookup"><span data-stu-id="2bc78-176">user.surname</span></span> |
    | <span data-ttu-id="2bc78-177">emailaddress</span><span class="sxs-lookup"><span data-stu-id="2bc78-177">emailaddress</span></span> | <span data-ttu-id="2bc78-178">User.mail</span><span class="sxs-lookup"><span data-stu-id="2bc78-178">user.mail</span></span> |
    | <span data-ttu-id="2bc78-179">name</span><span class="sxs-lookup"><span data-stu-id="2bc78-179">name</span></span> | <span data-ttu-id="2bc78-180">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="2bc78-180">user.userprincipalname</span></span> |
    
    <span data-ttu-id="2bc78-181">a.</span><span class="sxs-lookup"><span data-stu-id="2bc78-181">a.</span></span> <span data-ttu-id="2bc78-182">Kliknij ten atrybut można otworzyć **atrybutu Edytuj** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2bc78-182">Click on the attribute to open the **Edit Attribute** dialog.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mypolicies-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="2bc78-184">b.</span><span class="sxs-lookup"><span data-stu-id="2bc78-184">b.</span></span> <span data-ttu-id="2bc78-185">Usuń wartość adresu URL z **Namespace**.</span><span class="sxs-lookup"><span data-stu-id="2bc78-185">Delete the URL value from the **Namespace**.</span></span>
    
    <span data-ttu-id="2bc78-186">c.</span><span class="sxs-lookup"><span data-stu-id="2bc78-186">c.</span></span> <span data-ttu-id="2bc78-187">Kliknij przycisk **Ok** Aby zapisać ustawienia.</span><span class="sxs-lookup"><span data-stu-id="2bc78-187">Click **Ok** to save the setting.</span></span>
    
6. <span data-ttu-id="2bc78-188">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="2bc78-188">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_certificate.png) 

7. <span data-ttu-id="2bc78-190">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="2bc78-190">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mypolicies-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="2bc78-192">Na **myPolicies konfiguracji** kliknij **skonfigurować myPolicies** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="2bc78-192">On the **myPolicies Configuration** section, click **Configure myPolicies** to open **Configure sign-on** window.</span></span> <span data-ttu-id="2bc78-193">Kopiuj **SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="2bc78-193">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_configure.png) 

9. <span data-ttu-id="2bc78-195">Aby skonfigurować logowanie jednokrotne w **myPolicies** stronie, musisz wysłać pobrany **Certificate(Base64)** i **SAML pojedynczy znak na adres URL usługi** do [ myPolicies obsługuje zespołu](mailto:support@mypolicies.com).</span><span class="sxs-lookup"><span data-stu-id="2bc78-195">To configure single sign-on on **myPolicies** side, you need to send the downloaded **Certificate(Base64)** and **SAML Single Sign-On Service URL** to [myPolicies support team](mailto:support@mypolicies.com).</span></span> 

> [!TIP]
> <span data-ttu-id="2bc78-196">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="2bc78-196">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2bc78-197">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="2bc78-197">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2bc78-198">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2bc78-198">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2bc78-199">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="2bc78-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="2bc78-200">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="2bc78-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="2bc78-202">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="2bc78-202">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2bc78-203">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="2bc78-203">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2bc78-205">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="2bc78-205">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2bc78-207">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2bc78-207">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2bc78-209">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="2bc78-209">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2bc78-211">a.</span><span class="sxs-lookup"><span data-stu-id="2bc78-211">a.</span></span> <span data-ttu-id="2bc78-212">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2bc78-212">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2bc78-213">b.</span><span class="sxs-lookup"><span data-stu-id="2bc78-213">b.</span></span> <span data-ttu-id="2bc78-214">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2bc78-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2bc78-215">c.</span><span class="sxs-lookup"><span data-stu-id="2bc78-215">c.</span></span> <span data-ttu-id="2bc78-216">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="2bc78-216">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2bc78-217">d.</span><span class="sxs-lookup"><span data-stu-id="2bc78-217">d.</span></span> <span data-ttu-id="2bc78-218">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="2bc78-218">Click **Create**.</span></span>
 
### <a name="creating-a-mypolicies-test-user"></a><span data-ttu-id="2bc78-219">Tworzenie użytkownika testowego myPolicies</span><span class="sxs-lookup"><span data-stu-id="2bc78-219">Creating a myPolicies test user</span></span>

<span data-ttu-id="2bc78-220">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w myPolicies.</span><span class="sxs-lookup"><span data-stu-id="2bc78-220">In this section, you create a user called Britta Simon in myPolicies.</span></span> <span data-ttu-id="2bc78-221">Praca z [myPolicies obsługuje zespołu](mailto:support@mypolicies.com) Aby dodać użytkowników do platformy myPolicies.</span><span class="sxs-lookup"><span data-stu-id="2bc78-221">Work with [myPolicies support team](mailto:support@mypolicies.com) to add the users in the myPolicies platform.</span></span> <span data-ttu-id="2bc78-222">Użytkownicy muszą utworzyć i aktywowana, aby użyć rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="2bc78-222">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2bc78-223">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="2bc78-223">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2bc78-224">W tej sekcji musisz włączyć Simona Britta do użycia usługi Azure logowania jednokrotnego za udzielanie dostępu do myPolicies.</span><span class="sxs-lookup"><span data-stu-id="2bc78-224">In this section, you enable Britta Simon to use Azure single sign-on by granting access to myPolicies.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="2bc78-226">**Aby przypisać Simona Britta myPolicies, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="2bc78-226">**To assign Britta Simon to myPolicies, perform the following steps:**</span></span>

1. <span data-ttu-id="2bc78-227">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="2bc78-227">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="2bc78-229">Na liście aplikacji zaznacz **myPolicies**.</span><span class="sxs-lookup"><span data-stu-id="2bc78-229">In the applications list, select **myPolicies**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_app.png) 

3. <span data-ttu-id="2bc78-231">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="2bc78-231">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="2bc78-233">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="2bc78-233">Click **Add** button.</span></span> <span data-ttu-id="2bc78-234">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2bc78-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="2bc78-236">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="2bc78-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2bc78-237">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2bc78-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2bc78-238">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2bc78-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2bc78-239">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="2bc78-239">Testing single sign-on</span></span>

<span data-ttu-id="2bc78-240">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="2bc78-240">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2bc78-241">Po kliknięciu kafelka myPolicies w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji myPolicies.</span><span class="sxs-lookup"><span data-stu-id="2bc78-241">When you click the myPolicies tile in the Access Panel, you should get automatically signed-on to your myPolicies application.</span></span>
<span data-ttu-id="2bc78-242">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2bc78-242">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2bc78-243">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="2bc78-243">Additional resources</span></span>

* [<span data-ttu-id="2bc78-244">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2bc78-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2bc78-245">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2bc78-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_203.png

