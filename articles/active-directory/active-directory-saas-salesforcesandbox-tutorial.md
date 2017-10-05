---
title: 'Samouczek: Integracji Azure Active Directory z piaskownicy Salesforce | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i usług Salesforce piaskownicy."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 90e08b9cf2feb93de4877bec9734352949896dca
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a><span data-ttu-id="8f32e-103">Samouczek: Integracji Azure Active Directory z piaskownicy usług Salesforce</span><span class="sxs-lookup"><span data-stu-id="8f32e-103">Tutorial: Azure Active Directory integration with Salesforce Sandbox</span></span>

<span data-ttu-id="8f32e-104">Z tego samouczka dowiesz się integrowanie piaskownicy usługi Salesforce z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8f32e-104">In this tutorial, you learn how to integrate Salesforce Sandbox with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8f32e-105">Integrowanie piaskownicy usługi Salesforce z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="8f32e-105">Integrating Salesforce Sandbox with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8f32e-106">Można kontrolować w usłudze Azure AD, który ma dostęp do usług Salesforce piaskownicy</span><span class="sxs-lookup"><span data-stu-id="8f32e-106">You can control in Azure AD who has access to Salesforce Sandbox</span></span>
- <span data-ttu-id="8f32e-107">Umożliwia użytkownikom automatycznie pobrać podpisany w przypadku piaskownicy Salesforce (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f32e-107">You can enable your users to automatically get signed-on to Salesforce Sandbox (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8f32e-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="8f32e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8f32e-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8f32e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8f32e-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8f32e-110">Prerequisites</span></span>

<span data-ttu-id="8f32e-111">Aby skonfigurować integrację usługi Azure AD z piaskownicy Salesforce, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="8f32e-111">To configure Azure AD integration with Salesforce Sandbox, you need the following items:</span></span>

- <span data-ttu-id="8f32e-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f32e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8f32e-113">Piaskownica Salesforce jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="8f32e-113">A Salesforce Sandbox single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8f32e-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="8f32e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8f32e-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="8f32e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8f32e-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="8f32e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8f32e-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8f32e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8f32e-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="8f32e-118">Scenario description</span></span>
<span data-ttu-id="8f32e-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="8f32e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8f32e-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="8f32e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8f32e-121">Dodawanie piaskownicy usługi Salesforce z galerii</span><span class="sxs-lookup"><span data-stu-id="8f32e-121">Adding Salesforce Sandbox from the gallery</span></span>
2. <span data-ttu-id="8f32e-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="8f32e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-salesforce-sandbox-from-the-gallery"></a><span data-ttu-id="8f32e-123">Dodawanie piaskownicy usługi Salesforce z galerii</span><span class="sxs-lookup"><span data-stu-id="8f32e-123">Adding Salesforce Sandbox from the gallery</span></span>
<span data-ttu-id="8f32e-124">Aby skonfigurować integrację piaskownicy usługi Salesforce z usługą Azure AD, należy dodać piaskownicy usługi Salesforce z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="8f32e-124">To configure the integration of Salesforce Sandbox into Azure AD, you need to add Salesforce Sandbox from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8f32e-125">**Aby dodać piaskownicy usługi Salesforce z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="8f32e-125">**To add Salesforce Sandbox from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8f32e-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="8f32e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="8f32e-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="8f32e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8f32e-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="8f32e-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="8f32e-131">Kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8f32e-131">Click **New application** button on the top of the dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="8f32e-133">W polu wyszukiwania wpisz **piaskownicy Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="8f32e-133">In the search box, type **Salesforce Sandbox**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_search.png)

5. <span data-ttu-id="8f32e-135">W panelu wyników wybierz **piaskownicy Salesforce**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="8f32e-135">In the results panel, select **Salesforce Sandbox**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8f32e-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="8f32e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8f32e-138">W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z piaskownicy Salesforce oparte na użytkownika testowego o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="8f32e-138">In this section, you configure and test Azure AD single sign-on with Salesforce Sandbox based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8f32e-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w piaskownicy Salesforce jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8f32e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Salesforce Sandbox is to a user in Azure AD.</span></span> <span data-ttu-id="8f32e-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i danemu użytkownikowi w piaskownicy Salesforce musi określone.</span><span class="sxs-lookup"><span data-stu-id="8f32e-140">In other words, a link relationship between an Azure AD user and the related user in Salesforce Sandbox needs to be established.</span></span>

<span data-ttu-id="8f32e-141">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w piaskownicy Salesforce.</span><span class="sxs-lookup"><span data-stu-id="8f32e-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Salesforce Sandbox.</span></span>

