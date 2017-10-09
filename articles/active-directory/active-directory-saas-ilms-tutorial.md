---
title: 'Samouczek: Integracji Azure Active Directory z iLMS | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i iLMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d6e11639-6cea-48c9-b008-246cf686e726
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/13/2017
ms.author: jeedes
ms.openlocfilehash: da0936de23afcd5a4213aa6f699165f9bfa82c35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ilms"></a><span data-ttu-id="d9fc3-103">Samouczek: Integracji Azure Active Directory z iLMS</span><span class="sxs-lookup"><span data-stu-id="d9fc3-103">Tutorial: Azure Active Directory integration with iLMS</span></span>

<span data-ttu-id="d9fc3-104">Z tego samouczka, dowiesz się, jak iLMS toointegrate w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d9fc3-104">In this tutorial, you learn how toointegrate iLMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d9fc3-105">Integracja z usługą Azure AD iLMS zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="d9fc3-105">Integrating iLMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d9fc3-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooiLMS</span><span class="sxs-lookup"><span data-stu-id="d9fc3-106">You can control in Azure AD who has access tooiLMS</span></span>
- <span data-ttu-id="d9fc3-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooiLMS (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9fc3-107">You can enable your users tooautomatically get signed-on tooiLMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d9fc3-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="d9fc3-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d9fc3-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d9fc3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9fc3-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d9fc3-110">Prerequisites</span></span>

<span data-ttu-id="d9fc3-111">tooconfigure integracji z usługą Azure AD z iLMS należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="d9fc3-111">tooconfigure Azure AD integration with iLMS, you need hello following items:</span></span>

- <span data-ttu-id="d9fc3-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9fc3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d9fc3-113">ILMS jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="d9fc3-113">An iLMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d9fc3-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d9fc3-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="d9fc3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d9fc3-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="d9fc3-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d9fc3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d9fc3-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="d9fc3-118">Scenario description</span></span>
<span data-ttu-id="d9fc3-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d9fc3-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="d9fc3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d9fc3-121">Dodawanie iLMS z galerii hello</span><span class="sxs-lookup"><span data-stu-id="d9fc3-121">Adding iLMS from hello gallery</span></span>
2. <span data-ttu-id="d9fc3-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="d9fc3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ilms-from-hello-gallery"></a><span data-ttu-id="d9fc3-123">Dodawanie iLMS z galerii hello</span><span class="sxs-lookup"><span data-stu-id="d9fc3-123">Adding iLMS from hello gallery</span></span>
<span data-ttu-id="d9fc3-124">tooconfigure hello integracji iLMS do usługi Azure AD, należy iLMS tooadd z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-124">tooconfigure hello integration of iLMS into Azure AD, you need tooadd iLMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d9fc3-125">**iLMS tooadd z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="d9fc3-125">**tooadd iLMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d9fc3-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="d9fc3-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d9fc3-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="d9fc3-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-131">tooadd new application, click **New application** button on hello top of hello dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="d9fc3-133">W polu wyszukiwania hello wpisz **iLMS**.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-133">In hello search box, type **iLMS**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_search.png)

5. <span data-ttu-id="d9fc3-135">Wybierz w panelu wyników hello **iLMS**, następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-135">In hello results panel, select **iLMS**, then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d9fc3-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="d9fc3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d9fc3-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z iLMS w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-138">In this section, you configure and test Azure AD single sign-on with iLMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d9fc3-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w iLMS jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in iLMS is tooa user in Azure AD.</span></span> <span data-ttu-id="d9fc3-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w iLMS musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-140">In other words, a link relationship between an Azure AD user and hello related user in iLMS needs toobe established.</span></span>

<span data-ttu-id="d9fc3-141">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w iLMS.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in iLMS.</span></span>

