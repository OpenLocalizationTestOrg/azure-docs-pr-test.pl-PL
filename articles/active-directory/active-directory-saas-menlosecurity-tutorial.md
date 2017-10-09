---
title: 'Samouczek: Azure Active Directory integracji z zabezpieczeniami Menlo | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Menlo zabezpieczeń."
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
ms.openlocfilehash: 193d12eedf31f4f08e1d141936d6e918c36a2109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-menlo-security"></a><span data-ttu-id="e5440-103">Samouczek: Azure Active Directory integracji z zabezpieczeniami Menlo</span><span class="sxs-lookup"><span data-stu-id="e5440-103">Tutorial: Azure Active Directory integration with Menlo Security</span></span>

<span data-ttu-id="e5440-104">Z tego samouczka, dowiesz się, jak toointegrate Menlo zabezpieczeń w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e5440-104">In this tutorial, you learn how toointegrate Menlo Security with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e5440-105">Integracja z usługą Azure AD Menlo zabezpieczeń zawiera hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="e5440-105">Integrating Menlo Security with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e5440-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooMenlo zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="e5440-106">You can control in Azure AD who has access tooMenlo Security</span></span>
- <span data-ttu-id="e5440-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooMenlo zabezpieczeń (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e5440-107">You can enable your users tooautomatically get signed-on tooMenlo Security (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e5440-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="e5440-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e5440-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz.</span><span class="sxs-lookup"><span data-stu-id="e5440-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="e5440-110">[Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e5440-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e5440-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e5440-111">Prerequisites</span></span>

<span data-ttu-id="e5440-112">tooconfigure integracji usługi Azure AD z zabezpieczeniami Menlo należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="e5440-112">tooconfigure Azure AD integration with Menlo Security, you need hello following items:</span></span>

- <span data-ttu-id="e5440-113">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e5440-113">An Azure AD subscription</span></span>
- <span data-ttu-id="e5440-114">Zabezpieczenia Menlo jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="e5440-114">A Menlo Security single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e5440-115">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="e5440-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e5440-116">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="e5440-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e5440-117">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="e5440-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e5440-118">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e5440-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e5440-119">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="e5440-119">Scenario description</span></span>
<span data-ttu-id="e5440-120">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="e5440-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e5440-121">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="e5440-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e5440-122">Dodawanie zabezpieczeń Menlo z galerii hello</span><span class="sxs-lookup"><span data-stu-id="e5440-122">Adding Menlo Security from hello gallery</span></span>
2. <span data-ttu-id="e5440-123">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="e5440-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-menlo-security-from-hello-gallery"></a><span data-ttu-id="e5440-124">Dodawanie zabezpieczeń Menlo z galerii hello</span><span class="sxs-lookup"><span data-stu-id="e5440-124">Adding Menlo Security from hello gallery</span></span>
<span data-ttu-id="e5440-125">tooconfigure hello integrację Menlo zabezpieczeń w usłudze Azure Active Directory, należy tooadd Menlo zabezpieczeń z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="e5440-125">tooconfigure hello integration of Menlo Security into Azure AD, you need tooadd Menlo Security from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e5440-126">**tooadd Menlo zabezpieczeń z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="e5440-126">**tooadd Menlo Security from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e5440-127">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="e5440-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="e5440-129">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="e5440-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e5440-130">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="e5440-130">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="e5440-132">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e5440-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="e5440-134">W polu wyszukiwania hello wpisz **zabezpieczeń Menlo**.</span><span class="sxs-lookup"><span data-stu-id="e5440-134">In hello search box, type **Menlo Security**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_search.png)

5. <span data-ttu-id="e5440-136">W panelu wyników hello, wybierz **zabezpieczeń Menlo**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="e5440-136">In hello results panel, select **Menlo Security**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e5440-138">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="e5440-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e5440-139">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Menlo zabezpieczenia oparte na użytkownika testowego o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="e5440-139">In this section, you configure and test Azure AD single sign-on with Menlo Security based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e5440-140">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow hello użytkownika odpowiednikiem zabezpieczeń Menlo jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e5440-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Menlo Security is tooa user in Azure AD.</span></span> <span data-ttu-id="e5440-141">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi zabezpieczeń Menlo musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="e5440-141">In other words, a link relationship between an Azure AD user and hello related user in Menlo Security needs toobe established.</span></span>

<span data-ttu-id="e5440-142">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** Menlo zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="e5440-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Menlo Security.</span></span>

<span data-ttu-id="e5440-143">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z zabezpieczeniami Menlo, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="e5440-143">tooconfigure and test Azure AD single sign-on with Menlo Security, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e5440-144">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="e5440-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e5440-145">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="e5440-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e5440-146">**[Tworzenie użytkownika testowego zabezpieczeń Menlo](#creating-a-menlo-security-test-user)**  -toohave odpowiednikiem Simona Britta Menlo zabezpieczeń, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e5440-146">**[Creating a Menlo Security test user](#creating-a-menlo-security-test-user)** - toohave a counterpart of Britta Simon in Menlo Security that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e5440-147">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="e5440-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e5440-148">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="e5440-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e5440-149">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e5440-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e5440-150">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Menlo zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="e5440-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Menlo Security application.</span></span>

<span data-ttu-id="e5440-151">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Menlo zabezpieczeń, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="e5440-151">**tooconfigure Azure AD single sign-on with Menlo Security, perform hello following steps:**</span></span>

1. <span data-ttu-id="e5440-152">W portalu Azure na powitania hello **zabezpieczeń Menlo** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="e5440-152">In hello Azure portal, on hello **Menlo Security** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="e5440-154">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="e5440-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_samlbase.png)

3. <span data-ttu-id="e5440-156">Na powitania **Menlo zabezpieczeń domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="e5440-156">On hello **Menlo Security Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_url.png)

    <span data-ttu-id="e5440-158">a.</span><span class="sxs-lookup"><span data-stu-id="e5440-158">a.</span></span> <span data-ttu-id="e5440-159">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.menlosecurity.com/account/login`</span><span class="sxs-lookup"><span data-stu-id="e5440-159">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.menlosecurity.com/account/login`</span></span>

    <span data-ttu-id="e5440-160">b.</span><span class="sxs-lookup"><span data-stu-id="e5440-160">b.</span></span> <span data-ttu-id="e5440-161">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.menlosecurity.com/safeview-auth-server/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="e5440-161">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.menlosecurity.com/safeview-auth-server/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e5440-162">Wartości te nie są hello prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="e5440-162">These values are not hello real.</span></span> <span data-ttu-id="e5440-163">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="e5440-163">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e5440-164">Skontaktuj się z [zespołem pomocy technicznej klienta zabezpieczeń Menlo](https://www.menlosecurity.com/menlo-contact) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="e5440-164">Contact [Menlo Security Client support team](https://www.menlosecurity.com/menlo-contact) tooget these values.</span></span> 
 
4. <span data-ttu-id="e5440-165">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="e5440-165">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello Certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_certificate.png) 

5. <span data-ttu-id="e5440-167">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e5440-167">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e5440-169">Na powitania **konfiguracji zabezpieczeń Menlo** kliknij **Konfigurowanie zabezpieczeń Menlo** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="e5440-169">On hello **Menlo Security Configuration** section, click **Configure Menlo Security** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e5440-170">Kopiuj hello **SAML identyfikator jednostki**, i **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="e5440-170">Copy hello **SAML Entity ID**, and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_configure.png) 

7. <span data-ttu-id="e5440-172">tooconfigure rejestracji jednokrotnej w **zabezpieczeń Menlo** strona, logowania toohello **zabezpieczeń Menlo** witryny sieci Web jako administrator.</span><span class="sxs-lookup"><span data-stu-id="e5440-172">tooconfigure single sign-on on **Menlo Security** side, login toohello **Menlo Security** website as an administrator.</span></span>

8. <span data-ttu-id="e5440-173">W obszarze **ustawienia** Przejdź zbyt**uwierzytelniania** i wykonywanie następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="e5440-173">Under **Settings** go too**Authentication** and perform following actions:</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-menlosecurity-tutorial/menlo_user_setup.png)

    <span data-ttu-id="e5440-175">a.</span><span class="sxs-lookup"><span data-stu-id="e5440-175">a.</span></span> <span data-ttu-id="e5440-176">Zaznacz pole wyboru hello **Włącz uwierzytelnianie użytkowników przy użyciu SAML**.</span><span class="sxs-lookup"><span data-stu-id="e5440-176">Tick hello checkbox **Enable user authentication using SAML**.</span></span>

    <span data-ttu-id="e5440-177">b.</span><span class="sxs-lookup"><span data-stu-id="e5440-177">b.</span></span> <span data-ttu-id="e5440-178">Wybierz **Zezwalaj dostępu zewnętrznego** za**tak**.</span><span class="sxs-lookup"><span data-stu-id="e5440-178">Select **Allow External Access** too**Yes**.</span></span>

    <span data-ttu-id="e5440-179">c.</span><span class="sxs-lookup"><span data-stu-id="e5440-179">c.</span></span> <span data-ttu-id="e5440-180">W obszarze **SAML dostawcy**, wybierz pozycję **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e5440-180">Under **SAML Provider**, select **Azure Active Directory**.</span></span>

    <span data-ttu-id="e5440-181">d.</span><span class="sxs-lookup"><span data-stu-id="e5440-181">d.</span></span> <span data-ttu-id="e5440-182">**SAML 2.0 Endpoint** : hello Wklej **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e5440-182">**SAML 2.0 Endpoint** : Paste hello **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e5440-183">e.</span><span class="sxs-lookup"><span data-stu-id="e5440-183">e.</span></span> <span data-ttu-id="e5440-184">**Identyfikator usługi (Wystawca)** : hello Wklej **identyfikator jednostki SAML** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e5440-184">**Service Identifier (Issuer)** : Paste hello **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e5440-185">f.</span><span class="sxs-lookup"><span data-stu-id="e5440-185">f.</span></span> <span data-ttu-id="e5440-186">**Certyfikat X.509** : Otwórz hello **certyfikatu (Base64)** pobrane z hello portalu Azure w programie Notatnik i wklej go w tym polu.</span><span class="sxs-lookup"><span data-stu-id="e5440-186">**X.509 Certificate** : Open hello **Certificate (Base64)** downloaded from hello Azure Portal in notepad and paste it in this box.</span></span>

    <span data-ttu-id="e5440-187">g.</span><span class="sxs-lookup"><span data-stu-id="e5440-187">g.</span></span> <span data-ttu-id="e5440-188">Kliknij przycisk **zapisać** toosave hello ustawienia.</span><span class="sxs-lookup"><span data-stu-id="e5440-188">Click **Save** toosave hello settings.</span></span>

> [!TIP]
> <span data-ttu-id="e5440-189">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="e5440-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e5440-190">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="e5440-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e5440-191">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e5440-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e5440-192">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e5440-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="e5440-193">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="e5440-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="e5440-195">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="e5440-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e5440-196">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="e5440-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e5440-198">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="e5440-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e5440-200">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e5440-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e5440-202">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="e5440-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e5440-204">a.</span><span class="sxs-lookup"><span data-stu-id="e5440-204">a.</span></span> <span data-ttu-id="e5440-205">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e5440-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e5440-206">b.</span><span class="sxs-lookup"><span data-stu-id="e5440-206">b.</span></span> <span data-ttu-id="e5440-207">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e5440-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e5440-208">c.</span><span class="sxs-lookup"><span data-stu-id="e5440-208">c.</span></span> <span data-ttu-id="e5440-209">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="e5440-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e5440-210">d.</span><span class="sxs-lookup"><span data-stu-id="e5440-210">d.</span></span> <span data-ttu-id="e5440-211">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="e5440-211">Click **Create**.</span></span>
 
### <a name="creating-a-menlo-security-test-user"></a><span data-ttu-id="e5440-212">Tworzenie użytkownika testowego Menlo zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="e5440-212">Creating a Menlo Security test user</span></span>
 
<span data-ttu-id="e5440-213">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta Menlo zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="e5440-213">In this section, you create a user called Britta Simon in Menlo Security.</span></span> <span data-ttu-id="e5440-214">Praca z [zespołem pomocy technicznej klienta zabezpieczeń Menlo](https://www.menlosecurity.com/menlo-contact) tooadd hello użytkowników hello Menlo zabezpieczeń platformy.</span><span class="sxs-lookup"><span data-stu-id="e5440-214">Work with [Menlo Security Client support team](https://www.menlosecurity.com/menlo-contact) tooadd hello users in hello Menlo Security platform.</span></span> <span data-ttu-id="e5440-215">Użytkownicy muszą utworzyć i aktywowana, aby użyć rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="e5440-215">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e5440-216">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e5440-216">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e5440-217">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooMenlo zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="e5440-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMenlo Security.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="e5440-219">**tooassign tooMenlo Simona Britta zabezpieczeń, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="e5440-219">**tooassign Britta Simon tooMenlo Security, perform hello following steps:**</span></span>

1. <span data-ttu-id="e5440-220">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="e5440-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="e5440-222">Z listy aplikacji hello wybierz **zabezpieczeń Menlo**.</span><span class="sxs-lookup"><span data-stu-id="e5440-222">In hello applications list, select **Menlo Security**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_app.png) 

3. <span data-ttu-id="e5440-224">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="e5440-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="e5440-226">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e5440-226">Click **Add** button.</span></span> <span data-ttu-id="e5440-227">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e5440-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="e5440-229">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="e5440-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e5440-230">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e5440-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e5440-231">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e5440-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e5440-232">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e5440-232">Testing single sign-on</span></span>

<span data-ttu-id="e5440-233">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="e5440-233">In this section, you test your Azure AD single sign-on configuration.</span></span>

<span data-ttu-id="e5440-234">Otwórz okno przeglądarki w "Sesję InPrivate" lub "Incognito" Tryb tootrigger nowego uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="e5440-234">Open a browser window in an "InPrivate" or "Incognito" mode tootrigger a new authentication.</span></span>  <span data-ttu-id="e5440-235">W programie Internet Explorer użyj klawiszy Ctrl + Shift + P.</span><span class="sxs-lookup"><span data-stu-id="e5440-235">In Internet Explorer, use Ctrl+Shift+P.</span></span>  <span data-ttu-id="e5440-236">W przeglądarce Chrome użyj klawiszy Ctrl + Shift + N.</span><span class="sxs-lookup"><span data-stu-id="e5440-236">In Chrome, use Ctrl+Shift+N.</span></span>  <span data-ttu-id="e5440-237">W oknie przeglądania prywatnej hello przeglądanie tooa chronionych zasobów i przeprowadzanie logowania usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e5440-237">In hello private browsing window, browse tooa protected resource and perform an Azure AD login.</span></span>  <span data-ttu-id="e5440-238">Po pomyślnym logowaniu będzie żądanej witryny toohello podjęte w sesji izolacji.</span><span class="sxs-lookup"><span data-stu-id="e5440-238">Upon successful login, you will be taken toohello requested site in an isolation session.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e5440-239">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="e5440-239">Additional resources</span></span>

* [<span data-ttu-id="e5440-240">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e5440-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e5440-241">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e5440-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



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

