---
title: 'Samouczek: Azure Active Directory integracji z produktem Workday | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i dzień roboczy."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e9da692e-4a65-4231-8ab3-bc9a87b10bca
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 164d5c644f120fa86e2b690649241892764b64b7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workday"></a><span data-ttu-id="710a7-103">Samouczek: Azure Active Directory integracji z produktem Workday</span><span class="sxs-lookup"><span data-stu-id="710a7-103">Tutorial: Azure Active Directory integration with Workday</span></span>

<span data-ttu-id="710a7-104">Z tego samouczka dowiesz się integrowanie pracy z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="710a7-104">In this tutorial, you learn how to integrate Workday with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="710a7-105">Integrowanie pracy z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="710a7-105">Integrating Workday with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="710a7-106">Można kontrolować w usłudze Azure AD, który ma dostęp do produktu Workday</span><span class="sxs-lookup"><span data-stu-id="710a7-106">You can control in Azure AD who has access to Workday</span></span>
- <span data-ttu-id="710a7-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do produktu Workday (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="710a7-107">You can enable your users to automatically get signed-on to Workday (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="710a7-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="710a7-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="710a7-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="710a7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="710a7-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="710a7-110">Prerequisites</span></span>

<span data-ttu-id="710a7-111">Aby skonfigurować integrację usługi Azure AD z produktem Workday, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="710a7-111">To configure Azure AD integration with Workday, you need the following items:</span></span>

- <span data-ttu-id="710a7-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="710a7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="710a7-113">Produktu Workday jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="710a7-113">A Workday single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="710a7-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="710a7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="710a7-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="710a7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="710a7-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="710a7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="710a7-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="710a7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="710a7-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="710a7-118">Scenario description</span></span>
<span data-ttu-id="710a7-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="710a7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="710a7-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="710a7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="710a7-121">Dodawanie produktu Workday z galerii</span><span class="sxs-lookup"><span data-stu-id="710a7-121">Adding Workday from the gallery</span></span>
2. <span data-ttu-id="710a7-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="710a7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workday-from-the-gallery"></a><span data-ttu-id="710a7-123">Dodawanie produktu Workday z galerii</span><span class="sxs-lookup"><span data-stu-id="710a7-123">Adding Workday from the gallery</span></span>
<span data-ttu-id="710a7-124">Aby skonfigurować integrację z produktu Workday do usługi Azure AD, należy dodać produktu Workday z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="710a7-124">To configure the integration of Workday into Azure AD, you need to add Workday from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="710a7-125">**Aby dodać produktu Workday z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="710a7-125">**To add Workday from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="710a7-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="710a7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="710a7-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="710a7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="710a7-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="710a7-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="710a7-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="710a7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="710a7-133">W polu wyszukiwania wpisz **produktu Workday**.</span><span class="sxs-lookup"><span data-stu-id="710a7-133">In the search box, type **Workday**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-workday-tutorial/tutorial_workday_search.png)

5. <span data-ttu-id="710a7-135">W panelu wyników wybierz **produktu Workday**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="710a7-135">In the results panel, select **Workday**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-workday-tutorial/tutorial_workday_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="710a7-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="710a7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="710a7-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z produktu Workday oparte na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="710a7-138">In this section, you configure and test Azure AD single sign-on with Workday based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="710a7-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w produktu Workday jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="710a7-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Workday is to a user in Azure AD.</span></span> <span data-ttu-id="710a7-140">Innymi słowy musi można ustanowić łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w pracy.</span><span class="sxs-lookup"><span data-stu-id="710a7-140">In other words, a link relationship between an Azure AD user and the related user in Workday needs to be established.</span></span>

<span data-ttu-id="710a7-141">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w pracy.</span><span class="sxs-lookup"><span data-stu-id="710a7-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Workday.</span></span>

<span data-ttu-id="710a7-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z produktem Workday, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="710a7-142">To configure and test Azure AD single sign-on with Workday, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="710a7-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="710a7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="710a7-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="710a7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="710a7-145">**[Tworzenie użytkownika testowego produktu Workday](#creating-a-workday-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta produktu Workday połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="710a7-145">**[Creating a Workday test user](#creating-a-workday-test-user)** - to have a counterpart of Britta Simon in Workday that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="710a7-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="710a7-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="710a7-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="710a7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="710a7-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="710a7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="710a7-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji produktu Workday.</span><span class="sxs-lookup"><span data-stu-id="710a7-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workday application.</span></span>

