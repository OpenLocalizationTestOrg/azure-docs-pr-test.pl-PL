---
title: 'Samouczek: Integracji Azure Active Directory z Voyance | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Voyance."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 539dc1f9-64c9-4dce-b259-2b0b49dcf857
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2017
ms.author: jeedes
ms.openlocfilehash: e2cb9eb6b20e8611a9f6e8529b7c85a8d86ec3e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-voyance"></a><span data-ttu-id="d18e3-103">Samouczek: Integracji Azure Active Directory z Voyance</span><span class="sxs-lookup"><span data-stu-id="d18e3-103">Tutorial: Azure Active Directory integration with Voyance</span></span>

<span data-ttu-id="d18e3-104">Z tego samouczka, dowiesz się, jak toointegrate Voyance w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d18e3-104">In this tutorial, you learn how toointegrate Voyance with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d18e3-105">Integracja z usługą Azure AD Voyance zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="d18e3-105">Integrating Voyance with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d18e3-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooVoyance</span><span class="sxs-lookup"><span data-stu-id="d18e3-106">You can control in Azure AD who has access tooVoyance</span></span>
- <span data-ttu-id="d18e3-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooVoyance (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d18e3-107">You can enable your users tooautomatically get signed-on tooVoyance (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d18e3-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="d18e3-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d18e3-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d18e3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d18e3-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d18e3-110">Prerequisites</span></span>

<span data-ttu-id="d18e3-111">tooconfigure integracji z usługą Azure AD z Voyance należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="d18e3-111">tooconfigure Azure AD integration with Voyance, you need hello following items:</span></span>

- <span data-ttu-id="d18e3-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d18e3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d18e3-113">Voyance logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="d18e3-113">A Voyance single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d18e3-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="d18e3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d18e3-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="d18e3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d18e3-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="d18e3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d18e3-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d18e3-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d18e3-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="d18e3-118">Scenario description</span></span>
<span data-ttu-id="d18e3-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="d18e3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d18e3-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="d18e3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d18e3-121">Dodawanie Voyance z galerii hello</span><span class="sxs-lookup"><span data-stu-id="d18e3-121">Adding Voyance from hello gallery</span></span>
2. <span data-ttu-id="d18e3-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="d18e3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-voyance-from-hello-gallery"></a><span data-ttu-id="d18e3-123">Dodawanie Voyance z galerii hello</span><span class="sxs-lookup"><span data-stu-id="d18e3-123">Adding Voyance from hello gallery</span></span>
<span data-ttu-id="d18e3-124">tooconfigure hello integracji Voyance do usługi Azure AD, należy tooadd Voyance z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="d18e3-124">tooconfigure hello integration of Voyance into Azure AD, you need tooadd Voyance from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d18e3-125">**tooadd Voyance z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="d18e3-125">**tooadd Voyance from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d18e3-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="d18e3-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="d18e3-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="d18e3-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d18e3-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="d18e3-129">Then go too**All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. <span data-ttu-id="d18e3-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d18e3-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nowy przycisk aplikacji Hello][3]

4. <span data-ttu-id="d18e3-133">W polu wyszukiwania hello wpisz **Voyance**, wybierz pozycję **Voyance** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="d18e3-133">In hello search box, type **Voyance**, select  **Voyance**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![Voyance hello listy wyników](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d18e3-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d18e3-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="d18e3-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Voyance w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="d18e3-136">In this section, you configure and test Azure AD single sign-on with Voyance based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d18e3-137">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Voyance jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d18e3-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Voyance is tooa user in Azure AD.</span></span> <span data-ttu-id="d18e3-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Voyance musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="d18e3-138">In other words, a link relationship between an Azure AD user and hello related user in Voyance needs toobe established.</span></span>

<span data-ttu-id="d18e3-139">W Voyance, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="d18e3-139">In Voyance, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d18e3-140">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Voyance, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="d18e3-140">tooconfigure and test Azure AD single sign-on with Voyance, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d18e3-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="d18e3-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d18e3-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="d18e3-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d18e3-143">**[Tworzenie użytkownika testowego Voyance](#create-a-voyance-test-user)**  -toohave odpowiednikiem Simona Britta w Voyance, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d18e3-143">**[Create a Voyance test user](#create-a-voyance-test-user)** - toohave a counterpart of Britta Simon in Voyance that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d18e3-144">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d18e3-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d18e3-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="d18e3-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="d18e3-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d18e3-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="d18e3-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Voyance.</span><span class="sxs-lookup"><span data-stu-id="d18e3-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Voyance application.</span></span>

<span data-ttu-id="d18e3-148">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Voyance, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="d18e3-148">**tooconfigure Azure AD single sign-on with Voyance, perform hello following steps:**</span></span>

1. <span data-ttu-id="d18e3-149">W portalu Azure na powitania hello **Voyance** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="d18e3-149">In hello Azure portal, on hello **Voyance** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="d18e3-151">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d18e3-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_samlbase.png)

3. <span data-ttu-id="d18e3-153">Na powitania **Voyance domeny i adres URL** sekcji, wykonaj następujące kroki, jeśli chcesz, aby aplikacja hello tooconfigure w hello **IDP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="d18e3-153">On hello **Voyance Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Adresy URL i domeny Voyance pojedynczy informacje logowania dla dostawców tożsamości](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_url1.png)

    <span data-ttu-id="d18e3-155">a.</span><span class="sxs-lookup"><span data-stu-id="d18e3-155">a.</span></span> <span data-ttu-id="d18e3-156">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.nyansa.com`</span><span class="sxs-lookup"><span data-stu-id="d18e3-156">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.nyansa.com`</span></span>

    <span data-ttu-id="d18e3-157">b.</span><span class="sxs-lookup"><span data-stu-id="d18e3-157">b.</span></span> <span data-ttu-id="d18e3-158">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.nyansa.com/saml/create/`</span><span class="sxs-lookup"><span data-stu-id="d18e3-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.nyansa.com/saml/create/`</span></span>

4. <span data-ttu-id="d18e3-159">Sprawdź **Pokaż zaawansowane ustawienia adresu URL** i wykonywać powitania po kroku, jeśli chcesz, aby aplikacja hello tooconfigure w **SP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="d18e3-159">Check **Show advanced URL settings** and perform hello following step if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Adresy URL i domeny Voyance pojedynczy informacje logowania dla dostawcy](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_url2.png)

    <span data-ttu-id="d18e3-161">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.nyansa.com/`</span><span class="sxs-lookup"><span data-stu-id="d18e3-161">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.nyansa.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="d18e3-162">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="d18e3-162">These values are not real.</span></span> <span data-ttu-id="d18e3-163">Zaktualizować te wartości z hello rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="d18e3-163">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="d18e3-164">Skontaktuj się z [zespołem pomocy technicznej klienta Voyance](mailto:support@nyansa.com) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="d18e3-164">Contact [Voyance Client support team](mailto:support@nyansa.com) tooget these values.</span></span> 

5. <span data-ttu-id="d18e3-165">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="d18e3-165">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_certificate.png) 

6. <span data-ttu-id="d18e3-167">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d18e3-167">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-voyance-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="d18e3-169">Na powitania **konfiguracji Voyance** kliknij **skonfigurować Voyance** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="d18e3-169">On hello **Voyance Configuration** section, click **Configure Voyance** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="d18e3-170">Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="d18e3-170">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfiguracja Voyance](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_configure.png) 

8. <span data-ttu-id="d18e3-172">W oknie przeglądarki innej witryny sieci web, logowania jednokrotnego tooyour Voyance dzierżawy z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="d18e3-172">In a different web browser window, sign-on tooyour Voyance tenant as an administrator.</span></span>

9. <span data-ttu-id="d18e3-173">Przejdź toohello prawym górnym rogu paska nawigacyjnego hello i kliknij pozycję hello listy rozwijanej informacją "**University xyz**".</span><span class="sxs-lookup"><span data-stu-id="d18e3-173">Go toohello top right corner of hello navigation bar and click on hello drop-down that says "**Acme University**".</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej w aplikacji po stronie xyz University](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_001.png) 

10. <span data-ttu-id="d18e3-175">Kliknij przycisk "**ustawienia administratora**".</span><span class="sxs-lookup"><span data-stu-id="d18e3-175">Click "**Admin Settings**".</span></span>

    ![Konfigurowanie rejestracji jednokrotnej ustawieniami aplikacji po stronie administratora](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_002.png)

11. <span data-ttu-id="d18e3-177">Kliknij przycisk "**dostępu użytkownika**" kartę.</span><span class="sxs-lookup"><span data-stu-id="d18e3-177">Click "**User Access**" tab.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej na dostęp do aplikacji po stronie użytkownika](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_003.png)

12. <span data-ttu-id="d18e3-179">Kliknij przycisk hello "**wyłączeniu logowania jednokrotnego**" przycisk tooconfigure usługi Azure AD jako dostawca tożsamości przy użyciu SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="d18e3-179">Click hello "**SSO is disabled**" button tooconfigure Azure AD as an IdP using SAML 2.0.</span></span>

    ![Konfigurowanie jednego logowania w aplikacji po stronie rejestracji Jednokrotnej jest wyłączony przycisk](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_004.png)

13. <span data-ttu-id="d18e3-181">Przejdź za**SAML v2** sekcji i wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="d18e3-181">Go too**SAML v2** section and perform below steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej w aplikacji po stronie SAML v2](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_005.png)
    
    <span data-ttu-id="d18e3-183">a.</span><span class="sxs-lookup"><span data-stu-id="d18e3-183">a.</span></span> <span data-ttu-id="d18e3-184">Wybierz **włączone**.</span><span class="sxs-lookup"><span data-stu-id="d18e3-184">Select **Enabled**.</span></span>
    
    <span data-ttu-id="d18e3-185">b.</span><span class="sxs-lookup"><span data-stu-id="d18e3-185">b.</span></span> <span data-ttu-id="d18e3-186">Wklej **SAML pojedynczy znak na adres URL usługi**, która została skopiowana z hello portalu Azure do hello **adres URL logowania IdP** pole tekstowe.</span><span class="sxs-lookup"><span data-stu-id="d18e3-186">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal Into hello **IdP Login URL** textbox.</span></span>

    <span data-ttu-id="d18e3-187">c.</span><span class="sxs-lookup"><span data-stu-id="d18e3-187">c.</span></span> <span data-ttu-id="d18e3-188">Otwórz z pobranego certyfikatu szyfrowania Base64 w Notatniku hello kopiowania zawartości go do Schowka, a następnie wklej go toohello **IdP Cert** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="d18e3-188">Open your downloaded Base64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **IdP Cert** textbox.</span></span>
    
    <span data-ttu-id="d18e3-189">d.</span><span class="sxs-lookup"><span data-stu-id="d18e3-189">d.</span></span> <span data-ttu-id="d18e3-190">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="d18e3-190">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="d18e3-191">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="d18e3-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d18e3-192">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="d18e3-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d18e3-193">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d18e3-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d18e3-194">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d18e3-194">Create an Azure AD test user</span></span>

<span data-ttu-id="d18e3-195">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="d18e3-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="d18e3-197">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="d18e3-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d18e3-198">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="d18e3-198">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-voyance-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d18e3-200">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="d18e3-200">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-voyance-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d18e3-202">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d18e3-202">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![przycisk Dodaj Hello](./media/active-directory-saas-voyance-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d18e3-204">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="d18e3-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-voyance-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d18e3-206">a.</span><span class="sxs-lookup"><span data-stu-id="d18e3-206">a.</span></span> <span data-ttu-id="d18e3-207">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d18e3-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d18e3-208">b.</span><span class="sxs-lookup"><span data-stu-id="d18e3-208">b.</span></span> <span data-ttu-id="d18e3-209">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d18e3-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d18e3-210">c.</span><span class="sxs-lookup"><span data-stu-id="d18e3-210">c.</span></span> <span data-ttu-id="d18e3-211">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="d18e3-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d18e3-212">d.</span><span class="sxs-lookup"><span data-stu-id="d18e3-212">d.</span></span> <span data-ttu-id="d18e3-213">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d18e3-213">Click **Create**.</span></span>
 
### <a name="create-a-voyance-test-user"></a><span data-ttu-id="d18e3-214">Tworzenie użytkownika testowego Voyance</span><span class="sxs-lookup"><span data-stu-id="d18e3-214">Create a Voyance test user</span></span>

<span data-ttu-id="d18e3-215">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w Voyance.</span><span class="sxs-lookup"><span data-stu-id="d18e3-215">hello objective of this section is toocreate a user called Britta Simon in Voyance.</span></span> <span data-ttu-id="d18e3-216">Voyance obsługę w czasie, który jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="d18e3-216">Voyance supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="d18e3-217">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="d18e3-217">There is no action item for you in this section.</span></span> <span data-ttu-id="d18e3-218">Nowy użytkownik jest tworzona podczas próby tooaccess Voyance, jeśli go jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="d18e3-218">A new user is created during an attempt tooaccess Voyance if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="d18e3-219">Jeśli potrzebujesz ręcznie toocreate użytkownika, należy toocontact [zespołem pomocy technicznej Voyance](maiLto:support@nyansa.com).</span><span class="sxs-lookup"><span data-stu-id="d18e3-219">If you need toocreate a user manually, you need toocontact [Voyance support team](maiLto:support@nyansa.com).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="d18e3-220">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d18e3-220">Assign hello Azure AD test user</span></span>

<span data-ttu-id="d18e3-221">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooVoyance.</span><span class="sxs-lookup"><span data-stu-id="d18e3-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooVoyance.</span></span>

![Przypisanie roli użytkownika hello][200]

<span data-ttu-id="d18e3-223">**tooassign tooVoyance Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="d18e3-223">**tooassign Britta Simon tooVoyance, perform hello following steps:**</span></span>

1. <span data-ttu-id="d18e3-224">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="d18e3-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="d18e3-226">Z listy aplikacji hello wybierz **Voyance**.</span><span class="sxs-lookup"><span data-stu-id="d18e3-226">In hello applications list, select **Voyance**.</span></span>

    ![łącze Voyance Hello na liście aplikacji hello](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_app.png) 

3. <span data-ttu-id="d18e3-228">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="d18e3-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![łącze "Użytkownicy i grupy" Hello][202]

4. <span data-ttu-id="d18e3-230">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d18e3-230">Click **Add** button.</span></span> <span data-ttu-id="d18e3-231">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d18e3-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Okienko Dodaj przypisania Hello][203]

5. <span data-ttu-id="d18e3-233">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="d18e3-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d18e3-234">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d18e3-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d18e3-235">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d18e3-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="d18e3-236">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d18e3-236">Test single sign-on</span></span>

<span data-ttu-id="d18e3-237">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="d18e3-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d18e3-238">Po kliknięciu kafelka Voyance hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Voyance aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d18e3-238">When you click hello Voyance tile in hello Access Panel, you should get automatically signed-on tooyour Voyance application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d18e3-239">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="d18e3-239">Additional resources</span></span>

* [<span data-ttu-id="d18e3-240">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d18e3-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d18e3-241">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d18e3-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_203.png

