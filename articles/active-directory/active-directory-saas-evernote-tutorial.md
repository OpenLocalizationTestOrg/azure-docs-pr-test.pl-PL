---
title: 'Samouczek: Integracji Azure Active Directory z Evernote | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Evernote."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 4d7017e571ed12a0b155aa188c6b0ecb3c9898a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-evernote"></a><span data-ttu-id="8a475-103">Samouczek: Integracji Azure Active Directory z Evernote</span><span class="sxs-lookup"><span data-stu-id="8a475-103">Tutorial: Azure Active Directory integration with Evernote</span></span>

<span data-ttu-id="8a475-104">Z tego samouczka, dowiesz się, jak toointegrate Evernote w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8a475-104">In this tutorial, you learn how toointegrate Evernote with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8a475-105">Integracja z usługą Azure AD Evernote zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="8a475-105">Integrating Evernote with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8a475-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooEvernote.</span><span class="sxs-lookup"><span data-stu-id="8a475-106">You can control in Azure AD who has access tooEvernote.</span></span>
- <span data-ttu-id="8a475-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooEvernote (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8a475-107">You can enable your users tooautomatically get signed-on tooEvernote (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="8a475-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="8a475-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="8a475-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8a475-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8a475-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8a475-110">Prerequisites</span></span>

<span data-ttu-id="8a475-111">tooconfigure integracji z usługą Azure AD z Evernote należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="8a475-111">tooconfigure Azure AD integration with Evernote, you need hello following items:</span></span>

- <span data-ttu-id="8a475-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a475-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8a475-113">Evernote logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="8a475-113">An Evernote single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8a475-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="8a475-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8a475-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="8a475-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8a475-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="8a475-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8a475-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8a475-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8a475-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="8a475-118">Scenario description</span></span>
<span data-ttu-id="8a475-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="8a475-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8a475-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="8a475-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8a475-121">Dodawanie Evernote z galerii hello</span><span class="sxs-lookup"><span data-stu-id="8a475-121">Adding Evernote from hello gallery</span></span>
2. <span data-ttu-id="8a475-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="8a475-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-evernote-from-hello-gallery"></a><span data-ttu-id="8a475-123">Dodawanie Evernote z galerii hello</span><span class="sxs-lookup"><span data-stu-id="8a475-123">Adding Evernote from hello gallery</span></span>
<span data-ttu-id="8a475-124">tooconfigure hello integracji Evernote do usługi Azure AD, należy tooadd Evernote z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="8a475-124">tooconfigure hello integration of Evernote into Azure AD, you need tooadd Evernote from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8a475-125">**tooadd Evernote z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="8a475-125">**tooadd Evernote from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8a475-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="8a475-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="8a475-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="8a475-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8a475-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="8a475-129">Then go too**All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. <span data-ttu-id="8a475-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8a475-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nowy przycisk aplikacji Hello][3]

4. <span data-ttu-id="8a475-133">W polu wyszukiwania hello wpisz **Evernote**, wybierz pozycję **Evernote** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="8a475-133">In hello search box, type **Evernote**, select **Evernote** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Evernote hello listy wyników](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="8a475-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8a475-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="8a475-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Evernote w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="8a475-136">In this section, you configure and test Azure AD single sign-on with Evernote based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8a475-137">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Evernote jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8a475-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Evernote is tooa user in Azure AD.</span></span> <span data-ttu-id="8a475-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Evernote musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="8a475-138">In other words, a link relationship between an Azure AD user and hello related user in Evernote needs toobe established.</span></span>

<span data-ttu-id="8a475-139">W Evernote, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="8a475-139">In Evernote, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8a475-140">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Evernote, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="8a475-140">tooconfigure and test Azure AD single sign-on with Evernote, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8a475-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="8a475-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8a475-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="8a475-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8a475-143">**[Tworzenie użytkownika testowego Evernote](#create-an-evernote-test-user)**  -toohave odpowiednikiem Simona Britta w Evernote, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8a475-143">**[Create an Evernote test user](#create-an-evernote-test-user)** - toohave a counterpart of Britta Simon in Evernote that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8a475-144">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="8a475-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8a475-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="8a475-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="8a475-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8a475-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="8a475-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Evernote.</span><span class="sxs-lookup"><span data-stu-id="8a475-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Evernote application.</span></span>

<span data-ttu-id="8a475-148">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Evernote, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="8a475-148">**tooconfigure Azure AD single sign-on with Evernote, perform hello following steps:**</span></span>

1. <span data-ttu-id="8a475-149">W portalu Azure na powitania hello **Evernote** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="8a475-149">In hello Azure portal, on hello **Evernote** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="8a475-151">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="8a475-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_samlbase.png)

3. <span data-ttu-id="8a475-153">Na powitania **Evernote domeny i adres URL** sekcji, wykonaj następujące kroki, jeśli chcesz tooconfigure aplikacji hello w rozszerzeniu IDP zainicjował tryb hello:</span><span class="sxs-lookup"><span data-stu-id="8a475-153">On hello **Evernote Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in IDP initiated mode:</span></span>

    ![Adresy URL i domeny Evernote pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_url.png)

    <span data-ttu-id="8a475-155">W hello **identyfikator** pole tekstowe, wprowadź adres URL hello:`https://www.evernote.com/saml2`</span><span class="sxs-lookup"><span data-stu-id="8a475-155">In hello **Identifier** textbox, type hello URL: `https://www.evernote.com/saml2`</span></span>

4. <span data-ttu-id="8a475-156">Sprawdź **Pokaż zaawansowane ustawienia adresu URL** i wykonywać powitania po kroku, jeśli chcesz, aby aplikacja hello tooconfigure w **SP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="8a475-156">Check **Show advanced URL settings** and perform hello following step if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Adresy URL i domeny Evernote pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_url1.png)

    <span data-ttu-id="8a475-158">W hello **Zaloguj się na adres URL** pole tekstowe, wprowadź adres URL hello:`https://www.evernote.com/Login.action`</span><span class="sxs-lookup"><span data-stu-id="8a475-158">In hello **Sign on URL** textbox, type hello URL: `https://www.evernote.com/Login.action`</span></span>   

5. <span data-ttu-id="8a475-159">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="8a475-159">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_certificate.png) 

