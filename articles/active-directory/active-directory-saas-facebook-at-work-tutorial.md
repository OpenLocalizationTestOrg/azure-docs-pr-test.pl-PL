---
title: 'Samouczek: Integracji Azure Active Directory z miejsca pracy przez Facebook | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i miejsca pracy przez usługi Facebook."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: jeedes
ms.openlocfilehash: fd19b3f178a2aee7dd2f204d6d3cf6df8fe6b444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a><span data-ttu-id="65c62-103">Samouczek: Integracji Azure Active Directory z miejsca pracy przez usługi Facebook</span><span class="sxs-lookup"><span data-stu-id="65c62-103">Tutorial: Azure Active Directory integration with Workplace by Facebook</span></span>

<span data-ttu-id="65c62-104">Z tego samouczka, dowiesz się, jak toointegrate miejsca pracy w serwisie Facebook w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="65c62-104">In this tutorial, you learn how toointegrate Workplace by Facebook with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="65c62-105">Integrowanie miejsca pracy przez Facebook z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="65c62-105">Integrating Workplace by Facebook with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="65c62-106">Można kontrolować w usłudze Azure AD, kto ma dostęp tooWorkplace przez usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="65c62-106">You can control in Azure AD who has access tooWorkplace by Facebook.</span></span>
- <span data-ttu-id="65c62-107">Umożliwia użytkownikom tooautomatically uzyskać zalogowanego tooWorkplace przez Facebook (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65c62-107">You can enable your users tooautomatically get signed on tooWorkplace by Facebook (single sign-on) with their Azure AD accounts.</span></span>
- <span data-ttu-id="65c62-108">Możesz zarządzać kont w jednej centralnej lokalizacji: hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="65c62-108">You can manage your accounts in one central location: hello Azure portal.</span></span>

<span data-ttu-id="65c62-109">Aby uzyskać więcej informacji na temat oprogramowania jako usługa (SaaS) integracji aplikacji z usługą Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="65c62-109">For more details about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65c62-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="65c62-110">Prerequisites</span></span>

<span data-ttu-id="65c62-111">tooconfigure integracji usługi Azure AD z miejsca pracy przez usługi Facebook, należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="65c62-111">tooconfigure Azure AD integration with Workplace by Facebook, you need hello following items:</span></span>

- <span data-ttu-id="65c62-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="65c62-112">An Azure AD subscription</span></span>
- <span data-ttu-id="65c62-113">Dołączanie w serwisie Facebook rejestracji jednokrotnej (SSO) włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="65c62-113">A Workplace by Facebook single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="65c62-114">kroki hello tootest w tym samouczku, wykonaj te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="65c62-114">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="65c62-115">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="65c62-115">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="65c62-116">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="65c62-116">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="65c62-117">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="65c62-117">Scenario description</span></span>
<span data-ttu-id="65c62-118">W tym samouczku można przetestować logowania jednokrotnego programu Azure AD w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="65c62-118">In this tutorial, you test Azure AD SSO in a test environment.</span></span> <span data-ttu-id="65c62-119">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="65c62-119">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="65c62-120">Dodaj obszar roboczy w serwisie Facebook z galerii hello.</span><span class="sxs-lookup"><span data-stu-id="65c62-120">Add Workplace by Facebook from hello gallery.</span></span>
2. <span data-ttu-id="65c62-121">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="65c62-121">Configure and test Azure AD single sign-on.</span></span>

## <a name="add-workplace-by-facebook-from-hello-gallery"></a><span data-ttu-id="65c62-122">Dodawanie miejsca pracy przez Facebook z galerii hello</span><span class="sxs-lookup"><span data-stu-id="65c62-122">Add Workplace by Facebook from hello gallery</span></span>
<span data-ttu-id="65c62-123">tooconfigure hello integrację z miejsca pracy przez usługi Facebook usługi Azure AD, Dodaj obszar roboczy w serwisie Facebook hello galerii tooyour listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="65c62-123">tooconfigure hello integration of Workplace by Facebook into Azure AD, add Workplace by Facebook from hello gallery tooyour list of managed SaaS apps.</span></span>

1. <span data-ttu-id="65c62-124">W hello [portalu Azure](https://portal.azure.com), w lewym okienku hello, wybierz **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="65c62-124">In hello [Azure portal](https://portal.azure.com), in hello left pane, select **Azure Active Directory**.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="65c62-126">Przeglądaj zbyt**aplikacje dla przedsiębiorstw** > **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="65c62-126">Browse too**Enterprise applications** > **All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. <span data-ttu-id="65c62-128">tooadd hello nowej aplikacji, wybierz pozycję **nowej aplikacji** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="65c62-128">tooadd hello new application, select **New application** on hello top of hello dialog box.</span></span>

    ![Nowy przycisk aplikacji Hello][3]

4. <span data-ttu-id="65c62-130">W polu wyszukiwania hello wpisz **miejsca pracy przez Facebook**i wybierz **miejsca pracy przez Facebook** z wyników.</span><span class="sxs-lookup"><span data-stu-id="65c62-130">In hello search box, type **Workplace by Facebook**, and select **Workplace by Facebook** from results.</span></span> <span data-ttu-id="65c62-131">Następnie wybierz **Dodaj**, tooadd hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="65c62-131">Then select **Add**, tooadd hello application.</span></span>

    ![Obszar roboczy w serwisie Facebook hello listy wyników](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_search.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="65c62-133">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="65c62-133">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="65c62-134">W tej sekcji Konfiguracja i testowanie usługi Azure AD SSO z miejsca pracy przez Facebook, na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="65c62-134">In this section, you configure and test Azure AD SSO with Workplace by Facebook, based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="65c62-135">Aby toowork logowania jednokrotnego usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w miejscu pracy przez Facebook jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65c62-135">For SSO toowork, Azure AD needs tooknow what hello counterpart user in Workplace by Facebook is tooa user in Azure AD.</span></span> <span data-ttu-id="65c62-136">Innymi słowy można ustanowić połączonego relacji między użytkownika usługi Azure AD i hello użytkownikowi w miejscu pracy przez usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="65c62-136">In other words, a linked relationship between an Azure AD user and hello related user in Workplace by Facebook should be established.</span></span>

<span data-ttu-id="65c62-137">Ustanowić tę relację, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w miejscu pracy przez usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="65c62-137">Establish this relationship by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Workplace by Facebook.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="65c62-138">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="65c62-138">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="65c62-139">W tej sekcji włączenia funkcji logowania jednokrotnego usługi Azure AD w portalu Azure hello i konfigurowanie logowania jednokrotnego w miejscu pracy aplikacji usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="65c62-139">In this section, you enable Azure AD SSO in hello Azure portal, and you configure SSO in your Workplace by Facebook application.</span></span>

1. <span data-ttu-id="65c62-140">W portalu Azure na powitania hello **miejsca pracy przez Facebook** strona integracji aplikacji, wybierz opcję **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="65c62-140">In hello Azure portal, on hello **Workplace by Facebook** application integration page, select **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="65c62-142">W hello **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="65c62-142">In hello **Single sign-on** dialog box, select **Mode** as **SAML-based Sign-on** tooenable SSO.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. <span data-ttu-id="65c62-144">W hello **miejsca pracy przez domenę usługi Facebook i adresy URL** sekcji, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="65c62-144">In hello **Workplace by Facebook Domain and URLs** section, do hello following:</span></span>

    <span data-ttu-id="65c62-145">a.</span><span class="sxs-lookup"><span data-stu-id="65c62-145">a.</span></span> <span data-ttu-id="65c62-146">W hello **adres URL logowania** wpisz adres URL, który używa hello następującego wzorca:`https://<company subdomain>.facebook.com`</span><span class="sxs-lookup"><span data-stu-id="65c62-146">In hello **Sign-on URL** text box, type a URL that uses hello following pattern: `https://<company subdomain>.facebook.com`</span></span>

    <span data-ttu-id="65c62-147">b.</span><span class="sxs-lookup"><span data-stu-id="65c62-147">b.</span></span> <span data-ttu-id="65c62-148">W hello **identyfikator** wpisz adres URL, który używa hello następującego wzorca:`https://www.facebook.com/company/<scim company id>`</span><span class="sxs-lookup"><span data-stu-id="65c62-148">In hello **Identifier** text box, type a URL that uses hello following pattern: `https://www.facebook.com/company/<scim company id>`</span></span>

    > [!NOTE]
    > <span data-ttu-id="65c62-149">Te wartości są tylko przykładem.</span><span class="sxs-lookup"><span data-stu-id="65c62-149">These values are an example only.</span></span> <span data-ttu-id="65c62-150">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="65c62-150">Update these values with hello actual sign-on URL and identifier.</span></span> <span data-ttu-id="65c62-151">Skontaktuj się z pomocą hello [miejsca pracy przez zespół obsługi klienta usługi Facebook](https://workplace.fb.com/faq/) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="65c62-151">Contact hello [Workplace by Facebook Client support team](https://workplace.fb.com/faq/) tooget these values.</span></span> 

4. <span data-ttu-id="65c62-152">W hello **SAML certyfikat podpisywania** wybierz opcję **certyfikatu (Base64)**, a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="65c62-152">In hello **SAML Signing Certificate** section, select **Certificate (Base64)**, and then save hello certificate file on your computer.</span></span>

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. <span data-ttu-id="65c62-154">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="65c62-154">Select **Save**.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="65c62-156">W hello **miejsca pracy przez konfigurację usługi Facebook** zaznacz **skonfigurować miejsca pracy przez Facebook** tooopen hello **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="65c62-156">In hello **Workplace by Facebook Configuration** section, select **Configure Workplace by Facebook** tooopen hello **Configure sign-on** window.</span></span> <span data-ttu-id="65c62-157">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **krótkimi opisami** sekcji.</span><span class="sxs-lookup"><span data-stu-id="65c62-157">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference** section.</span></span>

    ![Obszar roboczy w konfiguracji usługi Facebook](./media/active-directory-saas-facebook-at-work-tutorial/config.png) 

7. <span data-ttu-id="65c62-159">W oknie przeglądarki innej witryny sieci web Zaloguj się tooyour miejsca pracy przez Facebook witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="65c62-159">In a different web browser window, sign in tooyour Workplace by Facebook company site as an administrator.</span></span>
  
   > [!NOTE] 
   > <span data-ttu-id="65c62-160">W ramach procesu uwierzytelniania SAML hello miejsca pracy można użyć ciągów zapytania zapasowej kilobajtów too2.5 rozmiar w kolejności toopass parametry tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="65c62-160">As part of hello SAML authentication process, Workplace can use query strings of up too2.5 kilobytes in size in order toopass parameters tooAzure AD.</span></span>

8. <span data-ttu-id="65c62-161">W hello **pulpitu nawigacyjnego firmy**, przejdź toohello **uwierzytelniania** kartę.</span><span class="sxs-lookup"><span data-stu-id="65c62-161">In hello **Company Dashboard**, go toohello **Authentication** tab.</span></span>

9. <span data-ttu-id="65c62-162">W obszarze **uwierzytelnianie SAML**, wybierz pozycję **logowania jednokrotnego tylko** z listy rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="65c62-162">Under **SAML Authentication**, select **SSO Only** from hello drop-down list.</span></span>

10. <span data-ttu-id="65c62-163">Wprowadź wartości hello skopiowanych z hello **miejsca pracy przez konfigurację usługi Facebook** sekcji hello portalu Azure do odpowiednich pól hello:</span><span class="sxs-lookup"><span data-stu-id="65c62-163">Enter hello values copied from hello **Workplace by Facebook Configuration** section of hello Azure portal into hello corresponding fields:</span></span>

    *   <span data-ttu-id="65c62-164">W **adres URL SAML** pole tekstowe, Wklej wartość hello **pojedynczy znak na adres URL usługi**, które zostały skopiowane z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="65c62-164">In the **SAML URL** text box, paste hello value of **Single Sign-On Service URL**, which you have copied from hello Azure portal.</span></span>
    *   <span data-ttu-id="65c62-165">W **adres URL wystawcy SAML** pole tekstowe, Wklej hello wartość **identyfikator jednostki SAML**, które zostały skopiowane z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="65c62-165">In the **SAML Issuer URL** text box, paste hello value of **SAML Entity ID**, which you have copied from hello Azure portal.</span></span>
    *   <span data-ttu-id="65c62-166">W **SAML wylogowania przekierowania (opcjonalnie)**, Wklej wartość hello **Sign-Out URL**, które zostały skopiowane z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="65c62-166">In **SAML Logout Redirect (optional)**, paste hello value of **Sign-Out URL**, which you have copied from hello Azure portal.</span></span>
    *   <span data-ttu-id="65c62-167">Otwórz z **certyfikatu algorytmem base-64** w Notatniku pobrane z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="65c62-167">Open your **base-64 encoded certificate** in Notepad, downloaded from hello Azure portal.</span></span> <span data-ttu-id="65c62-168">Skopiuj zawartość hello go do Schowka, a następnie wklej go toothe **certyfikatu SAML** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="65c62-168">Copy hello content of it into your clipboard, and then paste it toothe **SAML Certificate** text box.</span></span>

11. <span data-ttu-id="65c62-169">Może być konieczne odbiorców hello tooenter adres URL, adres URL odbiorcy i ACS (usługa konsumenta potwierdzenia) adres URL, na liście hello **Konfiguracja SAML** sekcji.</span><span class="sxs-lookup"><span data-stu-id="65c62-169">You might need tooenter hello audience URL, recipient URL, and ACS (Assertion Consumer Service) URL, listed under hello **SAML Configuration** section.</span></span>

12. <span data-ttu-id="65c62-170">Przewiń toohello dołu hello sekcji, a następnie wybierz **Test rejestracji Jednokrotnej**.</span><span class="sxs-lookup"><span data-stu-id="65c62-170">Scroll toohello bottom of hello section, and select **Test SSO**.</span></span> <span data-ttu-id="65c62-171">Zostanie wyświetlone okno podręczne ze strony logowania hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65c62-171">A pop-up window appears, with hello Azure AD sign-in page.</span></span> <span data-ttu-id="65c62-172">tooauthenticate, wprowadź swoje poświadczenia, jak zwykle.</span><span class="sxs-lookup"><span data-stu-id="65c62-172">tooauthenticate, enter your credentials as normal.</span></span> <span data-ttu-id="65c62-173">Upewnij się, adres e-mail hello zwrócony z usługi Azure AD jest taki sam, jak hello konto firmowe, w którym użytkownik jest zalogowany przy użyciu hello.</span><span class="sxs-lookup"><span data-stu-id="65c62-173">Ensure hello email address returned back from Azure AD is hello same as hello Workplace account you are logged in with.</span></span>

13. <span data-ttu-id="65c62-174">Jeśli hello test zakończyło się pomyślnie, przewiń toohello u dołu strony hello oraz wybierz **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="65c62-174">If hello test has finished successfully, scroll toohello bottom of hello page and select **Save**.</span></span>

14. <span data-ttu-id="65c62-175">Teraz przedstawiono wszystkich osób korzystających z miejsca pracy z usługą Azure AD strony logowania dla uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="65c62-175">Anyone using Workplace is now presented with Azure AD sign-in page for authentication.</span></span>

<span data-ttu-id="65c62-176">Możesz wybrać tooconfigure SAML wylogowaniu adresu URL, który może być używane toopoint na wyrejestrowywania hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65c62-176">You can choose tooconfigure a SAML sign out URL, which can be used toopoint at hello Azure AD sign-out page.</span></span> <span data-ttu-id="65c62-177">Gdy to ustawienie jest włączone i skonfigurowane, hello użytkownik nie jest już wyrejestrowywania toohello bezpośrednie miejsca pracy.</span><span class="sxs-lookup"><span data-stu-id="65c62-177">When this setting is enabled and configured, hello user is no longer directed toohello Workplace sign-out page.</span></span> <span data-ttu-id="65c62-178">Zamiast tego użytkownik hello jest toohello przekierowany adres URL, który został dodany w ustawieniu przekierowania wylogowania SAML hello.</span><span class="sxs-lookup"><span data-stu-id="65c62-178">Instead, hello user is redirected toohello URL that was added in hello SAML sign-out redirect setting.</span></span>


> [!TIP]
> <span data-ttu-id="65c62-179">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="65c62-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app.</span></span> <span data-ttu-id="65c62-180">Po dodaniu tej aplikacji z hello **usługi Active Directory** > **aplikacje dla przedsiębiorstw** po prostu wybierz hello **rejestracji jednokrotnej** kartę i hello dostępu osadzone dokumentacji za pośrednictwem hello **konfiguracji** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="65c62-180">After adding this app from hello **Active Directory** > **Enterprise Applications** section, simply select hello **Single Sign-On** tab, and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="65c62-181">Więcej o hello osadzonych dokumentacji funkcji w hello [usługi Azure AD osadzonych dokumentacji]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="65c62-181">You can read more about hello embedded documentation feature in hello [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="configure-reauthentication-frequency"></a><span data-ttu-id="65c62-182">Konfigurowanie częstotliwości ponowne uwierzytelnianie</span><span class="sxs-lookup"><span data-stu-id="65c62-182">Configure reauthentication frequency</span></span>

<span data-ttu-id="65c62-183">Można skonfigurować tooprompt dołączanie sprawdzania SAML codziennie trzech dni, co tydzień, dwa tygodnie, co miesiąc lub nigdy.</span><span class="sxs-lookup"><span data-stu-id="65c62-183">You can configure Workplace tooprompt for a SAML check every day, three days, one week, two weeks, one month, or never.</span></span>

> [!NOTE] 
><span data-ttu-id="65c62-184">Hello minimalną wartość sprawdzania SAML hello w aplikacjach mobilnych ustawiono tooone tygodnia.</span><span class="sxs-lookup"><span data-stu-id="65c62-184">hello minimum value for hello SAML check on mobile applications is set tooone week.</span></span>

<span data-ttu-id="65c62-185">Możesz też wymusić SAML zresetować dla wszystkich użytkowników.</span><span class="sxs-lookup"><span data-stu-id="65c62-185">You can also force a SAML reset for all users.</span></span> <span data-ttu-id="65c62-186">toodo hello, użyj **SAML wymagają uwierzytelniania wszystkich użytkowników, którzy teraz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="65c62-186">toodo this, use hello **Require SAML authentication for all users now** button.</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="65c62-187">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="65c62-187">Create an Azure AD test user</span></span>
<span data-ttu-id="65c62-188">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="65c62-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

1. <span data-ttu-id="65c62-190">W hello **portalu Azure**, w lewym okienku hello, wybierz **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="65c62-190">In hello **Azure portal**, in hello left pane, select **Azure Active Directory**.</span></span>

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="65c62-192">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**i wybierz **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="65c62-192">toodisplay hello list of users, go too**Users and groups**, and select **All users**.</span></span>
    
    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="65c62-194">Witaj tooopen **użytkownika** okno dialogowe, wybierz opcję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="65c62-194">tooopen hello **User** dialog box, select **Add**.</span></span>
 
    ![przycisk Dodaj Hello](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="65c62-196">W hello **użytkownika** okna dialogowego pozycję hello następujące:</span><span class="sxs-lookup"><span data-stu-id="65c62-196">In hello **User** dialog box, do hello following:</span></span>
 
    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="65c62-198">a.</span><span class="sxs-lookup"><span data-stu-id="65c62-198">a.</span></span> <span data-ttu-id="65c62-199">W hello **nazwa** polu tekstowym **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="65c62-199">In hello **Name** text box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="65c62-200">b.</span><span class="sxs-lookup"><span data-stu-id="65c62-200">b.</span></span> <span data-ttu-id="65c62-201">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="65c62-201">In hello **User name** text box, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="65c62-202">c.</span><span class="sxs-lookup"><span data-stu-id="65c62-202">c.</span></span> <span data-ttu-id="65c62-203">Wybierz **Pokaż hasło**i zapisz ją.</span><span class="sxs-lookup"><span data-stu-id="65c62-203">Select **Show Password**, and write it down.</span></span>

    <span data-ttu-id="65c62-204">d.</span><span class="sxs-lookup"><span data-stu-id="65c62-204">d.</span></span> <span data-ttu-id="65c62-205">Wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="65c62-205">Select **Create**.</span></span>
 
### <a name="create-a-workplace-by-facebook-test-user"></a><span data-ttu-id="65c62-206">Utwórz pracy przez użytkownika testowego usługi Facebook</span><span class="sxs-lookup"><span data-stu-id="65c62-206">Create a Workplace by Facebook test user</span></span>

<span data-ttu-id="65c62-207">W tej sekcji o nazwie Simona Britta tworzenia użytkownika w miejscu pracy przez usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="65c62-207">In this section, a user called Britta Simon is created in Workplace by Facebook.</span></span> <span data-ttu-id="65c62-208">Obszar roboczy w serwisie Facebook obsługę w czasie, który jest domyślnie włączona.</span><span class="sxs-lookup"><span data-stu-id="65c62-208">Workplace by Facebook supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="65c62-209">Brak akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="65c62-209">There is no action for you in this section.</span></span> <span data-ttu-id="65c62-210">Jeśli użytkownik nie istnieje w miejscu pracy przez usługi Facebook, nowy jest tworzona podczas próby tooaccess miejsca pracy przez Facebook.</span><span class="sxs-lookup"><span data-stu-id="65c62-210">If a user doesn't exist in Workplace by Facebook, a new one is created when you attempt tooaccess Workplace by Facebook.</span></span>

>[!Note]
><span data-ttu-id="65c62-211">Toocreate użytkownik ręcznie, należy skontaktować się z hello [miejsca pracy przez zespół obsługi klienta usługi Facebook](https://workplace.fb.com/faq/).</span><span class="sxs-lookup"><span data-stu-id="65c62-211">If you need toocreate a user manually, contact hello [Workplace by Facebook Client support team](https://workplace.fb.com/faq/).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="65c62-212">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="65c62-212">Assign hello Azure AD test user</span></span>

<span data-ttu-id="65c62-213">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooWorkplace przez usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="65c62-213">In this section, you enable Britta Simon toouse Azure SSO by granting access tooWorkplace by Facebook.</span></span>

![Przypisz użytkownika][200] 

1. <span data-ttu-id="65c62-215">W hello Azure umożliwia wyświetlanie aplikacji hello portalu, Otwórz.</span><span class="sxs-lookup"><span data-stu-id="65c62-215">In hello Azure portal, open hello applications view.</span></span> <span data-ttu-id="65c62-216">Przejdź do widoku katalogu toohello znajduje się zbyt**aplikacje dla przedsiębiorstw**, a następnie wybierz **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="65c62-216">Go toohello directory view, go too**Enterprise applications**, and then select **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="65c62-218">Z listy aplikacji hello wybierz **miejsca pracy przez Facebook**.</span><span class="sxs-lookup"><span data-stu-id="65c62-218">In hello applications list, select **Workplace by Facebook**.</span></span>

    ![Witaj miejsca pracy przez łącze usługi Facebook na liście aplikacji hello](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_app.png) 

3. <span data-ttu-id="65c62-220">W menu hello powitania po lewej stronie wybierz **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="65c62-220">In hello menu on hello left, select **Users and groups**.</span></span>

    ![łącze "Użytkownicy i grupy" Hello][202] 

4. <span data-ttu-id="65c62-222">Wybierz pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="65c62-222">Select **Add**.</span></span> <span data-ttu-id="65c62-223">Następnie w hello **Dodaj przydziału** okienku wybierz **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="65c62-223">Then, in hello **Add Assignment** pane, select **Users and groups**.</span></span>

    ![Okienko Dodaj przypisania Hello][203]

5. <span data-ttu-id="65c62-225">W hello **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="65c62-225">In hello **Users and groups** dialog box, select **Britta Simon** in hello users list.</span></span>

6. <span data-ttu-id="65c62-226">W hello **użytkowników i grup** okno dialogowe, wybierz opcję **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="65c62-226">In hello **Users and groups** dialog box, select **Select**.</span></span>

7. <span data-ttu-id="65c62-227">W hello **Dodaj przydziału** okno dialogowe, wybierz opcję **przypisać**.</span><span class="sxs-lookup"><span data-stu-id="65c62-227">In hello **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="65c62-228">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="65c62-228">Test single sign-on</span></span>

<span data-ttu-id="65c62-229">Jeśli chcesz tootest ustawienia logowania jednokrotnego, otwórz hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="65c62-229">If you want tootest your SSO settings, open hello Access Panel.</span></span>
<span data-ttu-id="65c62-230">Aby uzyskać więcej informacji, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="65c62-230">For more information, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="65c62-231">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="65c62-231">Next steps</span></span>

* <span data-ttu-id="65c62-232">Zobacz hello [lista samouczków dotyczących toointegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md).</span><span class="sxs-lookup"><span data-stu-id="65c62-232">See hello [list of tutorials on how toointegrate SaaS Apps with Azure Active Directory](active-directory-saas-tutorial-list.md).</span></span>
* <span data-ttu-id="65c62-233">Odczyt [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="65c62-233">Read [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>
* <span data-ttu-id="65c62-234">Dowiedz się więcej o tym, jak za[skonfigurować Inicjowanie obsługi użytkowników](active-directory-saas-facebook-at-work-provisioning-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="65c62-234">Learn more about how too[configure user provisioning](active-directory-saas-facebook-at-work-provisioning-tutorial.md).</span></span>



<!--Image references-->

[1]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_203.png