<span data-ttu-id="710a7-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z produktem Workday, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="710a7-150">**To configure Azure AD single sign-on with Workday, perform the following steps:**</span></span>

1. <span data-ttu-id="710a7-151">W portalu Azure na **produktu Workday** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="710a7-151">In the Azure portal, on the **Workday** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="710a7-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="710a7-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workday-tutorial/tutorial_workday_samlbase.png)

3. <span data-ttu-id="710a7-155">Na **produktu Workday domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="710a7-155">On the **Workday Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workday-tutorial/tutorial_workday_url.png)

    <span data-ttu-id="710a7-157">a.</span><span class="sxs-lookup"><span data-stu-id="710a7-157">a.</span></span> <span data-ttu-id="710a7-158">W **adres URL logowania** tekstowym, wpisz wartość, jak:`https://impl.workday.com/<tenant>/login-saml2.htmld`</span><span class="sxs-lookup"><span data-stu-id="710a7-158">In the **Sign-on URL** textbox, type the value as: `https://impl.workday.com/<tenant>/login-saml2.htmld`</span></span>

    <span data-ttu-id="710a7-159">b.</span><span class="sxs-lookup"><span data-stu-id="710a7-159">b.</span></span> <span data-ttu-id="710a7-160">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://impl.workday.com/<tenant>/login-saml.htmld`</span><span class="sxs-lookup"><span data-stu-id="710a7-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://impl.workday.com/<tenant>/login-saml.htmld`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="710a7-161">Wartości te nie są rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="710a7-161">These values are not the real.</span></span> <span data-ttu-id="710a7-162">Rzeczywisty adres URL logowania i adres URL odpowiedzi, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="710a7-162">Update these values with the actual Sign-on URL and Reply URL.</span></span> <span data-ttu-id="710a7-163">Adres URL odpowiedzi muszą mieć poddomeny na przykład: www, wd2, wd3, wd3 impl, wd5, wd5 impl).</span><span class="sxs-lookup"><span data-stu-id="710a7-163">Your reply URL must have a subdomain for example: www, wd2, wd3, wd3-impl, wd5, wd5-impl).</span></span> <span data-ttu-id="710a7-164">Przy użyciu przypominać "*http://www.myworkday.com*" działa, ale "*http://myworkday.com*" nie ma.</span><span class="sxs-lookup"><span data-stu-id="710a7-164">Using something like "*http://www.myworkday.com*" works but "*http://myworkday.com*" does not.</span></span> <span data-ttu-id="710a7-165">Skontaktuj się z [zespołem pomocy technicznej klienta produktu Workday](https://www.workday.com/en-us/partners-services/services/support.html) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="710a7-165">Contact [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) to get these values.</span></span> 
 

4. <span data-ttu-id="710a7-166">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="710a7-166">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workday-tutorial/tutorial_workday_certificate.png) 

5. <span data-ttu-id="710a7-168">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="710a7-168">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workday-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="710a7-170">Na **konfiguracji produktu Workday** kliknij **Konfigurowanie produktu Workday** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="710a7-170">On the **Workday Configuration** section, click **Configure Workday** to open **Configure sign-on** window.</span></span> <span data-ttu-id="710a7-171">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="710a7-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    <span data-ttu-id="710a7-172">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workday-tutorial/tutorial_workday_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="710a7-172">![Configure Single Sign-On](./media/active-directory-saas-workday-tutorial/tutorial_workday_configure.png) 
<CS></span></span>
7. <span data-ttu-id="710a7-173">W oknie przeglądarki innej witryny sieci web należy zalogować się jako administrator do witryny firmy produktu Workday.</span><span class="sxs-lookup"><span data-stu-id="710a7-173">In a different web browser window, log in to your Workday company site as an administrator.</span></span>

8. <span data-ttu-id="710a7-174">Przejdź do **Menu \> Workbench**.</span><span class="sxs-lookup"><span data-stu-id="710a7-174">Go to **Menu \> Workbench**.</span></span>
   
    <span data-ttu-id="710a7-175">![Workbench](./media/active-directory-saas-workday-tutorial/IC782923.png "Workbench")</span><span class="sxs-lookup"><span data-stu-id="710a7-175">![Workbench](./media/active-directory-saas-workday-tutorial/IC782923.png "Workbench")</span></span>

