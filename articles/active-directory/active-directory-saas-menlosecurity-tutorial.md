---
title: 'Samouczek: Azure Active Directory integracji z zabezpieczeniami Menlo | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Menlo zabezpieczeń."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9e63fe6b-0ad0-405d-9e41-6a1a40a41df8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: jeedes
ms.openlocfilehash: 75366abafa551d21630b0edddb65db23b9ea9d42
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-menlo-security"></a><span data-ttu-id="5086d-103">Samouczek: Azure Active Directory integracji z zabezpieczeniami Menlo</span><span class="sxs-lookup"><span data-stu-id="5086d-103">Tutorial: Azure Active Directory integration with Menlo Security</span></span>

<span data-ttu-id="5086d-104">Z tego samouczka dowiesz się integrowanie Menlo zabezpieczeń w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5086d-104">In this tutorial, you learn how to integrate Menlo Security with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5086d-105">Integrowanie Menlo zabezpieczeń z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="5086d-105">Integrating Menlo Security with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5086d-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Menlo zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="5086d-106">You can control in Azure AD who has access to Menlo Security</span></span>
- <span data-ttu-id="5086d-107">Umożliwia użytkownikom automatycznie pobrać zalogowane zabezpieczeń Menlo (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5086d-107">You can enable your users to automatically get signed-on to Menlo Security (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5086d-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="5086d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5086d-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz.</span><span class="sxs-lookup"><span data-stu-id="5086d-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="5086d-110">[Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5086d-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5086d-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5086d-111">Prerequisites</span></span>

<span data-ttu-id="5086d-112">Aby skonfigurować integrację usługi Azure AD z zabezpieczeniami Menlo, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="5086d-112">To configure Azure AD integration with Menlo Security, you need the following items:</span></span>

- <span data-ttu-id="5086d-113">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5086d-113">An Azure AD subscription</span></span>
- <span data-ttu-id="5086d-114">Zabezpieczenia Menlo jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="5086d-114">A Menlo Security single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5086d-115">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="5086d-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5086d-116">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="5086d-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5086d-117">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="5086d-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5086d-118">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5086d-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5086d-119">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="5086d-119">Scenario description</span></span>
<span data-ttu-id="5086d-120">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="5086d-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5086d-121">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="5086d-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5086d-122">Dodawanie zabezpieczeń Menlo z galerii</span><span class="sxs-lookup"><span data-stu-id="5086d-122">Adding Menlo Security from the gallery</span></span>
2. <span data-ttu-id="5086d-123">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="5086d-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-menlo-security-from-the-gallery"></a><span data-ttu-id="5086d-124">Dodawanie zabezpieczeń Menlo z galerii</span><span class="sxs-lookup"><span data-stu-id="5086d-124">Adding Menlo Security from the gallery</span></span>
<span data-ttu-id="5086d-125">Aby skonfigurować integrację Menlo zabezpieczeń w usłudze Azure Active Directory, należy dodać Menlo zabezpieczeń z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="5086d-125">To configure the integration of Menlo Security into Azure AD, you need to add Menlo Security from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5086d-126">**Aby dodać Menlo zabezpieczeń z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5086d-126">**To add Menlo Security from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5086d-127">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="5086d-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="5086d-129">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="5086d-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5086d-130">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="5086d-130">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="5086d-132">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5086d-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="5086d-134">W polu wyszukiwania wpisz **zabezpieczeń Menlo**.</span><span class="sxs-lookup"><span data-stu-id="5086d-134">In the search box, type **Menlo Security**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_search.png)

5. <span data-ttu-id="5086d-136">W panelu wyników wybierz **zabezpieczeń Menlo**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="5086d-136">In the results panel, select **Menlo Security**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5086d-138">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="5086d-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5086d-139">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Menlo zabezpieczenia oparte na użytkownika testowego o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="5086d-139">In this section, you configure and test Azure AD single sign-on with Menlo Security based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5086d-140">Do rejestracji jednokrotnej do pracy usługi Azure AD musi ustalić użytkownika odpowiednika w Menlo zabezpieczeń do użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5086d-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Menlo Security is to a user in Azure AD.</span></span> <span data-ttu-id="5086d-141">Innymi słowy relację łącza między użytkownika usługi Azure AD i danemu użytkownikowi zabezpieczeń Menlo musi określone.</span><span class="sxs-lookup"><span data-stu-id="5086d-141">In other words, a link relationship between an Azure AD user and the related user in Menlo Security needs to be established.</span></span>

<span data-ttu-id="5086d-142">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** Menlo zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="5086d-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Menlo Security.</span></span>

