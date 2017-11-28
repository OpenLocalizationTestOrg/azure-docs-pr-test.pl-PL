---
title: 'Samouczek: Integracji Azure Active Directory z Pingboard | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Pingboard."
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
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 008c670a8043da0c67ccefde48d5ef721c75d97c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pingboard"></a><span data-ttu-id="ce7ef-103">Samouczek: Integracji Azure Active Directory z Pingboard</span><span class="sxs-lookup"><span data-stu-id="ce7ef-103">Tutorial: Azure Active Directory integration with Pingboard</span></span>

<span data-ttu-id="ce7ef-104">Z tego samouczka dowiesz się integrowanie Pingboard z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ce7ef-104">In this tutorial, you learn how to integrate Pingboard with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ce7ef-105">Integracja z usługą Azure AD Pingboard zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="ce7ef-105">Integrating Pingboard with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ce7ef-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Pingboard</span><span class="sxs-lookup"><span data-stu-id="ce7ef-106">You can control in Azure AD who has access to Pingboard</span></span>
- <span data-ttu-id="ce7ef-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Pingboard (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce7ef-107">You can enable your users to automatically get signed-on to Pingboard (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ce7ef-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu zarządzania Azure</span><span class="sxs-lookup"><span data-stu-id="ce7ef-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="ce7ef-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ce7ef-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ce7ef-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ce7ef-110">Prerequisites</span></span>

<span data-ttu-id="ce7ef-111">Aby skonfigurować integrację usługi Azure AD z Pingboard, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="ce7ef-111">To configure Azure AD integration with Pingboard, you need the following items:</span></span>

- <span data-ttu-id="ce7ef-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce7ef-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ce7ef-113">Pingboard jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="ce7ef-113">A Pingboard single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ce7ef-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ce7ef-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="ce7ef-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ce7ef-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="ce7ef-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ce7ef-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ce7ef-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="ce7ef-118">Scenario description</span></span>
<span data-ttu-id="ce7ef-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ce7ef-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="ce7ef-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ce7ef-121">Dodawanie Pingboard z galerii</span><span class="sxs-lookup"><span data-stu-id="ce7ef-121">Adding Pingboard from the gallery</span></span>
2. <span data-ttu-id="ce7ef-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="ce7ef-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pingboard-from-the-gallery"></a><span data-ttu-id="ce7ef-123">Dodawanie Pingboard z galerii</span><span class="sxs-lookup"><span data-stu-id="ce7ef-123">Adding Pingboard from the gallery</span></span>
<span data-ttu-id="ce7ef-124">Aby skonfigurować integrację usługi Azure AD Pingboard, należy dodać Pingboard z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-124">To configure the integration of Pingboard into Azure AD, you need to add Pingboard from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ce7ef-125">**Aby dodać Pingboard z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="ce7ef-125">**To add Pingboard from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ce7ef-126">W  **[portalu zarządzania Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="ce7ef-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ce7ef-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="ce7ef-131">Kliknij przycisk **Dodaj** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="ce7ef-133">W polu wyszukiwania wpisz **Pingboard**.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-133">In the search box, type **Pingboard**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_search.png)

5. <span data-ttu-id="ce7ef-135">W panelu wyników wybierz **Pingboard**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-135">In the results panel, select **Pingboard**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ce7ef-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="ce7ef-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ce7ef-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Pingboard w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-138">In this section, you configure and test Azure AD single sign-on with Pingboard based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ce7ef-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Pingboard jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Pingboard is to a user in Azure AD.</span></span> <span data-ttu-id="ce7ef-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Pingboard musi się.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-140">In other words, a link relationship between an Azure AD user and the related user in Pingboard needs to be established.</span></span>

<span data-ttu-id="ce7ef-141">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w Pingboard.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Pingboard.</span></span>

<span data-ttu-id="ce7ef-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Pingboard, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="ce7ef-142">To configure and test Azure AD single sign-on with Pingboard, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ce7ef-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ce7ef-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ce7ef-145">**[Tworzenie użytkownika testowego Pingboard](#creating-a-pingboard-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Pingboard połączonego z jej reprezentacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-145">**[Creating a Pingboard test user](#creating-a-pingboard-test-user)** - to have a counterpart of Britta Simon in Pingboard that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="ce7ef-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ce7ef-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ce7ef-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ce7ef-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ce7ef-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu zarządzania Azure i skonfigurować logowanie jednokrotne w aplikacji Pingboard.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Pingboard application.</span></span>

<span data-ttu-id="ce7ef-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Pingboard, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="ce7ef-150">**To configure Azure AD single sign-on with Pingboard, perform the following steps:**</span></span>

1. <span data-ttu-id="ce7ef-151">W portalu zarządzania Azure na **Pingboard** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-151">In the Azure Management portal, on the **Pingboard** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="ce7ef-153">Na **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** Włącz funkcji logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_samlbase.png)

3. <span data-ttu-id="ce7ef-155">Na **Pingboard domeny i adres URL** sekcji, wykonaj następujące kroki, aby skonfigurować aplikację w **IDP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="ce7ef-155">On the **Pingboard Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_url.png)

    <span data-ttu-id="ce7ef-157">a.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-157">a.</span></span> <span data-ttu-id="ce7ef-158">W **identyfikator** tekstowym, wpisz wartość, jak:`http://<entity-id>.pingboard.com/sp`</span><span class="sxs-lookup"><span data-stu-id="ce7ef-158">In the **Identifier** textbox, type the value as: `http://<entity-id>.pingboard.com/sp`</span></span>

    <span data-ttu-id="ce7ef-159">b.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-159">b.</span></span> <span data-ttu-id="ce7ef-160">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<entity-id>.pingboard.com/auth/saml/consume`</span><span class="sxs-lookup"><span data-stu-id="ce7ef-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<entity-id>.pingboard.com/auth/saml/consume`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ce7ef-161">Należy pamiętać, że nie są one rzeczywiste wartości.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-161">Please note that these are not the real values.</span></span> <span data-ttu-id="ce7ef-162">Należy zaktualizować te wartości z rzeczywistego identyfikatora i adres URL odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="ce7ef-163">W tym miejscu zalecamy można używać unikatowej wartości ciągu w identyfikatorze.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="ce7ef-164">Skontaktuj się z [zespołem pomocy technicznej klienta Pingboard](https://support.pingboard.com/) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-164">Contact [Pingboard Client support team](https://support.pingboard.com/) to get these values.</span></span> 

4. <span data-ttu-id="ce7ef-165">Sprawdź **Pokaż zaawansowane ustawienia adresu URL**, jeśli chcesz skonfigurować aplikację w **SP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="ce7ef-165">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_sp_initiated01.png)

    <span data-ttu-id="ce7ef-167">a.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-167">a.</span></span> <span data-ttu-id="ce7ef-168">W **adres URL logowania** tekstowym, wpisz wartość, jak:`http://<sub-domain>.pingboard.com/sign_in`</span><span class="sxs-lookup"><span data-stu-id="ce7ef-168">In the **Sign-on URL** textbox, type the value as: `http://<sub-domain>.pingboard.com/sign_in`</span></span>
     
5. <span data-ttu-id="ce7ef-169">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_certificate.png) 

