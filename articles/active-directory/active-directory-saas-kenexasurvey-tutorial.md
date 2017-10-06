---
title: "Samouczek: Azure Active Directory integrację ze IBM Kenexa ankiety | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i IBM Kenexa ankiety przedsiębiorstwa."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c7aac6da-f4bf-419e-9e1a-16b460641a52
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: cf7ed886b4418ac396ca7056827ee10fd7a19ef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ibm-kenexa-survey-enterprise"></a><span data-ttu-id="ce944-103">Samouczek: Azure Active Directory integrację ze IBM Kenexa ankiety</span><span class="sxs-lookup"><span data-stu-id="ce944-103">Tutorial: Azure Active Directory integration with IBM Kenexa Survey Enterprise</span></span>

<span data-ttu-id="ce944-104">Z tego samouczka, dowiesz się, jak toointegrate IBM Kenexa ankiety przedsiębiorstwa w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ce944-104">In this tutorial, you learn how toointegrate IBM Kenexa Survey Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ce944-105">Integrowanie IBM Kenexa ankiety przedsiębiorstwa z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="ce944-105">Integrating IBM Kenexa Survey Enterprise with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ce944-106">Można kontrolować w usłudze Azure AD, kto ma dostęp tooIBM Kenexa ankiety przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="ce944-106">You can control in Azure AD who has access tooIBM Kenexa Survey Enterprise.</span></span>
- <span data-ttu-id="ce944-107">Tooautomatically użytkowników logowania tooIBM Kenexa ankiety przedsiębiorstwa można włączyć za pomocą rejestracji jednokrotnej (SSO) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ce944-107">You can enable your users tooautomatically sign in tooIBM Kenexa Survey Enterprise by using single sign-on (SSO) with their Azure AD accounts.</span></span>
- <span data-ttu-id="ce944-108">Możesz zarządzać kont w jednej centralnej lokalizacji: hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ce944-108">You can manage your accounts in one central location: hello Azure portal.</span></span>

<span data-ttu-id="ce944-109">Jeśli chcesz tooknow więcej informacji na temat oprogramowania jako usługa (SaaS) integracji aplikacji z usługą Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ce944-109">If you want tooknow more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ce944-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ce944-110">Prerequisites</span></span>

<span data-ttu-id="ce944-111">tooconfigure integracji usługi Azure AD z IBM Kenexa ankiety Enterprise należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="ce944-111">tooconfigure Azure AD integration with IBM Kenexa Survey Enterprise, you need hello following items:</span></span>

- <span data-ttu-id="ce944-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce944-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ce944-113">Włączone IBM Kenexa ankiety Enterprise SSO subskrypcji</span><span class="sxs-lookup"><span data-stu-id="ce944-113">An IBM Kenexa Survey Enterprise SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ce944-114">Podczas testowania czynności hello w tym samouczku, firma Microsoft zaleca, nie używaj do środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="ce944-114">When you test hello steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="ce944-115">kroki hello tootest w tym samouczku, wykonaj te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="ce944-115">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="ce944-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="ce944-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ce944-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ce944-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ce944-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="ce944-118">Scenario description</span></span>
<span data-ttu-id="ce944-119">W tym samouczku można przetestować logowania jednokrotnego programu Azure AD w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="ce944-119">In this tutorial, you test Azure AD SSO in a test environment.</span></span> <span data-ttu-id="ce944-120">Scenariusz Hello opisane w samouczku hello składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="ce944-120">hello scenario outlined in hello tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="ce944-121">Dodawanie IBM Kenexa ankiety przedsiębiorstwa z galerii hello</span><span class="sxs-lookup"><span data-stu-id="ce944-121">Adding IBM Kenexa Survey Enterprise from hello gallery</span></span>
* <span data-ttu-id="ce944-122">Konfigurowanie i testowania logowania jednokrotnego programu Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce944-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-ibm-kenexa-survey-enterprise-from-hello-gallery"></a><span data-ttu-id="ce944-123">Dodaj IBM Kenexa ankiety przedsiębiorstwa z galerii hello</span><span class="sxs-lookup"><span data-stu-id="ce944-123">Add IBM Kenexa Survey Enterprise from hello gallery</span></span>
<span data-ttu-id="ce944-124">tooconfigure hello integracji IBM Kenexa ankiety przedsiębiorstwa w usłudze Azure AD, Dodaj IBM Kenexa ankiety przedsiębiorstwa z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="ce944-124">tooconfigure hello integration of IBM Kenexa Survey Enterprise into Azure AD, add IBM Kenexa Survey Enterprise from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ce944-125">tooadd IBM Kenexa ankiety przedsiębiorstwa z galerii hello hello następujące:</span><span class="sxs-lookup"><span data-stu-id="ce944-125">tooadd IBM Kenexa Survey Enterprise from hello gallery, do hello following:</span></span>

