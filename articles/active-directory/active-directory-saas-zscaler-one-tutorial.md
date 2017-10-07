---
title: 'Samouczek: Azure Active Directory integracji z jednego Zscaler | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Zscaler jeden."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f352e00d-68d3-4a77-bb92-717d055da56f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 5179cb2cc54482334d574951a1ac64e722e5f578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-one"></a><span data-ttu-id="5f433-103">Samouczek: Azure Active Directory integracji z jednego Zscaler</span><span class="sxs-lookup"><span data-stu-id="5f433-103">Tutorial: Azure Active Directory integration with Zscaler One</span></span>

<span data-ttu-id="5f433-104">Z tego samouczka, dowiesz się, jak toointegrate Zscaler jednego z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5f433-104">In this tutorial, you learn how toointegrate Zscaler One with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5f433-105">Integrowanie Zscaler jednego z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="5f433-105">Integrating Zscaler One with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5f433-106">Można kontrolować w usłudze Azure AD, kto ma dostęp tooZscaler, jeden</span><span class="sxs-lookup"><span data-stu-id="5f433-106">You can control in Azure AD who has access tooZscaler One</span></span>
- <span data-ttu-id="5f433-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooZscaler jedną (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5f433-107">You can enable your users tooautomatically get signed-on tooZscaler One (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5f433-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="5f433-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5f433-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5f433-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5f433-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5f433-110">Prerequisites</span></span>

<span data-ttu-id="5f433-111">tooconfigure integracji usługi Azure AD z jednym Zscaler należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="5f433-111">tooconfigure Azure AD integration with Zscaler One, you need hello following items:</span></span>

- <span data-ttu-id="5f433-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5f433-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5f433-113">Jeden Zscaler logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="5f433-113">A Zscaler One single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5f433-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="5f433-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5f433-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="5f433-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5f433-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="5f433-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5f433-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna tutaj: [oferta wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5f433-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5f433-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="5f433-118">Scenario description</span></span>
<span data-ttu-id="5f433-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="5f433-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5f433-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="5f433-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5f433-121">Dodawanie Zscaler jednego z galerii hello</span><span class="sxs-lookup"><span data-stu-id="5f433-121">Adding Zscaler One from hello gallery</span></span>
2. <span data-ttu-id="5f433-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="5f433-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-one-from-hello-gallery"></a><span data-ttu-id="5f433-123">Dodawanie Zscaler jednego z galerii hello</span><span class="sxs-lookup"><span data-stu-id="5f433-123">Adding Zscaler One from hello gallery</span></span>
<span data-ttu-id="5f433-124">tooconfigure hello integracji Zscaler co w usłudze Azure Active Directory, należy tooadd Zscaler jednego z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="5f433-124">tooconfigure hello integration of Zscaler One into Azure AD, you need tooadd Zscaler One from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5f433-125">**tooadd Zscaler jednego z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="5f433-125">**tooadd Zscaler One from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5f433-126">W hello ** [portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="5f433-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="5f433-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="5f433-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5f433-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="5f433-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="5f433-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5f433-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="5f433-133">W polu wyszukiwania hello wpisz **Zscaler jeden**.</span><span class="sxs-lookup"><span data-stu-id="5f433-133">In hello search box, type **Zscaler One**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_search.png)

5. <span data-ttu-id="5f433-135">W panelu wyników hello, wybierz **Zscaler jeden**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="5f433-135">In hello results panel, select **Zscaler One**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5f433-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="5f433-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5f433-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z jednego Zscaler w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="5f433-138">In this section, you configure and test Azure AD single sign-on with Zscaler One based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5f433-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow hello odpowiednikiem użytkownika w jednym Zscaler jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5f433-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zscaler One is tooa user in Azure AD.</span></span> <span data-ttu-id="5f433-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w jednym Zscaler musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="5f433-140">In other words, a link relationship between an Azure AD user and hello related user in Zscaler One needs toobe established.</span></span>

<span data-ttu-id="5f433-141">W jednej Zscaler przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="5f433-141">In Zscaler One, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5f433-142">tooconfigure i test usługi Azure AD rejestracji jednokrotnej z jednego Zscaler należy hello toocomplete po bloków konstrukcyjnych:</span><span class="sxs-lookup"><span data-stu-id="5f433-142">tooconfigure and test Azure AD single sign-on with Zscaler One, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5f433-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on) ** -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="5f433-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5f433-144">**[Konfigurowanie ustawień serwera proxy](#configuring-proxy-settings) ** — ustawienia serwera proxy hello tooconfigure w programie Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="5f433-144">**[Configuring proxy settings](#configuring-proxy-settings)** - tooconfigure hello proxy settings in Internet Explorer</span></span>
3. <span data-ttu-id="5f433-145">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user) ** -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="5f433-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="5f433-146">**[Tworzenie użytkownika testowego Zscaler jeden](#creating-a-zscaler-one-test-user) ** -toohave odpowiednikiem Simona Britta w Zscaler jeden będący toohello połączonej usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5f433-146">**[Creating a Zscaler One test user](#creating-a-zscaler-one-test-user)** - toohave a counterpart of Britta Simon in Zscaler One that is linked toohello Azure AD representation of user.</span></span>
5. <span data-ttu-id="5f433-147">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="5f433-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
6. <span data-ttu-id="5f433-148">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on) ** -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="5f433-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5f433-149">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5f433-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5f433-150">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne Zscaler jednej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5f433-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zscaler One application.</span></span>

<span data-ttu-id="5f433-151">**tooconfigure usługi Azure AD rejestracji jednokrotnej z jednego Zscaler wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="5f433-151">**tooconfigure Azure AD single sign-on with Zscaler One, perform hello following steps:**</span></span>

1. <span data-ttu-id="5f433-152">W portalu Azure na powitania hello **Zscaler jeden** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="5f433-152">In hello Azure portal, on hello **Zscaler One** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="5f433-154">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="5f433-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_samlbase.png)

3. <span data-ttu-id="5f433-156">Na powitania **Zscaler jednej domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="5f433-156">On hello **Zscaler One Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_url.png)

    <span data-ttu-id="5f433-158">W polu tekstowym adres URL logowania hello wpisz adres URL hello używany przez Twoje użytkowników toosign na tooyour Zscaler jedną aplikację.</span><span class="sxs-lookup"><span data-stu-id="5f433-158">In hello Sign-on URL textbox, type hello URL used by your users toosign-on tooyour Zscaler One application.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5f433-159">Masz tooupdate tej wartości z hello rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="5f433-159">You have tooupdate this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="5f433-160">Skontaktuj się z [zespołem pomocy technicznej Zscaler jeden klient](https://www.zscaler.com/company/contact) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="5f433-160">Contact [Zscaler One Client support team](https://www.zscaler.com/company/contact) tooget these values.</span></span>

