---
title: 'Samouczek: Integracji Azure Active Directory z Citrix ShareFile | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Citrix ShareFile."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: e14fc310-bac4-4f09-99ef-87e5c77288b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2017
ms.author: jeedes
ms.openlocfilehash: d7eaf140e56c40f9f621062849dd8558588ffd1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-sharefile"></a><span data-ttu-id="55818-103">Samouczek: Integracji Azure Active Directory z Citrix ShareFile</span><span class="sxs-lookup"><span data-stu-id="55818-103">Tutorial: Azure Active Directory integration with Citrix ShareFile</span></span>

<span data-ttu-id="55818-104">Z tego samouczka, dowiesz się, jak toointegrate Citrix ShareFile w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="55818-104">In this tutorial, you learn how toointegrate Citrix ShareFile with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="55818-105">Integracja z usługą Azure AD Citrix ShareFile zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="55818-105">Integrating Citrix ShareFile with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="55818-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooCitrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="55818-106">You can control in Azure AD who has access tooCitrix ShareFile.</span></span>
- <span data-ttu-id="55818-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooCitrix ShareFile (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="55818-107">You can enable your users tooautomatically get signed-on tooCitrix ShareFile (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="55818-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="55818-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="55818-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="55818-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="55818-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="55818-110">Prerequisites</span></span>

<span data-ttu-id="55818-111">tooconfigure integracji usługi Azure AD z Citrix ShareFile, należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="55818-111">tooconfigure Azure AD integration with Citrix ShareFile, you need hello following items:</span></span>

- <span data-ttu-id="55818-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="55818-112">An Azure AD subscription</span></span>
- <span data-ttu-id="55818-113">Citrix ShareFile logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="55818-113">A Citrix ShareFile single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="55818-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="55818-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="55818-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="55818-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="55818-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="55818-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="55818-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="55818-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="55818-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="55818-118">Scenario description</span></span>
<span data-ttu-id="55818-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="55818-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="55818-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="55818-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="55818-121">Dodaj Citrix ShareFile z galerii hello</span><span class="sxs-lookup"><span data-stu-id="55818-121">Add Citrix ShareFile from hello gallery</span></span>
2. <span data-ttu-id="55818-122">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="55818-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-citrix-sharefile-from-hello-gallery"></a><span data-ttu-id="55818-123">Dodaj Citrix ShareFile z galerii hello</span><span class="sxs-lookup"><span data-stu-id="55818-123">Add Citrix ShareFile from hello gallery</span></span>
<span data-ttu-id="55818-124">tooconfigure hello integracji Citrix ShareFile do usługi Azure AD, należy tooadd Citrix ShareFile z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="55818-124">tooconfigure hello integration of Citrix ShareFile into Azure AD, you need tooadd Citrix ShareFile from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="55818-125">**tooadd Citrix ShareFile z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="55818-125">**tooadd Citrix ShareFile from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="55818-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="55818-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="55818-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="55818-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="55818-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="55818-129">Then go too**All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. <span data-ttu-id="55818-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="55818-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nowy przycisk aplikacji Hello][3]