<span data-ttu-id="d9fc3-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z iLMS, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="d9fc3-142">tooconfigure and test Azure AD single sign-on with iLMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d9fc3-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d9fc3-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d9fc3-145">**[Tworzenie użytkownika testowego iLMS](#creating-an-ilms-test-user)**  -toohave odpowiednikiem Simona Britta w iLMS, że jego reprezentacja toohello połączonej usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-145">**[Creating an iLMS test user](#creating-an-ilms-test-user)** - toohave a counterpart of Britta Simon in iLMS that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="d9fc3-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d9fc3-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d9fc3-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d9fc3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d9fc3-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji iLMS.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your iLMS application.</span></span>

<span data-ttu-id="d9fc3-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z iLMS, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="d9fc3-150">**tooconfigure Azure AD single sign-on with iLMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="d9fc3-151">W portalu Azure na powitania hello **iLMS** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-151">In hello Azure portal, on hello **iLMS** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="d9fc3-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_samlbase.png)

3. <span data-ttu-id="d9fc3-155">Na powitania **iLMS domeny i adres URL** sekcji, wykonaj następujące kroki, jeśli chcesz, aby aplikacja hello tooconfigure w hello **IDP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="d9fc3-155">On hello **iLMS Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url.png)

    <span data-ttu-id="d9fc3-157">a.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-157">a.</span></span> <span data-ttu-id="d9fc3-158">W hello **identyfikator** pole tekstowe, Wklej hello **identyfikator** wartość skopiować z **usługodawcy** sekcji SAML ustawień w portalu administracyjnym iLMS.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-158">In hello **Identifier** textbox, paste hello **Identifier** value you copy from **Service Provider** section of SAML settings in iLMS admin portal.</span></span>

    <span data-ttu-id="d9fc3-159">b.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-159">b.</span></span> <span data-ttu-id="d9fc3-160">W hello **adres URL odpowiedzi** pole tekstowe, Wklej hello **(adres URL punktu końcowego)** wartość skopiować z **usługodawcy** sekcji SAML ustawień w portalu administratora iLMS o następujących hello wzorzec`https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span><span class="sxs-lookup"><span data-stu-id="d9fc3-160">In hello **Reply URL** textbox, paste hello **Endpoint (URL)** value you copy from **Service Provider** section of SAML settings in iLMS admin portal having hello following pattern `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span></span>

    >[!Note]
    ><span data-ttu-id="d9fc3-161">Ta 123456 jest Przykładowa wartość identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-161">This '123456' is an example value of identifier.</span></span>

4. <span data-ttu-id="d9fc3-162">Sprawdź **Pokaż zaawansowane ustawienia adresu URL**, jeśli chcesz, aby aplikacja hello tooconfigure w **SP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="d9fc3-162">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url1.png)

    <span data-ttu-id="d9fc3-164">W hello **adres URL logowania** pole tekstowe, Wklej hello **(adres URL punktu końcowego)** wartość skopiować z **usługodawcy** sekcji SAML ustawień w portalu administracyjnym iLMS jako`https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span><span class="sxs-lookup"><span data-stu-id="d9fc3-164">In hello **Sign-on URL** textbox, paste hello **Endpoint (URL)** value you copy from **Service Provider** section of SAML settings in iLMS admin portal as `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span></span>     

5. <span data-ttu-id="d9fc3-165">tooenable JIT inicjowania obsługi administracyjnej, iLMS aplikacji oczekuje potwierdzenia SAML hello w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-165">tooenable JIT provisioning, iLMS application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="d9fc3-166">Skonfiguruj powitania po oświadczeń dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-166">Configure hello following claims for this application.</span></span> <span data-ttu-id="d9fc3-167">Można zarządzać hello wartości tych atrybutów z hello **atrybuty użytkownika** sekcji na stronie integracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-167">You can manage hello values of these attributes from hello **User Attributes** section on application integration page.</span></span> <span data-ttu-id="d9fc3-168">powitania po zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-168">hello following screenshot shows an example for this.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ilms-tutorial/4.png)
    
    <span data-ttu-id="d9fc3-170">Utwórz **działu, Region** i **dzielenia** atrybutów, a następnie dodaj nazwę hello tych atrybutów w iLMS.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-170">Create **Department, Region** and **Division** attributes and add hello name of these attributes in iLMS.</span></span> <span data-ttu-id="d9fc3-171">Te atrybuty pokazanym powyżej są wymagane.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-171">All these attributes shown above are required.</span></span>    

    > [!NOTE] 
    > <span data-ttu-id="d9fc3-172">Masz tooenable **Utwórz konto użytkownika Un-recognized** w iLMS toomap te atrybuty.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-172">You have tooenable **Create Un-recognized User Account** in iLMS toomap these attributes.</span></span> <span data-ttu-id="d9fc3-173">Postępuj zgodnie z instrukcjami hello [tutaj](http://support.inspiredelearning.com/customer/portal/articles/2204526) tooget pomysł na powitania atrybuty konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-173">Follow hello instructions [here](http://support.inspiredelearning.com/customer/portal/articles/2204526) tooget an idea on hello attributes configuration.</span></span>

6. <span data-ttu-id="d9fc3-174">W hello **atrybuty użytkownika** sekcji na powitania **logowanie jednokrotne** okna dialogowego, skonfiguruj atrybut tokenu SAML, jak pokazano w powyższy obraz powitania i wykonywać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="d9fc3-174">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="d9fc3-175">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="d9fc3-175">Attribute Name</span></span> | <span data-ttu-id="d9fc3-176">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="d9fc3-176">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="d9fc3-177">dzielenie</span><span class="sxs-lookup"><span data-stu-id="d9fc3-177">division</span></span> | <span data-ttu-id="d9fc3-178">User.Department</span><span class="sxs-lookup"><span data-stu-id="d9fc3-178">user.department</span></span> |
    | <span data-ttu-id="d9fc3-179">Region</span><span class="sxs-lookup"><span data-stu-id="d9fc3-179">region</span></span> | <span data-ttu-id="d9fc3-180">User.state</span><span class="sxs-lookup"><span data-stu-id="d9fc3-180">user.state</span></span> |
    | <span data-ttu-id="d9fc3-181">Dział</span><span class="sxs-lookup"><span data-stu-id="d9fc3-181">department</span></span> | <span data-ttu-id="d9fc3-182">User.jobtitle</span><span class="sxs-lookup"><span data-stu-id="d9fc3-182">user.jobtitle</span></span> |

    <span data-ttu-id="d9fc3-183">a.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-183">a.</span></span> <span data-ttu-id="d9fc3-184">Kliknij przycisk **Dodaj atrybut** tooopen hello **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-184">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_04.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_05.png)
    
    <span data-ttu-id="d9fc3-187">b.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-187">b.</span></span> <span data-ttu-id="d9fc3-188">W hello **nazwa** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-188">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="d9fc3-189">c.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-189">c.</span></span> <span data-ttu-id="d9fc3-190">Z hello **wartość** listy wartości atrybutu hello typ wyświetlanego dla tego wiersza.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-190">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="d9fc3-191">d.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-191">d.</span></span> <span data-ttu-id="d9fc3-192">Kliknij przycisk **Ok**</span><span class="sxs-lookup"><span data-stu-id="d9fc3-192">Click **Ok**</span></span>

