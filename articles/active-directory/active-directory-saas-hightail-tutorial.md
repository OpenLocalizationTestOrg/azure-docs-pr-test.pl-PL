---
title: 'Samouczek: Integracji Azure Active Directory z Hightail | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Hightail."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e15206ac-74b0-46e4-9329-892c7d242ec0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: 2b36fcf8d5773255fdf89de2dccdceb95c032bd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hightail"></a><span data-ttu-id="8ca00-103">Samouczek: Integracji Azure Active Directory z Hightail</span><span class="sxs-lookup"><span data-stu-id="8ca00-103">Tutorial: Azure Active Directory integration with Hightail</span></span>

<span data-ttu-id="8ca00-104">Z tego samouczka, dowiesz się, jak toointegrate Hightail z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8ca00-104">In this tutorial, you learn how toointegrate Hightail with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8ca00-105">Integracja z usługą Azure AD Hightail zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="8ca00-105">Integrating Hightail with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8ca00-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooHightail</span><span class="sxs-lookup"><span data-stu-id="8ca00-106">You can control in Azure AD who has access tooHightail</span></span>
- <span data-ttu-id="8ca00-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooHightail (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ca00-107">You can enable your users tooautomatically get signed-on tooHightail (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8ca00-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="8ca00-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8ca00-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8ca00-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8ca00-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8ca00-110">Prerequisites</span></span>

<span data-ttu-id="8ca00-111">tooconfigure integracji z usługą Azure AD z Hightail należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="8ca00-111">tooconfigure Azure AD integration with Hightail, you need hello following items:</span></span>

- <span data-ttu-id="8ca00-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ca00-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8ca00-113">Hightail logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="8ca00-113">A Hightail single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8ca00-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="8ca00-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8ca00-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="8ca00-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8ca00-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="8ca00-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8ca00-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8ca00-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8ca00-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="8ca00-118">Scenario description</span></span>
<span data-ttu-id="8ca00-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="8ca00-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8ca00-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="8ca00-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8ca00-121">Dodawanie Hightail z galerii hello</span><span class="sxs-lookup"><span data-stu-id="8ca00-121">Adding Hightail from hello gallery</span></span>
2. <span data-ttu-id="8ca00-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="8ca00-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hightail-from-hello-gallery"></a><span data-ttu-id="8ca00-123">Dodawanie Hightail z galerii hello</span><span class="sxs-lookup"><span data-stu-id="8ca00-123">Adding Hightail from hello gallery</span></span>
<span data-ttu-id="8ca00-124">tooconfigure hello integracji Hightail do usługi Azure AD, należy tooadd Hightail z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="8ca00-124">tooconfigure hello integration of Hightail into Azure AD, you need tooadd Hightail from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8ca00-125">**tooadd Hightail z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="8ca00-125">**tooadd Hightail from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8ca00-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="8ca00-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="8ca00-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="8ca00-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8ca00-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="8ca00-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="8ca00-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8ca00-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="8ca00-133">W polu wyszukiwania hello wpisz **Hightail**.</span><span class="sxs-lookup"><span data-stu-id="8ca00-133">In hello search box, type **Hightail**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_search.png)

5. <span data-ttu-id="8ca00-135">W panelu wyników hello zaznacz **Hightail**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="8ca00-135">In hello results panel, select **Hightail**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8ca00-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="8ca00-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8ca00-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Hightail w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="8ca00-138">In this section, you configure and test Azure AD single sign-on with Hightail based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8ca00-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Hightail jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8ca00-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Hightail is tooa user in Azure AD.</span></span> <span data-ttu-id="8ca00-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Hightail musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="8ca00-140">In other words, a link relationship between an Azure AD user and hello related user in Hightail needs toobe established.</span></span>

