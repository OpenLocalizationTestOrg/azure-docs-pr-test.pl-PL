---
title: 'Samouczek: Integracji Azure Active Directory z Allocadia | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Allocadia."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c415fc55-6dc1-49f2-a8a2-2fc6e3790d65
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: jeedes
ms.openlocfilehash: 8e97c365383ecdb72cc1cd449b522b75875fc1db
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-allocadia"></a><span data-ttu-id="44160-103">Samouczek: Integracji Azure Active Directory z Allocadia</span><span class="sxs-lookup"><span data-stu-id="44160-103">Tutorial: Azure Active Directory integration with Allocadia</span></span>

<span data-ttu-id="44160-104">Z tego samouczka dowiesz się integrowanie Allocadia z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="44160-104">In this tutorial, you learn how to integrate Allocadia with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="44160-105">Integracja z usługą Azure AD Allocadia zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="44160-105">Integrating Allocadia with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="44160-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Allocadia</span><span class="sxs-lookup"><span data-stu-id="44160-106">You can control in Azure AD who has access to Allocadia</span></span>
- <span data-ttu-id="44160-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Allocadia (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="44160-107">You can enable your users to automatically get signed-on to Allocadia (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="44160-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="44160-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="44160-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="44160-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44160-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="44160-110">Prerequisites</span></span>

<span data-ttu-id="44160-111">Aby skonfigurować integrację usługi Azure AD z Allocadia, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="44160-111">To configure Azure AD integration with Allocadia, you need the following items:</span></span>

- <span data-ttu-id="44160-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="44160-112">An Azure AD subscription</span></span>
- <span data-ttu-id="44160-113">Allocadia jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="44160-113">An Allocadia single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="44160-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="44160-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="44160-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="44160-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="44160-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="44160-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="44160-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="44160-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="44160-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="44160-118">Scenario description</span></span>
<span data-ttu-id="44160-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="44160-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="44160-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="44160-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="44160-121">Dodawanie Allocadia z galerii</span><span class="sxs-lookup"><span data-stu-id="44160-121">Adding Allocadia from the gallery</span></span>
2. <span data-ttu-id="44160-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="44160-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-allocadia-from-the-gallery"></a><span data-ttu-id="44160-123">Dodawanie Allocadia z galerii</span><span class="sxs-lookup"><span data-stu-id="44160-123">Adding Allocadia from the gallery</span></span>
<span data-ttu-id="44160-124">Aby skonfigurować integrację usługi Azure AD Allocadia, należy dodać Allocadia z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="44160-124">To configure the integration of Allocadia into Azure AD, you need to add Allocadia from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="44160-125">**Aby dodać Allocadia z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="44160-125">**To add Allocadia from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="44160-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="44160-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="44160-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="44160-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="44160-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="44160-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="44160-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="44160-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="44160-133">W polu wyszukiwania wpisz **Allocadia**.</span><span class="sxs-lookup"><span data-stu-id="44160-133">In the search box, type **Allocadia**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_search.png)

5. <span data-ttu-id="44160-135">W panelu wyników wybierz **Allocadia**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="44160-135">In the results panel, select **Allocadia**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="44160-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="44160-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="44160-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Allocadia na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="44160-138">In this section, you configure and test Azure AD single sign-on with Allocadia based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="44160-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Allocadia jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="44160-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Allocadia is to a user in Azure AD.</span></span> <span data-ttu-id="44160-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Allocadia musi się.</span><span class="sxs-lookup"><span data-stu-id="44160-140">In other words, a link relationship between an Azure AD user and the related user in Allocadia needs to be established.</span></span>

<span data-ttu-id="44160-141">W Allocadia, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="44160-141">In Allocadia, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="44160-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Allocadia, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="44160-142">To configure and test Azure AD single sign-on with Allocadia, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="44160-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="44160-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="44160-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="44160-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="44160-145">**[Tworzenie użytkownika testowego Allocadia](#creating-an-allocadia-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Allocadia połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="44160-145">**[Creating an Allocadia test user](#creating-an-allocadia-test-user)** - to have a counterpart of Britta Simon in Allocadia that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="44160-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="44160-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="44160-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="44160-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="44160-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="44160-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="44160-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Allocadia.</span><span class="sxs-lookup"><span data-stu-id="44160-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Allocadia application.</span></span>

<span data-ttu-id="44160-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Allocadia, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="44160-150">**To configure Azure AD single sign-on with Allocadia, perform the following steps:**</span></span>

1. <span data-ttu-id="44160-151">W portalu Azure na **Allocadia** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="44160-151">In the Azure portal, on the **Allocadia** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="44160-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="44160-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_samlbase.png)