4. <span data-ttu-id="5f433-161">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="5f433-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_certificate.png) 

5. <span data-ttu-id="5f433-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5f433-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5f433-165">Na powitania **Zscaler jedną konfigurację** kliknij **skonfigurować jeden Zscaler** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="5f433-165">On hello **Zscaler One Configuration** section, click **Configure Zscaler One** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5f433-166">Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="5f433-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_configure.png) 

7. <span data-ttu-id="5f433-168">W oknie przeglądarki innej witryny sieci web Zaloguj się za tooyour Zscaler jednej witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="5f433-168">In a different web browser window, log in tooyour Zscaler One company site as an administrator.</span></span>

8. <span data-ttu-id="5f433-169">W menu hello na górze hello, kliknij przycisk **administracji**.</span><span class="sxs-lookup"><span data-stu-id="5f433-169">In hello menu on hello top, click **Administration**.</span></span>
   
    <span data-ttu-id="5f433-170">![Administracja](./media/active-directory-saas-zscaler-one-tutorial/ic800206.png "administracji")</span><span class="sxs-lookup"><span data-stu-id="5f433-170">![Administration](./media/active-directory-saas-zscaler-one-tutorial/ic800206.png "Administration")</span></span>

9. <span data-ttu-id="5f433-171">W obszarze **administratorom zarządzanie & role**, kliknij przycisk **Zarządzanie użytkownikami & uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="5f433-171">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="5f433-172">![Zarządzaj użytkownikami & uwierzytelniania](./media/active-directory-saas-zscaler-one-tutorial/ic800207.png "zarządzania użytkownikami i uwierzytelniania")</span><span class="sxs-lookup"><span data-stu-id="5f433-172">![Manage Users & Authentication](./media/active-directory-saas-zscaler-one-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

10. <span data-ttu-id="5f433-173">W hello **wybierz opcje uwierzytelniania dla Twojej organizacji** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="5f433-173">In hello **Choose Authentication Options for your Organization** section, perform hello following steps:</span></span>   
                
    <span data-ttu-id="5f433-174">![Uwierzytelnianie](./media/active-directory-saas-zscaler-one-tutorial/ic800208.png "uwierzytelniania")</span><span class="sxs-lookup"><span data-stu-id="5f433-174">![Authentication](./media/active-directory-saas-zscaler-one-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="5f433-175">a.</span><span class="sxs-lookup"><span data-stu-id="5f433-175">a.</span></span> <span data-ttu-id="5f433-176">Wybierz **uwierzytelnianie przy użyciu SAML logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="5f433-176">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="5f433-177">b.</span><span class="sxs-lookup"><span data-stu-id="5f433-177">b.</span></span> <span data-ttu-id="5f433-178">Kliknij przycisk **skonfigurować SAML pojedynczego logowania jednokrotnego parametry**.</span><span class="sxs-lookup"><span data-stu-id="5f433-178">Click **Configure SAML Single Sign-On Parameters**.</span></span>

11. <span data-ttu-id="5f433-179">Na powitania **skonfigurować SAML pojedynczych logowania jednokrotnego parametrów** strony okna dialogowego, wykonaj następujące kroki hello, a następnie kliknij **gotowe**</span><span class="sxs-lookup"><span data-stu-id="5f433-179">On hello **Configure SAML Single Sign-On Parameters** dialog page, perform hello following steps, and then click **Done**</span></span>

    <span data-ttu-id="5f433-180">![Logowanie jednokrotne](./media/active-directory-saas-zscaler-one-tutorial/ic800209.png "logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="5f433-180">![Single Sign-On](./media/active-directory-saas-zscaler-one-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="5f433-181">a.</span><span class="sxs-lookup"><span data-stu-id="5f433-181">a.</span></span> <span data-ttu-id="5f433-182">Wklej hello **SAML pojedynczy znak na adres URL usługi** wartość, która została skopiowana z hello portalu Azure do hello **adres URL hello SAML portalu toowhich użytkowników są wysyłane do uwierzytelniania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="5f433-182">Paste hello **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **URL of hello SAML Portal toowhich users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="5f433-183">b.</span><span class="sxs-lookup"><span data-stu-id="5f433-183">b.</span></span> <span data-ttu-id="5f433-184">W hello **atrybutu zawierającego nazwę logowania** pole tekstowe, typ **NameID**.</span><span class="sxs-lookup"><span data-stu-id="5f433-184">In hello **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="5f433-185">c.</span><span class="sxs-lookup"><span data-stu-id="5f433-185">c.</span></span> <span data-ttu-id="5f433-186">tooupload pobranego certyfikatu, kliknij przycisk **Zscaler pem**.</span><span class="sxs-lookup"><span data-stu-id="5f433-186">tooupload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="5f433-187">d.</span><span class="sxs-lookup"><span data-stu-id="5f433-187">d.</span></span> <span data-ttu-id="5f433-188">Wybierz **Włącz SAML automatycznego inicjowania obsługi**.</span><span class="sxs-lookup"><span data-stu-id="5f433-188">Select **Enable SAML Auto-Provisioning**.</span></span>

12. <span data-ttu-id="5f433-189">Na powitania **skonfigurować uwierzytelnianie użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="5f433-189">On hello **Configure User Authentication** dialog page, perform hello following steps:</span></span>

    <span data-ttu-id="5f433-190">![Administracja](./media/active-directory-saas-zscaler-one-tutorial/ic800210.png "administracji")</span><span class="sxs-lookup"><span data-stu-id="5f433-190">![Administration](./media/active-directory-saas-zscaler-one-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="5f433-191">a.</span><span class="sxs-lookup"><span data-stu-id="5f433-191">a.</span></span> <span data-ttu-id="5f433-192">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="5f433-192">Click **Save**.</span></span>

    <span data-ttu-id="5f433-193">b.</span><span class="sxs-lookup"><span data-stu-id="5f433-193">b.</span></span> <span data-ttu-id="5f433-194">Kliknij przycisk **Aktywuj teraz**.</span><span class="sxs-lookup"><span data-stu-id="5f433-194">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="5f433-195">Konfigurowanie ustawień serwera proxy</span><span class="sxs-lookup"><span data-stu-id="5f433-195">Configuring proxy settings</span></span>
### <a name="tooconfigure-hello-proxy-settings-in-internet-explorer"></a><span data-ttu-id="5f433-196">ustawienia serwera proxy hello tooconfigure w programie Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="5f433-196">tooconfigure hello proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="5f433-197">Uruchom **programu Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="5f433-197">Start **Internet Explorer**.</span></span>

2. <span data-ttu-id="5f433-198">Wybierz **Opcje internetowe** z hello **narzędzia** menu Otwórz hello **Opcje internetowe** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5f433-198">Select **Internet options** from hello **Tools** menu for open hello **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="5f433-199">![Opcje internetowe](./media/active-directory-saas-zscaler-one-tutorial/ic769492.png "Opcje internetowe")</span><span class="sxs-lookup"><span data-stu-id="5f433-199">![Internet Options](./media/active-directory-saas-zscaler-one-tutorial/ic769492.png "Internet Options")</span></span>

3. <span data-ttu-id="5f433-200">Kliknij przycisk hello **połączeń** kartę.</span><span class="sxs-lookup"><span data-stu-id="5f433-200">Click hello **Connections** tab.</span></span>   
  
     <span data-ttu-id="5f433-201">![Połączenia](./media/active-directory-saas-zscaler-one-tutorial/ic769493.png "połączeń")</span><span class="sxs-lookup"><span data-stu-id="5f433-201">![Connections](./media/active-directory-saas-zscaler-one-tutorial/ic769493.png "Connections")</span></span>

4. <span data-ttu-id="5f433-202">Kliknij przycisk **ustawienia sieci LAN** tooopen hello **ustawienia sieci LAN** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5f433-202">Click **LAN settings** tooopen hello **LAN Settings** dialog.</span></span>

5. <span data-ttu-id="5f433-203">W sekcji serwer Proxy hello wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="5f433-203">In hello Proxy server section, perform hello following steps:</span></span>   
   
    <span data-ttu-id="5f433-204">![Serwer proxy](./media/active-directory-saas-zscaler-one-tutorial/ic769494.png "serwera Proxy")</span><span class="sxs-lookup"><span data-stu-id="5f433-204">![Proxy server](./media/active-directory-saas-zscaler-one-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="5f433-205">a.</span><span class="sxs-lookup"><span data-stu-id="5f433-205">a.</span></span> <span data-ttu-id="5f433-206">Wybierz **Użyj serwera proxy dla sieci LAN**.</span><span class="sxs-lookup"><span data-stu-id="5f433-206">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="5f433-207">b.</span><span class="sxs-lookup"><span data-stu-id="5f433-207">b.</span></span> <span data-ttu-id="5f433-208">W polu tekstowym adres hello, wpisz **gateway.zscalerone.net**.</span><span class="sxs-lookup"><span data-stu-id="5f433-208">In hello Address textbox, type **gateway.zscalerone.net**.</span></span>

    <span data-ttu-id="5f433-209">c.</span><span class="sxs-lookup"><span data-stu-id="5f433-209">c.</span></span> <span data-ttu-id="5f433-210">W polu tekstowym portu hello, wpisz **80**.</span><span class="sxs-lookup"><span data-stu-id="5f433-210">In hello Port textbox, type **80**.</span></span>

    <span data-ttu-id="5f433-211">d.</span><span class="sxs-lookup"><span data-stu-id="5f433-211">d.</span></span> <span data-ttu-id="5f433-212">Wybierz **używaj serwera proxy dla adresów lokalnych**.</span><span class="sxs-lookup"><span data-stu-id="5f433-212">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="5f433-213">e.</span><span class="sxs-lookup"><span data-stu-id="5f433-213">e.</span></span> <span data-ttu-id="5f433-214">Kliknij przycisk **OK** tooclose hello **ustawienia sieci lokalnej (LAN)** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5f433-214">Click **OK** tooclose hello **Local Area Network (LAN) Settings** dialog.</span></span>

6. <span data-ttu-id="5f433-215">Kliknij przycisk **OK** tooclose hello **Opcje internetowe** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5f433-215">Click **OK** tooclose hello **Internet Options** dialog.</span></span>

> [!TIP]
> <span data-ttu-id="5f433-216">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="5f433-216">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5f433-217">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello ** Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="5f433-217">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5f433-218">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5f433-218">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5f433-219">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5f433-219">Creating an Azure AD test user</span></span>
<span data-ttu-id="5f433-220">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="5f433-220">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="5f433-222">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="5f433-222">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5f433-223">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="5f433-223">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zscaler-one-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5f433-225">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="5f433-225">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zscaler-one-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5f433-227">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5f433-227">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zscaler-one-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5f433-229">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="5f433-229">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zscaler-one-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5f433-231">a.</span><span class="sxs-lookup"><span data-stu-id="5f433-231">a.</span></span> <span data-ttu-id="5f433-232">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5f433-232">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5f433-233">b.</span><span class="sxs-lookup"><span data-stu-id="5f433-233">b.</span></span> <span data-ttu-id="5f433-234">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5f433-234">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5f433-235">c.</span><span class="sxs-lookup"><span data-stu-id="5f433-235">c.</span></span> <span data-ttu-id="5f433-236">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="5f433-236">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5f433-237">d.</span><span class="sxs-lookup"><span data-stu-id="5f433-237">d.</span></span> <span data-ttu-id="5f433-238">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="5f433-238">Click **Create**.</span></span>
 
### <a name="creating-a-zscaler-one-test-user"></a><span data-ttu-id="5f433-239">Tworzenie Zscaler jednego użytkownika testowego</span><span class="sxs-lookup"><span data-stu-id="5f433-239">Creating a Zscaler One test user</span></span>

<span data-ttu-id="5f433-240">tooenable usługi Azure AD użytkownicy toolog tooZscaler co muszą być elastycznie tooZscaler, jeden.</span><span class="sxs-lookup"><span data-stu-id="5f433-240">tooenable Azure AD users toolog in tooZscaler One, they must be provisioned tooZscaler One.</span></span> <span data-ttu-id="5f433-241">W przypadku hello z jednego Zscaler Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="5f433-241">In hello case of Zscaler One, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="5f433-242">tooconfigure aprowizacji użytkowników, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="5f433-242">tooconfigure user provisioning, perform hello following steps:</span></span>

1. <span data-ttu-id="5f433-243">Zaloguj się za tooyour **Zscaler jeden** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="5f433-243">Log in tooyour **Zscaler One** tenant.</span></span>

2. <span data-ttu-id="5f433-244">Kliknij przycisk **administracji**.</span><span class="sxs-lookup"><span data-stu-id="5f433-244">Click **Administration**.</span></span>   
   
    <span data-ttu-id="5f433-245">![Administracja](./media/active-directory-saas-zscaler-one-tutorial/ic781035.png "administracji")</span><span class="sxs-lookup"><span data-stu-id="5f433-245">![Administration](./media/active-directory-saas-zscaler-one-tutorial/ic781035.png "Administration")</span></span>

3. <span data-ttu-id="5f433-246">Kliknij przycisk **Zarządzanie użytkownikami**.</span><span class="sxs-lookup"><span data-stu-id="5f433-246">Click **User Management**.</span></span>   
        
     <span data-ttu-id="5f433-247">![Dodaj](./media/active-directory-saas-zscaler-one-tutorial/ic781036.png "Dodaj")</span><span class="sxs-lookup"><span data-stu-id="5f433-247">![Add](./media/active-directory-saas-zscaler-one-tutorial/ic781036.png "Add")</span></span>

4. <span data-ttu-id="5f433-248">W hello **użytkowników** , kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="5f433-248">In hello **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="5f433-249">![Dodaj](./media/active-directory-saas-zscaler-one-tutorial/ic781037.png "Dodaj")</span><span class="sxs-lookup"><span data-stu-id="5f433-249">![Add](./media/active-directory-saas-zscaler-one-tutorial/ic781037.png "Add")</span></span>

5. <span data-ttu-id="5f433-250">W sekcji Dodaj użytkownika hello wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="5f433-250">In hello Add User section, perform hello following steps:</span></span>
        
    <span data-ttu-id="5f433-251">![Dodaj użytkownika](./media/active-directory-saas-zscaler-one-tutorial/ic781038.png "Dodaj użytkownika")</span><span class="sxs-lookup"><span data-stu-id="5f433-251">![Add User](./media/active-directory-saas-zscaler-one-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="5f433-252">a.</span><span class="sxs-lookup"><span data-stu-id="5f433-252">a.</span></span> <span data-ttu-id="5f433-253">Hello typu **UserID**, **Nazwa wyświetlana użytkownika**, **hasło**, **Potwierdź hasło**, a następnie wybierz **grup**i hello **działu** prawidłowy Azure AD konta tooprovision.</span><span class="sxs-lookup"><span data-stu-id="5f433-253">Type hello **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and hello **Department** of a valid Azure AD account you want tooprovision.</span></span>

    <span data-ttu-id="5f433-254">b.</span><span class="sxs-lookup"><span data-stu-id="5f433-254">b.</span></span> <span data-ttu-id="5f433-255">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="5f433-255">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="5f433-256">Możesz użyć innych Zscaler jednego użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez tooprovision Zscaler jednego konta użytkownika usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5f433-256">You can use any other Zscaler One user account creation tools or APIs provided by Zscaler One tooprovision Azure AD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5f433-257">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5f433-257">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5f433-258">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooZscaler, jeden.</span><span class="sxs-lookup"><span data-stu-id="5f433-258">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZscaler One.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="5f433-260">**tooassign tooZscaler Simona Britta, jednego, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="5f433-260">**tooassign Britta Simon tooZscaler One, perform hello following steps:**</span></span>

1. <span data-ttu-id="5f433-261">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="5f433-261">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="5f433-263">Z listy aplikacji hello wybierz **Zscaler jeden**.</span><span class="sxs-lookup"><span data-stu-id="5f433-263">In hello applications list, select **Zscaler One**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_app.png) 

3. <span data-ttu-id="5f433-265">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="5f433-265">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="5f433-267">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5f433-267">Click **Add** button.</span></span> <span data-ttu-id="5f433-268">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5f433-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="5f433-270">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="5f433-270">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5f433-271">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5f433-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5f433-272">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5f433-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5f433-273">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5f433-273">Testing single sign-on</span></span>

<span data-ttu-id="5f433-274">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="5f433-274">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5f433-275">Po kliknięciu kafelka Zscaler jeden hello w hello panelu dostępu, należy pobrać automatycznie zalogowane tooyour Zscaler jedną aplikację.</span><span class="sxs-lookup"><span data-stu-id="5f433-275">When you click hello Zscaler One tile in hello Access Panel, you should get automatically signed-on tooyour Zscaler One application.</span></span>
<span data-ttu-id="5f433-276">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5f433-276">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5f433-277">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="5f433-277">Additional resources</span></span>

* [<span data-ttu-id="5f433-278">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5f433-278">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5f433-279">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5f433-279">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_203.png

