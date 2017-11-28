---
title: 'Samouczek: Integracji Azure Active Directory z Workstars | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Workstars."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 51a4a4e4-ff60-4971-b3f8-a0367b70d220
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: 86250d7538f058d2a821ded7dda0b2fc185d80df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workstars"></a><span data-ttu-id="0e994-103">Samouczek: Integracji Azure Active Directory z Workstars</span><span class="sxs-lookup"><span data-stu-id="0e994-103">Tutorial: Azure Active Directory integration with Workstars</span></span>

<span data-ttu-id="0e994-104">Z tego samouczka, dowiesz się, jak toointegrate Workstars w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0e994-104">In this tutorial, you learn how toointegrate Workstars with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0e994-105">Integracja z usługą Azure AD Workstars zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="0e994-105">Integrating Workstars with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0e994-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooWorkstars.</span><span class="sxs-lookup"><span data-stu-id="0e994-106">You can control in Azure AD who has access tooWorkstars.</span></span>
- <span data-ttu-id="0e994-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooWorkstars (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0e994-107">You can enable your users tooautomatically get signed-on tooWorkstars (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="0e994-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0e994-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="0e994-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0e994-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0e994-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0e994-110">Prerequisites</span></span>

<span data-ttu-id="0e994-111">tooconfigure integracji z usługą Azure AD z Workstars należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="0e994-111">tooconfigure Azure AD integration with Workstars, you need hello following items:</span></span>

- <span data-ttu-id="0e994-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e994-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0e994-113">Workstars logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="0e994-113">A Workstars single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0e994-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="0e994-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0e994-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="0e994-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0e994-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="0e994-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0e994-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0e994-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0e994-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="0e994-118">Scenario description</span></span>
<span data-ttu-id="0e994-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="0e994-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0e994-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="0e994-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0e994-121">Dodawanie Workstars z galerii hello</span><span class="sxs-lookup"><span data-stu-id="0e994-121">Adding Workstars from hello gallery</span></span>
2. <span data-ttu-id="0e994-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="0e994-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workstars-from-hello-gallery"></a><span data-ttu-id="0e994-123">Dodawanie Workstars z galerii hello</span><span class="sxs-lookup"><span data-stu-id="0e994-123">Adding Workstars from hello gallery</span></span>
<span data-ttu-id="0e994-124">tooconfigure hello integracji Workstars do usługi Azure AD, należy tooadd Workstars z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="0e994-124">tooconfigure hello integration of Workstars into Azure AD, you need tooadd Workstars from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0e994-125">**tooadd Workstars z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="0e994-125">**tooadd Workstars from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e994-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="0e994-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="0e994-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="0e994-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0e994-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="0e994-129">Then go too**All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. <span data-ttu-id="0e994-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0e994-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nowy przycisk aplikacji Hello][3]

4. <span data-ttu-id="0e994-133">W polu wyszukiwania hello wpisz **Workstars**, wybierz pozycję **Workstars** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="0e994-133">In hello search box, type **Workstars**, select **Workstars** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Workstars hello listy wyników](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="0e994-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="0e994-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="0e994-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Workstars w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="0e994-136">In this section, you configure and test Azure AD single sign-on with Workstars based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0e994-137">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Workstars jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0e994-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workstars is tooa user in Azure AD.</span></span> <span data-ttu-id="0e994-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Workstars musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="0e994-138">In other words, a link relationship between an Azure AD user and hello related user in Workstars needs toobe established.</span></span>

<span data-ttu-id="0e994-139">W Workstars, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="0e994-139">In Workstars, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0e994-140">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Workstars, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="0e994-140">tooconfigure and test Azure AD single sign-on with Workstars, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0e994-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="0e994-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0e994-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="0e994-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0e994-143">**[Tworzenie użytkownika testowego Workstars](#create-a-workstars-test-user)**  -toohave odpowiednikiem Simona Britta w Workstars, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0e994-143">**[Create a Workstars test user](#create-a-workstars-test-user)** - toohave a counterpart of Britta Simon in Workstars that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0e994-144">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="0e994-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0e994-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="0e994-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="0e994-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="0e994-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="0e994-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Workstars.</span><span class="sxs-lookup"><span data-stu-id="0e994-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workstars application.</span></span>

<span data-ttu-id="0e994-148">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Workstars, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="0e994-148">**tooconfigure Azure AD single sign-on with Workstars, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e994-149">W portalu Azure na powitania hello **Workstars** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="0e994-149">In hello Azure portal, on hello **Workstars** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="0e994-151">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="0e994-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_samlbase.png)

3. <span data-ttu-id="0e994-153">Na powitania **Workstars domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="0e994-153">On hello **Workstars Domain and URLs** section, perform hello following steps:</span></span>

    ![Adresy URL i domeny Workstars pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_url.png)

    <span data-ttu-id="0e994-155">a.</span><span class="sxs-lookup"><span data-stu-id="0e994-155">a.</span></span> <span data-ttu-id="0e994-156">W hello **identyfikator** pole tekstowe, wprowadź adres URL hello:`https://workstars.com`</span><span class="sxs-lookup"><span data-stu-id="0e994-156">In hello **Identifier** textbox, type hello URL: `https://workstars.com`</span></span>

    <span data-ttu-id="0e994-157">b.</span><span class="sxs-lookup"><span data-stu-id="0e994-157">b.</span></span> <span data-ttu-id="0e994-158">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.workstars.com/saml/login_check`</span><span class="sxs-lookup"><span data-stu-id="0e994-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.workstars.com/saml/login_check`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0e994-159">wartość Hello nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="0e994-159">hello value is not real.</span></span> <span data-ttu-id="0e994-160">Wartość hello aktualizacji z hello rzeczywisty adres URL odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="0e994-160">Update hello value with hello actual Reply URL.</span></span> <span data-ttu-id="0e994-161">Skontaktuj się z [Workstars obsługuje zespołu](https://support.workstars.com) tooget hello wartość.</span><span class="sxs-lookup"><span data-stu-id="0e994-161">Contact [Workstars support team](https://support.workstars.com) tooget hello value.</span></span>
 
4. <span data-ttu-id="0e994-162">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="0e994-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_certificate.png) 

5. <span data-ttu-id="0e994-164">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0e994-164">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-workstars-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0e994-166">Na powitania **konfiguracji Workstars** kliknij **skonfigurować Workstars** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="0e994-166">On hello **Workstars Configuration** section, click **Configure Workstars** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0e994-167">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="0e994-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfiguracja Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_configure.png) 

