---
title: 'Samouczek: Integracji Azure Active Directory z Expensify | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Expensify."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1e761484-7a2f-4321-91f4-6d5d0b69344e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: jeedes
ms.openlocfilehash: 141513ef27c90dae2d77a52ecab2f89c4e5a55ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-expensify"></a><span data-ttu-id="6309a-103">Samouczek: Integracji Azure Active Directory z Expensify</span><span class="sxs-lookup"><span data-stu-id="6309a-103">Tutorial: Azure Active Directory integration with Expensify</span></span>

<span data-ttu-id="6309a-104">Z tego samouczka, dowiesz się, jak toointegrate Expensify z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6309a-104">In this tutorial, you learn how toointegrate Expensify with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6309a-105">Integracja z usługą Azure AD Expensify zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="6309a-105">Integrating Expensify with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6309a-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooExpensify</span><span class="sxs-lookup"><span data-stu-id="6309a-106">You can control in Azure AD who has access tooExpensify</span></span>
- <span data-ttu-id="6309a-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooExpensify (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6309a-107">You can enable your users tooautomatically get signed-on tooExpensify (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6309a-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="6309a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6309a-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6309a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6309a-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6309a-110">Prerequisites</span></span>

<span data-ttu-id="6309a-111">tooconfigure integracji z usługą Azure AD z Expensify należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="6309a-111">tooconfigure Azure AD integration with Expensify, you need hello following items:</span></span>

- <span data-ttu-id="6309a-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6309a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6309a-113">Expensify jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="6309a-113">An Expensify single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6309a-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="6309a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6309a-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="6309a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6309a-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="6309a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6309a-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6309a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6309a-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="6309a-118">Scenario description</span></span>
<span data-ttu-id="6309a-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="6309a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6309a-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="6309a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6309a-121">Dodawanie Expensify z galerii hello</span><span class="sxs-lookup"><span data-stu-id="6309a-121">Adding Expensify from hello gallery</span></span>
2. <span data-ttu-id="6309a-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="6309a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-expensify-from-hello-gallery"></a><span data-ttu-id="6309a-123">Dodawanie Expensify z galerii hello</span><span class="sxs-lookup"><span data-stu-id="6309a-123">Adding Expensify from hello gallery</span></span>
<span data-ttu-id="6309a-124">tooconfigure hello integracji Expensify do usługi Azure AD, należy tooadd Expensify z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="6309a-124">tooconfigure hello integration of Expensify into Azure AD, you need tooadd Expensify from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6309a-125">**tooadd Expensify z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="6309a-125">**tooadd Expensify from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6309a-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="6309a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="6309a-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="6309a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6309a-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="6309a-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="6309a-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6309a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="6309a-133">W polu wyszukiwania hello wpisz **Expensify**.</span><span class="sxs-lookup"><span data-stu-id="6309a-133">In hello search box, type **Expensify**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_search.png)

5. <span data-ttu-id="6309a-135">W panelu wyników hello zaznacz **Expensify**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="6309a-135">In hello results panel, select **Expensify**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6309a-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="6309a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6309a-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Expensify w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="6309a-138">In this section, you configure and test Azure AD single sign-on with Expensify based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6309a-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Expensify jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6309a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Expensify is tooa user in Azure AD.</span></span> <span data-ttu-id="6309a-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Expensify musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="6309a-140">In other words, a link relationship between an Azure AD user and hello related user in Expensify needs toobe established.</span></span>

<span data-ttu-id="6309a-141">W Expensify, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="6309a-141">In Expensify, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6309a-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Expensify, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="6309a-142">tooconfigure and test Azure AD single sign-on with Expensify, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6309a-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="6309a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6309a-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="6309a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6309a-145">**[Tworzenie użytkownika testowego Expensify](#creating-an-expensify-test-user)**  -toohave odpowiednikiem Simona Britta w Expensify, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6309a-145">**[Creating an Expensify test user](#creating-an-expensify-test-user)** - toohave a counterpart of Britta Simon in Expensify that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6309a-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="6309a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6309a-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="6309a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6309a-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="6309a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6309a-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Expensify.</span><span class="sxs-lookup"><span data-stu-id="6309a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Expensify application.</span></span>

<span data-ttu-id="6309a-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Expensify, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="6309a-150">**tooconfigure Azure AD single sign-on with Expensify, perform hello following steps:**</span></span>

1. <span data-ttu-id="6309a-151">W portalu Azure na powitania hello **Expensify** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="6309a-151">In hello Azure portal, on hello **Expensify** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="6309a-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="6309a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_samlbase.png)