6. <span data-ttu-id="8a475-161">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8a475-161">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-evernote-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="8a475-163">Na powitania **konfiguracji Evernote** kliknij **skonfigurować Evernote** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="8a475-163">On hello **Evernote Configuration** section, click **Configure Evernote** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8a475-164">Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="8a475-164">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfiguracja Evernote](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_configure.png) 

8. <span data-ttu-id="8a475-166">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy Evernote jako administrator.</span><span class="sxs-lookup"><span data-stu-id="8a475-166">In a different web browser window, log into your Evernote company site as an administrator.</span></span>

9. <span data-ttu-id="8a475-167">Przejdź do zbyt**"Konsoli administracyjnej"**</span><span class="sxs-lookup"><span data-stu-id="8a475-167">Go too**'Admin Console'**</span></span>

    ![Konsola administracyjna](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_adminconsole.png)

10. <span data-ttu-id="8a475-169">Z hello **"Konsoli administracyjnej"**, przejdź zbyt**"Zabezpieczenia"** i wybierz **"Logowanie jednokrotne"**</span><span class="sxs-lookup"><span data-stu-id="8a475-169">From hello **'Admin Console'**, go too**‘Security’** and select **‘Single Sign-On’**</span></span>

    ![Ustawienia logowania jednokrotnego](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_sso.png)

