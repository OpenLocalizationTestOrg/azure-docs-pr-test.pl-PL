---
title: 'Samouczek: Integracji Azure Active Directory z Strona stanu | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Strona stanu."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f6ee8bb3-df43-4c0d-bf84-89f18deac4b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 7c6717017984241e9e459273ead4b5e062311120
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-statuspage"></a><span data-ttu-id="0a93b-103">Samouczek: Integracji Azure Active Directory z Strona stanu</span><span class="sxs-lookup"><span data-stu-id="0a93b-103">Tutorial: Azure Active Directory integration with StatusPage</span></span>

<span data-ttu-id="0a93b-104">Z tego samouczka, dowiesz się, jak toointegrate Strona stanu w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0a93b-104">In this tutorial, you learn how toointegrate StatusPage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0a93b-105">Integracja z usługą Azure AD Strona stanu zawiera hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="0a93b-105">Integrating StatusPage with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0a93b-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooStatusPage</span><span class="sxs-lookup"><span data-stu-id="0a93b-106">You can control in Azure AD who has access tooStatusPage</span></span>
- <span data-ttu-id="0a93b-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooStatusPage (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a93b-107">You can enable your users tooautomatically get signed-on tooStatusPage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0a93b-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="0a93b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0a93b-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0a93b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0a93b-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0a93b-110">Prerequisites</span></span>

<span data-ttu-id="0a93b-111">tooconfigure integracji z usługą Azure AD z Strona stanu, należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="0a93b-111">tooconfigure Azure AD integration with StatusPage, you need hello following items:</span></span>

- <span data-ttu-id="0a93b-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a93b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0a93b-113">Strona stanu logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="0a93b-113">A StatusPage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0a93b-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="0a93b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0a93b-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="0a93b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0a93b-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="0a93b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0a93b-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0a93b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0a93b-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="0a93b-118">Scenario description</span></span>
<span data-ttu-id="0a93b-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="0a93b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0a93b-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="0a93b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0a93b-121">Strona Dodawanie stanu z galerii hello</span><span class="sxs-lookup"><span data-stu-id="0a93b-121">Adding StatusPage from hello gallery</span></span>
2. <span data-ttu-id="0a93b-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="0a93b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-statuspage-from-hello-gallery"></a><span data-ttu-id="0a93b-123">Strona Dodawanie stanu z galerii hello</span><span class="sxs-lookup"><span data-stu-id="0a93b-123">Adding StatusPage from hello gallery</span></span>
<span data-ttu-id="0a93b-124">tooconfigure hello integracji Strona stanu do usługi Azure AD, należy tooadd Strona stanu z listy tooyour galerii hello zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="0a93b-124">tooconfigure hello integration of StatusPage into Azure AD, you need tooadd StatusPage from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0a93b-125">**tooadd Strona stanu z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="0a93b-125">**tooadd StatusPage from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0a93b-126">W hello ** [portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="0a93b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="0a93b-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="0a93b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0a93b-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="0a93b-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="0a93b-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0a93b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="0a93b-133">W polu wyszukiwania hello wpisz **Strona stanu**.</span><span class="sxs-lookup"><span data-stu-id="0a93b-133">In hello search box, type **StatusPage**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_search.png)

5. <span data-ttu-id="0a93b-135">W panelu wyników hello zaznacz **Strona stanu**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="0a93b-135">In hello results panel, select **StatusPage**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0a93b-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="0a93b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0a93b-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Strona stanu w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="0a93b-138">In this section, you configure and test Azure AD single sign-on with StatusPage based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0a93b-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Strona stanu jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0a93b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in StatusPage is tooa user in Azure AD.</span></span> <span data-ttu-id="0a93b-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Strona stanu musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="0a93b-140">In other words, a link relationship between an Azure AD user and hello related user in StatusPage needs toobe established.</span></span>

<span data-ttu-id="0a93b-141">Strona stanu, przypisywanie wartości hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="0a93b-141">In StatusPage, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0a93b-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Strona stanu, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="0a93b-142">tooconfigure and test Azure AD single sign-on with StatusPage, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0a93b-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on) ** -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="0a93b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0a93b-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user) ** -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="0a93b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0a93b-145">**[Tworzenie użytkownika testowego Strona stanu](#creating-a-statuspage-test-user) ** -toohave odpowiednikiem Simona Britta w Strona stanu, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0a93b-145">**[Creating a StatusPage test user](#creating-a-statuspage-test-user)** - toohave a counterpart of Britta Simon in StatusPage that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0a93b-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="0a93b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0a93b-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on) ** -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="0a93b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0a93b-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="0a93b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0a93b-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w aplikacji strona stanu.</span><span class="sxs-lookup"><span data-stu-id="0a93b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your StatusPage application.</span></span>

<span data-ttu-id="0a93b-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Strona stanu, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="0a93b-150">**tooconfigure Azure AD single sign-on with StatusPage, perform hello following steps:**</span></span>

1. <span data-ttu-id="0a93b-151">W portalu Azure na powitania hello **Strona stanu** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="0a93b-151">In hello Azure portal, on hello **StatusPage** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="0a93b-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="0a93b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_samlbase.png)