3. <span data-ttu-id="6309a-155">Na powitania **Expensify domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="6309a-155">On hello **Expensify Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_url.png)

    <span data-ttu-id="6309a-157">a.</span><span class="sxs-lookup"><span data-stu-id="6309a-157">a.</span></span> <span data-ttu-id="6309a-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://www.expensify.com/authentication/saml/login`</span><span class="sxs-lookup"><span data-stu-id="6309a-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://www.expensify.com/authentication/saml/login`</span></span>

    <span data-ttu-id="6309a-159">b.</span><span class="sxs-lookup"><span data-stu-id="6309a-159">b.</span></span> <span data-ttu-id="6309a-160">W hello **adres URL identyfikatora** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://www.<companyname>.expensify.com/`</span><span class="sxs-lookup"><span data-stu-id="6309a-160">In hello **Identifier URL** textbox, type a URL using hello following pattern: `https://www.<companyname>.expensify.com/`</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="6309a-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="6309a-161">These values are not real.</span></span> <span data-ttu-id="6309a-162">Zaktualizować te wartości hello rzeczywisty adres URL logowania i identyfikator adresu URL.</span><span class="sxs-lookup"><span data-stu-id="6309a-162">Update these values with hello actual Sign-On URL and Identifier URL.</span></span> <span data-ttu-id="6309a-163">Skontaktuj się z [zespołem pomocy technicznej klienta Expensify](mailto:help@expensify.com) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="6309a-163">Contact [Expensify Client support team](mailto:help@expensify.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="6309a-164">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="6309a-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_certificate.png) 

