---
title: 'Samouczek: Integracji Azure Active Directory z Pantheon | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Pantheon."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2c965d1-666f-44c2-b08f-b73163096374
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 5c3e54aef1f64dbab77d40a8c098172d609bfec8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pantheon"></a><span data-ttu-id="59228-103">Samouczek: Integracji Azure Active Directory z Pantheon</span><span class="sxs-lookup"><span data-stu-id="59228-103">Tutorial: Azure Active Directory integration with Pantheon</span></span>

<span data-ttu-id="59228-104">Z tego samouczka, dowiesz się, jak toointegrate Pantheon w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="59228-104">In this tutorial, you learn how toointegrate Pantheon with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="59228-105">Integracja z usługą Azure AD Pantheon zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="59228-105">Integrating Pantheon with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="59228-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooPantheon</span><span class="sxs-lookup"><span data-stu-id="59228-106">You can control in Azure AD who has access tooPantheon</span></span>
- <span data-ttu-id="59228-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooPantheon (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="59228-107">You can enable your users tooautomatically get signed-on tooPantheon (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="59228-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="59228-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="59228-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="59228-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="59228-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="59228-110">Prerequisites</span></span>

<span data-ttu-id="59228-111">tooconfigure integracji z usługą Azure AD z Pantheon należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="59228-111">tooconfigure Azure AD integration with Pantheon, you need hello following items:</span></span>

- <span data-ttu-id="59228-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="59228-112">An Azure AD subscription</span></span>
- <span data-ttu-id="59228-113">Pantheon logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="59228-113">A Pantheon single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="59228-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="59228-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="59228-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="59228-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="59228-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="59228-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="59228-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="59228-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="59228-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="59228-118">Scenario description</span></span>
<span data-ttu-id="59228-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="59228-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="59228-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="59228-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="59228-121">Dodawanie Pantheon z galerii hello</span><span class="sxs-lookup"><span data-stu-id="59228-121">Adding Pantheon from hello gallery</span></span>
2. <span data-ttu-id="59228-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="59228-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pantheon-from-hello-gallery"></a><span data-ttu-id="59228-123">Dodawanie Pantheon z galerii hello</span><span class="sxs-lookup"><span data-stu-id="59228-123">Adding Pantheon from hello gallery</span></span>
<span data-ttu-id="59228-124">tooconfigure hello integracji Pantheon do usługi Azure AD, należy tooadd Pantheon z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="59228-124">tooconfigure hello integration of Pantheon into Azure AD, you need tooadd Pantheon from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="59228-125">**tooadd Pantheon z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="59228-125">**tooadd Pantheon from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="59228-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="59228-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="59228-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="59228-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="59228-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="59228-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="59228-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="59228-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="59228-133">W polu wyszukiwania hello wpisz **Pantheon**.</span><span class="sxs-lookup"><span data-stu-id="59228-133">In hello search box, type **Pantheon**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_search.png)

5. <span data-ttu-id="59228-135">W panelu wyników hello zaznacz **Pantheon**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="59228-135">In hello results panel, select **Pantheon**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="59228-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="59228-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="59228-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Pantheon w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="59228-138">In this section, you configure and test Azure AD single sign-on with Pantheon based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="59228-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Pantheon jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="59228-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Pantheon is tooa user in Azure AD.</span></span> <span data-ttu-id="59228-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Pantheon musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="59228-140">In other words, a link relationship between an Azure AD user and hello related user in Pantheon needs toobe established.</span></span>

<span data-ttu-id="59228-141">W Pantheon, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="59228-141">In Pantheon, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="59228-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Pantheon, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="59228-142">tooconfigure and test Azure AD single sign-on with Pantheon, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="59228-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="59228-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="59228-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="59228-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="59228-145">**[Tworzenie użytkownika testowego Pantheon](#creating-a-pantheon-test-user)**  -toohave odpowiednikiem Simona Britta w Pantheon, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="59228-145">**[Creating a Pantheon test user](#creating-a-pantheon-test-user)** - toohave a counterpart of Britta Simon in Pantheon that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="59228-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="59228-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="59228-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="59228-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="59228-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="59228-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="59228-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Pantheon.</span><span class="sxs-lookup"><span data-stu-id="59228-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Pantheon application.</span></span>

<span data-ttu-id="59228-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Pantheon, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="59228-150">**tooconfigure Azure AD single sign-on with Pantheon, perform hello following steps:**</span></span>

1. <span data-ttu-id="59228-151">W portalu Azure na powitania hello **Pantheon** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="59228-151">In hello Azure portal, on hello **Pantheon** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="59228-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="59228-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_samlbase.png)

