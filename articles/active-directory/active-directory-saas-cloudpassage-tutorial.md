---
title: 'Samouczek: Integracji Azure Active Directory z CloudPassage | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i CloudPassage."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bfe1f14e-74e4-4680-ac9e-f7355e1c94cc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 32fb007b90f071626c9b40fb5afc341dd3c1ae99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cloudpassage"></a><span data-ttu-id="03036-103">Samouczek: Integracji Azure Active Directory z CloudPassage</span><span class="sxs-lookup"><span data-stu-id="03036-103">Tutorial: Azure Active Directory integration with CloudPassage</span></span>

<span data-ttu-id="03036-104">Z tego samouczka, dowiesz się, jak toointegrate CloudPassage w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="03036-104">In this tutorial, you learn how toointegrate CloudPassage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="03036-105">Integracja z usługą Azure AD CloudPassage zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="03036-105">Integrating CloudPassage with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="03036-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooCloudPassage</span><span class="sxs-lookup"><span data-stu-id="03036-106">You can control in Azure AD who has access tooCloudPassage</span></span>
- <span data-ttu-id="03036-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooCloudPassage (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="03036-107">You can enable your users tooautomatically get signed-on tooCloudPassage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="03036-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="03036-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="03036-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="03036-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="03036-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="03036-110">Prerequisites</span></span>

<span data-ttu-id="03036-111">tooconfigure integracji z usługą Azure AD z CloudPassage należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="03036-111">tooconfigure Azure AD integration with CloudPassage, you need hello following items:</span></span>

- <span data-ttu-id="03036-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="03036-112">An Azure AD subscription</span></span>
- <span data-ttu-id="03036-113">CloudPassage logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="03036-113">A CloudPassage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="03036-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="03036-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="03036-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="03036-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="03036-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="03036-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="03036-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="03036-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="03036-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="03036-118">Scenario description</span></span>
<span data-ttu-id="03036-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="03036-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="03036-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="03036-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="03036-121">Dodawanie CloudPassage z galerii hello</span><span class="sxs-lookup"><span data-stu-id="03036-121">Adding CloudPassage from hello gallery</span></span>
2. <span data-ttu-id="03036-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="03036-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cloudpassage-from-hello-gallery"></a><span data-ttu-id="03036-123">Dodawanie CloudPassage z galerii hello</span><span class="sxs-lookup"><span data-stu-id="03036-123">Adding CloudPassage from hello gallery</span></span>
<span data-ttu-id="03036-124">tooconfigure hello integracji CloudPassage do usługi Azure AD, należy tooadd CloudPassage z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="03036-124">tooconfigure hello integration of CloudPassage into Azure AD, you need tooadd CloudPassage from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="03036-125">**tooadd CloudPassage z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="03036-125">**tooadd CloudPassage from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="03036-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="03036-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="03036-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="03036-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="03036-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="03036-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="03036-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="03036-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="03036-133">W polu wyszukiwania hello wpisz **CloudPassage**.</span><span class="sxs-lookup"><span data-stu-id="03036-133">In hello search box, type **CloudPassage**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_search.png)

5. <span data-ttu-id="03036-135">W panelu wyników hello zaznacz **CloudPassage**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="03036-135">In hello results panel, select **CloudPassage**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="03036-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="03036-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="03036-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z CloudPassage na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="03036-138">In this section, you configure and test Azure AD single sign-on with CloudPassage based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="03036-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w CloudPassage jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="03036-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in CloudPassage is tooa user in Azure AD.</span></span> <span data-ttu-id="03036-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w CloudPassage musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="03036-140">In other words, a link relationship between an Azure AD user and hello related user in CloudPassage needs toobe established.</span></span>