3. <span data-ttu-id="0a93b-155">Na powitania **domeny Strona stanu i adresów URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="0a93b-155">On hello **StatusPage Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_url.png)

    <span data-ttu-id="0a93b-157">a.</span><span class="sxs-lookup"><span data-stu-id="0a93b-157">a.</span></span> <span data-ttu-id="0a93b-158">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="0a93b-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<subdomain>.statuspagestaging.com/` |
    | `https://<subdomain>.statuspage.io/` |

    <span data-ttu-id="0a93b-159">b.</span><span class="sxs-lookup"><span data-stu-id="0a93b-159">b.</span></span> <span data-ttu-id="0a93b-160">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="0a93b-160">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span> 
    | |
    |--|
    | `https://<subdomain>.statuspagestaging.com/sso/saml/consume` |
    | `https://<subdomain>.statuspage.io/sso/saml/consume` |

    > [!NOTE]
    > <span data-ttu-id="0a93b-161">Skontaktuj się z zespołem pomocy technicznej Strona stanu hello na [ SupportTeam@statuspage.io ](mailto:SupportTeam@statuspage.io)toorequest metadanych tooconfigure potrzeby logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="0a93b-161">Contact hello StatusPage support team at [SupportTeam@statuspage.io](mailto:SupportTeam@statuspage.io)toorequest metadata necessary tooconfigure single sign-on.</span></span> 
    >
    ><span data-ttu-id="0a93b-162">a.</span><span class="sxs-lookup"><span data-stu-id="0a93b-162">a.</span></span> <span data-ttu-id="0a93b-163">Z metadanych hello Kopiuj Witaj wystawca wartość, a następnie wklej go do hello **identyfikator** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="0a93b-163">From hello metadata, copy hello Issuer value, and then paste it into hello **Identifier** textbox.</span></span>
    >
    ><span data-ttu-id="0a93b-164">b.</span><span class="sxs-lookup"><span data-stu-id="0a93b-164">b.</span></span> <span data-ttu-id="0a93b-165">Z metadanych hello, skopiuj adres URL odpowiedzi hello, a następnie wklej go do hello **adres URL odpowiedzi** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="0a93b-165">From hello metadata, copy hello Reply URL, and then paste it into hello **Reply URL** textbox.</span></span>

4. <span data-ttu-id="0a93b-166">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="0a93b-166">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_certificate.png) 

5. <span data-ttu-id="0a93b-168">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0a93b-168">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-statuspage-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0a93b-170">Na powitania **Strona stanu konfiguracji** kliknij **strona Konfigurowanie stanu** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="0a93b-170">On hello **StatusPage Configuration** section, click **Configure StatusPage** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0a93b-171">Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="0a93b-171">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_configure.png) 