7. <span data-ttu-id="d9fc3-193">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-193">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_certificate.png) 

8. <span data-ttu-id="d9fc3-195">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-195">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-iLMS-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="d9fc3-197">W oknie przeglądarki innej witryny sieci web, zaloguj się za tooyour **portalu administracyjnego iLMS** jako administrator.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-197">In a different web browser window, log in tooyour **iLMS admin portal** as an administrator.</span></span>

10. <span data-ttu-id="d9fc3-198">Kliknij przycisk **SSO:SAML** w obszarze **ustawienia** karcie Ustawienia SAML tooopen i wykonywać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="d9fc3-198">Click **SSO:SAML** under **Settings** tab tooopen SAML settings and perform hello following steps:</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ilms-tutorial/1.png) 

    <span data-ttu-id="d9fc3-200">a.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-200">a.</span></span> <span data-ttu-id="d9fc3-201">Rozwiń węzeł hello **usługodawcy** hello sekcji i skopiuj **identyfikator** i **(adres URL punktu końcowego)** wartość.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-201">Expand hello **Service Provider** section and copy hello **Identifier** and **Endpoint (URL)** value.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ilms-tutorial/2.png) 

    <span data-ttu-id="d9fc3-203">b.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-203">b.</span></span> <span data-ttu-id="d9fc3-204">W obszarze **dostawcy tożsamości** kliknij **Importowanie metadanych**.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-204">Under **Identity Provider** section, click **Import Metadata**.</span></span>
    
    <span data-ttu-id="d9fc3-205">c.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-205">c.</span></span> <span data-ttu-id="d9fc3-206">Wybierz hello **metadanych** plik pobrany z portalu Azure z **certyfikat podpisywania SAML** sekcji.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-206">Select hello **Metadata** file downloaded from Azure Portal from **SAML Signing Certificate** section.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig1.png) 

    <span data-ttu-id="d9fc3-208">d.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-208">d.</span></span> <span data-ttu-id="d9fc3-209">Jeśli chcesz, aby tooenable JIT inicjowania obsługi administracyjnej toocreate iLMS kont un-rozpoznaje użytkowników, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="d9fc3-209">If you want tooenable JIT provisioning toocreate iLMS accounts for un-recognize users, follow below steps:</span></span>
        
       - <span data-ttu-id="d9fc3-210">Sprawdź **utworzyć konto użytkownika nie jest rozpoznawaną**.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-210">Check **Create Un-recognized User Account**.</span></span>
       
       ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig2.png)

       -  <span data-ttu-id="d9fc3-212">Mapowanie atrybutów hello w usłudze Azure AD z atrybutami hello w iLMS.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-212">Map hello attributes in Azure AD with hello attributes in iLMS.</span></span> <span data-ttu-id="d9fc3-213">W kolumnie atrybutu hello Określ hello atrybutów nazwy lub hello wartości domyślnej.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-213">In hello attribute column, specify hello attributes name or hello default value.</span></span>

    <span data-ttu-id="d9fc3-214">e.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-214">e.</span></span> <span data-ttu-id="d9fc3-215">Przejdź za**reguły biznesowe** karcie i wykonywać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="d9fc3-215">Go too**Business Rules** tab and perform hello following steps:</span></span> 
        
       ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ilms-tutorial/5.png)

       - <span data-ttu-id="d9fc3-217">Sprawdź **Tworzenie regionów Un-recognized, działów i działów** toocreate regionach, działów i działów, które jeszcze nie istnieją w czasie hello rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-217">Check **Create Un-recognized Regions, Divisions and Departments** toocreate Regions, Divisions, and Departments that do not already exist at hello time of Single Sign-on.</span></span>
        
       - <span data-ttu-id="d9fc3-218">Sprawdź **aktualizacji użytkownika profilu podczas logowania** toospecify Określa, czy profil użytkownika hello jest aktualizowany przy każdej rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-218">Check **Update User Profile During Sign-in** toospecify whether hello user’s profile is updated with each Single Sign-on.</span></span> 
        
       - <span data-ttu-id="d9fc3-219">Jeśli hello **"Aktualizacji puste wartości dla innych niż obowiązkowego pola w profilu użytkownika"** opcja jest zaznaczona, profil opcjonalne pola, które są puste podczas logowania zostanie także spowodować profil iLMS użytkownika hello toocontain puste wartości dla tych pól.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-219">If hello **“Update Blank Values for Non Mandatory Fields in User Profile”** option is checked, optional profile fields that are blank upon sign in will also cause hello user’s iLMS profile toocontain blank values for those fields.</span></span>
        
       - <span data-ttu-id="d9fc3-220">Sprawdź **Wyślij E-mail z powiadomieniem błąd** , a następnie wprowadź adres e-mail użytkownika hello hello miejscu tooreceive hello błąd powiadomienia e-mail.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-220">Check **Send Error Notification Email** and enter hello email of hello user where you want tooreceive hello error notification email.</span></span>

