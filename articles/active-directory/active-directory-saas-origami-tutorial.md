---
title: 'Samouczek: Integracji Azure Active Directory z Origami | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Origami."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a28bb0ba-b564-46ba-accc-e587699295d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: a45f2d2b8d2271cf0fc58cb8fad92f007cb5e691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-origami"></a><span data-ttu-id="d15b7-103">Samouczek: Integracji Azure Active Directory z Origami</span><span class="sxs-lookup"><span data-stu-id="d15b7-103">Tutorial: Azure Active Directory integration with Origami</span></span>

<span data-ttu-id="d15b7-104">Z tego samouczka, dowiesz się, jak toointegrate Origami w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d15b7-104">In this tutorial, you learn how toointegrate Origami with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d15b7-105">Integracja z usługą Azure AD Origami zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="d15b7-105">Integrating Origami with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d15b7-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooOrigami</span><span class="sxs-lookup"><span data-stu-id="d15b7-106">You can control in Azure AD who has access tooOrigami</span></span>
- <span data-ttu-id="d15b7-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooOrigami (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d15b7-107">You can enable your users tooautomatically get signed-on tooOrigami (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d15b7-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="d15b7-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d15b7-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d15b7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d15b7-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d15b7-110">Prerequisites</span></span>

<span data-ttu-id="d15b7-111">tooconfigure integracji z usługą Azure AD z Origami należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="d15b7-111">tooconfigure Azure AD integration with Origami, you need hello following items:</span></span>

- <span data-ttu-id="d15b7-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d15b7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d15b7-113">Origami logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="d15b7-113">An Origami single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d15b7-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="d15b7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d15b7-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="d15b7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d15b7-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="d15b7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d15b7-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d15b7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d15b7-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="d15b7-118">Scenario description</span></span>
<span data-ttu-id="d15b7-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="d15b7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d15b7-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="d15b7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d15b7-121">Dodawanie Origami z galerii hello</span><span class="sxs-lookup"><span data-stu-id="d15b7-121">Adding Origami from hello gallery</span></span>
2. <span data-ttu-id="d15b7-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="d15b7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-origami-from-hello-gallery"></a><span data-ttu-id="d15b7-123">Dodawanie Origami z galerii hello</span><span class="sxs-lookup"><span data-stu-id="d15b7-123">Adding Origami from hello gallery</span></span>
<span data-ttu-id="d15b7-124">tooconfigure hello integracji Origami do usługi Azure AD, należy tooadd Origami z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="d15b7-124">tooconfigure hello integration of Origami into Azure AD, you need tooadd Origami from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d15b7-125">**tooadd Origami z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="d15b7-125">**tooadd Origami from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d15b7-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="d15b7-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="d15b7-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="d15b7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d15b7-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="d15b7-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="d15b7-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d15b7-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="d15b7-133">W polu wyszukiwania hello wpisz **Origami**.</span><span class="sxs-lookup"><span data-stu-id="d15b7-133">In hello search box, type **Origami**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-origami-tutorial/tutorial_origami_search.png)

5. <span data-ttu-id="d15b7-135">W panelu wyników hello zaznacz **Origami**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="d15b7-135">In hello results panel, select **Origami**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-origami-tutorial/tutorial_origami_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d15b7-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="d15b7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d15b7-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Origami w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="d15b7-138">In this section, you configure and test Azure AD single sign-on with Origami based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d15b7-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Origami jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d15b7-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Origami is tooa user in Azure AD.</span></span> <span data-ttu-id="d15b7-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Origami musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="d15b7-140">In other words, a link relationship between an Azure AD user and hello related user in Origami needs toobe established.</span></span>