7. <span data-ttu-id="0e994-169">W innym oknie przeglądarki Zaloguj się w witrynie firmy Workstars tooyour jako administrator.</span><span class="sxs-lookup"><span data-stu-id="0e994-169">In another browser window, sign on tooyour Workstars company site as an administrator.</span></span>

8. <span data-ttu-id="0e994-170">Witaj głównym pasku narzędzi, kliknij przycisk **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="0e994-170">In hello main toolbar, click **Settings**.</span></span>

    ![Ustaw Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_sett.png)

9. <span data-ttu-id="0e994-172">Przejdź za**Sign On** > **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="0e994-172">Go too**Sign On** > **Settings**.</span></span>

    ![Logować Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_signon.png)

    ![Ustawienia Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_settings.png)

10. <span data-ttu-id="0e994-175">Na powitania **pojedynczy znak na (SAML) — ustawienia** wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="0e994-175">On hello **Single Sign On (SAML) - Settings** page, perform hello following steps:</span></span>
    
    ![Workstars saml](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_saml.png)

    <span data-ttu-id="0e994-177">a.</span><span class="sxs-lookup"><span data-stu-id="0e994-177">a.</span></span> <span data-ttu-id="0e994-178">W **Nazwa dostawcy tożsamości** pole tekstowe, typ **usługi Office 365**.</span><span class="sxs-lookup"><span data-stu-id="0e994-178">In **Identity Provider Name** textbox, type **Office 365**.</span></span>

    <span data-ttu-id="0e994-179">b.</span><span class="sxs-lookup"><span data-stu-id="0e994-179">b.</span></span> <span data-ttu-id="0e994-180">W hello **identyfikator jednostki dostawcy tożsamości** pole tekstowe, Wklej wartość hello **identyfikator jednostki SAML**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0e994-180">In hello **Identity Provider Entity ID** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="0e994-181">c.</span><span class="sxs-lookup"><span data-stu-id="0e994-181">c.</span></span> <span data-ttu-id="0e994-182">Kopiowanie zawartości hello hello pliku pobranego certyfikatu w programie Notatnik, a następnie wklej go do hello **x509 certyfikatu** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="0e994-182">Copy hello content of hello downloaded certificate file in notepad, and then paste it into hello **x509 Certificate** textbox.</span></span> 

    <span data-ttu-id="0e994-183">d.</span><span class="sxs-lookup"><span data-stu-id="0e994-183">d.</span></span> <span data-ttu-id="0e994-184">W hello **adres URL logowania jednokrotnego SAML** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0e994-184">In hello **SAML SSO URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="0e994-185">e.</span><span class="sxs-lookup"><span data-stu-id="0e994-185">e.</span></span> <span data-ttu-id="0e994-186">W hello **zdalnego adresu URL wylogowania** pole tekstowe, Wklej wartość hello **Sign-Out URL**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0e994-186">In hello **Remote Logout URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="0e994-187">f.</span><span class="sxs-lookup"><span data-stu-id="0e994-187">f.</span></span> <span data-ttu-id="0e994-188">Wybierz **Identyfikatora nazwy** jako **poczty E-mail (ustawienie domyślne)**.</span><span class="sxs-lookup"><span data-stu-id="0e994-188">select **Name ID** as **Email (Default)**.</span></span>

    <span data-ttu-id="0e994-189">g.</span><span class="sxs-lookup"><span data-stu-id="0e994-189">g.</span></span> <span data-ttu-id="0e994-190">Kliknij przycisk **potwierdzić**.</span><span class="sxs-lookup"><span data-stu-id="0e994-190">Click **Confirm**.</span></span>
    
