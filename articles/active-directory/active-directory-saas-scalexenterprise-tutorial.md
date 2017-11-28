---
title: "Samouczek: Integrację usługi Azure Active Directory ze ScaleX | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i ScaleX Enterprise."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2379a8d-a659-45f1-87db-9ba156d83183
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: e398b98d9e0957b5f92c82359651c345d22c3a54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scalex-enterprise"></a><span data-ttu-id="70a46-103">Samouczek: Integrację usługi Azure Active Directory ze ScaleX</span><span class="sxs-lookup"><span data-stu-id="70a46-103">Tutorial: Azure Active Directory integration with ScaleX Enterprise</span></span>

<span data-ttu-id="70a46-104">Z tego samouczka, dowiesz się, jak toointegrate ScaleX przedsiębiorstwa w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="70a46-104">In this tutorial, you learn how toointegrate ScaleX Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="70a46-105">Integrowanie ScaleX organizacji z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="70a46-105">Integrating ScaleX Enterprise with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="70a46-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooScaleX przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="70a46-106">You can control in Azure AD who has access tooScaleX Enterprise</span></span>
- <span data-ttu-id="70a46-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooScaleX przedsiębiorstwa (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="70a46-107">You can enable your users tooautomatically get signed-on tooScaleX Enterprise (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="70a46-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="70a46-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="70a46-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz.</span><span class="sxs-lookup"><span data-stu-id="70a46-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="70a46-110">Co to jest dostęp do aplikacji i logowanie jednokrotne z [usługi Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="70a46-110">What is application access and single sign-on with [Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="70a46-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="70a46-111">Prerequisites</span></span>

<span data-ttu-id="70a46-112">tooconfigure integracji usługi Azure AD z ScaleX Enterprise należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="70a46-112">tooconfigure Azure AD integration with ScaleX Enterprise, you need hello following items:</span></span>

- <span data-ttu-id="70a46-113">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="70a46-113">An Azure AD subscription</span></span>
- <span data-ttu-id="70a46-114">ScaleX Enterprise jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="70a46-114">A ScaleX Enterprise single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="70a46-115">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="70a46-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="70a46-116">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="70a46-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="70a46-117">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="70a46-117">Do not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="70a46-118">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="70a46-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="70a46-119">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="70a46-119">Scenario description</span></span>
<span data-ttu-id="70a46-120">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="70a46-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="70a46-121">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="70a46-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="70a46-122">Dodawanie ScaleX przedsiębiorstwa z galerii hello</span><span class="sxs-lookup"><span data-stu-id="70a46-122">Adding ScaleX Enterprise from hello gallery</span></span>
2. <span data-ttu-id="70a46-123">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="70a46-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-scalex-enterprise-from-hello-gallery"></a><span data-ttu-id="70a46-124">Dodawanie ScaleX przedsiębiorstwa z galerii hello</span><span class="sxs-lookup"><span data-stu-id="70a46-124">Adding ScaleX Enterprise from hello gallery</span></span>
<span data-ttu-id="70a46-125">tooconfigure hello integracji przedsiębiorstwa ScaleX w tooAzure AD, należy tooadd ScaleX przedsiębiorstwa z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="70a46-125">tooconfigure hello integration of ScaleX Enterprise in tooAzure AD, you need tooadd ScaleX Enterprise from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="70a46-126">**tooadd ScaleX przedsiębiorstwa z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="70a46-126">**tooadd ScaleX Enterprise from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="70a46-127">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="70a46-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="70a46-129">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="70a46-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="70a46-130">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="70a46-130">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="70a46-132">Kliknij przycisk **Dodaj** przycisk u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="70a46-132">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="70a46-134">W polu wyszukiwania hello wpisz **ScaleX Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="70a46-134">In hello search box, type **ScaleX Enterprise**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_search.png)

5. <span data-ttu-id="70a46-136">W panelu wyników hello, wybierz **ScaleX Enterprise**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="70a46-136">In hello results panel, select **ScaleX Enterprise**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="70a46-138">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="70a46-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="70a46-139">W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z ScaleX Enterprise oparte na użytkownika testowego o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="70a46-139">In this section, you configure and test Azure AD single sign-on with ScaleX Enterprise based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="70a46-140">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w przedsiębiorstwie ScaleX jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="70a46-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ScaleX Enterprise is tooa user in Azure AD.</span></span> <span data-ttu-id="70a46-141">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w przedsiębiorstwie ScaleX musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="70a46-141">In other words, a link relationship between an Azure AD user and hello related user in ScaleX Enterprise needs toobe established.</span></span>

