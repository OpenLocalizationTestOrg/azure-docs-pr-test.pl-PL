---
title: 'Samouczek: Integracji Azure Active Directory z Bime | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Bime."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bdcf0729-c880-4c95-b739-0f6345b17dd8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 1213725028dd8ce90f22fa6e9c50ffabebc8f3fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bime"></a><span data-ttu-id="9c389-103">Samouczek: Integracji Azure Active Directory z Bime</span><span class="sxs-lookup"><span data-stu-id="9c389-103">Tutorial: Azure Active Directory integration with Bime</span></span>

<span data-ttu-id="9c389-104">Z tego samouczka, dowiesz się, jak toointegrate Bime w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9c389-104">In this tutorial, you learn how toointegrate Bime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9c389-105">Integracja z usługą Azure AD Bime zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="9c389-105">Integrating Bime with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9c389-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooBime</span><span class="sxs-lookup"><span data-stu-id="9c389-106">You can control in Azure AD who has access tooBime</span></span>
- <span data-ttu-id="9c389-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooBime (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9c389-107">You can enable your users tooautomatically get signed-on tooBime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9c389-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="9c389-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9c389-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9c389-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9c389-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9c389-110">Prerequisites</span></span>

<span data-ttu-id="9c389-111">tooconfigure integracji z usługą Azure AD z Bime należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="9c389-111">tooconfigure Azure AD integration with Bime, you need hello following items:</span></span>

- <span data-ttu-id="9c389-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9c389-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9c389-113">Bime logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="9c389-113">A Bime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9c389-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="9c389-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9c389-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="9c389-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9c389-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="9c389-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9c389-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna tutaj: [oferta wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9c389-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9c389-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="9c389-118">Scenario description</span></span>
<span data-ttu-id="9c389-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="9c389-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9c389-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="9c389-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9c389-121">Dodawanie Bime z galerii hello</span><span class="sxs-lookup"><span data-stu-id="9c389-121">Adding Bime from hello gallery</span></span>
2. <span data-ttu-id="9c389-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="9c389-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bime-from-hello-gallery"></a><span data-ttu-id="9c389-123">Dodawanie Bime z galerii hello</span><span class="sxs-lookup"><span data-stu-id="9c389-123">Adding Bime from hello gallery</span></span>
<span data-ttu-id="9c389-124">tooconfigure hello integracji Bime do usługi Azure AD, należy tooadd Bime z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="9c389-124">tooconfigure hello integration of Bime into Azure AD, you need tooadd Bime from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9c389-125">**tooadd Bime z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="9c389-125">**tooadd Bime from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9c389-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="9c389-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="9c389-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="9c389-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9c389-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="9c389-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="9c389-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9c389-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="9c389-133">W polu wyszukiwania hello wpisz **Bime**.</span><span class="sxs-lookup"><span data-stu-id="9c389-133">In hello search box, type **Bime**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bime-tutorial/tutorial_bime_search.png)

5. <span data-ttu-id="9c389-135">W panelu wyników hello zaznacz **Bime**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="9c389-135">In hello results panel, select **Bime**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bime-tutorial/tutorial_bime_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9c389-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="9c389-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9c389-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Bime w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="9c389-138">In this section, you configure and test Azure AD single sign-on with Bime based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9c389-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Bime jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9c389-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Bime is tooa user in Azure AD.</span></span> <span data-ttu-id="9c389-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Bime musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="9c389-140">In other words, a link relationship between an Azure AD user and hello related user in Bime needs toobe established.</span></span>

<span data-ttu-id="9c389-141">W Bime, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="9c389-141">In Bime, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9c389-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Bime, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="9c389-142">tooconfigure and test Azure AD single sign-on with Bime, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9c389-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="9c389-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9c389-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="9c389-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9c389-145">**[Tworzenie użytkownika testowego Bime](#creating-a-bime-test-user)**  -toohave odpowiednikiem Simona Britta w Bime, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9c389-145">**[Creating a Bime test user](#creating-a-bime-test-user)** - toohave a counterpart of Britta Simon in Bime that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9c389-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="9c389-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9c389-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="9c389-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9c389-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9c389-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9c389-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Bime.</span><span class="sxs-lookup"><span data-stu-id="9c389-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Bime application.</span></span>

<span data-ttu-id="9c389-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Bime, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="9c389-150">**tooconfigure Azure AD single sign-on with Bime, perform hello following steps:**</span></span>

1. <span data-ttu-id="9c389-151">W portalu Azure na powitania hello **Bime** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="9c389-151">In hello Azure portal, on hello **Bime** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="9c389-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="9c389-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bime-tutorial/tutorial_bime_samlbase.png)