<span data-ttu-id="d15b7-141">W Origami, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="d15b7-141">In Origami, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d15b7-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Origami, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="d15b7-142">tooconfigure and test Azure AD single sign-on with Origami, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d15b7-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="d15b7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d15b7-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="d15b7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d15b7-145">**[Tworzenie użytkownika testowego Origami](#creating-an-origami-test-user)**  -toohave odpowiednikiem Simona Britta w Origami, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d15b7-145">**[Creating an Origami test user](#creating-an-origami-test-user)** - toohave a counterpart of Britta Simon in Origami that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d15b7-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d15b7-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d15b7-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="d15b7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d15b7-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d15b7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d15b7-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Origami.</span><span class="sxs-lookup"><span data-stu-id="d15b7-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Origami application.</span></span>

<span data-ttu-id="d15b7-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Origami, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="d15b7-150">**tooconfigure Azure AD single sign-on with Origami, perform hello following steps:**</span></span>

1. <span data-ttu-id="d15b7-151">W portalu Azure na powitania hello **Origami** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="d15b7-151">In hello Azure portal, on hello **Origami** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="d15b7-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d15b7-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-origami-tutorial/tutorial_origami_samlbase.png)

3. <span data-ttu-id="d15b7-155">Na powitania **Origami domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="d15b7-155">On hello **Origami Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-origami-tutorial/tutorial_origami_url.png)

    <span data-ttu-id="d15b7-157">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://live.origamirisk.com/origami/account/login?account=<companyname>`</span><span class="sxs-lookup"><span data-stu-id="d15b7-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://live.origamirisk.com/origami/account/login?account=<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d15b7-158">wartość Hello nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="d15b7-158">hello value is not real.</span></span> <span data-ttu-id="d15b7-159">Wartość hello aktualizacji z hello rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="d15b7-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="d15b7-160">Skontaktuj się z [zespołem pomocy technicznej klienta Origami](https://wordpress.org/support/theme/origami) tooget hello wartość.</span><span class="sxs-lookup"><span data-stu-id="d15b7-160">Contact [Origami Client support team](https://wordpress.org/support/theme/origami) tooget hello value.</span></span> 
 
4. <span data-ttu-id="d15b7-161">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="d15b7-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-origami-tutorial/tutorial_origami_certificate.png) 

5. <span data-ttu-id="d15b7-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d15b7-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-origami-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d15b7-165">Na powitania **konfiguracji Origami** kliknij **skonfigurować Origami** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="d15b7-165">On hello **Origami Configuration** section, click **Configure Origami** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="d15b7-166">Witaj kopii **Sign-Out adresu URL i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="d15b7-166">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-origami-tutorial/tutorial_origami_configure.png) 

7. <span data-ttu-id="d15b7-168">Zaloguj się za toohello Origami konta z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="d15b7-168">Log in toohello Origami account with Admin rights.</span></span>

8. <span data-ttu-id="d15b7-169">W menu hello na górze hello, kliknij przycisk **Admin**.</span><span class="sxs-lookup"><span data-stu-id="d15b7-169">In hello menu on hello top, click **Admin**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-origami-tutorial/tutorial_origami_51.png)