<span data-ttu-id="5086d-143">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z zabezpieczeniami Menlo, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="5086d-143">To configure and test Azure AD single sign-on with Menlo Security, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5086d-144">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="5086d-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5086d-145">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="5086d-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5086d-146">**[Tworzenie użytkownika testowego zabezpieczeń Menlo](#creating-a-menlo-security-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Menlo zabezpieczeń, które jest połączone z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5086d-146">**[Creating a Menlo Security test user](#creating-a-menlo-security-test-user)** - to have a counterpart of Britta Simon in Menlo Security that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5086d-147">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="5086d-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5086d-148">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="5086d-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5086d-149">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5086d-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5086d-150">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Menlo zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="5086d-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Menlo Security application.</span></span>

<span data-ttu-id="5086d-151">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Menlo zabezpieczeń, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5086d-151">**To configure Azure AD single sign-on with Menlo Security, perform the following steps:**</span></span>

1. <span data-ttu-id="5086d-152">W portalu Azure na **zabezpieczeń Menlo** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="5086d-152">In the Azure portal, on the **Menlo Security** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="5086d-154">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="5086d-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_samlbase.png)

3. <span data-ttu-id="5086d-156">Na **Menlo zabezpieczeń domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5086d-156">On the **Menlo Security Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_url.png)

    <span data-ttu-id="5086d-158">a.</span><span class="sxs-lookup"><span data-stu-id="5086d-158">a.</span></span> <span data-ttu-id="5086d-159">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.menlosecurity.com/account/login`</span><span class="sxs-lookup"><span data-stu-id="5086d-159">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.menlosecurity.com/account/login`</span></span>

    <span data-ttu-id="5086d-160">b.</span><span class="sxs-lookup"><span data-stu-id="5086d-160">b.</span></span> <span data-ttu-id="5086d-161">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.menlosecurity.com/safeview-auth-server/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="5086d-161">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.menlosecurity.com/safeview-auth-server/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5086d-162">Wartości te nie są rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="5086d-162">These values are not the real.</span></span> <span data-ttu-id="5086d-163">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="5086d-163">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="5086d-164">Skontaktuj się z [zespołem pomocy technicznej klienta zabezpieczeń Menlo](https://www.menlosecurity.com/menlo-contact) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="5086d-164">Contact [Menlo Security Client support team](https://www.menlosecurity.com/menlo-contact) to get these values.</span></span> 
 
4. <span data-ttu-id="5086d-165">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="5086d-165">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the Certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_certificate.png) 

5. <span data-ttu-id="5086d-167">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5086d-167">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5086d-169">Na **konfiguracji zabezpieczeń Menlo** , kliknij przycisk **Konfigurowanie zabezpieczeń Menlo** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="5086d-169">On the **Menlo Security Configuration** section, click **Configure Menlo Security** to open **Configure sign-on** window.</span></span> <span data-ttu-id="5086d-170">Kopiuj **SAML identyfikator jednostki**, i **SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="5086d-170">Copy the **SAML Entity ID**, and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_configure.png) 

7. <span data-ttu-id="5086d-172">Aby skonfigurować logowanie jednokrotne w **zabezpieczeń Menlo** strona, zaloguj się do **Menlo zabezpieczeń** witryny sieci Web jako administrator.</span><span class="sxs-lookup"><span data-stu-id="5086d-172">To configure single sign-on on **Menlo Security** side, login to the **Menlo Security** website as an administrator.</span></span>

8. <span data-ttu-id="5086d-173">W obszarze **ustawienia** przejdź do **uwierzytelniania** i wykonywanie następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="5086d-173">Under **Settings** go to **Authentication** and perform following actions:</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-menlosecurity-tutorial/menlo_user_setup.png)

    <span data-ttu-id="5086d-175">a.</span><span class="sxs-lookup"><span data-stu-id="5086d-175">a.</span></span> <span data-ttu-id="5086d-176">Zaznacz pole wyboru **Włącz uwierzytelnianie użytkowników przy użyciu SAML**.</span><span class="sxs-lookup"><span data-stu-id="5086d-176">Tick the checkbox **Enable user authentication using SAML**.</span></span>

    <span data-ttu-id="5086d-177">b.</span><span class="sxs-lookup"><span data-stu-id="5086d-177">b.</span></span> <span data-ttu-id="5086d-178">Wybierz **dostęp do zewnętrznych** do **tak**.</span><span class="sxs-lookup"><span data-stu-id="5086d-178">Select **Allow External Access** to **Yes**.</span></span>

    <span data-ttu-id="5086d-179">c.</span><span class="sxs-lookup"><span data-stu-id="5086d-179">c.</span></span> <span data-ttu-id="5086d-180">W obszarze **SAML dostawcy**, wybierz pozycję **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5086d-180">Under **SAML Provider**, select **Azure Active Directory**.</span></span>

    <span data-ttu-id="5086d-181">d.</span><span class="sxs-lookup"><span data-stu-id="5086d-181">d.</span></span> <span data-ttu-id="5086d-182">**SAML 2.0 Endpoint** : Wklej **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="5086d-182">**SAML 2.0 Endpoint** : Paste the **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="5086d-183">e.</span><span class="sxs-lookup"><span data-stu-id="5086d-183">e.</span></span> <span data-ttu-id="5086d-184">**Identyfikator usługi (Wystawca)** : Wklej **identyfikator jednostki SAML** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="5086d-184">**Service Identifier (Issuer)** : Paste the **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="5086d-185">f.</span><span class="sxs-lookup"><span data-stu-id="5086d-185">f.</span></span> <span data-ttu-id="5086d-186">**Certyfikat X.509** : Otwórz **certyfikatu (Base64)** pobrany z portalu Azure w programie Notatnik i wklej go w tym polu.</span><span class="sxs-lookup"><span data-stu-id="5086d-186">**X.509 Certificate** : Open the **Certificate (Base64)** downloaded from the Azure Portal in notepad and paste it in this box.</span></span>

    <span data-ttu-id="5086d-187">g.</span><span class="sxs-lookup"><span data-stu-id="5086d-187">g.</span></span> <span data-ttu-id="5086d-188">Kliknij przycisk **zapisać** Aby zapisać ustawienia.</span><span class="sxs-lookup"><span data-stu-id="5086d-188">Click **Save** to save the settings.</span></span>