3. <span data-ttu-id="9c389-155">Na powitania **Bime domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="9c389-155">On hello **Bime Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bime-tutorial/tutorial_bime_url.png)

    <span data-ttu-id="9c389-157">a.</span><span class="sxs-lookup"><span data-stu-id="9c389-157">a.</span></span> <span data-ttu-id="9c389-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<tenant-name>.Bimeapp.com`</span><span class="sxs-lookup"><span data-stu-id="9c389-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.Bimeapp.com`</span></span>

    <span data-ttu-id="9c389-159">b.</span><span class="sxs-lookup"><span data-stu-id="9c389-159">b.</span></span> <span data-ttu-id="9c389-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<tenant-name>.Bimeapp.com`</span><span class="sxs-lookup"><span data-stu-id="9c389-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenant-name>.Bimeapp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9c389-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="9c389-161">These values are not real.</span></span> <span data-ttu-id="9c389-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="9c389-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="9c389-163">Skontaktuj się z [zespołem pomocy technicznej klienta Bime](https://bime.zendesk.com/hc/categories/202604307-Support-tech-notes-and-tips-) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="9c389-163">Contact [Bime Client support team](https://bime.zendesk.com/hc/categories/202604307-Support-tech-notes-and-tips-) tooget these values.</span></span> 
 
4. <span data-ttu-id="9c389-164">Na powitania **certyfikat podpisywania SAML** hello kopiowania, sekcji **odcisk PALCA** wartość z zakresu od hello certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="9c389-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value from hello certificate.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bime-tutorial/tutorial_bime_certificate.png) 

5. <span data-ttu-id="9c389-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9c389-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bime-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9c389-168">Na powitania **konfiguracji Bime** kliknij **skonfigurować Bime** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="9c389-168">On hello **Bime Configuration** section, click **Configure Bime** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="9c389-169">Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="9c389-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bime-tutorial/tutorial_bime_configure.png) 

7. <span data-ttu-id="9c389-171">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy Bime jako administrator.</span><span class="sxs-lookup"><span data-stu-id="9c389-171">In a different web browser window, log into your Bime company site as an administrator.</span></span>

8. <span data-ttu-id="9c389-172">Witaj pasku narzędzi, kliknij przycisk **Admin**, a następnie **konta**.</span><span class="sxs-lookup"><span data-stu-id="9c389-172">In hello toolbar, click **Admin**, and then **Account**.</span></span>
   
    <span data-ttu-id="9c389-173">![Administrator](./media/active-directory-saas-bime-tutorial/ic775558.png "administratora")</span><span class="sxs-lookup"><span data-stu-id="9c389-173">![Admin](./media/active-directory-saas-bime-tutorial/ic775558.png "Admin")</span></span>

9. <span data-ttu-id="9c389-174">Strony konfiguracji konta hello wykonywanie hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="9c389-174">On hello account configuration page, perform hello following steps:</span></span>
   
    <span data-ttu-id="9c389-175">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bime-tutorial/ic775559.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="9c389-175">![Configure Single Sign-On](./media/active-directory-saas-bime-tutorial/ic775559.png "Configure Single Sign-On")</span></span>
   
    <span data-ttu-id="9c389-176">a.</span><span class="sxs-lookup"><span data-stu-id="9c389-176">a.</span></span> <span data-ttu-id="9c389-177">Wybierz **uwierzytelnianie Włącz SAML**.</span><span class="sxs-lookup"><span data-stu-id="9c389-177">Select **Enable SAML authentication**.</span></span>

    <span data-ttu-id="9c389-178">b.</span><span class="sxs-lookup"><span data-stu-id="9c389-178">b.</span></span> <span data-ttu-id="9c389-179">W hello **zdalnego adresu URL logowania** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="9c389-179">In hello **Remote Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="9c389-180">c.</span><span class="sxs-lookup"><span data-stu-id="9c389-180">c.</span></span>  <span data-ttu-id="9c389-181">Wklej hello **odcisk palca** wartość z portalu Azure do hello **odcisk palca certyfikatu** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="9c389-181">Paste hello **Thumbprint** value from Azure portal into hello **Certificate Fingerprint** textbox.</span></span>       
   
    <span data-ttu-id="9c389-182">d.</span><span class="sxs-lookup"><span data-stu-id="9c389-182">d.</span></span> <span data-ttu-id="9c389-183">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="9c389-183">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="9c389-184">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="9c389-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9c389-185">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="9c389-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9c389-186">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9c389-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9c389-187">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9c389-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="9c389-188">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="9c389-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="9c389-190">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="9c389-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9c389-191">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="9c389-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9c389-193">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="9c389-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9c389-195">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9c389-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9c389-197">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="9c389-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9c389-199">a.</span><span class="sxs-lookup"><span data-stu-id="9c389-199">a.</span></span> <span data-ttu-id="9c389-200">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9c389-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9c389-201">b.</span><span class="sxs-lookup"><span data-stu-id="9c389-201">b.</span></span> <span data-ttu-id="9c389-202">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9c389-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9c389-203">c.</span><span class="sxs-lookup"><span data-stu-id="9c389-203">c.</span></span> <span data-ttu-id="9c389-204">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="9c389-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9c389-205">d.</span><span class="sxs-lookup"><span data-stu-id="9c389-205">d.</span></span> <span data-ttu-id="9c389-206">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="9c389-206">Click **Create**.</span></span>
 
### <a name="creating-a-bime-test-user"></a><span data-ttu-id="9c389-207">Tworzenie użytkownika testowego Bime</span><span class="sxs-lookup"><span data-stu-id="9c389-207">Creating a Bime test user</span></span>