11. <span data-ttu-id="8a475-171">Skonfiguruj hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="8a475-171">Configure hello following values:</span></span>

    ![Ustawienia certyfikatów](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_certx.png)
    
    <span data-ttu-id="8a475-173">a.</span><span class="sxs-lookup"><span data-stu-id="8a475-173">a.</span></span>  <span data-ttu-id="8a475-174">**Włącz logowanie Jednokrotne:** rejestracji Jednokrotnej jest domyślnie włączona (kliknij **wyłączyć logowanie jednokrotne** wymaganie rejestracji Jednokrotnej hello tooremove)</span><span class="sxs-lookup"><span data-stu-id="8a475-174">**Enable SSO:** SSO is enabled by default (Click **Disable Single Sign-on** tooremove hello SSO requirement)</span></span>

    <span data-ttu-id="8a475-175">b.</span><span class="sxs-lookup"><span data-stu-id="8a475-175">b.</span></span> <span data-ttu-id="8a475-176">Wklej **SAML rejestracji jednokrotnej adres URL usługi** wartość, która została skopiowana z hello portalu Azure do hello **adres URL żądania HTTP SAML** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="8a475-176">Paste **SAML Single sign-on Service URL** value, which you have copied from hello Azure portal into hello **SAML HTTP Request URL** textbox.</span></span>

    <span data-ttu-id="8a475-177">c.</span><span class="sxs-lookup"><span data-stu-id="8a475-177">c.</span></span> <span data-ttu-id="8a475-178">Otwórz hello certyfikat pobrany z usługi Azure AD w programie Notatnik i skopiuj zawartości hello tym "BEGIN certyfikatu" i "END CERTIFICATE" i wklej go do hello **certyfikatu X.509** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="8a475-178">Open hello downloaded certificate from Azure AD in a notepad and copy hello content including "BEGIN CERTIFICATE" and "END CERTIFICATE" and paste it into hello **X.509 Certificate** textbox.</span></span> 

    <span data-ttu-id="8a475-179">d.Click **zapisać zmiany**</span><span class="sxs-lookup"><span data-stu-id="8a475-179">d.Click **Save Changes**</span></span>

> [!TIP]
> <span data-ttu-id="8a475-180">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="8a475-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8a475-181">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="8a475-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8a475-182">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8a475-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="8a475-183">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a475-183">Create an Azure AD test user</span></span>

<span data-ttu-id="8a475-184">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="8a475-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="8a475-186">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="8a475-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8a475-187">W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8a475-187">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-evernote-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="8a475-189">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="8a475-189">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-evernote-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="8a475-191">Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="8a475-191">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![przycisk Dodaj Hello](./media/active-directory-saas-evernote-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="8a475-193">W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="8a475-193">In hello **User** dialog box, perform hello following steps:</span></span>

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-evernote-tutorial/create_aaduser_04.png)

    <span data-ttu-id="8a475-195">a.</span><span class="sxs-lookup"><span data-stu-id="8a475-195">a.</span></span> <span data-ttu-id="8a475-196">W hello **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8a475-196">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8a475-197">b.</span><span class="sxs-lookup"><span data-stu-id="8a475-197">b.</span></span> <span data-ttu-id="8a475-198">W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="8a475-198">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="8a475-199">c.</span><span class="sxs-lookup"><span data-stu-id="8a475-199">c.</span></span> <span data-ttu-id="8a475-200">Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="8a475-200">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="8a475-201">d.</span><span class="sxs-lookup"><span data-stu-id="8a475-201">d.</span></span> <span data-ttu-id="8a475-202">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="8a475-202">Click **Create**.</span></span>
 
### <a name="create-an-evernote-test-user"></a><span data-ttu-id="8a475-203">Tworzenie użytkownika testowego Evernote</span><span class="sxs-lookup"><span data-stu-id="8a475-203">Create an Evernote test user</span></span>

<span data-ttu-id="8a475-204">W przypadku użytkowników usługi Azure AD toolog kolejności tooenable do Evernote muszą mieć przydzielone do Evernote.</span><span class="sxs-lookup"><span data-stu-id="8a475-204">In order tooenable Azure AD users toolog into Evernote, they must be provisioned into Evernote.</span></span>  
<span data-ttu-id="8a475-205">W przypadku hello Evernote Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="8a475-205">In hello case of Evernote, provisioning is a manual task.</span></span>

