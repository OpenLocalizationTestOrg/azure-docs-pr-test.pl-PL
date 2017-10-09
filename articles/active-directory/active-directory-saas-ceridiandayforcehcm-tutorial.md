---
title: 'Samouczek: Integracji Azure Active Directory z Ceridian Dayforce HCM | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Ceridian Dayforce HCM."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 7adf1eb3-d063-45d6-96a8-fd53b329b3f3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 4d72f29b4e5e30ef8881806d789f6676fc541e2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ceridian-dayforce-hcm"></a><span data-ttu-id="33e47-103">Samouczek: Integracji Azure Active Directory z Ceridian Dayforce HCM</span><span class="sxs-lookup"><span data-stu-id="33e47-103">Tutorial: Azure Active Directory integration with Ceridian Dayforce HCM</span></span>

<span data-ttu-id="33e47-104">Z tego samouczka, dowiesz się, jak toointegrate HCM Dayforce Ceridian w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="33e47-104">In this tutorial, you learn how toointegrate Ceridian Dayforce HCM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="33e47-105">Integracja z usługą Azure AD Ceridian Dayforce HCM zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="33e47-105">Integrating Ceridian Dayforce HCM with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="33e47-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooCeridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="33e47-106">You can control in Azure AD who has access tooCeridian Dayforce HCM.</span></span>
- <span data-ttu-id="33e47-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooCeridian HCM Dayforce (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="33e47-107">You can enable your users tooautomatically get signed-on tooCeridian Dayforce HCM (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="33e47-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="33e47-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="33e47-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="33e47-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="33e47-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="33e47-110">Prerequisites</span></span>

<span data-ttu-id="33e47-111">tooconfigure integracji usługi Azure AD z Ceridian Dayforce HCM, należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="33e47-111">tooconfigure Azure AD integration with Ceridian Dayforce HCM, you need hello following items:</span></span>

- <span data-ttu-id="33e47-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="33e47-112">An Azure AD subscription</span></span>
- <span data-ttu-id="33e47-113">Ceridian Dayforce HCM jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="33e47-113">A Ceridian Dayforce HCM single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="33e47-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="33e47-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="33e47-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="33e47-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="33e47-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="33e47-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="33e47-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="33e47-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="33e47-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="33e47-118">Scenario description</span></span>
<span data-ttu-id="33e47-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="33e47-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="33e47-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="33e47-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="33e47-121">Dodawanie Ceridian Dayforce HCM z galerii hello</span><span class="sxs-lookup"><span data-stu-id="33e47-121">Adding Ceridian Dayforce HCM from hello gallery</span></span>
2. <span data-ttu-id="33e47-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="33e47-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ceridian-dayforce-hcm-from-hello-gallery"></a><span data-ttu-id="33e47-123">Dodawanie Ceridian Dayforce HCM z galerii hello</span><span class="sxs-lookup"><span data-stu-id="33e47-123">Adding Ceridian Dayforce HCM from hello gallery</span></span>
<span data-ttu-id="33e47-124">tooconfigure hello integracji Ceridian Dayforce HCM do usługi Azure AD, należy tooadd Ceridian Dayforce HCM z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="33e47-124">tooconfigure hello integration of Ceridian Dayforce HCM into Azure AD, you need tooadd Ceridian Dayforce HCM from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="33e47-125">**tooadd Ceridian Dayforce HCM z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="33e47-125">**tooadd Ceridian Dayforce HCM from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="33e47-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="33e47-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="33e47-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="33e47-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="33e47-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="33e47-129">Then go too**All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. <span data-ttu-id="33e47-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="33e47-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nowy przycisk aplikacji Hello][3]