<span data-ttu-id="8ca00-141">W Hightail, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="8ca00-141">In Hightail, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8ca00-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Hightail, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="8ca00-142">tooconfigure and test Azure AD single sign-on with Hightail, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8ca00-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="8ca00-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8ca00-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="8ca00-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8ca00-145">**[Tworzenie użytkownika testowego Hightail](#creating-a-hightail-test-user)**  -toohave odpowiednikiem Simona Britta w Hightail, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8ca00-145">**[Creating a Hightail test user](#creating-a-hightail-test-user)** - toohave a counterpart of Britta Simon in Hightail that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8ca00-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="8ca00-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8ca00-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="8ca00-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8ca00-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8ca00-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8ca00-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Hightail.</span><span class="sxs-lookup"><span data-stu-id="8ca00-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Hightail application.</span></span>

<span data-ttu-id="8ca00-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Hightail, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="8ca00-150">**tooconfigure Azure AD single sign-on with Hightail, perform hello following steps:**</span></span>

1. <span data-ttu-id="8ca00-151">W portalu Azure na powitania hello **Hightail** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="8ca00-151">In hello Azure portal, on hello **Hightail** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="8ca00-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="8ca00-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_samlbase.png)

3. <span data-ttu-id="8ca00-155">Na powitania **Hightail domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="8ca00-155">On hello **Hightail Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url.png)

     <span data-ttu-id="8ca00-157">W hello **adres URL odpowiedzi** pole tekstowe, wprowadź adres URL hello jako:`https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse`</span><span class="sxs-lookup"><span data-stu-id="8ca00-157">In hello **Reply URL** textbox, type hello URL as: `https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8ca00-158">Witaj poprzedniego wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="8ca00-158">hello preceding value is not real value.</span></span> <span data-ttu-id="8ca00-159">Wartość hello zostanie zaktualizowany hello rzeczywiste odpowiedzi adresu URL, który znajduje się w dalszej części samouczka hello.</span><span class="sxs-lookup"><span data-stu-id="8ca00-159">You will update hello value with hello actual Reply URL, which is explained later in hello tutorial.</span></span>
 
4. <span data-ttu-id="8ca00-160">Na powitania **Hightail domeny i adres URL** sekcji, jeśli chcesz, aby aplikacja hello tooconfigure w **SP zainicjował tryb**, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="8ca00-160">On hello **Hightail Domain and URLs** section, If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url1.png)

    <span data-ttu-id="8ca00-162">a.</span><span class="sxs-lookup"><span data-stu-id="8ca00-162">a.</span></span> <span data-ttu-id="8ca00-163">Kliknij przycisk hello **Pokaż zaawansowane ustawienia adresu URL**.</span><span class="sxs-lookup"><span data-stu-id="8ca00-163">Click hello **Show advanced URL settings**.</span></span>

    <span data-ttu-id="8ca00-164">b.</span><span class="sxs-lookup"><span data-stu-id="8ca00-164">b.</span></span> <span data-ttu-id="8ca00-165">W hello **na adres URL logowania** pole tekstowe, wprowadź adres URL hello jako:`https://www.hightail.com/loginSSO`</span><span class="sxs-lookup"><span data-stu-id="8ca00-165">In hello **Sign On URL** textbox, type hello URL as: `https://www.hightail.com/loginSSO`</span></span>

4. <span data-ttu-id="8ca00-166">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="8ca00-166">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_certificate.png) 

5. <span data-ttu-id="8ca00-168">Hightail aplikacji oczekuje potwierdzenia SAML hello w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="8ca00-168">Hightail application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="8ca00-169">Skonfiguruj powitania po oświadczeń dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8ca00-169">Please configure hello following claims for this application.</span></span> <span data-ttu-id="8ca00-170">Można zarządzać hello wartości tych atrybutów z hello **"Atrribute"** kartę aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="8ca00-170">You can manage hello values of these attributes from hello **"Atrribute"** tab of hello application.</span></span> <span data-ttu-id="8ca00-171">powitania po zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="8ca00-171">hello following screenshot shows an example for this.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_attribute.png) 

