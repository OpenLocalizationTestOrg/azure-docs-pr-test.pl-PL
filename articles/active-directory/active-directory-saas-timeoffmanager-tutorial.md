---
title: 'Samouczek: Integracji Azure Active Directory z TimeOffManager | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i TimeOffManager."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3685912f-d5aa-4730-ab58-35a088fc1cc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: c871257bfb49883e31b1c4860a9d7faa70e9ab48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-timeoffmanager"></a><span data-ttu-id="090d4-103">Samouczek: Integracji Azure Active Directory z TimeOffManager</span><span class="sxs-lookup"><span data-stu-id="090d4-103">Tutorial: Azure Active Directory integration with TimeOffManager</span></span>

<span data-ttu-id="090d4-104">Z tego samouczka, dowiesz się, jak toointegrate TimeOffManager w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="090d4-104">In this tutorial, you learn how toointegrate TimeOffManager with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="090d4-105">Integracja z usługą Azure AD TimeOffManager zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="090d4-105">Integrating TimeOffManager with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="090d4-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooTimeOffManager</span><span class="sxs-lookup"><span data-stu-id="090d4-106">You can control in Azure AD who has access tooTimeOffManager</span></span>
- <span data-ttu-id="090d4-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooTimeOffManager (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="090d4-107">You can enable your users tooautomatically get signed-on tooTimeOffManager (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="090d4-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="090d4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="090d4-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="090d4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="090d4-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="090d4-110">Prerequisites</span></span>

<span data-ttu-id="090d4-111">tooconfigure integracji z usługą Azure AD z TimeOffManager należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="090d4-111">tooconfigure Azure AD integration with TimeOffManager, you need hello following items:</span></span>