11. <span data-ttu-id="d9fc3-221">Kliknij przycisk **zapisać** przycisk toosave hello ustawienia.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-221">Click **Save** button toosave hello settings.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ilms-tutorial/save.png)

> [!TIP]
> <span data-ttu-id="d9fc3-223">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="d9fc3-223">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d9fc3-224">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-224">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d9fc3-225">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d9fc3-225">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
    
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d9fc3-226">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9fc3-226">Creating an Azure AD test user</span></span>
<span data-ttu-id="d9fc3-227">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-227">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="d9fc3-229">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="d9fc3-229">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d9fc3-230">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-230">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d9fc3-232">Przejdź za**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** toodisplay hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-232">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d9fc3-234">U góry okna dialogowego hello powitania kliknij **Dodaj** tooopen hello **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-234">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d9fc3-236">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="d9fc3-236">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d9fc3-238">a.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-238">a.</span></span> <span data-ttu-id="d9fc3-239">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-239">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d9fc3-240">b.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-240">b.</span></span> <span data-ttu-id="d9fc3-241">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-241">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d9fc3-242">c.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-242">c.</span></span> <span data-ttu-id="d9fc3-243">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-243">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d9fc3-244">d.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-244">d.</span></span> <span data-ttu-id="d9fc3-245">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-245">Click **Create**.</span></span>
 
### <a name="creating-an-ilms-test-user"></a><span data-ttu-id="d9fc3-246">Tworzenie użytkownika testowego iLMS</span><span class="sxs-lookup"><span data-stu-id="d9fc3-246">Creating an iLMS test user</span></span>

<span data-ttu-id="d9fc3-247">Aplikacja obsługuje tylko w czasie Inicjowanie obsługi użytkowników i uwierzytelnianie użytkowników są tworzone automatycznie w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-247">Application supports Just in time user provisioning and after authentication users are created in hello application automatically.</span></span> <span data-ttu-id="d9fc3-248">JIT będzie działać, jeśli kliknięto hello **Utwórz konto użytkownika Un-recognized** wyboru podczas SAML ustawienie konfiguracji w portalu administracyjnym iLMS.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-248">JIT will work, if you have clicked hello **Create Un-recognized User Account** checkbox during SAML configuration setting at iLMS admin portal.</span></span>

