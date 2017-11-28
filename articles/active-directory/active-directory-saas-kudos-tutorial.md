---
title: 'Samouczek: Integracji Azure Active Directory z Kudos | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Kudos."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 39c47ce6-4944-47ba-8f53-3afa95398034
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: c1b481463574461f9948db2b83843fefa5d74e99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kudos"></a><span data-ttu-id="c6cfa-103">Samouczek: Integracji Azure Active Directory z Kudos</span><span class="sxs-lookup"><span data-stu-id="c6cfa-103">Tutorial: Azure Active Directory integration with Kudos</span></span>

<span data-ttu-id="c6cfa-104">Z tego samouczka, dowiesz się, jak toointegrate Kudos w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c6cfa-104">In this tutorial, you learn how toointegrate Kudos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c6cfa-105">Integracja z usługą Azure AD Kudos zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="c6cfa-105">Integrating Kudos with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c6cfa-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooKudos</span><span class="sxs-lookup"><span data-stu-id="c6cfa-106">You can control in Azure AD who has access tooKudos</span></span>
- <span data-ttu-id="c6cfa-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooKudos (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6cfa-107">You can enable your users tooautomatically get signed-on tooKudos (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c6cfa-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c6cfa-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c6cfa-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c6cfa-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c6cfa-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c6cfa-110">Prerequisites</span></span>

<span data-ttu-id="c6cfa-111">tooconfigure integracji z usługą Azure AD z Kudos należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="c6cfa-111">tooconfigure Azure AD integration with Kudos, you need hello following items:</span></span>

- <span data-ttu-id="c6cfa-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6cfa-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c6cfa-113">Kudos logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="c6cfa-113">A Kudos single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c6cfa-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c6cfa-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="c6cfa-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c6cfa-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c6cfa-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c6cfa-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c6cfa-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="c6cfa-118">Scenario description</span></span>
<span data-ttu-id="c6cfa-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c6cfa-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="c6cfa-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c6cfa-121">Dodawanie Kudos z galerii hello</span><span class="sxs-lookup"><span data-stu-id="c6cfa-121">Adding Kudos from hello gallery</span></span>
2. <span data-ttu-id="c6cfa-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="c6cfa-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kudos-from-hello-gallery"></a><span data-ttu-id="c6cfa-123">Dodawanie Kudos z galerii hello</span><span class="sxs-lookup"><span data-stu-id="c6cfa-123">Adding Kudos from hello gallery</span></span>
<span data-ttu-id="c6cfa-124">tooconfigure hello integracji Kudos do usługi Azure AD, należy tooadd Kudos z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-124">tooconfigure hello integration of Kudos into Azure AD, you need tooadd Kudos from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c6cfa-125">**tooadd Kudos z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="c6cfa-125">**tooadd Kudos from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c6cfa-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="c6cfa-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c6cfa-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="c6cfa-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="c6cfa-133">W polu wyszukiwania hello wpisz **Kudos**.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-133">In hello search box, type **Kudos**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_search.png)

5. <span data-ttu-id="c6cfa-135">W panelu wyników hello zaznacz **Kudos**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-135">In hello results panel, select **Kudos**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c6cfa-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="c6cfa-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c6cfa-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Kudos w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-138">In this section, you configure and test Azure AD single sign-on with Kudos based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c6cfa-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Kudos jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kudos is tooa user in Azure AD.</span></span> <span data-ttu-id="c6cfa-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Kudos musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-140">In other words, a link relationship between an Azure AD user and hello related user in Kudos needs toobe established.</span></span>

<span data-ttu-id="c6cfa-141">W Kudos, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-141">In Kudos, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c6cfa-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Kudos, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="c6cfa-142">tooconfigure and test Azure AD single sign-on with Kudos, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c6cfa-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c6cfa-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c6cfa-145">**[Tworzenie użytkownika testowego Kudos](#creating-a-kudos-test-user)**  -toohave odpowiednikiem Simona Britta w Kudos, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-145">**[Creating a Kudos test user](#creating-a-kudos-test-user)** - toohave a counterpart of Britta Simon in Kudos that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c6cfa-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c6cfa-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c6cfa-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="c6cfa-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c6cfa-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Kudos.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kudos application.</span></span>

<span data-ttu-id="c6cfa-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Kudos, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="c6cfa-150">**tooconfigure Azure AD single sign-on with Kudos, perform hello following steps:**</span></span>

1. <span data-ttu-id="c6cfa-151">W portalu Azure na powitania hello **Kudos** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-151">In hello Azure portal, on hello **Kudos** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="c6cfa-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_samlbase.png)

3. <span data-ttu-id="c6cfa-155">Na powitania **Kudos domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="c6cfa-155">On hello **Kudos Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_url.png)

    <span data-ttu-id="c6cfa-157">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<company>.kudosnow.com`</span><span class="sxs-lookup"><span data-stu-id="c6cfa-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company>.kudosnow.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="c6cfa-158">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-158">This value is not real.</span></span> <span data-ttu-id="c6cfa-159">Zaktualizuj tę wartość z hello rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="c6cfa-160">Skontaktuj się z [zespołem pomocy technicznej klienta Kudos](http://success.kudosnow.com/home) tooget tej wartości.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-160">Contact [Kudos Client support team](http://success.kudosnow.com/home) tooget this value.</span></span> 
 
4. <span data-ttu-id="c6cfa-161">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_certificate.png) 

5. <span data-ttu-id="c6cfa-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kudos-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c6cfa-165">Na powitania **konfiguracji Kudos** kliknij **skonfigurować Kudos** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-165">On hello **Kudos Configuration** section, click **Configure Kudos** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c6cfa-166">Kopiuj hello **Sign-Out adresu URL i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="c6cfa-166">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_configure.png) 

7. <span data-ttu-id="c6cfa-168">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy Kudos jako administrator.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-168">In a different web browser window, log into your Kudos company site as an administrator.</span></span>

8. <span data-ttu-id="c6cfa-169">W menu hello na górze hello, kliknij przycisk **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-169">In hello menu on hello top, click **Settings**.</span></span>
   
    <span data-ttu-id="c6cfa-170">![Ustawienia](./media/active-directory-saas-kudos-tutorial/ic787806.png "ustawienia")</span><span class="sxs-lookup"><span data-stu-id="c6cfa-170">![Settings](./media/active-directory-saas-kudos-tutorial/ic787806.png "Settings")</span></span>

9. <span data-ttu-id="c6cfa-171">Kliknij przycisk **integracji \> logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-171">Click **Integrations \> SSO**.</span></span>

10. <span data-ttu-id="c6cfa-172">W hello **logowania jednokrotnego** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="c6cfa-172">In hello **SSO** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="c6cfa-173">![USŁUGA REJESTRACJI JEDNOKROTNEJ](./media/active-directory-saas-kudos-tutorial/ic787807.png "LOGOWANIA JEDNOKROTNEGO")</span><span class="sxs-lookup"><span data-stu-id="c6cfa-173">![SSO](./media/active-directory-saas-kudos-tutorial/ic787807.png "SSO")</span></span>
   
    <span data-ttu-id="c6cfa-174">a.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-174">a.</span></span> <span data-ttu-id="c6cfa-175">W **Zaloguj się na adres URL** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-175">In **Sign on URL** textbox, paste hello value of  **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="c6cfa-176">b.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-176">b.</span></span> <span data-ttu-id="c6cfa-177">Otwieranie certyfikatu zakodowanego base-64 w Notatniku hello kopiowania zawartości go do Schowka, a następnie wklej go toohello **certyfikatu X.509** pole tekstowe</span><span class="sxs-lookup"><span data-stu-id="c6cfa-177">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **X.509 certificate** textbox</span></span>
   
    <span data-ttu-id="c6cfa-178">c.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-178">c.</span></span> <span data-ttu-id="c6cfa-179">W **tooURL wylogowania**, Wklej wartość hello **Sign-Out URL** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-179">In **Logout tooURL**, paste hello value of  **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="c6cfa-180">d.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-180">d.</span></span> <span data-ttu-id="c6cfa-181">W hello **adres URL Kudos** tekstowym, wpisz nazwę swojej firmy.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-181">In hello **Your Kudos URL** textbox, type your company name.</span></span>
   
    <span data-ttu-id="c6cfa-182">e.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-182">e.</span></span> <span data-ttu-id="c6cfa-183">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-183">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="c6cfa-184">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="c6cfa-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c6cfa-185">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c6cfa-186">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c6cfa-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c6cfa-187">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6cfa-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="c6cfa-188">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="c6cfa-190">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="c6cfa-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c6cfa-191">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kudos-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c6cfa-193">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kudos-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c6cfa-195">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kudos-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c6cfa-197">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="c6cfa-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kudos-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c6cfa-199">a.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-199">a.</span></span> <span data-ttu-id="c6cfa-200">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c6cfa-201">b.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-201">b.</span></span> <span data-ttu-id="c6cfa-202">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c6cfa-203">c.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-203">c.</span></span> <span data-ttu-id="c6cfa-204">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c6cfa-205">d.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-205">d.</span></span> <span data-ttu-id="c6cfa-206">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-206">Click **Create**.</span></span>
 
### <a name="creating-a-kudos-test-user"></a><span data-ttu-id="c6cfa-207">Tworzenie użytkownika testowego Kudos</span><span class="sxs-lookup"><span data-stu-id="c6cfa-207">Creating a Kudos test user</span></span>

<span data-ttu-id="c6cfa-208">W przypadku użytkowników usługi Azure AD toolog kolejności tooenable do Kudos muszą mieć przydzielone do Kudos.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-208">In order tooenable Azure AD users toolog into Kudos, they must be provisioned into Kudos.</span></span> 

<span data-ttu-id="c6cfa-209">W przypadku hello Kudos Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-209">In hello case of Kudos, provisioning is a manual task.</span></span>

<span data-ttu-id="c6cfa-210">**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="c6cfa-210">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="c6cfa-211">Zaloguj się za tooyour **Kudos** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-211">Log in tooyour **Kudos** company site as administrator.</span></span>

2. <span data-ttu-id="c6cfa-212">W menu hello na górze hello, kliknij przycisk **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-212">In hello menu on hello top, click **Settings**.</span></span>
   
   <span data-ttu-id="c6cfa-213">![Ustawienia](./media/active-directory-saas-kudos-tutorial/ic787806.png "ustawienia")</span><span class="sxs-lookup"><span data-stu-id="c6cfa-213">![Settings](./media/active-directory-saas-kudos-tutorial/ic787806.png "Settings")</span></span>

3. <span data-ttu-id="c6cfa-214">Kliknij przycisk **użytkownika administratora**.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-214">Click **User Admin**.</span></span>

4. <span data-ttu-id="c6cfa-215">Kliknij przycisk hello **użytkowników** , a następnie kliknij pozycję **dodać użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-215">Click hello **Users** tab, and then click **Add a User**.</span></span>
   
   <span data-ttu-id="c6cfa-216">![Użytkownik Administrator](./media/active-directory-saas-kudos-tutorial/ic787809.png "użytkownika administratora")</span><span class="sxs-lookup"><span data-stu-id="c6cfa-216">![User Admin](./media/active-directory-saas-kudos-tutorial/ic787809.png "User Admin")</span></span>

5. <span data-ttu-id="c6cfa-217">W hello **dodać użytkownika** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="c6cfa-217">In hello **Add a User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="c6cfa-218">![Dodawanie użytkownika](./media/active-directory-saas-kudos-tutorial/ic787810.png "Dodawanie użytkownika")</span><span class="sxs-lookup"><span data-stu-id="c6cfa-218">![Add a User](./media/active-directory-saas-kudos-tutorial/ic787810.png "Add a User")</span></span>
   
    <span data-ttu-id="c6cfa-219">a.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-219">a.</span></span> <span data-ttu-id="c6cfa-220">Typ hello **imię**, **nazwisko**, **E-mail** i inne szczegóły prawidłowe konto usługi Azure Active Directory mają tooprovision w hello powiązanych pól tekstowych.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-220">Type hello **First Name**, **Last Name**, **Email** and other details of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>
   
    <span data-ttu-id="c6cfa-221">b.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-221">b.</span></span> <span data-ttu-id="c6cfa-222">Kliknij przycisk **Utwórz użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-222">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="c6cfa-223">Możesz użyć innych Kudos użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Kudos tooprovision kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-223">You can use any other Kudos user account creation tools or APIs provided by Kudos tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c6cfa-224">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6cfa-224">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c6cfa-225">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooKudos.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-225">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKudos.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="c6cfa-227">**tooassign tooKudos Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="c6cfa-227">**tooassign Britta Simon tooKudos, perform hello following steps:**</span></span>

1. <span data-ttu-id="c6cfa-228">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-228">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="c6cfa-230">Z listy aplikacji hello wybierz **Kudos**.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-230">In hello applications list, select **Kudos**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_app.png) 

3. <span data-ttu-id="c6cfa-232">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-232">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="c6cfa-234">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-234">Click **Add** button.</span></span> <span data-ttu-id="c6cfa-235">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="c6cfa-237">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-237">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c6cfa-238">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c6cfa-239">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c6cfa-240">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="c6cfa-240">Testing single sign-on</span></span>

<span data-ttu-id="c6cfa-241">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-241">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c6cfa-242">Po kliknięciu kafelka Kudos hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Kudos aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c6cfa-242">When you click hello Kudos tile in hello Access Panel, you should get automatically signed-on tooyour Kudos application.</span></span> <span data-ttu-id="c6cfa-243">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c6cfa-243">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c6cfa-244">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="c6cfa-244">Additional resources</span></span>

* [<span data-ttu-id="c6cfa-245">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c6cfa-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c6cfa-246">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c6cfa-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_203.png