6. <span data-ttu-id="8ca00-173">W hello **atrybuty użytkownika** sekcji na powitania **logowanie jednokrotne** okna dialogowego, skonfiguruj atrybut tokenu SAML, jak pokazano w obrazie hello i wykonywać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="8ca00-173">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="8ca00-174">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="8ca00-174">Attribute Name</span></span> | <span data-ttu-id="8ca00-175">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="8ca00-175">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="8ca00-176">Imię</span><span class="sxs-lookup"><span data-stu-id="8ca00-176">FirstName</span></span> | <span data-ttu-id="8ca00-177">User.givenName</span><span class="sxs-lookup"><span data-stu-id="8ca00-177">user.givenname</span></span> |
    | <span data-ttu-id="8ca00-178">Nazwisko</span><span class="sxs-lookup"><span data-stu-id="8ca00-178">LastName</span></span> | <span data-ttu-id="8ca00-179">User.surname</span><span class="sxs-lookup"><span data-stu-id="8ca00-179">user.surname</span></span> |
    | <span data-ttu-id="8ca00-180">Adres e-mail</span><span class="sxs-lookup"><span data-stu-id="8ca00-180">Email</span></span> | <span data-ttu-id="8ca00-181">User.mail</span><span class="sxs-lookup"><span data-stu-id="8ca00-181">user.mail</span></span> |    
    | <span data-ttu-id="8ca00-182">Tożsamości użytkownika</span><span class="sxs-lookup"><span data-stu-id="8ca00-182">UserIdentity</span></span> | <span data-ttu-id="8ca00-183">User.mail</span><span class="sxs-lookup"><span data-stu-id="8ca00-183">user.mail</span></span> |
    
    <span data-ttu-id="8ca00-184">a.</span><span class="sxs-lookup"><span data-stu-id="8ca00-184">a.</span></span> <span data-ttu-id="8ca00-185">Kliknij przycisk **Dodaj atrybut** tooopen hello **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8ca00-185">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_04.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="8ca00-188">b.</span><span class="sxs-lookup"><span data-stu-id="8ca00-188">b.</span></span> <span data-ttu-id="8ca00-189">W hello **nazwa** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="8ca00-189">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="8ca00-190">c.</span><span class="sxs-lookup"><span data-stu-id="8ca00-190">c.</span></span> <span data-ttu-id="8ca00-191">Z hello **wartość** listy wartości atrybutu hello typ wyświetlanego dla tego wiersza.</span><span class="sxs-lookup"><span data-stu-id="8ca00-191">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="8ca00-192">d.</span><span class="sxs-lookup"><span data-stu-id="8ca00-192">d.</span></span> <span data-ttu-id="8ca00-193">Pozostaw hello **Namespace** puste.</span><span class="sxs-lookup"><span data-stu-id="8ca00-193">Leave hello **Namespace** blank.</span></span>
    
    <span data-ttu-id="8ca00-194">e.</span><span class="sxs-lookup"><span data-stu-id="8ca00-194">e.</span></span> <span data-ttu-id="8ca00-195">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="8ca00-195">Click **Ok**.</span></span>

7. <span data-ttu-id="8ca00-196">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8ca00-196">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hightail-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="8ca00-198">Na powitania **Hightail konfiguracji** kliknij **skonfigurować Hightail** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="8ca00-198">On hello **Hightail Configuration** section, click **Configure Hightail** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8ca00-199">Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="8ca00-199">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_configure.png) 

    >[!NOTE] 
    ><span data-ttu-id="8ca00-201">Przed skonfigurowaniem hello rejestracji jednokrotnej w aplikacji Hightail, białą listę domenę poczty e-mail z Hightail zespołu, aby hello wszystkich użytkowników, którzy korzystają z tej domeny można Użyj funkcji rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="8ca00-201">Before configuring hello Single Sign On at Hightail app, please white list your email domain with Hightail team so that all hello users who are using this domain can use Single Sign On functionality.</span></span>


