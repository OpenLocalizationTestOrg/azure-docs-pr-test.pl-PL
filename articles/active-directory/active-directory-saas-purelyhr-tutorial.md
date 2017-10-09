---
title: 'Samouczek: Integracji Azure Active Directory z PurelyHR | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i PurelyHR."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 86a9c454-596d-4902-829a-fe126708f739
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: bdc1748ed650cff36b1ef7d7330dd2a17b3bc760
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-purelyhr"></a><span data-ttu-id="e7ce3-103">Samouczek: Integracji Azure Active Directory z PurelyHR</span><span class="sxs-lookup"><span data-stu-id="e7ce3-103">Tutorial: Azure Active Directory integration with PurelyHR</span></span>

<span data-ttu-id="e7ce3-104">Z tego samouczka, dowiesz się, jak toointegrate PurelyHR w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e7ce3-104">In this tutorial, you learn how toointegrate PurelyHR with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e7ce3-105">Integracja z usługą Azure AD PurelyHR zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="e7ce3-105">Integrating PurelyHR with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e7ce3-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooPurelyHR</span><span class="sxs-lookup"><span data-stu-id="e7ce3-106">You can control in Azure AD who has access tooPurelyHR</span></span>
- <span data-ttu-id="e7ce3-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooPurelyHR (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7ce3-107">You can enable your users tooautomatically get signed-on tooPurelyHR (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e7ce3-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="e7ce3-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e7ce3-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e7ce3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e7ce3-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e7ce3-110">Prerequisites</span></span>

<span data-ttu-id="e7ce3-111">tooconfigure integracji z usługą Azure AD z PurelyHR należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="e7ce3-111">tooconfigure Azure AD integration with PurelyHR, you need hello following items:</span></span>

- <span data-ttu-id="e7ce3-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7ce3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e7ce3-113">PurelyHR jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="e7ce3-113">A PurelyHR single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e7ce3-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e7ce3-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="e7ce3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e7ce3-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e7ce3-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e7ce3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e7ce3-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="e7ce3-118">Scenario description</span></span>
<span data-ttu-id="e7ce3-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e7ce3-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="e7ce3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e7ce3-121">Dodawanie PurelyHR z galerii hello</span><span class="sxs-lookup"><span data-stu-id="e7ce3-121">Adding PurelyHR from hello gallery</span></span>
2. <span data-ttu-id="e7ce3-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="e7ce3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-purelyhr-from-hello-gallery"></a><span data-ttu-id="e7ce3-123">Dodawanie PurelyHR z galerii hello</span><span class="sxs-lookup"><span data-stu-id="e7ce3-123">Adding PurelyHR from hello gallery</span></span>
<span data-ttu-id="e7ce3-124">tooconfigure hello integracji PurelyHR do usługi Azure AD, należy tooadd PurelyHR z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-124">tooconfigure hello integration of PurelyHR into Azure AD, you need tooadd PurelyHR from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e7ce3-125">**tooadd PurelyHR z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="e7ce3-125">**tooadd PurelyHR from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e7ce3-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="e7ce3-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e7ce3-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="e7ce3-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="e7ce3-133">W polu wyszukiwania hello wpisz **PurelyHR**.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-133">In hello search box, type **PurelyHR**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_search.png)

5. <span data-ttu-id="e7ce3-135">W panelu wyników hello zaznacz **PurelyHR**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-135">In hello results panel, select **PurelyHR**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e7ce3-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="e7ce3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e7ce3-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z PurelyHR na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="e7ce3-138">In this section, you configure and test Azure AD single sign-on with PurelyHR based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e7ce3-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w PurelyHR jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PurelyHR is tooa user in Azure AD.</span></span> <span data-ttu-id="e7ce3-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w PurelyHR musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-140">In other words, a link relationship between an Azure AD user and hello related user in PurelyHR needs toobe established.</span></span>

<span data-ttu-id="e7ce3-141">W PurelyHR, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-141">In PurelyHR, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e7ce3-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z PurelyHR, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="e7ce3-142">tooconfigure and test Azure AD single sign-on with PurelyHR, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e7ce3-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e7ce3-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e7ce3-145">**[Tworzenie użytkownika testowego PurelyHR](#creating-a-purelyhr-test-user)**  -toohave odpowiednikiem Simona Britta w PurelyHR, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-145">**[Creating a PurelyHR test user](#creating-a-purelyhr-test-user)** - toohave a counterpart of Britta Simon in PurelyHR that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e7ce3-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e7ce3-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e7ce3-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e7ce3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e7ce3-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your PurelyHR application.</span></span>

<span data-ttu-id="e7ce3-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z PurelyHR, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="e7ce3-150">**tooconfigure Azure AD single sign-on with PurelyHR, perform hello following steps:**</span></span>

1. <span data-ttu-id="e7ce3-151">W portalu Azure na powitania hello **PurelyHR** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-151">In hello Azure portal, on hello **PurelyHR** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="e7ce3-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_samlbase.png)

3. <span data-ttu-id="e7ce3-155">Na powitania **PurelyHR domeny i adres URL** sekcji, wykonaj następujące kroki, jeśli chcesz, aby aplikacja hello tooconfigure w hello **IDP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="e7ce3-155">On hello **PurelyHR Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_url.png)
   
    <span data-ttu-id="e7ce3-157">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyID>.purelyhr.com/sso-consume`</span><span class="sxs-lookup"><span data-stu-id="e7ce3-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyID>.purelyhr.com/sso-consume`</span></span>

