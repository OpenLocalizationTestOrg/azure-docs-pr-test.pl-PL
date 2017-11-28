---
title: "Samouczek: Integracji Azure Active Directory z MOVEit Transfer — integracji z usługą Azure AD | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i MOVEit Transfer — integracji z usługą Azure AD."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8ff7102d-be73-4888-ae81-d8e3d01dd534
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 5bbe4f2d952bd45c4d58d55ffc3467b4eb871fd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moveit-transfer---azure-ad-integration"></a><span data-ttu-id="05a78-103">Samouczek: Integracji Azure Active Directory z MOVEit Transfer — integracji z usługą Azure AD</span><span class="sxs-lookup"><span data-stu-id="05a78-103">Tutorial: Azure Active Directory integration with MOVEit Transfer - Azure AD integration</span></span>

<span data-ttu-id="05a78-104">Z tego samouczka, dowiesz się, jak toointegrate MOVEit Transfer — integracji z usługą Azure AD z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="05a78-104">In this tutorial, you learn how toointegrate MOVEit Transfer - Azure AD integration with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="05a78-105">Integrowanie MOVEit Transfer — integracji z usługą Azure AD z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="05a78-105">Integrating MOVEit Transfer - Azure AD integration with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="05a78-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooMOVEit Transfer — integracji z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05a78-106">You can control in Azure AD who has access tooMOVEit Transfer - Azure AD integration.</span></span>
- <span data-ttu-id="05a78-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooMOVEit Transfer — Integracja usługi Azure AD (logowanie jednokrotne) z konta usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05a78-107">You can enable your users tooautomatically get signed-on tooMOVEit Transfer - Azure AD integration (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="05a78-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="05a78-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="05a78-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="05a78-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05a78-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="05a78-110">Prerequisites</span></span>

<span data-ttu-id="05a78-111">tooconfigure integracji usługi Azure AD z MOVEit Transfer — integracji z usługą Azure AD, należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="05a78-111">tooconfigure Azure AD integration with MOVEit Transfer - Azure AD integration, you need hello following items:</span></span>

- <span data-ttu-id="05a78-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="05a78-112">An Azure AD subscription</span></span>
- <span data-ttu-id="05a78-113">MOVEit Transfer — usługi Azure AD integracji jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="05a78-113">A MOVEit Transfer - Azure AD integration single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="05a78-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="05a78-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="05a78-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="05a78-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="05a78-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="05a78-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="05a78-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="05a78-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="05a78-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="05a78-118">Scenario description</span></span>
<span data-ttu-id="05a78-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="05a78-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="05a78-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="05a78-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="05a78-121">Dodawanie MOVEit Transfer — integracji z usługą Azure AD z galerii hello</span><span class="sxs-lookup"><span data-stu-id="05a78-121">Adding MOVEit Transfer - Azure AD integration from hello gallery</span></span>
2. <span data-ttu-id="05a78-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="05a78-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-moveit-transfer---azure-ad-integration-from-hello-gallery"></a><span data-ttu-id="05a78-123">Dodawanie MOVEit Transfer — integracji z usługą Azure AD z galerii hello</span><span class="sxs-lookup"><span data-stu-id="05a78-123">Adding MOVEit Transfer - Azure AD integration from hello gallery</span></span>
<span data-ttu-id="05a78-124">Integracja hello tooconfigure transferu MOVEit - integracji usługi Azure AD do usługi Azure AD, należy tooadd MOVEit Transfer — integracji usługi Azure AD z listy tooyour galerii hello zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="05a78-124">tooconfigure hello integration of MOVEit Transfer - Azure AD integration into Azure AD, you need tooadd MOVEit Transfer - Azure AD integration from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="05a78-125">**tooadd MOVEit Transfer — integracji z usługą Azure AD z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="05a78-125">**tooadd MOVEit Transfer - Azure AD integration from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="05a78-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="05a78-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="05a78-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="05a78-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="05a78-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="05a78-129">Then go too**All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. <span data-ttu-id="05a78-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="05a78-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nowy przycisk aplikacji Hello][3]

4. <span data-ttu-id="05a78-133">W polu wyszukiwania hello wpisz **MOVEit Transfer — integracji z usługą Azure AD**, wybierz pozycję **MOVEit Transfer — integracji z usługą Azure AD** z panelu wyników następnie kliknij przycisk **Dodaj** hello tooadd przycisk aplikacja.</span><span class="sxs-lookup"><span data-stu-id="05a78-133">In hello search box, type **MOVEit Transfer - Azure AD integration**, select **MOVEit Transfer - Azure AD integration** from result panel then click **Add** button tooadd hello application.</span></span>

    ![MOVEit Transfer — integracji usługi Azure AD hello listy wyników](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="05a78-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="05a78-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="05a78-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z MOVEit Transfer — integracji z usługą Azure AD w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="05a78-136">In this section, you configure and test Azure AD single sign-on with MOVEit Transfer - Azure AD integration based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="05a78-137">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD wymaga tooknow użytkownika odpowiednikiem hello transferu MOVEit — integracji z usługą Azure AD jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05a78-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in MOVEit Transfer - Azure AD integration is tooa user in Azure AD.</span></span> <span data-ttu-id="05a78-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w MOVEit Transfer — integracji z usługą Azure AD musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="05a78-138">In other words, a link relationship between an Azure AD user and hello related user in MOVEit Transfer - Azure AD integration needs toobe established.</span></span>

<span data-ttu-id="05a78-139">W MOVEit Transfer — integracji z usługą Azure AD, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="05a78-139">In MOVEit Transfer - Azure AD integration, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="05a78-140">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z MOVEit Transfer — integracji z usługą Azure AD, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="05a78-140">tooconfigure and test Azure AD single sign-on with MOVEit Transfer - Azure AD integration, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="05a78-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="05a78-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="05a78-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="05a78-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="05a78-143">**[Tworzenie przeniesienia MOVEit - użytkownika testowego integracji usługi Azure AD](#create-a-moveit-transfer---azure-ad-integration-test-user)**  - toohave odpowiednikiem Simona Britta transferu MOVEit - integracji usługi Azure AD z toohello połączonej usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="05a78-143">**[Create a MOVEit Transfer - Azure AD integration test user](#create-a-moveit-transfer---azure-ad-integration-test-user)** - toohave a counterpart of Britta Simon in MOVEit Transfer - Azure AD integration that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="05a78-144">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="05a78-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="05a78-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="05a78-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="05a78-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="05a78-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="05a78-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w transferu MOVEit - aplikacji integracji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05a78-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your MOVEit Transfer - Azure AD integration application.</span></span>

<span data-ttu-id="05a78-148">**tooconfigure usługi Azure AD rejestracji jednokrotnej z MOVEit Transfer — integracji z usługą Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="05a78-148">**tooconfigure Azure AD single sign-on with MOVEit Transfer - Azure AD integration, perform hello following steps:**</span></span>

1. <span data-ttu-id="05a78-149">W portalu Azure na powitania hello **MOVEit Transfer — integracji z usługą Azure AD** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="05a78-149">In hello Azure portal, on hello **MOVEit Transfer - Azure AD integration** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="05a78-151">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="05a78-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_samlbase.png)

3. <span data-ttu-id="05a78-153">Na powitania **MOVEit Transfer — adresy URL i integracji z usługą Azure AD domeny** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="05a78-153">On hello **MOVEit Transfer - Azure AD integration Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_url.png)

    <span data-ttu-id="05a78-155">a.</span><span class="sxs-lookup"><span data-stu-id="05a78-155">a.</span></span> <span data-ttu-id="05a78-156">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://contoso.com`</span><span class="sxs-lookup"><span data-stu-id="05a78-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://contoso.com`</span></span>

    <span data-ttu-id="05a78-157">b.</span><span class="sxs-lookup"><span data-stu-id="05a78-157">b.</span></span> <span data-ttu-id="05a78-158">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://contoso.com/<tenatid>`</span><span class="sxs-lookup"><span data-stu-id="05a78-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://contoso.com/<tenatid>`</span></span>

    <span data-ttu-id="05a78-159">c.</span><span class="sxs-lookup"><span data-stu-id="05a78-159">c.</span></span> <span data-ttu-id="05a78-160">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`</span><span class="sxs-lookup"><span data-stu-id="05a78-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`</span></span>    
     
    > [!NOTE] 
    > <span data-ttu-id="05a78-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="05a78-161">These values are not real.</span></span> <span data-ttu-id="05a78-162">Zaktualizować te wartości z hello rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="05a78-162">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="05a78-163">Może się odwoływać te wartości później w **adres URL metadanych dostawcy usługi** sekcji lub skontaktuj się z [MOVEit Transfer — zespołem pomocy technicznej klienta integracji usługi Azure AD](https://community.ipswitch.com/s/support) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="05a78-163">You can refer these values later in **Service Provider Metadata URL** section or contact [MOVEit Transfer - Azure AD integration Client support team](https://community.ipswitch.com/s/support) tooget these values.</span></span>

4. <span data-ttu-id="05a78-164">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="05a78-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_certificate.png) 

5. <span data-ttu-id="05a78-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="05a78-166">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="05a78-168">Zaloguj się na tooyour MOVEit Transfer dzierżawy z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="05a78-168">Sign on tooyour MOVEit Transfer tenant as an administrator.</span></span>

7. <span data-ttu-id="05a78-169">W okienku nawigacji po lewej stronie powitania kliknij **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="05a78-169">On hello left navigation pane, click **Settings**.</span></span>

    ![Strona aplikacji w sekcji Ustawienia](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_000.png)

8. <span data-ttu-id="05a78-171">Kliknij przycisk **pojedynczego logować** łącza, która znajduje się w **zasad zabezpieczeń -> uwierzytelniania użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="05a78-171">Click **Single Signon** link, which is under **Security Policies -> User Auth**.</span></span>

    ![Strony aplikacji na zasady zabezpieczeń](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_001.png)

9. <span data-ttu-id="05a78-173">Kliknij przycisk hello adres URL metadanych łącze toodownload hello metadanych dokumentu.</span><span class="sxs-lookup"><span data-stu-id="05a78-173">Click hello Metadata URL link toodownload hello metadata document.</span></span>

    ![Adres URL metadanych dostawcy usługi](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_002.png)
    
    * <span data-ttu-id="05a78-175">Sprawdź **entityID** odpowiada **identyfikator** w hello **MOVEit Transfer — integracji z usługą Azure AD domeny i adres URL** sekcji.</span><span class="sxs-lookup"><span data-stu-id="05a78-175">Verify **entityID** matches **Identifier** in hello **MOVEit Transfer - Azure AD integration Domain and URLs** section .</span></span>
    * <span data-ttu-id="05a78-176">Sprawdź **AssertionConsumerService** odpowiada adresu URL lokalizacji **adres URL odpowiedzi** w hello **MOVEit Transfer — adresy URL i integracji z usługą Azure AD domeny** sekcji.</span><span class="sxs-lookup"><span data-stu-id="05a78-176">Verify **AssertionConsumerService** Location URL matches **REPLY URL** in hello **MOVEit Transfer - Azure AD integration Domain and URLs** section.</span></span>
    
    ![Konfigurowanie jednej logowania w aplikacji po stronie](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_007.png)

10. <span data-ttu-id="05a78-178">Kliknij przycisk **Dodawanie dostawcy tożsamości** przycisk tooadd nowego dostawcę tożsamości federacyjnych.</span><span class="sxs-lookup"><span data-stu-id="05a78-178">Click **Add Identity Provider** button tooadd a new Federated Identity Provider.</span></span>

    ![Dodaj dostawcę tożsamości](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_003.png)

11. <span data-ttu-id="05a78-180">Kliknij przycisk **Przeglądaj...**  tooselect hello pliku metadanych, który został pobrany z portalu Azure, a następnie kliknij przycisk **Dodawanie dostawcy tożsamości** tooupload hello pobrany plik.</span><span class="sxs-lookup"><span data-stu-id="05a78-180">Click **Browse...** tooselect hello metadata file which you downloaded from Azure portal, then click **Add Identity Provider** tooupload hello downloaded file.</span></span>

    ![Dostawca tożsamości SAML](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_004.png)

12. <span data-ttu-id="05a78-182">Wybierz opcję "**tak**" jako **włączone** w hello **Edycja ustawień tożsamości federacyjnych dostawca...**  i kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="05a78-182">Select "**Yes**" as **Enabled** in hello **Edit Federated Identity Provider Settings...** page and click **Save**.</span></span>

    ![Ustawienia dostawcy tożsamości federacyjnych](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_005.png)

13. <span data-ttu-id="05a78-184">W hello **Edycja ustawień tożsamości federacyjnych dostawca użytkownika** wykonaj hello następujące akcje:</span><span class="sxs-lookup"><span data-stu-id="05a78-184">In hello **Edit Federated Identity Provider User Settings** page, perform hello following actions:</span></span>
    
    ![Edytuj ustawienia dostawcy tożsamości federacyjnych](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_006.png)
    
    <span data-ttu-id="05a78-186">a.</span><span class="sxs-lookup"><span data-stu-id="05a78-186">a.</span></span> <span data-ttu-id="05a78-187">Wybierz **SAML NameID** jako **nazwa logowania**.</span><span class="sxs-lookup"><span data-stu-id="05a78-187">Select **SAML NameID** as **Login name**.</span></span>
    
    <span data-ttu-id="05a78-188">b.</span><span class="sxs-lookup"><span data-stu-id="05a78-188">b.</span></span> <span data-ttu-id="05a78-189">Wybierz **innych** jako **imię i nazwisko** w hello **nazwa atrybutu** pole tekstowe umieścić wartość hello: `http://schemas.microsoft.com/identity/claims/displayname`.</span><span class="sxs-lookup"><span data-stu-id="05a78-189">Select **Other** as **Full name** and in hello **Attribute name** textbox put hello value: `http://schemas.microsoft.com/identity/claims/displayname`.</span></span>
    
    <span data-ttu-id="05a78-190">c.</span><span class="sxs-lookup"><span data-stu-id="05a78-190">c.</span></span> <span data-ttu-id="05a78-191">Wybierz **innych** jako **E-mail** w hello **nazwa atrybutu** pole tekstowe umieścić wartość hello: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="05a78-191">Select **Other** as **Email** and in hello **Attribute name** textbox put hello value: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
    
    <span data-ttu-id="05a78-192">d.</span><span class="sxs-lookup"><span data-stu-id="05a78-192">d.</span></span> <span data-ttu-id="05a78-193">Wybierz **tak** jako **automatyczne tworzenie konta logowaniu**.</span><span class="sxs-lookup"><span data-stu-id="05a78-193">Select **Yes** as **Auto-create account on signon**.</span></span>
    
    <span data-ttu-id="05a78-194">e.</span><span class="sxs-lookup"><span data-stu-id="05a78-194">e.</span></span> <span data-ttu-id="05a78-195">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="05a78-195">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="05a78-196">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="05a78-196">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="05a78-197">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="05a78-197">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="05a78-198">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="05a78-198">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="05a78-199">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="05a78-199">Create an Azure AD test user</span></span>

<span data-ttu-id="05a78-200">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="05a78-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="05a78-202">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="05a78-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="05a78-203">W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="05a78-203">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="05a78-205">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="05a78-205">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="05a78-207">Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="05a78-207">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![przycisk Dodaj Hello](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="05a78-209">W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="05a78-209">In hello **User** dialog box, perform hello following steps:</span></span>

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_04.png)

    <span data-ttu-id="05a78-211">a.</span><span class="sxs-lookup"><span data-stu-id="05a78-211">a.</span></span> <span data-ttu-id="05a78-212">W hello **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="05a78-212">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="05a78-213">b.</span><span class="sxs-lookup"><span data-stu-id="05a78-213">b.</span></span> <span data-ttu-id="05a78-214">W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="05a78-214">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="05a78-215">c.</span><span class="sxs-lookup"><span data-stu-id="05a78-215">c.</span></span> <span data-ttu-id="05a78-216">Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="05a78-216">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="05a78-217">d.</span><span class="sxs-lookup"><span data-stu-id="05a78-217">d.</span></span> <span data-ttu-id="05a78-218">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="05a78-218">Click **Create**.</span></span>
 
### <a name="create-a-moveit-transfer---azure-ad-integration-test-user"></a><span data-ttu-id="05a78-219">Tworzenie przeniesienia MOVEit - użytkownika testowego integracji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="05a78-219">Create a MOVEit Transfer - Azure AD integration test user</span></span>

<span data-ttu-id="05a78-220">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w MOVEit Transfer — integracji z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05a78-220">hello objective of this section is toocreate a user called Britta Simon in MOVEit Transfer - Azure AD integration.</span></span> <span data-ttu-id="05a78-221">MOVEit Transfer — integracji z usługą Azure AD obsługę just in time, które zostało włączone.</span><span class="sxs-lookup"><span data-stu-id="05a78-221">MOVEit Transfer - Azure AD integration supports just-in-time provisioning, which you have enabled.</span></span> <span data-ttu-id="05a78-222">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="05a78-222">There is no action item for you in this section.</span></span> <span data-ttu-id="05a78-223">Nowy użytkownik został utworzony podczas próby tooaccess MOVEit Transfer — integracji usługi Azure AD, jeśli go jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="05a78-223">A new user is created during an attempt tooaccess MOVEit Transfer - Azure AD integration if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="05a78-224">Jeśli potrzebujesz ręcznie toocreate użytkownika, należy toocontact hello [MOVEit Transfer — zespołem pomocy technicznej klienta integracji usługi Azure AD](https://community.ipswitch.com/s/support).</span><span class="sxs-lookup"><span data-stu-id="05a78-224">If you need toocreate a user manually, you need toocontact hello [MOVEit Transfer - Azure AD integration Client support team](https://community.ipswitch.com/s/support).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="05a78-225">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="05a78-225">Assign hello Azure AD test user</span></span>

<span data-ttu-id="05a78-226">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooMOVEit Transfer — integracji z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05a78-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMOVEit Transfer - Azure AD integration.</span></span>

![Przypisanie roli użytkownika hello][200] 

<span data-ttu-id="05a78-228">**tooassign tooMOVEit Simona Britta Transfer — integracji z usługą Azure AD, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="05a78-228">**tooassign Britta Simon tooMOVEit Transfer - Azure AD integration, perform hello following steps:**</span></span>

1. <span data-ttu-id="05a78-229">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="05a78-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="05a78-231">Z listy aplikacji hello wybierz **MOVEit Transfer — integracji z usługą Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="05a78-231">In hello applications list, select **MOVEit Transfer - Azure AD integration**.</span></span>

    ![Witaj MOVEit Transfer — integracji z usługą Azure AD łącza na liście aplikacji hello](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_app.png)  

3. <span data-ttu-id="05a78-233">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="05a78-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![łącze "Użytkownicy i grupy" Hello][202]

4. <span data-ttu-id="05a78-235">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="05a78-235">Click **Add** button.</span></span> <span data-ttu-id="05a78-236">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="05a78-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Okienko Dodaj przypisania Hello][203]

5. <span data-ttu-id="05a78-238">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="05a78-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="05a78-239">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="05a78-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="05a78-240">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="05a78-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="05a78-241">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="05a78-241">Test single sign-on</span></span>

<span data-ttu-id="05a78-242">Celem Hello w tej sekcji jest tootest programu Azure AD SSO konfiguracji przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="05a78-242">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="05a78-243">Po kliknięciu hello MOVEit Transfer — kafelka integracji usługi Azure AD w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour MOVEit Transfer — aplikacji integracji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05a78-243">When you click hello MOVEit Transfer - Azure AD integration tile in hello Access Panel, you should get automatically signed-on tooyour MOVEit Transfer - Azure AD integration application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="05a78-244">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="05a78-244">Additional resources</span></span>

* [<span data-ttu-id="05a78-245">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="05a78-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="05a78-246">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="05a78-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_203.png