<span data-ttu-id="70a46-142">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w przedsiębiorstwie ScaleX.</span><span class="sxs-lookup"><span data-stu-id="70a46-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ScaleX Enterprise.</span></span>

<span data-ttu-id="70a46-143">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z ScaleX przedsiębiorstwa, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="70a46-143">tooconfigure and test Azure AD single sign-on with ScaleX Enterprise, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="70a46-144">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="70a46-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="70a46-145">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="70a46-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="70a46-146">**[Tworzenie użytkownika testowego ScaleX Enterprise](#creating-a-scalex-enterprise-test-user)**  -toohave odpowiednikiem Simona Britta w przedsiębiorstwie ScaleX, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="70a46-146">**[Creating a ScaleX Enterprise test user](#creating-a-scalex-enterprise-test-user)** - toohave a counterpart of Britta Simon in ScaleX Enterprise that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="70a46-147">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="70a46-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="70a46-148">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="70a46-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="70a46-149">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="70a46-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="70a46-150">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w aplikacji przedsiębiorstwa ScaleX.</span><span class="sxs-lookup"><span data-stu-id="70a46-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ScaleX Enterprise application.</span></span>

<span data-ttu-id="70a46-151">**tooconfigure usługi Azure AD rejestracji jednokrotnej z ScaleX przedsiębiorstwa, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="70a46-151">**tooconfigure Azure AD single sign-on with ScaleX Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="70a46-152">W portalu Azure na powitania hello **ScaleX Enterprise** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="70a46-152">In hello Azure portal, on hello **ScaleX Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="70a46-154">Na powitania **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="70a46-154">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_samlbase.png)

3. <span data-ttu-id="70a46-156">Na powitania **ScaleX domeny przedsiębiorstwa i adres URL** sekcji, wykonaj następujące kroki, jeśli chcesz, aby aplikacja hello tooconfigure w hello **IDP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="70a46-156">On hello **ScaleX Enterprise Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url1.png)

    <span data-ttu-id="70a46-158">a.</span><span class="sxs-lookup"><span data-stu-id="70a46-158">a.</span></span> <span data-ttu-id="70a46-159">W hello **identyfikator** pole tekstowe, wartość hello typu przy użyciu hello następującego wzorca:`https://platform.rescale.com/saml2/<company id>/`</span><span class="sxs-lookup"><span data-stu-id="70a46-159">In hello **Identifier** textbox, type hello value using hello following pattern: `https://platform.rescale.com/saml2/<company id>/`</span></span>

    <span data-ttu-id="70a46-160">b.</span><span class="sxs-lookup"><span data-stu-id="70a46-160">b.</span></span> <span data-ttu-id="70a46-161">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://platform.rescale.com/saml2/<company id>/acs/`</span><span class="sxs-lookup"><span data-stu-id="70a46-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://platform.rescale.com/saml2/<company id>/acs/`</span></span>

4. <span data-ttu-id="70a46-162">Sprawdź **Pokaż zaawansowane ustawienia adresu URL**, jeśli chcesz, aby aplikacja hello tooconfigure w **SP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="70a46-162">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url2.png)

    <span data-ttu-id="70a46-164">W hello **adres URL logowania** pole tekstowe, wartość hello typu przy użyciu hello następującego wzorca:`https://platform.rescale.com/saml2/<company id>/sso/`</span><span class="sxs-lookup"><span data-stu-id="70a46-164">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://platform.rescale.com/saml2/<company id>/sso/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="70a46-165">Nie są hello wartości rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="70a46-165">These are not hello real values.</span></span> <span data-ttu-id="70a46-166">Z hello rzeczywisty identyfikator, adres URL odpowiedzi lub adres URL logowania, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="70a46-166">Update these values with hello actual Identifier, Reply URL or Sign-On URL.</span></span> <span data-ttu-id="70a46-167">Skontaktuj się z [zespołem pomocy technicznej klienta Enterprise ScaleX](http://info.rescale.com/contact_sales) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="70a46-167">Contact [ScaleX Enterprise Client support team](http://info.rescale.com/contact_sales) tooget these values.</span></span> 