9. <span data-ttu-id="8ca00-202">tooget logowania jednokrotnego skonfigurowane dla aplikacji, należy na toosign tooyour Hightail dzierżawy z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="8ca00-202">tooget SSO configured for your application, you need toosign-on tooyour Hightail tenant as an administrator.</span></span>
   
    <span data-ttu-id="8ca00-203">a.</span><span class="sxs-lookup"><span data-stu-id="8ca00-203">a.</span></span> <span data-ttu-id="8ca00-204">W menu hello na górze powitania kliknij hello **konta** i wybierz **skonfigurować SAML**.</span><span class="sxs-lookup"><span data-stu-id="8ca00-204">In hello menu on hello top, click hello **Account** tab and select **Configure SAML**.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_001.png) 

    <span data-ttu-id="8ca00-206">b.</span><span class="sxs-lookup"><span data-stu-id="8ca00-206">b.</span></span> <span data-ttu-id="8ca00-207">Zaznacz pole wyboru hello z **Włącz uwierzytelnianie SAML**.</span><span class="sxs-lookup"><span data-stu-id="8ca00-207">Select hello checkbox of **Enable SAML Authentication**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_002.png) 

    <span data-ttu-id="8ca00-209">c.</span><span class="sxs-lookup"><span data-stu-id="8ca00-209">c.</span></span> <span data-ttu-id="8ca00-210">Otwieranie certyfikatu zakodowanego base-64 w Notatniku pobrany z portalu Azure, hello kopiowania zawartości go do Schowka, a następnie wklej go toohello **SAML certyfikat podpisywania tokenu** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="8ca00-210">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **SAML Token Signing Certificate** textbox.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_003.png) 

    <span data-ttu-id="8ca00-212">d.</span><span class="sxs-lookup"><span data-stu-id="8ca00-212">d.</span></span> <span data-ttu-id="8ca00-213">W hello **SAML urzędu (dostawcy tożsamości)** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi** skopiowany z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="8ca00-213">In hello **SAML Authority (Identity Provider)** textbox, paste hello value of **SAML Single Sign-On Service URL** copied from Azure portal.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_004.png)

    <span data-ttu-id="8ca00-215">e.</span><span class="sxs-lookup"><span data-stu-id="8ca00-215">e.</span></span> <span data-ttu-id="8ca00-216">Jeśli chcesz, aby aplikacja hello tooconfigure w **IDP zainicjował tryb** wybierz **"Dostawcy tożsamości (IdP) zainicjował logowania"**.</span><span class="sxs-lookup"><span data-stu-id="8ca00-216">If you wish tooconfigure hello application in **IDP initiated mode** select **"Identity Provider (IdP) initiated log in"**.</span></span> <span data-ttu-id="8ca00-217">Jeśli **SP zainicjował tryb** wybierz **"Dostawcy usług (SP) zainicjował logowania"**.</span><span class="sxs-lookup"><span data-stu-id="8ca00-217">If **SP initiated mode** select **"Service Provider (SP) initiated log in"**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_006.png)

    <span data-ttu-id="8ca00-219">f.</span><span class="sxs-lookup"><span data-stu-id="8ca00-219">f.</span></span> <span data-ttu-id="8ca00-220">Skopiuj adres URL klienta SAML hello wystąpienia i wklej go w **adres URL odpowiedzi** textbox w **Hightail domeny i adres URL** sekcji z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="8ca00-220">Copy hello SAML consumer URL for your instance and paste it in **Reply URL** textbox in **Hightail Domain and URLs** section on Azure portal.</span></span>
    
    <span data-ttu-id="8ca00-221">g.</span><span class="sxs-lookup"><span data-stu-id="8ca00-221">g.</span></span> <span data-ttu-id="8ca00-222">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="8ca00-222">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="8ca00-223">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="8ca00-223">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8ca00-224">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="8ca00-224">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8ca00-225">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8ca00-225">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8ca00-226">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ca00-226">Creating an Azure AD test user</span></span>
