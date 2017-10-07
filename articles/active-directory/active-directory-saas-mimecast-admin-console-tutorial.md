---
title: 'Samouczek: Integracji Azure Active Directory z konsoli administracyjnej Mimecast | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Mimecast konsoli administracyjnej."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 81c50614-f49b-4bbc-97d5-3cf77154305f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: 5a04a5abd9ff30d484bce0a5c97a1d3e48b69e4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-admin-console"></a><span data-ttu-id="7f463-103">Samouczek: Integracji Azure Active Directory z konsoli administracyjnej Mimecast</span><span class="sxs-lookup"><span data-stu-id="7f463-103">Tutorial: Azure Active Directory integration with Mimecast Admin Console</span></span>

<span data-ttu-id="7f463-104">Z tego samouczka, dowiesz się, jak Konsola administracyjna Mimecast toointegrate w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7f463-104">In this tutorial, you learn how toointegrate Mimecast Admin Console with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7f463-105">Integrowanie Mimecast konsoli administracyjnej z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="7f463-105">Integrating Mimecast Admin Console with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7f463-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooMimecast konsoli administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="7f463-106">You can control in Azure AD who has access tooMimecast Admin Console.</span></span>
- <span data-ttu-id="7f463-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooMimecast konsoli administracyjnej (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f463-107">You can enable your users tooautomatically get signed-on tooMimecast Admin Console (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="7f463-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="7f463-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="7f463-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7f463-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7f463-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7f463-110">Prerequisites</span></span>

<span data-ttu-id="7f463-111">tooconfigure integracji usługi Azure AD z konsoli administracyjnej Mimecast należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="7f463-111">tooconfigure Azure AD integration with Mimecast Admin Console, you need hello following items:</span></span>

- <span data-ttu-id="7f463-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f463-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7f463-113">Konsola administracyjna Mimecast logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="7f463-113">A Mimecast Admin Console single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7f463-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="7f463-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7f463-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="7f463-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7f463-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="7f463-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7f463-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7f463-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7f463-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="7f463-118">Scenario description</span></span>
<span data-ttu-id="7f463-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="7f463-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7f463-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="7f463-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7f463-121">Dodawanie Mimecast konsoli administracyjnej z galerii hello</span><span class="sxs-lookup"><span data-stu-id="7f463-121">Adding Mimecast Admin Console from hello gallery</span></span>
2. <span data-ttu-id="7f463-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="7f463-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mimecast-admin-console-from-hello-gallery"></a><span data-ttu-id="7f463-123">Dodawanie Mimecast konsoli administracyjnej z galerii hello</span><span class="sxs-lookup"><span data-stu-id="7f463-123">Adding Mimecast Admin Console from hello gallery</span></span>
<span data-ttu-id="7f463-124">tooconfigure hello integracji konsoli administracyjnej Mimecast do usługi Azure AD, należy tooadd Mimecast konsoli administracyjnej z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="7f463-124">tooconfigure hello integration of Mimecast Admin Console into Azure AD, you need tooadd Mimecast Admin Console from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7f463-125">**tooadd Mimecast konsoli administracyjnej z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="7f463-125">**tooadd Mimecast Admin Console from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7f463-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="7f463-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="7f463-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="7f463-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7f463-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="7f463-129">Then go too**All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. <span data-ttu-id="7f463-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7f463-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nowy przycisk aplikacji Hello][3]

4. <span data-ttu-id="7f463-133">W polu wyszukiwania hello wpisz **Mimecast konsoli administracyjnej**, wybierz pozycję **Mimecast konsoli administracyjnej** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="7f463-133">In hello search box, type **Mimecast Admin Console**, select **Mimecast Admin Console** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Konsola administracyjna Mimecast hello listy wyników](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7f463-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="7f463-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="7f463-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z konsoli administracyjnej Mimecast w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="7f463-136">In this section, you configure and test Azure AD single sign-on with Mimecast Admin Console based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7f463-137">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w konsoli administracyjnej Mimecast jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f463-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Mimecast Admin Console is tooa user in Azure AD.</span></span> <span data-ttu-id="7f463-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w konsoli administracyjnej Mimecast musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="7f463-138">In other words, a link relationship between an Azure AD user and hello related user in Mimecast Admin Console needs toobe established.</span></span>

<span data-ttu-id="7f463-139">W konsoli administracyjnej Mimecast, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="7f463-139">In Mimecast Admin Console, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7f463-140">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z konsoli administracyjnej Mimecast, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="7f463-140">tooconfigure and test Azure AD single sign-on with Mimecast Admin Console, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7f463-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="7f463-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7f463-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="7f463-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7f463-143">**[Tworzenie użytkownika testowego konsoli administracyjnej Mimecast](#create-a-mimecast-admin-console-test-user)**  -toohave odpowiednikiem Simona Britta w konsoli administracyjnej Mimecast, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7f463-143">**[Create a Mimecast Admin Console test user](#create-a-mimecast-admin-console-test-user)** - toohave a counterpart of Britta Simon in Mimecast Admin Console that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7f463-144">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="7f463-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7f463-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="7f463-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7f463-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="7f463-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7f463-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w aplikacji konsoli administracyjnej Mimecast.</span><span class="sxs-lookup"><span data-stu-id="7f463-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Mimecast Admin Console application.</span></span>

<span data-ttu-id="7f463-148">**tooconfigure usługi Azure AD rejestracji jednokrotnej z konsoli administracyjnej Mimecast, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="7f463-148">**tooconfigure Azure AD single sign-on with Mimecast Admin Console, perform hello following steps:**</span></span>

1. <span data-ttu-id="7f463-149">W portalu Azure na powitania hello **konsoli administracyjnej Mimecast** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="7f463-149">In hello Azure portal, on hello **Mimecast Admin Console** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="7f463-151">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="7f463-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_samlbase.png)

3. <span data-ttu-id="7f463-153">Na powitania **adresy URL i domeny konsoli administracyjnej Mimecast** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="7f463-153">On hello **Mimecast Admin Console Domain and URLs** section, perform hello following steps:</span></span>

    ![Adresy URL i domeny konsoli administracyjnej Mimecast pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_url.png)

    <span data-ttu-id="7f463-155">W hello **adres URL logowania** pole tekstowe, wprowadź adres URL hello:</span><span class="sxs-lookup"><span data-stu-id="7f463-155">In hello **Sign-on URL** textbox, type hello URL:</span></span>
    | |
    | -- |
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|

    > [!NOTE] 
    > <span data-ttu-id="7f463-156">znak Hello na adres URL jest określonym regionie.</span><span class="sxs-lookup"><span data-stu-id="7f463-156">hello sign on URL is region specific.</span></span>

4. <span data-ttu-id="7f463-157">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="7f463-157">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_certificate.png) 

5. <span data-ttu-id="7f463-159">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="7f463-159">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7f463-161">Na powitania **Konfiguracja konsoli administratora Mimecast** , kliknij przycisk **skonfigurować konsoli administracyjnej Mimecast** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="7f463-161">On hello **Mimecast Admin Console Configuration** section, click **Configure Mimecast Admin Console** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7f463-162">Kopiuj hello **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="7f463-162">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfiguracja konsoli administratora Mimecast](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_configure.png) 