7. <span data-ttu-id="0a93b-173">W innym oknie przeglądarki Zaloguj się w witrynie firmy Strona stanu tooyour jako administrator.</span><span class="sxs-lookup"><span data-stu-id="0a93b-173">In another browser window, sign on tooyour StatusPage company site as an administrator.</span></span>

8. <span data-ttu-id="0a93b-174">Witaj głównym pasku narzędzi, kliknij przycisk **Zarządzaj kontem**.</span><span class="sxs-lookup"><span data-stu-id="0a93b-174">In hello main toolbar, click **Manage Account**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_06.png) 

10. <span data-ttu-id="0a93b-176">Kliknij przycisk hello **rejestracji jednokrotnej** kartę.</span><span class="sxs-lookup"><span data-stu-id="0a93b-176">Click hello **Single Sign-on** tab.</span></span> 
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_07.png) 

11. <span data-ttu-id="0a93b-178">Na stronie Ustawienia logowania jednokrotnego hello wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="0a93b-178">On hello SSO Setup page, perform hello following steps:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_08.png) 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_09.png) 
 
    <span data-ttu-id="0a93b-181">a.</span><span class="sxs-lookup"><span data-stu-id="0a93b-181">a.</span></span> <span data-ttu-id="0a93b-182">W hello **logowania jednokrotnego, docelowy adres URL** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0a93b-182">In hello **SSO Target URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="0a93b-183">b.</span><span class="sxs-lookup"><span data-stu-id="0a93b-183">b.</span></span> <span data-ttu-id="0a93b-184">Otwórz pobrany certyfikat w Notatniku, hello kopiowania zawartości, a następnie wklej go do hello **certyfikatu** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="0a93b-184">Open your downloaded certificate in Notepad, copy hello content, and then paste it into hello **Certificate** textbox.</span></span> 

    <span data-ttu-id="0a93b-185">c.</span><span class="sxs-lookup"><span data-stu-id="0a93b-185">c.</span></span> <span data-ttu-id="0a93b-186">Kliknij przycisk **Zapisywanie konfiguracji**.</span><span class="sxs-lookup"><span data-stu-id="0a93b-186">Click **SAVE CONFIGURATION**.</span></span>

> [!TIP]
> <span data-ttu-id="0a93b-187">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="0a93b-187">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0a93b-188">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello ** Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="0a93b-188">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0a93b-189">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0a93b-189">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0a93b-190">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a93b-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="0a93b-191">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="0a93b-191">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="0a93b-193">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="0a93b-193">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0a93b-194">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="0a93b-194">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-statuspage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0a93b-196">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="0a93b-196">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-statuspage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0a93b-198">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0a93b-198">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-statuspage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0a93b-200">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="0a93b-200">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-statuspage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0a93b-202">a.</span><span class="sxs-lookup"><span data-stu-id="0a93b-202">a.</span></span> <span data-ttu-id="0a93b-203">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0a93b-203">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0a93b-204">b.</span><span class="sxs-lookup"><span data-stu-id="0a93b-204">b.</span></span> <span data-ttu-id="0a93b-205">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0a93b-205">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0a93b-206">c.</span><span class="sxs-lookup"><span data-stu-id="0a93b-206">c.</span></span> <span data-ttu-id="0a93b-207">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="0a93b-207">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0a93b-208">d.</span><span class="sxs-lookup"><span data-stu-id="0a93b-208">d.</span></span> <span data-ttu-id="0a93b-209">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="0a93b-209">Click **Create**.</span></span>
 
### <a name="creating-a-statuspage-test-user"></a><span data-ttu-id="0a93b-210">Tworzenie użytkownika testowego Strona stanu</span><span class="sxs-lookup"><span data-stu-id="0a93b-210">Creating a StatusPage test user</span></span>

