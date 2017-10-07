---
title: "Samouczek: Integrację usługi Azure Active Directory ze Mozy | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Mozy Enterprise."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 489b5e62-85c2-45c9-8766-326632d48114
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: jeedes
ms.openlocfilehash: bab0df4f3621b784cd8edfda3c8e10fe5a7ced9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mozy-enterprise"></a><span data-ttu-id="de8fb-103">Samouczek: Integrację usługi Azure Active Directory ze Mozy</span><span class="sxs-lookup"><span data-stu-id="de8fb-103">Tutorial: Azure Active Directory integration with Mozy Enterprise</span></span>

<span data-ttu-id="de8fb-104">Z tego samouczka, dowiesz się, jak toointegrate Mozy przedsiębiorstwa w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="de8fb-104">In this tutorial, you learn how toointegrate Mozy Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="de8fb-105">Integrowanie Mozy organizacji z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="de8fb-105">Integrating Mozy Enterprise with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="de8fb-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooMozy przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="de8fb-106">You can control in Azure AD who has access tooMozy Enterprise</span></span>
- <span data-ttu-id="de8fb-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooMozy przedsiębiorstwa (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="de8fb-107">You can enable your users tooautomatically get signed-on tooMozy Enterprise (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="de8fb-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="de8fb-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="de8fb-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="de8fb-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="de8fb-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="de8fb-110">Prerequisites</span></span>

<span data-ttu-id="de8fb-111">tooconfigure integracji usługi Azure AD z Mozy Enterprise należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="de8fb-111">tooconfigure Azure AD integration with Mozy Enterprise, you need hello following items:</span></span>

- <span data-ttu-id="de8fb-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="de8fb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="de8fb-113">Mozy Enterprise logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="de8fb-113">A Mozy Enterprise single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="de8fb-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="de8fb-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="de8fb-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="de8fb-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="de8fb-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="de8fb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="de8fb-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="de8fb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="de8fb-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="de8fb-118">Scenario description</span></span>
<span data-ttu-id="de8fb-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="de8fb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="de8fb-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="de8fb-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="de8fb-121">Dodawanie Mozy przedsiębiorstwa z galerii hello</span><span class="sxs-lookup"><span data-stu-id="de8fb-121">Adding Mozy Enterprise from hello gallery</span></span>
2. <span data-ttu-id="de8fb-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="de8fb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mozy-enterprise-from-hello-gallery"></a><span data-ttu-id="de8fb-123">Dodawanie Mozy przedsiębiorstwa z galerii hello</span><span class="sxs-lookup"><span data-stu-id="de8fb-123">Adding Mozy Enterprise from hello gallery</span></span>
<span data-ttu-id="de8fb-124">tooconfigure hello integracji Mozy przedsiębiorstwa w usłudze Azure Active Directory, należy tooadd Mozy przedsiębiorstwa z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="de8fb-124">tooconfigure hello integration of Mozy Enterprise into Azure AD, you need tooadd Mozy Enterprise from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="de8fb-125">**tooadd Mozy przedsiębiorstwa z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="de8fb-125">**tooadd Mozy Enterprise from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="de8fb-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="de8fb-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="de8fb-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="de8fb-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="de8fb-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="de8fb-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="de8fb-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="de8fb-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="de8fb-133">W polu wyszukiwania hello wpisz **Mozy Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="de8fb-133">In hello search box, type **Mozy Enterprise**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_search.png)

5. <span data-ttu-id="de8fb-135">W panelu wyników hello, wybierz **Mozy Enterprise**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="de8fb-135">In hello results panel, select **Mozy Enterprise**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="de8fb-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="de8fb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="de8fb-138">W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z Mozy przedsiębiorstwa w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="de8fb-138">In this section, you configure and test Azure AD single sign-on with Mozy Enterprise based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="de8fb-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w przedsiębiorstwie Mozy jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="de8fb-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Mozy Enterprise is tooa user in Azure AD.</span></span> <span data-ttu-id="de8fb-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w przedsiębiorstwie Mozy musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="de8fb-140">In other words, a link relationship between an Azure AD user and hello related user in Mozy Enterprise needs toobe established.</span></span>