7. <span data-ttu-id="7f463-164">W oknie przeglądarki innej witryny sieci web Zaloguj się do konsoli administracyjnej Mimecast jako administrator.</span><span class="sxs-lookup"><span data-stu-id="7f463-164">In a different web browser window, log into your Mimecast Admin Console as an administrator.</span></span>

8. <span data-ttu-id="7f463-165">Przejdź za**usług \> aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="7f463-165">Go too**Services \> Application**.</span></span>

    <span data-ttu-id="7f463-166">![Usługi](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794998.png "usług")</span><span class="sxs-lookup"><span data-stu-id="7f463-166">![Services](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794998.png "Services")</span></span>

9. <span data-ttu-id="7f463-167">Kliknij przycisk **profile uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="7f463-167">Click **Authentication Profiles**.</span></span>

    <span data-ttu-id="7f463-168">![Profile uwierzytelniania](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794999.png "profile uwierzytelniania")</span><span class="sxs-lookup"><span data-stu-id="7f463-168">![Authentication Profiles](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794999.png "Authentication Profiles")</span></span>
    
10. <span data-ttu-id="7f463-169">Kliknij przycisk **nowy profil uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="7f463-169">Click **New Authentication Profile**.</span></span>

    <span data-ttu-id="7f463-170">![Nowych profilów uwierzytelniania](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795000.png "nowych profilów uwierzytelniania")</span><span class="sxs-lookup"><span data-stu-id="7f463-170">![New Authentication Profiles](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795000.png "New Authentication Profiles")</span></span>