<span data-ttu-id="8f32e-142">Do konfigurowania i testowania usługi Azure AD rejestracji jednokrotnej z piaskownicy Salesforce, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="8f32e-142">To configure and test Azure AD single sign-on with Salesforce Sandbox, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8f32e-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="8f32e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8f32e-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="8f32e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8f32e-145">**[Tworzenie użytkownika testowego piaskownicy Salesforce](#creating-a-salesforce-sandbox-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta piaskownicy Salesforce, połączonej z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8f32e-145">**[Creating a Salesforce Sandbox test user](#creating-a-salesforce-sandbox-test-user)** - to have a counterpart of Britta Simon in Salesforce Sandbox that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8f32e-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="8f32e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8f32e-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="8f32e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8f32e-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8f32e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8f32e-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne do aplikacji Salesforce piaskownicy.</span><span class="sxs-lookup"><span data-stu-id="8f32e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Salesforce Sandbox application.</span></span>

<span data-ttu-id="8f32e-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z piaskownicy Salesforce, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="8f32e-150">**To configure Azure AD single sign-on with Salesforce Sandbox, perform the following steps:**</span></span>

1. <span data-ttu-id="8f32e-151">W portalu Azure na **piaskownicy Salesforce** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="8f32e-151">In the Azure portal, on the **Salesforce Sandbox** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="8f32e-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="8f32e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_samlbase.png)