6. <span data-ttu-id="ce7ef-171">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-171">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pingboard-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="ce7ef-173">Aby skonfigurować logowanie Jednokrotne po stronie Pingboard, Otwórz nowe okno przeglądarki i zaloguj się do swojego konta Pingboard.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-173">To configure SSO on Pingboard side, open a new browser window and log in to your Pingboard Account.</span></span> <span data-ttu-id="ce7ef-174">Musisz być administratorem Pingboard, aby skonfigurować funkcji logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-174">You must be a Pingboard admin to set up single sign on.</span></span>

8. <span data-ttu-id="ce7ef-175">Wybierz z górnego menu **aplikacji > integracji**</span><span class="sxs-lookup"><span data-stu-id="ce7ef-175">From the top menu select **Apps > Integrations**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pingboard-tutorial/Pingboard_integration.png)

9.  <span data-ttu-id="ce7ef-177">Na **integracji** strony, Znajdź **"Azure Active Directory"** Kafelek, a następnie kliknij go.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-177">On the **Integrations** page, find the **"Azure Active Directory"** tile, and click it.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pingboard-tutorial/Pingboard_aad.png)

10. <span data-ttu-id="ce7ef-179">W modalne, kliknij poniżej **"Konfiguruj"**</span><span class="sxs-lookup"><span data-stu-id="ce7ef-179">In the modal that follows click **"Configure"**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pingboard-tutorial/Pingboard_configure.png)