11. <span data-ttu-id="7f463-171">W hello **profilu uwierzytelniania** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="7f463-171">In hello **Authentication Profile** section, perform hello following steps:</span></span>

    <span data-ttu-id="7f463-172">![Profil uwierzytelniania](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795015.png "profilu uwierzytelniania")</span><span class="sxs-lookup"><span data-stu-id="7f463-172">![Authentication Profile](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795015.png "Authentication Profile")</span></span>
    
    <span data-ttu-id="7f463-173">a.</span><span class="sxs-lookup"><span data-stu-id="7f463-173">a.</span></span> <span data-ttu-id="7f463-174">W hello **opis** tekstowym, wpisz nazwę dla danej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="7f463-174">In hello **Description** textbox, type a name for your configuration.</span></span>
    
    <span data-ttu-id="7f463-175">b.</span><span class="sxs-lookup"><span data-stu-id="7f463-175">b.</span></span> <span data-ttu-id="7f463-176">Wybierz **wymusić uwierzytelnianie SAML dla konsoli administracyjnej Mimecast**.</span><span class="sxs-lookup"><span data-stu-id="7f463-176">Select **Enforce SAML Authentication for Mimecast Admin Console**.</span></span>
    
    <span data-ttu-id="7f463-177">c.</span><span class="sxs-lookup"><span data-stu-id="7f463-177">c.</span></span> <span data-ttu-id="7f463-178">Jako **dostawcy**, wybierz pozycję **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7f463-178">As **Provider**, select **Azure Active Directory**.</span></span>
    
    <span data-ttu-id="7f463-179">d.</span><span class="sxs-lookup"><span data-stu-id="7f463-179">d.</span></span> <span data-ttu-id="7f463-180">Wklej **identyfikator jednostki SAML**, która została skopiowana z hello portalu Azure do hello **adres URL wystawcy** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="7f463-180">Paste **SAML Entity ID**, which you have copied from hello Azure portal into hello **Issuer URL** textbox.</span></span>
    
    <span data-ttu-id="7f463-181">e.</span><span class="sxs-lookup"><span data-stu-id="7f463-181">e.</span></span> <span data-ttu-id="7f463-182">Wklej **SAML pojedynczy znak na adres URL usługi**, która została skopiowana z hello portalu Azure do hello **adres URL logowania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="7f463-182">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **Login URL** textbox.</span></span>

    <span data-ttu-id="7f463-183">f.</span><span class="sxs-lookup"><span data-stu-id="7f463-183">f.</span></span> <span data-ttu-id="7f463-184">Wklej **SAML pojedynczy znak na adres URL usługi**, która została skopiowana z hello portalu Azure do hello **adresu URL wylogowania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="7f463-184">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **Logout URL** textbox.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="7f463-185">Witaj wartość adresu URL logowania i wartość adresu URL wylogowania hello są dla hello konsoli administracyjnej Mimecast hello takie same.</span><span class="sxs-lookup"><span data-stu-id="7f463-185">hello Login URL value and hello Logout URL value are for hello Mimecast Admin Console hello same.</span></span>
    
    <span data-ttu-id="7f463-186">g.</span><span class="sxs-lookup"><span data-stu-id="7f463-186">g.</span></span> <span data-ttu-id="7f463-187">Otwórz swój certyfikat base-64 pobrany z portalu Azure w programie Notatnik, Usuń pierwszy wiersz hello ("*--*") i hello ostatniego wiersza ("*--*"), hello kopiowania pozostałej zawartości z niego do Schowka a następnie wklej go toohello **certyfikat dostawcy tożsamości (metadanymi)** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="7f463-187">Open your base-64 certificate downloaded from Azure portal in notepad, remove hello first line (“*--*“) and hello last line (“*--*“), copy hello remaining content of it into your clipboard, and then paste it toohello **Identity Provider Certificate (Metadata)** textbox.</span></span>
    
    <span data-ttu-id="7f463-188">h.</span><span class="sxs-lookup"><span data-stu-id="7f463-188">h.</span></span> <span data-ttu-id="7f463-189">Wybierz **Zezwalaj funkcji logowania jednokrotnego w**.</span><span class="sxs-lookup"><span data-stu-id="7f463-189">Select **Allow Single Sign On**.</span></span>
    
    <span data-ttu-id="7f463-190">i.</span><span class="sxs-lookup"><span data-stu-id="7f463-190">i.</span></span> <span data-ttu-id="7f463-191">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="7f463-191">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="7f463-192">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="7f463-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7f463-193">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="7f463-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7f463-194">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7f463-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7f463-195">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f463-195">Create an Azure AD test user</span></span>