<span data-ttu-id="de8fb-141">W przedsiębiorstwie Mozy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="de8fb-141">In Mozy Enterprise, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="de8fb-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Mozy przedsiębiorstwa, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="de8fb-142">tooconfigure and test Azure AD single sign-on with Mozy Enterprise, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="de8fb-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="de8fb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="de8fb-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="de8fb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="de8fb-145">**[Tworzenie użytkownika testowego Mozy Enterprise](#creating-a-mozy-enterprise-test-user)**  -toohave odpowiednikiem Simona Britta w przedsiębiorstwie Mozy, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="de8fb-145">**[Creating a Mozy Enterprise test user](#creating-a-mozy-enterprise-test-user)** - toohave a counterpart of Britta Simon in Mozy Enterprise that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="de8fb-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="de8fb-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="de8fb-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="de8fb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="de8fb-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="de8fb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="de8fb-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować rejestracji jednokrotnej w aplikacji Mozy przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="de8fb-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Mozy Enterprise application.</span></span>

<span data-ttu-id="de8fb-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Mozy przedsiębiorstwa, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="de8fb-150">**tooconfigure Azure AD single sign-on with Mozy Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="de8fb-151">W portalu Azure na powitania hello **Mozy Enterprise** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="de8fb-151">In hello Azure portal, on hello **Mozy Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="de8fb-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="de8fb-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_samlbase.png)