4. <span data-ttu-id="33e47-133">W polu wyszukiwania hello wpisz **Ceridian Dayforce HCM**, wybierz pozycję **Ceridian Dayforce HCM** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="33e47-133">In hello search box, type **Ceridian Dayforce HCM**, select **Ceridian Dayforce HCM** from result panel then click **Add** button tooadd hello application.</span></span>

    ![HCM Dayforce Ceridian hello listy wyników](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="33e47-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="33e47-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="33e47-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z HCM Dayforce Ceridian w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="33e47-136">In this section, you configure and test Azure AD single sign-on with Ceridian Dayforce HCM based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="33e47-137">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Ceridian Dayforce HCM jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="33e47-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Ceridian Dayforce HCM is tooa user in Azure AD.</span></span> <span data-ttu-id="33e47-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Ceridian Dayforce HCM musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="33e47-138">In other words, a link relationship between an Azure AD user and hello related user in Ceridian Dayforce HCM needs toobe established.</span></span>

<span data-ttu-id="33e47-139">W Ceridian Dayforce HCM, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="33e47-139">In Ceridian Dayforce HCM, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="33e47-140">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Ceridian Dayforce HCM, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="33e47-140">tooconfigure and test Azure AD single sign-on with Ceridian Dayforce HCM, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="33e47-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="33e47-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="33e47-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="33e47-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="33e47-143">**[Tworzenie użytkownika testowego Ceridian Dayforce HCM](#create-a-ceridian-dayforce-hcm-test-user)**  -toohave odpowiednikiem Simona Britta w Ceridian Dayforce HCM, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="33e47-143">**[Create a Ceridian Dayforce HCM test user](#create-a-ceridian-dayforce-hcm-test-user)** - toohave a counterpart of Britta Simon in Ceridian Dayforce HCM that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="33e47-144">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="33e47-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="33e47-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="33e47-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="33e47-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="33e47-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="33e47-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="33e47-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Ceridian Dayforce HCM application.</span></span>

<span data-ttu-id="33e47-148">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Ceridian Dayforce HCM, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="33e47-148">**tooconfigure Azure AD single sign-on with Ceridian Dayforce HCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="33e47-149">W portalu Azure na powitania hello **Ceridian Dayforce HCM** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="33e47-149">In hello Azure portal, on hello **Ceridian Dayforce HCM** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="33e47-151">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="33e47-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_samlbase.png)

3. <span data-ttu-id="33e47-153">Na powitania **Ceridian Dayforce HCM domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="33e47-153">On hello **Ceridian Dayforce HCM Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_url.png)
    
    <span data-ttu-id="33e47-155">a.</span><span class="sxs-lookup"><span data-stu-id="33e47-155">a.</span></span> <span data-ttu-id="33e47-156">W hello **na adres URL logowania** pole tekstowe, wprowadź adres URL hello używany przez Twoje użytkowników toosign na tooyour Ceridian Dayforce HCM aplikacji.</span><span class="sxs-lookup"><span data-stu-id="33e47-156">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour Ceridian Dayforce HCM application.</span></span>
    
    | <span data-ttu-id="33e47-157">Środowisko</span><span class="sxs-lookup"><span data-stu-id="33e47-157">Environment</span></span> | <span data-ttu-id="33e47-158">ADRES URL</span><span class="sxs-lookup"><span data-stu-id="33e47-158">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="33e47-159">W środowisku produkcyjnym</span><span class="sxs-lookup"><span data-stu-id="33e47-159">For production</span></span> | `https://sso.dayforcehcm.com/<DayforcehcmNamespace>` |
    | <span data-ttu-id="33e47-160">Dla testu</span><span class="sxs-lookup"><span data-stu-id="33e47-160">For test</span></span> | `https://ssotest.dayforcehcm.com/<DayforcehcmNamespace>` |
    
    <span data-ttu-id="33e47-161">b.</span><span class="sxs-lookup"><span data-stu-id="33e47-161">b.</span></span> <span data-ttu-id="33e47-162">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="33e47-162">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    
    | <span data-ttu-id="33e47-163">Środowisko</span><span class="sxs-lookup"><span data-stu-id="33e47-163">Environment</span></span> | <span data-ttu-id="33e47-164">ADRES URL</span><span class="sxs-lookup"><span data-stu-id="33e47-164">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="33e47-165">W środowisku produkcyjnym</span><span class="sxs-lookup"><span data-stu-id="33e47-165">For production</span></span> | `https://ncpingfederate.dayforcehcm.com/sp` |
    | <span data-ttu-id="33e47-166">Dla testu</span><span class="sxs-lookup"><span data-stu-id="33e47-166">For test</span></span> | `https://fs-test.dayforcehcm.com/sp` |
    
    <span data-ttu-id="33e47-167">c.</span><span class="sxs-lookup"><span data-stu-id="33e47-167">c.</span></span> <span data-ttu-id="33e47-168">W hello **adres URL odpowiedzi** pole tekstowe, wprowadź adres URL hello używane przez usługi Azure AD toopost hello odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="33e47-168">In hello **Reply URL** textbox, type hello URL used by Azure AD toopost hello response.</span></span>
    
    | <span data-ttu-id="33e47-169">Środowisko</span><span class="sxs-lookup"><span data-stu-id="33e47-169">Environment</span></span> | <span data-ttu-id="33e47-170">ADRES URL</span><span class="sxs-lookup"><span data-stu-id="33e47-170">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="33e47-171">W środowisku produkcyjnym</span><span class="sxs-lookup"><span data-stu-id="33e47-171">For production</span></span> | `https://ncpingfederate.dayforcehcm.com/sp/ACS.saml2` |
    | <span data-ttu-id="33e47-172">Dla testu</span><span class="sxs-lookup"><span data-stu-id="33e47-172">For test</span></span> | `https://fs-test.dayforcehcm.com/sp/ACS.saml2` |
    
    > [!NOTE] 
    > <span data-ttu-id="33e47-173">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="33e47-173">These values are not real.</span></span> <span data-ttu-id="33e47-174">Zaktualizować te wartości z hello rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="33e47-174">Update these values with hello actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="33e47-175">Skontaktuj się z [zespołem pomocy technicznej klienta HCM Dayforce Ceridian](https://www.ceridian.com/contact-us/index.html) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="33e47-175">Contact [Ceridian Dayforce HCM Client support team](https://www.ceridian.com/contact-us/index.html) tooget these values.</span></span>

4. <span data-ttu-id="33e47-176">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="33e47-176">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_certificate.png) 

5. <span data-ttu-id="33e47-178">Aplikacja Ceridian Dayforce HCM oczekuje potwierdzenia SAML hello w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="33e47-178">Your Ceridian Dayforce HCM application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="33e47-179">Praca z [zespołem pomocy technicznej Ceridian Dayforce HCM](https://www.ceridian.com/contact-us/index.html) pierwszy identyfikator użytkownika hello tooidentify.</span><span class="sxs-lookup"><span data-stu-id="33e47-179">Work with [Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html) first tooidentify hello correct user identifier.</span></span> <span data-ttu-id="33e47-180">Firma Microsoft zaleca używanie hello **"name"** atrybut jako identyfikator użytkownika.</span><span class="sxs-lookup"><span data-stu-id="33e47-180">Microsoft recommends using hello **"name"** attribute as user identifier.</span></span> <span data-ttu-id="33e47-181">Można zarządzać hello wartości tych atrybutów z hello **atrybuty użytkownika** sekcji na stronie integracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="33e47-181">You can manage hello values of these attributes from hello **User Attributes** section on application integration page.</span></span> <span data-ttu-id="33e47-182">powitania po zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="33e47-182">hello following screenshot shows an example for this.</span></span>  

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_07.png)

6. <span data-ttu-id="33e47-184">W hello **atrybuty użytkownika** sekcji na powitania **logowanie jednokrotne** okna dialogowego, skonfiguruj atrybut tokenu SAML, jak pokazano w powyższy obraz powitania i wykonywać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="33e47-184">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="33e47-185">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="33e47-185">Attribute Name</span></span>  | <span data-ttu-id="33e47-186">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="33e47-186">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    | <span data-ttu-id="33e47-187">name</span><span class="sxs-lookup"><span data-stu-id="33e47-187">name</span></span>  | <span data-ttu-id="33e47-188">User.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="33e47-188">user.extensionattribute2</span></span> |    

    <span data-ttu-id="33e47-189">a.</span><span class="sxs-lookup"><span data-stu-id="33e47-189">a.</span></span> <span data-ttu-id="33e47-190">Kliknij przycisk **Dodaj atrybut** tooopen hello **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="33e47-190">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_attribute_04.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="33e47-193">b.</span><span class="sxs-lookup"><span data-stu-id="33e47-193">b.</span></span> <span data-ttu-id="33e47-194">W hello **nazwa** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="33e47-194">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="33e47-195">c.</span><span class="sxs-lookup"><span data-stu-id="33e47-195">c.</span></span> <span data-ttu-id="33e47-196">W hello **wartość** listy, wybierz hello atrybut użytkownika ma toouse implementacji.</span><span class="sxs-lookup"><span data-stu-id="33e47-196">In hello **Value** list, select hello user attribute you want toouse for your implementation.</span></span>
    <span data-ttu-id="33e47-197">Na przykład, jeśli mają hello toouse identyfikator pracownika jako identyfikator unikatowy użytkownika, a wartość atrybutu hello są przechowywane w hello ExtensionAttribute2, następnie wybierz **user.extensionattribute2**.</span><span class="sxs-lookup"><span data-stu-id="33e47-197">For example, if you want toouse hello EmployeeID as unique user identifier and you have stored hello attribute value in hello ExtensionAttribute2, then select **user.extensionattribute2**.</span></span>
    
    <span data-ttu-id="33e47-198">d.</span><span class="sxs-lookup"><span data-stu-id="33e47-198">d.</span></span> <span data-ttu-id="33e47-199">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="33e47-199">Click **Ok**.</span></span>

7. <span data-ttu-id="33e47-200">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="33e47-200">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="33e47-202">Na powitania **Ceridian Dayforce HCM konfiguracji** kliknij **skonfigurować HCM Dayforce Ceridian** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="33e47-202">On hello **Ceridian Dayforce HCM Configuration** section, click **Configure Ceridian Dayforce HCM** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="33e47-203">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="33e47-203">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Ceridian Dayforce HCM konfiguracji](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_configure.png) 

