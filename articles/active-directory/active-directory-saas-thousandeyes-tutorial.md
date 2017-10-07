---
title: 'Samouczek: Integracji Azure Active Directory z ThousandEyes | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i ThousandEyes."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 790e3f1e-1591-4dd6-87df-590b7bf8b4ba
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: jeedes
ms.openlocfilehash: fbfbfb71809355b1b138762757a851907737730b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thousandeyes"></a><span data-ttu-id="c5d83-103">Samouczek: Integracji Azure Active Directory z ThousandEyes</span><span class="sxs-lookup"><span data-stu-id="c5d83-103">Tutorial: Azure Active Directory integration with ThousandEyes</span></span>

<span data-ttu-id="c5d83-104">Z tego samouczka, dowiesz się, jak toointegrate ThousandEyes w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c5d83-104">In this tutorial, you learn how toointegrate ThousandEyes with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c5d83-105">Integracja z usługą Azure AD ThousandEyes zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="c5d83-105">Integrating ThousandEyes with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c5d83-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooThousandEyes</span><span class="sxs-lookup"><span data-stu-id="c5d83-106">You can control in Azure AD who has access tooThousandEyes</span></span>
- <span data-ttu-id="c5d83-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooThousandEyes (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5d83-107">You can enable your users tooautomatically get signed-on tooThousandEyes (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c5d83-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c5d83-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c5d83-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c5d83-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c5d83-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c5d83-110">Prerequisites</span></span>

<span data-ttu-id="c5d83-111">tooconfigure integracji z usługą Azure AD z ThousandEyes należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="c5d83-111">tooconfigure Azure AD integration with ThousandEyes, you need hello following items:</span></span>

- <span data-ttu-id="c5d83-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5d83-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c5d83-113">ThousandEyes logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="c5d83-113">A ThousandEyes single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c5d83-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="c5d83-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c5d83-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="c5d83-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c5d83-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="c5d83-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c5d83-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna tutaj: [oferta wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c5d83-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c5d83-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="c5d83-118">Scenario description</span></span>
<span data-ttu-id="c5d83-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="c5d83-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c5d83-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="c5d83-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c5d83-121">Dodawanie ThousandEyes z galerii hello</span><span class="sxs-lookup"><span data-stu-id="c5d83-121">Adding ThousandEyes from hello gallery</span></span>
2. <span data-ttu-id="c5d83-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="c5d83-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thousandeyes-from-hello-gallery"></a><span data-ttu-id="c5d83-123">Dodawanie ThousandEyes z galerii hello</span><span class="sxs-lookup"><span data-stu-id="c5d83-123">Adding ThousandEyes from hello gallery</span></span>
<span data-ttu-id="c5d83-124">tooconfigure hello integracji ThousandEyes do usługi Azure AD, należy tooadd ThousandEyes z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="c5d83-124">tooconfigure hello integration of ThousandEyes into Azure AD, you need tooadd ThousandEyes from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c5d83-125">**tooadd ThousandEyes z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="c5d83-125">**tooadd ThousandEyes from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5d83-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="c5d83-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="c5d83-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="c5d83-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c5d83-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="c5d83-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="c5d83-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c5d83-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="c5d83-133">W polu wyszukiwania hello wpisz **ThousandEyes**.</span><span class="sxs-lookup"><span data-stu-id="c5d83-133">In hello search box, type **ThousandEyes**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_search.png)

5. <span data-ttu-id="c5d83-135">W panelu wyników hello zaznacz **ThousandEyes**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="c5d83-135">In hello results panel, select **ThousandEyes**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c5d83-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="c5d83-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c5d83-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z ThousandEyes w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="c5d83-138">In this section, you configure and test Azure AD single sign-on with ThousandEyes based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c5d83-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w ThousandEyes jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c5d83-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ThousandEyes is tooa user in Azure AD.</span></span> <span data-ttu-id="c5d83-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w ThousandEyes musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="c5d83-140">In other words, a link relationship between an Azure AD user and hello related user in ThousandEyes needs toobe established.</span></span>