1. <span data-ttu-id="ce944-126">W hello [portalu Azure](https://portal.azure.com), w lewym okienku hello, kliknij przycisk hello **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ce944-126">In hello [Azure portal](https://portal.azure.com), in hello left pane, click hello **Azure Active Directory** button.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="ce944-128">Wybierz **aplikacje dla przedsiębiorstw**, a następnie wybierz **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ce944-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. <span data-ttu-id="ce944-130">tooadd aplikacji, kliknij przycisk hello **nowej aplikacji** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ce944-130">tooadd an application, click hello **New application** button.</span></span>

    ![Nowy przycisk aplikacji Hello][3]

4. <span data-ttu-id="ce944-132">W polu wyszukiwania hello wpisz **IBM Kenexa ankiety Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="ce944-132">In hello search box, type **IBM Kenexa Survey Enterprise**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_search.png)

5. <span data-ttu-id="ce944-134">Hello listy wyników, wybierz **IBM Kenexa ankiety Enterprise**, a następnie kliknij przycisk hello **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="ce944-134">In hello results list, select **IBM Kenexa Survey Enterprise**, and then click hello **Add** button tooadd hello application.</span></span>

    ![IBM Kenexa ankiety Enterprise hello listy wyników](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ce944-136">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ce944-136">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="ce944-137">W tej sekcji Konfiguracja i testowanie logowania jednokrotnego AD Azure z przedsiębiorstwem ankiety Kenexa IBM oparte na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="ce944-137">In this section, you configure and test Azure AD SSO with IBM Kenexa Survey Enterprise based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ce944-138">Aby toowork logowania jednokrotnego usługi Azure AD musi tooidentify hello IBM Kenexa ankiety Enterprise użytkownika odpowiednikiem w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ce944-138">For SSO toowork, Azure AD needs tooidentify hello IBM Kenexa Survey Enterprise user counterpart in Azure AD.</span></span> <span data-ttu-id="ce944-139">Innymi słowy usługi Azure AD ustanowić relację łącza między użytkownika usługi Azure AD i powiązanych użytkowników w przedsiębiorstwie ankiety Kenexa IBM.</span><span class="sxs-lookup"><span data-stu-id="ce944-139">In other words, Azure AD must establish a link relationship between an Azure AD user and a related user in IBM Kenexa Survey Enterprise.</span></span>

<span data-ttu-id="ce944-140">tooestablish hello łącze relację, przypisać wartość hello hello **nazwy użytkownika** w przedsiębiorstwie ankiety Kenexa IBM jako wartość hello hello **Username** w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ce944-140">tooestablish hello link relationship, assign hello value of hello **user name** in IBM Kenexa Survey Enterprise as hello value of hello **Username** in Azure AD.</span></span>

<span data-ttu-id="ce944-141">tooconfigure i Azure AD SSO z IBM Kenexa ankiety przedsiębiorstwa, pełny test hello bloków konstrukcyjnych w hello w dwóch następnych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="ce944-141">tooconfigure and test Azure AD SSO with IBM Kenexa Survey Enterprise, complete hello building blocks in hello next two sections.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="ce944-142">Konfigurowanie usługi Azure AD logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="ce944-142">Configure Azure AD SSO</span></span>

<span data-ttu-id="ce944-143">W tej sekcji włączenia funkcji logowania jednokrotnego usługi Azure AD w hello portalu Azure i skonfiguruj logowania jednokrotnego w aplikacji IBM Kenexa ankiety przedsiębiorstwa, wykonując następujące hello:</span><span class="sxs-lookup"><span data-stu-id="ce944-143">In this section, you enable Azure AD SSO in hello Azure portal and configure SSO in your IBM Kenexa Survey Enterprise application by doing hello following:</span></span>

1. <span data-ttu-id="ce944-144">W portalu Azure na powitania hello **IBM Kenexa ankiety Enterprise** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="ce944-144">In hello Azure portal, on hello **IBM Kenexa Survey Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![IBM Kenexa ankiety Enterprise Konfigurowanie logowania jednokrotnego łącza][4]

2. <span data-ttu-id="ce944-146">W hello **logowanie jednokrotne** okno dialogowe, w hello **tryb** wybierz opcję **na języku SAML logowania jednokrotnego** tooenable logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="ce944-146">In hello **Single sign-on** dialog box, in hello **Mode** box, select **SAML-based Sign-on** tooenable SSO.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_samlbase.png)