11. <span data-ttu-id="ce7ef-181">Na następnej stronie można zauważyć, że "Integracja z usługą Azure rejestracji Jednokrotnej jest włączona.".</span><span class="sxs-lookup"><span data-stu-id="ce7ef-181">On the following page, you will notice that "Azure SSO Integration is enabled.".</span></span> <span data-ttu-id="ce7ef-182">Otwórz pobrany plik XML metadanych w programie Notatnik i Wklej zawartość **metadanych IDP**.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-182">Open the downloaded Metadata XML file in a notepad and paste the content in **IDP Metadata**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pingboard-tutorial/Pingboard_sso_configure.png)

12. <span data-ttu-id="ce7ef-184">Plik zostanie zweryfikowany, a jeśli wszystko jest poprawny, pojedynczy znak na zostanie ono włączone</span><span class="sxs-lookup"><span data-stu-id="ce7ef-184">The file will be validated, and if everything is correct, single sign on will now be enabled</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ce7ef-185">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce7ef-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="ce7ef-186">Celem tej sekcji jest tworzenie użytkownika testowego w portalu zarządzania Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-186">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="ce7ef-188">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="ce7ef-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ce7ef-189">W **portalu zarządzania Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-189">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ce7ef-191">Przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** do wyświetlenia na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-191">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ce7ef-193">W górnej części okna dialogowego kliknij **Dodaj** otworzyć **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-193">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ce7ef-195">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ce7ef-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ce7ef-197">a.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-197">a.</span></span> <span data-ttu-id="ce7ef-198">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ce7ef-199">b.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-199">b.</span></span> <span data-ttu-id="ce7ef-200">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-200">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ce7ef-201">c.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-201">c.</span></span> <span data-ttu-id="ce7ef-202">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ce7ef-203">d.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-203">d.</span></span> <span data-ttu-id="ce7ef-204">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-204">Click **Create**.</span></span>
 
### <a name="creating-a-pingboard-test-user"></a><span data-ttu-id="ce7ef-205">Tworzenie użytkownika testowego Pingboard</span><span class="sxs-lookup"><span data-stu-id="ce7ef-205">Creating a Pingboard test user</span></span>

<span data-ttu-id="ce7ef-206">Aby włączyć użytkowników usługi Azure AD zalogować się do Pingboard, musi być przygotowana do Pingboard.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-206">In order to enable Azure AD users to log into Pingboard, they must be provisioned into Pingboard.</span></span>  
<span data-ttu-id="ce7ef-207">W przypadku Pingboard Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-207">In the case of Pingboard, provisioning is a manual task.</span></span>

<span data-ttu-id="ce7ef-208">**Aby udostępnić konta użytkowników, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="ce7ef-208">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="ce7ef-209">Zaloguj się do witryny firmy Pingboard jako administrator.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-209">Log in to your Pingboard company site as an administrator.</span></span>