<span data-ttu-id="7f463-196">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="7f463-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="7f463-198">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="7f463-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7f463-199">W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="7f463-199">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="7f463-201">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="7f463-201">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="7f463-203">Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="7f463-203">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![przycisk Dodaj Hello](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="7f463-205">W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="7f463-205">In hello **User** dialog box, perform hello following steps:</span></span>

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_04.png)

    <span data-ttu-id="7f463-207">a.</span><span class="sxs-lookup"><span data-stu-id="7f463-207">a.</span></span> <span data-ttu-id="7f463-208">W hello **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7f463-208">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7f463-209">b.</span><span class="sxs-lookup"><span data-stu-id="7f463-209">b.</span></span> <span data-ttu-id="7f463-210">W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="7f463-210">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="7f463-211">c.</span><span class="sxs-lookup"><span data-stu-id="7f463-211">c.</span></span> <span data-ttu-id="7f463-212">Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="7f463-212">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="7f463-213">d.</span><span class="sxs-lookup"><span data-stu-id="7f463-213">d.</span></span> <span data-ttu-id="7f463-214">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="7f463-214">Click **Create**.</span></span>
 
### <a name="create-a-mimecast-admin-console-test-user"></a><span data-ttu-id="7f463-215">Tworzenie użytkownika testowego Mimecast konsoli administracyjnej</span><span class="sxs-lookup"><span data-stu-id="7f463-215">Create a Mimecast Admin Console test user</span></span>

<span data-ttu-id="7f463-216">W przypadku użytkowników usługi Azure AD toolog kolejności tooenable w konsoli administracyjnej Mimecast muszą mieć przydzielone do konsoli administracyjnej Mimecast.</span><span class="sxs-lookup"><span data-stu-id="7f463-216">In order tooenable Azure AD users toolog into Mimecast Admin Console, they must be provisioned into Mimecast Admin Console.</span></span> <span data-ttu-id="7f463-217">W przypadku hello Mimecast konsoli administracyjnej Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="7f463-217">In hello case of Mimecast Admin Console, provisioning is a manual task.</span></span>

* <span data-ttu-id="7f463-218">Należy tooregister domeny, przed przystąpieniem do tworzenia użytkowników.</span><span class="sxs-lookup"><span data-stu-id="7f463-218">You need tooregister a domain before you can create users.</span></span>

<span data-ttu-id="7f463-219">**tooconfigure aprowizacji użytkowników, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="7f463-219">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="7f463-220">Zaloguj się na tooyour **konsoli administracyjnej Mimecast** jako administrator.</span><span class="sxs-lookup"><span data-stu-id="7f463-220">Sign on tooyour **Mimecast Admin Console** as administrator.</span></span>
2. <span data-ttu-id="7f463-221">Przejdź za**katalogów \> wewnętrzne**.</span><span class="sxs-lookup"><span data-stu-id="7f463-221">Go too**Directories \> Internal**.</span></span>
   
   <span data-ttu-id="7f463-222">![Katalogi](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795003.png "katalogów")</span><span class="sxs-lookup"><span data-stu-id="7f463-222">![Directories](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795003.png "Directories")</span></span>
3. <span data-ttu-id="7f463-223">Kliknij przycisk **zarejestrować nową domenę**.</span><span class="sxs-lookup"><span data-stu-id="7f463-223">Click **Register New Domain**.</span></span>
   
   <span data-ttu-id="7f463-224">![Zarejestrować nową domenę](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795004.png "zarejestrować nową domenę")</span><span class="sxs-lookup"><span data-stu-id="7f463-224">![Register New Domain](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795004.png "Register New Domain")</span></span>