- <span data-ttu-id="090d4-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="090d4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="090d4-113">TimeOffManager logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="090d4-113">A TimeOffManager single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="090d4-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="090d4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="090d4-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="090d4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="090d4-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="090d4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="090d4-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="090d4-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="090d4-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="090d4-118">Scenario description</span></span>
<span data-ttu-id="090d4-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="090d4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="090d4-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="090d4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="090d4-121">Dodaj TimeOffManager z galerii hello</span><span class="sxs-lookup"><span data-stu-id="090d4-121">Add TimeOffManager from hello gallery</span></span>
2. <span data-ttu-id="090d4-122">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="090d4-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-timeoffmanager-from-hello-gallery"></a><span data-ttu-id="090d4-123">Dodaj TimeOffManager z galerii hello</span><span class="sxs-lookup"><span data-stu-id="090d4-123">Add TimeOffManager from hello gallery</span></span>
<span data-ttu-id="090d4-124">tooconfigure hello integracji TimeOffManager do usługi Azure AD, należy tooadd TimeOffManager z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="090d4-124">tooconfigure hello integration of TimeOffManager into Azure AD, you need tooadd TimeOffManager from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="090d4-125">**tooadd TimeOffManager z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="090d4-125">**tooadd TimeOffManager from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="090d4-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="090d4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="090d4-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="090d4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="090d4-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="090d4-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="090d4-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="090d4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="090d4-133">W polu wyszukiwania hello wpisz **TimeOffManager**, wybierz pozycję **TimeOffManager** z panelu wyników, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="090d4-133">In hello search box, type **TimeOffManager**, select **TimeOffManager** from result panel and then click **Add** button tooadd hello application.</span></span>

    ![Dodaj z galerii](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="090d4-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="090d4-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="090d4-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z TimeOffManager w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="090d4-136">In this section, you configure and test Azure AD single sign-on with TimeOffManager based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="090d4-137">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w TimeOffManager jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="090d4-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TimeOffManager is tooa user in Azure AD.</span></span> <span data-ttu-id="090d4-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w TimeOffManager musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="090d4-138">In other words, a link relationship between an Azure AD user and hello related user in TimeOffManager needs toobe established.</span></span>

<span data-ttu-id="090d4-139">W TimeOffManager, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="090d4-139">In TimeOffManager, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="090d4-140">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z TimeOffManager, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="090d4-140">tooconfigure and test Azure AD single sign-on with TimeOffManager, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="090d4-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="090d4-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="090d4-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="090d4-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="090d4-143">**[Tworzenie użytkownika testowego TimeOffManager](#create-a-timeoffmanager-test-user)**  -toohave odpowiednikiem Simona Britta w TimeOffManager, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="090d4-143">**[Create a TimeOffManager test user](#create-a-timeoffmanager-test-user)** - toohave a counterpart of Britta Simon in TimeOffManager that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="090d4-144">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="090d4-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="090d4-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="090d4-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="090d4-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="090d4-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="090d4-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji TimeOffManager.</span><span class="sxs-lookup"><span data-stu-id="090d4-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TimeOffManager application.</span></span>

<span data-ttu-id="090d4-148">**tooconfigure usługi Azure AD rejestracji jednokrotnej z TimeOffManager, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="090d4-148">**tooconfigure Azure AD single sign-on with TimeOffManager, perform hello following steps:**</span></span>

1. <span data-ttu-id="090d4-149">W portalu Azure na powitania hello **TimeOffManager** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="090d4-149">In hello Azure portal, on hello **TimeOffManager** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="090d4-151">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="090d4-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![SAML na podstawie logowania jednokrotnego](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_samlbase.png)

3. <span data-ttu-id="090d4-153">Na powitania **TimeOffManager domeny i adres URL** sekcji, wykonaj następujące hello:</span><span class="sxs-lookup"><span data-stu-id="090d4-153">On hello **TimeOffManager Domain and URLs** section, perform hello following:</span></span>

     ![Sekcja TimeOffManager domeny i adresy URL](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_url.png)

    <span data-ttu-id="090d4-155">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company_id=<companyid>`</span><span class="sxs-lookup"><span data-stu-id="090d4-155">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company_id=<companyid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="090d4-156">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="090d4-156">This value is not real.</span></span> <span data-ttu-id="090d4-157">Zaktualizuj tę wartość przy hello rzeczywisty adres URL odpowiedzi służący.</span><span class="sxs-lookup"><span data-stu-id="090d4-157">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="090d4-158">Można uzyskać wartość tego parametru **logowania jednokrotnego strony ustawień** którym znajduje się w dalszej części samouczka hello lub skontaktuj się z [zespołem pomocy technicznej TimeOffManager](http://www.timeoffmanager.com/contact-us.aspx).</span><span class="sxs-lookup"><span data-stu-id="090d4-158">You can get this value from **Single Sign on settings page** which is explained later in hello tutorial or Contact [TimeOffManager support team](http://www.timeoffmanager.com/contact-us.aspx).</span></span>
 
4. <span data-ttu-id="090d4-159">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="090d4-159">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Sekcja certyfikat podpisywania SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_certificate.png) 

5. <span data-ttu-id="090d4-161">Celem Hello w tej sekcji jest toooutline jak tooenable użytkowników tooauthenticate tooTimeOffManger do swojego konta w usłudze Azure AD przy użyciu Federacji oparte na powitania protokołu SAML.</span><span class="sxs-lookup"><span data-stu-id="090d4-161">hello objective of this section is toooutline how tooenable users tooauthenticate tooTimeOffManger with their account in Azure AD using federation based on hello SAML protocol.</span></span>
    
    <span data-ttu-id="090d4-162">Aplikacja TimeOffManger oczekuje potwierdzenia SAML hello w określonym formacie wymaga możesz tooadd atrybutu niestandardowego mapowania tooyour SAML tokenu atrybuty konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="090d4-162">Your TimeOffManger application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="090d4-163">powitania po zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="090d4-163">hello following screenshot shows an example for this.</span></span>

    <span data-ttu-id="090d4-164">![atrybuty tokenu SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_attrb.png "atrybuty tokenu saml")</span><span class="sxs-lookup"><span data-stu-id="090d4-164">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_attrb.png "saml token attributes")</span></span>
    
    | <span data-ttu-id="090d4-165">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="090d4-165">Attribute Name</span></span> | <span data-ttu-id="090d4-166">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="090d4-166">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="090d4-167">Imię</span><span class="sxs-lookup"><span data-stu-id="090d4-167">Firstname</span></span> |<span data-ttu-id="090d4-168">User.givenName</span><span class="sxs-lookup"><span data-stu-id="090d4-168">User.givenname</span></span> |
    | <span data-ttu-id="090d4-169">nazwisko</span><span class="sxs-lookup"><span data-stu-id="090d4-169">Lastname</span></span> |<span data-ttu-id="090d4-170">User.surname</span><span class="sxs-lookup"><span data-stu-id="090d4-170">User.surname</span></span> |
    | <span data-ttu-id="090d4-171">Adres e-mail</span><span class="sxs-lookup"><span data-stu-id="090d4-171">Email</span></span> |<span data-ttu-id="090d4-172">User.mail</span><span class="sxs-lookup"><span data-stu-id="090d4-172">User.mail</span></span> |
    
    <span data-ttu-id="090d4-173">a.</span><span class="sxs-lookup"><span data-stu-id="090d4-173">a.</span></span>  <span data-ttu-id="090d4-174">Dla każdego wiersza danych w powyższej tabeli powitania kliknij **Dodaj atrybut użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="090d4-174">For each data row in hello table above, click **add user attribute**.</span></span>
    
    <span data-ttu-id="090d4-175">![atrybuty tokenu SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb.png "atrybuty tokenu saml")</span><span class="sxs-lookup"><span data-stu-id="090d4-175">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb.png "saml token attributes")</span></span>
    
    <span data-ttu-id="090d4-176">![atrybuty tokenu SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb1.png "atrybuty tokenu saml")</span><span class="sxs-lookup"><span data-stu-id="090d4-176">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb1.png "saml token attributes")</span></span>
    
    <span data-ttu-id="090d4-177">b.</span><span class="sxs-lookup"><span data-stu-id="090d4-177">b.</span></span>  <span data-ttu-id="090d4-178">W hello **nazwa atrybutu** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="090d4-178">In hello **Attribute Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="090d4-179">c.</span><span class="sxs-lookup"><span data-stu-id="090d4-179">c.</span></span>  <span data-ttu-id="090d4-180">W hello **wartość atrybutu** pole tekstowe, wartość atrybutu hello wybierz wyświetlanego dla tego wiersza.</span><span class="sxs-lookup"><span data-stu-id="090d4-180">In hello **Attribute Value** textbox, select hello attribute  value shown for that row.</span></span>
    
    <span data-ttu-id="090d4-181">d.</span><span class="sxs-lookup"><span data-stu-id="090d4-181">d.</span></span>  <span data-ttu-id="090d4-182">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="090d4-182">Click **Ok**.</span></span>
    
6. <span data-ttu-id="090d4-183">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="090d4-183">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="090d4-185">Na powitania **konfiguracji TimeOffManager** kliknij **skonfigurować TimeOffManager** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="090d4-185">On hello **TimeOffManager Configuration** section, click **Configure TimeOffManager** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="090d4-186">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="090d4-186">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Sekcja konfiguracji TimeOffManager](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_configure.png) 

8. <span data-ttu-id="090d4-188">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy TimeOffManager jako administrator.</span><span class="sxs-lookup"><span data-stu-id="090d4-188">In a different web browser window, log into your TimeOffManager company site as an administrator.</span></span>

9. <span data-ttu-id="090d4-189">Przejdź za**konta \> opcje konta \> ustawień rejestracji jednokrotnej**.</span><span class="sxs-lookup"><span data-stu-id="090d4-189">Go too**Account \> Account Options \> Single Sign-On Settings**.</span></span>
   
   <span data-ttu-id="090d4-190">![Single Sign-On ustawienia](./media/active-directory-saas-timeoffmanager-tutorial/ic795917.png "Single Sign-On ustawienia")</span><span class="sxs-lookup"><span data-stu-id="090d4-190">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795917.png "Single Sign-On Settings")</span></span>
7. <span data-ttu-id="090d4-191">W hello **ustawień rejestracji jednokrotnej** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="090d4-191">In hello **Single Sign-On Settings** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="090d4-192">![Single Sign-On ustawienia](./media/active-directory-saas-timeoffmanager-tutorial/ic795918.png "Single Sign-On ustawienia")</span><span class="sxs-lookup"><span data-stu-id="090d4-192">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795918.png "Single Sign-On Settings")</span></span>
   
   <span data-ttu-id="090d4-193">a.</span><span class="sxs-lookup"><span data-stu-id="090d4-193">a.</span></span> <span data-ttu-id="090d4-194">Otwieranie certyfikatu zakodowanego base-64 w Notatniku hello kopiowania zawartości go do Schowka, a następnie wklej hello cały certyfikat do **certyfikatu X.509** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="090d4-194">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste hello entire Certificate into **X.509 Certificate** textbox.</span></span>
   
   <span data-ttu-id="090d4-195">b.</span><span class="sxs-lookup"><span data-stu-id="090d4-195">b.</span></span> <span data-ttu-id="090d4-196">W **wystawcy Idp** pole tekstowe, Wklej wartość hello **identyfikator jednostki SAML** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="090d4-196">In **Idp Issuer** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="090d4-197">c.</span><span class="sxs-lookup"><span data-stu-id="090d4-197">c.</span></span> <span data-ttu-id="090d4-198">W **adres URL punktu końcowego IdP** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="090d4-198">In **IdP Endpoint URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="090d4-199">d.</span><span class="sxs-lookup"><span data-stu-id="090d4-199">d.</span></span> <span data-ttu-id="090d4-200">Jako **wymusić SAML**, wybierz pozycję **nr**.</span><span class="sxs-lookup"><span data-stu-id="090d4-200">As **Enforce SAML**, select **No**.</span></span>
   
   <span data-ttu-id="090d4-201">e.</span><span class="sxs-lookup"><span data-stu-id="090d4-201">e.</span></span> <span data-ttu-id="090d4-202">Jako **automatyczne tworzenie użytkowników**, wybierz pozycję **tak**.</span><span class="sxs-lookup"><span data-stu-id="090d4-202">As **Auto-Create Users**, select **Yes**.</span></span>
   
   <span data-ttu-id="090d4-203">f.</span><span class="sxs-lookup"><span data-stu-id="090d4-203">f.</span></span> <span data-ttu-id="090d4-204">W **adresu URL wylogowania** pole tekstowe, Wklej wartość hello **Sign-Out URL** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="090d4-204">In **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="090d4-205">g.</span><span class="sxs-lookup"><span data-stu-id="090d4-205">g.</span></span> <span data-ttu-id="090d4-206">Kliknij przycisk **zapisać zmiany**.</span><span class="sxs-lookup"><span data-stu-id="090d4-206">click **Save Changes**.</span></span>

11. <span data-ttu-id="090d4-207">W **logowania jednokrotnego ustawienia** strony wartość hello kopiowania **adres URL usługi klienta potwierdzenia** i wklej go w hello **adres URL odpowiedzi** pole tekstowe w obszarze **TimeOffManager Adresy URL i domeny** sekcji w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="090d4-207">In **Single Sign on settings** page, copy hello value of **Assertion Consumer Service URL** and paste it in hello **Reply URL** text box under **TimeOffManager Domain and URLs** section in Azure portal.</span></span> 

      <span data-ttu-id="090d4-208">![Single Sign-On ustawienia](./media/active-directory-saas-timeoffmanager-tutorial/ic795915.png "Single Sign-On ustawienia")</span><span class="sxs-lookup"><span data-stu-id="090d4-208">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795915.png "Single Sign-On Settings")</span></span>

> [!TIP]
> <span data-ttu-id="090d4-209">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="090d4-209">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="090d4-210">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="090d4-210">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="090d4-211">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="090d4-211">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="090d4-212">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="090d4-212">Create an Azure AD test user</span></span>
<span data-ttu-id="090d4-213">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="090d4-213">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="090d4-215">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="090d4-215">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="090d4-216">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="090d4-216">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="090d4-218">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="090d4-218">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Użytkownicy i grupy--> Wszyscy użytkownicy](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="090d4-220">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="090d4-220">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Dodawanie przycisku](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="090d4-222">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="090d4-222">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Strony okna dialogowego użytkownika](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="090d4-224">a.</span><span class="sxs-lookup"><span data-stu-id="090d4-224">a.</span></span> <span data-ttu-id="090d4-225">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="090d4-225">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="090d4-226">b.</span><span class="sxs-lookup"><span data-stu-id="090d4-226">b.</span></span> <span data-ttu-id="090d4-227">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="090d4-227">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="090d4-228">c.</span><span class="sxs-lookup"><span data-stu-id="090d4-228">c.</span></span> <span data-ttu-id="090d4-229">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="090d4-229">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="090d4-230">d.</span><span class="sxs-lookup"><span data-stu-id="090d4-230">d.</span></span> <span data-ttu-id="090d4-231">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="090d4-231">Click **Create**.</span></span>
 
### <a name="create-a-timeoffmanager-test-user"></a><span data-ttu-id="090d4-232">Tworzenie użytkownika testowego TimeOffManager</span><span class="sxs-lookup"><span data-stu-id="090d4-232">Create a TimeOffManager test user</span></span>

<span data-ttu-id="090d4-233">Użytkownicy usługi Azure AD toolog kolejności tooenable do TimeOffManager muszą być tooTimeOffManager elastycznie.</span><span class="sxs-lookup"><span data-stu-id="090d4-233">In order tooenable Azure AD users toolog into TimeOffManager, they must be provisioned tooTimeOffManager.</span></span>  

<span data-ttu-id="090d4-234">TimeOffManager obsługuje tylko w czasie Inicjowanie obsługi użytkowników.</span><span class="sxs-lookup"><span data-stu-id="090d4-234">TimeOffManager supports just in time user provisioning.</span></span> <span data-ttu-id="090d4-235">Nie ma elementu akcji dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="090d4-235">There is no action item for you.</span></span>  

<span data-ttu-id="090d4-236">Witaj użytkownicy są automatycznie dodawane podczas logowania pierwszy hello przy użyciu rejestracji jednokrotnej w.</span><span class="sxs-lookup"><span data-stu-id="090d4-236">hello users are added automatically during hello first login using single sign on.</span></span>

>[!NOTE]
><span data-ttu-id="090d4-237">Możesz użyć innych TimeOffManager użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez TimeOffManager tooprovision kont użytkowników usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="090d4-237">You can use any other TimeOffManager user account creation tools or APIs provided by TimeOffManager tooprovision Azure AD user accounts.</span></span>
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="090d4-238">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="090d4-238">Assign hello Azure AD test user</span></span>

<span data-ttu-id="090d4-239">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooTimeOffManager.</span><span class="sxs-lookup"><span data-stu-id="090d4-239">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTimeOffManager.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="090d4-241">**tooassign tooTimeOffManager Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="090d4-241">**tooassign Britta Simon tooTimeOffManager, perform hello following steps:**</span></span>

1. <span data-ttu-id="090d4-242">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="090d4-242">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="090d4-244">Z listy aplikacji hello wybierz **TimeOffManager**.</span><span class="sxs-lookup"><span data-stu-id="090d4-244">In hello applications list, select **TimeOffManager**.</span></span>

    ![TimeOffManager listy aplikacji](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_app.png) 

3. <span data-ttu-id="090d4-246">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="090d4-246">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="090d4-248">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="090d4-248">Click **Add** button.</span></span> <span data-ttu-id="090d4-249">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="090d4-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="090d4-251">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="090d4-251">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="090d4-252">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="090d4-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="090d4-253">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="090d4-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="090d4-254">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="090d4-254">Test single sign-on</span></span>

<span data-ttu-id="090d4-255">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="090d4-255">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="090d4-256">Po kliknięciu kafelka TimeOffManager hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour TimeOffManager aplikacji.</span><span class="sxs-lookup"><span data-stu-id="090d4-256">When you click hello TimeOffManager tile in hello Access Panel, you should get automatically signed-on tooyour TimeOffManager application.</span></span> <span data-ttu-id="090d4-257">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="090d4-257">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="090d4-258">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="090d4-258">Additional resources</span></span>

* [<span data-ttu-id="090d4-259">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="090d4-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="090d4-260">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="090d4-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_203.png