3. <span data-ttu-id="44160-155">Na **Allocadia domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="44160-155">On the **Allocadia Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_url.png)

    <span data-ttu-id="44160-157">a.</span><span class="sxs-lookup"><span data-stu-id="44160-157">a.</span></span> <span data-ttu-id="44160-158">W **identyfikator** tekstowym, wpisz adres URL za pomocą następujących wzorców:</span><span class="sxs-lookup"><span data-stu-id="44160-158">In the **Identifier** textbox, type a URL using the following patterns:</span></span> 
       
     <span data-ttu-id="44160-159">Dla środowiska testowego-`https://na2standby.allocadia.com`</span><span class="sxs-lookup"><span data-stu-id="44160-159">For test environment -  `https://na2standby.allocadia.com`</span></span>
    
     <span data-ttu-id="44160-160">W środowisku produkcyjnym —`https://na2.allocadia.com`</span><span class="sxs-lookup"><span data-stu-id="44160-160">For production environment - `https://na2.allocadia.com`</span></span>

    <span data-ttu-id="44160-161">b.</span><span class="sxs-lookup"><span data-stu-id="44160-161">b.</span></span> <span data-ttu-id="44160-162">W **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą następujących wzorców:</span><span class="sxs-lookup"><span data-stu-id="44160-162">In the **Reply URL** textbox, type a URL using the following patterns:</span></span> 
    
     <span data-ttu-id="44160-163">Dla środowiska testowego-`https://na2standby.allocadia.com/allocadia/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="44160-163">For test environment - `https://na2standby.allocadia.com/allocadia/saml/SSO`</span></span>
    
     <span data-ttu-id="44160-164">W środowisku produkcyjnym —`https://na2.allocadia.com/allocadia/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="44160-164">For production environment - `https://na2.allocadia.com/allocadia/saml/SSO`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="44160-165">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="44160-165">These values are not real.</span></span> <span data-ttu-id="44160-166">Rzeczywisty identyfikator i adres URL odpowiedzi, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="44160-166">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="44160-167">Skontaktuj się z [zespołem pomocy technicznej Allocadia](mailTo:support@allocadia.com) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="44160-167">Contact [Allocadia support team](mailTo:support@allocadia.com) to get these values.</span></span>

4. <span data-ttu-id="44160-168">Aplikacja Allocadia oczekuje potwierdzenia języka SAML w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="44160-168">Allocadia application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="44160-169">Skonfiguruj następujące oświadczeń dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="44160-169">Configure the following claims for this application.</span></span> <span data-ttu-id="44160-170">Możesz zarządzać wartości tych atrybutów z "**atrybuty użytkownika**" sekcji na stronie integracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="44160-170">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="44160-171">Poniższy zrzut ekranu przedstawia przykład dla tej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="44160-171">The following screenshot shows an example for this configuration.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_attributes.png)
    
5. <span data-ttu-id="44160-173">W **atrybuty użytkownika** sekcji na **logowanie jednokrotne** okna dialogowego, skonfiguruj atrybut tokenu SAML, jak pokazano w obrazie i wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="44160-173">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="44160-174">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="44160-174">Attribute Name</span></span> | <span data-ttu-id="44160-175">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="44160-175">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="44160-176">Imię</span><span class="sxs-lookup"><span data-stu-id="44160-176">firstname</span></span> | <span data-ttu-id="44160-177">User.givenName</span><span class="sxs-lookup"><span data-stu-id="44160-177">user.givenname</span></span> |
    | <span data-ttu-id="44160-178">nazwisko</span><span class="sxs-lookup"><span data-stu-id="44160-178">lastname</span></span> | <span data-ttu-id="44160-179">User.surname</span><span class="sxs-lookup"><span data-stu-id="44160-179">user.surname</span></span> |
    | <span data-ttu-id="44160-180">Adres e-mail</span><span class="sxs-lookup"><span data-stu-id="44160-180">email</span></span> | <span data-ttu-id="44160-181">User.mail</span><span class="sxs-lookup"><span data-stu-id="44160-181">user.mail</span></span> |
    
    <span data-ttu-id="44160-182">a.</span><span class="sxs-lookup"><span data-stu-id="44160-182">a.</span></span> <span data-ttu-id="44160-183">Kliknij przycisk **Dodaj atrybut** otworzyć **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="44160-183">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-allocadia-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="44160-185">b.</span><span class="sxs-lookup"><span data-stu-id="44160-185">b.</span></span> <span data-ttu-id="44160-186">W **nazwa** tekstowym, wpisz nazwę atrybut wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="44160-186">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-allocadia-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="44160-188">c.</span><span class="sxs-lookup"><span data-stu-id="44160-188">c.</span></span> <span data-ttu-id="44160-189">Z **wartość** listy, wpisz wartość atrybutu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="44160-189">From the **Value** list, type the attribute value shown for that row.</span></span>
 
    <span data-ttu-id="44160-190">d.</span><span class="sxs-lookup"><span data-stu-id="44160-190">d.</span></span> <span data-ttu-id="44160-191">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="44160-191">Click **Ok**.</span></span>



