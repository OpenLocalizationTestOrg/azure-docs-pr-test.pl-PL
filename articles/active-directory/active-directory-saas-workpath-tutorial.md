---
title: 'Samouczek: Integracji Azure Active Directory z Workpath | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Workpath."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 320b0daf-14be-4813-b59b-25a6a5070690
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: f4efa56d2c0374a977c1e46dad64b596cc9c3ea8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workpath"></a><span data-ttu-id="31d6e-103">Samouczek: Integracji Azure Active Directory z Workpath</span><span class="sxs-lookup"><span data-stu-id="31d6e-103">Tutorial: Azure Active Directory integration with Workpath</span></span>

<span data-ttu-id="31d6e-104">Z tego samouczka dowiesz się integrowanie Workpath z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="31d6e-104">In this tutorial, you learn how to integrate Workpath with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="31d6e-105">Integracja z usługą Azure AD Workpath zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="31d6e-105">Integrating Workpath with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="31d6e-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Workpath</span><span class="sxs-lookup"><span data-stu-id="31d6e-106">You can control in Azure AD who has access to Workpath</span></span>
- <span data-ttu-id="31d6e-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Workpath (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="31d6e-107">You can enable your users to automatically get signed-on to Workpath (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="31d6e-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="31d6e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="31d6e-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="31d6e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="31d6e-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="31d6e-110">Prerequisites</span></span>

<span data-ttu-id="31d6e-111">Aby skonfigurować integrację usługi Azure AD z Workpath, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="31d6e-111">To configure Azure AD integration with Workpath, you need the following items:</span></span>

- <span data-ttu-id="31d6e-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="31d6e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="31d6e-113">Workpath jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="31d6e-113">A Workpath single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="31d6e-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="31d6e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="31d6e-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="31d6e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="31d6e-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="31d6e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="31d6e-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="31d6e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="31d6e-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="31d6e-118">Scenario description</span></span>
<span data-ttu-id="31d6e-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="31d6e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="31d6e-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="31d6e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="31d6e-121">Dodawanie Workpath z galerii</span><span class="sxs-lookup"><span data-stu-id="31d6e-121">Adding Workpath from the gallery</span></span>
2. <span data-ttu-id="31d6e-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="31d6e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workpath-from-the-gallery"></a><span data-ttu-id="31d6e-123">Dodawanie Workpath z galerii</span><span class="sxs-lookup"><span data-stu-id="31d6e-123">Adding Workpath from the gallery</span></span>
<span data-ttu-id="31d6e-124">Aby skonfigurować integrację usługi Azure AD Workpath, należy dodać Workpath z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="31d6e-124">To configure the integration of Workpath into Azure AD, you need to add Workpath from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="31d6e-125">**Aby dodać Workpath z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="31d6e-125">**To add Workpath from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="31d6e-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="31d6e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="31d6e-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="31d6e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="31d6e-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="31d6e-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="31d6e-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="31d6e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="31d6e-133">W polu wyszukiwania wpisz **Workpath**.</span><span class="sxs-lookup"><span data-stu-id="31d6e-133">In the search box, type **Workpath**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_search.png)

5. <span data-ttu-id="31d6e-135">W panelu wyników wybierz **Workpath**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="31d6e-135">In the results panel, select **Workpath**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="31d6e-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="31d6e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="31d6e-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Workpath na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="31d6e-138">In this section, you configure and test Azure AD single sign-on with Workpath based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="31d6e-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Workpath jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="31d6e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Workpath is to a user in Azure AD.</span></span> <span data-ttu-id="31d6e-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Workpath musi się.</span><span class="sxs-lookup"><span data-stu-id="31d6e-140">In other words, a link relationship between an Azure AD user and the related user in Workpath needs to be established.</span></span>

<span data-ttu-id="31d6e-141">W Workpath, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="31d6e-141">In Workpath, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="31d6e-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Workpath, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="31d6e-142">To configure and test Azure AD single sign-on with Workpath, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="31d6e-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="31d6e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="31d6e-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="31d6e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="31d6e-145">**[Tworzenie użytkownika testowego Workpath](#creating-a-workpath-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Workpath połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="31d6e-145">**[Creating a Workpath test user](#creating-a-workpath-test-user)** - to have a counterpart of Britta Simon in Workpath that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="31d6e-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="31d6e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="31d6e-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="31d6e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="31d6e-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="31d6e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="31d6e-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Workpath.</span><span class="sxs-lookup"><span data-stu-id="31d6e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workpath application.</span></span>

<span data-ttu-id="31d6e-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Workpath, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="31d6e-150">**To configure Azure AD single sign-on with Workpath, perform the following steps:**</span></span>

1. <span data-ttu-id="31d6e-151">W portalu Azure na **Workpath** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="31d6e-151">In the Azure portal, on the **Workpath** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="31d6e-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="31d6e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_samlbase.png)