<span data-ttu-id="9c389-208">W przypadku użytkowników usługi Azure AD toolog kolejności tooenable w tooBime muszą mieć przydzielone do Bime.</span><span class="sxs-lookup"><span data-stu-id="9c389-208">In order tooenable Azure AD users toolog in tooBime, they must be provisioned into Bime.</span></span> <span data-ttu-id="9c389-209">W przypadku hello Bime Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="9c389-209">In hello case of Bime, provisioning is a manual task.</span></span>

<span data-ttu-id="9c389-210">**tooconfigure aprowizacji użytkowników, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="9c389-210">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="9c389-211">Zaloguj się za tooyour **Bime** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="9c389-211">Log in tooyour **Bime** tenant.</span></span>

2. <span data-ttu-id="9c389-212">Witaj pasku narzędzi, kliknij przycisk **Admin**, a następnie **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="9c389-212">In hello toolbar, click **Admin**, and then **Users**.</span></span>
   
    <span data-ttu-id="9c389-213">![Administrator](./media/active-directory-saas-bime-tutorial/ic775561.png "administratora")</span><span class="sxs-lookup"><span data-stu-id="9c389-213">![Admin](./media/active-directory-saas-bime-tutorial/ic775561.png "Admin")</span></span>

3. <span data-ttu-id="9c389-214">W hello **listy użytkowników**, kliknij przycisk **Dodaj nowego użytkownika** ("+").</span><span class="sxs-lookup"><span data-stu-id="9c389-214">In hello **Users List**, click **Add New User** (“+”).</span></span>
   
    <span data-ttu-id="9c389-215">![Użytkownicy](./media/active-directory-saas-bime-tutorial/ic775562.png "użytkowników")</span><span class="sxs-lookup"><span data-stu-id="9c389-215">![Users](./media/active-directory-saas-bime-tutorial/ic775562.png "Users")</span></span>

4. <span data-ttu-id="9c389-216">Na powitania **szczegóły użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="9c389-216">On hello **User Details** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="9c389-217">![Szczegóły użytkownika](./media/active-directory-saas-bime-tutorial/ic775563.png "szczegóły użytkownika")</span><span class="sxs-lookup"><span data-stu-id="9c389-217">![User Details](./media/active-directory-saas-bime-tutorial/ic775563.png "User Details")</span></span>
   
    <span data-ttu-id="9c389-218">a.</span><span class="sxs-lookup"><span data-stu-id="9c389-218">a.</span></span> <span data-ttu-id="9c389-219">W hello **imię** pole tekstowe, wprowadź hello imię użytkownika, takich jak **Britta**.</span><span class="sxs-lookup"><span data-stu-id="9c389-219">In hello **First name** textbox, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="9c389-220">b.</span><span class="sxs-lookup"><span data-stu-id="9c389-220">b.</span></span> <span data-ttu-id="9c389-221">W hello **nazwisko** pole tekstowe, wprowadź hello nazwisko użytkownika, takich jak **Simona**.</span><span class="sxs-lookup"><span data-stu-id="9c389-221">In hello **Last name** textbox, enter hello last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="9c389-222">c.</span><span class="sxs-lookup"><span data-stu-id="9c389-222">c.</span></span> <span data-ttu-id="9c389-223">W hello **E-mail** pole tekstowe, wprowadź adres e-mail użytkownika, takie jak hello  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="9c389-223">In hello **Email** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="9c389-224">d.</span><span class="sxs-lookup"><span data-stu-id="9c389-224">d.</span></span> <span data-ttu-id="9c389-225">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="9c389-225">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="9c389-226">Możesz użyć innych Bime użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Bime tooprovision kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="9c389-226">You can use any other Bime user account creation tools or APIs provided by Bime tooprovision AAD user accounts.</span></span>
>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9c389-227">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="9c389-227">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9c389-228">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooBime.</span><span class="sxs-lookup"><span data-stu-id="9c389-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBime.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="9c389-230">**tooassign tooBime Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="9c389-230">**tooassign Britta Simon tooBime, perform hello following steps:**</span></span>

1. <span data-ttu-id="9c389-231">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="9c389-231">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="9c389-233">Z listy aplikacji hello wybierz **Bime**.</span><span class="sxs-lookup"><span data-stu-id="9c389-233">In hello applications list, select **Bime**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bime-tutorial/tutorial_bime_app.png) 

3. <span data-ttu-id="9c389-235">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="9c389-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="9c389-237">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9c389-237">Click **Add** button.</span></span> <span data-ttu-id="9c389-238">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9c389-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="9c389-240">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="9c389-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9c389-241">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9c389-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9c389-242">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9c389-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9c389-243">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9c389-243">Testing single sign-on</span></span>

<span data-ttu-id="9c389-244">Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="9c389-244">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9c389-245">Po kliknięciu kafelka Bime hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Bime aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9c389-245">When you click hello Bime tile in hello Access Panel, you should get automatically signed-on tooyour Bime application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9c389-246">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="9c389-246">Additional resources</span></span>

* [<span data-ttu-id="9c389-247">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9c389-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9c389-248">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9c389-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bime-tutorial/tutorial_general_203.png

