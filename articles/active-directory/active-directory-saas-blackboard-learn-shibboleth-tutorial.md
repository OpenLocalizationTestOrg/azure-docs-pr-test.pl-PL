---
title: "Samouczek: Integracji Azure Active Directory z tablica Dowiedz się - Shibboleth | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między nauki tablica - Shibboleth i Azure Active Directory."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e435cbb4-c0f0-400e-943c-5c923fa8ddf2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jeedes
ms.openlocfilehash: 40aa3ec5f42b93157af3c56daaadfa66203b21d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-blackboard-learn---shibboleth"></a><span data-ttu-id="44fcd-103">Samouczek: Integracji Azure Active Directory z tablica Dowiedz się - Shibboleth</span><span class="sxs-lookup"><span data-stu-id="44fcd-103">Tutorial: Azure Active Directory integration with Blackboard Learn - Shibboleth</span></span>

<span data-ttu-id="44fcd-104">Z tego samouczka, dowiesz się, jak tablica informacji - toointegrate Shibboleth w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="44fcd-104">In this tutorial, you learn how toointegrate Blackboard Learn - Shibboleth with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="44fcd-105">Integrowanie informacje tablica - Shibboleth z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="44fcd-105">Integrating Blackboard Learn - Shibboleth with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="44fcd-106">Można kontrolować w usłudze Azure AD, kto ma dostęp tooBlackboard informacje - Shibboleth</span><span class="sxs-lookup"><span data-stu-id="44fcd-106">You can control in Azure AD who has access tooBlackboard Learn - Shibboleth</span></span>
- <span data-ttu-id="44fcd-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooBlackboard informacje - Shibboleth (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="44fcd-107">You can enable your users tooautomatically get signed-on tooBlackboard Learn - Shibboleth (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="44fcd-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="44fcd-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="44fcd-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="44fcd-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44fcd-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="44fcd-110">Prerequisites</span></span>

<span data-ttu-id="44fcd-111">tooconfigure integracji usługi Azure AD z tablica Dowiedz się - Shibboleth, należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="44fcd-111">tooconfigure Azure AD integration with Blackboard Learn - Shibboleth, you need hello following items:</span></span>

- <span data-ttu-id="44fcd-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="44fcd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="44fcd-113">Tablica Dowiedz się - Shibboleth jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="44fcd-113">A Blackboard Learn - Shibboleth single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="44fcd-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="44fcd-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="44fcd-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="44fcd-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="44fcd-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="44fcd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="44fcd-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="44fcd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="44fcd-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="44fcd-118">Scenario description</span></span>
<span data-ttu-id="44fcd-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="44fcd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="44fcd-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="44fcd-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="44fcd-121">Dodawanie informacje tablica - Shibboleth z galerii hello</span><span class="sxs-lookup"><span data-stu-id="44fcd-121">Adding Blackboard Learn - Shibboleth from hello gallery</span></span>
2. <span data-ttu-id="44fcd-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="44fcd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-blackboard-learn---shibboleth-from-hello-gallery"></a><span data-ttu-id="44fcd-123">Dodawanie informacje tablica - Shibboleth z galerii hello</span><span class="sxs-lookup"><span data-stu-id="44fcd-123">Adding Blackboard Learn - Shibboleth from hello gallery</span></span>
<span data-ttu-id="44fcd-124">tooconfigure hello integracji tablica Dowiedz się - Shibboleth do usługi Azure AD, należy dowiedzieć się tablica - tooadd Shibboleth z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="44fcd-124">tooconfigure hello integration of Blackboard Learn - Shibboleth into Azure AD, you need tooadd Blackboard Learn - Shibboleth from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="44fcd-125">**Dowiedz się tablica - tooadd Shibboleth z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="44fcd-125">**tooadd Blackboard Learn - Shibboleth from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="44fcd-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="44fcd-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="44fcd-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="44fcd-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="44fcd-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="44fcd-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="44fcd-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="44fcd-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="44fcd-133">W polu wyszukiwania hello wpisz **tablica Dowiedz się - Shibboleth**.</span><span class="sxs-lookup"><span data-stu-id="44fcd-133">In hello search box, type **Blackboard Learn - Shibboleth**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_search.png)

5. <span data-ttu-id="44fcd-135">W panelu wyników hello, wybierz **tablica Dowiedz się - Shibboleth**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="44fcd-135">In hello results panel, select **Blackboard Learn - Shibboleth**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="44fcd-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="44fcd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="44fcd-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z tablica Dowiedz się więcej — Shibboleth oparte na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="44fcd-138">In this section, you configure and test Azure AD single sign-on with Blackboard Learn - Shibboleth based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="44fcd-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD wymaga tooknow użytkownika odpowiednikiem hello w tablica Dowiedz się więcej — Shibboleth jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="44fcd-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Blackboard Learn - Shibboleth is tooa user in Azure AD.</span></span> <span data-ttu-id="44fcd-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Dowiedz się tablica - Shibboleth musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="44fcd-140">In other words, a link relationship between an Azure AD user and hello related user in Blackboard Learn - Shibboleth needs toobe established.</span></span>