<span data-ttu-id="8a475-206">**tooprovision kont użytkowników, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="8a475-206">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="8a475-207">Zaloguj się za tooyour Evernote witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="8a475-207">Log in tooyour Evernote company site as an administrator.</span></span>

2. <span data-ttu-id="8a475-208">Kliknij przycisk hello **"Konsoli administracyjnej"**.</span><span class="sxs-lookup"><span data-stu-id="8a475-208">Click hello **'Admin Console'**.</span></span>

    ![Konsola administracyjna](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_adminconsole.png)

3. <span data-ttu-id="8a475-210">Z hello **"Konsoli administracyjnej"**, przejdź do zbyt**"Dodawanie użytkowników"**.</span><span class="sxs-lookup"><span data-stu-id="8a475-210">From hello **'Admin Console'**, go too**‘Add users’**.</span></span>

    ![Dodaj testUser](./media/active-directory-saas-evernote-tutorial/create_aaduser_0001.png)

4. <span data-ttu-id="8a475-212">**Dodawanie członków zespołu** w hello **E-mail** pole tekstowe, wpisz adres e-mail hello konta użytkownika i kliknij przycisk **zaprosić.**</span><span class="sxs-lookup"><span data-stu-id="8a475-212">**Add team members** in hello **Email** textbox, type hello email address of user account and click **Invite.**</span></span>

    ![Dodaj testUser](./media/active-directory-saas-evernote-tutorial/create_aaduser_0002.png)
    
5. <span data-ttu-id="8a475-214">Po wysłaniu zaproszenia, właścicielem konta usługi Azure Active Directory hello otrzymają wiadomość e-mail z zaproszeniem hello tooaccept.</span><span class="sxs-lookup"><span data-stu-id="8a475-214">After invitation is sent, hello Azure Active Directory account holder will receive an email tooaccept hello invitation.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="8a475-215">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a475-215">Assign hello Azure AD test user</span></span>

<span data-ttu-id="8a475-216">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooEvernote.</span><span class="sxs-lookup"><span data-stu-id="8a475-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEvernote.</span></span>

![Przypisanie roli użytkownika hello][200] 

<span data-ttu-id="8a475-218">**tooassign tooEvernote Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="8a475-218">**tooassign Britta Simon tooEvernote, perform hello following steps:**</span></span>

1. <span data-ttu-id="8a475-219">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="8a475-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="8a475-221">Z listy aplikacji hello wybierz **Evernote**.</span><span class="sxs-lookup"><span data-stu-id="8a475-221">In hello applications list, select **Evernote**.</span></span>

    ![łącze Evernote Hello na liście aplikacji hello](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_app.png)  

3. <span data-ttu-id="8a475-223">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="8a475-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![łącze "Użytkownicy i grupy" Hello][202]

4. <span data-ttu-id="8a475-225">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8a475-225">Click **Add** button.</span></span> <span data-ttu-id="8a475-226">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8a475-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Okienko Dodaj przypisania Hello][203]

5. <span data-ttu-id="8a475-228">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="8a475-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8a475-229">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8a475-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8a475-230">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8a475-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="8a475-231">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8a475-231">Test single sign-on</span></span>

<span data-ttu-id="8a475-232">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="8a475-232">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8a475-233">Po kliknięciu kafelka Evernote hello w hello Panel dostępu, należy pobrać zalogowane tooyour Evernote aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8a475-233">When you click hello Evernote tile in hello Access Panel, you should get signed-on tooyour Evernote application.</span></span> <span data-ttu-id="8a475-234">Można będzie można logować się jako konta organizacji, ale następnie toolog muszą się przy użyciu konta osobistego.</span><span class="sxs-lookup"><span data-stu-id="8a475-234">You'll be logging in as an Organization account but then need toolog in with your personal account.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="8a475-235">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="8a475-235">Additional resources</span></span>

* [<span data-ttu-id="8a475-236">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8a475-236">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8a475-237">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8a475-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_203.png