4. <span data-ttu-id="7f463-225">Po utworzeniu nowej domeny, kliknij przycisk **nowy adres**.</span><span class="sxs-lookup"><span data-stu-id="7f463-225">After your new domain has been created, click **New Address**.</span></span>
   
   <span data-ttu-id="7f463-226">![Nowy adres](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795005.png "nowy adres")</span><span class="sxs-lookup"><span data-stu-id="7f463-226">![New Address](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795005.png "New Address")</span></span>
5. <span data-ttu-id="7f463-227">W hello nowego okna dialogowego adres i wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="7f463-227">In hello new address dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="7f463-228">![Zapisz](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795006.png "Zapisz")</span><span class="sxs-lookup"><span data-stu-id="7f463-228">![Save](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795006.png "Save")</span></span>
   
   <span data-ttu-id="7f463-229">a.</span><span class="sxs-lookup"><span data-stu-id="7f463-229">a.</span></span> <span data-ttu-id="7f463-230">Typ hello **adres E-mail**, **globalną nazwę**, **hasło**, i **Potwierdź hasło** atrybutów elementów prawidłową usługi Azure AD konto ma mają tooprovision do hello powiązanych pól tekstowych.</span><span class="sxs-lookup"><span data-stu-id="7f463-230">Type hello **Email Address**, **Global Name**, **Password**, and **Confirm Password** attributes of a valid Azure AD account you want tooprovision into hello related textboxes.</span></span>

   <span data-ttu-id="7f463-231">b.</span><span class="sxs-lookup"><span data-stu-id="7f463-231">b.</span></span> <span data-ttu-id="7f463-232">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="7f463-232">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="7f463-233">Można użyć innych narzędzi tworzenia konta użytkownika konsoli administracyjnej Mimecast lub interfejsów API dostarczonych przez konta użytkowników usługi Azure AD tooprovision Mimecast konsoli administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="7f463-233">You can use any other Mimecast Admin Console user account creation tools or APIs provided by Mimecast Admin Console tooprovision Azure AD user accounts.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="7f463-234">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f463-234">Assign hello Azure AD test user</span></span>

<span data-ttu-id="7f463-235">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooMimecast konsoli administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="7f463-235">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMimecast Admin Console.</span></span>

![Przypisanie roli użytkownika hello][200] 

<span data-ttu-id="7f463-237">**tooassign tooMimecast Simona Britta konsoli administracyjnej, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="7f463-237">**tooassign Britta Simon tooMimecast Admin Console, perform hello following steps:**</span></span>

1. <span data-ttu-id="7f463-238">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="7f463-238">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="7f463-240">Z listy aplikacji hello wybierz **konsoli administracyjnej Mimecast**.</span><span class="sxs-lookup"><span data-stu-id="7f463-240">In hello applications list, select **Mimecast Admin Console**.</span></span>

    ![łącze konsoli administracyjnej Mimecast Hello na liście aplikacji hello](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_app.png)  

3. <span data-ttu-id="7f463-242">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="7f463-242">In hello menu on hello left, click **Users and groups**.</span></span>

    ![łącze "Użytkownicy i grupy" Hello][202]

4. <span data-ttu-id="7f463-244">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="7f463-244">Click **Add** button.</span></span> <span data-ttu-id="7f463-245">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7f463-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Okienko Dodaj przypisania Hello][203]

5. <span data-ttu-id="7f463-247">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="7f463-247">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7f463-248">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7f463-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7f463-249">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7f463-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="7f463-250">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="7f463-250">Test single sign-on</span></span>

<span data-ttu-id="7f463-251">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="7f463-251">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7f463-252">Po kliknięciu kafelka konsoli administracyjnej Mimecast hello w hello Panel dostępu, należy pobrać aplikacji konsoli administracyjnej Mimecast tooyour zalogowane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="7f463-252">When you click hello Mimecast Admin Console tile in hello Access Panel, you should get automatically signed-on tooyour Mimecast Admin Console application.</span></span>
<span data-ttu-id="7f463-253">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7f463-253">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7f463-254">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="7f463-254">Additional resources</span></span>

* [<span data-ttu-id="7f463-255">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7f463-255">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7f463-256">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7f463-256">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_203.png