4. <span data-ttu-id="e7ce3-158">Sprawdź **Pokaż zaawansowane ustawienia adresu URL**, jeśli chcesz, aby aplikacja hello tooconfigure w **SP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="e7ce3-158">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_url1.png)
    
    <span data-ttu-id="e7ce3-160">W hello **adres URL logowania** pole tekstowe, wartość hello typu przy użyciu hello następującego wzorca:`https://<companyID>.purelyhr.com/sso-initiate`</span><span class="sxs-lookup"><span data-stu-id="e7ce3-160">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://<companyID>.purelyhr.com/sso-initiate`</span></span>
     
    > [!NOTE]
    > <span data-ttu-id="e7ce3-161">Wartości te nie są hello prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-161">These values are not hello real.</span></span> <span data-ttu-id="e7ce3-162">Adres URL odpowiedzi rzeczywiste hello i adres URL logowania, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-162">Update these values with hello actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="e7ce3-163">Skontaktuj się z [zespołem pomocy technicznej klienta PurelyHR](http://support.purelyhr.com/) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-163">Contact [PurelyHR Client support team](http://support.purelyhr.com/) tooget these values.</span></span> 

5. <span data-ttu-id="e7ce3-164">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_certificate.png) 

6. <span data-ttu-id="e7ce3-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-purelyhr-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="e7ce3-168">Na powitania **konfiguracji PurelyHR** kliknij **skonfigurować PurelyHR** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-168">On hello **PurelyHR Configuration** section, click **Configure PurelyHR** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e7ce3-169">Kopiuj hello **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="e7ce3-169">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_configure.png) 

8. <span data-ttu-id="e7ce3-171">tooconfigure rejestracji jednokrotnej w **PurelyHR** strona, logowania tootheir witryny sieci Web jako administrator.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-171">tooconfigure single sign-on on **PurelyHR** side, login tootheir website as an administrator.</span></span>

9. <span data-ttu-id="e7ce3-172">Otwórz hello **pulpitu nawigacyjnego** opcje hello hello narzędzi i kliknij przycisk z **ustawienia logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-172">Open hello **Dashboard** from hello options in hello toolbar and click **SSO Settings**.</span></span>

10. <span data-ttu-id="e7ce3-173">Wklej hello wartości w polach hello opisane poniżej-</span><span class="sxs-lookup"><span data-stu-id="e7ce3-173">Paste hello values in hello boxes as described below-</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-purelyhr-tutorial/purelyhr-dashboard-sso-settings.png)    

    <span data-ttu-id="e7ce3-175">a.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-175">a.</span></span> <span data-ttu-id="e7ce3-176">Otwórz hello **Certificate(Bas64)** pobrane z hello portalu Azure w programie Notatnik i skopiuj wartości certyfikatu hello.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-176">Open hello **Certificate(Bas64)** downloaded from hello Azure portal in notepad and copy hello certificate value.</span></span> <span data-ttu-id="e7ce3-177">Witaj Wklej skopiowane wartości do hello **certyfikatu X.509** pole.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-177">Paste hello copied value into hello **X.509 Certificate** box.</span></span>

    <span data-ttu-id="e7ce3-178">b.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-178">b.</span></span> <span data-ttu-id="e7ce3-179">W hello **adres URL wystawcy Idp** Wklej hello **identyfikator jednostki SAML** skopiowanych z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-179">In hello **Idp Issuer URL** box, paste hello **SAML Entity ID** copied from hello Azure portal.</span></span>

    <span data-ttu-id="e7ce3-180">c.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-180">c.</span></span> <span data-ttu-id="e7ce3-181">W hello **adres URL punktu końcowego Idp** Wklej hello **SAML pojedynczy znak na adres URL usługi** skopiowanych z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-181">In hello **Idp Endpoint URL** box, paste hello **SAML Single Sign-On Service URL** copied from hello Azure portal.</span></span> 

    <span data-ttu-id="e7ce3-182">d.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-182">d.</span></span> <span data-ttu-id="e7ce3-183">Sprawdź hello **automatyczne tworzenie użytkowników** wyboru tooenable użytkownika automatycznego inicjowania obsługi administracyjnej w PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-183">Check hello **Auto-Create Users** checkbox tooenable automatic user provisioning in PurelyHR.</span></span>

    <span data-ttu-id="e7ce3-184">e.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-184">e.</span></span> <span data-ttu-id="e7ce3-185">Kliknij przycisk **Zapisz zmiany** toosave hello ustawienia.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-185">Click **Save Changes** toosave hello settings.</span></span>