3. <span data-ttu-id="8f32e-155">Na **Salesforce piaskownicy domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="8f32e-155">On the **Salesforce Sandbox Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_url.png)

     <span data-ttu-id="8f32e-157">W **adres URL logowania** tekstowym, wpisz wartość, przy użyciu następującego wzorca:`https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="8f32e-157">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<subdomain>.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8f32e-158">Ta wartość nie jest rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="8f32e-158">This value is not the real.</span></span> <span data-ttu-id="8f32e-159">Zaktualizuj tę wartość przy rzeczywisty adres URL logowania. Skontaktuj się z [zespołem pomocy technicznej klienta piaskownicy Salesforce](https://help.salesforce.com/support) aby zyskać tę wartość.</span><span class="sxs-lookup"><span data-stu-id="8f32e-159">Update this value with the actual Sign-on URL.Contact [Salesforce Sandbox Client support team](https://help.salesforce.com/support) to get this value.</span></span>


4. <span data-ttu-id="8f32e-160">Jeśli skonfigurowano już program rejestracji jednokrotnej dla innego wystąpienia usług Salesforce piaskownicy w katalogu, a następnie należy także skonfigurować **identyfikator** mają taką samą wartość jak **Zaloguj się na adres URL**.</span><span class="sxs-lookup"><span data-stu-id="8f32e-160">If you have already configured single sign-on for another Salesforce Sandbox instance in your directory, then you must also configure the **Identifier** to have the same value as the **Sign on URL**.</span></span> 
    
    >[!Note]
    ><span data-ttu-id="8f32e-161">**Identyfikator** można znaleźć pola sprawdzając **Pokaż zaawansowane ustawienia** wyboru na **Konfigurowanie adresu URL aplikacji** strony okna dialogowego</span><span class="sxs-lookup"><span data-stu-id="8f32e-161">The **Identifier** field can be found by checking the **Show advanced settings** checkbox on the **Configure App URL** page of the dialog</span></span> 


5. <span data-ttu-id="8f32e-162">Na **certyfikat podpisywania SAML** kliknij **certyfikatu** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="8f32e-162">On the **SAML Signing Certificate** section, click **Certificate** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_certificate.png) 

6. <span data-ttu-id="8f32e-164">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8f32e-164">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="8f32e-166">Na **konfiguracji piaskownicy Salesforce** , kliknij przycisk **skonfigurować piaskownicy Salesforce** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="8f32e-166">On the **Salesforce Sandbox Configuration** section, click **Configure Salesforce Sandbox** to open **Configure sign-on** window.</span></span> <span data-ttu-id="8f32e-167">Kopiuj **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="8f32e-167">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    <span data-ttu-id="8f32e-168">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="8f32e-168">![Configure Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS></span></span>
8. <span data-ttu-id="8f32e-169">Otwórz nową kartę w przeglądarce i zaloguj się do konta administratora usługi Salesforce piaskownicy.</span><span class="sxs-lookup"><span data-stu-id="8f32e-169">Open a new tab in your browser and log in to your Salesforce Sandbox administrator account.</span></span>

9. <span data-ttu-id="8f32e-170">W menu u góry kliknij **Instalatora**.</span><span class="sxs-lookup"><span data-stu-id="8f32e-170">In the menu on the top, click **Setup**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforcesandbox-tutorial/IC781024.png)
10. <span data-ttu-id="8f32e-172">W okienku nawigacji po lewej stronie kliknij **kontroli bezpieczeństwa**, a następnie kliknij przycisk **ustawień rejestracji jednokrotnej**.</span><span class="sxs-lookup"><span data-stu-id="8f32e-172">In the navigation pane on the left, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforcesandbox-tutorial/IC781025.png)
11. <span data-ttu-id="8f32e-174">W sekcji Ustawienia rejestracji jednokrotnej, wykonaj następujące kroki: ![skonfigurować logowanie jednokrotne](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png)</span><span class="sxs-lookup"><span data-stu-id="8f32e-174">On the Single Sign-On Settings section, perform the following steps:  ![Configure Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png)</span></span>
     
     <span data-ttu-id="8f32e-175">a.</span><span class="sxs-lookup"><span data-stu-id="8f32e-175">a.</span></span>  <span data-ttu-id="8f32e-176">Wybierz **SAML włączone**.</span><span class="sxs-lookup"><span data-stu-id="8f32e-176">Select **SAML Enabled**.</span></span> 

     <span data-ttu-id="8f32e-177">b.</span><span class="sxs-lookup"><span data-stu-id="8f32e-177">b.</span></span>  <span data-ttu-id="8f32e-178">Kliknij przycisk **Nowy**.</span><span class="sxs-lookup"><span data-stu-id="8f32e-178">Click **New**.</span></span>

12. <span data-ttu-id="8f32e-179">W sekcji SAML jednego ustawienia rejestracji wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="8f32e-179">On the SAML Single Sign-On Settings section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforcesandbox-tutorial/IC781027.png)

    <span data-ttu-id="8f32e-181">a.In pole tekstowe Nazwa wpisz nazwę konfiguracji (np.: *SPSSOWAAD\_testu*).</span><span class="sxs-lookup"><span data-stu-id="8f32e-181">a.In the Name textbox, type the name of the configuration (e.g.: *SPSSOWAAD\_Test*).</span></span> 

    <span data-ttu-id="8f32e-182">b.</span><span class="sxs-lookup"><span data-stu-id="8f32e-182">b.</span></span> <span data-ttu-id="8f32e-183">Wklej **identyfikator jednostki SMAL** wartości do **wystawcy** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="8f32e-183">Paste **SMAL Entity ID** value into the **Issuer** textbox.</span></span>

    <span data-ttu-id="8f32e-184">c.</span><span class="sxs-lookup"><span data-stu-id="8f32e-184">c.</span></span> <span data-ttu-id="8f32e-185">W **identyfikator jednostki** pole tekstowe, typ **https://test.salesforce.com** Jeśli pierwsze wystąpienie piaskownicy Salesforce, które ma zostać dodane do katalogu.</span><span class="sxs-lookup"><span data-stu-id="8f32e-185">In the **Entity Id** textbox, type **https://test.salesforce.com** if it is the first Salesforce Sandbox instance that you are adding to your directory.</span></span> <span data-ttu-id="8f32e-186">Jeśli masz już dodany wystąpienia usług Salesforce piaskownicy, następnie dla **identyfikator jednostki** wpisz **na adres URL logowania**, która powinna być w następującym formacie:`http://company.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="8f32e-186">If you have already added an instance of Salesforce Sandbox, then for the **Entity ID** type in the **Sign On URL**, which should be in this format: `http://company.my.salesforce.com`</span></span>  
 
    <span data-ttu-id="8f32e-187">d.</span><span class="sxs-lookup"><span data-stu-id="8f32e-187">d.</span></span> <span data-ttu-id="8f32e-188">Kliknij przycisk **Przeglądaj** przekazywania pobranego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="8f32e-188">Click **Browse** to upload the downloaded certificate.</span></span>  

    <span data-ttu-id="8f32e-189">e.</span><span class="sxs-lookup"><span data-stu-id="8f32e-189">e.</span></span> <span data-ttu-id="8f32e-190">Jako **typ tożsamości SAML**, wybierz pozycję **potwierdzenia zawiera identyfikator federacji z obiektu użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="8f32e-190">As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.</span></span>
 
    <span data-ttu-id="8f32e-191">f.</span><span class="sxs-lookup"><span data-stu-id="8f32e-191">f.</span></span> <span data-ttu-id="8f32e-192">Jako **lokalizacji tożsamości SAML**, wybierz pozycję **jest tożsamość w elemencie NameIdentifier instrukcji podmiotu**.</span><span class="sxs-lookup"><span data-stu-id="8f32e-192">As **SAML Identity Location**, select **Identity is in the NameIdentifier element of the Subject statement**.</span></span>

    <span data-ttu-id="8f32e-193">g.</span><span class="sxs-lookup"><span data-stu-id="8f32e-193">g.</span></span> <span data-ttu-id="8f32e-194">Wklej **pojedynczy znak na adres URL usługi** do **adresu URL logowania do dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="8f32e-194">Paste **Single Sign-On Service URL** into the **Identity Provider Login URL** textbox.</span></span> 

    <span data-ttu-id="8f32e-195">h.</span><span class="sxs-lookup"><span data-stu-id="8f32e-195">h.</span></span> <span data-ttu-id="8f32e-196">SFDC nie obsługuje SAML wylogowania.</span><span class="sxs-lookup"><span data-stu-id="8f32e-196">SFDC does not support SAML logout.</span></span>  <span data-ttu-id="8f32e-197">Jako obejście, Wklej "https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0" go do **adres URL wylogowania dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="8f32e-197">As a workaround, paste 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' it into the **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="8f32e-198">i.</span><span class="sxs-lookup"><span data-stu-id="8f32e-198">i.</span></span> <span data-ttu-id="8f32e-199">Jako **dostawcy zainicjował żądanie powiązania usługi**, wybierz pozycję **HTTP POST**.</span><span class="sxs-lookup"><span data-stu-id="8f32e-199">As **Service Provider Initiated Request Binding**, select **HTTP POST**.</span></span> 

    <span data-ttu-id="8f32e-200">j.</span><span class="sxs-lookup"><span data-stu-id="8f32e-200">j.</span></span> <span data-ttu-id="8f32e-201">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="8f32e-201">Click **Save**.</span></span>