2. <span data-ttu-id="ce7ef-210">Kliknij przycisk **"Dodaj pracownika"** znajdującego się na **katalogu** strony.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-210">Click **“Add Employee”** button on **Directory** page.</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-pingboard-tutorial/create_testuser_add.png)

3. <span data-ttu-id="ce7ef-212">Na **"Dodaj pracownika"** okna dialogowego wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-212">On the **“Add Employee”** dialog page, perform the following steps.</span></span>

    ![Zaproś inne osoby](./media/active-directory-saas-pingboard-tutorial/create_testuser_name.png)

    <span data-ttu-id="ce7ef-214">a.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-214">a.</span></span> <span data-ttu-id="ce7ef-215">W **imię i nazwisko** tekstowym, wpisz pełną nazwę Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-215">In the **Full Name** textbox, type the full name of Britta Simon.</span></span>

    <span data-ttu-id="ce7ef-216">b.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-216">b.</span></span> <span data-ttu-id="ce7ef-217">W **E-mail** tekstowym, wpisz adres e-mail konta Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-217">In the **Email** textbox, type the email address of Britta Simon account.</span></span>

    <span data-ttu-id="ce7ef-218">c.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-218">c.</span></span> <span data-ttu-id="ce7ef-219">W **stanowisko** tekstowym, wpisz nazwę zadania Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-219">In the **Job Title** textbox, type the job title of Britta Simon.</span></span>

    <span data-ttu-id="ce7ef-220">d.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-220">d.</span></span> <span data-ttu-id="ce7ef-221">W **lokalizacji** listy rozwijanej wybierz lokalizację Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-221">In the **Location** dropdown, select the location  of Britta Simon.</span></span>
    
    <span data-ttu-id="ce7ef-222">e.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-222">e.</span></span> <span data-ttu-id="ce7ef-223">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-223">Click **Add**.</span></span>   

4. <span data-ttu-id="ce7ef-224">Ekran potwierdzenia rozpocznie pracę, aby potwierdzić dodanie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-224">A confirmation screen will come up to confirm the addition of user.</span></span>
    
    ![Upewnij się](./media/active-directory-saas-pingboard-tutorial/create_testuser_confirm.png)
        
    > [!NOTE]
    > <span data-ttu-id="ce7ef-226">Właścicielem konta usługi Azure Active Directory otrzymasz wiadomość e-mail, a następnie kliknij łącze, aby potwierdzić swoje konto, zanim staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-226">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ce7ef-227">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce7ef-227">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ce7ef-228">W tej sekcji można włączyć Simona Britta do udostępnienia jej Pingboard za pomocą usługi Azure rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-228">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Pingboard.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="ce7ef-230">**Aby przypisać Simona Britta Pingboard, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="ce7ef-230">**To assign Britta Simon to Pingboard, perform the following steps:**</span></span>

1. <span data-ttu-id="ce7ef-231">Otwórz widok aplikacji w portalu zarządzania Azure, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-231">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="ce7ef-233">Na liście aplikacji zaznacz **Pingboard**.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-233">In the applications list, select **Pingboard**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_app.png) 

3. <span data-ttu-id="ce7ef-235">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-235">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="ce7ef-237">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-237">Click **Add** button.</span></span> <span data-ttu-id="ce7ef-238">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="ce7ef-240">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ce7ef-241">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ce7ef-242">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ce7ef-243">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ce7ef-243">Testing single sign-on</span></span>

<span data-ttu-id="ce7ef-244">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-244">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ce7ef-245">Po kliknięciu kafelka Pingboard w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Pingboard.</span><span class="sxs-lookup"><span data-stu-id="ce7ef-245">When you click the Pingboard tile in the Access Panel, you should get automatically signed-on to your Pingboard application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ce7ef-246">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="ce7ef-246">Additional resources</span></span>

* [<span data-ttu-id="ce7ef-247">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ce7ef-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ce7ef-248">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ce7ef-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_203.png