3. <span data-ttu-id="de8fb-155">Na powitania **Mozy domeny przedsiębiorstwa i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="de8fb-155">On hello **Mozy Enterprise Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_url.png)

    <span data-ttu-id="de8fb-157">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<tenantname>.Mozyenterprise.com`</span><span class="sxs-lookup"><span data-stu-id="de8fb-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.Mozyenterprise.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="de8fb-158">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="de8fb-158">This value is not real.</span></span> <span data-ttu-id="de8fb-159">Zaktualizuj tę wartość z hello rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="de8fb-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="de8fb-160">Skontaktuj się z [zespołem pomocy technicznej klienta Enterprise Mozy](http://support.mozy.com/) tooget tej wartości.</span><span class="sxs-lookup"><span data-stu-id="de8fb-160">Contact [Mozy Enterprise Client support team](http://support.mozy.com/) tooget this value.</span></span>

4. <span data-ttu-id="de8fb-161">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="de8fb-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_certificate.png) 

5. <span data-ttu-id="de8fb-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="de8fb-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="de8fb-165">Na powitania **konfiguracja dla przedsiębiorstw Mozy** , kliknij przycisk **skonfigurować Mozy Enterprise** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="de8fb-165">On hello **Mozy Enterprise Configuration** section, click **Configure Mozy Enterprise** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="de8fb-166">Kopiuj hello **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="de8fb-166">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_configure.png) 

7. <span data-ttu-id="de8fb-168">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy Mozy Enterprise jako administrator.</span><span class="sxs-lookup"><span data-stu-id="de8fb-168">In a different web browser window, log into your Mozy Enterprise company site as an administrator.</span></span>

8. <span data-ttu-id="de8fb-169">W hello **konfiguracji** kliknij **zasady uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="de8fb-169">In hello **Configuration** section, click **Authentication Policy**.</span></span>
   
   <span data-ttu-id="de8fb-170">![Zasady uwierzytelniania](./media/active-directory-saas-mozy-enterprise-tutorial/ic777314.png "zasady uwierzytelniania")</span><span class="sxs-lookup"><span data-stu-id="de8fb-170">![Authentication policy](./media/active-directory-saas-mozy-enterprise-tutorial/ic777314.png "Authentication policy")</span></span>

9. <span data-ttu-id="de8fb-171">Na powitania **zasady uwierzytelniania** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="de8fb-171">On hello **Authentication Policy** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="de8fb-172">![Zasady uwierzytelniania](./media/active-directory-saas-mozy-enterprise-tutorial/ic777315.png "zasady uwierzytelniania")</span><span class="sxs-lookup"><span data-stu-id="de8fb-172">![Authentication policy](./media/active-directory-saas-mozy-enterprise-tutorial/ic777315.png "Authentication policy")</span></span>
   
   <span data-ttu-id="de8fb-173">a.</span><span class="sxs-lookup"><span data-stu-id="de8fb-173">a.</span></span> <span data-ttu-id="de8fb-174">Wybierz **usługi katalogowej** jako **dostawcy**.</span><span class="sxs-lookup"><span data-stu-id="de8fb-174">Select **Directory Service** as **Provider**.</span></span>
   
   <span data-ttu-id="de8fb-175">b.</span><span class="sxs-lookup"><span data-stu-id="de8fb-175">b.</span></span> <span data-ttu-id="de8fb-176">Wybierz **wypychania LDAP**.</span><span class="sxs-lookup"><span data-stu-id="de8fb-176">Select **Use LDAP Push**.</span></span>
   
   <span data-ttu-id="de8fb-177">c.</span><span class="sxs-lookup"><span data-stu-id="de8fb-177">c.</span></span> <span data-ttu-id="de8fb-178">Kliknij przycisk hello **uwierzytelnianie SAML** kartę.</span><span class="sxs-lookup"><span data-stu-id="de8fb-178">Click hello **SAML Authentication** tab.</span></span>
   
   <span data-ttu-id="de8fb-179">d.</span><span class="sxs-lookup"><span data-stu-id="de8fb-179">d.</span></span> <span data-ttu-id="de8fb-180">Wklej **SAML pojedynczy znak na adres URL usługi**, która została skopiowana z hello portalu Azure do hello **adres URL uwierzytelniania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="de8fb-180">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **Authentication URL** textbox.</span></span>
   
   <span data-ttu-id="de8fb-181">e.</span><span class="sxs-lookup"><span data-stu-id="de8fb-181">e.</span></span> <span data-ttu-id="de8fb-182">Wklej **SAML identyfikator jednostki**, która została skopiowana z hello portalu Azure do hello **punktu końcowego SAML** pole tekstowe.</span><span class="sxs-lookup"><span data-stu-id="de8fb-182">Paste **SAML Entity ID**, which you have copied from hello Azure portal into hello **SAML Endpoint** textbox.</span></span>
   
   <span data-ttu-id="de8fb-183">f.</span><span class="sxs-lookup"><span data-stu-id="de8fb-183">f.</span></span> <span data-ttu-id="de8fb-184">Otwórz pobrany zakodowanego certyfikatu base-64 w Notatniku hello kopiowania zawartości go do Schowka, a następnie wklej hello cały certyfikat do **certyfikatu SAML** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="de8fb-184">Open your downloaded base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste hello entire Certificate into **SAML Certificate** textbox.</span></span>
   
   <span data-ttu-id="de8fb-185">g.</span><span class="sxs-lookup"><span data-stu-id="de8fb-185">g.</span></span> <span data-ttu-id="de8fb-186">Wybierz **włączenia logowania jednokrotnego dla administratorów toolog się przy użyciu swoich poświadczeń sieciowych**.</span><span class="sxs-lookup"><span data-stu-id="de8fb-186">Select **Enable SSO for Admins toolog in with their network credentials**.</span></span>
   
   <span data-ttu-id="de8fb-187">h.</span><span class="sxs-lookup"><span data-stu-id="de8fb-187">h.</span></span> <span data-ttu-id="de8fb-188">Kliknij przycisk **zapisać zmiany**.</span><span class="sxs-lookup"><span data-stu-id="de8fb-188">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="de8fb-189">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="de8fb-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="de8fb-190">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="de8fb-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="de8fb-191">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="de8fb-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="de8fb-192">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="de8fb-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="de8fb-193">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="de8fb-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="de8fb-195">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="de8fb-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="de8fb-196">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="de8fb-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="de8fb-198">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="de8fb-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="de8fb-200">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="de8fb-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="de8fb-202">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="de8fb-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="de8fb-204">a.</span><span class="sxs-lookup"><span data-stu-id="de8fb-204">a.</span></span> <span data-ttu-id="de8fb-205">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="de8fb-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="de8fb-206">b.</span><span class="sxs-lookup"><span data-stu-id="de8fb-206">b.</span></span> <span data-ttu-id="de8fb-207">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="de8fb-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="de8fb-208">c.</span><span class="sxs-lookup"><span data-stu-id="de8fb-208">c.</span></span> <span data-ttu-id="de8fb-209">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="de8fb-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="de8fb-210">d.</span><span class="sxs-lookup"><span data-stu-id="de8fb-210">d.</span></span> <span data-ttu-id="de8fb-211">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="de8fb-211">Click **Create**.</span></span>
 
### <a name="creating-a-mozy-enterprise-test-user"></a><span data-ttu-id="de8fb-212">Tworzenie użytkownika testowego Mozy przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="de8fb-212">Creating a Mozy Enterprise test user</span></span>

<span data-ttu-id="de8fb-213">W kolejności tooenable usługi Azure AD użytkownicy toolog Mozy w przedsiębiorstwie musi być zainicjowana Mozy w przedsiębiorstwie.</span><span class="sxs-lookup"><span data-stu-id="de8fb-213">In order tooenable Azure AD users toolog into Mozy Enterprise, they must be provisioned into Mozy Enterprise.</span></span> <span data-ttu-id="de8fb-214">W przypadku hello Mozy przedsiębiorstwa Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="de8fb-214">In hello case of Mozy Enterprise, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="de8fb-215">Możesz użyć innych Mozy Enterprise użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez tooprovision Mozy Enterprise kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="de8fb-215">You can use any other Mozy Enterprise user account creation tools or APIs provided by Mozy Enterprise tooprovision AAD user accounts.</span></span>

<span data-ttu-id="de8fb-216">**tooprovision kont użytkowników, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="de8fb-216">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="de8fb-217">Zaloguj się za tooyour **Mozy Enterprise** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="de8fb-217">Log in tooyour **Mozy Enterprise** tenant.</span></span>

2. <span data-ttu-id="de8fb-218">Kliknij przycisk **użytkowników**, a następnie kliknij przycisk **Dodaj nowego użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="de8fb-218">Click **Users**, and then click **Add New User**.</span></span>
   
   <span data-ttu-id="de8fb-219">![Użytkownicy](./media/active-directory-saas-mozy-enterprise-tutorial/ic777317.png "użytkowników")</span><span class="sxs-lookup"><span data-stu-id="de8fb-219">![Users](./media/active-directory-saas-mozy-enterprise-tutorial/ic777317.png "Users")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="de8fb-220">Witaj **Dodaj nowego użytkownika** tylko wtedy, gdy tylko jest wyświetlana opcja **Mozy** został wybrany jako dostawca hello w obszarze **zasady uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="de8fb-220">hello **Add New User** option is only displayed only if **Mozy** is selected as hello provider under **Authentication policy**.</span></span> <span data-ttu-id="de8fb-221">Jeśli skonfigurowano uwierzytelnianie SAML, następnie hello użytkownicy są automatycznie dodawane na ich pierwsze logowanie za pomocą rejestracji jednokrotnej w.</span><span class="sxs-lookup"><span data-stu-id="de8fb-221">If SAML Authentication is configured, then hello users are added automatically on their first login through Single sign on.</span></span>
    
3. <span data-ttu-id="de8fb-222">Witaj nowego okna dialogowego użytkowników i wykonywanie hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="de8fb-222">On hello new user dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="de8fb-223">![Dodawanie użytkowników](./media/active-directory-saas-mozy-enterprise-tutorial/ic777318.png "Dodawanie użytkowników")</span><span class="sxs-lookup"><span data-stu-id="de8fb-223">![Add Users](./media/active-directory-saas-mozy-enterprise-tutorial/ic777318.png "Add Users")</span></span>
   
   <span data-ttu-id="de8fb-224">a.</span><span class="sxs-lookup"><span data-stu-id="de8fb-224">a.</span></span> <span data-ttu-id="de8fb-225">Z hello **wybierz grupę** listy, wybierz grupę.</span><span class="sxs-lookup"><span data-stu-id="de8fb-225">From hello **Choose a Group** list, select a group.</span></span>
   
   <span data-ttu-id="de8fb-226">b.</span><span class="sxs-lookup"><span data-stu-id="de8fb-226">b.</span></span> <span data-ttu-id="de8fb-227">Z hello **jakiego rodzaju użytkownika** listy, wybierz typ.</span><span class="sxs-lookup"><span data-stu-id="de8fb-227">From hello **What type of user** list, select a type.</span></span>
   
   <span data-ttu-id="de8fb-228">c.</span><span class="sxs-lookup"><span data-stu-id="de8fb-228">c.</span></span> <span data-ttu-id="de8fb-229">W hello **Username** pole tekstowe, nazwa typu hello użytkownika hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="de8fb-229">In hello **Username** textbox, type hello name of hello Azure AD user.</span></span>
   
   <span data-ttu-id="de8fb-230">d.</span><span class="sxs-lookup"><span data-stu-id="de8fb-230">d.</span></span> <span data-ttu-id="de8fb-231">W hello **E-mail** pole tekstowe, typ hello adres e-mail użytkownika hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="de8fb-231">In hello **Email** textbox, type hello email address of hello Azure AD user.</span></span>
   
   <span data-ttu-id="de8fb-232">e.</span><span class="sxs-lookup"><span data-stu-id="de8fb-232">e.</span></span> <span data-ttu-id="de8fb-233">Wybierz **wysyłania wiadomości e-mail z instrukcją użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="de8fb-233">Select **Send user instruction email**.</span></span>
   
   <span data-ttu-id="de8fb-234">f.</span><span class="sxs-lookup"><span data-stu-id="de8fb-234">f.</span></span> <span data-ttu-id="de8fb-235">Kliknij przycisk **dodać użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="de8fb-235">Click **Add User(s)**.</span></span>

     >[!NOTE]
     > <span data-ttu-id="de8fb-236">Po utworzeniu użytkownika hello, wiadomości e-mail będą wysyłane toohello użytkownika usługi Azure AD, który zawiera konto hello tooconfirm łącza, zanim staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="de8fb-236">After creating hello user, an email will be sent toohello Azure AD user that includes a link tooconfirm hello account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="de8fb-237">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="de8fb-237">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="de8fb-238">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooMozy przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="de8fb-238">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMozy Enterprise.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="de8fb-240">**tooassign Simona Britta tooMozy przedsiębiorstwa, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="de8fb-240">**tooassign Britta Simon tooMozy Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="de8fb-241">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="de8fb-241">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="de8fb-243">Z listy aplikacji hello wybierz **Mozy Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="de8fb-243">In hello applications list, select **Mozy Enterprise**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_app.png) 

3. <span data-ttu-id="de8fb-245">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="de8fb-245">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="de8fb-247">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="de8fb-247">Click **Add** button.</span></span> <span data-ttu-id="de8fb-248">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="de8fb-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="de8fb-250">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="de8fb-250">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="de8fb-251">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="de8fb-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="de8fb-252">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="de8fb-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="de8fb-253">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="de8fb-253">Testing single sign-on</span></span>

<span data-ttu-id="de8fb-254">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="de8fb-254">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="de8fb-255">Po kliknięciu hello Mozy Enterprise kafelka w hello Panel dostępu, należy pobrać strony logowania organizacji Mozy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="de8fb-255">When you click hello Mozy Enterprise tile in hello Access Panel, you should get login page of Mozy Enterprise application.</span></span>
<span data-ttu-id="de8fb-256">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="de8fb-256">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="de8fb-257">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="de8fb-257">Additional resources</span></span>

* [<span data-ttu-id="de8fb-258">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="de8fb-258">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="de8fb-259">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="de8fb-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_203.png