<span data-ttu-id="03036-141">W CloudPassage, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="03036-141">In CloudPassage, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="03036-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z CloudPassage, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="03036-142">tooconfigure and test Azure AD single sign-on with CloudPassage, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="03036-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="03036-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="03036-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="03036-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="03036-145">**[Tworzenie użytkownika testowego CloudPassage](#creating-a-cloudpassage-test-user)**  -toohave odpowiednikiem Simona Britta w CloudPassage, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="03036-145">**[Creating a CloudPassage test user](#creating-a-cloudpassage-test-user)** - toohave a counterpart of Britta Simon in CloudPassage that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="03036-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="03036-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="03036-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="03036-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="03036-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="03036-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="03036-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="03036-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your CloudPassage application.</span></span>

<span data-ttu-id="03036-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z CloudPassage, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="03036-150">**tooconfigure Azure AD single sign-on with CloudPassage, perform hello following steps:**</span></span>

1. <span data-ttu-id="03036-151">W portalu Azure na powitania hello **CloudPassage** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="03036-151">In hello Azure portal, on hello **CloudPassage** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="03036-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="03036-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_samlbase.png)

3. <span data-ttu-id="03036-155">Na powitania **CloudPassage domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="03036-155">On hello **CloudPassage Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_url.png)

    <span data-ttu-id="03036-157">a.</span><span class="sxs-lookup"><span data-stu-id="03036-157">a.</span></span> <span data-ttu-id="03036-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://portal.cloudpassage.com/saml/init/accountid`</span><span class="sxs-lookup"><span data-stu-id="03036-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://portal.cloudpassage.com/saml/init/accountid`</span></span>

    <span data-ttu-id="03036-159">b.</span><span class="sxs-lookup"><span data-stu-id="03036-159">b.</span></span> <span data-ttu-id="03036-160">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca: `https://portal.cloudpassage.com/saml/consume/accountid`.</span><span class="sxs-lookup"><span data-stu-id="03036-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://portal.cloudpassage.com/saml/consume/accountid`.</span></span> <span data-ttu-id="03036-161">Możesz też uzyskać wartość tego atrybutu, klikając **dokumentacji ustawienia logowania jednokrotnego** w hello **ustawień rejestracji jednokrotnej** sekcji portalem CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="03036-161">You can get your value for this attribute by clicking **SSO Setup documentation** in hello **Single Sign-on Settings** section of your CloudPassage portal.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_05.png)
     
    > [!NOTE] 
    > <span data-ttu-id="03036-163">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="03036-163">These values are not real.</span></span> <span data-ttu-id="03036-164">Witaj rzeczywisty adres URL odpowiedzi służący i adres URL logowania, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="03036-164">Update these values with hello actual Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="03036-165">Skontaktuj się z [zespołem pomocy technicznej klienta CloudPassage](https://www.cloudpassage.com/company/contact/) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="03036-165">Contact [CloudPassage Client support team](https://www.cloudpassage.com/company/contact/) tooget these values.</span></span> 

4. <span data-ttu-id="03036-166">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="03036-166">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_certificate.png) 

5. <span data-ttu-id="03036-168">Aplikacja CloudPassage oczekuje potwierdzenia SAML hello w określonym formacie wymaga możesz tooadd atrybutu niestandardowego mapowania tooyour SAML tokenu atrybuty konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="03036-168">Your CloudPassage application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span>   
<span data-ttu-id="03036-169">powitania po zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="03036-169">hello following screenshot shows an example for this.</span></span>
   
   ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_25.png) 