<span data-ttu-id="8ca00-227">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="8ca00-227">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="8ca00-229">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="8ca00-229">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8ca00-230">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="8ca00-230">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8ca00-232">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="8ca00-232">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8ca00-234">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8ca00-234">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8ca00-236">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="8ca00-236">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8ca00-238">a.</span><span class="sxs-lookup"><span data-stu-id="8ca00-238">a.</span></span> <span data-ttu-id="8ca00-239">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8ca00-239">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8ca00-240">b.</span><span class="sxs-lookup"><span data-stu-id="8ca00-240">b.</span></span> <span data-ttu-id="8ca00-241">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8ca00-241">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8ca00-242">c.</span><span class="sxs-lookup"><span data-stu-id="8ca00-242">c.</span></span> <span data-ttu-id="8ca00-243">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="8ca00-243">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8ca00-244">d.</span><span class="sxs-lookup"><span data-stu-id="8ca00-244">d.</span></span> <span data-ttu-id="8ca00-245">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="8ca00-245">Click **Create**.</span></span>
 
### <a name="creating-a-hightail-test-user"></a><span data-ttu-id="8ca00-246">Tworzenie użytkownika testowego Hightail</span><span class="sxs-lookup"><span data-stu-id="8ca00-246">Creating a Hightail test user</span></span>

<span data-ttu-id="8ca00-247">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w Hightail.</span><span class="sxs-lookup"><span data-stu-id="8ca00-247">hello objective of this section is toocreate a user called Britta Simon in Hightail.</span></span> 

<span data-ttu-id="8ca00-248">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="8ca00-248">There is no action item for you in this section.</span></span> <span data-ttu-id="8ca00-249">Hightail obsługuje użytkownika w czasie inicjowania obsługi administracyjnej oparta na powitania oświadczenia niestandardowe.</span><span class="sxs-lookup"><span data-stu-id="8ca00-249">Hightail supports just-in-time user provisioning based on hello custom claims.</span></span> <span data-ttu-id="8ca00-250">Jeśli skonfigurowano hello oświadczenia niestandardowe, jak pokazano w sekcji hello  **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  powyżej, użytkownik zostanie automatycznie utworzone w aplikacji hello go jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="8ca00-250">If you have configured hello custom claims as shown in hello section **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** above, a user is automatically created in hello application it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="8ca00-251">Jeśli potrzebujesz ręcznie toocreate użytkownika, należy toocontact hello [zespołem pomocy technicznej Hightail](mailto:support@hightail.com).</span><span class="sxs-lookup"><span data-stu-id="8ca00-251">If you need toocreate a user manually, you need toocontact hello [Hightail support team](mailto:support@hightail.com).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8ca00-252">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ca00-252">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8ca00-253">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooHightail.</span><span class="sxs-lookup"><span data-stu-id="8ca00-253">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHightail.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="8ca00-255">**tooassign tooHightail Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="8ca00-255">**tooassign Britta Simon tooHightail, perform hello following steps:**</span></span>

1. <span data-ttu-id="8ca00-256">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="8ca00-256">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="8ca00-258">Z listy aplikacji hello wybierz **Hightail**.</span><span class="sxs-lookup"><span data-stu-id="8ca00-258">In hello applications list, select **Hightail**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_app.png) 

3. <span data-ttu-id="8ca00-260">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="8ca00-260">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="8ca00-262">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8ca00-262">Click **Add** button.</span></span> <span data-ttu-id="8ca00-263">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8ca00-263">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="8ca00-265">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="8ca00-265">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8ca00-266">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8ca00-266">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8ca00-267">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8ca00-267">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8ca00-268">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8ca00-268">Testing single sign-on</span></span>

<span data-ttu-id="8ca00-269">Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="8ca00-269">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8ca00-270">Po kliknięciu kafelka Hightail hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Hightail aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8ca00-270">When you click hello Hightail tile in hello Access Panel, you should get automatically signed-on tooyour Hightail application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="8ca00-271">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="8ca00-271">Additional resources</span></span>

* [<span data-ttu-id="8ca00-272">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8ca00-272">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8ca00-273">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8ca00-273">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_203.png