<span data-ttu-id="c5d83-141">W ThousandEyes, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="c5d83-141">In ThousandEyes, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c5d83-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z ThousandEyes, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="c5d83-142">tooconfigure and test Azure AD single sign-on with ThousandEyes, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c5d83-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="c5d83-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c5d83-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="c5d83-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c5d83-145">**[Tworzenie użytkownika testowego ThousandEyes](#creating-a-thousandeyes-test-user)**  -toohave odpowiednikiem Simona Britta w ThousandEyes, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c5d83-145">**[Creating a ThousandEyes test user](#creating-a-thousandeyes-test-user)** - toohave a counterpart of Britta Simon in ThousandEyes that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c5d83-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="c5d83-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c5d83-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="c5d83-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c5d83-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="c5d83-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c5d83-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="c5d83-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ThousandEyes application.</span></span>

<span data-ttu-id="c5d83-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z ThousandEyes, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="c5d83-150">**tooconfigure Azure AD single sign-on with ThousandEyes, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5d83-151">W portalu Azure na powitania hello **ThousandEyes** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="c5d83-151">In hello Azure portal, on hello **ThousandEyes** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="c5d83-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="c5d83-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_samlbase.png)

3. <span data-ttu-id="c5d83-155">Na powitania **ThousandEyes domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="c5d83-155">On hello **ThousandEyes Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_url.png)

    <span data-ttu-id="c5d83-157">W hello **adres URL logowania** tekstowym, wpisz adres URL jako:`https://app.thousandeyes.com/login/sso`</span><span class="sxs-lookup"><span data-stu-id="c5d83-157">In hello **Sign-on URL** textbox, type a URL as: `https://app.thousandeyes.com/login/sso`</span></span>

4. <span data-ttu-id="c5d83-158">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="c5d83-158">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_certificate.png) 

5. <span data-ttu-id="c5d83-160">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c5d83-160">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c5d83-162">Na powitania **konfiguracji ThousandEyes** kliknij **skonfigurować ThousandEyes** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="c5d83-162">On hello **ThousandEyes Configuration** section, click **Configure ThousandEyes** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c5d83-163">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="c5d83-163">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_configure.png) 

7. <span data-ttu-id="c5d83-165">W oknie przeglądarki innej witryny sieci web, zaloguj się na tooyour **ThousandEyes** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="c5d83-165">In a different web browser window, sign on tooyour **ThousandEyes** company site as an administrator.</span></span>

8. <span data-ttu-id="c5d83-166">W menu hello na górze hello, kliknij przycisk **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="c5d83-166">In hello menu on hello top, click **Settings**.</span></span>
   
    <span data-ttu-id="c5d83-167">![Ustawienia](./media/active-directory-saas-thousandeyes-tutorial/ic790066.png "ustawienia")</span><span class="sxs-lookup"><span data-stu-id="c5d83-167">![Settings](./media/active-directory-saas-thousandeyes-tutorial/ic790066.png "Settings")</span></span>

9. <span data-ttu-id="c5d83-168">Kliknij przycisk **konta**</span><span class="sxs-lookup"><span data-stu-id="c5d83-168">Click **Account**</span></span>
   
    <span data-ttu-id="c5d83-169">![Konto](./media/active-directory-saas-thousandeyes-tutorial/ic790067.png "konta")</span><span class="sxs-lookup"><span data-stu-id="c5d83-169">![Account](./media/active-directory-saas-thousandeyes-tutorial/ic790067.png "Account")</span></span>

10. <span data-ttu-id="c5d83-170">Kliknij przycisk hello **zabezpieczeń i uwierzytelniania** kartę.</span><span class="sxs-lookup"><span data-stu-id="c5d83-170">Click hello **Security & Authentication** tab.</span></span>
   
    <span data-ttu-id="c5d83-171">![Bezpieczeństwo i uwierzytelniania](./media/active-directory-saas-thousandeyes-tutorial/ic790068.png "zabezpieczeń i uwierzytelniania")</span><span class="sxs-lookup"><span data-stu-id="c5d83-171">![Security & Authentication](./media/active-directory-saas-thousandeyes-tutorial/ic790068.png "Security & Authentication")</span></span>

