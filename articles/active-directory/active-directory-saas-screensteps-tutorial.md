---
title: 'Samouczek: Integracji Azure Active Directory z ScreenSteps | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i ScreenSteps."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4563fe94-a88f-4895-a07f-79df44889cf9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: fd041e5fe4552727eeda2dabc1773d8043d410f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-screensteps"></a><span data-ttu-id="fb200-103">Samouczek: Integracji Azure Active Directory z ScreenSteps</span><span class="sxs-lookup"><span data-stu-id="fb200-103">Tutorial: Azure Active Directory integration with ScreenSteps</span></span>

<span data-ttu-id="fb200-104">Z tego samouczka, dowiesz się, jak toointegrate ScreenSteps w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fb200-104">In this tutorial, you learn how toointegrate ScreenSteps with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fb200-105">Integracja z usługą Azure AD ScreenSteps zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="fb200-105">Integrating ScreenSteps with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="fb200-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="fb200-106">You can control in Azure AD who has access tooScreenSteps.</span></span>
- <span data-ttu-id="fb200-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooScreenSteps (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fb200-107">You can enable your users tooautomatically get signed-on tooScreenSteps (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="fb200-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="fb200-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="fb200-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fb200-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fb200-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="fb200-110">Prerequisites</span></span>

<span data-ttu-id="fb200-111">tooconfigure integracji z usługą Azure AD z ScreenSteps należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="fb200-111">tooconfigure Azure AD integration with ScreenSteps, you need hello following items:</span></span>

- <span data-ttu-id="fb200-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="fb200-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fb200-113">ScreenSteps logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="fb200-113">A ScreenSteps single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fb200-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="fb200-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fb200-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="fb200-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fb200-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="fb200-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fb200-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fb200-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fb200-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="fb200-118">Scenario description</span></span>
<span data-ttu-id="fb200-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="fb200-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fb200-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="fb200-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fb200-121">Dodawanie ScreenSteps z galerii hello</span><span class="sxs-lookup"><span data-stu-id="fb200-121">Adding ScreenSteps from hello gallery</span></span>
2. <span data-ttu-id="fb200-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="fb200-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-screensteps-from-hello-gallery"></a><span data-ttu-id="fb200-123">Dodawanie ScreenSteps z galerii hello</span><span class="sxs-lookup"><span data-stu-id="fb200-123">Adding ScreenSteps from hello gallery</span></span>
<span data-ttu-id="fb200-124">tooconfigure hello integracji ScreenSteps do usługi Azure AD, należy tooadd ScreenSteps z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="fb200-124">tooconfigure hello integration of ScreenSteps into Azure AD, you need tooadd ScreenSteps from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="fb200-125">**tooadd ScreenSteps z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="fb200-125">**tooadd ScreenSteps from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="fb200-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="fb200-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="fb200-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="fb200-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="fb200-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="fb200-129">Then go too**All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. <span data-ttu-id="fb200-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="fb200-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nowy przycisk aplikacji Hello][3]

4. <span data-ttu-id="fb200-133">W polu wyszukiwania hello wpisz **ScreenSteps**, wybierz pozycję **ScreenSteps** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="fb200-133">In hello search box, type **ScreenSteps**, select **ScreenSteps** from result panel then click **Add** button tooadd hello application.</span></span>

    ![ScreenSteps hello listy wyników](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="fb200-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="fb200-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="fb200-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z ScreenSteps w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="fb200-136">In this section, you configure and test Azure AD single sign-on with ScreenSteps based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fb200-137">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w ScreenSteps jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fb200-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ScreenSteps is tooa user in Azure AD.</span></span> <span data-ttu-id="fb200-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w ScreenSteps musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="fb200-138">In other words, a link relationship between an Azure AD user and hello related user in ScreenSteps needs toobe established.</span></span>

<span data-ttu-id="fb200-139">W ScreenSteps, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="fb200-139">In ScreenSteps, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="fb200-140">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z ScreenSteps, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="fb200-140">tooconfigure and test Azure AD single sign-on with ScreenSteps, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="fb200-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="fb200-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="fb200-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="fb200-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fb200-143">**[Tworzenie użytkownika testowego ScreenSteps](#create-a-screensteps-test-user)**  -toohave odpowiednikiem Simona Britta w ScreenSteps, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fb200-143">**[Create a ScreenSteps test user](#create-a-screensteps-test-user)** - toohave a counterpart of Britta Simon in ScreenSteps that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="fb200-144">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="fb200-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fb200-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="fb200-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="fb200-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="fb200-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="fb200-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="fb200-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ScreenSteps application.</span></span>

<span data-ttu-id="fb200-148">**tooconfigure usługi Azure AD rejestracji jednokrotnej z ScreenSteps, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="fb200-148">**tooconfigure Azure AD single sign-on with ScreenSteps, perform hello following steps:**</span></span>

1. <span data-ttu-id="fb200-149">W portalu Azure na powitania hello **ScreenSteps** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="fb200-149">In hello Azure portal, on hello **ScreenSteps** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="fb200-151">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="fb200-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_samlbase.png)

3. <span data-ttu-id="fb200-153">Na powitania **ScreenSteps domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="fb200-153">On hello **ScreenSteps Domain and URLs** section, perform hello following steps:</span></span>

    ![Adresy URL i domeny ScreenSteps pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_url.png)

    <span data-ttu-id="fb200-155">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<tenantname>.ScreenSteps.com`</span><span class="sxs-lookup"><span data-stu-id="fb200-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.ScreenSteps.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fb200-156">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="fb200-156">This value is not real.</span></span> <span data-ttu-id="fb200-157">Zaktualizuj tę wartość z hello rzeczywisty logowania jednokrotnego adresu URL, który znajduje się w dalszej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="fb200-157">Update this value with hello actual Sign-On URL, which is explained later in this tutorial.</span></span> 

4. <span data-ttu-id="fb200-158">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="fb200-158">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_certificate.png) 

5. <span data-ttu-id="fb200-160">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="fb200-160">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-screensteps-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fb200-162">Na powitania **konfiguracji ScreenSteps** kliknij **skonfigurować ScreenSteps** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="fb200-162">On hello **ScreenSteps Configuration** section, click **Configure ScreenSteps** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="fb200-163">Kopiuj hello **Sign-Out adresu URL i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="fb200-163">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfiguracja ScreenSteps](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_configure.png) 

7. <span data-ttu-id="fb200-165">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy ScreenSteps jako administrator.</span><span class="sxs-lookup"><span data-stu-id="fb200-165">In a different web browser window, log into your ScreenSteps company site as an administrator.</span></span>

8. <span data-ttu-id="fb200-166">Kliknij przycisk **ustawienia konta**.</span><span class="sxs-lookup"><span data-stu-id="fb200-166">Click **Account Settings**.</span></span>

    <span data-ttu-id="fb200-167">![Zarządzanie kontami](./media/active-directory-saas-screensteps-tutorial/ic778523.png "Zarządzanie kontami")</span><span class="sxs-lookup"><span data-stu-id="fb200-167">![Account management](./media/active-directory-saas-screensteps-tutorial/ic778523.png "Account management")</span></span>

9. <span data-ttu-id="fb200-168">Kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="fb200-168">Click **Single Sign-on**.</span></span>

    <span data-ttu-id="fb200-169">![Zdalne uwierzytelnianie](./media/active-directory-saas-screensteps-tutorial/ic778524.png "uwierzytelniania zdalnego")</span><span class="sxs-lookup"><span data-stu-id="fb200-169">![Remote authentication](./media/active-directory-saas-screensteps-tutorial/ic778524.png "Remote authentication")</span></span>

10. <span data-ttu-id="fb200-170">Kliknij przycisk **Tworzenie końcowego rejestracji jednokrotnej**.</span><span class="sxs-lookup"><span data-stu-id="fb200-170">Click **Create Single Sign-on Endpoint**.</span></span>

    <span data-ttu-id="fb200-171">![Zdalne uwierzytelnianie](./media/active-directory-saas-screensteps-tutorial/ic778525.png "uwierzytelniania zdalnego")</span><span class="sxs-lookup"><span data-stu-id="fb200-171">![Remote authentication](./media/active-directory-saas-screensteps-tutorial/ic778525.png "Remote authentication")</span></span>

11. <span data-ttu-id="fb200-172">W hello **utworzyć jeden znak na punkt końcowy** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="fb200-172">In hello **Create Single Sign-on Endpoint** section, perform hello following steps:</span></span>

    <span data-ttu-id="fb200-173">![Tworzenie punktu końcowego uwierzytelniania](./media/active-directory-saas-screensteps-tutorial/ic778526.png "Tworzenie punktu końcowego uwierzytelniania")</span><span class="sxs-lookup"><span data-stu-id="fb200-173">![Create an authentication endpoint](./media/active-directory-saas-screensteps-tutorial/ic778526.png "Create an authentication endpoint")</span></span>
    
    <span data-ttu-id="fb200-174">a.</span><span class="sxs-lookup"><span data-stu-id="fb200-174">a.</span></span> <span data-ttu-id="fb200-175">W hello **tytuł** tekstowym, wpisz tytuł.</span><span class="sxs-lookup"><span data-stu-id="fb200-175">In hello **Title** textbox, type a title.</span></span>
    
    <span data-ttu-id="fb200-176">b.</span><span class="sxs-lookup"><span data-stu-id="fb200-176">b.</span></span> <span data-ttu-id="fb200-177">Z hello **tryb** listy, wybierz **SAML**.</span><span class="sxs-lookup"><span data-stu-id="fb200-177">From hello **Mode** list, select **SAML**.</span></span>
    
    <span data-ttu-id="fb200-178">c.</span><span class="sxs-lookup"><span data-stu-id="fb200-178">c.</span></span> <span data-ttu-id="fb200-179">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="fb200-179">Click **Create**.</span></span>

12. <span data-ttu-id="fb200-180">**Edytuj** hello nowy punkt końcowy.</span><span class="sxs-lookup"><span data-stu-id="fb200-180">**Edit** hello new endpoint.</span></span>

    <span data-ttu-id="fb200-181">![Edytuj punktu końcowego](./media/active-directory-saas-screensteps-tutorial/ic778528.png "edycji punktu końcowego")</span><span class="sxs-lookup"><span data-stu-id="fb200-181">![Edit endpoint](./media/active-directory-saas-screensteps-tutorial/ic778528.png "Edit endpoint")</span></span>

13. <span data-ttu-id="fb200-182">W hello **edytować jeden znak na punkt końcowy** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="fb200-182">In hello **Edit Single Sign-on Endpoint** section, perform hello following steps:</span></span>

    <span data-ttu-id="fb200-183">![Uwierzytelniania zdalnego punktu końcowego](./media/active-directory-saas-screensteps-tutorial/ic778527.png "uwierzytelniania zdalnego punktu końcowego")</span><span class="sxs-lookup"><span data-stu-id="fb200-183">![Remote authentication endpoint](./media/active-directory-saas-screensteps-tutorial/ic778527.png "Remote authentication endpoint")</span></span>

    <span data-ttu-id="fb200-184">a.</span><span class="sxs-lookup"><span data-stu-id="fb200-184">a.</span></span> <span data-ttu-id="fb200-185">Kliknij przycisk **Przekaż nowy plik certyfikatu SAML**, a następnie przekaż hello certyfikatu, który został pobrany z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="fb200-185">Click **Upload new SAML Certificate file**, and then upload hello certificate, which you have downloaded from Azure portal.</span></span>
    
    <span data-ttu-id="fb200-186">b.</span><span class="sxs-lookup"><span data-stu-id="fb200-186">b.</span></span> <span data-ttu-id="fb200-187">Wklej **SAML pojedynczy znak na adres URL usługi** wartość, która została skopiowana z hello portalu Azure do hello **zdalnego adresu URL logowania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="fb200-187">Paste **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **Remote Login URL** textbox.</span></span>
    
    <span data-ttu-id="fb200-188">c.</span><span class="sxs-lookup"><span data-stu-id="fb200-188">c.</span></span> <span data-ttu-id="fb200-189">Wklej **Sign-Out URL** wartość, która została skopiowana z hello portalu Azure do hello **adres URL wylogowania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="fb200-189">Paste **Sign-Out URL** value, which you have copied from hello Azure portal into hello **Log out URL** textbox.</span></span>
    
    <span data-ttu-id="fb200-190">d.</span><span class="sxs-lookup"><span data-stu-id="fb200-190">d.</span></span> <span data-ttu-id="fb200-191">Wybierz **grupy** tooassign toowhen użytkowników, które zostały udostępnione.</span><span class="sxs-lookup"><span data-stu-id="fb200-191">Select a **Group** tooassign users toowhen they are provisioned.</span></span>
    
    <span data-ttu-id="fb200-192">e.</span><span class="sxs-lookup"><span data-stu-id="fb200-192">e.</span></span> <span data-ttu-id="fb200-193">Kliknij przycisk **aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="fb200-193">Click **Update**.</span></span>

    <span data-ttu-id="fb200-194">f.</span><span class="sxs-lookup"><span data-stu-id="fb200-194">f.</span></span> <span data-ttu-id="fb200-195">Witaj kopii **adres URL klienta SAML** toohello Schowka i Wklej w toohello **adres URL logowania** textbox w **ScreenSteps domeny i adres URL** sekcji.</span><span class="sxs-lookup"><span data-stu-id="fb200-195">Copy hello **SAML Consumer URL** toohello clipboard and paste in toohello **Sign-on URL** textbox in **ScreenSteps Domain and URLs** section.</span></span>
    
    <span data-ttu-id="fb200-196">g.</span><span class="sxs-lookup"><span data-stu-id="fb200-196">g.</span></span> <span data-ttu-id="fb200-197">Zwraca toohello **edytować jeden znak na punkt końcowy**.</span><span class="sxs-lookup"><span data-stu-id="fb200-197">Return toohello **Edit Single Sign-on Endpoint**.</span></span>
    
    <span data-ttu-id="fb200-198">h.</span><span class="sxs-lookup"><span data-stu-id="fb200-198">h.</span></span> <span data-ttu-id="fb200-199">Kliknij przycisk hello **domyślnym kontem** przycisk toouse ten punkt końcowy dla wszystkich użytkowników, którzy logują ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="fb200-199">Click hello **Make default for account** button toouse this endpoint for all users who log into ScreenSteps.</span></span> <span data-ttu-id="fb200-200">Alternatywnie możesz kliknąć hello **dodać tooSite** przycisk toouse ten punkt końcowy dla określonych witryn internetowych w **ScreenSteps**.</span><span class="sxs-lookup"><span data-stu-id="fb200-200">Alternatively you can click hello **Add tooSite** button toouse this endpoint for specific sites in **ScreenSteps**.</span></span>

> [!TIP]
> <span data-ttu-id="fb200-201">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="fb200-201">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="fb200-202">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="fb200-202">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="fb200-203">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fb200-203">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="fb200-204">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="fb200-204">Create an Azure AD test user</span></span>

<span data-ttu-id="fb200-205">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="fb200-205">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="fb200-207">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="fb200-207">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="fb200-208">W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="fb200-208">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-screensteps-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="fb200-210">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="fb200-210">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-screensteps-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="fb200-212">Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="fb200-212">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![przycisk Dodaj Hello](./media/active-directory-saas-screensteps-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="fb200-214">W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="fb200-214">In hello **User** dialog box, perform hello following steps:</span></span>

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-screensteps-tutorial/create_aaduser_04.png)

    <span data-ttu-id="fb200-216">a.</span><span class="sxs-lookup"><span data-stu-id="fb200-216">a.</span></span> <span data-ttu-id="fb200-217">W hello **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fb200-217">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fb200-218">b.</span><span class="sxs-lookup"><span data-stu-id="fb200-218">b.</span></span> <span data-ttu-id="fb200-219">W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="fb200-219">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="fb200-220">c.</span><span class="sxs-lookup"><span data-stu-id="fb200-220">c.</span></span> <span data-ttu-id="fb200-221">Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="fb200-221">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="fb200-222">d.</span><span class="sxs-lookup"><span data-stu-id="fb200-222">d.</span></span> <span data-ttu-id="fb200-223">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="fb200-223">Click **Create**.</span></span>
 
### <a name="create-a-screensteps-test-user"></a><span data-ttu-id="fb200-224">Tworzenie użytkownika testowego ScreenSteps</span><span class="sxs-lookup"><span data-stu-id="fb200-224">Create a ScreenSteps test user</span></span>

<span data-ttu-id="fb200-225">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="fb200-225">In this section, you create a user called Britta Simon in ScreenSteps.</span></span> <span data-ttu-id="fb200-226">Praca z [zespołem pomocy technicznej klienta ScreenSteps](https://www.screensteps.com/contact) do dodawania użytkowników hello hello ScreenSteps platformy.</span><span class="sxs-lookup"><span data-stu-id="fb200-226">Work with [ScreenSteps Client support team](https://www.screensteps.com/contact) to add hello users in hello ScreenSteps platform.</span></span> <span data-ttu-id="fb200-227">Użytkownicy muszą utworzyć i aktywowana, aby użyć rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="fb200-227">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="fb200-228">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="fb200-228">Assign hello Azure AD test user</span></span>

<span data-ttu-id="fb200-229">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="fb200-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooScreenSteps.</span></span>

![Przypisanie roli użytkownika hello][200] 

<span data-ttu-id="fb200-231">**tooassign tooScreenSteps Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="fb200-231">**tooassign Britta Simon tooScreenSteps, perform hello following steps:**</span></span>

1. <span data-ttu-id="fb200-232">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="fb200-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="fb200-234">Z listy aplikacji hello wybierz **ScreenSteps**.</span><span class="sxs-lookup"><span data-stu-id="fb200-234">In hello applications list, select **ScreenSteps**.</span></span>

    ![łącze ScreenSteps Hello na liście aplikacji hello](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_app.png)  

3. <span data-ttu-id="fb200-236">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="fb200-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![łącze "Użytkownicy i grupy" Hello][202]

4. <span data-ttu-id="fb200-238">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="fb200-238">Click **Add** button.</span></span> <span data-ttu-id="fb200-239">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="fb200-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Okienko Dodaj przypisania Hello][203]

5. <span data-ttu-id="fb200-241">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="fb200-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="fb200-242">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="fb200-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fb200-243">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="fb200-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="fb200-244">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="fb200-244">Test single sign-on</span></span>

<span data-ttu-id="fb200-245">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="fb200-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="fb200-246">Po kliknięciu powitalne ScreenSteps kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour ScreenSteps aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fb200-246">When you click hello ScreenSteps tile in hello Access Panel, you should get automatically signed-on tooyour ScreenSteps application.</span></span>
<span data-ttu-id="fb200-247">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fb200-247">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="fb200-248">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="fb200-248">Additional resources</span></span>

* [<span data-ttu-id="fb200-249">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fb200-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fb200-250">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fb200-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_203.png