3. <span data-ttu-id="31d6e-155">Na **Workpath domeny i adres URL** sekcji, jeśli chcesz skonfigurować aplikację w **IDP** tryb inicjowane, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="31d6e-155">On the **Workpath Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_url.png)

    <span data-ttu-id="31d6e-157">a.</span><span class="sxs-lookup"><span data-stu-id="31d6e-157">a.</span></span> <span data-ttu-id="31d6e-158">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://api.workpath.com/v1/saml/metadata/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="31d6e-158">In the **Identifier** textbox, type a URL using the following pattern: `https://api.workpath.com/v1/saml/metadata/<instancename>`</span></span>

    <span data-ttu-id="31d6e-159">b.</span><span class="sxs-lookup"><span data-stu-id="31d6e-159">b.</span></span> <span data-ttu-id="31d6e-160">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://api.workpath.com/v1/saml/assert/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="31d6e-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://api.workpath.com/v1/saml/assert/<instancename>`</span></span>

4. <span data-ttu-id="31d6e-161">Sprawdź **Pokaż zaawansowane ustawienia adresu URL**.</span><span class="sxs-lookup"><span data-stu-id="31d6e-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="31d6e-162">Jeśli chcesz skonfigurować aplikację w **SP** inicjowane tryb, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="31d6e-162">If you wish to configure the application in **SP** initiated mode, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_url1.png)

    <span data-ttu-id="31d6e-164">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.workpath.com/ `</span><span class="sxs-lookup"><span data-stu-id="31d6e-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.workpath.com/ `</span></span>

    > [!NOTE] 
    > <span data-ttu-id="31d6e-165">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="31d6e-165">These values are not real.</span></span> <span data-ttu-id="31d6e-166">Rzeczywisty adres URL logowania, identyfikator i adres URL odpowiedzi, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="31d6e-166">Update these values with the actual Sign-on URL, Identifier and Reply URL.</span></span> <span data-ttu-id="31d6e-167">Skontaktuj się z [zespołem pomocy technicznej Workpath](https://help.workpath.com) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="31d6e-167">Contact [Workpath support team](https://help.workpath.com) to get these values.</span></span>

5. <span data-ttu-id="31d6e-168">Aplikacja Workpath oczekuje potwierdzenia języka SAML w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="31d6e-168">Workpath application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="31d6e-169">Skonfiguruj następujące oświadczeń dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="31d6e-169">Configure the following claims for this application.</span></span> <span data-ttu-id="31d6e-170">Możesz zarządzać wartości tych atrybutów z "**atrybuty użytkownika**" sekcji na stronie integracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="31d6e-170">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="31d6e-171">Poniższy zrzut ekranu przedstawia przykład dla tej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="31d6e-171">The following screenshot shows an example for this configuration.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_attributes.png)
    
6. <span data-ttu-id="31d6e-173">W **atrybuty użytkownika** sekcji na **logowanie jednokrotne** okna dialogowego, skonfiguruj atrybut tokenu SAML, jak pokazano w obrazie i wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="31d6e-173">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="31d6e-174">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="31d6e-174">Attribute Name</span></span> | <span data-ttu-id="31d6e-175">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="31d6e-175">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="31d6e-176">Imię</span><span class="sxs-lookup"><span data-stu-id="31d6e-176">first_name</span></span> | <span data-ttu-id="31d6e-177">User.givenName</span><span class="sxs-lookup"><span data-stu-id="31d6e-177">user.givenname</span></span> |
    | <span data-ttu-id="31d6e-178">nazwisko</span><span class="sxs-lookup"><span data-stu-id="31d6e-178">last_name</span></span> | <span data-ttu-id="31d6e-179">User.surname</span><span class="sxs-lookup"><span data-stu-id="31d6e-179">user.surname</span></span> |
    
    <span data-ttu-id="31d6e-180">a.</span><span class="sxs-lookup"><span data-stu-id="31d6e-180">a.</span></span> <span data-ttu-id="31d6e-181">Kliknij przycisk **Dodaj atrybut** otworzyć **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="31d6e-181">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workpath-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="31d6e-183">b.</span><span class="sxs-lookup"><span data-stu-id="31d6e-183">b.</span></span> <span data-ttu-id="31d6e-184">W **nazwa** tekstowym, wpisz nazwę atrybut wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="31d6e-184">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workpath-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="31d6e-186">c.</span><span class="sxs-lookup"><span data-stu-id="31d6e-186">c.</span></span> <span data-ttu-id="31d6e-187">Z **wartość** listy, wpisz wartość atrybutu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="31d6e-187">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="31d6e-188">d.</span><span class="sxs-lookup"><span data-stu-id="31d6e-188">d.</span></span> <span data-ttu-id="31d6e-189">Pozostaw **Namespace** puste pole tekstowe.</span><span class="sxs-lookup"><span data-stu-id="31d6e-189">Leave the **Namespace** textbox blank.</span></span>
    
    <span data-ttu-id="31d6e-190">e.</span><span class="sxs-lookup"><span data-stu-id="31d6e-190">e.</span></span> <span data-ttu-id="31d6e-191">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="31d6e-191">Click **Ok**.</span></span>
    