4. <span data-ttu-id="55818-133">W polu wyszukiwania hello wpisz **Citrix ShareFile**, wybierz pozycję **Citrix ShareFile** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="55818-133">In hello search box, type **Citrix ShareFile**, select **Citrix ShareFile** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Citrix ShareFile w hello liście wyników](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="55818-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="55818-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="55818-136">W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z Citrix ShareFile w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="55818-136">In this section, you configure and test Azure AD single sign-on with Citrix ShareFile based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="55818-137">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Citrix ShareFile jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="55818-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Citrix ShareFile is tooa user in Azure AD.</span></span> <span data-ttu-id="55818-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Citrix ShareFile musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="55818-138">In other words, a link relationship between an Azure AD user and hello related user in Citrix ShareFile needs toobe established.</span></span>

<span data-ttu-id="55818-139">W Citrix ShareFile, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="55818-139">In Citrix ShareFile, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="55818-140">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Citrix ShareFile, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="55818-140">tooconfigure and test Azure AD single sign-on with Citrix ShareFile, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="55818-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="55818-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="55818-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="55818-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="55818-143">**[Tworzenie użytkownika testowego Citrix ShareFile](#create-a-citrix-sharefile-test-user)**  -toohave odpowiednikiem Simona Britta w Citrix ShareFile, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="55818-143">**[Create a Citrix ShareFile test user](#create-a-citrix-sharefile-test-user)** - toohave a counterpart of Britta Simon in Citrix ShareFile that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="55818-144">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="55818-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="55818-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="55818-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="55818-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="55818-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="55818-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="55818-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Citrix ShareFile application.</span></span>

<span data-ttu-id="55818-148">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Citrix ShareFile, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="55818-148">**tooconfigure Azure AD single sign-on with Citrix ShareFile, perform hello following steps:**</span></span>

1. <span data-ttu-id="55818-149">W portalu Azure na powitania hello **Citrix ShareFile** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="55818-149">In hello Azure portal, on hello **Citrix ShareFile** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="55818-151">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="55818-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_samlbase.png)

3. <span data-ttu-id="55818-153">Na powitania **Citrix ShareFile domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="55818-153">On hello **Citrix ShareFile Domain and URLs** section, perform hello following steps:</span></span>

    ![Adresy URL i domeny ShareFile Citrix pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_url.png)
    
    <span data-ttu-id="55818-155">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<tenant-name>.sharefile.com/saml/login`</span><span class="sxs-lookup"><span data-stu-id="55818-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.sharefile.com/saml/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="55818-156">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="55818-156">This value is not real.</span></span> <span data-ttu-id="55818-157">Zaktualizuj tę wartość z hello rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="55818-157">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="55818-158">Skontaktuj się z [zespołem pomocy technicznej klienta ShareFile Citrix](https://www.citrix.co.in/products/sharefile/support.html) tooget tej wartości.</span><span class="sxs-lookup"><span data-stu-id="55818-158">Contact [Citrix ShareFile Client support team](https://www.citrix.co.in/products/sharefile/support.html) tooget this value.</span></span> 

4. <span data-ttu-id="55818-159">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="55818-159">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_certificate.png) 

5. <span data-ttu-id="55818-161">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="55818-161">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-sharefile-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="55818-163">Na powitania **konfigurację serwera Citrix ShareFile** , kliknij przycisk **skonfigurować Citrix ShareFile** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="55818-163">On hello **Citrix ShareFile Configuration** section, click **Configure Citrix ShareFile** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="55818-164">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="55818-164">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfiguracja Citrix ShareFile](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_configure.png) 

7. <span data-ttu-id="55818-166">W oknie przeglądarki innej witryny sieci web, zaloguj się do Twojego **Citrix ShareFile** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="55818-166">In a different web browser window, log into your **Citrix ShareFile** company site as an administrator.</span></span>

8. <span data-ttu-id="55818-167">Witaj pasku narzędzi u góry hello, kliknij przycisk **Admin**.</span><span class="sxs-lookup"><span data-stu-id="55818-167">In hello toolbar on hello top, click **Admin**.</span></span>

9. <span data-ttu-id="55818-168">Wybierz w okienku nawigacji po lewej stronie powitania **skonfigurować logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="55818-168">In hello left navigation pane, select **Configure Single Sign-On**.</span></span>
   
    <span data-ttu-id="55818-169">![Konto administracji](./media/active-directory-saas-sharefile-tutorial/ic773627.png "konta administracji")</span><span class="sxs-lookup"><span data-stu-id="55818-169">![Account Administration](./media/active-directory-saas-sharefile-tutorial/ic773627.png "Account Administration")</span></span>

10. <span data-ttu-id="55818-170">Na powitania **rejestracji jednokrotnej / Konfiguracja SAML 2.0** strony okna dialogowego, w obszarze **podstawowe ustawienia**, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="55818-170">On hello **Single Sign-On/ SAML 2.0 Configuration** dialog page under **Basic Settings**, perform hello following steps:</span></span>
   
    <span data-ttu-id="55818-171">![Logowanie jednokrotne](./media/active-directory-saas-sharefile-tutorial/ic773628.png "logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="55818-171">![Single sign-on](./media/active-directory-saas-sharefile-tutorial/ic773628.png "Single sign-on")</span></span>
   
    <span data-ttu-id="55818-172">a.</span><span class="sxs-lookup"><span data-stu-id="55818-172">a.</span></span> <span data-ttu-id="55818-173">Kliknij przycisk **Włącz SAML**.</span><span class="sxs-lookup"><span data-stu-id="55818-173">Click **Enable SAML**.</span></span>
    
    <span data-ttu-id="55818-174">b.</span><span class="sxs-lookup"><span data-stu-id="55818-174">b.</span></span> <span data-ttu-id="55818-175">W **Your wystawcy IDP / identyfikator jednostki** pole tekstowe, Wklej wartość hello **identyfikator jednostki SAML** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="55818-175">In **Your IDP Issuer/ Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="55818-176">c.</span><span class="sxs-lookup"><span data-stu-id="55818-176">c.</span></span> <span data-ttu-id="55818-177">Kliknij przycisk **zmiany** dalej toohello **certyfikatu X.509** pola, a następnie przekazywania hello certyfikat pobrany z portalu Azure hello.</span><span class="sxs-lookup"><span data-stu-id="55818-177">Click **Change** next toohello **X.509 Certificate** field and then upload hello certificate you downloaded from hello Azure portal.</span></span>
    
    <span data-ttu-id="55818-178">d.</span><span class="sxs-lookup"><span data-stu-id="55818-178">d.</span></span> <span data-ttu-id="55818-179">W **adres URL logowania** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="55818-179">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="55818-180">e.</span><span class="sxs-lookup"><span data-stu-id="55818-180">e.</span></span> <span data-ttu-id="55818-181">W **adresu URL wylogowania** pole tekstowe, Wklej wartość hello **Sign-Out URL** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="55818-181">In **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

11. <span data-ttu-id="55818-182">Kliknij przycisk **zapisać** na powitania Citrix ShareFile portalu zarządzania.</span><span class="sxs-lookup"><span data-stu-id="55818-182">Click **Save** on hello Citrix ShareFile management portal.</span></span>

> [!TIP]
> <span data-ttu-id="55818-183">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="55818-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="55818-184">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="55818-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="55818-185">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="55818-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="55818-186">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="55818-186">Create an Azure AD test user</span></span>

<span data-ttu-id="55818-187">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="55818-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="55818-189">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="55818-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="55818-190">W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="55818-190">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-sharefile-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="55818-192">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="55818-192">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-sharefile-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="55818-194">Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="55818-194">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![przycisk Dodaj Hello](./media/active-directory-saas-sharefile-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="55818-196">W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="55818-196">In hello **User** dialog box, perform hello following steps:</span></span>

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-sharefile-tutorial/create_aaduser_04.png)

    <span data-ttu-id="55818-198">a.</span><span class="sxs-lookup"><span data-stu-id="55818-198">a.</span></span> <span data-ttu-id="55818-199">W hello **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="55818-199">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="55818-200">b.</span><span class="sxs-lookup"><span data-stu-id="55818-200">b.</span></span> <span data-ttu-id="55818-201">W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="55818-201">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="55818-202">c.</span><span class="sxs-lookup"><span data-stu-id="55818-202">c.</span></span> <span data-ttu-id="55818-203">Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="55818-203">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="55818-204">d.</span><span class="sxs-lookup"><span data-stu-id="55818-204">d.</span></span> <span data-ttu-id="55818-205">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="55818-205">Click **Create**.</span></span>
 
### <a name="create-a-citrix-sharefile-test-user"></a><span data-ttu-id="55818-206">Tworzenie użytkownika testowego Citrix ShareFile</span><span class="sxs-lookup"><span data-stu-id="55818-206">Create a Citrix ShareFile test user</span></span>

<span data-ttu-id="55818-207">W kolejności tooenable usługi Azure AD użytkownicy toolog do Citrix ShareFile musi być przygotowana do Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="55818-207">In order tooenable Azure AD users toolog into Citrix ShareFile, they must be provisioned into Citrix ShareFile.</span></span> <span data-ttu-id="55818-208">W przypadku hello Citrix ShareFile Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="55818-208">In hello case of Citrix ShareFile, provisioning is a manual task.</span></span>

<span data-ttu-id="55818-209">**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="55818-209">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="55818-210">Zaloguj się za tooyour **Citrix ShareFile** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="55818-210">Log in tooyour **Citrix ShareFile** tenant.</span></span>

2. <span data-ttu-id="55818-211">Kliknij przycisk **Zarządzanie użytkownikami \> Zarządzanie główną użytkowników \> + Tworzenie pracownika**.</span><span class="sxs-lookup"><span data-stu-id="55818-211">Click **Manage Users \> Manage Users Home \> + Create Employee**.</span></span>
   
   <span data-ttu-id="55818-212">![Tworzenie pracownika](./media/active-directory-saas-sharefile-tutorial/IC781050.png "Tworzenie pracownika")</span><span class="sxs-lookup"><span data-stu-id="55818-212">![Create Employee](./media/active-directory-saas-sharefile-tutorial/IC781050.png "Create Employee")</span></span>

3. <span data-ttu-id="55818-213">Na powitania **podstawowe informacje** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="55818-213">On hello **Basic Information** section, perform below steps:</span></span>
   
   <span data-ttu-id="55818-214">![Podstawowe informacje](./media/active-directory-saas-sharefile-tutorial/IC799951.png "podstawowe informacje")</span><span class="sxs-lookup"><span data-stu-id="55818-214">![Basic Information](./media/active-directory-saas-sharefile-tutorial/IC799951.png "Basic Information")</span></span>
   
   <span data-ttu-id="55818-215">a.</span><span class="sxs-lookup"><span data-stu-id="55818-215">a.</span></span> <span data-ttu-id="55818-216">W hello **adres E-mail** tekstowym, wpisz adres e-mail hello Simona Britta jako  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="55818-216">In hello **Email Address** textbox, type hello email address of Britta Simon as **brittasimon@contoso.com**.</span></span>
   
   <span data-ttu-id="55818-217">b.</span><span class="sxs-lookup"><span data-stu-id="55818-217">b.</span></span> <span data-ttu-id="55818-218">W hello **imię** pole tekstowe, typ **imię** użytkownika jako **Britta**.</span><span class="sxs-lookup"><span data-stu-id="55818-218">In hello **First Name** textbox, type **first name** of user as **Britta**.</span></span>
   
   <span data-ttu-id="55818-219">c.</span><span class="sxs-lookup"><span data-stu-id="55818-219">c.</span></span> <span data-ttu-id="55818-220">W hello **nazwisko** pole tekstowe, typ **nazwisko** użytkownika jako **Simona**.</span><span class="sxs-lookup"><span data-stu-id="55818-220">In hello **Last Name** textbox, type **last name** of user as **Simon**.</span></span>

4. <span data-ttu-id="55818-221">Kliknij przycisk **dodać użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="55818-221">Click **Add User**.</span></span>
  
   >[!NOTE]
   ><span data-ttu-id="55818-222">właścicielem konta usługi Azure AD Hello będzie otrzymywać wiadomości e-mail i postępuj zgodnie tooconfirm łącze swojego konta przed staje się aktywny. Możesz użyć innych Citrix ShareFile użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez tooprovision Citrix ShareFile kont użytkowników usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="55818-222">hello Azure AD account holder will receive an email and follow a link tooconfirm their account before it becomes active.You can use any other Citrix ShareFile user account creation tools or APIs provided by Citrix ShareFile tooprovision Azure AD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="55818-223">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="55818-223">Assign hello Azure AD test user</span></span>

<span data-ttu-id="55818-224">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooCitrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="55818-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCitrix ShareFile.</span></span>

![Przypisanie roli użytkownika hello][200] 

<span data-ttu-id="55818-226">**tooassign tooCitrix Simona Britta ShareFile, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="55818-226">**tooassign Britta Simon tooCitrix ShareFile, perform hello following steps:**</span></span>

1. <span data-ttu-id="55818-227">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="55818-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="55818-229">Z listy aplikacji hello wybierz **Citrix ShareFile**.</span><span class="sxs-lookup"><span data-stu-id="55818-229">In hello applications list, select **Citrix ShareFile**.</span></span>

    ![Witaj Citrix ShareFile łącza na liście aplikacji hello](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_app.png)  

3. <span data-ttu-id="55818-231">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="55818-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![łącze "Użytkownicy i grupy" Hello][202]

4. <span data-ttu-id="55818-233">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="55818-233">Click **Add** button.</span></span> <span data-ttu-id="55818-234">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="55818-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Okienko Dodaj przypisania Hello][203]

5. <span data-ttu-id="55818-236">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="55818-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="55818-237">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="55818-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="55818-238">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="55818-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="55818-239">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="55818-239">Test single sign-on</span></span>

<span data-ttu-id="55818-240">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="55818-240">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="55818-241">Po kliknięciu hello Citrix ShareFile kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Citrix ShareFile aplikacji.</span><span class="sxs-lookup"><span data-stu-id="55818-241">When you click hello Citrix ShareFile tile in hello Access Panel, you should get automatically signed-on tooyour Citrix ShareFile application.</span></span>
<span data-ttu-id="55818-242">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="55818-242">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="55818-243">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="55818-243">Additional resources</span></span>

* [<span data-ttu-id="55818-244">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="55818-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="55818-245">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="55818-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_203.png