> [!TIP]
> <span data-ttu-id="5086d-189">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="5086d-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5086d-190">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="5086d-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5086d-191">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5086d-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5086d-192">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5086d-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="5086d-193">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="5086d-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="5086d-195">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5086d-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5086d-196">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="5086d-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5086d-198">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="5086d-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5086d-200">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5086d-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5086d-202">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5086d-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5086d-204">a.</span><span class="sxs-lookup"><span data-stu-id="5086d-204">a.</span></span> <span data-ttu-id="5086d-205">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5086d-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5086d-206">b.</span><span class="sxs-lookup"><span data-stu-id="5086d-206">b.</span></span> <span data-ttu-id="5086d-207">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5086d-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5086d-208">c.</span><span class="sxs-lookup"><span data-stu-id="5086d-208">c.</span></span> <span data-ttu-id="5086d-209">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="5086d-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5086d-210">d.</span><span class="sxs-lookup"><span data-stu-id="5086d-210">d.</span></span> <span data-ttu-id="5086d-211">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="5086d-211">Click **Create**.</span></span>
 
### <a name="creating-a-menlo-security-test-user"></a><span data-ttu-id="5086d-212">Tworzenie użytkownika testowego Menlo zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="5086d-212">Creating a Menlo Security test user</span></span>
 
<span data-ttu-id="5086d-213">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta Menlo zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="5086d-213">In this section, you create a user called Britta Simon in Menlo Security.</span></span> <span data-ttu-id="5086d-214">Praca z [zespołem pomocy technicznej klienta zabezpieczeń Menlo](https://www.menlosecurity.com/menlo-contact) Aby dodać użytkowników do platformy Menlo zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="5086d-214">Work with [Menlo Security Client support team](https://www.menlosecurity.com/menlo-contact) to add the users in the Menlo Security platform.</span></span> <span data-ttu-id="5086d-215">Użytkownicy muszą utworzyć i aktywowana, aby użyć rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="5086d-215">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5086d-216">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5086d-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5086d-217">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Menlo zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="5086d-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Menlo Security.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="5086d-219">**Aby przypisać Simona Britta Menlo zabezpieczeń, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5086d-219">**To assign Britta Simon to Menlo Security, perform the following steps:**</span></span>

1. <span data-ttu-id="5086d-220">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="5086d-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="5086d-222">Na liście aplikacji zaznacz **zabezpieczeń Menlo**.</span><span class="sxs-lookup"><span data-stu-id="5086d-222">In the applications list, select **Menlo Security**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_app.png) 

3. <span data-ttu-id="5086d-224">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="5086d-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="5086d-226">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5086d-226">Click **Add** button.</span></span> <span data-ttu-id="5086d-227">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5086d-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="5086d-229">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="5086d-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5086d-230">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5086d-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5086d-231">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5086d-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5086d-232">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5086d-232">Testing single sign-on</span></span>

<span data-ttu-id="5086d-233">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="5086d-233">In this section, you test your Azure AD single sign-on configuration.</span></span>

<span data-ttu-id="5086d-234">Otwórz okno przeglądarki w trybie "Sesję InPrivate" lub "Incognito" Aby wyzwolić nowego uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="5086d-234">Open a browser window in an "InPrivate" or "Incognito" mode to trigger a new authentication.</span></span>  <span data-ttu-id="5086d-235">W programie Internet Explorer użyj klawiszy Ctrl + Shift + P.</span><span class="sxs-lookup"><span data-stu-id="5086d-235">In Internet Explorer, use Ctrl+Shift+P.</span></span>  <span data-ttu-id="5086d-236">W przeglądarce Chrome użyj klawiszy Ctrl + Shift + N.</span><span class="sxs-lookup"><span data-stu-id="5086d-236">In Chrome, use Ctrl+Shift+N.</span></span>  <span data-ttu-id="5086d-237">W oknie przeglądania prywatne przejdź do chronionych zasobów i wykonywać logowania usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5086d-237">In the private browsing window, browse to a protected resource and perform an Azure AD login.</span></span>  <span data-ttu-id="5086d-238">Po pomyślnym logowaniu nastąpi przekierowanie do żądanej witryny w sesji izolacji.</span><span class="sxs-lookup"><span data-stu-id="5086d-238">Upon successful login, you will be taken to the requested site in an isolation session.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5086d-239">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="5086d-239">Additional resources</span></span>

* [<span data-ttu-id="5086d-240">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5086d-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5086d-241">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5086d-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_203.png