6. <span data-ttu-id="03036-171">W hello **atrybuty użytkownika** sekcji na powitania **logowanie jednokrotne** okna dialogowego, skonfiguruj atrybut tokenu SAML, jak pokazano w powyższy obraz powitania i wykonywać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="03036-171">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>

    | <span data-ttu-id="03036-172">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="03036-172">Attribute Name</span></span> | <span data-ttu-id="03036-173">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="03036-173">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="03036-174">Imię</span><span class="sxs-lookup"><span data-stu-id="03036-174">firstname</span></span> |<span data-ttu-id="03036-175">User.givenName</span><span class="sxs-lookup"><span data-stu-id="03036-175">user.givenname</span></span> |
    | <span data-ttu-id="03036-176">nazwisko</span><span class="sxs-lookup"><span data-stu-id="03036-176">lastname</span></span> |<span data-ttu-id="03036-177">User.surname</span><span class="sxs-lookup"><span data-stu-id="03036-177">user.surname</span></span> |
    | <span data-ttu-id="03036-178">Adres e-mail</span><span class="sxs-lookup"><span data-stu-id="03036-178">email</span></span> |<span data-ttu-id="03036-179">User.mail</span><span class="sxs-lookup"><span data-stu-id="03036-179">user.mail</span></span> |
    
    <span data-ttu-id="03036-180">a.</span><span class="sxs-lookup"><span data-stu-id="03036-180">a.</span></span> <span data-ttu-id="03036-181">Kliknij przycisk **Dodaj atrybut** tooopen hello **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="03036-181">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cloudpassage-tutorial/tutorial_attribute_04.png)
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cloudpassage-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="03036-184">b.</span><span class="sxs-lookup"><span data-stu-id="03036-184">b.</span></span> <span data-ttu-id="03036-185">W hello **nazwa** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="03036-185">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="03036-186">c.</span><span class="sxs-lookup"><span data-stu-id="03036-186">c.</span></span> <span data-ttu-id="03036-187">Z hello **wartość** listy wartości atrybutu hello typ wyświetlanego dla tego wiersza.</span><span class="sxs-lookup"><span data-stu-id="03036-187">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="03036-188">d.</span><span class="sxs-lookup"><span data-stu-id="03036-188">d.</span></span> <span data-ttu-id="03036-189">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="03036-189">Click **Ok**.</span></span>

7. <span data-ttu-id="03036-190">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="03036-190">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="03036-192">Na powitania **konfiguracji CloudPassage** kliknij **skonfigurować CloudPassage** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="03036-192">On hello **CloudPassage Configuration** section, click **Configure CloudPassage** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="03036-193">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="03036-193">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_configure.png) 

9. <span data-ttu-id="03036-195">W oknie innej przeglądarki, witryny firmy CloudPassage tooyour logowania jako administrator.</span><span class="sxs-lookup"><span data-stu-id="03036-195">In a different browser window, sign-on tooyour CloudPassage company site as administrator.</span></span>

10. <span data-ttu-id="03036-196">Witaj menu u góry hello, kliknij przycisk **ustawienia**, a następnie kliknij przycisk **administrowania lokacją**.</span><span class="sxs-lookup"><span data-stu-id="03036-196">In hello menu on hello top, click **Settings**, and then click **Site Administration**.</span></span> 
   
    ![Konfigurowanie rejestracji jednokrotnej][12]

11. <span data-ttu-id="03036-198">Kliknij przycisk hello **ustawienia uwierzytelniania** kartę.</span><span class="sxs-lookup"><span data-stu-id="03036-198">Click hello **Authentication Settings** tab.</span></span> 
   
    ![Konfigurowanie rejestracji jednokrotnej][13]