<span data-ttu-id="44fcd-141">Dowiedz się więcej tablica - Shibboleth, przypisywanie wartości hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="44fcd-141">In Blackboard Learn - Shibboleth, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="44fcd-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z tablica Dowiedz się - Shibboleth, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="44fcd-142">tooconfigure and test Azure AD single sign-on with Blackboard Learn - Shibboleth, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="44fcd-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="44fcd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="44fcd-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="44fcd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="44fcd-145">**[Tworzenie tablica informacji - użytkownika testowego Shibboleth](#creating-a-blackboard-learn---shibboleth-test-user)**  - toohave odpowiednikiem Simona Britta w Dowiedz się, tablica - Shibboleth, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="44fcd-145">**[Creating a Blackboard Learn - Shibboleth test user](#creating-a-blackboard-learn---shibboleth-test-user)** - toohave a counterpart of Britta Simon in Blackboard Learn - Shibboleth that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="44fcd-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="44fcd-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="44fcd-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="44fcd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="44fcd-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="44fcd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="44fcd-149">W tej sekcji włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w sieci tablica informacje - Shibboleth aplikacji.</span><span class="sxs-lookup"><span data-stu-id="44fcd-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Blackboard Learn - Shibboleth application.</span></span>

<span data-ttu-id="44fcd-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z tablica Dowiedz się - Shibboleth, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="44fcd-150">**tooconfigure Azure AD single sign-on with Blackboard Learn - Shibboleth, perform hello following steps:**</span></span>

1. <span data-ttu-id="44fcd-151">W portalu Azure na powitania hello **tablica Dowiedz się - Shibboleth** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="44fcd-151">In hello Azure portal, on hello **Blackboard Learn - Shibboleth** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="44fcd-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="44fcd-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_samlbase.png)