3. <span data-ttu-id="ce944-148">W hello **IBM Kenexa ankiety Enterprise domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="ce944-148">In hello **IBM Kenexa Survey Enterprise Domain and URLs** section, perform hello following steps:</span></span>

    ![IBM Kenexa ankiety Enterprise domeny i adres URL z jednym informacje logowania jednokrotnego](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_url.png)

    <span data-ttu-id="ce944-150">a.</span><span class="sxs-lookup"><span data-stu-id="ce944-150">a.</span></span> <span data-ttu-id="ce944-151">W hello **identyfikator** tekstowym, wpisz adres URL z hello następującego wzorca:`https://surveys.kenexa.com/<companycode>`</span><span class="sxs-lookup"><span data-stu-id="ce944-151">In hello **Identifier** textbox, type a URL with hello following pattern: `https://surveys.kenexa.com/<companycode>`</span></span>

    <span data-ttu-id="ce944-152">b.</span><span class="sxs-lookup"><span data-stu-id="ce944-152">b.</span></span> <span data-ttu-id="ce944-153">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL z hello następującego wzorca:`https://surveys.kenexa.com/<companycode>/tools/sso.asp`</span><span class="sxs-lookup"><span data-stu-id="ce944-153">In hello **Reply URL** textbox, type a URL with hello following pattern: `https://surveys.kenexa.com/<companycode>/tools/sso.asp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ce944-154">Witaj poprzedniej wartości nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="ce944-154">hello preceding values are not real.</span></span> <span data-ttu-id="ce944-155">Można aktualizować hello rzeczywisty identyfikator i adres URL odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="ce944-155">Update them with hello actual identifier and reply URL.</span></span> <span data-ttu-id="ce944-156">tooobtain hello wartości rzeczywistych, skontaktuj się z pomocą hello [zespołem pomocy technicznej Enterprise ankiety Kenexa IBM](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="ce944-156">tooobtain hello actual values, contact hello [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span>

4. <span data-ttu-id="ce944-157">W obszarze **certyfikat podpisywania SAML**, kliknij przycisk **certyfikatu (Base64)**, a następnie zapisz hello certyfikatu pliku tooyour komputera.</span><span class="sxs-lookup"><span data-stu-id="ce944-157">Under **SAML Signing Certificate**, click **Certificate (Base64)**, and then save hello certificate file tooyour computer.</span></span>

    ![Witaj link do pobierania certyfikatu (Base64)](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_certificate.png) 

    <span data-ttu-id="ce944-159">Hello aplikacja całościowa ankiety Kenexa IBM oczekuje potwierdzeń zabezpieczeń potwierdzenia Markup Language (SAML) hello tooreceive w określonym formacie, który wymaga możesz tooadd atrybutu niestandardowego mapowania toohello konfiguracji z atrybutów tokenu SAML.</span><span class="sxs-lookup"><span data-stu-id="ce944-159">hello IBM Kenexa Survey Enterprise application expects tooreceive hello Security Assertions Markup Language (SAML) assertions in a specific format, which requires you tooadd custom attribute mappings toohello configuration of your SAML token attributes.</span></span> <span data-ttu-id="ce944-160">Witaj wartość hello oświadczenia identyfikatora użytkownika w odpowiedzi hello musi odpowiadać hello identyfikator logowania jednokrotnego, który jest skonfigurowany w systemie Kenexa hello.</span><span class="sxs-lookup"><span data-stu-id="ce944-160">hello value of hello user-identifier claim in hello response must match hello SSO ID that's configured in hello Kenexa system.</span></span> <span data-ttu-id="ce944-161">toomap hello identyfikator odpowiedniego użytkownika w organizacji jako SSO Internet Datagram Protocol (IDP), Praca z hello [zespołem pomocy technicznej Enterprise ankiety Kenexa IBM](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="ce944-161">toomap hello appropriate user identifier in your organization as SSO Internet Datagram Protocol (IDP), work with hello [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span> 

    <span data-ttu-id="ce944-162">Domyślnie usługi Azure AD Ustawia identyfikator użytkownika hello jako wartość głównej nazwy (UPN) użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="ce944-162">By default, Azure AD sets hello user identifier as hello user principal name (UPN) value.</span></span> <span data-ttu-id="ce944-163">Można zmienić tę wartość na powitania **atrybutu** karcie, jak pokazano w hello następującego zrzutu ekranu.</span><span class="sxs-lookup"><span data-stu-id="ce944-163">You can change this value on hello **Attribute** tab, as shown in hello following screenshot.</span></span> <span data-ttu-id="ce944-164">Integracja Hello działa tylko po zakończeniu hello mapowania poprawnie.</span><span class="sxs-lookup"><span data-stu-id="ce944-164">hello integration works only after you've completed hello mapping correctly.</span></span>
    
    ![okno dialogowe Hello atrybutów użytkownika](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_attribute.png) 

5. <span data-ttu-id="ce944-166">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="ce944-166">Click **Save**.</span></span>

    ![Witaj skonfigurować logowanie jednokrotne przycisk zapisywania](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ce944-168">tooopen hello **Konfigurowanie logowania jednokrotnego** okna, w obszarze **konfiguracja dla przedsiębiorstw ankiety Kenexa IBM**, kliknij przycisk **skonfigurować IBM Kenexa ankiety Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="ce944-168">tooopen hello **Configure sign-on** window, under **IBM Kenexa Survey Enterprise Configuration**, click **Configure IBM Kenexa Survey Enterprise**.</span></span> 
 
    ![łącze skonfigurować IBM Kenexa ankiety Enterprise Hello](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_configure.png)

7. <span data-ttu-id="ce944-170">Kopiuj hello **Sign-Out adres URL**, **SAML identyfikator jednostki**, i **SAML pojedynczy znak na adres URL usługi** wartości z hello **krótki przewodnik** sekcji.</span><span class="sxs-lookup"><span data-stu-id="ce944-170">Copy hello **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values from hello **Quick Reference** section.</span></span>

8. <span data-ttu-id="ce944-171">W hello **Konfigurowanie logowania jednokrotnego** okna, w obszarze **krótkimi opisami**, hello kopiowania **Sign-Out adres URL**, **identyfikator jednostki SAML**, i  **SAML pojedynczy znak na adres URL usługi** wartości.</span><span class="sxs-lookup"><span data-stu-id="ce944-171">In hello **Configure sign-on** window, under **Quick Reference**, copy hello **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values.</span></span>

9. <span data-ttu-id="ce944-172">tooconfigure logowania jednokrotnego na powitania **IBM Kenexa ankiety Enterprise** po stronie, Wyślij hello pobrane **certyfikatu (Base64)**, **Sign-Out URL**, **identyfikator jednostki SAML**, i **SAML pojedynczy znak na adres URL usługi** wartości toohello [zespołem pomocy technicznej Enterprise ankiety Kenexa IBM](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="ce944-172">tooconfigure SSO on hello **IBM Kenexa Survey Enterprise** side, send hello downloaded **Certificate (Base64)**, **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values toohello [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span>

> [!TIP]
> <span data-ttu-id="ce944-173">Może się odwoływać tooa zwięzły wersji tych instrukcji w hello [portalu Azure](https://portal.azure.com) podczas konfigurowania aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="ce944-173">You can refer tooa concise version of these instructions in hello [Azure portal](https://portal.azure.com) while you are setting up hello app.</span></span> <span data-ttu-id="ce944-174">Po dodaniu aplikacji hello z hello **usługi Active Directory** > **aplikacje dla przedsiębiorstw** po prostu kliknij hello **logowanie jednokrotne** karcie, a następnie przejść Witaj osadzonych dokumentacji za pośrednictwem hello **konfiguracji** sekcji na końcu hello.</span><span class="sxs-lookup"><span data-stu-id="ce944-174">After you add hello app from hello **Active Directory** > **Enterprise Applications** section, simply click hello **single sign-on** tab, and then access hello embedded documentation through hello **Configuration** section at hello end.</span></span> <span data-ttu-id="ce944-175">toolearn więcej informacji na temat hello osadzonych dokumentacji funkcji, zobacz [usługi Azure AD osadzonych dokumentacji](https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="ce944-175">toolearn more about hello embedded documentation feature, see [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ce944-176">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce944-176">Create an Azure AD test user</span></span>
<span data-ttu-id="ce944-177">W tej sekcji możesz tworzyć użytkownika testowego Simona Britta w hello portalu Azure, wykonując następujące hello:</span><span class="sxs-lookup"><span data-stu-id="ce944-177">In this section, you create test user Britta Simon in hello Azure portal by doing hello following:</span></span>

![Tworzenie użytkownika testowego usługi Azure AD][100]

1. <span data-ttu-id="ce944-179">W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ce944-179">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ce944-181">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="ce944-181">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>
    
    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ce944-183">Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="ce944-183">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>
 
    ![przycisk Dodaj Hello](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ce944-185">W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="ce944-185">In hello **User** dialog box, perform hello following steps:</span></span>
 
    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ce944-187">a.</span><span class="sxs-lookup"><span data-stu-id="ce944-187">a.</span></span> <span data-ttu-id="ce944-188">W hello **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ce944-188">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ce944-189">b.</span><span class="sxs-lookup"><span data-stu-id="ce944-189">b.</span></span> <span data-ttu-id="ce944-190">W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="ce944-190">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="ce944-191">c.</span><span class="sxs-lookup"><span data-stu-id="ce944-191">c.</span></span> <span data-ttu-id="ce944-192">Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="ce944-192">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="ce944-193">d.</span><span class="sxs-lookup"><span data-stu-id="ce944-193">d.</span></span> <span data-ttu-id="ce944-194">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="ce944-194">Click **Create**.</span></span>
 
### <a name="create-an-ibm-kenexa-survey-enterprise-test-user"></a><span data-ttu-id="ce944-195">Tworzenie użytkownika testowego IBM Kenexa ankiety Enterprise</span><span class="sxs-lookup"><span data-stu-id="ce944-195">Create an IBM Kenexa Survey Enterprise test user</span></span>

<span data-ttu-id="ce944-196">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w przedsiębiorstwie ankiety Kenexa IBM.</span><span class="sxs-lookup"><span data-stu-id="ce944-196">In this section, you create a user called Britta Simon in IBM Kenexa Survey Enterprise.</span></span> 

<span data-ttu-id="ce944-197">toocreate użytkowników w hello systemu IBM Kenexa ankiety przedsiębiorstwa i mapy hello identyfikator logowania jednokrotnego dla nich, możesz pracować z hello [zespołem pomocy technicznej Enterprise ankiety Kenexa IBM](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="ce944-197">toocreate users in hello IBM Kenexa Survey Enterprise system and map hello SSO ID for them, you can work with hello [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span> <span data-ttu-id="ce944-198">Ta wartość Identyfikatora logowania jednokrotnego również musi być zamapowany toohello wartość identyfikatora użytkownika z usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ce944-198">This SSO ID value should also be mapped toohello user identifier value from Azure AD.</span></span> <span data-ttu-id="ce944-199">Można zmienić to ustawienie domyślne na powitania **atrybutu** kartę.</span><span class="sxs-lookup"><span data-stu-id="ce944-199">You can change this default setting on hello **Attribute** tab.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="ce944-200">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce944-200">Assign hello Azure AD test user</span></span>

<span data-ttu-id="ce944-201">W tej sekcji możesz włączyć użytkownika toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooIBM Kenexa ankiety Enterprise.</span><span class="sxs-lookup"><span data-stu-id="ce944-201">In this section, you enable user Britta Simon toouse Azure SSO by granting access tooIBM Kenexa Survey Enterprise.</span></span>

![Przypisanie roli użytkownika hello][200] 

<span data-ttu-id="ce944-203">tooassign użytkownika tooIBM Simona Britta Kenexa Enterprise ankiety, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="ce944-203">tooassign user Britta Simon tooIBM Kenexa Survey Enterprise, do hello following:</span></span>

1. <span data-ttu-id="ce944-204">Hello portalu Azure, otwórz hello **aplikacji** wyświetlić, przejdź toohello **katalogu** widok, wybierz opcję **aplikacje dla przedsiębiorstw**, a następnie kliknij przycisk **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ce944-204">In hello Azure portal, open hello **Applications** view, go toohello **Directory** view, select **Enterprise applications**, and then click **All applications**.</span></span>

    ![Witaj, "Aplikacje przedsiębiorstwa" i "Wszystkie aplikacje" łącza][201] 

2. <span data-ttu-id="ce944-206">W hello **aplikacji** listy, wybierz **IBM Kenexa ankiety Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="ce944-206">In hello **Applications** list, select **IBM Kenexa Survey Enterprise**.</span></span>

    ![łącze IBM Kenexa ankiety Enterprise Hello na liście aplikacji hello](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_app.png) 

3. <span data-ttu-id="ce944-208">W okienku po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="ce944-208">In hello left pane, click **Users and groups**.</span></span>

    ![łącze "Użytkownicy i grupy" Hello][202] 

4. <span data-ttu-id="ce944-210">Kliknij przycisk hello **Dodaj** przycisk, a następnie w hello **Dodaj przydziału** okienku wybierz **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="ce944-210">Click hello **Add** button and then, in hello **Add Assignment** pane, select **Users and groups**.</span></span>

    ![Okienko Dodaj przypisania Hello][203]

5. <span data-ttu-id="ce944-212">W hello **użytkowników i grup** okno dialogowe, w hello **użytkowników** listy, wybierz **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="ce944-212">In hello **Users and groups** dialog box, in hello **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="ce944-213">W hello **użytkowników i grup** okna dialogowego kliknij hello **wybierz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ce944-213">In hello **Users and groups** dialog box, click hello **Select** button.</span></span>

7. <span data-ttu-id="ce944-214">W hello **Dodaj przydziału** okna dialogowego kliknij hello **przypisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ce944-214">In hello **Add Assignment** dialog box, click hello **Assign** button.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="ce944-215">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ce944-215">Test single sign-on</span></span>

<span data-ttu-id="ce944-216">W tej sekcji możesz przetestować konfigurację programu Azure AD z logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="ce944-216">In this section, you test your Azure AD SSO configuration by using hello Access Panel.</span></span>

<span data-ttu-id="ce944-217">Po kliknięciu hello **IBM Kenexa ankiety Enterprise** kafelka w hello Panel dostępu, powinien być automatycznie zalogowano tooyour aplikacja całościowa ankiety Kenexa IBM.</span><span class="sxs-lookup"><span data-stu-id="ce944-217">When you click hello **IBM Kenexa Survey Enterprise** tile in hello Access Panel, you should be automatically signed in tooyour IBM Kenexa Survey Enterprise application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ce944-218">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="ce944-218">Additional resources</span></span>

* [<span data-ttu-id="ce944-219">Lista samouczków dotyczących toointegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ce944-219">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ce944-220">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ce944-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_203.png

 