11. <span data-ttu-id="c5d83-172">W hello **ustawienia logowania jednokrotnego** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="c5d83-172">In hello **Setup Single Sign-On** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="c5d83-173">![Konfiguracja rejestracji jednokrotnej](./media/active-directory-saas-thousandeyes-tutorial/ic790069.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="c5d83-173">![Setup Single Sign-On](./media/active-directory-saas-thousandeyes-tutorial/ic790069.png "Setup Single Sign-On")</span></span>
  
    <span data-ttu-id="c5d83-174">a.</span><span class="sxs-lookup"><span data-stu-id="c5d83-174">a.</span></span> <span data-ttu-id="c5d83-175">Wybierz **Włącz rejestrację jednokrotną**.</span><span class="sxs-lookup"><span data-stu-id="c5d83-175">Select **Enable Single Sign-On**.</span></span>
  
    <span data-ttu-id="c5d83-176">b.</span><span class="sxs-lookup"><span data-stu-id="c5d83-176">b.</span></span> <span data-ttu-id="c5d83-177">W **adres URL strony logowania** pole tekstowe, Wklej **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c5d83-177">In **Login Page URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="c5d83-178">c.</span><span class="sxs-lookup"><span data-stu-id="c5d83-178">c.</span></span> <span data-ttu-id="c5d83-179">W **adres URL strony wylogowania** pole tekstowe, Wklej **Sign-Out URL** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c5d83-179">In **Logout Page URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="c5d83-180">d.</span><span class="sxs-lookup"><span data-stu-id="c5d83-180">d.</span></span> <span data-ttu-id="c5d83-181">**Wystawca dostawcy tożsamości** pole tekstowe, Wklej **identyfikator jednostki SAML** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c5d83-181">**Identity Provider Issuer** textbox, paste **SAML Entity ID** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="c5d83-182">e.</span><span class="sxs-lookup"><span data-stu-id="c5d83-182">e.</span></span> <span data-ttu-id="c5d83-183">W **certyfikatu weryfikacji**, kliknij przycisk **wybierz plik**, a następnie przekaż certyfikat hello został pobrany z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c5d83-183">In **Verification Certificate**, click **Choose file**, and then upload hello certificate you have downloaded from Azure portal.</span></span>
  
    <span data-ttu-id="c5d83-184">f.</span><span class="sxs-lookup"><span data-stu-id="c5d83-184">f.</span></span> <span data-ttu-id="c5d83-185">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="c5d83-185">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="c5d83-186">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="c5d83-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c5d83-187">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="c5d83-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c5d83-188">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c5d83-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c5d83-189">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5d83-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="c5d83-190">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="c5d83-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="c5d83-192">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="c5d83-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5d83-193">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="c5d83-193">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c5d83-195">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="c5d83-195">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c5d83-197">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c5d83-197">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c5d83-199">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="c5d83-199">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c5d83-201">a.</span><span class="sxs-lookup"><span data-stu-id="c5d83-201">a.</span></span> <span data-ttu-id="c5d83-202">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c5d83-202">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c5d83-203">b.</span><span class="sxs-lookup"><span data-stu-id="c5d83-203">b.</span></span> <span data-ttu-id="c5d83-204">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c5d83-204">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c5d83-205">c.</span><span class="sxs-lookup"><span data-stu-id="c5d83-205">c.</span></span> <span data-ttu-id="c5d83-206">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="c5d83-206">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c5d83-207">d.</span><span class="sxs-lookup"><span data-stu-id="c5d83-207">d.</span></span> <span data-ttu-id="c5d83-208">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="c5d83-208">Click **Create**.</span></span>
 
### <a name="creating-a-thousandeyes-test-user"></a><span data-ttu-id="c5d83-209">Tworzenie użytkownika testowego ThousandEyes</span><span class="sxs-lookup"><span data-stu-id="c5d83-209">Creating a ThousandEyes test user</span></span>

<span data-ttu-id="c5d83-210">W przypadku użytkowników usługi Azure AD toolog kolejności tooenable do ThousandEyes muszą mieć przydzielone do ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="c5d83-210">In order tooenable Azure AD users toolog into ThousandEyes, they must be provisioned into ThousandEyes.</span></span>  
<span data-ttu-id="c5d83-211">W przypadku hello ThousandEyes Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="c5d83-211">In hello case of ThousandEyes, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="c5d83-212">Możesz użyć innych ThousandEyes użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez tooprovision ThousandEyes usługi Azure Active Directory kont użytkowników.</span><span class="sxs-lookup"><span data-stu-id="c5d83-212">You can use any other ThousandEyes user account creation tools or APIs provided by ThousandEyes tooprovision Azure Active Directory user accounts.</span></span>

<span data-ttu-id="c5d83-213">**tooprovision tooThousandEyes konta użytkownika, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="c5d83-213">**tooprovision a user account tooThousandEyes, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5d83-214">Zaloguj się do witryny firmy ThousandEyes jako administrator.</span><span class="sxs-lookup"><span data-stu-id="c5d83-214">Log into your ThousandEyes company site as an administrator.</span></span>

2. <span data-ttu-id="c5d83-215">Kliknij przycisk **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="c5d83-215">Click **Settings**.</span></span>
   
    <span data-ttu-id="c5d83-216">![Ustawienia](./media/active-directory-saas-thousandeyes-tutorial/IC790066.png "ustawienia")</span><span class="sxs-lookup"><span data-stu-id="c5d83-216">![Settings](./media/active-directory-saas-thousandeyes-tutorial/IC790066.png "Settings")</span></span>

3. <span data-ttu-id="c5d83-217">Kliknij przycisk **konta**.</span><span class="sxs-lookup"><span data-stu-id="c5d83-217">Click **Account**.</span></span>
   
    <span data-ttu-id="c5d83-218">![Konto](./media/active-directory-saas-thousandeyes-tutorial/IC790067.png "konta")</span><span class="sxs-lookup"><span data-stu-id="c5d83-218">![Account](./media/active-directory-saas-thousandeyes-tutorial/IC790067.png "Account")</span></span>

4. <span data-ttu-id="c5d83-219">Kliknij przycisk hello **konta & użytkowników** kartę.</span><span class="sxs-lookup"><span data-stu-id="c5d83-219">Click hello **Accounts & Users** tab.</span></span>
   
    <span data-ttu-id="c5d83-220">![Konta & użytkowników](./media/active-directory-saas-thousandeyes-tutorial/IC790073.png "konta & użytkowników")</span><span class="sxs-lookup"><span data-stu-id="c5d83-220">![Accounts & Users](./media/active-directory-saas-thousandeyes-tutorial/IC790073.png "Accounts & Users")</span></span>

5. <span data-ttu-id="c5d83-221">W hello **Dodawanie użytkowników i kont** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="c5d83-221">In hello **Add Users & Accounts** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="c5d83-222">![Dodaj konta użytkowników](./media/active-directory-saas-thousandeyes-tutorial/IC790074.png "dodawania kont użytkowników")</span><span class="sxs-lookup"><span data-stu-id="c5d83-222">![Add User Accounts](./media/active-directory-saas-thousandeyes-tutorial/IC790074.png "Add User Accounts")</span></span>   
  
    <span data-ttu-id="c5d83-223">a.</span><span class="sxs-lookup"><span data-stu-id="c5d83-223">a.</span></span> <span data-ttu-id="c5d83-224">W **nazwa** pole tekstowe, nazwę użytkownika, takie jak hello typu **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="c5d83-224">In **Name** textbox, type hello name of user like **Britta Simon**.</span></span>

    <span data-ttu-id="c5d83-225">b.</span><span class="sxs-lookup"><span data-stu-id="c5d83-225">b.</span></span> <span data-ttu-id="c5d83-226">W **E-mail** pole tekstowe, powitalne wiadomości e-mail użytkownika, takich jak  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="c5d83-226">In **Email** textbox, type hello email of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="c5d83-227">b.</span><span class="sxs-lookup"><span data-stu-id="c5d83-227">b.</span></span> <span data-ttu-id="c5d83-228">Kliknij przycisk **tooAccount Dodaj nowego użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="c5d83-228">Click **Add New User tooAccount**.</span></span>
      
     >[!NOTE]
     ><span data-ttu-id="c5d83-229">Właściciel konta usługi Azure Active Directory Hello będzie otrzymasz wiadomość e-mail, w tym tooconfirm łącza i aktywować hello konta.</span><span class="sxs-lookup"><span data-stu-id="c5d83-229">hello Azure Active Directory account holder will get an email including a link tooconfirm and activate hello account.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c5d83-230">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5d83-230">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c5d83-231">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="c5d83-231">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooThousandEyes.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="c5d83-233">**tooassign tooThousandEyes Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="c5d83-233">**tooassign Britta Simon tooThousandEyes, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5d83-234">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="c5d83-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="c5d83-236">Z listy aplikacji hello wybierz **ThousandEyes**.</span><span class="sxs-lookup"><span data-stu-id="c5d83-236">In hello applications list, select **ThousandEyes**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_app.png) 

3. <span data-ttu-id="c5d83-238">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="c5d83-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="c5d83-240">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c5d83-240">Click **Add** button.</span></span> <span data-ttu-id="c5d83-241">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c5d83-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="c5d83-243">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="c5d83-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c5d83-244">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c5d83-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c5d83-245">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c5d83-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c5d83-246">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="c5d83-246">Testing single sign-on</span></span>

<span data-ttu-id="c5d83-247">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="c5d83-247">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c5d83-248">Po kliknięciu powitalne ThousandEyes kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour ThousandEyes aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c5d83-248">When you click hello ThousandEyes tile in hello Access Panel, you should get automatically signed-on tooyour ThousandEyes application.</span></span>

<span data-ttu-id="c5d83-249">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c5d83-249">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c5d83-250">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="c5d83-250">Additional resources</span></span>

* [<span data-ttu-id="c5d83-251">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c5d83-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c5d83-252">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c5d83-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_203.png