<span data-ttu-id="d9fc3-249">Jeśli potrzebujesz toocreate użytkownika ręcznie, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="d9fc3-249">If you need toocreate an user manually, then follow below steps :</span></span>

1. <span data-ttu-id="d9fc3-250">Zaloguj się w witrynie firmy iLMS tooyour jako administrator.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-250">Log in tooyour iLMS company site as an administrator.</span></span>

2. <span data-ttu-id="d9fc3-251">Kliknij przycisk **"Zarejestruj użytkownika"** w obszarze **użytkowników** karcie tooopen **zarejestrować użytkownika** strony.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-251">Click **“Register User”** under **Users** tab tooopen **Register User** page.</span></span> 
   
   ![Dodawanie pracownika](./media/active-directory-saas-ilms-tutorial/3.png)

3. <span data-ttu-id="d9fc3-253">Na powitania **"Zarejestruj użytkownika"** wykonaj następujące kroki hello.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-253">On hello **“Register User”** page, perform hello following steps.</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-ilms-tutorial/create_testuser_add.png)

    <span data-ttu-id="d9fc3-255">a.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-255">a.</span></span> <span data-ttu-id="d9fc3-256">W hello **imię** pole tekstowe, typ hello imię Britta.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-256">In hello **First Name** textbox, type hello first name Britta.</span></span>
   
    <span data-ttu-id="d9fc3-257">b.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-257">b.</span></span> <span data-ttu-id="d9fc3-258">W hello **nazwisko** pole tekstowe, typ hello nazwisko Simona.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-258">In hello **Last Name** textbox, type hello last name Simon.</span></span>

    <span data-ttu-id="d9fc3-259">c.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-259">c.</span></span> <span data-ttu-id="d9fc3-260">W hello **identyfikator wiadomości E-mail** pole tekstowe, adres e-mail hello typu Simona Britta konta.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-260">In hello **Email ID** textbox, type hello email address of Britta Simon account.</span></span>

    <span data-ttu-id="d9fc3-261">d.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-261">d.</span></span> <span data-ttu-id="d9fc3-262">W hello **Region** listy rozwijanej wybierz hello wartość dla regionu.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-262">In hello **Region** dropdown, select hello value for region.</span></span>

    <span data-ttu-id="d9fc3-263">e.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-263">e.</span></span> <span data-ttu-id="d9fc3-264">W hello **dzielenia** listy rozwijanej wybierz hello wartość podziału.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-264">In hello **Division** dropdown, select hello value for division.</span></span>

    <span data-ttu-id="d9fc3-265">f.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-265">f.</span></span> <span data-ttu-id="d9fc3-266">W hello **działu** listy rozwijanej wybierz hello wartość dla działu.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-266">In hello **Department** dropdown, select hello value for department.</span></span>

    <span data-ttu-id="d9fc3-267">g.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-267">g.</span></span> <span data-ttu-id="d9fc3-268">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-268">Click **Save**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d9fc3-269">Możesz wysłać toouser poczty rejestracji, wybierając **wysłać wiadomość E-mail rejestracji** wyboru.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-269">You can send registration mail toouser by selecting **Send Registration Mail** checkbox.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d9fc3-270">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9fc3-270">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d9fc3-271">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie jej tooiLMS dostępu.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-271">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooiLMS.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="d9fc3-273">**tooassign tooiLMS Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="d9fc3-273">**tooassign Britta Simon tooiLMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="d9fc3-274">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-274">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="d9fc3-276">Z listy aplikacji hello wybierz **iLMS**.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-276">In hello applications list, select **iLMS**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_app.png) 

3. <span data-ttu-id="d9fc3-278">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-278">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="d9fc3-280">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-280">Click **Add** button.</span></span> <span data-ttu-id="d9fc3-281">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-281">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="d9fc3-283">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-283">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d9fc3-284">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-284">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d9fc3-285">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-285">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d9fc3-286">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d9fc3-286">Testing single sign-on</span></span>

<span data-ttu-id="d9fc3-287">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-287">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d9fc3-288">Po kliknięciu powitalne iLMS kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour iLMS aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d9fc3-288">When you click hello iLMS tile in hello Access Panel, you should get automatically signed-on tooyour iLMS application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d9fc3-289">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="d9fc3-289">Additional resources</span></span>

* [<span data-ttu-id="d9fc3-290">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d9fc3-290">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d9fc3-291">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d9fc3-291">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_203.png