5. <span data-ttu-id="70a46-168">Aplikacja ScaleX oczekuje potwierdzenia SAML hello w określonym formacie wymaga możesz toomodify atrybutu niestandardowego mapowania tooyour SAML tokenu atrybuty konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="70a46-168">Your ScaleX application expects hello SAML assertions in a specific format, which requires you toomodify custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="70a46-169">Kliknij przycisk **widoku i edytować wszystkie atrybuty użytkowników** hello tooopen wyboru niestandardowych atrybutów ustawienia.</span><span class="sxs-lookup"><span data-stu-id="70a46-169">Click **View and edit all other user attributes** checkbox tooopen hello custom attributes settings.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scalexenterprise-tutorial/scalex_attributes.png)
    
    <span data-ttu-id="70a46-171">a.</span><span class="sxs-lookup"><span data-stu-id="70a46-171">a.</span></span> <span data-ttu-id="70a46-172">Kliknij prawym przyciskiem myszy atrybut hello **nazwa** i kliknij przycisk Usuń.</span><span class="sxs-lookup"><span data-stu-id="70a46-172">Right click hello attribute **name** and click delete.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scalexenterprise-tutorial/delete_attribute_name.png)

    <span data-ttu-id="70a46-174">b.</span><span class="sxs-lookup"><span data-stu-id="70a46-174">b.</span></span> <span data-ttu-id="70a46-175">Kliknij przycisk **emailaddress** okno edycji atrybucie hello tooopen atrybutu.</span><span class="sxs-lookup"><span data-stu-id="70a46-175">Click **emailaddress** attribute tooopen hello Edit Attribute window.</span></span> <span data-ttu-id="70a46-176">Zmień wartość z **user.mail** za**user.userprincipalname** i kliknij przycisk Ok.</span><span class="sxs-lookup"><span data-stu-id="70a46-176">Change its value from **user.mail** too**user.userprincipalname** and click Ok.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scalexenterprise-tutorial/edit_email_attribute.png)   
    
5. <span data-ttu-id="70a46-178">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="70a46-178">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello Certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_certificate.png) 

6. <span data-ttu-id="70a46-180">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="70a46-180">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="70a46-182">Na powitania **konfiguracja dla przedsiębiorstw ScaleX** , kliknij przycisk **skonfigurować ScaleX Enterprise** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="70a46-182">On hello **ScaleX Enterprise Configuration** section, click **Configure ScaleX Enterprise** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="70a46-183">Kopiuj hello **SAML identyfikator jednostki** i **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="70a46-183">Copy hello **SAML Entity ID** and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_configure.png) 

8. <span data-ttu-id="70a46-185">tooconfigure rejestracji jednokrotnej w **ScaleX Enterprise** strona, logowania toohello ScaleX Enterprise witryny sieci Web firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="70a46-185">tooconfigure single sign-on on **ScaleX Enterprise** side, login toohello ScaleX Enterprise company website as an administrator.</span></span>

9. <span data-ttu-id="70a46-186">Kliknij menu hello w górnym hello prawo i wybierz **administracji Contoso**.</span><span class="sxs-lookup"><span data-stu-id="70a46-186">Click hello menu in hello upper right and select **Contoso Administration**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="70a46-187">Firma Contoso jest tylko przykładowe.</span><span class="sxs-lookup"><span data-stu-id="70a46-187">Contoso is just an example.</span></span> <span data-ttu-id="70a46-188">Powinno to być rzeczywista nazwa firmy.</span><span class="sxs-lookup"><span data-stu-id="70a46-188">This should be your actual Company Name.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scalexenterprise-tutorial/Test_Admin.png) 

10. <span data-ttu-id="70a46-190">Wybierz **integracji** z górnego menu hello i wybierz **rejestracji jednokrotnej**.</span><span class="sxs-lookup"><span data-stu-id="70a46-190">Select **Integrations** from hello top menu and select **Single Sign-On**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scalexenterprise-tutorial/admin_sso.png) 