<span data-ttu-id="0a93b-211">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w Strona stanu.</span><span class="sxs-lookup"><span data-stu-id="0a93b-211">hello objective of this section is toocreate a user called Britta Simon in StatusPage.</span></span>

<span data-ttu-id="0a93b-212">Strona stanu obsługę w czasie.</span><span class="sxs-lookup"><span data-stu-id="0a93b-212">StatusPage supports just-in-time provisioning.</span></span> <span data-ttu-id="0a93b-213">Została już włączona w [Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="0a93b-213">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

<span data-ttu-id="0a93b-214">**toocreate użytkownika o nazwie Simona Britta w Strona stanu, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="0a93b-214">**toocreate a user called Britta Simon in StatusPage, perform hello following steps:**</span></span>

1. <span data-ttu-id="0a93b-215">Logowania jednokrotnego tooyour Strona stanu witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="0a93b-215">Sign-on tooyour StatusPage company site as an administrator.</span></span>

2. <span data-ttu-id="0a93b-216">W menu hello na górze hello, kliknij przycisk **Zarządzaj kontem**.</span><span class="sxs-lookup"><span data-stu-id="0a93b-216">In hello menu on hello top, click **Manage Account**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_06.png)

3. <span data-ttu-id="0a93b-218">Kliknij przycisk hello **członków zespołu** kartę.</span><span class="sxs-lookup"><span data-stu-id="0a93b-218">Click hello **Team Members** tab.</span></span> 
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_10.png) 

4. <span data-ttu-id="0a93b-220">Kliknij przycisk **członek zespołu Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="0a93b-220">Click **ADD TEAM MEMBER**.</span></span> 
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_11.png) 

5. <span data-ttu-id="0a93b-222">Typ hello **adres E-mail**, **imię**, i **nazwisko** z prawidłowym użytkownikiem tooprovision do umieszczenia hello związane z pól tekstowych.</span><span class="sxs-lookup"><span data-stu-id="0a93b-222">Type hello **Email Address**, **First Name**, and **Sur Name** of a valid user you want tooprovision into hello related textboxes.</span></span> 
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_12.png) 

6. <span data-ttu-id="0a93b-224">Jako **roli**, wybierz **Administrator klienta**.</span><span class="sxs-lookup"><span data-stu-id="0a93b-224">As **Role**, choose **Client Administrator**.</span></span>

7. <span data-ttu-id="0a93b-225">Kliknij przycisk **Utwórz konto**.</span><span class="sxs-lookup"><span data-stu-id="0a93b-225">Click **CREATE ACCOUNT**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0a93b-226">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a93b-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0a93b-227">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooStatusPage.</span><span class="sxs-lookup"><span data-stu-id="0a93b-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooStatusPage.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="0a93b-229">**tooassign tooStatusPage Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="0a93b-229">**tooassign Britta Simon tooStatusPage, perform hello following steps:**</span></span>

1. <span data-ttu-id="0a93b-230">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="0a93b-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="0a93b-232">Z listy aplikacji hello wybierz **Strona stanu**.</span><span class="sxs-lookup"><span data-stu-id="0a93b-232">In hello applications list, select **StatusPage**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_app.png) 

3. <span data-ttu-id="0a93b-234">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="0a93b-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="0a93b-236">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0a93b-236">Click **Add** button.</span></span> <span data-ttu-id="0a93b-237">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0a93b-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="0a93b-239">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="0a93b-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0a93b-240">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0a93b-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0a93b-241">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0a93b-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0a93b-242">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="0a93b-242">Testing single sign-on</span></span>

<span data-ttu-id="0a93b-243">Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="0a93b-243">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0a93b-244">Po kliknięciu kafelka Strona stanu hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Strona stanu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0a93b-244">When you click hello StatusPage tile in hello Access Panel, you should get automatically signed-on tooyour StatusPage application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0a93b-245">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="0a93b-245">Additional resources</span></span>

* [<span data-ttu-id="0a93b-246">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0a93b-246">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0a93b-247">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0a93b-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_203.png

