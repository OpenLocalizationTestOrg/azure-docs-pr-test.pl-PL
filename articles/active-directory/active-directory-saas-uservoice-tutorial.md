---
title: 'Samouczek: Integracji Azure Active Directory z UserVoice | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i usługi UserVoice."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 684a405b-8932-46f6-b43a-4d97a42b6b87
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.openlocfilehash: 9eade8435ae6c6a3821bbbec9ab7c27ed7ad91ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-uservoice"></a><span data-ttu-id="88bf1-103">Samouczek: Integracji Azure Active Directory z UserVoice</span><span class="sxs-lookup"><span data-stu-id="88bf1-103">Tutorial: Azure Active Directory integration with UserVoice</span></span>

<span data-ttu-id="88bf1-104">Z tego samouczka, dowiesz się, jak toointegrate UserVoice w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="88bf1-104">In this tutorial, you learn how toointegrate UserVoice with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="88bf1-105">Integracja z usługą Azure AD UserVoice zawiera hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="88bf1-105">Integrating UserVoice with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="88bf1-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooUserVoice.</span><span class="sxs-lookup"><span data-stu-id="88bf1-106">You can control in Azure AD who has access tooUserVoice.</span></span>
- <span data-ttu-id="88bf1-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooUserVoice (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="88bf1-107">You can enable your users tooautomatically get signed-on tooUserVoice (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="88bf1-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="88bf1-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="88bf1-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="88bf1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="88bf1-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="88bf1-110">Prerequisites</span></span>

<span data-ttu-id="88bf1-111">tooconfigure integracji z usługą Azure AD z UserVoice należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="88bf1-111">tooconfigure Azure AD integration with UserVoice, you need hello following items:</span></span>

- <span data-ttu-id="88bf1-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="88bf1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="88bf1-113">UserVoice logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="88bf1-113">A UserVoice single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="88bf1-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="88bf1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="88bf1-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="88bf1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="88bf1-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="88bf1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="88bf1-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="88bf1-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="88bf1-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="88bf1-118">Scenario description</span></span>
<span data-ttu-id="88bf1-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="88bf1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="88bf1-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="88bf1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="88bf1-121">Dodawanie UserVoice z galerii hello</span><span class="sxs-lookup"><span data-stu-id="88bf1-121">Adding UserVoice from hello gallery</span></span>
2. <span data-ttu-id="88bf1-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="88bf1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-uservoice-from-hello-gallery"></a><span data-ttu-id="88bf1-123">Dodawanie UserVoice z galerii hello</span><span class="sxs-lookup"><span data-stu-id="88bf1-123">Adding UserVoice from hello gallery</span></span>
<span data-ttu-id="88bf1-124">tooconfigure hello integracji usługi UserVoice w usłudze Azure Active Directory, należy tooadd UserVoice z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="88bf1-124">tooconfigure hello integration of UserVoice into Azure AD, you need tooadd UserVoice from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="88bf1-125">**tooadd UserVoice z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="88bf1-125">**tooadd UserVoice from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="88bf1-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="88bf1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="88bf1-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="88bf1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="88bf1-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="88bf1-129">Then go too**All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. <span data-ttu-id="88bf1-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="88bf1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nowy przycisk aplikacji Hello][3]