11. <span data-ttu-id="70a46-192">Wypełnij formularz hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="70a46-192">Complete hello form as follows:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scalexenterprise-tutorial/scalex_admin_save.png) 
    
    <span data-ttu-id="70a46-194">a.</span><span class="sxs-lookup"><span data-stu-id="70a46-194">a.</span></span> <span data-ttu-id="70a46-195">Wybierz **"Utwórz każdy użytkownik, który może uwierzytelniać z logowania jednokrotnego."**</span><span class="sxs-lookup"><span data-stu-id="70a46-195">Select **“Create any user who can authenticate with SSO.”**</span></span>

    <span data-ttu-id="70a46-196">b.</span><span class="sxs-lookup"><span data-stu-id="70a46-196">b.</span></span> <span data-ttu-id="70a46-197">**Saml dostawcy usług**: wkleić wartość hello ***urn: oasis: nazwy: tc: SAML:2.0:nameid-format: stałe***</span><span class="sxs-lookup"><span data-stu-id="70a46-197">**Service Provider saml**: Paste hello value ***urn:oasis:names:tc:SAML:2.0:nameid-format:persistent***</span></span>

    <span data-ttu-id="70a46-198">c.</span><span class="sxs-lookup"><span data-stu-id="70a46-198">c.</span></span> <span data-ttu-id="70a46-199">**Nazwa dostawcy tożsamości pola wiadomości e-mail w odpowiedzi ACS**: wkleić hello wartość`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span><span class="sxs-lookup"><span data-stu-id="70a46-199">**Name of Identity Provider email field in ACS response**: Paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span></span>

    <span data-ttu-id="70a46-200">d.</span><span class="sxs-lookup"><span data-stu-id="70a46-200">d.</span></span> <span data-ttu-id="70a46-201">**Identyfikator jednostki EntityDescriptor dostawcy tożsamości:** hello Wklej **identyfikator jednostki SAML** kopiuje wartość hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="70a46-201">**Identity Provider EntityDescriptor Entity ID:** Paste hello **SAML Entity ID** value copied from hello Azure portal.</span></span>

    <span data-ttu-id="70a46-202">e.</span><span class="sxs-lookup"><span data-stu-id="70a46-202">e.</span></span> <span data-ttu-id="70a46-203">**Adres URL SingleSignOnService dostawcy tożsamości:** hello Wklej **SAML pojedynczy znak na adres URL usługi** z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="70a46-203">**Identity Provider SingleSignOnService URL:** Paste hello **SAML Single Sign-On Service URL** from hello Azure portal.</span></span>

    <span data-ttu-id="70a46-204">f.</span><span class="sxs-lookup"><span data-stu-id="70a46-204">f.</span></span> <span data-ttu-id="70a46-205">**Certyfikat publiczny X509 dostawcy tożsamości:** Otwórz hello X509 certyfikat pobrany z hello Azure w programie Notatnik i Wklej zawartość hello, w tym polu.</span><span class="sxs-lookup"><span data-stu-id="70a46-205">**Identity Provider public X509 certificate:** Open hello X509 certificate downloaded from hello Azure in notepad and paste hello contents in this box.</span></span> <span data-ttu-id="70a46-206">Upewnij się, Brak Brak wiersza w podziałów hello środkowej hello treści certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="70a46-206">Ensure there are no line breaks in hello middle of hello certificate contents.</span></span>
    
    <span data-ttu-id="70a46-207">g.</span><span class="sxs-lookup"><span data-stu-id="70a46-207">g.</span></span> <span data-ttu-id="70a46-208">Sprawdź następujące pola wyboru hello: **włączone, NameID szyfrowania i AuthnRequests logowania.**</span><span class="sxs-lookup"><span data-stu-id="70a46-208">Check hello following checkboxes: **Enabled, Encrypt NameID and Sign AuthnRequests.**</span></span>

    <span data-ttu-id="70a46-209">h.</span><span class="sxs-lookup"><span data-stu-id="70a46-209">h.</span></span> <span data-ttu-id="70a46-210">Kliknij przycisk **ustawienia logowania jednokrotnego aktualizacji** toosave hello ustawienia.</span><span class="sxs-lookup"><span data-stu-id="70a46-210">Click **Update SSO Settings** toosave hello settings.</span></span>

> [!TIP]
> <span data-ttu-id="70a46-211">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="70a46-211">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="70a46-212">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="70a46-212">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="70a46-213">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="70a46-213">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="70a46-214">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="70a46-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="70a46-215">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="70a46-215">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="70a46-217">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="70a46-217">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="70a46-218">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="70a46-218">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="70a46-220">Przejdź za**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** toodisplay hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="70a46-220">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="70a46-222">U góry okna dialogowego hello hello, kliknij przycisk **Dodaj** tooopen hello **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="70a46-222">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="70a46-224">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="70a46-224">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="70a46-226">a.</span><span class="sxs-lookup"><span data-stu-id="70a46-226">a.</span></span> <span data-ttu-id="70a46-227">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="70a46-227">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="70a46-228">b.</span><span class="sxs-lookup"><span data-stu-id="70a46-228">b.</span></span> <span data-ttu-id="70a46-229">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="70a46-229">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="70a46-230">c.</span><span class="sxs-lookup"><span data-stu-id="70a46-230">c.</span></span> <span data-ttu-id="70a46-231">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="70a46-231">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="70a46-232">d.</span><span class="sxs-lookup"><span data-stu-id="70a46-232">d.</span></span> <span data-ttu-id="70a46-233">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="70a46-233">Click **Create**.</span></span>
 
### <a name="creating-a-scalex-enterprise-test-user"></a><span data-ttu-id="70a46-234">Tworzenie użytkownika testowego ScaleX Enterprise</span><span class="sxs-lookup"><span data-stu-id="70a46-234">Creating a ScaleX Enterprise test user</span></span>

<span data-ttu-id="70a46-235">toolog użytkowników tooenable usługi Azure AD w tooScaleX przedsiębiorstwa muszą mieć przydzielone w tooScaleX przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="70a46-235">tooenable Azure AD users toolog in tooScaleX Enterprise, they must be provisioned in tooScaleX Enterprise.</span></span> <span data-ttu-id="70a46-236">W przypadku hello ScaleX przedsiębiorstwa Inicjowanie obsługi to zadanie automatycznej i nie są wymagane żadne czynności ręcznych.</span><span class="sxs-lookup"><span data-stu-id="70a46-236">In hello case of ScaleX Enterprise, provisioning is an automatic task and no manual steps are required.</span></span> <span data-ttu-id="70a46-237">Każdy użytkownik, który może pomyślnie wykonać uwierzytelnienia przy użyciu poświadczeń logowania jednokrotnego będą automatycznie udostępniane na powitania po stronie ScaleX.</span><span class="sxs-lookup"><span data-stu-id="70a46-237">Any user who can successfully authenticate with SSO credentials will be automatically provisioned on hello ScaleX side.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="70a46-238">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="70a46-238">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="70a46-239">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie Enterprise tooScaleX dostępu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="70a46-239">In this section, you enable Britta Simon toouse Azure single sign-on by granting user access tooScaleX Enterprise.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="70a46-241">**tooassign Simona Britta tooScaleX przedsiębiorstwa, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="70a46-241">**tooassign Britta Simon tooScaleX Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="70a46-242">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="70a46-242">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="70a46-244">Z listy aplikacji hello wybierz **ScaleX Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="70a46-244">In hello applications list, select **ScaleX Enterprise**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_app.png) 

3. <span data-ttu-id="70a46-246">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="70a46-246">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="70a46-248">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="70a46-248">Click **Add** button.</span></span> <span data-ttu-id="70a46-249">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="70a46-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="70a46-251">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="70a46-251">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="70a46-252">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="70a46-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="70a46-253">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="70a46-253">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="70a46-254">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="70a46-254">Testing single sign-on</span></span>

<span data-ttu-id="70a46-255">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="70a46-255">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="70a46-256">Kliknij hello ScaleX Enterprise kafelka w hello Panel dostępu, otrzymasz automatycznie zalogowane tooyour aplikacja całościowa ScaleX.</span><span class="sxs-lookup"><span data-stu-id="70a46-256">Click hello ScaleX Enterprise tile in hello Access Panel, you will get automatically signed-on tooyour ScaleX Enterprise application.</span></span> <span data-ttu-id="70a46-257">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="70a46-257">For more information about hello Access Panel, see [Introduction toohello Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="70a46-258">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="70a46-258">Additional resources</span></span>

* [<span data-ttu-id="70a46-259">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="70a46-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="70a46-260">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="70a46-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_203.png