> [!TIP]
> <span data-ttu-id="e7ce3-186">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="e7ce3-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e7ce3-187">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e7ce3-188">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e7ce3-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e7ce3-189">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7ce3-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="e7ce3-190">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="e7ce3-192">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="e7ce3-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e7ce3-193">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-193">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e7ce3-195">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-195">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e7ce3-197">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-197">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e7ce3-199">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="e7ce3-199">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e7ce3-201">a.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-201">a.</span></span> <span data-ttu-id="e7ce3-202">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-202">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e7ce3-203">b.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-203">b.</span></span> <span data-ttu-id="e7ce3-204">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-204">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e7ce3-205">c.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-205">c.</span></span> <span data-ttu-id="e7ce3-206">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-206">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e7ce3-207">d.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-207">d.</span></span> <span data-ttu-id="e7ce3-208">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-208">Click **Create**.</span></span>
 
### <a name="creating-a-purelyhr-test-user"></a><span data-ttu-id="e7ce3-209">Tworzenie użytkownika testowego PurelyHR</span><span class="sxs-lookup"><span data-stu-id="e7ce3-209">Creating a PurelyHR test user</span></span>

<span data-ttu-id="e7ce3-210">toolog użytkowników tooenable usługi Azure AD w tooPurelyHR, muszą mieć przydzielone do PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-210">tooenable Azure AD users toolog in tooPurelyHR, they must be provisioned into PurelyHR.</span></span> <span data-ttu-id="e7ce3-211">W PurelyHR Inicjowanie obsługi to zadanie automatycznej i są wymagane żadne czynności ręczne włączenie użytkownika automatycznego inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-211">In PurelyHR, provisioning is an automatic task and no manual steps are required when automatic user provisioning is enabled.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e7ce3-212">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7ce3-212">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e7ce3-213">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooPurelyHR.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-213">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPurelyHR.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="e7ce3-215">**tooassign tooPurelyHR Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="e7ce3-215">**tooassign Britta Simon tooPurelyHR, perform hello following steps:**</span></span>

1. <span data-ttu-id="e7ce3-216">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-216">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="e7ce3-218">Z listy aplikacji hello wybierz **PurelyHR**.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-218">In hello applications list, select **PurelyHR**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_app.png) 

3. <span data-ttu-id="e7ce3-220">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-220">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="e7ce3-222">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-222">Click **Add** button.</span></span> <span data-ttu-id="e7ce3-223">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-223">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="e7ce3-225">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-225">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e7ce3-226">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-226">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e7ce3-227">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-227">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e7ce3-228">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e7ce3-228">Testing single sign-on</span></span>

<span data-ttu-id="e7ce3-229">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-229">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e7ce3-230">Kliknij hello przyjęcia LMS kafelka w hello panelu dostępu get automatycznie zalogowane tooyour przyjęcia LMS aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-230">Click hello Absorb LMS tile in hello Access Panel, you get automatically signed-on tooyour Absorb LMS application.</span></span>

<span data-ttu-id="e7ce3-231">Aby uzyskać więcej informacji na temat hello Panel dostępu Zobacz.</span><span class="sxs-lookup"><span data-stu-id="e7ce3-231">For more information about hello Access Panel, see.</span></span> <span data-ttu-id="e7ce3-232">[Wprowadzenie toohello panelu dostępu](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="e7ce3-232">[Introduction toohello Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e7ce3-233">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="e7ce3-233">Additional resources</span></span>

* [<span data-ttu-id="e7ce3-234">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e7ce3-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e7ce3-235">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e7ce3-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_203.png