### <a name="enable-your-domain"></a><span data-ttu-id="8f32e-202">Włącz domeny</span><span class="sxs-lookup"><span data-stu-id="8f32e-202">Enable your domain</span></span>
<span data-ttu-id="8f32e-203">W tej sekcji założono, że już utworzono domeny.</span><span class="sxs-lookup"><span data-stu-id="8f32e-203">This section assumes that you already have created a domain.</span></span>  <span data-ttu-id="8f32e-204">Aby uzyskać więcej informacji, zobacz [Definiowanie Twojej nazwy domeny](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span><span class="sxs-lookup"><span data-stu-id="8f32e-204">For more information, see [Defining Your Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span></span>

<span data-ttu-id="8f32e-205">**Aby włączyć domeny, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="8f32e-205">**To enable your domain, perform the following steps:**</span></span>

1. <span data-ttu-id="8f32e-206">W okienku nawigacji po lewej stronie kliknij **Zarządzanie domenami**, a następnie kliknij przycisk **Moje domeny.**</span><span class="sxs-lookup"><span data-stu-id="8f32e-206">In the left navigation pane, click **Domain Management**, and then click **My Domain.**</span></span>
   
     ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforcesandbox-tutorial/IC781029.png)
   
   >[!NOTE]
   ><span data-ttu-id="8f32e-208">Upewnij się, że poprawnie skonfigurowano domenę.</span><span class="sxs-lookup"><span data-stu-id="8f32e-208">Please make sure that your domain has been configured correctly.</span></span> 

2. <span data-ttu-id="8f32e-209">W **ustawienia strony logowania** kliknij **Edytuj**, następnie jako **usługi uwierzytelniania**, wybierz nazwę SAML pojedynczy znak na ustawienie z poprzedniej sekcji, a na koniec kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="8f32e-209">In the **Login Page Settings** section, click **Edit**, then, as **Authentication Service**, select the name of the SAML Single Sign-On Setting from the previous section, and finally click **Save**.</span></span>
   
   ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforcesandbox-tutorial/IC781030.png)

<span data-ttu-id="8f32e-211">Jak masz domenę skonfigurowane, użytkownicy należy używać URL domeny na potrzeby logowania do usługi Salesforce piaskownicy.</span><span class="sxs-lookup"><span data-stu-id="8f32e-211">As soon as you have a domain configured, your users should use the domain URL to login to the Salesforce sandbox.</span></span>  