12. <span data-ttu-id="03036-200">W hello **ustawień rejestracji jednokrotnej** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="03036-200">In hello **Single Sign-on Settings** section, perform hello following steps:</span></span> 
   
    ![Konfigurowanie rejestracji jednokrotnej][14]

    <span data-ttu-id="03036-202">a.</span><span class="sxs-lookup"><span data-stu-id="03036-202">a.</span></span> <span data-ttu-id="03036-203">Wybierz **sign-on(SSO) włączyć pojedynczego (dokumentacja Instalatora logowania jednokrotnego)** wyboru.</span><span class="sxs-lookup"><span data-stu-id="03036-203">Select **Enable Single sign-on(SSO)(SSO Setup Documentation)** checkbox.</span></span>
    
    <span data-ttu-id="03036-204">b.</span><span class="sxs-lookup"><span data-stu-id="03036-204">b.</span></span> <span data-ttu-id="03036-205">Wklej **identyfikator jednostki SAML** do hello **adres URL wystawcy SAML** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="03036-205">Paste **SAML Entity ID** into hello **SAML issuer URL** textbox.</span></span>
  
    <span data-ttu-id="03036-206">c.</span><span class="sxs-lookup"><span data-stu-id="03036-206">c.</span></span> <span data-ttu-id="03036-207">Wklej **SAML pojedynczy znak na adres URL usługi** do hello **adres URL punktu końcowego SAML** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="03036-207">Paste **SAML Single Sign-On Service URL** into hello **SAML endpoint URL** textbox.</span></span>
  
    <span data-ttu-id="03036-208">d.</span><span class="sxs-lookup"><span data-stu-id="03036-208">d.</span></span> <span data-ttu-id="03036-209">Wklej **Sign-Out URL** do hello **strony docelowej wylogowania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="03036-209">Paste **Sign-Out URL** into hello **Logout landing page** textbox.</span></span>
  
    <span data-ttu-id="03036-210">e.</span><span class="sxs-lookup"><span data-stu-id="03036-210">e.</span></span> <span data-ttu-id="03036-211">Otwórz pobrany certyfikat w Notatniku, hello kopia zawartości pobranej certyfikatu do Schowka, a następnie wklej go do hello **x 509 certyfikatu** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="03036-211">Open your downloaded certificate in notepad, copy hello content of downloaded certificate into your clipboard, and then paste it into hello **x 509 certificate** textbox.</span></span>
  
    <span data-ttu-id="03036-212">f.</span><span class="sxs-lookup"><span data-stu-id="03036-212">f.</span></span> <span data-ttu-id="03036-213">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="03036-213">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="03036-214">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="03036-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="03036-215">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="03036-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="03036-216">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="03036-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="03036-217">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="03036-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="03036-218">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="03036-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="03036-220">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="03036-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="03036-221">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="03036-221">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="03036-223">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="03036-223">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="03036-225">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="03036-225">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="03036-227">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="03036-227">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="03036-229">a.</span><span class="sxs-lookup"><span data-stu-id="03036-229">a.</span></span> <span data-ttu-id="03036-230">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="03036-230">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="03036-231">b.</span><span class="sxs-lookup"><span data-stu-id="03036-231">b.</span></span> <span data-ttu-id="03036-232">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="03036-232">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="03036-233">c.</span><span class="sxs-lookup"><span data-stu-id="03036-233">c.</span></span> <span data-ttu-id="03036-234">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="03036-234">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="03036-235">d.</span><span class="sxs-lookup"><span data-stu-id="03036-235">d.</span></span> <span data-ttu-id="03036-236">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="03036-236">Click **Create**.</span></span>
 
### <a name="creating-a-cloudpassage-test-user"></a><span data-ttu-id="03036-237">Tworzenie użytkownika testowego CloudPassage</span><span class="sxs-lookup"><span data-stu-id="03036-237">Creating a CloudPassage test user</span></span>

<span data-ttu-id="03036-238">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="03036-238">hello objective of this section is toocreate a user called Britta Simon in CloudPassage.</span></span>

<span data-ttu-id="03036-239">**toocreate użytkownika o nazwie Simona Britta w CloudPassage, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="03036-239">**toocreate a user called Britta Simon in CloudPassage, perform hello following steps:**</span></span>

1. <span data-ttu-id="03036-240">Logowania jednokrotnego tooyour **CloudPassage** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="03036-240">Sign-on tooyour **CloudPassage** company site as an administrator.</span></span> 

2. <span data-ttu-id="03036-241">Witaj pasku narzędzi u góry hello, kliknij przycisk **ustawienia**, a następnie kliknij przycisk **administrowania lokacją**.</span><span class="sxs-lookup"><span data-stu-id="03036-241">In hello toolbar on hello top, click **Settings**, and then click **Site Administration**.</span></span> 
   
   ![Tworzenie użytkownika testowego CloudPassage][22] 

3. <span data-ttu-id="03036-243">Kliknij przycisk hello **użytkowników** , a następnie kliknij pozycję **Dodaj nowego użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="03036-243">Click hello **Users** tab, and then click **Add New User**.</span></span> 
   
   ![Tworzenie użytkownika testowego CloudPassage][23]