9. <span data-ttu-id="33e47-205">tooconfigure rejestracji jednokrotnej w **Ceridian Dayforce HCM** strony, należy pobrać hello toosend **XML metadanych** i **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** za[zespołem pomocy technicznej Ceridian Dayforce HCM](https://www.ceridian.com/contact-us/index.html).</span><span class="sxs-lookup"><span data-stu-id="33e47-205">tooconfigure single sign-on on **Ceridian Dayforce HCM** side, you need toosend hello downloaded **Metadata XML** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html).</span></span>

> [!TIP]
> <span data-ttu-id="33e47-206">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="33e47-206">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="33e47-207">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="33e47-207">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="33e47-208">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="33e47-208">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="33e47-209">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="33e47-209">Create an Azure AD test user</span></span>

<span data-ttu-id="33e47-210">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="33e47-210">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="33e47-212">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="33e47-212">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="33e47-213">W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="33e47-213">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="33e47-215">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="33e47-215">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="33e47-217">Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="33e47-217">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![przycisk Dodaj Hello](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="33e47-219">W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="33e47-219">In hello **User** dialog box, perform hello following steps:</span></span>

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_04.png)

    <span data-ttu-id="33e47-221">a.</span><span class="sxs-lookup"><span data-stu-id="33e47-221">a.</span></span> <span data-ttu-id="33e47-222">W hello **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="33e47-222">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="33e47-223">b.</span><span class="sxs-lookup"><span data-stu-id="33e47-223">b.</span></span> <span data-ttu-id="33e47-224">W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="33e47-224">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="33e47-225">c.</span><span class="sxs-lookup"><span data-stu-id="33e47-225">c.</span></span> <span data-ttu-id="33e47-226">Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="33e47-226">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="33e47-227">d.</span><span class="sxs-lookup"><span data-stu-id="33e47-227">d.</span></span> <span data-ttu-id="33e47-228">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="33e47-228">Click **Create**.</span></span>
 
### <a name="create-a-ceridian-dayforce-hcm-test-user"></a><span data-ttu-id="33e47-229">Tworzenie użytkownika testowego Ceridian Dayforce HCM</span><span class="sxs-lookup"><span data-stu-id="33e47-229">Create a Ceridian Dayforce HCM test user</span></span>

<span data-ttu-id="33e47-230">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="33e47-230">hello objective of this section is toocreate a user called Britta Simon in Ceridian Dayforce HCM.</span></span> <span data-ttu-id="33e47-231">Praca z hello [zespołem pomocy technicznej Ceridian Dayforce HCM](https://www.ceridian.com/contact-us/index.html) użytkowników tooget dodanych w hello Ceridian Dayforce HCM aplikacji.</span><span class="sxs-lookup"><span data-stu-id="33e47-231">Work with hello [Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html) tooget users added in hello Ceridian Dayforce HCM application.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="33e47-232">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="33e47-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="33e47-233">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooCeridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="33e47-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCeridian Dayforce HCM.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="33e47-235">**tooassign tooCeridian Simona Britta Dayforce HCM, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="33e47-235">**tooassign Britta Simon tooCeridian Dayforce HCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="33e47-236">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="33e47-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="33e47-238">Z listy aplikacji hello wybierz **Ceridian Dayforce HCM**.</span><span class="sxs-lookup"><span data-stu-id="33e47-238">In hello applications list, select **Ceridian Dayforce HCM**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_app.png) 

3. <span data-ttu-id="33e47-240">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="33e47-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="33e47-242">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="33e47-242">Click **Add** button.</span></span> <span data-ttu-id="33e47-243">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="33e47-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="33e47-245">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="33e47-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="33e47-246">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="33e47-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="33e47-247">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="33e47-247">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="33e47-248">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="33e47-248">Assign hello Azure AD test user</span></span>

<span data-ttu-id="33e47-249">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooCeridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="33e47-249">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCeridian Dayforce HCM.</span></span>

![Przypisanie roli użytkownika hello][200] 

<span data-ttu-id="33e47-251">**tooassign tooCeridian Simona Britta Dayforce HCM, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="33e47-251">**tooassign Britta Simon tooCeridian Dayforce HCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="33e47-252">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="33e47-252">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="33e47-254">Z listy aplikacji hello wybierz **Ceridian Dayforce HCM**.</span><span class="sxs-lookup"><span data-stu-id="33e47-254">In hello applications list, select **Ceridian Dayforce HCM**.</span></span>

    ![łącze Ceridian Dayforce HCM Hello na liście aplikacji hello](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_app.png)  

3. <span data-ttu-id="33e47-256">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="33e47-256">In hello menu on hello left, click **Users and groups**.</span></span>

    ![łącze "Użytkownicy i grupy" Hello][202]

4. <span data-ttu-id="33e47-258">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="33e47-258">Click **Add** button.</span></span> <span data-ttu-id="33e47-259">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="33e47-259">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Okienko Dodaj przypisania Hello][203]

5. <span data-ttu-id="33e47-261">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="33e47-261">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="33e47-262">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="33e47-262">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="33e47-263">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="33e47-263">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="33e47-264">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="33e47-264">Test single sign-on</span></span>

<span data-ttu-id="33e47-265">Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="33e47-265">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="33e47-266">Po kliknięciu kafelka Ceridian Dayforce HCM hello w hello Panel dostępu, należy pobrać zalogowane automatycznie tooyour Ceridian Dayforce HCM aplikacji.</span><span class="sxs-lookup"><span data-stu-id="33e47-266">When you click hello Ceridian Dayforce HCM tile in hello Access Panel, you should get automatically signed-on tooyour Ceridian Dayforce HCM application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="33e47-267">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="33e47-267">Additional resources</span></span>

* [<span data-ttu-id="33e47-268">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="33e47-268">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="33e47-269">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="33e47-269">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_203.png