9. <span data-ttu-id="d15b7-171">Na stronie okna dialogowego konfiguracji na znak pojedynczego hello wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="d15b7-171">On hello Single Sign On Setup dialog page, perform hello following steps:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-origami-tutorial/tutorial_origami_531.png)

    <span data-ttu-id="d15b7-173">a.</span><span class="sxs-lookup"><span data-stu-id="d15b7-173">a.</span></span> <span data-ttu-id="d15b7-174">Wybierz **włączenia funkcji logowania jednokrotnego w**.</span><span class="sxs-lookup"><span data-stu-id="d15b7-174">Select **Enable Single Sign On**.</span></span>

    <span data-ttu-id="d15b7-175">b.</span><span class="sxs-lookup"><span data-stu-id="d15b7-175">b.</span></span> <span data-ttu-id="d15b7-176">W hello **dostawcy tożsamości logowania URL strony** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d15b7-176">In hello **Identity Provider's Sign-in Page URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="d15b7-177">c.</span><span class="sxs-lookup"><span data-stu-id="d15b7-177">c.</span></span> <span data-ttu-id="d15b7-178">W hello **adres URL strony Sign-out dostawcy tożsamości** pole tekstowe, Wklej wartość hello **Sign-Out URL**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d15b7-178">In hello **Identity Provider's Sign-out Page URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="d15b7-179">d.</span><span class="sxs-lookup"><span data-stu-id="d15b7-179">d.</span></span> <span data-ttu-id="d15b7-180">Kliknij przycisk **Przeglądaj** tooupload hello certyfikatu został pobrany z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d15b7-180">Click **Browse** tooupload hello certificate you have downloaded from hello Azure portal.</span></span>

    <span data-ttu-id="d15b7-181">e.</span><span class="sxs-lookup"><span data-stu-id="d15b7-181">e.</span></span> <span data-ttu-id="d15b7-182">Kliknij przycisk **zapisać zmiany**.</span><span class="sxs-lookup"><span data-stu-id="d15b7-182">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="d15b7-183">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="d15b7-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d15b7-184">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="d15b7-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d15b7-185">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d15b7-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d15b7-186">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d15b7-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="d15b7-187">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="d15b7-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="d15b7-189">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="d15b7-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d15b7-190">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="d15b7-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-origami-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d15b7-192">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="d15b7-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-origami-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d15b7-194">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d15b7-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-origami-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d15b7-196">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="d15b7-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-origami-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d15b7-198">a.</span><span class="sxs-lookup"><span data-stu-id="d15b7-198">a.</span></span> <span data-ttu-id="d15b7-199">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d15b7-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d15b7-200">b.</span><span class="sxs-lookup"><span data-stu-id="d15b7-200">b.</span></span> <span data-ttu-id="d15b7-201">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d15b7-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d15b7-202">c.</span><span class="sxs-lookup"><span data-stu-id="d15b7-202">c.</span></span> <span data-ttu-id="d15b7-203">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="d15b7-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d15b7-204">d.</span><span class="sxs-lookup"><span data-stu-id="d15b7-204">d.</span></span> <span data-ttu-id="d15b7-205">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d15b7-205">Click **Create**.</span></span>
 
### <a name="creating-an-origami-test-user"></a><span data-ttu-id="d15b7-206">Tworzenie użytkownika testowego Origami</span><span class="sxs-lookup"><span data-stu-id="d15b7-206">Creating an Origami test user</span></span>

<span data-ttu-id="d15b7-207">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Origami.</span><span class="sxs-lookup"><span data-stu-id="d15b7-207">In this section, you create a user called Britta Simon in Origami.</span></span> 

1. <span data-ttu-id="d15b7-208">Zaloguj się za toohello Origami konta z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="d15b7-208">Log in toohello Origami account with Admin rights.</span></span>

2. <span data-ttu-id="d15b7-209">W menu hello na górze hello, kliknij przycisk **Admin**.</span><span class="sxs-lookup"><span data-stu-id="d15b7-209">In hello menu on hello top, click **Admin**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-origami-tutorial/tutorial_origami_51.png)

3. <span data-ttu-id="d15b7-211">Na powitania **użytkowników i zabezpieczeń** okna dialogowego, kliknij przycisk **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="d15b7-211">On hello **Users and Security** dialog, click **Users**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-origami-tutorial/tutorial_origami_54.png)

4. <span data-ttu-id="d15b7-213">Kliknij przycisk **Dodaj nowego użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="d15b7-213">Click **Add New User**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-origami-tutorial/tutorial_origami_55.png)