3. <span data-ttu-id="44fcd-155">Na powitania **tablica Poznaj - Shibboleth domeny i adresy URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="44fcd-155">On hello **Blackboard Learn - Shibboleth Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_url.png)

    <span data-ttu-id="44fcd-157">a.</span><span class="sxs-lookup"><span data-stu-id="44fcd-157">a.</span></span> <span data-ttu-id="44fcd-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/Login`</span><span class="sxs-lookup"><span data-stu-id="44fcd-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/Login`</span></span>

    <span data-ttu-id="44fcd-159">b.</span><span class="sxs-lookup"><span data-stu-id="44fcd-159">b.</span></span> <span data-ttu-id="44fcd-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<yourblackoardlearnserver>.blackboardlearn.com/shibboleth-sp`</span><span class="sxs-lookup"><span data-stu-id="44fcd-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<yourblackoardlearnserver>.blackboardlearn.com/shibboleth-sp`</span></span>

    <span data-ttu-id="44fcd-161">c.</span><span class="sxs-lookup"><span data-stu-id="44fcd-161">c.</span></span> <span data-ttu-id="44fcd-162">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/SAML2/POST`</span><span class="sxs-lookup"><span data-stu-id="44fcd-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/SAML2/POST`</span></span>
 
    > [!NOTE] 
    > <span data-ttu-id="44fcd-163">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="44fcd-163">These values are not real.</span></span> <span data-ttu-id="44fcd-164">Zaktualizować te wartości z hello rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="44fcd-164">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="44fcd-165">Skontaktuj się z [tablica Dowiedz się - zespołem pomocy technicznej klienta Shibboleth](https://www.blackboard.com/forms/contact-us_form.aspx) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="44fcd-165">Contact [Blackboard Learn - Shibboleth Client support team](https://www.blackboard.com/forms/contact-us_form.aspx) tooget these values.</span></span> 

4. <span data-ttu-id="44fcd-166">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="44fcd-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_certificate.png) 

5. <span data-ttu-id="44fcd-168">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="44fcd-168">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="44fcd-170">Na powitania **tablica Dowiedz się - Shibboleth konfiguracji** , kliknij przycisk **skonfigurować tablica informacji - Shibboleth** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="44fcd-170">On hello **Blackboard Learn - Shibboleth Configuration** section, click **Configure Blackboard Learn - Shibboleth** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="44fcd-171">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="44fcd-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_configure.png) 

7. <span data-ttu-id="44fcd-173">tooconfigure rejestracji jednokrotnej w **tablica Dowiedz się - Shibboleth** strony, należy pobrać hello toosend **XML metadanych** i **Sign-Out adres URL, identyfikator jednostki SAML i SAML logowania jednokrotnego usługi pojedynczej Adres URL** za[tablica Dowiedz się - zespołem pomocy technicznej Shibboleth](https://www.blackboard.com/forms/contact-us_form.aspx).</span><span class="sxs-lookup"><span data-stu-id="44fcd-173">tooconfigure single sign-on on **Blackboard Learn - Shibboleth** side, you need toosend hello downloaded **Metadata XML** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Blackboard Learn - Shibboleth support team](https://www.blackboard.com/forms/contact-us_form.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="44fcd-174">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="44fcd-174">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="44fcd-175">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="44fcd-175">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="44fcd-176">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="44fcd-176">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="44fcd-177">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="44fcd-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="44fcd-178">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="44fcd-178">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="44fcd-180">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="44fcd-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="44fcd-181">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="44fcd-181">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="44fcd-183">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="44fcd-183">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="44fcd-185">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="44fcd-185">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="44fcd-187">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="44fcd-187">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="44fcd-189">a.</span><span class="sxs-lookup"><span data-stu-id="44fcd-189">a.</span></span> <span data-ttu-id="44fcd-190">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="44fcd-190">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="44fcd-191">b.</span><span class="sxs-lookup"><span data-stu-id="44fcd-191">b.</span></span> <span data-ttu-id="44fcd-192">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="44fcd-192">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="44fcd-193">c.</span><span class="sxs-lookup"><span data-stu-id="44fcd-193">c.</span></span> <span data-ttu-id="44fcd-194">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="44fcd-194">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="44fcd-195">d.</span><span class="sxs-lookup"><span data-stu-id="44fcd-195">d.</span></span> <span data-ttu-id="44fcd-196">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="44fcd-196">Click **Create**.</span></span>
 
### <a name="creating-a-blackboard-learn---shibboleth-test-user"></a><span data-ttu-id="44fcd-197">Tworzenie tablica informacji - Shibboleth użytkownika testowego</span><span class="sxs-lookup"><span data-stu-id="44fcd-197">Creating a Blackboard Learn - Shibboleth test user</span></span>

<span data-ttu-id="44fcd-198">W tej sekcji można utworzyć użytkownika o nazwie Simona Britta w tablica Dowiedz się - Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="44fcd-198">In this section, you create a user called Britta Simon in Blackboard Learn - Shibboleth.</span></span> <span data-ttu-id="44fcd-199">Praca z Twojej [tablica Dowiedz się - Shibboleth zespołem pomocy technicznej](https://www.blackboard.com/forms/contact-us_form.aspx) tooadd hello użytkowników w hello tablica Dowiedz się - Shibboleth platformy.</span><span class="sxs-lookup"><span data-stu-id="44fcd-199">Work with your [Blackboard Learn - Shibboleth support team](https://www.blackboard.com/forms/contact-us_form.aspx) tooadd hello users in hello Blackboard Learn - Shibboleth platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="44fcd-200">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="44fcd-200">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="44fcd-201">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooBlackboard informacje - Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="44fcd-201">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBlackboard Learn - Shibboleth.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="44fcd-203">**tooassign Simona Britta tooBlackboard informacje - Shibboleth, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="44fcd-203">**tooassign Britta Simon tooBlackboard Learn - Shibboleth, perform hello following steps:**</span></span>

1. <span data-ttu-id="44fcd-204">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="44fcd-204">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="44fcd-206">Z listy aplikacji hello wybierz **tablica Dowiedz się - Shibboleth**.</span><span class="sxs-lookup"><span data-stu-id="44fcd-206">In hello applications list, select **Blackboard Learn - Shibboleth**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_app.png) 

3. <span data-ttu-id="44fcd-208">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="44fcd-208">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="44fcd-210">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="44fcd-210">Click **Add** button.</span></span> <span data-ttu-id="44fcd-211">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="44fcd-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="44fcd-213">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="44fcd-213">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="44fcd-214">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="44fcd-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="44fcd-215">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="44fcd-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="44fcd-216">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="44fcd-216">Testing single sign-on</span></span>

<span data-ttu-id="44fcd-217">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="44fcd-217">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="44fcd-218">Po kliknięciu hello tablica Dowiedz się - Shibboleth kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Dowiedz się tablica - Shibboleth aplikacji.</span><span class="sxs-lookup"><span data-stu-id="44fcd-218">When you click hello Blackboard Learn - Shibboleth tile in hello Access Panel, you should get automatically signed-on tooyour Blackboard Learn - Shibboleth application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="44fcd-219">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="44fcd-219">Additional resources</span></span>

* [<span data-ttu-id="44fcd-220">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="44fcd-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="44fcd-221">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="44fcd-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_203.png