<span data-ttu-id="8f32e-212">Aby uzyskać wartość adresu URL, kliknij profil rejestracji Jednokrotnej, utworzony w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="8f32e-212">To get the value of the URL, click the SSO profile you have created in the previous section.</span></span>    

> [!TIP]
> <span data-ttu-id="8f32e-213">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="8f32e-213">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8f32e-214">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="8f32e-214">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8f32e-215">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8f32e-215">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8f32e-216">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f32e-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="8f32e-217">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="8f32e-217">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="8f32e-219">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="8f32e-219">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8f32e-220">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="8f32e-220">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8f32e-222">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="8f32e-222">to display the list of users go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8f32e-224">W górnej części okna dialogowego, kliknij przycisk **Dodaj** otworzyć **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8f32e-224">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8f32e-226">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="8f32e-226">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8f32e-228">a.</span><span class="sxs-lookup"><span data-stu-id="8f32e-228">a.</span></span> <span data-ttu-id="8f32e-229">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8f32e-229">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8f32e-230">b.</span><span class="sxs-lookup"><span data-stu-id="8f32e-230">b.</span></span> <span data-ttu-id="8f32e-231">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8f32e-231">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8f32e-232">c.</span><span class="sxs-lookup"><span data-stu-id="8f32e-232">c.</span></span> <span data-ttu-id="8f32e-233">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="8f32e-233">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8f32e-234">d.</span><span class="sxs-lookup"><span data-stu-id="8f32e-234">d.</span></span> <span data-ttu-id="8f32e-235">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="8f32e-235">Click **Create**.</span></span>
 
### <a name="creating-a-salesforce-sandbox-test-user"></a><span data-ttu-id="8f32e-236">Tworzenie użytkownika testowego piaskownicy usług Salesforce</span><span class="sxs-lookup"><span data-stu-id="8f32e-236">Creating a Salesforce Sandbox test user</span></span>

<span data-ttu-id="8f32e-237">W tej sekcji użytkownika o nazwie Simona Britta jest tworzony w piaskownicy Salesforce.</span><span class="sxs-lookup"><span data-stu-id="8f32e-237">In this section, a user called Britta Simon is created in Salesforce Sandbox.</span></span> <span data-ttu-id="8f32e-238">Piaskownica SalesForce obsługę w czasie, który jest domyślnie włączona.</span><span class="sxs-lookup"><span data-stu-id="8f32e-238">Salesforce Sandbox supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="8f32e-239">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="8f32e-239">There is no action item for you in this section.</span></span> <span data-ttu-id="8f32e-240">Jeśli użytkownik nie istnieje w piaskownicy Salesforce, nowy jest tworzony przy próbie uzyskania dostępu do piaskownicy Salesforce.</span><span class="sxs-lookup"><span data-stu-id="8f32e-240">If a user doesn't already exist in Salesforce Sandbox, a new one is created when you attempt to access Salesforce Sandbox.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8f32e-241">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f32e-241">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8f32e-242">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do piaskownicy Salesforce.</span><span class="sxs-lookup"><span data-stu-id="8f32e-242">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Salesforce Sandbox.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="8f32e-244">**Aby przypisać Simona Britta piaskownicy Salesforce, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="8f32e-244">**To assign Britta Simon to Salesforce Sandbox, perform the following steps:**</span></span>

1. <span data-ttu-id="8f32e-245">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="8f32e-245">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="8f32e-247">Na liście aplikacji zaznacz **piaskownicy Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="8f32e-247">In the applications list, select **Salesforce Sandbox**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_app.png) 

3. <span data-ttu-id="8f32e-249">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="8f32e-249">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="8f32e-251">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8f32e-251">Click **Add** button.</span></span> <span data-ttu-id="8f32e-252">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8f32e-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="8f32e-254">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="8f32e-254">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8f32e-255">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8f32e-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8f32e-256">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8f32e-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8f32e-257">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8f32e-257">Testing single sign-on</span></span>

<span data-ttu-id="8f32e-258">Jeśli chcesz przetestować ustawienia logowania jednokrotnego, otwórz Panel dostępu.</span><span class="sxs-lookup"><span data-stu-id="8f32e-258">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="8f32e-259">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8f32e-259">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8f32e-260">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="8f32e-260">Additional resources</span></span>

* [<span data-ttu-id="8f32e-261">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8f32e-261">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8f32e-262">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8f32e-262">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="8f32e-263">Skonfiguruj Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="8f32e-263">Configure User Provisioning</span></span>](active-directory-saas-salesforce-sandbox-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_203.png