3. <span data-ttu-id="59228-155">Na powitania **Pantheon domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="59228-155">On hello **Pantheon Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_url.png)

    <span data-ttu-id="59228-157">a.</span><span class="sxs-lookup"><span data-stu-id="59228-157">a.</span></span> <span data-ttu-id="59228-158">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`urn:auth0:pantheon:<orgname>-SSO`</span><span class="sxs-lookup"><span data-stu-id="59228-158">In hello **Identifier** textbox, type a URL using hello following pattern: `urn:auth0:pantheon:<orgname>-SSO`</span></span>

    <span data-ttu-id="59228-159">b.</span><span class="sxs-lookup"><span data-stu-id="59228-159">b.</span></span> <span data-ttu-id="59228-160">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://pantheon.auth0.com/login/callback?connection=<orgname>-SSO`</span><span class="sxs-lookup"><span data-stu-id="59228-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://pantheon.auth0.com/login/callback?connection=<orgname>-SSO`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="59228-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="59228-161">These values are not real.</span></span> <span data-ttu-id="59228-162">Witaj rzeczywisty identyfikator i odpowiedzi adresu URL, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="59228-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="59228-163">Skontaktuj się z [zespołem pomocy technicznej Pantheon](https://pantheon.io/docs/getting-support/) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="59228-163">Contact [Pantheon support team](https://pantheon.io/docs/getting-support/) tooget these values.</span></span>

4. <span data-ttu-id="59228-164">Aplikacja pantheon oczekuje hello potwierdzenia języka SAML w określonym formacie, który wymaga możesz tooset hello UserIdentifier wartość atrybutu z adresu e-mail użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="59228-164">Pantheon application expects hello SAML assertion in specific format, which requires you tooset hello UserIdentifier attribute value with hello user’s email address.</span></span> <span data-ttu-id="59228-165">Domyślnie usługi Azure AD używa hello UserPrincipalName UserIdentifier atrybutu.</span><span class="sxs-lookup"><span data-stu-id="59228-165">By default Azure AD uses hello UserPrincipalName for UserIdentifier attribute.</span></span> <span data-ttu-id="59228-166">Jednak dla pomyślnej integracji tooadjust toomatch tej wartości z adresu e-mail użytkownika.</span><span class="sxs-lookup"><span data-stu-id="59228-166">But for successful integration you need tooadjust this value toomatch with user’s email address.</span></span> <span data-ttu-id="59228-167">Integracja Hello działa tylko po wykonaniu hello poprawne mapowania.</span><span class="sxs-lookup"><span data-stu-id="59228-167">hello integration will only work after doing hello correct mapping.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pantheon-tutorial/tutorial_attribute.png)  


5. <span data-ttu-id="59228-169">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="59228-169">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_certificate.png)

6. <span data-ttu-id="59228-171">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="59228-171">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pantheon-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="59228-173">Na powitania **konfiguracji Pantheon** kliknij **skonfigurować Pantheon** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="59228-173">On hello **Pantheon Configuration** section, click **Configure Pantheon** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="59228-174">Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="59228-174">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_configure.png) 

