---
title: 'Samouczek: Integracji Azure Active Directory z miejsca pracy przez Facebook | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i miejsca pracy przez usługi Facebook."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 1590a66f215f0c093d24ff602c0ad951ba1e1eea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a><span data-ttu-id="b3e1e-103">Samouczek: Integracji Azure Active Directory z miejsca pracy przez usługi Facebook</span><span class="sxs-lookup"><span data-stu-id="b3e1e-103">Tutorial: Azure Active Directory integration with Workplace by Facebook</span></span>

<span data-ttu-id="b3e1e-104">Z tego samouczka dowiesz się sposobu integracji z usługą Azure Active Directory (Azure AD) miejsca pracy przez usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-104">In this tutorial, you learn how to integrate Workplace by Facebook with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b3e1e-105">Integrowanie miejsca pracy przez Facebook z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="b3e1e-105">Integrating Workplace by Facebook with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b3e1e-106">Można kontrolować w usłudze Azure AD, który ma dostęp do miejsca pracy przez usługi Facebook</span><span class="sxs-lookup"><span data-stu-id="b3e1e-106">You can control in Azure AD who has access to Workplace by Facebook</span></span>
- <span data-ttu-id="b3e1e-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do miejsca pracy przez Facebook (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b3e1e-107">You can enable your users to automatically get signed-on to Workplace by Facebook (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b3e1e-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="b3e1e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b3e1e-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b3e1e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b3e1e-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b3e1e-110">Prerequisites</span></span>

<span data-ttu-id="b3e1e-111">Aby skonfigurować integrację usługi Azure AD z miejsca pracy przez usługi Facebook, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="b3e1e-111">To configure Azure AD integration with Workplace by Facebook, you need the following items:</span></span>

- <span data-ttu-id="b3e1e-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b3e1e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b3e1e-113">Dołączanie w serwisie Facebook logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="b3e1e-113">A Workplace by Facebook single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b3e1e-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b3e1e-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="b3e1e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b3e1e-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b3e1e-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b3e1e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b3e1e-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="b3e1e-118">Scenario description</span></span>
<span data-ttu-id="b3e1e-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b3e1e-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="b3e1e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b3e1e-121">Dodawanie miejsca pracy przez Facebook z galerii</span><span class="sxs-lookup"><span data-stu-id="b3e1e-121">Adding Workplace by Facebook from the gallery</span></span>
2. <span data-ttu-id="b3e1e-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="b3e1e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workplace-by-facebook-from-the-gallery"></a><span data-ttu-id="b3e1e-123">Dodawanie miejsca pracy przez Facebook z galerii</span><span class="sxs-lookup"><span data-stu-id="b3e1e-123">Adding Workplace by Facebook from the gallery</span></span>
<span data-ttu-id="b3e1e-124">Aby skonfigurować integrację usługi Azure AD miejsca pracy przez usługi Facebook, należy dodać miejsca pracy przez Facebook z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-124">To configure the integration of Workplace by Facebook into Azure AD, you need to add Workplace by Facebook from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b3e1e-125">**Aby dodać miejsce pracy przez Facebook z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="b3e1e-125">**To add Workplace by Facebook from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b3e1e-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="b3e1e-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b3e1e-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="b3e1e-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="b3e1e-133">W polu wyszukiwania wpisz **miejsca pracy przez Facebook**.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-133">In the search box, type **Workplace by Facebook**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_search.png)

5. <span data-ttu-id="b3e1e-135">W panelu wyników wybierz **miejsca pracy przez Facebook**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-135">In the results panel, select **Workplace by Facebook**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b3e1e-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="b3e1e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b3e1e-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z miejsca pracy przez usługi Facebook na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="b3e1e-138">In this section, you configure and test Azure AD single sign-on with Workplace by Facebook based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b3e1e-139">Do rejestracji jednokrotnej do pracy usługi Azure AD musi ustalić użytkownika odpowiednika w miejscu pracy przez Facebook dla użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Workplace by Facebook is to a user in Azure AD.</span></span> <span data-ttu-id="b3e1e-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i danemu użytkownikowi w miejscu pracy przez Facebook musi określone.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-140">In other words, a link relationship between an Azure AD user and the related user in Workplace by Facebook needs to be established.</span></span>

<span data-ttu-id="b3e1e-141">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w miejscu pracy przez usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Workplace by Facebook.</span></span>

<span data-ttu-id="b3e1e-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z miejsca pracy przez usługi Facebook, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="b3e1e-142">To configure and test Azure AD single sign-on with Workplace by Facebook, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b3e1e-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b3e1e-144">**[Konfigurowanie częstotliwości ponowne uwierzytelnianie](#configuring-reauthentication-frequency)**  — Aby skonfigurować miejsca pracy z monitem o wyboru SAML.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-144">**[Configuring Reauthentication Frequency](#configuring-reauthentication-frequency)** - to configure Workplace to prompt for a SAML check.</span></span>
3. <span data-ttu-id="b3e1e-145">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="b3e1e-146">**[Tworzenie pracy przez użytkownika testowego Facebook](#creating-a-workplace-by-facebook-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta miejsca pracy przez Facebook połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-146">**[Creating a Workplace by Facebook test user](#creating-a-workplace-by-facebook-test-user)** - to have a counterpart of Britta Simon in Workplace by Facebook that is linked to the Azure AD representation of user.</span></span>
5. <span data-ttu-id="b3e1e-147">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
6. <span data-ttu-id="b3e1e-148">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b3e1e-149">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="b3e1e-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b3e1e-150">W tej sekcji możesz włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w miejscu pracy przez aplikację usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workplace by Facebook application.</span></span>

<span data-ttu-id="b3e1e-151">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z miejsca pracy przez usługi Facebook, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="b3e1e-151">**To configure Azure AD single sign-on with Workplace by Facebook, perform the following steps:**</span></span>

1. <span data-ttu-id="b3e1e-152">W portalu Azure na **miejsca pracy przez Facebook** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-152">In the Azure portal, on the **Workplace by Facebook** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="b3e1e-154">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. <span data-ttu-id="b3e1e-156">Na **miejsca pracy przez domenę usługi Facebook i adresy URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b3e1e-156">On the **Workplace by Facebook Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_url.png)

    <span data-ttu-id="b3e1e-158">a.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-158">a.</span></span> <span data-ttu-id="b3e1e-159">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<instancename>.facebook.com`</span><span class="sxs-lookup"><span data-stu-id="b3e1e-159">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instancename>.facebook.com`</span></span>

    <span data-ttu-id="b3e1e-160">b.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-160">b.</span></span> <span data-ttu-id="b3e1e-161">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://www.facebook.com/company/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="b3e1e-161">In the **Identifier** textbox, type a URL using the following pattern: `https://www.facebook.com/company/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b3e1e-162">Wartości te nie są rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-162">These values are not the real.</span></span> <span data-ttu-id="b3e1e-163">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-163">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="b3e1e-164">Skontaktuj się z [miejsca pracy przez zespół obsługi klienta usługi Facebook](https://workplace.fb.com/faq/) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-164">Contact [Workplace by Facebook Client support team](https://workplace.fb.com/faq/) to get these values.</span></span> 

4. <span data-ttu-id="b3e1e-165">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-165">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. <span data-ttu-id="b3e1e-167">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-167">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b3e1e-169">Na **miejsca pracy przez konfigurację usługi Facebook** , kliknij przycisk **skonfigurować miejsca pracy przez Facebook** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-169">On the **Workplace by Facebook Configuration** section, click **Configure Workplace by Facebook** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b3e1e-170">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="b3e1e-170">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workplacebyfacebook-tutorial/config.png) 

7. <span data-ttu-id="b3e1e-172">W oknie przeglądarki innej witryny sieci web, zaloguj się do miejsca pracy przez Facebook witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-172">In a different web browser window, login to your Workplace by Facebook company site as an administrator.</span></span>
  
   > [!NOTE] 
   > <span data-ttu-id="b3e1e-173">W ramach procesu uwierzytelniania SAML miejsce pracy mogą używać ciągów zapytań do 2,5 kilobajtów rozmiaru w celu przekazania parametrów do usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-173">As part of the SAML authentication process, Workplace may utilize query strings of up to 2.5 kilobytes in size in order to pass parameters to Azure AD.</span></span>

8. <span data-ttu-id="b3e1e-174">W **pulpitu nawigacyjnego firmy**, przejdź do **uwierzytelniania** kartę.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-174">In the **Company Dashboard**, go to the **Authentication** tab.</span></span>

9. <span data-ttu-id="b3e1e-175">W obszarze **uwierzytelnianie SAML**, wybierz pozycję **logowania jednokrotnego tylko** z listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-175">Under **SAML Authentication**, select **SSO Only** from the drop-down list.</span></span>

10. <span data-ttu-id="b3e1e-176">Wprowadzanie wartości skopiowanych z **miejsca pracy przez konfigurację usługi Facebook** części portalu Azure do odpowiednich pól:</span><span class="sxs-lookup"><span data-stu-id="b3e1e-176">Input the values copied from **Workplace by Facebook Configuration** section of the Azure portal into the corresponding fields:</span></span>

    *   <span data-ttu-id="b3e1e-177">W **adres URL SAML** pole tekstowe, Wklej wartość **pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-177">In **SAML URL** textbox, paste the value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="b3e1e-178">W **pole tekstowe adres URL wystawcy SAML**, Wklej wartość **identyfikator jednostki SAML**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-178">In **SAML Issuer URL textbox**, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="b3e1e-179">W **przekierowania wylogowania SAML** (opcjonalnie), Wklej wartość **Sign-Out URL**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-179">In **SAML Logout Redirect** (Optional), paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="b3e1e-180">Otwórz z **certyfikatu algorytmem base-64** w Notatniku pobrany z portalu Azure, należy skopiować zawartość go do Schowka, a następnie wklej go do **certyfikatu SAML** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-180">Open your **base-64 encoded certificate** in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **SAML Certificate** textbox.</span></span>

11. <span data-ttu-id="b3e1e-181">Musisz wprowadzić adres URL odbiorców, adres URL odbiorcy, i adres URL ACS (usługa konsumenta potwierdzenia) w folderze **Konfiguracja SAML** sekcji.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-181">You may need to enter the Audience URL, Recipient URL, and ACS (Assertion Consumer Service) URL listed under the **SAML Configuration** section.</span></span>

12. <span data-ttu-id="b3e1e-182">Przewiń w dół do sekcji, a następnie kliknij przycisk **Test rejestracji Jednokrotnej** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-182">Scroll to the bottom of the section and click the **Test SSO** button.</span></span> <span data-ttu-id="b3e1e-183">Ten wyniki w oknie podręcznym znajdujących się ze strony logowania usługi Azure AD przedstawione.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-183">This results in a popup window appearing with Azure AD login page presented.</span></span> <span data-ttu-id="b3e1e-184">Wprowadź swoje poświadczenia w normalnie w celu uwierzytelnienia.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-184">Enter your credentials in as normal to authenticate.</span></span> 

    <span data-ttu-id="b3e1e-185">**Rozwiązywanie problemów:** zapewnienia zwracanych wstecz z usługi Azure AD jest taka sama jak konto firmowe, użytkownik jest zalogowany przy użyciu adresu e-mail.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-185">**Troubleshooting:** Ensure the email address being returned back from Azure AD is the same as the Workplace account you are logged in with.</span></span>

13. <span data-ttu-id="b3e1e-186">Po zakończeniu pomyślnie testu, przewiń w dół strony i kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-186">Once the test has been completed successfully, scroll to the bottom of the page and click the **Save** button.</span></span>

14. <span data-ttu-id="b3e1e-187">Wszyscy użytkownicy korzystający z miejsca pracy zostanie teraz wyświetlone strony logowania usługi Azure AD do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-187">All users using Workplace will now be presented with Azure AD login page for authentication.</span></span>

15. <span data-ttu-id="b3e1e-188">**SAML wylogowania przekierowania (opcjonalnie)** -</span><span class="sxs-lookup"><span data-stu-id="b3e1e-188">**SAML Logout Redirect (optional)** -</span></span> 

    <span data-ttu-id="b3e1e-189">Można opcjonalnie skonfigurować SAML Url wylogowania, którego można użyć, aby wskazywały na strony wylogowania usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-189">You can choose to optionally configure a SAML Logout Url, which can be used to point at Azure AD's logout page.</span></span> <span data-ttu-id="b3e1e-190">Gdy to ustawienie jest włączone i skonfigurowane, użytkownik nie jest już będzie kierowany do strony wylogowania w miejscu pracy.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-190">When this setting is enabled and configured, the user will no longer be directed to the Workplace logout page.</span></span> <span data-ttu-id="b3e1e-191">Zamiast tego użytkownik zostanie przekierowany do adresu url, który został dodany w ustawieniu przekierowania wylogowania SAML.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-191">Instead, the user will be redirected to the url that was added in the SAML Logout Redirect setting.</span></span>


> [!TIP]
> <span data-ttu-id="b3e1e-192">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="b3e1e-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b3e1e-193">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b3e1e-194">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b3e1e-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="configuring-reauthentication-frequency"></a><span data-ttu-id="b3e1e-195">Konfigurowanie częstotliwości ponowne uwierzytelnianie</span><span class="sxs-lookup"><span data-stu-id="b3e1e-195">Configuring Reauthentication Frequency</span></span>

<span data-ttu-id="b3e1e-196">Można skonfigurować miejsca pracy, aby monitować wyboru SAML co dzień, trzech dni, tygodni, dwóch tygodni, miesięcy lub nigdy.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-196">You can configure Workplace to prompt for a SAML check every day, three days, week, two weeks, month or never.</span></span>

> [!NOTE] 
><span data-ttu-id="b3e1e-197">Minimalna wartość wyboru SAML na aplikacje mobilne wynosi tydzień.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-197">The minimum value for the SAML check on mobile applications is set to one week.</span></span>

<span data-ttu-id="b3e1e-198">Możesz też wymusić SAML zresetować dla wszystkich użytkowników za pomocą przycisku: Wymagaj SAML uwierzytelnianie dla wszystkich użytkowników.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-198">You can also force a SAML reset for all users using the button: Require SAML authentication for all users now.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b3e1e-199">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b3e1e-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="b3e1e-200">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="b3e1e-202">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="b3e1e-202">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b3e1e-203">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-203">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b3e1e-205">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-205">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b3e1e-207">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-207">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b3e1e-209">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b3e1e-209">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b3e1e-211">a.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-211">a.</span></span> <span data-ttu-id="b3e1e-212">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-212">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b3e1e-213">b.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-213">b.</span></span> <span data-ttu-id="b3e1e-214">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b3e1e-215">c.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-215">c.</span></span> <span data-ttu-id="b3e1e-216">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-216">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b3e1e-217">d.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-217">d.</span></span> <span data-ttu-id="b3e1e-218">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-218">Click **Create**.</span></span>
 
### <a name="creating-a-workplace-by-facebook-test-user"></a><span data-ttu-id="b3e1e-219">Tworzenie pracy przez użytkownika testowego usługi Facebook</span><span class="sxs-lookup"><span data-stu-id="b3e1e-219">Creating a Workplace by Facebook test user</span></span>

<span data-ttu-id="b3e1e-220">W tej sekcji o nazwie Simona Britta tworzenia użytkownika w miejscu pracy przez usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-220">In this section, a user called Britta Simon is created in Workplace by Facebook.</span></span> <span data-ttu-id="b3e1e-221">Obszar roboczy w serwisie Facebook obsługę w czasie, który jest domyślnie włączona.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-221">Workplace by Facebook supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="b3e1e-222">Brak akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-222">There is no action for you in this section.</span></span> <span data-ttu-id="b3e1e-223">Jeśli użytkownik nie istnieje w miejscu pracy przez usługi Facebook, nowy jest tworzona przy próbie uzyskania dostępu do miejsca pracy przez usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-223">If a user doesn't exist in Workplace by Facebook, a new one is created when you attempt to access Workplace by Facebook.</span></span>

>[!Note]
><span data-ttu-id="b3e1e-224">Jeśli trzeba ręcznie utworzyć użytkownika, skontaktuj się z [miejsca pracy przez zespół obsługi klienta usługi Facebook](https://workplace.fb.com/faq/)</span><span class="sxs-lookup"><span data-stu-id="b3e1e-224">If you need to create a user manually, Contact [Workplace by Facebook Client support team](https://workplace.fb.com/faq/)</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b3e1e-225">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b3e1e-225">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b3e1e-226">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do miejsca pracy przez usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workplace by Facebook.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="b3e1e-228">**Aby przypisać Simona Britta do miejsca pracy przez usługi Facebook, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="b3e1e-228">**To assign Britta Simon to Workplace by Facebook, perform the following steps:**</span></span>

1. <span data-ttu-id="b3e1e-229">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="b3e1e-231">Na liście aplikacji zaznacz **miejsca pracy przez Facebook**.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-231">In the applications list, select **Workplace by Facebook**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_app.png) 

3. <span data-ttu-id="b3e1e-233">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-233">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="b3e1e-235">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-235">Click **Add** button.</span></span> <span data-ttu-id="b3e1e-236">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="b3e1e-238">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b3e1e-239">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b3e1e-240">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b3e1e-241">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="b3e1e-241">Testing single sign-on</span></span>

<span data-ttu-id="b3e1e-242">Jeśli chcesz przetestować jednego ustawienia logowania jednokrotnego, otwórz Panel dostępu.</span><span class="sxs-lookup"><span data-stu-id="b3e1e-242">If you want to test your single sign-on settings, open the Access Panel.</span></span>
<span data-ttu-id="b3e1e-243">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b3e1e-243">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="b3e1e-244">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="b3e1e-244">Additional resources</span></span>

* [<span data-ttu-id="b3e1e-245">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b3e1e-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b3e1e-246">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b3e1e-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="b3e1e-247">Skonfiguruj Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="b3e1e-247">Configure User Provisioning</span></span>](active-directory-saas-workplacebyfacebook-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_203.png