4. <span data-ttu-id="88bf1-133">W polu wyszukiwania hello wpisz **UserVoice**, wybierz pozycję **UserVoice** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="88bf1-133">In hello search box, type **UserVoice**, select **UserVoice** from result panel then click **Add** button tooadd hello application.</span></span>

    ![UserVoice hello listy wyników](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="88bf1-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="88bf1-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="88bf1-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z UserVoice w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="88bf1-136">In this section, you configure and test Azure AD single sign-on with UserVoice based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="88bf1-137">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w UserVoice jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="88bf1-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in UserVoice is tooa user in Azure AD.</span></span> <span data-ttu-id="88bf1-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w UserVoice musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="88bf1-138">In other words, a link relationship between an Azure AD user and hello related user in UserVoice needs toobe established.</span></span>

<span data-ttu-id="88bf1-139">W UserVoice, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="88bf1-139">In UserVoice, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="88bf1-140">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z UserVoice, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="88bf1-140">tooconfigure and test Azure AD single sign-on with UserVoice, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="88bf1-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="88bf1-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="88bf1-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="88bf1-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="88bf1-143">**[Tworzenie użytkownika testowego UserVoice](#create-a-uservoice-test-user)**  -toohave odpowiednikiem Simona Britta w UserVoice, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="88bf1-143">**[Create a UserVoice test user](#create-a-uservoice-test-user)** - toohave a counterpart of Britta Simon in UserVoice that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="88bf1-144">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="88bf1-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="88bf1-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="88bf1-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="88bf1-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="88bf1-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="88bf1-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w aplikacji UserVoice.</span><span class="sxs-lookup"><span data-stu-id="88bf1-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your UserVoice application.</span></span>

<span data-ttu-id="88bf1-148">**tooconfigure usługi Azure AD rejestracji jednokrotnej z UserVoice, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="88bf1-148">**tooconfigure Azure AD single sign-on with UserVoice, perform hello following steps:**</span></span>

1. <span data-ttu-id="88bf1-149">W portalu Azure na powitania hello **UserVoice** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="88bf1-149">In hello Azure portal, on hello **UserVoice** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="88bf1-151">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="88bf1-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_samlbase.png)

3. <span data-ttu-id="88bf1-153">Na powitania **UserVoice domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="88bf1-153">On hello **UserVoice Domain and URLs** section, perform hello following steps:</span></span>

    ![Adresy URL i domeny UserVoice pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_url.png)

    <span data-ttu-id="88bf1-155">a.</span><span class="sxs-lookup"><span data-stu-id="88bf1-155">a.</span></span> <span data-ttu-id="88bf1-156">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<tenantname>.UserVoice.com`</span><span class="sxs-lookup"><span data-stu-id="88bf1-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.UserVoice.com`</span></span>

    <span data-ttu-id="88bf1-157">b.</span><span class="sxs-lookup"><span data-stu-id="88bf1-157">b.</span></span> <span data-ttu-id="88bf1-158">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<tenantname>.UserVoice.com`</span><span class="sxs-lookup"><span data-stu-id="88bf1-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenantname>.UserVoice.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="88bf1-159">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="88bf1-159">These values are not real.</span></span> <span data-ttu-id="88bf1-160">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="88bf1-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="88bf1-161">Skontaktuj się z [zespołem pomocy technicznej klienta UserVoice](https://www.uservoice.com/) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="88bf1-161">Contact [UserVoice Client support team](https://www.uservoice.com/) tooget these values.</span></span>

4. <span data-ttu-id="88bf1-162">Na powitania **certyfikat podpisywania SAML** hello kopiowania, sekcji **odcisk PALCA** wartości certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="88bf1-162">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_certificate.png) 

5. <span data-ttu-id="88bf1-164">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="88bf1-164">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-uservoice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="88bf1-166">Na powitania **konfiguracji UserVoice** kliknij **skonfigurować UserVoice** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="88bf1-166">On hello **UserVoice Configuration** section, click **Configure UserVoice** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="88bf1-167">Witaj kopii **Sign-Out adresu URL i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="88bf1-167">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfiguracja usługi UserVoice](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_configure.png) 

7. <span data-ttu-id="88bf1-169">W oknie przeglądarki innej witryny sieci web Zaloguj się w witrynie firmy UserVoice tooyour jako administrator.</span><span class="sxs-lookup"><span data-stu-id="88bf1-169">In a different web browser window, log in tooyour UserVoice company site as an administrator.</span></span>

8. <span data-ttu-id="88bf1-170">Hello pasku narzędzi u góry hello, kliknij przycisk **ustawienia**, a następnie wybierz **portalu sieci Web** hello menu.</span><span class="sxs-lookup"><span data-stu-id="88bf1-170">In hello toolbar on hello top, click **Settings**, and then select **Web portal** from hello menu.</span></span>
   
    <span data-ttu-id="88bf1-171">![W sekcji Ustawienia na stronie aplikacji](./media/active-directory-saas-uservoice-tutorial/ic777519.png "ustawienia")</span><span class="sxs-lookup"><span data-stu-id="88bf1-171">![Settings Section On App Side](./media/active-directory-saas-uservoice-tutorial/ic777519.png "Settings")</span></span>

9. <span data-ttu-id="88bf1-172">Na powitania **portalu sieci Web** na karcie hello **uwierzytelnianie użytkownika** kliknij **Edytuj** tooopen hello **Edytuj uwierzytelnianie użytkownika** okna dialogowego Strona.</span><span class="sxs-lookup"><span data-stu-id="88bf1-172">On hello **Web portal** tab, in hello **User authentication** section, click **Edit** tooopen hello **Edit User Authentication** dialog page.</span></span>
   
    <span data-ttu-id="88bf1-173">![Portal sieci Web kartę](./media/active-directory-saas-uservoice-tutorial/ic777520.png "portalu sieci Web")</span><span class="sxs-lookup"><span data-stu-id="88bf1-173">![Web portal Tab](./media/active-directory-saas-uservoice-tutorial/ic777520.png "Web portal")</span></span>

10. <span data-ttu-id="88bf1-174">Na powitania **Edytuj uwierzytelnianie użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="88bf1-174">On hello **Edit User Authentication** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="88bf1-175">![Edytuj uwierzytelnianie użytkownika](./media/active-directory-saas-uservoice-tutorial/ic777521.png "Edytuj uwierzytelnianie użytkownika")</span><span class="sxs-lookup"><span data-stu-id="88bf1-175">![Edit user authentication](./media/active-directory-saas-uservoice-tutorial/ic777521.png "Edit user authentication")</span></span>
   
    <span data-ttu-id="88bf1-176">a.</span><span class="sxs-lookup"><span data-stu-id="88bf1-176">a.</span></span> <span data-ttu-id="88bf1-177">Kliknij przycisk **logowanie jednokrotne (SSO)**.</span><span class="sxs-lookup"><span data-stu-id="88bf1-177">Click **Single Sign-On (SSO)**.</span></span>
 
    <span data-ttu-id="88bf1-178">b.</span><span class="sxs-lookup"><span data-stu-id="88bf1-178">b.</span></span> <span data-ttu-id="88bf1-179">Wklej hello **SAML pojedynczy znak na adres URL usługi** wartość, która została skopiowana z hello portalu Azure do hello **logowania jednokrotnego zdalnego logowania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="88bf1-179">Paste hello **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **SSO Remote Sign-In** textbox.</span></span>

    <span data-ttu-id="88bf1-180">c.</span><span class="sxs-lookup"><span data-stu-id="88bf1-180">c.</span></span> <span data-ttu-id="88bf1-181">Wklej hello **Sign-Out adres URL** wartość, która została skopiowana z hello portalu Azure do hello **Sign-Out zdalnego logowania jednokrotnego textbox**.</span><span class="sxs-lookup"><span data-stu-id="88bf1-181">Paste hello **Sign-Out URL** value, which you have copied from hello Azure portal into hello **SSO Remote Sign-Out textbox**.</span></span>
 
    <span data-ttu-id="88bf1-182">d.</span><span class="sxs-lookup"><span data-stu-id="88bf1-182">d.</span></span> <span data-ttu-id="88bf1-183">Wklej hello **odcisk palca** wartość, która została skopiowana z portalu Azure do **bieżącego odcisk palca certyfikatu SHA1** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="88bf1-183">Paste hello **Thumbprint** value , which you have copied from Azure portal  into the **Current certificate SHA1 fingerprint** textbox.</span></span>
    
    <span data-ttu-id="88bf1-184">e.</span><span class="sxs-lookup"><span data-stu-id="88bf1-184">e.</span></span> <span data-ttu-id="88bf1-185">Kliknij przycisk **Zapisz ustawienia uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="88bf1-185">Click **Save authentication settings**.</span></span>

> [!TIP]
> <span data-ttu-id="88bf1-186">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="88bf1-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="88bf1-187">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="88bf1-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="88bf1-188">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="88bf1-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="88bf1-189">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="88bf1-189">Create an Azure AD test user</span></span>

<span data-ttu-id="88bf1-190">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="88bf1-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="88bf1-192">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="88bf1-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="88bf1-193">W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="88bf1-193">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-uservoice-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="88bf1-195">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="88bf1-195">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-uservoice-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="88bf1-197">Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="88bf1-197">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![przycisk Dodaj Hello](./media/active-directory-saas-uservoice-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="88bf1-199">W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="88bf1-199">In hello **User** dialog box, perform hello following steps:</span></span>

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-uservoice-tutorial/create_aaduser_04.png)

    <span data-ttu-id="88bf1-201">a.</span><span class="sxs-lookup"><span data-stu-id="88bf1-201">a.</span></span> <span data-ttu-id="88bf1-202">W hello **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="88bf1-202">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="88bf1-203">b.</span><span class="sxs-lookup"><span data-stu-id="88bf1-203">b.</span></span> <span data-ttu-id="88bf1-204">W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="88bf1-204">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="88bf1-205">c.</span><span class="sxs-lookup"><span data-stu-id="88bf1-205">c.</span></span> <span data-ttu-id="88bf1-206">Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="88bf1-206">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="88bf1-207">d.</span><span class="sxs-lookup"><span data-stu-id="88bf1-207">d.</span></span> <span data-ttu-id="88bf1-208">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="88bf1-208">Click **Create**.</span></span>
 
### <a name="create-a-uservoice-test-user"></a><span data-ttu-id="88bf1-209">Tworzenie użytkownika testowego UserVoice</span><span class="sxs-lookup"><span data-stu-id="88bf1-209">Create a UserVoice test user</span></span>

<span data-ttu-id="88bf1-210">toolog użytkowników tooenable usługi Azure AD w tooUserVoice, muszą mieć przydzielone do UserVoice.</span><span class="sxs-lookup"><span data-stu-id="88bf1-210">tooenable Azure AD users toolog in tooUserVoice, they must be provisioned into UserVoice.</span></span> <span data-ttu-id="88bf1-211">W przypadku hello UserVoice Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="88bf1-211">In hello case of UserVoice, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="88bf1-212">tooprovision konta użytkownika, należy wykonać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="88bf1-212">tooprovision a user account, perform hello following steps:</span></span>
1. <span data-ttu-id="88bf1-213">Zaloguj się za tooyour **UserVoice** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="88bf1-213">Log in tooyour **UserVoice** tenant.</span></span>

2. <span data-ttu-id="88bf1-214">Przejdź za**ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="88bf1-214">Go too**Settings**.</span></span>
   
    <span data-ttu-id="88bf1-215">![Ustawienia](./media/active-directory-saas-uservoice-tutorial/ic777811.png "ustawienia")</span><span class="sxs-lookup"><span data-stu-id="88bf1-215">![Settings](./media/active-directory-saas-uservoice-tutorial/ic777811.png "Settings")</span></span>

3. <span data-ttu-id="88bf1-216">Kliknij przycisk **ogólne**.</span><span class="sxs-lookup"><span data-stu-id="88bf1-216">Click **General**.</span></span>

4. <span data-ttu-id="88bf1-217">Kliknij przycisk **agentów i uprawnienia**.</span><span class="sxs-lookup"><span data-stu-id="88bf1-217">Click **Agents and permissions**.</span></span>
   
    <span data-ttu-id="88bf1-218">![Agenci i uprawnienia](./media/active-directory-saas-uservoice-tutorial/ic777812.png "agentów i uprawnień")</span><span class="sxs-lookup"><span data-stu-id="88bf1-218">![Agents and permissions](./media/active-directory-saas-uservoice-tutorial/ic777812.png "Agents and permissions")</span></span>

5. <span data-ttu-id="88bf1-219">Kliknij przycisk **dodać Administratorzy**.</span><span class="sxs-lookup"><span data-stu-id="88bf1-219">Click **Add admins**.</span></span>
   
    <span data-ttu-id="88bf1-220">![Dodaj administratorów](./media/active-directory-saas-uservoice-tutorial/ic777813.png "dodać administratorów")</span><span class="sxs-lookup"><span data-stu-id="88bf1-220">![Add admins](./media/active-directory-saas-uservoice-tutorial/ic777813.png "Add admins")</span></span>

6. <span data-ttu-id="88bf1-221">Na powitania **zaprosić Administratorzy** okna dialogowego, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="88bf1-221">On hello **Invite admins** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="88bf1-222">![Zaproś Administratorzy](./media/active-directory-saas-uservoice-tutorial/ic777814.png "zaprosić Administratorzy")</span><span class="sxs-lookup"><span data-stu-id="88bf1-222">![Invite admins](./media/active-directory-saas-uservoice-tutorial/ic777814.png "Invite admins")</span></span>
   
    <span data-ttu-id="88bf1-223">a.</span><span class="sxs-lookup"><span data-stu-id="88bf1-223">a.</span></span> <span data-ttu-id="88bf1-224">W polu tekstowym wiadomości powitania, wpisz adres e-mail hello konta hello tooprovision, a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="88bf1-224">In hello Emails textbox, type hello email address of hello account you want tooprovision, and then click **Add**.</span></span>
   
    <span data-ttu-id="88bf1-225">b.</span><span class="sxs-lookup"><span data-stu-id="88bf1-225">b.</span></span> <span data-ttu-id="88bf1-226">Kliknij przycisk **zaprosić**.</span><span class="sxs-lookup"><span data-stu-id="88bf1-226">Click **Invite**.</span></span>

> [!NOTE]
> <span data-ttu-id="88bf1-227">Możesz użyć innych UserVoice użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez UserVoice tooprovision kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="88bf1-227">You can use any other UserVoice user account creation tools or APIs provided by UserVoice tooprovision AAD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="88bf1-228">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="88bf1-228">Assign hello Azure AD test user</span></span>

<span data-ttu-id="88bf1-229">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooUserVoice.</span><span class="sxs-lookup"><span data-stu-id="88bf1-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooUserVoice.</span></span>

![Przypisanie roli użytkownika hello][200] 

<span data-ttu-id="88bf1-231">**tooassign tooUserVoice Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="88bf1-231">**tooassign Britta Simon tooUserVoice, perform hello following steps:**</span></span>

1. <span data-ttu-id="88bf1-232">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="88bf1-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="88bf1-234">Z listy aplikacji hello wybierz **UserVoice**.</span><span class="sxs-lookup"><span data-stu-id="88bf1-234">In hello applications list, select **UserVoice**.</span></span>

    ![łącze UserVoice Hello na liście aplikacji hello](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_app.png)  

3. <span data-ttu-id="88bf1-236">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="88bf1-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![łącze "Użytkownicy i grupy" Hello][202]

4. <span data-ttu-id="88bf1-238">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="88bf1-238">Click **Add** button.</span></span> <span data-ttu-id="88bf1-239">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="88bf1-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Okienko Dodaj przypisania Hello][203]

5. <span data-ttu-id="88bf1-241">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="88bf1-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="88bf1-242">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="88bf1-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="88bf1-243">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="88bf1-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="88bf1-244">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="88bf1-244">Test single sign-on</span></span>

<span data-ttu-id="88bf1-245">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="88bf1-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="88bf1-246">Po kliknięciu kafelka UserVoice hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour UserVoice aplikacji.</span><span class="sxs-lookup"><span data-stu-id="88bf1-246">When you click hello UserVoice tile in hello Access Panel, you should get automatically signed-on tooyour UserVoice application.</span></span>
<span data-ttu-id="88bf1-247">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="88bf1-247">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="88bf1-248">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="88bf1-248">Additional resources</span></span>

* [<span data-ttu-id="88bf1-249">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="88bf1-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="88bf1-250">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="88bf1-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_203.png