7. <span data-ttu-id="31d6e-192">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="31d6e-192">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_certificate.png) 

8. <span data-ttu-id="31d6e-194">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="31d6e-194">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workpath-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="31d6e-196">Na **konfiguracji Workpath** , kliknij przycisk **skonfigurować Workpath** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="31d6e-196">On the **Workpath Configuration** section, click **Configure Workpath** to open **Configure sign-on** window.</span></span> <span data-ttu-id="31d6e-197">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="31d6e-197">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_configure.png) 

10. <span data-ttu-id="31d6e-199">Aby skonfigurować logowanie jednokrotne w **Workpath** stronie, musisz wysłać pobrany **XML metadanych**, **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** do [Zespołem pomocy technicznej Workpath](https://help.workpath.com).</span><span class="sxs-lookup"><span data-stu-id="31d6e-199">To configure single sign-on on **Workpath** side, you need to send the downloaded **Metadata XML**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Workpath support team](https://help.workpath.com).</span></span> 

> [!TIP]
> <span data-ttu-id="31d6e-200">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="31d6e-200">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="31d6e-201">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="31d6e-201">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="31d6e-202">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="31d6e-202">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="31d6e-203">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="31d6e-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="31d6e-204">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="31d6e-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="31d6e-206">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="31d6e-206">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="31d6e-207">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="31d6e-207">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-workpath-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="31d6e-209">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="31d6e-209">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-workpath-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="31d6e-211">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="31d6e-211">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-workpath-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="31d6e-213">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="31d6e-213">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-workpath-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="31d6e-215">a.</span><span class="sxs-lookup"><span data-stu-id="31d6e-215">a.</span></span> <span data-ttu-id="31d6e-216">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="31d6e-216">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="31d6e-217">b.</span><span class="sxs-lookup"><span data-stu-id="31d6e-217">b.</span></span> <span data-ttu-id="31d6e-218">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="31d6e-218">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="31d6e-219">c.</span><span class="sxs-lookup"><span data-stu-id="31d6e-219">c.</span></span> <span data-ttu-id="31d6e-220">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="31d6e-220">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="31d6e-221">d.</span><span class="sxs-lookup"><span data-stu-id="31d6e-221">d.</span></span> <span data-ttu-id="31d6e-222">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="31d6e-222">Click **Create**.</span></span>
 
### <a name="creating-a-workpath-test-user"></a><span data-ttu-id="31d6e-223">Tworzenie użytkownika testowego Workpath</span><span class="sxs-lookup"><span data-stu-id="31d6e-223">Creating a Workpath test user</span></span>

<span data-ttu-id="31d6e-224">Workpath obsługuje tylko w czasie Inicjowanie obsługi użytkowników.</span><span class="sxs-lookup"><span data-stu-id="31d6e-224">Workpath supports Just in time user provisioning.</span></span> <span data-ttu-id="31d6e-225">Po uwierzytelnieniu użytkownicy są automatycznie tworzone w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="31d6e-225">After authentication users are created in the application automatically.</span></span> 


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="31d6e-226">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="31d6e-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="31d6e-227">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Workpath.</span><span class="sxs-lookup"><span data-stu-id="31d6e-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workpath.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="31d6e-229">**Aby przypisać Simona Britta Workpath, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="31d6e-229">**To assign Britta Simon to Workpath, perform the following steps:**</span></span>

1. <span data-ttu-id="31d6e-230">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="31d6e-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="31d6e-232">Na liście aplikacji zaznacz **Workpath**.</span><span class="sxs-lookup"><span data-stu-id="31d6e-232">In the applications list, select **Workpath**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_app.png) 

3. <span data-ttu-id="31d6e-234">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="31d6e-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="31d6e-236">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="31d6e-236">Click **Add** button.</span></span> <span data-ttu-id="31d6e-237">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="31d6e-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="31d6e-239">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="31d6e-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="31d6e-240">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="31d6e-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="31d6e-241">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="31d6e-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="31d6e-242">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="31d6e-242">Testing single sign-on</span></span>

<span data-ttu-id="31d6e-243">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="31d6e-243">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="31d6e-244">Po kliknięciu kafelka Workpath w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Workpath.</span><span class="sxs-lookup"><span data-stu-id="31d6e-244">When you click the Workpath tile in the Access Panel, you should get automatically signed-on to your Workpath application.</span></span>
<span data-ttu-id="31d6e-245">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="31d6e-245">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="31d6e-246">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="31d6e-246">Additional resources</span></span>

* [<span data-ttu-id="31d6e-247">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="31d6e-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="31d6e-248">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="31d6e-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_203.png