4. <span data-ttu-id="03036-245">W hello **Dodaj nowego użytkownika** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="03036-245">In hello **Add New User** section, perform hello following steps:</span></span> 
   
   ![Tworzenie użytkownika testowego CloudPassage][24]
    
    <span data-ttu-id="03036-247">a.</span><span class="sxs-lookup"><span data-stu-id="03036-247">a.</span></span> <span data-ttu-id="03036-248">W hello **imię** tekstowym, wpisz Britta.</span><span class="sxs-lookup"><span data-stu-id="03036-248">In hello **First Name** textbox, type Britta.</span></span> 
  
    <span data-ttu-id="03036-249">b.</span><span class="sxs-lookup"><span data-stu-id="03036-249">b.</span></span> <span data-ttu-id="03036-250">W hello **nazwisko** tekstowym, wpisz Simona.</span><span class="sxs-lookup"><span data-stu-id="03036-250">In hello **Last Name** textbox, type Simon.</span></span>
  
    <span data-ttu-id="03036-251">c.</span><span class="sxs-lookup"><span data-stu-id="03036-251">c.</span></span> <span data-ttu-id="03036-252">W hello **Username** pole tekstowe, hello **E-mail** pole tekstowe i hello **ponownie poczty E-mail** pole tekstowe, wpisz nazwę użytkownika w Britta w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="03036-252">In hello **Username** textbox, hello **Email** textbox and hello **Retype Email** textbox, type Britta's user name in Azure AD.</span></span>
  
    <span data-ttu-id="03036-253">d.</span><span class="sxs-lookup"><span data-stu-id="03036-253">d.</span></span> <span data-ttu-id="03036-254">Jako **typu dostępu**, wybierz pozycję **Włącz dostęp do portalu Halo**.</span><span class="sxs-lookup"><span data-stu-id="03036-254">As **Access Type**, select **Enable Halo Portal Access**.</span></span>
  
    <span data-ttu-id="03036-255">e.</span><span class="sxs-lookup"><span data-stu-id="03036-255">e.</span></span> <span data-ttu-id="03036-256">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="03036-256">Click **Add**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="03036-257">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="03036-257">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="03036-258">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooCloudPassage.</span><span class="sxs-lookup"><span data-stu-id="03036-258">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCloudPassage.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="03036-260">**tooassign tooCloudPassage Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="03036-260">**tooassign Britta Simon tooCloudPassage, perform hello following steps:**</span></span>

1. <span data-ttu-id="03036-261">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="03036-261">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="03036-263">Z listy aplikacji hello wybierz **CloudPassage**.</span><span class="sxs-lookup"><span data-stu-id="03036-263">In hello applications list, select **CloudPassage**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_app.png) 

3. <span data-ttu-id="03036-265">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="03036-265">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="03036-267">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="03036-267">Click **Add** button.</span></span> <span data-ttu-id="03036-268">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="03036-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="03036-270">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="03036-270">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="03036-271">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="03036-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="03036-272">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="03036-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="03036-273">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="03036-273">Testing single sign-on</span></span>

<span data-ttu-id="03036-274">Celem Hello w tej sekcji jest tootest programu Azure AD SSO konfiguracji przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="03036-274">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="03036-275">Po kliknięciu kafelka CloudPassage hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour CloudPassage aplikacji.</span><span class="sxs-lookup"><span data-stu-id="03036-275">When you click hello CloudPassage tile in hello Access Panel, you should get automatically signed-on tooyour CloudPassage application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="03036-276">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="03036-276">Additional resources</span></span>

* [<span data-ttu-id="03036-277">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="03036-277">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="03036-278">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="03036-278">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_04.png
[12]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_07.png
[13]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_08.png
[14]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_09.png
[15]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_10.png
[22]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_15.png
[23]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_16.png
[24]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_17.png

[100]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_203.png

