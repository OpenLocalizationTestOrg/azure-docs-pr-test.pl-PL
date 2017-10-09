---
title: 'Samouczek: Integracji Azure Active Directory z etouches | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i etouches."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 76cccaa8-859c-4c16-9d1d-8a6496fc7520
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 5f3ff7550e660b0fc52612140ca55061504b5edd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-etouches"></a><span data-ttu-id="c8e29-103">Samouczek: Integracji Azure Active Directory z etouches</span><span class="sxs-lookup"><span data-stu-id="c8e29-103">Tutorial: Azure Active Directory integration with etouches</span></span>

<span data-ttu-id="c8e29-104">Z tego samouczka, dowiesz się, jak etouches toointegrate w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c8e29-104">In this tutorial, you learn how toointegrate etouches with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c8e29-105">Integracja z usługą Azure AD etouches zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="c8e29-105">Integrating etouches with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c8e29-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooetouches</span><span class="sxs-lookup"><span data-stu-id="c8e29-106">You can control in Azure AD who has access tooetouches</span></span>
- <span data-ttu-id="c8e29-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooetouches (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c8e29-107">You can enable your users tooautomatically get signed-on tooetouches (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c8e29-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c8e29-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c8e29-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c8e29-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c8e29-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c8e29-110">Prerequisites</span></span>

<span data-ttu-id="c8e29-111">tooconfigure integracji z usługą Azure AD z etouches należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="c8e29-111">tooconfigure Azure AD integration with etouches, you need hello following items:</span></span>

- <span data-ttu-id="c8e29-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c8e29-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c8e29-113">Etouches logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="c8e29-113">An etouches single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c8e29-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="c8e29-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c8e29-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="c8e29-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c8e29-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="c8e29-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c8e29-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c8e29-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c8e29-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="c8e29-118">Scenario description</span></span>
<span data-ttu-id="c8e29-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="c8e29-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c8e29-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="c8e29-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c8e29-121">Dodawanie etouches z galerii hello</span><span class="sxs-lookup"><span data-stu-id="c8e29-121">Adding etouches from hello gallery</span></span>
2. <span data-ttu-id="c8e29-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="c8e29-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-etouches-from-hello-gallery"></a><span data-ttu-id="c8e29-123">Dodawanie etouches z galerii hello</span><span class="sxs-lookup"><span data-stu-id="c8e29-123">Adding etouches from hello gallery</span></span>
<span data-ttu-id="c8e29-124">tooconfigure hello integracji etouches do usługi Azure AD, należy etouches tooadd z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="c8e29-124">tooconfigure hello integration of etouches into Azure AD, you need tooadd etouches from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c8e29-125">**etouches tooadd z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="c8e29-125">**tooadd etouches from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c8e29-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="c8e29-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="c8e29-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="c8e29-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c8e29-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="c8e29-129">Then go too**All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. <span data-ttu-id="c8e29-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c8e29-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nowy przycisk aplikacji Hello][3]

4. <span data-ttu-id="c8e29-133">W polu wyszukiwania hello wpisz **etouches**, wybierz pozycję **etouches** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="c8e29-133">In hello search box, type **etouches**, select **etouches** from result panel then click **Add** button tooadd hello application.</span></span>

    ![etouches hello listy wyników](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c8e29-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="c8e29-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="c8e29-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z etouches w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="c8e29-136">In this section, you configure and test Azure AD single sign-on with etouches based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c8e29-137">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w etouches jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c8e29-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in etouches is tooa user in Azure AD.</span></span> <span data-ttu-id="c8e29-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w etouches musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="c8e29-138">In other words, a link relationship between an Azure AD user and hello related user in etouches needs toobe established.</span></span>

<span data-ttu-id="c8e29-139">W etouches, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="c8e29-139">In etouches, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c8e29-140">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z etouches, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="c8e29-140">tooconfigure and test Azure AD single sign-on with etouches, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c8e29-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="c8e29-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c8e29-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="c8e29-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c8e29-143">**[Tworzenie użytkownika testowego etouches](#create-an-etouches-test-user)**  -toohave odpowiednikiem Simona Britta w etouches, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c8e29-143">**[Create an etouches test user](#create-an-etouches-test-user)** - toohave a counterpart of Britta Simon in etouches that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c8e29-144">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="c8e29-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c8e29-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="c8e29-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="c8e29-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="c8e29-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="c8e29-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji etouches.</span><span class="sxs-lookup"><span data-stu-id="c8e29-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your etouches application.</span></span>

<span data-ttu-id="c8e29-148">**tooconfigure usługi Azure AD rejestracji jednokrotnej z etouches, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="c8e29-148">**tooconfigure Azure AD single sign-on with etouches, perform hello following steps:**</span></span>

1. <span data-ttu-id="c8e29-149">W portalu Azure na powitania hello **etouches** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="c8e29-149">In hello Azure portal, on hello **etouches** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="c8e29-151">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="c8e29-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_samlbase.png)

3. <span data-ttu-id="c8e29-153">Na powitania **etouches domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="c8e29-153">On hello **etouches Domain and URLs** section, perform hello following steps:</span></span>

    ![informacje logowania z jednym etouches domeny i adres URL](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_url.png)

    <span data-ttu-id="c8e29-155">a.</span><span class="sxs-lookup"><span data-stu-id="c8e29-155">a.</span></span> <span data-ttu-id="c8e29-156">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://www.eiseverywhere.com/saml/accounts/?sso&accountid=<ACCOUNTID>`</span><span class="sxs-lookup"><span data-stu-id="c8e29-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://www.eiseverywhere.com/saml/accounts/?sso&accountid=<ACCOUNTID>`</span></span>

    <span data-ttu-id="c8e29-157">b.</span><span class="sxs-lookup"><span data-stu-id="c8e29-157">b.</span></span> <span data-ttu-id="c8e29-158">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://www.eiseverywhere.com/<instance name>`</span><span class="sxs-lookup"><span data-stu-id="c8e29-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://www.eiseverywhere.com/<instance name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c8e29-159">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="c8e29-159">These values are not real.</span></span> <span data-ttu-id="c8e29-160">Zaktualizuj wartość hello z rzeczywistego hello Zaloguj się na adres URL i identyfikator, który znajduje się w dalszej części samouczka hello.</span><span class="sxs-lookup"><span data-stu-id="c8e29-160">You update hello value with hello actual Sign on URL and Identifier, which is explained later in hello tutorial.</span></span>
    > 

4. <span data-ttu-id="c8e29-161">Aplikacja etouches oczekuje potwierdzenia SAML hello w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="c8e29-161">etouches application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="c8e29-162">Skonfiguruj powitania po oświadczeń dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c8e29-162">Configure hello following claims for this application.</span></span> <span data-ttu-id="c8e29-163">Można zarządzać hello wartości tych atrybutów z hello **atrybut użytkownika** aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="c8e29-163">You can manage hello values of these attributes from hello **User Attribute** of hello application.</span></span> <span data-ttu-id="c8e29-164">powitania po zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="c8e29-164">hello following screenshot shows an example for this.</span></span> 

    ![Atrybut użytkownika](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_attribute.png) 

5. <span data-ttu-id="c8e29-166">W hello **atrybuty użytkownika** sekcji na powitania **logowanie jednokrotne** okna dialogowego, skonfiguruj atrybut tokenu SAML, jak pokazano w obrazie hello i wykonywać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="c8e29-166">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="c8e29-167">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="c8e29-167">Attribute Name</span></span> | <span data-ttu-id="c8e29-168">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="c8e29-168">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="c8e29-169">Adres e-mail</span><span class="sxs-lookup"><span data-stu-id="c8e29-169">Email</span></span> | <span data-ttu-id="c8e29-170">User.mail</span><span class="sxs-lookup"><span data-stu-id="c8e29-170">user.mail</span></span> |    
    
    <span data-ttu-id="c8e29-171">a.</span><span class="sxs-lookup"><span data-stu-id="c8e29-171">a.</span></span> <span data-ttu-id="c8e29-172">Kliknij przycisk **Dodaj atrybut** tooopen hello **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c8e29-172">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Dodaj atrybut](./media/active-directory-saas-etouches-tutorial/tutorial_attribute_04.png)

    ![Dodaj atrybut okna dialogowego](./media/active-directory-saas-etouches-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="c8e29-175">b.</span><span class="sxs-lookup"><span data-stu-id="c8e29-175">b.</span></span> <span data-ttu-id="c8e29-176">W hello **nazwa** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="c8e29-176">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="c8e29-177">c.</span><span class="sxs-lookup"><span data-stu-id="c8e29-177">c.</span></span> <span data-ttu-id="c8e29-178">Z hello **wartość** listy wartości atrybutu hello typ wyświetlanego dla tego wiersza.</span><span class="sxs-lookup"><span data-stu-id="c8e29-178">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="c8e29-179">d.</span><span class="sxs-lookup"><span data-stu-id="c8e29-179">d.</span></span> <span data-ttu-id="c8e29-180">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="c8e29-180">Click **Ok**.</span></span> 

6. <span data-ttu-id="c8e29-181">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="c8e29-181">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_certificate.png) 

7. <span data-ttu-id="c8e29-183">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c8e29-183">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-etouches-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="c8e29-185">tooget logowania jednokrotnego skonfigurowane dla danej aplikacji, wykonaj następujące kroki w hello etouches aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="c8e29-185">tooget SSO configured for your application, perform hello following steps in hello etouches application:</span></span> 

    ![Konfiguracja etouches](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_06.png) 

    <span data-ttu-id="c8e29-187">a.</span><span class="sxs-lookup"><span data-stu-id="c8e29-187">a.</span></span> <span data-ttu-id="c8e29-188">Logowanie za**etouches** aplikacji przy użyciu uprawnień administratora hello.</span><span class="sxs-lookup"><span data-stu-id="c8e29-188">Login too**etouches** application using hello Admin rights.</span></span>
   
    <span data-ttu-id="c8e29-189">b.</span><span class="sxs-lookup"><span data-stu-id="c8e29-189">b.</span></span> <span data-ttu-id="c8e29-190">Przejdź toohello **SAML** konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="c8e29-190">Go toohello **SAML** Configuration.</span></span>

    <span data-ttu-id="c8e29-191">c.</span><span class="sxs-lookup"><span data-stu-id="c8e29-191">c.</span></span> <span data-ttu-id="c8e29-192">W hello **ustawienia ogólne** sekcji, Otwórz swój certyfikat pobrany z portalu Azure w programie Notatnik hello kopiowania zawartości i wklej go w pole tekstowe metadanych hello IDP.</span><span class="sxs-lookup"><span data-stu-id="c8e29-192">In hello **General Settings** section, open your downloaded certificate from Azure portal in notepad, copy hello content, and then paste it into hello IDP metadata textbox.</span></span> 

    <span data-ttu-id="c8e29-193">d.</span><span class="sxs-lookup"><span data-stu-id="c8e29-193">d.</span></span> <span data-ttu-id="c8e29-194">Polecenie hello **Zapisz & pozostać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c8e29-194">Click on hello **Save & Stay** button.</span></span>
  
    <span data-ttu-id="c8e29-195">e.</span><span class="sxs-lookup"><span data-stu-id="c8e29-195">e.</span></span> <span data-ttu-id="c8e29-196">Polecenie hello **metadane aktualizacji** przycisku na powitania sekcji metadanych SAML.</span><span class="sxs-lookup"><span data-stu-id="c8e29-196">Click on hello **Update Metadata** button in hello SAML Metadata section.</span></span> 

    <span data-ttu-id="c8e29-197">f.</span><span class="sxs-lookup"><span data-stu-id="c8e29-197">f.</span></span> <span data-ttu-id="c8e29-198">Ten otwiera hello strony i wykonania rejestracji Jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="c8e29-198">This opens hello page and perform SSO.</span></span> <span data-ttu-id="c8e29-199">Raz hello logowania jednokrotnego działa, a następnie można skonfigurować hello nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c8e29-199">Once hello SSO is working then you can set up hello username.</span></span>

    <span data-ttu-id="c8e29-200">g.</span><span class="sxs-lookup"><span data-stu-id="c8e29-200">g.</span></span> <span data-ttu-id="c8e29-201">W polu nazwy użytkownika hello wybrać hello **emailaddress** pokazane na poniższym obrazie hello.</span><span class="sxs-lookup"><span data-stu-id="c8e29-201">In hello Username field, select hello **emailaddress** as shown in hello image below.</span></span> 

    <span data-ttu-id="c8e29-202">h.</span><span class="sxs-lookup"><span data-stu-id="c8e29-202">h.</span></span> <span data-ttu-id="c8e29-203">Kopiuj hello **SP identyfikator jednostki** wartość i wklej go do hello **identyfikator** pola tekstowego, który znajduje się w **etouches domeny i adres URL** sekcji z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c8e29-203">Copy hello **SP entity ID** value and paste it into hello **Identifier**  textbox, which is in **etouches Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="c8e29-204">i.</span><span class="sxs-lookup"><span data-stu-id="c8e29-204">i.</span></span> <span data-ttu-id="c8e29-205">Kopia hello **adres URL logowania jednokrotnego / ACS** wartość i wklej go do hello **Zaloguj się na adres URL** pola tekstowego, który znajduje się w **etouches domeny i adres URL** sekcji z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c8e29-205">Copy hello **SSO URL / ACS** value and paste it into hello **Sign on URL** textbox, which is in **etouches Domain and URLs** section on Azure portal.</span></span>
   
> [!TIP]
> <span data-ttu-id="c8e29-206">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="c8e29-206">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c8e29-207">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="c8e29-207">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c8e29-208">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c8e29-208">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c8e29-209">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c8e29-209">Create an Azure AD test user</span></span>
<span data-ttu-id="c8e29-210">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="c8e29-210">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="c8e29-212">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="c8e29-212">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c8e29-213">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="c8e29-213">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-etouches-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c8e29-215">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="c8e29-215">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-etouches-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c8e29-217">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c8e29-217">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![przycisk Dodaj Hello](./media/active-directory-saas-etouches-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c8e29-219">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="c8e29-219">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-etouches-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c8e29-221">a.</span><span class="sxs-lookup"><span data-stu-id="c8e29-221">a.</span></span> <span data-ttu-id="c8e29-222">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c8e29-222">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c8e29-223">b.</span><span class="sxs-lookup"><span data-stu-id="c8e29-223">b.</span></span> <span data-ttu-id="c8e29-224">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c8e29-224">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c8e29-225">c.</span><span class="sxs-lookup"><span data-stu-id="c8e29-225">c.</span></span> <span data-ttu-id="c8e29-226">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="c8e29-226">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c8e29-227">d.</span><span class="sxs-lookup"><span data-stu-id="c8e29-227">d.</span></span> <span data-ttu-id="c8e29-228">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="c8e29-228">Click **Create**.</span></span>
 
### <a name="create-an-etouches-test-user"></a><span data-ttu-id="c8e29-229">Tworzenie użytkownika testowego etouches</span><span class="sxs-lookup"><span data-stu-id="c8e29-229">Create an etouches test user</span></span>

<span data-ttu-id="c8e29-230">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w etouches.</span><span class="sxs-lookup"><span data-stu-id="c8e29-230">In this section, you create a user called Britta Simon in etouches.</span></span> <span data-ttu-id="c8e29-231">Praca z [etouches klienta obsługuje zespołu](https://www.etouches.com/event-software/support/customer-support/) użytkowników hello tooadd hello etouches platformy.</span><span class="sxs-lookup"><span data-stu-id="c8e29-231">Work with [etouches Client support team](https://www.etouches.com/event-software/support/customer-support/) tooadd hello users in hello etouches platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="c8e29-232">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c8e29-232">Assign hello Azure AD test user</span></span>

<span data-ttu-id="c8e29-233">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooetouches.</span><span class="sxs-lookup"><span data-stu-id="c8e29-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooetouches.</span></span>

![Przypisanie roli użytkownika hello][200] 

<span data-ttu-id="c8e29-235">**tooassign tooetouches Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="c8e29-235">**tooassign Britta Simon tooetouches, perform hello following steps:**</span></span>

1. <span data-ttu-id="c8e29-236">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="c8e29-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="c8e29-238">Z listy aplikacji hello wybierz **etouches**.</span><span class="sxs-lookup"><span data-stu-id="c8e29-238">In hello applications list, select **etouches**.</span></span>

    ![łącze etouches Hello na liście aplikacji hello](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_app.png) 

3. <span data-ttu-id="c8e29-240">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="c8e29-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![łącze "Użytkownicy i grupy" Hello][202] 

4. <span data-ttu-id="c8e29-242">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c8e29-242">Click **Add** button.</span></span> <span data-ttu-id="c8e29-243">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c8e29-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Okienko Dodaj przypisania Hello][203]

5. <span data-ttu-id="c8e29-245">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="c8e29-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c8e29-246">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c8e29-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c8e29-247">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c8e29-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="c8e29-248">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="c8e29-248">Test single sign-on</span></span>


<span data-ttu-id="c8e29-249">Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="c8e29-249">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c8e29-250">Po kliknięciu powitalne etouches kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour etouches aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c8e29-250">When you click hello etouches tile in hello Access Panel, you should get automatically signed-on tooyour etouches application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c8e29-251">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="c8e29-251">Additional resources</span></span>

* [<span data-ttu-id="c8e29-252">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c8e29-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c8e29-253">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c8e29-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_203.png