6. <span data-ttu-id="44160-192">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="44160-192">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_certificate.png) 


7. <span data-ttu-id="44160-194">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="44160-194">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-allocadia-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="44160-196">Skonfigurować logowanie jednokrotne w **Allocadia** stronie, musisz wysłać pobrany **XML metadanych** do [zespołem pomocy technicznej Allocadia](mailTo:support@allocadia.com).</span><span class="sxs-lookup"><span data-stu-id="44160-196">To configure single sign-on on **Allocadia** side, you need to send the downloaded **Metadata XML** to [Allocadia support team](mailTo:support@allocadia.com).</span></span> <span data-ttu-id="44160-197">To ustawienie, aby były prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one wartość.</span><span class="sxs-lookup"><span data-stu-id="44160-197">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="44160-198">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="44160-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="44160-199">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="44160-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="44160-200">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="44160-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="44160-201">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="44160-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="44160-202">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="44160-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="44160-204">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="44160-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="44160-205">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="44160-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-allocadia-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="44160-207">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="44160-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-allocadia-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="44160-209">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="44160-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-allocadia-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="44160-211">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="44160-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-allocadia-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="44160-213">a.</span><span class="sxs-lookup"><span data-stu-id="44160-213">a.</span></span> <span data-ttu-id="44160-214">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="44160-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="44160-215">b.</span><span class="sxs-lookup"><span data-stu-id="44160-215">b.</span></span> <span data-ttu-id="44160-216">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="44160-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="44160-217">c.</span><span class="sxs-lookup"><span data-stu-id="44160-217">c.</span></span> <span data-ttu-id="44160-218">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="44160-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="44160-219">d.</span><span class="sxs-lookup"><span data-stu-id="44160-219">d.</span></span> <span data-ttu-id="44160-220">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="44160-220">Click **Create**.</span></span>
 
### <a name="creating-an-allocadia-test-user"></a><span data-ttu-id="44160-221">Tworzenie użytkownika testowego Allocadia</span><span class="sxs-lookup"><span data-stu-id="44160-221">Creating an Allocadia test user</span></span>

<span data-ttu-id="44160-222">Aplikacja obsługuje tylko w czasie Inicjowanie obsługi użytkowników.</span><span class="sxs-lookup"><span data-stu-id="44160-222">Application supports Just in time user provisioning.</span></span> <span data-ttu-id="44160-223">Po uwierzytelnieniu użytkownicy są automatycznie tworzone w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="44160-223">After authentication users are created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="44160-224">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="44160-224">Assigning the Azure AD test user</span></span>

<span data-ttu-id="44160-225">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Allocadia.</span><span class="sxs-lookup"><span data-stu-id="44160-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Allocadia.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="44160-227">**Aby przypisać Simona Britta Allocadia, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="44160-227">**To assign Britta Simon to Allocadia, perform the following steps:**</span></span>

1. <span data-ttu-id="44160-228">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="44160-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="44160-230">Na liście aplikacji zaznacz **Allocadia**.</span><span class="sxs-lookup"><span data-stu-id="44160-230">In the applications list, select **Allocadia**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_app.png) 

3. <span data-ttu-id="44160-232">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="44160-232">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="44160-234">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="44160-234">Click **Add** button.</span></span> <span data-ttu-id="44160-235">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="44160-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="44160-237">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="44160-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="44160-238">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="44160-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="44160-239">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="44160-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="44160-240">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="44160-240">Testing single sign-on</span></span>

<span data-ttu-id="44160-241">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="44160-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="44160-242">Po kliknięciu kafelka Allocadia w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Allocadia.</span><span class="sxs-lookup"><span data-stu-id="44160-242">When you click the Allocadia tile in the Access Panel, you should get automatically signed-on to your Allocadia application.</span></span>
<span data-ttu-id="44160-243">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="44160-243">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="44160-244">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="44160-244">Additional resources</span></span>

* [<span data-ttu-id="44160-245">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="44160-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="44160-246">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="44160-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_203.png