5. <span data-ttu-id="d15b7-215">W oknie dialogowym Dodawanie nowego użytkownika hello wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="d15b7-215">On hello Add New User dialog, perform hello following steps:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-origami-tutorial/tutorial_origami_56.png)

    <span data-ttu-id="d15b7-217">a.</span><span class="sxs-lookup"><span data-stu-id="d15b7-217">a.</span></span> <span data-ttu-id="d15b7-218">W hello **nazwy użytkownika** pole tekstowe, wprowadź adres e-mail użytkownika, takie jak hello  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="d15b7-218">In hello **User Name** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="d15b7-219">b.</span><span class="sxs-lookup"><span data-stu-id="d15b7-219">b.</span></span> <span data-ttu-id="d15b7-220">W hello **hasło** tekstowym, wpisz hasło.</span><span class="sxs-lookup"><span data-stu-id="d15b7-220">In hello **Password** textbox, type a password.</span></span>

    <span data-ttu-id="d15b7-221">c.</span><span class="sxs-lookup"><span data-stu-id="d15b7-221">c.</span></span> <span data-ttu-id="d15b7-222">W hello **Potwierdź hasło** tekstowym, wpisz ponownie hasło hello.</span><span class="sxs-lookup"><span data-stu-id="d15b7-222">In hello **Confirm Password** textbox, type hello password again.</span></span>

    <span data-ttu-id="d15b7-223">d.</span><span class="sxs-lookup"><span data-stu-id="d15b7-223">d.</span></span> <span data-ttu-id="d15b7-224">W hello **imię** pole tekstowe, wprowadź hello imię użytkownika, takich jak **Britta**.</span><span class="sxs-lookup"><span data-stu-id="d15b7-224">In hello **First Name** textbox, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="d15b7-225">e.</span><span class="sxs-lookup"><span data-stu-id="d15b7-225">e.</span></span> <span data-ttu-id="d15b7-226">W hello **nazwisko** pole tekstowe, wprowadź hello nazwisko użytkownika, takich jak **Simona**.</span><span class="sxs-lookup"><span data-stu-id="d15b7-226">In hello **Last Name** textbox, enter hello last name of user like **Simon**.</span></span>

    <span data-ttu-id="d15b7-227">f.</span><span class="sxs-lookup"><span data-stu-id="d15b7-227">f.</span></span> <span data-ttu-id="d15b7-228">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="d15b7-228">Click **Save**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-origami-tutorial/tutorial_origami_57.png)

6. <span data-ttu-id="d15b7-230">Przypisz **ról użytkownika** i **dostępu klienta** toohello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d15b7-230">Assign **User Roles** and **Client Access** toohello user.</span></span> 
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-origami-tutorial/tutorial_origami_58.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d15b7-232">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d15b7-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d15b7-233">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooOrigami.</span><span class="sxs-lookup"><span data-stu-id="d15b7-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOrigami.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="d15b7-235">**tooassign tooOrigami Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="d15b7-235">**tooassign Britta Simon tooOrigami, perform hello following steps:**</span></span>

1. <span data-ttu-id="d15b7-236">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="d15b7-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="d15b7-238">Z listy aplikacji hello wybierz **Origami**.</span><span class="sxs-lookup"><span data-stu-id="d15b7-238">In hello applications list, select **Origami**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-origami-tutorial/tutorial_origami_app.png) 

3. <span data-ttu-id="d15b7-240">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="d15b7-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="d15b7-242">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d15b7-242">Click **Add** button.</span></span> <span data-ttu-id="d15b7-243">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d15b7-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="d15b7-245">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="d15b7-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d15b7-246">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d15b7-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d15b7-247">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d15b7-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d15b7-248">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d15b7-248">Testing single sign-on</span></span>

<span data-ttu-id="d15b7-249">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="d15b7-249">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d15b7-250">Po kliknięciu kafelka Origami hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Origami aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d15b7-250">When you click hello Origami tile in hello Access Panel, you should get automatically signed-on tooyour Origami application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d15b7-251">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="d15b7-251">Additional resources</span></span>

* [<span data-ttu-id="d15b7-252">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d15b7-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d15b7-253">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d15b7-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-origami-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-origami-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-origami-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-origami-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-origami-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-origami-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-origami-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-origami-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-origami-tutorial/tutorial_general_203.png