8. <span data-ttu-id="59228-176">tooconfigure rejestracji jednokrotnej w **Pantheon** strony, należy pobrać hello toosend **certyfikatu** i **SAML pojedynczy znak na adres URL usługi** zbyt[Pantheon obsługuje zespołu](https://pantheon.io/docs/getting-support/).</span><span class="sxs-lookup"><span data-stu-id="59228-176">tooconfigure single sign-on on **Pantheon** side, you need toosend hello downloaded **Certificate** and **SAML Single Sign-On Service URL** too[Pantheon support team](https://pantheon.io/docs/getting-support/).</span></span>

     > [!Note]
     > <span data-ttu-id="59228-177">Należy również tooprovide hello domeny poczty E-mail informacji i Data i godzina należy tooenable tego połączenia.</span><span class="sxs-lookup"><span data-stu-id="59228-177">You also need tooprovide hello Email Domain(s) information and Date Time when you want tooenable this connection.</span></span> <span data-ttu-id="59228-178">Można znaleźć więcej szczegółów na temat z [tutaj](https://pantheon.io/docs/sso-organizations/)</span><span class="sxs-lookup"><span data-stu-id="59228-178">You can find more details about it from [here](https://pantheon.io/docs/sso-organizations/)</span></span>

> [!TIP]
> <span data-ttu-id="59228-179">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="59228-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="59228-180">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="59228-180">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="59228-181">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="59228-181">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="59228-182">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="59228-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="59228-183">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="59228-183">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="59228-185">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="59228-185">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="59228-186">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="59228-186">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="59228-188">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="59228-188">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="59228-190">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="59228-190">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="59228-192">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="59228-192">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="59228-194">a.</span><span class="sxs-lookup"><span data-stu-id="59228-194">a.</span></span> <span data-ttu-id="59228-195">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="59228-195">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="59228-196">b.</span><span class="sxs-lookup"><span data-stu-id="59228-196">b.</span></span> <span data-ttu-id="59228-197">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="59228-197">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="59228-198">c.</span><span class="sxs-lookup"><span data-stu-id="59228-198">c.</span></span> <span data-ttu-id="59228-199">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="59228-199">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="59228-200">d.</span><span class="sxs-lookup"><span data-stu-id="59228-200">d.</span></span> <span data-ttu-id="59228-201">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="59228-201">Click **Create**.</span></span>
 
### <a name="creating-a-pantheon-test-user"></a><span data-ttu-id="59228-202">Tworzenie użytkownika testowego Pantheon</span><span class="sxs-lookup"><span data-stu-id="59228-202">Creating a Pantheon test user</span></span>

<span data-ttu-id="59228-203">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Pantheon.</span><span class="sxs-lookup"><span data-stu-id="59228-203">In this section, you create a user called Britta Simon in Pantheon.</span></span> <span data-ttu-id="59228-204">Wykonaj hello poniżej czynności tooadd hello użytkownika w Pantheon.</span><span class="sxs-lookup"><span data-stu-id="59228-204">Please follow hello below steps tooadd hello user in Pantheon.</span></span> 

>[!NOTE] 
><span data-ttu-id="59228-205">Dla logowania jednokrotnego toowork użytkownik musi utworzyć pierwszy w Pantheon toobe.</span><span class="sxs-lookup"><span data-stu-id="59228-205">For SSO toowork user needs toobe created first in Pantheon.</span></span>

1. <span data-ttu-id="59228-206">TooPantheon logowania przy użyciu poświadczeń administratora.</span><span class="sxs-lookup"><span data-stu-id="59228-206">Login tooPantheon with admin credentials.</span></span>

2. <span data-ttu-id="59228-207">Przejdź za**organizacji** strony pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="59228-207">Navigate too**Organization** dashboard page.</span></span>
 
3. <span data-ttu-id="59228-208">Kliknij przycisk **osób**.</span><span class="sxs-lookup"><span data-stu-id="59228-208">Click **People**.</span></span>

4. <span data-ttu-id="59228-209">Kliknij przycisk **Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="59228-209">Click **Add user**.</span></span>

5. <span data-ttu-id="59228-210">Wprowadź adres e-mail użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="59228-210">Enter hello user's email address.</span></span>

6. <span data-ttu-id="59228-211">Wybierz rolę użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="59228-211">Choose hello user's role.</span></span>

7. <span data-ttu-id="59228-212">Kliknij przycisk **Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="59228-212">Click **Add user**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="59228-213">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="59228-213">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="59228-214">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooPantheon.</span><span class="sxs-lookup"><span data-stu-id="59228-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPantheon.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="59228-216">**tooassign tooPantheon Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="59228-216">**tooassign Britta Simon tooPantheon, perform hello following steps:**</span></span>

1. <span data-ttu-id="59228-217">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="59228-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="59228-219">Z listy aplikacji hello wybierz **Pantheon**.</span><span class="sxs-lookup"><span data-stu-id="59228-219">In hello applications list, select **Pantheon**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_app.png) 

3. <span data-ttu-id="59228-221">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="59228-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="59228-223">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="59228-223">Click **Add** button.</span></span> <span data-ttu-id="59228-224">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="59228-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="59228-226">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="59228-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="59228-227">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="59228-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="59228-228">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="59228-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="59228-229">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="59228-229">Testing single sign-on</span></span>

<span data-ttu-id="59228-230">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="59228-230">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="59228-231">Po kliknięciu kafelka Pantheon hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Pantheon aplikacji.</span><span class="sxs-lookup"><span data-stu-id="59228-231">When you click hello Pantheon tile in hello Access Panel, you should get automatically signed-on tooyour Pantheon application.</span></span>
<span data-ttu-id="59228-232">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="59228-232">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="59228-233">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="59228-233">Additional resources</span></span>

* [<span data-ttu-id="59228-234">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="59228-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="59228-235">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="59228-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_203.png