> [!TIP]
> <span data-ttu-id="0e994-191">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="0e994-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0e994-192">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="0e994-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0e994-193">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0e994-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="0e994-194">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e994-194">Create an Azure AD test user</span></span>

<span data-ttu-id="0e994-195">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="0e994-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="0e994-197">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="0e994-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e994-198">W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0e994-198">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-workstars-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="0e994-200">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="0e994-200">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-workstars-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="0e994-202">Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="0e994-202">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![przycisk Dodaj Hello](./media/active-directory-saas-workstars-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="0e994-204">W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="0e994-204">In hello **User** dialog box, perform hello following steps:</span></span>

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-workstars-tutorial/create_aaduser_04.png)

    <span data-ttu-id="0e994-206">a.</span><span class="sxs-lookup"><span data-stu-id="0e994-206">a.</span></span> <span data-ttu-id="0e994-207">W hello **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0e994-207">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0e994-208">b.</span><span class="sxs-lookup"><span data-stu-id="0e994-208">b.</span></span> <span data-ttu-id="0e994-209">W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="0e994-209">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="0e994-210">c.</span><span class="sxs-lookup"><span data-stu-id="0e994-210">c.</span></span> <span data-ttu-id="0e994-211">Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="0e994-211">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="0e994-212">d.</span><span class="sxs-lookup"><span data-stu-id="0e994-212">d.</span></span> <span data-ttu-id="0e994-213">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="0e994-213">Click **Create**.</span></span>
  
### <a name="create-a-workstars-test-user"></a><span data-ttu-id="0e994-214">Tworzenie użytkownika testowego Workstars</span><span class="sxs-lookup"><span data-stu-id="0e994-214">Create a Workstars test user</span></span>

<span data-ttu-id="0e994-215">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Workstars.</span><span class="sxs-lookup"><span data-stu-id="0e994-215">In this section, you create a user called Britta Simon in Workstars.</span></span> <span data-ttu-id="0e994-216">Praca z [Workstars obsługuje zespołu](https://support.workstars.com) użytkowników hello tooadd hello Workstars platformy.</span><span class="sxs-lookup"><span data-stu-id="0e994-216">Work with [Workstars support team](https://support.workstars.com) tooadd hello users in hello Workstars platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="0e994-217">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e994-217">Assign hello Azure AD test user</span></span>

<span data-ttu-id="0e994-218">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooWorkstars.</span><span class="sxs-lookup"><span data-stu-id="0e994-218">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkstars.</span></span>

![Przypisanie roli użytkownika hello][200] 

<span data-ttu-id="0e994-220">**tooassign tooWorkstars Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="0e994-220">**tooassign Britta Simon tooWorkstars, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e994-221">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="0e994-221">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="0e994-223">Z listy aplikacji hello wybierz **Workstars**.</span><span class="sxs-lookup"><span data-stu-id="0e994-223">In hello applications list, select **Workstars**.</span></span>

    ![łącze Workstars Hello na liście aplikacji hello](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_app.png)  

3. <span data-ttu-id="0e994-225">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="0e994-225">In hello menu on hello left, click **Users and groups**.</span></span>

    ![łącze "Użytkownicy i grupy" Hello][202]

4. <span data-ttu-id="0e994-227">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0e994-227">Click **Add** button.</span></span> <span data-ttu-id="0e994-228">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0e994-228">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Okienko Dodaj przypisania Hello][203]

5. <span data-ttu-id="0e994-230">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="0e994-230">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0e994-231">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0e994-231">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0e994-232">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0e994-232">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="0e994-233">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="0e994-233">Test single sign-on</span></span>

<span data-ttu-id="0e994-234">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="0e994-234">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0e994-235">Po kliknięciu powitalne Workstars kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Workstars aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0e994-235">When you click hello Workstars tile in hello Access Panel, you should get automatically signed-on tooyour Workstars application.</span></span>
<span data-ttu-id="0e994-236">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0e994-236">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="0e994-237">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="0e994-237">Additional resources</span></span>

* [<span data-ttu-id="0e994-238">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0e994-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0e994-239">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0e994-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_203.png