5. <span data-ttu-id="6309a-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6309a-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-expensify-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6309a-168">Logowanie Jednokrotne w Expensify tooenable, należy najpierw tooenable **kontroli domeny** w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="6309a-168">tooenable SSO in Expensify, you first need tooenable **Domain Control** in hello application.</span></span> <span data-ttu-id="6309a-169">Formant domeny można włączyć w aplikacji hello hello kroki wymienione [tutaj](http://help.expensify.com/domain-control).</span><span class="sxs-lookup"><span data-stu-id="6309a-169">You can enable Domain Control in hello application through hello steps listed [here](http://help.expensify.com/domain-control).</span></span> <span data-ttu-id="6309a-170">Aby uzyskać dodatkową pomoc, Praca z [zespołem pomocy technicznej klienta Expensify](mailto:help@expensify.com).</span><span class="sxs-lookup"><span data-stu-id="6309a-170">For additional support, work with [Expensify Client support team](mailto:help@expensify.com).</span></span> <span data-ttu-id="6309a-171">Po utworzeniu włączona funkcja Kontrola domeny, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="6309a-171">Once you have Domain Control enabled, follow these steps:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_51.png)
    
    <span data-ttu-id="6309a-173">a.</span><span class="sxs-lookup"><span data-stu-id="6309a-173">a.</span></span> <span data-ttu-id="6309a-174">Zaloguj się na tooyour Expensify aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6309a-174">Sign on tooyour Expensify application.</span></span>
    
    <span data-ttu-id="6309a-175">b.</span><span class="sxs-lookup"><span data-stu-id="6309a-175">b.</span></span> <span data-ttu-id="6309a-176">Witaj pasku narzędzi u góry hello, kliknij przycisk **Admin**.</span><span class="sxs-lookup"><span data-stu-id="6309a-176">In hello toolbar on hello top, click **Admin**.</span></span>
    
    <span data-ttu-id="6309a-177">c.</span><span class="sxs-lookup"><span data-stu-id="6309a-177">c.</span></span> <span data-ttu-id="6309a-178">W lewym panelu powitania kliknij **domeny**.</span><span class="sxs-lookup"><span data-stu-id="6309a-178">In hello left panel, click **Domain**.</span></span>
    
    <span data-ttu-id="6309a-179">d.</span><span class="sxs-lookup"><span data-stu-id="6309a-179">d.</span></span> <span data-ttu-id="6309a-180">Kliknij nazwę zweryfikowanej domeny.</span><span class="sxs-lookup"><span data-stu-id="6309a-180">Click your verified domain name.</span></span>
    
    <span data-ttu-id="6309a-181">e.</span><span class="sxs-lookup"><span data-stu-id="6309a-181">e.</span></span> <span data-ttu-id="6309a-182">W lewym panelu powitania kliknij **SAML**, a następnie wybierz **włączone**.</span><span class="sxs-lookup"><span data-stu-id="6309a-182">In hello left panel, click **SAML**, and then select **Enabled**.</span></span>
    
    <span data-ttu-id="6309a-183">f.</span><span class="sxs-lookup"><span data-stu-id="6309a-183">f.</span></span> <span data-ttu-id="6309a-184">Otwórz hello pobrane z usługi Azure AD w Notatniku hello kopiowania zawartości, metadanych Federacji, a następnie wklej go do hello **metadanych dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="6309a-184">Open hello downloaded Federation Metadata from Azure AD in notepad, copy hello content, and then paste it into hello **Identity Provider Metadata** textbox.</span></span>

> [!TIP]
> <span data-ttu-id="6309a-185">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="6309a-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6309a-186">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="6309a-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6309a-187">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6309a-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6309a-188">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6309a-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="6309a-189">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="6309a-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="6309a-191">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="6309a-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6309a-192">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="6309a-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-expensify-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6309a-194">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="6309a-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-expensify-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6309a-196">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6309a-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-expensify-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6309a-198">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="6309a-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-expensify-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6309a-200">a.</span><span class="sxs-lookup"><span data-stu-id="6309a-200">a.</span></span> <span data-ttu-id="6309a-201">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6309a-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6309a-202">b.</span><span class="sxs-lookup"><span data-stu-id="6309a-202">b.</span></span> <span data-ttu-id="6309a-203">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6309a-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6309a-204">c.</span><span class="sxs-lookup"><span data-stu-id="6309a-204">c.</span></span> <span data-ttu-id="6309a-205">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="6309a-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6309a-206">d.</span><span class="sxs-lookup"><span data-stu-id="6309a-206">d.</span></span> <span data-ttu-id="6309a-207">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="6309a-207">Click **Create**.</span></span>
 
### <a name="creating-an-expensify-test-user"></a><span data-ttu-id="6309a-208">Tworzenie użytkownika testowego Expensify</span><span class="sxs-lookup"><span data-stu-id="6309a-208">Creating an Expensify test user</span></span>

<span data-ttu-id="6309a-209">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Expensify.</span><span class="sxs-lookup"><span data-stu-id="6309a-209">In this section, you create a user called Britta Simon in Expensify.</span></span> <span data-ttu-id="6309a-210">Praca z [zespołem pomocy technicznej klienta Expensify](mailto:help@expensify.com) tooadd hello użytkowników hello Expensify platformy.</span><span class="sxs-lookup"><span data-stu-id="6309a-210">Work with [Expensify Client support team](mailto:help@expensify.com) tooadd hello users in hello Expensify platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6309a-211">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="6309a-211">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6309a-212">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooExpensify.</span><span class="sxs-lookup"><span data-stu-id="6309a-212">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooExpensify.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="6309a-214">**tooassign tooExpensify Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="6309a-214">**tooassign Britta Simon tooExpensify, perform hello following steps:**</span></span>

1. <span data-ttu-id="6309a-215">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="6309a-215">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="6309a-217">Z listy aplikacji hello wybierz **Expensify**.</span><span class="sxs-lookup"><span data-stu-id="6309a-217">In hello applications list, select **Expensify**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_app.png) 

3. <span data-ttu-id="6309a-219">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="6309a-219">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="6309a-221">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6309a-221">Click **Add** button.</span></span> <span data-ttu-id="6309a-222">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6309a-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="6309a-224">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="6309a-224">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6309a-225">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6309a-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6309a-226">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6309a-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6309a-227">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="6309a-227">Testing single sign-on</span></span>

<span data-ttu-id="6309a-228">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="6309a-228">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>  

<span data-ttu-id="6309a-229">Po kliknięciu kafelka Expensify hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Expensify aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6309a-229">When you click hello Expensify tile in hello Access Panel, you should get automatically signed-on tooyour Expensify application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6309a-230">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="6309a-230">Additional resources</span></span>

* [<span data-ttu-id="6309a-231">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6309a-231">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6309a-232">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6309a-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_203.png

