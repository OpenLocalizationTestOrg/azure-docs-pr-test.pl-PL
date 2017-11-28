---
title: 'Samouczek: Integracji Azure Active Directory z TOPdesk - publicznego | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i TOPdesk - publicznego."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0873299f-ce70-457b-addc-e57c5801275f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: ef0dd06157ecc3b33814590039f5cbae64e8c916
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---public"></a><span data-ttu-id="6bcaa-103">Samouczek: Integracji Azure Active Directory z TOPdesk - publicznego</span><span class="sxs-lookup"><span data-stu-id="6bcaa-103">Tutorial: Azure Active Directory integration with TOPdesk - Public</span></span>

<span data-ttu-id="6bcaa-104">Z tego samouczka, dowiesz się, jak toointegrate TOPdesk - publicznego w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6bcaa-104">In this tutorial, you learn how toointegrate TOPdesk - Public with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6bcaa-105">Integrowanie TOPdesk - publicznego z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="6bcaa-105">Integrating TOPdesk - Public with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6bcaa-106">Można kontrolować w usłudze Azure AD mającego dostęp tooTOPdesk - publicznego.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-106">You can control in Azure AD who has access tooTOPdesk - Public.</span></span>
- <span data-ttu-id="6bcaa-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooTOPdesk — publiczny (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-107">You can enable your users tooautomatically get signed-on tooTOPdesk - Public (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="6bcaa-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="6bcaa-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6bcaa-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6bcaa-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6bcaa-110">Prerequisites</span></span>

<span data-ttu-id="6bcaa-111">tooconfigure integracji usługi Azure AD z TOPdesk - publiczny, należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="6bcaa-111">tooconfigure Azure AD integration with TOPdesk - Public, you need hello following items:</span></span>

- <span data-ttu-id="6bcaa-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6bcaa-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6bcaa-113">TOPdesk — publiczny jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="6bcaa-113">A TOPdesk - Public single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6bcaa-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6bcaa-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="6bcaa-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6bcaa-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6bcaa-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6bcaa-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6bcaa-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="6bcaa-118">Scenario description</span></span>
<span data-ttu-id="6bcaa-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6bcaa-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="6bcaa-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6bcaa-121">Dodawanie TOPdesk - publicznego z galerii hello</span><span class="sxs-lookup"><span data-stu-id="6bcaa-121">Adding TOPdesk - Public from hello gallery</span></span>
2. <span data-ttu-id="6bcaa-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="6bcaa-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-topdesk---public-from-hello-gallery"></a><span data-ttu-id="6bcaa-123">Dodawanie TOPdesk - publicznego z galerii hello</span><span class="sxs-lookup"><span data-stu-id="6bcaa-123">Adding TOPdesk - Public from hello gallery</span></span>
<span data-ttu-id="6bcaa-124">Integracja hello tooconfigure TOPdesk - publicznych do usługi Azure AD, należy tooadd TOPdesk - publicznego z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-124">tooconfigure hello integration of TOPdesk - Public into Azure AD, you need tooadd TOPdesk - Public from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6bcaa-125">**tooadd TOPdesk - publicznego z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="6bcaa-125">**tooadd TOPdesk - Public from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6bcaa-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="6bcaa-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6bcaa-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-129">Then go too**All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. <span data-ttu-id="6bcaa-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nowy przycisk aplikacji Hello][3]

4. <span data-ttu-id="6bcaa-133">W hello wyszukiwania wpisz **TOPdesk - publicznego**, wybierz pozycję **TOPdesk - publicznego** z panelu wyników kliknięcie **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-133">In hello search box, type **TOPdesk - Public**, select **TOPdesk - Public** from result panel then click **Add** button tooadd hello application.</span></span>

    ![TOPdesk - publicznego hello listy wyników](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="6bcaa-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="6bcaa-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="6bcaa-136">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z TOPdesk — publiczny w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-136">In this section, you configure and test Azure AD single sign-on with TOPdesk - Public based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6bcaa-137">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD wymaga tooknow użytkownika odpowiednikiem hello w TOPdesk — publiczny jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TOPdesk - Public is tooa user in Azure AD.</span></span> <span data-ttu-id="6bcaa-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w TOPdesk - publicznego musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-138">In other words, a link relationship between an Azure AD user and hello related user in TOPdesk - Public needs toobe established.</span></span>

<span data-ttu-id="6bcaa-139">W TOPdesk - publiczny, przypisz wartości hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-139">In TOPdesk - Public, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6bcaa-140">tooconfigure i testowanie usługi Azure AD rejestracji jednokrotnej z TOPdesk — publiczny, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="6bcaa-140">tooconfigure and test Azure AD single sign-on with TOPdesk - Public, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6bcaa-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6bcaa-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6bcaa-143">**[Utwórz TOPdesk - użytkownika testowego publicznego](#create-a-topdesk---public-test-user)**  - toohave odpowiednikiem Simona Britta w TOPdesk - publicznego, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-143">**[Create a TOPdesk - Public test user](#create-a-topdesk---public-test-user)** - toohave a counterpart of Britta Simon in TOPdesk - Public that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6bcaa-144">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6bcaa-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="6bcaa-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="6bcaa-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="6bcaa-147">W tej sekcji włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w sieci TOPdesk - publicznych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TOPdesk - Public application.</span></span>

<span data-ttu-id="6bcaa-148">**tooconfigure usługi Azure AD rejestracji jednokrotnej z TOPdesk - publiczny, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="6bcaa-148">**tooconfigure Azure AD single sign-on with TOPdesk - Public, perform hello following steps:**</span></span>

1. <span data-ttu-id="6bcaa-149">W portalu Azure na powitania hello **TOPdesk - publicznego** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-149">In hello Azure portal, on hello **TOPdesk - Public** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="6bcaa-151">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_samlbase.png)

3. <span data-ttu-id="6bcaa-153">Na powitania **TOPdesk - domeny publicznej i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="6bcaa-153">On hello **TOPdesk - Public Domain and URLs** section, perform hello following steps:</span></span>

    ![TOPdesk - domeny publicznej i adresów URL jednym informacje logowania jednokrotnego](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_url.png)

    <span data-ttu-id="6bcaa-155">a.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-155">a.</span></span> <span data-ttu-id="6bcaa-156">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.topdesk.net`</span><span class="sxs-lookup"><span data-stu-id="6bcaa-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.topdesk.net`</span></span>
    
    <span data-ttu-id="6bcaa-157">b.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-157">b.</span></span> <span data-ttu-id="6bcaa-158">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.topdesk.net/tas/public/login/verify`</span><span class="sxs-lookup"><span data-stu-id="6bcaa-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.topdesk.net/tas/public/login/verify`</span></span>

    <span data-ttu-id="6bcaa-159">c.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-159">c.</span></span> <span data-ttu-id="6bcaa-160">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.topdesk.net/tas/public/login/saml`</span><span class="sxs-lookup"><span data-stu-id="6bcaa-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.topdesk.net/tas/public/login/saml`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="6bcaa-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-161">These values are not real.</span></span> <span data-ttu-id="6bcaa-162">Zaktualizować te wartości z hello rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-162">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="6bcaa-163">Adres URL odpowiedzi jest explaned później w samouczku.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-163">Reply URL is explaned later in tutorial.</span></span> <span data-ttu-id="6bcaa-164">Skontaktuj się z [TOPdesk - zespołem pomocy technicznej klienta publicznego](https://help.topdesk.com/saas/enterprise/user/) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-164">Contact [TOPdesk - Public Client support team](https://help.topdesk.com/saas/enterprise/user/) tooget these values.</span></span>  

4. <span data-ttu-id="6bcaa-165">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_certificate.png) 

5. <span data-ttu-id="6bcaa-167">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-167">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="6bcaa-169">Na powitania **TOPdesk - publicznej konfiguracji** kliknij **skonfigurować TOPdesk - publicznego** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-169">On hello **TOPdesk - Public Configuration** section, click **Configure TOPdesk - Public** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="6bcaa-170">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="6bcaa-170">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![TOPdesk - publicznej konfiguracji](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_configure.png) 

7. <span data-ttu-id="6bcaa-172">Zaloguj się na tooyour **TOPdesk - publicznego** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-172">Sign on tooyour **TOPdesk - Public** company site as an administrator.</span></span>

8. <span data-ttu-id="6bcaa-173">W hello **TOPdesk** menu, kliknij przycisk **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-173">In hello **TOPdesk** menu, click **Settings**.</span></span>
   
    <span data-ttu-id="6bcaa-174">![Ustawienia](./media/active-directory-saas-topdesk-public-tutorial/ic790598.png "ustawienia")</span><span class="sxs-lookup"><span data-stu-id="6bcaa-174">![Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790598.png "Settings")</span></span>

9. <span data-ttu-id="6bcaa-175">Kliknij przycisk **ustawienia logowania**.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-175">Click **Login Settings**.</span></span>
   
    <span data-ttu-id="6bcaa-176">![Ustawienia logowania](./media/active-directory-saas-topdesk-public-tutorial/ic790599.png "ustawienia logowania")</span><span class="sxs-lookup"><span data-stu-id="6bcaa-176">![Login Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790599.png "Login Settings")</span></span>

10. <span data-ttu-id="6bcaa-177">Rozwiń węzeł hello **ustawienia logowania** menu, a następnie kliknij przycisk **ogólne**.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-177">Expand hello **Login Settings** menu, and then click **General**.</span></span>
   
    <span data-ttu-id="6bcaa-178">![Ogólne](./media/active-directory-saas-topdesk-public-tutorial/ic790600.png "ogólne")</span><span class="sxs-lookup"><span data-stu-id="6bcaa-178">![General](./media/active-directory-saas-topdesk-public-tutorial/ic790600.png "General")</span></span>

11. <span data-ttu-id="6bcaa-179">W hello **publicznego** sekcji hello **logowania SAML** konfiguracji sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="6bcaa-179">In hello **Public** section of hello **SAML login** configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="6bcaa-180">![Ustawienia techniczne](./media/active-directory-saas-topdesk-public-tutorial/ic790601.png "ustawienia techniczne")</span><span class="sxs-lookup"><span data-stu-id="6bcaa-180">![Technical Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790601.png "Technical Settings")</span></span>
   
    <span data-ttu-id="6bcaa-181">a.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-181">a.</span></span> <span data-ttu-id="6bcaa-182">Kliknij przycisk **Pobierz** toodownload hello pliku metadanych publicznego, a następnie zapisz go lokalnie na komputerze.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-182">Click **Download** toodownload hello public metadata file, and then save it locally on your computer.</span></span>
   
    <span data-ttu-id="6bcaa-183">b.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-183">b.</span></span> <span data-ttu-id="6bcaa-184">Otwórz plik metadanych hello pobrana, a następnie zlokalizuj hello **AssertionConsumerService** węzła.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-184">Open hello downloaded metadata file, and then locate hello **AssertionConsumerService** node.</span></span>

    <span data-ttu-id="6bcaa-185">![AssertionConsumerService](./media/active-directory-saas-topdesk-public-tutorial/ic790619.png "AssertionConsumerService")</span><span class="sxs-lookup"><span data-stu-id="6bcaa-185">![AssertionConsumerService](./media/active-directory-saas-topdesk-public-tutorial/ic790619.png "AssertionConsumerService")</span></span>
   
    <span data-ttu-id="6bcaa-186">c.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-186">c.</span></span> <span data-ttu-id="6bcaa-187">Hello kopiowania **AssertionConsumerService** wartość, wklej tę wartość w hello **adres URL odpowiedzi** textbox w **TOPdesk - domeny publicznej i adres URL** sekcji.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-187">Copy hello **AssertionConsumerService** value, paste this value in hello **Reply URL** textbox in **TOPdesk - Public Domain and URLs** section.</span></span>      
   
12. <span data-ttu-id="6bcaa-188">toocreate plik certyfikatu, należy wykonać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="6bcaa-188">toocreate a certificate file, perform hello following steps:</span></span>
    
    <span data-ttu-id="6bcaa-189">![Certyfikat](./media/active-directory-saas-topdesk-public-tutorial/ic790606.png "certyfikatu")</span><span class="sxs-lookup"><span data-stu-id="6bcaa-189">![Certificate](./media/active-directory-saas-topdesk-public-tutorial/ic790606.png "Certificate")</span></span>
    
    <span data-ttu-id="6bcaa-190">a.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-190">a.</span></span> <span data-ttu-id="6bcaa-191">Otwórz hello pobrany plik metadanych z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-191">Open hello downloaded metadata file from Azure portal.</span></span>
    
    <span data-ttu-id="6bcaa-192">b.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-192">b.</span></span> <span data-ttu-id="6bcaa-193">Rozwiń węzeł hello **RoleDescriptor** węzła, który ma **xsi: type** z **przekazywani: ApplicationServiceType**.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-193">Expand hello **RoleDescriptor** node that has a **xsi:type** of **fed:ApplicationServiceType**.</span></span>
    
    <span data-ttu-id="6bcaa-194">c.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-194">c.</span></span> <span data-ttu-id="6bcaa-195">Skopiuj wartość hello hello **X509Certificate** węzła.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-195">Copy hello value of hello **X509Certificate** node.</span></span>
    
    <span data-ttu-id="6bcaa-196">d.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-196">d.</span></span> <span data-ttu-id="6bcaa-197">Zapisz hello skopiowane **X509Certificate** wartość lokalnie na komputerze w pliku.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-197">Save hello copied **X509Certificate** value locally on your computer in a file.</span></span>

13. <span data-ttu-id="6bcaa-198">W hello **publicznego** kliknij **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-198">In hello **Public** section, click **Add**.</span></span>
    
    <span data-ttu-id="6bcaa-199">![Logowania SAML](./media/active-directory-saas-topdesk-public-tutorial/ic790625.png "logowania SAML")</span><span class="sxs-lookup"><span data-stu-id="6bcaa-199">![SAML Login](./media/active-directory-saas-topdesk-public-tutorial/ic790625.png "SAML Login")</span></span>

14. <span data-ttu-id="6bcaa-200">Na powitania **Asystenta konfiguracji SAML** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="6bcaa-200">On hello **SAML configuration assistant** dialog page, perform hello following steps:</span></span>
    
    <span data-ttu-id="6bcaa-201">![Asystent konfiguracji SAML](./media/active-directory-saas-topdesk-public-tutorial/ic790608.png "Asystenta konfiguracji SAML")</span><span class="sxs-lookup"><span data-stu-id="6bcaa-201">![SAML Configuration Assistant](./media/active-directory-saas-topdesk-public-tutorial/ic790608.png "SAML Configuration Assistant")</span></span>
    
    <span data-ttu-id="6bcaa-202">a.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-202">a.</span></span> <span data-ttu-id="6bcaa-203">tooupload metadanych pobranych plików z portalu Azure, w obszarze **metadanych Federacji**, kliknij przycisk **Przeglądaj**.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-203">tooupload your downloaded metadata file from Azure portal, under **Federation Metadata**, click **Browse**.</span></span>

    <span data-ttu-id="6bcaa-204">b.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-204">b.</span></span> <span data-ttu-id="6bcaa-205">tooupload pliku certyfikatu, w obszarze **certyfikatu (RSA)**, kliknij przycisk **Przeglądaj**.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-205">tooupload your certificate file, under **Certificate (RSA)**, click **Browse**.</span></span>

    <span data-ttu-id="6bcaa-206">c.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-206">c.</span></span> <span data-ttu-id="6bcaa-207">plik z logo hello tooupload uzyskano z zespołem pomocy technicznej TOPdesk hello, w obszarze **ikona Logo**, kliknij przycisk **Przeglądaj**.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-207">tooupload hello logo file you got from hello TOPdesk support team, under **Logo icon**, click **Browse**.</span></span>

    <span data-ttu-id="6bcaa-208">d.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-208">d.</span></span> <span data-ttu-id="6bcaa-209">W hello **atrybutu nazwy użytkownika** pole tekstowe, typ `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-209">In hello **User name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="6bcaa-210">e.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-210">e.</span></span> <span data-ttu-id="6bcaa-211">W hello **Nazwa wyświetlana** tekstowym, wpisz nazwę dla danej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-211">In hello **Display name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="6bcaa-212">f.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-212">f.</span></span> <span data-ttu-id="6bcaa-213">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-213">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="6bcaa-214">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="6bcaa-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6bcaa-215">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6bcaa-216">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6bcaa-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="6bcaa-217">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6bcaa-217">Create an Azure AD test user</span></span>

<span data-ttu-id="6bcaa-218">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="6bcaa-220">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="6bcaa-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6bcaa-221">W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-221">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="6bcaa-223">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-223">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="6bcaa-225">Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-225">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![przycisk Dodaj Hello](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="6bcaa-227">W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="6bcaa-227">In hello **User** dialog box, perform hello following steps:</span></span>

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_04.png)

    <span data-ttu-id="6bcaa-229">a.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-229">a.</span></span> <span data-ttu-id="6bcaa-230">W hello **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-230">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6bcaa-231">b.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-231">b.</span></span> <span data-ttu-id="6bcaa-232">W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-232">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="6bcaa-233">c.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-233">c.</span></span> <span data-ttu-id="6bcaa-234">Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-234">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="6bcaa-235">d.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-235">d.</span></span> <span data-ttu-id="6bcaa-236">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-236">Click **Create**.</span></span>
 
### <a name="create-a-topdesk---public-test-user"></a><span data-ttu-id="6bcaa-237">Utwórz TOPdesk - użytkownika testowego publiczny</span><span class="sxs-lookup"><span data-stu-id="6bcaa-237">Create a TOPdesk - Public test user</span></span>

<span data-ttu-id="6bcaa-238">W kolejności tooenable usługi Azure AD użytkownicy toolog do TOPdesk - publiczny, muszą mieć przydzielone do TOPdesk - publicznego.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-238">In order tooenable Azure AD users toolog into TOPdesk - Public, they must be provisioned into TOPdesk - Public.</span></span>  
<span data-ttu-id="6bcaa-239">W przypadku hello TOPdesk - publiczny, inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-239">In hello case of TOPdesk - Public, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="6bcaa-240">tooconfigure aprowizacji użytkowników, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="6bcaa-240">tooconfigure user provisioning, perform hello following steps:</span></span>
1. <span data-ttu-id="6bcaa-241">Zaloguj się na tooyour **TOPdesk - publicznego** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-241">Sign on tooyour **TOPdesk - Public** company site as administrator.</span></span>

2. <span data-ttu-id="6bcaa-242">W menu hello na górze hello, kliknij przycisk **TOPdesk \> nowy \> pliki obsługi \> osoby**.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-242">In hello menu on hello top, click **TOPdesk \> New \> Support Files \> Person**.</span></span>
   
    <span data-ttu-id="6bcaa-243">![Osoba](./media/active-directory-saas-topdesk-public-tutorial/ic790628.png "osoby")</span><span class="sxs-lookup"><span data-stu-id="6bcaa-243">![Person](./media/active-directory-saas-topdesk-public-tutorial/ic790628.png "Person")</span></span>

3. <span data-ttu-id="6bcaa-244">W oknie dialogowym nowej osoby hello wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="6bcaa-244">On hello New Person dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="6bcaa-245">![Nowej osoby](./media/active-directory-saas-topdesk-public-tutorial/ic790629.png "nowej osoby")</span><span class="sxs-lookup"><span data-stu-id="6bcaa-245">![New Person](./media/active-directory-saas-topdesk-public-tutorial/ic790629.png "New Person")</span></span>
   
    <span data-ttu-id="6bcaa-246">a.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-246">a.</span></span> <span data-ttu-id="6bcaa-247">Kliknij kartę Ogólne hello.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-247">Click hello General tab.</span></span>

    <span data-ttu-id="6bcaa-248">b.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-248">b.</span></span> <span data-ttu-id="6bcaa-249">W hello **nazwisko** tekstowym, wpisz nazwisko użytkownika hello, takich jak Simona</span><span class="sxs-lookup"><span data-stu-id="6bcaa-249">In hello **Surname** textbox, type Surname of hello user like Simon</span></span>
 
    <span data-ttu-id="6bcaa-250">c.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-250">c.</span></span> <span data-ttu-id="6bcaa-251">Wybierz **lokacji** hello konta.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-251">Select a **Site** for hello account.</span></span>
 
    <span data-ttu-id="6bcaa-252">d.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-252">d.</span></span> <span data-ttu-id="6bcaa-253">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-253">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="6bcaa-254">Można użyć innych TOPdesk — narzędzia do tworzenia konta użytkownika publiczny lub interfejsów API dostarczonych przez TOPdesk - kont użytkowników tooprovision publicznej usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-254">You can use any other TOPdesk - Public user account creation tools or APIs provided by TOPdesk - Public tooprovision Azure AD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="6bcaa-255">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="6bcaa-255">Assign hello Azure AD test user</span></span>

<span data-ttu-id="6bcaa-256">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooTOPdesk - publicznego.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-256">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTOPdesk - Public.</span></span>

![Przypisanie roli użytkownika hello][200] 

<span data-ttu-id="6bcaa-258">**tooassign tooTOPdesk Simona Britta - publiczny, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="6bcaa-258">**tooassign Britta Simon tooTOPdesk - Public, perform hello following steps:**</span></span>

1. <span data-ttu-id="6bcaa-259">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-259">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="6bcaa-261">Z listy aplikacji hello wybierz **TOPdesk - publicznego**.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-261">In hello applications list, select **TOPdesk - Public**.</span></span>

    ![Witaj TOPdesk - publicznego łącze w listę aplikacji hello](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_app.png)  

3. <span data-ttu-id="6bcaa-263">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-263">In hello menu on hello left, click **Users and groups**.</span></span>

    ![łącze "Użytkownicy i grupy" Hello][202]

4. <span data-ttu-id="6bcaa-265">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-265">Click **Add** button.</span></span> <span data-ttu-id="6bcaa-266">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-266">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Okienko Dodaj przypisania Hello][203]

5. <span data-ttu-id="6bcaa-268">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-268">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6bcaa-269">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-269">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6bcaa-270">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-270">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="6bcaa-271">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="6bcaa-271">Test single sign-on</span></span>

<span data-ttu-id="6bcaa-272">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-272">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6bcaa-273">Po kliknięciu hello TOPdesk - publicznego kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour TOPdesk - publicznych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6bcaa-273">When you click hello TOPdesk - Public tile in hello Access Panel, you should get automatically signed-on tooyour TOPdesk - Public application.</span></span>
<span data-ttu-id="6bcaa-274">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6bcaa-274">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6bcaa-275">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="6bcaa-275">Additional resources</span></span>

* [<span data-ttu-id="6bcaa-276">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6bcaa-276">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6bcaa-277">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6bcaa-277">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_203.png

