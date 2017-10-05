---
title: "Samouczek: Azure Active Directory integrację z klientem Gorilla ziemi | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Gorilla ziemi."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: jeedes
ms.openlocfilehash: 744c420aa0298c59c44e645b95a716ad876752de
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-land-gorilla-client"></a><span data-ttu-id="1b4a0-103">Samouczek: Integracji Azure Active Directory z ziemi Gorilla klienta</span><span class="sxs-lookup"><span data-stu-id="1b4a0-103">Tutorial: Azure Active Directory integration with Land Gorilla Client</span></span>

<span data-ttu-id="1b4a0-104">Z tego samouczka dowiesz się integrowanie ziemi Gorilla klienta z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1b4a0-104">In this tutorial, you learn how to integrate Land Gorilla Client with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1b4a0-105">Integrowanie ziemi Gorilla klienta z usługi Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="1b4a0-105">Integrating Land Gorilla Client with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1b4a0-106">Można kontrolować w usłudze Azure AD, który ma dostęp do ziemi Gorilla klienta</span><span class="sxs-lookup"><span data-stu-id="1b4a0-106">You can control in Azure AD who has access to Land Gorilla Client</span></span>
- <span data-ttu-id="1b4a0-107">Umożliwia użytkownikom automatycznie pobrać zalogowane klientowi Gorilla ziemi (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1b4a0-107">You can enable your users to automatically get signed-on to Land Gorilla Client (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1b4a0-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu zarządzania Azure</span><span class="sxs-lookup"><span data-stu-id="1b4a0-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="1b4a0-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1b4a0-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="1b4a0-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1b4a0-110">Prerequisites</span></span>

<span data-ttu-id="1b4a0-111">Aby skonfigurować integrację usługi Azure AD z klientem Gorilla ziemi, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="1b4a0-111">To configure Azure AD integration with Land Gorilla Client, you need the following items:</span></span>

- <span data-ttu-id="1b4a0-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1b4a0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1b4a0-113">Klient Gorilla ziemi jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="1b4a0-113">A Land Gorilla Client single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="1b4a0-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="1b4a0-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="1b4a0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1b4a0-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="1b4a0-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1b4a0-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="1b4a0-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="1b4a0-118">Scenario description</span></span>
<span data-ttu-id="1b4a0-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1b4a0-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="1b4a0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1b4a0-121">Dodawanie klienta Gorilla ziemi z galerii</span><span class="sxs-lookup"><span data-stu-id="1b4a0-121">Adding Land Gorilla Client from the gallery</span></span>
2. <span data-ttu-id="1b4a0-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="1b4a0-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-land-gorilla-client-from-the-gallery"></a><span data-ttu-id="1b4a0-123">Dodawanie klienta Gorilla ziemi z galerii</span><span class="sxs-lookup"><span data-stu-id="1b4a0-123">Adding Land Gorilla Client from the gallery</span></span>
<span data-ttu-id="1b4a0-124">Aby skonfigurować integrację usługi Azure AD ziemi Gorilla klienta, należy dodać ziemi Gorilla klienta z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-124">To configure the integration of Land Gorilla Client into Azure AD, you need to add Land Gorilla Client from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1b4a0-125">**Aby dodać klienta Gorilla ziemi z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="1b4a0-125">**To add Land Gorilla Client from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1b4a0-126">W  **[portalu zarządzania Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="1b4a0-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1b4a0-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="1b4a0-131">Kliknij przycisk **Dodaj** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="1b4a0-133">W polu wyszukiwania wpisz **klienta Gorilla ziemi**.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-133">In the search box, type **Land Gorilla Client**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_search.png)

5. <span data-ttu-id="1b4a0-135">W panelu wyników wybierz **klienta Gorilla ziemi**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-135">In the results panel, select **Land Gorilla Client**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_addfromgallery.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1b4a0-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="1b4a0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1b4a0-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z klientem Gorilla ziemi w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-138">In this section, you configure and test Azure AD single sign-on with Land Gorilla Client based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1b4a0-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w kliencie Gorilla ziemi jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Land Gorilla Client is to a user in Azure AD.</span></span> <span data-ttu-id="1b4a0-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w kliencie Gorilla ziemi musi się.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-140">In other words, a link relationship between an Azure AD user and the related user in Land Gorilla Client needs to be established.</span></span>

<span data-ttu-id="1b4a0-141">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** ziemi Gorilla klienta.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Land Gorilla Client.</span></span>

<span data-ttu-id="1b4a0-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z klientem Gorilla ziemi, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="1b4a0-142">To configure and test Azure AD single sign-on with Land Gorilla Client, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1b4a0-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1b4a0-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z grupą ograniczone.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with limited group.</span></span>
3. <span data-ttu-id="1b4a0-145">**[Tworzenie użytkownika testowego Gorilla ziemi](#creating-a-land-gorilla-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-145">**[Creating a Land Gorilla test user](#creating-a-land-gorilla-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="1b4a0-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1b4a0-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1b4a0-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="1b4a0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1b4a0-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu zarządzania Azure i skonfigurować logowanie jednokrotne w aplikacji klienta Gorilla ziemi.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Land Gorilla Client application.</span></span>

<span data-ttu-id="1b4a0-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z klientem Gorilla ziemi, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="1b4a0-150">**To configure Azure AD single sign-on with Land Gorilla Client, perform the following steps:**</span></span>

1. <span data-ttu-id="1b4a0-151">W portalu zarządzania Azure na **klienta Gorilla ziemi** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-151">In the Azure Management portal, on the **Land Gorilla Client** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="1b4a0-153">Na **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** Włącz funkcji logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_samlbase.png)

3. <span data-ttu-id="1b4a0-155">Na **adresy URL i domeny klienta grunt Gorilla** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="1b4a0-155">On the **Land Gorilla Client Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_url_02.png)

    <span data-ttu-id="1b4a0-157">a.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-157">a.</span></span> <span data-ttu-id="1b4a0-158">W **identyfikator** tekstowym, wpisz wartość, przy użyciu jednej z następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="1b4a0-158">In the **Identifier** textbox, type the value using one of the following pattern:</span></span> 
    
    `https://<customer domain>.landgorilla.com/` 
    
    `https://www.<customer domain>.landgorilla.com`

    <span data-ttu-id="1b4a0-159">b.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-159">b.</span></span> <span data-ttu-id="1b4a0-160">W **adres URL odpowiedzi** tekstowym, wpisz adres URL przy użyciu jednej z następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="1b4a0-160">In the **Reply URL** textbox, type a URL using one of the following pattern:</span></span>

    `https://<customer domain>.landgorilla.com/simplesaml/module.php/core/authenticate.php`

    `https://www.<customer domain>.landgorilla.com/simplesaml/module.php/core/authenticate.php`

    `https://<customer domain>.landgorilla.com/simplesaml/module.php/saml/sp/saml2-acs.php/default-sp`
    
    `https://www.<customer domain>.landgorilla.com/simplesaml/module.php/saml/sp/saml2-acs.php/default-sp`

    > [!NOTE] 
    > <span data-ttu-id="1b4a0-161">Należy pamiętać, że nie są one rzeczywiste wartości.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-161">Please note that these are not the real values.</span></span> <span data-ttu-id="1b4a0-162">Należy zaktualizować te wartości z rzeczywistego identyfikatora i adres URL odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="1b4a0-163">W tym miejscu zalecamy można używać unikatowej wartości ciągu w identyfikatorze.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="1b4a0-164">Skontaktuj się z [ziemi Gorilla klienta team](https://www.landgorilla.com/support/) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-164">Contact [Land Gorilla Client team](https://www.landgorilla.com/support/) to get these values.</span></span> 

4. <span data-ttu-id="1b4a0-165">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_certificate.png) 

5. <span data-ttu-id="1b4a0-167">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-167">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-landgorilla-tutorial/tutorial_general_400.png) 

6. <span data-ttu-id="1b4a0-169">Aby uzyskać pełną konfiguracji logowania jednokrotnego dla aplikacji na końcu Gorilla ziemi, skontaktuj się z [zespołem pomocy technicznej klienta Gorilla ziemi](https://www.landgorilla.com/support/) i udostępnia je z pobranego **"XML metadanych** pliku.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-169">To get SSO configuration complete for your application at Land Gorilla end, Contact [Land Gorilla Client support team](https://www.landgorilla.com/support/) and provide them with the downloaded **“Metadata XML** file.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1b4a0-170">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1b4a0-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="1b4a0-171">Celem tej sekcji jest tworzenie użytkownika testowego w portalu zarządzania Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-171">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="1b4a0-173">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="1b4a0-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1b4a0-174">W **portalu zarządzania Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-174">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1b4a0-176">Przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** do wyświetlenia na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-176">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1b4a0-178">W górnej części okna dialogowego kliknij **Dodaj** otworzyć **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-178">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1b4a0-180">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="1b4a0-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1b4a0-182">a.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-182">a.</span></span> <span data-ttu-id="1b4a0-183">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1b4a0-184">b.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-184">b.</span></span> <span data-ttu-id="1b4a0-185">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1b4a0-186">c.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-186">c.</span></span> <span data-ttu-id="1b4a0-187">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1b4a0-188">d.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-188">d.</span></span> <span data-ttu-id="1b4a0-189">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-189">Click **Create**.</span></span> 

### <a name="creating-a-land-gorilla-test-user"></a><span data-ttu-id="1b4a0-190">Tworzenie użytkownika testowego Gorilla ziemi</span><span class="sxs-lookup"><span data-stu-id="1b4a0-190">Creating a Land Gorilla test user</span></span>

<span data-ttu-id="1b4a0-191">We współpracy z [zespołem pomocy technicznej Gorilla ziemi](https://www.landgorilla.com/support/) Aby dodać użytkowników do platformy Gorilla ziemi.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-191">Please work with [Land Gorilla support team](https://www.landgorilla.com/support/) to add the users in the Land Gorilla platform.</span></span>
    
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1b4a0-192">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1b4a0-192">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1b4a0-193">W tej sekcji można włączyć Simona Britta na udostępnienie jej do ziemi Gorilla klienta za pomocą usługi Azure rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-193">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Land Gorilla Client.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="1b4a0-195">**Aby przypisać Simona Britta ziemi Gorilla klienta, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="1b4a0-195">**To assign Britta Simon to Land Gorilla Client, perform the following steps:**</span></span>

1. <span data-ttu-id="1b4a0-196">Otwórz widok aplikacji w portalu zarządzania Azure, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-196">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="1b4a0-198">Na liście aplikacji zaznacz **klienta Gorilla ziemi**.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-198">In the applications list, select **Land Gorilla Client**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_app.png) 

3. <span data-ttu-id="1b4a0-200">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-200">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="1b4a0-202">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-202">Click **Add** button.</span></span> <span data-ttu-id="1b4a0-203">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-203">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="1b4a0-205">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-205">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1b4a0-206">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-206">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1b4a0-207">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-207">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="1b4a0-208">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="1b4a0-208">Testing single sign-on</span></span>

<span data-ttu-id="1b4a0-209">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-209">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1b4a0-210">Po kliknięciu kafelka ziemi Gorilla klienta w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji klienckiej Gorilla ziemi.</span><span class="sxs-lookup"><span data-stu-id="1b4a0-210">When you click the Land Gorilla Client tile in the Access Panel, you should get automatically signed-on to your Land Gorilla Client application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="1b4a0-211">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="1b4a0-211">Additional resources</span></span>

* [<span data-ttu-id="1b4a0-212">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1b4a0-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1b4a0-213">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1b4a0-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_203.png