9. <span data-ttu-id="710a7-176">Przejdź do **konta administracji**.</span><span class="sxs-lookup"><span data-stu-id="710a7-176">Go to **Account Administration**.</span></span>
   
    <span data-ttu-id="710a7-177">![Konto administracji](./media/active-directory-saas-workday-tutorial/IC782924.png "konta administracji")</span><span class="sxs-lookup"><span data-stu-id="710a7-177">![Account Administration](./media/active-directory-saas-workday-tutorial/IC782924.png "Account Administration")</span></span>

10. <span data-ttu-id="710a7-178">Przejdź do **Edytuj ustawienia dzierżawy — zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="710a7-178">Go to **Edit Tenant Setup – Security**.</span></span>
   
    <span data-ttu-id="710a7-179">![Edytuj zabezpieczenia dzierżawy](./media/active-directory-saas-workday-tutorial/IC782925.png "Edytuj zabezpieczenia dzierżawy")</span><span class="sxs-lookup"><span data-stu-id="710a7-179">![Edit Tenant Security](./media/active-directory-saas-workday-tutorial/IC782925.png "Edit Tenant Security")</span></span>

11. <span data-ttu-id="710a7-180">W **adresów URL przekierowań** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="710a7-180">In the **Redirection URLs** section, perform the following steps:</span></span>
   
    <span data-ttu-id="710a7-181">![Adresy URL przekierowania](./media/active-directory-saas-workday-tutorial/IC7829581.png "adresów URL przekierowań")</span><span class="sxs-lookup"><span data-stu-id="710a7-181">![Redirection URLs](./media/active-directory-saas-workday-tutorial/IC7829581.png "Redirection URLs")</span></span>
   
    <span data-ttu-id="710a7-182">a.</span><span class="sxs-lookup"><span data-stu-id="710a7-182">a.</span></span> <span data-ttu-id="710a7-183">Kliknij przycisk **Dodaj wiersz**.</span><span class="sxs-lookup"><span data-stu-id="710a7-183">Click **Add Row**.</span></span>
   
    <span data-ttu-id="710a7-184">b.</span><span class="sxs-lookup"><span data-stu-id="710a7-184">b.</span></span> <span data-ttu-id="710a7-185">W **Przekierowywanie adresu URL logowania do** pole tekstowe i **adresem URL przekierowania Mobile** pole tekstowe, typ **adres URL logowania** zostały wprowadzone na **produktu Workday domeny i adres URL** części portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="710a7-185">In the **Login Redirect URL** textbox and the **Mobile Redirect URL** textbox, type the **Sign-on URL** you have entered on the **Workday Domain and URLs** section of the Azure portal.</span></span>
   
    <span data-ttu-id="710a7-186">c.</span><span class="sxs-lookup"><span data-stu-id="710a7-186">c.</span></span> <span data-ttu-id="710a7-187">W portalu Azure na **konfigurowania rejestracji** okna, kopiowania **Sign-Out adres URL**, a następnie wklej go do **adresem URL przekierowania wylogowania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="710a7-187">In the Azure portal, on the **Configure sign-on** window, copy the **Sign-Out URL**, and then paste it into the **Logout Redirect URL** textbox.</span></span>
   
    <span data-ttu-id="710a7-188">d.</span><span class="sxs-lookup"><span data-stu-id="710a7-188">d.</span></span>  <span data-ttu-id="710a7-189">W **środowiska** tekstowym, wpisz nazwę środowiska.</span><span class="sxs-lookup"><span data-stu-id="710a7-189">In **Environment** textbox, type the environment name.</span></span>  

    >[!NOTE]
    > <span data-ttu-id="710a7-190">Wartość atrybutu środowisko jest powiązany z wartością adres URL dzierżawy:</span><span class="sxs-lookup"><span data-stu-id="710a7-190">The value of the Environment attribute is tied to the value of the tenant URL:</span></span>  
    ><span data-ttu-id="710a7-191">— Czy nazwy domeny adresu URL dzierżawy produktu Workday rozpoczyna się od impl na przykład: *https://impl.workday.com/\<dzierżawy\>/login-saml2.htmld*), **środowiska** atrybutu należy wybrać opcję implementacji.</span><span class="sxs-lookup"><span data-stu-id="710a7-191">-If the domain name of the Workday tenant URL starts with impl for example: *https://impl.workday.com/\<tenant\>/login-saml2.htmld*), the **Environment** attribute must be set to Implementation.</span></span>  
    ><span data-ttu-id="710a7-192">— Jeśli nazwa domeny rozpoczynają się od czegoś innego, należy skontaktować się [zespołem pomocy technicznej klienta produktu Workday](https://www.workday.com/en-us/partners-services/services/support.html) uzyskanie odpowiedniego **środowiska** wartość.</span><span class="sxs-lookup"><span data-stu-id="710a7-192">-If the domain name starts with something else, you need to contact [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) to get the matching **Environment** value.</span></span>

12. <span data-ttu-id="710a7-193">W **Instalatora SAML** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="710a7-193">In the **SAML Setup** section, perform the following steps:</span></span>
   
    <span data-ttu-id="710a7-194">![Instalator SAML](./media/active-directory-saas-workday-tutorial/IC782926.png "Instalatora SAML")</span><span class="sxs-lookup"><span data-stu-id="710a7-194">![SAML Setup](./media/active-directory-saas-workday-tutorial/IC782926.png "SAML Setup")</span></span>
   
    <span data-ttu-id="710a7-195">a.</span><span class="sxs-lookup"><span data-stu-id="710a7-195">a.</span></span>  <span data-ttu-id="710a7-196">Wybierz **włączyć uwierzytelnianie SAML**.</span><span class="sxs-lookup"><span data-stu-id="710a7-196">Select **Enable SAML Authentication**.</span></span>
   
    <span data-ttu-id="710a7-197">b.</span><span class="sxs-lookup"><span data-stu-id="710a7-197">b.</span></span>  <span data-ttu-id="710a7-198">Kliknij przycisk **Dodaj wiersz**.</span><span class="sxs-lookup"><span data-stu-id="710a7-198">Click **Add Row**.</span></span>

13. <span data-ttu-id="710a7-199">W sekcji SAML dostawcy tożsamości wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="710a7-199">In the SAML Identity Providers section, perform the following steps:</span></span>
   
    <span data-ttu-id="710a7-200">![Dostawców tożsamości SAML](./media/active-directory-saas-workday-tutorial/IC7829271.png "dostawców tożsamości SAML")</span><span class="sxs-lookup"><span data-stu-id="710a7-200">![SAML Identity Providers](./media/active-directory-saas-workday-tutorial/IC7829271.png "SAML Identity Providers")</span></span>
   
    <span data-ttu-id="710a7-201">a.</span><span class="sxs-lookup"><span data-stu-id="710a7-201">a.</span></span> <span data-ttu-id="710a7-202">W polu tekstowym Nazwa dostawcy tożsamości, wpisz nazwę dostawcy (na przykład: *SPInitiatedSSO*).</span><span class="sxs-lookup"><span data-stu-id="710a7-202">In the Identity Provider Name textbox, type a provider name (for example: *SPInitiatedSSO*).</span></span>
   
    <span data-ttu-id="710a7-203">b.</span><span class="sxs-lookup"><span data-stu-id="710a7-203">b.</span></span> <span data-ttu-id="710a7-204">W portalu Azure na **Konfigurowanie logowania jednokrotnego** okna, kopiowania **identyfikator jednostki SAML** wartość, a następnie wklej ją do **wystawcy** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="710a7-204">In the Azure portal, on the **Configure sign-on** window, copy the **SAML Entity ID** value, and then paste it into the **Issuer** textbox.</span></span>
   
    <span data-ttu-id="710a7-205">c.</span><span class="sxs-lookup"><span data-stu-id="710a7-205">c.</span></span> <span data-ttu-id="710a7-206">Wybierz **włączyć Workday wylogowania inicjowane**.</span><span class="sxs-lookup"><span data-stu-id="710a7-206">Select **Enable Workday Initiated Logout**.</span></span>
   
    <span data-ttu-id="710a7-207">d.</span><span class="sxs-lookup"><span data-stu-id="710a7-207">d.</span></span> <span data-ttu-id="710a7-208">W portalu Azure na **Konfigurowanie logowania jednokrotnego** okna, kopiowania **Sign-Out URL** wartość, a następnie wklej ją do **adresu URL wylogowania żądania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="710a7-208">In the Azure portal, on the **Configure sign-on** window, copy the **Sign-Out URL** value, and then paste it into the **Logout Request URL** textbox.</span></span>

    <span data-ttu-id="710a7-209">e.</span><span class="sxs-lookup"><span data-stu-id="710a7-209">e.</span></span> <span data-ttu-id="710a7-210">Kliknij przycisk **certyfikatu klucza publicznego dostawcy tożsamości**, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="710a7-210">Click **Identity Provider Public Key Certificate**, and then click **Create**.</span></span> 

    <span data-ttu-id="710a7-211">![Utwórz](./media/active-directory-saas-workday-tutorial/IC782928.png "tworzenie")</span><span class="sxs-lookup"><span data-stu-id="710a7-211">![Create](./media/active-directory-saas-workday-tutorial/IC782928.png "Create")</span></span>

    <span data-ttu-id="710a7-212">f.</span><span class="sxs-lookup"><span data-stu-id="710a7-212">f.</span></span> <span data-ttu-id="710a7-213">Kliknij przycisk **x509 Utwórz klucz publiczny**.</span><span class="sxs-lookup"><span data-stu-id="710a7-213">Click **Create x509 Public Key**.</span></span> 

    <span data-ttu-id="710a7-214">![Utwórz](./media/active-directory-saas-workday-tutorial/IC782929.png "tworzenie")</span><span class="sxs-lookup"><span data-stu-id="710a7-214">![Create](./media/active-directory-saas-workday-tutorial/IC782929.png "Create")</span></span>


14. <span data-ttu-id="710a7-215">W **klucza publicznego widoku x509** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="710a7-215">In the **View x509 Public Key** section, perform the following steps:</span></span> 
   
    <span data-ttu-id="710a7-216">![Klucz publiczny widoku x509](./media/active-directory-saas-workday-tutorial/IC782930.png "widoku x509 klucza publicznego")</span><span class="sxs-lookup"><span data-stu-id="710a7-216">![View x509 Public Key](./media/active-directory-saas-workday-tutorial/IC782930.png "View x509 Public Key")</span></span> 
   
    <span data-ttu-id="710a7-217">a.</span><span class="sxs-lookup"><span data-stu-id="710a7-217">a.</span></span> <span data-ttu-id="710a7-218">W **nazwa** tekstowym, wpisz nazwę dla certyfikatu (na przykład: *ŚOI\_SP*).</span><span class="sxs-lookup"><span data-stu-id="710a7-218">In the **Name** textbox, type a name for your certificate (for example: *PPE\_SP*).</span></span>
   
    <span data-ttu-id="710a7-219">b.</span><span class="sxs-lookup"><span data-stu-id="710a7-219">b.</span></span> <span data-ttu-id="710a7-220">W **ważny od** tekstowym, wpisz poprawna wartość atrybutu certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="710a7-220">In the **Valid From** textbox, type the valid from attribute value of your certificate.</span></span>
   
    <span data-ttu-id="710a7-221">c.</span><span class="sxs-lookup"><span data-stu-id="710a7-221">c.</span></span>  <span data-ttu-id="710a7-222">W **ważny do** tekstowym, wpisz prawidłową wartość atrybutu certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="710a7-222">In the **Valid To** textbox, type the valid to attribute value of your certificate.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="710a7-223">Możesz uzyskać prawidłową z datę i poprawna data z pobranego certyfikatu, kliknij go dwukrotnie.</span><span class="sxs-lookup"><span data-stu-id="710a7-223">You can get the valid from date and the valid to date from the downloaded certificate by double-clicking it.</span></span>  <span data-ttu-id="710a7-224">Daty są wyświetlane w obszarze **szczegóły** kartę.</span><span class="sxs-lookup"><span data-stu-id="710a7-224">The dates are listed under the **Details** tab.</span></span>
    > 
    >
   
    <span data-ttu-id="710a7-225">d.</span><span class="sxs-lookup"><span data-stu-id="710a7-225">d.</span></span>  <span data-ttu-id="710a7-226">Otwórz w Notatniku certyfikatu zakodowanego base-64, a następnie skopiuj zawartość tego.</span><span class="sxs-lookup"><span data-stu-id="710a7-226">Open your base-64 encoded certificate in notepad, and then copy the content of it.</span></span>
   
    <span data-ttu-id="710a7-227">e.</span><span class="sxs-lookup"><span data-stu-id="710a7-227">e.</span></span>  <span data-ttu-id="710a7-228">W **certyfikatu** pole tekstowe, Wklej zawartość Schowka.</span><span class="sxs-lookup"><span data-stu-id="710a7-228">In the **Certificate** textbox, paste the content of your clipboard.</span></span>
   
    <span data-ttu-id="710a7-229">f.</span><span class="sxs-lookup"><span data-stu-id="710a7-229">f.</span></span>  <span data-ttu-id="710a7-230">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="710a7-230">Click **OK**.</span></span>

15. <span data-ttu-id="710a7-231">Wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="710a7-231">Perform the following steps:</span></span> 
   
    <span data-ttu-id="710a7-232">![Konfiguracja rejestracji Jednokrotnej](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguratio.png "konfiguracji logowania jednokrotnego")</span><span class="sxs-lookup"><span data-stu-id="710a7-232">![SSO configuration](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguratio.png "SSO configuration")</span></span>
   
    <span data-ttu-id="710a7-233">a.</span><span class="sxs-lookup"><span data-stu-id="710a7-233">a.</span></span>  <span data-ttu-id="710a7-234">Włącz **x509 pary klucza prywatnego**.</span><span class="sxs-lookup"><span data-stu-id="710a7-234">Enable the **x509 Private Key Pair**.</span></span>
   
    <span data-ttu-id="710a7-235">b.</span><span class="sxs-lookup"><span data-stu-id="710a7-235">b.</span></span>  <span data-ttu-id="710a7-236">W **identyfikator dostawcy usługi** pole tekstowe, typ **http://www.workday.com**.</span><span class="sxs-lookup"><span data-stu-id="710a7-236">In the **Service Provider ID** textbox, type **http://www.workday.com**.</span></span>
   
    <span data-ttu-id="710a7-237">c.</span><span class="sxs-lookup"><span data-stu-id="710a7-237">c.</span></span>  <span data-ttu-id="710a7-238">Wybierz **Włącz SP zainicjował uwierzytelnianie SAML**.</span><span class="sxs-lookup"><span data-stu-id="710a7-238">Select **Enable SP Initiated SAML Authentication**.</span></span>
   
    <span data-ttu-id="710a7-239">d.</span><span class="sxs-lookup"><span data-stu-id="710a7-239">d.</span></span>  <span data-ttu-id="710a7-240">W portalu Azure na **Konfigurowanie logowania jednokrotnego** okna, kopiowania **SAML pojedynczy znak na adres URL usługi** wartość, a następnie wklej ją do **adres URL usługi logowania jednokrotnego IdP** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="710a7-240">In the Azure portal, on the **Configure sign-on** window, copy the **SAML Single Sign-On Service URL** value, and then paste it into the **IdP SSO Service URL** textbox.</span></span>
   
    <span data-ttu-id="710a7-241">e.</span><span class="sxs-lookup"><span data-stu-id="710a7-241">e.</span></span> <span data-ttu-id="710a7-242">Wybierz **nie Deflate żądania uwierzytelnienia zainicjowane SP**.</span><span class="sxs-lookup"><span data-stu-id="710a7-242">Select **Do Not Deflate SP-initiated Authentication Request**.</span></span>
   
    <span data-ttu-id="710a7-243">f.</span><span class="sxs-lookup"><span data-stu-id="710a7-243">f.</span></span> <span data-ttu-id="710a7-244">Jako **podpisu żądania uwierzytelnienia**, wybierz pozycję **SHA256**.</span><span class="sxs-lookup"><span data-stu-id="710a7-244">As **Authentication Request Signature Method**, select **SHA256**.</span></span> 
   
    <span data-ttu-id="710a7-245">![Metoda podpisu żądania uwierzytelniania](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguration.png "metoda podpisu żądania uwierzytelniania")</span><span class="sxs-lookup"><span data-stu-id="710a7-245">![Authentication Request Signature Method](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguration.png "Authentication Request Signature Method")</span></span> 
   
    <span data-ttu-id="710a7-246">g.</span><span class="sxs-lookup"><span data-stu-id="710a7-246">g.</span></span> <span data-ttu-id="710a7-247">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="710a7-247">Click **OK**.</span></span> 
   
    <span data-ttu-id="710a7-248">![OK](./media/active-directory-saas-workday-tutorial/IC782933.png "OK")
<CE></span><span class="sxs-lookup"><span data-stu-id="710a7-248">![OK](./media/active-directory-saas-workday-tutorial/IC782933.png "OK")
<CE></span></span>

> [!TIP]
> <span data-ttu-id="710a7-249">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="710a7-249">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="710a7-250">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="710a7-250">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="710a7-251">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="710a7-251">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="710a7-252">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="710a7-252">Creating an Azure AD test user</span></span>
<span data-ttu-id="710a7-253">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="710a7-253">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="710a7-255">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="710a7-255">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="710a7-256">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="710a7-256">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="710a7-258">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="710a7-258">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="710a7-260">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="710a7-260">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="710a7-262">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="710a7-262">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="710a7-264">a.</span><span class="sxs-lookup"><span data-stu-id="710a7-264">a.</span></span> <span data-ttu-id="710a7-265">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="710a7-265">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="710a7-266">b.</span><span class="sxs-lookup"><span data-stu-id="710a7-266">b.</span></span> <span data-ttu-id="710a7-267">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="710a7-267">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="710a7-268">c.</span><span class="sxs-lookup"><span data-stu-id="710a7-268">c.</span></span> <span data-ttu-id="710a7-269">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="710a7-269">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="710a7-270">d.</span><span class="sxs-lookup"><span data-stu-id="710a7-270">d.</span></span> <span data-ttu-id="710a7-271">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="710a7-271">Click **Create**.</span></span>
 
### <a name="creating-a-workday-test-user"></a><span data-ttu-id="710a7-272">Tworzenie użytkownika testowego produktu Workday</span><span class="sxs-lookup"><span data-stu-id="710a7-272">Creating a Workday test user</span></span>

<span data-ttu-id="710a7-273">Aby uzyskać udostępnione do produktu Workday użytkownika testowego, należy skontaktować się [zespołem pomocy technicznej klienta produktu Workday](https://www.workday.com/en-us/partners-services/services/support.html).</span><span class="sxs-lookup"><span data-stu-id="710a7-273">To get a test user provisioned into Workday, you need to contact the [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html).</span></span>
<span data-ttu-id="710a7-274">[Zespołem pomocy technicznej klienta produktu Workday](https://www.workday.com/en-us/partners-services/services/support.html) tworzy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="710a7-274">The [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) creates the user for you.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="710a7-275">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="710a7-275">Assigning the Azure AD test user</span></span>

<span data-ttu-id="710a7-276">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do produktu Workday.</span><span class="sxs-lookup"><span data-stu-id="710a7-276">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workday.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="710a7-278">**Aby przypisać Simona Britta do produktu Workday, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="710a7-278">**To assign Britta Simon to Workday, perform the following steps:**</span></span>

1. <span data-ttu-id="710a7-279">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="710a7-279">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="710a7-281">Na liście aplikacji zaznacz **produktu Workday**.</span><span class="sxs-lookup"><span data-stu-id="710a7-281">In the applications list, select **Workday**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workday-tutorial/tutorial_workday_app.png) 

3. <span data-ttu-id="710a7-283">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="710a7-283">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="710a7-285">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="710a7-285">Click **Add** button.</span></span> <span data-ttu-id="710a7-286">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="710a7-286">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="710a7-288">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="710a7-288">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="710a7-289">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="710a7-289">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="710a7-290">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="710a7-290">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="710a7-291">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="710a7-291">Testing single sign-on</span></span>

<span data-ttu-id="710a7-292">Jeśli chcesz przetestować jednego ustawienia logowania jednokrotnego, otwórz Panel dostępu.</span><span class="sxs-lookup"><span data-stu-id="710a7-292">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="710a7-293">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="710a7-293">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="710a7-294">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="710a7-294">Additional resources</span></span>

* [<span data-ttu-id="710a7-295">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="710a7-295">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="710a7-296">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="710a7-296">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="710a7-297">Skonfiguruj Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="710a7-297">Configure User Provisioning</span></span>](active-directory-saas-workday-inbound-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workday-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workday-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workday-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workday-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workday-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workday-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workday-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workday-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workday-tutorial/tutorial_general_203.png

